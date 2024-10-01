# Local GitLab Runner Documentation for CI/CD

GitLab offers 400 free minutes per month for GitLab Runner usage. To avoid unnecessary costs and gain more flexibility in configuring your CI/CD pipeline, you can set up a local GitLab Runner on your own machine.

## Requirements

Make sure you have the following installed on your local machine:

- Docker

## Installing GitLab Runner on macOS

For the full documentation, you can refer to the official [GitLab Runner Install Guide](https://docs.gitlab.com/runner/install/).

### Steps to Install GitLab Runner:

1. **Download the binary for your system:**

    - For Intel-based systems:
      ```bash
      sudo curl --output /usr/local/bin/gitlab-runner "https://s3.dualstack.us-east-1.amazonaws.com/gitlab-runner-downloads/latest/binaries/gitlab-runner-darwin-amd64"
      ```

    - For Apple Silicon-based systems:
      ```bash
      sudo curl --output /usr/local/bin/gitlab-runner "https://s3.dualstack.us-east-1.amazonaws.com/gitlab-runner-downloads/latest/binaries/gitlab-runner-darwin-arm64"
      ```

2. **Give execution permissions to GitLab Runner:**
   ```bash
   sudo chmod +x /usr/local/bin/gitlab-runner
   ```

Once these steps are completed, GitLab Runner will be installed on your machine.

---

## Registering GitLab Runner on Local macOS

1. **Start the registration process:**
   ```bash
   gitlab-runner register
   ```

2. **Enter the GitLab instance URL:**

    - In the prompt for the runner registration URL, enter the following:
      ```
      https://gitlab.com/
      ```

3. **Obtain your GitLab CI token:**

    - Navigate to your GitLab project:
        - Go to `Settings -> CI/CD -> Runners` (click "Expand").
        - Under the **Project Runners** section, click the three vertical dots next to **New project runner**.
        - A popup window will appear showing the **Registration Token**. Copy it.

    - Paste the copied token in the registration prompt for the GitLab CI token.

4. **Fill in a description, name, and tags:**

    - Enter any desired information for the name, description, and tags for your runner.

5. **Select the executor:**

    - For the runner environment, choose `docker` and hit Enter.

6. **Select the Docker image:**

    - The recommended default image will likely be `ruby`. It's a good idea to use this recommended image.

7. **Finish registration:**

    - Once these steps are completed, you should see a confirmation message that the GitLab Runner was registered successfully.

---

## Setting Up GitLab Runner

1. **Install the runner as a service:**

    - To link the registered runner with your local device, run:
      ```bash
      gitlab-runner install
      ```

2. **Start GitLab Runner:**

    - Before starting, ensure that Docker is installed and running on your machine.
    - GitLab Runner will automatically allocate a container for itself when Docker is active.
      ```bash
      gitlab-runner start
      ```

Now your local GitLab Runner is up and running!

--- 

By following these steps, you can effectively use a local GitLab Runner, avoiding the usage of the free minutes provided by GitLab and giving you more control over your CI/CD pipeline setup.


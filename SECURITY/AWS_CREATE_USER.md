# Instructions for Granting Access to Another User in AWS

## Step 1: Sign in to the AWS Console

1. Open a web browser and go to the [AWS Management Console](https://aws.amazon.com/console/).
2. Enter your login credentials (username and password).
3. If you have two-factor authentication enabled, follow the instructions to complete the sign-in.

## Step 2: Navigate to IAM

1. On the main AWS console page, find and select **Services** in the top menu.
2. In the **Security, Identity, & Compliance** section, select **IAM** (Identity and Access Management).

## Step 3: Create a New User or Select an Existing One

### Creating a New User:

1. In the left panel, select **Users**.
2. Click the **Add user** button.
3. Enter a username in the **User name** field.
4. Select access type:
   - Check both **Programmatic access** (for API and CLI) and **AWS Management Console access** (for console access).
5. Click **Next: Permissions**.

### Selecting an Existing User:

1. In the left panel, select **Users**.
2. Find and click on the name of the user you want to grant access to.

## Step 4: Assign Permissions

You can choose to grant either full access or specific permissions.

### Granting Full Access:

1. **When creating a new user**:
   - On the **Set permissions** page, select **Attach existing policies directly**.
   - In the search box, type `AdministratorAccess`.
   - Check the box next to the **AdministratorAccess** policy.

2. **When editing an existing user**:
   - Navigate to the **Permissions** tab.
   - Click the **Add permissions** button.
   - Select **Attach policies directly**.
   - In the search box, type `AdministratorAccess`.
   - Check the box next to the **AdministratorAccess** policy.
   - Click **Next: Review**.

### Granting Specific Permissions:

1. **When creating a new user**:
   - On the **Set permissions** page, select **Attach existing policies directly**.
   - Search for specific policies that you want to assign (e.g., `AmazonS3FullAccess`, `AmazonEC2ReadOnlyAccess`).
   - Check the boxes next to the desired policies.

2. **When editing an existing user**:
   - Navigate to the **Permissions** tab.
   - Click the **Add permissions** button.
   - Select **Attach policies directly**.
   - Search for and select the specific policies you want to assign.
   - Click **Next: Review**.

## Step 5: Complete the Process

1. If you created a new user, on the confirmation page, click the **Create user** button.
2. If you are editing an existing user, click the **Add permissions** button.

## Step 6: Provide Access to the User

1. If you created a new user, you will receive access to their username and temporary password. Save this information.
2. Inform the new user of their username and temporary password.
3. If you enabled multi-factor authentication (MFA), provide instructions for setting it up.

## Additional Recommendations

- **Verify Permissions**: Ask the new user to sign in to their account and ensure they have access to all necessary resources.
- **Monitor Actions**: Consider using AWS CloudTrail to monitor the actions of the user with full or specific access.

By following these instructions, you will be able to grant either full access or selected permissions to another user in AWS.
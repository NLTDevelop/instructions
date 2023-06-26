## SSH

Create ssh key pair

```bash
ssh-keygen -t rsa -b 4096 -C "
```

Add ssh key to ssh-agent

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

Copy ssh key to clipboard

```bash
pbcopy < ~/.ssh/id_rsa.pub
```

Open ssh folder

```bash
open ~/.ssh
```

Show public key

```bash
cat ~/.ssh/id_rsa.pub
```
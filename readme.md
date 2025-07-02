# WSL Development Environment Setup

## Prerequisites

- Windows 10/11 with WSL2 installed
- Docker Desktop for Windows
- SSH key configured with your Git provider (GitLab in our case)

## Install and Configure WSL

In Windows PowerShell as Administrator:

```
wsl --install -d Ubuntu
```

After Installation, create Username and Password when prompted (Don't skip through otherwise when running you will work in root instead of your user)

Set Ubuntu as the default distribution:

```
wsl --set-default Ubuntu
Ubuntu config --default-user your-username
```

### Troubleshooting

If you get root@... instead of your username, set default user:

1. ubuntu config --default-user your-actual-username
2. wsl shutdown
3. wsl

## Generate SSH Keys (If you don't have them)

For detailed SSH key setup instructions, see the [GitLab SSH documentation](https://gitlab.wa.spectranetix.com/help/user/ssh.md).

Generate new SSH key pair:

```
ssh-keygen -t rsa -b 4096 -C "your.email@Pacific-Defense.com"
```

When prompted:
- Press Enter to save to default location :: /home/username/.ssh/id_rsa
- Enter a passphrase (I just skipped this and left it blank)
- Confirm passphrase (Again, I just left this blank and pressed enter)

Display your Public Key:

```
cat ~/.ssh/id_rsa.pub
```

## Add SSH Key to Gitlab

For complete instructions, see the [GitLab SSH documentation](https://gitlab.wa.spectranetix.com/help/user/ssh.md).

1. Copy the entire output from cat ~/.ssh/id_rsa.pub
2. Go to GitLab in your browser
3. Click your profile picture --> Edit Profile
4. Go to SSH Keys in the left sidebar
5. Paste your public key in the "Key" field
6. Give it a title (I named mine, "MYCOMPUTER")
7. Click "Add Key"

## Configure SSH Agent and Test Connection

In Ubuntu Terminal Start ssh agent and add key

```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

Then test your gitlabs connection

```
ssh -T git@gitlab.wa.spectranetix.com
```

If it worked properly you should see "Welcome to GitLab, Username!"

### Troubleshooting

**Host Key verifaction failed problem:**

You have to accept the host key when prompted or add it as a known host:

```
ssh-keyscan gitlab.wa.spectranetix.com >> ~/.ssh/known_hosts
```

**Permission denied problem:**

1. Double check that you copied the ENTIRE public key (including ssh-rsa and email)
2. Verify the key was added to Gitlab correctly
3. Make sure you are using the right GitLab domain

## Alternative Steps

Let's assume you already went through the ssh key and git clone steps on your C drive. You want to mount everything to home in wsl, and this is how you can do that:

All of the following steps will be done in your Ubuntu terminal then you can do "code ." to start accessing the specific code files in VSCode.

If you already have SSH keys on Windows:

```
mkdir -p ~/.ssh
```

Copy from windows:

```
cp /mnt/c/Users/User.Name/.ssh/id_rsa ~/.ssh/
cp /mnt/c/Users/User.Name/.ssh/id_rsa.pub ~/.ssh/
```

set correct permissions:

```
chmod 600 ~/.ssh/id_rsa
chmod 644 ~/.ssh/id_rsa.pub
```

add to SSH agent

```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

test connection

```
ssh -T git@gitlab.wa.spectranetix.com
```

After these go ahead and continue from step 5 onwards.

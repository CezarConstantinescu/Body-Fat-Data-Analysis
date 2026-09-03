# Working with Git

A brief guide to Git workflow for creating branches, committing changes, pushing, and creating merge requests on GitLab.

## Installing Git

**macOS:**
```bash
brew install git
```
Or download the installer from [https://git-scm.com/download/mac](https://git-scm.com/download/mac).

**Windows:**
Download and run the installer from [https://git-scm.com/download/win](https://git-scm.com/download/win). During installation, keep the default options.

**Linux:**
```bash
sudo apt install git   # Debian/Ubuntu
sudo dnf install git   # Fedora
```

Verify the installation:
```bash
git --version
```

---

## Setting Up SSH Keys for GitLab

Before you can push to GitLab, you need to set up SSH authentication. This allows GitLab to verify your identity without requiring a password each time.

### 1. Generate an SSH Key Pair

The `.ssh` folder lives inside your **home directory**:

- **macOS/Linux**: `/Users/your-username/.ssh` (macOS) or `/home/your-username/.ssh` (Linux) — shorthand: `~/.ssh`
- **Windows**: `C:\Users\your-username\.ssh`

This folder may already exist. If it doesn't, create it:

**On macOS/Linux or Windows (Git Bash):**
```bash
mkdir -p ~/.ssh
```

**On Windows (Command Prompt or PowerShell):**
```powershell
mkdir $env:USERPROFILE\.ssh
```

Then generate the key (works on all platforms):
```bash
ssh-keygen -t ed25519
```

When prompted for the file location, press Enter to accept the default — this saves the key inside your `.ssh` folder automatically. You do not need to navigate into the folder first.

```bash
ssh-keygen -t ed25519
```

**What is `-t ed25519`?**
- The `-t` flag specifies the **type** of cryptographic algorithm to use for the key
- `ed25519` is a modern, secure, and efficient public-key signature algorithm
- It's faster and produces smaller keys than the older RSA algorithm
- Ed25519 keys are 256 bits and are considered very secure
- If your system doesn't support ed25519 (rare on modern systems), you can use `-t rsa -b 4096` instead

The SSH key will be created in the current `.ssh` directory:
- **macOS/Linux**: `~/.ssh/` (e.g., `/Users/username/.ssh/` or `/home/username/.ssh/`)
- **Windows**: `C:\Users\username\.ssh\` (when using Git Bash, this is `~/.ssh/`)

You'll be prompted to:
- **Enter a file location**: Press Enter to use the default location (`id_ed25519` - it will be saved in the current `.ssh` folder)
- **Enter a passphrase**: You can press Enter for no passphrase, or enter a secure passphrase for extra security

### 2. Copy Your Public Key

After generating the key, copy your public key to the clipboard:

**On macOS:**
```bash
pbcopy < ~/.ssh/id_ed25519.pub
```

**On Linux:**
```bash
cat ~/.ssh/id_ed25519.pub
```
Then manually copy the output.

**On Windows (Git Bash):**
```bash
cat ~/.ssh/id_ed25519.pub | clip
```

The public key will look something like:
```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIG... user@hostname
```

### 3. Add Your Public Key to GitLab

1. Log in to your GitLab account
2. Click on your profile picture (top right) → **Preferences** (or go to https://gitlab.com/-/profile/preferences)
3. In the left sidebar, click **SSH Keys**
4. In the **Key** field, paste your public key
5. Give it a descriptive **Title** (e.g., "My Laptop" or "MacBook Pro")
6. Optionally set an expiration date
7. Click **Add key**

### 4. Test Your SSH Connection

Verify that your SSH key is working:

```bash
ssh -T git@gitlab.com
```

You should see a message like:
```
Welcome to GitLab, @username!
```

If you see a permission denied error, make sure you've added the correct public key to GitLab.

### 5. Configure Git to Use SSH

When cloning repositories, use the SSH URL instead of HTTPS:

```bash
git clone git@gitlab.com:username/repository-name.git
```

If you've already cloned using HTTPS, you can change the remote URL:

```bash
git remote set-url origin git@gitlab.com:username/repository-name.git
```

---

## Basic Workflow

### 1. Pull the Latest Changes

Before creating a new branch, make sure you have the latest version of `main`:
```bash
git checkout main
git pull origin main
```

### 2. Create a Branch

Create and switch to a new branch:
```bash
git checkout -b feature/your-feature-name
```

Or using the newer syntax:
```bash
git switch -c feature/your-feature-name
```

**Best practices:**
- Use descriptive branch names (e.g., `feature/add-login`, `fix/bug-in-calculation`)
- Prefix with `feature/`, `fix/`, `docs/`, etc. to indicate the type of change
- In our classes, the branch name will follow this standard: `feature/SIA-1101-1`, `feature/SDBIS-1101-1`. The `SIA-1101-1` part will be taken from task title.


### 3. Make Your Changes

Edit files, add new files, or delete files as needed.

### 4. Stage Changes

Add specific files:
```bash
git add filename.R
git add another-file.md
```

Or add all changes:
```bash
git add .
```

Check what will be committed:
```bash
git status
```

### 5. Commit Changes

Commit your staged changes with a descriptive message:
```bash
git commit -m "Add correlation analysis section to EDA notebook"
```

**Commit message best practices:**
- Use clear, descriptive messages
- Start with a verb (Add, Fix, Update, Remove, etc.)
- Keep the first line under 50 characters if possible
- Add more details in the body if needed (use `git commit` without `-m` for a multi-line message)

### 6. Push to Origin

Push your branch to the remote repository:
```bash
git push origin feature/your-feature-name
```

If this is the first push for this branch, set the upstream:
```bash
git push -u origin feature/your-feature-name
```

After setting upstream once, you can use:
```bash
git push
```

### 7. Create a Merge Request on GitLab

1. After pushing, GitLab will show a notification with a link to create a merge request
2. Click "Create merge request" or go to your project on GitLab
3. Navigate to **Merge Requests** → **New merge request**
4. Select your branch as the source branch
5. Select the target branch (usually `main` or `master`)
6. Fill in:
   - **Title**: Clear description of your changes
   - **Description**: Detailed explanation of what was changed and why
7. Assign reviewers if needed
8. Click **Create merge request**


## Complete Example

```bash
# 1. Pull latest changes
git checkout main
git pull origin main

# 2. Create and switch to new branch
git checkout -b feature/add-new-plot

# 3. Make changes (edit files, etc.)

# 4. Stage changes
git add 1_ggplot2/ggplot2_introduction.qmd

# 5. Commit
git commit -m "Add new plot section to ggplot2 introduction"

# 6. Push to origin
git push -u origin feature/add-new-plot

# 7. Create merge request on GitLab web interface
```

## Useful Commands

- `git status` - Check the status of your working directory
- `git log` - View commit history
- `git diff` - See changes before staging
- `git diff --staged` - See staged changes
- `git branch` - List all branches
- `git branch -d branch-name` - Delete a local branch (after merging)

## Tips

- **Pull before you push**: Always pull the latest changes before pushing:
  ```bash
  git pull origin main
  ```
- **Small, focused commits**: Make commits that represent logical units of work
- **Write good commit messages**: Future you (and your team) will thank you
- **Review before pushing**: Use `git status` and `git diff` to review your changes


# GIT and PyTorch for Apple Silicon - M3

This repository is your one-stop destination, offering a beginner friendly guide to setting up Git and PyTorch for Apple Silicon (M3) Macs. As Apple's ARM-based Macs gain popularity, ensuring PyTorch's peak performance on this platform becomes paramount. Whether you're a seasoned developer or a newcomer, this repository is your gateway to unleashing the full potential of PyTorch while mastering the fundamental setup of Git.

# Git Setup

## Getting Started with Git and VSCode on macOS

Welcome to a beginner-friendly guide on setting up Git and Visual Studio Code (VSCode) on your macOS machine! Whether you're new to programming or just starting with Git and code editors, we'll walk you through the steps to get you up and running smoothly.

## Prerequisites

Before we begin, make sure you have a macOS machine ready. Let's dive in!

### Step 1: Install Homebrew

Homebrew is a package manager for macOS that makes installing and managing software packages a breeze.

Open your Terminal and paste the following command:

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

Once installed, run the following 2 commands as prompted. These 2 commands add brew to the path and allow to run brew commands to install packages
```shell
* (echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> /Users/akhil/.zprofile
* eval "$(/opt/homebrew/bin/brew shellenv)"
```

In the terminal now enter: `brew help` to check if brew was added to the path.

### Step 2: Install VsCode

Visit the website: https://code.visualstudio.com/download to install VsCode

### Step 3: Install Git

Open your terminal and exectue the following command

```shell
brew install git
```
### Step 4: Configure Git Details

The `git config` commands are used to set your Git configuration, including your username and email. The example commands you provided:

```shell
git config --global user.name “Akhil Pusapati”
git config --global user.email Pusapati.akhil@gmail.com
```

Set your global Git username to "Akhil Pusapati" and your global Git email to "Pusapati.akhil@gmail.com." These values are used to identify you as the author of your Git commits.

Here's why you would want to configure Git with your name and email:

1. **Authorship**: When you make commits in a Git repository, it's essential to associate them with an author. Setting your name and email ensures that Git knows who authored each commit.

2. **Communication**: Your email is used for communication related to your Git activity, such as receiving notifications about pull requests, issues, or other collaboration efforts on platforms like GitHub.

3. **Accountability**: It helps others identify you as the contributor to a particular code change, making it easier for collaboration and code review.

4. **Commit History**: When you contribute to open-source projects or collaborate with others, having the correct name and email in your Git configuration ensures that your contributions are accurately recorded in the commit history.

In summary, configuring your Git username and email is a fundamental step in setting up your identity within the Git version control system, allowing for proper tracking of your contributions and communication related to your Git activity.

Certainly! Here's the content you provided in a simplified format within a `readme.md` file:

### Step 5: Generate and Setup SSH Keys for GitHub

Follow these steps to set up SSH keys for GitHub:

1. Visit [GitHub's SSH key documentation](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) for detailed instructions. You can access and write data in repositories on GitHub.com using SSH (Secure Shell Protocol). When you set up SSH, you will need to generate a new private SSH key and add it to the SSH agent. You must also add the public SSH key to your account on GitHub before you use the key to authenticate or sign commits. <br/>
**The steps below will provide a simple explanation for the same:**

#### 1. Generate SSH Keys for GitHub

To securely access and write data in GitHub repositories using SSH, follow these steps:

1. Visit [GitHub's SSH key documentation](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) for detailed instructions.

2. **Generate a New SSH Key**: You will create a new SSH key pair. The private key stays on your local machine, and the public key is shared with GitHub for authentication. Paste the below command into your terminal. Replace "your_email@example.com" with your GitHub email address

   ```sh
   ssh-keygen -t ed25519 -C your_email@example.com
   ```
   - Press enter when prompted "Enter file in which to save the key".
   - **Optional:** You can choose to set a passphrase for added security when using your private key. When prompted for a passphrase, enter a password. I typically use my computer password for this.This passphrase is separate from your GitHub password.

   - `-t ed25519`: This specifies the type of key to generate, which is recommended for modern systems.
   - `-C your_email@example.com`: This adds an optional comment to help identify the key.
   
   

3. **Check for Key Files**: After generating the key pair, check if the key files were created on your system. These files are used for authentication.

   ```sh
   cd ~/.ssh
   ls -la
   ```

   - `id_ed25519`: This is your private key.
   - `id_ed25519.pub`: This is your public key.

#### 2. Start the SSH Agent

Before you can use your SSH key for authentication, you need to start the SSH agent, which will manage your keys.

```sh
eval "$(ssh-agent -s)"
```

This command initiates the SSH agent in the background.

#### 3. Configure SSH Key Usage

To ensure that your SSH key is used correctly, you need to configure your SSH client. Specifically, you will configure SSH to use the key you generated.

1. **Create or Edit SSH Config File**:

   If you don't already have an SSH configuration file, you can create one. Otherwise, open the existing SSH config file.

   ```sh
   open ~/.ssh/config  # If the file doesn't exist, create it
   ```

   To create the file enter the following command into the terminal
   ```sh
   touch ~/.ssh/config  # create file called config
   ```
   This will create a new file called config in the ~/.ssh folder.

2. **Add SSH Configuration**:

   Inside the SSH configuration file, add the following lines:

   ```sh
   Host github.com
     AddKeysToAgent yes
     UseKeychain yes
     IdentityFile ~/.ssh/id_ed25519
   ```

   - `Host github.com`: This specifies the remote host (GitHub) for which this configuration applies.
   - `AddKeysToAgent yes`: This tells SSH to automatically add your private key to the SSH agent when you use it.
   - `UseKeychain yes`: On macOS, this option enables the system's keychain to store your passphrase.
   - `IdentityFile ~/.ssh/id_ed25519`: This points to your private key file.

#### 4. Add SSH Key to SSH Agent

To add your SSH key to the SSH agent, run the following command:

```sh
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

This command prompts you for the passphrase you set (if any) when generating the key.

#### 5. Add SSH Key to Your GitHub Account

Finally, you need to let GitHub know about your public SSH key for authentication:

- **Copy the Public Key to Your Clipboard**:

  ```sh
  pbcopy < ~/.ssh/id_ed25519.pub
  ```

- **Go to GitHub**:

  - Access your GitHub account settings.
  - Under the "SSH and GPG keys" section, add a new SSH key by pasting the copied public key.

#### 6. Test the SSH Connection to GitHub

To ensure that your SSH connection to GitHub is working correctly, run the following command in the terminal:

```sh
ssh -T git@github.com
```

This will confirm that your SSH key is set up properly for authentication.

That's it! You've successfully created and configured your SSH keys for secure access to GitHub repositories.
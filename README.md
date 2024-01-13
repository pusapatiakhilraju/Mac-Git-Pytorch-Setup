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

Visit [GitHub's SSH key documentation](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) for detailed instructions. You can access and write data in repositories on GitHub.com using SSH (Secure Shell Protocol). When you set up SSH, you will need to generate a new private SSH key and add it to the SSH agent. You must also add the public SSH key to your account on GitHub before you use the key to authenticate or sign commits. <br/>

**The steps below will provide a simple explanation for the same:**

#### 1. Generate SSH Keys for GitHub

To securely access and write data in GitHub repositories using SSH, follow these steps:

1. **Generate a New SSH Key**: Firstly, You will create a new SSH key pair. The private key stays on your local machine, and the public key is shared with GitHub for authentication. Paste the below command into your terminal. Replace "your_email@example.com" with your GitHub email address

   ```sh
   ssh-keygen -t ed25519 -C your_email@example.com
   ```
   - Press enter when prompted "Enter file in which to save the key".
   - **Optional:** You can choose to set a passphrase for added security when using your private key. When prompted for a passphrase, enter a password. I typically use my computer password for this.This passphrase is separate from your GitHub password.

   - `-t ed25519`: This specifies the type of key to generate, which is recommended for modern systems.
   - `-C your_email@example.com`: This adds an optional comment to help identify the key.
   
   

2. **Check for Key Files**: After generating the key pair, check if the key files were created on your system. These files are used for authentication.

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

   If the file doesn't exist then to create the file enter the following command into the terminal
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

To add your SSH key to the SSH agent, run the following command from the terminal:

```sh
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

This command prompts you for the passphrase you set (if any) when generating the key.

#### 5. Add SSH Key to Your GitHub Account

Finally, you need to let GitHub know about your public SSH key for authentication:

- **Copy the Public Key to Your Clipboard**:
Paste the below command into the terminal and press enter to copy the public key to your clipboard.
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


# Pytorch -M3 Mac Setup

**Note:** As of January 2024, Apple has introduced the M3 versions of Mac, further expanding the range of Apple Silicon devices. This guide remains relevant for all Apple Silicon Macs, including the M3 series.

# Setting Up PyTorch on Apple Silicon (M1, M2, M1 Pro, M1 Max, M1 Ultra) for Data Science and Machine Learning

## Introduction

This guide will help you set up a machine learning environment with PyTorch on your Apple Silicon Mac, such as the M1, M2, M3, M1 Pro, M1 Max, M1 Ultra, M3 Pro, or M3 Max. You'll also enable PyTorch to use the Apple Silicon GPU for potentially faster computations.

Before we begin, we want to give credit and thanks to [Daniel Bourke](https://github.com/mrdbourke/pytorch-apple-silicon) for his excellent repository, from which we've borrowed setup code and instructions.

## Prerequisites

1. An Apple Silicon Mac (M1, M2, M1 Pro, M1 Max, M1 Ultra,M3, M3 Pro, M3 Max etc).
2. macOS 12.3+ (PyTorch will work on previous versions, but the GPU on your Mac won't be utilized, resulting in slower code).

## Step-by-Step Setup (For Beginners)

### 1. Install Homebrew

- Download and install Homebrew from [brew.sh](https://brew.sh).
- Follow the installation steps provided by Homebrew. **Note:** the simple steps to install brew are also provided in the git setup section.

### 2. Install Miniforge3 (Conda installer)

- Download [Miniforge3](https://raw.githubusercontent.com/pusapatiakhilraju/Mac-GitPytorch-Setup/master/miniforge-MacOSX-arm64.sh) for macOS arm64 chips (M1, M2, M1 Pro, M1 Max, M1 Ultra,  M3 Pro, M3 Max). 
- Install Miniforge3 into your home directory by running the following commands in the terminal:

   ```bash
   chmod +x ~/Downloads/Miniforge3-MacOSX-arm64.sh
   sh ~/Downloads/Miniforge3-MacOSX-arm64.sh
   ```

- Activate Miniforge3 by running:

   ```bash
   source ~/miniforge3/bin/activate
   ```

- **Restart your terminal.**

### 3. Create a PyTorch Environment

- Create a directory for your PyTorch environment (you can choose any name), for example:

   ```bash
   mkdir pytorch-test
   cd pytorch-test
   ```

- Make and activate a Conda environment with Python 3.8 (considered the most stable for this setup):

   ```bash
   conda create --name myenv python=3.8
   conda activate myenv
   ```

### 4. Install PyTorch and Dependencies

- Install PyTorch 1.12.0+ for Mac using pip. You can find the latest version on the [PyTorch getting started page](https://pytorch.org/get-started/locally/).

   ```bash
   pip3 install torch torchvision torchaudio
   ```

- This will install various packages, including PyTorch.

- Install common data science packages:

   ```bash
   conda install jupyter pandas numpy matplotlib scikit-learn tqdm
   ```

### 5. Start Jupyter Notebook

- Launch Jupyter Notebook by running:

   ```bash
   jupyter notebook
   ```

- In the Jupyter Notebook interface, create a new notebook by selecting "New" -> "Notebook: Python 3 (ipykernel)".

### 6. Verify Your Setup

- In the newly created notebook, run the following code to verify that all dependencies are available and check your PyTorch version and GPU access:

   ```python
   import torch
   import numpy as np
   import pandas as pd
   import sklearn
   import matplotlib.pyplot as plt

   print(f"PyTorch version: {torch.__version__}")

   # Check PyTorch has access to MPS (Metal Performance Shader, Apple's GPU architecture)
   print(f"Is MPS (Metal Performance Shader) built? {torch.backends.mps.is_built()}")
   print(f"Is MPS available? {torch.backends.mps.is_available()}")

   # Set the device
   device = "mps" if torch.backends.mps.is_available() else "cpu"
   print(f"Using device: {device}")
   ```

- If everything worked, you should see output similar to the following:

   ```
   PyTorch version: 1.12.0
   Is MPS (Metal Performance Shader) built? True
   Is MPS available? True
   Using device: mps
   ```

- You are now all set up to run PyTorch on your Apple Silicon device with GPU acceleration!

### 7. Utilizing the Apple Silicon GPU

- To run data and models on your Apple Silicon GPU, use the PyTorch device name "mps" with `.to("mps")`. MPS stands for Metal Performance Shaders, which is Apple's GPU framework.

   ```python
   import torch

   # Set the device
   device = "mps" if torch.backends.mps.is_available() else "cpu"

   # Create data and send it to the device
   x = torch.rand(size=(3, 4)).to(device)
   ```

- You should see output indicating that the tensor is on your Apple Silicon GPU.

Congratulations! Your Apple Silicon device is now ready for data science and machine learning with PyTorch and other essential libraries.

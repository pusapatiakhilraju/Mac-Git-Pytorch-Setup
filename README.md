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

Once it finished installing, run the following 2 commands as prompted. These 2 commands add brew to the path and allow to run brew commands to install packages
* (echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> /Users/akhil/.zprofile
* eval "$(/opt/homebrew/bin/brew shellenv)"

Type: brew help and see if brew is added to the path

### Step 2: Install VsCode

Visit the website: https://code.visualstudio.com/download to install VsCode

### Step 2: Install Git

Open your terminal and exectue the following command

```shell
brew install git

---
title: Managing multiple Python versions on macOS with pyenv
layout: default
---

If you’ve ever worked on multiple Python projects at the same time, you’ve likely run into the challenge of switching between Python versions. Thankfully, a tool called pyenv makes managing multiple Python versions a breeze. This tutorial will walk you through setting up pyenv to manage multiple Python versions on macOS.

## Prerequisites

Before you begin, you will need to ensure you have the following installed on your macOS machine:

* A terminal application, such as Terminal or iTerm  
* Homebrew

Homebrew is a package manager for macOS. For more information on Homebrew, [see the official Homebrew site](https://brew.sh/).

If you don’t have Homebrew installed, open a terminal window and run the following command:  
/bin/bash \-c "$(curl \-fsSL [https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh](https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh))"  
Follow the prompts to complete the installation.

## 1\. Installing pyenv

Now, you will install pyenv using Homebrew. Run the following command:  
```
brew install pyenv
```

## 2\. Installing Python versions

Now that you have installed pyenv, you can use it to install multiple Python versions on your machine. To view a list of available Python versions, run the following command:  
```
pyenv install --list
```

To install a specific version of Python, run the following command:  
```
pyenv install <version>
```

For example, to install Python 3.13.3, you would run the following command:  
```
pyenv install 3.13.3
```

## 3\. Setting Python versions

It is often useful to set a specific Python version to be used by default across your system. To set a global default Python version, run the following command:  
```
pyenv global <version>
```

To set a local Python version to be used in a specific directory, first navigate to the directory in your terminal, then run the following command:  
```
pyenv local <version>
```

To check the current active Python version, run the following command:  
```
pyenv version
```

## 4\. (Optional) Creating a virtual environment

When using pyenv local, packages and dependencies are installed into the global specified version. For example, if directory A is using a local Python version of 3.13.3 and you install numpy 1.23.0, this version will be installed into the global Python 3.13.3 environment. This means that if directory B is using Python 3.13.3, it will also use numpy 1.23.0.

In many cases, it is useful to keep some projects’ packages and dependencies separate from others. Virtual environments make this possible by creating separate Python environments per project. This means that you can install Python dependencies into a specific environment without affecting other projects or the global Python environment.

To create a new virtual environment, use the `virtualenv` tool. Run the following command:  
```
pyenv virtualenv <version> <environment_name>
```

For example, to create a virtual environment called `myproject-env` using Python 3.13.3, you would run the following command:  
```
pyenv virtualenv 3.13.3 myproject-env
```

This would create a new Python virtual environment in `~/.pyenv/versions/3.13.3/envs/myproject-env`.

## 5\. (Optional) Activating a virtual environment

After creating a virtual Python environment, you need to activate it. This tells your shell session to switch to the specific Python version and packages for the specified environment. To activate a virtual environment, run the following command:  
```
pyenv activate <environment_name>
```

For example, to activate the virtual environment called “myproject-env”, you would run the following command:  
```
pyenv activate myproject-env
```

## Summary

Congratulations\! You have now learned how to:

* Install multiple Python versions using pyenv  
* Set global and local Python versions for different projects  
* (Optionally) Use isolated Python environments using pyenv-virtualenv for easier dependency management

With these steps, managing projects with different Python versions and dependencies becomes much simpler. Happy coding\!
---
layout: page
title: Installation instructions
nav_order: 2
---

# AE353 - Design Project Environment Setup

Melkior Ornik, Timothy Bretl and Gokul Puthumanaillam

August, 2024

## Overview

This document provides instructions for setting up the Python environment required for the design projects on your device. We provide instructions for Linux, macOS and Windows devices. In case you have any issues following these instructions, please post on the discussions section in Canvas and we will help you troubleshoot your installation. **Do not worry if some of the terms in the instructions below are not familiar to you**. We gratefully acknowledge Prof. Tim Bretl for developing the simulation environments used in the design projects.

# Linux (Ubuntu/Debian-based Distros)

### Command-line basics

##### How to open a terminal

When we say "open a terminal," we're referring to starting the **Terminal** application. Here's how you can do it:

- Press `Ctrl` + `Alt` + `T` to open the terminal.
- Alternatively, you can search for "Terminal" using the Ubuntu Dash or application menu of other distributions.

##### How to run a command

When we say "run a command," we mean type something into the terminal window and press Enter. For instance:

> run the command `pwd` to find your current working directory

You would type `pwd` into the terminal window and press Enter. The output might look something like:

```
gokulp01@gokul:~$ pwd
/home/gokulp01
```

##### How to change the working directory

On your system, files are organized in directories. When working on the command line, you're situated in one of these directories. Commands can access files in this directory but cannot (by default) access files in other directories.

When we instruct "change the working directory," we mean to switch to a different directory.

To do this, run the command:

```
cd path/to/directory
```

where "`path/to/directory`" is the path of the directory you want to navigate to.

### ⚠️ Do this once

##### Install required dependencies

Open a terminal and run:

```
sudo apt update
sudo apt install -y build-essential python3-pip
```

This will install the basic build tools and Python's package manager, `pip`.

##### Install conda

[Conda](https://docs.conda.io/) is a package manager primarily for Python.

First, check if conda is already installed:

```
conda update -n base conda
```

If the above succeeds, conda is installed, and you should proceed to the next step. If not, continue with installing conda.

For Linux, download Miniconda using `wget` and install:

```
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
```

If you do not have wget, install it using:

```
sudo apt install wget
```

Follow the prompts. You might need to restart the terminal or run `source ~/.bashrc` to update your path.

##### Create a conda environment

To create an environment for your work, open a terminal and run:

```
conda create -n ae353
```

Then, activate the environment and install necessary packages:

```
conda activate ae353
conda config --env --add channels conda-forge
conda config --env --set channel_priority strict
conda install -y python=3 numpy scipy sympy matplotlib \
    notebook ipywidgets imageio imageio-ffmpeg \
    pybullet meshcat-python
```

##### Get the code

Open a terminal and change the working directory to a folder in which you would like to put all your files. Then, use [git](https://git-scm.com/) to download the code from the ae353 github repository by running this command:

```
git clone https://github.com/uiuc-ae353/ae353-fa24
```

This is a fork of Prof. Bretl's simulation environment.

This process will take very little time. When it completes, you should find a new folder called `ae353-fa24` inside your working directory.

### Do this every time

##### Change your working directory

Open a terminal and navigate to your working directory, `ae353-fa24`.

##### Activate your conda environment

Run:

```
conda activate ae353
```

Your terminal prefix should change to `(ae353)`, indicating you're now in the `ae353` environment.

##### Start a jupyter notebook

Run:

```
jupyter notebook
```

This will launch Jupyter Notebook in your browser. Navigate to open any `.ipynb` notebooks.

**It's advisable to duplicate and work on a copy of the original notebook. If you're familiar with `git`, this step might not be necessary.**

# MacOS

Some of the instructions here is a repeat of the Linux system instructions.

### Learn command-line basics

##### How to open a terminal

When we say "open a terminal," what we mean is to start the **Terminal** application. Here is one way to do that:

- Click the Launchpad icon in the Dock.
- Type "Terminal" in the search field.
- Click Terminal.

See documentation on [Open Terminal](https://support.apple.com/guide/terminal/open-or-quit-terminal-apd5265185d-f365-44cb-8b09-71a064a42125/mac) for more information. Note that it is often helpful to have more than one terminal window open at the same time (or more than one tab in the same window).

##### How to run a command

When we say "run a command," what we mean is to type something into the terminal window and press return. For example, suppose we said:

> run the command `pwd` to find your current working directory

You would type `pwd` into the terminal window and press return, with the result being something like this:

```
(base) gokulp01@gokul ~ % pwd
/Users/gokulp01
```

See documentation on [Execute commands and run tools in Terminal on Mac for more information](https://support.apple.com/guide/terminal/execute-commands-and-run-tools-apdb66b5242-0d18-49fc-9c47-a2498b7c91d5/mac). Also see the [Command Line Primer](https://developer.apple.com/library/archive/documentation/OpenSource/Conceptual/ShellScripting/CommandLInePrimer/CommandLine.html) for a list of frequently used commands.

##### How to change the working directory

All the files on your computer are organized in folders, which are commonly referred to as "directories." When you are working on the command line in a terminal, you are working in one of these directories. Commands you run can find files in that directory, but cannot (by default) find files in other directories.

When we say "change the working directory," we mean exactly that --- telling the terminal the directory in which you want to work.

To do this, we run the command

```
cd path/to/directory
```

where "`path/to/directory`" is replaced by the location of the directory in which you want to work. One easy way way to find this location (i.e., the "path" to your directory) is by dragging its folder from the Finder into your terminal window (see documentation on [Drag items into a Terminal window on Mac](https://support.apple.com/guide/terminal/drag-items-into-a-terminal-window-trml106/mac)). In particular, I would first type "`cd `" (note the single trailing space):

```
(base) gokulp01@gokul ~ % cd
```

Then, I would drag a folder into the terminal window and press return. For instance, suppose I had created a folder called `ae353-fa24` somewhere on my computer and dragged it in, then pressed return --- I would see something like this:

```
(base) gokulp01@gokul ~ % cd /Users/gokulp01/Documents/ae353-fa24
(base) gokulp01@gokul ae353-fa24 %
```

See documentation on [Specify files and folders in Terminal on Mac](https://support.apple.com/guide/terminal/specify-files-and-folders-apd3cf6fe02-3ec8-48f1-951f-866e52955fc8/mac) for other ways to specify the path to a directory.

### ⚠️ Do this once

##### Install xcode command line tools

Open a terminal and run this command, accepting all default options:

```
xcode-select --install
```

You may be asked to restart your computer during or after this process. Please do so.

##### Install conda

[Conda](https://docs.conda.io/) is a package manager that you will use to install python, along with a number of required tools.

Open a terminal. Check if conda is already installed by trying to update it to its latest version (something you should do from time to time anyway):

```
conda update -n base conda
```

If this process succeeds, then conda is installed, and you should skip to the next step. If this process does not succeed, then you still need to install conda, and you should continue with this step.

Follow the instructions for [Installing on macOS](https://docs.conda.io/projects/conda/en/latest/user-guide/install/macos.html). It is easiest to use the [Miniconda installer](https://docs.conda.io/en/latest/miniconda.html), in particular the appropriate `.pkg` file for your architecture (Intel or Silicon) --- just double-click the `.pkg` file after it downloads and accept all the default options (you need not "verify your installer hashes" or run a bash command or anything).

##### Create a conda environment

An "environment" is like a sandbox where you can install software without causing any conflict with other things you might have installed on your computer. To create an environment for work in AE353, open a terminal and run this command:

```
conda create -n ae353
```

You may see something like `WARNING: A conda environment already exists` and be asked if you want to `Remove existing environment`. This means that you already created an environment called `ae353`. Perhaps something went wrong and you are creating it again --- in this case, type `y` to remove the existing environment and proceed to recreate it. From then on, accept all default options.

Finally, run the following commands (copy _the entire thing_, paste it into your terminal, and press return):

```
conda activate ae353
conda config --env --add channels conda-forge
conda config --env --set channel_priority strict
conda install -y python=3 numpy scipy sympy matplotlib \
    notebook ipywidgets imageio imageio-ffmpeg \
    pybullet meshcat-python
```

##### Get the code

Open a terminal and change the working directory to a folder in which you would like to put all your files. Then, use [git](https://git-scm.com/) to download the code from the ae353 github repository by running this command:

```
git clone https://github.com/uiuc-ae353/ae353-fa24
```

This is a fork of Prof. Bretl's simulation environment.

### Do this every time

##### Change your working directory

Open a terminal and change your working directory to `ae353-fa24`, wherever you put this.

##### Activate your conda environment

Run this command:

```
conda activate ae353
```

You should see the prefix to your terminal prompt change from `(base)` to `(ae353)`. This means you are in the conda environment you created for work with AE353.

##### Start a jupyter notebook

Run this command:

```
jupyter notebook
```

A browser window should open with the jupyter notebook interface. You can now navigate to and open any of the notebooks (with extension `.ipynb`) used for in-class examples or for design projects.

**We strongly recommend you duplicate and work with a copy of any given notebook rather than working with the original.** Feel free to ignore this suggestion if you are a `git` expert.

# Windows

### Learn command-line basics

##### How to open an anaconda powershell

When we say "open an anaconda powershell," what we mean is to start the **Anaconda Powershell Prompt (Miniconda)** application. Here is one way to do that:

- Click the Windows search bar near the bottom-left corner of your desktop.
- Type "anaconda" into the search field.
- Click **Anaconda Powershell Prompt (Miniconda)**.

Note that this application will only exist after you follow the instructions to [Install conda](#install-conda-1).

##### How to run a command

When we say "run a command," what we mean is to type something into the window of an anaconda powershell and press enter. See [this beginners guide](https://www.makeuseof.com/tag/a-beginners-guide-to-the-windows-command-line/) to [Windows Commands](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands).

##### How to change the working directory

All the files on your computer are organized in folders, which are commonly referred to as "directories." When you are working on the command line, you are working in one of these directories. Commands you run can find files in that directory, but cannot (by default) find files in other directories.

When we say "change the working directory," we mean exactly that --- telling an anaconda powershell the directory in which you want to work.

To do this, we run the command

```
cd path\to\directory
```

where "`path\to\directory`" is replaced by the location of the directory in which you want to work. One easy way way to find this location (i.e., the "path" to your directory) is by dragging its folder from the File Explorer into your powershell window (see documentation on [Quickly Copy Files Paths to Your Command Prompt via Drag and Drop](https://lifehacker.com/quickly-copy-file-paths-to-your-command-prompt-via-drag-5382503). In particular, I would first type "`cd `" (note the single trailing space):

```
C:\Users\jakek>cd
```

Then, I would drag a folder into the powershell window and press enter. For instance, suppose I had created a folder called `ae353-fa24` somewhere on my computer and dragged it in, then pressed enter --- I would see something like this:

```
C:\Users\jakek>cd C:\Users\jakek\OneDrive\Documents\ae353-fa24
C:\Users\jakek\OneDrive\Documents\ae353-fa24>
```

See documentation on [Find and Open Files using Windows Command Prompt](https://www.faqforge.com/windows/windows-10/find-and-open-files-using-windows-command-prompt/) for a way to search for the directory location of files on your computer.

### ⚠️ Do this once

##### Install conda

[Conda](https://docs.conda.io/) is a package manager that you will use to install python, along with a number of required tools.

Try to open an **anaconda powershell**.

If you can, then conda may already be installed. Try to update it to its latest version (something you should do from time to time anyway) by running the following command in the powershell:

```
conda update -n base conda
```

If this process succeeds, then conda is installed properly, and you should skip to the next step. If this process does not succeed, or if you couldn't open an anaconda powershell in the first place, then you still need to install conda, and you should continue with this step.

Follow the instructions for [Installing on Windows](https://docs.conda.io/projects/conda/en/latest/user-guide/install/windows.html). It is easiest to use the [Miniconda installer](https://conda.io/miniconda.html), in particular the [Miniconda3 Windows 64-bit](https://repo.anaconda.com/miniconda/Miniconda3-latest-Windows-x86_64.exe) --- just double-click the `.exe` file after it downloads and accept all the default options (you need not "verify your installer hashes").

##### Create a conda environment

An "environment" is like a sandbox where you can install software without causing any conflict with other things you might have installed on your computer. To create an environment for work in AE353, open an **anaconda powershell** and run this command:

```
conda create -n ae353
```

You may see something like `WARNING: A conda environment already exists` and be asked if you want to `Remove existing environment`. This means that you already created an environment called `ae353`. Perhaps something went wrong and you are creating it again --- in this case, type `y` to remove the existing environment and proceed to recreate it. From then on, accept all default options.

Finally, run the following commands (copy _the entire thing_, paste it into your powershell, and press enter):

```
conda activate ae353
conda config --env --add channels conda-forge
conda config --env --set channel_priority strict
conda install -y python=3 numpy scipy sympy matplotlib
conda install -y notebook ipywidgets imageio imageio-ffmpeg
conda install -y pybullet meshcat-python
conda install -y git
```

Note that (unlike for MacOS) we are using conda to install [git](https://git-scm.com/) --- this seemed simplest, rather than figuring out how to make system-installed software accessible to the anaconda powershell. The only consequence of this choice is that you will need to be in the `ae353` environment to run git.

##### Get the code

Open an **anaconda powershell** and change the working directory to a folder in which you would like to put all your files.

Then, activate your conda environment:

```
conda activate ae353
```

Open a terminal and change the working directory to a folder in which you would like to put all your files. Then, use [git](https://git-scm.com/) to download the code from the ae353 github repository by running this command:

```
git clone https://github.com/uiuc-ae353/ae353-fa24
```

This is a fork of Prof. Bretl's simulation environment.

This process will take very little time. When it completes, you should find a new folder called `ae353-fa24` inside your working directory.

### Do this every time

##### Change your working directory

Open an **anaconda powershell** and change your working directory to `ae353-fa24`, wherever you put this.

##### Activate your conda environment

Run this command:

```
conda activate ae353
```

You should see the prefix to your powershell prompt change from `(base)` to `(ae353)`. This means you are in the conda environment you created for work with AE353.

##### Get the latest version of the code

Run this command:

```
git pull
```

Do not worry, this will not overwrite any of your own work. If you see any errors or warnings, post a note to [Campuswire](https://campuswire.com/c/G9558828D/) and course staff will help resolve them.

##### Start a jupyter notebook

Run this command:

```
jupyter notebook
```

A browser window should open with the jupyter notebook interface. You can now navigate to and open any of the notebooks (with extension `.ipynb`) used for in-class examples or for design projects.

**We strongly recommend you duplicate and work with a copy of any given notebook rather than working with the original.** Feel free to ignore this suggestion if you are a `git` expert.

## Testing your setup

To test your setup, first activate your conda environment (follow the system specific instructions). After cloning the repository, you should be able to see a directory named `ae353-installation-tests`. Change your working directory to `ae353-installation-tests/tests` and open a Jupyter notebook here:

```
cd ae353-fa24/ae353-installation-tests/tests
jupyter notebook
```

This should open a browser window with the Jupyter notebook.

Open the notebook DroneDemo.ipynb in the test subfolder using the Jupyter notebook interface in
your browser.Run all the cells in the notebook. If all the cells run without throwing an error, your installation is
successful. A new window with a simulation showing a drones and some rings should also show
up. If you get any errors at this stage, followup in Canvas.

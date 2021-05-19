---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Conda Environments and Jupyter Notebooks"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-04-25T15:04:34-04:00
lastmod: 2020-04-25T15:04:34-04:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

Here is a cheatsheet in using Anaconda with some of my personal preferences that I have retained. If you do follow this, *please* let me know if something is not working correctly!

![](anaconda.png)

# What is Anaconda?

Simply put, Anaconda is an open-source package management system for Python. One of its most popular applications, Jupyter, is commonly used for data science related projects. In this article, I have tried to detail the steps from creating a virtual environment in Anaconda to using it in your Jupyter notebooks.

### Installing Anaconda

1. Go to the Anaconda website [here](https://www.anaconda.com/products/individual).
2. Click on the appropriate distribution (Mac or Linux) and download the Anaconda installer for **Python 3.7**.
3. Open Terminal and execute the following commands:

```
cd ~/Downloads
chmod +x Anaconda3-2020.02-MacOSX-x86_64.sh
./Anaconda3-2020.02-MacOSX-x86_64.sh
```

***If you're on a Linux distribution, the downloaded file has a different name, so execute the commands above with the downloaded file name.***

:exclamation: You should reset your Terminal window by simply restarting it.

# Setting up your virtual environment

Creating a virtual environment for your Python project has many benefits, including version control for you and your collaborators and managing sets of installed packages for separate projects. Here are 5 steps to creating your Anaconda virtual environment and using it in a Jupyter notebook.

### 1 - Creating the virtual environment

```
conda create -n YOUR_ENV_NAME python=3.7
```

The command above specifies Python version in the environment to be 3.7, since this is the most stable and updated version at the moment. However, you can use a different version if you prefer.

### 2 - Creating a Terminal Shortcut

My preference is to create a Terminal shortcut to activate the environment.

```
echo "alias SHORTCUT_COMMAND='conda activate YOUR_ENV_NAME'" | cat - ~/.bash_profile > ~/.bash_profile
source ~/.bash_profile
```

***If you are on a Linux distribution, replace ```~/.bash_profile``` by ```~/.bashrc``` due to the difference in file names.***

### 3 - Activating your environment

With the shortcut created using the commands above, you can now activate the environment by simply typing its name in Terminal!

```
YOUR_ENV_NAME
```

### 4 - Installing packages

Say you want to install some Python packages called `package1`, `package2` and `package3`. You can use the code below to do so.

```
conda install -n YOUR_ENV_NAME package1 package2 package3
```

### 5 - Adding the environment to Jupyter

Often times, it would be desirable to be able to access the environment in a Jupyter notebook, which is often used for coding in Python (it's definitely my favorite!). To add your newly created environment to Jupyter, run the following commands in Terminal.

```
conda install -n YOUR_ENV_NAME ipykernel -c conda-forge
python -m ipykernel install --user --name YOUR_ENV_NAME
```

##### Running into `command not found: jupyter`

One of the packages that you may have to install is jupyter itself!

```
conda install -n YOUR_ENV_NAME -c conda-forge jupyterlab
```

# Ready to code!

Your environment should be ready to use in your Jupyter notebooks!

</br>

# Other (hopefully) useful things

### Locating your virtual environment

My preference is to go the folder in which your environment is installed and simply removing it. To find the directory in which your virtual environment is located, you can do:

```
source activate YOUR_ENV_NAME # to activate your environment
which python
```

You should get an output under the following format: `SOME_DIRECTORY/YOUR_ENV_NAME/bin/python`. The directory in which your environment is located is simply `SOME_DIRECTORY`.

##### Example

When I run `which python` after activating my environment called `ml`, I obtain `/Users/larry/anaconda3/envs/ml/bin/python`. It follows that the directory where my conda environments are located is `Users/larry/anaconda3/envs/`.

### Deleting your environment

Once you have located your environment (see above) and found the directory in which your environments are located and that we will call `SOME_DIRECTORY`. To delete your environment, run the following commands:

```
cd SOME_DIRECTORY
rm -rf YOUR_ENV_NAME
```

### Removing your environment from Jupyter

Although you have deleted your environment and it no longer exists, for some reason the option to select it as a kernel is still available in your Jupyter notebook, although selecting it won't work. To remove the environment as an option in the Jupyter notebook, run the following.

```
jupyter kernelspec uninstall YOUR_ENV_NAME
```

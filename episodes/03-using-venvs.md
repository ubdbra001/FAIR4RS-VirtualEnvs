---
title: Getting started with `venv`and `pip`
teaching: 10
exercises: 0
---

::: questions

- How do I create a venv?
- How do I install packages into my new venv?

:::::


::: objectives

- Create a new virtual environment
- Learn how to activate and deactivate the virtual environment
- Installing packages in your environment

:::::

## Introduction

Now we have a grasp of the steps needed to capture the package layer of the computational 
environment, so let's get started with `venv` and `pip`. 

## Creating a new Virtual Environment

We can set up a new virtual environment anywhere, but it's generally considered good practice to 
set it up in the folder for your project.

So let's start by creating a directory for our project using the terminal, and the moving into it.

```bash
mkdir my-new-project
cd my-new-project
```

Now we can create our virtual environment using the `venv` module:

```bash
python -m venv .venv
```
::: instructor

This command consists of two parts:  
1. `python -m venv` - Create a new python virtual environment  
2. `.venv` - In a directory called `.venv`  

::::

If we view the contents of the `my-new-project` directory by using `ls` (for Windows) or `ls -a` 
(for MacOS /Linux), we should see that there is now a `.venv` sub-directory.

::: callout

### What should I call my virtual environment directory?

You can call the directory that contains the virtual environment whatever you like, but the two 
conventional names are `venv` and `.venv`.

The primary difference between these two is that the `.` at the start of `.venv` indicates to MacOS 
and Linux-based operating systems that this directory should be hidden when you view the parent
directory (i.e. `my-new-project`).

In this course I will default to `.venv` but you don't have to copy me.

:::::

## Activating the new virtual environment

Now you've created the virtual environment you're ready to start installing packages, right?

Not quite, the next step is activating the environment. This step effectively tells your operating system 
that it should be using the Python interpreter in your new virtual environment, rather than the one 
in the base environment. We'll see why this is important later.  

The command you use to do this will depend on the OS you are using:

:::: tab

### Windows 
`.venv/Scripts/activate`

### MacOS/Linux
`source .venv/bin/activate`

::::::

Once you've done this you should see a prompt with name of you environment appear on the left of
your console, e.g:

::: tab

### Windows

`(.venv) PS C:\Users\Daniel\Projects\my-new-project> `

### MacOS/Linux

`(.venv) dan@DCS032157:~/my-new-project$ `

::::

Now you are ready to start installing packages for your project.


::::: callout

### Prompt name blues

If you called the directory you created your environment `.venv` you'll notice that the name of the
environment displayed in your console is the same. This isn't very informative, especially if you're
switching between multiple projects (are you sure you're installing that package in the right 
`.venv`?)

By defult this name is the same name you gave to the directory contianing the virtual environment, 
so you could address this by giving the directory a different name e.g.:
`python -m venv my-new-project-venv`, and this will be reflected in the console:

::: tab

### Windows

`(my-new-project-venv) PS C:\Users\Daniel\Projects\my-new-project> `

### MacOS/Linux

`(my-new-project-venv) dan@DCS032157:~/my-new-project$ `

::::

However, this does mean you have to remember the name you gave to the virtual environment for 
each project. Not the end of the world, but a bit annoying.


#### `--prompt` to the rescue

Handily, `venv` gives you the option to customise the text in the console for each project:

```bash
python -m venv .venv --prompt my-new-project
```
Which will set the virtual environment directory name to `venv`, but also set the console 
prompt to `my-new-project`:

::: tab

### Windows

`(my-new-project) PS C:\Users\Daniel\Projects\my-new-project> `

### MacOS/Linux

`(my-new-project) dan@DCS032157:~/my-new-project$ `

::::

You can even use the name of the current directory without having to type it out:

```bash
python -m venv .venv --prompt .
```

::::::

## Deactivating the current virtual environment

Deactivating the currently activated virtual environment and returning to using the base environment
is as simple as using the deactivate command:

```bash
deactivate
```

If you want to reactivate the environment then just follow the steps to activate it, no need to 
create a new one.


::: challenge

### Your Turn 1

Create a new project folder, create a new virtual environment inside it, and activate that virtual 
environment.  
Try and make sure to name your virtual environment something memorable.

:::::


## Using your Virtual Environment

Now you have a virtual environment set up for your project, let's start using it.

### Installing packages into the Virtual Environment

First let's reactivate our virtual environment if it's not already active:

::: tab

### Windows 
`.venv/Scripts/activate`

### MacOS/Linux
`source .venv/bin/activate`

:::::

Now we can install packages using `pip` as we would usually, e.g:

```bash
python -m pip install emoji
```

Which will install the latest available version of the `emoji` package to our environment.  

You can check what is installed in your current environment by running:

```bash
python -m pip list
```

```
Package Version
------- -------
emoji   2.14.0
pip     24.2
```

You should also verify that the code is accessible to you by starting the Python interpreter
(type `python` at the command line) and then running the code below:

```python
import emoji

print(emoji.emojize('Python is :thumbs_up:'))
```

To exit the Python interpreter you can either type `exit()` and press return, or 
use the keyboard shortcut `Ctrl`/`Cmd` + `D`

::: challenge

### Your turn 2

Try installing and using a different package (e.g. `numpy`, `pandas`, `pillow`).  
Try using `python -m pip list` when your virtual environment is activated to see if the package is 
available in your environment.  
What happens if you deactivate you environment and try and run the emoji code above?
Use `python -m pip list` to help you investigate

:::::


## The nuts and bolts of Virtual environments

At this point you may be wondering what is going on behind the scenes to make this all work.
So, lets take a brief detour to give you an idea.

### Peeking inside .venv

Lets start by looking in the `.venv` directory in your project.
The contents will be slightly different depending on your operating system:  

::: tab

### Windows

```
📂 my-new-project/
└── 📂 .venv/
    ├── 📂 Include/
    ├── 📂 Lib/
    |   └── 📂 site-packages/
    ├── 📂 Scripts/
    |   ├── 📄 activate.bat
    |   ├── 📄 deactivate.bat
    |   ├── 📄 pip.exe
    |   ├── 📄 python.exe
    |   └── ...
    └── 📄 pyvenv.cfg
```

The sub-directories of interest here are:  
 - `Scripts`, which contains the files used to activate/deactivate the virtual environment,
 as well as a copy of Python and Pip  
 - `Lib`, which contains all the packages you have installed within the virtual envoronment
 (although ususlly nested within sub-directories, e.g. `Lib/site-packages/`)  


### MacOS/Linux

```
📂 my-new-project/
└── 📂 .venv/
    ├── 📂 bin/
    |   ├── 📄 activate
    |   ├── 📄 pip
    |   ├── 📄 python
    |   └── ...
    ├── 📂 include/
    ├── 📂 lib/
    |   └── 📂 python3.12/
    |       └── 📂 site-packages/
    └── 📄 pyvenv.cfg
```

The sub-directories of interest here are:  
 - `bin`, which contains the files used to activate/deactivate the virtual environment,
 as well as a copy of Python and Pip  
 - `lib`, which contains all the packages you have installed within the virtual envoronment
 (although ususlly nested within sub-directories, e.g. `lib/python3.12/site-packages/`)  

:::::

So, when you set up the virtual environment `venv` will (amongst other things):  
- create a copy of the Python interpreter (and `pip`) in the `.venv` directory  
- create a place where it can install packages, and  
- setup some files that allow the virtual environment to be activated and deactivated  

But you now have (at least) two Python executables on your computer. How does you computer know 
which one to use within the virtual environment?

### The path to Python

To explain this we need to introduce environmental variables, and specifically the `PATH` 
environmental variable.  
Environmental variables are values held by your Operating System which tell the Operating System 
and installed programs how to behave.  
One of the more common ones that you may come across is the `PATH` variable which, in essence, 
is a is a list of places that your computer will check for executables.  
So, when you run `python` in the console your computer will go through this list of places, get the 
location of the Python executables on your system, and then run Python from the first place it 
finds that executable.

You can see what directories are in your `PATH` variable by running:

:::: tab

### Windows 
`$env:path`

To make the output a bit more human readable (one line per directory) use:  
`$env:path -split ';'`

### MacOS/Linux
`echo $PATH`

To make the output a bit more human readable (one line per directory) use:  
`echo -e ${PATH//:/\\n}`

::::::

You can also see the locations of a specific executable on the `PATH` by running:

:::: tab

### Windows
`where.exe python`

### MacOS/Linux
`which -a python`
::::::

::::: challenge

Run the above commands while your virtual environment is activated vs deactivated.  
What differences do you see in the `PATH` variable, and the list of Python locations?

::::::

### Pulling it together

The parts we've looked at in the last 2 sections give us a clearer idea of what Python is doing 
when you create and activate a virtual environment:

1. You run `python -m venv .venv`:  
    - A directory called `.venv` is created  
    - A standard directory structure is created within `.venv`  
    - A copy of Python, pip, and the activate/deactivate files are put in a sub-directory of 
    `.venv` (where will depend on your OS)

2. You activate the virtual environment:  
    - The path to the `.venv` directory is added to start of the system's `PATH` environmental variable  
    - The path to the `site-packages` directory  within `.venv` is added to the `PYTHONPATH` environmental
    variable  
      - Not discussed in detail but this is how Python knows where to install/import packages  

3. You deactivate the virtual environment:  
    - The path to `.venv` is removed from the start of the system's `PATH` environmental variable  
    - The path to `site-packages` within `.venv` is removed from the `PYTHONPATH` environmental 
    variable


:::: keypoints

 - You can create, activate, and deactivate virtual environments using the `venv` package
 - You can installing packages in a virtual environment using `pip install`, and view installed 
 packages with `pip list`
 - Python and `venv` create an directory on your computer that contains your virtual environment (
a separate Python interpreter and library)
 - Activating and deactivating the virtual environment modifies the `PATH` and `PYTHONPATH` 
 environmental variables to add/remove the path to the directory containing the virtual environment.

::::::

---
title: Using `venv` and `pip` to capture a computational environment
teaching: 10
exercises: 0
---

::: questions

- How do I use `venv` and `pip` to capture my computational environments?

:::::

::: objectives

- How to specify specific versions of a package
- Recording packages installed in an environment
- Restoring packages to an environment

:::::

Now we've got the basics of how to use `venv` to create a virtual environment and then install 
packages to it, let's move onto using these tools to record and restore the packages we install.

## Specifying specific versions for a package

Before we start we have to address the question: What if we want to install a specific version of a 
package for our project?  
Currently we have been using the command `python -m pip install numpy`, but by default this will 
install the latest version of `numpy`.  
Not particularly useful if we need to use anything other than the latest version.

In this case we can use 
[Version Specifiers](https://packaging.python.org/en/latest/specifications/version-specifiers/#id5) 
to tell `pip` exactly which version we want to install.

::: spoiler

### Software Versioning

Software Versioning is the practice of assigning an identifier to a particular release or state of 
a piece of software. This allows you to indicate what version of a particular bit of software you 
used to do something (e.g. execute code, run an analysis, etc.)

#### Semantic versioning
The primary versioning system used is called '[Semantic Versioning](https://semver.org)' and follows the following 
pattern: Major.minor.patch  
For example, the version of Python I am currently using is 3.12.1, so it has:
  - a major version of 3,  
  - a minor version of 12, and  
  - a patch version of 1  

#### Calendar versioning
An alternative, and lesser used system is called '[Calendar versioning](https://calver.org)' and follows the following
pattern: Year.month  
For example, the latest release of the Ubuntu operating system is: 24.10, indicating it was 
released in October 2024.  

For more details about software versioning see the 
[FAIR4RS Packaging lesson](https://fair2-for-research-software.github.io/FAIR4RS-Packaging/)
:::::

There are a whole range of different specifiers but the two most useful in this case are:  

  - `~=` - Compatible release  

  - `==` - Version match  

### Compatible release

This matches any version of the package that is expected to be compatible with the version 
specified, e.g.:  

  - `~= 3.1` will select version 3.1 or later, but not version 4.0 or later 

  - `~= 3.1.2` will select version 3.1 or later, but not version 3.2 or later

### Version match

This matches a version of a package exactly, e.g.:

  - `== 3.1` will select version 3.1 (or 3.1.0), and no other version.

  - `== 3.1.*` will select any version that starts with 3.1, and is equivalent to `~= 3.1.0`

So if you wanted to install the latest version of `numpy` version 1 you could use either:

```
python -m pip install numpy~=1.0
```

or

```
python -m pip install numpy==1.*
```

Version specifier are also used when we record the packages we've used our project, which we'll see 
next.

## Recording the packages installed

So far, we've seen how virtual environments can be used to isolate the dependencies for each of our 
projects, but how do we ensure that this environment can be recreated?

We've used `pip list` to see the packages we've installed before, so maybe we could use this and 
copy everything listed into a file?

As with a previous solution, this would work, but is manual and may be prone to errors so it is 
better to get the computer to do this for you. Also, `pip` lists all the packages available in your 
environment, not just the ones you installed, which is not ideal.

Luckily we have `pip freeze`. `pip freeze` will output a list of packages with version specifiers 
for the packages you installed in your virtual environment. These can then be written to a file
(conventionally called `requirements.txt`) that can then be used to restore all the packages installed
into a new environment.

```
python -m pip freeze > requirements.txt
```

The `>` symbol here can be read as: 'write the output of the command on the left into the file on 
the right' (instead of displaying it on screen)

**Note**: `pip` will not automatically update the `requirements.txt` file to include packages you 
install after running `pip freeze`. So be sure to rerun it periodically, and especially after you 
install new packages.

:::::: challenge

Use `pip freeze` to record all the packages installed in your virtual environment.  
Take a look at the `requirements.txt` file generated. What do you notice?

:::::::

:::: callout

Now you have a file that has captured the packages used in your computational environment, you can 
put it under version control alongside your code.  
This ensures that anyone who accesses your code can also recreate this part of your computational 
environment.

::::::

## Restoring an environment from a `requirements.txt` file

Now recreating a project environment can be done in 3 steps:

1. Create a new environment

2. Activate the environment

3. Install the dependencies from `requirements.txt`: 
`python -m pip install --requirement requirements.txt`

You should be familiar with how to do steps 1 and 2, and step 3 is a small modification to how 
you'd typically install packages.

:::: callout

The `--requirement` option tells `pip` that you are installing the packages from a file and to 
look in the file for the specific package names and versions.  
This can be shortened to just `-r`.

::::::

:::: challenge

[Here](files/requirements.txt) is a requirements.txt file from one of my projects.  
I'd like you to download it, and follow the steps above to recreate the computational environment.  
(You may have to right click and select "Save file as...")  

What packages (names and versions) did I have installed in this environment?  
Can you recreate this level of my computational environment?

::::::

:::: keypoints

 - Package versions can be specified by using the semantic versioning syntax (or, less commonly, 
 the calendar versioning syntax).
 - `pip freeze` can be used to get a list of installed packages, and these can be written to a file.
 - Packages can be restored from a file produced by `pip freeze` by using the `--requirement` 
option with `pip install`.

::::::

# Reproducible Computational Environments - Virtual Environments

## About

Ensuring that others are able to take your code, run it, and are able to produce the same (or equivalent) results is one of the key tenets of FAIR and reproducible research software. However, this can be at odds with changes over time to code that you are using but is not your own (i.e. packages/libraries). What can you do to ensure your code and results are reproducible when you re-run it in 1, 2, or 5 years?

This course will provide you with an overview of different ways to answer this question, and then focus on virtual environments as one possible solution. Specifically: What virtual environments are, how they work, and how you can use them to isolate and record the dependencies for your projects to ensure reproducibility.

## Target audience

This course is aimed at people who know the basics of Python programming and who write code or software for research, from writing a couple of scripts to automate data collection to writing entire data analysis software. The course is particularly relevant to people who would like to follow best practices and increase the reproducibility of their research code.

This course is intended for researchers who use the Python programming language, but the basic concepts can be applied to other programming languages.

## Outline

- What is computational reproducibility?
  - Code/software is rarely static
  - Levels of computational reproducibility:
    - Package/library level - Virtual environments
    - OS level - Virtualisation/Containers
- What are Virtual environments and why should I use them?
  - What are Virtual environments?
  - Why use Virtual environments?
  - Why use `venv`?
- How do I use a Virtual environment:
  - Creating a virtual environment
  - Activating/Deactivating a virtual environment
  - Installing packages in a virtual environment
  - Specific versions
  - Listing installed packages
  - Recording installed packages & pinning
  - Upgrading installed packages
- Limitations:
  - Managing different versions of Python
  - Installing more complex packages
  - Keeping track of added/removed packages
  - Alternatives to `venv`
- Next steps:
  - Packaging
  - Containers

## Prerequisites

Some experience with developing research software or scripts, for example in Python or R.

## Learning outcomes

After completing this course, participants should be able to:

- Understand what computational reproducibility is, and why it is an issue for research
- Describe the different levels of computational reproducibility
- Understand the high-level nature and purpose of a virtual environment
- Use venv along with pip to create and manage virtual environments
- Understand the limitations of `venv`, and options to address them

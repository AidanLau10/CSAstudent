---
layout: post
title: Tools Verify using Shell
description: Linux and the shell is used in this example to setup and verify the installation of the tools.  Additionally, a few programming exercises are included.
categories: ['DevOps']
permalink: /devops/tools/verify
menu: nav/tools_setup.html
toc: True
comments: True
---

## Computers and Terminals

A brief overview of Terminal and Linux is a step on your way to becoming a Linux expert. When a computer boots up, **a kernel (MacOS, Windows, Linux) is started**. This kernel is the core of the operating system and manages hardware resources. Above the kernel, various applications run, including the **shell** and **terminal**, which allow users to interact with the system using a basic set of commands provided by the kernel.

Typically, casual users interact with the system through a Desktop User Interface (UI) that is started by the computer's boot-up processes. However, to interact directly with the shell, users can run a "terminal" application through the Desktop UI. Additionally, **VS Code provides the ability to activate a "terminal"** within its editing environment, making it convenient for developers to execute commands without leaving the code editor.

In this next phase, we will use a Jupyter notebook to perform Linux commands through a terminal. The Jupyter notebook is an application that runs above the kernel, providing an interactive environment for writing and executing code, including shell commands. This setup allows us to seamlessly integrate code execution, data analysis, and documentation in one place, enhancing our productivity and learning experience.

## Setup a Personal GitHub Pages Project

You will be making a personal copy of the course repository. Be sure to have a GitHub account!!!

- Use the **Green "Use this Template"** button on the [portfolio_2025](https://github.com/nighthawkcoders/portfolio_2025) repository page to set up your personal GitHub Pages repository.
- Create a new repository.
- Fill in the dialog and select the **Repository Name** to be under your GitHub ID ownership.

    ![create repo]({{ site.baseurl }}/images/notebooks/foundation/create_repo.jpg)

- After this is complete, use the **Green "Code"** button on the newly created repository page to capture your "Project Repo" name.

In the next few code cells, we will run a bash (shell) script to pull a GitHub project. 

## Shell Script and Variables

We will ultimately run a bash (shell) script to pull a GitHub project. This next script simply sets up the necessary **environment variables** to tell the script the location of repository from GitHub and where to copy the output.

For now, focus on each line that begins with `export`. These are **shell variables**. Each line has a **name** (after the keyword `export`) and a **value** (after the equal sign).

Here is a full description:

- **Creates a temporary file** `/tmp/variables.sh` to store environment variables.
- **Sets the `project_dir` variable** to your home directory with a subdirectory named `nighthawk`. You can change `nighthawk` to a different name to test your git clone.
- **Sets the `project` variable** to a subdirectory within `project_dir` named `portfolio_2025`. You can change `portfolio_2025` to the name of your project.
- **Sets the `project_repo` variable** to the URL of the GitHub repository. Change this to the project you created from the `portfolio_2025` template.

**By running this script, you will prepare your environment for cloning** and working on your GitHub project. This is an essential step in setting up your development environment and ensuring that all dependencies are correctly configured.


```python
%%script bash

# Dependency Variables, set to match your project directories

cat <<EOF > /tmp/variables.sh
export project_dir=$HOME/downloads/vscode  # change nighthawk to different name to test your git clone
export project=\$project_dir/teacher2025  # change student_2025 to name of project from git clone
export project_repo="https://github.com/AidanLau10/teacher2025.git"  # change to project you created from portfolio_2025 template 
EOF
```

## Describing the Outputs of the Variables

The next script will extract the saved variables and display their values. Here is a description of the commands:

- The `source` command loads the variables that we saved in the `/tmp/variables.sh` file in the previous code cell.
- The `echo` commands display the contents of the named variables:
  - **project_dir**: The directory where your project is located.
  - **project**: The specific project directory within `project_dir`.
  - **project_repo**: The URL of the GitHub repository.

By running this script, you can verify that the environment variables are correctly set in your development environment. If they don't match up, go back to the previous code cell and make the necessary corrections.


```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

# Output shown title and value variables
echo "Project dir: $project_dir"
echo "Project: $project"
echo "Repo: $project_repo"
```

    Project dir: /Users/aidanlau/downloads/vscode
    Project: /Users/aidanlau/downloads/vscode/teacher2025
    Repo: https://github.com/AidanLau10/teacher2025.git


## Project Setup and Analysis with Bash Scripts
The bash scripts that follow automate what was done in the Tools Installation procedures with regards to cloning a GitHub project. Doing this in a script fashion adds the following benefits:

- After completing these steps, we will have notes on how to set up and verify a project.
- By reviewing these commands, you will start to learn the basics of Linux.
- By setting up these code cells, you will be learning how to develop automated scripts using Shell programming.
- You will learn that pretty much anything we type on a computer can be automated through the use of variables and a coding language.

### Pull Code

> Pull code from GitHub to your machine. This is a **bash script**, a sequence of commands, that will create a project directory and add the "project" from GitHub to the vscode directory. There is conditional logic to make sure that the clone only happens if it does not (!) exist. Here are some key elements in this code:

- `cd` command (change directory), remember this from the terminal session.
- `if` statements (conditional statements, called selection statements by College Board), code inside only happens if the condition is met.

Run the script two times and you will see that the output changes.  In the second run, the files exist and it impact the flow of the code.


```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Using conditional statement to create a project directory and project"

cd ~    # start in home directory

# Conditional block to make a project directory
if [ ! -d $project_dir ]
then 
    echo "Directory $project_dir does not exist... making directory $project_dir"
    mkdir -p $project_dir
fi
echo "Directory $project_dir exists." 

# Conditional block to git clone a project from project_repo
if [ ! -d $project ]
then
    echo "Directory $project does not exist... cloning $project_repo"
    cd $project_dir
    git clone $project_repo
    cd ~
fi
echo "Directory $project exists."
```

    Using conditional statement to create a project directory and project
    Directory /Users/aidanlau/downloads/vscode exists.
    Directory /Users/aidanlau/downloads/vscode/teacher2025 does not exist... cloning https://github.com/AidanLau10/teacher2025.git


    Cloning into 'teacher2025'...


    Directory /Users/aidanlau/downloads/vscode/teacher2025 exists.


### Look at Files in GitHub Project

> All computers contain files and directories. The clone brought more files from the cloud to your machine. Review the bash shell script, observe the commands that show and interact with files and directories. These were used during setup.

- `ls` lists computer files in Unix and Unix-like operating systems.
- `cd` offers a way to navigate and change the working directory.
- `pwd` prints the working directory.
- `echo` is used to display a line of text/string that is passed as an argument.


```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Navigate to project, then navigate to area wwhere files were cloned"
cd $project
pwd

echo ""
echo "list top level or root of files with project pulled from github"
ls

```

    Navigate to project, then navigate to area wwhere files were cloned
    /Users/aidanlau/downloads/vscode/teacher2025
    
    list top level or root of files with project pulled from github
    404.html
    Gemfile
    LICENSE
    Makefile
    README.md
    README4YML.md
    _config.yml
    [34m_data[m[m
    [34m_includes[m[m
    [34m_layouts[m[m
    [34m_notebooks[m[m
    [34m_posts[m[m
    [34m_sass[m[m
    [34massets[m[m
    [34mdesign[m[m
    [34mimages[m[m
    index.md
    [34mkasm_design[m[m
    [34mnavigation[m[m
    [34mnode_backend[m[m
    requirements.txt
    [34mscripts[m[m


### Look at File List with Hidden and Long Attributes

> Most Linux commands have options to enhance behavior. The enhanced listing below shows permission bits, owner of the file, size, and date.

Some useful `ls` flags:
- `-a`: List all files including hidden files.
- `-l`: List in long format.
- `-h`: Human-readable file sizes.
- `-t`: Sort by modification time.
- `-R`: Reverse the order of the sort.

[ls reference](https://www.rapidtables.com/code/linux/ls.html)


```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Navigate to project, then navigate to area wwhere files were cloned"
cd $project
pwd

echo ""
echo "list all files in long format"
ls -al   # all files -a (hidden) in -l long listing
```

    Navigate to project, then navigate to area wwhere files were cloned
    /Users/aidanlau/downloads/vscode/teacher2025
    
    list all files in long format
    total 136
    drwxr-xr-x  28 aidanlau  staff    896 Aug 23 09:33 [34m.[m[m
    drwxr-xr-x@ 51 aidanlau  staff   1632 Aug 23 09:33 [34m..[m[m
    drwxr-xr-x  12 aidanlau  staff    384 Aug 23 09:33 [34m.git[m[m
    drwxr-xr-x   3 aidanlau  staff     96 Aug 23 09:33 [34m.github[m[m
    -rw-r--r--   1 aidanlau  staff    251 Aug 23 09:33 .gitignore
    drwxr-xr-x   3 aidanlau  staff     96 Aug 23 09:33 [34m.vscode[m[m
    -rw-r--r--   1 aidanlau  staff    436 Aug 23 09:33 404.html
    -rw-r--r--   1 aidanlau  staff    122 Aug 23 09:33 Gemfile
    -rw-r--r--   1 aidanlau  staff  11357 Aug 23 09:33 LICENSE
    -rw-r--r--   1 aidanlau  staff   3551 Aug 23 09:33 Makefile
    -rw-r--r--   1 aidanlau  staff  14185 Aug 23 09:33 README.md
    -rw-r--r--   1 aidanlau  staff     79 Aug 23 09:33 README4YML.md
    -rw-r--r--   1 aidanlau  staff    842 Aug 23 09:33 _config.yml
    drwxr-xr-x   7 aidanlau  staff    224 Aug 23 09:33 [34m_data[m[m
    drwxr-xr-x  19 aidanlau  staff    608 Aug 23 09:33 [34m_includes[m[m
    drwxr-xr-x   9 aidanlau  staff    288 Aug 23 09:33 [34m_layouts[m[m
    drwxr-xr-x   7 aidanlau  staff    224 Aug 23 09:33 [34m_notebooks[m[m
    drwxr-xr-x  13 aidanlau  staff    416 Aug 23 09:33 [34m_posts[m[m
    drwxr-xr-x   7 aidanlau  staff    224 Aug 23 09:33 [34m_sass[m[m
    drwxr-xr-x   6 aidanlau  staff    192 Aug 23 09:33 [34massets[m[m
    drwxr-xr-x   3 aidanlau  staff     96 Aug 23 09:33 [34mdesign[m[m
    drwxr-xr-x  24 aidanlau  staff    768 Aug 23 09:33 [34mimages[m[m
    -rw-r--r--   1 aidanlau  staff  11586 Aug 23 09:33 index.md
    drwxr-xr-x   6 aidanlau  staff    192 Aug 23 09:33 [34mkasm_design[m[m
    drwxr-xr-x  10 aidanlau  staff    320 Aug 23 09:33 [34mnavigation[m[m
    drwxr-xr-x   8 aidanlau  staff    256 Aug 23 09:33 [34mnode_backend[m[m
    -rw-r--r--   1 aidanlau  staff     57 Aug 23 09:33 requirements.txt
    drwxr-xr-x  16 aidanlau  staff    512 Aug 23 09:33 [34mscripts[m[m



```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Look for posts"
export posts=$project/_posts  # _posts inside project
cd $posts  # this should exist per fastpages
pwd  # present working directory
ls -lR  # list posts recursively
```

    Look for posts
    /Users/aidanlau/downloads/vscode/teacher2025/_posts
    total 240
    -rw-r--r--  1 aidanlau  staff   4326 Aug 23 09:33 2023-08-21-python_flask.md
    -rw-r--r--  1 aidanlau  staff  11347 Aug 23 09:33 2023-08-30-agile_methodolgy.md
    -rw-r--r--  1 aidanlau  staff   6265 Aug 23 09:33 2023-08-31-javascript_project-binary-calculator.md
    -rw-r--r--  1 aidanlau  staff   6712 Aug 23 09:33 2023-08-31-javascript_project-calculator.md
    -rw-r--r--  1 aidanlau  staff   5707 Aug 23 09:33 2023-08-31-javascript_project-game-of-life.md
    -rw-r--r--  1 aidanlau  staff   3811 Aug 23 09:33 2023-08-31-javascript_project-music-api.md
    -rw-r--r--  1 aidanlau  staff  14282 Aug 23 09:33 2023-08-31-javascript_project-snake-game.md
    -rw-r--r--  1 aidanlau  staff   3683 Aug 23 09:33 2023-09-12-python-flask-repo.md
    -rw-r--r--  1 aidanlau  staff  48002 Aug 23 09:33 2023-10-03-java-types-student-2.ipynb
    -rw-r--r--  1 aidanlau  staff   2698 Aug 23 09:33 2024-07-11-GPTchatbot.md
    drwxr-xr-x  4 aidanlau  staff    128 Aug 23 09:33 [34mKasm[m[m
    
    ./Kasm:
    total 0
    drwxr-xr-x  3 aidanlau  staff   96 Aug 23 09:33 [34mConfig_Guides[m[m
    drwxr-xr-x  4 aidanlau  staff  128 Aug 23 09:33 [34mMultiServer[m[m
    
    ./Kasm/Config_Guides:
    total 8
    -rw-r--r--  1 aidanlau  staff  3167 Aug 23 09:33 2024-07-12-terraform-vs-ansible.md
    
    ./Kasm/MultiServer:
    total 160
    -rw-r--r--  1 aidanlau  staff  55630 Aug 23 09:33 2024-07-12-multiserver-development.md
    -rw-r--r--  1 aidanlau  staff  21730 Aug 23 09:33 2024-07-12-multiserver-install.md



```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Look for notebooks"
export notebooks=$project/_notebooks  # _notebooks is inside project
cd $notebooks   # this should exist per fastpages
pwd  # present working directory
ls -lR  # list notebooks recursively
```

    Look for notebooks
    /Users/aidanlau/downloads/vscode/teacher2025/_notebooks
    total 24
    -rw-r--r--  1 aidanlau  staff  10436 Aug 23 09:33 2023-08-23-jupyter-notebook-python.ipynb
    drwxr-xr-x  8 aidanlau  staff    256 Aug 23 09:33 [34mCSA[m[m
    drwxr-xr-x  4 aidanlau  staff    128 Aug 23 09:33 [34mCSP[m[m
    drwxr-xr-x  9 aidanlau  staff    288 Aug 23 09:33 [34mFoundation[m[m
    drwxr-xr-x  6 aidanlau  staff    192 Aug 23 09:33 [34mKASM[m[m
    
    ./CSA:
    total 0
    drwxr-xr-x   4 aidanlau  staff  128 Aug 23 09:33 [34mchatgpt[m[m
    drwxr-xr-x   7 aidanlau  staff  224 Aug 23 09:33 [34mfullstack_java[m[m
    drwxr-xr-x   3 aidanlau  staff   96 Aug 23 09:33 [34mspring[m[m
    drwxr-xr-x  11 aidanlau  staff  352 Aug 23 09:33 [34munits_1_to_10[m[m
    drwxr-xr-x   6 aidanlau  staff  192 Aug 23 09:33 [34munits_1_to_10_examples[m[m
    drwxr-xr-x  11 aidanlau  staff  352 Aug 23 09:33 [34munits_1_to_10_quiz[m[m
    
    ./CSA/chatgpt:
    total 40
    -rw-r--r--  1 aidanlau  staff  6512 Aug 23 09:33 2024-07-16-chatgpt-code.ipynb
    -rw-r--r--  1 aidanlau  staff  8992 Aug 23 09:33 2024-07-16-chatgpt-intro.ipynb
    
    ./CSA/fullstack_java:
    total 88
    -rw-r--r--  1 aidanlau  staff   4384 Aug 23 09:33 2024-07-21-Fullstack-intro.ipynb
    -rw-r--r--  1 aidanlau  staff  12072 Aug 23 09:33 2024-07-22-Fullstack-backend.ipynb
    -rw-r--r--  1 aidanlau  staff   2909 Aug 23 09:33 2024-07-22-Fullstack-design.ipynb
    -rw-r--r--  1 aidanlau  staff   8853 Aug 23 09:33 2024-07-22-Fullstack-example.ipynb
    -rw-r--r--  1 aidanlau  staff   4621 Aug 23 09:33 2024-07-22-Fullstack-frontend.ipynb
    
    ./CSA/spring:
    total 32
    -rw-r--r--  1 aidanlau  staff  13812 Aug 23 09:33 2023-10-02-java-spring-anatomy.ipynb
    
    ./CSA/units_1_to_10:
    total 488
    -rw-r--r--  1 aidanlau  staff  13973 Aug 23 09:33 2024-06-24-unit_2.ipynb
    -rw-r--r--  1 aidanlau  staff  17230 Aug 23 09:33 2024-06-24-unit_3.ipynb
    -rw-r--r--  1 aidanlau  staff  11517 Aug 23 09:33 2024-06-24-unit_4.ipynb
    -rw-r--r--  1 aidanlau  staff  17743 Aug 23 09:33 2024-06-24-unit_5.ipynb
    -rw-r--r--  1 aidanlau  staff  31117 Aug 23 09:33 2024-06-24-unit_6.ipynb
    -rw-r--r--  1 aidanlau  staff  42237 Aug 23 09:33 2024-06-29-unit_7.ipynb
    -rw-r--r--  1 aidanlau  staff  42641 Aug 23 09:33 2024-07-02-unit_8.ipynb
    -rw-r--r--  1 aidanlau  staff  55677 Aug 23 09:33 2024-07-08-unit_9.ipynb
    drwxr-xr-x  9 aidanlau  staff    288 Aug 23 09:33 [34munit_01[m[m
    
    ./CSA/units_1_to_10/unit_01:
    total 120
    -rw-r--r--  1 aidanlau  staff  14270 Aug 23 09:33 2023-10-03-java-types-student-1.ipynb
    -rw-r--r--  1 aidanlau  staff   2172 Aug 23 09:33 2024-06-23-unit_1._intro.ipynb
    -rw-r--r--  1 aidanlau  staff   5162 Aug 23 09:33 2024-06-24-unit_1_primatives.ipynb
    -rw-r--r--  1 aidanlau  staff   2360 Aug 23 09:33 2024-06-24-unit_1_reference.ipynb
    -rw-r--r--  1 aidanlau  staff   8198 Aug 23 09:33 2024-06-24-unit_1_stack_heap.ipynb
    -rw-r--r--  1 aidanlau  staff   5932 Aug 23 09:33 2024-07-01-unit_1_examples.ipynb
    -rw-r--r--  1 aidanlau  staff   5428 Aug 23 09:33 2024-07-13-unit_1_quiz.ipynb
    
    ./CSA/units_1_to_10_examples:
    total 40
    -rw-r--r--  1 aidanlau  staff  3891 Aug 23 09:33 2024-06-24-unit_2_examples.ipynb
    -rw-r--r--  1 aidanlau  staff  3004 Aug 23 09:33 2024-06-24-unit_3_examples.ipynb
    -rw-r--r--  1 aidanlau  staff  3954 Aug 23 09:33 2024-06-24-unit_4_examples.ipynb
    -rw-r--r--  1 aidanlau  staff  4446 Aug 23 09:33 2024-06-24-unit_5_examples.ipynb
    
    ./CSA/units_1_to_10_quiz:
    total 96
    -rw-r--r--  1 aidanlau  staff  3658 Aug 23 09:33 2024-07-13-unit_2_quiz.ipynb
    -rw-r--r--  1 aidanlau  staff  1656 Aug 23 09:33 2024-07-13-unit_3_quiz.ipynb
    -rw-r--r--  1 aidanlau  staff  1473 Aug 23 09:33 2024-07-13-unit_4_quiz.ipynb
    -rw-r--r--  1 aidanlau  staff  6515 Aug 23 09:33 2024-07-13-unit_5_quiz.ipynb
    -rw-r--r--  1 aidanlau  staff  5533 Aug 23 09:33 2024-07-13-unit_6_quiz.ipynb
    -rw-r--r--  1 aidanlau  staff  4703 Aug 23 09:33 2024-07-13-unit_7_quiz.ipynb
    -rw-r--r--  1 aidanlau  staff  3657 Aug 23 09:33 2024-07-13-unit_8_quiz.ipynb
    -rw-r--r--  1 aidanlau  staff  2701 Aug 23 09:33 2024-07-13-unit_9_quiz.ipynb
    -rw-r--r--  1 aidanlau  staff  1753 Aug 23 09:33 2024-07-14-unit_10_quiz.ipynb
    
    ./CSP:
    total 0
    drwxr-xr-x   7 aidanlau  staff  224 Aug 23 09:33 [34mbig-ideas[m[m
    drwxr-xr-x  12 aidanlau  staff  384 Aug 23 09:33 [34mflask[m[m
    
    ./CSP/big-ideas:
    total 0
    drwxr-xr-x   3 aidanlau  staff   96 Aug 23 09:33 [34mbig-idea-1[m[m
    drwxr-xr-x   4 aidanlau  staff  128 Aug 23 09:33 [34mbig-idea-2[m[m
    drwxr-xr-x  12 aidanlau  staff  384 Aug 23 09:33 [34mbig-idea-3-part-1-fundamentals[m[m
    drwxr-xr-x  12 aidanlau  staff  384 Aug 23 09:33 [34mbig-idea-3-part-2-concepts[m[m
    drwxr-xr-x   6 aidanlau  staff  192 Aug 23 09:33 [34mbig-idea-3-part-2-reinforce[m[m
    
    ./CSP/big-ideas/big-idea-1:
    total 24
    -rw-r--r--  1 aidanlau  staff  8415 Aug 23 09:33 2023-10-04-big-idea-1_python-errors.ipynb
    
    ./CSP/big-ideas/big-idea-2:
    total 232
    -rw-r--r--  1 aidanlau  staff  100550 Aug 23 09:33 2023-10-02-python_data-abstraction-1.ipynb
    -rw-r--r--  1 aidanlau  staff   13398 Aug 23 09:33 2023-10-02-python_data-abstraction-2.ipynb
    
    ./CSP/big-ideas/big-idea-3-part-1-fundamentals:
    total 304
    -rw-r--r--  1 aidanlau  staff   4643 Aug 23 09:33 2023-10-04-big-idea-3-fundamentals.ipynb
    -rw-r--r--  1 aidanlau  staff  11462 Aug 23 09:33 2023-10-05-big-idea-3-1.ipynb
    -rw-r--r--  1 aidanlau  staff  18277 Aug 23 09:33 2023-10-05-big-idea-3-2.ipynb
    -rw-r--r--  1 aidanlau  staff  48623 Aug 23 09:33 2023-10-05-big-idea-3-3.ipynb
    -rw-r--r--  1 aidanlau  staff   4959 Aug 23 09:33 2023-10-05-big-idea-3-4.ipynb
    -rw-r--r--  1 aidanlau  staff   4470 Aug 23 09:33 2023-10-10-big-idea-3-5.ipynb
    -rw-r--r--  1 aidanlau  staff   7767 Aug 23 09:33 2023-10-10-big-idea-3-6.ipynb
    -rw-r--r--  1 aidanlau  staff   7602 Aug 23 09:33 2023-10-11-big-idea-3-7.ipynb
    -rw-r--r--  1 aidanlau  staff  14573 Aug 23 09:33 2023-10-12-big-idea-3-8.ipynb
    -rw-r--r--  1 aidanlau  staff  12678 Aug 23 09:33 2023-10-19-big-idea-3-10.ipynb
    
    ./CSP/big-ideas/big-idea-3-part-2-concepts:
    total 328
    -rw-r--r--  1 aidanlau  staff   4297 Aug 23 09:33 2023-10-04-big-idea-3-concepts.ipynb
    -rw-r--r--  1 aidanlau  staff  12569 Aug 23 09:33 2023-10-13-big-idea-3-9.ipynb
    -rw-r--r--  1 aidanlau  staff   7367 Aug 23 09:33 2023-10-19-big-idea-3-11.ipynb
    -rw-r--r--  1 aidanlau  staff  10418 Aug 23 09:33 2023-10-22-big-idea-3-12.ipynb
    -rw-r--r--  1 aidanlau  staff   8633 Aug 23 09:33 2023-10-22-big-idea-3-13.ipynb
    -rw-r--r--  1 aidanlau  staff  56044 Aug 23 09:33 2023-10-26-big-idea-3-14.ipynb
    -rw-r--r--  1 aidanlau  staff   5656 Aug 23 09:33 2023-10-26-big-idea-3-15.ipynb
    -rw-r--r--  1 aidanlau  staff   9927 Aug 23 09:33 2023-10-27-big-idea-3-16.ipynb
    -rw-r--r--  1 aidanlau  staff  14019 Aug 23 09:33 2023-10-27-big-idea-3-17.ipynb
    -rw-r--r--  1 aidanlau  staff  13720 Aug 23 09:33 2023-10-27-big-idea-3-18.ipynb
    
    ./CSP/big-ideas/big-idea-3-part-2-reinforce:
    total 112
    -rw-r--r--  1 aidanlau  staff   9854 Aug 23 09:33 2023-10-28-big-idea-3_Iteration.ipynb
    -rw-r--r--  1 aidanlau  staff  13096 Aug 23 09:33 2023-10-28-big-idea-3_python-lists.ipynb
    -rw-r--r--  1 aidanlau  staff  14581 Aug 23 09:33 2023-10-29-big-idea-3_algorithms.ipynb
    -rw-r--r--  1 aidanlau  staff  10278 Aug 23 09:33 2023-10-30-big-idea-3_developing-procedures.ipynb
    
    ./CSP/flask:
    total 544
    -rw-r--r--  1 aidanlau  staff  22339 Aug 23 09:33 2021-01-25-flask-code-style.ipynb
    -rw-r--r--  1 aidanlau  staff   5997 Aug 23 09:33 2024-01-24-flask-intro.ipynb
    -rw-r--r--  1 aidanlau  staff   8876 Aug 23 09:33 2024-01-25-flask-anatomy.ipynb
    -rw-r--r--  1 aidanlau  staff  89001 Aug 23 09:33 2024-01-25-flask-code-full_stack.ipynb
    -rw-r--r--  1 aidanlau  staff  49612 Aug 23 09:33 2024-01-25-flask-code-ideation.ipynb
    -rw-r--r--  1 aidanlau  staff  26212 Aug 23 09:33 2024-01-25-flask-code-login-page.ipynb
    -rw-r--r--  1 aidanlau  staff  14682 Aug 23 09:33 2024-01-25-flask-code-sign-up.ipynb
    -rw-r--r--  1 aidanlau  staff  13216 Aug 23 09:33 2024-01-25-flask-play-in-jupyter.ipynb
    -rw-r--r--  1 aidanlau  staff   2248 Aug 23 09:33 2024-01-26-flask-scrum.ipynb
    -rw-r--r--  1 aidanlau  staff  22289 Aug 23 09:33 2024-01-27-flask-deploy-aws.ipynb
    
    ./Foundation:
    total 8
    -rw-r--r--   1 aidanlau  staff  3974 Aug 23 09:33 2024-08-21-sprint1_plan.ipynb
    drwxr-xr-x   5 aidanlau  staff   160 Aug 23 09:33 [34mA-pair_programming[m[m
    drwxr-xr-x   8 aidanlau  staff   256 Aug 23 09:33 [34mB-tools_and_equipment[m[m
    drwxr-xr-x   8 aidanlau  staff   256 Aug 23 09:33 [34mC-github_pages[m[m
    drwxr-xr-x   6 aidanlau  staff   192 Aug 23 09:33 [34mD-sass_basics[m[m
    drwxr-xr-x  10 aidanlau  staff   320 Aug 23 09:33 [34mE-frontend_development[m[m
    drwxr-xr-x   3 aidanlau  staff    96 Aug 23 09:33 [34mF-projects[m[m
    
    ./Foundation/A-pair_programming:
    total 48
    -rw-r--r--  1 aidanlau  staff   5433 Aug 23 09:33 2023-08-16-pair_programming.md
    -rw-r--r--  1 aidanlau  staff   3918 Aug 23 09:33 2023-08-16-pair_showcase.ipynb
    -rw-r--r--  1 aidanlau  staff  11624 Aug 23 09:33 2023-08-17-pair_habits.ipynb
    
    ./Foundation/B-tools_and_equipment:
    total 216
    -rw-r--r--  1 aidanlau  staff   9767 Aug 23 09:33 2023-08-19-devops_accounts.ipynb
    -rw-r--r--  1 aidanlau  staff   5931 Aug 23 09:33 2023-08-21-devops_tools-home.ipynb
    -rw-r--r--  1 aidanlau  staff  18564 Aug 23 09:33 2023-08-21-devops_tools-setup.ipynb
    -rw-r--r--  1 aidanlau  staff  23156 Aug 23 09:33 2023-08-22-devops_tools-verify.ipynb
    -rw-r--r--  1 aidanlau  staff  32288 Aug 23 09:33 2023-08-23-devops-githhub_pages-play.ipynb
    -rw-r--r--  1 aidanlau  staff   9479 Aug 23 09:33 2023-08-23-devops-hacks.ipynb
    
    ./Foundation/C-github_pages:
    total 128
    -rw-r--r--  1 aidanlau  staff  14718 Aug 23 09:33 2023-08-23-github_pages-intro.ipynb
    -rw-r--r--  1 aidanlau  staff  12484 Aug 23 09:33 2023-08-23-github_pages-markdonwn.ipynb
    -rw-r--r--  1 aidanlau  staff  10111 Aug 23 09:33 2023-08-24-github_pages-anatomy.ipynb
    -rw-r--r--  1 aidanlau  staff   3850 Aug 23 09:33 2023-08-25-github_pages-utterances.ipynb
    -rw-r--r--  1 aidanlau  staff  10291 Aug 23 09:33 2023-08-26-github-pages-jekyll.ipynb
    -rw-r--r--  1 aidanlau  staff   2149 Aug 23 09:33 2023-08-27-github-pages-hacks.ipynb
    
    ./Foundation/D-sass_basics:
    total 112
    -rw-r--r--  1 aidanlau  staff  12586 Aug 23 09:33 2023-09-01-SASS-basics-play.ipynb
    -rw-r--r--  1 aidanlau  staff  11648 Aug 23 09:33 2023-09-01-SASS_basics-intro.ipynb
    -rw-r--r--  1 aidanlau  staff  13865 Aug 23 09:33 2023-09-02-SASS_basics-coding.ipynb
    -rw-r--r--  1 aidanlau  staff   8415 Aug 23 09:33 2024-07-20-SASS-hacks.ipynb
    
    ./Foundation/E-frontend_development:
    total 248
    -rw-r--r--  1 aidanlau  staff   6951 Aug 23 09:33 2023-08-27-frontend-basics-playground.ipynb
    -rw-r--r--  1 aidanlau  staff   7054 Aug 23 09:33 2023-08-28-frontend-basics-html.ipynb
    -rw-r--r--  1 aidanlau  staff   7204 Aug 23 09:33 2023-08-28-frontend-basics-js-errors.ipynb
    -rw-r--r--  1 aidanlau  staff  16924 Aug 23 09:33 2023-08-29-frontend-basics-of-js.ipynb
    -rw-r--r--  1 aidanlau  staff  20154 Aug 23 09:33 2023-08-30-frontend-basics-js-data-types.ipynb
    -rw-r--r--  1 aidanlau  staff  12454 Aug 23 09:33 2023-08-30-frontend-basics-js-with-html.ipynb
    -rw-r--r--  1 aidanlau  staff  12781 Aug 23 09:33 2023-08-30-frontend-input.ipynb
    -rw-r--r--  1 aidanlau  staff  25250 Aug 23 09:33 2023-08-30-frontend-output_objects.ipynb
    
    ./Foundation/F-projects:
    total 16
    -rw-r--r--  1 aidanlau  staff  7079 Aug 23 09:33 2023-08-30-javascript_project-play.ipynb
    
    ./KASM:
    total 0
    drwxr-xr-x  8 aidanlau  staff  256 Aug 23 09:33 [34mConfig_Guides[m[m
    drwxr-xr-x  5 aidanlau  staff  160 Aug 23 09:33 [34mDatabase[m[m
    drwxr-xr-x  5 aidanlau  staff  160 Aug 23 09:33 [34mMultiServer[m[m
    drwxr-xr-x  5 aidanlau  staff  160 Aug 23 09:33 [34mWorkspaces[m[m
    
    ./KASM/Config_Guides:
    total 56
    -rw-r--r--  1 aidanlau  staff  4804 Aug 23 09:33 2024-07-05-docker-cronjob-for-containers.ipynb
    -rw-r--r--  1 aidanlau  staff  3646 Aug 23 09:33 2024-07-05-manual-addition-of-docker-images.ipynb
    -rw-r--r--  1 aidanlau  staff  1183 Aug 23 09:33 2024-07-12-security-group-configuration.ipynb
    -rw-r--r--  1 aidanlau  staff  3222 Aug 23 09:33 2024-07-15-manual-registry-addition.ipynb
    -rw-r--r--  1 aidanlau  staff  2088 Aug 23 09:33 2024-07-15-persistent-data.ipynb
    -rw-r--r--  1 aidanlau  staff  2292 Aug 23 09:33 2024-07-31-plans-for-big-meet.ipynb
    
    ./KASM/Database:
    total 88
    -rw-r--r--  1 aidanlau  staff  11567 Aug 23 09:33 2024-08-10-rds-documentation.ipynb
    -rw-r--r--  1 aidanlau  staff   4665 Aug 23 09:33 2024-08-14-migration.ipynb
    -rw-r--r--  1 aidanlau  staff  23557 Aug 23 09:33 2024-08-14-python-api-4-kasm.ipynb
    
    ./KASM/MultiServer:
    total 56
    -rw-r--r--  1 aidanlau  staff  18056 Aug 23 09:33 2024-07-30-autoscale-config.ipynb
    -rw-r--r--  1 aidanlau  staff   3663 Aug 23 09:33 2024-08-07-persistent-storage.ipynb
    -rw-r--r--  1 aidanlau  staff   3473 Aug 23 09:33 2024-08-14-workspace-registry-admin.ipynb
    
    ./KASM/Workspaces:
    total 40
    -rw-r--r--  1 aidanlau  staff  8672 Aug 23 09:33 2024-08-14-container-building.ipynb
    -rw-r--r--  1 aidanlau  staff  1285 Aug 23 09:33 2024-08-14-dockerhub-push.ipynb
    -rw-r--r--  1 aidanlau  staff  3038 Aug 23 09:33 2024-08-14-nighthawk-registry.ipynb



```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Look for images, print working directory, list files"
cd $project/images  # this should exist per fastpages
pwd
ls -lR
```

    Look for images, print working directory, list files
    /Users/aidanlau/downloads/vscode/teacher2025/images
    total 4176
    -rw-r--r--   1 aidanlau  staff  129584 Aug 23 09:33 agile.webp
    drwxr-xr-x  26 aidanlau  staff     832 Aug 23 09:33 [34mbinary[m[m
    drwxr-xr-x   9 aidanlau  staff     288 Aug 23 09:33 [34mcourse-brag[m[m
    -rw-r--r--   1 aidanlau  staff  134051 Aug 23 09:33 createusersample.png
    -rw-r--r--   1 aidanlau  staff   15406 Aug 23 09:33 favicon.ico
    -rw-r--r--   1 aidanlau  staff  177895 Aug 23 09:33 food.png
    drwxr-xr-x   5 aidanlau  staff     160 Aug 23 09:33 [34mfullstack[m[m
    -rw-r--r--   1 aidanlau  staff  244133 Aug 23 09:33 homesample.png
    -rw-r--r--   1 aidanlau  staff  220573 Aug 23 09:33 information.png
    drwxr-xr-x   5 aidanlau  staff     160 Aug 23 09:33 [34mjokes[m[m
    drwxr-xr-x  13 aidanlau  staff     416 Aug 23 09:33 [34mjpa-lesson-images[m[m
    drwxr-xr-x   3 aidanlau  staff      96 Aug 23 09:33 [34mkasm[m[m
    -rw-r--r--   1 aidanlau  staff  155071 Aug 23 09:33 loginesample.png
    -rw-r--r--   1 aidanlau  staff   34239 Aug 23 09:33 logo.png
    drwxr-xr-x   3 aidanlau  staff      96 Aug 23 09:33 [34mnotebooks[m[m
    drwxr-xr-x  11 aidanlau  staff     352 Aug 23 09:33 [34mplatformer[m[m
    -rw-r--r--   1 aidanlau  staff  165794 Aug 23 09:33 postmanexample.png
    -rw-r--r--   1 aidanlau  staff  207818 Aug 23 09:33 sleep.png
    -rw-r--r--   1 aidanlau  staff  203861 Aug 23 09:33 stress.png
    -rw-r--r--   1 aidanlau  staff  168467 Aug 23 09:33 tracker1.png
    -rw-r--r--   1 aidanlau  staff  244703 Aug 23 09:33 waterfood.png
    -rw-r--r--   1 aidanlau  staff   12911 Aug 23 09:33 wireframe.png
    
    ./binary:
    total 10080
    -rw-r--r--  1 aidanlau  staff   37088 Aug 23 09:33 1.png
    -rw-r--r--  1 aidanlau  staff   39155 Aug 23 09:33 2.png
    -rw-r--r--  1 aidanlau  staff  145986 Aug 23 09:33 andgate.png
    -rw-r--r--  1 aidanlau  staff  221394 Aug 23 09:33 ascii_label.png
    -rw-r--r--  1 aidanlau  staff   82759 Aug 23 09:33 b.png
    -rw-r--r--  1 aidanlau  staff  322245 Aug 23 09:33 binary_math_conversion.png
    -rw-r--r--  1 aidanlau  staff  298587 Aug 23 09:33 binary_shift.png
    -rw-r--r--  1 aidanlau  staff   19526 Aug 23 09:33 codetable.png
    -rw-r--r--  1 aidanlau  staff   82392 Aug 23 09:33 color_block.png
    -rw-r--r--  1 aidanlau  staff  457749 Aug 23 09:33 color_code.png
    -rw-r--r--  1 aidanlau  staff  301661 Aug 23 09:33 elaboration_of_shift.png
    -rw-r--r--  1 aidanlau  staff   30647 Aug 23 09:33 halt.png
    -rw-r--r--  1 aidanlau  staff  121894 Aug 23 09:33 integer_math_neg.png
    -rw-r--r--  1 aidanlau  staff  125395 Aug 23 09:33 integer_math_pos.png
    -rw-r--r--  1 aidanlau  staff  419775 Aug 23 09:33 logic_gate_application.png
    -rw-r--r--  1 aidanlau  staff  536361 Aug 23 09:33 logic_gate_lab.png
    -rw-r--r--  1 aidanlau  staff  107742 Aug 23 09:33 logic_gates.png
    -rw-r--r--  1 aidanlau  staff  888227 Aug 23 09:33 logic_of_shift.png
    -rw-r--r--  1 aidanlau  staff   17921 Aug 23 09:33 problems.png
    -rw-r--r--  1 aidanlau  staff   38846 Aug 23 09:33 reverse.png
    -rw-r--r--  1 aidanlau  staff  373203 Aug 23 09:33 sample_unicode.png
    -rw-r--r--  1 aidanlau  staff  145986 Aug 23 09:33 truth.png
    -rw-r--r--  1 aidanlau  staff  245559 Aug 23 09:33 twos_complement.png
    -rw-r--r--  1 aidanlau  staff   55105 Aug 23 09:33 unsigned_addition.png
    
    ./course-brag:
    total 5504
    -rw-r--r--  1 aidanlau  staff  536162 Aug 23 09:33 ccr.png
    -rw-r--r--  1 aidanlau  staff  654211 Aug 23 09:33 csa.png
    -rw-r--r--  1 aidanlau  staff  311888 Aug 23 09:33 csa24.png
    -rw-r--r--  1 aidanlau  staff  680581 Aug 23 09:33 csp.png
    -rw-r--r--  1 aidanlau  staff  323986 Aug 23 09:33 csp24.png
    -rw-r--r--  1 aidanlau  staff  270084 Aug 23 09:33 csse.png
    -rw-r--r--  1 aidanlau  staff   27531 Aug 23 09:33 qr.png
    
    ./fullstack:
    total 80
    -rw-r--r--  1 aidanlau  staff  15371 Aug 23 09:33 newvars.png
    -rw-r--r--  1 aidanlau  staff   8035 Aug 23 09:33 quickSketch.png
    -rw-r--r--  1 aidanlau  staff  14073 Aug 23 09:33 variables.png
    
    ./jokes:
    total 3576
    -rw-r--r--  1 aidanlau  staff  1040469 Aug 23 09:33 debug.png
    -rw-r--r--  1 aidanlau  staff   245915 Aug 23 09:33 postman.png
    -rw-r--r--  1 aidanlau  staff   533869 Aug 23 09:33 run.png
    
    ./jpa-lesson-images:
    total 1480
    -rw-r--r--  1 aidanlau  staff   15657 Aug 23 09:33 columnName.jpg
    -rw-r--r--  1 aidanlau  staff   48430 Aug 23 09:33 email.jpg
    -rw-r--r--  1 aidanlau  staff   83139 Aug 23 09:33 haslastname.jpg
    -rw-r--r--  1 aidanlau  staff   85779 Aug 23 09:33 jpa.jpg
    -rw-r--r--  1 aidanlau  staff  201269 Aug 23 09:33 largeterminal.jpg
    -rw-r--r--  1 aidanlau  staff   62635 Aug 23 09:33 partial.jpg
    -rw-r--r--  1 aidanlau  staff   75480 Aug 23 09:33 postman.jpg
    -rw-r--r--  1 aidanlau  staff   42227 Aug 23 09:33 search2.jpg
    -rw-r--r--  1 aidanlau  staff   27237 Aug 23 09:33 userJpaRepositoryFile.jpg
    -rw-r--r--  1 aidanlau  staff   37602 Aug 23 09:33 userTable.jpg
    -rw-r--r--  1 aidanlau  staff   56784 Aug 23 09:33 walloftext.jpg
    
    ./kasm:
    total 272
    -rw-r--r--  1 aidanlau  staff  138312 Aug 23 09:33 kasmv2.png
    
    ./notebooks:
    total 0
    drwxr-xr-x  6 aidanlau  staff  192 Aug 23 09:33 [34mfoundation[m[m
    
    ./notebooks/foundation:
    total 728
    -rw-r--r--  1 aidanlau  staff  310743 Aug 23 09:33 create_repo.png
    -rw-r--r--  1 aidanlau  staff   29416 Aug 23 09:33 push.jpg
    -rw-r--r--  1 aidanlau  staff   17105 Aug 23 09:33 stage.jpg
    -rw-r--r--  1 aidanlau  staff    6659 Aug 23 09:33 wsl.jpg
    
    ./platformer:
    total 248
    -rw-r--r--   1 aidanlau  staff    841 Aug 23 09:33 1_lopez.png
    -rw-r--r--   1 aidanlau  staff   8525 Aug 23 09:33 Untitled drawing.png
    -rw-r--r--   1 aidanlau  staff  91596 Aug 23 09:33 background.png
    drwxr-xr-x  32 aidanlau  staff   1024 Aug 23 09:33 [34mbackgrounds[m[m
    -rw-r--r--   1 aidanlau  staff  15406 Aug 23 09:33 favicon.ico
    drwxr-xr-x  21 aidanlau  staff    672 Aug 23 09:33 [34mobstacles[m[m
    drwxr-xr-x  28 aidanlau  staff    896 Aug 23 09:33 [34mplatforms[m[m
    drwxr-xr-x  34 aidanlau  staff   1088 Aug 23 09:33 [34msprites[m[m
    drwxr-xr-x  11 aidanlau  staff    352 Aug 23 09:33 [34mtransitions[m[m
    
    ./platformer/backgrounds:
    total 21528
    -rw-r--r--  1 aidanlau  staff   989059 Aug 23 09:33 BossBackground.png
    -rw-r--r--  1 aidanlau  staff   916487 Aug 23 09:33 Congratulations!!!.png
    -rw-r--r--  1 aidanlau  staff    23764 Aug 23 09:33 avenidawide3.jpg
    -rw-r--r--  1 aidanlau  staff    10759 Aug 23 09:33 bat.png
    -rw-r--r--  1 aidanlau  staff    71134 Aug 23 09:33 castles.png
    -rw-r--r--  1 aidanlau  staff    32795 Aug 23 09:33 clouds.png
    -rw-r--r--  1 aidanlau  staff   180238 Aug 23 09:33 desertbg.png
    -rw-r--r--  1 aidanlau  staff    43261 Aug 23 09:33 devil.png
    -rw-r--r--  1 aidanlau  staff    61795 Aug 23 09:33 flyingplayers.png
    -rw-r--r--  1 aidanlau  staff    47684 Aug 23 09:33 game_over.png
    -rw-r--r--  1 aidanlau  staff    33177 Aug 23 09:33 greek.png
    -rw-r--r--  1 aidanlau  staff   232046 Aug 23 09:33 hills.png
    -rw-r--r--  1 aidanlau  staff   160593 Aug 23 09:33 home.png
    -rw-r--r--  1 aidanlau  staff    28317 Aug 23 09:33 icewater.png
    -rw-r--r--  1 aidanlau  staff   150548 Aug 23 09:33 mini.png
    -rw-r--r--  1 aidanlau  staff   258834 Aug 23 09:33 miniHogwarts.png
    -rw-r--r--  1 aidanlau  staff    29894 Aug 23 09:33 moon.jpg
    -rw-r--r--  1 aidanlau  staff   194001 Aug 23 09:33 mountains.jpg
    -rw-r--r--  1 aidanlau  staff  3804266 Aug 23 09:33 multiplayerbackground.png
    -rw-r--r--  1 aidanlau  staff   101005 Aug 23 09:33 narwhal.png
    -rw-r--r--  1 aidanlau  staff   663965 Aug 23 09:33 planet.jpg
    -rw-r--r--  1 aidanlau  staff   230522 Aug 23 09:33 podium.jpg
    -rw-r--r--  1 aidanlau  staff    48819 Aug 23 09:33 quidditch2.jpg
    -rw-r--r--  1 aidanlau  staff   328600 Aug 23 09:33 reef.png
    -rw-r--r--  1 aidanlau  staff   188425 Aug 23 09:33 school-fish.png
    -rw-r--r--  1 aidanlau  staff   863997 Aug 23 09:33 skibidiCompletion.png
    -rw-r--r--  1 aidanlau  staff      721 Aug 23 09:33 snowfall.png
    -rw-r--r--  1 aidanlau  staff   543088 Aug 23 09:33 springfield.png
    -rw-r--r--  1 aidanlau  staff   599642 Aug 23 09:33 water.png
    -rw-r--r--  1 aidanlau  staff   118454 Aug 23 09:33 winter.png
    
    ./platformer/obstacles:
    total 1720
    -rw-r--r--  1 aidanlau  staff   81268 Aug 23 09:33 Chest.png
    -rw-r--r--  1 aidanlau  staff   33120 Aug 23 09:33 Trident.png
    -rw-r--r--  1 aidanlau  staff   25554 Aug 23 09:33 blue-tube-up.png
    -rw-r--r--  1 aidanlau  staff   25477 Aug 23 09:33 blue-tube.png
    -rw-r--r--  1 aidanlau  staff   32653 Aug 23 09:33 cabin.png
    -rw-r--r--  1 aidanlau  staff   16925 Aug 23 09:33 coin.png
    -rw-r--r--  1 aidanlau  staff   23107 Aug 23 09:33 coinanimation.png
    -rw-r--r--  1 aidanlau  staff   43191 Aug 23 09:33 dimonds.png
    -rw-r--r--  1 aidanlau  staff   66987 Aug 23 09:33 flag.png
    -rw-r--r--  1 aidanlau  staff   24701 Aug 23 09:33 iceberg.png
    -rw-r--r--  1 aidanlau  staff    7163 Aug 23 09:33 laser.png
    -rw-r--r--  1 aidanlau  staff   11955 Aug 23 09:33 snitch.png
    -rw-r--r--  1 aidanlau  staff   22801 Aug 23 09:33 snowflake.png
    -rw-r--r--  1 aidanlau  staff   19408 Aug 23 09:33 star.png
    -rw-r--r--  1 aidanlau  staff   60071 Aug 23 09:33 toilet.png
    -rw-r--r--  1 aidanlau  staff  248218 Aug 23 09:33 tree.png
    -rw-r--r--  1 aidanlau  staff   29442 Aug 23 09:33 tube.png
    -rw-r--r--  1 aidanlau  staff   21876 Aug 23 09:33 vbucks.png
    -rw-r--r--  1 aidanlau  staff   48319 Aug 23 09:33 whompingwillowtree.png
    
    ./platformer/platforms:
    total 4688
    -rw-r--r--  1 aidanlau  staff     8474 Aug 23 09:33 Chocolatefrog.jpg
    -rw-r--r--  1 aidanlau  staff    75783 Aug 23 09:33 alien.png
    -rw-r--r--  1 aidanlau  staff    41211 Aug 23 09:33 brick_block.png
    -rw-r--r--  1 aidanlau  staff     2782 Aug 23 09:33 brick_wall.png
    -rw-r--r--  1 aidanlau  staff    10690 Aug 23 09:33 bubbles.png
    -rw-r--r--  1 aidanlau  staff     6537 Aug 23 09:33 cobblestone.png
    -rw-r--r--  1 aidanlau  staff    26145 Aug 23 09:33 grass.png
    -rw-r--r--  1 aidanlau  staff    56810 Aug 23 09:33 ground.png
    -rw-r--r--  1 aidanlau  staff    15969 Aug 23 09:33 island.png
    -rw-r--r--  1 aidanlau  staff    84023 Aug 23 09:33 lava.jpg
    -rw-r--r--  1 aidanlau  staff    23906 Aug 23 09:33 lionpattern.jpg
    -rw-r--r--  1 aidanlau  staff   143056 Aug 23 09:33 magic_beam.png
    -rw-r--r--  1 aidanlau  staff    66332 Aug 23 09:33 mario_block_spritesheet_v2.png
    -rw-r--r--  1 aidanlau  staff    27915 Aug 23 09:33 mushroom.png
    -rw-r--r--  1 aidanlau  staff     4921 Aug 23 09:33 narwhalfloor.png
    -rw-r--r--  1 aidanlau  staff   115313 Aug 23 09:33 rockslava.png
    -rw-r--r--  1 aidanlau  staff    64074 Aug 23 09:33 sand.png
    -rw-r--r--  1 aidanlau  staff      298 Aug 23 09:33 sandblock.png
    -rw-r--r--  1 aidanlau  staff     8076 Aug 23 09:33 sandstone.png
    -rw-r--r--  1 aidanlau  staff    55870 Aug 23 09:33 skibidiBlock.png
    -rw-r--r--  1 aidanlau  staff   330989 Aug 23 09:33 snowyfloor.png
    -rw-r--r--  1 aidanlau  staff     7447 Aug 23 09:33 snowywood.png
    -rw-r--r--  1 aidanlau  staff    39059 Aug 23 09:33 stone.jpg
    -rw-r--r--  1 aidanlau  staff  1092399 Aug 23 09:33 turf.png
    -rw-r--r--  1 aidanlau  staff    27827 Aug 23 09:33 yellowredpattern.jpg
    -rw-r--r--  1 aidanlau  staff    17518 Aug 23 09:33 yellowtowerpattern.jpg
    
    ./platformer/sprites:
    total 17232
    -rw-r--r--  1 aidanlau  staff    38055 Aug 23 09:33 alert.gif
    -rw-r--r--  1 aidanlau  staff    51640 Aug 23 09:33 alien.png
    -rw-r--r--  1 aidanlau  staff   120450 Aug 23 09:33 boss.png
    -rw-r--r--  1 aidanlau  staff     6736 Aug 23 09:33 canelopezspritesheet.png
    -rw-r--r--  1 aidanlau  staff     3167 Aug 23 09:33 cerberus.png
    -rw-r--r--  1 aidanlau  staff   103701 Aug 23 09:33 dementor2.png
    -rw-r--r--  1 aidanlau  staff    49625 Aug 23 09:33 dracomalfoy.png
    -rw-r--r--  1 aidanlau  staff    24281 Aug 23 09:33 dragon.png
    -rw-r--r--  1 aidanlau  staff   141829 Aug 23 09:33 escaper.png
    -rw-r--r--  1 aidanlau  staff   121796 Aug 23 09:33 flying-goomba.png
    -rw-r--r--  1 aidanlau  staff   356155 Aug 23 09:33 flying-ufo.png
    -rw-r--r--  1 aidanlau  staff   121815 Aug 23 09:33 goomba.png
    -rw-r--r--  1 aidanlau  staff    91068 Aug 23 09:33 goombaspritesheet.png
    -rw-r--r--  1 aidanlau  staff    14232 Aug 23 09:33 harryanimation2.png
    -rw-r--r--  1 aidanlau  staff    15902 Aug 23 09:33 harryanimation3.png
    -rw-r--r--  1 aidanlau  staff    15969 Aug 23 09:33 island.png
    -rw-r--r--  1 aidanlau  staff   164132 Aug 23 09:33 jellyfish.png
    -rw-r--r--  1 aidanlau  staff   162387 Aug 23 09:33 knight.png
    -rw-r--r--  1 aidanlau  staff    17116 Aug 23 09:33 lopezanimation.png
    -rw-r--r--  1 aidanlau  staff     6609 Aug 23 09:33 lopezspritesheet3.png
    -rwxr-xr-x  1 aidanlau  staff  3851947 Aug 23 09:33 [31mmario.png[m[m
    -rw-r--r--  1 aidanlau  staff   111425 Aug 23 09:33 monkey.png
    -rw-r--r--  1 aidanlau  staff    49605 Aug 23 09:33 narwhal_boss.png
    -rw-r--r--  1 aidanlau  staff   181376 Aug 23 09:33 noirio.png
    -rw-r--r--  1 aidanlau  staff    59931 Aug 23 09:33 owl.png
    -rw-r--r--  1 aidanlau  staff    23940 Aug 23 09:33 penguin.png
    -rw-r--r--  1 aidanlau  staff   457104 Aug 23 09:33 skibidiEnemy.png
    -rw-r--r--  1 aidanlau  staff   155875 Aug 23 09:33 skibidiTItan.png
    -rw-r--r--  1 aidanlau  staff    26141 Aug 23 09:33 snowman.png
    -rw-r--r--  1 aidanlau  staff  1683899 Aug 23 09:33 white_mario.png
    -rw-r--r--  1 aidanlau  staff   376506 Aug 23 09:33 white_mario1.png
    -rw-r--r--  1 aidanlau  staff   152460 Aug 23 09:33 zombie.png
    
    ./platformer/transitions:
    total 9512
    -rw-r--r--  1 aidanlau  staff  123315 Aug 23 09:33 IceMinigameEnd.png
    -rw-r--r--  1 aidanlau  staff  750112 Aug 23 09:33 greeceEnd.png
    -rw-r--r--  1 aidanlau  staff   20774 Aug 23 09:33 greenscreen.png
    -rw-r--r--  1 aidanlau  staff  951532 Aug 23 09:33 hillsEnd.png
    -rw-r--r--  1 aidanlau  staff  211655 Aug 23 09:33 hogwartsminiEnd.jpg
    -rw-r--r--  1 aidanlau  staff  859809 Aug 23 09:33 miniEnd.png
    -rw-r--r--  1 aidanlau  staff  917436 Aug 23 09:33 quidditchEnd.png
    -rw-r--r--  1 aidanlau  staff  917788 Aug 23 09:33 waterEnd.png
    -rw-r--r--  1 aidanlau  staff   94865 Aug 23 09:33 winterEnd.png


### Look inside a Markdown File
> "cat" reads data from the file and gives its content as output


```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Navigate to project, then navigate to area wwhere files were cloned"

cd $project
echo "show the contents of README.md"
echo ""

cat README.md  # show contents of file, in this case markdown
echo ""
echo "end of README.md"

```

    Navigate to project, then navigate to area wwhere files were cloned
    show the contents of README.md
    
    # Introduction
    
    Nighthawk Pages is a project designed to support students in their Computer Science and Software Engineering education. It offers a wide range of resources including tech talks, code examples, and educational blogs.
    
    GitHub Pages can be customized by the blogger to support computer science learnings as the student works through the pathway of using Javascript, Python/Flask, Java/Spring.  
    
    ## Student Requirements
    
    Del Norte HS students will be required to review their personal GitHub Pages at each midterm and final.  This review will contain a compilation of personal work performed within each significant grading period.
    
    In general, Students and Teachers are expected to use GitHub pages to build lessons, complete classroom hacks, perform work on JavaScript games, and serve as a frontend to full-stack applications.
    
    Exchange of information could be:
    
    1. sharing a file:  `wget "raw-link.ipynb"
    2. creating a template from this repository
    3. sharing a fork among team members
    4. etc.
    
    ---
    
    ## History
    
    This project is in its 3rd revision (aka 3.0).
    
    The project was initially based on Fastpages. But this project has diverged from those roots into an independent entity.  The decision to separate from Fastpages was influenced by the deprecation of Fastpages by authors.  It is believed by our community that the authors of fastpages turned toward Quatro.  After that change of direction fastpages did not align with the Teacher's goals and student needs. The Nighthawk Pages project has more of a raw development blogging need.
    
    ### License
    
    The Apache license has its roots in Fastpages.  Thus, it carries its license forward.  However, most of the code is likely unrecognizable from those roots.
    
    ### Key Features
    
    - **Code Examples**: Provides practical coding examples in JavaScript, including a platformer game, and frontend code for user databases using Python and Java backends.
    - **Educational Blogs**: Offers instructional content on various topics such as developer tools setup, deployment on AWS, SQL databases, machine learning, and data structures. It utilizes Jupyter Notebooks for interactive lessons and coding challenges.
    - **Tools and Integrations**: Features GitHub actions for blog publishing, Utterances for blog commenting, local development support via Makefile and scripts, and styling with the Minima Theme and SASS. It also includes a new integration with GitHub Projects and Issues.
    
    ### Contributions
    
    - **Notable Contributions**: Highlights significant contributions to the project, including theme development, search and tagging functionality, GitHub API integration, and the incorporation of GitHub Projects into GitHub pages. Contributors such as Tirth Thakker, Mirza Beg, and Toby Ledder have played crucial roles in these developments.
    
    - **Blog Contributions**:  Often students contribute articles and blogs to this project.  Their names are typically listed in the front matter of their contributing post.
    
    ---
    
    ## GitHub Pages setup
    
    The absolutes in setup up...
    
    **Activate GitHub Pages Actions**: This step involves enabling GitHub Pages Actions for your project. By doing so, your project will be automatically deployed using GitHub Pages Actions, ensuring that your project is always up to date with the latest changes you push to your repository.
    
    - On the GitHub website for the repository go to the menu: Settings -> Pages ->Build
    - Under the Deployment location on the page, select "GitHub Actions".
    
    **Update `_config.yml`**: You need to modify the `_config.yml` file to reflect your repository's name. This configuration is crucial because it ensures that your project's styling is correctly applied, making your deployed site look as intended rather than unstyled or broken.
    
    ```text
    github_repo: "portfolio_2025" 
    baseurl: "/portfolio_2025"
    ```
    
    **Set Repository Name in Makefile**: Adjust the `REPO_NAME` variable in your Makefile to match your GitHub repository's name. This action facilitates the automatic updating of posts and notebooks on your local development server, improving the development process.
    
    ```make
    # Configuration, override port with usage: make PORT=4200
    PORT ?= 4100
    REPO_NAME ?= portfolio_2025
    LOG_FILE = /tmp/jekyll$(PORT).log
    ```
    
    ### Tool requirements
    
    All `GitHub Pages` websites are managed on GitHub infrastructure and use GitHub version control.  Each time we change files in GitHub it initiates a GitHub Action, a continuous integration and development toolset, that rebuilds and publishes the site with Jekyll.  
    
    - GitHub uses `Jekyll` to transform your markdown and HTML content into static websites and blogs. [Jekyll](https://jekyllrb.com/).
    - A Linux shell is required to work with this project integration with GitHub Pages, GitHub and VSCode.  Ubuntu is the preferred shell, though MacOS shell is supported as well.  There will be some key setup scripts that follow in the README.
    - Visual Studio Code is the Nighthawk Pages author's preferred code editor and extensible development environment.  VSCode has a rich ecosystem of developer extensions that ease working with GitHub Pages, GitHub, and many programming languages.  Setting up VSCode and extensions will be elaborated upon in this document.
    - An anatomy section in this README will describe GitHub Pages and conventions that are used to organize content and files.  This includes file names, key coding files, metadata tagging of blogs, styling tooling for blogs, etc.
    
    ### Development Environment Setup
    
    Comprehensive start. A topic-by-topic guide to getting this project running is published [here](https://nighthawkcoders.github.io/portfolio_2025/devops/tools/home).
    
    Quick start.  A quick start below is a reminder, but is dependent on your knowledge.  Only follow this instruction if you need a refresher.  Always default to the comprehensive start if any problem occurs.
    
    #### Clone Repo
    
    Run these commands to obtain the project, then locate into the project directory with the terminal, install an extensive set of tools, and make.
    
    ```bash
    git clone <this-repo> # git clone https://github.com/nighthawkcoders/portfolio_2025.git 
    cd <repo-dir>/scripts # cd portfolio_2025
    ```
    
    #### Windows WSL and/or Ubuntu Users
    
    - Execute the script: `./activate_ubuntu.sh`
    
    #### macOS Users
    
    - Execute the script: `./activate_macos.sh`
    
    #### Kasm Cloud Desktop Users
    
    - Execute the script: `./activate.sh`
    
    ## Run Server on localhost
    
    To preview the project you will need to "make" the project.
    
    ### Bundle install
    
    The very first time you clone run project you will need to run this Ruby command as the final part of your setup.
    
    ```bash
    bundle install
    ```
    
    ### Start the Server  
    
    This requires running terminal commands `make`, `make stop`, `make clean`, or `make convert` to manage the running server.  Logging of details will appear in the terminal.   A `Makefile` has been created in the project to support commands and start processes.
    
    Start the server, this is the best choice for initial and iterative development.  Note. after the initial `make`, you should see files automatically refresh in the terminal on VSCode save.
    
      ```bash
      make
      ```
    
    ### Load web application into the Browser
    
    Start the preview server in the terminal,
    The terminal output from `make` shows the server address. "Cmd" or "Ctl" click the http location to open the preview server in a browser. Here is an example Server address message, click on the Server address to load:...
    
      ```text
      http://0.0.0.0:4100/portfolio_2025/
      ```
    
    ### Regeneration of web application
    
    Save on ".ipynb" or ".md" file activiates "regeneration". An example terminal message is below.  Refresh the browser to see updates after the message displays.
    
      ```text
      Regenerating: 1 file(s) changed at 2023-07-31 06:54:32
          _notebooks/2024-01-04-cockpit-setup.ipynb
      ```
    
    ### Other "make" commands
    
    Terminal messages are generated from background processes.  At any time, click return or enter in a terminal window to obtain a prompt.  Once you have the prompt you can use the terminal as needed for other tasks.  Always return to the root of project `cd ~/vscode/portfolio_2025` for all "make" actions.
    
    #### Stop the preview server
    
    Stopping the server ends the web server applications running process.  However, it leaves constructed files in the project in a ready state for the next time you run `make`.
    
      ```bash
      make stop
      ```
    
    ### Clean the local web application environment
    
    This command will top the server and "clean" all previously constructed files (ie .ipynb -> .md). This is the best choice when renaming files has created duplicates that are visible when previewing work.
    
      ```bash
      make clean
      ```
    
    ### Observe build errors
    
    Test Jupyter Notebook conversions (ie .ipynb -> .md), this is the best choice to see if an IPYNB conversion error is occurring.
    
      ```bash
      make convert
      ```
    
    ---
    
    ## Development Support
    
    ### File Names in "_posts", "_notebooks"
    
    There are two primary directories for creating blogs.  The "_posts" directory is for authoring in markdown only.  The "_notebooks" allows for markdown, pythons, javascript and more.
    
    To name a file, use the following structure (If dates are in the future, review your config.yml setting if you want them to be viewed).  Review these naming conventions.
    
    - For markdown files in _posts:
      - year-month-day-fileName.md
        - GOOD EXAMPLE: 2021-08-02-First-Day.md
        - BAD EXAMPLE: 2021-8-2-first-day.md
        - BAD EXAMPLE: first-day.md
        - BAD EXAMPLE: 2069-12-31-First-Day.md
    
    - For Jupyter notebooks in _notebooks:
      - year-month-day-fileName.ipynb
        - GOOD EXAMPLE: 2021-08-02-First-Day.ipynb
        - BAD EXAMPLE: 2021-8-2-first-day.ipynb
        - BAD EXAMPLE: first-day.ipynb
        - BAD EXAMPLE: 2069-12-31-First-Day.ipynb
    
    ### Tags
    
    Tags are used to organize pages by their tag the way to add tags is to add the following to your front matter such as the example seen here `categories: [Tools]` Each item in the same category will be lumped together to be seen easily on the search page.
    
    ### Search
    
    All pages can be searched for using the built-in search bar. This search bar will search for any word in the title of a page or in the page itself. This allows for easily finding pages and information that you are looking for. However, sometimes this may not be desirable so to hide a page from the search you need to add `search_exclude: true` to the front matter of the page. This will hide the page from appearing when the viewer uses search.
    
    ### Navigation Bar
    
    To add pages to the top navigation bar use _config.yml to order and determine which menus you want and how to order them.  Review the_config.yml in this project for an example.
    
    ### Blog Page
    
    There is a blog page that has options for images and a description of the page. This page can help the viewer understand what the page is about and what they can expect to find on the page. The way to add images to a page is to have the following front matter `image: /images/file.jpg` and then the name of the image that you want to use. The image must be in the `images` folder. Furthermore, if you would like the file to not show up on the blog page `hide: true` can be added to the front matter.
    
    ### SASS support
    
    NIGHTHAWK Pages support a variety of different themes that are each overlaid on top of minima. To use each theme, go to the "_sass/minima/custom-styles.scss" file and simply comment or uncomment the theme you want to use.
    
    To learn about the minima themes search for "GitHub Pages minima" and review the README.
    
    To find a new theme search for "Github Pages Themes".
    
    ### Includes
    
    - Nighthawk Pages uses liquid syntax to import many common page elements that are present throughout the repository. These common elements are imported from the _includes directory. If you want to add one of these common elements, use liquid syntax to import the desired element to your file. Here’s an example of the liquid syntax used to import: `{%- include post_list.html -%}` Note that the liquid syntax is surrounded by curly braces and percent signs. This can be used anywhere in the repository.
    
    ### Layouts
    
    - To use or create a custom page layout, make an HTML page inside the _layouts directory, and when you want to use that layout in a file, use the following front matter `layout: [your layout here]`.  All layouts will be written in liquid to define the structure of the page.
    
    ### Metadata
    
    Metadata, also known as "front matter", is a set of key-value pairs that can provide additional information to GitHub Pages about .md and .ipynb files. This can and probably will be used in other file types (ie doc, pdf) if we add them to the system.
    
    In the front matter, you can also define things like a title and description for the page.  Additional front matter is defined to place content on the "Computer Science Lab Notebook" page.  The `courses:` key will place data on a specific page with the nested `week:` placing data on a specific row on the page.  The `type:` key in "front matter" will place the blog under the plans, hacks(ToDo), and tangibles columns.
    
    - In our files, the front matter is defined at the top of the page or the first markdown cell.
    
      - First, open one of the .md or .ipynb files already included in either your _posts|_notebooks folder.
    
      - In the .md file, you should notice something similar to this at the top of the page. To see this in your .ipynb files you will need to double-click the markdown cell at the top of the file.
    
      ```yaml
      ---
      toc: true
      comments: true
      layout: post
      title: Jupyter Python Sample
      description: Example Blog!!!  This shows code and notes from hacks.
      type: ccc
      courses: { csa: {week: 5} }
      ---
      ```
    
    - The front matter will always have '---' at the top and bottom to distinguish it and each key-value pair will be separated by a ':'.
    
    - Here we can modify things like the title and description.
    
    - The type value will tell us which column this is going to appear under the time box supported pages.  The "ccc" stands for Code, Code, Code.
    
    - The courses will tell us which menu item it will be under, in this case, the `csa` menu, and the `week` tells it what row (week) it will appear under that menu.
    
    end of README.md


## Env, Git, and GitHub

> Env(ironment) is used to capture things like the path to the Code or Home directory. Git and GitHub are not only used to exchange code between individuals but are also often used to exchange code through servers, in our case for website deployment. All tools we use have behind-the-scenes relationships with the system they run on (MacOS, Windows, Linux) or a relationship with servers to which they are connected (e.g., GitHub). There is an "env" command in bash. There are environment files and setting files (e.g., `.git/config`) for Git. They both use a key/value concept.

- `env` shows settings for your shell.
- `git clone` sets up a directory of files.
- `cd $project` allows the user to move inside that directory of files.
- `.git` is a hidden directory that is used by Git to establish a relationship between the machine and the Git server on GitHub.


```python
%%script bash

# This command has no dependencies

echo "Show the shell environment variables, key on left of equal value on right"
echo ""

env
```

    Show the shell environment variables, key on left of equal value on right
    
    MANPATH=/opt/homebrew/share/man::
    VSCODE_CRASH_REPORTER_PROCESS_TYPE=extensionHost
    GEM_HOME=/Users/aidanlau/gems
    TERM=xterm-color
    SHELL=/bin/zsh
    CLICOLOR=1
    TMPDIR=/var/folders/wq/3kh_gm3s1ng_p6ms613g7_zc0000gn/T/
    HOMEBREW_REPOSITORY=/opt/homebrew
    CONDA_SHLVL=1
    PYTHONUNBUFFERED=1
    CONDA_PROMPT_MODIFIER=(base) 
    ORIGINAL_XDG_CURRENT_DESKTOP=undefined
    MallocNanoZone=0
    PYDEVD_USE_FRAME_EVAL=NO
    PYTHONIOENCODING=utf-8
    USER=aidanlau
    COMMAND_MODE=unix2003
    CONDA_EXE=/opt/homebrew/anaconda3/bin/conda
    SSH_AUTH_SOCK=/private/tmp/com.apple.launchd.gAQ1qXHCGu/Listeners
    __CF_USER_TEXT_ENCODING=0x1F5:0x0:0x0
    PAGER=cat
    ELECTRON_RUN_AS_NODE=1
    VSCODE_AMD_ENTRYPOINT=vs/workbench/api/node/extensionHostProcess
    _CE_CONDA=
    CONDA_ROOT=/opt/homebrew/anaconda3
    PATH=/opt/homebrew/anaconda3/bin:/opt/homebrew/anaconda3/condabin:/Users/aidanlau/gems/bin:/Users/aidanlau/.rbenv/shims:/Users/aidanlau/gems/bin:/Users/aidanlau/gems/bin:/Users/aidanlau/gems/bin:/Users/aidanlau/.rbenv/shims:/Users/aidanlau/gems/bin:/Users/aidanlau/gems/bin:/Users/aidanlau/.rbenv/shims:/Users/aidanlau/.rbenv/shims:/Users/aidanlau/.rbenv/shims:/opt/homebrew/opt/python@3/libexec/bin:/Users/aidanlau/.rbenv/shims:/Users/aidanlau/gems/bin:/opt/homebrew/bin:/opt/homebrew/sbin:/usr/local/bin:/System/Cryptexes/App/usr/bin:/usr/bin:/bin:/usr/sbin:/sbin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/local/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/appleinternal/bin:/Library/Frameworks/Mono.framework/Versions/Current/Commands
    CONDA_PREFIX=/opt/homebrew/anaconda3
    __CFBundleIdentifier=com.microsoft.VSCode
    PWD=/Users/aidanlau/Downloads/vscode/CSAstudent/_notebooks/Foundation/B-tools_and_equipment
    VSCODE_HANDLES_UNCAUGHT_ERRORS=true
    MPLBACKEND=module://matplotlib_inline.backend_inline
    PYTHON_FROZEN_MODULES=on
    XPC_FLAGS=0x0
    FORCE_COLOR=1
    RBENV_SHELL=zsh
    _CE_M=
    XPC_SERVICE_NAME=0
    SHLVL=3
    HOME=/Users/aidanlau
    APPLICATION_INSIGHTS_NO_DIAGNOSTIC_CHANNEL=1
    VSCODE_NLS_CONFIG={"userLocale":"en-us","osLocale":"en-us","resolvedLanguage":"en","defaultMessagesFile":"/Applications/Visual Studio Code.app/Contents/Resources/app/out/nls.messages.json","locale":"en","availableLanguages":{}}
    PYDEVD_IPYTHON_COMPATIBLE_DEBUGGING=1
    HOMEBREW_PREFIX=/opt/homebrew
    CONDA_ALLOW_SOFTLINKS=false
    CONDA_PYTHON_EXE=/opt/homebrew/anaconda3/bin/python
    LOGNAME=aidanlau
    LC_CTYPE=UTF-8
    VSCODE_IPC_HOOK=/Users/aidanlau/Library/Application Support/Code/1.92-main.sock
    VSCODE_CODE_CACHE_PATH=/Users/aidanlau/Library/Application Support/Code/CachedData/fee1edb8d6d72a0ddff41e5f71a671c23ed924b9
    CLICOLOR_FORCE=1
    CONDA_DEFAULT_ENV=base
    VSCODE_PID=53575
    INFOPATH=/opt/homebrew/share/info:
    HOMEBREW_CELLAR=/opt/homebrew/Cellar
    GIT_PAGER=cat
    VSCODE_CWD=/
    _=/usr/bin/env



```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

cd $project

echo ""
echo "show the secrets of .git config file"
cd .git
ls -l config

echo ""
echo "look at config file"
cat config
```

    
    show the secrets of .git config file
    -rw-r--r--  1 aidanlau  staff  311 Aug 23 09:33 config
    
    look at config file
    [core]
    	repositoryformatversion = 0
    	filemode = true
    	bare = false
    	logallrefupdates = true
    	ignorecase = true
    	precomposeunicode = true
    [remote "origin"]
    	url = https://github.com/AidanLau10/teacher2025.git
    	fetch = +refs/heads/*:refs/remotes/origin/*
    [branch "main"]
    	remote = origin
    	merge = refs/heads/main


## Advanced Shell project

> This example was requested by a student (Jun Lim, CSA). The request was to make a Jupyter file using bash; I adapted the request to markdown. This type of thought will have great extrapolation to coding and possibilities of using Lists, Arrays, or APIs to build user interfaces. JavaScript is a language where building HTML is very common.

> To get more interesting output from the terminal, this will require using something like mdless (https://github.com/ttscoff/mdless). This enables seeing markdown in rendered format.
- On Desktop [Install PKG from MacPorts](https://www.macports.org/install.php)
- In Terminal on MacOS
    - [Install ncurses](https://ports.macports.org/port/ncurses/)
    - ```gem install mdless```
    
> Output of the example is much nicer in "Jupyter"

This is starting the process of documentation.


```python
%%script bash

# This example has an error in VSCode; it runs best on Jupyter
cd /tmp

file="sample.md"
if [ -f "$file" ]; then
    rm $file
fi

# Create a markdown file using tee and here document (<<EOF)
tee -a $file >/dev/null <<EOF
# Show Generated Markdown
This introductory paragraph and this line and the title above are generated using tee with the standard input (<<) redirection operator.
- This bulleted element is still part of the tee body.
EOF

# Append additional lines to the markdown file using echo and redirection (>>)
echo "- This bulleted element and lines below are generated using echo with standard output (>>) redirection operator." >> $file
echo "- The list definition, as is, is using space to separate lines. Thus the use of commas and hyphens in output." >> $file

# Define an array of actions and their descriptions
actions=("ls,list-directory" "cd,change-directory" "pwd,present-working-directory" "if-then-fi,test-condition" "env,bash-environment-variables" "cat,view-file-contents" "tee,write-to-output" "echo,display-content-of-string" "echo_text_>\$file,write-content-to-file" "echo_text_>>\$file,append-content-to-file")

# Loop through the actions array and append each action to the markdown file
for action in ${actions[@]}; do
  action=${action//-/ }  # Convert dash to space
  action=${action//,/: } # Convert comma to colon
  action=${action//_text_/ \"sample text\" } # Convert _text_ to "sample text", note escape character \ to avoid "" having meaning
  echo "    - ${action//-/ }" >> $file  # Append action to file
done

echo ""
echo "File listing and status"
ls -l $file # List file details
wc $file   # Show word count
mdless $file  # Render markdown from terminal (requires mdless installation)

rm $file  # Clean up temporary file
```

    
    File listing and status
    -rw-r--r--  1 aidanlau  wheel  808 Aug 23 09:33 sample.md
          15     132     808 sample.md
    
    
    [0;37m[0;1;90;47mShow Generated Markdown [0;2;30;47m======================================================[0;37m
    
    [0;37mThis introductory paragraph and this line and the title above are generated using tee with the standard input (<<) redirection operator.[0;37m
    
     [0;1;91m* [0;97mThis bulleted element is still part of the tee body.[0;37m
     [0;1;91m* [0;97mThis bulleted element and lines below are generated using echo with standard output (>>) redirection operator.[0;37m
     [0;1;91m* [0;97mThe list definition, as is, is using space to separate lines. Thus the use of commas and hyphens in output.
       [0;1;91m* [0;97mls: list directory[0;97m
       [0;1;91m* [0;97mcd: change directory[0;97m
       [0;1;91m* [0;97mpwd: present working directory[0;97m
       [0;1;91m* [0;97mif then fi: test condition[0;97m
       [0;1;91m* [0;97menv: bash environment variables[0;97m
       [0;1;91m* [0;97mcat: view file contents[0;97m
       [0;1;91m* [0;97mtee: write to output[0;97m
       [0;1;91m* [0;97mecho: display content of string[0;97m
       [0;1;91m* [0;97mecho "sample text" >$file: write content to file[0;97m
       [0;1;91m* [0;97mecho "sample text" >>$file: append content to file[0;97m[0;37m
    
    [0m

## Display Shell commands help using `man`

> The previous example used a markdown file to store a list of actions and their descriptions. This example uses the `man` command to generate a markdown file with descriptions of the commands. The markdown file is then displayed using `mdless`.

In coding, we should try to get data from the content creators instead of creating it on our own. This approach has several benefits:
- **Accuracy**: Descriptions from `man` pages are authoritative and accurate, as they come directly from the documentation provided by the command's developers.
- **Consistency**: Automatically generating descriptions ensures consistency in formatting and terminology.
- **Efficiency**: It saves time and effort, especially when dealing with a large number of commands.
- **Up-to-date Information**: `man` pages are regularly updated with the latest information, ensuring that the descriptions are current.


```python
%%script bash

# This example has an error in VSCode; it runs best on Jupyter
cd /tmp

file="sample.md"
if [ -f "$file" ]; then
    rm $file
fi

# Set locale to C to avoid locale-related errors
export LC_ALL=C

# Create a markdown file using tee and here document (<<EOF)
tee -a $file >/dev/null <<EOF
# Show Generated Markdown
This introductory paragraph and this line and the title above are generated using tee with the standard input (<<) redirection operator.
- This bulleted element is still part of the tee body.
EOF

# Append additional lines to the markdown file using echo and redirection (>>)
echo "- This bulleted element and lines below are generated using echo with standard output (>>) redirection operator." >> $file
echo "- The list definition, as is, is using space to separate lines. Thus the use of commas and hyphens in output." >> $file

# Define an array of commands
commands=("ls" "cat" "tail" "pwd" "env" "grep" "awk" "sed" "curl" "wget")

# Loop through the commands array and append each command description to the markdown file
for cmd in ${commands[@]}; do
  description=$(man $cmd | col -b | awk '/^NAME/{getline; print}')
  echo "    - $description" >> $file
done

echo ""
echo "File listing and status"
ls -l $file # List file details
wc $file   # Show word count
mdless $file  # Render markdown from terminal (requires mdless installation)

rm $file  # Clean up temporary file
```

    
    File listing and status
    -rw-r--r--  1 aidanlau  wheel  972 Aug 23 09:34 sample.md
          15     151     972 sample.md
    
    
    [0;37m[0;1;90;47mShow Generated Markdown [0;2;30;47m======================================================[0;37m
    
    [0;37mThis introductory paragraph and this line and the title above are generated using tee with the standard input (<<) redirection operator.[0;37m
    
     [0;1;91m* [0;97mThis bulleted element is still part of the tee body.[0;37m
     [0;1;91m* [0;97mThis bulleted element and lines below are generated using echo with standard output (>>) redirection operator.[0;37m
     [0;1;91m* [0;97mThe list definition, as is, is using space to separate lines. Thus the use of commas and hyphens in output.
       [0;1;91m* [0;97mls - list directory contents[0;97m
       [0;1;91m* [0;97mcat - concatenate and print files[0;97m
       [0;1;91m* [0;97mtail - display the last part of a file[0;97m
       [0;1;91m* [0;97mpwd - return working directory name[0;97m
       [0;1;91m* [0;97menv - set environment and execute command, or print environment[0;97m
       [0;1;91m* [0;97mgrep, egrep, fgrep, rgrep, bzgrep, bzegrep, bzfgrep, zgrep, zegrep,[0;97m
       [0;1;91m* [0;97mawk - pattern-directed scanning and processing language[0;97m
       [0;1;91m* [0;97msed - stream editor[0;97m
       [0;1;91m* [0;97mcurl - transfer a URL[0;97m
       [0;1;91m* [0;97mWget - The non-interactive network downloader.[0;97m[0;37m
    
    [0m

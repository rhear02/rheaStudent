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
export project_dir=$HOME/rhearajashekhar/vscode  # change nighthawk to different name to test your git clone
export project=\$project_dir/rheaStudent  # change student_2025 to name of project from git clone
export project_repo="https://github.com/nighthawkcoders/rheaStudent.git"  # change to project you created from portfolio_2025 template 
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

    Project dir: /Users/rhearajashekhar/rhearajashekhar/vscode
    Project: /Users/rhearajashekhar/rhearajashekhar/vscode/rheaStudent
    Repo: https://github.com/nighthawkcoders/rheaStudent.git


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
    Directory /Users/rhearajashekhar/rhearajashekhar/vscode exists.
    Directory /Users/rhearajashekhar/rhearajashekhar/vscode/rheaStudent does not exist... cloning https://github.com/nighthawkcoders/rheaStudent.git


    Cloning into 'rheaStudent'...
    remote: Repository not found.
    fatal: repository 'https://github.com/nighthawkcoders/rheaStudent.git/' not found


    Directory /Users/rhearajashekhar/rhearajashekhar/vscode/rheaStudent exists.


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


    bash: line 6: cd: /Users/rhearajashekhar/rhearajashekhar/vscode/rheaStudent: No such file or directory


    /Users/rhearajashekhar/vscode/rheaStudent/_notebooks/Foundation/B-tools_and_equipment
    
    list top level or root of files with project pulled from github
    2023-08-19-devops_accounts.ipynb
    2023-08-21-devops_tools-home.ipynb
    2023-08-21-devops_tools-setup.ipynb
    2023-08-22-devops_tools-verify.ipynb
    2023-08-23-devops-githhub_pages-play.ipynb
    2023-08-23-devops-hacks.ipynb


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


    bash: line 6: cd: /Users/rhearajashekhar/rhearajashekhar/vscode/rheaStudent: No such file or directory


    /Users/rhearajashekhar/vscode/rheaStudent/_notebooks/Foundation/B-tools_and_equipment
    
    list all files in long format
    total 248
    drwxr-xr-x  8 rhearajashekhar  staff    256 Aug 23 08:48 [34m.[m[m
    drwxr-xr-x  5 rhearajashekhar  staff    160 Aug 23 08:48 [34m..[m[m
    -rw-r--r--  1 rhearajashekhar  staff   9767 Aug 23 08:48 2023-08-19-devops_accounts.ipynb
    -rw-r--r--  1 rhearajashekhar  staff   5931 Aug 23 08:48 2023-08-21-devops_tools-home.ipynb
    -rw-r--r--  1 rhearajashekhar  staff  22859 Aug 23 08:48 2023-08-21-devops_tools-setup.ipynb
    -rw-r--r--@ 1 rhearajashekhar  staff  35023 Aug 27 09:00 2023-08-22-devops_tools-verify.ipynb
    -rw-r--r--  1 rhearajashekhar  staff  32309 Aug 23 08:48 2023-08-23-devops-githhub_pages-play.ipynb
    -rw-r--r--  1 rhearajashekhar  staff   9478 Aug 23 08:48 2023-08-23-devops-hacks.ipynb



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


    bash: line 7: cd: /Users/rhearajashekhar/rhearajashekhar/vscode/rheaStudent/_posts: No such file or directory


    /Users/rhearajashekhar/vscode/rheaStudent/_notebooks/Foundation/B-tools_and_equipment
    total 248
    -rw-r--r--  1 rhearajashekhar  staff   9767 Aug 23 08:48 2023-08-19-devops_accounts.ipynb
    -rw-r--r--  1 rhearajashekhar  staff   5931 Aug 23 08:48 2023-08-21-devops_tools-home.ipynb
    -rw-r--r--  1 rhearajashekhar  staff  22859 Aug 23 08:48 2023-08-21-devops_tools-setup.ipynb
    -rw-r--r--@ 1 rhearajashekhar  staff  35023 Aug 27 09:00 2023-08-22-devops_tools-verify.ipynb
    -rw-r--r--  1 rhearajashekhar  staff  32309 Aug 23 08:48 2023-08-23-devops-githhub_pages-play.ipynb
    -rw-r--r--  1 rhearajashekhar  staff   9478 Aug 23 08:48 2023-08-23-devops-hacks.ipynb



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


    bash: line 7: cd: /Users/rhearajashekhar/rhearajashekhar/vscode/rheaStudent/_notebooks: No such file or directory


    /Users/rhearajashekhar/vscode/rheaStudent/_notebooks/Foundation/B-tools_and_equipment
    total 248
    -rw-r--r--  1 rhearajashekhar  staff   9767 Aug 23 08:48 2023-08-19-devops_accounts.ipynb
    -rw-r--r--  1 rhearajashekhar  staff   5931 Aug 23 08:48 2023-08-21-devops_tools-home.ipynb
    -rw-r--r--  1 rhearajashekhar  staff  22859 Aug 23 08:48 2023-08-21-devops_tools-setup.ipynb
    -rw-r--r--@ 1 rhearajashekhar  staff  35023 Aug 27 09:00 2023-08-22-devops_tools-verify.ipynb
    -rw-r--r--  1 rhearajashekhar  staff  32309 Aug 23 08:48 2023-08-23-devops-githhub_pages-play.ipynb
    -rw-r--r--  1 rhearajashekhar  staff   9478 Aug 23 08:48 2023-08-23-devops-hacks.ipynb



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


    bash: line 6: cd: /Users/rhearajashekhar/rhearajashekhar/vscode/rheaStudent/images: No such file or directory


    /Users/rhearajashekhar/vscode/rheaStudent/_notebooks/Foundation/B-tools_and_equipment
    total 248
    -rw-r--r--  1 rhearajashekhar  staff   9767 Aug 23 08:48 2023-08-19-devops_accounts.ipynb
    -rw-r--r--  1 rhearajashekhar  staff   5931 Aug 23 08:48 2023-08-21-devops_tools-home.ipynb
    -rw-r--r--  1 rhearajashekhar  staff  22859 Aug 23 08:48 2023-08-21-devops_tools-setup.ipynb
    -rw-r--r--@ 1 rhearajashekhar  staff  35023 Aug 27 09:00 2023-08-22-devops_tools-verify.ipynb
    -rw-r--r--  1 rhearajashekhar  staff  32309 Aug 23 08:48 2023-08-23-devops-githhub_pages-play.ipynb
    -rw-r--r--  1 rhearajashekhar  staff   9478 Aug 23 08:48 2023-08-23-devops-hacks.ipynb


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


    bash: line 7: cd: /Users/rhearajashekhar/rhearajashekhar/vscode/rheaStudent: No such file or directory


    show the contents of README.md
    


    cat: README.md: No such file or directory


    
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
    
    NVM_INC=/Users/rhearajashekhar/.nvm/versions/node/v22.5.0/include/node
    rvm_bin_path=/Users/rhearajashekhar/.rvm/bin
    VSCODE_CRASH_REPORTER_PROCESS_TYPE=extensionHost
    NVM_CD_FLAGS=-q
    TERM=xterm-color
    SHELL=/bin/zsh
    CLICOLOR=1
    TMPDIR=/var/folders/k5/9p51wpxs2wxdyptwcngz8h540000gn/T/
    HOMEBREW_REPOSITORY=/opt/homebrew
    PYTHONUNBUFFERED=1
    ORIGINAL_XDG_CURRENT_DESKTOP=undefined
    MallocNanoZone=0
    PYDEVD_USE_FRAME_EVAL=NO
    PYTHONIOENCODING=utf-8
    USER=rhearajashekhar
    NVM_DIR=/Users/rhearajashekhar/.nvm
    COMMAND_MODE=unix2003
    rvm_path=/Users/rhearajashekhar/.rvm
    SSH_AUTH_SOCK=/private/tmp/com.apple.launchd.GKQVq5KhIf/Listeners
    __CF_USER_TEXT_ENCODING=0x1F5:0x0:0x0
    PAGER=cat
    VIRTUAL_ENV=/Users/rhearajashekhar/vscode/rheaStudent/venv
    ELECTRON_RUN_AS_NODE=1
    VSCODE_AMD_ENTRYPOINT=vs/workbench/api/node/extensionHostProcess
    rvm_prefix=/Users/rhearajashekhar
    PATH=/Users/rhearajashekhar/vscode/rheaStudent/venv/bin:/Users/rhearajashekhar/.rbenv/shims:/Users/rhearajashekhar/.rbenv/bin:/opt/homebrew/bin:/opt/homebrew/sbin:/Users/rhearajashekhar/.nvm/versions/node/v22.5.0/bin:/Library/Frameworks/Python.framework/Versions/3.12/bin:/usr/local/bin:/System/Cryptexes/App/usr/bin:/usr/bin:/bin:/usr/sbin:/sbin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/local/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/appleinternal/bin:/Users/rhearajashekhar/.rvm/bin:/Users/rhearajashekhar/.rvm/bin
    __CFBundleIdentifier=com.microsoft.VSCode
    PWD=/Users/rhearajashekhar/vscode/rheaStudent/_notebooks/Foundation/B-tools_and_equipment
    VSCODE_HANDLES_UNCAUGHT_ERRORS=true
    MPLBACKEND=module://matplotlib_inline.backend_inline
    PYTHON_FROZEN_MODULES=on
    XPC_FLAGS=0x0
    FORCE_COLOR=1
    RBENV_SHELL=zsh
    XPC_SERVICE_NAME=0
    rvm_version=1.29.12 (latest)
    SHLVL=2
    HOME=/Users/rhearajashekhar
    VSCODE_NLS_CONFIG={"locale":"en-us","osLocale":"en-us","availableLanguages":{},"_languagePackSupport":true}
    PYDEVD_IPYTHON_COMPATIBLE_DEBUGGING=1
    HOMEBREW_PREFIX=/opt/homebrew
    LOGNAME=rhearajashekhar
    LC_CTYPE=UTF-8
    VSCODE_IPC_HOOK=/Users/rhearajashekhar/Library/Application Support/Code/1.90-main.sock
    VSCODE_CODE_CACHE_PATH=/Users/rhearajashekhar/Library/Application Support/Code/CachedData/89de5a8d4d6205e5b11647eb6a74844ca23d2573
    CLICOLOR_FORCE=1
    NVM_BIN=/Users/rhearajashekhar/.nvm/versions/node/v22.5.0/bin
    VSCODE_PID=57578
    INFOPATH=/opt/homebrew/share/info:
    HOMEBREW_CELLAR=/opt/homebrew/Cellar
    GIT_PAGER=cat
    VSCODE_L10N_BUNDLE_LOCATION=
    VSCODE_CWD=/
    VIRTUAL_ENV_PROMPT=(venv) 
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

    bash: line 5: cd: /Users/rhearajashekhar/rhearajashekhar/vscode/rheaStudent: No such file or directory


    
    show the secrets of .git config file


    bash: line 9: cd: .git: No such file or directory
    ls: config: No such file or directory


    
    look at config file


    cat: config: No such file or directory



    ---------------------------------------------------------------------------

    CalledProcessError                        Traceback (most recent call last)

    Cell In[12], line 1
    ----> 1 get_ipython().run_cell_magic('script', 'bash', '\n# Extract saved variables\nsource /tmp/variables.sh\n\ncd $project\n\necho ""\necho "show the secrets of .git config file"\ncd .git\nls -l config\n\necho ""\necho "look at config file"\ncat config\n')


    File ~/vscode/rheaStudent/venv/lib/python3.12/site-packages/IPython/core/interactiveshell.py:2541, in InteractiveShell.run_cell_magic(self, magic_name, line, cell)
       2539 with self.builtin_trap:
       2540     args = (magic_arg_s, cell)
    -> 2541     result = fn(*args, **kwargs)
       2543 # The code below prevents the output from being displayed
       2544 # when using magics with decorator @output_can_be_silenced
       2545 # when the last Python token in the expression is a ';'.
       2546 if getattr(fn, magic.MAGIC_OUTPUT_CAN_BE_SILENCED, False):


    File ~/vscode/rheaStudent/venv/lib/python3.12/site-packages/IPython/core/magics/script.py:315, in ScriptMagics.shebang(self, line, cell)
        310 if args.raise_error and p.returncode != 0:
        311     # If we get here and p.returncode is still None, we must have
        312     # killed it but not yet seen its return code. We don't wait for it,
        313     # in case it's stuck in uninterruptible sleep. -9 = SIGKILL
        314     rc = p.returncode or -9
    --> 315     raise CalledProcessError(rc, cell)


    CalledProcessError: Command 'b'\n# Extract saved variables\nsource /tmp/variables.sh\n\ncd $project\n\necho ""\necho "show the secrets of .git config file"\ncd .git\nls -l config\n\necho ""\necho "look at config file"\ncat config\n'' returned non-zero exit status 1.


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
    -rw-r--r--@ 1 rhearajashekhar  wheel  808 Aug 27 08:53 sample.md
          15     132     808 sample.md


    bash: line 36: mdless: command not found


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

    No manual entry for wget


    
    File listing and status
    -rw-r--r--@ 1 rhearajashekhar  wheel  919 Aug 27 08:53 sample.md
          15     145     919 sample.md


    bash: line 37: mdless: command not found


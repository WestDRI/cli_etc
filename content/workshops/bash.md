---
title: Automation and scripting in bash for absolute beginners
topic: Shell
slug: bash
weight: 12
execute:
  error: true
format: hugo
---



## Background

### What are Unix shells?

A Unix shell is a command line interpreter: the user enters commands as text, either interactively in the command line or in a script, and the shell passes them to the operating system.

#### Bash

Bash (<em>Bourne Again SHell</em>), released in 1989, is part of the GNU Project and is the default Unix shell on many systems (MacOS recently changed its default to zsh).

#### Other shells

Prior to Bash, the default was the Bourne shell (sh).

A new and popular shell (backward compatible with Bash) is zsh. It extends Bash's capabilities.

Another shell in the same family is the KornShell (ksh).

All these shells are quite similar. The C shell (csh) however was modeled on the C programming language.

Bash is the most common shell and the one which makes the most sense to learn as a first Unix shell.

### Why use a shell?

Unix shells allow to automate repetitive tasks: it is easy to rerun a script (a file with a number of commands) while automating GUI operations is really difficult.

They are lightweight and powerful to launch tools, modify files, search, or combine commands.

They also allow to work on remote machines and HPC systems.

## How we will use Bash today

We will connect to a remote HPC system via SSH (secure shell) using a terminal on your laptop.

### Linux and MacOS users

Linux users: open the terminal emulator of your choice.
MacOS users: open "Terminal".

Then type:

``` bash
ssh userxx@bashworkshop.c3.ca
```

### Windows users

We suggest using {{<a "https://mobaxterm.mobatek.net/download.html" "the free version of MobaXterm.">}}

MobaXterm comes with a terminal emulator and a simple interface for remote SSH sessions.

Open MobaXterm, click on "Session", then "SSH", and fill in the Remote host name and your username. {{<a "https://mobaxterm.mobatek.net/demo.html" "Here">}} is a live demo.

### Password

We will give you the password for our training cluster during the workshop. When prompted, enter it.

{{<notes>}}
Note that you will not see any character as you type: Linux uses blind typing for safety. Type slowly and make sure not to make typo. It can be weird to use blind typing at first!
{{</notes>}}

## Bash: the basics

### The prompt

Customizable.  
By default, often gives the username and the hostname.  
Usually ends with `$`.

### Help on commands

Man pages:

``` bash
man <command>
```

{{<notes>}}
Man pages open in a pager (usually `less`).  
Navigate up/down with the space bar and the `b` key.  
Quit the pager with the `q` key.
{{</notes>}}

Help pages:

``` bash
<command> --help
```

Inspect commands:

``` bash
command -V <command>
```

### Examples of commands

- Print working directory: `pwd`
- Change directory: `cd`
- Print: `echo`
- Print content of a file: `cat`
- List: `ls`
- Copy: `cp`
- Move or rename: `mv`
- Create a new directory: `mkdir`
- Create a new file: `touch`

### Keybindings

Clear the terminal (command `clear`) with C-l (this means: press the Ctrl and L keys at the same time).

Navigate command history with C-p and C-n (or up and down arrows).

You can auto-complete commands by pressing the tab key.

## Bash scripting: the basics

You can put the commands you used directly in the terminal into a script. They will be run when you execute the script.

### File name

Shell scripts, including Bash scripts, are usually given the extension `sh` (e.g. `my_script.sh`).

You can store scripts anywhere, but it may be a good idea to store them in a `~/bin` directory.

### Syntax

#### Shebang

Scripts must start with a shebang (`#!`) followed by the name of the interpreter you are using. To use Bash, start your scripts with:

``` bash
#!/bin/bash
```

You may also encounter this notation:

``` bash
#!/usr/bin/env bash
```

See {{<a "https://stackoverflow.com/questions/16365130/what-is-the-difference-between-usr-bin-env-bash-and-usr-bin-bash" "here">}} for the difference.

#### Comments

Start with `#`. Anything to the left of this character is ignored by the interpreter and is for humans only.

#### Commands

Each command starts on a new line or after a semicolon.

### Executing a script

There are two ways to execute a script:

``` bash
bash my_script.sh
```

``` bash
./my_script.sh  # The dot represents the current directory
```

In the latter case, you need to make sure that your script is executable by first running:

``` bash
chmod u+x my_script.sh  # Make the script executable by the user
```

### Our first script

Open a text editor and type:

``` bash
#!/bin/bash

echo "This is our first script."
```

Save and close the file.

Now run the script.

## Variables

### Declaring variables

Declare a variable with the `=` sign and without spaces:

``` bash
variable=Test
```

``` bash
variable=This string is the value of the variable  # Oops...
```

    Error in running command bash

``` bash
variable="This string is the value of the variable"
```

``` bash
variable='This string is the value of the variable'
```

``` bash
variable='This string's the value of the variable'  # Oops...
```

    bash: -c: line 1: unexpected EOF while looking for matching `''
    bash: -c: line 2: syntax error: unexpected end of file

``` bash
variable="This string's the value of the variable"
```

``` bash
variable="This string is the value of the variable called "variable""  # Oops...
```

``` bash
variable="This string is the value of the variable called \"variable\""  # \ is the escape character
```

### Expanding a variable's value

Expand a variable (access its value) with `$`:

``` bash
variable=Test
echo $variable
```

    Test

``` bash
variable=Test; echo "$variable"
```

    Test

{{<emph_inline>}}
Single quotes don't expand variables.
{{</emph_inline>}}

``` bash
variable=Test; echo '$variable'
```

    $variable

### Passing variables to a Bash script

Create the script `name.sh` with:

``` bash
#!/bin/bash

echo "My name is $1."  # $1 refers to the first variable passed to the script
```

You can now pass a variable to this script with:

``` bash
bash name.sh Marie
```

    My name is Marie.

You can pass several variables to a script. Copy `name.sh` to `name2.sh` and edit `name2.sh` to look like the following:

``` bash
#!/bin/bash

echo "My name is $1 and I am $2 years old."
```

``` bash
bash name2.sh Marie 43
```

    My name is Marie and I am 43 years old.

You can also pass any number of variables to a script:

``` bash
#!/bin/bash

echo $@
```

``` bash
bash script.sh argument1 argument2 argument3 argument4
```

    argument1 argument2 argument3 argument4

### Brace expansion

``` bash
echo {1..5}
```

    1 2 3 4 5

``` bash
echo {01..10}
```

    01 02 03 04 05 06 07 08 09 10

``` bash
echo {1..5}.txt
```

    1.txt 2.txt 3.txt 4.txt 5.txt

``` bash
echo {r..v}
```

    r s t u v

``` bash
echo {file1,file2}.sh   # no space after the comma
```

    file1.sh file2.sh

``` bash
touch {file1,file2}.sh
```

``` bash
touch file{3..6}.sh
```

``` bash
echo {list,of,strings}
```

    list of strings

### Wildcards

``` bash
rm file*.sh
```

## Loops

``` bash
for <iterable> in <list>
do
    <statement1>
    <statement2>
    ...
done
```

{{<ex>}}
Let's create the script `names.sh`:

``` bash
#!/bin/bash

for name in $@
do
    echo $name
done
```

Now let's run it with a list of arguments:

``` bash
bash names.sh Patrick Paul Marie Alex
```

    Patrick
    Paul
    Marie
    Alex

{{</ex>}}

## Let's put it all together to automate some task

This is a rather silly example, but bear with me and let's imagine that it actually makes sense (of course, you don't write that many thesis chapters so you would probably never automate these tasks...)

So... let's imagine that each time you write a thesis chapter, you do the same things:

- you create a directory with the name of the chapter,
- you create a number of subdirectories (for your source code, your manuscript, your data, and your results),
- you create a Python script in the source code directory,
- you create a markdown document in your manuscript directory,
- you put the whole thing under version control with Git,
- you create a `.gitignore` file in which you put the data subdirectory.

{{<exercise>}}
Write a script that would do all this, then test the script.

Give it a try on your own before looking at the solution below...
{{</exercise>}}

{{< solution >}}

Here is what the script looks like (let's call it `chapter.sh`):

``` bash
#!/bin/bash

mkdir $1
cd $1
mkdir src data results ms
touch src/$1.py ms/$1.md
git init
echo data/ > .gitignore
```

You then run the script:

``` bash
bash chapter.sh chapter1
```

You can verify that all the files and directories got created with:

``` bash
tree chapter1
```

    chapter1/
    ├── data
    ├── ms
    │   └── chapter1.md
    ├── results
    └── src
        └── chapter1.py

and:

``` bash
ls -aF chapter1
```

    ./  ../  data/  .git/  .gitignore  ms/  results/  src/

You can also verify the content of your `.gitignore` file with:

``` bash
cat chapter1/.gitignore
```

    data/

{{< /solution >}}

## Resources

One very useful (although very dense) resource is the {{<a "https://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html" "Bash manual.">}}

You can also get information on Bash from within Bash with:

``` bash
info bash
```

and:

``` bash
man bash
```

There are also countless resources online and don't forget to Google anything you don't know how to do: you will almost certainly find the answer on {{<a "https://stackoverflow.com/" "StackOverflow">}} or some Stack Exchange site.

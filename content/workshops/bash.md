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

While automating GUI operations is really difficult, it is easy to rerun a script (a file with a number of commands). Unix shells thus allow the creation of reproducible workflows and the automation of repetitive tasks.

They are powerful to launch tools, modify files, search text, or combine commands.

They also allow to work on remote machines and HPC systems.

## How we will use Bash today

Bash is a Unix shell. You thus need a Unix or Unix-like operating system.

We will connect to a remote HPC system via SSH (secure shell). HPC systems always run Linux.

Those on Linux or MacOS can alternatively use Bash directly on their machine. On MacOS, the default is now zsh (you can see that by typing `echo $SHELL` in Terminal), but zsh is fully compatible with Bash commands, so it is totally fine to use it instead. If you really want to use Bash, simply launch it by typing in Terminal: `bash`.

### Connecting to a remote HPC system via SSH

#### Usernames and password

We will give you a link to an etherpad during the workshop. Add your name next to a free username to claim it.

We will also give you the password for our training cluster. When prompted, enter it.

{{<notes>}}
Note that you will not see any character as you type the password: this is called blind typing and is a Linux safety feature. Type slowly and make sure not to make typos. It can be unsettling at first not to get any feed-back while typing.
{{</notes>}}

#### Linux and MacOS users

Linux users: open the terminal emulator of your choice.  
MacOS users: open "Terminal".

Then type:

``` bash
ssh userxx@bashworkshop.c3.ca  # Replace userxx by your username (e.g. user09)
```

#### Windows users

We suggest using {{<a "https://mobaxterm.mobatek.net/download.html" "the free version of MobaXterm.">}}

MobaXterm comes with a terminal emulator and a GUI interface for SSH sessions.

Open MobaXterm, click on "Session", then "SSH", and fill in the Remote host name and your username. {{<a "https://mobaxterm.mobatek.net/demo.html" "Here">}} is a live demo.

## Bash: the basics

### The prompt

In command-line interfaces, a command prompt is a sequence of characters indicating that the interpreter is ready to accept input. It can also provide some information (e.g. time, error types, username and hostname, etc.)

The Bash prompt is customizable. By default, it often gives the username and the hostname, and it typically ends with `$`.

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

Instead of typing commands one at a time directly in a terminal, you can write them down, one per line, in a text file called a script.

They will be run in the order in which they are written when you execute the script.

This is a great way to automate tasks: to rerun this sequence of commands, you simply have to rerun the script.

### File name

Shell scripts, including Bash scripts, are usually given the extension `sh` (e.g. `my_script.sh`).

You can store scripts anywhere, but a common practice is to store them in a `~/bin` directory.

### Syntax

#### Shebang

Scripts can be written for any interpreter (e.g. Bash, Python, R, etc.) The way to tell the system which one to use is to use a shebang (`#!`) followed by the path of the interpreter on the first line of the script.

To use Bash, start your scripts with:

``` bash
#!/bin/bash
```

You may also encounter this notation:

``` bash
#!/usr/bin/env bash
```

If you are curious, you can read the answers to {{<a "https://stackoverflow.com/q/16365130/9210961" "this Stack Overflow question">}} for the differences between the two.

#### Comments

Anything to the left of `#` is ignored by the interpreter and is for human consumption only.

``` bash
# You can write full-line comments

pwd       # You can also write comments after commands
```

### Executing scripts

There are two ways to execute a script:

``` bash
bash my_script.sh
```

``` bash
./my_script.sh  # The dot represents the current directory
```

In the latter case, you need to make sure that your script is executable by first running:

``` bash
chmod u+x my_script.sh  # This makes the script executable by the user (i.e. you)
```

### Our first script

Open a text editor (e.g. nano) and type:

``` bash
#!/bin/bash

echo "This is our first script."
```

Save and close the file.

{{<exercise>}}
Now run the script with one, then the other method.<br><br>
What does this script do?
{{</exercise>}}

## Variables

### Declaring variables

You can declare a variable (i.e. a name that holds a value) with the `=` sign.

{{<emph_inline>}}!! Make sure not to put spaces around the equal sign.{{</emph_inline>}}

``` bash
variable=Test
```

### Quotes

Let's experiment with quotes:

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

To expand a variable (to access its value), you need to prepend its name with `$`:

``` bash
variable=Test
echo variable
```

    variable

Mmmm... not really want we want!

``` bash
variable=Test
echo $variable
```

    Test

``` bash
variable=Test; echo "$variable"
```

    Test

{{<emph_inline>}}!! Single quotes don't expand variables.{{</emph_inline>}}

``` bash
variable=Test; echo '$variable'
```

    $variable

### Passing variables to a Bash script

Create a script called `name.sh` with the following content:

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
echo {file1,file2}.sh
```

    file1.sh file2.sh

{{<emph_inline>}}!! Make sure not to add a space after the comma.{{</emph_inline>}}

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

Wildcards are really powerful to apply a command to all the elements having a common pattern.

For instance, we can delete all the files we created earlier (`file1.sh`, `file2.sh`, etc.) with a single command:

``` bash
rm file*.sh
```

{{<emph_inline>}}!! Be very careful that `rm` is irreversible. Deleted files do not go to the trash: they are gone.{{</emph_inline>}}

## Loops

To apply a set of commands to all the elements of a list, you can use for loops. The general structure is as follows:

``` bash
for <iterable> in <list>
do
    <statement1>
    <statement2>
    ...
done
```

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

{{<exercise>}}
Compare the outputs of the following 2 scripts:

- script1.sh:

``` bash
#!/bin/bash

echo $@
```

- script2.sh:

``` bash
#!/bin/bash

for i in $@
do
    echo $i
done
```

How do you explain the difference between running:

``` bash
bash script1.sh arg1 arg2 arg3
```

and running:

``` bash
bash script2.sh arg1 arg2 arg3
```

{{</exercise>}}

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

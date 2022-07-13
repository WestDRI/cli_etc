#+title: Introduction to Git & GitHub
#+topic: Git
#+slug: 2022_git_m2pi
#+weight: 13

*<center style="font-size: 2rem;">Workshop for <a href="https://m2pi.ca/" target="_blank">Math<sup>Industry</sup> 2022</a>, July 11–29, 2022</center>*

#### *Abstract*

{{<def>}}
Git is a powerful version control system allowing to record, access, and restore the history of projects. After setting up remotes on the internet or other network, Git is also a mighty collaboration tool.

In this workshop, we will:

- explain what version control is and what the benefits are,
- get you started with Git,
- use the popular online Git repository hosting site GitHub to introduce a workflow typical of many companies.
{{</def>}}

## Why version control?
{{<br size="4">}}

{{<imgbshadow src="/img/git/git_img/vc.jpg" margin="auto" title="" width="50%" line-height="2rem">}}
from <a href="http://geek-and-poke.com/" target="_blank">Geek&Poke &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;</a>
{{</imgbshadow>}}
{{<br size="2">}}

{{<imgbshadow src="https://phdcomics.com/comics/archive/phd101212s.gif" margin="auto" title="" width="67%" line-height="2rem">}}
from <a href="http://phdcomics.com/" target="_blank">PhD &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&ensp;&nbsp;</a>
{{</imgbshadow>}}

## Which version control system?
{{<br size="4">}}

<script type="text/javascript" src="https://ssl.gstatic.com/trends_nrtr/3029_RC01/embed_loader.js"></script> <script type="text/javascript"> trends.embed.renderExploreWidget("TIMESERIES", {"comparisonItem":[{"keyword":"/m/05vqwg","geo":"","time":"2004-01-01 2022-07-13"},{"keyword":"/m/08441_","geo":"","time":"2004-01-01 2022-07-13"},{"keyword":"/m/012ct9","geo":"","time":"2004-01-01 2022-07-13"},{"keyword":"/m/09d6g","geo":"","time":"2004-01-01 2022-07-13"}],"category":0,"property":""}, {"exploreQuery":"date=all&q=%2Fm%2F05vqwg,%2Fm%2F08441_,%2Fm%2F012ct9,%2Fm%2F09d6g","guestPath":"https://trends.google.com:443/trends/embed/"}); </script>

Looking at Google trends for web searches, there is a clear winner...
{{<br size="3">}}

{{<imgbshadow src="https://imgs.xkcd.com/comics/git.png" margin="auto" title="" width="100%" line-height="2rem">}}
from <a href="https://xkcd.com/" target="_blank">xkcd.com &nbsp;</a>
{{</imgbshadow>}}

## Install Git

### MacOS & Linux users

Install Git from {{<a "https://git-scm.com/downloads" "the official website.">}}

### Windows users

Install {{<a "https://gitforwindows.org/" "Git for Windows.">}} This will also install Git Bash, a Bash emulator.

## Create a free GitHub account

Sign up for a {{<a "https://github.com/" "free GitHub account.">}}

Later on, to avoid having to type your password all the time, you should {{<a "https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh" "set up SSH for your account.">}}


## Configure Git

### User identity

```sh
git config --global user.name "<Your Name>"
git config --global user.email "<your@email>"
```

#### Example

```sh
git config --global user.name "John Doe"
git config --global user.email "john.doe@gmail.com"
```

### Text editor

```sh
git config --global core.editor "<text-editor>"
```

#### Example for nano

```sh
git config --global core.editor "nano"
```

### Line ending

#### macOS, Linux, or WSL

```sh
git config --global core.autocrlf input
```

#### Windows

```sh
git config --global core.autocrlf true
```

### List settings

```sh
git config --list
```

## Git documentation

### Internal documentation

#### Man pages

```sh
git <command> --help
git help <command>
man git-<command>
```

##### Example

```sh
git commit --help
git help commit
man git-commit
```

##### Useful keybindings when you are in the pager

```sh
SPACE      scroll one screen down
b          scroll one screen up
q          quit
```

#### Command options

```sh
git <command> -h
```

##### Example

```sh
git commit -h
```

### Online documentation

- Official {{<a "https://git-scm.com/docs" "Git manual">}}
- Open source {{<a "https://git-scm.com/book/en/v2" "Pro Git book">}}

#### Courses & workshops

- {{<a "https://westgrid-cli.netlify.app/workshops/" "Western Canada Research Computing Git workshops">}}
- {{<a "https://wgschool.netlify.app/git/" "last summer Western Canada Research Computing Git course">}}
- {{<a "https://autumnschool.netlify.app/git/" "last fall Western Canada Research Computing Git course">}}
- the {{<a "http://swcarpentry.github.io/git-novice/" "Software Carpentry Git lesson">}}

#### Q & A

- {{<a "https://stackoverflow.com/questions/tagged/git" "Stack Overflow's Git tag">}}

## Understanding Git

### Project history

Git saves the history of a project as a series of snapshots:

{{<imgbshadow src="/img/git/git_img/diagrams_v3/02.png" bg="#e6e6e6" margin="rem" title="" width="%" line-height="0.5rem">}}
{{</imgbshadow>}}

Those snapshots are called commits:

{{<imgbshadow src="/img/git/git_img/diagrams_v3/03.png" bg="#e6e6e6" margin="rem" title="" width="%" line-height="0.5rem">}}
{{</imgbshadow>}}

Commits are identified by unique *hash*:

{{<imgbshadow src="/img/git/git_img/diagrams_v3/03.png" bg="#e6e6e6" margin="rem" title="" width="%" line-height="0.5rem">}}
{{</imgbshadow>}}

Each commit contains these metadata:

- author,

- date and time,

- the hash of parent commit(s),

- a message.

As soon as you create the first commit, a pointer called a *branch* is created and it points to that commit. By default, that first branch is called `main`:

{{<imgbshadow src="/img/git/git_img/diagrams_v3/08.png" bg="#e6e6e6" margin="rem" title="" width="%" line-height="0.5rem">}}
{{</imgbshadow>}}

Another pointed (`HEAD`) points to the branch `main`.

`HEAD` indicates where we are in the project history.

{{<imgbshadow src="/img/git/git_img/diagrams_v3/08.png" bg="#e6e6e6" margin="rem" title="" width="%" line-height="0.5rem">}}
{{</imgbshadow>}}

### Recording history

As you create more commits, the history grows ...

{{<imgbshadow src="/img/git/git_img/diagrams_v3/05.png" bg="#e6e6e6" margin="rem" title="" width="%" line-height="0.5rem">}}
{{</imgbshadow>}}

... and the pointers `HEAD` and `main` automatically move to the last commit:

{{<imgbshadow src="/img/git/git_img/diagrams_v3/04.png" bg="#e6e6e6" margin="rem" title="" width="%" line-height="0.5rem">}}
{{</imgbshadow>}}

For simplicity, the diagrams can be simplified this way:

{{<imgbshadow src="/img/git/git_img/diagrams_v3/13.png" bg="#e6e6e6" margin="rem" title="" width="%" line-height="0.5rem">}}
{{</imgbshadow>}}

### Displaying the commit history

#### As a list

```sh
git log --oneline
```

##### Making it more readable

```sh
git log \
    --graph \
    --date-order \
    --date=short \
    --pretty=format:'%C(cyan)%h %C(blue)%ar %C(auto)%d'`
                   `'%C(yellow)%s%+b %C(magenta)%ae'
```

#### As a graph

```sh
git log --graph
```

##### As a graph showing all commits

```sh
git log --graph --all
```

## How does Git work?

### The three trees of Git

A useful representation of Git's functioning is to imagine three file trees:

{{<imgbshadow src="/img/git/git_img/diagrams_v2/05.png" bg="#e6e6e6" margin="rem" title="" width="%" line-height="0.5rem">}}
{{</imgbshadow>}}

### Making changes to the working tree

When you work on your project, your working tree changes:

{{<imgbshadow src="/img/git/git_img/diagrams_v2/10.png" bg="#e6e6e6" margin="rem" title="" width="%" line-height="0.5rem">}}
{{</imgbshadow>}}

### Staging changes

You organize your next snapshot by picking and choosing some changes

```sh
git add <what-you-want-to-commit-next>
```

Those changes move to the *index* or *staging area*:

{{<imgbshadow src="/img/git/git_img/diagrams_v2/11.png" bg="#e6e6e6" margin="rem" title="" width="%" line-height="0.5rem">}}
{{</imgbshadow>}}

### Creating a commit

Finally you create a commit with what is in the staging area:

```sh
git commit -m "<message>"
```

{{<imgbshadow src="/img/git/git_img/diagrams_v2/12.png" bg="#e6e6e6" margin="rem" title="" width="%" line-height="0.5rem">}}
{{</imgbshadow>}}

## Remotes

### What are remotes?

Remotes are copies of a project & its history.

They can be located anywhere, including on external drive or on the same machine as the project, although they are often on a different machine to serve as backup, or on a network (e.g. internet) to serve as a syncing hub for collaborations.

Popular online Git repository managers & hosting services:

- {{<a "https://github.com" "GitHub">}}
- {{<a "https://gitlab.com" "GitLab">}}
- {{<a "https://bitbucket.org" "Bitbucket">}}

## Collaboration

### 3 situations

- You create a project on your machine and want others to contribute to it (1).

- You want to contribute to a project started by others & ...

	&emsp;&emsp;... you have write access to it (2).

    &emsp;&emsp;... you do **not** have write access to it (3).

### (1) You start the project

#### Create a remote on GitHub

##### 1. Create an empty repository on GitHub

- Go to the {{<a "https://github.com" "GitHub website,">}} login, and go to your home page.

- Look for the `Repositories` tab & click the green `New` button.

- Enter the name you want for your repo, *without spaces*.

- Make the repository public or private.

##### 2. Link empty repository to your repo

Click on the `Code` green drop-down button, select SSH {{<a "https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/connecting-to-github-with-ssh" "if you have set SSH for your GitHub account">}} or HTTPS and copy the address.

In the command line, `cd` inside your project, and add the remote:

```sh
git remote add <remote-name> <remote-address>
```

`remote-name` is a convenience name to identify that remote. You can choose any name, but since Git automatically call the remote `origin` when you clone a repo, it is common practice to use `origin` as the name for the first remote.
{{<br size="1">}}

{{<notes>}}
Example (using an SSH address):
{{</notes>}}

```sh
git remote add origin git@github.com:<user>/<repo>.git
```

{{<notes>}}
Example (using an HTTPS address):
{{</notes>}}

```sh
git remote add origin https://github.com/<user>/<repo>.git
```

If you are working alone on this project and you only wanted to have a remote for backup, you are set.

If you don't want to grant others write access to the project, and you only accept contributions through pull requests, you are also set.

If you want to grant your collaborators write access to the project however, you need to add them to it.

#### Invite collaborators

- Go to your GitHub project page.

- Click on the `Settings` tab.

- Click on the `Manage access` section on the left-hand side (you will be prompted for your GitHub password).

- Click on the `Invite a collaborator` green button.

- Invite your collaborators with one of their GitHub user name, their email address, or their full name.

### (2) Write access to project

#### Clone project

`cd` to location where you want your local copy, then:

```sh
git clone <remote-address> <local-name>
```

This sets the project as a remote to your new local copy and that remote is automatically called `origin`.

Without `<local-name>`, the repo will have the name of the last part of the remote address.

### (3) No write access to project

#### Collaborate without write access

1. Fork the project.

2. Clone your fork on your machine.

3. Add the initial project as a second remote & call it `upstream`.

## Working with remotes

### Get information on remotes

List remotes:

```sh
git remote
```

List remotes with their addresses:

```sh
git remote -v
```

Get more information on a remote:

```sh
git remote show <remote-name>
```

{{<notes>}}
Example:
{{</notes>}}

```sh
git remote show origin
```

### Manage remotes

Rename a remote:

```sh
git remote rename <old-remote-name> <new-remote-name>
```

Delete a remote:

```sh
git remote remove <remote-name>
```

Change the address of a remote:

```sh
git remote set-url <remote-name> <new-url> [<old-url>]
```

### Get data from a remote

If you collaborate on a project, you have to get the data added by your teammates to keep your local project up to date.

To download new data from a remote, you have 2 options:

- `git fetch`

- `git pull`

#### Fetch changes

*Fetching* downloads the data from a remote that you don't already have in your local version of the project:

```sh
git fetch <remote-name>
```

The branches on the remote are now accessible locally as `<remote-name>/<branch>`. You can inspect them or you can merge them into your local branches.

{{<notes>}}
Example:
{{</notes>}}

```sh
git fetch origin
```

#### Pull changes

*Pulling* fetches the changes & merges them onto your local branches:

```sh
git pull <remote-name> <branch>
```

{{<notes>}}
Example:
{{</notes>}}

```sh
git pull origin main
```

If your branch is already tracking a remote branch, you can omit the arguments:

```sh
git pull
```

### Push to a remote

Uploading data to the remote is called *pushing*:

```sh
git push <remote-name> <branch-name>
```

{{<notes>}}
Example:
{{</notes>}}

```sh
git push origin main
```

You can set an upstream branch to track a local branch with the `-u` flag:

```sh
git push -u <remote-name> <branch-name>
```

{{<notes>}}
Example:
{{</notes>}}

```sh
git push -u origin main
```

From now on, all you have to run when you are on `main` is:

```sh
git push
```

### Submit a pull request

1. Pull from `upstream` to update your local project.

2. Create & checkout a new branch.

3. Make & commit your changes on that branch.

4. Push that branch to your fork (i.e. `origin` — remember that you do not have write access to `upstream`).

5. Go to the original project GitHub's page & open a pull request.
{{<br size="5">}}

{{<imgb2 src="/img/git/git_img/gitout.png" margin="auto" title="" width="60%" line-height="2rem">}}
by <a href="https://www.redbubble.com/people/jscript/shop#profile" target="_blank">jscript &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;</a>
{{</imgb2>}}

## Comments & questions

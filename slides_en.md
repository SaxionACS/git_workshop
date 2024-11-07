---
title: Git & version control
subtitle: not only for software engineers
author: Dawid Zalewski & Ronald Tangelder
date: \today{}
# theme: Dresden
colortheme: default
fontfamily: noto-sans
header-includes:
- \usepackage{lmodern}
- \usepackage{pgf}
- \usepackage{tikz}
- \usepackage{textpos}


- \useoutertheme{infolines}
- \useoutertheme[subsection=false]{miniframes}

# - \addtobeamertemplate{frametitle}{}{ \begin{textblock*}{100mm}(0.9\textwidth,-1.25cm) \includegraphics[height=0.55cm,keepaspectratio]{logo.png} \end{textblock*}}
- \setbeamertemplate{caption}{\raggedright\insertcaption\par}
- \useinnertheme{circles}

- \definecolor{text}{RGB}{0, 0, 0}
- \definecolor{text_light}{RGB}{68, 84, 106}
- \definecolor{sax_green}{RGB}{0, 156, 130}
- \definecolor{sax_red}{RGB}{206, 21, 79}
- \definecolor{sax_grey}{RGB}{186, 186, 186}
- \definecolor{sax_blue}{RGB}{0, 144, 179}

- \setbeamercolor{palette primary}{fg=white,bg=sax_green}
- \setbeamercolor{palette secondary}{fg=white,bg=sax_green}
- \setbeamercolor{palette tertiary}{fg=text_light,bg=sax_green}
- \setbeamercolor{palette quaternary}{fg=blue, bg=sax_green}
- \setbeamercolor{structure}{fg=sax_red} # itemize, enumerate, etc
- \setbeamercolor{section in toc}{fg=white, bg=white} # TOC sections
- \setbeamercolor{subsection in head/foot}{bg=sax_green,fg=text_light}
- \setbeamercolor{section in head/foot}{bg=sax_green,fg=text_light}

- \newcommand{\nologo}{\setbeamertemplate{logo}{}}


# - \usebackgroundtemplate{\includegraphics[width=\paperwidth,height=\paperheight]{wallpaper2.png}}
classoption:
   - compress
   - xcolor=dvipsnames
fontsize: 11pt
aspectratio: 43
colorlinks: true
lang: en-US
---

# Intro

## Version Control Systems

*Version control* is a system in which changes to a file or group of files are tracked over time so that later a specific version can be retrieved.

## Why version control?

* Retrieve previous versions of files or the whole project
* View changes between two points in time
* Tracking who changed what

## Local version control

\begin{center}
\includegraphics[width=0.6\textwidth]{./images/local.png}
\end{center}

## Centralized version control

\begin{center}
\includegraphics[width=0.7\textwidth]{./images/centralized.png}
\end{center}

## Distributed version control

\begin{center}
\includegraphics[width=0.5\textwidth]{./images/distributed.png}
\end{center}

## What is git

Git is a *distributed* version control system

* Each team member can work independently
* Almost all operations are local
* Everyone has a local copy of the database (repository)

## Before we start

* Git client: [http://git-scm.com/download/](http://git-scm.com/download/)
  * Get the right version for your system
  * Including *Git Bash* (only Windows)
* GUI tool: [http://git-scm.com/downloads/guis](http://git-scm.com/downloads/guis)
    * For example [Github Desktop](https://desktop.github.com/)

\begin{block}{Info}
\center{We will (try) not to use GUI tools.}
\end{block}

## Getting started - a few settings

```console
$ git config --global user.name "Dawid Zalewski"
$ git config --global user.email "d.r.zalewski@saxion.nl"
```

## Getting started - text editor

You can also change the default text editor:

For Notepad++:

```console
$ git config --global core.editor 
"'notepad++.exe' -multiInst -nosession"
```

For Visual Studio Code:

```console
$ git config --global core.editor "code --wait"
```

## Getting started - check the settings

```console
$ git config --list
```

# Local version control

## Initialize a repository

```console
$ mkdir my_project
$ cd my_project/
$ git init
Initialized empty Git repository in ...
$ git status
On branch master

Initial commit

nothing to commit (create/copy files 
 and use "git add" to track)
```

## Three states

There are three states that files can be in:

* 'modified'
* 'staged' (prepared for a `commit`)
* 'commited'

## Three states

\begin{block}{Modified}
A file has been modified but not yet commited to the database
\end{block}

\begin{block}{Staged}
A modified file is included in the next commit
\end{block}

\begin{block}{Committed}
All data is safe in the local database
\end{block}

## Git workflow & environment

\begin{center}
\includegraphics[width=0.8\textwidth]{./images/git_workflow.pdf}
\end{center}

## Environment

### Working directory

The directory structure and files in which you make changes

### Staging Area

An *Intermediate station* between the **working directory** and the **repository**

Allows for selective *committing* of changes

### Repository

Collection (backup database) of all commits, branches, tags, ...

## First commit

Create a new file (readme.txt) in the `my_project` folder

For VS Code users:

```console
$ code readme.txt
```

* Type in some text and save.

## Check

```console
$ ls -l

total 1
-rw-r--r-- 1 zalda 197609 7 Apr 11 12:55 readme.txt
```

## Git status

```console
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what 
   will be committed)

        readme.txt

nothing added to commit but untracked files present 
 (use "git add" to track)
```

## Where is `readme.txt`

\begin{center}
\includegraphics[width=0.8\textwidth]{./images/git_workflow_wd.pdf}
\end{center}

## To the *Staging Area*: `git add`

```console
$ git add readme.txt
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

  new file:   readme.txt
```

## Where is `readme.txt`

\begin{center}
\includegraphics[width=0.8\textwidth]{./images/git_workflow_sa.pdf}
\end{center}

## Adding a commit: `git commit`

```console
$ git commit -m "readme.txt added"
[master (root-commit) af84a5e] readme.txt added
 1 file changed, 1 insertion(+)
 create mode 100644 readme.txt

$ git status
On branch master
nothing to commit, working tree clean
```

## Where is `readme.txt`

\begin{center}
\includegraphics[width=0.8\textwidth]{./images/git_workflow_in_repo.pdf}
\end{center}

## One more check

```console
$ git log
commit af84a5e... (HEAD -> master)
Author: Dawid Zalewski <d.r.zalewski@saxion.nl>
Date:   Wed Aug 11 14:56:28 2021 +0200

    readme.txt added
```

The original file remains in the folder.

By the way, it's in the *Staging Area* as well.

## Let's modify something

Open `readme.txt` and add some text / modify something.

```console
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what
   will be committed)
  (use "git checkout -- <file>..." to
   discard changes in working directory)

        modified:   readme.txt

no changes added to commit 
 (use "git add" and/or "git commit -a")
```

## Git recognizes the changes

\begin{center}
\includegraphics[width=0.8\textwidth]{./images/git_workflow_changes.pdf}
\end{center}

## Back to the Staging Area

```console
$ git add .
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   readme.txt
```

## `git add .`

```console
$ git add .
```

* `.` is de current directory (incl. sub-dirs)
* You can also add files individually
  (by mentioning their names)
* **Please note!** Works only *within* the directory containing repository

## Staging area after `git add .`

\begin{center}
\includegraphics[width=0.7\textwidth]{./images/git_workflow_add_dot.pdf}
\end{center}

Note that `readme.txt` is still in the directory.

git only acknowledges that it is ready for committing as well.

## Committing changes

```console
$ git commit -m "added a line to readme.txt"
[master 3d6f93c] added a line to readme.txt
 1 file changed, 1 insertions(+), 0 deletion(-)
 ```

## The situation after the commit

\begin{center}
\includegraphics[width=0.7\textwidth]{./images/git_workflow_two_commits.pdf}
\end{center}

We have now commits!

## One more file (try it yourself)

Create a new file (e.g. info.txt) and:

* Add it to the *Staging Area*.
* Commit it.

## One more file (code)

~~~bash
$ touch info.txt
$ code info.txt
$ git add .
$ git commit -m "info.txt added"
$ git log --oneline
~~~

## We now have two files

\begin{center}
\includegraphics[width=0.7\textwidth]{./images/git_workflow_two_files.pdf}
\end{center}

# Git time machine

## Undoing local changes

There are changes in a file (e.g. `info.txt`) that you want to undo.

```console
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." 
    to update what will be committed)
  (use "git checkout -- <file>..." 
    to discard changes in working directory)

        modified:   info.txt
```

## Undoing local changes

\begin{center}
\includegraphics[width=0.7\textwidth]{./images/git_workflow_replace_from_sa.pdf}
\end{center}

## Undoing local changes

```console
$ git checkout -- info.txt

$ git status
On branch master
nothing to commit, working tree clean
```

## Restoring a file to a previous revision

\begin{center}
\includegraphics[width=0.7\textwidth]{./images/git_workflow_timemachine.pdf}
\end{center}

## Restoring a file to a previous revision

```console
$ git log --oneline
303da9c (HEAD -> master) info.txt added
3d6f93c readme updated
af84a5e readme.txt added

$ git checkout af84a5e -- readme.txt
```

## The situation after `checkout`

```console
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   readme.txt
```

## The situation after `checkout`

\begin{center}
\includegraphics[width=0.7\textwidth]{./images/git_workflow_after_timemachine_1.pdf}
\end{center}

## The situation after `checkout`: what now?

Or: make new changes,

   followed by `git add .` & `git commit`

Or: commit directly

```console
$ git commit -m "readme.txt back to original revision"
[master 4000548] readme.txt back to original revision
 1 file changed, 1 deletion(-)
```

## The situation after `checkout` and `commit`

\begin{center}
\includegraphics[width=0.7\textwidth]{./images/git_workflow_after_timemachine_2.pdf}
\end{center}

## Just checking...

```console
$ git log --oneline
4000548 (HEAD -> master) readme.txt back to original revision
303da9c info.txt added
3d6f93c readme updated
af84a5e readme.txt added
```

# Git remote

## Why remote

\begin{center}
\includegraphics[width=0.5\textwidth]{./images/distributed.png}
\end{center}

## Github

[https://github.com/](https://github.com/)

* (Still) most popular git-hosting service
* Free for everyone (with restrictions)
* Free for education (without restrictions)
* GitHub Classroom (continued)

## Creating a new repository on GitHub

\begin{center}
\includegraphics[width=0.9\textwidth]{./images/github_create_new.png}
\end{center}

## Entering details

\begin{center}
\includegraphics[width=0.9\textwidth]{./images/github_new_repo.png}
\end{center}

## Public vs. Private

### Public

Anyone can see and copy (but not modify) the files.

Only the owner and team members can modify the files.

### Private

Only the owner and team members can see, copy or modify the files.

## Linking local with remote

\begin{center}
\includegraphics[width=1.0\textwidth]{./images/github_instructions.png}
\end{center}

## Linking an existing (local) repo with a remote

```console
$ git remote add origin
    https://github.com/SaxionACS/git_workshop.git
$ git push -u origin master
```

Replace the url in the command with your repo url!

## Alternative: cloning the remote to a new folder

```console
$ mkdir my_project
$ cd my_project
$ git clone 
  https://github.com/SaxionACS/git_workshop.git
```

## Has it worked?

\begin{center}
\includegraphics[width=1.0\textwidth]{./images/github_after_push.png}
\end{center}

## Has it worked?

```console
$ git remote -v

origin  
 https://github.com/SaxionACS/git_workshop.git (fetch)
origin  
 https://github.com/SaxionACS/git_workshop.git (push)
```

## What's next?

It depends:

* Solo user
* Team user

## Remote for a solo user

```console
$ git pull
[work on project]
$ git status
$ git add .
$ git commit -m "..."
$ git push
```

- `pull`: Changes remote -> local
- `push`: Changes local -> remote

## Remote for a team: collaborators

\begin{center}
\includegraphics[width=1.0\textwidth]{./images/github_collab.png}
\end{center}

## Remote for a team: initialization

Everyone must point their local repo to the same remote.

One person takes care of the initialization of the remote repository.

Then:

```console
$ git clone 
  https://github.com/SaxionACS/git_workshop.git
```

## Remote for a team: workflow

```console
$ git pull --rebase
[work on files]
$ git status
$ git add .
$ git commit -m "..."
$ git pull --rebase
$ git push
```

`--rebase` enables "simple" commit history

## Working with remote

\begin{center}
\includegraphics[width=0.9\textwidth]{./images/git_workflow_remote.pdf}
\end{center}

# GitHub for education

## GitHub for students

* Free pro accounts
* Some extra freebees
* Check [https://education.github.com/pack](https://education.github.com/pack) for more info
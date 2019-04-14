---
title: Git en versiebeheer
subtitle: niet alleen voor coders
author: Dawid Zalewski
date: \today{}
# theme: Dresden
colortheme: default
fontfamily: noto-sans
header-includes:
- \usepackage{cmbright}
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

## Versiebeheersysteem

Versiebeheer is het systeem waarin veranderingen in een bestand of groep van bestanden over de tijd wordt bijgehouden, zodat je later specifieke versies kan opvragen.

## Waarom versiebeheer

* Terughalen van eerdere versies van bestanden of het hele project
* Bekijken wijzigingen tussen twee momenten in de tijd
* Opvolgen wie wat aangepast heeft

## Lokale versiebeheersystemen

\begin{center}
\includegraphics[width=0.6\textwidth]{./images/local.png}
\end{center}

## Gecentraliseerde versiebeheersystemen

\begin{center}
\includegraphics[width=0.7\textwidth]{./images/centralized.png}
\end{center}

## Gedistribueerde versiebeheersystemen

\begin{center}
\includegraphics[width=0.5\textwidth]{./images/distributed.png}
\end{center}

## Wat is git

Git is een *gedistribueerd* versiebeheersysteem

* Elk teamlid kan onafhankelijk werken
* Bijna alle handelingen zijn **lokaal**
* Iedereen heeft een lokale kopie van de database (repository)

## Om te beginnen

* Git client: [http://git-scm.com/download/](http://git-scm.com/download/)
  * Pak de juiste versie voor jouw systeem,
  * Inclusief *Git Bash* (alleen Windows)
* GUI tool: [http://git-scm.com/downloads/guis](http://git-scm.com/downloads/guis)
    * Bijv. [Github Desktop](https://desktop.github.com/)

\begin{block}{Info}
\center{Wij gaan (proberen) geen GUI tools te gebruiken.}
\end{block}

## Aan de slag - een paar instellingen

Git moet weten wie jij bent:

```bash
$ git config --global user.name "Dawid Zalewski"
$ git config --global user.email "d.r.zalewski@saxion.nl"
```

## Aan de slag - tekst editor

Je kan ook de default tekst editor aanpassen:

Voor Notepad++:

```bash
$ git config --global core.editor 
"'notepad++.exe' -multiInst -nosession"
```

For Visual Studio Code:

```bash
$ git config --global core.editor "code --wait"
```

## Aan de slag - controleer de instellingen

```bash
$ git config --list
```

# Lokaal versiebeheer

## Initialiseer repository

```bash
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

## Drie toestanden

Er zijn drie toestanden waarin bestanden zich kunnen bevinden:

* _gewijzigd_ ('modified'),
* _voorbereid_ voor een commit ('staged')
* _gecommit_ ('commited'),

## Drie toestanden

\begin{block}{Modified}
Een bestand is gewijzigd maar nog niet naar de database gecommit
\end{block}

\begin{block}{Staged}
Een aangepast bestand wordt in de volgende commit meegenomen
\end{block}

\begin{block}{Committed}
Alle data zit veilig in de lokale database
\end{block}

## Git workflow & omgeving

\begin{center}
\includegraphics[width=0.8\textwidth]{./images/git_workflow.pdf}
\end{center}

## Werkomgeving

### Working directory

De directorystructuur en bestanden waarin je wijzigingen aanbrengt

### Staging Area

*Tussenstation* tussen **working directory** en **repository**

Laat toe wijzigingen selectief te *committen*

### Repository

Verzameling (backup database) van alle commits, branches, tags, ...

## Eerste commit

Maak een nieuw bestand aan (readme.txt) in de `my_project` map

Voor VS Code gebruikers:

```bash
$ code readme.txt
```

* Type wat tekst in en sla op.

## Contoleer

```bash
$ ls -l

total 1
-rw-r--r-- 1 zalda 197609 7 Apr 11 12:55 readme.txt
```

## Git status

```bash
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

## Waar is `readme.txt`

\begin{center}
\includegraphics[width=0.8\textwidth]{./images/git_workflow_wd.pdf}
\end{center}

## Naar de *Staging Area*: `git add`

```bash
$ git add readme.txt
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

  new file:   readme.txt
```

## Waar is `readme.txt`

\begin{center}
\includegraphics[width=0.8\textwidth]{./images/git_workflow_sa.pdf}
\end{center}

## Een commit toevoegen: `git commit`

```bash
$ git commit -m "readme.txt toegevoegd"
[master (root-commit) af84a5e] readme.txt toegevoegd
 1 file changed, 1 insertion(+)
 create mode 100644 readme.txt

$ git status
On branch master
nothing to commit, working tree clean
```

## Waar is `readme.txt`

\begin{center}
\includegraphics[width=0.8\textwidth]{./images/git_workflow_in_repo.pdf}
\end{center}

## Even checken

```bash
$ git log
commit af84a5e... (HEAD -> master)
Author: Dawid Zalewski <d.r.zalewski@saxion.nl>
Date:   Thu Apr 11 14:56:28 2019 +0200

    readme.txt toegevoegd
```



Het originele bestand blijft in de map zitten.

Trouwens ook in de Staging Area.

## Laten we iets aanpassen

Open `readme.txt` en voeg wat tekst toe / pas iets aan.

```bash
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

## Git herkent de wijzigingen

\begin{center}
\includegraphics[width=0.8\textwidth]{./images/git_workflow_changes.pdf}
\end{center}

## Alweer naar de Staging Area

```bash
$ git add .
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   readme.txt
```

## `git add .`

```bash
$ git add .
```

* `.` is de huidige directory (incl. onderliggende)
* Je kan ook bestanden individueel toevoegen
  (door zijn namen te vermelden)
* **Let op!** Werkt enkel *binnen* de directory met repository

## Staging area na `git add .`

\begin{center}
\includegraphics[width=0.7\textwidth]{./images/git_workflow_add_dot.pdf}
\end{center}

Let op: `readme.txt` zit nog steeds in de map.

git erkent slechts dat hij ook voor het commiten klaar is.

## Wijzigingen commiten

```bash
$ git commit -m "een regel in readme.txt toegevoegd"
[master 3d6f93c] een regel in readme.txt toegevoegd
 1 file changed, 1 insertions(+), 0 deletion(-)
 ```

## De situatie na de commit

\begin{center}
\includegraphics[width=0.7\textwidth]{./images/git_workflow_two_commits.pdf}
\end{center}

Wij hebben nu twee commits!

## Een bestandje verder (zelf proberen)

Maak een nieuwe file aan (bijv. info.txt) en:

* Voeg hem aan de Staging Area toe.
* Commit hem.

## Een bestandje verder (code)

~~~bash
$ touch info.txt
$ code info.txt
$ git add .
$ git commit -m "Initiële revisie info.txt"
$ git log --oneline
~~~

## Nu hebben wij twee files

\begin{center}
\includegraphics[width=0.7\textwidth]{./images/git_workflow_two_files.pdf}
\end{center}

# Git time machine

## Locale wijzigingen ongedaan maken

Er zitten wijzigingen in een bestand (bijv. `info.txt`) die je ongedaan wilt maken.

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." 
    to update what will be committed)
  (use "git checkout -- <file>..." 
    to discard changes in working directory)

        modified:   info.txt
```

## Locale wijzigingen ongedaan maken

\begin{center}
\includegraphics[width=0.7\textwidth]{./images/git_workflow_replace_from_sa.pdf}
\end{center}

## Locale wijzigingen ongedaan maken

```bash
$ git checkout -- info.txt

$ git status
On branch master
nothing to commit, working tree clean
```

## Een bestand naar een eerdere revisie zetten

\begin{center}
\includegraphics[width=0.7\textwidth]{./images/git_workflow_timemachine.pdf}
\end{center}

## Een bestand naar een eerdere revisie zetten

```bash
$ git log --oneline
303da9c (HEAD -> master) info.txt toegevoegd
3d6f93c readme updated
af84a5e readme.txt added

$ git checkout af84a5e -- readme.txt
```

## De situatie na de checkout

```bash
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   readme.txt
```

## De situatie na de checkout

\begin{center}
\includegraphics[width=0.7\textwidth]{./images/git_workflow_after_timemachine_1.pdf}
\end{center}

## De situatie na de checkout: wat nu?

Of: nieuwe wijzigingen aanbrengen,

   vervolgd  door `git add .` & `git commit`

Of: direct commiten

```bash
$ git commit -m "readme.txt naar originele revisie"
[master 4000548] readme.txt naar originele revisie
 1 file changed, 1 deletion(-)
```

## De situatie na de checkout en commit

\begin{center}
\includegraphics[width=0.7\textwidth]{./images/git_workflow_after_timemachine_2.pdf}
\end{center}

## Even controlleren...

```bash
$ git log --oneline
4000548 (HEAD -> master) readme.txt naar originele revisie
303da9c info.txt toegevoegt
3d6f93c readme updated
af84a5e readme.txt added
```

# Git remote

## Waarom remote

\begin{center}
\includegraphics[width=0.5\textwidth]{./images/distributed.png}
\end{center}

## Github

[https://github.com/](https://github.com/)

* Meest populaire git-hosting service
* Gratis voor iederen (met beperkingen)
* Gratis voor onderwijs (zonder beperkingen)
* GitHub Classroom (verder)

## Een nieuwe repository op GitHub aanmaken

\begin{center}
\includegraphics[width=0.9\textwidth]{./images/github_create_new.png}
\end{center}

## Details invoeren

\begin{center}
\includegraphics[width=0.9\textwidth]{./images/github_new_repo.png}
\end{center}

## Public vs. Private

### Public

Iedereen kan de bestanden zien en kopiëren (maar niet wijzigen).

Alleen de eigenaar en de teamleden kunnen de bestanden aanpassen.

### Private

Alleen de eigenaar en de teamleden kunnen de bestanden zien, kopiëren of aanpassen.

## Lokaal en remote koppelen

\begin{center}
\includegraphics[width=1.0\textwidth]{./images/github_instructions.png}
\end{center}

## Een bestande repo met een remote koppelen

```bash
$ git remote add origin
    https://github.com/SaxionACS/git_workshop.git
$ git push -u origin master
```

## Alternatief: remote clonen naar een nieuwe map

```bash
$ mkdir my_project
$ cd my_project
$ git clone 
  https://github.com/SaxionACS/git_workshop.git
```

## Is het gelukt?

\begin{center}
\includegraphics[width=1.0\textwidth]{./images/github_after_push.png}
\end{center}

## Is het gelukt?

```bash
$ git remote -v

origin  
 https://github.com/SaxionACS/git_workshop.git (fetch)
origin  
 https://github.com/SaxionACS/git_workshop.git (push)
```

## Wat nou

Het hangt eraf:

* Solo gebruiker
* Team gebruiker

## Remote voor een solo gebruiker

```bash
$ git pull
[bewerk bestanden]
$ git status
$ git add .
$ git commit -m "..."
$ git push
```

- `pull`: Wijzigingen remote -> lokaal
- `push`: Wijzigingen lokaal -> remote

## Remote voor een team: collaborators

\begin{center}
\includegraphics[width=1.0\textwidth]{./images/github_collab.png}
\end{center}

## Remote voor een team: initializatie

Iedereen moet zijn lokale repo naar dezelfde remote verwijzen.

Één person zorgt voor de initialisatie van de remote repository.

Dan:

```bash
$ git clone 
  https://github.com/SaxionACS/git_workshop.git
```

## Remote voor een team: workflow

```bash
$ git pull --rebase
[bewerk bestanden]
$ git status
$ git add .
$ git commit -m "..."
$ git pull --rebase
$ git push
```

`--rebase` zorgt voor "eenvoudige" historiek

## Werken met remote

\begin{center}
\includegraphics[width=0.9\textwidth]{./images/git_workflow_remote.pdf}
\end{center}

# GitHub voor onderwijs

## GitHub voor docenten

* Koppel aan emailadres van je school aan je GitHub account
* Registreer je op GitHub Education: [https://education.github.com/teachers](https://education.github.com/teachers)
* Maak nieuwe Github "organisatie" aan
    * bijv. naam van je school of vak of project
* Vraag korting aan: [https://education.github.com/discount_requests/new](https://education.github.com/discount_requests/new)
* Je kan ook korting voor jouw persoonlijke account aanvragen.

## GitHub classroom

\begin{center}
\includegraphics[width=1.0\textwidth]{./images/github_classroom.png}
\end{center}

[https://classroom.github.com](https://classroom.github.com)

## Wat kun je ermee

* Opdrachten voor studenten zetten:
  [https://github.com/SaxionACS/AdventOfCode](https://github.com/SaxionACS/AdventOfCode)
* Presentaties maken;):
 [https://github.com/SaxionACS/git_workshop](https://github.com/SaxionACS/git_workshop)
  
## Mogelijkheden

- Feedback geven
    - issues, pull requests, commentaar
- Verbeteringen aanbrengen
    - online bestanden aanpassen
- Vooruitgang opvolgen
    - commit log (wie, wat, wanneer)
- Samenwerking beoordelen
  - commit log (wie, wat, wanneer)
- Discussies opvolgen
- Project plannen

## Demo & vragen

### Tijd voor demo & vragen

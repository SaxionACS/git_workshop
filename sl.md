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

- \addtobeamertemplate{frametitle}{}{ \begin{textblock*}{100mm}(0.9\textwidth,-1.25cm) \includegraphics[height=0.55cm,keepaspectratio]{logo.png} \end{textblock*}}
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
    * bv. [Github Desktop](https://desktop.github.com/)

\begin{block}{Info}
\center{Wij gaan (proberen) geen GUI tools te gebruiken.}
\end{block}

## Aan de slag - een paar instellingen

Git moet weten wie jij bent:

```bash
$ git config --global user.name "Dawid Zalewski"
$ git config --global user.email "d.r.zalewski@saxion.nl"
```

# Git & GitHub Workshop

This repository contains slides for a 2 hour git workshop for educators.

To create a pdf version of the presentation:

Install [pandoc](https://pandoc.org/) and make sure you have an up-to-date latex distribution with the `beamer` package installed.

Then:

```bash
pandoc -t beamer --slide-level=2 slides.md -o slides.pdf
```
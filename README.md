# The `image-handout` package

The  `image-handout`  allows you to quickly generate a handout from 
 a sequentially numbered set of screen shot images.

It provides a setup command `\SetupHandout` and a single command to insert a set of images `\insertimages`.

Images are expected to be sequentially numbered with a common image prefix, example: `MyPrefix1.png`, `MyPrefix2.png` etc.  Leading zeros should be avoided. 

How you create the images is up to you, but for Mac users, a couple of simple apps are provided to choose a folder to save screenshots and rename a set of screen shot files.

# Installation

Download the helper apps zip file [here](https://github.com/amunn/image-handout/blob/main/scripts/MacHelperApps.zip)  These should be installed in your Applications folder. 

Install the LaTeX package in your local `texmf` folder: on a Mac this will be `~/Library/texmf/tex/latex`. If you don't have this folder you will need to create it. 

If you're using Overleaf, upload the `.sty` file to your project. 

# How to make good screen shots

On a Mac, the default location for screenshots is the Desktop, but this is not very practical as a place for this use, so I've provided a small helper app `SetScreenShotFolder.app` that lets you choose a specific folder to store the iamges in.  A sensible organization would be to store the images in their own folder inside the folder containing the `.tex` file.

In order for your images to look uniform in a handout, you need to make sure that they are all (approximately) the same size. The best way to ensure this is to view the PDF at regular size, and then screenshot the entire width of the document for every example no matter how big or small it is.   The command to make a screen shot on a Mac is Command-Option-4, which then gives you a draggable guide to select the region to screen shot.

It's really a good idea to make all the screenshots at once. Even for a large paper this only takes a few minutes.

# Renaming the screenshots

The package assumes that each screenshot is numbered sequentially in a form `Prefix1.png`, `Prefix2.png`, etc. so I've provided a second helper app `RenameImages.app` to rename all the .png files in a folder sequetially with a common prefix. This app sorts the files sequentially by modification timestamp, so you should only run it once otherwise your screenshots may get out of order.

# Package commands

There are two main commands, a setup command `\SetupHandout` to set global parameters, and an insertion command `\insertimages`, which can also use local key-value setup options.

## Setup command

 - `\SetupHandout{}`
    - `prefix=<image-prefix>`
    - `end=<number of images>`
    - `path=<path to folder containing the images`
    - `start=<starting number>` (defaults to 1)

## Insertion command

 - `\insertimages[<local options]`
    

## Sample document

The simplest document would simply specify the location of the files, the image prefix and the number of images.

```
\documentclass{article}
\usepackage[margin=1in]{geometry}
\usepackage{image-handout}
\SetupHandout{prefix=myImage,end=20,path=ImageFolder}
\title{Your title}
\author{Citation of the paper}
\date{}
\begin{document}
\maketitle
\insertimages
\end{document}
```

## Good citation practices

It's important to make it clear where your examples are coming from, so I always make the `\author` field the actual citaion of the paper. If you use `biblatex` this is very simple. Suppose you have a `.bib` file entry `Author2022` you would do the following, which puts the title of the paper as the title of the handout, and the full citation as the author. Of course if your handout has more content than just the paper, you may want to add a separate bibliography elsewhere in the document. 

```
\usepackage[style=apa]{biblatex}
\addbibresource{your-bib-file.bib}
\title{\citetitle*{Author2022}}
\author{\fullcite{Author2022}}
```

## Mixed documents

If you are interspersing text between examples, such as section headings or your own text and examples, you may not want to include all the images at one time. Or if you are combining images from more than one paper you may have them in different folders with different image prefixes. In this case you would supply the relevant parameters directly as options to the `\insertimages` command.  Here's an example. 

```
\documentclass{article}
\usepackage[margin=1in]{geometry}
\usepackage{image-handout}
\SetupHandout{prefix=myImage,end=20,path=ImageFolder}
\title{Your title}
\author{Citation of the paper}
\date{}
\begin{document}
\insertimages[end=5]
Some more text
\insertimages[start=6,end=10]
Some more text
\insertimages[path=SecondImageFolder,prefix=SecondPrefix,end=5]
\end{document}
```


# The fine print

 Copyright 2024 by Alan Munn

 This package may be distributed and/or modified under the
 conditions of the LaTeX Project Public License, either version 1.3
 of this license or any later version.
 The latest version of this license is in
   http://www.latex-project.org/lppl.txt
 and version 1.3 or later is part of all distributions of LaTeX
 version 2005/12/01 or later.

 This package has the LPPL maintenance status `maintained'.
 
 The Current Maintainer of this package is Alan Munn.

 This package consists of the file `image-handout.sty` and documentation files
 `README.md`

 This package is currently experimental. Use at your own risk.

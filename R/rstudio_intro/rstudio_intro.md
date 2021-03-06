R for beginners using RStudio
===

`version: 2018-05-17`

> These notes are available on GitHub: https://github.com/stragu/CDS/blob/master/R/rstudio_intro/rstudio_intro.md

If you want to review the installation instructions: https://github.com/stragu/CDS/blob/master/R/Installation.md

## RStudio

RStudio is an open source IDE (Integrated Development Interface) for the R programming language.
We can use R for calculations and visualisations.

## Keep in mind

* Case sensitive
* No spaces in names
* Be ready to learn a new language, lots of new vocabulary

## Open RStudio

* If you are using your own laptop please open RStudio
  * Make sure you have a working internet connection

* On CDS computers:
  * Log in with your UQ username and password
  * Make sure you have a working internet connection
  * Go to search at bottom left corner (magnifiying glass) 
  * Open the ZENworks application
  * Look for the letter R 
  * Double click on RStudio which will install both R and RStudio 

## What are we going to learn?

At the end of this session you will be able to:

   * Create a project for data analysis
   * Create a folder structure
   * Know where to find help
   * Import files/datasets
   * Understand and move around layouts 
   * Use a few shortcuts
   * Know where packages are

## Material

### Rstudio Project

**Exercise 1** - New RStudio Project

* Click the "File" menu button (top left corner), then "New Project"
* Click "New Directory"
* Click "New Project" ("New empty project" if you have an older version of RStudio)
* In Directory name type the name of your project, e.g. "rstudio_intro" (Browse and select a folder where to locate your project, in our case the RProjects folder. If you don't have an RProjects folder, create it.)
* Click the "Create Project" button

:::info
Projects make managing multiple directories straightforward. You can create a .Rproj file in a new directory or an existing directory that already has R code and data. The .Rproj file stores information about our folder structure and the objects in the project (hence, manages history and .RData).
:::

### Maths and objects

R can be used like a calculator. Try the following commands:

```
3 * 4
10 / 2
11^6
```

We can store data by creating objects, and assigning values to them with the assignement operator `<-`:

```
x <- 42
y <- x / 9
```

You can use the shortcut Alt + - to type the assignement operator quicker.

### Using functions

An R function looks like this:

```
<functionname>(<argument(s)>)
```

In the console, we write a command and then execute it by pressing Enter.

For example, try running the following command:

```
log10(x)
```

#### Help

There are 3 ways to find help about a function in RStudio:

1. the shortcut command: `?functionname`
1. the help function: `help(functionname)`
1. the keyboard shortcut: press F1 after writing a function name

**Exercise 2** - Use the help pages to find out what these functions do:

* `sessionInfo()`
* `list.files()`
* `citation()`
* `setwd()`

`sessionInfo()` provides information about your platform, the version of R and the packages that you are using and their versions.

`list.files()` lists all the files in your working directory.

`citation()` outputs the proper way to cite the R software.

`setwd()` changes the working directory, i.e. the directory where we are located. This function _requires_ an argument: it can't run without setting a value for `dir` because it does not have a default for it.

Let's do some operations with two new functions:

`ls()` lists the objects in the current R environment.
For example, try running the `ls()` function after executing the command `a <- 42`.
Now, remove that object with the following command:

```
rm(a)
```

And list objects again with `ls()`.

You can also remove all the objects in the environment by using `ls()` as the value for the `list` argument:

```
rm(list = ls())
```

### Creating a folder structure

We are creating 2 folders:

* scripts
* data

For that, we use the function `dir.create()`:

```
dir.create("scripts")
dir.create("data")
```
    
**Exercise 3** - create a folder called "plots"

To create a folder called "plots":

```
dir.create("plots")
```

### Scripts

Scripts are useful to save a set of useful commands and make research reproducible.

**Exercise 4** - Create a new R script file

* click the button (+) located at the top left corner of your RStudio
* click on R script
* Save the file: File > Save (or ctrl + s or command + s)
* name the file "myscript.R"
* locate this file under the "scripts" folder

You can also create a script with the following command:

```
file.create("scripts/cmds.R")
```

... or using the shortcuts Ctrl + Shift + N (or Cmd + Shift + N).

To delete a file, use the `file.remove()` function:

```
file.remove("scripts/cmds.R")
```

You can recall your recent commands with the up arrow, which is especially useful to correct typos or slightly modify a long command.

**Exercise 5** - Add comments to your new R script file

Comments start with `#`

```
# Description:
# Author:
# Date:
```

To add comments to many lines: Ctrl + Shift + C or Cmd + Shift + C

While editing your script, you can run the active line (or the selected block of lines) by using Ctrl + Enter (or Cmd + Enter).

Instead of opening an RProject, you can open an R script and directly execute its content. This is helpful to re-run a whole project from the beginning (including necessary `library()` commands).

### Import files

**Exercise 6** - Read the description of these functions:

```
?download.file
?read.table
?read.csv
```

**Exercise 7** – Import data

Copy, paste and execute the following two commands:

```
download.file(url = "https://raw.githubusercontent.com/resbaz/r-novice-gapminder-files/master/data/gapminder-FiveYearData.csv",
  destfile = "data/gapminderdata.csv")
gapminder <- read.csv("data/gapminderdata.csv")
```

What do you think they do? Describe each one in detail.

You can type the name of your new object to print it to screen:

```
gapminder
```

Now find out more about the `str()` function, and have a look at the data:

```
?str
str(gapminder)
```

Remember that you can check what is in your environment with `ls()`, and remove objects with `rm()`.

### Packages

Packages add functionnalities to R and RStudio. There are more than 15000 available.

You can see the list of installed packages in your "Packages" tab, or by using the `library()` function without any argument.

We are going to install and load a new package that is useful for data visualisation: `ggplot2`.

```
?install.packages
?ggplot
??ggplot
install.packages("ggplot2")
?ggplot
?ggplot2::ggplot
library(ggplot2)
?ggplot
```

### Plotting

R has a number of base plotting functions to visualise data in many different ways, but the package `ggplot2` introduces a logic that makes data visualisation more streamlined, called "Grammar of graphics".

In its most basic form, a `ggplot2` plot needs a dataset, data mapped to aesthetics, and a geometry.

```
ggplot(gapminder, aes(x = year, y = pop)) +
  geom_point()
```

We can then add layers, map mor data to aesthetics, and further modify elements. For example, we can map the `colour` easthetic to the `continent` data.

### More shortcuts

* Run current line/selection: Ctrl + Enter (or Cmd + Enter)
* Find: Ctrl + F (or Cmd + F)
* Find in files: Ctrl + Shift + F (or Cmd + Shift + F)
* Cut: Ctrl + X (or Cmd + X)
* Copy: Ctrl + C (or Cmd + C)
* Paste: Ctrl + V (or Cmd + V)
* Select all: Ctrl + A (or Cmd + A)
* Delete line: Ctrl + D (or Cmd + D)
* Clear console: Ctrl + L (or Cmd  + L)
* Indent: Tab (at start of line)
* Outdent: Shift + Tab
* Insert `<-`: Alt + - (or Option + -)
* (Un)Comment lines: Ctrl + Shift + C (or Cmd + Shift + C)
* See shortcuts: Alt + Shift + K

#### Layouts

* Move focus to Source Editor Ctrl+1
* Move focus to Console Ctrl+2
* Move focus to Help Ctrl+3
* Show History Ctrl+4
* Show Files Ctrl+5
* Show Plots Ctrl+6
* Show Packages Ctrl+7
* Show Environment Ctrl+8
* Show Git/SVN or viewer Ctrl+9

### Demos

A real life example to use R graphics:

```
demo(graphics)
```

# Close Rproject

* File
* close project (It asks if you want to save your data)
* close RStudio

When you create a **project** in RStudio, it create an .Rproj file that gathers information about your project, and it allows you to save your **workspace** inside an .Rdata file. The .Rdata file is by default used to reload your workspace when you open your Rproject again. That brings back quite a few things, including the objects loaded in your **environment**, whatever source file (e.g. script) you had open, and your command history. You will find your command history in the "History" tab (upper right panel): all the commands that we used should be in there.
The console, on the other hand, only shows a brand new R **session**. Sessions are not persistent, and a new one is started when you open your project again, which is why you have to load any extra package your work requires again with the `library()` function.

## Important links

* RStudio Cheatsheet https://github.com/rstudio/cheatsheets/raw/master/rstudio-ide.pdf
* RStudio online learning https://www.rstudio.com/online-learning/
* Basic and advanced manuals https://cran.r-project.org/manuals.html
* Ask about any function or package http://www.rdocumentation.org/
* If you are looking how-to's or how to fix an error http://stackoverflow.com/questions/tagged/r
* Lynda.com R training and tutorials https://www.lynda.com/R-training-tutorials/1570-0.html remember to sign in with your organisational portal, https://web.library.uq.edu.au/library-services/training/lyndacom-online-courses)
* ANOVA in R http://homepages.inf.ed.ac.uk/bwebb/statistics/ANOVA_in_R.pdf or https://rcompanion.org/rcompanion/e_01.html
* R gapminder csv https://raw.githubusercontent.com/resbaz/r-novice-gapminder-files/master/data/gapminder-FiveYearData.csv
* If you need an R and/or RStudio workshop/session, please contact Centre for Digital Scholarship staff to organise one for you. 
https://web.library.uq.edu.au/locations-hours/centre-digital-scholarship
## Operator Notes:

As part of creating this book there are a bunch of new processes that I've had to get comfortable with. Here is the documentation for those steps for future reference. The primary reference I have used, with  lots of help from other sources, is the [Jupyterbook tutorial](https://jupyterbook.org/start/your-first-book.html).

### jbook-2 Environment: 9/1/2025

There has been a serious upgrade so I will be building a new Anaconda environment called jbook2 which will probably (but not certainly) be a substitute for jbook in the following operator notes. First....

**New Anaconda Env:**

[This stackoverflow post](https://stackoverflow.com/questions/41060382/using-pip-to-install-packages-to-an-anaconda-environment) seems incredibly helpful. This is where I will start.

**Install jupyter{book} v2:**

[This guide](https://next.jupyterbook.org/start/install/) from jupyter{book} seems most useful. Important to note that a standard conda install is not available at this time. Proceed cautiously!

**Upgrading 'old' books:**

Nicely enough the jupyterbook people have done some work to make it easier to convert version 1 books to version 2 books. [This page](https://next.jupyterbook.org/upgrade/) documents that process. I'll probably try it with the DPL book first since it's small and barely started. Less loss if the process blows up.

***MyST Information:**   

Start here: [https://mystmd.org/guide/quickstart#configure-site-and-page-options](https://mystmd.org/guide/quickstart#configure-site-and-page-options)

### jbook Environment:

I'm still need reminders in this environment but am realizing that creating a few separate environments for projects that need distinct software packages reduces the opportunities for conflicts between the different packages. 

The initial step is to start Jupyterlab from the jbook environment in Anaconda. This apparently connects all the paths appropriately this collection of software packages. **Note:** Ben R notes that he now works entirely in python and never uses Jupyterlab but I still think connecting the documentation and coding in one notebook is the best mode for me. Just noting....

In the terminal window the prompt will indicate the active environment and even if I open Jupyterlab from the jbook environment the (base) environment will be where the terminal lands. The prompt will look something like this.

```
(base) bruceemerson@Bruces-MacBook-Pro ~ %
```

When starting to work on the book activate the jbook environment using ``` conda activate jbook```.
```
(base) bruceemerson@Bruces-MacBook-Pro ~ % conda activate jbook
```
After doing so the prompt will indicate the jbook environment.
```
(jbook) bruceemerson@Bruces-MacBook-Pro book % 
```

### Navigate to root directory:

The next step is to navigate to the root directory for the book. This is the directory which contains the \_toc.yml file as well as the\_build folder where the built book is stored. Navigate using the usual 'cd', 'ls', and 'pwd' unix tools to navigate. Here is the ultimate destination for the Barca22 book.
```
/Users/bruceemerson/Documents/Jupyter/JupyterLabRepos/DPLMakerspace/3DPrinterBasics
```
### Build the book:

The book is built locally with the 'jupyterbook build' using the 'jb' shorthand. jupyterbook has a number of expectations about the nesting of markdown language and I usually get lots of red violations
```
(jbook) bruceemerson@Bruces-MacBook-Pro book % jb build .
```
jupyterbook has a number of expectations about the nesting of markdown language and I usually get lots of red violations like the following but they don't seem to keep the book from being built.
```
/Users/bruceemerson/Documents/Jupyter/JupyterLabRepos/DPLMakerspace/book/barcaSAE/Schedule.md:1: WARNING: Non-consecutive header level increase; 0 to 2 [myst.header]
```
This is the happy message I hope to get at the end of the build process.
```
===============================================================================

Finished generating HTML for book.
Your book's HTML pages are here:
    _build/html/
You can look at your book by opening this file in a browser:
    _build/html/index.html
Or paste this line directly into your browser bar:
    file:///Users/bruceemerson/Documents/Jupyter/JupyterLabRepos/Barca22/book/_build/html/index.html            

===============================================================================
```

### Public Book

I plan for this 'book' to be public but I'm not sure all that that will entail. 

### Build the book:

The book is built locally with the 'jupyterbook build' using the 'jb' shorthand. jupyterbook has a number of expectations about the nesting of markdown language and I usually get lots of red violations
```
(jbook) bruceemerson@Bruces-MacBook-Pro book % jb build .
```
jupyterbook has a number of expectations about the nesting of markdown language and I usually get lots of red violations like the following but they don't seem to keep the book from being built.
```
/Users/bruceemerson/Documents/Jupyter/JupyterLabRepos/Barca22/book/barcaSAE/Schedule.md:1: WARNING: Non-consecutive header level increase; 0 to 2 [myst.header]
```
This is the happy message I hope to get at the end of the build process.
```
===============================================================================

Finished generating HTML for book.
Your book's HTML pages are here:
    _build/html/
You can look at your book by opening this file in a browser:
    _build/html/index.html
Or paste this line directly into your browser bar:
    file:///Users/bruceemerson/Documents/Jupyter/JupyterLabRepos/Barca22/book/_build/html/index.html            

===============================================================================
```

### Creating the gh-pages branch:

The book that is built in the previous step has all the html files in the \_build folder and can be viewed on my local computer but aren't accessible (generally) to the broader public. In my feeble understanding the default characteristics of a git repo do not imagine that the user is accessing main branch files as source files for a static web page. gh-pages are a type of directory in the repo that does support use of the files as a static webpage source. [This portion](https://jupyterbook.org/start/publish.html) of the jupyterbook tutorial describes publishing the book using gh-pages. I installed the ```ghp-import``` package and worked out the kinks. This command line updates the gh-pages branch of the repo.

```
(jbook) bruceemerson@Bruces-MacBook-Pro book % ghp-import -n -p -f _build/html
```
Current PAT (personal access token)  

Expires October 2 2026!

**To regenerate the PAT use this link which stays the same (I think).**

This document will guide setting up generating the token. When I most recently did this I was unable to generate a fine grain token so I generated a 'classic' token (the one that expires 10/2/2026)

https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-fine-grained-personal-access-token

When the new PAT is regenerated the first ghp-import call will need to be without the -f (force) option so that the script has to login again and provide the new PAT. 
```
ghp-import -n -p _build/html
```

During the execution I may be asked for my user name and password for my github repo. Since Aug 2021 actually passwords are no longer accepted and a personal access token (PAT) is required to access the repo this way. PAT's have expiration dates and need to be regenerated from time to time. [This doc](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) will provide guidance. Remember to copy and save the actual PAT which is provided at the end of the process. There is no way to access this code after this point. If I lose it I suspect it may be aggravating to reset and generate a new one. Check the handy folder in Document/Bruce Personal. Copy/Paste to drop the PAT in for the password.

```
Username for 'https://github.com': smithrockmaker
Password for 'https://smithrockmaker@github.com': 
```

### Accessing the Webpages:

Going to the github repo for the book choose the gh-pages branch. Then examine the settings window (gear top right) to see the root webpage for the site. The first time the pages are created this needs to be edited to direct the user to the correct .html web source.

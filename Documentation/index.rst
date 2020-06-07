=============
Documentation
=============

| This proyect has been documented using **Sphinx**.
| Sphinx is a Python tool that makes it easy to create well done documentation. 
| Some of it features are the following

- Based in reStructuredText and Markdown markup languages.
- Output formats; HTML, LaTeX, ePub, Texinfo, manual pages, plain text.
- Extensive cross-references: semantic markup and automatic links for functions, classes, citations, glossary terms and more.
- Hierarchical structure: Based on a document tree with automatic links to siblings, parents and children.
- Code handling: automatic highlighting using the Pygments highlighter.
- Extensions: automatic testing of code snippets, inclusion of docstrings from Python modules (API docs), and more.
- Contributed extensions: more than 50 extensions contributed by users.

Deployment
==========

| The documentation has been created on an Ubuntu 19.04 virtual machine. No further explanation about the VM configuration is needed, after finishing the document is going to be deleted.
| To install Sphinx I executed the following commands;

.. code-block:: bash

   sudo apt-get update
   sudo apt-get install python
   sudo apt-get install python-pip
   sudo pip install -U sphinx
   cd ~/Documents

| The root path for the documentation is located at ~/Documents. In that directory I ran the command ``sphinx-quickstart`` which is a wizard that will setup an initial document which can be used as a pattern.
| 
| It's important separating the *build* and *source* directories so I can easily clean the built code and compile it as many times as I want.
| The project name is MasterServer, the authors Efren Garcia Ferez & Jose Domingo Alvarez Caba and the project version 1.0.0.
| Also its important to accept creating the *Makefile* so I can compile the code through the bash with the ``make`` command.
|
| The source code files are always in **reStructuredText** named with the xtension *.rst*, and the master document is always the *index.rst*
| ResTructuredText is a lightweight markup language designed to be processed and compiled into other formats.


-----
Theme
-----

| Sphinx supports lots of themes, both standard or created by the comunity. I used the **Material Design HTML Theme** which can be found `here <https://github.com/myyasuda/sphinx_materialdesign_theme>`__.
| 
| To install it simply run ``pip install sphinx_materialdesign_theme``. 
| In the *source/conf-py* file all the document settings can be edited, including the **Pygments** style, which is a syntax highlighter.
| The Pygments styles can be found `here <https://help.farbox.com/pygments.html>`__ and also try the different styles using a live demo `here <https://pygments.org/demo/#try>`__.
| 
| The theme features an attractive web interface and easy navigation. It can also be tuned by changing the banner and accent colors, along with the banner icon links.
| Each page, apart from the document, includes the following features

- Source code, which can be seen clicking the *< >* button on the top right corner. That means the reStructuredText syntax is self-documented.
- Search content, which can be done clicking the magnifier next to the source code button.
- Home button.
- MasterServer webpage link.
- GitHub full document link.

---------
Compiling
---------

| Sphinx supports a wide variety of output formats. Some of them are LaTeX PDF, ePUB and HTML.
| Simply changing into the document root directory and running ``make html`` will compile the source code.
| Cleaning the compiled code can be done with ``make clean``.
| To compile it as *latexpdf* first some packages need to be installed

.. code-block:: bash

   apt-get install texlive-latex-recommended
   apt-get install texlive-latex-extra
   apt-get install texlive-fonts-recommended

| Then simply run ``make latexpdf``

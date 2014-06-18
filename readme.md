Updating the CPAC UG is fairly straightforward. I use a package called Sphinx (http://sphinx-doc.org/) to generate the files from reStructuredText documents (which is like Markdown, if you're familiar with that). The Sphinx site has a good rST reference if you're new to it. If you have EPD or Anaconda, Sphinx is already installed. Otherwise you can get it through pip.

The process goes like this:
1) Extract the attached archive and put it somewhere on your local. I have a folder called /CPAC/Sphinx
2) Fork https://github.com/FCP-INDI/fcp-indi.github.com to a different folder on your local (I have /CPAC/Github)
3) Update what you want in the .rst file for the page you want to change (in the /source directory of the attached archive)
4) Run the sphinx build command to generate updated HTML pages (written to the /build directory). This command can be run from anywhere. The syntax is:
sphinx-build -b html /path/to/source/dir /path/to/build/dir
5) Check that the HTML pages contain the changes you made.
6) Copy the updated HTML pages to /docs/user/ in your github fork (replacing the old versions).
7) Commit your changes
8) Push to master (this will automatically trigger Github to update the pages, though it may take up to 15 minutes).

edit: make sure conf.py is set up.

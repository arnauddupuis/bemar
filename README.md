# bemar (Batch Episodes Move And Rename)

This very simple and autonomous software does only one thing: move and rename your TV episodes automatically.
It is written in Perl.
It requires a very limited number of dependcies that should be part of the Perl distribution for any system.

The configuration file is really straightforward. It is composed of sections that gives instructions about the pattern of the files and the place to move them.
Pattern can use some variables that are automatically set. 
Episodes have to be name according to the sXXeYY "standard" for some variables to be properly extracted.

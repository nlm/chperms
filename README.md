chperms
=======

Massively change file and directory owner and modes

SYNOPSIS
--------

    chperms [OPTIONS] <RULE FILE> <DIR [DIR ..]>

DESCRIPTION
-----------

This tool changes owner/group and modes in a directory tree, according to a rule file.

OPTIONS
-------

       -h --help               show the help

       -v --verbose            be verbose (can be repeated)

       -n --dryrun             tell what would have been done,
                               but doesn't actually do anything

RULES FILE SYNTAX
-----------------

A rules file describes the owner, group, and modes of file and directories. It is composed of multiple line, each describing a rule.  A rule begins by a filename or fnmatch()-compatible pattern, and is followed by zero or more rule specs. A rule spec is of the form <type>:<arg>. The different types are :

- User specifier (u). Takes a valid system user name as argument. Tells who will be the owner of the file or directory.

- Group specifier (g). Takes a valid system group name as argument. Tells who will be the group of the file or directory.

- File mode specifier (f). Takes a valid mode as argument (ex: 644). Tells which modes should be applied to matching files.

- Directory mode specifier (d). Takes a valid mode as argument (ex: 755). Tells which modes should be applied to matching directories.

To simplify the syntax, you can begin a line with one or more TAB characters (\t).  The line will be considered as a subdir of the last described directory.  A line must not have more than 1 more TAB than the previous one.

EXAMPLES
--------

The following line tells that everyting under the chosen directory tree will have 'root' as owned, 'root' as group, that files will be set at mode 644 and directories at mode 755 :

    * f:644 d:755 u:root g:root

The following line tells that all files under the 'bin' subdirectory and with the '.sh' extension will have their mode set to 755.  (All other files will inherit from the less-specific matching rules, if any).

    bin/*.sh f:755

The following line tells that the 'images' subdirectory will have mode 755. It does not contain a pattern, so permissions will not be propageted to its content.

    images f:644 d:755

EXIT VALUES
-----------

The program will exit with a non-zero value if it encountered errors.  Else, it will exit with status 0.

AUTHOR
------

Nicolas Limage <nicolas@xephon.org>

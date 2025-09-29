# Linux Primer
Documentation for common Linux tasks that are useful for developers and system admins.

## Conventions
Code blocks beginning with symbols are commands. The symbols have the following meanings:
```
$	Linux shell (BASH etc), standard user
#	Linux shell (BASH etc), priviliged user (sudo or root)
PS	Windows Powershell
\>	Windows Command Prompt

<foo>       Required Parameter
[<BAR>]     Optional Parameter
```

## Chapters

### [Files](./Chapters/01-files.md) - Create, Read, Update, Delete
* Create a new empty file
* Create a new directory
* View the contents of a file
* Move files or directories
* Rename a file or directory
* Copy files and directories
* Copy a single file
* Copy files from one directory to another
* Copy an entire directory from one location to another
* Copy a file while preserving attributes
* Delete files and directories
* Delete an empty directory
* Delete a directory and all of its contents
* Force delete file(s)

### [Access Control](./Chapters/03-access-control.md) - Permissions and Ownership
* File and directory permissions
    * Permission Types
    * File Ownership
* Changing ownership and permissions
    * Change Owner
    * Change Group
    * Change Mode
        * Symbolic permissions
        * Octal permissions
    * Recursive Operations
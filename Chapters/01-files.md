# File Management

## Create, Read, Update, Delete

### Create a new empty file

It is sometimes necessary to create an empty file. This can be done using the `touch` command.

```$ touch /path/to/file```

Using ```touch``` on a file that already exists will not modify the file, but it will update the modified timestamp.

To create a new text file and open it for editing you can type the command for your favourite editor followed by the path to the file. This will open the editor in a state where saving or writing out the file will save to the path you specify.

```$ vim /path/to/file```

```$ nano /path/to/file```

### Create a new directory

The `mkdir` command (**M**a**K**e **DIR**ectory) can be used to create new directories.

```$ mkdir [<OPTIONS>] /path/to/directory```

When creating a new directory its parent directory must already exist. For example, if you try to create `./new_dir/also_new_dir/` and `./new_dir` does not exist then an error will be returned.

```mkdir: cannot create directory ‘./new_dir/also_new_dir/’: No such file or directory```

To create a new directory, and create any parent directories that do not exist, use the `-p` option.

```$ mkdir -p ./new_dir/also_new_dir/```

If `./new_dir/` does not exist then it will be created.

### View the contents of a file

There are many ways to view the contents of text files from the command line. Two of the most commonly used commands are `cat` and `less`

For smaller files (no more than a few lines), use the `cat` command.

```$ cat /path/to/file```

For larger files, the `less` command is more useful, as it allows for scrolling using the cursor keys, as well as `Home`, `End`, `PgUp`, and `PgDn`.

```$ less /path/to/file```

To quit, press `q`.

### Move files or directories

The `mv` command (**M**o**V**e) moves files or directories from one path to another.

```$ mv [<OPTIONS>] /path/to/source /path/to/destination```


### Rename a file or directory

There is no dedicated command for renaming files in Linux. Instead the file is moved from one file name to another.

`$ mv [<OPTIONS>] oldname newname`

#### Rename a file without overwriting any existing files

`$ mv -n image001.png logo.png`

### Copy files and directories

The `cp` command (**C**o**P**y) can be used to copy files or direcories from one path to another.

`$ cp [<options>] /path/to/source [/path/to/more/sources] /path/to/destination`

### Copy a single file

`$ cp /path/to/source /path/to/destination`

### Copy files from one directory to another

`$ cp /path/to/file1 /path/to/file2 /path/to/destination`

### Copy an entire directory from one location to another

`$ cp -r /path/to/source/directory /path/to/destination/directory`

### Copy a file while preserving attributes

By default, when copying a file certain attributes may be modified. For example, if copying using the sudo command the ownership of the copied file will be changed to the root user. The modification and access timestamps are also changed when copying a file.

 It is sometimes desirable to preserve file attributes such as ownership or mode. This can be done with the `--preserve` option.

`$ cp --preserve=[options] /path/to/source /path/to/destination`

The following attributes are preserved by default if no option is passed.

| Attribute | Description |
|--|--|
| mode | Access permissions |
| ownership | The user and group that own the file |
| timestamps | Modification and access timestamps |

#### Example usage

`$ cp --preserve=ownership /var/www/old-site/index.html /var/www/new-site/index.html`

Copies index.html from `/var/www/old-site/` to `/var/www/new-site/`, preserving the existing ownership.

**WARNING**

The `mv` and `cp` commands will overwrite any file that already exists at the destination path. This is known as "clobbering". To avoid this, use the `-n` option. Alternatively, you can use the `-i` option to decide how to handle each file conflict individually. If in doubt, use `-i`.

### Delete files and directories

The `rm` command (**R**e**M**ove) can be used to delete files.

`$ rm [<OPTIONS>] /path/to/file1 [/path/to/file1 /path/to/file1...]`

### Delete an empty directory

The `rmdir` command (**R**e**M**ove **DIR**ectory)

`$ rmdir [<OPTIONS>] /path/to/dir1 [/path/to/dir2 /path/to/dir3...]`

### Delete a directory and all of its contents

To delete a directory and all of its contents you can use `rm` with the `-r` option. 

`$ rm -r [<OPTIONS>] /path/to/file1 [/path/to/dir2 /path/to/dir3...]`

### Force delete file(s)

The `-f` option can be used to ignore any errors and suppress any confirmations. If `$ rm -rf /path/to/directory` is used then all files and folders in that directory that you have permissions to modify will be deleted without asking for confirmation. Use with caution - doubly so when using the `sudo` command.

#### Example usage

`$ rm -r /var/www/old-site/`

Removes the directory `/var/www/old-site/` and all its contents, including all files and subdirectories located within.

`$ rm -rf /var/www/old-site/`

Removes the directory `/var/www/old-site/` and all its contents, including all files and subdirectories located within without asking for any sort of confirmation.

**WARNING**

The `rm` command will remove any file without warning. To avoid this, use the `-i` option to decide how to confirm each deletion.

When using `-r` you must be especially careful, as this is a recursive action that not only removes the path, but **all** files and directories within that path.

When deleting large numbers of files it can be useful to create a directory called `./files_to_delete` and `mv` the files there before using `rm -r` to delete the directory.
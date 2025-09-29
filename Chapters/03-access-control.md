# Access Control
Files and directories in Linux have permissions metadata that controls which users and groups can interact with them.

## File and directory permissions

### Permission Types

Linux has three file permissions; read write and execute.

#### Read (r)

The read permission (denoted as ```r```) allows a user to view and read the contents of a file. It also allows limited access to list the contents of a directory.

#### Write (w)

The write permission (denoted as ```w```) grants the ability to modify the contents of a file or add, remove, and rename files within a directory.

#### Execute (x)

The execute permission (denoted as ```x```), for files, allows a user to run the file as a program or script. It also allows a user to access a directory and its contents.

### File ownership

Files and directories are owned by a user and a group. Different permissions apply depending on the user that is accessing the file.

Below is a directory listing, produced using the command `$ ls -la`. It shows all of the files in a directory, as well as their permissions and owners.

```
$ ls -la
drwxr-x---  14 myuser myuser 4.0K Mar  8  2022 .
drwxr-xr-x  19 root   root   4.0K Mar  7  2022 ..
drwxrwx---  4  myuser myuser 4.0K Dec  8 08:01 .config
drwx------  2  myuser myuser 4.0K Dec  3 09:31 .ssh
-rw-r-----  1  myuser mygroup 91K Nov 25 14:05 picture.jpg
-rw-rw----  1  myuser myuser 102M Oct 22 09:42 video.mkv
```
Permissions are reported by the ls command as a 10 character string. In the above example, the permissions for the file **picture.jpg** are ```-rw-rw-r--```.

|Type   | Owner permissions (u) | Group permissions (g) | Others permissions (o)|
|-------|-------------------|-------------------|--------------------|
|```-```| ```rw-```         | ```r--```         | ```---```          |

#### File type
The type character signifies the type of file that this is. Regular files are designated with a ```-```, directories are designated with a ```d```.

#### Owner permissions (u)
These three characters indicate the permissions that the user that owns the file has.

#### Group permissions (g)
These three characters indicate the permissions that the group that owns the file has. These permissions apply to all users that are members of the group that owns the file.

#### Others permissions (o)
These three characters indicate the permissions that users and groups who are not the file owner and not a member of the group that owns the file.

## Changing ownership and permissions

It is often neccesary to change the owner or permissions of a file or directory.

Standard users cannot change the owner of a file, but they can change the group of any file that they own to any group that they are a member of. 

### Change Owner
The ```chown``` command (**CH**ange **OWN**er) chages the user, and optionally the group, that owns a file.

```# chown [<OPTIONS>] <username>[:<group>] /path/to/file```

#### Change owner of single file
```# chown devuser ~/Downloads/Picture.gif```

Changes the owner of ```~/Downloads/Picture.gif``` to the user "devuser".

#### Change owner and group of single file
```# chown devuser:developers /mnt/share/Picture.gif```

Changes the owner of ```/mnt/share/Picture.gif``` to the user "devuser" and the group "developers".

### Change group
The ```chgrp``` command (**CH**ange **GR**ou**P**) changes the group that owns a file.

```# chgrp [<OPTIONS>] <group> /path/to/file```

#### Change the group of single file
```$ chgrp developers /mnt/share/accounts.csv```

Changes the group of ```/mnt/share/accounts.csv``` to the group "developers".

### Change Mode
The ```chmod``` command (**CH**ange **MOD**e) changes access permissions of files and directories. It allows users to specify who can read, write, or execute a file. Users may change the mode of any file that they own.

The syntax of ```chmod``` is as follows:
```chmod [<options>] <mode> /path/to/file```

The mode component can be specified in two ways - symbolic mode or octal mode.

#### Symbolic permissions
Symbolic notation in uses letters to represent permissions and who they apply to. Permissions can be set, added and removed for each permission category using the letters defined above (```u```, ```g```, and ```o```), as well as for all with ```a```.

Actions are specified with ```+``` to add, ```-``` to remove, or ```=``` to set permissions explicitly.

#### Octal permissions
Octal notation uses a three digit number to specify the permissions for a file or directory. The first digit specifies owner permissions (u), the second specifies group permissions (g), and the third specifies the others permission (o).

Each digit is can be set from 0 to 7, and their meaning is calculated by adding the values of read (4), write (2), and execute (1) permissions.

#### Examples

```$ chmod u=rwx,g=rx,o= /mnt/share/my_script.py```

Sets ```/mnt/share/my_script.py``` to be readable, writeable and executable by the owner, readable and executable by the group and not accessible by other users.

```$ chmod u+wx,g+x,o-x /mnt/share/your_script.py```

Modifies ```/mnt/share/your_script.py``` to add write and execute permissions for the owner, execute permissions for the group and remove execute from others.

```$ chmod a=rwx /mnt/share/data.csv```

Sets ```/mnt/share/data.csv``` to be readable, writeable, and executable by all users.


```$ chmod 740 /mnt/share/init_script.sh```

Sets ```/mnt/share/init_script.sh``` to be readable, writeable and executable by the owner, readable by the group and not accessible by other users.

```$ chmod 664 /mnt/share/picture.gif```

Sets ```/mnt/share/picture.gif``` to be readable and writeable by the owner and group and readable by other users.


### Recursive Operations
```chown```, ```chgrp```, and ```chmod``` can all be used with ```-R``` to change the ownership properties of all files in a directory.

Care must be taken when using recursion, as all files and directories inside the directory being modified will be affected. This is particularly problematic for ```chmod```, as if the execute permission is removed from a directory it is no longer accessible.

#### Change owner and group of a directory and all files within
```# chown -R devuser:developers /mnt/share/pictures/```

Changes the owner of the directory```/mnt/share/pictures/``` and all files within it to the user "devuser" and the group "developers". Notice that this action requires root/sudo

#### Change group of a directory and all files within
```$ chgrp -R developers /mnt/share/documentation/```

Changes the group of the directory```/mnt/share/documentation/``` and all files within it to the group "developers". Note that if you do not own this file or you are not in this file's ownership group then this action will require root/sudo.

#### Change the permissions of all files in a directory without modifying the directory permissions

```$ find /mnt/share/documentation -type f -exec chmod 664 {} \;```

This changes the permissions of all files inside ```/mnt/share/documentation/``` to be readable and writeable by the owner and group, but read only for everyone else. It achieves this by using the ```find``` command with the ```type``` specified as ```-f``` for files. The ```-exec``` option specifies that for each result that is found a command should be run. ```find``` replaces the ```{}``` placeholder with the path to each result. ```\;``` denotes the end of the command to be run.
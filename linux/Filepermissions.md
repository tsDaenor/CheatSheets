ls -Z

| `rwx rwx rwx` | 111 111 111 |
| `rw- rw- rw-` | 110 110 110 |
| `rwx --- ---` | 111 000 000 |

and so on...

| `rwx` |111 in binary|7|
| `rw-` |110 in binary|6|
| `r-x` |101 in binary|5|
| `r--` |100 in binary|4|

Now, if you represent each of the three sets of permissions (owner, group, and other) as a single digit, you have a pretty convenient way of expressing the possible permissions settings. For example, if we wanted to set some_file to have read and write permission for the owner, but wanted to keep the file private from others, we would:
```
[me@linuxbox me]$ chmod 600 some_file
```
Here is a table of numbers that covers all the common settings. The ones beginning with "7" are used with programs (since they enable execution) and the rest are for other kinds of files.

|Value||	Meaning|
|-------------|-------------|-------------|
|777| (rwxrwxrwx)| No restrictions on permissions. Anybody may do anything. Generally not a desirable setting.|
|755 |(rwxr-xr-x)| The file's owner may read, write, and execute the file. All others may read and execute the file. This setting is common for programs that are used by all users.|
|700| (rwx------) |The file's owner may read, write, and execute the file. Nobody else has any rights. This setting is useful for programs that only the owner may use and must be kept private from others.|
|666| (rw-rw-rw-)| All users may read and write the file.|
|644|(rw-r--r--)| The owner may read and write a file, while all others may only read the file. A common setting for data files that everybody may read, but only the owner may change.|
|600| (rw-------) |The owner may read and write a file. All others have no rights. A common setting for data files that the owner wants to keep private.|

Directory permissions

The chmod command can also be used to control the access permissions for directories. In most ways, the permissions scheme for directories works the same way as they do with files. However, the execution permission is used in a different way. It provides control for access to file listing and other things. Here are some useful settings for directories:

|Value||	Meaning|
|-------------|-------------|-------------|
|777| (rwxrwxrwx)| No restrictions on permissions. Anybody may list files, create new files in the directory and delete files in the directory. Generally not a good setting.|
|755 |(rwxr-xr-x) |The directory owner has full access. All others may list the directory, but cannot create files nor delete them. This setting is common for directories that you wish to share with other users.|
|700 |(rwx------)| The directory owner has full access. Nobody else has any rights. This setting is useful for directories that only the owner may use and must be kept private from others.|


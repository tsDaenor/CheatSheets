#Users and groups
##user

command | use
---|---
`adduser` | Command used to add user accounts.
`chage` | Used to change the time the user's password will expire.
`chfn` | Change a user's finger information
`chsh` | Change a user's shell.
`chown` | Change the owner of file(s ) to another user.
`id` | Print group or user ID numbers for the specified user.
`newgrp` | Allows a user to log in to a new group.
`newusers` | Update and create new users in batch form.
`nologin` | Prevent non-root users from logging onto the system.
`passwd` | Used to update a user's password. The command "passwd username" will set the password for the given user.
`pwconv` | Used to create the file /etc/shadow from the file /etc/passwd to convert to shadow passwords.
`pwunconv` | Uses the files /etc/passwd and /etc/shadow to create /etc/passwd, then deletes /etc/shadow to convert from shadow passwords.
`su` | run a shell with substitute user and group IDs
`useradd` | Create a new user or update default new user information
`userdel` | Delete a user account and their files from the system. The command "userdel -r newuser" will remove the user and deletes their home directory.
`usermod` | Modify a user account.

##groups

command | use
---|---
`chgrp` | Changes the group ownership of files.
`gpasswd` | Used to administer the /etc/group file.
`groupadd` | Create a new group.
`grpconv` | Creates /etc/gshadow from the file /etc/group which converts to shadow passwords.
`grpunconv` | Uses the files /etc/passwd and /etc/shadow to create /etc/passwd, then deletes /etc/shadow which converts from shadow passwords.
`groupdel` | Delete a group
`groupmod` | Modify a group
`groups` | print the groups a user is in
`grpck` | Verify the integrity of group files.

##Other useful commands/examples:

command | use
---|---
`find / -user username -ls`	|	Gives a list of all files owned by username.
`chown -R myuser /home/myuser`	|	Changes ownership of all files in mysuer home directory to myuser.
`chmod +s filename`	|	Sets the uid

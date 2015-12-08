adduser(8) - Command used to add user accounts.
chage (1) - Used to change the time the user's password will expire.
chfn(1) - Change a user's finger information
chsh(1) - Change a user's shell.
chgrp (1) - Changes the group ownership of files.
chown (1) - Change the owner of file(s ) to another user.
gpasswd (1) - Used to administer the /etc/group file.
groupadd (8) - Create a new group.
grpconv (8) - Creates /etc/gshadow from the file /etc/group which converts to shadow passwords.
grpunconv (8)- Uses the files /etc/passwd and /etc/shadow to create /etc/passwd, then deletes /etc/shadow which converts from shadow passwords.
groupdel (8) - Delete a group
groupmod (8) - Modify a group
groups (1) - print the groups a user is in
grpck (8) - Verify the integrity of group files.
id(1) - Print group or user ID numbers for the specified user.
newgrp(1) - Allows a user to log in to a new group.
newusers (8) - Update and create new users in batch form.
nologin (5) - Prevent non-root users from logging onto the system.
passwd (1) - Used to update a user's password. The command "passwd username" will set the password for the given user.
pwconv (8) - Used to create the file /etc/shadow from the file /etc/passwd to convert to shadow passwords.
pwunconv (8) - Uses the files /etc/passwd and /etc/shadow to create /etc/passwd, then deletes /etc/shadow to convert from shadow passwords.
su (1) - run a shell with substitute user and group IDs
useradd (8) - Create a new user or update default new user information
userdel (8) - Delete a user account and their files from the system. The command "userdel -r newuser" will remove the user and deletes their home directory.
usermod (8) - Modify a user account.
Other useful commands/examples:

find / -user username -ls		Gives a list of all files owned by username.
chown -R myuser /home/myuser		Changes ownership of all files in mysuer home directory to myuser.
chmod +s filename		Sets the uid
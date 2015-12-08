Open a terminal in your local system.
Enter ssh-keygen at the command line. 
The command prompts you for a file to save the key in:
$ ssh-keygen 
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/emmap1/.ssh/id_rsa):
Press enter to accept the default key and path, /c/Users/<yourname>/.ssh/id_rsa, or you can create a key with another name.
To create a key with a name other than the default, specify the full path to the key. For example, to create a key called my-new-ssh-key, you would enter a path like this at the prompt:
$ ssh-keygen 
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Documents and Settings/emmap1/.ssh/id_rsa): /c/Users/emmap1/My Documents/keys/my-new-ssh-key
Enter and renter a passphrase when prompted.
Unless you need a key for a process such as script, you should always provide a passphrase. 
The command creates your default identity with its public and private keys. The whole interaction looks similar to the following: 
$ ssh-keygen 
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/emmap1/.ssh/id_rsa):
Created directory '/c/Users/emmap1/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/emmap1/.ssh/id_rsa.
Your public key has been saved in /c/Users/emmap1/.ssh/id_rsa.pub.
The key fingerprint is: e7:94:d1:a3:02:ee:38:6e:a4:5e:26:a3:a9:f4:95:d4 emmap1@EMMA-PC
List the contents of ~/.ssh to view the key files.
You should see something like the following:
$ ls ~/.ssh 
id_rsa id_rsa.pub
The command created two files, one for the public key (for example id_rsa.pub) and one for the private key (for example, id_rsa).

Start GitBash.
Edit your ~/.bashrc file.
If you don't have a .bashrc file you can create the file using your favorite text editor. Keep in mind the file must be in your ~ (home) directory and must be named exactly . bashrc .
Add the following lines to the file:
Chrome and Opera introduce ASCII \xa0 (non-breaking space characters) on paste that can appear in your destination file. If you copy and paste the lines below, copy from another browser to avoid this problem.

1
SSH_ENV=$HOME/.ssh/environment
2
  
3
# start the ssh-agent
4
function start_agent {
5
    echo "Initializing new SSH agent..."
6
    # spawn ssh-agent
7
    /usr/bin/ssh-agent | sed 's/^echo/#echo/' > "${SSH_ENV}"
8
    echo succeeded
9
    chmod 600 "${SSH_ENV}"
10
    . "${SSH_ENV}" > /dev/null
11
    /usr/bin/ssh-add
12
}
13
  
14
if [ -f "${SSH_ENV}" ]; then
15
     . "${SSH_ENV}" > /dev/null
16
     ps -ef | grep ${SSH_AGENT_PID} | grep ssh-agent$ > /dev/null || {
17
        start_agent;
18
    }
19
else
20
    start_agent;
21
fi
Save and close the file.
Close GitBash, then reopen GitBash.
The system prompts you for your passphrase:

1
Welcome to Git (version 1.7.8-preview20111206)
2
Run 'git help git' to display the help index.
3
Run 'git help <command>' to display help for specific commands.
4
Enter passphrase for /c/Documents and Settings/manthony/.ssh/id_rsa:
Enter your passphrase.
After accepting your passphrase, the system displays the command shell prompt. 
Verify that the script identity added your identity successfully by querying the SSH agent:
$ ssh-add -l
2048 0f:37:21:af:1b:31:d5:cd:65:58:b2:68:4a:ba:a2:46 /Users/manthony/.ssh/id_rsa (RSA)
After you install your public key to Bitbucket, having this script should prevent you from having to enter a password each time you push or pull a repository from Bitbucket.
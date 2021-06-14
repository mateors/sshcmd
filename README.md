
## SSH - Secure Shell
## What is SSH ?
> The Secure Shell Protocol is a cryptographic network protocol for operating network services securely over an unsecured network.

> SSH, also known as Secure Shell or Secure Socket Shell, is a network protocol that gives users, particularly system administrators, a secure way to access a computer over an unsecured network.

## Who created SSH?
Tatu Ylönen, in 1995 from Finland.

> SSH is a network protocol that gives users, particularly system administrators, a secure way to access a computer over an unsecured network.

> SSH implementation comes with scp utility for remote file transfer that utilises SSH protocol. SSH for file transfer is also utilised by other applications such as sftp and rsync which can make use of SSH to secure its network transaction.


## What is ssh key?
> Essentially, SSH keys are an authentication method used to gain access to an encrypted connection between systems and then ultimately use that connection to manage the remote system

## Check ssh version
> `ssh -V`

![version output](./ssh_version.png)

## SSH Key Generation
> `ssh-keygen -t rsa -b 4096 -C "mateors github account"`

> `ssh-keygen -t rsa -b 4096 -C "your@email.com"` you may use either email or comment

![ssh_key_generate](./ssh_keygen.png)

## What is eval?
> eval is a built-in Linux command which is used to execute arguments as a shell command.

## Start your ssh-agent
> `eval $(ssh-agent -s)`

![ssh_agent_start](./ssh_agent_start.png)

## Check SSH Identity
> `ssh-add -l`

![ssh_identity_check](./ssh_identity_check.png)

## Check public key
> `ls ~/.ssh`
> `cat ~/.ssh/id_rsa.pub`

## Copy the public key
> `clip < ~/.ssh/id_rsa.pub`

![public_key_copy_into_clipboard](./public_key_copy_into_clipboard.png)

## Paste the clipboard into github following address
> location-> https://github.com/settings/ssh/new

![ssh_gpg_key](./ssh_gpg_key.png)

![paste_public_key_into_github](./paste_public_key_into_github.png)

![settings_keys](./settings_keys.png)

## To Verify Authentication
> `ssh -T git@github.com`

![verify_connection](./verify_connection.png)

# To change the passpharse
> `ssh-keygen -p`

# Delete single named private key from ssh-agent
> `ssh-add -d ~/.ssh/id_rsa`

# Remove ALL private keys from the ssh-agent
> `ssh-add -D`

# SSH Linux pipeline

> Get content of a file from home directory login to remote server create a file and paste its content there\
> `cat ~/file.txt | ssh user@serverip "touch ~/file.txt && cat >> ~/file.txt"`

> Above technique used to copy public key from local to remote machine\
> `cat ~/.ssh/id_rsa.pub | ssh user@serverip "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"`

# SSH Server
The SSH server configuration file is located here: /etc/ssh/sshd_config. An SSH configuration
can be validated by running the command:
> `/usr/ubin/sshd -t`

> Anytime a change is made to the server’s SSH config file, the SSH service must be restarted.

## View the SSH server status
`systemctl status ssh`

## Restart the SSH server
`systemctl restart ssh`

## Stop the SSH server
`systemctl stop ssh`

## Start the SSH server
> `systemctl start ssh`

## Protecting the SSH Server
>You might also consider add-on solutions to block IP addresses that repeatedly connect but fail to authenticate, such as fail2ban and blacklistd


>To some extent, sshd(8) protects itself via privilege separation. Only a small section of the service runs with root privileges. Most of the server runs as an
unprivileged user. This means that if an intruder successfully breaks into the server daemon, he can only do a limited amount of damage to your system. It’s
still really annoying, but not devastating.

> a simple way to reduce risk to your SSH service is to reduce the number of IP addresses that can access it\
> `/etc/hosts.allow`

>The most effective way to protect your server, however, is to disable passwords and only allow logins via keys. 

Reference:
* [Windows Installation](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse)

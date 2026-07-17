**SSH (Secure Shell)** is a **secure network protocol** that allows you to **connect to and manage a remote computer or server over a network** using an encrypted connection.

Think of it like this:

- **Without SSH:** Sending commands is like sending a postcard—anyone who intercepts it can read it.
- **With SSH:** Sending commands is like sending a sealed, locked letter—only the intended recipient can read it.

Also, SSH clients connect to the SSH server on **Transmission Control Protocol (TCP) port 22** unless the server is configured to use a different port.

SSH is a cryptographic network protocol that provides secure communication between:

1. **SSH Client** → The machine you use to connect
2. **SSH Server (sshd)** → The remote machine you want to access

Install SSH.
```
sudo apt install openssh-server
```

Check.
```
systemctl status ssh
```

Enable.
```
sudo systemctl enable ssh
```

Restart.
```
sudo systemctl restart ssh
```

Verify.
```
ss -tlnp
```

To access remote server.
```
ssh <user-name>@<user-internetprotocol>
```

To connect using domain name.
```
ssh user@domain-name
```

Specifies a custom SSH port.
```
ssh -p PORT username@host
```

Specifies the private key file used for authentication.
```
ssh -i /path/to/private_key username@host
```
Note: `-i` can be define identity files.

Displays basic debugging information.
```
ssh -v user@host
```

More.
```
ssh -vv user@host
```

Highest level.
```
ssh -vvv user@host
```

Important Note: 
It can be useful for,
- Troubleshooting connection problems.
- Viewing authentication attempts.
- Checking which configuration files are used.

Show the effective client configuration.
```
ssh -G user@host
```

Show the effective server configuration.
```
sudo sshd -T
```

To access the SSH configuration directory.
```
cd /etc/ssh/
```
That's the moment we can list these directories we can found.
`/etc/ssh/`
├── `ssh_config` can be stored SSH client configuration.
├── `ssh_config.d/`  can be stored Additional client configuration.
├── `sshd_config`  can be stored SSH server configuration.
├── `sshd_config.d/`  can be stored additional server configuration.
├── `ssh_host_rsa_key` can be stored RSA private host key.
├── `ssh_host_rsa_key.pub` can be stored RSA public host key.
├── `ssh_host_ed25519_key` can be stored Ed25519 private host key.
├── `ssh_host_ed25519_key.pub` can be stored Ed25519 public host key.
├── `ssh_host_ecdsa_key` can be stored ECDSA private host key.
└── `ssh_host_ecdsa_key.pub` can be stored ECDSA public host key.

To check whether port 22 is listening.
```
sudo ss -tln | grep :22
```

Creates a public/private key pair for passwordless authentication.
```
ssh-keygen -t ed25519
```

Copies your public key to a remote server so you can log in without a password.
```
ssh-copy-id user@192.168.1.100
```

Securely copies files between computers over SSH.
```
scp report.pdf user@server:/home/user/
```

Download a file.
```
scp user@server:/home/user/report.pdf .
```

Transfers files interactively using SSH encryption.
```
sftp user@192.168.1.100
```

Useful commands inside the SFTP prompt.
```
put file.txt
```

```
get file.txt
```

```
ls
```

```pwd
cd
```

```
exit
```

Keeps your private keys in memory so you don't have to enter the passphrase every time.
```
eval "$(ssh-agent -s)"
```

Loads your private key into the running SSH agent.
```
ssh-add ~/.ssh/id_ed25519
```

Now, We can move forward [[About Configuration File]] for the better understand purpose.

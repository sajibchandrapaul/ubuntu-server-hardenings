A **configuration file** is a text file that stores settings for a program.

Instead of typing the same options every time you run a program, the program reads its configuration file automatically.

The client reads.
```
/etc/ssh/ssh_config
```
This file controls:
- How your computer connects to servers
- Default username
- Default port
- Identity file (Private keys)
- Preferred authentication method
- Connection timeout
- Compression
- ProxyJump

The server reads.
```
/etc/ssh/sshd_config
```
This file controls:
- Who may log in
- Which port SSH listens on
- Password authentication
- Public key authentication
- Root login
- Maximum login attempts
- Session timeout
- Security restrictions

To check list SSH configuration files.
```
ls -l /etc/ssh
```

View the client configuration.
```
cat /etc/ssh/ssh_config
```

View the server configuration.
```
sudo cat /etc/ssh/sshd_config
```

Test SSH server configuration syntax.
```
sudo sshd -t
```

Check the SSH version.
```
ssh -V
```

Check the server daemon version.
```
sshd -V
```

Reload configuration without disconnecting users.
```
sudo systemctl reload ssh
```

Now, We can move forward [[Understanding sshd_config Directives]] for the better understand purpose.
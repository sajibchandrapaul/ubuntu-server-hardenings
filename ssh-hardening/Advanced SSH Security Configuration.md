In these lesson is where SSH configuration becomes closer to **enterprise system administration**.

### For Match Blocks, 
A `Match` block allows you to apply different SSH rules to different users, groups, hosts, or networks.

Normally:
```
PermitRootLogin no
PasswordAuthentication no
```
applied everyone.
But, Sometimes you need different behavior for the secure system purpose.

Example:
- Administrators → Full SSH access
- Developers → Limited access
- Backup users → Only file transfer
- Vendors → Restricted environment

In these format it can be work.

Example:
```
Match User sajibchandrapaul
    PasswordAuthentication yes
```

It's means the user `sajibchandrapaul` can be gets password authentication enabled. Other users follow the global configuration.

Global settings come first.

Example.
```
PasswordAuthentication no

Match User sajibchandrapaul
    PasswordAuthentication yes
```
In these command means:
- **Globally:** Password authentication is disabled.
- **For user `sajibchandrapaul`:** Password authentication is enabled.

### For User-Specific SSH Policies,
In these policies purpose you can create rules for individual users.

Example:
```
Match User developer
    X11Forwarding no
    AllowTcpForwarding no
```
It means for user `developer` we can disable,
- GUI forwarding
- SSH tunneling

### For Group-Specific SSH Policies,
Managing individual users becomes difficult in large organizations.

Instead, use groups.

Example.
```
Match Group developers
    X11Forwarding no
    AllowTcpForwarding no
```
It means anyone inside `developers` group gets these restrictions.

### For `ForceCommand`,
`ForceCommand` forces a user to execute only a specific command.

The user cannot run normal shell commands.

Example.
```
Match User backup
    ForceCommand internal-sftp
```
When the `backup` user can be access the system they can't run shell command.

Like.
```
$ bash
$ ls
$ sudo
```
Instead, they only get, SFTP session for the system.

### For `ChrootDirectory`,
The `Chroot` means **Change Root Directory**. It creates a restricted environment for a user.

User thinks their directory is:
```
/
```
but actually it is a small isolated directory.

`Chroot` user sees:
```
/
├── uploads
└── downloads
```
They cannot see the real files system.

Configuration.
```
Match User ftpuser
    ChrootDirectory /srv/ftp
    ForceCommand internal-sftp
```
It's can be used for:
- SFTP servers
- Customer file access
- Vendor access
- Secure file exchange

Important Note: The `chroot` directory must be owned by root.

### For `PermitTTY`,
Teletypewriter (TTY) means a terminal session.

In Linux/Unix systems, a **TTY is a terminal interface that allows a user to interact with the system by entering commands and receiving output.**

For the allow the system.
```
PermitTTY yes
```

Disable:
```
PermitTTY no
```

### For `AllowTcpForwarding`,
SSH can create encrypted tunnels.

For Allow:
```
AllowTcpForwarding yes
```

Disable:
```
AllowTcpForwarding no
```

### For `GatewayPorts`,
Controls whether remote forwarded ports can listen publicly.

Allow.
```
GatewayPorts yes
```
It's means allows public forwarding.

Don't agree.
```
GatewayPorts no
```
It can be recommended.

Clientspecified.
```
GatewayPorts clientspecified
```
It's means client decide.

A production based server might use for the better secure thoughts:
```
Port 2222

PermitRootLogin no

PasswordAuthentication no

PubkeyAuthentication yes


AllowGroups ssh-admins developers


Match Group developers
    AllowTcpForwarding no
    X11Forwarding no


Match User backup
    ForceCommand internal-sftp
    ChrootDirectory /backup
    PermitTTY no
```

Now, We can move forward [[SSH Logging, Monitoring & Troubleshooting]] for the better understand purpose.
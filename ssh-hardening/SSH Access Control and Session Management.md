In these section we will learn how enterprise systems control.

For `AuthorizedKeysFile`,

`AuthorizedKeysFile` defines **where SSH looks for a user's public keys**.

Syntax.
```
AuthorizedKeysFile .ssh/authorized_keys
```

Default location:
```
/home/username/.ssh/authorized_keys
```
Note: `username` can be notice based on the your system.

SSH checks:
```
/home/sajibchandrapaul/.ssh/authorized_keys
```
In these section I can use `sajibchandrapaul` it's mine system username.

For check.
```
cat /home/sajibchandrapaul/.ssh/authorized_keys
```

Output Like.
```
ssh-ed25519 AAAAC3Nz... sajibchandrapaul@laptop
```

Your laptop has:
```
~/.ssh/id_ed25519
```
- Private key stays on your laptop.
- Public key goes to the server.

Custom Location Example.
```
AuthorizedKeysFile /etc/ssh/keys/%u
```
It's means store each user's SSH public key in `/etc/ssh/keys/` directory, and replace `%u` with the username.

For `AllowUsers`,

`AllowUsers` specifies **which users are allowed to SSH into the server**

Syntax:
```
AllowUsers username
```
Based on requirement you can use `username` for the secure system.

Multiple users.
```
AllowUsers sajib alice bob
```

With IP restrictions.
```
AllowUsers admin@192.168.1.50
```

For multiple.
```
AllowUsers admin@10.10.1.0/24 deploy@203.0.113.10
```
In these last two command can be use `admin` and `deploy` based on username.

For `AllowGroups`,

Instead of managing individual users, companies usually manage groups.

Syntax:
```
AllowGroups <groupname>
```

Like.
```
AllowGroups sshduser
```

For `DenyUsers`,

Explicitly block specific users.

Syntax:
```
DenyUsers <username>
```

Multiple.
```
DenyUsers <username1> <username2>
```

Like.
```
DenyUsers guest
```

For `DenyGroups`,

Blocks an entire group.

Syntax.
```
DenyGroups contractors
```
 In these here `contractors` is group name.

For `MaxAuthTries`,

Controls how many authentication attempts are allowed.

Default:
```
MaxAuthTries 6
```

`MaxAuthTries` defines the maximum number of authentication attempts allowed per SSH connection. The default value is often higher (such as 6), but reducing it to `3` is a common security hardening practice because it limits repeated password/key guessing attempts.

Why?

To reduce:

- Brute-force attacks
- Password guessing
- Automated attacks

For `LoginGraceTime`,

Controls how long a user has to authenticate.

Example:
```
LoginGraceTime 60
```
In these means can be suer has `60 seconds` to successfully login. After timeout it can be goes to `Connection closed` for the better security can use `30 seconds` best practice.

For `ClientAliveInterval`,

Server checks if the client is still alive.

Example:
```
ClientAliveInterval 300
```
It's means can be every `300 seconds` server sends a check.

Useful for:

- Broken connections
- Dead sessions
- Network failures

For `ClientAliveCountMax`,

Works with:
```
ClientAliveCountMax 2
```
`ClientAliveCountMax` defines **how many unanswered client alive messages** the SSH server will tolerate before disconnecting the SSH session.

For `X11Forwarding`,

X11 allows Linux graphical applications to display on another computer.

Example:
```
X11Forwarding yes
```
means SSH allows **X11 forwarding**, which lets you run a graphical Linux application on a remote server and display its GUI on your local machine.

For `PermitEmptyPasswords`,

Controls whether users with empty passwords can login.

Example:
```
PermitEmptyPasswords yes
```
It's means system allowed empty passwords.

Production Hardened Example.
```
Port 2222

PermitRootLogin no

PasswordAuthentication no

PubkeyAuthentication yes

AuthorizedKeysFile .ssh/authorized_keys

AllowGroups sshusers

MaxAuthTries 3

LoginGraceTime 30

ClientAliveInterval 300

ClientAliveCountMax 2

X11Forwarding no

PermitEmptyPasswords no
```

Now, We can move forward [[Advanced SSH Security Configuration]] for the better understand purpose.

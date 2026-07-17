What is a Directive?

A **directive** is a configuration instruction.
Think of it as a **rule** that tells the SSH server what to do.

`Port` → can be define about directives!

Open the server configuration file.
```
sudo nano /etc/ssh/sshd_config
```

Outcome.
```
#Port 22
#ListenAddress 0.0.0.0
#PermitRootLogin prohibit-password
#PasswordAuthentication yes
#PubkeyAuthentication yes
```
In these section `#` can be called comments.

For the `#Port 22`,

It tells the SSH server **which TCP port to listen on** for incoming SSH connections.

Why Change the Port?

Changing the port does **not** make SSH inherently secure.

However, it can:
- Reduce automated scans on port 22
- Reduce noise from bots
- Reduce failed login attempts

It should **not** replace proper security measures like SSH keys and disabling root login.
```
port <your-sutiable-port>
```

Now clients must specify the port:
```
ssh -p <your-sutiable-port> user@server
```

The set of instruction port list:
🧪 Lab / Learning
```
2222
2200
2022
```

🖥️ VPS / Production Server
```
2222
22022
22222
10022
```

🏢 Enterprise Environment
```
10022
22022
20222
22222
```

For the `ListenAddress`,

It tells SSH **which IP address(es) to listen on**.

Think of your server as a building with multiple doors (network interfaces). `ListenAddress` decides which doors SSH will answer.

If you set custom `ListenAddress`  and at the same time SSH ignores requests to any other IP address.

Syntax:
```
ListenAddress 0.0.0.0
```

If you did custom.
```
ListenAddress <your-internetprotocol>
```

Like.
```
ListenAddress 192.168.1.100
```

For `PermitRootLogin`,

Syntax.
```
PermitRootLogin yes
```
It's means Root login is allowed.

For the secure your system It more important things.
Also, Root is the **superuser**.

It can:

- Delete files
- Create users
- Stop services
- Change passwords
- Install software

If an attacker gains root access, they effectively control the entire system.

For the better secure system.
```
PermitRootLogin no
```
Root login is completely disabled. Also, It will be recommended for almost all production servers.

But, We have another solution it's called `prohibit-password`,

`prohibit-password` In SSH configuration, **`prohibit-password`** is an authentication setting that controls whether a user can log in using a password.

For `prohibit-password`.
```
PermitRootLogin prohibit-password
```
It can be did:
- Root may log in **only** with an SSH key.
- Password login is blocked.
- This is a common and secure default on many Linux distributions.

For `PasswordAuthentication`,

Syntax.
```
PasswordAuthentication yes
```
It can be controls whether users can authenticate with a **password**.

If you can did.
```
PasswordAuthentication no
```
It's means:
- Password logins are disabled.
- Only methods such as SSH public key authentication are allowed.
- This is the recommended configuration after you've set up SSH keys.

Why Disable Passwords?
Passwords can be:
- Guessed
- Stolen
- Reused
- Brute-forced
SSH keys are much stronger and harder to compromise.

For `PubkeyAuthentication`,

Syntax:
```
PubkeyAuthentication yes
```
It's means controls whether SSH allows **public key authentication**.

You can connect using:
```
ssh -i ~/.ssh/id_ed25519 user@server
```

If you have default keys.
```
ssh user@server
```

If you can did.
```
PubkeyAuthentication no
```
- SSH ignores public keys.
- Only other enabled authentication methods (such as passwords) will work.
- This is rarely recommended in modern environments.

Best practice.

For a production Linux server, a common secure starting point is:
```
Port 2222
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
```

Remember: **Do not disable password authentication until you've confirmed that SSH key login works**, or you could lock yourself out of the server.

Now, We can move forward [[SSH Access Control and Session Management]] for the better understand purpose.

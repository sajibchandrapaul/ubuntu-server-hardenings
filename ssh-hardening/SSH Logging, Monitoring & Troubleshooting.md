Every SSH connection leaves a record. 
SSH logs information such as:
- Successful logins
- Failed logins
- Invalid usernames
- Wrong passwords
- Public key authentication
- Session start and end
- Disconnect reasons
- Configuration errors
Think of SSH logs as the **security camera footage** for your SSH server.


The location depends on your Linux distribution.

Ubuntu / Debian.
```
/var/log/auth.log
```

RHEL / Rocky / AlmaLinux.
```
/var/log/secure
```

Modern Linux systems commonly use **systemd's journal**, which you can access with `journalctl`.
Also, `journalctl` displays logs collected by `systemd`.

Basic command:
```
sudo journalctl
```
Note: This shows all system logs, which can be overwhelming.

View only SSH logs on your system. Since the SSH server runs as the `ssh` service on Ubuntu:
```
sudo journalctl -u ssh
```

View recent SSH logs. Last 20 entries:
```
sudo journalctl -u ssh -n 20
```

Follow logs in real time.
```
sudo journalctl -u ssh -f
```
- Now open another terminal and log in via SSH.
- You'll immediately see new log entries appear.
- This is very useful for troubleshooting.

Count failed attempts.

Ubuntu:
```
sudo grep "Failed password" /var/log/auth.log
```

With the journal:
```
sudo journalctl -u ssh | grep "Failed password"
```

Count.
```
sudo journalctl -u ssh | grep "Failed password" | wc -l
```

Find the most active attacker IPs.
```
sudo journalctl -u ssh | grep "Failed password"
```

### For `Fail2Ban`,
Fail2Ban is a security tool that watches log files. When it detects repeated failed logins, it automatically blocks the attacker's IP using the firewall.

Configuration:
```
maxretry = 5
```
If any attacker try access the server before the system did IP's address block. 

Check Fail2Ban status.
```
sudo fail2ban-client status
```

Check the SSH jail.
```
sudo fail2ban-client status sshd
```


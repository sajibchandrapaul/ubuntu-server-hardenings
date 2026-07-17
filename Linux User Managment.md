User management is the system used to create, track, and secure user accounts. It controls exactly who can access your software, devices, or data. It ensures users only get the permissions they need to do their jobs. 

The demographics are user path. ![[user-management.png]]
For the command purpose, We can use two types of command:
1. `useradd` is the low-level, distro-agnostic binary — precise but does nothing extra unless you tell it to.
2. `adduser` interactive and does the based on need setup automatically.

So that, basically for the manually work purpose `useradd` can be perfect. For the better, time reduced we can did work for `adduser` command based.

For the `useradd` purpose.
```
sudo useradd -m -s /bin/bash -c "Sajib Chandra Paul" sajibchandrapaul
```
Important Note:

- `-m` → create the home directory (`/home/sajibchandrapaul`), copying files from `/etc/skel/`
- `-s /bin/bash` → set the login shell to Bash
- `-c "Sajib Chandra Paul"` → set the comment field (usually full name) in `/etc/passwd`
- `-L` it can be used for the lock user.
- `-U` it can be used for the unlock user.

If you forget `-m`, the user is created but **has no home directory** — logging in as that user will drop them in `/` or fail, depending on config. This is a very common beginner mistake.

To **change a user's home directory** in Linux and optionally **move the existing home directory contents** based your need.
```
sudo usermod -m -d /home/<your-wish> <user-name>
```
Note: `<your-wish>` can be refer which want after change home directories.

Change User Information.
```
sudo usermod -c "New Description" username
```

Disable account after a date.
```
sudo chage -E 2026-12-31 <username>
```

You'd then need to set a password manually.
```
sudo passwd sajibchandrapaul
```

To set password expiration.
```
sudo chage -M 90 username
```
Important Note: In these command can be mentioned password expires after 90 days.
Also somethings are:
- `-m 7` Minimum 7 days before changing password agains.
- `-M 90` Password expires after 90 days.
- `-W 14` Warning 14 days before expiry.

Change your own password.
```
passwd
```

Change another user's password.
```
sudo passwd <username>
```

To view the Linux system configuration file that defines the default settings for user account creation and password policies, use:
```
cat /etc/login.defs
```

View password expiry policy.
```
chage -l <user>
```

For the automatic purpose.
```
sudo adduser sajibchandrapaul
```

After creating a user either way, verify with.
```
getent passwd sajibchandrapaul
```
- Output Format: `username:x:UID:GID:comment:home_dir:shell`

Check if the home directory actually exists.
```
ls -ld /home/sajibchandrapaul
```

To check **basic information about every local user account** on a Linux system.
```
cat /etc/passwd
```
Important note for UID purposes:
- `0` means root
- `1–999` System users/services.
- `1000+` Regular users.

To see groups.
```
cat /etc/group
```

Encrypted password information.
```
sudo cat /etc/shadow
```
Important notes for Algorithm hash code process:
- `$y$` use Yescrypt
- `$6$` use SHA-512
- `$5$` use SHA-256
- `$2b$` use bcrypt
- `$1$` use MD5

To **secure group information file** in Linux.
```
sudo cat /etc/gshadow
```

To create group.
```
sudo groupadd <group-name>
```

To set a password for a group.
```
sudo gpasswd <group-name>
```

To add user to a new group, but default group will remain same.
```
sudo usermod -aG <group-name> <user-name> 
```

To change the default group.
```
sudo usermod -g <group-name> <user-name>
```

To deleted user.
```
sudo userdel <user-name>
```

Will remove home directories.
```
sudo userdel -r <user-name>
```

Forced deleted user even if the user logged in the system.
```
sudo userdel -f <user-name>
```

Show logged-in users and activity.
```
w
```

Show user's groups.
```
groups username
```

Show login history.
```
last
```

User information.
```
finger username
```

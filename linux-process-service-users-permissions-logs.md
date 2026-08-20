# Linux Basics

Hands-on practice with Linux process management, services, users and groups, file permissions, and system logs.

## Processes

### ps

Shows information about running processes.

```bash
ps aux
```

- `a`: shows processes for all users
- `u`: shows detailed user-oriented information
- `x`: includes processes without a terminal

Another common form:

```bash
ps -ef
```

### top

Shows running processes and system resource usage in real time.

```bash
top
```

Useful keys:

- `q`: quit
- `k`: kill a process
- `P`: sort by CPU usage
- `M`: sort by memory usage

### Background Process

```bash
sleep 300 &
```

`sleep 300` waits for 300 seconds.

`&` runs the command in the background.

Useful job-control commands:

```bash
jobs
fg
bg
```

### kill

Terminates or sends a signal to a process.

```bash
kill PID
```

The default signal is `SIGTERM`.

Common alternatives:

```bash
kill -15 PID
kill -9 PID
```

`SIGTERM` asks the process to terminate gracefully.

`SIGKILL` forcefully terminates the process and should normally be used only when necessary.

---

## Services and systemd

### systemctl

Used to manage systemd services.

Check service status:

```bash
systemctl status ssh
```

Start a service:

```bash
sudo systemctl start ssh
```

Stop a service:

```bash
sudo systemctl stop ssh
```

Restart a service:

```bash
sudo systemctl restart ssh
```

Check whether a service is running:

```bash
systemctl is-active ssh
```

Check whether a service starts automatically at boot:

```bash
systemctl is-enabled ssh
```

`systemctl` is the standard way to manage services on modern Ubuntu systems.

---

## Users and Groups

### whoami

Shows the current username.

```bash
whoami
```

### id

Shows UID, GID, and group membership.

```bash
id
id devuser
```

### groups

Shows group membership.

```bash
groups
```

### useradd

Creates a new user.

```bash
sudo useradd -m devuser
```

`-m` creates a home directory.

An alternative on Ubuntu is:

```bash
sudo adduser devuser
```

`adduser` provides a more interactive user creation process.

### groupadd

Creates a new group.

```bash
sudo groupadd devtest
```

### usermod

Adds a user to a supplementary group.

```bash
sudo usermod -aG devtest devuser
```

- `-G`: specifies supplementary groups
- `-a`: appends the group without removing existing group memberships

---

## File Permissions

### ls -l

Shows file permissions, owner, group, size, and modification time.

```bash
ls -l test.txt
```

Example:

```text
-rw-r--r-- 1 shima shima 0 test.txt
```

Permissions are divided into:

```text
-rw- r-- r--
 │   │   │
 │   │   └── Others
 │   └────── Group
 └────────── Owner
```

- `r`: read
- `w`: write
- `x`: execute

### chmod

Changes file permissions.

```bash
chmod 600 test.txt
```

Only the owner can read and write.

```bash
chmod 644 test.txt
```

The owner can read and write, while group and others can only read.

Symbolic permissions can also be used:

```bash
chmod u+x script.sh
chmod g+w file.txt
chmod o-r file.txt
```

- `u`: owner
- `g`: group
- `o`: others

### chown

Changes file ownership.

```bash
sudo chown shima:devtest test.txt
```

This changes the owner to `shima` and the group to `devtest`.

---

## Directory Permissions

Directory permissions are different from file permissions.

For directories:

- `r`: list contents
- `w`: create or delete entries
- `x`: enter or traverse the directory

Check directory permissions:

```bash
ls -ld /home/shima
```

### namei

Useful for troubleshooting permissions along a complete path.

```bash
namei -l /tmp/test.txt
```

It shows the permissions of each directory and file in the path.

---

## ACL

ACL (Access Control List) provides more detailed access control than the standard owner/group/others permission model.

View ACLs:

```bash
getfacl /tmp/test.txt
```

Example:

```text
user::rw-
group::rw-
other::r--
```

ACLs are useful when specific users or groups need permissions beyond the standard model.

---

## File Attributes

### lsattr

Shows filesystem-level attributes.

```bash
lsattr /tmp/test.txt
```

File attributes are different from normal permissions shown by `ls -l`.

For example, the `i` attribute means **immutable**.

Immutable files cannot normally be modified, deleted, or renamed until the attribute is removed.

Attributes are managed with:

```bash
chattr
```

---

## Logs

### journalctl

Used to view logs collected by systemd.

View SSH logs:

```bash
sudo journalctl -u ssh
```

View the last 20 entries:

```bash
sudo journalctl -u ssh -n 20
```

Follow new log entries in real time:

```bash
sudo journalctl -u ssh -f
```

Show errors from the current boot:

```bash
sudo journalctl -p err -b
```

- `-u`: filter by service
- `-n`: show a specific number of recent entries
- `-f`: follow new entries
- `-p err`: show error-level messages
- `-b`: current boot

Traditional log files can also be found under:

```text
/var/log/
```

---

## SSH

SSH (Secure Shell) provides secure remote access to Linux systems.

Example:

```bash
ssh username@server-ip
```

Example:

```bash
ssh shima@192.168.1.10
```

The SSH service can be managed using:

```bash
systemctl status ssh
systemctl restart ssh
```

SSH logs can be investigated using:

```bash
journalctl -u ssh
```

A basic troubleshooting flow is:

```text
SSH problem
    ↓
systemctl status ssh
    ↓
journalctl -u ssh
    ↓
Check the logs
```

---

## Key Takeaways

In this lab I practiced:

- Process management
- Background processes
- Process signals
- systemd services
- Users and groups
- File permissions
- File ownership
- Directory permissions
- ACL
- File attributes
- System logs
- SSH troubleshooting

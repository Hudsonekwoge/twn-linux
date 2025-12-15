
![Structure of usernames in linux](https://raw.githubusercontent.com/Hudsonekwoge/twn-linux/main/assets/output_of_linux_user_account_in_passwd.png)


## Adding a new user ##

**`adduser` vs. `useradd` Command Differences**

| Feature | `adduser` (Recommended for Debian/Ubuntu) | `useradd` (Recommended for Red Hat/CentOS) |
| :--- | :--- | :--- |
| **User Interface** | **Interactive Script** (Higher Level) | **Binary Executable** (Lower Level) |
| **Default Behavior** | Prompts for passwords and user details. | Non-interactive; requires options to set password/home directory. |
| **Configuration** | Reads settings from the `/etc/adduser.conf` file. | Reads default settings from `/etc/default/useradd` and `/etc/login.defs`. |
| **Home Directory**| **Automatically** creates the home directory and copies skeleton files from `/etc/skel`. | **Does NOT** create the home directory or copy skeleton files by default; requires the `-m` option to do so. |
| **System Group** | **Automatically** creates a primary group with the same name as the username (UID=GID). | **Does NOT** automatically create a primary group; the new user is added to a default group (e.g., `users`), unless the `-N` option is specified. |
| **Portability** | Primarily used and behaves consistently on Debian, Ubuntu, and related distributions. | A standard command on most systems, but its defaults vary widely. |

**Which to Choose?**

* **For quick, general use:** Use `adduser` (e.g., `sudo adduser newuser`).
* **For automation and scripting:** Use `useradd` (e.g., `sudo useradd -m -s /bin/bash newuser`).

To add a new user `hudson`:
```
adduser hudson
```
To change the user's password:
```
passwd hudson
```

## Creating a new group 
**`addgroup` vs. `groupadd` Command Differences**

| Feature | `addgroup` (Recommended for Debian/Ubuntu) | `groupadd` (Recommended for Red Hat/CentOS) |
| :--- | :--- | :--- |
| **User Interface** | **Interactive Script** (Higher Level) | **Binary Executable** (Lower Level) |
| **GIDs (Group IDs)** | Checks `/etc/group` and automatically selects the **lowest available GID** above a certain threshold (usually 1000). | **Automatically selects the next available GID** sequentially, based on the last GID used in `/etc/group`. |
| **Default Behavior** | User-friendly, often wraps `groupadd` but applies Debian/Ubuntu specific defaults. | Non-interactive; designed for scripts and precise command-line control. |
| **Configuration** | Reads settings from the `/etc/adduser.conf` file, which includes GID range limits. | Reads default settings from `/etc/default/groupadd` and `/etc/login.defs`. |
| **Error Handling** | Better error reporting and often prompts the user for correction if an issue occurs. | Fails silently or reports low-level error codes, making it less intuitive for manual use. |
| **Portability** | Primarily used and behaves consistently on Debian, Ubuntu, and related distributions. | A standard command on most systems, but its defaults vary widely. |

**Which to Choose?**

* **For quick, general use:** Use `addgroup` (e.g., `sudo addgroup new_devs`).
* **For scripting and automation:** Use `groupadd` (e.g., `sudo groupadd -g 2005 new_devs`).

Create a new group:
```
groupadd devops
```
Change the primary group of the user `hudson` to `devops`:
```
sudo usermod -g devops hudson
```
Since we don't need the `hudson` group, delete it:
```
sudo groupdel hudson
```

We can also add a user to multiple **secondary groups** besides the strictly one **primary group**:
```
sudo usermod -G list_of_comma_separated_groups username
```
The challenge with using only the `-G` option is that it will overwrite the existing list of groups. To avoid that, add the `append` option:
```
sudo usermod -aG admin,ninja hudson
```

Print out the groups a user belongs to:
- Running just `groups` prints out the groups the currently logged in user belongs to
- `groups hudson` prints out the groups of the user hudson

Add a user by specifying the group at the creation time

```
sudo useradd -G devops nicole
```
- `-G` creates the user with one or more secondary groups
- `-d` is used to create a custom home directory
- and other options for shell, etc

Remove Nicole from the devops group
```
sudo gpasswd -d nicole devops
```

To delete a group:
```
sudo groupdel hudson
```

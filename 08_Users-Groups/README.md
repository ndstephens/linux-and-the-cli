# Users and Groups

## Principle of Least Power

- Linux is inherently a multi-user system
- Many of the users of the system aren't even human users
- Many programs will create their own users and groups to keep themselves separate from other users

## USERS

### `whoami`

- Returns the name of the currently active user

### `cat /etc/passwd`

- Displays all the currently registered users on that computer
- Many/most of them are programs that have their own user to keep their permissions separate from yours
- `passwd` is a file that keeps track of all users
- At the end of each line is shown their `home-directory` and `login shell/command`
  - eg. `username:...:/home/username:/bin/bash`
    - their home-directory is `/home/username`
    - they are dropped in to `bash` when they log in
  - some program-created users have "dead-end" login shells
    - eg. `/bin/false` or `/usr/sbin/nologin`
    - these prevent interactive login or other safe guards

### Principle of Least Power

- Each user/program should have the least amount of privilege (power) as possible to complete their tasks
- Helps to lower the number of attack vectors and keep potential damage to a minimum
- Also good to limit your own permissions to prevent accidental mistakes

### `root` - root user ... aka "Superuser"

- The root user is the only one that, by default, has permissions on the root `/` of the computer
- Has no restrictions on what it can do
- When you run `whoami` you should see `root`

### `sudo <command>`

- Stands for `super-user-do`
- Enables root-user privileges (for a single command) while currently active as a user other than `root`
  - May have to enter the user's password
- However, that user may not have been given super-user privileges, in which case it won't work
  - Also called being in the "sudoers file"

### `su <username>` - switch user

- Switches you to that user
  - May have to enter their password (if they created one for their account)

### `useradd <username>` - create a new user

- Need to be the `root` user or able to use `sudo`

```sh
useradd -s /bin/bash -m -g devs <username>
```

> This will create a new user with `bash` as their default shell (the -s part), (otherwise with Ubuntu the default shell is `dash`),
>
> ...with a pre-set home directory (the -m part), (otherwise with Ubuntu it's the root but they don't have any privileges there),
>
> (In this case the user's home directory would be `/home/devs` or wherever that group's home directory is)
>
> ...and they'll be a part of the "devs" group (the -g part)

### `passwd <username>` - add a password

- Add a password to the user account.
- You will be prompted for it after entering the command (and prompted again for verification)
- Need to be the `root` user or able to use `sudo`

### `usermod` - modify a user account

- Allows you to modify user accounts (add to a group, switch their default shell, etc).

#### \- EXAMPLE:

- Add a user to the "sudoers" or "sudo group" (has `sudo` privileges):

```sh
usermod -aG sudo <username>
```

> `-aG` (or `--append --groups`) allows you to append new groups to the user.
>
> the `sudo` before <username> is the actual name of the group.

### `userdel <username>` - delete a user

- Need to be the `root` user or able to use `sudo`

---

## GROUPS

- Just like we can add and subtract permissions from a user in Linux, we can actually do it for whole cohorts of users using groups

### \- The "sudo group" (sudoers)

- These users can use `sudo`

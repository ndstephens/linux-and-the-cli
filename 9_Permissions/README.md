# Permissions

- Permissions control how every file and directory can be interacted with by users and groups
- They are set uniquely for users, groups, and everyone else
- If you create a file or folder using `sudo` then its user and group permissions will be `root`
- If you use `ls -la`, at the start of each line will be the permissions
- Separated out they look similar to:

```sh
d rwx rwx rwx
```

> The first `d` or `-` represents if it's a directory or file
>
> The following groupings represent the permissions for the user, the group, and then everyone that is not that user or in that group
>
> For each group `r` represents `read` permission, `w` for `write`, and `x` for execute. `x` means it's an executing program (just like all the commands we've been using on the CLI)

```sh
-rw-rw-r-- # is a file, it has read-and-write permission for the user and the group, and read permission for everyone else, no write. The file is not executable.

drwx------ # is a directory that can only be written and modified by the user. It's unreadable and unwritable by the group and the rest of the system.

-rwxr-xr-x # is a file, everyone can read it, everyone can execute it, and only the user can write to it.
```

## `chown` - change owner

- Enables you to change ownership of a file or directory

```sh
chown nate:nate my-folder
# or
chown <user>:<group> <file-or-folder>
chown <user> <file-or-folder> # just the user/owner
chown :<group> <file-or-folder> # just the group
```

## `chmod` - change mode

- Allows you to directly change the permissions of a file or folder rather than changing the owners.
- You change the permissions of the user and group that currently own that file or folder (and the permissions of everyone else)
- `u` for user, `g` for group, and `o` for everyone else (or "other")
- `r` for read, `w` for write, and `x` for execute

```sh
chmod u=rw,g=rw,o=rw file.txt # make it so anyone can read or write to this file
```

- There is also a binary way to do this:

```sh
chmod 777 file.txt # same as u=rwx,g=rwx,o=rwx
```

> This starts with "0" being zero permissions.
>
> Add `4` to that number if you want to enable `read` permissions.
>
> Add `2` for `write`.
>
> Add `1` for `executable`.

```sh
chmod 640 secret.txt # would make it read+write for the user, read for the group, and no permission for anyone else
```

> 0 = "---"
>
> 1 = "--x"
>
> 2 = "-w-"
>
> 3 = "-wx"
>
> 4 = "r--"
>
> 5 = "r-x"
>
> 6 = "rw-"
>
> 7 = "rwx"

- You can also just update whether or not it's executable (`x`)

```sh
chmod +x secret.txt # add executable
chmod -x secret.txt # remove executable
```

> Technically you can do that with `r` and `w` as well, it's just not as common

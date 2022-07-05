# SFTP - Secure File Transfer Protocol

## Connect

- Usually best to first setup SSH with the remote.
  - This is b/c `ssh` and `sftp` use the same/similar ports and protocols.
- Then you can use the same connection command by replacing `ssh` with `sftp`

```sh
sftp <remote-user-account>@<remote-ip-address-or-domain>
```

## Interact with file systems

- The `sftp` interactive shell is similar to a less friendly and stripped down version of `bash`.
- The thing to keep in mind is you're in two directories at the same time as opposed to normal `bash` when you're just in one.
- With `sftp`, you have a `local context` and a `remote context` (you're basically in both at the same time)
  - In order to run a local command, tack an `l` to the start of whatever command you're running, like `lls`, `lpwd`, or `lcd`.
  - When you want to do it on the remote machine, just run the commands like normal, like `ls`, `pwd`, or `cd`.
  - Review the commands you can run while in `sftp` by running `help` when in `sftp`
  - Use `!<command>` to execute that command in the local shell (or just `!` to escape to the local shell)

```sh
lpwd # local home directory
pwd # remote home directory
lls # the list of files in the local home directory
ls # the list of files in the remote home directory
help # see all the shared commands you can do
```

```sh
!touch file-to-put.txt # local only
```

> Do not spend too much time inside `sftp` because it's easier do everything in `ssh` except file transfers.

## Transferring files

- The two key commands you need to know are `get` and `put`.
  - It's from the perspective of your `local computer`, and usually you're connecting from local to remote
  - `getting` something will download it from remote to local
  - `putting` something will upload it from local to remote.

```sh
put file-to-put.txt putted-file.txt # second argument is optional, if you omit it'll just use the same name
get putted-file.txt gotten-file.txt # same thing, second one is optional
```

- **_REMEMBER:_** here's a good place to use `tar` to bundle some files together inside of moving them around individually

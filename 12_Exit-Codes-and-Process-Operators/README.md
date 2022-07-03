# Exit Codes and Process Operators

## Exit Codes

- Whenever a process exits, it exits with an exit code.
- This exit code corresponds to if a process successfully completed whatever you told it to do successfully.
  - `0` means it finished or exited successfully. All other numbers mean it did not finish successfully.
- Sometimes this is a bit misleading because some programs are meant to be stopped before they complete (`yes` will never actually complete by itself).
- A program that successfully runs and exits by itself will have an exit code of `0`. Try this:

```sh
date # show current date, runs successfully
echo $? # `$?` corresponds to the last exit code, in this case 0
yes # hit CTRL+C to stop it
echo $? # you stopped it so it exited with a non-zero code, 130
```

- Some common exit codes:

  - 0: means it was successful. Anything other than 0 means it failed
  - 1: a good general catch-all "there was an error"
  - 2: a bash internal error, meaning you or the program tried to use bash in an incorrect way
  - 126: Either you don't have permission or the file isn't executable
  - 127: Command not found
  - 128: The exit command itself had a problem, usually that you provided a non-integer exit code to it
  - 130: You ended the program with CTRL+C
  - 137: You ended the program with SIGKILL
  - 255: Out-of-bounds, you tried to exit with a code larger than 255

- Why are exit codes important?
  - Can be useful to see if a command succeeded or not.
  - Also useful for running programs in a sequence using operations.

---

## Process Operators

- What if you need to run two processes in a row, one right after another?

### `&&`

- Runs from left to right.
- Will bail if any command along the way fails.
- Successful sequence:

```sh
touch status.txt && date >> status.txt && uptime >> status.txt
cat status.txt
```

> A user needed to create a file, add the date to it, then add the current uptime to it.

- Failed sequence:

```sh
date && cat not-real-file.txt && echo hi # the date will display but hi won't
```

### `||`

- Will continue to run even if the first or current command fails.

```sh
false || echo hi # you'll see hi
false && echo hi # you won't see hi
```

> `false` is a command that always returns `1`
>
> `true` is a command that always returns `0`

### `;`

- Will always run the next command.

```sh
false ; true ; echo hey # you'll see hey
```

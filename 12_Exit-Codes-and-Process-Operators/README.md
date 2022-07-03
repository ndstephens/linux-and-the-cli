# Exit Codes and Process Operators

## Exit Codes

- Whenever a process exits, it exits with an exit code.
- This exit code corresponds to if a process successfully completed whatever you told it to do successfully.
  - `0` means it finished or exited successfully. All other numbers mean it did not finish successfully.
- Sometimes this is a bit misleading because some programs are meant to be stopped before they complete (`yes` will never actually complete by itself).
- A program that successfully runs and exits by itself will have an exit code of `0`.

### `$?`

- Corresponds to the last exit code.

```sh
date # show current date, runs successfully
echo $? # `$?` corresponds to the last exit code, in this case 0
yes # hit CTRL+C to stop it
echo $? # you stopped it so it exited with a non-zero code, 130
```

### Common exit codes:

- 0: means it was successful. Anything other than 0 means it failed
- 1: a good general catch-all "there was an error"
- 2: a bash internal error, meaning you or the program tried to use bash in an incorrect way
- 126: Either you don't have permission or the file isn't executable
- 127: Command not found
- 128: The exit command itself had a problem, usually that you provided a non-integer exit code to it
- 130: You ended the program with CTRL+C
- 137: You ended the program with SIGKILL
- 255: Out-of-bounds, you tried to exit with a code larger than 255

### Why are exit codes important?

- Can be useful to see if a command succeeded or not.
- Also useful for running programs in a sequence using operations.

---

## Process Operators

- What if you need to run two or more processes in a row, right after another?

### `&&`

- Runs from left to right.
- Will only run the next command if the previous one succeeded.
- Will bail if any command along the way fails.
- Successful sequence:

```sh
touch status.txt && date >> status.txt && uptime >> status.txt
cat status.txt
```

> A user needed to create a file, add the date to it, then add the current uptime to it.
> Each process exited with a `0` when it was done b/c it was successful.

- Failed sequence:

```sh
date && cat not-real-file.txt && echo hi # the date will display but hi won't
```

### `||`

- Will continue to run if the previous command fails.
- Otherwise it stops after the first successful command.

```sh
true || echo hi # (nothing)
true && echo hi # hi
false || echo hi # hi
false && echo hi # (nothing)
```

> `false` is a command that always returns `1` (failed exit code)
>
> `true` is a command that always returns `0` (success exit code)

### `;`

- Will always run the next command, regardless of the exit code of the previous command.

```sh
false ; true ; echo hey # hey
```

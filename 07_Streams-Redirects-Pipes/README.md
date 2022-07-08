# Streams, Redirect, and Pipes

Linux has a concept where basically all program inputs and outputs (which are text) are actually `streams` of data/text. Like plumbing pipes where you can connect and disconnect sections to redirect water to different places, so too can you connect and disconnect streams of data.

---

## Redirects - `>`, `>>`, `<`

**REDIRECTS are for streaming data between PROGRAMS and FILES:**

- `stdout` _and_ `stderr`
  - `>` - **REPLACE** - redirect a program's output stream to a file and **_replace_** its content
  - `>>` - **APPEND** - redirect a program's output stream to a file and **_append_** its content
- `stdout`
  - `1>` `1>>` - **ONLY** redirect a program's `stdout` output stream to a file
- `stderr`
  - `2>` `2>>` - **ONLY** redirect a program's `stderr` output stream to a file
- `stdin` - `<` - redirect a file's content into a program's input stream via `stdin`

---

## Standard Streams

- For streaming between programs and files or other programs
- `stdout` and `stderr` are output streams from a program
  - **_by default `stdout` and `stderr` output to the terminal screen, unless redirected or piped_**
- `stdin` is an input stream to a program

> The following will include examples using **REDIRECTS**. Pipes follow in the next section.

### `stdout` - standard output

- program output stream for all **_normal_** or **_non-error_** text
- if not redirected or piped, `stdout` by default goes to your terminal screen
- **_REMEMBER..._** the program `cat` outputs (concatenates) a file's contents to the terminal screen via `stdout`, unless it is redirected

```sh
echo "this will redirect stdout to the file and not the terminal screen" 1> file.txt
```

> The `1>` redirects echo's `stdout` from going to the terminal window and instead into a file, `file.txt`. We don't see the output of `echo` because it's been redirected.
>
> If anything had existed in `file.txt` its contents would have been replaced with the output of `echo`.

```sh
cat file.txt 1> new-file.txt
```

> `cat` outputs the content of `file.txt` to `stdout` and then `stdout` is redirected to a new file.
>
> So basically we did `cp` with more steps and concepts involved.

```sh
ls -lsah 1> output.txt # replace the contents of `output.txt` with the output of `ls -lsah`
ls -lsah 1>> output.txt # append the output of `ls -lsah` to `output.txt`
```

> What would you expect the contents of `output.txt` to be now?
>
> It's two outputs of `ls -lsah`.

### `stderr` - standard error

- program output stream for all **_caught_** or **_error_** text
- if not redirected or piped, `stderr` by default goes to your terminal screen

### Examples:

#### \- No Error:

```sh
ls -lsah 2> error-log.txt
```

> Because no error is thrown, you'll see the normal output of `stdout` on the terminal screen since we didn't redirect it (no use of `1>`) and a new file called `error-log.txt` will be created with nothing in it.

#### \- Error:

```sh
cat file-that-doesnt-exist.txt 1> file.txt
```

> The error message `cat: file-that-doesnt-exist.txt: No such file or directory` is output to the terminal screen because we're not redirecting `stderr` (no usage of `2>`). Nothing is redirected to `file.txt` b/c there was no output to `stdout`.

#### \- Error:

```sh
cat file-that-doesnt-exist.txt 2>> error-log.txt
```

> Nothing is output to the terminal screen because the error output text `cat: file-that-doesnt-exist.txt: No such file or directory` gets redirected and appended to `error-log.txt` since we used `2>>`.

### Redirecting both `stdout` and `stderr`

- This will redirect each of those streams to different files:

```sh
ls -lsah 1> stdout-log.txt 2> stderr-log.txt
```

- Or we can have them go to the same file too:

```sh
ls -lsah 1> log.txt 2> log.txt
# OR...
ls -lsah > log.txt
```

#### \- Using `/dev/null` to discard redirects

- Let's say you're running a program that's very noisy and you really only care if there's an error:

```sh
ls -lsah 1> /dev/null # assume this is a very noisy program
```

> This will run the command and only print the errors to the terminal window. Everything else (`stdout`) gets chucked into the infinite abyss. Useful sometimes

### `stdin` - standard input

- program input stream

```sh
cat < log.txt
```

> Redirect `log.txt`'s content into `cat` (via `stdin`). `cat` then outputs the text to the terminal screen via its `stdout`.
>
> `cat log.txt` would have of course done the same thing.

- Let's say it's a very long file and we want to find one very specific line:

```sh
grep "error-log.txt" < log.txt
```

> We took the contents of `log.txt` and redirected that to `grep`'s input stream via `stdin`.
>
> `grep` then looked for a line that contained the string "error-log.txt" and output the results to the terminal screen via its `stdout`.
>
> Would normally do this using a pipe instead...see example in `Pipes` section below.

### Using `stdin`, `stdout`, and `stderr`

- What if we want to use `stdin`, `stdout`, and `stderr`...and throw away the errors?

```sh
grep "error-log.txt" < log.txt 1> output.txt 2> /dev/null
```

---

## Pipes - `|`

**PIPES are for streaming data between PROGRAMS**

- Sometimes called a vertical bar
- Takes a program's output (`stdout` or `stderr`) and and streams it into another program's input (`stdin`)
- To redo the example from above:

```sh
cat log.txt | grep "error-log.txt"
```

> `cat` sends the contents of `log.txt` to `stdout` and then `|` will pipe `stdout` to the input of `grep` via its `stdin`.
>
> `grep` will then search for a text match and output its results to `stdout` to be displayed on the terminal screen.

### EXAMPLES:

#### \- Find a running process:

```sh
ps aux | grep "ps aux"
```

> `ps aux` outputs all processes to `stdout`.
>
> `stdout` is then piped into the `stdin` of `grep`.
>
> `grep` then finds just the lines it needs and outputs those to `stdout` and onto the terminal screen.
>
> This should output two lines...the original `ps aux` call and the `grep` process itself that we're running to find that `ps aux` process. Very meta!!

#### \- Find a process running in the background then kill it:

```sh
ps aux | grep "node"
```

> From the results you can grab the process-id (ex. "1224") and then kill it...

```sh
kill -9 1224
```

#### \- Script to auto-respond to interactive requests:

- `rm -i *.txt` will interactively try to remove all files with the `.txt` extension (in your current working directory).
  - It'll confirm with you on each one asking for either a `y` or `n`
- `yes` is a program that infinitely loops a `y` to `stdout` (or `n` with an argument)

```sh
yes n | rm -i *.txt
```

> `n` is infinitely output to `stdout`.
>
> `rm -i *.txt` uses those from `stdin` to answer "no" to every request to delete the next `*.txt` file.
>
> (All of the requests are still output to the terminal screen from `rm`'s `stdout` as they would have been without using `yes`).

---

## Takeaway:

- Pipes are used a lot.
- With pipes we can combine smaller programs (commands) like `grep`, `cat`, `yes` and others to make higher level programs.
- This is the beginning of Bash scripting

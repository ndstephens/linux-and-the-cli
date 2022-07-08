# Anatomy of a CLI Command

## `man <command>`

- displays the **_manual_** for a program
  - ex. `man ls`
- `--help` is usually more succinct
  - ex. `ls --help`
- uses the `less` program to work

## `<command> --help`

- a flag used after any command to get basic info about that command
  - eg. `ls --help`

## `which <command>`

- will tell you the path of the program you provide it as an argument
  - eg. `which ls` --> `/bin/ls`

## `whereis <command>`

- will tell you the path of the program you provide it as an argument
  - eg. `whereis ls` --> `ls: /bin/ls`
- **_Seems to work better sometimes_**

---

## FLAGS

### Short-Form (`-`)

- **_short-form_** flags are intended to be combined
  - `-a` and `-l` combine to `-al`
  - therefore any flag that begins with the `-` **_short-form_**, and followed by **_more than one_** character, is a combination of **_short-form_** flags

### Long-Form (`--`)

- **_long-form_** of `-a` is `--all`...which is very different from `-all`
  - `-all` is actually equivalent to the combo of the following short-form flags: `-a`, `-l`, and `-l` again
  - any flag that begins with the `--` **_long-form_** is a single flag and can not be directly combined with other flags

### Example:

- a useful **_short-form_** flag combo for `ls` is `-lah`
  - `-l` to display the long-format of the files and folders
  - `-a` to display hidden files and folders
  - `-h` to display the size information in a "human-readable" format

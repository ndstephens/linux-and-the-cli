# Interacting with Files

## `man`

- displays the **_manual_** for a program
  - ex. `man ls`
- `--help` is usually more succinct...`ls --help`
- uses the `less` program to work

## `less`

- for reading files **_a page at a time_**
- displays text in its own reader mode (**NOT** `std-out`)
- follows similar commands as `VIM`
- `q` to quit
- type a `<number>` (and `return`) to jump to that line
- `/` followed by a search term string for searching
  - `n` to get the next match
  - `N` to get the previous match
- `space` to page down
- `b` to page up

## `cat`

- unless `less` it outputs the entire file all at once
- outputs to `std-out`
- `cat` is short for **_concatenate_** because it concatenates the file to the standard output

## `head` & `tail`

- both work the same
- will output the first/last lines of a file
- by default it will output `10` lines
- set the number of lines using the flag `-n` followed by the number of lines
  - ex. `tail -n 3 textfile.txt`
- can update **_in real-time_** if you **_follow_** a file using the `-f` flag
  - ex. `tail -f textfile.txt`
  - will display the last 10 lines and update in real-time as more lines are added to the `textfile.txt` file

## `mkdir` - make directory

- creates a new folder/directory at the current location
  - eg. `mkdir new-folder`
- use the `-p` flag to create multiple nested directories
  - eg. `mkdir -p nested/folder/structure`
- both can also use and absolute path

## `touch`

- primary intent was to just _touch_ a currently existing file to update its `last_modified` or `last_accessed` time
- often is used for creating a new file at the current location
  - eg. `touch new-file.txt`
  - can also use an absolute path

## `rm` - remove

- **_BE VERY CAREFUL!! PERMANENTLY DELETES!!_**
- **FILES:**
  - eg. `rm file.txt`
- **DIRECTORIES:**
  - add the `-r` flag...means `recursive`
    - eg. `rm -r my-directory`
    - if the folder has anything in it you'll need to confirm every deletion
  - add the `-f` flag...means `force`
    - eg. `rm -rf my-directory`
    - will recursively delete everything within (and including) `my-directory`
- can instead use [trash-cli](https://github.com/andreafrancia/trash-cli)
  - puts items into a trash folder for later recovery (or permanent deletion)
  - eg. `trash-put textfile.txt`

## `cp` - copy

- **FILES**
  - eg. `cp source-file.txt destination-file.txt`
  - can also copy a file into a directory and keep the original file name
    - eg. `cp source-file.txt my-folder`
- **DIRECTORIES**
  - copy an entire folder and everything recursively in it
    - eg. `cp -R source-folder destination-folder`

## `mv` - move

- primarily used for `renaming` a file or folder
  - eg. `mv file.txt renamed.txt`
  - eg. `move folder-name new-folder-name`
  - notice you don't need a recursive flag when renaming a folder

## `tar`

- group together files and folders into a single file as a `tarball` (like a zip file)
- EX. put three files and a folder into a single tarball
  - `tar -cf archive.tar file1.txt file2.txt folder1`
  - you should now see a file called `archive.tar`. it's a single file that contains the above files and folder
  - this method **_DOES NOT COMPRESS_** the archive
- EX. `compress` the tarball with `-z` flag (also requires different file naming structure)
  - `tar -zcf archive.tar.gz file1.txt file2.txt folder1`
- EX. `unpack` or `extract` the archive (swap `-c` for `-x`)
  - `tar -xzf archive.tar.gz -C destination-folder`
  - without `-C destination-folder` it will extract in the current location

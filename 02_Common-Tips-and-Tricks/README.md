# Common Tips and Tricks

## Reverse Search (your command history)

- `CTRL-R`
- then start typing a string that was contained within a command you previously used
- the most recently used match will display
- hit `CTRL-R` again to search one step further back in your command history

## `.bash_history`

- a file containing a history of all the bash commands you previously ran
- it is only written to once you've exited your current bash session...not written to in real-time
- be careful with this as it contains **_everything_** you've typed into the command line...including credentials such as **_passwords_**

> should research how to delete such things from history

## `!!`

- referred to as "bang bang"
- `!!` is replaced with whatever was the last command you ran
- often used when you run a command and then discover `sudo` was needed
  - `sudo !!`

## Copy & Paste

- on Mac `CMD-C` and `CMD-V` will work
- on Windows will need to use `SHIFT-CTRL-C` and `SHIFT-CTRL-V`

### Be Careful...

- when copying from a website, JavaScript can switch what you think you're copying with something nefarious
- the copied string can end with a carriage return `\n` which, if pasted into the command line, would execute that code
- always best to either type things into the command line yourself, or _first_ paste what you copied into a text editor to view it safely

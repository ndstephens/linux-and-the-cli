# Environments

- The current session of your shell has many global variables already set
- Some are set and/or modified by the OS, or programs, or by you
- These are called `environment variables`
- You can modify these permanently, for a single session, or just for one command

## `env` or `printenv`

- Display all the currently set variables

## `$<VARIABLE>`

- Reference a single variable

```sh
echo hello my name is $USER # USER is currently set to "nate"
```

> Should see `hello my name is nate`

## Modify a variable for a single command:

```sh
USER=bob bash -c 'echo $USER' # bob
echo $USER # nate
```

> We add `VARIABLE=value` at the beginning to temporarily modify the variable, followed by `bash -c '<command-with-VAR>'` to execute the command (in quotes).
>
> The next reference to the variable is back to its original value.

## Modify a variable for a session:

- What if we want to modify a variable for a whole session (until you close this open session of bash).
- If you open another tab of bash, even while this one is still running, it is a different session.

```sh
echo $GREETING # (nothing if it didn't exist yet)
GREETING=hello
echo $GREETING # hello
```

> Once we close the session window, `GREETING` goes away.

## Permanently create or update a variable

- The following are global options. But usually you should only do this on a per-user basis by updating their `.bashrc` file in their home directory (explained in the next section).
  - The first global option is editing `/etc/environment`. This will modify every user's environment (often not what you want). Each line in that environment file should be `VARIABLE=value` with one per line.
  - Similar with `/etc/profile` and `/etc/bashrc` except with these you can actually invoke `scripts` within them. Again, this is **_system-wide_** and **_not_** usually what you want.

## `.bashrc` and `.bash_profile`

- If using `bash` for your shell there are two files in your user's home directory, `.bashrc` and `.bash_profile`.
  - If using `zsh` there is a `.zshrc` file.
- These are the files you need to configure and customize your `bash` shell.
- You can set things like telling `Node.js` you're in `development` mode, set up `git` how you want to, customize colors, update the `PATH`, or really anything you can write a `bash` command for.
- `.bash_profile` is only run on login shells. That is to say, it's only run once for each time you log in to your computer. It is not run after that.
- `.bashrc` is run on every non-login shell, so it's run on every tab of `bash` you start up.
- Typically you want to run your customizations on every shell so you usually just want to modify `.bashrc` and leave `.bash_profile` alone.
- I'd suggest you put this in your `.bash_profile`:

```sh
if [ -f ~/.bashrc ]; then
    source ~/.bashrc
fi
```

> That way your `.bashrc` is always run. And after you put this in there you can just forget `.bash_profile` exists and always just modify `.bashrc`.

- To have variables that affect all shell sessions, you put a line in `.bashrc` that says:

```sh
export VARIABLE=value
```

> Now it will survive when you log out.
>
> If you want that variable to affect your current shell session **_immediately_**, you'll have to do a `. ~/.bashrc` so that it will reload your `.bashrc`. The `.` means execute in this context.
>
> You also could write `source ~/.bashrc` (they are similar commands).

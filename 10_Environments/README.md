# Environments

- The current session of your shell has many variables already set
- Some are set and/or modified by the OS, or programs, or by you
- These are called `environment variables`
- You can modify these permanently, for a single session, or just for one command

## `env` or `printenv`

- Display all the currently set variables

## `$<VARIABLE>`

- Display the variable

```sh
echo hello my name is $USER # USER is currently set to "nate"
```

> Should see `hello my name is nate`

## Replace a variable for a single command:

```sh
USER=brian echo hello my name is $USER # hello my name is brian
echo hello my name is $USER # hello my name is nate
```

> We add `VARIABLE=value` part at the beginning of the command to temporarily modify the variable.

## Replace a variable for a session:

- So what if we want to modify a variable for a whole session (until you close this open session of bash; if you open another tab of bash, even while this one is still running, it is a different session):

```sh
echo $GREETING # (nothing if it didn't exist yet)
GREETING=hello
echo $GREETING # hello
```

> Once we close the session window, `GREETING` goes away.

## Permanently create or update a variable

- The following are global options. But usually you should only do this on a per-user basis by updating their `.bashrc` file in their home directory (explained in the next section).
- The first global option is editing `/etc/environment`. This will modify every user's environment so it's often not what you want. Each line in that environment file's format should be `VARIABLE=value` with one per line.
- Similar with `/etc/profile` and `/etc/bashrc` except with these you can actually invoke `scripts` within them. Again, this is **_system-wide_** and **_not_** usually what you want.

## `.bashrc` and `.bash_profile`

- If using `bash` for your shell there are two files in your user's home directory, `.bashrc` and `.bash_profile`.
  - If using `zsh` there is a `.zshrc` file.
- These are the files you need to configure and customize your `bash` shell.
- You can set things like telling Node.js you're in development mode, set up git how you want to, customize colors, set path, or really anything you can write a `bash` command for.
- `.bash_profile` is only run on login shells. That is to say, it's only run once for each time you log in to your computer. It is not run after that.
- `.bashrc` is run on every non-login shell, so it's run on every tab of `bash` you start up.
- Typically you want to run your customizations on every shell so you actually just want to modify `.bashrc` and leave `.bash_profile` alone.
- Actually, what I'd suggest you do is go put this in your `.bash_profile`:

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
> You also could write `source ~/.bashrc` and that would work too.

# Scripts

- Bash allows you to put multiple commands into one file to create a "program of programs" which is called a shell script.
- Bash is actually a programming language, we have been just been running it one line at a time via a REPL.

## First Script

- Run `vim gen_files.sh` (or `nano gen_files.sh`), put the following code in it, and save it.

```sh
mkdir -p ~/temp # `-p` means don't error if the directory already exists (among other things)
cd ~/temp
touch file{1..10}.txt
echo done
```

> This script makes a directory called `temp`, changes to the directory, generates ten files within it, and notifies `stdout` when finished.
>
> `cd ~/temp` only lasts for the duration of the script if ran using `bash` b/c `bash` runs it as a `sub-process`. The `sub-process` will change directories but once the script is finished you'll go back to your `parent-process` (and original `pwd`).
>
> If using `.` or `source` you're prompt location (or `pwd`) will be `~/temp` after the script is finished...b/c they run the script in the same `process`.

- Now to run it, do `bash gen_files.sh` or `. gen_files.sh` (or `source gen_files.sh`).
- Notice we didn't have to make `gen_files.sh` an executable file.
  - That's because we're not actually executing it directly
  - We're executing `bash` or `.` (`.` and `source` are the same thing) and **_those_** are executing our script.

---

## Turn a Script into a Command/Program

### \- Hashbang (or shebang)

- What if wanted to actually make `gen_files.sh` a new command that we didn't have to feed into `bash` or `.`?
- What if we could basically make it indistinguishable from a normal command like `cp` or `curl`?

Open `gen_files.sh` and put this as **_the very first line_**.

```sh
#! /bin/bash
```

> This line (called a "hashbang" or "shebang") let's `bash` know how to interpret and execute this file.
>
> It must be on the first line and must start with `#!`.
>
> It's then always followed by the absolute path of the program that should execute it.
>
> In this example it's telling `bash` to use `bash` to interpret this file.
>
> However, it could also be something like `#! /bin/python3` for example (if that is where the `python3` program lives exactly).
>
> **_REMEMBER:_** you can find the absolute path of a program with `which <program>`.

### \- Make it Executable

- Remove the `.sh` extension from the file:

```sh
mv gen_files.sh gen_files
```

- The file also needs the executable permission.

```sh
chmod 700 gen_files # `rwx` permissions only for the user
# or...
chmod +x gen_files # allow the user, group, and other to all have exec permissions
```

- You can now execute it directly (without `bash` or `.`) by referencing it with a relative or absolute path.
  - It knows how to run b/c of the `hashbang`
- For example, if it's in your current 'pwd' you could run the following and it would execute:

```sh
./gen_files
```

- In order to run it as a command (or program) from anywhere, without referencing its location (with a relative or absolute path) we now need to put it in our `PATH`.

### \- Add it to your `PATH`

- Your `PATH` is a series of locations on your computer where programs live.
  - If I run `python3`, it goes through each of those locations and checks for anything called `python3`.
  - If there are two or more, it uses the first one it finds (the `path` furthest left in the `PATH`).
- You can view your `PATH` if you run `echo $PATH`. It will look similar to:

```sh
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
```

> In general don't mess any of those directories.
>
> All of those are system-wide bin directories (if you had more than one user they'd share them)

- A good idea is to have your own `~/my_bin` directory (name it whatever you want):

```sh
cd ~ # go to your user's `home` directory (or wherever you want to save this bin folder)
mkdir my_bin # create our own bin directory (can name it whatever you want)
mv gen_files my_bin/gen_files # move our custom command/program into that folder
PATH=~/my_bin:$PATH # add our folder to the start of the PATH list
echo $PATH # view our PATH and verify that `~/my_bin` is at the start
gen_files # now we can globally execute our custom program
```

> We added `~/my_bin` to our path so now `bash` can execute any custom-made program we put in there.
>
> We added `~/my_bin` to the **_start_** of our path.
>
> If, for example, we wanted a different `rm` program than the default one, we don't want to mess with the system-wide one, just ours.
>
> When calling `rm` ours would be found first and therefore run instead of the system-wide one.
>
> We would want ours to "shadow" the system one and to not mess with everyone else's `rm`.
>
> Everyone else would still use the original, or system-wide, `rm` b/c they don't have our `my-bin` directory in their path.

#### \- Persist `PATH` update:

- **_NOTE:_** in the example above we only set the `PATH` for just this session. Once we close our terminal, it'll go away.
- However we can add the following line to our `.bashrc` file and it'll always be set:

```sh
export PATH=~/my_bin:$PATH
```

> **_REMEMBER:_** whenever you make a change to `.bashrc` you have to rerun it or it won't take effect on your current session.
>
> Run `. ~/.bashrc` and you'll be set.

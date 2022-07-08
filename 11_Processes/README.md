# Processes

- Everything in Linux that is running is a `process`.
  - For example, if you have a shell open, you're running `bash` as a process.
- Every running process is assigned a process ID or `pid`.
- Every process is owned by a user (such as the root)
  - Remember...a "user" can be a program

## `ps` - processes snapshot

- `ps` will show the **_current user's_** running processes
- Can test the output by running a blank process for a set amount of time in the background, then running `ps` again to see if it's there:

```sh
sleep 10 & # creates a process that runs for 10 seconds and then exits. "&" means run in the background
ps
```

## `kill` an in-flight process

```sh
sleep 100 &
ps # find the sleep pid
kill -s SIGKILL <the pid from above>
ps # notice the process has been killed
```

> Note you'll frequently see `kill -s SIGKILL <pid>` as `kill -9 <pid>`. They mean the same thing.

## `ps aux`

- Will display the running processes from **_everyone_**, including all system processes.
- You'll see a few processes running by you, many from `root`, and a few from `systemd+`, `daemon`, and others.
- Can use `grep` to find exactly what you're looking for:

```sh
ps aux | grep ps
```

> Result will include just things with `ps` in them (including the `grep` command itself).

## Foreground and Background processes

- If something is running in the foreground you'll see all the output and you will wait until it's finished.
- If it's running in the background you can still see the output (unless you redirect it) but you can start doing other things.
- When you put the `&` at the end of a command it means "run in the background"
- Try `sleep 2 &` to see this. First it'll display the `pid`. After two or more seconds, hit enter again. Bash will let you know the job completed.

## Pause a process

- What if you want to pause a running process?

```sh
sleep 100
# hit `CTRL + Z` to pause it
jobs -l # notice process is stopped
bg 1 # move job to background.  it's the first and only item in the list, the number refers to that
jobs -l # notice process is running
fg 1 # reattach to the process and put in the foreground
```

> This is a great way to start and stop scripts and in particular if you have a long running task that you want to complete but don't want to wait and want to do other things.
>
> Do be aware that if you close your terminal, however, that it will kill all your running jobs.
>
> You'll need to use something like `tmux` to keep them running.

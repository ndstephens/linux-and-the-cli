# Subcommands

- Invoke a command within a command.

```sh
echo $(whoami) is the current user # nate is the current user
```

## `$( )`

- Allows you to put bash commands inside of it. Its output will be part of an input to another command.

```sh
echo $(date +%x) – $(uptime) >> log.txt

# 06/17/20 – 21:38:34 up 8:51, 1 user, load average: 0.00, 0.00, 0.00
```

> `+%x` formats the date. See `date --help`

- Can also use backticks ` `` ` instead of `$( )`.
- But the `$( )` notation is preferred...it's the newer method. Using backticks is the old way.
- You can nest subcommands infinitely.

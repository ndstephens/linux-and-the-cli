# `cron`

- Linux has a feature called `cron` that will run tasks on a schedule.
- There are two ways to accomplish this, an easy way to remember and a slightly less easy way.

## cron folders - (easier but less options)

Any script you put in any of the following will be run on that schedule:

- `/etc/cron.daily`
- `/etc/cron.hourly`
- `/etc/cron.monthly`
- `/etc/cron.weekly`

Just make sure they have executable privileges.

- `sudo chmod +x <file>` will do that.
- Anything in those folders will be run as `root`.

---

## crontab - (more complicated but greater control)

- If you need a more defined schedule (like every five minutes, every other Thursday, every six months, etc.) then you can use the classic way, `crontab`.
- With `crontab` you can define a very specific cron schedule to execute your scripts.

**_EXAMPLE:_**

- Let's say every two minutes we want to create a new file called `file-<date-in-seconds>.txt` in a directory called `~/cron-files`.
- First, let's make the script.
  - Create it in a directory referenced in your `PATH`.
  - Name it `make-new-file`.
  - Make it executable with `chmod +x make-new-file`.
  - Put the following code in there:

```sh
#! /bin/bash

mkdir -p ~/cron-files
cd ~/cron-files
touch file-$(date +%s).txt
```

> `date +%s` gives you the epoch timestamp, or how many seconds have elapsed since `Jan 1, 1970`.

- Now run `crontab -e` (it will run this as `root`)
  - If you'd like to run it as a `user` you can do that by running `crontab -u <user> -e`.
- The first time it will ask you what editor you prefer to use to edit your crontab.
- The comments in the file explain the process fairly well:

```sh
* * * * * <the command you want to run>
```

> I believe you need to supply the `command` as an absolute path...however maybe you can just enter the command name if it's in your `PATH`

- The above five stars mean it would run every minute (of every hour, of everyday, ...).
- Each of those stars represents a frequency:

```sh
<minutes> <hours> <day of the month> <month> <day of the week>
```

- The stars mean "every", hence why five stars runs every minute.
- So if we wanted to run the command **_only_** on the `fifth minute` of `every hour`, we could do this:

```sh
5 * * * * <command>
```

- If we wanted it to run every half hour on Sundays, we could do:

```sh
# both are equivalent
*/30 * * * 0 <command>
0,30 * * * 0 <command>
```

- And so on and so forth. You can also use one of the special strings in here too:

```sh
@daily <command>
@reboot <command> # every time it starts up
@weekly <command>
@yearly <command>
@monthly <command>
@annually <command>
```

---

## www.crontab.guru

- Make use of the site [crontab.guru](https://crontab.guru/) for help creating the schedule expressions

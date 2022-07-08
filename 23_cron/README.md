# `cron`

- Linux has a feature called `cron` that will run tasks on a schedule.
- There are two ways to accomplish this, an easy way to remember and a slightly less easy way.

## cron folders

Any script you put in any of the following will be run on a schedule:

- `/etc/cron.daily`
- `/etc/cron.hourly`
- `/etc/cron.monthly`
- `/etc/cron.weekly`

Just make sure they have executable privileges.

- `sudo chmod +x <file>` will do what you need it to do.
- Anything in here will be run as `root`.

## crontab

- If you need a more defined schedule (like every five minutes, every other Thursday, every six months, etc.) then you can use the classic way, `crontab`.
- With `crontab` you can define a cron schedule to execute your scripts.
- Let's say we want to make a new file in `~/cronfiles` every two minutes.
- First, let's make the script. In your home directory, create `make-new-file` and put this in there.

```sh
mkdir -p ~/temp-files
cd ~/temp-files
touch file-$(date +%s).txt
```

> `date +%s` gives you the epoch timestamp, or how many seconds have elapsed since `Jan 1, 1970`.

- Now, if you do `crontab -e` it will run this as root.
  - If you'd like to run it as a user you can do that by doing `crontab -u <user> -e`.
  - The first time it will ask you what editor you prefer to use to edit your crontab.
- The comments in the file explains the process fairly well:

```sh
* * * * * <the command you want to run>
```

- The above five stars would run every minute.
- Each of those stars represents a frequency:

```sh
<minutes> <hours> <day of the month> <month> <day of the week>
```

- The stars mean "every", hence why five stars runs every minute.
- So if we wanted to run the command `once` an hour **_only_** on the `fifth minute`, we could do this:

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

- Make use of the site [crontab.guru](https://crontab.guru/) for help creating the schedule expressions

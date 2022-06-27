# Signals and the Power of CTRL

- the `CTRL` key is very commonly used on the command line
- it's used for shortcuts and to send very specific signals to the shell

## Shortcuts

- `CTRL + A` –-> takes you to the beginning of the line
- `CTRL + E` –-> takes you to the end of the line
- `CTRL + K` –-> "yank" everything after the cursor
- `CTRL + U` –-> "yank" everything before the cursor
- `CTRL + Y` --> "paste" (paste in quotes because it doesn't actually go into your system clipboard) everything you yanked
- `CTRL + L` --> clear the screen
- `CTRL + R` –-> reverse search through history

## Signals

- `SIGINT` --> `CTRL + C`
  - If you hit `CTRL + C` while a program is running, you're telling it to **_interrupt_** what it's doing and stop
- `SIGQUIT` --> `CTRL + D`
  - less useful, many programs don't respond to a `SIGQUIT`
  - can also try typing in `exit`
- `SIGTERM` --> (no shortcut)
  - If I use the `kill` program to kill another program, the way it does that is by sending a SIGTERM to the program. The difference is that if the program doesn't exit, kill will still shut down the process
- `SIGKILL`
  - If you want a program to stop and stop **now**, you can do `kill -9 <program-id>` (or `kill -SIGKILL <program-id>`) and it will send `SIGKILL` which means to the program "don't clean up, just stop as soon as possible"
- More signals
  - If you run `kill -l` in your terminal, it'll show you all the signals your computer supports

| SIG-CMD         | SIG-CMD         | SIG-CMD         | SIG-CMD         | SIG-CMD         |
| --------------- | --------------- | --------------- | --------------- | --------------- |
| 1) SIGHUP       | 2) SIGINT       | 3) SIGQUIT      | 4) SIGILL       | 5) SIGTRAP      |
| 6) SIGABRT      | 7) SIGBUS       | 8) SIGFPE       | 9) SIGKILL      | 10) SIGUSR1     |
| 11) SIGSEGV     | 12) SIGUSR2     | 13) SIGPIPE     | 14) SIGALRM     | 15) SIGTERM     |
| 16) SIGSTKFLT   | 17) SIGCHLD     | 18) SIGCONT     | 19) SIGSTOP     | 20) SIGTSTP     |
| 21) SIGTTIN     | 22) SIGTTOU     | 23) SIGURG      | 24) SIGXCPU     | 25) SIGXFSZ     |
| 26) SIGVTALRM   | 27) SIGPROF     | 28) SIGWINCH    | 29) SIGIO       | 30) SIGPWR      |
| 31) SIGSYS      | 34) SIGRTMIN    | 35) SIGRTMIN+1  | 36) SIGRTMIN+2  | 37) SIGRTMIN+3  |
| 38) SIGRTMIN+4  | 39) SIGRTMIN+5  | 40) SIGRTMIN+6  | 41) SIGRTMIN+7  | 42) SIGRTMIN+8  |
| 43) SIGRTMIN+9  | 44) SIGRTMIN+10 | 45) SIGRTMIN+11 | 46) SIGRTMIN+12 | 47) SIGRTMIN+13 |
| 48) SIGRTMIN+14 | 49) SIGRTMIN+15 | 50) SIGRTMAX-14 | 51) SIGRTMAX-13 | 52) SIGRTMAX-12 |
| 53) SIGRTMAX-11 | 54) SIGRTMAX-10 | 55) SIGRTMAX-9  | 56) SIGRTMAX-8  | 57) SIGRTMAX-7  |
| 58) SIGRTMAX-6  | 59) SIGRTMAX-5  | 60) SIGRTMAX-4  | 61) SIGRTMAX-3  | 62) SIGRTMAX-2  |
| 63) SIGRTMAX-1  | 64) SIGRTMAX    |

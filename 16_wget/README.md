# `wget`

- `wget` works like `cp` but instead of copying a local file you're copying something off the net.
- You'll identify a remote file (usually a URL) that you want to fetch and save to your local file system:

```sh
wget https://raw.githubusercontent.com/btholt/bash2048/master/bash2048.sh
chmod 700 bash2048.sh
. bash2048.sh
```

> `wget` gets the file
>
> `chmod 700` makes the file executable, readable, and writable for the current user (and no one else)
>
> `. bash2048.sh` executes the file (it's a game)

- The one case you'll want to use `wget` is if you want `recursive downloads` of a site.
- `wget` has a peculiar ability that it will read the incoming document and download all the links it finds within it, crawling all the documents until it downloads all the files it found.
- That can occasionally be useful and not something `curl` does by itself.
- Otherwise you should usually use `curl`.
- `wget` does not use `stdin` and `stdout` so you can't use it with pipes `|`.

## ALWAYS REVIEW THE CODE IN A BASH SCRIPT YOU DOWNLOAD BEFORE RUNNING IT UNLESS YOU'RE 100% CERTAIN IT IS SAFE

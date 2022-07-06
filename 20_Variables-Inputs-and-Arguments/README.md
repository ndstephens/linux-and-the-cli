# Variables, User Inputs, and Arguments

## Variables

- As you write more complicated scripts you need to use variables to make it more flexible.

### Setting a Variable

- Setting a variable is as easy as saying `NAME=value`.
- You can use quotes too, optionally.
  - `NAME="value"`
- You do not have to make them uppercase though it's suggested as that's standard for bash scripts.

```sh
#! /bin/bash

DESTINATION=~/temp
FILE_PREFIX=file

mkdir -p $DESTINATION
cd $DESTINATION
touch ${FILE_PREFIX}{1..10}.txt
echo done
```

> In regards to `${FILE_PREFIX}{1..10}.txt`, why don't we need the `{}`'s for the first two referenced variables, but we do on that one?
>
> That's because we're inserting it in the middle of something.
>
> The `{}`'s let `bash` know where the variable name stops.
>
> The first two you can totally use them too e.g. `cd ${DESTINATION}` but it's optional.

- **_REMEMBER:_** if you use `$()` it means a subcommand like `touch $(whoami).txt`.

## User Input

- So what if we want users to be able to define the file prefix?
- There's a program called `read` that will get user input and define a variable based on it.
- Try it by running `read name && echo hello $name`

```sh
#! /bin/bash

DESTINATION=~/temp
read -p "enter a file prefix: " FILE_PREFIX # set FILE_PREFIX via a user input

mkdir -p $DESTINATION
cd $DESTINATION
touch ${FILE_PREFIX}{1..10}.txt
echo done
```

> The `-p` flag allows us to prompt the user with a string, letting them know what we're expecting.

## Arguments

- What if we want the user to be able to pass in the `path` to where we want to create the directory?
- We can do that via `arguments` (sometimes called `parameters` too.)
- We want the user to be able say `gen_files ~/<different_directory>` and use that input as `$DESTINATION`.

```sh
#! /bin/bash

DESTINATION=$1
read -p "enter a file prefix: " FILE_PREFIX

mkdir -p $DESTINATION
cd $DESTINATION
touch ${FILE_PREFIX}{1..10}.txt
echo done
```

> Here we just replaced what went into `DESTINATION` with `$1`.
>
> We totally could have replaced everywhere there was `DESTINATION` with `$1`, but it was easier (and made the script clearer) by replacing the contents of `DESTINATION` with `$1`.

- `$0` is available here too. It'll be `gen_files`. And if you gave two arguments, the second one will be `$2` and so on and so forth.

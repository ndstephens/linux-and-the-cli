# Variables, User Inputs, and Arguments

## Variables

- As you write more complicated scripts you need to use variables to make it more flexible.

### Setting a Variable

- Setting a variable is as easy as saying `NAME=value`.
- You can use quotes too, optionally.
  - `NAME="value"`
- You do not have to make them uppercase though it's suggested as that's standard for bash scripts.

#### \- EXAMPLE: create a script/program called `gen_files`

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
> With the first two you can still use `{}` (e.g. `cd ${DESTINATION}`) but it's optional.

- Run the program:

```sh
gen_files # runs the program
done # output from the program finishing

# 10 files named file.txt through file0.txt were created in `~/temp`
```

- **_REMEMBER:_** if you use `$( )` it means a subcommand like `touch $(whoami).txt`.

---

## User Input

User inputs are supplied by the user after running the command.

- So what if we want users to be able to define the file prefix?
- There's a program called `read` that will get user input and define a variable based on it.

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

- Run the program:

```sh
gen_files # runs the program
enter a file prefix: # prompt displayed in terminal
# user enters "log" and hits return
done # output from the program finishing

# 10 files named log1.txt through log10.txt were created in `~/temp`
```

---

## Arguments

Arguments are supplied directly after (on the same line as) the command.

- What if we want the user to be able to pass in the `path` to where we create the directory?
- We can do that via `arguments` (sometimes called `parameters` too)
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

> Here we just replaced `DESTINATION` with the first argument (`$1`).
>
> We could have replaced all uses of `DESTINATION` with `$1`, but it was easier (and made the script clearer) by replacing the contents of `DESTINATION` with `$1`.

- Run the program:

```sh
gen_files ~/my-directory # runs the program, setting DESTINATION to "~/my-directory"
enter a file prefix: # prompt displayed in terminal
# user enters "log" and hits return
done # output from the program finishing

# 10 files named log1.txt through log10.txt were created in `~/temp`
```

- `$0` is available here too. It'll be `gen_files` (the program). And if you gave two arguments, the second one will be `$2` and so on and so forth.

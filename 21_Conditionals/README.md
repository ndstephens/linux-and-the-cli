# Conditionals

- In order to write useful bash scripts you need conditionals.
- A conditional is a statement that only runs if a condition is true.

## `if` Statements

- Let's say we want to use the path `~/temp` if the user doesn't provide an argument.

```sh
#! /bin/bash

DESTINATION=$1
read -p "enter a file prefix: " FILE_PREFIX

if [ -z $DESTINATION ]; then
  echo "no path provided, defaulting to ~/temp"
  DESTINATION=~/temp
fi

mkdir -p $DESTINATION
cd $DESTINATION
touch ${FILE_PREFIX}{1..10}.txt
echo done
```

> Notice it begins with `if` and concludes with `fi` ("if" backwards).

### `[]` or `test`

- The `[]`'s are a special notation which actually translate to the `test` command.
  - They take the place of the `test` command.
- The condition in the example above actually evaluates to `test -z $DESTINATION`.
- **_NOTE:_** If you forget how to do conditional checks you can always run `man test` and it's a pretty understandable list of the various things you can do.
- In this case `-z $DESTINATION` is checking to see if `DESTINATION` is a zero length string which would mean the user didn't provide anything.

```sh
test -z ""
echo $? # 0, this is true
test -z "lol"
echo $? # 1, this is false
```

**_NOTE:_** unlike JavaScript...

- `0` means `true` (b/c it's a successful exit code)
- `1` means `false`

Examples of some other operators other than `-z`:

```sh
test 15 -eq 15 # 0
test brian = brian # 0
test brian != brian # 1
test 15 -gt 10 # 0 - gt means greater than
test 15 -le 10 # 1 - le means less than or equal to
test -e ~/some-file.txt # tests to see if a file exists
test -w ~/some-file.txt # tests to see if a file exists and you can write to it
```

---

## `else` and `elif`

```sh
if [ $1 -gt 10 ]; then
  echo "greater than 10"
elif [ $1 -lt 10 ]; then
  echo "less than 10"
else
  echo "equals 10"
fi
```

> This will let the user give an argument of a number and it will tell you if it's greater than, equal to, or less than 10 using conditionals.

---

## `case` Statements

```sh
case $1 in
  "smile")
    echo ":)"
    ;;
  "sad")
    echo ":("
    ;;
  "laugh")
    echo ":D"
    ;;
  "sword")
    echo "o()xxx[{::::::::::::::>"
    ;;
  "surprise")
    echo "O_O"
    ;;
  *)
    echo "I don't know that one yet!"
    ;;
esac
```

> Notice that, similar to `if` and `fi`, it begins with `case` and concludes with `esac` ("case" backwards).

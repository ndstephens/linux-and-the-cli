# Wildcards and Replacements (Expansions)

> `bash` does the translation of wildcards and replacements, **_not_** the programs

## Wildcards

- `*` represents **_0 or more_** characters of replacement
- `?` represents **_exactly one_** character of replacement
  - can use `??` to replace exactly `2` characters in a row

```sh
touch file1.txt file2.txt file.txt
ls file*.txt
ls file?.txt
```

> Notice the first ls call does output file.txt and the second one doesn't

- `[]` can limit the accepted characters
  - eg. `ls file[1-5].txt`
- `^` negates characters
  - eg. `ls file[^1-5].txt` any number **_except_** 1-5

## Expansions

- `{}`
- eg. You wanted to create three files using touch all at once. You could do:

```sh
touch file4.txt
touch file5.txt
touch file6.txt
```

- Or use an expansion:

```sh
touch file{4,5,6}.txt
# or
touch file{4..6}.txt
```

- Adding a blank after a comma would create a file with no number

```sh
touch file{4,5,6,}.txt
# also creates file.txt
```

- A few more examples

```sh
echo {a..z} # prints a to z
echo {z..a} # reverse order
echo {0..100..2} # prints every other (aka even) number from 0 to 100
echo {100..0..5} # prints every 5th number in reverse order from 100 to 0
echo {a..z}{1..5} # prints out a1 a2 a3 a4 a5 b1 b2 b3 <etc>
```

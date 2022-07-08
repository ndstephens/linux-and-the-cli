# Loops and Arrays

## Arrays and `for`-Loops

```sh
#!/bin/bash

friends=(Kyle Marc Jem "Brian Holt" Sarah) # an array

echo My second friend is ${friends[1]}

for friend in ${friends[*]} # for-loop
do
    echo friend: $friend
done

echo "I have ${#friends[*]} friends"
```

> The `friends=(Kyle Marc Jem "Brian Holt" Sarah)` line is how to `define an array`. If it's just one word (e.g. Kyle or Marc in this case) then you don't need quotes. You'll see for "Brian Holt" I added quotes so it can capture the space too.
>
> You see `${friends[1]}` is how you `access items in an array`. You do need the `{}` in this case or else it'll confuse `bash` with path expansion stuff.
>
> Then we do a loop. We need to type `${friends[*]}` to `access everything in the array`. If you wrote `echo ${friends[*]}` it would print the whole array.
>
> Then we can loop with `do` to **_start_** and `done` to **_end_** it.
>
> Lastly if you want to see the `length`, you use `${#friends[*]}`.

---

## `while`

- What if we wanted to make a program that wouldn't exit until you guessed the correct number?
- We can use a `while` loop together with read:

```sh
# let "NUM_TO_GUESS = ${RANDOM} % 10 + 1"
NUM_TO_GUESS=$(( $RANDOM % 10 + 1 ))
GUESSED_NUM=0

echo "guess a number between 1 and 10"

while [ $NUM_TO_GUESS -ne $GUESSED_NUM ]
do
  read -p "your guess: " GUESSED_NUM
done

echo "you got it!"
```

> `$RANDOM` is just a random number which we're using modulo (`%`) to get a random number between 1 and 10.
>
> On the line that starts with `read`, `GUESSED_NUM` does not start with a `$` b/c we aren't reading it as a variable. It is being set in that case.
>
> The `while` loop looks a lot like an `if statement`.

- `let` is a program that allows you to do math.
- You feed it a string of math of some variety and it will evaluate it for you.
- The shortcut to doing that (similar to how `test` works with `[]`) is the dollar sign (`$`) with double parentheses (`(( ))`).
- The two lines there are equivalent.

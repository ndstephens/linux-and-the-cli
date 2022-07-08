# VIM

## Basic Commands (or Command Modes)

### Command Mode

- the default mode
- highlight a character and press `x` to delete that character
- `:d` deletes the entire line
  - `:d3` will delete 3 lines
- `h` --> `left`
- `j` --> `down`
- `k` --> `up`
- `l` --> `right`
  - **_arrow keys also work_**

### Insert Mode (enables typing)

- press `i` key to enter `Insert Mode`
- should see `-- INSERT --` at the bottom of the screen
- press `esc` key to revert back to `Command Mode`
- **Save**
  - `:w` --> Save
  - `:wq` --> Save then Quit
- **Quit**
  - `:q` --> Quit
    - if you try to quit with unsaved changes it won't let you
  - `:q!` --> Quit without saving
  - `:qa!` --> "try to gracefully quit everything and if not, just quit anyway"
- **Exit**
  - `CTRL-D` a few times

---

## How to Learn VIM

- When in Command Mode
  - `:help tutor` starts the tutor where you can learn more
  - [vim-adventures](https://vim-adventures.com/)

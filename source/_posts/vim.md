---
title: Vim
categories: '-计算机'
date: 2024-2-16
abbrlink: 104c461b
---
# Vim

**Vim is an command-line-based editor purely used with keyboard**

## Modal editing (使用模式)

- **Normal**: for moving around a file and making edits ,press `<Esc>` to enter
- **Insert**: for inserting text, press `i` to enter
- **Replace**: for replacing text, press `r` to enter
- **Visual** (plain, line, or block): for selecting blocks of text, press `v` to enter
- **Command-line**: for running a command, press `:` to enter

## Basics

### Inserting text

From Normal mode, press `i` to **enter Insert mode**. Now, Vim behaves like any other text editor, until you press `<ESC>` to return to Normal mode. 



### Command-line

Command mode can be entered by typing `:` in Normal mode. Your cursor will jump to the command line at the bottom of the screen upon pressing `:`. This mode has many functionalities, including **opening, saving, and closing files, and quitting Vim.**

- `:q` quit (close window being edited now)
- `:w` save (“write”)
- `:wq` save and quit
- `:e {name of file}` open file for editing
- `:ls` show open buffers
- `:help {topic}`open help
  - example
    - `:help :w` opens help for the `:w` command
    - `:help w` opens help for the `w` movement

## Vim’s interface is a programming language

### Movement

- Basic movement: `hjkl` (left, down, up, right)

- Words: `w` (next word), `b` (beginning of word), `e` (end of word)

- Lines: `0` (beginning of line), `^` (first non-blank character), `$` (end of line)

- Screen: `H` (top of screen), `M` (middle of screen), `L` (bottom of screen)

- Scroll: `Ctrl-u` (up), `Ctrl-d` (down)

- File: `gg` (beginning of file), `G` (end of file)

- Line numbers: `:{number}<CR>` or `{number}G` (line {number})

- Misc: `%` (corresponding item)

- Find:

  ```plaintext
  f{character},t{character},F{character},T{character}
  ```

  - find/to forward/backward {character} on the current line
  - `,` / `;` for navigating matches

- Search: `/{regex}`, `n` / `N` for navigating matches

### Selection

Visual modes:

- Visual: `v`
- Visual Line: `V`
- Visual Block: `Ctrl-v` ***[Or denoted as ^v or <c-v>]***

Can use movement keys to make selection.

### Edits

*Everything that you used to do with the mouse, you now do with the keyboard using editing commands that compose with movement commands.* 

- `i` enter Insert mode
  - but for manipulating/deleting text, want to use something more than backspace
- `o` / `O` insert line below / above
- `d{motion}`delete {motion}
  - e.g. `dw` is delete word, `d$` is delete to end of line, `d0` is delete to beginning of line
- `c{motion}`change {motion}
  - e.g. `cw` is change word
  - like `d{motion}` followed by `i`
- `x` delete character (equal do `dl`)
- `s` substitute character (equal to `cl`)
- Visual mode + manipulation
  - select text, `d` to delete it or `c` to change it
- `u` to undo, `<C-r>` to redo
- `y` to copy / “yank” (some other commands like `d` also copy)
- `p` to paste
- Lots more to learn: e.g. `~` flips the case of a character

### Counts

- `3w` move 3 words forward
- `5j` move 5 lines down
- `7dw` delete 7 words

### Modifiers

You can use modifiers to change the meaning of a noun. Some modifiers are `i`, which means “inner” or “inside”, and `a`, which means “around”.

- `ci(` change the contents inside the current pair of parentheses
- `ci[` change the contents inside the current pair of square brackets
- `da'` delete a single-quoted string, including the surrounding single quotes

### Demo/EX

Here is a broken [fizz buzz](https://en.wikipedia.org/wiki/Fizz_buzz) implementation:

```python
def fizz_buzz(limit):
    for i in range(limit):
        if i % 3 == 0:
            print('fizz')
        if i % 5 == 0:
            print('fizz')
        if i % 3 and i % 5:
            print(i)
def main():
    fizz_buzz(10)
```

We will fix the following issues:

- Main is never called
- Starts at 0 instead of 1
- Prints “fizz” and “buzz” on separate lines for multiples of 15
- Prints “fizz” for multiples of 5
- Uses a hard-coded argument of 10 instead of taking a command-line argument

### Customizing Vim

Vim is customized through a plain-text configuration file in `~/.vimrc`

## Advanced Vim

Here are a few examples to show you the power of the editor. We can’t teach you all of these kinds of things, but you’ll learn them as you go. A good heuristic: whenever you’re using your editor and you think “there must be a better way of doing this”, there probably is: look it up online.

### Search and replace

`:s` (substitute) command ([documentation](http://vim.wikia.com/wiki/Search_and_replace)).

- ```plaintext
  %s/foo/bar/g
  ```

  - replace foo with bar globally in file

- ```plaintext
  %s/\[.*\](\(.*\))/\1/g
  ```

  - replace named Markdown links with plain URLs

### Multiple windows

- `:sp` / `:vsp` to split windows
- Can have multiple views of the same buffer.

### Macros

- `q{character}` to start recording a macro in register `{character}`
- `q` to stop recording
- `@{character}` replays the macro
- Macro execution stops on error
- `{number}@{character}` executes a macro {number} times
- Macros can be recursive
  - first clear the macro with `q{character}q`
  - record the macro, with `@{character}` to invoke the macro recursively (will be a no-op until recording is complete)
- Example: convert xml to json (file)
  - Array of objects with keys “name” / “email”
  - Use a Python program?
  - Use sed / regexes
    - `g/people/d`
    - `%s/<person>/{/g`
    - `%s/<name>\(.*\)<\/name>/"name": "\1",/g`
    - …
  - Vim commands / macros
    - `Gdd`, `ggdd` delete first and last lines
    - Macro to format a single element (register`e`)
      - Go to line with `<name>`
      - `qe^r"f>s": "<ESC>f<C"<ESC>q`
    - Macro to format a person
      - Go to line with `<person>`
      - `qpS{<ESC>j@eA,<ESC>j@ejS},<ESC>q`
    - Macro to format a person and go to the next person
      - Go to line with `<person>`
      - `qq@pjq`
    - Execute macro until end of file
      - `999@q`
    - Manually remove last `,` and add `[` and `]` delimiters
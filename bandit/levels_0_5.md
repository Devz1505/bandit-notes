# OverTheWire Bandit — Learning Notes

> Personal notes from solving OverTheWire Bandit.
> Focus on Linux concepts, not passwords.

---

# Level 0 — SSH Login

## Goal

Connect to the Bandit server using SSH.

---

## Concepts Learned

- SSH (Secure Shell) allows secure remote login.
- Every user has a username and password.
- SSH connects to a specific host and port.

---

## New Command

### ssh

Purpose:
Connect to a remote machine securely.

Syntax:

ssh username@host -p port

Example:

ssh bandit0@bandit.labs.overthewire.org -p 2220

---

## Mistakes I Made

- Forgot to specify the username.
- SSH defaulted to my Windows username and returned "Permission denied."

---

## Takeaways

- Always specify the username.
- The default SSH port is 22.
- Bandit uses port 2220.

---

# Level 0 → 1 — Reading Files

## Goal

Find the password stored in a file.

---

## Concepts Learned

- After logging in, you start in your home directory.
- Files can be viewed without opening an editor.
- Linux treats everything as files.

---

## New Commands

### ls

Purpose:
List files and directories.

Examples:

ls
ls -a
ls -l
ls -la

---

### cat

Purpose:
Display the contents of a text file.

Syntax:

cat filename

---

## Mistakes I Made

- None.

---

## Takeaways

- Use `ls` to explore.
- Use `cat` to read text files.

---

# Level 1 → 2 — Reading a File Named "-"

## Goal

Read a file whose filename is a single dash (`-`).

---

## Concepts Learned

- Some filenames have special meanings.
- `-` is interpreted as standard input by many commands.
- Prefixing a filename with `./` tells Linux it is a path.

---

## New Concepts

### Standard Input (stdin)

Some commands interpret `-` as "read from keyboard/input."

---

## Solutions

cat ./-

or

cat < -

---

## Mistakes I Made

- Tried:

cat -

which waited for keyboard input.

---

## Takeaways

- `./` means "current directory."
- `./` is useful whenever filenames begin with special characters.

---

# Level 2 → 3 — Spaces in Filenames

## Goal

Read a file whose name contains spaces.

---

## Concepts Learned

- The shell splits words at spaces.
- Spaces inside filenames must be escaped or quoted.

---

## Methods

Escape spaces:

cat spaces\ in\ this\ filename

or

Use quotes:

cat "spaces in this filename"

---

## Mistakes I Made

- Forgot that spaces separate command arguments.

---

## Takeaways

- Quotes preserve spaces.
- Backslash escapes a single character.

---

# Level 3 → 4 — Hidden Files

## Goal

Find a hidden file inside the `inhere` directory.

---

## Concepts Learned

- Hidden files begin with a dot (`.`).
- `ls` does not show hidden files by default.

---

## New Commands

### ls -a

Shows hidden files.

### ls -la

Shows hidden files with detailed information.

---

## Mistakes I Made

- Tried using `exit` when I only wanted to leave the directory.

---

## Takeaways

- `cd ..` moves to the parent directory.
- `exit` closes the current shell/session.
- Hidden files are normal files with names beginning with `.`.

---

# Level 4 → 5 — Human Readable Files

## Goal

Find the only human-readable file.

---

## Concepts Learned

- Binary files and text files are different.
- `file` identifies a file's type.
- Filenames beginning with `-` may be interpreted as command options.

---

## New Commands

### file

Purpose:

Determine a file's type.

Examples:

file filename

file ./*

---

## Mistakes I Made

Tried:

file -file00

Linux interpreted `-file00` as an option.

---

## Correct Method

file ./-file00

or

file ./*

---

## Takeaways

- `./` safely refers to files beginning with `-`.
- `file` is much better than randomly using `cat` on unknown files.

---

# Level 5 → 6 — Searching Files

## Goal

Find a file that is:

- Human-readable
- Exactly 1033 bytes
- Not executable

---

## Concepts Learned

- `find` searches recursively.
- `find` can filter by file type and size.
- File size units in `find` are important.

---

## New Commands

### find

Purpose:

Search for files matching conditions.

Examples:

find .

find . -type f

find . -size 1033c

---

### od

Purpose:

Display the raw contents of a file.

Example:

od -c filename

Useful for viewing:

- Newlines (`\n`)
- Tabs (`\t`)
- NUL bytes (`\0`)

---

## Important Discovery

In `find`:

c = bytes

b = 512-byte blocks

This was the biggest lesson of the level.

---

## Mistakes I Made

Tried:

find -size 1033b

Thinking `b` meant bytes.

It actually means 512-byte blocks.

---

## Correct Command

find . -type f -size 1033c

---

## Interesting Observation

Using:

od -c filename

showed:

- the password characters
- a newline (`\n`)
- remaining NUL bytes
- file offsets displayed in octal

---

## Takeaways

- Read `find --help` instead of guessing.
- `find` is one of Linux's most powerful commands.
- Learn what command options mean instead of memorizing them.

---

# Linux Concepts Learned So Far

## Commands

- ssh
- ls
- cat
- cd
- file
- find
- od

---

## Shell Concepts

- Hidden files (`.`)
- Current directory (`./`)
- Parent directory (`..`)
- Standard input
- Quoting filenames
- Escaping spaces
- Wildcards (`*`)
- Command options
- File paths

---

# Questions for Future Learning

- Why does `find` use 512-byte blocks by default?
- Why does `od` display offsets in octal?
- How does the shell expand `*` before executing commands?
- How do Linux permissions actually work?

---

# Personal Lessons

✔ Read the error message carefully.

✔ Read `--help` before searching online.

✔ Understand *why* a command works.

✔ Never memorize commands without understanding the concepts behind them.

✔ Every mistake teaches a Linux concept.
# OverTheWire Bandit — Learning Notes

> Personal notes from solving Bandit wargame challenges.
> No passwords posted — just concepts and lessons learned.

---

## Level 0 — SSH Login

**Concept:** Connecting to a remote server using SSH

**Syntax:** `ssh username@host -p port`

**Command used:** `ssh bandit0@bandit.labs.overthewire.org -p 2220`

**Mistake I made:** Forgot to specify the username. SSH defaulted to my Windows username and kept saying "permission denied."

**Takeaway:** Always specify the username before the @ symbol. The `-p` flag sets a non-standard port. Default SSH port is 22 — Bandit uses 2220.

---

## Level 0 → 1 — Reading Files

**Concept:** Navigating directories and reading files in Linux

**Commands learned:**
- `ls` — list files in current directory
- `cat readme` — print file contents to screen

**Takeaway:** After SSH login you land in the home directory. Use `ls` to look around, `cat` to read.

---

## Level 1 → 2 — Dashed Filename

**Concept:** Reading a file whose name is a special character (`-`)

**The problem:** `cat -` doesn't work because Linux interprets `-` as "read from standard input" not as a filename.

**Solutions that work:**
- `cat < -` — uses input redirection, the shell opens the file before cat sees it
- `cat ./-` — the `./` prefix tells cat "this is a file in the current directory"

**Takeaway:** Special characters in filenames need escaping or workarounds. The `./` prefix trick works for many special filename problems, not just dashes.

---

*More levels will be added as I progress.*
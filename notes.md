\# 🎮 OverTheWire Bandit — Learning Notes



> Personal notes from solving Bandit wargame challenges.

> No passwords posted — just concepts and lessons learned.



\---



\## Level 0 — SSH Login



| Item | Detail |

|------|--------|

| \*\*Concept\*\* | Connecting to a remote server using SSH |

| \*\*Syntax\*\* | `ssh username@host -p port` |

| \*\*Command\*\* | `ssh bandit0@bandit.labs.overthewire.org -p 2220` |



\*\*Mistake I made:\*\* Forgot to specify the username. SSH defaulted to my Windows username (`devav`) and kept saying "permission denied."



\*\*Takeaway:\*\* The `-p` flag sets a non-standard port. Default SSH port is 22 — Bandit uses 2220.



\---



\## Level 0 → 1 — Reading Files



| Item | Detail |

|------|--------|

| \*\*Concept\*\* | Navigating directories and reading files |

| \*\*Commands\*\* | `ls` — list files in current directory |

| | `cat readme` — print file contents to screen |



\*\*Takeaway:\*\* After SSH login you land in the home directory. Use `ls` to look around, `cat` to read.



\---



\*Levels will be added as I progress.\*


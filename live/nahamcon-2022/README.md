# [NahamCon CTF 2022](https://ctf.nahamcon.com)

## Summary
Only played for a couple hours while live and solved a few warm-up challenges.

## Solves
1. **Flagcat**: Download and run `cat` on a file
2. **Exit Vim**: Self-explanatory
3. **Crash Override**: Given source materials (C source code, ELF binary, and Makefile), SSH into VM running the \
  `crash_override` program. Source code showed a `win` method that would open and output contents of file `flag.txt`. \
  The `win` method was called when `SIGSEGV` signal was triggered, which could be triggered by exceeding the input buffer \
  set to 2048 characters. Input of a long string of `A` caused the program to print the flag.
4. **Read the Rules**: Flag in HTML webpage source
5. **Wizard**: A series of value transformations to and from binary, hexadecimal, octal, ASCII, Base64, and little- and big-endian. \
  Solved in a Python shell using `binascii` and other Python utilities/packages (didn't document at the time).

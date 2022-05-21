# [Cyber Apocalypse CTF 2022: Intergalactic Chase](https://www.hackthebox.com/events/cyber-apocalypse-2022)
## Summary
Played on-and-off for a few days. Biggest lesson: get better time management. Out of 60 available challenges, 
I only tried three because I stubbornly sunk way too much time into the entry web challenge (Kryptos Support).
I would have learned more (and probably gotten more solves) if I had timeboxed my attempts and moved on to other challenges.

## Solves
### pwn
- **Space Pirate Entrypoint**
  - 1 star
  - Download: zip with ELF binary, `glibc` library files, `gdb` history file, and fake flag file for local testing
  - Procedure: Ran strings on binary to find a leetspeak pass phrase and a command for `cat flag`. Used Ghidra to 
    disassemble and decompile binary. Follow function chain from `main()` to see that the program expects two inputs.
    First input: prompts "scan card" and checks for `2`. Second input: prompts for access code and checks against string
    `0nlyTh30r1g1n4lCr3wM3mb3r5C4nP455`. However, it only checks the first 14 characters, and then it checks for a 
    non-equal state. (This doesn't really make sense, and my notes are sparse--but it worked, so... :shrug:) Command is
    executed on system to `cat` the flag file to the console.

## Attempts
### web
- **Kryptos Support**
  - 1 star
  - Download: None (Access container through web browser)
  - Procedure: I threw things at the wall for literally days on end, and I learned that I don't have that many things
    to throw at the wall after all for web apps. I used Burp Suite to pick apart the requests and tried to fish out API
    endpoints. I found pages blocked by authorization, but couldn't spoof a sesssion cookie. Since the website was running
    in quirks mode, I tried to get the CSS files to illegally pull the blocked pages with relative imports. I tried basic 
    SQL and JavaScript injection, but I realized that I don't really know how to leverage either very well. Overall, I 
    realized that experience with web app development does not necessarily translate into web app exploitation.

### crypto
- **Android in the Middle**
  - 1 star
  - Download: zip with Python file
  - Procedure: 

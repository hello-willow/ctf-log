# [Cyber Apocalypse CTF 2022: Intergalactic Chase](https://www.hackthebox.com/events/cyber-apocalypse-2022)
## Summary
Played on-and-off for a few days. Biggest lesson: get better time management. Out of 60 available challenges, 
I only tried three because I stubbornly sunk way too much time into the entry web challenge (Kryptos Support).
I would have learned more (and probably gotten more solves) if I had timeboxed my attempts and moved on to other challenges.

## Solves 🐇
### pwn
- **Space Pirate Entrypoint**
  - 1 star
  - Download: zip with ELF binary, `glibc` library files, `gdb` history file, and fake flag file for local testing
  - Procedure: Ran strings on binary to find a leetspeak pass phrase and a command for `cat flag`. Used Ghidra to 
    disassemble and decompile binary. Follow function chain from `main()` to see that the program expects two inputs.
    First input: prompts "scan card" and checks for `2`. Second input: prompts for access code and checks against string
    `0nlyTh30r1g1n4lCr3wM3mb3r5C4nP455`. However, it only checks the first 14 characters, and then it checks for a 
    non-equal state. (This doesn't really make sense, but my notes are sparse and it worked, so... :shrug:) Command is
    executed on system to `cat` the flag file to the console.

## Attempts ♟️
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
  - Procedure: Read Python file to see a TCP server that expects two inputs to validate a user using public-key cryptography. 
    I ran the file to spawn a local TCP server, and used a Python shell to mimic the procedure outlined in the file. The file used AES
    encryption tools from the Python `Crypto.Cipher` package. First, the server generated two global variables. Using the Python `random`
    package, generate private key `c`. Then use `pow()` to generate the public key by raising the first global variable to the power of `c`,
    modulo the second global variable. Then again use `pow()` to raise the public key to the power of the private key, modulo the second 
    globabl variable. With this shared secret, create a key using `hashlib.md5()`. The key is used to create a new AES cipher object, 
    which is then used to encrypt the expected message (`Initialization Sequence - Code 0`). However, the server expects the message to 
    be in hex format, so run `.hex()` on the encrypted ciphertext. I tried several times on both the local and remote server, and I couldn't 
    get an encrypted message to be accepted. I think I understood the overall process, but something was not lining up.


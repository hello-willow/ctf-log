# crackmes

### `cr1n63y-cr4ckm3y`
- Author: binariez, Difficulty: 1.2
- Language: C/C++, Platform: Windows, Arch: x86
- Description: my first crackme
- Process: In Ghidra, examine disassembled & decompiled entry function. User input is checked against hardcoded value `0x3f`. Use CyberChef to translate to corresponding ASCII character.

### `Very Easy CrackMe`
- Author: szlug3ns, Difficulty: 1.3
- Language: C/C++, Platform: Windows, Arch: x86-64
- Description: Very Easy CrackMe for complete beginners
- Process: In Ghidra, find entry function. Track string processing through called function. Get lost in C++ string manipulation and indexing. Run `strings` on executable instead and find hex string in the output.

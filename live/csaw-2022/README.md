# [CSAW 2022](https://ctf.csaw.io/)

# Summary
Played Friday and Saturday afternoon and night. Need either a new computer or rollback to an older version of VMWare workstation. All VMs keep pegging the CPU and crashing with kernel alerts. Re-installed Windows and VMWare workstation, but didn't spend any more time fixing it. Workaround is to watch VM CPU usage and pause the VM before it locks up entirely.

## Solves 🐇
### RE
- **DockREleakage**
  - No need to run any containers on this. I just untarred the individual container layers (sidenote: the download is labeled a `.tar.gz`, but it's not actually compressed so it just needs to be untarred as well) and found the flag in a combination of plaintext and a base64 string. The `manifest.json` points to the config file, where commands to be executed in each layer show a base64 string and a couple of flag text files. The unicode `>` threw me for a second, but the decoded base64 string plus the plaintext in the Docker `latest` layer (marked in repositories file) produced the completed flag.

## Attempts ♟️
### web
- **World Wide Web**
  - Hyperlink hopscotch across series of webpages covered in anchor HTML tags. Used HTML search to quickly find the actual `href` in each page. Got to a dummy HTML page with just the text `Boooo!`, but that was not the flag. Page also sends a same-site lax cookie called `solChain`. I tried resending the cookie wiht BurpSuite but couldn't figure out what value it was looking for (simply JavaScript injection didn't do anything).
  - Notes from team solve: Use recursive option on `wget`: `wget -r -l 10000 http://web.chal.csaw.io:5010/`. Flag was in a file on page ~99.

### crypto
- **Phi Too Much in Common**
  - The server produces a new n, e, and c for (presumably) the same message every time. n is around 308 digits long, so I don't think factorization for p and q is plausible. I did some reading on Hastad's Broadcast Attack and the Chinese Remainder Theorem, but I couldn't get any of the math to work. (Also those all showed a low public exponent of around 3, and e here is much larger.)

### forensics
- **noir**
  - PNG steganography. In the downloaded `noir.png`, binwalk showed a Zlib file:
```
# binwalk noir.png

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 1359 x 1919, 8-bit/color RGBA, non-interlaced
41            0x29            Zlib compressed data, default compression
```

Extracted with `binwalk -e noir.png`. (Had to install older version of binwalk due to some bug where `--run-as-root` option wasn't working.) Result of extraction was a file `29.zlib`. (I think named for its hex location in the original file.) Binwalk on this file picked up three more data types (I think by detecting file signatures and magic bytes):
```
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
572157        0x8BAFD         Cisco IOS experimental microcode, for "mM"
1189462       0x122656        QNX4 Boot Block
2177596       0x213A3C        MySQL ISAM compressed data file Version 7
```
Extracted these files with `binwalk --dd='.*' 29.out`. File types of the three extracted files:

```
# file 122656  
122656: DOS executable (COM)

# file 213A3C 
213A3C: MySQL ISAM compressed data file Version 7
                                                                                                                        
# file 8BAFD 
8BAFD: cisco IOS experimental microcode for 'mM'
```
Didn't make any progress on analyzing, decompressing, or running any of these files. The MySQL ISAM file was marked as a false positive by another CTF write-up, and I couldn't figure out which processor or language to get either the DOS executable or the Cisco microcode to properly load in Ghidra.


### pwn
- **how2pwn**
  - Barely started this one, and I wish I had found it earlier because it seems like a well-designed challenge to learn shellcode. I still have the contents locally saved to a VM and might pick it back up later.

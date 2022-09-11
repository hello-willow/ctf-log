# [CSAW 2022](https://ctf.csaw.io/)

# Summary
Played Friday and Saturday afternoon and night. Need either a new computer or rollback to an older version of VMWare workstation. All VMs keep pegging the CPU and crashing with kernel alerts. Re-installed Windows and VMWare workstation, but didn't spend anymore time fixing it. Workaround is to watch VM CPU usage and pause the VM before it locks up entirely.

## Solves 🐇
### RE
- **DockREleakage**
  - No need to run any containers on this. I just untarred the individual container layers (sidenote: the download is labeled a .tar.gz, but it's not actually compressed so it just needs to be untarred as well) and found the flag in a combination of plaintext and a base64 string. The manifest.json points to the config file, where commands to be executed in each layer how a base64 string and a couple flag text files. The unicode `>` threw me for a second, but the decoded base64 string plus the plaintext in the Docker :latest layer (marked in repositories file) produced the completed flag.

## Attempts ♟️
### web

### crypto

### forensics

### pwn

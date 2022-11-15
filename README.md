# misc-command
Just a collections of commonly used command or script

## WSL/WSL2
1. Create new instance(s):
```bash
wsl --import <Distribution Name> <Installation Folder> <Ubuntu WSL2 Image Tarball path>
```
2. See distribution lists:
```bash
wsl -l -v
```
3. Login to instance:
```bash
wsl -d <Distribution Name>
```
4. Setup user accounts:
```bash
NEW_USER=<USERNAME>
useradd -m -G sudo -s /bin/bash "$NEW_USER"
passwd "$NEW_USER"
```
5. Configure default user:
```bash
tee /etc/wsl.conf <<_EOF
[user]
default=${NEW_USER}
_EOF
```
6. Shutdown WSL:
```bash
wsl --shutdown
```

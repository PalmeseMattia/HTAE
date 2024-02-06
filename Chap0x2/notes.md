```bash
$ objdump -D a.out -M intel | grep -A20 main.:
```
```nasm
0000000000001149 <main>:
    1149:       f3 0f 1e fa             endbr64
    114d:       55                      push   rbp
    114e:       48 89 e5                mov    rbp,rsp
    1151:       48 83 ec 10             sub    rsp,0x10
    1155:       c7 45 fc 00 00 00 00    mov    DWORD PTR [rbp-0x4],0x0 #set i to 0
    115c:       eb 13                   jmp    1171 <main+0x28>
    115e:       48 8d 05 9f 0e 00 00    lea    rax,[rip+0xe9f]        # 2004 <_IO_stdin_used+0x4>
    1165:       48 89 c7                mov    rdi,rax
    1168:       e8 e3 fe ff ff          call   1050 <puts@plt>
    116d:       83 45 fc 01             add    DWORD PTR [rbp-0x4],0x1      #add 1 to i
    1171:       83 7d fc 09             cmp    DWORD PTR [rbp-0x4],0x9      #cmp i to 9
    1175:       7e e7                   jle    115e <main+0x15>     #jmp if less than to 115e
    1177:       b8 00 00 00 00          mov    eax,0x0
    117c:       c9                      leave
    117d:       c3                      ret

Disassembly of section .fini:

0000000000001180 <_fini>:
    1180:       f3 0f 1e fa             endbr64
```
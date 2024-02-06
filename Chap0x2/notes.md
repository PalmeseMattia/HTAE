Objdump displays informations about object files. We can use it as a disassembler: 

```bash
objdump -D a.out -M intel | grep -A20 main.:
```

```nasm
0000000000001149 <main>:
    1149:       f3 0f 1e fa             endbr64
    114d:       55                      push   rbp
    114e:       48 89 e5                mov    rbp,rsp
    1151:       48 83 ec 10             sub    rsp,0x10
    1155:       c7 45 fc 00 00 00 00    mov    DWORD PTR [rbp-0x4],0x0      #set i to 0
    115c:       eb 13                   jmp    1171 <main+0x28>
    115e:       48 8d 05 9f 0e 00 00    lea    rax,[rip+0xe9f]              # 2004 <_IO_stdin_used+0x4>
    1165:       48 89 c7                mov    rdi,rax
    1168:       e8 e3 fe ff ff          call   1050 <puts@plt>
    116d:       83 45 fc 01             add    DWORD PTR [rbp-0x4],0x1      #add 1 to i
    1171:       83 7d fc 09             cmp    DWORD PTR [rbp-0x4],0x9      #cmp i to 9
    1175:       7e e7                   jle    115e <main+0x15>             #jmp if less than to 115e
    1177:       b8 00 00 00 00          mov    eax,0x0
    117c:       c9                      leave
    117d:       c3                      ret

Disassembly of section .fini:

0000000000001180 <_fini>:
    1180:       f3 0f 1e fa             endbr64
```

Let's start with debugging helloworld: 

```bash
gdb -q ./a.out
```

Add a breakpoint at the main function and run the program. 
After, we control the registers before the execution of the program: 
```gdb
(gdb) break main
(gdb) run
(gdb) info registers
```

```gdb
rax            0x555555555149      93824992235849
rbx            0x0                 0
rcx            0x555555557dc0      93824992247232
rdx            0x7fffffffe1b8      140737488347576
rsi            0x7fffffffe1a8      140737488347560
rdi            0x1                 1
rbp            0x7fffffffe090      0x7fffffffe090
rsp            0x7fffffffe090      0x7fffffffe090
r8             0x7ffff7fa7f10      140737353776912
r9             0x7ffff7fc9040      140737353912384
r10            0x7ffff7fc3908      140737353890056
r11            0x7ffff7fde660      140737353999968
r12            0x7fffffffe1a8      140737488347560
r13            0x555555555149      93824992235849
r14            0x555555557dc0      93824992247232
r15            0x7ffff7ffd040      140737354125376
rip            0x555555555151      0x555555555151 <main+8>
eflags         0x246               [ PF ZF IF ]
cs             0x33                51
ss             0x2b                43
ds             0x0                 0
es             0x0                 0
fs             0x0                 0
gs             0x0                 0
```

The first four registers are generics register. They are called:
- rax: register accumulator
- rbx: register base
- rcx: register counter
- rdx: register 

These registers, along with rax and rbx, form the set of primary general-purpose registers available for use in x86-64 assembly language programming.
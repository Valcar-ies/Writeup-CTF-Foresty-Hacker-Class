# Sanity Check
>Here is your flag: 
>466f726573747948437b77656c636f6d655f746f5f6861636b65725f636c6173735f666f72657374795f3539366537377d0a

## About the Challenge
Diberikan sebuah barisan karakter ascii dengan tampilan seperti berikut :

![gambar](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/d7e8b636-0a98-4453-a97c-d59384d014ce)

## Solution
Soal tersebut kemungkinan besar merupakan soal cryptography
dan asumsi saya rangkaian char ini merupakan hexadesimal, atau base16 yang terdiri dari angka 0-9 dan huruf a-f

>Saya mencoba menggunakan script python untuk mengubahnya 

```py 
import binascii
strings = "466f726573747948437b77656c636f6d655f746f5f6861636b65725f636c6173735f666f72657374795f3539366537377d0a"
print(binascii.unhexlify(strings))
```
![gambar](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/fb802beb-bec0-4e61-944f-e8b8d959bcd2)

Menghasilkan Output :
![gambar](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/3fc215a2-e1e8-4a7d-b190-98d8d66ad254)

Flag yang didapat :
```
ForestyHC{welcome_to_hacker_class_foresty_596e77}
```

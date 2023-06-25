# Recover Me 
## SOLUTION:

1. Pada challenge ini kita diberikan sebuah file gdocs dan diminta untuk mencari URL yang disembunyikan.
2. Untuk mendapatkan URL tersebut, saya membuka version history dari gdocs.

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/763212fa-840d-482b-ba72-c92fddd384f7)


![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/f65fdbd2-4099-4ca9-a1da-cccac702bb34)


> isi dari link

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/743357b3-ee7d-4c15-a71b-faed6d9ffcb8)


3. Namun nampaknya file png ini corrupt.

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/9752428f-f1f6-4937-b679-2fa7d53e3f18)


4. Mengetahui hal ini saya langsung mengecek CRC pada gambar. Benar saja bahwa signature header untuk PNG file ini tampered.

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/7f33f2df-6962-4874-82ea-e9ca170d8504)


5. Tidak hanya itu, saat saya scoll ke bawah, dapat dilihat bahwa CRC akhir dari PNG juga tampered.

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/959741ad-7485-4ec7-b46c-bd669e4db0e1)


6. Pada signature header saya mengubah hex value menjadi:

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/086cd574-dbe8-4157-b8bb-9a57256e97dd)


7. Lalu untuk CRC akhir saya mengubahnya menjadi:

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/1fc95e05-963c-4d6c-bb8c-485ea3f19157)


8. Langsung saja kita buka gambarnya.

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/8524a891-6f89-4d69-a598-7b9a52c7a834)


9. Flag berhasil di dapat!

## FLAG -> ForestyHC{f0rensh33sh_isnt_th4t_h4rdzz_h0h0_ef233c}

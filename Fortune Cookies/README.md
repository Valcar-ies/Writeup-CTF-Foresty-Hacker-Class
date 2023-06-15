# Fortune Cookies
> Would you like to have some fortune cookies?
> http://103.167.136.89:10088/

## About the Challenge
Diberikan sebuah website dengan tampilan seperti berikut :

![gambar](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/65375cd5-06f2-4cf9-8c25-04c799109d38)

## Solution
Cek Inspection dengan mengklik F12, Soal ini kemungkinan besar bermain dengan cookie

![gambar](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/ce088ce7-b8f1-40fe-9c8a-bbdbbb277dff)

Lalu buka cookie pada inspection dan ubah nilai flag dari 0 menjadi 1

![gambar](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/fdfe2376-d34c-48e9-97c0-a9eeeb9379fa)

Coba jalankan ulang website dengan click button "Get Your Fortune"

![gambar](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/3a5f268f-3e16-47d6-8cc2-d856112717cf)

Maka dapat dilihat, flag yang didapat adalah :

```
ForestyHC{here_is_your_fortun3_cookie_4a0a47}
```

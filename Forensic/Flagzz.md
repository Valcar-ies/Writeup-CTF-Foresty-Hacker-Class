# Flagzz 
## SOLUTION:

1. Pada challenge ini, kami diberikan sebuah file .wav yang nampaknya corrupt.

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/960eb6da-ecd7-4461-a3ec-1bcdce2ca61e)


2. Mengetahui hal ini audacity tidak bisa menerima file ini kecuali, kita mengimportkan raw data.

> Di audacity

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/f73700e2-0b0c-472c-be2b-28e43d663b2b)


![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/af5714ba-c8e2-4750-9043-bf321f2dc607)


![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/8ea63d62-31e8-44c8-afec-b1af451fcd17)


3. Nampaknya diberikan sebuah link -> bit.ly/flagzz.
4. Berikut adalah isinya:

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/04bc55cd-e81d-4296-b4b5-e6283b4c62e2)


5. Diberikan file pcap new generation. Langsung saja kita buka di wireshark.

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/4b40a1b0-d05a-4d72-a9ab-f78ba5b14cf2)


6. Nampaknya traffic yang ditangkap disini, merupakan web traffic. Pada mulanya saya mencari terlebih dahulu method POST yang ada pada traffic ini.
7. Diketahui terdapat 1 packet dengan POST method.


![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/c945b325-e77f-4b0d-8f5a-96da541c9561)


8. Langsung saja kita follow HTTP stream untuk melihat isi packet (request & response header/body).

![image](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/40c9499a-3d81-44e0-bc5b-90865c8ed4df)


9. Flag berhasil didapat (tertulis dengan format ascii art).


## FLAG -> ForestyHC{h3h3_u_found_m3_btw_infokan_libut_smt_a12e47}

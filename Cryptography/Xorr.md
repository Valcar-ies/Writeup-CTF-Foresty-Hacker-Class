# Xorrr
>Still remember last night?
>355c111740002628673f08580617432b36056c14425d072d6c0c6f196c10006c111745472d185a1b1f563c4055156e590704
1. Pada challenge ini diberikan sebuah XORed text -> `355c111740002628673f08580617432b36056c14425d072d6c0c6f196c10006c111745472d185a1b1f563c4055156e590704`.
2. Pada deskripsi soal tidak diberikan KEY yang dapat kita gunakan untuk mendekripsi ciphertext. Namun kita dapat me-leak KEY tersebut dengan menggunakan Format flag sebagai KEY. 
3. Notice, kita juga diberikan algoritma enkripsi yang digunakan:

```py
#!/usr/bin/python3

FLAG = b"ForestyCTF{XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX}"
KEY = b"??????????"

assert len(KEY) == 10

def encrypt(plaintext : bytes, key : bytes) -> bytes:
    ciphertext = []
    for i in range(len(plaintext)):
        ciphertext.append(plaintext[i] ^ key[i % len(key)])
    return bytes(ciphertext).hex()

encrypted_flag = encrypt(FLAG, KEY) 
print(encrypted_flag)
```

4. Hal yang menarik disini, terdapat deklarasi assert len(KEY) == 10, yang berarti panjang KEY haruslah 10.
5. Diketahui jika kita menggunakan format flag, maka panjang KEY adalah 11. Maka dari itu kita harus meng-exclude `{`.
6. Kita dapat me-reverse logic pada source code.
7. Berikut adalah modified scriptnya:

```py
#!/usr/bin/python3
'''
FLAG = b"ForestyCTF{XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX}"
KEY = b"??????????"

assert len(KEY) == 10

def encrypt(plaintext : bytes, key : bytes) -> bytes:
    ciphertext = []
    for i in range(len(plaintext)):
        ciphertext.append(plaintext[i] ^ key[i % len(key)])
    return bytes(ciphertext).hex()

encrypted_flag = encrypt(FLAG, KEY) 
print(encrypted_flag)

## enc flag = 355c111740002628673f08580617432b36056c14425d072d6c0c6f196c10006c111745472d185a1b1f563c4055156e590704
'''

encrypted_flag = "355c111740002628673f08580617432b36056c14425d072d6c0c6f196c10006c111745472d185a1b1f563c4055156e590704"
#KEY = "ForestyCTF" # leaking the xor key
KEY = "s3cr3t_k3y" # leaked XOR KEY [we shall use this]

def decrypt(ciphertext: str, key: bytes) -> bytes:
    ciphertext_bytes = bytes.fromhex(ciphertext)
    plaintext = []
    for i in range(len(ciphertext_bytes)):
        plaintext.append(ciphertext_bytes[i] ^ ord(key[i % len(key)]))
    return bytes(plaintext)

decrypted_flag = decrypt(encrypted_flag, KEY)
print(decrypted_flag.decode()) # print flag
```
Hasil Output :

![gambar](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/c3e7d407-5fee-4dee-9270-24045005da4e)

Flag yang didapat!
```console
ForestyCTF{keep_in_m1nd__x0r_is_rev3rsible_2fa124}
```




# Vigenere
>You have stumbled upon a suspicious piece of encrypted text. It appears to be encrypted using some cipher. Your task is to decrypt the message and uncover the hidden flag within.

1. Diberikan sebuah encrypted flag sebagai berikut: `KciikmwMQ{3q_z1y3gcws_tl1h3k_u1yv_w0v35lr_i3d_t15uis}`.
2. Berdasarkan judul soal, sudah sangat jelas bahwa enkripsi yang digunakan yaitu vigenere. 
3. Untuk melakukan dekripsi vigenere cipher, dibutuhkan sebuah "KEY". Mengingat tidak diberikan KEY pada deskripsi soal maka tidak mungkin untuk mendekripsi flag, kecuali menggunakan metode bruteforce.
4. Namun berdasarkan lecture terakhir.. Kunci yang mungkin digunakan oleh probset yaitu berada pada format flag -> **Foresty**.
5. Langsung saja kita coba decrypt.
6. Berikut adalah solver yang saya gunakan:

```py
def vigenere(strings, key):
    strings = strings.upper()
    key = key.upper()
    
    key_index = 0

    result = ""

    for i in strings:
        if i.isalpha():
            if i.isupper():
                ascii_offset = ord('A')
            key_stream = key[key_index % len(key)]

            if key_stream.isupper():
                key_offset = ord('A')
            char_enc_dec = chr(((ord(i) - ascii_offset - (ord(key_stream) - key_offset)) % 26) + ascii_offset)
            result += char_enc_dec

            key_index += 1
        else:
            result += i
    return result

strings = "KciikmwMQ{3q_z1y3gcws_tl1h3k_u1yv_w0v35lr_i3d_t15uis}"
decoded_strings = vigenere(strings, 'Foresty')
print(decoded_strings)
```

>Result
![gambar](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/aa9c9025-663c-4237-b435-fd30c317a9f8)

Didapatkan Flag dari hasil di atas 
```console
FORESTYHC{3Z_V1G3NERE_CH1P3R_W1TH_F0R35TY_K3Y_F15DEA}
```

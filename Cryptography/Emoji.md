# Emoji
>My friend sent a message that contains a lot of emojis. He says that there is a secret message behind it. Can you find the message behind it?

1. Pada challenge ini kita diberikan 2 file, yakni source code dan encrypted text.

> Source code (Given Hint)

```py
import string

def emojiCrypt(plainText):
    emojis = []
    for c in plainText:
        if c not in string.ascii_uppercase:
            emojis.append(c)
        else:
            code = string.ascii_uppercase.index(c) + 0x1F600
            emojis.append(chr(code))
    return ' '.join(emojis)
```

> Encrypted

```
😈 😒 😓 😇 😈 😒 😑 😄 😀 😋 😋 😘 😂 😑 😘 😏 😓 😎 😂 😇 😀 😋 😋
```

2. Karena diberikan source code untuk melakukan enkripsi, maka dapat kita reverse logicnya untuk melakukan dekripsi. Berikut adalah modified scriptnya:

```py
emoji = "😈 😒 😓 😇 😈 😒 😑 😄 😀 😋 😋 😘 😂 😑 😘 😏 😓 😎 😂 😇 😀 😋 😋"

no_space = ""
for emo in emoji:
    no_space += emo.strip(" ")
#print(no_space)

result = ""
for items in no_space:
    result += chr((ord(items) - 0x1F600) + ord('A'))
print(result)
```
>Hasil Output

![gambar](https://github.com/Valcar-ies/Writeup-CTF-Foresty-Hacker-Class/assets/84186470/51fba190-f4a7-4fcf-a0c9-e1dbda393437)

3. Wrap hasil output  dengan `ForestyHC{}`.
4. Flag berhasil didapat!

```console
ForestyHC{ISTHISREALLYCRYPTOCHALL}
```

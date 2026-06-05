---
title: The Man Himself
description: BYU CTF 2026
author: Zinko
date: 2026-04-10
categories: [Crypto]
media_subpath: '/assets/img/posts/TheManHimself'
---

This challenge was hard due to my own incompetence using python...

## Challenge

Starting by connecting to the server I do some poking around.

![We have keys!](Intro.png)

I fortunately know that one of the cool properties of the xor function is that you can inverse it.

This inverse property means that because A ^ B = C, C ^ B = A.

Using this property allows me to come up with an algorithm to solve the challenge.

We're given key 1. We're also given the result of key 1 ^ key 2 (which I'll call B). This we can do key 1 ^ B = key 2.

Rinse and repeat for the rest and we have our solve algorithm

## Python troubles
It was at this point that I started having issues with python...

After messing around for a while I figured out the keys I was given on each connection were different. The connection died after a minute and I couldn't copy and paste things fast enough.

I was going to have to script this.

In order to get a connection setup I was advised to use pwntools. My python install is a bit broken so getting it installed was an... ordeal.

Alas, the installation was completed and I was ready to script. 

I start off my making a remote connection.
```python
conn = remote('server', port)
print(str(conn.recv()))
```

I had a hard time splitting parsing the text and splitting the keys but here's my jank solution that finally worked.
```python
connArr = str(conn.recv())
connArr = connArr.split(": ")
kOA = connArr[1].split('\\n')
kTwA = connArr[2].split('\\n')
kThA = connArr[3].split('\\n')
kFA = connArr[4].split('\\n')
```

Now, I found out the hard way that hex() is not a datatype in python, it converts a int to a string. I had lots of issues trying to convert between ints and hex due to that lack of knowledge.

```python
keyOne =  int(kOA[0],16)
keyTwoIsh = int(kTwA[0],16)
keyThrees = int(kThA[0],16)
flagIsh = int(kFA[0],16)
```

Now that I had all of the my information in int format I was able to xor them together. Using the formula I created earlier we ended up with this.
```python
keyTwo = keyTwoIsh ^ keyOne
keyThree = keyTwo ^ keyThrees
flag = keyThree ^ flagIsh
```

I then try sending my string using `conn.send(hex(flag).encode())` but it didn't work. After 20 minutes of banging my head against a wall I realized that the program didn't want my encoded hex, it wanted a decoded string.

I took the hex string I sent and threw it into cyberchief, voila!

`I'm_4_b1g_b1g_p00py_p4nts_unf0rtun4t3ly`

I threw this string back into the program and got the flag.

Flag: byuctf{x0r_1s_4ctu4lIy_just_4_ch1ll_guy_0meg4l0l}

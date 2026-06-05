---
title: JavaScript Easy
description: BYU CTF 2026
author: Zinko
date: 2025-12-05
categories: [Rev]
---

The goal of this challenge is for us to reverse a obfuscated javascript file! Now I haven't done much rev so this is going to be exciting...

We're given our file... what even am I looking at...

```javascript
const _0xdd87f8=_0x2701;(function(_0x539a6a,_0x39c5b2){const _0x50ae1d=_0x2701,_0x2ed310=_0x539a6a();while(!![]){try{const _0x5d0398=-parseInt(_0x50ae1d(0xec))/0x1*(parseInt(_0x50ae1d(0xf0))/0x2)+-parseInt(_0x50ae1d(0xea))/0x3+parseInt(_0x50ae1d(0xeb))/0x4+-parseInt(_0x50ae1d(0xe8))/0x5*(-parseInt(_0x50ae1d(0xf3))/0x6)+parseInt(_0x50ae1d(0xef))/0x7+-parseInt(_0x50ae1d(0xf1))/0x8*(parseInt(_0x50ae1d(0xee))/0x9)+parseInt(_0x50ae1d(0xf5))/0xa;if(_0x5d0398===_0x39c5b2)break;else _0x2ed310['push'](_0x2ed310['shift']());}catch(_0x27b245){_0x2ed310['push'](_0x2ed310['shift']());}}}(_0x4f75,0x60a23));const flagData=[0x23,0x1e,0x57,0x22,0x13,0x44,0x3a,0xd,0x51,0x1e,0x3,0x47,0x2e,0x5,0x44,0x1e,0xe,0x51,0x1e,0x2,0x43,0x32,0x1e,0x7d,0x36,0xe,0x56,0x29,0x38,0x56,0x2e,0x8,0x4e,0x32,0x1a];function checkFlag(_0x1d632a){const _0x37f8bd=_0x2701;if(_0x1d632a[_0x37f8bd(0xf6)]!=flagData[_0x37f8bd(0xf6)])return-0x1;for(let _0x5c1d65=0x0;_0x5c1d65<flagData[_0x37f8bd(0xf6)];_0x5c1d65+=0x3){if((_0x1d632a[_0x37f8bd(0xf2)](_0x5c1d65)^0x41)!=flagData[_0x5c1d65])return-0x1;}for(let _0x3eec29=0x1;_0x3eec29<flagData[_0x37f8bd(0xf6)];_0x3eec29+=0x3){if((_0x1d632a['charCodeAt'](_0x3eec29)^0x67)!=flagData[_0x3eec29])return-0x1;}for(let _0x4093a3=0x2;_0x4093a3<flagData[_0x37f8bd(0xf6)];_0x4093a3+=0x3){if((_0x1d632a[_0x37f8bd(0xf2)](_0x4093a3)^0x22)!=flagData[_0x4093a3])return-0x1;}return 0x0;}const userInput=prompt(_0xdd87f8(0xed));function _0x2701(_0x1a41ef,_0x199f7d){const _0x4f75a2=_0x4f75();return _0x2701=function(_0x270179,_0x30ad77){_0x270179=_0x270179-0xe8;let _0x3ea788=_0x4f75a2[_0x270179];return _0x3ea788;},_0x2701(_0x1a41ef,_0x199f7d);}!checkFlag(userInput)?console[_0xdd87f8(0xe9)](_0xdd87f8(0xf4)):console[_0xdd87f8(0xe9)]('nope');function _0x4f75(){const _0x18a6be=['charCodeAt','254526CeWYok','You\x20got\x20it!','8359870apaJgI','length','25rBvkPJ','log','1615677dSVEPq','1774720fyuYfc','2KXGBtB','fleg?','9CHhLNi','2314963vMWEyW','710926vZIYDE','1417480IONgKn'];_0x4f75=function(){return _0x18a6be;};return _0x4f75();}
```

That is a lot of words that I have no idea what they mean. I proceed to do some poking around and find this cool online tool called https://deobfuscate.io/.

I put it in there to try to figure out what I'm even looking at and this is my result:

```javascript
const flagData = [0x23, 0x1e, 0x57, 0x22, 0x13, 0x44, 0x3a, 0xd, 0x51, 0x1e, 0x3, 0x47, 0x2e, 0x5, 0x44, 0x1e, 0xe, 0x51, 0x1e, 0x2, 0x43, 0x32, 0x1e, 0x7d, 0x36, 0xe, 0x56, 0x29, 0x38, 0x56, 0x2e, 0x8, 0x4e, 0x32, 0x1a];
function checkFlag(_0x1d632a) {
  if (_0x1d632a.length != flagData.length) {
    return -0x1;
  }
  for (let _0x5c1d65 = 0x0; _0x5c1d65 < flagData.length; _0x5c1d65 += 0x3) {
    if ((_0x1d632a.charCodeAt(_0x5c1d65) ^ 0x41) != flagData[_0x5c1d65]) {
      return -0x1;
    }
  }
  for (let _0x3eec29 = 0x1; _0x3eec29 < flagData.length; _0x3eec29 += 0x3) {
    if ((_0x1d632a.charCodeAt(_0x3eec29) ^ 0x67) != flagData[_0x3eec29]) {
      return -0x1;
    }
  }
  for (let _0x4093a3 = 0x2; _0x4093a3 < flagData.length; _0x4093a3 += 0x3) {
    if ((_0x1d632a.charCodeAt(_0x4093a3) ^ 0x22) != flagData[_0x4093a3]) {
      return -0x1;
    }
  }
  return 0x0;
}
const userInput = prompt("fleg?");
if (!checkFlag(userInput)) {
  console.log("You got it!");
} else {
  console.log('nope');
}
```

This is much more reasonable now, the code is readable (well I supposed if you're blind it didn't make much of a difference).

I next set at improving the readability even further by renaming variables (I wonder if blind people are actually really good at rev because they don't have to make it human readable).

```javascript
function checkFlag(flag) {
    if (flag.length != flagData.length) {
        return -0x1;
    }
    for (let i = 0x0; i < flagData.length; _0x5c1d65 += 0x3) {
        if ((flag.charCodeAt(i) ^ 0x41) != flagData[i]) {
            return -0x1;
        }
    }
    for (let i = 0x1; i < flagData.length; i += 0x3) {
        if ((flag.charCodeAt(i) ^ 0x67) != flagData[i]) {
            return -0x1;
        }
    }
    for (let i = 0x2; i < flagData.length; i += 0x3) {
        if ((flag.charCodeAt(i) ^ 0x22) != flagData[i]) {
            return -0x1;
        }
    }
    return 0x0;
}
```

At this point it become obvious to me what was happening. It was going through our flag and xoring every 3rd character with a key (I mean braille is a form of binary right? I wonder if there's some sort of connecting that blind people would just be able to read the bits of the code better?). 

I then set about writing a reversal script. I could've had AI write it and it would've been like 5x faster but I decided to do it on my own.

A few syntax errors later I have my solve code.

```javascript
for (let i = 0; i < flagData.length; i+= 3){
        newFlagChar=flagData[i] ^ 0x41;
        newFlagData.push(newFlagChar);
    }

    for (let i = 1; i < flagData.length; i+= 3){
        newFlagChar=flagData[i] ^ 0x67;
        newFlagData.push(newFlagChar);
    }

    for (let i = 2; i < flagData.length; i+= 3){
        newFlagChar=flagData[i] ^ 0x22;
        newFlagData.push(newFlagChar);
    }
    
    console.log(newFlagData);
```

From this I get my array of numbers and I start seeings ones I like! We got 98, 117, and others that are in the ascii lowercase letter range. I start decoding it manually to check it out.

To my apprehension I realized that my array was incorrect!
```
98 -> b
99 -> c
123 -> {
```

That doesn't say byuctf{} like it's supposed to!

I then realized that it is only grabbing every 3rd character. Faces were palmed today.

Alas I resolved to write new code, making it better then ever before (and also adding an auto ascii translator so I didn't have to do it manually).

With that we have our final solve code.

```Javascript
const flagData = [0x23, 0x1e, 0x57, 0x22, 0x13, 0x44, 0x3a, 0xd, 0x51, 0x1e, 0x3, 0x47, 0x2e, 0x5, 0x44, 0x1e, 0xe, 0x51, 0x1e, 0x2, 0x43, 0x32, 0x1e, 0x7d, 0x36, 0xe, 0x56, 0x29, 0x38, 0x56, 0x2e, 0x8, 0x4e, 0x32, 0x1a];

let newFlagData= [];

function decodeFlag(flag) {
    if (flag.length != flagData.length) {
        return -0x1;
    }

    for (let i =0; i < flagData.length; i+=1){
        if (i%3==0){
            newFlagChar=flagData[i] ^ 0x41;
            newFlagData.push(newFlagChar);
        } else if (i%3==1) {
            newFlagChar=flagData[i] ^ 0x67;
            newFlagData.push(newFlagChar);
        } else if (i%3==2) {
            newFlagChar=flagData[i] ^ 0x22;
            newFlagData.push(newFlagChar);
        }
    }

    console.log(newFlagData);

    let fflag = String.fromCharCode(...newFlagData);

    console.log(fflag);
}
decodeFlag(flagData)
```

Flag: `byuctf{js_deobf_is_easy_with_tools}`

(I think I may have mildly overcomplicated this but that's just how the crumble cookies).

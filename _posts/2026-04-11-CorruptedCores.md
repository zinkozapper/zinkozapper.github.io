---
title: Corrupted Cores
description: BYU CTF 2026
author: Zinko
date: 2026-04-11
categories: [Forensics]
media_subpath: '/assets/img/posts/CorruptedCores'
---

## Corrupted Cores

This challenge was a part of a really cool series. There were 4 flags total hidden in this pcapng file. I'm on going to focus on the hardest one.

![GLaDOS_Network.pcapng](AllPackets.png)

The ICMP, NTP, and TCP packets were all used for other challenges in the series so I ignore them. 

In the challenge description there is a hint that says "Hint: the voices may not belong to a single identity."

Whenever I said identity I immediately thought about MAC addresses and started checking the ARP packets. No luck.

The other thing I thought of related to identity were the IP addresses. There are some strange public ones in this capture.

I knew the flag started with byuctf{ so my goal was to find that string somewhere.

I tried seeing if the public ip addresses decoded to ascii characters. Unfortunately 89 decodes to Y, and 77 is M. Our address ranges are just to high for this.

I kept drilling with the source ip addresses and noticed that they had a character output in wireshark.

![IP address characters](IpEncoded.png)

I throw those characters into cyberchef on a whim to see if they decode into anything or are just random gibrish.

To my absolute amazement, those characters 'Ynl1' when base 64 decoded turned into 'byu'! This was the beginning of the flag.

I then went through all the packets that had non private ip addresses and compiled their ip sources together.

Decoding the entire string gives us the flag.

Flag: byuctf{Th3_P4rt_Wt3r3_H3_K!lls_Y0u}

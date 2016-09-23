---
layout: page
title: Challenge 3 - ScreenApp
permalink: /challenges/screenapp
---

**Can you find anything wrong with my application?** I bought it on the *MobileStore* for a few dollars💰  and it allows me to **pair my smartphone with an airplane TV**. I can then control different things on the screen and get information about my account directly from my phone. It's pretty neat! If you've ever had to deal with these old tactil screens on a flight before... you know what I'm talking about.

![drawing of an airplane screen](/images/challenges/screenapp.jpg)

So whenever I find myself in an airplane with that kind of monitor in front of my seat, I can find the pairing page on the menu of that little screen to start the process. It will display 4 random numbers that I will have to type into the smartphone app. After that, these numbers are hashed with SHA-256 to produce a key `k`.

I am then asked to connect to the video display's own wifi hotspot. I know which wifi it is thanks to the SSID displayed on it!

An ephemeral Diffie-Hellman key exchange with a modulus of 768 bits is done between the app and the screen, then both ends use the shared secret created out of that key exchange XOR'ed with the previous key `k` as the session key. This session key is used to encrypt any data from the screen to the phone and from the phone to the screen using AES in ECB mode.

It looks secure, but I'm not too sure since I'm a noob :)

Thanks!

Bob

---

> This challenge is definitely not the easiest one. It is not a deal breaker though, and we are not expecting you to find all the cryptographic flaws. We just want to see how you would go and brainstorm about this kind of problem. What power could an attacker have? What could an attacker do? etc... 

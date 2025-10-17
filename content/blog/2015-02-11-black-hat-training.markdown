---
layout: "post"
title:  "CS Debuts Crypto Training at Black Hat"
date:   2015-02-11 13:56:07
categories: training 
excerpt: "Cryptography Services will be debuting our Crypto Training Course: <a href='https://www.blackhat.com/us-15/training/beyond-the-beast-deep-dives-into-crypto-vulnerabilities.html'>Beyond the Beast: Deep Dives into Crypto Vulnerabilities</a> at Black Hat Vegas this summer."
---

Cryptography Services will be debuting our Crypto Training Course: [Beyond the Beast: Deep Dives into Crypto Vulnerabilities](https://www.blackhat.com/us-15/training/beyond-the-beast-deep-dives-into-crypto-vulnerabilities.html) at Black Hat Vegas this summer. We're stoked to be able to offer this course publicly, not just for the opportunity to teach, but also to learn and hang out with folks who are willing to let us share our passion for crypto. If you've been interested in the topic and followed the high-profile bugs, but haven't really had the opportunity to deeply dive into the subject as a whole - this training is for you.  

We've really focused the training on drawing out the foundations of cryptographic vulnerabilities. It's these topics that occur over and over again in the bugs found publicly and privately, and when people have moved off the primitives everyone knows are vulnerable today - we'll still be using them to attack new constructions tomorrow.  We're going to cover how these  are evident in attacks in the past, how algorithms and protocols have evolved over time to address these concerns, and what they look like at the heart of the most popular bugs today. Pulling from the course description:

* Module One focuses on what the right and wrong questions are when you're talking about cryptography with people - why focusing on matching keylengths isn't going to find you something exploitable and what will. 

* Module Two focuses on randomness, unpredictability, uniqueness. It covers the requisite info on spotting Random vs SecureRandom, but quickly dives deeper and talks about why randomness, uniqueness, and unpredictability are so important for constructions like GCM and stream ciphers (as well as CBC and key generation). 

* Module Three focuses on integrity, and covers AEAD modes, how to use them safely and how to exploit them, disk encryption, encrypt-then-mac, and unauthenticated modes like ECB/CBC/CTR. 

* Module Four is about complicated protocols and systems deployed at scale, and how to trace through them, following how trust is granted, what its scope is, how it can be impersonated, and how the system falls apart when anything is slightly off. 

* Module Five is Math. There's just no getting around it - but it also leads to some of the most impressive attacks. We look at several standards, many provably secure, and show how the slightest missing sanity check allows for an often-devastating adaptive chosen ciphertext attack on RSA, DSA, ECC, and unauthenticated block cipher modes. 

* Module Six tackles side channels, going in depth on the two aspects of cryptographic oracles: how the oracle is exposed and how to take advantage of what it tells you. We cover timing, errors, and the CPU cache, starting off showing how to apply the attacks you've just learned, and then moving on to show how to extract key bits from hand-optimized algorithm implementations. 

As we're wrapping up, because there's just so much interesting crypto out there, we'll lay out what news sources we read to keep up on the latest happenings in the cryptographic community and do a whirlwind tour of some interesting topics like wide-block constructions and hash-based digital signatures. Finally, we'll leave you with what findings and techniques have impressed us - the ones we think people will be using in the next decade of high-profile cryptographic attacks. 

Be sure to [register early](https://www.blackhat.com/us-15/training/beyond-the-beast-deep-dives-into-crypto-vulnerabilities.html) to take advantage of Black Hat's discounts, and if you have questions about the course feel free to [email us](mailto:CryptographyServices@nccgroup.com)!

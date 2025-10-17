---
layout: "post"
title:  "Announcing an east coast offering of our Beyond the BEAST Crypto Training"
date:   2015-09-23 8:30:07
categories: cryptography training
excerpt: November 17th and 18th will be an offering of our Beyond the BEAST training in New York City, previously seen at Black Hat. Contact us right away to reserve your seat!
aliases:
 - /cryptography/training/2015/09/23/announcing-an-east-coast-training-offering.html
---

In August we premiered a new training course we developed as a back-to-back [sold-out offering at Black Hat in Las Vegas](https://www.blackhat.com/us-15/training/beyond-the-beast-deep-dives-into-crypto-vulnerabilities.html).  We're offering it again in November at [Black Hat Europe](https://www.blackhat.com/eu-15/training/beyond-the-beast-deep-dives-into-crypto-vulnerabilities.html) - and we're announcing that we're offering an open registration a week later - <strong>November 17th and 18th in New York City</strong>.

We spend our days researching and assessing cryptographic implementations and protocols. We kept seeing the same types of flaws being demonstrated again and again - sometimes verbatim but sometimes in a slightly new incarnation. We took all of those flaws, grouped them up a bit, and turned it into a training course that will help you design and implement secure cryptographic systems - or identify weaknesses in existing ones.

<blockquote>I think, the training was awesome. The exercises were helpful and you guys were around to help out with the dumbest of questions. I have been looking for cryptanalysis training for a while, and this was exactly what I wanted. - Attendee</blockquote>

We'll talk about what attacks in the past took advantage of them, how algorithms and protocols have evolved over time to address these concerns, and what they look like now where they're at the heart of the most popular bugs today. The other major areas we hit are cryptographic exploitation primitives such as chosen block boundaries, and more protocol-related topics, such as how to understand and trace authentication in complex protocols. 

* Module One focuses on what the right and wrong questions are when you're talking about cryptography with people - why focusing on matching keylengths isn't going to find you something exploitable and what will. 
* Module Two focuses on randomness, unpredictability, uniqueness. It covers the requisite info on spotting Random vs SecureRandom, but quickly dives deeper and talks about why randomness, uniqueness, and unpredictability are so important for constructions like GCM and stream ciphers (as well as CBC and key generation). 
* Module three focuses on integrity, and covers AEAD modes, how to use them safely and how to exploit them, disk encryption, encrypt-then-mac, and unauthenticated modes like ECB/CBC/CTR. 
* Module four is about complicated protocols and systems deployed at scale, and how to trace through them, following how trust is granted, what its scope is, how it can be impersonated, and how the system falls apart when anything is slightly off. 
* Module five is Math. There's just no getting around it - but it also leads to some of the most impressive attacks. We look at several standards, many provably secure, and show how a slightest missing sanity check allows for an often-devastating adaptive chosen ciphertext attack on RSA, DSA, ECC, and unauthenticated block cipher modes. 
* Module six tackles side channels, going in depth on the two aspects of cryptographic oracles: how the oracle is exposed and how to take advantage of what it tells you. We cover timing, error, and the CPU cache, starting off showing how to apply the attacks you've just learned, and then moving on to show how to extract key bits from hand-optimized algorithm implementations. 
* Module seven covers a host of flaws that don't fit neatly into any of the previous buckets. These range from complex protocol flow limitations, to very simple and compact mistakes that keep popping up. 
* Module eight talks about the cryptographic community - we lay out what news sources we read to keep up on the latest happenings  and do a whirlwind tour of some interesting topics coming up in the future - things like wide-block constructions and hash-based digital signatures. 

<blockquote>I found great value in the presentation and knowledge transferred. The course is spot on. - Attendee</blockquote>

Course requirements are minimal.  We've targeted it at students who have a strong interest in cryptography and some measure of cryptographic understanding (such as the difference between symmetric and asymmetric crypto). The ideal student has investigated one or more recent cryptographic attacks deeply enough to be able to explain it, but has not sat down and read PKCS or NIST standards describing algorithm implementation. No explicit understanding of statistics or high-level math is required, as the focus is on the underlying causes of the vulnerabilities. We cover a wide breadth of topics in the course, and provide printed slide decks.

Some experience programming is recommended - please bring a laptop prepared with an environment you're comfortable with, and with Python 2.7 installed. You don't have to program in Python, but the exercises are in Python and it does make it easier. 

Space is limited of course - we won't exceed our capability to work with people individually.  We've priced the course competitively at <strong>$2500/person before October 31st</strong>, and $3000 after. Group discounts are available. To reserve your seat contact us at <a href="mailto:CryptographyServices@nccgroup.com">CryptographyServices@nccgroup.com</a>.

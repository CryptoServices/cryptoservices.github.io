---
layout: "post"
title:  "Beyond the BEAST Returns to Black Hat USA"
date:   2016-02-12 12:30:07
categories: cryptography training
excerpt: 
---

Last year we premiered a new training course we developed as a back-to-back sold-out offering at Black Hat in Las Vegas. This year [we're offering it again at Black Hat](https://www.blackhat.com/us-16/training/beyond-the-beast-a-broad-survey-of-crypto-vulnerabilities.html). Since debuting last year, we've offered the course more than a half-dozen times, and gotten outstanding feedback that has helped us improve it each successive offering. We've updated the course significantly since last year - improving the layout, content, and exercises. We've taken a few existing topics and added a few more to create the new Subverting Signatures module, retooled our coverage of Randomness to include more analysis on PRNGs in the abstract and more exploiting specific broken PRNGs, and included more information about ECC - both background and attacks.

The Cryptography Services practice at NCC Group spends our days researching and assessing cryptographic implementations and protocols. We kept seeing the same types of flaws being demonstrated again and again - sometimes verbatim but sometimes in a slightly new incarnation. We took all of those flaws, grouped them up a bit, and turned it into a training course that will help you design and implement secure cryptographic systems - or identify weaknesses in existing ones.

<blockquote>I think, the training was awesome. The exercises were helpful and you guys were around to help out with the dumbest of questions. I have been looking for cryptanalysis training for a while, and this was exactly what I wanted. - Attendee</blockquote>

We'll talk about what attacks in the past took advantage of them, how algorithms and protocols have evolved over time to address these concerns, and what they look like now where they're at the heart of the most popular bugs today. The other major areas we hit are cryptographic exploitation primitives such as chosen block boundaries, and more protocol-related topics, such as how to understand and trace authentication in complex protocols. 

* Module One focuses on what the right and wrong questions are when you're talking about cryptography with people - why focusing on matching keylengths isn't going to find you something exploitable and what will.

* Module Two focuses on randomness, unpredictability, uniqueness. It covers the requisite info on spotting Random vs SecureRandom, but quickly dives deeper and talks about why randomness, uniqueness, and unpredictability are so important for constructions like GCM and stream ciphers (as well as CBC and key generation).

* Module three focuses on integrity, and covers unauthenticated modes like ECB/CBC/CTR, AEAD modes, encrypt-then-mac, and how to take advantage of this topic in spaces like disk encryption.

* Module four is about complicated protocols and systems deployed at scale, and how to trace through them, following how trust is granted, what its scope is, how it can be impersonated, and how the system falls apart when anything is slightly off.

* Module five is all about signatures. We talk about signature reuse, reinterpretation, and more - including one of our favorite flaws: the SSL 3 omission that persisted and was exploited in new ways for a full 19 years before finally being fixed.

* Module six is Math. There's just no getting around it - but it also leads to some of the most impressive attacks. We look at several standards, many provably secure, and show how a slightest missing sanity check allows for an often-devastating adaptive chosen ciphertext attack on RSA, DSA, ECC, and unauthenticated block cipher modes.

* Module seven tackles side channels, going in depth on the two aspects of cryptographic oracles: how the oracle is exposed and how to take advantage of what it tells you. We cover timing, error, and the CPU cache, starting off showing how to apply the attacks you've just learned, and then moving on to show how to extract key bits from hand-optimized algorithm implementations.


We wrap up by talking about the cryptographic community. We lay out what news sources we read to keep up on the latest happenings and do a whirlwind tour of some interesting topics coming up in the future - things like wide-block constructions and hash-based digital signatures. 

<blockquote>I found great value in the presentation and knowledge transferred. The course is spot on. - Attendee</blockquote>

Course requirements are minimal.  We've targeted it at students who have a strong interest in cryptography and some measure of cryptographic understanding (such as the difference between symmetric and asymmetric crypto). The ideal student has investigated one or more recent cryptographic attacks deeply enough to be able to explain it, but has not sat down and read PKCS or NIST standards describing algorithm implementation. No explicit understanding of statistics or high-level math is required, as the focus is on the underlying causes of the vulnerabilities. We cover a wide breadth of topics in the course, and provide printed slide decks.


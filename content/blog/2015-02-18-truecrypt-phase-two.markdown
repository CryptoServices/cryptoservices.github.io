---
layout: "post"
title:  "Truecrypt Phase Two Audit Announced"
date:   2015-02-18 16:56:07
categories: fde 
excerpt: "Cryptography Services will be conducting the second phase of the <a href='http://istruecryptauditedyet.com/'>Truecrypt Audit</a>, focusing on the cryptography of the project as it is used in the most common configurations. This follows up iSEC's Phase One Audit, and will complement the work done there"
aliases:
 - /fde/2015/02/18/truecrypt-phase-two.html
---

iSEC Partners completed the [first phase](https://isecpartners.github.io/news/2014/04/14/iSEC-Completes-Truecrypt-Audit.html) of the Truecrypt audit almost a year ago, focusing on the Windows kernel code, bootloader, filesystem driver, and surrounding areas. But the cryptography was left to a second phase, to be looked at in a specialized engagement. 

[That second phase is here](http://blog.cryptographyengineering.com/2015/02/another-update-on-truecrypt-audit.html), and NCC Group's Cryptography Services team will be doing it.  The primary threat models CS will be focusing on are a Truecrypt-encrypted laptop or container 'at rest' - perhaps the laptop was stolen or the container obtained from a cloud provider. We want to be sure that the cryptography used to protect these encrypted volumes is solid and free of any errors that could allow recovery of the data.  Because of the nature of the work, we'll be focusing on the mode widely used and standardized components: XTS mode used with AES, as well as the Double and Triple Compositions.  It's likely we'll be getting eyes on several other crypto-related portions of the codebase, but these will be the primary focus.

The Truecrypt audit has been one of the biggest crowd-sourced security endeavors on the Internet, so we know that there are high expectations for this work.  Just as iSEC performed a thorough review and did an excellent job on their portion, CS is excited to tackle our portion and perform the same quality of service.  The timeline for performing the audit is not yet set in stone, but we expect to complete it in the early to mid Spring.  

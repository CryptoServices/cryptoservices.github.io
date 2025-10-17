---
layout: "post"
title:  "Factoring RSA Keys With TLS Perfect Forward Secrecy"
date:   2015-09-10 14:30:07
categories: cryptography
author: "David Wong"
excerpt: Florian Weimer from the Red Hat Product Security team has just released a technical report entitled "Factoring RSA Keys With TLS Perfect Forward Secrecy
aliases:
 - /cryptography/2015/09/10/factoring-rsa-keys-with-tls-perfect-forward-secrecy.html
---


**Florian Weimer** from the Red Hat Product Security team has just released a technical report entitled "[Factoring RSA Keys With TLS Perfect Forward Secrecy](https://people.redhat.com/~fweimer/rsa-crt-leaks.pdf)"

## Wait what happened?

A team of researchers ran an attack for nine months, and from 4.8 billion of ephemeral handshakes with different TLS servers **they recovered hundreds of private keys**.

The theory of the attack is actually pretty old, [Lenstra's famous memo on the CRT optimization](http://infoscience.epfl.ch/record/164524/files/nscan20.PDF) was written in 1996. Basicaly, when using the CRT optimization to compute a RSA signature, if a fault happens, a simple computation will allow the private key to be recovered. This kind of attacks are usually thought of and fought in the realm of *smartcards* and other *embedded devices*, where faults can be induced with lasers and other magical weapons.

The research is novel in a way because they made use of **Accidental Fault Attack**, which is one of the rare kind of remote side-channel attacks.

This is interesting, the oldest passive form of *Accidental Fault Attack* I can think of is **Bit Squatting** that might go back to 2011 at that [defcon talk](https://www.youtube.com/watch?v=aT7mnSstKGs).

## But first, what is vulnerable?

Any library that uses the CRT optimization for RSA might be vulnerable. A cheap countermeasure would be to verify the signature after computing it, which is what most libraries do. The paper has a nice list of who is doing that.

<table>
<thead>
<tr><td>Implementation</td><td>Verification</td></tr>
</thead>
<tbody>
<tr><td>cryptlib 3.4.2</td><td>disabled by default</td></tr>
<tr><td>GnuPG 1.4.1.8</td><td>yes</td></tr>
<tr><td>GNUTLS</td><td>see libgcrypt and Nettle</td></tr>
<tr><td>Go 1.4.1</td><td>no</td></tr>
<tr><td>libgcrypt 1.6.2</td><td>no</td></tr>
<tr><td>Nettle 3.0.0</td><td>no</td></tr>
<tr><td>NSS</td><td>yes</td></tr>
<tr><td>ocaml-nocrypto 0.5.1</td><td>no</td></tr>
<tr><td>OpenJDK 8</td><td>yes</td></tr>
<tr><td>OpenSSL 1.0.1l</td><td>yes</td></tr>
<tr><td>OpenSwan 2.6.44</td><td>no</td></tr>
<tr><td>PolarSSL 1.3.9</td><td>no</td></tr>
</tbody>
</table>

But is it about what library you are using? Your server still has to be defective to produce a fault. The paper also have a nice table displaying what vendors, in their experiments, where most prone to have this vulnerability.
<table>
<thead>
<tr><td>Vendor</td><td>Keys</td><td>PKI</td><td>Rate</td></tr>
</thead>
<tbody>
<tr><td>Citrix</td><td>2</td><td>yes</td><td>medium</td></tr>
<tr><td>Hillstone Networks</td><td>237</td><td>no</td><td>low</td></tr>
<tr><td>Alteon/Nortel</td><td>2</td><td>no</td><td>high</td></tr>
<tr><td>Viprinet</td><td>1</td><td>no</td><td>always</td></tr>
<tr><td>QNO</td><td>3</td><td>no</td><td>medium</td></tr>
<tr><td>ZyXEL</td><td>26</td><td>no</td><td>low</td></tr>
<tr><td>BEJY</td><td>1</td><td>yes</td><td>low</td></tr>
<tr><td>Fortinet</td><td>2</td><td>no</td><td>very low</td></tr>
</tbody>
</table>

If you're using one of these you might want to check with your vendor if a firmware update or other solutions were talked about after the discovery of this attack. You might also want to revoke your keys.

Since the tests were done on a broad scale and not on particular machines, it is obvious that **more are vulnerable to this attack**. Also only instances connected to internet that offered TLS on port 443 were tested. The vulnerability could potentially exist in any stack using this CRT optimization with RSA.

The first thing you should do is assess where in your stack the RSA algorithm is used to sign. Does it use CRT? If so, does it verify the signature? 

## What can cause your server to produce such erroneous signatures

They list 5 reasons in the paper:

* old or vulnerable libraries that have broken operations on integer. For example [CVE-2014-3570](https://web.nvd.nist.gov/view/vuln/detail?vulnId=CVE-2014-3570) was an issue that caused the square operations of OpenSSL to not work properly for some inputs

* race conditions, when applications are multithreaded

* arithmetic unit of the CPU [is broken by design](http://iacr.org/archive/crypto2008/51570222/51570222.pdf) or by fatigue

* [corruption of the private key](https://eprint.iacr.org/2002/076.pdf)

* errors in the CPU cache, other caches or the main memory

Note that at the end of the paper, they investigate if a special hardware might be the cause and end up with the conclusion that several devices leaking the private keys were using [Cavium](http://www.cavium.com/) hardware, and in some cases their "custom" version of OpenSSL.

## I'm curious. How does that work?

### RSA-CRT

Remember, RSA signature is basically \\(y = x^d \pmod{n}\\) with \\(x\\) the message, \\(d\\) the private key and \\(n\\) the public modulus. Also you might want to use a padding system but we won't cover that here. And then you can verify a signature by doing \\(y^e \pmod{n}\\) and verify if it is equal to \\(x\\) (with \\(e\\) the public exponent).

CRT is short for Chinese Remainder Theorem (I should have said that earlier). It's an optimization that allows to compute the signatures in \\(\mathbb{Z}\_p\\) and \\(\mathbb{Z}\_q\\) and then combine it into \\(\mathbb{Z}\_n\\) (remember \\(n = pq\\)). It's way faster like that.

So basically what you do is:



\\[ \begin{cases} y\_p = x^d \pmod{p} \\\\ y\_q = x^d \pmod{q} \end{cases} \\]

and then combine these two values to get the signature:

$$ y = y\_p q (q^{-1} \pmod{p}) + y\_q p (p^{-1} \pmod{q}) \pmod{n} $$

And you can verify yourself, this value will be equals to \\(y\_p \pmod{p}\\) and \\(y\_q \pmod{q}\\).

### The vulnerability

Let's say that an error occurs in only one of these two elements. For example, \\(y\_p\\) is not correctly computed. We'll call it \\(\widetilde{y\_p}\\) instead. It is then is combined with a correct \\(y\_q\\) to produce a wrong signature that we'll call \\(\widetilde{y}\\) .

So you should have:

\\[
\begin{cases}
\widetilde{y} = \widetilde{y}\_p \pmod{p}\\\\
\widetilde{y} = y\_q \pmod{q}
\end{cases}
\\]

Let's notice that if we raise that to the power \\(e\\) and remove \\(x\\) from it we get:

$$
\begin{cases}
\widetilde{y}^e - x = \widetilde{y}^e\_p - x = a \pmod{p}\\\\
\widetilde{y}^e - x = y\_q^e - x = 0 \pmod{q}
\end{cases}
$$

This is it. We now know that \\(q \mid \widetilde{y}^e - x\\) while it also divides \\(n\\). Whereas \\(p\\) doesn't divide \\(\widetilde{y}^e - x\\) anymore. We just have to compute the Greatest Common Divisor of \\(n\\) and \\(\widetilde{y}^e - x\\) to recover \\(q\\).

### The attack

The attack could potentially work on anything that display a RSA signature. But the paper focuses itself on TLS.

A normal TLS handshake is a two round trip protocol that looks like this:

![normal_tls_handshake](http://i.imgur.com/VcYhMv1.png)

The client (the first person who speaks) first sends a *helloClient* packet. A thing filled with bytes saying things like "this is a handshake", "this is TLS version 1.0", "I can use this algorithm for the handshake", "I can use this algorithm for encrypting our communications", etc...

Here's what it looks like in Wireshark:

![client hello](http://i.imgur.com/EYYKmXm.png)

The server (the second person who speaks) replies with 3 messages: a similar *ServerHello*, a message with his *certificate* (and that's how we authenticate the server) and a *ServerHelloDone* message only consisting of a few bytes saying "I'm done here!".

A second round trip is then done where the client encrypts a key with the server's public key and they later use it to compute the TLS shared key. We won't cover them.

Another kind of handshake can be performed if both the client and the server accepts ephemeral key exchange algorithms (Diffie-Hellman or Elliptic Curve Diffie-Hellman). This is to provide *Perfect Forward Secrecy*: if the conversations are recorded by a third party, and the private key of the server is later recovered, nothing will be compromised. Instead of using the server's public key to compute the shared key, the server will generate a *ephemeral* public key and use it to perform an *ephemeral handshake*. This key is usually used just for this session or occasionally for a limited number of sessions.

![ephemeral_handshake](http://i.imgur.com/gEkuTiq.png)

When this occurs, an extra packet called **ServerKeyExchange** is sent. It contains the server's ephemeral public key.

(Interestingly the signature is not computed over the algorithm used for the ephemeral key exchange, that led to a long series of attacks which recently ended with [FREAK](https://freakattack.com/) and [Logjam](https://weakdh.org/).)

Checking if the signature is correctly performed is how they checked for this potential vulnerability.

## I'm a researcher, what's in it for me?

Well what are you waiting for? Go read the paper!

But here are a list of what I found interesting:

* instead of DDoSing one target, they broadcasted their attack.

> We implemented a crawler which performs TLS handshakes and looks for miscomputed RSA signatures. We ran this crawler for several months.
The intention behind this configuration is to spread the load as widely as possible. We did not want to target particular servers because that might have been viewed as a denial-of-service attack by individual server operators. We assumed that if a vulnerable implementation is out in the wild and it is somewhat widespread, this experimental setup still ensures the collection of a fair number of handshake samples to show its existence.
We believe this approach—probing many installations across the Internet, as opposed to stressing a few in a lab—is a novel way to discover side-channel vulnerabilities which has not been attempted before.

* they used public information to choose what to target, like [scans.io](https://scans.io/), [tlslandscape](https://securityblog.redhat.com/2014/09/10/tls-landscape/) and [certificate-transparency](http://www.certificate-transparency.org/).

* Some TLS servers need a valid Server Name Indication to complete a handshake, so connecting on port 443 of random IPs should not be very efficient. But they found that it was actually not a problem and most keys found like that were from weird certificates that wouldn't even be trusted by your browser.

* To avoid too many DNS resolutions they bypassed the TTL values and cached everything (they used [PowerDNS](https://www.powerdns.com/) for that.)

* They guess what devices were used to perform the TLS handshakes from what was written in the x509 certificates in the *subject distinguished name* field or *Common Name* field.

* They used `SSL_set_msg_callback()` ([see doc](https://www.openssl.org/docs/manmaster/ssl/SSL_CTX_set_msg_callback.html)) to avoid modifying OpenSSL.

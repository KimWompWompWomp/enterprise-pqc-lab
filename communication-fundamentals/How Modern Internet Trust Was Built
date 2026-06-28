# How Modern Internet Trust Was Built

## Purpose

The purpose of this research note is to explain how modern internet security evolved from early cryptography into the trust systems we use today, especially **TLS**, **certificates**, **certificate authorities**, and **public key infrastructure (PKI)**.

TLS did not appear out of nowhere. It is the result of decades of work around one core problem:

> How can two parties communicate securely over a network that neither side fully controls?

To understand TLS, we first need to understand the history of cryptography, the key distribution problem, public key cryptography, digital signatures, certificates, and eventually PKI.

---

## 1. What TLS Does at a High Level

**Transport Layer Security (TLS)** is the protocol that protects much of the communication we use on the internet today. It is the security layer behind **HTTPS** and is also used in many other protocols and systems.

At a high level, TLS helps provide:

### Confidentiality

TLS prevents unauthorized parties from reading the contents of communication while data is in transit.

### Integrity

TLS helps ensure that data is not modified in transit without detection.

### Authentication

TLS allows a client, such as a browser, to verify that it is communicating with the intended server. In some cases, TLS can also authenticate the client to the server through **mutual TLS (mTLS)**.

TLS does **not** directly guarantee availability. Availability depends on whether systems, networks, servers, and supporting infrastructure remain reachable and operational. TLS can protect communication, but it cannot guarantee that a website or service will stay online.

---

## 2. The Historical Problem: Secure Communication Required Shared Secrets

For most of cryptographic history, encryption was **symmetric**. That means the same secret key was used to encrypt and decrypt a message.

A simple example:

```text
Alice and Bob both know secret key K.

Alice uses K to encrypt the message.
Bob uses K to decrypt the message.
```

This works well if Alice and Bob can safely exchange the key beforehand. However, it creates a major problem at scale.

If every pair of users needs a unique shared secret, the number of keys grows quickly:

```text
Number of pairwise keys = n(n - 1) / 2
```

For example:

| Number of People | Pairwise Shared Keys Needed |
| ---------------: | --------------------------: |
|               10 |                          45 |
|              100 |                       4,950 |
|            1,000 |                     499,500 |
|        1,000,000 |          Nearly 500 billion |

This is the **key distribution problem**.

The issue is circular:

> To communicate securely, two parties first need a secure way to exchange the secret key.

That may be possible in small, controlled environments, but it becomes extremely difficult across large networks, governments, enterprises, banks, military systems, vendors, web servers, and users who have never met.

This key distribution problem is one of the reasons public key cryptography became so important.

---

## 3. Early Cryptography Before Computers

The need to hide meaning is much older than computers. Early forms of cryptography were used in religion, diplomacy, military command, trade secrecy, and political communication.

Some of the earliest examples are often traced to ancient Egypt, where scribes used non-standard hieroglyphs in tomb inscriptions. These were not encryption systems in the modern mathematical sense, but they show an early human instinct to restrict meaning to certain readers.

Over time, cryptography evolved from writing tricks into more structured systems, such as:

* Substitution ciphers
* Transposition ciphers
* Codebooks
* Mechanical cryptography
* Mathematical cryptography
* Computer-based cryptographic protocols

The important point is that the underlying need stayed the same:

> Protect the meaning of a message from people who are not supposed to understand it.

Modern TLS solves a much more complex version of this same problem.

---

## 4. The 1970s: Public Key Cryptography Changes the Game

In the 1970s, cryptography went through one of its most important transformations.

Before public key cryptography, secure communication mostly depended on shared secret keys. The challenge was getting those keys to the right parties without exposing them.

Public key cryptography introduced a new idea:

> A user can have two mathematically related keys: one public and one private.

The **public key** can be shared openly. The **private key** must remain secret.

This changed the mental model of cryptography. Before this, the assumption was that cryptographic keys had to be hidden. Public key cryptography showed that some key material could be public without destroying security, as long as the private key remained protected and the underlying math was hard to reverse.

---

## 5. Diffie-Hellman and the Key Agreement Breakthrough

In 1976, **Whitfield Diffie** and **Martin Hellman** published *New Directions in Cryptography*. This paper introduced foundational ideas behind public key cryptography and showed how two parties could establish a shared secret over an insecure channel.

The most important question was:

> How can two people who have never met create a shared secret while an attacker may be watching the communication?

**Diffie-Hellman key exchange** answers this by allowing both parties to exchange public values and combine those public values with their own private values. Both parties end up with the same shared secret, but an attacker observing the exchange cannot efficiently calculate that secret.

A simplified flow looks like this:

```text
Alice creates a private value.
Bob creates a private value.

Alice sends Bob a public value derived from her private value.
Bob sends Alice a public value derived from his private value.

Alice combines Bob’s public value with her private value.
Bob combines Alice’s public value with his private value.

Both arrive at the same shared secret.
```

The key idea is that Diffie-Hellman is not primarily “encrypting a message with a public key.” It is a **key agreement method**. It allows two parties to create a shared secret that can then be used with symmetric encryption.

This matters because symmetric encryption is still used for the bulk encryption of data. Public key cryptography helps solve the setup and trust problems. Symmetric cryptography is then used because it is efficient for encrypting actual traffic.

---

## 6. Ralph Merkle’s Contribution

**Ralph Merkle** also played a major role in the early development of public key ideas. His work on **Merkle’s puzzles** showed a method for two parties to establish a secret over an insecure channel using computational asymmetry.

Merkle’s idea was not the same as modern Diffie-Hellman, but it was historically important because it helped show that secure communication over insecure channels was possible without a pre-shared secret.

This period should be understood as a cluster of related breakthroughs. Merkle, Diffie, Hellman, and later Rivest, Shamir, and Adleman all contributed to the emergence of modern public key cryptography.

---

## 7. RSA and Practical Public Key Cryptography

In 1978, **Ron Rivest**, **Adi Shamir**, and **Leonard Adleman** published the RSA cryptosystem. RSA became one of the first practical public key cryptosystems and supported both public key encryption and digital signatures.

RSA helped make the public key concept usable in real systems.

A simplified RSA-style mental model is:

```text
Public key: can be shared openly
Private key: must remain secret
```

For encryption:

```text
Sender encrypts using recipient’s public key.
Recipient decrypts using recipient’s private key.
```

For digital signatures:

```text
Sender signs using sender’s private key.
Receiver verifies using sender’s public key.
```

This distinction is important. Public key encryption and digital signatures are related, but they solve different problems.

**Encryption** is about confidentiality.

**Digital signatures** are about authenticity, integrity, and non-repudiation.

---

## 8. Digital Signatures: Proving Who Signed Something

Digital signatures are one of the most important concepts that eventually led to certificates and PKI.

For confidentiality, the recipient’s public key can be used so that only the recipient’s private key can decrypt the message.

For signatures, the sender uses their own private key to create a signature. Anyone with the sender’s public key can verify that signature.

This provides several security properties:

### Authenticity

The verifier has evidence that the message was signed by the holder of the private key.

### Integrity

If the message changes after signing, the signature verification fails.

### Non-Repudiation

The signer has difficulty denying that they signed the message, assuming the private key was not compromised and the signing process was properly controlled.

Digital signatures became crucial because certificates rely on them.

A **certificate authority (CA)** signs a certificate with its private key. Other systems verify that certificate using the CA’s public key.

This is the foundation of certificate-based trust.

---

## 9. The Remaining Problem: Public Keys Do Not Prove Identity by Themselves

Public key cryptography solved a major technical problem, but it created another one:

> How do I know that this public key actually belongs to the person, server, company, or system I think it belongs to?

A public key by itself is just data. It does not automatically prove identity.

For example, suppose Alice wants to talk to Bob. An attacker, Mallory, sits between them:

```text
Alice ↔ Mallory ↔ Bob
```

Mallory can perform one key exchange with Alice and another key exchange with Bob.

Alice thinks she is communicating securely with Bob. Bob thinks he is communicating securely with Alice. In reality, Mallory can decrypt, inspect, modify, and re-encrypt the traffic between them.

This is the classic **man-in-the-middle problem**.

Diffie-Hellman allows two parties to establish a shared secret, but unauthenticated Diffie-Hellman does not prove who is on the other side of the exchange.

This is where certificates and PKI become necessary.

---

## 10. Certificates: Binding Identity to a Public Key

A certificate binds an identity to a public key.

A simplified certificate may include:

```text
Subject: example.com
Subject public key: 03:AB:91:...
Issuer: DigiCert
Valid from: date
Valid until: date
Allowed uses: server authentication
Signature: signed by the issuer
```

The certificate authority’s signature is what allows other systems to verify that the certificate has not been altered and that the CA vouched for the binding between the identity and the public key.

In simple terms:

> A certificate says, “This public key belongs to this identity, and this trusted authority has signed that claim.”

This is the bridge between public key cryptography and practical internet trust.

---

## 11. X.509 and the Structure of Modern Certificates

**X.509** became the dominant certificate format used in modern PKI. X.509 certificates are used in TLS, enterprise PKI, smart cards, code signing, S/MIME email, device identity, and many other systems.

An X.509 certificate includes structured information such as:

* Subject
* Issuer
* Serial number
* Validity period
* Subject public key
* Key usage
* Extended key usage
* Subject Alternative Name
* Certificate policies
* Revocation information
* Issuer signature

TLS uses X.509 certificates to help a client verify the identity of a server.

In HTTPS, this is how a browser determines whether the server certificate presented by a website is valid for the domain being visited.

---

## 12. Public Key Infrastructure: The Trust System Around Certificates

**Public Key Infrastructure (PKI)** is the broader system that manages certificates, keys, trust chains, policies, and revocation.

PKI typically includes:

* Root certificate authorities
* Intermediate certificate authorities
* End-entity certificates
* Certificate policies
* Certificate issuance processes
* Certificate revocation
* Certificate lifecycle management
* Hardware security modules
* Trust stores
* Audit requirements

A typical public TLS certificate chain looks like this:

```text
Root CA
  ↓ signs
Intermediate CA
  ↓ signs
Leaf certificate for example.com
```

Browsers and operating systems trust certain root CAs by default. If a website presents a certificate chain that leads back to a trusted root, and the certificate is valid for the domain, the browser can establish trust in the server’s public key.

This does not mean the website is safe in every possible sense. It means the certificate validation process succeeded and the browser has authenticated the server identity according to PKI rules.

---

## 13. SDNS, OSI, and Early Network Security Standardization

While public key cryptography and certificates were developing, governments and standards bodies were also working on secure networking frameworks.

The **Secure Data Network System (SDNS)** was an NSA-led project intended to define security services for networked systems. NISTIR 90-4250 documented several SDNS security protocol specifications.

The SDNS work included security protocols at different layers of the OSI model, including:

* **SP3** for network-layer security
* **SP4** for transport-layer security
* **Message Security Protocol (MSP)** for message protection
* **Key Management Protocol (KMP)** for key management

This matters historically because it shows that many of today’s concerns were already being addressed in early secure networking work:

* Confidentiality
* Integrity
* Authentication
* Key management
* Interoperability
* Layered network security

The OSI model also influenced how people thought about networking at the time. Government and industry efforts pushed for standard protocol profiles so that different vendors and systems could interoperate.

Even though the modern internet did not fully adopt the OSI protocol stack in the way some expected, the layered security thinking from that era helped shape later approaches to network security.

---

## 14. From SSL to TLS

In the 1990s, the growth of the World Wide Web created a need for secure browser-to-server communication.

Netscape developed **SSL**, or **Secure Sockets Layer**, as an early protocol for securing web traffic. SSL 3.0 became the major predecessor to TLS.

**TLS 1.0** was standardized by the IETF in 1999. TLS built on the ideas behind SSL but became the open standard for securing internet communication.

At a high level, TLS combines several ideas:

### Certificates for Authentication

The server presents a certificate so the client can verify the server’s identity.

### Public Key Cryptography for Key Establishment and Authentication

TLS uses asymmetric cryptography during the handshake.

### Symmetric Encryption for Bulk Data Protection

After the handshake, both sides use symmetric session keys to encrypt traffic efficiently.

### Integrity Protection

TLS helps detect tampering or modification of data in transit.

This combination is what makes TLS practical. Public key cryptography solves the trust and key establishment problem. Symmetric cryptography protects the actual traffic efficiently.

---

## 15. How TLS Works Today at a Simplified Level

When a browser connects to an HTTPS website, a simplified TLS flow looks like this:

```text
1. Browser connects to website.
2. Website sends its certificate.
3. Browser checks whether the certificate is valid.
4. Browser verifies that the certificate matches the domain.
5. Browser validates the certificate chain to a trusted root CA.
6. Browser and server perform a key exchange.
7. Both sides derive shared symmetric session keys.
8. Application data is encrypted and protected using those session keys.
```

Modern TLS, especially TLS 1.3, is designed to be faster, cleaner, and more secure than older SSL/TLS versions. It removes many outdated algorithms and simplifies the handshake process.

The important point is that TLS is not just one algorithm. It is a protocol that combines identity, key exchange, encryption, integrity protection, and certificate validation.

---

## 16. Why This History Matters for Post-Quantum Cryptography

This history matters because much of modern PKI still depends on public key algorithms such as RSA and elliptic curve cryptography.

A cryptographically relevant quantum computer would threaten many of the asymmetric algorithms used for:

* Key exchange
* Digital signatures
* Certificates
* Code signing
* Software updates
* Device identity
* Enterprise authentication
* TLS handshakes

This is why post-quantum cryptography is not just an algorithm replacement project. It is a PKI migration problem.

Organizations need to understand:

* Where certificates are used
* Which algorithms are used in those certificates
* Which systems depend on RSA, ECC, ECDH, or ECDSA
* Which systems can support new algorithms
* How quickly certificates and keys can be rotated
* Whether vendors support post-quantum or hybrid approaches
* Whether internal PKI can adapt to new standards

The same historical issue keeps returning:

> Secure communication depends not only on strong cryptographic algorithms, but also on key management, identity binding, interoperability, and operational trust.

That is why the evolution from early cryptography to TLS is so important. It shows that cryptography is never just math. It is infrastructure.

---

## Summary

Modern TLS and PKI are the result of several historical developments:

1. Symmetric cryptography created the key distribution problem.
2. Public key cryptography introduced a way to communicate without pre-sharing secrets.
3. Diffie-Hellman showed how two parties could establish a shared secret over an insecure channel.
4. RSA made public key encryption and digital signatures practical.
5. Digital signatures made it possible to prove authenticity and integrity.
6. Certificates bound public keys to identities.
7. X.509 standardized certificate structures.
8. PKI created the trust infrastructure around certificates.
9. SSL and TLS brought these ideas into everyday internet communication.
10. Post-quantum cryptography is now forcing the next major evolution of this trust system.

The core story is simple:

> Public key cryptography solved the key distribution problem, but PKI solved the identity problem.

TLS depends on both.

---

## Key Technical Corrections

### TLS Does Not Guarantee Availability

TLS primarily provides confidentiality, integrity, and authentication. It does not guarantee that a system will remain online or reachable.

### Diffie-Hellman Is Key Agreement, Not Message Encryption

Diffie-Hellman allows two parties to establish a shared secret over an insecure channel. That shared secret can then be used for symmetric encryption.

### Digital Signatures Prove Control of a Private Key

A valid digital signature proves that the signer had access to the corresponding private key. It does not automatically prove human intent if the private key was stolen or misused.

### Certificates Bind Identity to Public Keys

A public key alone does not prove identity. Certificates solve this by binding an identity, such as a domain name, to a public key.

### PKI Is the Trust System Around Certificates

PKI includes the certificate authorities, policies, trust stores, revocation systems, lifecycle processes, and governance mechanisms that make certificate-based trust work.

---

## References

* [New Directions in Cryptography - Diffie and Hellman](https://ee.stanford.edu/~hellman/publications/24.pdf)
* [A Method for Obtaining Digital Signatures and Public-Key Cryptosystems - RSA](https://people.csail.mit.edu/rivest/Rsapaper.pdf)
* [RFC 2246 - TLS 1.0](https://www.ietf.org/rfc/rfc2246.txt)
* [RFC 8446 - TLS 1.3](https://datatracker.ietf.org/doc/html/rfc8446)
* [RFC 5280 - Internet X.509 Public Key Infrastructure Certificate and CRL Profile](https://datatracker.ietf.org/doc/html/rfc5280)
* [NISTIR 90-4250 - Secure Data Network System Security Protocols](https://nvlpubs.nist.gov/nistpubs/Legacy/IR/nistir90-4250.pdf)
* [NIST Post-Quantum Cryptography Project](https://csrc.nist.gov/projects/post-quantum-cryptography)

# Cryptography History

## Goal
To clearly explain the origination of TLS and how TLS works today. 

## What does TLS Do (High Level) 
TLS protects the communications that we use today from attackers that might steal information when the data is in transit. It ensures that we achieve all three elements of the CIA Triad: Confidentialiy, Integrity, and Availability. TLS has become the standard when communicating across the internet, and ensures that we do that effectively and securely. 

## History 
Background: Much of this happened before I was born. A lot of the technologies that we use today spawned into our lives without much background on the story behind it. We were given technology at a young age and gained profiency that transltates to the devices that we used today. But in terms of understanding how we got here in the first place, that has always been a gray area with many of the people that I work with and myself. And at the time of this writing, it seems that this topic, although very uninteresting to most people, is not widely published. 

### Brief History Lesson

1. Before the 1970s: encryption required shared secrets

For most of cryptographic history, encryption was symmetric: both sides needed the same secret key. That works if two parties can safely meet beforehand, but it breaks down at scale. 

The earliest signs of cryptography go back thousands of years, long before computers, PKI, TLS, or modern encryption. The basic human need was the same: hide meaning from anyone who was not supposed to understand the message.

Cryptography started as clever writing tricks, then became a tool for religion, trade secrecy, military command, diplomacy, and eventually mathematics.

The earliest known examples are usually traced to ancient Egypt, around 1900 BCE, where scribes used non-standard hieroglyphs in tomb inscriptions. This was not “encryption” in the modern military or mathematical sense, but it shows an early instinct to obscure meaning and make writing understandable only to certain people.

2. 1976: public-key cryptography changes the game

In 1976, Whitfield Diffie and Martin Hellman published “New Directions in Cryptography.” This introduced the public idea of asymmetric cryptography: a system where a person can have a public key and a private key, and the public key does not need to be kept secret.  

The 1976 Diffie-Hellman paper mattered because it attacked the oldest practical problem in cryptography:

How do two people who have never met create a shared secret over an insecure channel?

Before 1976, that sounded almost impossible.

Before public-key cryptography, most encryption was symmetric encryption.

That means the same secret key is used to encrypt and decrypt.

Example:

Alice and Bob both know secret key K.

Alice uses K to encrypt.
Bob uses K to decrypt.




The core issue was key distribution. If every pair of people, systems, banks, militaries, servers, or applications needed a shared secret, the number of keys explodes. You do not yet have PKI here. You only have the problem PKI will eventually help solve.

IN 1976, Ralph Merkle published one of the first protocosl to securely generate a symmetric cryptographic key over a public channel. Before this, systems that were communicating to one another had to know about each other in order for them to trust them. With DH, it makes it possible for two systems to securely establish a shared secret key over a insecure channel. 

The National Security Agency (NSA) launched a project called the Secure Data Network System (SDNS), with the intent to be used for standardization of the security services in the Open System Interconnection (OSI) architecture, which basically means ensuring interoperability the computer network that has been established in the 1960’s, which back then was crucial since much of the network traffic at the time were academic institutions and government related activities. The OSI architecture was created by the International Organization for Standardization (ISO) in the late 70’s. It was intended to support the emergence of the computer networking methods that were competing for application. In the early 90’s the US required through Federal Information Processing Standards, FIPS 146-1, the use of a common set of data communication protocols, OSI protocols, that enable vendors to have interoperability for the systems that they create for a variety of applications. If there was one thing to take away from this, its that there was a big push for computer networks to use a common set of protocols to ensure that all the vendors will be able to operate with one another, even if there is a variety of applicability between the vendor systems. There was a lot of segmentation that came with these different networks. This led to isolated domains of information which were difficult and expensive to integrate into other networks. 

NIST came out with SDNS which provided standardization of the security services into vendor products.


SP3 and SP4 were two of many protocols that came out of the SDNS project that were created to securely transmit messages between systems. SP3 is a SNICP (subnetwork independent convergence protocol). A convergence protocol is a layer that allows for the higher level applications to communicate with one snother without relying on the lower level technology. The document NIST IR 90-4250 explains the esrly protolcs thst were designed to protect the esrly ages of the internet. The document introduces elements of the modern PKI which js astronishing since the document itself is from the 90's. 

Another piece of document that came around this time was the 




## References
https://en.wikipedia.org/wiki/Transport_Layer_Security

https://nvlpubs.nist.gov/nistpubs/Legacy/IR/nistir90-4250.pdf

https://www.computerhistory.org/internethistory/1980s/

https://www.govinfo.gov/content/pkg/GOVPUB-C13-8921a1e6cdfd7122d1ffa88bd9ee0aa1/pdf/GOVPUB-C13-8921a1e6cdfd7122d1ffa88bd9ee0aa1.pdf




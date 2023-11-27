![IRD logo](../Images/IRlogo.gif)
![Software Dev](../Images/SoftwareDev.png)

# Mutual Authentication and Cipher Supported  

All Gateway Services channel users sending messages to IR do so over a secure network connection. The certifcate's Common Name (CN) are exchanged via the Developer Portal and the Digital Service Provider's (DSP) server certificates are used to connect to IR using a protocol known as mutual TLS (mTLS) / Client Certificate Authentication. mTLS allows IR to identify the DSP sending the message and encrypts the message in transit. 

The Common Name (CN), also known as the Fully Qualified Domain Name (FQDN), is the characteristic value within a Distinguished Name (DN). Typically, it is composed of Host Domain Name and looks like, "www.digicorp.com" or "digicorp.com".

# TLS Cipher Support

IR is making changes to the TLS authentication and cipher support to improve the security and to align with the most recent recommendations in the [NZISM (New Zealand Information Security Manual)](https://nzism.gcsb.govt.nz/ism-document/#Section-15853). 

To support this, the following Test environments will be moving all IR to ECC (elliptic curve) certificates on **Wednesday, 14 February 2024**: 

*	test5.services.ird.govt.nz  
*	test6.services.ird.govt.nz

We will be only supporting the ciphers listed below:

 |TLS Version |	IANA Cipher Name |OpenSSL Cipher Name| Key Exchange| Authenication | Encryption | Hash |
 | --- | --- | --- | --- | --- |--- | --- |
| TLS1.3| TLS_AES_256_GCM_SHA384 | TLS_AES_256_GCM_SHA384  |-|-| Advanced Encryption Standard with 256bit key in Galois/Counter mode (AES 256 GCM)| SHA384|
| TLS1.3| TLS_AES_128_GCM_SHA256	| TLS_AES_128_GCM_SHA256 |-|-|Advanced Encryption Standard with 128bit key in Galois/Counter mode (AES 128 GCM) | SHA256 |
| TLS1.3| TLS_CHACHA20_POLY1305_SHA256	| TLS_CHACHA20_POLY1305_SHA256 |-|-|ChaCha stream cipher and Poly1305 authenticator (CHACHA20 POLY1305)| SHA256 |
| TLS1.2|TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 |	ECDH-ECDSA-AES256-GCM-SHA384 | Elliptic Curve Diffie-Hellman Ephemeral (ECDHE) | Elliptic Curve Digital Signature Algorithm (ECDSA)|Advanced Encryption Standard with 256bit key in Galois/Counter mode (AES 256 GCM)| SHA384|
| TLS1.2|TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256	| ECDH-ECDSA-AES128-GCM-SHA256 | Elliptic Curve Diffie-Hellman Ephemeral (ECDHE)| Elliptic Curve Digital Signature Algorithm (ECDSA)|Advanced Encryption Standard with 128bit key in Galois/Counter mode (AES 128 GCM)| SHA256|
| TLS1.2|TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256	| ECDHE-ECDSA-CHACHA20-POLY1305 | Elliptic Curve Diffie-Hellman Ephemeral (ECDHE)|Elliptic Curve Digital Signature Algorithm (ECDSA)|ChaCha stream cipher and Poly1305 authenticator (CHACHA20 POLY1305)| SHA256|


>On **Wednesday 26 June 2024**, the Production environment will be changed to ECC certificates, and the cipher suite restricted to those listed above.

<hr/>

##  Mutual TLS Authentication (mTLS) / Client Certificate Authentication

We operate in a typical CA trust-based authentication model (utilising mTLS) so that any certificate that contains a pre-approved Common Name (CN) and is issued only by one of IR’s approved trusted root Certificate Authorities will be accepted. 

You need to ensure a Common Name is generated in the Developer Portal and used as part of the process of ordering a certificate from the approved list of CA’s below:

* Amazon
* Comodo
* Digicert
* Entrust
* GeoTrust
* Let’s Encrypt
* Sectigo
* Thawte

DSP Common Name will be assigned through the IR Developer Portal, and will use the DSP’s registered DNS domain, prefixed with a unique security identifier assigned by IR, for example:

* `298f9c17bbbe48958994982c383c409c.irdgws.yourdomainname.com` 
* `298f9c17bbbe48958994982c383c409c.irdgws.test.yourdomainname.com` 
* `298f9c17bbbe48958994982c383c409c.irdgws.prod.yourdomainname.com`

> NOTE: The assigned Common Name has to match exactly with your certifcate and what is loaded on our systems.  

> NOTE: Separate certificates are required to access test and production environments. We request you only use this Common Name certificate for mTLS with IR and this certificate is not used for other messages exchanges or web sites you may have.


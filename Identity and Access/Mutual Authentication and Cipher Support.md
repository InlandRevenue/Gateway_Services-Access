![IRD logo](../Images/IRlogo.gif)
![Software Dev](../Images/SoftwareDev.png)

# Mutual Authentication and Cipher Supported  

Currently all Gateway Services channel users sending messages to IR do so over a secure network connection. CNAMEs are exchanged during on-boarding and the public certifctes are used to connect to IR using a protocol known as mutual TLS (mTLS). This allows IR to identify the Digital Service Provider (DSP) sending the message and encrypts the message in transit. 

Changes are being made to how we use these certificates, how we are allowing mTLS 1.3 as well as continuing support for 1.2, and as well as changes we'll be making to our cyphers. 



## Enablement of TLS 1.3 (Changing 31 December 2022)

In addition to the TLS 1.2 protocol already offered, IR will also enable the newer TLS 1.3 protocol, which offers considerable improvements in both security and performance. 

TLS 1.3 specifies a much smaller and more prescriptive suite of ciphers than was offered by previous iterations of the protocol. 
Of these, IR’s security gateways do not currently support the CCM mode of operation, reducing the list of supported ciphers over TLS 1.3 to:
 
* TLS_AES_128_GCM_SHA256 
* TLS_AES_256_GCM_SHA384 
* TLS_CHACHA20_POLY1305_SHA256 

### IR systems now support TLS1.3

#### Your action and by when?
  
* DSP’s that support only the TLS1.2 protocol are very unlikely to be affected by the enablement of TLS1.3, but IR urges DSPs in this position to begin investigating an upgrade path to support TLS 1.3 by 31 December 2022. 

##	Deprecating TLS 1.2 Ciphers - Changing 31 March and 31 December 2022

IR will also take the opportunity to deprecate some older ciphers and algorithms supported by our current TLS 1.2 implementation. Specifically, IR intends to remove support for Diffie Hellman ephemeral (DHE) key exchange, and SHA-1 for message integrity. 

#### IR’s currently supported TLS 1.2 cipher suite is shown below. 

| TLS 1.2 cipher suite | Deprecate Support  |
| --- | --- |
| `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA` | 31 March 2022|
| `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256` | 31 December 2022|
| `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA` | 31 March 2022 |
| _`TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`_ | 31 December 2022|
| `TLS_RSA_WITH_AES_128_CBC_SHA` | 31 March 2022|
| _`TLS_RSA_WITH_AES_128_CBC_SHA256`_ | 31 December 2022|
| `TLS_RSA_WITH_AES_256_CBC_SHA` | 31 March 2022 |
| _`TLS_RSA_WITH_AES_256_CBC_SHA256`_ | 31 December 2022|
| `TLS_DHE_RSA_WITH_AES_128_CBC_SHA` | 31 March 2022|
| `TLS_DHE_RSA_WITH_AES_128_CBC_SHA256` | 31 March 2022|
| `TLS_DHE_RSA_WITH_AES_256_CBC_SHA` | 31 March 2022|
| `TLS_DHE_RSA_WITH_AES_256_CBC_SHA256` | 31 March 2022 |
| `TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256` ||
| `TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384` ||
| _`TLS_RSA_WITH_AES_128_GCM_SHA256`_ | 31 December 2022|
| _`TLS_RSA_WITH_AES_256_GCM_SHA384`_ | 31 December 2022|
| `TLS_DHE_RSA_WITH_AES_128_GCM_SHA256` |31 March 2022|
| `TLS_DHE_RSA_WITH_AES_256_GCM_SHA384` |31 March 2022|

> Cipher Block Chaining (CBC) mode has demonstrated itself to be problematic in recent years, and limitations in RSA when used for key agreement (not for digital signature authentication) means that IR will deprecate support for the italicised ciphers.


## Certificate Authentication 

In the past, DSPs were required to register an X.509 certificate with IR that the DSP will use for client authentication when establishing a TLS session with IR’s Gateway Services endpoint (services.ird.govt.nz:4046 and corresponding test URLs).  IR used a technique called certificate pinning to associate the expected certificate with the DSP’s client identity, ensuring a very high level of access security. 

But this approach had the drawback that it precluded DSPs from automating certificate rollover and had a high operational cost for both DSPs and IR when managing renewed certificates. 

We have now adopted a more typical CA trust-based authentication model (utilising mTLS) so that any certificate that contains a pre-approved subject Common Name (CNAME) and is issued only by one of IR’s approved trusted root Certificate Authorities will be accepted. The change applies to both Test and Prod environments

This means you will now need to ensure a CNAME is generated in the Developer Portal and used as part of the process of purchasing a certificate from the approved list of CA’s below.

* Amazon
* Comodo
* Digicert
* Entrust
* GeoTrust
* Let’s Encrypt
* Sectigo
* Thawte

DSP subject CNAMEs will be assigned through the IR Developer Portal, and will use the DSP’s registered DNS domain, prefixed with a unique security identifier assigned by IR, for example: 
* 0123456789abcdef.irdgws.yourdomainname.com or 
* 0123456789abcdef.irdgws.test.yourdomainname.com or   
* 0123456789abcdef.irdgws.prod.yourdomainname.com

### Your action and by when?

> We implemented our changes on 26 May 2021, but this will only impact you when you next roll over/renew your X.509 certificate. Any certificates that have been pinned prior to removal of the upload capability will be supported for a remaining 12 months or until their date of expiry (whichever is earlier).

**Please note:** Separate certificates will be required to access test and production environments. We request you only use this CNAME certificate for mTLS with IR and this certificate is not used for other messages exchanges or web sites you may have. 
IR advises deprecating the TLS 1.2 cyphers at the same time you change to CNAME certificates. IR will not accept new certificates for registration under the current pinning-based authentication method once the new trust-based model is implemented, the mTLS certificate upload capability has now been removed from the Developer Portal.  
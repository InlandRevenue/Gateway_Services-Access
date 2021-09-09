
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
  
* DSP’s that support only the TLS1.2 protocol are very unlikely to be affected by the enablement of TLS1.3, but IR urges DSPs in this position to begin investigating an upgrade path to support TLS 1.3 by 31 December 2022 (20+ Months). 

##	Deprecating TLS 1.2 Ciphers - Changing 31 March and 31 December 2022

IR will also take the opportunity to deprecate some older ciphers and algorithms supported by our current TLS 1.2 implementation. Specifically, IR intends to remove support for Diffie Hellman ephemeral (DHE) key exchange, and SHA-1 for message integrity. 

#### IR’s currently supported TLS 1.2 cipher suite is shown below. 

| TLS 1.2 cipher suite | End of Life |
| --- | --- |
| TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA | 31 March 2022|
| TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256 | 31 December 2022|
| TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA | 31 March 2022 |
| TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384 | 31 December 2022|
| TLS_RSA_WITH_AES_128_CBC_SHA | 31 March 2022|
| TLS_RSA_WITH_AES_128_CBC_SHA256 | 31 December 2022|
| TLS_RSA_WITH_AES_256_CBC_SHA | 31 March 2022 |
| TLS_RSA_WITH_AES_256_CBC_SHA256 | 31 December 2022|
| TLS_DHE_RSA_WITH_AES_128_CBC_SHA | 31 March 2022|
| TLS_DHE_RSA_WITH_AES_128_CBC_SHA256 | 31 March 2022|
| TLS_DHE_RSA_WITH_AES_256_CBC_SHA | 31 March 2022|
| TLS_DHE_RSA_WITH_AES_256_CBC_SHA256 | 31 March 2022 |
| TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 ||
| TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 ||
| TLS_RSA_WITH_AES_128_GCM_SHA256 | 31 December 2022|
| TLS_RSA_WITH_AES_256_GCM_SHA384 | 31 December 2022|
| TLS_DHE_RSA_WITH_AES_128_GCM_SHA256 |31 March 2022|
| TLS_DHE_RSA_WITH_AES_256_GCM_SHA384 |31 March 2022|

Cipher Block Chaining (CBC) mode has demonstrated itself to be problematic in recent years, and limitations in RSA when used for key agreement (not for digital signature authentication) means that IR will deprecate support for the italicised ciphers.


## Certificate Authentication 

In the past, DSPs were required to register an X.509 certificate with IR that the DSP will use for client authentication when establishing a TLS session with IR’s Gateway Services endpoint (services.ird.govt.nz:4046 and corresponding test URLs).  IR used a technique called certificate pinning to associate the expected certificate with the DSP’s client identity, ensuring a very high level of access security. 

But this approach had the drawback that it precluded DSPs from automating certificate rollover and had a high operational cost for both DSPs and IR when managing renewed certificates. 

We have now adopted a more typical CA trust-based authentication model (utilising mTLS) so that any certificate that contains a pre-approved subject Common Name (CNAME) and is issued only by one of IR’s approved trusted root Certificate Authorities will be accepted. The change applies to both Test and Prod environments

This means you will now need to ensure a CNAME is generated in the Developer Portal and used as part of the process of purchasing a certificate from the approved list of CA’s below.

|Supplier 	|Root Certificate Authority |
| --- | --- |
|Amazon |	Amazon Root CA 1 |
||SHA256 Thumbprint: 8e:cd:e6:88:4f:3d:87:b1:12:5b:a3:1a:c3:fc:b1:3d:70:16:de:7f:57:cc:90:4f:e1:cb:97:c6:ae:98:19:6e |
| |	Amazon Root CA 2 |
| |SHA256 Thumbprint: 1b:a5:b2:aa:8c:65:40:1a:82:96:01:18:f8:0b:ec:4f:62:30:4d:83:ce:c4:71:3a:19:c3:9c:01:1e:a4:6d:b4 |
| |	Amazon Root CA 3 |
| |SHA256 Thumbprint: 18:ce:6c:fe:7b:f1:4e:60:b2:e3:47:b8:df:e8:68:cb:31:d0:2e:bb:3a:da:27:15:69:f5:03:43:b4:6d:b3:a4 |
| |	Amazon Root CA 4 |
| |SHA256 Thumbprint: e3:5d:28:41:9e:d0:20:25:cf:a6:90:38:cd:62:39:62:45:8d:a5:c6:95:fb:de:a3:c2:2b:0b:fb:25:89:70:92 |
|Comodo |	COMODO Certification Authority  |
||SHA256 Thumbprint: 1a:0d:20:44:5d:e5:ba:18:62:d1:9e:f8:80:85:8c:bc:e5:01:02:b3:6e:8f:0a:04:0c:3c:69:e7:45:22:fe:6e |
| |	Secure Certificate Services  |
||SHA256 Thumbprint: bd:81:ce:3b:4f:65:91:d1:1a:67:b5:fc:7a:47:fd:ef:25:52:1b:f9:aa:4e:18:b9:e3:df:2e:34:a7:80:3b:e8 |
| |	Trusted Certificate Services  |
||SHA256 Thumbprint: 3f:06:e5:56:81:d4:96:f5:be:16:9e:b5:38:9f:9f:2b:8f:f6:1e:17:08:df:68:81:72:48:49:cd:5d:27:cb:69 |
| |	AAA Certificate Services  |
||SHA256 Thumbprint: d7:a7:a0:fb:5d:7e:27:31:d7:71:e9:48:4e:bc:de:f7:1d:5f:0c:3e:0a:29:48:78:2b:c8:3e:e0:ea:69:9e:f4 |
| 	Digicert| 	DigiCert Global Root CA |
||SHA256 Thumbprint: 43:48:a0:e9:44:4c:78:cb:26:5e:05:8d:5e:89:44:b4:d8:4f:96:62:bd:26:db:25:7f:89:34:a4:43:c7:01:61 |
||	DigiCert Global Root G2 |
||SHA256 Thumbprint: cb:3c:cb:b7:60:31:e5:e0:13:8f:8d:d3:9a:23:f9:de:47:ff:c3:5e:43:c1:14:4c:ea:27:d4:6a:5a:b1:cb:5f |
||	DigiCert Global Root G3 |
||SHA256 Thumbprint: 31:ad:66:48:f8:10:41:38:c7:38:f3:9e:a4:32:01:33:39:3e:3a:18:cc:02:29:6e:f9:7c:2a:c9:ef:67:31:d0 |
||	DigiCert High Assurance EV Root CA  
||SHA256 Thumbprint: 74:31:e5:f4:c3:c1:ce:46:90:77:4f:0b:61:e0:54:40:88:3b:a9:a0:1e:d0:0b:a6:ab:d7:80:6e:d3:b1:18:cf |
|Entrust |	Entrust Root Certification Authority |
||SHA256 Thumbprint: 73:c1:76:43:4f:1b:c6:d5:ad:f4:5b:0e:76:e7:27:28:7c:8d:e5:76:16:c1:e6:e6:14:1a:2b:2c:bc:7d:8e:4c |
||	Entrust Root Certification Authority - EC1 |
||SHA256 Thumbprint: 02:ed:0e:b2:8c:14:da:45:16:5c:56:67:91:70:0d:64:51:d7:fb:56:f0:b2:ab:1d:3b:8e:b0:70:e5:6e:df:f5 |
||	Entrust Root Certification Authority - G2 |
||SHA256 Thumbprint: 43:df:57:74:b0:3e:7f:ef:5f:e4:0d:93:1a:7b:ed:f1:bb:2e:6b:42:73:8c:4e:6d:38:41:10:3d:3a:a7:f3:39 |
||	Entrust Root Certification Authority - G3 |
||SHA256 Thumbprint: 15:83:99:55:9e:30:85:02:7d:3c:d7:e8:13:92:3f:8b:54:e5:4f:f7:25:e6:7e:70:d0:28:6b:b1:d5:02:de:64 |
||	Entrust.net Certification Authority (2048) |
||SHA256 Thumbprint: 6d:c4:71:72:e0:1c:bc:b0:bf:62:58:0d:89:5f:e2:b8:ac:9a:d4:f8:73:80:1e:0c:10:b9:c8:37:d2:1e:b1:77 |
|GeoTrust 	|GeoTrust Primary Certification Authority  |
||SHA256 Thumbprint: 37:d5:10:06:c5:12:ea:ab:62:64:21:f1:ec:8c:92:01:3f:c5:f8:2a:e9:8e:e5:33:eb:46:19:b8:de:b4:d0:6c |
||	GeoTrust Primary Certification Authority - G2 |
||SHA256 Thumbprint: 5e:db:7a:c4:3b:82:a0:6a:87:61:e8:d7:be:49:79:eb:f2:61:1f:7d:d7:9b:f9:1c:1c:6b:56:6a:21:9e:d7:66 |
||	GeoTrust Primary Certification Authority – G3 |
||SHA256 Thumbprint: b4:78:b8:12:25:0d:f8:78:63:5c:2a:a7:ec:7d:15:5e:aa:62:5e:e8:29:16:e2:cd:29:43:61:88:6c:d1:fb:d4 |
||	GeoTrust Primary Certification Authority – G4 |
||SHA256 Thumbprint: 9e:50:37:38:72:2e:0a:10:4c:f6:59:ff:9f:92:f0:b5:b3:66:2a:cd:11:2d:46:64:d1:e7:db:93:ab:f4:6a:59 |
||	GeoTrust Global CA  |
||SHA256 Thumbprint: ff:85:6a:2d:25:1d:cd:88:d3:66:56:f4:50:12:67:98:cf:ab:aa:de:40:79:9c:72:2d:e4:d2:b5:db:36:a7:3a |
||	GeoTrust Global CA 2 |
||SHA256 Thumbprint: ca:2d:82:a0:86:77:07:2f:8a:b6:76:4f:f0:35:67:6c:fe:3e:5e:32:5e:01:21:72:df:3f:92:09:6d:b7:9b:85 |
||	GeoTrust Universal CA  |
||SHA256 Thumbprint: a0:45:9b:9f:63:b2:25:59:f5:fa:5d:4c:6d:b3:f9:f7:2f:f1:93:42:03:35:78:f0:73:bf:1d:1b:46:cb:b9:12 |
||	GeoTrust Universal CA 2 |
||SHA256 Thumbprint: a0:23:4f:3b:c8:52:7c:a5:62:8e:ec:81:ad:5d:69:89:5d:a5:68:0d:c9:1d:1c:b8:47:7f:33:f8:78:b9:5b:0b |
|Let’s Encrypt |	DST Root CA X3 |
||SHA256 Thumbprint: 06:87:26:03:31:a7:24:03:d9:09:f1:05:e6:9b:cf:0d:32:e1:bd:24:93:ff:c6:d9:20:6d:11:bc:d6:77:07:39 |
||	ISRG Root X1 |
||SHA256 Thumbprint: 96:bc:ec:06:26:49:76:f3:74:60:77:9a:cf:28:c5:a7:cf:e8:a3:c0:aa:e1:1a:8f:fc:ee:05:c0:bd:df:08:c6 |
||	ISRG Root X2 |
||SHA256 Thumbprint: 69:72:9b:8e:15:a8:6e:fc:17:7a:57:af:b7:17:1d:fc:64:ad:d2:8c:2f:ca:8c:f1:50:7e:34:45:3c:cb:14:70 |
|Sectigo |	USERTrust RSA Certification Authority  |
||SHA256 Thumbprint: e7:93:c9:b0:2f:d8:aa:13:e2:1c:31:22:8a:cc:b0:81:19:64:3b:74:9c:89:89:64:b1:74:6d:46:c3:d4:cb:d2 |
|Thawte| 	thawte Primary Root CA  |
||SHA256 Thumbprint: 8d:72:2f:81:a9:c1:13:c0:79:1d:f1:36:a2:96:6d:b2:6c:95:0a:97:1d:b4:6b:41:99:f4:ea:54:b7:8b:fb:9f |
||	thawte Primary Root CA - G2 
||SHA256 Thumbprint: a4:31:0d:50:af:18:a6:44:71:90:37:2a:86:af:af:8b:95:1f:fb:43:1d:83:7f:1e:56:88:b4:59:71:ed:15:57 |
||	thawte Primary Root CA – G3 
||SHA256 Thumbprint: 4b:03:f4:58:07:ad:70:f2:1b:fc:2c:ae:71:c9:fd:e4:60:4c:06:4c:f5:ff:b6:86:ba:e5:db:aa:d7:fd:d3:4c |
||	thawte Primary Root CA – G4 |
||SHA256 Thumbprint: cb:b0:27:07:16:0f:4f:77:29:1a:27:56:14:48:69:1c:a5:90:18:08:e5:f3:6e:75:84:49:a8:62:aa:52:72:cb |

DSP subject CNAMEs will be assigned through the IR Developer Portal, and will use the DSP’s registered DNS domain, prefixed with a unique security identifier assigned by IR, for example: 
* 0123456789abcdef.irdgws.yourdomainname.com, or 
* 0123456789abcdef.irdgws.test.yourdomainname.com  

Your action and by when?
---

> We implemented our changes on 26 May 2021, but this will only impact you when you next roll over/renew your X.509 certificate. Any certificates that have been pinned prior to removal of the upload capability will be supported for a remaining 12 months or until their date of expiry (whichever is earlier).

**Please note:** Separate certificates will be required to access test and production environments. We request you only use this CNAME certificate for mTLS with IR and this certificate is not used for other messages exchanges or web sites you may have. IR advises deprecating the TLS 1.2 cyphers at the same time you change to CNAME certificates. IR will not accept new certificates for registration under the current pinning-based authentication method once the new trust-based model is implemented, the mTLS certificate upload capability has now been removed from the Developer Portal.  

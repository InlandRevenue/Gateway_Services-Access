![IRD logo](../Images/IRlogo.gif)
![Software Dev](../Images/SoftwareDev.png)

# How to Integrate M2M JWT Authentication 

### Key Documentation 
* What is the JSON Web Token structure?
   * Header
   * Payload
   * Signature
* Generate self-signed RSA sha256 2048 bit private key and public certifcate
   * openSSL command line example
* Generate a digitally signed JWT
   * Sample BASH shell script


## What is the JSON Web Token structure?
In its compact form, JSON Web Tokens consist of three parts separated by dots (.), which are:

* Header
* Payload
* Signature

Therefore, a JWT typically looks like the following.

`xxxxx.yyyyy.zzzzz`

Let's break down the different parts.

#### Header
The header typically consists of two parts: the type of the token, which is JWT, and the signing algorithmabeing used, such as RSA SHA-256.

For example:
```
{
  "alg": "RS256",
  "typ": "JWT",
  "kid": "M2M"
}
```

Then, this JSON is _Base64Url_ encoded to form the first part of the JWT.

#### Payload
The second part of the token is the payload, which contains the claims. Claims are statements about an entity (typically, the user) and additional data. There are three types of claims: registered, public, and private claims.

 * ***Registered claims:*** These are a set of predefined claims which are mandatory to provide a set of useful, 
 interoperable claims. These are: **(iss)** (issuer), **exp** (expiration time), **sub** (subject), **aud** (audience), and others.

> Notice that the claim names are only three characters long as JWT is meant to be compact.
> The **"sub"** must match the thumbprint of the public signing certifcate. 

 * ***Private claims:*** These are the custom claims created to share information between parties that agree on using them and are neither registered or public claims.
   These are: **startLogon** (START Logon) an optional parameter if the myIR username is required. 

An example payload could be:   
``` 
{
  "sub": "01B976835ECD5F58D5DE4AB89B827A99962CC4C50FCEE86E6352F536C5E4DACC",
  "iss": "Digital Service Provider",
  "startLogon": "",
  "iat": 1604886360,
  "exp": 1604886900
}
```   
   
The payload is then Base64Url encoded to form the second part of the JSON Web Token.   
   
> Do note that for signed tokens this information, though protected against tampering, is readable by anyone. Do not put secret information in the payload or header elements of a JWT unless it is encrypted.   
   
#### Signature

To create the signature part you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.

For example if you want to use the RSA SHA256 algorithm, the signature will be created in the following way:

```
RSASHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  {private.key})
```
  
The signature is used to verify the message wasn't changed along the way, and, in the case of tokens signed with a private key, it can also verify that the sender of the JWT is who it says it is.

#### Putting all together

The output is three Base64-URL strings separated by dots that can be easily passed in HTML and HTTP environments, while being more compact when compared to XML-based standards such as SAML.

The following shows a JWT that has the previous header and payload encoded, and it is signed with a private key.

``` 
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ik0yTSJ9.eyJzdWIiOiJGMkM5RjhGMTRGOUE0MzIwOTVEQjhCOUZDMUVCNzQ2QzY3ODNCN0MzNDM3NTQ1NjFGOUFFQ0NCN0M3ODJFNjMyIiwiaXNzIjoiRGlnaXRhbCBTZXJ2aWNlIFByb3ZpZGVyIiwic3RhcnRMb2dvbiI6IiIsImlhdCI6MTYwNDg5MDY5NSwiZXhwIjoxNjA0ODkxMjM1fQ.RLKLzj7loojV7ah4JfGCETFIWAAQ8vgcjVhL8F7BJpUMj8PTlEf2eKSfm_ByhL4q6b9sRL2Fr1AI_q5UUQBTONW7XozW0_gf7sVKdybqbDt1sNu5cQoDjbgPFb8-podiZE0Y1aKNPbR8UvRNUJb_tM04t1tuTGTuZiA7Syr2NLQDl65lSrOdHIV418HMTw-W8ukCIZkzIDMyDkCMXqKuhes_ASD_zRsD4lFr7rJa5T-eSkyD-vq_TxgwA5NKOWxUgFYeOv6Wi3hO3Rplf1AWK5aBfzJERM2S1OkPAyp9eogLMKF-XivyqVh8aSC0isNyUvQGo6uZy-6vV0X1r32Dxw
```

If you want to play with JWT and put these concepts into practice, you can use jwt.io Debugger to decode, verify, and generate JWTs.

#### Example Public RSA SHA256 Certifcate 

This is what is sent to Indand Revenue and is what is used to validate incoming JWTs.
```
-----BEGIN CERTIFICATE-----
MIIDXTCCAkWgAwIBAgIJALb18oC9dy/BMA0GCSqGSIb3DQEBCwUAMEUxCzAJBgNV
BAYTAkFVMRMwEQYDVQQIDApTb21lLVN0YXRlMSEwHwYDVQQKDBhJbnRlcm5ldCBX
aWRnaXRzIFB0eSBMdGQwHhcNMjAxMTA5MDI0NzEyWhcNMjAxMjA5MDI0NzEyWjBF
MQswCQYDVQQGEwJBVTETMBEGA1UECAwKU29tZS1TdGF0ZTEhMB8GA1UECgwYSW50
ZXJuZXQgV2lkZ2l0cyBQdHkgTHRkMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIB
CgKCAQEAt953sK9R0O8DSTwfvKdOPG+Xx7YkOT5xydSeVV+ItbhCwrC5pHIevqSw
5AXYM8GYO1LAo2tpyWfRfzlQeLJYZns7u5IBJlPkuSL+B4WAZXEuJ94enOEDZn4t
p7fmWFDoO4qjNiQNNgJIvNBmAbGqRM+nfRRVD6kG2SMw0cERk2I3FJ8o2aduAQXb
NQo9gP6vLfnt/JCS1QFXTCB9dXcdCakgRqj7FWFiNWy4NG/EqM19zYXFusrmpUoG
8XTF+upFo/nioRu/28H4jDmXFo5FD6iOeDCzLnkFDzxX1775ZzEFn6C4CBbMP987
F6x+oXQsBjazCJlS8ctXHXiWWO0/xwIDAQABo1AwTjAdBgNVHQ4EFgQU3lMNm2ON
vEKK/USZ0QW4xQyxm3AwHwYDVR0jBBgwFoAU3lMNm2ONvEKK/USZ0QW4xQyxm3Aw
DAYDVR0TBAUwAwEB/zANBgkqhkiG9w0BAQsFAAOCAQEAZNqBKuC+OY6G3FpjjkRo
iCDiv6eGkYuh4+I8chFBiHifOQkTHFnFd+S7D3Fa7mg7cP579QCvT5uR1prt1cgF
LXddeJ13XFrSKNm1izbidWhMW74oruW1+pytI/0fPaMmYBY54mvyM6iebrfgWfrd
W/or1LkiAPzMWX9oyt2nZViWvTrTXxs3bS+uElgA/nk/Th7okNg37eOs3H8nztlV
uz3FQOxOrQEUjnwNkVuAkMy33C/JWU3X5rRg4lLIGU4klWtbbZRKHESy+dwdC+pc
zYlzlScLvgiKJ4siu8Qc/XaglgMIUkfMJFlq7+UlCS1Hz1Col8HCnUOFtHAom1DW
WQ==
-----END CERTIFICATE-----
```


## Generate self-signed RSA sha256 2048 bit private key and public certifcate 

This is a command on how you can generate a self-signed public and private RSA key pair:

```  
openssl req  -nodes -new -x509 -keyout private.key -out public.crt
``` 

## Generate a digitally signed JWT 

> This script is only intended for demonstrational & developer training purpose only and is not inteneded to be used in production. Refer to your programming language on how you can generate a JWT. 

This BASH shell script is to show how to create a JWT and have it signed using the RSA `private.key`.

## JWT Bash Script
```
#!/bin/bash
PEM=$( cat ./private.key )

# Get the thumbprint from the public certifcate.
THUMBPRINT=$( openssl x509 -in ./public.crt -fingerprint -noout -sha256 )

# Extract the thumb print value and delete the colons
THUMBPRINT=$(cut -d '=' -f 2 <<< "$THUMBPRINT" | tr --delete :)

echo "DEBUG"
echo ${THUMBPRINT}
echo ""

NOW=$( date +%s )
IAT="${NOW}"
# expire 9 minutes in the future.
EXP=$((${NOW} + 540))

HEADER_RAW='{"alg":"RS256","typ":"JWT","kid":"M2M"}'
HEADER=$( echo -n "${HEADER_RAW}" | openssl base64 | tr -d '=' | tr '/+' '_-' | tr -d '\n' )

PAYLOAD_RAW='{"sub":"'${THUMBPRINT}'","iss":"Digital Service Provider","startLogon":"","iat":'"${IAT}"',"exp":'"${EXP}"'}'
PAYLOAD=$( echo -n "${PAYLOAD_RAW}" | openssl base64 | tr -d '=' | tr '/+' '_-' | tr -d '\n' )

HEADER_PAYLOAD="${HEADER}"."${PAYLOAD}"

SIGNATURE=$( openssl dgst -sha256 -sign <(echo -n "${PEM}") <(echo -n "${HEADER_PAYLOAD}") | openssl base64 | tr -d '=' | tr '/+' '_-' | tr -d '\n' )

JWT="${HEADER_PAYLOAD}"."${SIGNATURE}"

echo $JWT

echo ""
echo "Open JWT.IO website and copy & past the above JWT"
echo ""
echo "Copy & paste the certifcate to the verify Signature:"
echo ""

cat ./public.crt

```
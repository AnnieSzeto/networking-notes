# mTLS

### Domain Name Service and How Things Work

DNS query path:

- Client > enters a domain name into a web browser
  - if cached locally: site is fetched and DNS system ends here, else:
- Recursive DNS resolver > DNS query recurses up hierarchy
  - if found: address is returned to client and cashed. else:
- Root server > directs resolver to correct Top Level Domain (TLD) server
- TLD server > responds with IP address of the domain's nameserver
- Authoratative nameserver > responds with domain's IP address
- Resolver responds to web browser with IP address for requested domain
  - address is cached on the way back and stored locally

### Encyption, Trust, and Certificates

Data on the internet is encrypted for privacy and security, this mitigates Man-In-The-Middle attacks. This encryption has a cypher key that must be pre-shared to decrypt/encrypt data.

Trust is established through chains of certificates signed by trusted 3rd-parties. Certificates are signed by a Certificate Authority's private key, which can be checked by softwares (e.g. browser) by the CA's public key. If the software/browser trusts a Root CA, any intermediate signed will be trusted and any signed by the trusted intermediate will be trusted, and so forth, forming a "chain" of trust. This authenticates web servers, as attackers will often set up fake websites to trick users/steal data.

Due to the expense of private/public key pairs, they are usually only used to share the symmetric encryption key, which is much cheaper to maintain.

### Secure Sockets Layer (SSL) _[depreciated]_ and Transport Layer Security (TLS)

In 1991, SSL 3.0 -> TLS, there is minimal differences between versions. The name change was mostly an indicator of change in ownership (Netscape to Internet Engineering Task Force (IETF)), the two terms are often used interchangeably.

SSL/TLS is a protocol for encrypting, securing, and authenitcating communcations in the internet. TLS is the most widely deployed standard for secure communication (e.g. HTTPS).

**Encryption:** hides data being transferred from 3rd-parties

**Authentication:** ensures the parties exchanging information are who they claim to be

**Integrity:** verifies that the data has not been forged or tampred with.

### TLS Handshake

1. 'Client hello' Message
   - **_Client_** initiates handshake via 'hello' message: includes client TLS versions, cipher suites (set of algorithms), string of random bytes 'client random'
2. 'Server hello' Message
   - **_Server_** sends a message: contains the server's SSL certificate (and public key), server's chosen cipher suite, string of random bytes 'server random'
3. Authentication & Premaster Secret
   - **_Client_** verifies server's SSL cert with the CA that issued it. Then sends another string of random bytes 'premaster secret' which is encrupted with the public key (from SSL cert).
4. Private Key Used
   - **_Server_** decripts the premaster secret.
5. Session Keys created
   - Both **_client and server_** genereate session keys from 'client random', 'server random', and 'premaster secret'
6. Client is ready
   - **_Client_** sends encrypted 'finished' message with session key
7. Server is ready
   - **_Server_** sends encrypted 'finished' message with session key
8. Secure symmetric encription achieved
   - Handshake completed, communication continues via session keys

All TLS Handshakes uses asymmetric cryptography (private/public key pair), but not all uses the private key to generate session keys, e.g. Diffie-Hellman handshake.

tldr version:

1. Client connects to server
2. Server presents its certificate
3. Client verifies server's certificate
4. Client and server exchange info over encrypted connection

## What is mTLS?

Mutual TLS is a method for mutual authentication, verifying both parties and that they both have the correct private key.

### How is it different

Both the client and server have a certificate and both sides authenticate using the private/public key pair, meaning **_additional steps_** in mTLS Handshakes compared to just TLS:

1. Client connects to server

2. Server presents its certificate

3. Client verifies server's certificate

4. **_Client presents its TLS certificate_**

5. **_Server verifies client's certificate_**

6. **_Server grants access_**

7. Client and server exchange info over encrypted connection

A root TLS certificate is necessary for mTLS since the organisation implementing mTLS needs to act as its own certificate authority.

## Where is mTLS frequently used?

Often used in Zero Trust security frameworks, where no user/device/network is trusted by default. It provides additional security, ensuring trust in both directions.

For everyday purposes on the public internet, the one-way TLS authentication is sufficient. Replacing TLS with mTLS would be near-impossible due to the managing of client certificates needed.

MTLS is highly usefula nd practical for individual organisations that uses a Zero Trust approach for network security.

## Example application

Cloudflare Zero Trust uses mTLS for Zero Trust security. Cloudflare API Shield also uses mTLS for verification.

An example of mTLS usage is Uber. With one of the largest deplyments of Apache Kafka platform, Uber uses TLS on the transport layer for encryption and uses mTLS to authicate the identity of both clients and Kafka brokers. Kafka provides their own custom authoriser for authorisation.

### Diagram

![image](./TLS%20and%20mTLS%20Handshake.png)

link to excalidraw: https://excalidraw.com/#json=TmgSFFjVUXkPZCOvuv1Bx,z37ScC45xNM3GwK-_oUxhw

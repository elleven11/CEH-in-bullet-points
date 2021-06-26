## Cryptography

### Block cipher

- 📝 Fixed-size blocks of data using a symmetric key
- Data bits are split up into blocks and fed into the cipher
- Each block of data (usually 64 bits) is encrypted with key and algorithm
- Simpler and slower than stream ciphers
- Key chosen for cipher must have a length larger than the data, if not, it is vulnerable to frequency attacks

### Stream cipher

- 📝 One bit at a time using a symmetric key
- Combines each bit with a pseudorandom cipher digit stream (keystream)
- Works at a high rate of speed
- Usually done by an combining XOR with random generated key.


### Actors of PKI (Public Key Infrastructure)

- **Validation authority (VA)**
  - 📝 Used to validate certificates, stores certificates with their public keys
- **Certificate authority (CA)**
  - Also known as **certification authority**
  - 📝 Third party to issue and verify [digital certificate](#digital-certificate)s
    - Digital certificates contain public key and the identity of the owner.
  - E.g. [Comodo](https://ssl.comodo.com/), [IdentTrust](https://www.identrust.com/), [GoDaddy](https://godaddy.com/web-security/ssl-certificate)
- **Registration authority (RA)**
  - 📝 Acts as verifier for the certificate authority
- **Certificate Management System**
  - Generates, distributes, stores, and verifies certificates
- **End user**
  - Requests, manages, and uses certificates

## IPSec

- IPsec is an end-to-end security scheme
- 📝 Part of IPv4 suite so it runs on layer 3 (internet layer) in [TCP/IP model](./../03-scanning-networks/tcpip-basics.md#tcpip-model) or layer 3 (transport) in [OSI model](./../03-scanning-networks/tcpip-basics.md#osi-model)
- 📝 Provides security through
  - **Authentication** through authenticating both parts
  - **Integrity** through using a hash algorithm to ensure that data is not tampered with.
  - **Non-repudiation** through using public key digital signatures to prove message origin.
  - **Confidentiality** through encryption

### IKE (Internet Key Exchange)

- Also known as **IKEv1** or **IKEv2** depending on the version.
- 📝 Encrypts packets (payloads and headers) between parts
- Uses [X.509](./encrypting-communication.md#x509) for public key and encryption
- Cryptographic settings are established through ***Internet Key Exchange crypto profile*** (IKE policies)
- Tool: [`ike-scan`](https://github.com/royhills/ike-scan)
  - Discover, fingerprint and test IPsec VPN servers and firewalls
  - Sends a specially crafted IKE packet to each host within a network
- 📝 Deployed widely to implement e.g.
  - virtual private networks (VPNs)
  - remote user access through dial up connection to private networks

### IPSec security architecture

- **Authentication Headers (AH)**
  - Provides connectionless integrity and authentication for the entire IP packet
  - Provides protection against replay attacks
- **Encapsulating Security Payloads (ESP)**
  - 📝 In addition to AH it provides confidentiality through encryption
  - Unlike AH, it does not provide integrity and authentication for entire IP packet
    - The outer header (including any outer IPv4 options or IPv6 extension headers) remains unprotected
  - Supports encryption-only and (❗ insecure) authentication-only configurations
- **Security Associations (SA)**
  - Provides the bundle of algorithms and data to provide the parameters necessary for AH and/or ESP

### IPSec modes of operation

- AH and ESP can be implemented in both modes

#### Transport mode

- Usually authenticated
- Only payload is optionally encrypted.
- Not compatible with NAT when authenticated.
- 📝 Used within same network

#### Tunnel mode

- Entire packet is encrypted and authenticated.
- Compatible with NAT
- 📝 Used to create virtual private networks between different networks.

### Diffie-Hellman groups

- Diffie-Hellman group 1—768 bit 
- Diffie-Hellman group 2 —1024 bit 
- Diffie-Hellman group 5—1536 bit 
- Diffie-Hellman group 14—2048 bit 
- Diffie-Hellman group 19—256 bit elliptic curve
- Diffie-Hellman group 20—384 bit elliptic curve

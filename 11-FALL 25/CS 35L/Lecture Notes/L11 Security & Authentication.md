## CIA Triad
### 1. Confidentiality
- Sensitive data only **accessible** by authorized users
### 2. Integrity
- Sensitive data only **modifiable** by authorized users
- Maintains accuracy, consistency, and trustworthiness of data
### 3. Availability
- Services available when needed by clients

## Software Vulnerabilities
### SQL Injection Attack
- Use prepared statements and parameterized queries to protect against **SQLi**
	- Sanitize input parameters to prevent injection attacks:
		- Parameterized queries: specify where parameters should be inserted
		- Usual syntax to reference the parameter by index: `@0`, `@1`
- Violates **confidentiality**, **integrity**

### Cross-Site Scripting (XSS) Attack
- Attacker injects **JavaScript code** into the trusted site, and the browser executes the code

## Security Design Principle: Zero Trust Principle, Trust Boundaries
- Users and devices should not be trusted by default
- Any input might be malicious: **sanitize all inputs**

### Security Through Obscurity
- Concealing the mechanisms of the system to enhance security -- but if the details can be discovered, it opens vulnerabilities
	- Like hiding the key in the flowerpot
- **Should NOT be the primary approach!** Attackers shouldn't be able to break in just by understanding how it works

### Open Design Principle
- Use robust, public security mechanisms
#### Public Scrutiny
- Full transparency allows experts to examine the design for potential vulnerabilities
- ex. Apply when proposing a *new security approach*
#### Complementary Obscurity
- Hide implementation **details** to make it harder to exploit known vulnerabilities
- ex. Apply when implementing an *existing commercial system*

## Encryption
### Symmetric Encryption
- ex. AES
- Ensures confidentiality
- Uses a single, shared secret key for both encrypting and decrypting data

### Public-Key Cryptography
- ex. RSA
- Allows you to encrypt and decrypt data without having to secretly exchange a key
- Each user generates a mathematically linked pair of keys: a public key and a private key
- **Encryption**: Anyone can use your public key to encrypt a message, but only you can decrypt it
- **Decryption**: You use your private key to decrypt messages that were encrypted with your public key
- **Digital signatures**: Encrypting a document with your private key allows everyone to read it with your public key, but guarantees you are the only one who could have written it

## Client-Server Authentication
### Session-Based Authentication via Session Cookies
- After initial authentication, server generates a **session ID** that the client sends with every request (a **cookie**)
	- Session ID is stored in a client-side cookie (`HttpOnly` cookie prevents client-side JS from accessing it)
- Session cookies are **stateful**, as the server needs to maintain a record of each active session

### Authentication via JSON Web Token (JWT)
- After initial authentication, server generates a **token** (JWT) that the client sends with every request and signs it with a secret key
- JWT identifies the user and is stored client-side in memory in cookies
- **Stateless** since the server does not need to store the session ID

## Principle of Least Privilege
- In order to reduce the attack surface and the impact of a security breach, every program and user should operate using the **least privileges necessary** to complete the job
- Split your application into **separate components** and apply the principle: If an attacker compromises one component the impact is reduced
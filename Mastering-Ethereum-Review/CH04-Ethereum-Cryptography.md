- 이더리움 디지털 서명&타원곡선함수 - [https://borntodevelop.tistory.com/entry/이더리움의-디지털-서명과-타원곡선-함수](https://borntodevelop.tistory.com/entry/%EC%9D%B4%EB%8D%94%EB%A6%AC%EC%9B%80%EC%9D%98-%EB%94%94%EC%A7%80%ED%84%B8-%EC%84%9C%EB%AA%85%EA%B3%BC-%ED%83%80%EC%9B%90%EA%B3%A1%EC%84%A0-%ED%95%A8%EC%88%98)

# **📌 CH04: Ethereum Cryptography**

Ethereum employs various cryptographic techniques to ensure **security and integrity**.

These techniques apply to key components like account generation, transaction signing, block production, and smart contract integrity.

---

## **📌 1️⃣ Public-Key Cryptography**

### **🔹 EOA and Contract Account Addresses**

- **EOA (Externally Owned Account)**: Controlled by a private key
- **Contract Account**: Smart contract code deployed at an address, activated externally

### **🔹 Basic Principle of PKC**

- Flow: Private Key → Public Key → Address
- Messages are **signed** with a private key and **verified** using the public key

📌 **Analogy:**

> The private key is like a "password", and the public key is a "mail address"  
> Only the sender can sign (send), but anyone can verify

---

## **📌 2️⃣ Elliptic Curve Cryptography (ECC)**

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c2ba559c-cb6d-4c61-bec3-1760fafc9a92/384d15af-3818-491a-affc-5c69e35e6a82/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662MUASCH7%2F20250522%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250522T034056Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEBMaCXVzLXdlc3QtMiJHMEUCIQCrB7XBtf5pRZP8S%2F728%2BFp67xMdIb3AboWFIzWIz5x%2FAIgGFIS9BWAZARz0LqyJ7CHNwJmMnQMXlEGKZVl8js1KSgqiAQIy%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDAuRaoKd0Id7kdg8NircA6hTsDc%2FeTdi4z9hASPkSDxPgjQ8BjnyjK5PAEaM7oUvc7GveNUobXg%2BN1QhviVH96BwCRPPQogFqS2HGoa8WyTt43QP74TtZshF3HTbqNsncxRY%2F3Cr7QfwxxH4P0F1WzQzCczFNS1jpaJSejYL1bMvhSGAmyCXYBm8tChpFC9%2FqRLbz66VMEXU7zZ6n5rUbbXQqZfC8ELFQemybCKas%2F%2FRmAAuJqmGPO5kZaCWM%2FI2m3P48ztvM1TxYQj1bwl%2B4bblg8IWGCAO3CZMzNYUHPXLTbTjCesvIjt07X%2FEEhz2xBQlxV2ovI%2FtO0YoP%2B9cSg4cbvl0PVMrrPMrFBpkvptwV6tJuJWThrXP2brEsv5N6SAtRYDeAmY6ExjMeHklzWWDYI3kpS8uM%2B7Kv1XvLUt5DACLneSW1z3dSqnTS9zovgekuivMQSb%2FZl4xTRmihuGo6pyaJSJMuObGsPy%2B%2Fxma5yasNxQEd2hLWUaXVDk6Gab50jDTcmx%2FDOY5TyBOObOoqybZfXCwI0NxD0fArfncd2iwxrt0him1vkTjW%2FzEX4tgpecJ%2Fu7ZaP9amwPCw17Tcbb3nEdff4KfUc44GYE3Vnq%2Bik1jyzR1Z5t5%2F2pLtpQ%2F6TM9MCka%2BFUNMM2TusEGOqUBBQwujXQGBN%2B0N42674D559Qv8Q9UOpGZNbjiZ3I5rbXY4TwIL7Nt0oPChONHTNUZbDLSrubFnumm9z5sT%2FgrcAmxjyryGBwQimgD7hx%2FpnisRG1UB7TJH7jSlGXgYEwzn7GaCD%2Bn17NLUE5r%2BZW2cZWncgIDA4DelqmCNoEAWks5u2FkJeGkeXG6NOK5gH1HspveE6x5nSXBYjjSGLNO6bGZNfnI&X-Amz-Signature=a6d2696e6606cc32839e917f6061fcdb481e31de20e8884160b7f51d92b0d91f&X-Amz-SignedHeaders=host&x-id=GetObject)

### **🔹 Concept of ECC**

- Uses points on an elliptic curve to generate keys
- Security is based on the difficulty of the discrete logarithm problem
  > Ethereum uses the secp256k1 curve

### **🔹 ECC Process**

1. Generate a **256-bit random private key**
2. **Public Key = Private Key × Generator Point (G)** on the curve
3. Apply **Keccak-256** to the public key → take the **last 20 bytes** → Ethereum address

📌 **Analogy:**

> ECC is like solving a “pathfinding problem”  
> The destination (public key) is visible, but the starting point (private key) is hard to reverse-engineer

---

## **📌 3️⃣ Digital Signature and Verification (ECDSA)**

### **🔹 Principle of ECDSA**

- ECDSA (Elliptic Curve Digital Signature Algorithm) is a signature algorithm based on ECC
- Signing a transaction allows others on the network to **verify the sender’s identity**

### **🔹 Signing Flow**

1. Generate a hash of the transaction (Keccak-256)
2. Sign the hash with the private key
3. Network nodes use the public key to verify the signature

📌 **Analogy:**

> A digital signature is like a "fingerprint and seal"  
> It can be verified by anyone, but is nearly impossible to forge

---

## **📌 4️⃣ Hash Functions and Keccak-256**

### **🔹 Properties of Hash Functions**

| Property            | Description                                                 |
| ------------------- | ----------------------------------------------------------- |
| Deterministic       | Same input always gives same output                         |
| Irreversible        | Original data cannot be derived from the hash               |
| Collision-Resistant | Extremely low probability of two different inputs colliding |
| Fast Computation    | Generates output quickly                                    |
| Random-Like Output  | Appears unpredictable and random                            |

### **🔹 Keccak-256**

- Based on SHA-3
- Used in Ethereum for transaction hashing, address generation, and state hashing

📌 **Applications**

- Verifying transaction integrity
- Address computation
- Block hashing
- Zero-knowledge proofs, message fingerprinting

---

## **📌 5️⃣ Ethereum Address Generation Process**

### **🔹 Generation Steps**

1. Generate a random **256-bit private key**
2. Derive the public key (secp256k1)
3. Apply Keccak-256 hashing to the public key
4. Take the last 20 bytes → Ethereum address

📌 **Analogy:**

> Generating an address is like building a mailbox (address) from a lock (public key) and key (private key)

---

## **📌 6️⃣ Inter-Exchange Client Address Protocol (ICAP)**

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c2ba559c-cb6d-4c61-bec3-1760fafc9a92/a6ca2421-e237-4d90-9d7d-a7efc3380ac8/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662MUASCH7%2F20250522%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250522T034057Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEBMaCXVzLXdlc3QtMiJHMEUCIQCrB7XBtf5pRZP8S%2F728%2BFp67xMdIb3AboWFIzWIz5x%2FAIgGFIS9BWAZARz0LqyJ7CHNwJmMnQMXlEGKZVl8js1KSgqiAQIy%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDAuRaoKd0Id7kdg8NircA6hTsDc%2FeTdi4z9hASPkSDxPgjQ8BjnyjK5PAEaM7oUvc7GveNUobXg%2BN1QhviVH96BwCRPPQogFqS2HGoa8WyTt43QP74TtZshF3HTbqNsncxRY%2F3Cr7QfwxxH4P0F1WzQzCczFNS1jpaJSejYL1bMvhSGAmyCXYBm8tChpFC9%2FqRLbz66VMEXU7zZ6n5rUbbXQqZfC8ELFQemybCKas%2F%2FRmAAuJqmGPO5kZaCWM%2FI2m3P48ztvM1TxYQj1bwl%2B4bblg8IWGCAO3CZMzNYUHPXLTbTjCesvIjt07X%2FEEhz2xBQlxV2ovI%2FtO0YoP%2B9cSg4cbvl0PVMrrPMrFBpkvptwV6tJuJWThrXP2brEsv5N6SAtRYDeAmY6ExjMeHklzWWDYI3kpS8uM%2B7Kv1XvLUt5DACLneSW1z3dSqnTS9zovgekuivMQSb%2FZl4xTRmihuGo6pyaJSJMuObGsPy%2B%2Fxma5yasNxQEd2hLWUaXVDk6Gab50jDTcmx%2FDOY5TyBOObOoqybZfXCwI0NxD0fArfncd2iwxrt0him1vkTjW%2FzEX4tgpecJ%2Fu7ZaP9amwPCw17Tcbb3nEdff4KfUc44GYE3Vnq%2Bik1jyzR1Z5t5%2F2pLtpQ%2F6TM9MCka%2BFUNMM2TusEGOqUBBQwujXQGBN%2B0N42674D559Qv8Q9UOpGZNbjiZ3I5rbXY4TwIL7Nt0oPChONHTNUZbDLSrubFnumm9z5sT%2FgrcAmxjyryGBwQimgD7hx%2FpnisRG1UB7TJH7jSlGXgYEwzn7GaCD%2Bn17NLUE5r%2BZW2cZWncgIDA4DelqmCNoEAWks5u2FkJeGkeXG6NOK5gH1HspveE6x5nSXBYjjSGLNO6bGZNfnI&X-Amz-Signature=e9a1f5de370c5222dcadd4087cd8fe3c813390589e292c505320c8ca232796d8&X-Amz-SignedHeaders=host&x-id=GetObject)

- A protocol for encoding Ethereum addresses to make them **compatible with global financial systems**
- Can encode both Ethereum addresses and human-readable names from the Ethereum Name Registry (ENS)
- Represents addresses in **IBAN format**, improving interoperability and readability

📌 **Analogy:**

> ICAP is like “wrapping” an Ethereum address in an IBAN format — like converting an address into an international bank account number

---

## **📌 7️⃣ Conclusion: The Role of Cryptography in Ethereum**

- All trust in Ethereum is **founded on cryptography**
- The public-key-based system provides both **verifiability and security**
- Combining ECC, hashing, and digital signatures enables a **trustless decentralized system**

📌 **Final Note:**

Ethereum’s security isn’t just about code — it’s **architected on cryptographic principles**.

This foundation ensures **user privacy, system integrity, and ecosystem-wide trust.** 🔐

---

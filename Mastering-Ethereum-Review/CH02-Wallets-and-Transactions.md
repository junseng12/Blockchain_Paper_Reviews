# **📌 CH02: Basics of Ethereum Wallets and Transactions**

Ethereum goes beyond being a simple cryptocurrency — it adopts an **account-based model** as a **smart contract platform**.

At its core are concepts like **wallets, private keys, EOA/CA, and transaction structure**.

---

## **📌 1️⃣ Basic Units and Account Structure in Ethereum**

### **🔹 Ether Units (Ether, Wei)**

- 1 ETH = 10¹⁸ Wei (the smallest unit)
- Transaction and contract execution fees are typically expressed in **Gwei (10⁹ Wei)**

### **🔹 Types of Accounts**

| Type                               | Description                                |
| ---------------------------------- | ------------------------------------------ |
| **EOA (Externally Owned Account)** | An account controlled by a private key     |
| **CA (Contract Account)**          | An account governed by smart contract code |

📌 **Analogy:**

> An EOA is like a person holding a wallet, while a CA is a robot that operates the wallet automatically.  
> A human (EOA) can act directly, whereas a robot (CA) must be externally triggered.

---

## **📌 2️⃣ Concept and Types of Wallets**

### **🔹 What is a Wallet?**

- An Ethereum wallet is not just a storage device — it’s a **private key management system**.
- Private key → Public key → Address creation → Transaction signing

### **💼 Major Wallet Types**

| Wallet Type           | Description                               |
| --------------------- | ----------------------------------------- |
| **Hardware Wallet**   | Offline storage like Ledger, Trezor       |
| **Software Wallet**   | Online wallets like MetaMask, MyCrypto    |
| **Paper Wallet**      | Offline printouts of private key/address  |
| **Browser Extension** | Run directly in browsers (e.g., MetaMask) |

📌 **Analogy:**

> A wallet is like an “automated vault.”  
> You need the key (private key) to access funds. The wallet securely stores and uses the key.

---

## **📌 3️⃣ Using Wallets via MetaMask**

### **🔹 Types of Networks**

- **Mainnet**: Real Ethereum with real value
- **Testnet**: Test environments using free ETH (e.g., Goerli, Sepolia)
- **Localnet**: Local development networks (e.g., Ganache)

📌 Example:

> Tried using the Ropsten testnet, but couldn’t get test ETH due to faucet limits.  
> Nowadays, Goerli and Sepolia are preferred.

---

## **📌 4️⃣ Transaction Structure and Flow**

### **🔹 Example: ETH Transfer Between EOAs**

- Create an EOA → EOA transaction in MetaMask
- Click send → Confirm gas fee → Sign → Broadcast → **Included in block**

### **🔹 Differences with CA**

| Aspect             | EOA                      | CA                                |
| ------------------ | ------------------------ | --------------------------------- |
| Transaction Source | Directly signed and sent | Triggered by external transaction |
| State Changes      | Manual                   | Executed through contract logic   |
| Private Key        | Present                  | Not applicable                    |

📌 **Analogy:**

> An EOA is “a person sending money.”  
> A CA is “an automated responder system” that operates when invoked.

---

## **📌 5️⃣ Transaction Explorer: Etherscan**

- After a transaction is made, Etherscan can show:
  - Transaction hash
  - Sender and receiver addresses
  - Gas used
  - Contract creation
  - Block number, etc.

📌 **Analogy:**

> Etherscan is the “official registry” of the blockchain.  
> Every transaction is recorded and publicly viewable here.

---

## **📌 6️⃣ Conclusion: Wallets and Transactions are the User–Blockchain Interface**

📌 A wallet is not just a storage container for digital assets —  
it’s a **user interface for managing private keys and creating transactions**.

- Distinction between EOA and CA is **core to Ethereum’s execution model**
- MetaMask is **the most widely-used wallet from beginners to advanced developers**
- Understanding the network environment (Mainnet/Testnet/Localnet) is essential for correct usage

🚀 **In Summary:**

Mastering Ethereum wallets is not just about sending tokens —  
it’s about understanding and actively participating in how the blockchain works internally.

---

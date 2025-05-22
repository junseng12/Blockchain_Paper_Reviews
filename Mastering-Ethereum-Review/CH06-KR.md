## 📌 **1. What is a transaction?**

- Ethereum is a single large **state machine**.
- Transactions are the **only way to change the state** and the only means of executing smart contracts in the EVM.
- Only an **external account (EOA)** can create transactions; smart contracts cannot create transactions directly.
- Smart contracts only operate when called by other transactions.
  > 📍 Key Summary
  >
  > - **EOA** → **Transaction** creation

> - **Transaction** → **State** change
> - **State change** → **Contract execution**

---

## 📌 **2. Transaction Structure**

In Ethereum, a transaction is a binary message with the following fields:
| Field | Description |
| ------------- | -------------------------------------------------- |
| **Nonce** | Sequence of transactions sent from each address |
| **Gas Price** | Ether price to be paid per gas unit (unit: wei) |
| **Gas Limit** | Maximum amount of gas that can be paid |
| **Recipient** | Recipient's address (EOA or contract address) |
| **Value** | Amount of Ether to be sent |
| **Data** | Additional data used when calling the contract |
| **v, r, s** | ECDSA values for digital signatures (sender proof) |

- This data is serialized using **RLP encoding**.
- The **From address** is not included because it can be restored from the **v, r, s values**.
<details>
<summary>RLP encoding principle and example</summary>

### 📌 **1. RLP (Recursive Length Prefix) encoding**

RLP encoding is a **serialization method for efficiently storing and transmitting data in Ethereum**. Its purpose is to compress transaction data to take up **minimal space**.

### ✅ **RLP Encoding Principle**

RLP consists of **two main elements**.

1. **Data is a simple single value** (byte string)
2. **Data is a list of multiple values** (array)
   The RLP encoding method differs for each case.

### ✅ **RLP Encoding Method (Step-by-Step)**

**For a single value (Value)**

1. **Numbers in the range 0–127 (1 byte)**
   → Stored as is (e.g., `0x7F` → `0x7F`)
2. **Data in the range 0–55 bytes**
   → `0x80 + data length` + `data` (e.g., `“dog”` → `0x83 646F67`)
3. **Data of 56 bytes or more**
   → `0xB7 + data length (bytes)` + `data`
   **For lists (List)**
4. **Total data is 55 bytes or less**
   → `0xC0 + list length` + `RLP (each element)`
5. **Total data is 56 bytes or more**

## → `0xF7 + list length (bytes)` + `RLP (each element)`

### ✅ **RLP encoding example**

**Example 1: String “dog” (single value)**

1. “dog” → byte conversion → `0x646F67`
2. Length = 3 bytes → `0x80 + 3 = 0x83`
3. Final result = `0x83 646F67`
   **Example 2: List [“cat”, ‘dog’]**
4. “cat” → `0x83636174` (RLP conversion)
5. “dog” → `0x83646F67` (RLP conversion)
6. List length = `0x83636174` + `0x83646F67` = 6 bytes
   → `0xC0 + 6 = 0xC6`
7. Final result: `0xC6 83636174 83646F67`
</details>

---

## 📌 **3. Importance of Nonce**

- Nonce indicates the **order of transactions** and is used to **prevent duplicate transactions**.
- Each account has an independent nonce value (starting from 0 and increasing by 1).

### 🚩 **Example of the necessity of nonce**

- Maintaining transaction order
  ① **Nonce 3:** Transfer 6 Ether (important transaction, sufficient balance)
  ② **Nonce 4:** Transfer 8 Ether (failed due to insufficient balance)

⇒ **Thanks to nonce,** nonce 3 is executed first, and nonce 4 fails, maintaining transaction order.

- Preventing retransmission attacks (duplication prevention)
  Even if the same transaction is copied and retransmitted multiple times, duplicate transactions can be prevented because the nonce is different.

### 🚩 **Nonce precautions**

- If the transaction nonce is empty (missing), subsequent transactions will not be processed and will stop.
- If the same nonce is duplicated, only one will be adopted.

---

## 📌 **4. Role of Gas**

- The unit of measurement for transaction processing costs in Ethereum.
- Gas costs are calculated as follows: **Gas Cost = Gas Price × Gas Used**
- If a transaction exceeds the gas limit, it fails and the state is restored to its original state.

### 🚗 **Understanding with a car analogy**

- **Gas Limit:** The capacity of the fuel tank (maximum usable fuel).
- **Gas Price:** The price per liter of fuel.
- **Gas Used:** The amount of fuel consumed based on the actual distance traveled.

## 📌 5**. Value and Data Fields**

| Transaction Type                  | Value | Data | Description                               |
| --------------------------------- | ----- | ---- | ----------------------------------------- |
| Payment only                      | ✅    | ❌   | Ether only is transferred                 |
| Contract function call only       | ❌    | ✅   | Contract call with data                   |
| Payment and function call         | ✅    | ✅   | Contract call with Ether                  |
| Neither payment nor function call | ❌    | ❌   | (Meaningless transaction that wastes gas) |

---

## 📌 6**. Digital Signature (ECDSA)**

- Transactions are signed using the ECDSA algorithm.
- Signing process:
  ① Transaction data → RLP encoding

② Keccak-256 hash calculation

      ③ ECDSA signature with the signer's private key

④ Add the generated signature value (v, r, s) to the transaction

- Through the signature:
🔹 Proof of ownership
🔹 Prevention of transaction repudiation
🔹 Transaction data integrity assurance
<details>
<summary>**Raw Transaction Creation with EIP-155**</summary>

### **📌 What is EIP-155?**

EIP-155 is an Ethereum Improvement Proposal (EIP) introduced in 2016 to prevent replay attacks.

### **💡 What is a replay attack?**

Previously, Ethereum (ETH) and Ethereum Classic (ETC) shared the same chain, which led to the issue where **a transaction sent on one chain could be executed on the other chain as well**.
For example:

1. A sends a transaction to B transferring 10 ETH on the Ethereum mainnet 💰
2. B copies this transaction and sends it on the Ethereum Classic network 🤯
3. A unintentionally sends 10 ETC to B as well 😱 (since the accounts share the same private key)
👉 To address this issue, **EIP-155 introduced a “chain ID” to transactions**.
👉 Each blockchain is assigned a unique **chain ID**, ensuring that a transaction signed on one network is invalid on another!
<details>
<summary>EIP-55 (Ethereum address checksum, different from EIP-155)</summary>

## **✅ EIP-155 vs EIP-55 Differences**

| EIP         | Concept                                | Role                                                                     | Purpose of introduction                                                                                                                                                     | Example                                                                   |
| ----------- | -------------------------------------- | ------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| **EIP-155** | **Prevent transaction replay**         | **Add chain ID** to distinguish transactions between networks            | **Introduced to prevent replay attacks, where transactions are executed repeatedly on different chains (such as Ethereum and Ethereum Classic) after chains are separated** | _Chain ID:_ _`1`_ _(Ethereum),_ _`61`_ _(Ethereum Classic) etc._          |
| **EIP-55**  | **Address Checksum (typo prevention)** | Adds a **case-sensitive checksum** to Ethereum addresses to detect typos | **Prevents incorrect Ethereum address input, prevent users from accidentally sending funds to the wrong address**                                                           | _`0x52908400098527886E0F7030069857D2E4169EE7`_ _(EIP-55-applied address)_ |

### 📌 **What is EIP-55?**

**EIP-55** is an **address checksum** method for detecting errors in Ethereum addresses.
Ethereum addresses are **20 bytes (160 bits) long, consisting of 40 hexadecimal digits (0**~~**9, A**~~**F)**,
and can be represented using only lowercase or uppercase letters.
✔️ **Issues before EIP-55**

- Ethereum addresses were valid regardless of case sensitivity (i.e., `0xabcd...` and `0xABCD...` are the same address)
- However, typos could result in funds being sent to the wrong address! 😨
  ✔️ **Solution after EIP-55**
- Changed to a **checksum method that converts specific characters in the address to uppercase** to detect typos
- If a user enters an **incorrect address, the wallet software can detect the error**.

---

## **📍 Background of EIP-55 (Why is it necessary?)**

Ethereum's address system, unlike Bitcoin's, used a **pure hexadecimal (hex) format without a checksum**.
In other words, **Ethereum addresses originally had no typo detection functionality**.
For example:
Bitcoin address: `1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa` (with checksum)
Ethereum address: `0x4bbeeb066ed09b7aed07bf39eee0460dfa261520` (no checksum)
💡 **Issues**
✔️ If a user **enters even one character incorrectly**, there is a possibility that the transaction will be sent to a completely different address.
✔️ Most Ethereum wallets use **QR codes** or **copy-paste addresses**,
✔️ but **manual input** carries the risk of typos.
✔️ The Ethereum network has **“no way to reverse a mistaken transaction!”** 😨
💡 **Solution**
✔️ Introduce a method that applies a checksum by **hashing the Ethereum address using Keccak-256**
✔️ Convert the Ethereum address to a **case-sensitive format** to enable **typo detection**.
✔️ Display a warning when an address without a checksum is entered in a wallet or block explorer.

---

## **📍 EIP-55 Checksum Application Method (How Does It Work?)**

### **🚀 1️⃣ Basic Principle**

1. Convert the **hexadecimal representation** of the Ethereum address to **lowercase** (excluding `0x`)
2. Generate a **Keccak-256 hash** (Keccak is the SHA3 hash algorithm used by Ethereum)
3. Use the generated hash value to **convert some characters in the address string to uppercase**

- Look at each byte of the Keccak hash value, and if it is greater than 7, change the corresponding character to uppercase

4. Finally, a **case-mixed checksum address** is generated.

---

### **🚀 2️⃣ Checksum conversion example (Step by Step)**

Example address:

```bash
0x52908400098527886E0F7030069857D2E4169EE7
```

### **✅ Step 1: Convert to lowercase**

```bash
0x52908400098527886e0f7030069857d2e4169ee7
```

### **✅ Step 2: Generate Keccak-256 hash**

Hash result:

```bash
0x1c1d9c3f78f6a23e902b101f81eb4ac69b8c5e1d3d1b6783f373c3a68818c1b1
```

### **✅ Step 3: Change specific characters to uppercase**

- First byte of the Keccak hash: `1C` (hexadecimal 1C = 28)
  → 28 (decimal) → **Keep the first character as lowercase**
- Second byte: `1D` (hexadecimal 1D = 29)
  → 29 (decimal) → **Change the second character to uppercase**
  Resulting final checksum-applied address:

```bash
0x52908400098527886E0F7030069857D2E4169EE7
```

## ✅ Mixed case!

## **📍 Compare with addresses where EIP-55 checksum is not applied**

| Address Type                | Example Address                              |
| --------------------------- | -------------------------------------------- |
| Regular Address (lowercase) | `0x52908400098527886e0f7030069857d2e4169ee7` |
| Checksum Address (EIP-55)   | `0x52908400098527886E0F7030069857D2E4169EE7` |

💡 **Differences**
✔️ **EIP-55 checksum addresses have specific characters in uppercase**
✔️ **Addresses with only lowercase letters cannot detect typos**
✔️ **Using checksum addresses allows you to detect typos** (errors occur if entered incorrectly)

---

## **📍 How to apply EIP-55**

### **🚀 1️⃣ Applying checksums in wallets and block explorers**

- Wallets and block explorers such as Metamask, MyEtherWallet (MEW), and Etherscan consider only addresses with EIP-55 checksums as valid.
- If users enter incorrect uppercase or lowercase letters, an error message will be displayed! 🚨

### **🚀 2️⃣ Checking the checksum in smart contracts**

- You can verify that the checksum is correct using `keccak256` in Solidity:

```solidity
function validateAddress(string memory _input) public pure returns (bool) {

return keccak256(abi.encodePacked(_input)) == keccak256(abi.encodePacked(“0x52908400098527886E0F7030069857D2E4169EE7”));
}
```

## ✔️ You can also check the validity of addresses in Ethereum smart contracts!

## **📍 What happens if you enter an address without a checksum?**

**In systems that apply EIP-55, entering an address without a checksum will result in an error!**
For example:

1. Enter an address with incorrect capitalization in Metamask
2. Metamask **checks the Keccak-256 hash** and verifies its validity
3. **Error message displayed!** → “The address is invalid.”

---

## **📍 Limitations of EIP-55**

✔️ EIP-55 can **detect typos but does not correct them**
✔️ **Software that only recognizes addresses with checksums may recognize addresses without checksums as errors**
✔️ **If you mainly use QR code scanning or copy-paste, the checksum feature may not be necessary**

---

## **🚀 Summary**

### **🔹 Key points of EIP-55**

✅ **Adds typo detection functionality for Ethereum addresses**
✅ **Converts specific characters to uppercase using Keccak-256 hashing**
✅ **Allows prevention of typos when using addresses with mixed case**
✅ **Allows only addresses with checksums to be accepted in wallets and block explorers**

---

### **🔹 Benefits of implementing EIP-55**

✔️ **Prevents typos when manually entering addresses**
✔️ **Wallets automatically detect errors when incorrect addresses are entered**
✔️ **Does not resolve security issues such as replay attacks, but prevents mistakes when sending transactions**

---

📌 **EIP-55 does not protect transactions; it reduces “address input errors”!**
📌 **Most wallets and block explorers in the Ethereum ecosystem have implemented the EIP-55 checksum!** ✅

## </details>

### **📌 Process of creating a raw transaction with EIP-155**

Let's take a step-by-step look at how to create a transaction using the EIP-155 method.

### **📍 Step 1: Transaction Data Configuration**

When applying EIP-155, the following is added to the existing transaction structure: **“chainId”, “0”, ‘0’**.
Existing structure:

```json
{
  “nonce”: 0,

“gasPrice”: “0x09184e72a000”, // 10 Gwei
  “gasLimit”: “0x30000”, // 200,000 Gas
  “to”: “0xrecipient_address”,
  “value”: “0x01”, // 1 wei
  ‘data’: “” // None, as this is a standard ETH transfer
}
```

🚨 **After applying EIP-155**

```json
{
  “nonce”: 0,
  “gasPrice”: “0x09184e72a000”,
  “gasLimit”: “0x30000”,
  ‘to’: “0xrecipient_address”,

“value”: “0x01”,
  “data”: “”,
  “chainId”: 1, // Ethereum mainnet chain ID
  “0”: 0,
  “0”: 0
}
```

✔️ **Added chain ID**
✔️ **Added ‘0’, “0” fields**

---

### **📍 Step 2: Sign the transaction**

After **RLP-encoding** the transaction data, you must apply the Keccak-256 hash to the value and sign it.
👉 **Signing method**

1. RLP-encode the transaction created above
2. Apply Keccak-256 hashing
3. Generate the v, r, and s signatures using **ECDSA signing**

- The v value is changed to **“chainId \* 2 + 35 or 36”** (EIP-155 applied)
  - Example: `v = (1 * 2) + 35 = 37`

---

### **📍 Step 3: Send the signed transaction**

Send the signed transaction to the Ethereum network!

```bash
const Web3 = require(“web3”);
const EthereumTx = require(“ethereumjs-tx”).Transaction;
const web3 = new Web3(“https://mainnet.infura.io/v3/YOUR_INFURA_PROJECT_ID”);
const rawTx = {
    nonce: web3.utils.toHex(0),

gasPrice: web3.utils.toHex(web3.utils.toWei(“10”, ‘gwei’)),
    gasLimit: web3.utils.toHex(21000),
to: “0xRecipientAddress”,

value: web3.utils.toHex(web3.utils.toWei(“0.1”, “ether”)),
    chainId: 1  // EIP-155 적용
};
const privateKey = Buffer.from(‘YOUR_PRIVATE_KEY’, “hex”);
const tx = new EthereumTx(rawTx, { chain: “mainnet” });
tx.sign(privateKey);
const serializedTx = tx.serialize();
web3.eth.sendSignedTransaction(“0x” + serializedTx.toString(‘hex’))
.on(“receipt”, console.log);
```

✔️ **EIP-155 applied**
✔️ **Includes chain ID → Prevents replay attacks**
✔️ **Sign and send**

---

### **📌 🚀 Easy-to-understand analogy**

🔗 **Before EIP-155**
➡️ “A package sent from Seoul is still valid in Busan” (executed on other chains)
🔗 **After EIP-155**
➡️ “A tag saying ‘Republic of Korea’ is attached to the package so that it is not valid in the United States!” (Distinguishes between networks)

## </details>

## 📌 7**. Offline Signing**

- A method of separating transaction creation and signing.
- Used to minimize the risk of exposing private keys.
  | Step | Description |
  | ---- | -------------------------------------- |
  | ① | Create an unsigned transaction on an online computer |
  | ② | Transfer to an offline computer and sign |
  | ③ | Transfer the signed transaction back online |
  | ④ | Send the signed transaction to the network |

## 📌 8**. Multi-Signature**

- A transaction method that requires multiple signatures.
- Can be implemented as a **contract**.
- Example: Ether can only be transferred if 2 out of 3 signers sign (2-of-3).

# **📌 CH05: Ethereum Wallet Architecture**

In Ethereum, a **wallet** can refer to several things, but it generally means a software application that allows users to interact with the Ethereum network.

A wallet manages private keys, generates addresses, tracks balances, and creates and signs transactions. Some wallets can also interact with **ERC-20 tokens and smart contracts**.

**Examples: Wallets supporting ERC-20 tokens and smart contracts (each has different features and support scopes)**

- **Wallets optimized for DApp usage** → MetaMask, Trust Wallet
- **Wallets powerful for smart contract execution** → MyEtherWallet, MyCrypto
- **For secure hardware environments** → Ledger, Trezor
- **For mobile convenience** → Trust Wallet, Klip

### **💡 Key Concept**

- Ethereum wallets **do not actually store ETH or tokens.**
  → All assets are stored on the **blockchain**, and wallets are just tools to manage **private keys**.
- Using a wallet proves **ownership** and enables **transaction signing**, making asset transfers possible.

---

## **Types of Ethereum Wallets**

Wallets are classified based on how they manage **private keys**.

### **1. Nondeterministic Wallet (JBOK)**

### **✅ JBOK (Just a Bunch of Keys)**

→ Each key is generated **randomly** and is unrelated to the others.

- Cons: Every new address requires **individual backup**, which is difficult to manage.
- Rarely used today — **HD wallets are preferred**.

### **📌 Keystore File (JSON)**

- One of the most used formats in nondeterministic wallets.
- Private key is stored in a JSON file **encrypted with AES-128**.
- Additional security: **KDF (Key Derivation Function)** is applied to defend against password cracking.

---

### **2. Deterministic Wallet**

- **All keys are derived from a single master seed.**
- Backing up just one **seed** allows the recovery of all keys → easier to manage.
- Most modern wallets use **deterministic (HD) structure**.

### **✅ HD Wallet (Hierarchical Deterministic, BIP-32)**

- Keys are generated in a tree structure according to the **BIP-32 standard**.
- Multiple keys can be generated from a single seed, allowing multiple addresses.
- Hierarchical structure enables **separation of personal, business, and departmental accounts**.

### **📌 Advantages of HD Wallets**

1. **Easy backup** → Save just one seed to recover all keys.
2. **New address generation** → Improves privacy.
3. **Deposit possible using only public keys** → Reduces hacking risk.

---

## **HD Wallet Structure (BIP-44)**

- **BIP-44 extends BIP-32 to support multiple coins and accounts.**
- Uses a tree structure to manage different cryptocurrencies.

**Example HD wallet derivation path:**

```plain text
m / purpose' / coin_type' / account' / change / address_index
```

Examples:

- **m/44'/60'/0'/0/0** → First address of the first Ethereum account.
- **m/44'/60'/1'/0/0** → First address of the second Ethereum account.

### **📌 Key Parameters**

- `purpose'`: Always **44'** (for BIP-44 standard)
- `coin_type'`: **60'** for Ethereum, **0'** for Bitcoin
- `account'`: Distinguishes user accounts
- `change`: 0 for receiving, 1 for change (Ethereum typically uses 0)
- `address_index`: Sequential index of generated addresses

---

### **Mnemonic Code Words (BIP-39)**

A word sequence encoding the random number (entropy) used as the seed for deterministic wallets.

**1. Generating Mnemonic Words**

Mnemonic words are generated automatically by wallets using a standardized BIP-39 process. Starting with entropy, a checksum is added, and then it is mapped to words from a predefined list.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c2ba559c-cb6d-4c61-bec3-1760fafc9a92/006a8121-ba79-47e5-b726-4e8ae2c868c6/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667CR47CBJ%2F20250521%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250521T215848Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEA4aCXVzLXdlc3QtMiJGMEQCIBgVA9MBtvdBuxqn1DRPIBussNYVh7Gq0ABZAWSBi3KHAiAlY34d0bXN%2Bpy26ZSqq6aWeACPAPsh%2BDYUt813NklneCqIBAjG%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMPb4sKve7oml8TmAUKtwDsmv5OnL3zgdOZWrQc2LyAs7LjRmYx6QXFOCExRgkPCbqEpiLHZYQ%2BcPzq8Nbunu48XP3eDNgYXle02fe%2Bug841OadDAIZRzPW7jJ04vThh%2BPbocXeCkMN2q0Ei1fzaQ2Hy%2BS9QRTr1Vtk3QmhdL%2FzRszNy87AyHc46Dc99tPkag6fefdyTLoaOcZDh%2BBjpqAPwJSeZ6SYWU1BlWpNI2ThTL4CO%2BoG%2BbGCJQ%2F2mXQksASTzFFepSzSiKHoS3KzABYtjDwiXQFQruHIT0zDKkv9O5ABMujXhKB8kzSysb5kkxOrepA4XUmgHvUljbhf2YHxhHcTcsxU1BnwApCZoHEtQY%2BfWc23%2BspSvGlVXqeTHaW9IZfoXH2UYYYSiVft0Qa2iwIPWHQPeGaRbf4dMm4wnNM6gAeywT%2BmbfO5jLLDSXFm%2FP7O3gRkA5gTeRkx0etFpnOlVBbyi3Jxk5U%2BrtH0pKsykuS3Dr1ccbHVnD3cTuNBHXHQcq9Wa%2Bg%2BSOqK8rwU3r304kT55r%2B2sIe2TQxmKxOfEHftjsqXR8F2QWiJNZ5ydUEpvAOcWIql1PHmGCW01eRkwGfH6D3V9N23M21lXRVQ7wVhYxVtgbHWEMe97p%2FkDzN86Ap%2FvK36FowzIa5wQY6pgEdISU4lNECWTL3bCsDcy3UxNL7Jv4WEfJ4n3DsZDnAW71xvoshZcRh8LI%2BhbmT%2F5xgUpZ1CRgZD3agZ55ZAUmaVTmRN6NDGCGtQncteSq4%2F0q%2F8D2nfrbQMcfzmnVWkQjQaTyPO0GIgX70fCrTt3VUqDZT6H4hbjn4s%2Fzp0mrm8FDPQ80PSY%2BYVkHPszajY94QJh3vj4P2%2Bm1YbKYJD85BR%2Be7Rhq5&X-Amz-Signature=68deafb9fb04c7f01398764cde3d48c02f146e06e2bc434c348a5f3d984e2b94&X-Amz-SignedHeaders=host&x-id=GetObject)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c2ba559c-cb6d-4c61-bec3-1760fafc9a92/30b010c8-c4d7-4f39-8916-cfa321e5bf39/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665QEVP3H3%2F20250521%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250521T215849Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEA4aCXVzLXdlc3QtMiJIMEYCIQC4hJhswgMnu3RL%2F%2FlRcjj%2FpwYi3XmtHjwo69XC1rfruQIhAKaw14yLzeqtyirgeIIJ%2Bd0ynDGc2A6AMxMSBFIE6xicKogECMf%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igyoyd%2Fp%2FLbVXk36E10q3APxynshs7fUiEbtCR19YmlUbC8oX2PVyMZQD%2FGPc0lI4wcxJK6KvR7J0LSxUY5yCLIvl92o9mShWeYGHsKRl0b1jp1VHaFXxx8rs7Urt3Zfj3fmnl7qKg2GUdSds3A%2B0nPqh0yYLw%2FIE2y0AJO9J8XxNmHeVwZJIRDG3w0t4wtT9264FP1Lpm32BSAyj3paXhtmDbILa964euFVvPDzqEYVo0qyFuIWcWfFddHF%2FyibTIQl71LB3jTYuoX6VNUGheH8VUK6JFroyJvo1ss9uk1e42iaFgWNWTrbt32g5R91FcbI78%2BIgBSVEMFjp2%2FfeuCFPNeRAoe2WBr1mC1bt9VOKr5k5%2BMCoEeBzlMVAcWGoKtPn8ijyZGdKldsoA%2BMtaM3ydKtoAMrRHY0wIQuXsINl6Q8cOk%2FmKJjZbFbq5tal%2F2Q35DP2Y8mjx9%2BpRhdCSr8HEgKPQOYHZj1SNGpxygwltN4x6GdbMY80z0hzaC3PPrlM6Waps8Q5j1BnCrFlsYgGx4nSTWIlXysaB64nhyx5J3AlJzV05kOmdoZqMF%2FNA5Zj8DMuJa278geDpQivBVaj8mW%2BpREMtUYwejLDAJIoRiObeqt7DWgeVxg7PHeiq1038FWVLlbrEretDCGmLnBBjqkAQyQKNRtOdvcPqjCkJrbYu%2FptAeC3L5QcXn9BJuoI3jjpoZFDnkg%2FV94M8ROcb2DwbphsXqqiY%2BkpvTQWJdeMnecxFW9n0O34Zy1cZCyG9P%2BP7LlnrCf4L8M%2FDC4K%2B6RUGiipH6ZXL8jarPpMNaWy2SzRKhNkIp33YAjrxbxHwig66thrXWHkaUYThohS49eDLKlkBnTA0gwK9wSZBRUkfwAShHN&X-Amz-Signature=3806e21f31cfa032a617c1dee9c9fc7082dfc2032fdc4492a9f52fcf5aa88a4c&X-Amz-SignedHeaders=host&x-id=GetObject)

1. Generate a 128-bit to 256-bit encrypted random sequence S.
2. Generate a checksum of S by calculating the length of the first SHA-256 hash value of S ÷ 32 bits of S.
3. Append the checksum to the end of the random sequence S.
4. Divide the sequence-checksum concatenation into 11-bit sections.
5. Map each 11-bit value to a word in a predefined dictionary of 2,048 words.
6. Create a mnemonic code from the word sequence while maintaining the order of the words.

**2. Mnemonic ⇒ Seed**

The mnemonic word represents an entropy of 128 to 256 bits. The entropy is then used to derive a longer (512 bit) seed using the key-stretching function PBKDF2. The generated seed is used to build a deterministic wallet and derive keys.

The key-stretching function takes two parameters: **mnemonic** and **_salt_**.

**- Purpose of Salt**

To make it difficult to build a lookup table that allows brute force attacks.

To enable the introduction of a passphrase that acts as an additional security element to protect the seed.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c2ba559c-cb6d-4c61-bec3-1760fafc9a92/61d2e987-6bb1-4ab6-8a5f-be44b0b23c24/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662CMHEVGR%2F20250521%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250521T215848Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEA4aCXVzLXdlc3QtMiJHMEUCIBpggiiC5GluA%2Fkwwg%2B%2Fh%2B%2F%2FA01XB1oYX4PM7Q%2Fnty9AAiEA%2B7tmNijh4mgIIZ3LjGfUp3t1nsV4H47jX5KY8VlJqUcqiAQIxv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDKwipd2A%2F%2BBdODdErircA%2F7R3rl%2BFsjGsp152aj4mgFhCOAGali8TC%2FsXS%2BMD%2FkAkfiZscsIQRBXOwyL6ArcKnGsN3I4apk6r6br2%2BwjB93tulHHnytFi4mQdrf3A0kPen8Ql%2B88zdnS8r8f5RTLQUP3GS2uR%2FbGJ78%2FFLB3hVYtXgTacu7lhDcD%2F3o00mJ4%2BB%2BgTyVxgHDij0qAjUoDuypMWqtwWTcv0TwHHaCc%2Fptl1EQDcgerlGuGDiSSklInM%2FlOtgWAdWvcWC8b2ljvMaWV3H1GvBrAYLfvQK3OMjaaQumtj3JxqhA7WAqq6OOoF%2BXRHfvidAp2e%2F4rAZxcTiIkoqW04s0jr81AloUtFphr1YVYdFfLg2eeqQztX3jxffjqwHcmu5IrZl36tjtyRHNhFBr2EknMUTeWh8a%2FqNOfR7jorLWrC%2Fc23TG5KRc60rPYQ8M6KJC6gSSzrqAiE931stvTYC8%2Bic74PXgSAAr5e9cUv5neuSIckoCbS1YdbpNHdJ7tY6qzDb2ISED1OFOzV8dcQy0dpkL6yiCqcDwZwrzH2QBJl1ucR8MERmViTRhvFzuB%2FHU0rPcSo9FfAFr%2B9vadj0ZpFGX3ek%2F77v9icjBGO%2BKIgGmKS%2BpWiYNrpWW0zmLvKkrFXzVvMOKGucEGOqUB4R78kRGHO3bFaeWgSUK1lw3xZB9spTty5OOot8L%2F4OezKc8DWRawl6J6rTov%2BtqVdz0C05FzWPwXNPuE%2BKzpoGgGumCYJ%2FOX70Qu90h%2Fy46Nc7eX7O1lFyMFat9BAGOZYMRnnKXV3CzDYhYgmOr56ya0P%2B6jB%2FqGbIyYMTnGmKblofCq0r3Vx3ReWzq6LP964hBYRMANl1aXijpt%2FKUJYcEeSiGL&X-Amz-Signature=dcaa672c549033c130151879eaef05475da134f7f5df2d4726b18bf39fdf2036&X-Amz-SignedHeaders=host&x-id=GetObject)

**-Continuing the process described in the previous section**

7. The first parameter to the PBKDF2 key stretching function is the _mnemonic_ generated in step 6.\*
8. The second parameter to the PBKDF2 key stretching function is _salt_. The salt consists of the string constant "mnemonic" concatenated with an optional user-supplied passphrase.
9. PBKDF2 uses the HMAC-SHA512 algorithm to stretch the mnemonic and salt parameters using 2,048 rounds of hashing to produce a 512-bit value as the final output. This 512-bit value is the seed.

---

## **Extended Keys**

- **Extended Public Key (xpub)**: Can generate all public addresses.
- **Extended Private Key (xprv)**: Manages the entire wallet’s private keys.
- **xpub can be stored on servers without risking funds**, although transaction history may be exposed.

### **📌 Comparison of xpub vs xprv**

|               | **Extended Public Key (xpub)**      | **Extended Private Key (xprv)**                     |
| ------------- | ----------------------------------- | --------------------------------------------------- |
| **Purpose**   | Generate multiple public addresses  | Manage and sign with all private keys               |
| **Analogy**   | “Account number issuing system”     | “Master PIN number” to withdraw from all accounts   |
| **Storage**   | Can be stored online ✅             | Must never be stored online ❌ (use offline backup) |
| **Hack Risk** | Reveals history, but funds are safe | Entire wallet can be drained if exposed             |

---

## **📌 Wallet Security and Best Practices**

- Use wallets compliant with **BIP-32, BIP-39, and BIP-44** standards.
- **Backup your mnemonic phrase** and store it safely (never digitally).
- Use **hardware wallets** (Ledger, Trezor) for enhanced security.
- You can generate safe receiving addresses using **xpub**.

---

## **✅ Conclusion**

1. A **wallet manages private keys**, while actual ETH is stored on the blockchain.
2. **HD wallets (BIP-32/BIP-44)** are essential for both management and security.
3. **Mnemonic codes (BIP-39)** are the most secure backup method.
4. Using **xpub/xprv** improves usability and security.
5. **Passphrase adds an extra security layer** on top of mnemonic.

---

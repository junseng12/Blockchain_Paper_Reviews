## 📌 **Token Concept Summary**

### 🔹 **Definition of Token**

- The word “token” originally comes from the Old English word “tācen,” which means ‘sign’ or “symbol.”
- Traditionally, it referred to physical tokens with a specific purpose (e.g., transportation tokens, laundry tokens, arcade tokens), which were originally **objects with little intrinsic value**.
- However, **blockchain-based digital tokens** have redefined this concept, evolving into a concept that can represent **assets, currency, access rights**, and more.

### 🔹 **Differences between traditional physical tokens and blockchain tokens**

| Item            | Physical tokens                                  | Blockchain tokens                                  |
| --------------- | ------------------------------------------------ | -------------------------------------------------- |
| Scope of use    | Can only be used in specific locations/companies | Can be used in the global market                   |
| Exchangeability | Mostly non-exchangeable                          | Can be exchanged for other tokens or currency      |
| Value           | Limited use results in low value                 | Multiple functions and liquidity enable high value |

---

## 📌 **Key use cases for tokens**

- **Digital currency**: The most common use case, functioning like money. (e.g., BTC, ETH)
- **Resource**: Represents resources such as computing power or storage space that can be used in the sharing economy.
- **Asset**: Represents ownership of real estate, gold, stocks, art, etc.
- **Access**: Grants access to specific services, websites, hotel rooms, etc.
- **Equity**: Represents ownership of a company or a DAO (Decentralized Autonomous Organization).
- **Voting**: Provides voting rights in on-chain governance.
- **Collectibles**: NFT digital art collectibles such as CryptoPunks.
- **Identity**: Represents identity information such as online avatars or national ID cards.
- **Attestation**: Serves as proof of credentials such as degrees or birth certificates.
- **Utility**: Used for accessing services.
  ➡️ **Blockchain tokens can perform multiple functions.**
  Example: Driver's license = Identity + Access + Attestation

---

## 📌 **Types of tokens**

### 🔹 **1️⃣ Fungibility**

- **Fungible**: Specific units can be exchanged for one another and retain the same value.
- Example: Fiat currency (USD, EUR), BTC, ETH, ERC-20 tokens
- **Non-fungible**: Each unit is unique and cannot be exchanged for another.
- Example: Artwork, real estate, NFT (ERC-721, ERC-1155)

### 🔹 **2️⃣ Intrinsic Value**

- **Intrinsic Tokens**: Assets that exist independently within the blockchain.
- Examples: ETH, NFT (on-chain storage)
- **No additional intermediaries required → No counterparty risk**
- **Extrinsic Tokens**: Tokens representing physical assets.
- Example: Tokens representing gold, real estate equity tokens
- **Requires trust in an external custodian → Counterparty risk**

---

## 📌 **Token Usage**

### 🔹 **1️⃣ Utility Tokens**

- Tokens used to access specific services or functions.
- Example: Filecoin (FIL) for purchasing file storage space, in-game item purchases.

### 🔹 **2️⃣ Equity Tokens**

- Tokens representing shares in a company or DAO (Decentralized Autonomous Organization).
- Examples: Security tokens (similar to stocks), DAO governance tokens.

### 🛑 **Important Note: Securities Laws and Regulatory Risks**

- Some projects attempt to **raise funds by disguising equity tokens as utility tokens.**
- However, as the saying goes, “If it looks like a duck and sounds like a duck, it's probably a duck,” regulatory authorities are likely to classify them as securities.

---

## 📌 **Ethereum Tokens**

### 🔹 **Difference between Ethereum and tokens**

| Category               | Ether (ETH)       | Ethereum Tokens (ERC-20, etc.)       |
| ---------------------- | ----------------- | ------------------------------------ |
| Blockchain Native      | O                 | X (requires smart contracts)         |
| Protocol-level Support | O                 | X                                    |
| Inter-account Transfer | Directly possible | Only possible within smart contracts |

➡️ **A smart contract is required to create a token.**
➡️ **Following the ERC standard improves compatibility and usability.**

---

## 📌 **ERC-20 Standard (Interchangeable Tokens)**

### 🔹 **Required Functions**

- `totalSupply()`: Returns the total token supply
- `balanceOf(address)`: Checks the balance of a specific address
- `transfer(address, uint256)`: Transfers tokens to a specific address
- `transferFrom(address, address, uint256)`: Transfers tokens from a delegated account
- `approve(address, uint256)`: Grants a delegated account permission to use a certain amount of tokens
- `allowance(address, address)`: Check the amount of tokens the authorized account can use

### 🔹 **Complementary Standards**

- **ERC-223**: Prevent loss by verifying whether a smart contract can receive tokens
- **ERC-777**: ERC-20 improvement, adds `send()` functionality
- **ERC-721 (NFT)**: Standard for representing non-fungible assets
- **ERC-1155**: Multi-token standard (mix of fungible and non-fungible tokens)

---

## 📌 **Limitations of ERC-20**

1️⃣ **Permanent loss of tokens if sent to the wrong smart contract address**
2️⃣ **When transferring tokens, only the “token contract DB” is changed, not the “actual address ownership status”**
3️⃣ **Gas must be paid in ETH when transferring tokens (gas fees cannot be paid with tokens themselves)**

<summary>Transfer VS. Allowance, TransferFrom in ERC-20</summary>

### **1️⃣ Fundamental differences between ETH & BTC and ERC-20 tokens**

✅ **ETH & BTC → Managed directly at the network level**
✅ **ERC-20 → Managed by a specific smart contract (token contract)**

### **🔹 1. How ETH and BTC work**

- ETH and BTC are the **basic assets** of the blockchain.
- They are **managed by the blockchain itself**, and their balances are tracked by address.
- **Transfers are made directly from the sender to the recipient.**
- **Each wallet (account) directly holds the assets.**
  🚀 **In other words, ETH and BTC are native coins managed directly by the blockchain without separate smart contracts!**

---

### **🔹 2. How ERC-20 tokens work**

- ERC-20 tokens are managed by **separate smart contracts**.
- They are not managed directly by the blockchain like ETH.
- Wallets do not hold ERC-20 tokens; instead, **“ERC-20 token contracts store information about who holds how much.”**
- **In other words, the actual ownership information of tokens is managed within the token contract, not across the entire blockchain.**
  📌 **Key differences**
- **ETH manages account balances directly on the blockchain.**
- **ERC-20 tokens manage account balances within the token contract**
- **In other words, owning a token means that it is “recorded in the contract's database”!**
  Now let's understand why permission mechanisms such as `approve()` and `transferFrom()` are necessary.

---

### **2️⃣ Why ERC-20 tokens use permission (approve) methods**

✅ **ETH transfer method:**

- ETH **manages balances on the blockchain itself**, so **the sender can transfer directly**.
- Example: `msg.sender.transfer(1 ETH);` → Transfer possible immediately.
  ✅ **ERC-20 transfer method:**
- ERC-20 is not a blockchain; **the token contract manages ownership**, so to send tokens, you must **instruct the token contract to “send this amount from this address to that address.”**
- Example: `ERC20Token.transfer(to, amount);`

---

### **3️⃣ Why is the “approve & transferFrom” method necessary?**

ERC-20 tokens can be transferred in two ways.

### **(1) Direct transfer (transfer)**

```solidity
function transfer(address to, uint256 amount) public returns (bool);
```

📌 **How it works:**

- This is the method where I directly send my tokens to another address.
- Example: `ERC20Token.transfer(0xBBB, 100); // Send 100 tokens`
- This method is suitable for **general user-to-user transactions.**

### **(2) Approve & Transfer From**

```solidity
function approve(address spender, uint256 amount) public returns (bool);
function transferFrom(address from, address to, uint256 amount) public returns (bool);
```

📌 **Why this method is needed:**

- When someone else needs to send tokens instead of the user, **the smart contract must send them.**
- For example, when managing tokens directly in **exchanges, DeFi services, or automated payment systems**.
- Using this method, **even if you don't send the tokens yourself, the approved address (contract) can send your tokens on your behalf.**

---

### **4️⃣ Example: “ERC-20 Tokens and Exchanges”**

**✔️ Consider the process of depositing an ERC-20 token into an exchange (e.g., Uniswap, Binance).**

### **(❌)** **Why `transfer()` alone is insufficient**

- You can send tokens to the exchange address using `transfer()`.
- However, the exchange has no way to verify that the tokens you sent belong to you.
- Since exchanges manage tokens via smart contracts, they need the ability to retrieve tokens directly from my wallet.

### **(✅)** **Using `approve()`\*\*** and\*\* **`transferFrom()`\*\***

1️⃣ Call `approve(spender, amount)`

- I give the exchange contract permission to use up to 100 of my tokens.

```solidity
ERC20Token.approve(exchangeContract, 100);
```

- In other words, **I allow the exchange contract to take up to 100 tokens from my wallet.**
  2️⃣ The exchange contract executes `transferFrom(owner, to, amount)`
- When a user deposits tokens on the exchange, the exchange contract directly takes them from my wallet.

```solidity
ERC20Token.transferFrom(userAddress, exchangeAddress, 100);
```

- **This way, even if the user doesn't send it directly, the exchange contract can automatically manage the tokens!** 🚀

---

### **5️⃣ Final Summary**

✅ **ETH is managed by the blockchain itself, so you can simply use **`transfer()`\*\* **!**
✅ **ERC-20 tokens are managed by a specific smart contract, so you need to manipulate the balance within the contract.**
✅ **There are two ways to send tokens:** **`transfer()`** **and** **`approve()`** **&** **`transferFrom()`** **, where the contract sends the tokens on your behalf.**
✅ **To automatically withdraw tokens from services like exchanges or DeFi, you need the `approve()` and `transferFrom()` methods!**
👉 **In other words, ERC-20 tokens use this method because it allows other contracts or exchanges to manage tokens on behalf of users without requiring them to send tokens directly.** 🚀

## 📌 **ERC-20 Improvements**

### **✅ ERC223 (Resolves issues with transferring tokens to smart contracts)**

- Added a feature to verify if a contract is a smart contract → Prevents accidental loss of tokens.
- Uses the `tokenFallback()` function to prevent tokens from being sent to contracts that cannot receive them.

### **✅ ERC777 (Extension of ERC20)**

- Compatible with ERC20 while adding the `send()` function to enable easy transfer like ETH.
- Supports the `tokensReceived()` function to prevent tokens from being sent to contracts that cannot receive them.
- Provides **additional metadata functionality** (userData, operatorData) → usable by businesses and DApps.

### **✅ ERC721 (NFT, Non-Fungible Tokens)**

- ERC20 tokens are all **identical in value (fungible)**
- ERC721 tokens are **unique and non-fungible** (non-interchangeable)
- Mainly used to represent unique assets such as **game items, digital art, and real estate ownership**.

---

## 📌 **Why extend the ERC20 token standard?**

- **The basic ERC20 standard only supports simple transfer functionality** → Token standards with additional features emerged.
- **Key extension features**
- 🔹 **Whitelist & Blacklist** (Allows token transfers only to specific users)
- 🔹 **Burning functionality** (Reduces the token supply)
- 🔹 **Token minting** (issuing new tokens)
- 🔹 **Crowdfunding functionality** (used in ICOs and IDOs)
- 🔹 **Voting functionality** (used for governance in DAOs)

---

## 📌 **ERC20 and ICO (Initial Coin Offering)**

- ERC20 tokens have grown exponentially as a **fundraising tool** in ICOs (Initial Coin Offerings).
- However, **many ICOs have been operated as scams or Ponzi schemes.**
- Regulatory authorities are increasingly likely to classify ERC20 as a **“security”** → increased legal risks.
- Currently, **models such as IDO (Initial DEX Offering) and IEO (Initial Exchange Offering) are emerging as alternatives to ICOs.**

---

### **📌 What does the issuance of on-chain voting rights through DAO mean?**

To understand this concept, it is helpful to compare **the traditional stock system** with **the DAO-based on-chain voting system.**

---

### **🔹 1️⃣ Traditional stock system (based on securities firms and regulations)**

📌 **What are stocks?**
✅ Stocks are securities issued by companies that represent ownership of the company.
✅ **Ownership must be guaranteed by a central authority (securities firm, government, etc.)**.
✅ **All activities such as stock trading, exercising voting rights, and receiving dividends are processed by intermediaries (brokerage firms, companies, regulations).**
📍 **The process of owning stocks in the traditional system**
1️⃣ When you buy Tesla stock, a brokerage firm (e.g., Samsung Securities) records it in your account.
2️⃣ The brokerage firm manages this information in conjunction with the NASDAQ exchange and the company (Tesla).
3️⃣ To sell shares or receive dividends, you must go through multiple intermediaries such as brokerage firms, financial institutions, and exchanges.
4️⃣ In other words, you do not directly manage the shares; instead, a central authority manages ownership on your behalf.
⚠ **Result: Even if you own stocks, you don't have direct control over them!**
👉 You must trust the brokerage firm and the financial system to protect your stocks.
👉 If the government halts trading of specific stocks or a company is delisted, you cannot use your stocks.

---

### **🔹 2️⃣ What is on-chain voting rights issuance through a DAO?**

📌 **What is a DAO (Decentralized Autonomous Organization)?**
✅ **An organization operated through blockchain smart contracts without a central authority**
✅ **Issues blockchain-based “on-chain voting rights (governance tokens)” instead of stocks to manage shares**
✅ **Smart contracts, not the company, automatically handle voting rights, equity, and dividends**
📍 **The process of managing shares in a DAO**
1️⃣ You purchase **governance tokens (on-chain voting rights)** issued by the DAO.
2️⃣ These tokens are recorded on the blockchain, so **ownership of equity is proven without approval from a securities firm or government**.
3️⃣ By holding these tokens, you can **directly vote on decisions made by the DAO** (e.g., changes to company policies, dividend payments, etc.).
4️⃣ Voting results are **immediately executed by smart contracts**, which either change policies or automatically distribute dividends.
5️⃣ You can **sell your governance tokens directly to others via P2P transactions at any time**.
📌 **Key difference: No intermediaries → Your private key is your ownership!**
✅ Without a brokerage firm or government, your wallet address (private key ownership) serves as **proof of ownership**.
✅ The DAO manages **ownership and voting rights through blockchain smart contracts**, eliminating the need for intermediaries.
✅ In other words, **I am the owner of the shares with my private key, and I can exercise all rights directly**.

---

### **🔹 3️⃣ Analogy: Traditional stocks vs. on-chain voting rights**

| Category                 | Traditional stock system (brokerage-based)                   | DAO-based on-chain voting rights                 |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------------------ |
| **Ownership Management** | Brokerage firm (Samsung Securities, Kiwoom Securities, etc.) | Blockchain smart contract                        |
| **Trading Method**       | Brokerage through a stock exchange (Nasdaq, KOSPI)           | Direct trading through P2P or DEX                |
| **Voting Method**        | Shareholders' meeting (schedule adjusted by the company)     | Immediate execution through DAO's smart contract |
| **Dividend Payment**     | Dividends paid according to the company's schedule           | Automatically paid by smart contracts            |
| **Regulatory Impact**    | Governed by financial regulations and laws                   | Operated autonomously on the blockchain network  |
| **Accessibility**        | Securities account required                                  | Anyone can create a wallet and participate       |

---

### 📌 **Staking & earning interest in DeFi (Decentralized Finance)**

**🔹Key points**
You can deposit ERC-20 tokens on a DeFi (Decentralized Finance) platform and earn interest.
✅ **Deposit process:**

- For example, let's say you stake (deposit) your ERC-20 tokens on a DeFi platform like AAVE.
- At this point, you are not **“sending your tokens to the AAVE contract,” but rather changing the internal data of the contract so that AAVE manages your balance on your behalf.**
- The AAVE contract records that it holds your tokens until you withdraw them.
  ✅ **Interest Payment:**
- While your tokens are staked, AAVE updates the contract data by adding 0.1% interest to your account daily.
- In essence, **the concept of interest is merely “manipulating contract data.”**
  ✅ **Withdrawal:**
- When you withdraw from AAVE, the AAVE contract **updates your ERC-20 balance back to your address.**
  👉 **Ultimately, all DeFi transactions are just “manipulation of data within an ERC-20 contract”!**

<summary>AAVE Principles</summary>

### **📌 Key Summary for Understanding AAVE**

1️⃣ When you deposit an ERC-20 token into AAVE, you receive an **aToken**.
2️⃣ The deposited funds are lent to other borrowers, and **borrowers pay interest.**
3️⃣ AAVE distributes a portion of the interest received to depositors.
4️⃣ **All of this is automatically executed by smart contracts**, with no centralized intermediary.
5️⃣ If a borrower cannot repay the loan, **the collateral is liquidated to prevent losses**.
👉 **AAVE operates like a bank but without a bank—it's an automated lending and interest payment system powered by blockchain smart contracts!** 🚀

---

### **📌 How AAVE utilizes deposited tokens**

You got it right! **In traditional finance, banks lend deposited money or invest it to generate profits, and then pay a portion of those profits to customers as interest.**
So how does a **DeFi platform like AAVE use deposited tokens to pay interest?** 🤔
To understand this, we need to look at **AAVE's core operating mechanism.**

---

## **1️⃣ AAVE lends out deposited tokens!**

The core principle of DeFi protocols like AAVE is **lending deposited tokens to others and earning interest on the loans**.
✅ **User A (Depositor, Lender)**

- If you deposit 1,000 USDT into AAVE, it is stored in the AAVE smart contract.
- AAVE doesn't just leave it there; it **lends it to someone who needs it.**
- For example, if someone wants to borrow 500 USDT, AAVE borrows part of the USDT you deposited.
  ✅ **User B (Borrower)**
- The borrower (B) who wants to borrow money pledges **collateral** and borrows 500 USDT from AAVE.
- For example, you can borrow 500 USDT by pledging 1 ETH (worth 3000 USDT) as collateral.
- The borrower must pay **interest** to AAVE. (e.g., 5% annual interest)
  ✅ **AAVE's revenue model**
- The borrower pays **loan interest**.
- AAVE returns a portion of the interest earned to the depositor (A) as **compensation (interest payment)**.
- In other words, AAVE's smart contract facilitates the flow of money from “borrower → AAVE → depositor” to enable interest payments.
  👉 **In other words, the interest you receive is a portion of the interest AAVE receives from borrowers!**
  👉 **AAVE operates like a bank, collecting deposits and lending them out, then rewarding
  depositors with interest on the loans!** 🚀

---

## **2️⃣ AAVE's Smart Contract Structure**

Let's take a closer look at how tokens actually move within AAVE.

### **🔹 1. Deposit Process**

- Users deposit **ERC-20 tokens (e.g., USDT, DAI, ETH, etc.) into AAVE.**
- The AAVE contract records the user's balance and issues **aToken (e.g., aUSDT, aDAI), a deposit proof token, on their behalf.**
- aTokens track the original deposited tokens at a 1:1 ratio while accruing interest.
  📌 **Example:**
  ✔ Depositing 1,000 USDT results in AAVE issuing “1,000 aUSDT” and sending it to your wallet.
  ✔ The number of aUSDT remains unchanged, but their value increases over time as interest is paid out.

### **🔹 2. Borrowing Process (Borrow)**

- Borrowers **pledge their assets (ETH, BTC, USDT, etc.) as collateral and borrow the desired tokens.**
- The AAVE contract disburses the loan amount from the deposited assets.
- Borrowers must pay interest and repay the loan within a specified period.
  📌 **Example:**
  ✔ User B pledges **1 ETH (3,000 USDT) as collateral and borrows 500 USDT**
  ✔ User B receives **500 USDT from the AAVE contract**
  ✔ User B must pay an additional **5% interest on the loan**

### **🔹 3. Interest Payment Process**

- When the borrower pays interest to the AAVE contract, a portion of this revenue is returned to the depositor.
- The depositor receives interest in the form of an increase in the value of their aToken (aUSDT, aDAI).
  📌 **Example:**
  ✔ AAVE receives 5% interest from the borrower.
  ✔ A portion is used for platform operating expenses, and **the remainder is distributed to depositors (A).**
  ✔ As a result, **the value of the aUSDT held by A increases, effectively receiving interest!**
  👉 **In this way, depositors (A) can automatically receive interest without any additional action!** 🚀

---

## **3️⃣ How does AAVE manage risk?**

AAVE uses a **collateral-based lending system**, so if the borrower fails to repay the loan, the collateral is liquidated to prevent losses.
🔹 **Overcollateralized Loans**:

- When borrowing from AAVE, collateral (ETH, BTC, etc.) must be pledged.
- Typically, collateral is required in amounts significantly higher than the loan amount. (e.g., 150% collateral ratio)
  🔹 **Liquidation System**:
- If a borrower fails to repay the loan or the collateral value decreases, the collateral is automatically sold to recover the loan amount.
- For example, if you pledge 1 ETH (3,000 USDT) as collateral and borrow 500 USDT, and the price of ETH drops to 2,500 USDT, **AAVE automatically liquidates the collateral to prevent losses.**
  👉 **In other words, AAVE has a system in place to protect depositors' principal by selling the collateral even if the borrower cannot repay the loan.** 🔒

---

## **4️⃣ Conclusion: AAVE's interest payments come from loan interest!**

✅ AAVE uses deposited assets to **lend to other users**.
✅ Borrowers pay interest, and **a portion of this is paid as compensation (interest) to depositors (A)**.
✅ To recover the loan, **collateral is required, and if the loan is not repaid, it is automatically liquidated to prevent losses**.
✅ Depositors **automatically receive interest if they hold aToken (aUSDT, aDAI, etc.)**.
👉 **Ultimately, the interest received from AAVE is “the compensation given to me because someone else borrowed the funds I deposited and paid interest on the loan”**! 🚀

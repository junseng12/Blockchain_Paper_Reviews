## **📌 1. Oracle Concept Summary**

### **🔹 What is an Oracle?**

- Blockchains **cannot retrieve external data on their own** → Smart contracts can only use data within the Ethereum blockchain.
- An **Oracle** is a system that helps smart contracts retrieve data from outside the blockchain.
- In simple terms, an Oracle acts as a bridge connecting the blockchain to the real world.
  📌 **Analogy:**
  The blockchain is an island where everything happens within its boundaries.
  However, when information from the outside world (weather, exchange rates, sports results, etc.) is needed, you need to use a boat (oracle) to retrieve it.

<summary>**📌 There is only one oracle, but there are multiple oracle providers!**</summary>

An oracle simply refers to the role of connecting blockchain and real-world data.
However, in reality, there are **multiple oracle services** that perform this role.
For example:

- Chainlink
- Band Protocol
- API3
- Pyth Network
- UMA (Universal Market Access)
- Tellor

---

## **📌 2. Why are oracles necessary?**

### **🔹 Limitations of Ethereum**

- **The Ethereum Virtual Machine (EVM) must be completely deterministic.**
- In other words, the same input must always produce the same result.
- As a result, **the blockchain itself cannot directly obtain random values or external data.**
- For example:

1. **Random value (random number) problem:**

- What if the `random()` function returns a different value each time it is executed within a smart contract?
- All nodes in the network cannot obtain the same result, making **consensus impossible** → blockchain cannot function.

2. **Cannot utilize external data:**

- Smart contracts can only access **data within the blockchain** (balance, status, etc.).
- However, there is no way to use **external data** such as **cryptocurrency exchange rates, weather information, or sports results** when needed.
- For example, to create a contract that says “Send ETH if the Bitcoin price is above $50,000,” you need to retrieve the BTC price → **An oracle is required!**

📌 **Analogy:**
A smart contract is like a person living on an island who cannot directly access external information.

However, when external information such as weather forecasts, news, or financial information is needed, it is received through an oracle (e.g., a ship or a mail carrier).

---

## **📌 3. Use cases for oracles**

Oracle plays the role of **transmitting real-world data to the blockchain** and is used in various places.

| **Oracle Data Types**             | **Use Cases**                                                                             |
| --------------------------------- | ----------------------------------------------------------------------------------------- |
| **Random Numbers**                | Casinos, lotteries, in-game item drop systems                                             |
| **Financial Data**                | Exchange rates, cryptocurrency prices (ETH/USD), stock price information                  |
| **Sports Results**                | Sports betting, fantasy sports                                                            |
| **Weather Information**           | Agricultural insurance (compensation in case of heavy rain), climate data-based contracts |
| **Public Data**                   | Political election results, government statistics                                         |
| **Internet of Things (IoT) Data** | Logistics, supply chain (Geolocation, RFID tracking)                                      |
| **Other Blockchain Data**         | Cross-chain bridge, BTC → ETH conversion                                                  |
| **Flight Information**            | Flight delay compensation insurance                                                       |

📌 **Example 1: Insurance Smart Contract**

- “If my flight is delayed by more than 2 hours, compensation will be paid automatically!”
- Ethereum smart contracts cannot access flight delay information.
- An oracle retrieves data from the **flight API** and transmits it to the smart contract → compensation is paid automatically.

📌 **Example 2: Sports Betting**

- “If Team A wins, you get double your bet back!”
- Blockchain cannot directly access game results.
- An oracle retrieves **official game result data from sources like ESPN or FIFA** and inputs it into the blockchain.

---

## **📌 4. How Oracles Work**

Oracles can be categorized into various types based on how they retrieve data and transmit it to smart contracts.

### **🔹 1) Immediate-read Oracle**

- Suitable for simple data queries (e.g., “Is this person an adult?”)
- Data does not change frequently and is retrieved only once when needed.

📌 **Example:**

- Government-operated identity verification oracle → “Is this user over 18 years old?”
- Degree verification oracle provided by a university → “Has this person received a specific degree?”

---

### **🔹 2) Publish-Subscribe Oracle**

- Data changes periodically and updates are required.
- Smart contracts continuously monitor (listen to) the oracle and automatically respond when data is updated.

📌 **Example:**

- **Cryptocurrency price feed (Chainlink, Band Protocol)**
- The smart contract executes a specific transaction when the ETH/USD price exceeds $2000.
- The oracle periodically updates the data and notifies of any changes.
- **Weather-based insurance**
- Automatically pays compensation when rainfall in a specific region exceeds a certain threshold.

---

### **🔹 3) Request-Response Oracle**

- Queries external data and responds whenever a specific request is made.
- Used when there is too much data to store permanently.
- The oracle retrieves the data and transmits it each time a request is sent.

📌 **Example:**

- “What is the current price of Bitcoin?” → Query the API and respond.
- “What is the current price of IBM stock?” → Request data only when needed.

---

## **📌 5. Oracle Security - Data Authentication**

One of the most important issues when using oracles is **data tampering and reliability**.
Since there is a risk of hacking or tampering with data while it is being transmitted on-chain, a **data authentication method** is necessary.

### **1️⃣ Authenticity Proofs**

🔹 **TLSNotary**

- A method of proving that the oracle sent a TLS (HTTPS security protocol) request
- TLSNotary is run on **Amazon Web Services (AWS) instances** to prevent hacking
- Issue: **You must trust AWS**

🔹 **Cryptographic Signatures**

- The institution providing the data adds a **digital signature** to ensure that the data has not been tampered with
- Smart contracts verify the signature to enhance data reliability

---

### **2️⃣ Trusted Execution Environment (TEE)**

🔹 **Intel SGX (Software Guard eXtensions) - Town Crier**

- Processes oracle data in a secure environment using Intel's SGX technology
- Protects data at the CPU level when the oracle provides data, reducing the risk of hacking
- Issue: **Must trust Intel**

---

## **📌 6. Computation Oracles**

Generally, oracles provide data, but in some cases, they also **perform computations**.
This method involves processing complex computations that are difficult to execute in Ethereum smart contracts **off-chain and returning only the results**.

### **1️⃣ Oraclize (AWS-based computation)**

- Runs Docker containers on AWS virtual machines to perform complex calculations
- Returns results to the Ethereum smart contract
- Drawback: **Not fully decentralized (must trust AWS)**

### **2️⃣ TrueBit (Decentralized Computation Oracle)**

- When a smart contract requests a complex computation, participants in the TrueBit network perform the computation
- Validators review the calculation results to prevent errors
- Bypassing Ethereum block gas limits enables large-scale computations

---

## **📌 7. Decentralized Oracles**

Centralized oracles (e.g., API providers like Oraclize, BlockOne IQ) act as a **single point of failure** because they provide data from a **single location**.

If this data provider is manipulated or hacked, **smart contracts receive incorrect information, leading to serious issues**.

To address this, **decentralized oracles** were introduced.

📌 **Chainlink (Chainlink)**

- Multiple data providers (nodes) provide data, and the final value is determined by majority vote or a specific algorithm.
- It operates on a blockchain and rewards oracle data providers with LINK tokens.

<summary>Chainlink Details</summary>

### 1. What is Chainlink?

Chainlink is a **Decentralized Oracle Network (DON)** that helps **smart contracts retrieve external data in a trustworthy manner**.

📌 **In simple terms?**

Chainlink is the “news reporter” of the blockchain.

When a smart contract asks, “Tell me the price of Bitcoin!”, Chainlink collects information from multiple data providers and then transmits the most reliable information to the blockchain.

---

### **📌 Why is Chainlink necessary?**

Existing oracles (e.g., specific API providers) are **centralized systems**.

If a specific API provider is hacked or provides false data, the smart contract using it will also rely on incorrect data.

✅ **Issues**

- Centralized oracles lack reliability (one person can manipulate the entire system)
- Hacking a specific oracle affects all smart contracts
- Contradicts the decentralization principle of blockchain

👉 **Solution: Chainlink's decentralized oracle network**

Chainlink uses **multiple independent nodes** to provide data, which is then verified to provide **the most reliable data to smart contracts**.

---

### **📌 How Chainlink works**

Chainlink's Oracle network consists of three main smart contracts.

1️⃣ **Reputation Contract**

- Evaluates the trustworthiness of Oracles that provide data
- Records the past performance of data providers, and nodes that frequently provide accurate data receive high scores
- Oracles with low trustworthiness are excluded

2️⃣ **Order-Matching Contract**

- When a smart contract requests, “Tell me the Bitcoin price!”,
  this contract finds an appropriate Oracle node and enters into a contract

3️⃣ **Aggregation Contract**

- Compares data received from multiple Oracle nodes to **determine the most reliable data**
- For example, if 5 nodes provide Bitcoin prices, the **median is adopted as the correct answer**

📌 **Example:**

If a smart contract wants to know the ETH/USD exchange rate?

1. Chainlink retrieves ETH/USD prices from multiple data providers (APIs, exchanges, etc.)
2. Each oracle reports its data (e.g., $1,999 / $2,000 / $2,001)
3. Chainlink's **aggregation contract determines the final ETH/USD price** (e.g., the median value of $2,000)
4. The final price is transmitted to the smart contract

📌 **What types of data can Chainlink provide?**

- Cryptocurrency prices (ETH/USD, BTC/USD)
- Traditional financial market data (S&P 500 index, gold prices)
- Sports game results
- Weather information (e.g., insurance payouts during heavy rain)
- Logistics and supply chain data (e.g., cargo arrival confirmation)

---

### **📌 Key features of Chainlink**

✅ **Decentralized oracle network**

- Instead of relying on a single centralized oracle, information is provided by multiple independent data providers

✅ **Economic Incentives (LINK Tokens)**

- Oracles that provide data receive **LINK tokens as rewards**
- Providing false data may result in losing **LINK tokens as penalties**
- Economic incentives to maintain data accuracy

✅ **Security and Transparency**

- All data requests and responses in the Chainlink network are **recorded on the blockchain**
- Anyone can track how data was provided

✅ **Support for Various Blockchains**

- Chainlink is **compatible with various blockchains, including Ethereum, BNB Chain, Solana, Polygon, Avalanche, and more**

---

### **📌 Chainlink use cases**

✅ **DeFi (Decentralized Finance)**

- DeFi protocols such as AAVE and Compound use Chainlink's oracles to **retrieve real-time asset price data**
- For example, a collateralized lending service that automatically liquidates when the price of ETH falls below a certain level

✅ **NFTs and gaming**

- Random NFT distribution in NFT projects (e.g., NFT lottery)
- Random events in blockchain-based games (e.g., calculating item drop probabilities)

✅ **Insurance and Real-World Data Utilization**

- Weather data-based insurance using Chainlink (e.g., automatic compensation during heavy snowfall)

👉 **Chainlink maintains the decentralization and trust of blockchain while safely retrieving real-world data!** 🚀

📌 **SchellingCoin**

- **Multiple participants submit data**, and **the median is adopted as the correct answer**.
- Submitting false data results in a **penalty**, **encouraging correct responses**.

---

## **📌 8. Oracle Security Issues and Solutions**

- Oracles weaken the blockchain security model by relying on external data, posing a risk of data manipulation.

### **🛑 Key Oracle Security Issues**

1️⃣ **Oracle Manipulation**

- If Oracle data is hacked, smart contracts execute based on incorrect information.
- Example: If an attacker manipulates the price of ETH to $10, all collateralized loans could be forced liquidated

2️⃣ **Single Point of Failure**

- Using a centralized oracle (Oraclize, specific API) means that if the oracle goes down or is manipulated, **all smart contracts are affected**

3️⃣ **Economic attacks (Flash Loan attacks)**

- An attacker can quickly take out a loan and influence the Chainlink oracle
- Example: In a past DeFi hacking case, the Chainlink price was manipulated to exploit interest rate adjustments

<summary>**Flash Loan attacks & solutions**</summary>

### **📌 What is a Flash Loan attack?**

A Flash Loan is a very powerful financial tool used in DeFi (Decentralized Finance). The core concept is that **you can borrow money without collateral and must repay it immediately within the same transaction**.
Typically, when borrowing money from a bank, you need to provide collateral (e.g., a house or car), but with a Flash Loan, **you can borrow money without collateral using smart contracts**.
However, this powerful feature can be exploited by hackers. Hackers use flash loans to carry out **flash loan attacks**, which involve price manipulation, loan liquidation, and price volatility manipulation of DeFi protocols to gain unfair advantages.

---

## **🔴 How Flash Loan Attacks Work**

1️⃣ **Borrow a large amount of funds (without collateral)**

- Hackers use flash loans on DeFi platforms like AAVE or dYdX to borrow large amounts of cryptocurrency.
- Flash loans must be repaid immediately within a single transaction, allowing hackers to perform other actions immediately after borrowing.

2️⃣ **Manipulate the price of DeFi protocols**

- The borrowed funds were used to buy (or sell) large quantities of specific tokens, **distorting prices on decentralized exchanges (DEXs)**.
- Unlike centralized exchanges, DEXs operate on a **liquidity pool-based model (AMM, Automated Market Maker)**, so large transactions can cause significant price fluctuations.

3️⃣ **Buying at a low price or selling at a high price after price manipulation**

- After price manipulation, the attacker executes transactions using the manipulated price through a pre-prepared smart contract.
- For example, in lending protocols like AAVE, forced liquidation occurs when the price of collateral assets changes, and attackers exploit this to seize collateral at low prices.

4️⃣ **After repaying the initial loan, the attack is successful**

- Finally, repaying the borrowed flash loan completes the transaction.
- As a result, the attacker **quickly reaped significant profits, while the DeFi protocol suffered substantial losses**.

---

## **💡 Flash Loan Attack Examples**

### **📌 1️⃣ bZx Attack (2020, approximately $360,000 stolen)**

✅ **Attack Process**

- The hacker takes a flash loan from AAVE and buys a large amount of WETH (Ethereum-based token).
- The price of WETH skyrockets on a liquidity pool-based DEX.
- The bZx lending protocol evaluates loans based on the WETH price, but **executes the loan incorrectly, trusting the manipulated price**.
- The hacker seizes the collateral at the manipulated price, repays the flash loan, and pockets the profits.

✅ **Outcome**

- Approximately **$360,000 in losses** occurred on the bZx protocol
- bZx subsequently analyzed the attack pattern and strengthened security

<summary>**How the attacker profited**</summary>

### **📌 The process by which the attacker profited**

### 1️⃣ **Borrowed 1,000 ETH via a flash loan**

- This is **borrowed money that must be repaid immediately**, and the attacker must eventually repay it.

### 2️⃣ **Massively purchased WETH using borrowed ETH → Price surges**

- For example, the price of WETH doubles
- (Originally 1 WETH = 2,000 USDT → Manipulated to 1 WETH = 4,000 USDT)

### 3️⃣ **Over-borrow from bZx using WETH as collateral**

- Originally, only **20,000 USDT** could be borrowed with 10 WETH as collateral,
- But with the manipulated price, **40,000 USDT** can be borrowed!
- **(Allowing borrowing of twice as much USDT as originally possible)**

### 4️⃣ **Repaying the Flash Loan**

- To repay the Flash Loan, **use part of the borrowed 40,000 USDT (e.g., 20,000 USDT) to repay the Flash Loan**
- **The attacker has now repaid the entire Flash Loan and has an additional 20,000 USDT remaining!** (This is the key point)

### 5️⃣ **Massive sale of WETH → price drop**

- To restore WETH to its original state, the attacker **sells a large amount of WETH on the market**
- As the price of WETH plummets, **1 WETH returns to 2,000 USDT.**
- **bZx executed the loan based on the manipulated price, so only 20,000 USDT could be recovered.**

✅ The attacker borrowed 1,000 ETH using a Flash Loan.

✅ Converted ETH to WETH to
**abnormally spike (manipulate) the WETH price!**

✅ Borrowed
**received an over-collateralized loan (40,000 USDT).**

✅ Even after repaying the Flash Loan,
**20,000 USDT remained in the attacker's possession.**

✅ The attacker sold WETH on the market at a discounted price to restore the price to its original level.

✅ When bZx attempted to recover the loan,
**the actual value of the collateral (WETH) was only 20,000 USDT...**

✅ Ultimately
**bZx was unable to recover the 20,000 USDT and incurred a loss.**

✅ The attacker
**walked away with 20,000 USDT!**

🚀🚀

---

### **📌 2️⃣ Cream Finance Attack (2021, approximately $130 million stolen)**

✅ **Attack Process**

- The attacker used a flash loan to borrow from the CREAM protocol
- **Price manipulation caused over-leverage**
- The attacker seized the collateral and repaid the flash loan

✅ **Result**

- Cream Finance suffered a loss of approximately $130 million (about 170 billion KRW)
- Subsequently implemented security patches and changed the price oracle

---

## **🔐 Flash Loan Attack Defense Methods**

### **1️⃣ Improve Price Oracle**

- Most Flash Loan attacks are based on **price manipulation**.
- Instead of using prices from decentralized exchanges (DEX), **referencing more accurate prices from decentralized oracles like Chainlink** can help defend against attacks.

### **2️⃣ Flash Loan Detection and Limitation**

- Add a **Flash Loan detection algorithm to smart contracts to block abnormal transaction patterns**
- Introduce a defense technique that **temporarily restricts loans when excessive price fluctuations occur in specific transactions**

### **3️⃣ Add liquidation protection mechanisms**

- Add a feature to **temporarily suspend liquidation when abnormal price fluctuations occur in the loan protocol**

### **4️⃣ Apply multi-signature and governance**

- Important smart contract updates related to price changes will be decided through **governance voting**
- **Modify the structure that triggers automatic liquidation based on specific oracle data**

---

## **📌 Conclusion: Flash loan attacks are powerful, but they can be defended against!**

Flash loans are a powerful feature in DeFi, but **they can also be exploited to manipulate the market and attack protocols**.

To prevent such attacks, **defense strategies such as improving price oracles and applying algorithms to detect flash loans in smart contracts** are important! 🔥

### **🔹Solution**:

- **Use a mechanism to verify oracle data** (SchellingCoin, Chainlink)
- **Use multiple data providers (nodes)** to decentralize
- **Utilize data signatures (Authenticity Proofs)** → Prevent data manipulation

---

## **📌 Conclusion**

1. **Blockchain cannot retrieve external data on its own, so oracles are necessary.**
2. **Through oracles, various data such as exchange rates, weather, and sports game results can be utilized in smart contracts.**
3. **Oracle types are categorized into immediate lookup, subscription-based, and request-response methods.**
4. **Centralized oracles have security vulnerabilities, and decentralized oracles (e.g., Chainlink) have emerged to address these issues.**

👉 **Oracle is a crucial technology connecting blockchain and the real world, with security being the most critical issue!**🚀

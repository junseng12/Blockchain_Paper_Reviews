## **📌 1. Understanding DApps (Decentralized Applications)**

### **🔹 What are DApps?**

- DApps are **decentralized applications** that operate without a central server, using **blockchain** and **P2P networks**.
- While traditional applications process and store data on a centralized server, DApps process application logic in a decentralized manner through **smart contracts**.
- **Smart contracts** are **deployed on the blockchain**, **cannot be changed**, and are processed in a **decentralized manner**.

📌 **Analogy:**

DApps are like **restaurants**. Traditional applications have a **chef** (server) who prepares all the dishes, but DApps have **automated cooking machines** (smart contracts) that cook and serve all the food. Customers simply **place an order**, and the **machine** automatically prepares and serves the food.

---

## **📌 2. Core Components of DApps**

### **🔹 1) Backend (smart contract)**

- **Smart contracts** store and manage **application logic**. They are deployed on the blockchain and are **immutable**.
- Smart contracts have **high gas costs**, so calculations must be minimized. The important things are **trustlessness (no trust required)** and **a decentralized execution environment**.

📌 **Analogy:**
Smart contracts work like a restaurant menu. The recipes (application logic) on the menu are processed by an automated machine, and the results are stored on the blockchain and cannot be modified.

---

### **🔹 2) Frontend (Web User Interface)**

- The frontend is built using traditional web technologies such as HTML, CSS, and JavaScript.
- It facilitates interaction between users and the blockchain through **Web3 wallets** such as **MetaMask**.

📌 **Analogy:**

The frontend is like the dining room of a restaurant. It allows customers to view the menu, place orders, and send those orders to the machine (smart contract). Users connect to this machine through an order form called MetaMask.

---

### **🔹 3) Data Storage**

- Smart contracts are not suitable for storing large amounts of data due to high gas costs.
- Most DApps use **distributed storage** like **IPFS (Inter-Planetary File System)** or **Swarm** to **store data externally**.

📌 **Analogy:**

Smart contracts are like **cooking machines** that prepare meals by retrieving ingredients from a **storage**. Large quantities of ingredients are stored in the **storage** (IPFS, Swarm), and the machine retrieves only the necessary ingredients as needed to prepare the meal.

---

### **🔹 4) Message Communication**

- Message communication in DApps is carried out in a distributed manner using a **P2P protocol** such as **Whisper**.
- **Whisper** enables secure **message exchange** between DApp users.

📌 **Analogy:**

Message communication is like **conversations between restaurant staff**. When a customer places an order, all conversations are handled through **secret conversations** (Whisper) between staff members, not through a **centralized server**.

---

## **📌 3. Advantages of DApps**

### **🔹 1) Resilience**

- Smart contracts are **deployed on the blockchain**, so they are not affected by issues with central servers, such as **server downtime**.
- The **blockchain** is **decentralized**, so even if the server goes down in one location, the application continues to operate.

📌 **Analogy:**

The **cooking machines** in a restaurant do not depend on a **central kitchen**. Even if the chef is sick or the power goes out, the **machines** continue to operate.

---

### **🔹 2) Transparency**

- DApps record all transactions **on the blockchain**, and **all code** is **public**.
- Anyone can review the operation of smart contracts, which increases reliability.

📌 **Analogy:**

In a restaurant, the cooking process of the **cooking machine** is **transparently disclosed**. **Customers** can **see everything** about how the food is prepared.

---

### **🔹 3) Censorship Resistance**

- DApps running on a blockchain cannot be censored. Since the code of a smart contract cannot be changed after distribution, no centralized authority can block the code or its operation.

📌 **Analogy:**

A restaurant's **cooking machine** is **not influenced by anyone**. Even if someone tries to prevent it from making food, the **machine** will **operate automatically**, and **external interference** is impossible.

---

## **📌 4. Example: Building an Auction DApp**

### **🔹 DApp Example - Auction Platform**

In this example, we build a DApp that sells **tokenized assets** (e.g., houses, cars, trademarks) using **ERC721** through **auctions**.

- **DeedRepository**: Issues and manages **ERC721 tokens** that represent assets.
- **AuctionRepository**: A **smart contract** that conducts auctions.

📌 **Analogy:**

An auction is like an auction event at a restaurant. **Customers** (users) connect to the **server** (smart contract) and **bid prices** like in an auction for **meals**. The **customer** who bids the highest price gets **that dish** (asset).

---

## **📌 5. DApp Security**

### **🔹 Security Audit and Vulnerability Prevention**

- DApps use smart contracts deployed on the blockchain, so security is extremely important. If vulnerabilities are discovered, significant losses can occur, making security audits essential.
- Common security vulnerabilities in smart contracts include **Reentrancy attacks**, **Integer Overflow**, and **Access Control**. These vulnerabilities must be identified through **security audits**.

📌 **Analogy:**

DApp security is like a thorough inspection of a building. After constructing a building, you must check that all windows and doors are properly locked and that the basic structure is sturdy. A security audit is like an expert performing such inspections.

---

## **📌 6. Limitations and Improvements of DApps**

### **🔹 Limitations of DApps**

- Most DApps still use some centralized systems (servers, databases, etc.), so complete decentralization has not been achieved.
- Due to **technical limitations**, **mobile DApp** development is relatively difficult.

📌 **Analogy:**

There are limits to how a restaurant can cook using **machines** (smart contracts). **Employees** (mobile apps) are needed to process customer orders, and those employees are managed in a **centralized** manner.

---

### **🔹 Improvements to DApps**

- **Swarm** and **IPFS** can be used to distribute all data across a decentralized network, achieving **complete decentralization**.
- Use **ENS** (Ethereum Name Service) to convert DApp addresses into **easy-to-understand names**.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c2ba559c-cb6d-4c61-bec3-1760fafc9a92/973d05dd-b244-48f5-b5a5-d890af8fa230/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665QIMJDI5%2F20250521%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250521T213909Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEA4aCXVzLXdlc3QtMiJHMEUCIHJTt%2BHneNJ%2FAJTIRZoyBZ54grrgzSexqEVEqplW5LJ2AiEAp7BUEYN7%2BNioinPdM%2FwZAT%2FHfFnF9IVKC4fiGMXa4JsqiAQIxv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDFO46DAptCscg%2BifASrcAxXFKxyjh7ZHod%2BGP1CjpJ8HFRvrTDQVF7xFhm%2BfDiPQV4XC2F0DEmYYvc9v5TKOnJoUeKQV%2FjUE3yz3cDBdJ5ZGB0R8dql8zgyjUkIWRd4gSRfkKsgltFrm%2BNWUWlVhj0CzI5HGwlC0Dt2hPyQnsuuuVQCwdIBbIbCgPey9waP7VMTZf%2BenQsfwaJfZ9%2FUilz18xVcg7kzM276zapt7%2BdjgVOfvOnrAenBfEi2g0nJQEF9yQ9L9RGfRoWm0iyg5iQVujGMwpKV8wjRSnzzQE5MHQKj4Wm8adpFD6p1CT4FECa3U4zqbEjyy%2BgD14yHC4%2B08IIId35yAVb0ZjKhdZdX8QLH4q0y0IxujuIgTdxYhomRbML2TNTjI3pUn%2BCdrLTXKPicTUV7zRk3eeAPMe0%2BOYpgCtvUJqeCy1snWaAIo6J0t3BzpN4IsyS05%2Fvv5PSm3AMFnZsquyuE64ZsRVTnTl5HSYim0UsiBDEtuWiTVpza1PnrrYO2Yck2dZUr8Zn4qkU5LxvLTcHdCCV8kJwWT8JOMk7I0xOuafDojGajfKR0XWoiWLfNIz0S9GFuOtmyVaD9%2FYQ6azyGzmSZd6zYkHbpfzz0LezQZ6A3IenHLTagDgE8BJYslNQpNMPiGucEGOqUBbqoKwN11cvgVknxbWz11tGqDLWmlGwjIBYSdJYmOZ2913DfmCXVAIOLyL1QhfNl87kEHUTM5hWWHzTKU8lb0gWcLI0slkPKZ25PXp2FnZh7OnhTvZ3X0qsncb9iOCKNtC%2BYsRpiksMsV9YScJaOT6Q9AKrpQWPPeybD9CttLm1Adc6kw8tQ77%2BQhA9%2FcJf4YFGz8MA6mq%2FhmS2oWVJ81tv2eRxtf&X-Amz-Signature=b29a6cf54633c4b209a24ef7f444851e0b99e4cf5581985b0f35436959d90b30&X-Amz-SignedHeaders=host&x-id=GetObject)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c2ba559c-cb6d-4c61-bec3-1760fafc9a92/afb39e5d-a7a1-4530-8e3b-afd757489c93/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665QIMJDI5%2F20250521%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250521T213909Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEA4aCXVzLXdlc3QtMiJHMEUCIHJTt%2BHneNJ%2FAJTIRZoyBZ54grrgzSexqEVEqplW5LJ2AiEAp7BUEYN7%2BNioinPdM%2FwZAT%2FHfFnF9IVKC4fiGMXa4JsqiAQIxv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDFO46DAptCscg%2BifASrcAxXFKxyjh7ZHod%2BGP1CjpJ8HFRvrTDQVF7xFhm%2BfDiPQV4XC2F0DEmYYvc9v5TKOnJoUeKQV%2FjUE3yz3cDBdJ5ZGB0R8dql8zgyjUkIWRd4gSRfkKsgltFrm%2BNWUWlVhj0CzI5HGwlC0Dt2hPyQnsuuuVQCwdIBbIbCgPey9waP7VMTZf%2BenQsfwaJfZ9%2FUilz18xVcg7kzM276zapt7%2BdjgVOfvOnrAenBfEi2g0nJQEF9yQ9L9RGfRoWm0iyg5iQVujGMwpKV8wjRSnzzQE5MHQKj4Wm8adpFD6p1CT4FECa3U4zqbEjyy%2BgD14yHC4%2B08IIId35yAVb0ZjKhdZdX8QLH4q0y0IxujuIgTdxYhomRbML2TNTjI3pUn%2BCdrLTXKPicTUV7zRk3eeAPMe0%2BOYpgCtvUJqeCy1snWaAIo6J0t3BzpN4IsyS05%2Fvv5PSm3AMFnZsquyuE64ZsRVTnTl5HSYim0UsiBDEtuWiTVpza1PnrrYO2Yck2dZUr8Zn4qkU5LxvLTcHdCCV8kJwWT8JOMk7I0xOuafDojGajfKR0XWoiWLfNIz0S9GFuOtmyVaD9%2FYQ6azyGzmSZd6zYkHbpfzz0LezQZ6A3IenHLTagDgE8BJYslNQpNMPiGucEGOqUBbqoKwN11cvgVknxbWz11tGqDLWmlGwjIBYSdJYmOZ2913DfmCXVAIOLyL1QhfNl87kEHUTM5hWWHzTKU8lb0gWcLI0slkPKZ25PXp2FnZh7OnhTvZ3X0qsncb9iOCKNtC%2BYsRpiksMsV9YScJaOT6Q9AKrpQWPPeybD9CttLm1Adc6kw8tQ77%2BQhA9%2FcJf4YFGz8MA6mq%2FhmS2oWVJ81tv2eRxtf&X-Amz-Signature=52cdf5de4450e4b20b97f29dbeafa6a4760886bf34e7f033585f8e7ff5817265&X-Amz-SignedHeaders=host&x-id=GetObject)

<summary>**ENS(이더리움 네임 서비스) 구체적인 원리**</summary>

**ENS** is an alternative to the **Domain Name System (DNS)** used on the Ethereum blockchain. The **basic principle** of ENS is to provide a **decentralized naming service** that connects **domains** and **resources** on the **blockchain**. In simple terms, **ENS is the blockchain version of DNS**.

### **🔹 Basic Structure of ENS**

ENS utilizes the **Ethereum blockchain** to connect domain names and other resources. For example, the name `ethereumbook.eth` can be linked to an Ethereum address or a specific resource.

### **🔹 Components of ENS**

1. **ENS Root Node**

   - The **basic unit** of ENS is a **node** (identifier) created by **hashing** a **name**. Names such as `ethereumbook.eth` are converted into unique nodes through **name hashes**.

2. **Name Hash**

   - ENS names are converted into hashes through an algorithm called **name hash**. This hash value is used as a unique identifier on the blockchain.
   - For example, `ethereumbook.eth` is converted to a **unique hash** value using the **keccak256** algorithm, and this hash value is converted to a **node** and stored in ENS.

3. **Registration**

   - ENS names are registered through an **auction system**. Names are purchased through an **auction process**, and the highest bidder wins the domain through a **Vickrey Auction**. In this method, only the **highest bid** and **second highest bid** are disclosed, and the **second highest bid** is ultimately paid.

4. **Resolver**

   - The resolver returns the **actual data** associated with an ENS name. It helps connect ENS names to blockchain addresses, **Swarm** hashes, **IPFS** addresses, and more.
   - For example, the subdomain `auction.ethereumbook.eth` converts the resources of a DApp stored in Swarm into an **address** that can be used by users.

5. **Background Management (Governance)**

   - ENS names are **managed by their owners**, who can renew or change them. ENS is designed so that **all operations are decentralized** and **network participants** operate it without a **central administrator**.

---

### **📌 ENS Operation Example**

### **🔹Summary of the entire process**

1. \*\*The user participates in an auction to register “mydomain.eth.”
2. \*\*The user bids in the auction and acquires the domain name by offering the highest price.
3. The domain name is hashed using the **Namehash algorithm** to create a \*\*unique identifier.
4. The generated \*\*Namehash value is stored in the ENS Registry.
5. The **resolver** converts this domain name into an actual **resource (e.g., Swarm hash or Ethereum address)**.
6. Users can access Swarm or Ethereum resources via **“mydomain.eth”**.

---

### **🔹ENS Operation Example: Registering and Linking “mydomain.eth”**

1. **User registers domain name (participates in auction)**

   - The user wants to register the name **“mydomain.eth”**. This domain is sold through an auction system.
   - ENS uses a **Vickrey Auction** to sell domain names. Here, users submit **private bids** and pay the **second-highest price**.

   📌 **Analogy:**
   In an auction, you submit a **sealed bid** for an item you want to buy, and the person who bids the highest price at the end wins the item, but the actual amount you pay is the **second highest amount**. This is a way to protect the interests of participants in a private auction.

2. **Namehash Generation**

   - After acquiring the domain “mydomain.eth” in the auction, the ENS system uses the **Namehash algorithm** to convert the name into a **hash** value.
     This hash value makes “mydomain.eth” a unique identifier, allowing all information related to this name to be tracked and managed on the blockchain.

   📌 **Analogy:**

   The domain name “mydomain.eth” is converted into a **unique number that can be found in the address book**, which is then converted into an identifier that can be tracked within the blockchain.

3. **Stored in the ENS Registry**

   - The unique hash value of **“mydomain.eth”** converted into Namehash is stored in a smart contract called the **ENS Registry**.

   The ENS Registry is the core registry of ENS, managing names and the resources (addresses, content, etc.) associated with those names.

   📌 **Analogy:**

   The ENS Registry is like a **phone book**, where it stores and manages information associated with each domain name's unique number.

4. **Resolver setup**

   - The domain name **“mydomain.eth”** registered in the ENS Registry is linked to a **resolver**. A resolver converts domain names into actual resource addresses.

   - For example, if **“mydomain.eth”** points to a DApp stored in **Swarm**, the resolver returns the **Swarm hash** of that DApp. This makes it easy to find the DApp's user interface.

   📌 **Analogy:**

   The resolver is like someone searching for an address at the post office. When you enter “mydomain.eth,” it returns the **actual address**, which is the Swarm hash or Ethereum address.

5. **Connect to Swarm or other resources**

   - The information returned by the resolver is the **actual content** (e.g., DApp files, images, etc.) stored in a distributed storage system like Swarm or an Ethereum address (e.g., a smart contract address).

   - For example, if “mydomain.eth” connects to a DApp hosted on Swarm, users can access the actual content of the DApp on Swarm through this address.

   📌 **Analogy:**

   - When you enter “mydomain.eth” in a web browser, the DApp hosted on Swarm or the Ethereum address appears as a website, just like when you enter a website address in the address bar.

**📌 Advantages of ENS**

- **Decentralization**: ENS uses a blockchain to manage domain names, eliminating the need for a centralized system.
- **Flexibility**: ENS supports connections to various resources (Ethereum addresses, Swarm hashes, etc.).
- **Censorship resistance**: Since it is blockchain-based, no one can censor or control the ENS system.

<summary>**Hash functions in ENS**</summary>

### **1. Characteristics of hash functions**

A hash function is a **one-way function** that typically generates a unique output for a given input. In other words, it **always generates the same output for the same input**, but **collisions** (the possibility of different inputs producing the same hash value) can theoretically occur.

### **2. Hash Functions and Their Role in ENS**

ENS uses hash functions, specifically **Namehash**, to convert domain names (e.g., “ethereumbook.eth”) into **unique identifiers**. The **Namehash** used in ENS undergoes multiple steps to **hash the name** and store the result as a **unique node**. This design is intended to **minimize the possibility of collisions**.

### **3. Why there is little concern about collisions**

The hash function used in ENS is the **keccak256** algorithm, which has a very low collision probability. This algorithm is designed to be **cryptographically secure** and **minimize the possibility of collisions**. Therefore, the probability of different input values generating the same hash value is very low and practically impossible.

### 📌 **Analogy:**

Namehash is like assigning a unique number to each person in a phone book. Even though the number of numbers is limited, there is **enough space to prevent collisions**, ensuring that the probability of overlapping with another person's number is very low.

### **4. ENS's collision prevention system**

- In ENS, **Namehash** is not just a simple hash value but a mechanism that generates a **unique identifier for each domain name**, thereby minimizing collisions.
- ENS's **auction system** and **resolver system** are designed to prevent collisions, ensuring that “different ENS names pointing to the same content” does not actually occur.
  Therefore, since the system is designed to prevent conflicts and ensure the ENS system operates normally, each ENS domain is associated with unique content, and ENS names pointing to the same content are managed to prevent such occurrences.

### **5. Conclusion**

- **While hash functions theoretically have the possibility of collisions, ENS uses a design and algorithm that minimizes collisions, so the likelihood of different ENS domains pointing to the same content is very low.**
- **While it is not possible to completely eliminate the possibility of collisions, ENS can safely manage each domain uniquely within practical limits.**
  Therefore, ENS's **basic design is sufficiently secure** and ensures that different ENS names **do not point to the same content.**

📌 **Analogy:**
A restaurant manages **all its cooking equipment** in a **distributed system** (Swarm, IPFS) and provides **names** (ENS) that are easy to remember.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c2ba559c-cb6d-4c61-bec3-1760fafc9a92/7abfce75-24f0-4b2d-9c63-190c6c1e6c98/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665QIMJDI5%2F20250521%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250521T213909Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEA4aCXVzLXdlc3QtMiJHMEUCIHJTt%2BHneNJ%2FAJTIRZoyBZ54grrgzSexqEVEqplW5LJ2AiEAp7BUEYN7%2BNioinPdM%2FwZAT%2FHfFnF9IVKC4fiGMXa4JsqiAQIxv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDFO46DAptCscg%2BifASrcAxXFKxyjh7ZHod%2BGP1CjpJ8HFRvrTDQVF7xFhm%2BfDiPQV4XC2F0DEmYYvc9v5TKOnJoUeKQV%2FjUE3yz3cDBdJ5ZGB0R8dql8zgyjUkIWRd4gSRfkKsgltFrm%2BNWUWlVhj0CzI5HGwlC0Dt2hPyQnsuuuVQCwdIBbIbCgPey9waP7VMTZf%2BenQsfwaJfZ9%2FUilz18xVcg7kzM276zapt7%2BdjgVOfvOnrAenBfEi2g0nJQEF9yQ9L9RGfRoWm0iyg5iQVujGMwpKV8wjRSnzzQE5MHQKj4Wm8adpFD6p1CT4FECa3U4zqbEjyy%2BgD14yHC4%2B08IIId35yAVb0ZjKhdZdX8QLH4q0y0IxujuIgTdxYhomRbML2TNTjI3pUn%2BCdrLTXKPicTUV7zRk3eeAPMe0%2BOYpgCtvUJqeCy1snWaAIo6J0t3BzpN4IsyS05%2Fvv5PSm3AMFnZsquyuE64ZsRVTnTl5HSYim0UsiBDEtuWiTVpza1PnrrYO2Yck2dZUr8Zn4qkU5LxvLTcHdCCV8kJwWT8JOMk7I0xOuafDojGajfKR0XWoiWLfNIz0S9GFuOtmyVaD9%2FYQ6azyGzmSZd6zYkHbpfzz0LezQZ6A3IenHLTagDgE8BJYslNQpNMPiGucEGOqUBbqoKwN11cvgVknxbWz11tGqDLWmlGwjIBYSdJYmOZ2913DfmCXVAIOLyL1QhfNl87kEHUTM5hWWHzTKU8lb0gWcLI0slkPKZ25PXp2FnZh7OnhTvZ3X0qsncb9iOCKNtC%2BYsRpiksMsV9YScJaOT6Q9AKrpQWPPeybD9CttLm1Adc6kw8tQ77%2BQhA9%2FcJf4YFGz8MA6mq%2FhmS2oWVJ81tv2eRxtf&X-Amz-Signature=b6a67a65d3a21a30b7d20f86a857cd096df914797f73147db5487202f9238d5e&X-Amz-SignedHeaders=host&x-id=GetObject)

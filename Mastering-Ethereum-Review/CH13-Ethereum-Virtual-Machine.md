## 📌 **1. Ethereum Virtual Machine (EVM) Concept**

### 🔹 **What is EVM?**

- **EVM** (Ethereum Virtual Machine) is a **core component of Ethereum**, serving as a **virtual computer environment** that executes smart contracts and modifies the blockchain state.
- EVM is responsible for **executing and deploying smart contracts**, and all Ethereum nodes use the same EVM to execute the same smart contracts and obtain the same results.

### 📌 **Analogy:**

- **Ethereum** is a huge **shared computer**, and EVM is like the **operating system (OS)** that runs on this computer.
- Smart contracts are **programs** that run on the OS, and the EVM is responsible for **resource management and security functions** necessary to run these programs.

---

## 📌 **1️⃣ Key Features of EVM**

### **🔹 Quasi–Turing Completeness**

- The EVM can execute almost any program like a **Turing-complete virtual machine**. However, it **limits execution time** through gas to prevent network crashes caused by infinite loops.
- In other words, it is a **secure computer** designed to prevent the execution of infinite loop programs.

### 📌 Analogy:

- The EVM is like a **“coin-operated karaoke machine.”**
- You can sing (code) only as many songs as you put coins in. You cannot sing infinitely, and songs (code) can only be executed within a **set amount (gas)**. When the time is up, it ends unconditionally.

---

## 📌 **2️⃣ EVM Structure and How It Works**

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c2ba559c-cb6d-4c61-bec3-1760fafc9a92/39173aa4-ca64-41a5-832f-e4da8553dfad/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664TC25ANY%2F20250521%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250521T213318Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEA4aCXVzLXdlc3QtMiJIMEYCIQDd%2BPNyPLP2TnQO2%2BZ%2BO5UmScLpMQ51irnu3UHoRhBaiAIhAIO%2F53fnDK8dG68lkgCKT8ivo%2F%2FfMF9ChoWX77%2FekBWJKogECMb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igzk4lA6lKeJ8puB8roq3AMXuBboC27cIJDZsnZJEpyRSCuh1th2NK%2ByGVSom1tpZu2CHGOhBisYSQyZg5%2FQYXxM5OgB7y3ahPL1y5%2F10dOG%2FZjZpJFfikDEJHO5lkBVOGZUWJHVjGlReN7Ig4%2BD3iVUDwvBm4uS%2BgKGKO130r%2FDHu8D4YSi%2B1atNIgnOKNgNTVLbV%2BaSjH7%2FUbKE8lRvh%2BcA2xS8u6mqLZp%2Fau2fNIrGLGr%2Fjo56NpWNXcY7cbXd6e%2FBcbexyg9YRONS3BhlGkVmuPjTJEQgPOBi6x08JDIA3qbC7lZKNqvVqKh%2BbODZy8IZkSSv106wLxPF%2FHf0V6OOGcon9g1%2FNmCUe6d3prFCH86ba1mj%2BqNpji3vlx2Icdm8hsY42SfpN52UoneExSMyp1clD6KbzQLMYzRjBlZw6VVbgCAVQZ7x%2BPjL735UCvgFI32xG7Y7PE%2F4u7e25Xxmf9Ko12aDG8UYPNE8WY93JKnT8VYtkVxRusHCQQ96srxfD60TuDVh2JmkZypuFKo%2Bn7kM1EUQB0kQ2UOC2L9F1sYG3qPhluoQoM5nI8%2F2IqSfyjQ8uZA1N1fEk5HMd4n%2F9tcC3%2BBAtNWZitbee2iCcTOTKGLiNMDknIK5DAiPCviMzPHn6feTBY6kDDAhrnBBjqkAYlWJMYYdLZkTLlF4DMa2v9kNZTi703nDr0CCDz1EHj%2Bg2LFVQCT6UoYtw0t4LqNP69ei2xJT4EBhLLhBcqgPNJpgDQUHQP9gjfr5KtAJRewgO5e9wVxr1PKWdrTdSWmsLYGibuPBn%2B0yVtlL2p2nPeWCQsgmkTLRpesODld%2BR25%2FU15sPkOIHu6vbF2Jg6mFAe3ljVmaRscWEoRXFjkJ2QDKsE9&X-Amz-Signature=8c4fac1aae31a31de15aeb5058738b25a72cde4d566e5081f0ad5bf110225908&X-Amz-SignedHeaders=host&x-id=GetObject)

## 📌 **Key Concepts of the EVM Execution Model**

## **1️⃣ What information is stored in the EVM State?**

📌 **Storage is the “permanent storage” of smart contracts**, and once stored, values are **maintained even after the transaction is completed**.
💡 **Information stored**

- **State variables** of smart contracts
- **User data** of specific contracts (e.g., balance, token ownership information)
- Data stored via `mapping` or `struct`
  📌 **Analogy**
  > Storage is like a bank vault.
  > If you store money (data) in a vault, you can retrieve it later.
  >
  >     However, opening the vault is expensive (gas fees), so it's best not to open it frequently.
  >
  > ✅ **Features**
  > ✔️ **Permanently stored on the blockchain** → Once stored, changes require gas fees
  > ✔️ **Stored by all nodes** → Maintained across the entire Ethereum network
  > ✔️ **Data persists even after transactions complete**

---

## **2️⃣ What information is retrieved from the EVM World State?**

📌 **The World State represents the “entire state” of the Ethereum blockchain at a given moment.**
It maintains the state and related information of each account.
💡 **Information retrieved**

- **State of each account (Account State)**
- **Externally Owned Account (EOA)**
- Address
- Balance
- Nonce (number of transactions executed by the account)
- **Smart Contract Account**
- Code Hash (code of the smart contract)
- Storage Root Hash (storage state of the smart contract) - **Information about the currently executing block (Block Header)**
- Block Number
- Gas Limit
- Difficulty

  📌 **Analogy**

  > Think of the World State as a **“database for the entire bank.”**
  > It is a **huge ledger** that records how many accounts there are, how much balance each account has, what the recent transactions were, and so on.
  > ✅ **Features**
  > ✔️ Maintains the **current state** of all accounts
  > ✔️ Used to retrieve the storage of a specific account
  > ✔️ **Loads the state before executing a smart contract** and updates the state after execution

---

## **3️⃣ What information is stored in the EVM Global Namespace of Variables and Units?**

📌 **The EVM Global Namespace stores variables that are only maintained during the execution of a specific transaction.**

This information disappears **when the transaction execution ends.**

💡 **Information stored**

- **Transaction global variables**
- `MSG.SENDER` → Address of the person who sent the transaction
- `MSG.VALUE` → ETH (wei) sent with the transaction
- `MSG.DATA` → Input data of the transaction (function call information, etc.)
  📌 **Analogy**
  > **Global variables are like “delivery information”**.
  > When a package (transaction) arrives,
  >
  > you can check who sent it (MSG.SENDER),
  >
  >     how much was sent (MSG.VALUE),
  >
  >
  >     and what was requested (MSG.DATA).
  >
  > ✅ **Features**
  > ✔️ Maintained only while a specific transaction is executing
  > ✔️ Disappears when the transaction ends
  > ✔️ Provides information required by the executing smart contract

---

## **4️⃣ Why does the State Machine Cycle revert when Remaining OPCODES is NO?**

📌 **Reason for reverting when there are no OPCODEs**

EVM is a “machine that executes commands sequentially.”
However, if there are no commands (OPCODEs) left to execute, it means that there is no code to execute.

✅ **Two possible situations**

1. **Normal termination:**

- Termination commands such as `STOP` or `RETURN` are executed, and the process ends without issues.

2. **Abnormal termination (revert occurs):**

- If there should be an OPCODE left to execute but it does not exist, an error occurs →
  **Revert!**
  📌 **Analogy**
  > OPCODE is like a “recipe.”
  > To cook, you need to follow the recipe in order, but
  >
  > if the recipe disappears in the middle, you won't know how to finish cooking,resulting in failure (Revert).
  > ✅ **In summary...**
  > ✔️ If the OPCODE is missing, there is no code to execute.
  > ✔️ If the execution does not terminate normally with `STOP` or `RETURN`, a **Revertoccurs**.
  > ✔️ If a smart contract does not terminate normally during execution, it **rolls backall state changes**.

---

## **📌 Final Summary**

| **Storage**                | **Role**                                               | **Information stored**                               |
| -------------------------- | ------------------------------------------------------ | ---------------------------------------------------- |
| **Storage (EVM State)**    | Permanent storage for smart contracts                  | State variables, user data                           |
| **World State**            | Current state of the Ethereum blockchain               | Information about each account and block information |
| **Global Namespace**       | Variables maintained only during transaction execution | `MSG.SENDER`, `MSG.VALUE`, `MSG.DATA`                |
| **OPCODE Execution Cycle** | Smart contract execution flow management               | If there are no remaining OPCODEs, Revert            |

<summary>**ARGS Storage Contents**</summary>

## **Role of ARGS in the smart contract call process**

📌 **When a specific function of a smart contract is executed, ARGS stores the data necessary for executing that function.**

**📌 Execution process (function call example)**

1. User **sends a transaction** → Request to execute a specific function of the smart contract
2. Load the smart contract's address and storage data from the EVM World State
3. Store transaction-related data in ARGS (TX Data)
4. Analyze ARGS to determine which function to execute
5. Pass the required input values (parameters) to the smart contract's internal variables
6. **Execute the actual operation and return the result (or change the state)**

✅ **📌 Example code**

```solidity
contract MyContract {
    uint256 public myValue;
    function setValue(uint256 _value) public {
        myValue = _value;
    }
}
```

**📌 Execution flow**

- When the user calls `setValue(100)`, **transaction data (msg.data)** is stored as follows.
- **ARGS analyzes this data to find the function to execute and retrieves the parameters.**

💡 **ARGS internal storage data**
| Byte Offset | Data | Description |
| ------------- | ------------------------------------------------------------------ | ------------------------------- |
| `0x00 - 0x03` | `0x60fe47b1` | Function identifier (Function Selector) |
| `0x04 - 0x23` | `0000000000000000000000000000000000000000000000000000000000000064` | Function parameter value `_value = 100` |
📌 **Analogy:**

> ARGS is “a letter (transaction data) sent to the smart contract.”
>
> The letter contains **“Execute this function (setValue)!”** and **“Input value (100)”**.
>
> The smart contract reads the letter and determines “Which function to execute?” and“What is the input value?”

### **🔹 EVM's data storage method**

EVM has three main storage spaces:
| Storage space | Description |
| ----------- | ---------------------------------------------- |
| **Stack** | Temporary storage space using the LIFO method |
| **Memory** | Volatile temporary storage, initialized when the transaction ends |
| **Storage** | Permanently stored in the blockchain state |

### 📌 Analogy:

- \*Stack\*\* is like a memory button on a calculator that temporarily stores numbers.
- **Memory** is a temporary notepad needed only while a program is running.
- **Storage** is like a hard disk that permanently stores data.

### **🔹 EVM execution environment**

When executing a smart contract, the EVM environment includes the following information.

- **Contract bytecode** (smart contract code)
- **Storage** (permanent storage)
- **Memory** (temporary storage)
- **Stack** (temporary space for operations)
- **Gas**: Computational resources available for execution
- **Environment variables**: Caller address, block information, etc.

---

## 📌 **3️⃣ EVM Gas**

### 🔹 **Gas Concept**

- In the EVM, all operations such as computation, storage, and transmission consume **gas**.
- Gas is the **fuel of the Ethereum network**, and the more computations are performed, the more gas is consumed.
- If gas runs out, the execution is terminated with an **Out-of-Gas (OOG)** error, and all operations are canceled.

### 📌 Analogy:

- In the EVM, gas is like the **fuel (gasoline)** in a car.
- The more distance a smart contract (car) travels or the heavier the load it carries, the more fuel it consumes.
- Just as a car stops when it runs out of fuel (gas), the EVM execution also stops immediately.

### 🔹 **Gas Cost and Gas Price**

- **Gas Cost**: The amount of gas required for a specific operation. (e.g., addition (ADD) requires 3 gas, multiplication (MUL) requires 5 gas)

- **Gas Price**: The amount of Ether (ETH) paid per unit of gas. A higher gas price ensures faster transaction processing.

| Concept         | Definition                                 |
| --------------- | ------------------------------------------ |
| Gas Cost        | Amount of gas consumed by an operation     |
| Gas Price       | Amount of Ether (ETH) paid per unit of gas |
| Transaction Fee | Gas Cost × Gas Price                       |

---

## 📌 **4️⃣ Status Change Failure: Out of Gas (OOG) and Revert**

We learned earlier that transactions fail when there is insufficient gas, but we need to clearly understand the **difference between OOG (Out of Gas) and Revert**.

| **Failure Type**     | **Description**                               | **Result**                     |
| -------------------- | --------------------------------------------- | ------------------------------ |
| **Out of Gas (OOG)** | Insufficient gas during transaction execution | All changes are rolled back    |
| **Revert**           | `require()` or `revert()` is executed         | Rollback without status change |
| **Assert failure**   | `assert()` statement fails                    | All gas consumed & rolled back |

- **Revert caused by Require() statement**: Only the gas used in the previous operation is consumed, and the remaining gas is returned without any state changes.

- **Out of Gas (OOG)**: All gas has been consumed, but there are still operations remaining, so execution is rolled back, and the gas already used is not returned.

- **Assert failure**: Even if less gas has been used, when `assert()` is executed, **all remaining gas is consumed and then rolled back**.

📌 **Analogy**

> OOG is like “the car stopped because it ran out of gas.” Revert is like “the car cannot start because the seatbelt is not fastened.” Assert failure is like “the engine exploded and the car was destroyed.”

---

## 📌 **5️⃣ Smart Contract Deployment and Runtime**

Smart contracts have two types of code:
| Type | Description |
| ----------------------- | ----------------------------------------------------------------------------------------------- |
| **Deployment Bytecode** | Code used only when deploying the contract (including initialization code such as constructors) |
| **Runtime Bytecode** | Code executed when the contract is called by an actual user after deployment |

- During deployment, **initial setup (such as state initialization)** is performed, and only the **Runtime Bytecode** required for execution is stored on the blockchain.

## 🚩 **Step 1: Deployment**

### 🔹 **What is it?**

- The **first step of installing a smart contract on the blockchain**.
- During deployment, the smart contract's **initial setup (initializing state variables, setting variables)** is performed.
- This is typically done using a special function called a **constructor**.

### 🔹 **What is Deployment Bytecode?**

- A special form of code used only when installing a smart contract on the blockchain for the first time.

- It is deployed in a format that includes the _constructor code + the actual execution code of the contract (Runtime Bytecode)_.

- This code is executed only once, and after that, only the Runtime Bytecode is stored on the blockchain, while the Deployment Bytecode is discarded.

### 📌 **Specific Process Example (Detailed Steps)**

| **Sequence** | **Process Description**                                                                                                                    |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------- | --- | --- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| ①            | **Transaction transmission** by the user to deploy the smart contract to the blockchain                                                    |
| ②            | The **to** address of the transaction is a special address (**0x0**). In other words, a request to create a new contract on the blockchain |
|              | --------                                                                                                                                   | ---------------------------------------------------------------------------------------------- |     | ①   | The **to** address of the transaction is a special address (**0x0**). In other words, it is a request to create a new contract on the blockchain. |
| ③            | The **data** field in the transaction contains the deployment code (**Deployment Bytecode**).                                              |
| ④            | The **EVM** loads this code and executes it once to perform **initialization tasks (setting state variables, etc.)**.                      |

| ⑤ | Once initialization is complete, only the **Runtime Bytecode** is stored on the blockchain. |

### 📌 **Analogy**

- Deploying a smart contract is like **installing software on a new computer**.
- During the installation process, various **initial settings (license authentication, user settings)** are made,
- The installation program is deleted when its role is complete, and only the actual program to be executed remains.

---

## 🚩 **Step 2: Execution Process (Runtime)**

### 🔹 **What happens?**

- This is the stage where users actually call the smart contract and **interact with it (function calls, etc.)**.
- Only the Runtime Bytecode stored on the blockchain is used.
- Every time the user calls a function of the smart contract, the Runtime Bytecode is executed on the EVM.

### 🔹 **What is Runtime Bytecode?**

- Code stored on the blockchain and used continuously.
- Code that is repeatedly executed every time the user interacts with the smart contract.
- Contains only the functions and logic to be executed, excluding initialization code such as the constructor, which is generated from the Deployment Bytecode.

### 📌 **Specific Process Example (Detailed Steps)**

| **Order** | **Process Description**                                                                                                               |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| ①         | The user sends a transaction calling a specific function within the smart contract.                                                   |
| ②         | The EVM reads the **function identifier** (Function Identifier) called in this transaction.                                           |
| ③         | The **Dispatcher** in the Runtime Bytecode reads the function identifier that was called and moves to the corresponding function code |
| ④         | The code of the called function is executed, which **changes the blockchain state** or **returns response data**                      |

### 📌 **Analogy**

- The runtime stage is similar to when **a user directly executes software** that has already been installed.
- Example: Click on an installed game to execute → User plays the game

---

### 📌 **Example of the entire flow of deployment and runtime**

- Assume that there is a smart contract written in Solidity:

```solidity
contract Example {
    uint public count;
    constructor(uint _initial) {
        count = _initial; // Initialization in the constructor
    }
    function increment() public {
        count = count + 1;
    }
}
```

### **🔸 Deployment Process**

| Step | Task                                                                                                         |
| ---- | ------------------------------------------------------------------------------------------------------------ |
| ①    | Create and send the deployment transaction for the `Example` smart contract                                  |
| ②    | The transaction is sent to the 0x0 address and contains the Deployment Bytecode                              |
| ③    | The EVM executes the Deployment Bytecode and runs the constructor (initializing `count`)                     |
| ④    | Once execution is complete, only the **`count`** **value and Runtime Bytecode are stored on the blockchain** |

### **🔸 Execution Process (Runtime)**

| Step | Task                                                                                                                                         |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| ①    | The user sends a transaction calling the `increment()` function of the smart contract                                                        |
| ②    | The EVM reads the function identifier (Function Identifier) from the transaction data and sends it to the Dispatcher of the Runtime Bytecode |
| ③    | The Dispatcher finds the location of the `increment()` function using the identifier and executes it                                         |
| ④    | `increment()` is executed, and the blockchain state is updated (`count` value increases)                                                     |

---

## 🎯 **Summary**

| Category                | Role                                                 | Characteristics                                   |
| ----------------------- | ---------------------------------------------------- | ------------------------------------------------- |
| **Deployment Bytecode** | Used only during the initial deployment phase        | Includes the constructor, deleted after execution |
| **Runtime Bytecode**    | Repeatedly used when the contract is actually called | Includes user functions, stored permanently       |

- Initial setup in the Deployment phase → Only the **execution code** in the Runtime phase is used thereafter.

  This two-stage distinction is designed to ensure that smart contracts are installed and operated safely and efficiently on the blockchain!

---

## 📌 6️⃣ **EVM Opcode and Execution Flow**

- **Opcode** is a **low-level instruction** executed by the EVM.
- Smart contract languages (Solidity) are compiled and converted into Opcode, which is then executed by the EVM.

### 📌 Analogy:

- **Solidity code** is like a **high-level language (English)** that humans can read, while Opcode is like **machine language** that the EVM can understand directly.
- Solidity → EVM Opcode → Mechanical execution → State change

---

## 📌 7️⃣ **Types of EVM Opcodes**

| Category                              | Main Opcode Examples                     |
| ------------------------------------- | ---------------------------------------- |
| **Arithmetic Operations**             | ADD, SUB, MUL, DIV, MOD                  |
| **Memory and Storage**                | MSTORE, MLOAD, SSTORE, SLOAD             |
| **Flow Control**                      | JUMP, JUMPI, STOP, RETURN                |
| **Logical Operations**                | AND, OR, NOT, XOR, LT, GT, EQ            |
| **Access to Environment Information** | CALLER, CALLVALUE, TIMESTAMP, BLOCKHASH  |
| **System Operations**                 | CREATE, CALL, DELEGATECALL, SELFDESTRUCT |

---

## 📌 **8️⃣ Proxy Contract Pattern (Reference)**

- Smart contracts are **immutable after deployment** by default, but **Proxy Contract Pattern** allows for upgrades.
- The contract containing the actual logic is deployed separately, and the proxy contract is designed to point to the logic contract, allowing only the logic contract to be replaced when necessary.

## ✅ Accurate Proxy Pattern Structure

The actual proxy pattern structure usually consists of two contracts, as follows.
| Contract Type | Role | Description |
| --------------------------------------- | ----------------------------------------- | ------------------------------------------------------------- |
| ✅ **Proxy Contract (프록시 컨트랙트)** | Manages state variables and delegates logic contract calls | Receives all user requests and stores **data (state)** |
| ✅ **Logic Contract (Logic Contract)** | Actual business logic implementation (calculation and processing) | **Does not store state data**, only performs logic processing |

---

## 🎯 Proxy Contract Pattern Architecture (2-contract structure):

```plain text
User → Proxy Contract (state variables + address storage)

↓ Delegate (delegate)
           Logic Contract (only performs logic processing)
```

- **Proxy Contract** stores state variables (data) but does not have actual logic, and when a call comes in, it **delegates processing to Logic Contract**.
- **Logic Contract** only performs calculations and does not store data, always using data from Proxy Contract.

---

## 🔄 Upgrade process (specific):

- Let's say that after initial deployment, a problem occurs while using Logic Contract (C).
- At this point, deploy the new, modified Logic Contract (D).
- Change the **address of Logic Contract** inside Proxy Contract from Logic Contract (C) to Logic Contract (D).
- From then on, the Proxy Contract calls Logic Contract (D), and the logic is immediately upgraded.

## ✅ Proxy Contract Pattern Usage Process

| Step                   | Description                                      | Hotel Analogy                                        |
| ---------------------- | ------------------------------------------------ | ---------------------------------------------------- |
| 1️⃣ Initial deployment  | Deploy and connect Proxy and Logic v1            | Reception directs guests to a room on the 1st floor  |
| 2️⃣ Issue detected      | Issue found in the existing Logic Contract       | The 1st floor room is inconvenient                   |
| 3️⃣ Upgrade preparation | Deploy the new Logic Contract                    | Prepare a new room on the 2nd floor                  |
| 4️⃣ Upgrade Execution   | Proxy updated to point to the new Logic contract | Reception updated to guide guests to 2nd floor rooms |
| 5️⃣ Completed           | Proxy remains unchanged; Logic upgrade completed | Guests now use the upgraded 2nd floor rooms          |

### 📌 **Issues** with the Proxy Contract Pattern

Since the Proxy Contract delegates actual logic processing to another contract, the following structure is required inside the Proxy:

```solidity
address public logicContract; // Store the logic contract address
```

- If a user with permission to change this variable (`logicContract`) is malicious,
  they can change the Proxy to point to a malicious Logic Contract.
- As a result, all user requests made through the Proxy can be manipulated or assets can be stolen, causing damage.
  📌 **Analogy:**
  > It's like a bank teller (Proxy) directing customers to a specific service team (Logic Contract),
  > but if the teller colludes with a scammer and directs customers to a fake service team, customers can easily be harmed.

---

## 📌 **Solutions and security measures**

There are various ways to prevent such attacks:

### ✅ 1) Strengthen access control

- Set very limited permissions for changing the Proxy Contract address.
- Generally, allow changes only through **multisig** or **governance (DAO voting)**.

### ✅ 2) Implement Timelocks and Transparent Upgrade Processes

- Set a **fixed delay time** (Timelock) before logic changes and notify all users transparently.
- This ensures sufficient time to verify the legitimacy of any detected changes.

### ✅ 3) Immutability & Limited Upgradability

- Design the system so that the Proxy Contract address can only be changed once, or design it so that only specific areas can be upgraded, thereby minimizing the possibility of attacks.

### ✅ 4) Transparent Proxy Pattern

- The Transparent Proxy pattern clearly separates the functions that handle upgrades from the functions actually called by users.
- This prevents situations where administrators accidentally call the wrong function or users unintentionally access restricted areas.

### ✅ 5) Use standardized Proxy implementations such as EIP-1967

- By using **secure, standardized Proxy Contract implementations** provided by OpenZeppelin and others, security vulnerabilities are reduced.

---

## 🎯 **Summary**

As you correctly pointed out, managing the Logic Contract address is the most important security issue in the Proxy Contract pattern. If exploited, it can cause significant damage, so

- **Access permission management**
- **Transparent upgrade process**
- **Use of verified standard implementations**
  Managing these three elements well can maximize security.

---

## 📌 **Summary and Conclusion**

- **EVM** is the core environment where Ethereum smart contracts are executed.
- The **gas system** prevents malicious infinite loop programs.
- The **proxy pattern** enables smart contract upgrades.
- Understanding the **internal workings of the EVM and opcodes** is essential for ensuring the stability of smart contracts.

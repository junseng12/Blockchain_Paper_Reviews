## 1️⃣ **What is Vyper? Why was it created?**

Vyper is a language for writing **smart contracts** that run on the **Ethereum Virtual Machine (EVM)**. It was designed to improve **security, readability, and auditability** over Solidity. In particular, **“making it as difficult as possible for developers to accidentally write vulnerable code”** is the core philosophy of Vyper.
💡 **Key design philosophies of Vyper**

1. **Keep code as intuitive as possible** → Code should be written in a way that is easy for humans to read.
2. **Prioritize security** → Remove features that could cause vulnerabilities.
3. **Structure that facilitates auditing** → Code flow is clearly visible.

## 2️⃣ **Major security issues in Solidity and Vyper's approach**

In Solidity, many smart contracts have been hacked due to **unexpected vulnerabilities**. According to research, a significant number of deployed smart contracts had the following vulnerabilities.

### 📌 **💀 Three major vulnerabilities in Solidity**

| Vulnerability type     | Description                                        | Example                                                                  |
| ---------------------- | -------------------------------------------------- | ------------------------------------------------------------------------ |
| **Suicidal Contracts** | Anyone can delete the contract                     | Designed to allow anyone to execute `selfdestruct()`                     |
| **Greedy Contracts**   | Cannot withdraw Ether under certain conditions     | `require()` condition is not met, causing funds to be permanently locked |
| **Prodigal Contracts** | Attackers can withdraw Ether without authorization | Incorrect access control allows anyone to withdraw funds                 |

## **Vyper prevents these issues by not supporting features that cause vulnerabilities.**

## 3️⃣ **Vyper vs Solidity Comparison**

Unlike Solidity, Vyper **intentionally removes several features**. The reason is **to enhance security by reducing the possibility of developer errors**.

### 🔍 **Features removed from Vyper and the reasons why**

| Solidity feature         | Reason for removal in Vyper                                                      | Example                                                                          |
| ------------------------ | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| **Modifiers**            | May contain hidden logic                                                         | Permission controls such as `onlyOwner` must be written directly in the function |
| **Class Inheritance**    | Complicates code flow and makes auditing difficult                               | No inheritance functionality such as `contract A is B`                           |
| **Inline Assembly**      | Direct execution of EVM low-level instructions possible → security vulnerability | Code like `assembly { mstore(0x40, add(mload(0x40), 0x20)) }` is not allowed     |
| **Function Overloading** | Reduced readability when multiple functions with the same name exist             | `function add(uint a) {...}` / `function add(uint a, uint b) {...}` not possible |
| **Implicit Typecasting** | Potential data loss during conversion                                            | Incorrect data may occur during `uint32 → uint16` conversion                     |

✅ **Vyper alternatives:**

- Validate directly within the function instead of using `Modifiers`
- Write clear code instead of using `Class Inheritance`
- Use only standard functions instead of `Inline Assembly`
- Use clear function names instead of `Function Overloading`
- Use clear `convert()` functions instead of `Implicit Typecasting`

## 4️⃣ **Infinite Loop Prevention**

**Solidity allows developers to write infinite loops,** but Vyper prevents them with the following restrictions.
| Feature | Solidity | Vyper |
| ------------- | ------------------------------- | --------------------------------------------- |
| `while` statement | ✅ Allowed | ❌ Not allowed |
| `for` statement | ✅ Allowed (unlimited iterations) | ✅ Allowed, but **the number of iterations must be specified** |
| **Recursive calls** | ✅ Allowed | ❌ Not allowed |
**📌 Reason:**
Allowing infinite loops makes it impossible to predict gas consumption and makes the code vulnerable to attacks such as “Gas Limit Attack.”

---

## 5️⃣ **Vyper's clear state change mechanism**

Solidity can be difficult to predict because **it is unclear when declared variables or states change**. Vyper recommends following the **“Condition → Effects → Interaction”** order to prevent this.
✅ **Considerations when writing code in Vyper**

1. **Condition (condition check)** → The required state must be checked before executing the function.
2. **Effects (state changes)** → Perform necessary state changes
3. **Interaction (interaction with external contracts)** → Execute last
   💡 **Example code:**

```python
@public
def withdraw(amount: uint256):
    assert self.balance >= amount  # Condition
    self.balance -= amount         # Effects
    send(msg.sender, amount)       # Interaction
```

🚨 **Conversely, if Interaction is executed first, it may be vulnerable to reentrancy attacks!**

## 6️⃣ **Vyper Function Decorators**

In Vyper, **decorators (@) are used** to clarify the role of functions.
| Decorator | Description | Example |
| ----------- | -------------------------- | --------------------------------------------- |
| `@public` | Public function (can be called externally) | `@public def deposit(): ...` |
| `@private` | Private function (cannot be called externally) | `@private def _internal_logic(): ...` |
| `@constant` | Function that cannot change state | `@constant def get_balance() -> uint256: ...` |
| `@payable` | Function that can receive Ether | `@payable def receive_funds(): ...` |
🚨 Using `@constant` and `@payable` together will cause an error → **This is because functions that send money must change the state!**

---

## 7️⃣ **Vyper's security features**

### 📌 **🛡️ Overflow prevention**

In Solidity, you must use the `SafeMath` library to prevent overflow,
but **Vyper automatically applies overflow prevention to all operations by default**.
💡 Solidity code (vulnerable code)

```solidity
uint256 a = 2**256 - 1;
a = a + 1;  // Overflow occurs → becomes 0
```

🔥 **Vyper automatically throws an exception → safe code execution!**

## 8️⃣ **Vyper's data storage method**

| Storage location | Description                                            | Example usage                      |
| ---------------- | ------------------------------------------------------ | ---------------------------------- |
| **Global State** | Smart contract storage space (expensive and permanent) | `self.balance = 100`               |
| **Logs**         | Recorded on the blockchain but cannot be read          | `log.Transfer(msg.sender, amount)` |

📌 **Logs cannot be read within the contract and can only be viewed on external services such as Etherscan!**

<summary>Log VS. Function</summary>

- **Difference between events (`event`) and function execution**
  | | **Function execution (\*\***`function`\***\*)** | **Event log (\*\***`event log`\***\*)** |
  | ---------------------- | -------------------------------------- | -------------------------------------------- |
  | Execution method | Executed within the contract | Only “recorded” on the blockchain |
  | Data storage | Changes the contract's state (`Global State`) | Stored in the blockchain log |
  | Cost (gas) | Expensive (includes Global State changes) | Relatively inexpensive (no storage space required) |
  | Read within contract | ✅ Possible (using state variables within functions) | ❌ Not possible (logs only exist on the blockchain) |
  | Use cases | Logic requiring state changes | Cases where logging is required but state changes are not needed |

### **📌 Key points**

- **Event logs (\*\***`event`\***\*) are execution (X), recording (O)**
- **No internal state changes in the contract** → Only a trace of “what happened” remains
- **Recorded on the blockchain, but cannot be read again within the contract**
- **Can be verified externally (Web3.js, Etherscan, The Graph, etc.)**

---

### **📌 ✅ Analogy: “Official certification stamp”**

👉 **Calling `event`\*\*** within the contract is like stamping an official document.\*\*

- Stamping the document does not change its contents.
- However, anyone can see that the document has been officially “issued.”
- To modify the document again, you must save it separately, but the stamp itself does not serve that purpose.
- You can look at the stamp and confirm that “this is the real document,” but it does not affect the creation of the document.
  ➡️ **Event logs serve the same purpose of recording that a transaction actually occurred!**

## **※ Vyper's online code editor & compiler**

Vyper has an online code editor and compiler

- Smart contracts ⇒ Converts to bytecode, ABI, and LLL in a web browser
- Provides only one version of the compiler software and updates it regularly
- Etherscan supports the online Vyper compiler to select the compiler version
- Remix also supports the Vyper plugin in the settings tab

---

## 🔥 **Conclusion: Summary of Vyper's features**

✅ **More secure than Solidity and designed to prevent errors**

✅ **Easy-to-read and audit-friendly structure**

✅ **Removes unnecessary features (modifiers, inheritance, etc.) to maintain concise code**

✅ **Prevents security issues such as infinite loops and overflows at the source**

# 1. Smart Contract Security

## 🔹 Security Best Practices

### 1️⃣ **Defensive Programming**

- **Minimalism & Simplicity**: The simpler the code, the stronger the security. Reduce unnecessary features and focus on core logic.
- **Code Reuse**: Utilizing verified libraries and existing contracts enhances security.
- **Code Quality**: Smart contracts should not be treated lightly like web development. They require the precision of aerospace engineering-level development.
- **Readability & Auditability**: Clear and easy-to-understand code is secure code.
- **Test Coverage**: All possible inputs must be tested. Unexpected inputs can damage the contract.

## 🔹 **Key Security Vulnerabilities and Prevention Methods**

### ⚠️ 1. **Reentrancy (Reentrancy Attack)**

### 🛑 **Vulnerability Description**

- When a contract sends Ether to an external address, if that address is a malicious contract, it can call back (Fallback function) and execute the original contract again.
- The famous **DAO hack** occurred in this manner, resulting in losses of hundreds of millions of dollars.

### 📌 **Vulnerable Code Example**

```solidity
function withdraw(uint _amount) public {
    require(balances[msg.sender] >= _amount);
    payable(msg.sender).transfer(_amount);  // 🔥 Vulnerability occurs!
    balances[msg.sender] -= _amount; // ❌ State update occurs later
}
```

- When executing `transfer()`, if the attacker's contract calls the Fallback function and re-executes `withdraw()`, the original contract's state can be updated repeatedly before the state update is completed.

### 🛠 **Solution**

1. **Checks-Effects-Interactions pattern**: State changes must be performed before external calls.
2. **Use Reentrancy Guard**: Add a mutex variable to prevent the contract from being called again.
3. **When using `call()` instead of `transfer()`, pass the minimum gas (2300 gas limit).
   ✅ **Updated Code\*\*

```solidity
bool private locked;
function withdraw(uint _amount) public {
    require(!locked, “Reentrancy detected!”);
    locked = true; // 🔒 Set lock
    require(balances[msg.sender] >= _amount);
    balances[msg.sender] -= _amount;

payable(msg.sender).transfer(_amount);
    locked = false; // 🔓 Unlock
}
```

### ⚠️ 2. **Integer Overflow & Underflow**

### 🛑 **Vulnerability Description**

- If an integer value exceeds the maximum/minimum range, it may cause unexpected results.
- For example, adding 255 to a `uint8` type variable can result in 0.

### 📌 **Vulnerable Code Example**

```solidity
function setBalance(uint _amount) public {
    balance[msg.sender] += _amount;  // 🔥 Overflow may occur
}
```

### 🛠 **Solution**

1. **Use the SafeMath library**
2. Overflow/underflow is automatically prevented in Solidity 0.8.x and above.
   ✅ **Improved code (SafeMath applied)**

```solidity
using SafeMath for uint256;
function setBalance(uint _amount) public {

balance[msg.sender] = balance[msg.sender].add(_amount); // Prevent overflow
}
```

---

### ⚠️ 3. **Authentication using tx.origin (Phishing Attack)**

### 🛑 **Vulnerability Description**

- Using `tx.origin` to authenticate the contract owner makes phishing attacks possible.
- An attacker can trick a user into calling their contract, thereby obtaining the victim's address from the original contract and stealing their assets.

### 📌 **Vulnerable code example**

```solidity
function withdraw() public {

require(tx.origin == owner, “Not the owner!”);  // ❌ Security vulnerability
    payable(msg.sender).transfer(address(this).balance);
}
```

### 🛠 **Solution**

1. **Use msg.sender instead of tx.origin**
2. Use multi-signature and approval systems
   ✅ **Improved code**

```solidity
function withdraw() public {
    require(msg.sender == owner, “Not the owner!”);  // ✅ Secure method
    payable(msg.sender).transfer(address(this).balance);
}
```

---

### ⚠️ 4. **Unchecked External Call**

### 🛑 **Vulnerability Description**

- When calling an external contract using `call()` or `send()`, if the return value is not checked, an attacker can create a transaction that intentionally fails and corrupts the contract's state.

### 📌 **Vulnerable Code Example**

```solidity
function sendFunds(address payable recipient, uint amount) public {

recipient.call{value: amount}(“”);  // ❌ Return value not checked
}
```

### 🛠 **Solution**

1. **Check the return value and call revert() if it fails**
2. **Use transfer() if possible (2300 gas limit)**
   ✅ **Fixed code**

```solidity
function sendFunds(address payable recipient, uint amount) public {
    (bool success, ) = recipient.call{value: amount}(“”);
    require(success, “Transfer failed!”); // ✅ Check return value
}
```

🔍 **Explanation**

- Store the return value of `call()` in the `bool success` variable.
- If `success` is `false`, **revert** the **transaction** to cancel execution.
- This allows the contract state to remain normal even if **the ether is not transferred.**

### ✅ **Why** is \*\*`transfer()` safer?

```solidity
recipient.transfer(amount);
```

- `transfer()` internally uses `call()`, but it has a **gas limit (2300 gas)**, so it cannot execute complex logic when executing the `fallback` function.
- Additionally, `transfer()` automatically **reverts the transaction** if it fails, so there is no need for separate `require(success, “Transfer failed!”)` handling.
📌 **In summary, use **`transfer()`** whenever possible, and if you must use **`call()`\*\*, always check the return value!
<summary>Analogy and specific examples of misuse</summary>

### 💡 **Easy-to-understand analogy**

✅ **Bank transfer example**
Let's consider a situation where a bank sends money to a customer.
1️⃣ **Vulnerable method (unchecked call)**

- A bank employee transfers 1 million won to a customer without checking whether the transfer was successful, simply entering the information into the system and ending the process.
- Due to an issue with the customer's account, the transfer fails, but the bank's system does not detect this and displays “Transfer Complete.”
- As a result, the customer does not receive the money, but the bank's system already processes it as withdrawn → **The money disappears!** 😱
  2️⃣ **Secure method (Checked Call)**
- After sending the transfer, the bank employee must confirm whether the transfer was successful.
- If the transfer fails, a “Transfer failed” message is displayed, and the transfer is retried or the customer is notified.
- In other words, **exception handling is performed when the transfer fails to prevent the money from disappearing.** ✅

## 🧨 **Attack Process (Exploit Flow)**

1️⃣ **The attacker** **deposits 1 ETH into `VictimContract`\*\***

- `victim.deposit{value: 1 ether}();` is executed → `balances[msg.sender]` increases by `1 ether`
  2️⃣ **The attacker** calls **`sendFunds()`\*\*** to request 1 ETH be sent to themselves\*\*
- `victim.sendFunds(payable(address(this)), 1 ether);`
- VictimContract attempts to send 1 ETH to `MaliciousContract` using `call()`
  3️⃣ **However, the attacker's contract intentionally fails the transaction (\*\***`fallback() { revert(); }`\***\*)**
- In other words, **the ether transfer fails!**
- But VictimContract does not check the return value of `call()`, so **the balance is deducted even if the transaction fails!**
  4️⃣ **As a result, the **`balances[msg.sender]`** value of the VictimContract decreases, but the Ether remains unchanged.**
- 💰 The attacker can continue to withdraw funds even after reducing the balance to 0.

## 🤔 **“But can't the hacker just steal the money directly?”**

That's right, this method alone doesn't allow the hacker to directly steal the money.
However, **this technique can be used to launch larger attacks!**
For example:
✅ **You can block normal users from withdrawing funds.**
✅ **You can launch a DoS (Denial of Service) attack to disrupt the service and prevent specific users from withdrawing funds.**
✅ **This can also be used to bypass conditions like “users with a balance of 0 cannot withdraw funds.”**

---

## 🔥 **Real-world example (DoS attack)**

**2016 “GovernMental Ponzi Scheme” smart contract**
This was an Ethereum-based Ponzi scheme,
where **1,100 ETH was locked in the contract, but someone managed to prevent withdrawals using a similar method.**
Ultimately, the contract remained in a state where withdrawals were impossible despite funds being present.
As such, this attack technique can be used not to directly steal funds but to **paralyze the contract or restrict withdrawals to specific users.**

---

### ⚠️ 5. **Block Timestamp Manipulation**

### 🛑 **Vulnerability Description**

- If the `block.timestamp` value is used for randomness generation, miners can manipulate it to maximize their own gains.

### 📌 **Vulnerable Code Example**

```solidity
function lottery() public {

if (block.timestamp % 2 == 0) {
        winner = msg.sender; // ❌ Can be manipulated
    }
}
```

🔍 **Why is this code vulnerable?**
✅ The block timestamp can be manipulated by miners!
✅ Miners can **slightly alter the timestamp value** when mining a block to make it **even** or **odd**
✅ Ultimately, attackers can **manipulate blocks to always win**

### 🛠 **Solution**

1. **Use block hash or external oracle for random number generation**
2. **Minimize timestamp-dependent logic**
   ✅ **Updated code**

```solidity
function lottery() public {
    require(block.timestamp > lastPlayed + 1 hours, “Wait for next round!”);
    lastPlayed = block.timestamp;
    // Random number generation logic changed
}
```

## **📝 Block timestamps can be manipulated!**

✅ Using block timestamps directly for random number generation allows miners to manipulate the results!
✅ Contracts with random elements such as lotteries, sweepstakes, betting, and games must use oracles or block hashes!
✅ **“Block timestamps are not trustworthy”** → Just remember this! 🔥

---

### ⚠️ 6. **Unexpected Ether (unexpected Ether)**

### 🎭 **💡 Analogy: “Bank account balance error”**

Let's assume there is a bank.
The principle is that a bank account can only receive or send money if there is a transaction history.
However, what if, for some reason, money could enter the account without a transaction history?
If an attacker finds a way to add money to the account by “ignoring the bank's transaction history,”

- The issue of the deposit amount and the actual balance not matching could arise
- **If the withdrawal logic is based on the deposit amount, a bug could occur where money cannot be withdrawn**
  Applying this concept to smart contracts, there are **two ways unexpected Ether could enter the contract!**

---

### 🛑 **Two ways unexpected Ether can occur**

1️⃣ **Forced transfer via selfdestruct()**
2️⃣ **Pre-sending Ether before deploying the contract (Pre-sent Ether)**

---

### ✅ **1. Forced transfer using selfdestruct()**

### 🛠 **Vulnerability concept**

Ethereum has a function called **selfdestruct()**.
Calling this function destroys the contract and forces all remaining Ether to be sent to a specific address!
At this point, the **`fallback`** function in the target contract is not executed!
In other words, **Ether can be sent bypassing the contract's logic.**

### 📌 **Example code**

```solidity
contract Attacker {
    constructor() payable {} // Stores ether
    function attack(address payable target) public {
        selfdestruct(target); // Forces ether to be sent to the target contract
    }
}
```

## ✅ **Even if the target contract does not have a **payable** function or does not allow deposits, ether is forcibly sent!**

### ✅ **2. Send ether in advance before deploying the contract (Pre-sent Ether)**

### 🛠 **Vulnerability Concept**

Ethereum **contract addresses are generated deterministically**.
This means that you can predict in advance which address a specific contract will be deployed to!
➡️ **If an attacker sends Ether to that address in advance,
➡️ **when the contract is deployed, it will start with Ether already in it!\*\*

### 📌 **Attack method**

1️⃣ The attacker calculates the address where a specific contract will be deployed in advance.
2️⃣ The attacker sends Ether to that address first.
3️⃣ After the contract is deployed, **the contract code** **uses `this.balance`\*\***, causing an incorrect calculation\*\*.

---

### 🚨 **📌 Actual attack example: EtherGame contract**

```solidity
contract EtherGame {
    uint public finalMileStone = 10 ether;
    uint public depositedWei;
    function play() external payable {
        require(msg.value == 0.5 ether);

uint currentBalance = this.balance + msg.value; // ⚠️ Use this.balance (vulnerable!)
        require(currentBalance <= finalMileStone);
        depositedWei += msg.value;
    }
}
```

### 🛑 **Attack scenario**

1️⃣ The attacker forces the contract to receive 0.1 ETH using **selfdestruct()** or **Pre-sent Ether**.
2️⃣ Users who call the `play()` function afterward find that the `this.balance` value is corrupted, making normal gameplay impossible.
3️⃣ If the attacker forces a large amount to be sent, **no one can receive the reward!**

### ✅ **Solution**

- **Do not calculate the contract's Ether balance directly using `this.balance`, but use a separate **`depositedWei`\*\* variable instead.
- `depositedWei` records only the value sent by the user, so it is not affected by external attacks.

```solidity
contract SecureEtherGame {

uint public finalMileStone = 10 ether;
    uint public depositedWei;
    function play() external payable {
        require(msg.value == 0.5 ether);
        uint currentBalance = depositedWei + msg.value; // ✅ Safe method

require(currentBalance <= finalMileStone);
        depositedWei += msg.value;
    }
}
```

---

### ⚠️ 7. **Delegatecall vulnerability**

### 🎭 **💡 Analogy: “Accident involving a designated driver”**

Let's assume there is a driver.

- The car owner (smart contract) does not **drive (execute the function) directly** but entrusts the driving (Delegatecall) to a driver.
- However, **what if the driver causes an accident?**
- The car owner is responsible even though they only entrusted the driving.
- The driver could **change the insurance or steal the car owner's money.**
  ➡️ **Delegatecall() can cause similar problems in smart contracts!**

---

### ⚠️ **Problems with Delegatecall()**

- `delegatecall()` **executes the code of an external contract while using the calling contract's** **`storage`\*\*** as-is\*\*
- What if an attacker can **change the library address**?
- They can **set a malicious contract as the library** and execute `delegatecall()` to tamper with data!

---

### 🚨 **📌 Actual attack case: Parity Multisig Wallet hack**

### **First hack (ownership change)**

Parity's Multisig Wallet library initializes the wallet through the `initWallet()` function.
However, the `initWallet()` function is **set to public**, allowing anyone to call it!

```solidity
function initWallet(address[] _owners, uint _required) public {
    m_numOwners = _owners.length;
    m_owners = _owners;

m_required = _required;
}
```

🔹 The attacker calls the `initWallet()` function to **change the owner to themselves**
🔹 Then, they steal all the Ether from the wallet!

### **Second Hack (Permanent Lock via Selfdestruct)**

- The attacker owns the library contract itself and calls the `kill()` function to **selfdestruct the library**
- As a result, **all Multisig Wallets become inoperable**
- Millions of dollars worth of ETH are **permanently locked!**

---

### ✅ **Delegatecall() Security Measures**

1️⃣ **The library is** **configured to not have state variables using the `library` keyword**
2️⃣ **Library functions are** **only callable via `internal`\*\***, not `external`\*\***\*\*
3️⃣ **When using delegatecall(), hardcode the address of a trusted library\*\*

---

## ⚠️ 8. Default Visibilities (default visibility settings)

**🚨 Vulnerability description:**

- In Solidity, **if visibility specifiers are not explicitly specified, the default is** **`public`**
- This means that anyone can call the function from outside → Unwanted state changes are possible
  **📌 Vulnerable code example:**

```solidity
contract HashForEther {
    function withdrawWinnings() {
        require(uint32(msg.sender) == 0);  // Only specific addresses are allowed
        _sendWinnings();
    }
    function _sendWinnings() {

msg.sender.transfer(address(this).balance);
    }
}
```

✅ The `_sendWinnings` function should only be called internally, but **the default** **`public`\*\*** means that anyone can call it!\*\*
➡️ An attacker can call `_sendWinnings` directly and steal all funds
**✅ Solution: Always explicitly specify function visibility (\*\***`private`\***\*,** **`internal`\*\***,\*\* **`external`\*\***,\*\* **`public`\*\***)\*\*

---

## ⚠️ 9. External Contract Referencing (External Contract Reference Vulnerability)

**🚨 Vulnerability Description:**

- In Solidity, **external contract addresses can be set directly and called**
- However, if an attacker manipulates this, **connecting to a malicious contract can cause security issues**
  **📌 Vulnerable Code Example:**

```solidity
contract EncryptionContract {

Rot13Encryption encryptionLibrary;
    constructor(Rot13Encryption _encryptionLibrary) {
        encryptionLibrary = _encryptionLibrary;
    }
    function encryptData(string memory data) public {
        encryptionLibrary.rot13Encrypt(data);  // ❌ External contract may be malicious code
    }
}
```

➡️ If an attacker changes `encryptionLibrary` to a malicious contract, unexpected code execution is possible
**✅ Solution:**

- **Set the library contract address to **`immutable`\*\*\*\* to make it unchangeable\*\*
- **Create the contract directly when deploying (\*\***`new`\*\* **keyword used)**

```solidity
contract SecureEncryptionContract {
    Rot13Encryption public immutable encryptionLibrary;
    constructor() {
        encryptionLibrary = new Rot13Encryption();
    }
    function encryptData(string memory data) public {

encryptionLibrary.rot13Encrypt(data);
    }
}
```

## ➡️ **Enhance security by preventing changes through external input values!**

## ⚠️ 10. Short Address Attack

**🚨 Vulnerability description:**

- Solidity functions **read fixed-size data (32 bytes)**
- However, if **incorrect encoding (e.g., an address that is 19 bytes instead of 20 bytes)** is used, **the EVM automatically adds zeros (padding)**
- **This allows an attacker to send additional funds or perform actions different from the original intent**
  **📌 Vulnerable code example (ERC20 token transfer):**

```solidity
function transfer(address to, uint256 value) public returns (bool) {
    to.call{value: value}(“”);  // ❌ Short address attack possible
    return true;
}
```

- If an attacker sends an address that is **1 byte shorter, the EVM automatically adds zeros, resulting in funds being sent to the wrong address**
  **✅ Solution:**
- **Directly verify ABI encoding (\*\***`msg.data.length`\*\* **check)**
- **Apply address validation in third-party applications**
- **When implementing the ERC-20 standard, use **`safeTransfer`\*\* **(utilize the **OpenZeppelin\*\* **library)**

```solidity
import “@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol”;
contract SecureERC20 {
    using SafeERC20 for IERC20;
    function secureTransfer(IERC20 token, address to, uint256 amount) public {
        token.safeTransfer(to, amount);
    }
}
```

## ➡️ **Using the **SafeERC20** library automatically validates and prevents attacks!**

## ⚠️ 11. **Constructors with Care (Constructor Vulnerability)**

**🚨 Vulnerability Description:**

- **In Solidity v0.4.22 and earlier, constructors had to have the same name as the contract.**
- **If the names are different, they behave like regular functions** → Anyone can call them
- This is a critical vulnerability that allows attackers to take ownership of the contract after it is deployed

---

### 📌 Vulnerable code example

```solidity
contract OwnerWallet {
    address public owner;
    // ❌ This is a constructor, but it has a different name from the contract name → It behaves like a regular function

function ownerWallet(address _owner) public {
        owner = _owner;
    }
    // Fallback function to store Ether
    function () external payable {}
    function withdraw() public {
        require(msg.sender == owner);
        msg.sender.transfer(address(this).balance);
    }
}
```

### 📌 Vulnerability Description

- The `ownerWallet` function was intended to be a constructor by the developer, but it differs from the **contract name** **`OwnerWallet`\*\***
- Therefore, it is treated as a **regular function**, and anyone can call `ownerWallet()` after deployment to **change the ownership**
- An attacker can call this function to change `owner = attacker's address` and then call `withdraw()` to **steal all Ether**

---

### ✅ Solution

- **In Solidity 0.4.22 and above, use the **`constructor`\*\* keyword in the constructor
- **Ensure that the constructor is clearly defined without typos**

```solidity
contract SecureWallet {
    address public owner;
    // ✅ Use the constructor keyword
    constructor(address _owner) public {
        owner = _owner;
    }
    function withdraw() public {
        require(msg.sender == owner);
        msg.sender.transfer(address(this).balance);
    }
}
```

## ➡️ Using `constructor` ensures that **the function is recognized as a constructor regardless of the contract name**, so no one can call it.

## ⚠️ 12. **Uninitialized Storage Pointers**

**🚨 Vulnerability Description:**

- In Solidity, **uninitialized** **`storage`** **variables can point to existing storage slots**
- **Unexpected state changes may occur**
- This can be exploited to allow an attacker to modify important contract variables (e.g., `owner`)

---

### 📌 Vulnerable code example

```solidity
// A locked name registrar
contract NameRegistrar {

bool public unlocked = false;  // Locked by default
    struct NameRecord {
        bytes32 name;
        address mappedAddress;
    }
    mapping(address => NameRecord) public registeredNameRecord;
    mapping(bytes32 => address) public resolve;
    function register(bytes32 _name, address _mappedAddress) public {

// ❌ Uninitialized storage variable → Overwrites existing storage slot
        NameRecord newRecord;
        newRecord.name = _name;
        newRecord.mappedAddress = _mappedAddress;
        resolve[_name] = _mappedAddress;
        registeredNameRecord[msg.sender] = newRecord;

require(unlocked);  // ✅ Check lock status
    }
}
```

### 📌 Vulnerability Description

- **`newRecord`\*\*** is used without initialization\*\*
- In Solidity, **structures** are **set to `storage` by default**, so `newRecord` **overwrites existing storage slots**
- **An attacker** can **force the registry to be unlocked by putting a specific value** **in `_name` that can change the **unlocked\*\* state
<summary>Detailed explanation</summary>

### ⚠️ **Reason for vulnerability**

1️⃣ `newRecord` is recognized as a `storage` type

- In Solidity, structures (`struct`) are stored in `storage` by default
- In other words, `newRecord` overwrites **existing storage slots in the contract** in an uninitialized state
  2️⃣ Since `newRecord` overwrites the storage slot, the `unlocked` state can also be changed
- Solidity **stores contract variables (state variables) sequentially in storage slots (Slots)**
- The first member (`name`) of the `NameRecord` structure may overwrite the slot where `unlocked` is stored
- An attacker can manipulate the value of `_name` to a **specific value** to forcefully change `unlocked` to `true`
  3️⃣ The `require(unlocked);` condition becomes meaningless
- **If unlocked is manipulated to true, registration that was originally not allowed becomes possible**
- Ultimately, an attacker can register a new name and address even when it was originally not possible to register

---

### ✅ Solution

- **Explicitly store the structure in memory (using the \*\***`memory`\*\* **specifier)**

```solidity
function register(bytes32 _name, address _mappedAddress) public {
    // ✅ Declare in memory to prevent overwriting the existing storage
    NameRecord memory newRecord;

newRecord.name = _name;
    newRecord.mappedAddress = _mappedAddress;
    resolve[_name] = _mappedAddress;
    registeredNameRecord[msg.sender] = newRecord;
    require(unlocked);
}
```

## ➡️ Using `memory` instead of `storage` eliminates the risk of modifying existing state variables.

### 🔥 **Real-world example: OpenAddressLottery & CryptoRoulette**

- Some hackers created contracts that exploited uninitialized storage variables to steal ether from attackers
- `OpenAddressLottery` and `CryptoRoulette` are honeypot examples designed to trick users into falling for the attack
- These contracts intentionally inserted vulnerabilities to trick attackers into believing they could gain an advantage

---

## ⚠️ 13. **Floating Point and Precision (Floating-Point and Precision Issues)**

**🚨 Vulnerability Description:**

- Solidity does not support floating-point operations (e.g., no `float` type)
- Only integer operations are possible → Precision loss may occur during division operations
- This can lead to losses during token conversions, financial operations, etc.

---

### 📌 Vulnerable Code Example

```solidity
contract FunWithNumbers {

uint constant public tokensPerEth = 10;
    uint constant public weiPerEth = 1e18;
    mapping(address => uint) public balances;
    function buyTokens() external payable {
        uint tokens = msg.value / weiPerEth * tokensPerEth;  // ❌ Precision issue occurs
        balances[msg.sender] += tokens;

}
    function sellTokens(uint tokens) public {
        require(balances[msg.sender] >= tokens);
        uint eth = tokens / tokensPerEth;  // ❌ Rounding error may occur
        balances[msg.sender] -= tokens;
        msg.sender.transfer(eth * weiPerEth);
    }
```

### 📌 Vulnerability Description

- When the amount entered is less than 1 ETH (e.g., 0.5 ETH) in the `msg.value / weiPerEth` operation, **`0`\*\*** occurs\*\*
- When selling less than 10 tokens in `sellTokens()`, there is a possibility that 0 ETH will be returned

---

### ✅ Solution

- **Perform multiplication before division to maintain precision**

```solidity
function buyTokens() external payable {
    uint tokens = (msg.value * tokensPerEth) / weiPerEth;  // ✅ Maintain precision
    balances[msg.sender] += tokens;
}
```

## ➡️ **Change the order of calculations to prevent precision loss**

## 🔹 **Conclusion**

- **All code may contain bugs** → Thorough testing and auditing are required.
- **Use verified libraries (such as OpenZeppelin) whenever possible** and prioritize security when writing new code.
- Adhere to the principle of “if it's not safe, don't use it,” and design all smart contracts with potential attacks in mind.

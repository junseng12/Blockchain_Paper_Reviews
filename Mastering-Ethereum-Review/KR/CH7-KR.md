## 📌 **1️⃣ 스마트 컨트랙트란?**

Ethereum에서는 **두 가지 유형의 계정**이 존재합니다.

- **EOA(Externally Owned Account, 외부 소유 계정)**
  - 사용자가 직접 제어하는 계정 (개인 키 사용)
  - 트랜잭션을 통해 컨트랙트 호출 가능
  - 예: Metamask, Ledger 같은 지갑이 관리하는 계정
- **CA(Contract Account, 컨트랙트 계정)**
  - **코드가 자체적으로 동작**하는 계정 (개인 키 없음)
  - 배포 후에는 불변(immutable)
  - 트랜잭션을 통해서만 실행 가능

➡️ **즉, 스마트 컨트랙트(Smart Contract)는 코드가 실행되는 컨트랙트 계정(CA)이다.**

<details>
<summary>Solidity의 특징과 구조</summary>

Solidity는 이더리움 스마트 컨트랙트를 작성하기 위해 만들어진 **고수준 프로그래밍 언어**입니다.

- **객체 지향 프로그래밍(OOP) 기반**
- **JavaScript/C++와 유사한 문법**
- **Ethereum Virtual Machine(EVM)에서 실행되는 바이트코드로 컴파일됨**

</details>

---

## 📌 **2️⃣ 스마트 컨트랙트의 주요 속성**

| 속성                                             | 설명                                          |
| ------------------------------------------------ | --------------------------------------------- |
| **Immutable (불변성)**                           | 배포 후 코드 변경 불가                        |
| **Deterministic (결정론적 실행)**                | 같은 입력 → 같은 결과                         |
| **Decentralized (분산 실행)**                    | 모든 노드에서 동일한 코드 실행                |
| **Gas Cost (가스 비용 발생)**                    | 실행마다 가스 비용이 발생                     |
| **Trigger-based Execution (트랜잭션 기반 실행)** | 직접 실행되지 않고 트랜잭션이 발생해야 실행됨 |
| **No Private Key (개인 키 없음)**                | EOAs와 달리 컨트랙트 계정은 개인 키가 없음    |

📌 **즉, 컨트랙트는 자체적으로 실행되지 않고 EOA가 발생시킨 트랜잭션에 의해 실행됨!**

## 📌 **3️⃣ 스마트 컨트랙트의 생명 주기**

스마트 컨트랙트는 **4가지 단계**로 구성됩니다.

### 🔹 1) 작성 & 컴파일

- Solidity 코드 작성 → `solc`를 사용하여 바이트코드로 변환.
- 컴파일 시 **ABI(Application Binary Interface) 생성**.

  ```solidity
  solidity
  복사편집
  pragma solidity ^0.8.0;
  contract Faucet {
      function withdraw(uint withdraw_amount) public {
          payable(msg.sender).transfer(withdraw_amount);
      }
      receive() external payable {} // 이더 수신 가능
  }
  ```

  - `solc --bin Faucet.sol` → 바이트코드 출력
  - `solc --abi Faucet.sol` → ABI 출력

### 🔹 2) 배포 (Deployment)

- **배포 트랜잭션(Contract Creation Transaction) 생성**
- `to` 필드는 `null`
- 컨트랙트 주소는 **(배포자 주소 + nonce)** 조합으로 결정됨.

  ```solidity
  solidity
  복사편집
  const tx = {
      from: "0xYourEOAAddress",
      to: null,  // 컨트랙트 배포이므로 null 설정
      data: "0x6080604052348015600...",  // 바이트코드
      gas: 3000000,
      gasPrice: web3.utils.toWei('20', 'gwei')
  };
  web3.eth.sendTransaction(tx);
  ```

### 🔹 3) 실행 (Execution)

- 컨트랙트는 EOA가 트랜잭션을 보낼 때만 실행됨.
- 컨트랙트끼리 호출 가능 (Nested Execution)

### 🔹 4) 삭제 (Selfdestruct)

- `selfdestruct(address)` 호출 시 컨트랙트가 삭제됨.
- 이더리움에서 데이터가 사라지는 유일한 방법.

```solidity
solidity
복사편집
function destroy() public {
    require(msg.sender == owner, "Only owner can destroy");
    selfdestruct(payable(owner));
}
```

📌 **하지만 과거 트랜잭션 기록은 블록체인에 남아 있음!**

## 📌 **5️⃣ Gas와 가스 최적화**

### 💰 **Gas란?**

- **Ethereum에서 트랜잭션 실행 비용**
- **1 Gas ≠ 1 ETH**, 가스는 `gasPrice`에 의해 ETH 단위로 환산됨.

### 🔥 **가스 비용 예시**

| 연산                        | 비용       |
| --------------------------- | ---------- |
| `SSTORE` (저장소 업데이트)  | 20,000 gas |
| `CALL` (외부 컨트랙트 호출) | 700 gas    |
| `ADD` (덧셈)                | 3 gas      |
| `JUMPDEST` (점프 위치)      | 1 gas      |

📌 **복잡한 연산일수록 가스 소모량이 많음!**

### ✅ **가스 최적화 방법**

1. **Storage 대신 Memory 활용** (저장소 접근 비용 ↓)
2. **`calldata`** **활용** (`memory`보다 비용 ↓)
3. **Loops 최소화** (`for` 대신 `mapping`)
4. **상태 변수 읽기 최소화** (`uint`을 `uint8`로 줄이기)

## 📌 **6️⃣ Solidity의 보안 고려 사항**

Solidity에서 보안 취약점은 **직접적인 금전적 손실**로 이어질 수 있음.

### ⚠️ **Reentrancy Attack**

- 컨트랙트에서 이더를 보낼 때, 공격자가 재귀 호출하여 여러 번 출금하는 공격.

```solidity
solidity
복사편집
function withdraw(uint _amount) public {
    require(balances[msg.sender] >= _amount, "잔액 부족");
    payable(msg.sender).transfer(_amount);
    balances[msg.sender] -= _amount;  // 🔥 문제 발생!
}
```

✅ **해결 방법**

- `transfer()` 대신 `call.value` 사용
- 상태 변경을 먼저 수행 (`checks-effects-interactions` 패턴 적용)4
<details>
<summary>✅ **Reentrancy Attack을 이해하기 쉽게 비유로 설명하기**</summary>

**💡 비유:**

은행에서 돈을 출금한다고 가정해보자.

- 은행원: "출금 요청을 확인하고, 요청한 금액을 고객에게 전달한 후 잔액을 업데이트해야지!"
- 그런데 만약 출금 요청을 처리하는 도중에 **고객이 다시 출금 요청을 보낼 수 있다면?**
- 이때, 은행 시스템이 **잔액을 업데이트하기 전에 출금 요청을 여러 번 처리**하게 되면 어떻게 될까?
  → 고객이 **실제 잔액보다 많은 돈을 출금할 수 있음**! 💸💸💸

</details>

```solidity
solidity
복사편집
function withdraw(uint _amount) public {
    require(balances[msg.sender] >= _amount, "잔액 부족");
    balances[msg.sender] -= _amount;  // ✅ 상태 변경 먼저!
    payable(msg.sender).transfer(_amount);
}
```

### ⚠️ **Integer Overflow & Underflow**

- Solidity 0.8 이상에서는 자동 방지됨.

```solidity
solidity
복사편집
// Solidity 0.7 이하에서는 SafeMath 사용 필요!
using SafeMath for uint256;
```

## **7️⃣ 스마트 컨트랙트에서의 이벤트 활용**

이벤트(Event): **트랜잭션 로그(Log) 기록을 남기는 방법**

### ✅ **이벤트 선언 및 사용 예시**

```solidity
solidity
복사편집
contract Example {
    event Transferred(address indexed _from, address indexed _to, uint _value);

    function send(address _to, uint _value) public {
        emit Transferred(msg.sender, _to, _value);
    }
}
```

- `emit`을 사용하여 이벤트를 발생시키면 **트랜잭션 로그에 기록됨**
- Etherscan 같은 블록 탐색기에서 이벤트를 조회할 수 있음

## 📌 msg.sender VS. tx.origin

## 🎭 **비유: 회사 사장(EOA), 매니저(A), 직원(B)**

**상황**

- 어떤 회사(이더리움 네트워크)가 있다고 하자.
- 사장(EOA)이 회사 매니저(A)에게 "직원(B)에게 자료를 요청해줘"라고 지시했다.
- 매니저(A)는 직원(B)에게 가서 "사장님이 자료 요청하셨으니 줘"라고 말한다.

---

### 🔹 **Solidity 코드로 표현하면:**

```solidity
solidity
복사편집
contract A {
    function callB(address _b) public {
        B(_b).someFunction();  // A가 B를 호출
    }
}
```

1️⃣ **사장(EOA)** → 매니저(A)에게 "B에게 someFunction()을 호출하라"는 트랜잭션을 보냄

2️⃣ **매니저(A)** → 직원(B)의 `someFunction()`을 실행함

---

## 🕵️‍♂️ **이때,** **`msg.sender`\*\***와\*\* **`tx.origin`** **값**

| 변수                      | 의미                          | 값         |
| ------------------------- | ----------------------------- | ---------- |
| `tx.origin`               | 최초로 트랜잭션을 시작한 사람 | 사장 (EOA) |
| `msg.sender` (B 입장에서) | 호출한 직전 컨트랙트          | A (매니저) |

즉, 스마트 컨트랙트 `B` 입장에서 보면:

- `msg.sender` = 매니저 `A`
- `tx.origin` = 사장 `EOA`

---

## 🔥 **이해 포인트**

- **`msg.sender`\*\***는 바로 직전 호출자\*\*
  → A가 B를 호출했으므로 B 입장에서 `msg.sender`는 A
- **`tx.origin`\*\***은 맨 처음 트랜잭션을 발생시킨 EOA\*\*
  → 이 모든 호출을 처음 시작한 것은 사장(EOA)이므로 `tx.origin`은 여전히 EOA

---

## ⚠️ **보안 문제점:** **`tx.origin`** **사용하면 위험!**

어떤 악성 컨트랙트가 `tx.origin`을 검증 조건으로 사용하면, 공격자가 다른 컨트랙트를 통해 호출하는 방식으로 속일 수 있다.

```solidity
solidity
복사편집
contract Malicious {
    function attack(Victim victim) public {
        victim.withdrawAll(); // 공격자가 Victim 컨트랙트를 실행하게 함
    }
}
contract Victim {
    function withdrawAll() public {
        require(tx.origin == owner, "Not owner!"); // tx.origin을 검증하는 방식 ❌ (위험!)
        payable(msg.sender).transfer(address(this).balance);
    }
}
```

- 만약 Victim 컨트랙트가 `tx.origin == owner`를 사용하면, **공격자가 중간 컨트랙트(Malicious)를 이용해 호출하더라도** **`tx.origin`\*\***은 여전히 원래의 EOA(피해자)가 됨\*\*.
- 따라서 **msg.sender로만 검증해야 안전**하다.

### 🔥 **결론: 왜** **`tx.origin`\*\***이 위험한가?\*\*

1️⃣ `tx.origin`을 사용하면 **중간에 악성 컨트랙트가 개입해도 공격자를 검출할 수 없음.**

2️⃣ `msg.sender`를 사용했다면, 악성 컨트랙트가 출금 요청할 때 `msg.sender == 악성 컨트랙트`가 되므로 차단 가능.

3️⃣ 그래서 **항상** **`msg.sender`\*\***를 사용해야 하고,\*\* **`tx.origin`\*\***은 보안에 취약해서 사용하지 않는 것이 좋다!\*\* 🚀

# 1. 스마트 컨트랙트 보안

## 🔹 보안 Best Practice

### 1️⃣ **방어적 프로그래밍 (Defensive Programming)**

- **최소한의 코드 (Minimalism & Simplicity)**: 코드가 단순할수록 보안이 강해진다. 불필요한 기능을 줄이고 핵심 로직에 집중해야 한다.
- **코드 재사용 (Code Reuse)**: 검증된 라이브러리와 기존 컨트랙트를 활용하는 것이 보안성을 높인다.
- **코드 품질 (Code Quality)**: 스마트 컨트랙트는 웹 개발처럼 가볍게 다뤄서는 안 된다. 항공우주 엔지니어링 수준의 정밀한 개발이 요구된다.
- **가독성 및 감사 가능성 (Readability & Auditability)**: 명확하고 이해하기 쉬운 코드가 보안성 높은 코드다.
- **테스트 커버리지 (Test Coverage)**: 모든 가능한 입력을 테스트해야 한다. 예상치 못한 인풋이 컨트랙트를 손상시킬 수 있다.

## 🔹 **주요 보안 취약점 및 방지 방법**

### ⚠️ 1. **Reentrancy (재진입 공격)**

### 🛑 **취약점 설명**

- 컨트랙트가 외부 주소로 이더를 보낼 때, 해당 주소가 악성 컨트랙트일 경우 다시 호출(Fallback 함수)하여 원래 컨트랙트를 다시 실행할 수 있음.
- 유명한 **DAO 해킹**이 이 방식으로 발생하여 수억 달러의 피해가 발생.

### 📌 **취약 코드 예시**

```solidity
function withdraw(uint _amount) public {
    require(balances[msg.sender] >= _amount);
    payable(msg.sender).transfer(_amount);  // 🔥 취약점 발생!
    balances[msg.sender] -= _amount; // ❌ 상태 업데이트가 나중에 발생
}
```

- `transfer()`를 실행할 때, 공격자의 컨트랙트가 Fallback 함수를 호출하면서 `withdraw()`를 다시 실행하면 원래 컨트랙트의 상태가 업데이트되기 전에 반복적으로 출금 가능.

### 🛠 **해결 방법**

1. **Checks-Effects-Interactions 패턴**: 상태를 먼저 변경한 후 외부 호출을 수행해야 함.
2. **Reentrancy Guard 사용**: 컨트랙트가 다시 호출되지 못하도록 뮤텍스(Mutex) 변수 추가.
3. **`transfer()`** **대신** **`call()`** **사용 시, 최소한의 가스만 전달** (2300 gas limit).

✅ **보완된 코드**

```solidity
bool private locked;
function withdraw(uint _amount) public {
    require(!locked, "Reentrancy detected!");
    locked = true; // 🔒 락 설정
    require(balances[msg.sender] >= _amount);
    balances[msg.sender] -= _amount;
    payable(msg.sender).transfer(_amount);
    locked = false; // 🔓 락 해제
}
```

### ⚠️ 2. **Integer Overflow & Underflow**

### 🛑 **취약점 설명**

- 정수 값이 최대/최소 범위를 초과할 경우, 예상치 못한 결과를 초래할 수 있음.
- 예를 들어, `uint8` 타입 변수에 255를 더하면 0이 되어버리는 문제가 발생할 수 있음.

### 📌 **취약 코드 예시**

```solidity
function setBalance(uint _amount) public {
    balance[msg.sender] += _amount;  // 🔥 오버플로우 발생 가능
}
```

### 🛠 **해결 방법**

1. **SafeMath 라이브러리 사용**
2. Solidity 0.8.x 이상에서는 자동으로 오버/언더플로우 방지됨.

✅ **보완된 코드 (SafeMath 적용)**

```solidity
using SafeMath for uint256;

function setBalance(uint _amount) public {
    balance[msg.sender] = balance[msg.sender].add(_amount); // 오버플로우 방지
}
```

---

### ⚠️ 3. **tx.origin을 사용한 인증 (Phishing Attack)**

### 🛑 **취약점 설명**

- `tx.origin`을 사용해 컨트랙트 소유자를 인증하면, 피싱 공격이 가능함.
- 공격자가 사용자에게 자신의 컨트랙트를 호출하도록 유도하고, 이를 통해 피해자의 주소를 원래 컨트랙트에서 인증받아 자산을 탈취할 수 있음.

### 📌 **취약 코드 예시**

```solidity
function withdraw() public {
    require(tx.origin == owner, "Not the owner!");  // ❌ 보안 취약
    payable(msg.sender).transfer(address(this).balance);
}
```

### 🛠 **해결 방법**

1. **tx.origin 대신 msg.sender 사용**
2. 다중 서명(Multi-signature) 및 승인 시스템 활용

✅ **보완된 코드**

```solidity
function withdraw() public {
    require(msg.sender == owner, "Not the owner!");  // ✅ 안전한 방식
    payable(msg.sender).transfer(address(this).balance);
}
```

---

### ⚠️ 4. **Unchecked External Call**

### 🛑 **취약점 설명**

- `call()` 또는 `send()`를 사용하여 외부 컨트랙트를 호출할 때, 반환값을 확인하지 않으면 공격자가 의도적으로 실패하는 트랜잭션을 만들어 컨트랙트의 상태를 손상시킬 수 있음.

### 📌 **취약 코드 예시**

```solidity
function sendFunds(address payable recipient, uint amount) public {
    recipient.call{value: amount}("");  // ❌ 반환 값 체크 안 함
}
```

### 🛠 **해결 방법**

1. **반환값을 확인하고 실패 시 revert() 호출**
2. **가능하면 transfer() 사용 (2300 gas 제한)**

✅ **보완된 코드**

```solidity
function sendFunds(address payable recipient, uint amount) public {
    (bool success, ) = recipient.call{value: amount}("");
    require(success, "Transfer failed!"); // ✅ 반환 값 체크
}
```

🔍 **설명**

- `call()`의 반환값을 `bool success` 변수에 저장.
- `success`가 `false`이면, **트랜잭션을** **`revert`\*\***시켜 실행을 취소\*\*.
- 이렇게 하면, **이더가 전송되지 못했을 경우 컨트랙트 상태를 정상적으로 유지할 수 있음.**

### ✅ **왜** **`transfer()`\*\***가 더 안전한가?\*\*

```solidity
recipient.transfer(amount);
```

- `transfer()`는 내부적으로 `call()`을 사용하지만, **가스 제한(2300 gas)** 이 있어 `fallback` 함수를 실행할 때 복잡한 로직을 실행할 수 없음.
- 또한, `transfer()`는 실패할 경우 자동으로 **트랜잭션을 revert**하기 때문에, 별도의 `require(success, "Transfer failed!")` 처리를 할 필요가 없음.

📌 **즉, 가능하면** **`transfer()`\*\***를 사용하고, 반드시\*\* **`call()`\*\***을 사용할 경우 반환값을 확인해야 한다!\*\*

<summary>비유 및  구체적인 악용 예시</summary>

### 💡 **이해하기 쉬운 비유**

✅ **은행 송금 예제**

은행에서 고객에게 돈을 보내는 상황을 생각해 봅시다.

1️⃣ **취약한 방식 (Unchecked Call)**

- 은행 직원이 고객에게 100만 원을 송금하면서, "송금이 잘 되었는지 확인도 안 하고" 그냥 시스템에 입력만 하고 끝냄.
- 고객 계좌에 장애가 있어서 송금이 실패했지만, 은행 시스템은 이를 감지하지 못하고 "송금 완료"라고 표시.
- 결과적으로 고객은 돈을 받지 못했는데, 은행 시스템에서는 이미 출금된 것으로 처리됨 → **돈이 증발하는 문제 발생!** 😱

2️⃣ **안전한 방식 (Checked Call)**

- 은행 직원이 송금을 보낸 뒤, "이체 성공 여부"를 반드시 확인함.
- 송금이 실패하면 **"이체 실패" 메시지를 표시하고, 다시 시도하거나 고객에게 알림을 보냄.**
- 즉, **송금 실패 시 예외 처리를 해서 돈이 증발하는 걸 막음.** ✅

## 🧨 **공격 과정 (Exploit Flow)**

1️⃣ **공격자가** **`VictimContract`\*\***에 1 ETH 예치\*\*

- `victim.deposit{value: 1 ether}();` 실행 → `balances[msg.sender]`가 `1 ether` 증가

2️⃣ **공격자가** **`sendFunds()`\*\***를 호출하여 자신에게 1 ETH 전송 요청\*\*

- `victim.sendFunds(payable(address(this)), 1 ether);`
- VictimContract는 `call()`을 사용하여 `MaliciousContract`로 1 ETH를 전송 시도

3️⃣ **하지만 공격자의 컨트랙트는 의도적으로 트랜잭션을 실패시킴 (\*\***`fallback() { revert(); }`\***\*)**

- 즉, **이더 전송 실패!**
- 하지만 VictimContract는 `call()`의 반환값을 확인하지 않으므로, **트랜잭션이 실패해도 잔액을 차감해버림!**

4️⃣ **결과적으로 VictimContract의** **`balances[msg.sender]`** **값이 줄어들었지만, 이더는 그대로 남아 있음**

- 💰 공격자는 추가적인 출금을 통해 **잔액을 0으로 만들고도 계속해서 인출** 가능

## 🤔 **"그럼 해커는 돈을 직접 빼갈 수는 없는 거 아냐?"**

맞아, 단순히 이 방법만으로 해커가 돈을 직접 훔쳐갈 수 있는 건 아니야.

하지만 **이 기법을 활용해서 더 큰 공격을 할 수 있어!**

예를 들어:

✅ **스마트 컨트랙트가 정상적인 사용자들의 출금을 막도록 만들 수 있다.**

✅ **서비스를 마비시켜서 특정 사용자가 돈을 인출하지 못하게 방해하는 DoS(서비스 거부) 공격이 가능하다.**

✅ **이걸 이용해 "기록상 잔액이 0인 사용자는 출금을 할 수 없다" 같은 조건을 우회할 수도 있다.**

---

## 🔥 **실제 사례 (DoS 공격)**

**2016년 "GovernMental Ponzi Scheme" 스마트 컨트랙트**

이더리움 기반의 폰지 사기였는데,

컨트랙트에 **1,100 ETH가 잠겨 있었지만, 누군가가 비슷한 방법으로 출금할 수 없게 만들어버렸어.**

결국 컨트랙트는 돈이 남아 있는데도 출금이 안 되는 상태가 됐지.

이처럼, 이 공격 기법은 해커가 직접 돈을 훔쳐가는 게 아니라 **컨트랙트를 마비시키거나, 특정 사용자만 출금할 수 있게 만드는 데 활용될 수 있어.**

---

### ⚠️ 5. **블록 타임스탬프 조작**

### 🛑 **취약점 설명**

- `block.timestamp` 값을 난수(Randomness) 생성에 사용하면, 채굴자가 이를 조작하여 자신의 이익을 극대화할 수 있음.

### 📌 **취약 코드 예시**

```solidity
function lottery() public {
    if (block.timestamp % 2 == 0) {
        winner = msg.sender; // ❌ 조작 가능
    }
}
```

🔍 **이 코드가 왜 취약할까?**

✅ 블록 타임스탬프는 **채굴자가 조작할 수 있음!**

✅ 채굴자는 블록을 채굴할 때 **timestamp 값을 살짝 바꿔서** `짝수` 또는 `홀수`로 조작 가능

✅ 결국, 공격자는 **항상 자신이 승리하는 방식으로 블록을 조작할 수 있음**

### 🛠 **해결 방법**

1. **난수 생성 시 블록 해시(blockhash) 또는 외부 오라클 활용**
2. **타임스탬프 의존 로직 최소화**

✅ **보완된 코드**

```solidity
function lottery() public {
    require(block.timestamp > lastPlayed + 1 hours, "Wait for next round!");
    lastPlayed = block.timestamp;
    // 난수 생성 로직 변경
}
```

## **📝 블록 타임스탬프는 조작 가능하다!**

✅ 블록 타임스탬프를 난수 생성에 직접 사용하면 **채굴자가 결과를 조작할 수 있음!**

✅ 로또, 복권, 베팅, 게임 같은 랜덤 요소가 중요한 컨트랙트는 **반드시 오라클 또는 블록 해시를 활용해야 함!**

✅ **"블록 타임스탬프는 신뢰할 수 없다"** → 이것만 기억하면 돼! 🔥

---

### ⚠️ 6. **Unexpected Ether (예상치 못한 이더)**

### 🎭 **💡 비유: "통장 잔고 오류"**

한 은행이 있다고 가정해 보자.

은행 계좌는 **입출금 내역이 있어야만 돈이 들어오거나 나갈 수 있음**이 원칙이다.

하지만 어떤 이유로 인해 **입출금 내역 없이도 통장에 돈이 들어올 수 있다면?**

만약 공격자가 **“은행의 입출금 내역을 무시하고”** 계좌에 돈을 추가하는 방법을 찾았다면,

- 예금액과 실제 잔액이 일치하지 않는 문제가 발생할 수 있음
- **출금 로직이 예금액을 기준으로 한다면, 돈을 인출하지 못하는 버그가 생길 수도 있음**

이 개념을 스마트 컨트랙트에 적용하면, **컨트랙트에 예상하지 못한 이더가 들어올 수 있는 두 가지 방법**이 있음!

---

### 🛑 **Unexpected Ether가 발생하는 2가지 방법**

1️⃣ **selfdestruct()를 통한 강제 송금**

2️⃣ **컨트랙트 배포 전, 미리 이더를 전송 (Pre-sent Ether)**

---

### ✅ **1. Selfdestruct()를 이용한 강제 송금**

### 🛠 **취약점 개념**

Ethereum에는 **selfdestruct()** 라는 함수가 있음.

이 함수를 호출하면 해당 컨트랙트는 파괴되며, **남아있는 모든 이더를 특정 주소로 강제 전송**할 수 있음!

이때, **타겟 컨트랙트에 존재하는** **`fallback`** **함수가 실행되지 않음!**

즉, **컨트랙트의 로직을 우회해서 이더를 보낼 수 있음.**

### 📌 **예제 코드**

```solidity
contract Attacker {
    constructor() payable {} // 이더를 담아둠

    function attack(address payable target) public {
        selfdestruct(target); // target 컨트랙트로 이더 강제 송금
    }
}
```

✅ **타겟 컨트랙트가** **`payable`** **함수가 없거나, 입금을 허용하지 않아도 이더가 강제로 들어옴!**

---

### ✅ **2. 컨트랙트 배포 전, 미리 이더를 전송 (Pre-sent Ether)**

### 🛠 **취약점 개념**

Ethereum의 **컨트랙트 주소는 결정론적으로 생성**됨.

즉, 특정 주소의 컨트랙트가 배포될 것을 미리 예상할 수 있음!

➡️ **공격자가 해당 주소에 미리 이더를 전송**해 놓으면,

➡️ **컨트랙트가 배포될 때, 이미 이더가 들어있는 상태로 시작!**

### 📌 **공격 방식**

1️⃣ 공격자는 특정 컨트랙트가 배포될 주소를 미리 계산

2️⃣ 해당 주소로 이더를 먼저 전송

3️⃣ 컨트랙트 배포 후, **컨트랙트 코드에서** **`this.balance`\*\***를 사용할 경우, 잘못된 계산을 하게 만듦\*\*

---

### 🚨 **📌 실제 공격 사례: EtherGame 컨트랙트**

```solidity
contract EtherGame {
    uint public finalMileStone = 10 ether;
    uint public depositedWei;

    function play() external payable {
        require(msg.value == 0.5 ether);
        uint currentBalance = this.balance + msg.value; // ⚠️ this.balance 사용 (취약!)
        require(currentBalance <= finalMileStone);
        depositedWei += msg.value;
    }
}
```

### 🛑 **공격 시나리오**

1️⃣ 공격자가 **selfdestruct()** 또는 **Pre-sent Ether** 방식으로 **컨트랙트에 0.1 ETH를 강제 전송**

2️⃣ 이후, `play()` 함수를 호출한 사용자들은 `this.balance` 값이 엉망이 되어 정상적인 게임이 불가능

3️⃣ 공격자가 큰 금액을 강제 송금하면, **아무도 보상을 받을 수 없게 됨!**

### ✅ **해결 방법**

- **컨트랙트의 이더 잔고를 직접** **`this.balance`\*\***로 계산하지 않고, 별도의\*\* **`depositedWei`** **변수를 사용**
- `depositedWei`는 사용자가 직접 송금한 값만을 기록하므로, 외부 공격의 영향을 받지 않음

```solidity
contract SecureEtherGame {
    uint public finalMileStone = 10 ether;
    uint public depositedWei;

    function play() external payable {
        require(msg.value == 0.5 ether);
        uint currentBalance = depositedWei + msg.value; // ✅ 안전한 방식
        require(currentBalance <= finalMileStone);
        depositedWei += msg.value;
    }
}
```

---

### ⚠️ 7. **Delegatecall 취약점**

### 🎭 **💡 비유: "대리운전 사고"**

한 운전자가 있다고 가정해보자.

- 차주(스마트 컨트랙트)는 **운전(함수 실행)을 직접 하지 않고** 대리운전(Delegatecall)을 맡김
- 하지만, **대리운전 기사가 사고를 내면?**
  - 차주는 대리운전을 맡겼을 뿐인데 **책임은 차주에게 있음**
  - 대리운전 기사가 **보험을 변경하거나, 차주의 돈을 빼가는 일도 가능**

➡️ **Delegatecall()은 스마트 컨트랙트에서 비슷한 문제를 일으킬 수 있음!**

---

### ⚠️ **Delegatecall()의 문제점**

- `delegatecall()`은 **외부 컨트랙트의 코드를 실행하면서도, 호출하는 컨트랙트의** **`storage`\*\***를 그대로 사용\*\*함
- 만약 공격자가 **라이브러리 주소를 변경**할 수 있다면?
  - **악성 컨트랙트를 라이브러리로 설정**하고, `delegatecall()`을 실행하여 데이터를 변조할 수 있음!

---

### 🚨 **📌 실제 공격 사례: Parity Multisig Wallet 해킹**

### **1차 해킹 (소유권 변경)**

Parity의 Multisig Wallet 라이브러리는 `initWallet()` 함수를 통해 지갑을 초기화함.

하지만 `initWallet()` 함수가 **public으로 설정**되어 있어, 누구나 호출 가능!

```solidity
function initWallet(address[] _owners, uint _required) public {
    m_numOwners = _owners.length;
    m_owners = _owners;
    m_required = _required;
}
```

🔹 공격자는 `initWallet()` 함수를 호출하여 **소유자를 본인으로 변경**

🔹 이후, 지갑의 모든 이더를 탈취!

### **2차 해킹 (selfdestruct로 영구 잠금)**

- 공격자는 라이브러리 컨트랙트 자체를 소유한 후, `kill()` 함수를 호출하여 **라이브러리를 selfdestruct**
- 이로 인해, **모든 Multisig Wallet이 작동 불능 상태가 됨**
- 수백만 달러 상당의 ETH가 **영구적으로 잠김!**

---

### ✅ **Delegatecall() 보안 대책**

1️⃣ **라이브러리는** **`library`** **키워드를 사용하여 상태 변수를 가지지 않도록 설정**

2️⃣ **라이브러리 함수는** **`external`\*\***이 아닌\*\* **`internal`\*\***로만 호출 가능하게 설정\*\*

3️⃣ **delegatecall() 사용 시, 신뢰할 수 있는 라이브러리 주소를 하드코딩**

---

## ⚠️ 8. Default Visibilities (기본 가시성 설정)

**🚨 취약점 설명:**

- Solidity에서 **가시성(visibility) 지정자를 명시하지 않으면 기본값은** **`public`**
- 즉, 함수를 외부에서 누구나 호출 가능 → 원치 않는 상태 변경 가능

**📌 취약 코드 예시:**

```solidity
contract HashForEther {
    function withdrawWinnings() {
        require(uint32(msg.sender) == 0);  // 특정 주소만 가능
        _sendWinnings();
    }

    function _sendWinnings() {
        msg.sender.transfer(address(this).balance);
    }
}
```

✅ `_sendWinnings` 함수는 내부적으로만 호출되어야 하지만, **기본값** **`public`\*\***이므로 누구나 호출 가능!\*\*

➡️ 공격자는 `_sendWinnings`를 직접 호출하여 모든 자금을 탈취 가능

**✅ 해결 방법: 함수 가시성을 반드시 명시적으로 지정 (\*\***`private`\***\*,** **`internal`\*\***,\*\* **`external`\*\***,\*\* **`public`\*\***)\*\*

---

## ⚠️ 9. External Contract Referencing (외부 컨트랙트 참조 취약점)

**🚨 취약점 설명:**

- Solidity에서는 **외부 컨트랙트의 주소를 직접 설정하여 호출 가능**
- 하지만, 공격자가 이를 조작하여 **악성 컨트랙트를 연결하면 보안 문제가 발생**

**📌 취약 코드 예시:**

```solidity
contract EncryptionContract {
    Rot13Encryption encryptionLibrary;

    constructor(Rot13Encryption _encryptionLibrary) {
        encryptionLibrary = _encryptionLibrary;
    }

    function encryptData(string memory data) public {
        encryptionLibrary.rot13Encrypt(data);  // ❌ 외부 컨트랙트가 악성 코드일 가능성 있음
    }
}
```

➡️ 만약 공격자가 `encryptionLibrary`를 악성 컨트랙트로 변경하면, 예상치 못한 코드 실행 가능

**✅ 해결 방법:**

- **라이브러리 컨트랙트 주소를** **`immutable`\*\***로 설정하여 변경 불가능하게 만들기\*\*
- **배포 시 직접 컨트랙트를 생성 (\*\***`new`\*\* **키워드 사용)**

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

➡️ **외부 입력값을 통한 변경을 방지하여 보안성 강화!**

---

## ⚠️ 10. Short Address Attack (짧은 주소 공격)

**🚨 취약점 설명:**

- Solidity의 함수는 **고정된 크기의 데이터(32바이트)를 읽음**
- 하지만, **잘못된 인코딩(예: 주소가 20바이트가 아닌 19바이트)**을 사용하면 **EVM이 자동으로 0을 추가 (패딩)**
- **이로 인해 공격자가 추가적인 자금을 전송하거나, 원래의 의도와 다른 행동을 수행할 수 있음**

**📌 취약 코드 예시 (ERC20 토큰 전송):**

```solidity
function transfer(address to, uint256 value) public returns (bool) {
    to.call{value: value}("");  // ❌ 짧은 주소 공격 가능
    return true;
}
```

- 공격자가 **1바이트 적은 주소를 보내면, EVM이 자동으로 0을 추가하여 잘못된 주소로 자금이 전송됨**

**✅ 해결 방법:**

- **ABI 인코딩을 직접 확인 (\*\***`msg.data.length`\*\* **체크)**
- **타사 애플리케이션에서 주소 유효성 검사 적용**
- **ERC-20 표준 구현 시** **`safeTransfer`** **사용 (\*\***`OpenZeppelin`\*\* **라이브러리 활용)**

```solidity
import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";

contract SecureERC20 {
    using SafeERC20 for IERC20;

    function secureTransfer(IERC20 token, address to, uint256 amount) public {
        token.safeTransfer(to, amount);
    }
}
```

➡️ **`SafeERC20`** **라이브러리를 사용하면 자동으로 유효성을 검사하여 공격을 방지 가능!**

---

## ⚠️ 11. **Constructors with Care (생성자 취약점)**

**🚨 취약점 설명:**

- **Solidity v0.4.22 이전에는 생성자가 계약과 동일한 이름을 가져야 했음**
- **이름이 다르면 일반 함수처럼 동작** → 누구나 호출 가능
- 이는 계약이 배포된 후 소유권이 공격자에게 넘어가는 치명적인 취약점 발생

---

### 📌 취약 코드 예시

```solidity
contract OwnerWallet {
    address public owner;

    // ❌ 생성자이지만, 계약 이름과 다름 → 일반 함수처럼 동작
    function ownerWallet(address _owner) public {
        owner = _owner;
    }

    // 이더를 보관할 수 있는 폴백 함수
    function () external payable {}

    function withdraw() public {
        require(msg.sender == owner);
        msg.sender.transfer(address(this).balance);
    }
}
```

### 📌 취약점 설명

- `ownerWallet` 함수는 개발자가 원래 생성자로 만들려 했지만, **계약 이름** **`OwnerWallet`\*\***과 다름\*\*
- 따라서 **일반 함수로 취급**되며, 배포 후 누구나 `ownerWallet()`을 호출해 **소유권을 변경 가능**
- 공격자가 이 함수를 호출하여 `owner = 공격자 주소`로 변경 후 `withdraw()`를 호출하면 **모든 이더 탈취 가능**

---

### ✅ 해결 방법

- **Solidity 0.4.22 이상에서는 생성자에** **`constructor`** **키워드 사용**
- **오타 없이 생성자 설정을 명확하게 할 것**

```solidity
contract SecureWallet {
    address public owner;

    // ✅ constructor 키워드 사용
    constructor(address _owner) public {
        owner = _owner;
    }

    function withdraw() public {
        require(msg.sender == owner);
        msg.sender.transfer(address(this).balance);
    }
}
```

➡️ `constructor`를 사용하면 **함수가 계약 이름과 무관하게 생성자로 인식**되므로, 누구도 호출할 수 없음

---

## ⚠️ 12. **Uninitialized Storage Pointers (초기화되지 않은 스토리지 포인터)**

**🚨 취약점 설명:**

- Solidity에서는 **초기화되지 않은** **`storage`** **변수가 기존 저장소 슬롯을 가리킬 수 있음**
- **예상치 못한 상태 변경 발생 가능**
- 이를 악용하면 공격자가 컨트랙트의 중요한 변수(예: `owner`)를 변경할 수도 있음

---

### 📌 취약 코드 예시

```solidity
// A locked name registrar
contract NameRegistrar {
    bool public unlocked = false;  // 기본적으로 잠겨 있음

    struct NameRecord {
        bytes32 name;
        address mappedAddress;
    }

    mapping(address => NameRecord) public registeredNameRecord;
    mapping(bytes32 => address) public resolve;

    function register(bytes32 _name, address _mappedAddress) public {
        // ❌ 초기화되지 않은 storage 변수 → 기존 저장소 슬롯을 덮어씀
        NameRecord newRecord;
        newRecord.name = _name;
        newRecord.mappedAddress = _mappedAddress;

        resolve[_name] = _mappedAddress;
        registeredNameRecord[msg.sender] = newRecord;

        require(unlocked);  // ✅ 잠금 상태 확인
    }
}
```

### 📌 취약점 설명

- **`newRecord`\*\***는 초기화되지 않은 상태에서 사용됨\*\*
- Solidity에서는 기본적으로 **구조체를** **`storage`\*\***로 설정**하므로, `newRecord`는 **기존 저장소 슬롯을 덮어씀\*\*
- **공격자가** **`unlocked`** **상태를 변경할 수 있는 특정 값을** **`_name`\*\***에 넣으면, 레지스트리를 강제 해제 가능!\*\*

<summary>구체적인 설명</summary>

### ⚠️ **취약점 발생 이유**

1️⃣ `newRecord`가 `storage` 타입으로 인식됨

- Solidity에서 구조체(`struct`)는 기본적으로 `storage`에 저장됨
- 즉, `newRecord`는 초기화되지 않은 상태에서 **컨트랙트의 기존 저장소 슬롯을 덮어씀**

2️⃣ `newRecord`가 저장소 슬롯을 덮어쓰기 때문에 `unlocked` 상태도 변경될 수 있음

- Solidity는 **컨트랙트 변수(상태 변수)를 저장소 슬롯(Slot)에 순차적으로 저장**
- `NameRecord` 구조체의 첫 번째 멤버(`name`)가 `unlocked`이 저장된 슬롯을 덮어쓸 가능성이 있음
- 공격자가 `_name` 값을 **특정 값**으로 조작하면 `unlocked`를 강제적으로 `true`로 변경 가능

3️⃣ `require(unlocked);` 조건이 의미가 없어짐

- **unlocked가 조작되어 true로 변경되면, 원래는 허용되지 않던 등록도 가능**
- 결국 공격자는 원래는 등록할 수 없는 상태에서도 새로운 이름과 주소를 등록할 수 있음

---

### ✅ 해결 방법

- **구조체를 메모리에 명시적으로 저장 (\*\***`memory`\*\* **지정자 사용)**

```solidity
function register(bytes32 _name, address _mappedAddress) public {
    // ✅ 메모리에 선언하여 기존 저장소 덮어쓰기 방지
    NameRecord memory newRecord;
    newRecord.name = _name;
    newRecord.mappedAddress = _mappedAddress;

    resolve[_name] = _mappedAddress;
    registeredNameRecord[msg.sender] = newRecord;

    require(unlocked);
}
```

➡️ `storage` 대신 `memory`를 사용하면, **기존 상태 변수를 변경할 위험이 사라짐**

---

### 🔥 **실제 사례: OpenAddressLottery & CryptoRoulette**

- 일부 해커들은 **초기화되지 않은 스토리지 변수를 악용하는 컨트랙트**를 만들어 공격자들에게 에테르를 빼앗음
- `OpenAddressLottery`와 `CryptoRoulette`은 사용자가 쉽게 속아 넘어가도록 유도한 허니팟(Honeypot) 사례
- 이러한 컨트랙트들은 의도적으로 취약점을 삽입하여, 공격자가 이득을 볼 수 있다고 착각하게 만듦

---

## ⚠️ 13. **Floating Point and Precision (부동소수점 및 정밀도 문제)**

**🚨 취약점 설명:**

- Solidity는 **부동소수점 연산을 지원하지 않음** (예: `float` 없음)
- **정수 연산만 가능** → 나눗셈 연산에서 정밀도 손실 발생 가능
- 이로 인해 **토큰 변환, 금융 연산 등에서 손실 발생 가능**

---

### 📌 취약 코드 예시

```solidity
contract FunWithNumbers {
    uint constant public tokensPerEth = 10;
    uint constant public weiPerEth = 1e18;
    mapping(address => uint) public balances;

    function buyTokens() external payable {
        uint tokens = msg.value / weiPerEth * tokensPerEth;  // ❌ 정밀도 문제 발생
        balances[msg.sender] += tokens;
    }

    function sellTokens(uint tokens) public {
        require(balances[msg.sender] >= tokens);
        uint eth = tokens / tokensPerEth;  // ❌ 반올림 오류 발생 가능
        balances[msg.sender] -= tokens;
        msg.sender.transfer(eth * weiPerEth);
    }
```

### 📌 취약점 설명

- `msg.value / weiPerEth` 연산에서 **1ETH보다 작은 금액(예: 0.5ETH) 입력 시** **`0`\*\***이 됨\*\*
- `sellTokens()`에서 **10개 미만의 토큰 판매 시, 0 ETH가 반환될 가능성**

---

### ✅ 해결 방법

- **나눗셈 연산 전에 곱셈을 수행하여 정밀도를 유지**

```solidity
function buyTokens() external payable {
    uint tokens = (msg.value * tokensPerEth) / weiPerEth;  // ✅ 정밀도 유지
    balances[msg.sender] += tokens;
}
```

➡️ **계산 순서를 바꿔서 정밀도 손실을 방지**

---

## 🔹 **결론**

- **모든 코드에는 버그가 있을 가능성이 있음** → 철저한 테스트 및 감사를 거쳐야 함.
- **최대한 검증된 라이브러리(OpenZeppelin 등)를 활용**하고, 새로운 코드 작성 시 보안성을 최우선으로 고려해야 함.
- \*"안전하지 않으면 사용하지 마라"**는 원칙을 지키고, 모든 스마트 컨트랙트는 **잠재적 공격을 고려하여 설계\*\*해야 함.

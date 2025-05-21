## 📌 **1. Ethereum Virtual Machine(EVM) 개념**

### 🔹 **EVM이란?**

- **EVM**(Ethereum Virtual Machine)은 **이더리움의 핵심 구성 요소**로, 스마트 컨트랙트를 실행하고, 블록체인 상태(state)를 변경하는 **가상 컴퓨터 환경**입니다.
- EVM은 **스마트 컨트랙트의 실행과 배포**를 담당하며, 모든 이더리움 노드는 동일한 EVM을 사용하여 같은 스마트 컨트랙트를 실행하고 같은 결과를 얻습니다.

### 📌 **비유:**

- **이더리움**은 거대한 **공유 컴퓨터**이고, EVM은 이 컴퓨터에서 돌아가는 **운영체제(OS)**와 같습니다.
- 스마트 컨트랙트는 OS에서 실행되는 **프로그램**이며, EVM은 이 프로그램을 실행할 때 필요한 **자원 관리와 보안 기능**을 담당합니다.

---

## 📌 **1️⃣ EVM의 주요 특징**

### **🔹 준 튜링 완전(Quasi–Turing Completeness)**

- EVM은 **튜링 완전한 가상 머신**처럼 거의 모든 프로그램을 실행할 수 있습니다. 단, 가스(gas)를 통해 **실행 시간을 제한**하여, 무한 반복 등으로 인한 네트워크 정지를 방지합니다.
- 즉, 무한 반복 프로그램이 실행될 가능성이 없도록 설계된 **안전한 컴퓨터**입니다.

### 📌 비유:

- EVM은 **"코인 노래방"**과 같습니다.
- 코인을 넣은 만큼만 노래(코드)를 부를 수 있습니다. 무한 반복으로 노래를 할 수 없고, **정해진 금액(가스)** 안에서만 노래(코드)가 실행됩니다. 시간이 끝나면 무조건 종료됩니다.

---

## 📌 **2️⃣ EVM의 구조 및 동작 원리**

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c2ba559c-cb6d-4c61-bec3-1760fafc9a92/39173aa4-ca64-41a5-832f-e4da8553dfad/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664TC25ANY%2F20250521%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250521T213318Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEA4aCXVzLXdlc3QtMiJIMEYCIQDd%2BPNyPLP2TnQO2%2BZ%2BO5UmScLpMQ51irnu3UHoRhBaiAIhAIO%2F53fnDK8dG68lkgCKT8ivo%2F%2FfMF9ChoWX77%2FekBWJKogECMb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igzk4lA6lKeJ8puB8roq3AMXuBboC27cIJDZsnZJEpyRSCuh1th2NK%2ByGVSom1tpZu2CHGOhBisYSQyZg5%2FQYXxM5OgB7y3ahPL1y5%2F10dOG%2FZjZpJFfikDEJHO5lkBVOGZUWJHVjGlReN7Ig4%2BD3iVUDwvBm4uS%2BgKGKO130r%2FDHu8D4YSi%2B1atNIgnOKNgNTVLbV%2BaSjH7%2FUbKE8lRvh%2BcA2xS8u6mqLZp%2Fau2fNIrGLGr%2Fjo56NpWNXcY7cbXd6e%2FBcbexyg9YRONS3BhlGkVmuPjTJEQgPOBi6x08JDIA3qbC7lZKNqvVqKh%2BbODZy8IZkSSv106wLxPF%2FHf0V6OOGcon9g1%2FNmCUe6d3prFCH86ba1mj%2BqNpji3vlx2Icdm8hsY42SfpN52UoneExSMyp1clD6KbzQLMYzRjBlZw6VVbgCAVQZ7x%2BPjL735UCvgFI32xG7Y7PE%2F4u7e25Xxmf9Ko12aDG8UYPNE8WY93JKnT8VYtkVxRusHCQQ96srxfD60TuDVh2JmkZypuFKo%2Bn7kM1EUQB0kQ2UOC2L9F1sYG3qPhluoQoM5nI8%2F2IqSfyjQ8uZA1N1fEk5HMd4n%2F9tcC3%2BBAtNWZitbee2iCcTOTKGLiNMDknIK5DAiPCviMzPHn6feTBY6kDDAhrnBBjqkAYlWJMYYdLZkTLlF4DMa2v9kNZTi703nDr0CCDz1EHj%2Bg2LFVQCT6UoYtw0t4LqNP69ei2xJT4EBhLLhBcqgPNJpgDQUHQP9gjfr5KtAJRewgO5e9wVxr1PKWdrTdSWmsLYGibuPBn%2B0yVtlL2p2nPeWCQsgmkTLRpesODld%2BR25%2FU15sPkOIHu6vbF2Jg6mFAe3ljVmaRscWEoRXFjkJ2QDKsE9&X-Amz-Signature=8c4fac1aae31a31de15aeb5058738b25a72cde4d566e5081f0ad5bf110225908&X-Amz-SignedHeaders=host&x-id=GetObject)

## 📌 **EVM Execution Model 내 주요 개념 정리**

    ## **1️⃣ EVM State의 Storage에 저장하는 정보는?**


    📌 **Storage는 스마트 컨트랙트의 "영구 저장소"**로, 한 번 저장된 값은 **트랜잭션이 종료된 후에도 유지**된다.


    💡 **저장하는 정보**

    - 스마트 컨트랙트의 **상태 변수(State Variables)**
    - 특정 컨트랙트의 **사용자 데이터** (예: 잔액, 토큰 소유 정보)
    - `mapping` 또는 `struct`을 통해 저장된 데이터

    📌 **비유**

    > Storage는 은행의 금고 같은 개념이야.

>     금고에 돈(데이터)을 보관하면, 나중에 다시 꺼낼 수 있어.
>
>
>     하지만 이 금고를 여는 데는 수수료(가스)가 비싸서, 자주 여닫지는 않는 게 좋아.

    ✅ **특징**


    ✔️ 블록체인에 **영구 저장됨** → 한 번 저장하면 가스비를 내고 변경해야 함


    ✔️ **모든 노드가 저장** → 이더리움 네트워크 전체에서 유지됨


    ✔️ 트랜잭션이 끝난 후에도 **데이터가 유지됨**


    ---


    ## **2️⃣ EVM World State에서 가져오는 정보는?**


    📌 **World State는 현재 이더리움 블록체인의 "전체 상태"를 나타냄.**


    각 계정(Account)의 상태와 관련 정보를 유지하고 있음.


    💡 **가져오는 정보**

    - **각 계정(Account State)의 상태**
        - **Externally Owned Account (EOA)**
            - 주소(Address)
            - 잔액(Balance)
            - 논스(Nonce, 해당 계정이 실행한 트랜잭션 수)
        - **Smart Contract Account**
            - 코드 해시(CodeHash, 해당 스마트 컨트랙트의 코드)
            - 저장소(Storage Root Hash, 스마트 컨트랙트의 저장소 상태)
    - **현재 실행 중인 블록(Block Header) 정보**
        - 블록 번호(Block Number)
        - 가스 리밋(Gas Limit)
        - 난이도(Difficulty)

    📌 **비유**

    > World State는 **"은행 전체의 데이터베이스"**라고 보면 돼.

>     각각의 계좌(Account)가 얼마나 있는지, 잔액이 얼마인지, 최근 거래가 무엇인지 등을 기록하는 **거대한 원장**이야.

    ✅ **특징**


    ✔️ 모든 계정의 **현재 상태**를 유지


    ✔️ 특정 계정의 저장소(Storage)를 불러올 때 사용


    ✔️ **스마트 컨트랙트 실행 전 상태를 로드**하고, 실행 후 상태를 갱신


    ---


    ## **3️⃣ EVM Global Namespace of Variables and Units에서 저장하는 정보는?**


    📌 **EVM Global Namespace는 특정 트랜잭션 실행 중에만 유지되는 변수**들을 저장.


    이 정보들은 **트랜잭션 실행이 끝나면 사라진다.**


    💡 **저장하는 정보**

    - **트랜잭션 전역 변수**
        - `MSG.SENDER` → 트랜잭션을 보낸 사람의 주소
        - `MSG.VALUE` → 트랜잭션과 함께 보낸 ETH(wei)
        - `MSG.DATA` → 트랜잭션의 입력 데이터 (함수 호출 정보 등)

    📌 **비유**

    > **전역 변수는 "택배 배송 정보"**라고 보면 돼.

>     택배(트랜잭션)가 도착하면,
>
>
>     누가 보냈는지(MSG.SENDER),
>
>
>     얼마를 보냈는지(MSG.VALUE),
>
>
>     무엇을 요청했는지(MSG.DATA)를 확인하는 것과 같아.

    ✅ **특징**


    ✔️ 특정 트랜잭션이 실행되는 동안만 유지


    ✔️ 트랜잭션이 끝나면 **사라짐**


    ✔️ 실행 중인 스마트 컨트랙트가 필요로 하는 정보를 제공


    ---


    ## **4️⃣ State Machine Cycle에서 Remaining OPCODES가 NO면 왜 Revert하는가?**


    📌 **OPCODE가 없으면 Revert하는 이유**


    EVM은 "명령어를 순차적으로 실행하는 기계"야.


    그런데 실행해야 할 명령어(OPCODE)가 **남아 있지 않다면**, 실행할 코드가 없다는 뜻이야.


    ✅ **가능한 상황 2가지**

    1. **정상적인 종료:**
        - `STOP`, `RETURN` 등 종료 명령어가 실행되면 문제없이 종료됨.
    2. **비정상적인 종료 (Revert 발생):**
        - 실행해야 할 OPCODE가 남아 있어야 하는데, 존재하지 않으면 오류 발생 → **Revert!**

    📌 **비유**

    > OPCODE는 "레시피(요리법)"와 같아.

>     요리를 하려면 레시피에 있는 순서대로 진행해야 하는데,
>
>
>     중간에 레시피가 사라지면 **"어떻게 요리를 끝내야 할지 몰라서 실패(Revert)"** 하는 거야.

    ✅ **정리하면...**


    ✔️ OPCODE가 남아 있지 않다는 건, 실행할 코드가 없다는 것


    ✔️ 정상적으로 `STOP`이나 `RETURN`으로 종료되지 않았다면 **Revert 발생**


    ✔️ 스마트 컨트랙트는 실행 도중 **정상적으로 종료되지 않으면 모든 상태 변경을 롤백**


    ---

## **📌 최종 정리**

| **저장소**              | **역할**                           | **저장하는 정보**                     |
| ----------------------- | ---------------------------------- | ------------------------------------- |
| **Storage (EVM State)** | 스마트 컨트랙트의 영구 저장소      | 상태 변수, 사용자 데이터              |
| **World State**         | 이더리움 블록체인의 현재 상태      | 각 계정(Account)의 정보 및 블록 정보  |
| **Global Namespace**    | 트랜잭션 실행 중에만 유지되는 변수 | `MSG.SENDER`, `MSG.VALUE`, `MSG.DATA` |
| **OPCODE 실행 사이클**  | 스마트 컨트랙트 실행 흐름 관리     | 남은 OPCODE가 없으면 Revert           |

<details>
<summary>**ARGS 저장내용**</summary>

## **스마트 컨트랙트 호출 과정에서 ARGS 역할**

📌 **스마트 컨트랙트의 특정 함수가 실행될 때, ARGS에는 그 함수의 실행에 필요한 데이터가 저장됨.**

**📌 실행 과정 (함수 호출 예제)**

1. 사용자가 **트랜잭션을 전송** → 스마트 컨트랙트의 특정 함수 실행 요청
2. EVM World State에서 **스마트 컨트랙트의 주소와 Storage 데이터 로드**
3. **ARGS(TX Data)에 트랜잭션 관련 데이터 저장**
4. **ARGS를 분석하여, 어떤 함수가 실행될지 결정**
5. **필요한 입력값(파라미터)을 스마트 컨트랙트 내부 변수에 전달**
6. **실제 연산 실행 후, 결과 반환 (혹은 상태 변경)**

✅ **📌 예제 코드**

```solidity
solidity
복사편집
contract MyContract {
    uint256 public myValue;

    function setValue(uint256 _value) public {
        myValue = _value;
    }
}
```

**📌 실행 흐름**

- 사용자가 `setValue(100)`을 호출하면, **트랜잭션 데이터 (msg.data)**가 다음과 같이 저장됨.
- **ARGS는 이 데이터를 분석하여 실행할 함수를 찾고, 파라미터를 가져옴.**

💡 **ARGS 내부 저장 데이터**

| 바이트 오프셋 | 데이터                                                             | 설명                            |
| ------------- | ------------------------------------------------------------------ | ------------------------------- |
| `0x00 - 0x03` | `0x60fe47b1`                                                       | 함수 식별자 (Function Selector) |
| `0x04 - 0x23` | `0000000000000000000000000000000000000000000000000000000000000064` | 함수 파라미터 값 `_value = 100` |

📌 **비유:**

> ARGS는 "스마트 컨트랙트에 전달된 편지(트랜잭션 데이터)"
>
> 편지에는 **"어떤 함수(setValue)를 실행해라!"** 와 **"입력값(100)"** 이 적혀 있음.
>
> 스마트 컨트랙트는 이 편지를 보고 "어떤 함수 실행?"과 "입력값이 뭐야?"를 결정함.

</details>

### **🔹 EVM의 데이터 저장 방식**

EVM은 크게 세 가지 저장공간을 가집니다:

| 저장 공간   | 설명                                           |
| ----------- | ---------------------------------------------- |
| **Stack**   | 데이터를 임시로 저장하는 LIFO 방식의 저장 공간 |
| **Memory**  | 휘발성 임시 저장소, 트랜잭션이 끝나면 초기화   |
| **Storage** | 영구적으로 블록체인 상태(state)에 저장됨       |

### 📌 비유:

- \*스택(Stack)\*\*은 계산기에서 임시로 숫자를 저장하는 메모리 버튼과 같음.
- **메모리**는 프로그램이 실행되는 동안만 필요한 임시 메모장.
- **스토리지**는 하드디스크처럼, 데이터를 영구적으로 보관.

### **🔹 EVM 실행 환경**

스마트 컨트랙트를 실행할 때, EVM 환경에는 다음과 같은 정보가 포함됩니다.

- **Contract bytecode** (스마트 컨트랙트 코드)
- **Storage** (영구 저장)
- **Memory** (임시 저장)
- **Stack** (연산 임시 공간)
- **가스(gas)** : 실행에 사용할 수 있는 계산 자원
- **환경 변수**: 호출자 주소, 블록 정보 등

---

## 📌 **3️⃣ EVM의 가스(Gas)**

### 🔹 **가스(Gas) 개념**

- EVM에서 연산, 저장, 전송 등의 모든 연산은 **가스**를 소비합니다.
- 가스는 **이더리움 네트워크의 연료**로, 연산량이 많을수록 소모하는 가스도 증가합니다.
- 가스가 부족하면 **Out-of-Gas(OOG)** 오류로 실행이 중단되고, 모든 작업이 취소됩니다.

### 📌 비유:

- EVM에서 가스는 자동차의 **연료(휘발유)** 와 같습니다.
- 스마트 컨트랙트(자동차)가 멀리 가거나 무거운 짐을 실으면 연료를 더 많이 소비합니다.
- 연료(가스)가 떨어지면 자동차가 멈추듯, EVM의 실행도 즉시 중단됩니다.

### 🔹 **가스 비용과 가스 가격**

- **Gas Cost**: 특정 연산에 드는 가스량. (예: 덧셈(ADD)은 3 가스, 곱셈(MUL)은 5 가스)
- **Gas Price(가스 가격)**: 사용자가 가스 1 단위당 지불하는 이더(ETH)의 양. 높은 가스 가격은 빠른 거래 처리를 보장.

| 개념                 | 정의                            |
| -------------------- | ------------------------------- |
| 가스 비용(Gas cost)  | 연산이 소비하는 가스의 양       |
| 가스 가격(Gas Price) | 가스 1단위당 지불할 이더량(ETH) |
| 거래 수수료          | Gas 비용 × Gas Price            |

---

## 📌 **4️⃣ 상태 변경 실패: Out of Gas(OOG)와 Revert**

이전에도 가스가 부족하면 트랜잭션이 실패한다고 배웠지만, **OOG(Out of Gas)와 Revert의 차이**를 명확히 알아야 해.

| **실패 유형**        | **설명**                           | **결과**                |
| -------------------- | ---------------------------------- | ----------------------- |
| **Out of Gas (OOG)** | 트랜잭션 실행 중 가스가 부족함     | 모든 변경 사항이 롤백됨 |
| **Revert**           | `require()` 또는 `revert()` 실행됨 | 상태 변경 없이 롤백됨   |
| **Assert 실패**      | `assert()` 문이 실패함             | 가스 전부 소모 & 롤백   |

- **Require()문에 의해 Revert 발생**: 이전 연산에 사용된 가스만 소모되고, 상태 변화 없이 남은 가스는 반환됨.
- **Out of Gas (OOG)**: 가스를 모두 소진했지만 연산이 남아 있어 실행이 롤백되며, 이미 사용된 가스는 반환되지 않음.
- **Assert 실패**: 가스를 덜 사용했더라도 `assert()` 실행 시 **남은 가스를 모두 소진한 후 롤백됨**.

📌 **비유**

> OOG는 "자동차 기름이 없어서 멈춘 경우"Revert는 "안전벨트를 안 매서 출발하지 못하는 경우"Assert 실패는 "엔진이 폭발해서 차가 박살나는 경우"

---

## 📌 **5️⃣ 스마트 컨트랙트 배포(Deployment)와 실행(Runtime)**

스마트 컨트랙트는 두 가지 형태의 코드가 존재:

| 형태                    | 설명                                                              |
| ----------------------- | ----------------------------------------------------------------- |
| **Deployment Bytecode** | 컨트랙트를 배포할 때만 사용되는 코드 (생성자 등 초기화 코드 포함) |
| **Runtime Bytecode**    | 배포 후 실제 사용자가 호출할 때 실행되는 코드                     |

- 배포 과정에서는 **초기 설정(상태 초기화 등)**을 수행한 후, 실행에 필요한 **Runtime Bytecode**만 블록체인에 저장됩니다.

## 🚩 **1단계: 배포 과정 (Deployment)**

    ### 🔹 **무엇을 하나?**

    - 스마트 컨트랙트를 **블록체인 위에 최초로 설치하는 단계**.
    - 배포 단계에서는 스마트 컨트랙트의 **초기 설정(상태 변수 초기화, 변수 설정)** 이 이루어짐.
    - 주로 **생성자(Constructor)** 라는 특별한 함수를 사용해 초기 설정 작업을 수행함.

    ### 🔹 **Deployment Bytecode란?**

    - 스마트 컨트랙트를 최초로 블록체인에 설치할 때만 사용되는 특별한 형태의 코드.
    - *생성자 코드 + 컨트랙트의 실제 실행 코드(Runtime Bytecode)**를 포함한 형태로 배포됨.
    - 이 코드는 **단 한 번만 실행되고 나면, 블록체인에는 Runtime Bytecode만 저장되고 Deployment Bytecode는 사라짐**.

    ### 📌 **구체적인 과정 예시 (상세 단계)**


    | **순서** | **과정 설명**                                                    |
    | ------ | ------------------------------------------------------------ |
    | ①      | 사용자가 스마트 컨트랙트를 블록체인에 배포하기 위한 **트랜잭션 전송**                     |
    | ②      | 트랜잭션의 **to** 주소는 특별한 주소(**0x0**). 즉, 블록체인 상에서 새로운 컨트랙트 생성 요청 |
    | ③      | 트랜잭션 내 **data** 필드에 배포용 코드(**Deployment Bytecode**)가 들어있음    |
    | ④      | **EVM**이 이 코드를 로드해서 최초로 한 번 실행하면서 **초기화 작업(상태 변수 설정 등)**을 수행 |
    | ⑤      | 초기화가 완료되면, 최종적으로 **Runtime Bytecode만** 블록체인에 저장됨             |


    ### 📌 **비유**

    - 스마트 컨트랙트를 배포하는 것은 **새 컴퓨터에 소프트웨어를 설치하는 과정**과 같음.
        - 설치 과정에서 다양한 **초기 설정(라이선스 인증, 사용자 설정)**을 하고,
        - 설치 프로그램은 그 역할이 끝나면 삭제되고, 실제 실행할 프로그램만 남음.

---

## 🚩 **2단계: 실행 과정 (Runtime)**

    ### 🔹 **무엇을 하나?**

    - 사용자가 실제로 스마트 컨트랙트를 호출해 **상호작용(함수 호출 등)** 하는 단계.
    - 블록체인에 저장된 Runtime Bytecode만 사용됨.
    - 사용자가 스마트 컨트랙트의 함수를 호출할 때마다 Runtime Bytecode가 EVM 위에서 실행됨.

    ### 🔹 **Runtime Bytecode란?**

    - 블록체인에 저장되어 지속적으로 사용되는 코드.
    - 사용자가 스마트 컨트랙트와 상호작용할 때마다 반복적으로 실행되는 코드.
    - Deployment Bytecode에서 생성자 등 초기화 코드를 제외한, 순수하게 **실행될 함수와 로직만 포함**.

    ### 📌 **구체적인 과정 예시 (상세 단계)**


    | **순서** | **과정 설명**                                                               |
    | ------ | ----------------------------------------------------------------------- |
    | ①      | 사용자가 스마트 컨트랙트 내 특정 함수를 호출하는 트랜잭션을 전송                                    |
    | ②      | EVM이 이 트랜잭션에서 호출한 **함수의 식별자**(Function Identifier)를 읽음                  |
    | ③      | Runtime Bytecode 내 **Dispatcher(분배자)** 가 호출된 함수 식별자를 읽고, 해당하는 함수 코드로 이동 |
    | ④      | 호출된 함수의 코드가 실행되고, 이로 인해 **블록체인 상태(state)가 변경**되거나, **응답 데이터를 반환**       |


    ### 📌 **비유**

    - Runtime 단계는 소프트웨어를 이미 설치한 후 **사용자가 소프트웨어를 직접 실행하는 것**과 같음.
        - 예: 설치된 게임을 클릭해서 실행 → 사용자가 게임 플레이

---

### 📌 **배포(Deployment)와 실행(Runtime)의 전체 흐름 예시**

    - Solidity로 작성된 스마트 컨트랙트가 있다고 가정:

    ```solidity
    solidity
    복사편집
    contract Example {
      uint public count;

      constructor(uint _initial) {
          count = _initial; // 생성자에서 초기화
      }

      function increment() public {
          count = count + 1;
      }
    }
    ```


    ### **🔸 배포 과정 (Deployment)**


    | 단계 | 작업                                                       |
    | -- | -------------------------------------------------------- |
    | ①  | `Example` 스마트 컨트랙트의 배포 트랜잭션을 생성하여 전송                     |
    | ②  | 트랜잭션은 0x0 주소로 보내지고, Deployment Bytecode가 담겨있음            |
    | ③  | EVM이 Deployment Bytecode를 실행하면서 생성자 실행(`count` 초기화)      |
    | ④  | 실행이 완료되면, **`count`** **값과 Runtime Bytecode만 블록체인에 저장**됨 |


    ### **🔸 실행 과정 (Runtime)**


    | 단계 | 작업                                                                                |
    | -- | --------------------------------------------------------------------------------- |
    | ①  | 사용자가 스마트 컨트랙트의 `increment()` 함수 호출 트랜잭션을 전송                                       |
    | ②  | EVM은 트랜잭션의 데이터에서 함수 식별자(Function Identifier)를 읽어 Runtime Bytecode의 Dispatcher로 보냄 |
    | ③  | Dispatcher는 식별자를 통해 `increment()` 함수 위치를 찾아 실행                                    |
    | ④  | `increment()`가 실행되며 블록체인의 상태(state)가 변경됨 (`count` 값 증가)                           |


    ---


    ## 🎯 **정리**


    | 구분                      | 역할                 | 특징                  |
    | ----------------------- | ------------------ | ------------------- |
    | **Deployment Bytecode** | 최초 배포 단계에서만 사용됨    | 생성자 포함, 1회 실행 후 삭제됨 |
    | **Runtime Bytecode**    | 실제 컨트랙트 호출 시 반복 사용 | 사용자 함수 포함, 영구적 저장   |

    - Deployment 단계에서 **초기 설정** → 이후에는 Runtime 단계의 **실행 코드**만 사용.

    이러한 두 단계의 구분을 통해 스마트 컨트랙트가 블록체인에 안전하고 효율적으로 설치되고 운영될 수 있도록 설계된 거야!

---

## 📌 6️⃣ **EVM Opcode와 실행 흐름**

- **Opcode**는 EVM에서 실행되는 **저수준(Low-level) 명령어**입니다.
- 스마트 컨트랙트 언어(Solidity)는 컴파일 후 Opcode로 변환되어 EVM에서 실행됩니다.

### 📌 비유:

- **Solidity 코드**가 사람이 읽는 **고급언어(영어)**라면, EVM이 이해하는 Opcode는 컴퓨터가 바로 이해할 수 있는 **기계어**와 같습니다.
- Solidity → EVM Opcode → 기계적 실행 → 상태(State) 변경

---

## 📌 7️⃣ **EVM의 Opcode 유형**

| 카테고리               | 주요 Opcode 예시                         |
| ---------------------- | ---------------------------------------- |
| **산술 연산**          | ADD, SUB, MUL, DIV, MOD                  |
| **메모리 및 저장공간** | MSTORE, MLOAD, SSTORE, SLOAD             |
| **흐름 제어**          | JUMP, JUMPI, STOP, RETURN                |
| **논리 연산**          | AND, OR, NOT, XOR, LT, GT, EQ            |
| **환경 정보 접근**     | CALLER, CALLVALUE, TIMESTAMP, BLOCKHASH  |
| **시스템 연산**        | CREATE, CALL, DELEGATECALL, SELFDESTRUCT |

---

## 📌 **8️⃣ Proxy Contract 패턴(참고)**

- 스마트 컨트랙트는 기본적으로 **배포 후 변경 불가**하나, **Proxy Contract Pattern**을 사용하면 업그레이드 가능.
- 실제 로직이 포함된 컨트랙트를 별도로 배포하고, 프록시 컨트랙트는 로직 컨트랙트를 가리키도록 설계하여, 필요 시 로직 컨트랙트만 교체 가능.

## ✅ 정확한 Proxy 패턴 구조

실제 Proxy 패턴 구조는 보통 두 개의 컨트랙트로 구성되며, 다음과 같아.

| 컨트랙트 타입                           | 역할                                      | 설명                                                          |
| --------------------------------------- | ----------------------------------------- | ------------------------------------------------------------- |
| ✅ **Proxy Contract (프록시 컨트랙트)** | 상태 변수 관리, 로직 컨트랙트 호출을 위임 | 사용자의 모든 요청을 받으며, **데이터(상태)**를 저장하고 있음 |
| ✅ **Logic Contract (로직 컨트랙트)**   | 실제 비즈니스 로직 구현 (연산 및 처리)    | **상태 데이터는 보관하지 않고**, 로직 처리만 수행             |

---

## 🎯 Proxy Contract 패턴 Architecture (2개 컨트랙트 구조) :

```plain text
사용자 → Proxy Contract (상태변수 + 주소 저장)
                   ↓ 위임(delegate)
           Logic Contract (로직 처리만 수행)
```

- **Proxy Contract**는 상태변수(데이터)를 보관하면서도 실제 로직은 가지고 있지 않으며, 호출이 오면 **Logic Contract로 처리를 위임(delegate)**하는 형태야.
- **Logic Contract**는 연산만 수행하고 데이터를 저장하지 않으며, 항상 Proxy Contract의 데이터를 사용.

---

## 🔄 업그레이드 과정 (구체적으로):

- 최초 배포 후 Logic Contract(C)를 사용 중 문제가 발생했다고 치자.
- 이때, 수정된 새 Logic Contract(D)를 새롭게 배포해.
- Proxy Contract 내부에 있는 **Logic Contract의 주소**를 Logic Contract (C)에서 Logic Contract (D)로 변경함.
- 이후부터는 Proxy Contract가 Logic Contract (D)를 호출하게 되며, 즉시 로직이 업그레이드돼.

## ✅ Proxy Contract 패턴 활용 과정

| 단계               | 설명                                      | 호텔 비유                             |
| ------------------ | ----------------------------------------- | ------------------------------------- |
| 1️⃣ 초기 배포       | Proxy와 Logic v1 배포 및 연결             | 리셉션에서 1층 객실 안내              |
| 2️⃣ 문제 발생       | 기존 Logic 컨트랙트에서 문제 발견         | 1층 객실이 불편함                     |
| 3️⃣ 업그레이드 준비 | 새 Logic 컨트랙트 배포                    | 2층에 새로운 객실 준비                |
| 4️⃣ 업그레이드 실행 | Proxy가 새 Logic 컨트랙트 가리키도록 변경 | 리셉션에서 2층 객실로 안내 변경       |
| 5️⃣ 완료            | Proxy는 그대로이며 로직만 업그레이드 완료 | 손님들은 업그레이드된 2층 객실을 사용 |

### 📌 Proxy Contract Pattern의 **문제점**

    Proxy Contract는 실제 로직 처리를 **다른 컨트랙트에게 위임**하는 방식이기 때문에, Proxy 내부에는 반드시 다음과 같은 구조가 필요해:


    ```solidity
    solidity
    복사편집
    address public logicContract; // 로직 컨트랙트 주소 저장
    ```

    - 이 변수(`logicContract`)를 변경할 수 있는 권한을 가진 사용자가 악의적이면,
    악성 Logic Contract를 가리키도록 Proxy를 변경할 수 있어.
    - 그 결과, Proxy를 통해 호출되는 모든 사용자의 요청을 조작하거나 자산을 탈취하는 등의 피해가 발생 가능.

    📌 **비유:**

    > 마치 은행 창구 직원(Proxy)이 고객을 특정 서비스팀(Logic Contract)으로 안내하는데,

>     창구 직원이 사기꾼과 결탁해 가짜 서비스팀으로 안내하면, 고객은 손쉽게 피해를 입을 수 있어.

    ---


    ## 📌 **해결책 및 보안 방법**


    이런 공격을 방지하기 위한 다양한 방법이 존재해:


    ### ✅ 1) 접근 제어(Access Control) 강화

    - Proxy Contract의 주소 변경 권한을 매우 제한적으로 설정함.
    - 일반적으로 **다중 서명(multisig)** 이나 **거버넌스(DAO 투표)** 를 통해서만 변경할 수 있게 함.

    ### ✅ 2) Timelock 및 투명한 업그레이드 과정 도입

    - 로직 변경 전에 **일정한 지연시간**(Timelock)을 설정하여, 모든 사용자에게 투명하게 공지함.
    - 변경이 감지되면 악성 코드 여부를 충분히 점검할 시간이 확보됨.

    ### ✅ 3) Immutable (불변성) & Limited Upgradability

    - 아예 Proxy Contract 주소를 **한 번만 변경 가능하게** 설계하거나,**특정 영역만 업그레이드 가능하게 설계**하여 공격 가능성을 최소화함.

    ### ✅ 4) Transparent Proxy 패턴

    - Transparent Proxy 방식은 업그레이드를 처리하는 함수와 실제 사용자가 호출하는 함수 간의 **명확한 구분**을 둠.
    - 이로 인해 관리자가 잘못된 함수를 호출하거나 사용자가 의도치 않게 접근하는 상황 방지.

    ### ✅ 5) EIP-1967 등 표준화된 Proxy 구현체 사용

    - OpenZeppelin 등에서 제공하는 **안전성이 검증된 표준 Proxy Contract 구현체**를 사용함으로써, 보안 취약점을 줄임.

    ---


    ## 🎯 **요약 정리**


    네가 정확하게 짚은 것처럼 Proxy Contract 패턴에서 Logic Contract 주소 관리는 가장 중요한 보안 이슈야. 이를 악용하면 큰 피해가 발생할 수 있으므로,

    - **접근 권한 관리**
    - **투명한 업그레이드 프로세스**
    - **검증된 표준 구현체 활용**

    이 세 가지 요소를 잘 관리하면 보안성을 극대화할 수 있어.

---

## 📌 **정리 및 결론**

- **EVM**은 이더리움 스마트 컨트랙트가 실행되는 핵심적인 환경.
- **가스 시스템**을 통해 악의적인 무한 반복 프로그램을 방지.
- **프록시 패턴**을 활용하면 스마트 컨트랙트 업그레이드 가능성을 제공.
- 스마트 컨트랙트의 안정성을 위해 **EVM 내부 동작 원리와 Opcode 이해**가 필수적입니다.

- 이더리움 디지털 서명&타원곡선함수 - [https://borntodevelop.tistory.com/entry/이더리움의-디지털-서명과-타원곡선-함수](https://borntodevelop.tistory.com/entry/%EC%9D%B4%EB%8D%94%EB%A6%AC%EC%9B%80%EC%9D%98-%EB%94%94%EC%A7%80%ED%84%B8-%EC%84%9C%EB%AA%85%EA%B3%BC-%ED%83%80%EC%9B%90%EA%B3%A1%EC%84%A0-%ED%95%A8%EC%88%98)

# **📌 CH04: 이더리움의 암호학 (Ethereum Cryptography)**

이더리움은 **보안성과 무결성**을 보장하기 위해 다양한 암호학적 기술을 사용한다.

이 기술들은 계정 주소 생성, 트랜잭션 서명, 블록 생성, 스마트 컨트랙트 무결성 등 핵심 요소에 적용된다.

---

## **📌 1️⃣ 공개키 암호화(Public-Key Cryptography)**

### **🔹 EOA와 Contract 계정 주소**

- **EOA(Externally Owned Account)**: 개인 키로 제어되는 계정
- **Contract Account**: 스마트 컨트랙트 코드가 배포된 주소 (외부에서 호출되어야 작동)

### **🔹 공개키 암호화(PKC)의 기본 원리**

- 개인 키(Private Key) → 공개 키(Public Key) → 주소(Address)로 이어지는 흐름
- 개인 키로 **메시지를 서명(Signing)**하고, 공개 키로 **검증(Verification)**

📌 **비유:**

> 개인 키는 "비밀번호", 공개 키는 "메일 주소"
>
> 메일을 보내는 사람만이 서명(전송) 가능, 누구나 확인(검증)은 가능

---

## **📌 2️⃣ 타원곡선 암호학(Elliptic Curve Cryptography)**

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c2ba559c-cb6d-4c61-bec3-1760fafc9a92/384d15af-3818-491a-affc-5c69e35e6a82/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662MUASCH7%2F20250522%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250522T034056Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEBMaCXVzLXdlc3QtMiJHMEUCIQCrB7XBtf5pRZP8S%2F728%2BFp67xMdIb3AboWFIzWIz5x%2FAIgGFIS9BWAZARz0LqyJ7CHNwJmMnQMXlEGKZVl8js1KSgqiAQIy%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDAuRaoKd0Id7kdg8NircA6hTsDc%2FeTdi4z9hASPkSDxPgjQ8BjnyjK5PAEaM7oUvc7GveNUobXg%2BN1QhviVH96BwCRPPQogFqS2HGoa8WyTt43QP74TtZshF3HTbqNsncxRY%2F3Cr7QfwxxH4P0F1WzQzCczFNS1jpaJSejYL1bMvhSGAmyCXYBm8tChpFC9%2FqRLbz66VMEXU7zZ6n5rUbbXQqZfC8ELFQemybCKas%2F%2FRmAAuJqmGPO5kZaCWM%2FI2m3P48ztvM1TxYQj1bwl%2B4bblg8IWGCAO3CZMzNYUHPXLTbTjCesvIjt07X%2FEEhz2xBQlxV2ovI%2FtO0YoP%2B9cSg4cbvl0PVMrrPMrFBpkvptwV6tJuJWThrXP2brEsv5N6SAtRYDeAmY6ExjMeHklzWWDYI3kpS8uM%2B7Kv1XvLUt5DACLneSW1z3dSqnTS9zovgekuivMQSb%2FZl4xTRmihuGo6pyaJSJMuObGsPy%2B%2Fxma5yasNxQEd2hLWUaXVDk6Gab50jDTcmx%2FDOY5TyBOObOoqybZfXCwI0NxD0fArfncd2iwxrt0him1vkTjW%2FzEX4tgpecJ%2Fu7ZaP9amwPCw17Tcbb3nEdff4KfUc44GYE3Vnq%2Bik1jyzR1Z5t5%2F2pLtpQ%2F6TM9MCka%2BFUNMM2TusEGOqUBBQwujXQGBN%2B0N42674D559Qv8Q9UOpGZNbjiZ3I5rbXY4TwIL7Nt0oPChONHTNUZbDLSrubFnumm9z5sT%2FgrcAmxjyryGBwQimgD7hx%2FpnisRG1UB7TJH7jSlGXgYEwzn7GaCD%2Bn17NLUE5r%2BZW2cZWncgIDA4DelqmCNoEAWks5u2FkJeGkeXG6NOK5gH1HspveE6x5nSXBYjjSGLNO6bGZNfnI&X-Amz-Signature=a6d2696e6606cc32839e917f6061fcdb481e31de20e8884160b7f51d92b0d91f&X-Amz-SignedHeaders=host&x-id=GetObject)

### **🔹 ECC 개념**

- 타원곡선 위의 점을 이용하여 키를 생성
- 이산대수 문제의 어려움을 이용한 보안성 확보
  > 이더리움에서는 secp256k1 곡선을 사용

### **🔹 ECC 흐름**

1. **개인 키 (256비트 랜덤 숫자) 생성**
2. **공개 키 = 개인 키 × 곡선 상의 생성점(G)**
3. **공개 키 → Keccak-256 해시 → 마지막 20바이트 → 주소**

📌 **비유:**

> ECC는 **"길 찾기 문제"**와 비슷
>
> 목적지(공개 키)는 쉽게 알 수 있지만, 출발점(개인 키)은 유추하기 어려움

---

## **📌 3️⃣ 디지털 서명과 검증 (ECDSA)**

### **🔹 ECDSA 원리**

- ECDSA(Elliptic Curve Digital Signature Algorithm)는 ECC 기반 서명 알고리즘
- 트랜잭션을 서명하면 네트워크 참여자는 **서명자가 누구인지 검증 가능**

### **🔹 서명 흐름**

1. 트랜잭션 해시 생성 (Keccak-256)
2. 개인 키로 해시를 서명
3. 네트워크는 공개 키를 통해 서명 검증

📌 **비유:**

> 서명은 "지문과 도장"
>
> 누구나 진위 여부를 확인할 수 있지만, 위조는 거의 불가능

---

## **📌 4️⃣ 해시 함수와 Keccak-256**

### **🔹 해시 함수의 특성**

| 특성        | 설명                                             |
| ----------- | ------------------------------------------------ |
| 결정론적    | 입력이 같으면 항상 동일한 출력                   |
| 비가역성    | 해시값으로 원본 데이터를 추정 불가               |
| 충돌 회피   | 서로 다른 입력이 같은 출력이 될 확률이 매우 낮음 |
| 빠른 계산   | 입력에 대해 빠르게 출력 생성                     |
| 난수 유사성 | 출력값이 예측 불가능하고 무작위적임              |

### **🔹 Keccak-256**

- SHA-3 기반 함수
- 이더리움에서 트랜잭션 해싱, 주소 생성, 상태 해시 등에 사용됨

📌 **사용 영역**

- 트랜잭션 무결성 검증
- 주소 계산
- 블록 해시
- 영지식증명, 메시지 핑거프린트 등

---

## **📌 5️⃣ 이더리움 주소 생성 과정**

### **🔹 주소 생성 흐름**

1. 개인 키 생성 (랜덤한 256비트 정수)
2. 공개 키 계산 (secp256k1 곡선)
3. Keccak-256로 공개 키 해싱
4. 해시의 마지막 20바이트를 이더리움 주소로 사용

📌 **비유:**

> 주소 생성은 "자물쇠(공개키)와 열쇠(개인키)로 우체통(주소)을 만드는 과정"

---

## **📌 6️⃣ Inter-Exchange Client Address Protocol (ICAP)**

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c2ba559c-cb6d-4c61-bec3-1760fafc9a92/a6ca2421-e237-4d90-9d7d-a7efc3380ac8/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662MUASCH7%2F20250522%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250522T034057Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEBMaCXVzLXdlc3QtMiJHMEUCIQCrB7XBtf5pRZP8S%2F728%2BFp67xMdIb3AboWFIzWIz5x%2FAIgGFIS9BWAZARz0LqyJ7CHNwJmMnQMXlEGKZVl8js1KSgqiAQIy%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDAuRaoKd0Id7kdg8NircA6hTsDc%2FeTdi4z9hASPkSDxPgjQ8BjnyjK5PAEaM7oUvc7GveNUobXg%2BN1QhviVH96BwCRPPQogFqS2HGoa8WyTt43QP74TtZshF3HTbqNsncxRY%2F3Cr7QfwxxH4P0F1WzQzCczFNS1jpaJSejYL1bMvhSGAmyCXYBm8tChpFC9%2FqRLbz66VMEXU7zZ6n5rUbbXQqZfC8ELFQemybCKas%2F%2FRmAAuJqmGPO5kZaCWM%2FI2m3P48ztvM1TxYQj1bwl%2B4bblg8IWGCAO3CZMzNYUHPXLTbTjCesvIjt07X%2FEEhz2xBQlxV2ovI%2FtO0YoP%2B9cSg4cbvl0PVMrrPMrFBpkvptwV6tJuJWThrXP2brEsv5N6SAtRYDeAmY6ExjMeHklzWWDYI3kpS8uM%2B7Kv1XvLUt5DACLneSW1z3dSqnTS9zovgekuivMQSb%2FZl4xTRmihuGo6pyaJSJMuObGsPy%2B%2Fxma5yasNxQEd2hLWUaXVDk6Gab50jDTcmx%2FDOY5TyBOObOoqybZfXCwI0NxD0fArfncd2iwxrt0him1vkTjW%2FzEX4tgpecJ%2Fu7ZaP9amwPCw17Tcbb3nEdff4KfUc44GYE3Vnq%2Bik1jyzR1Z5t5%2F2pLtpQ%2F6TM9MCka%2BFUNMM2TusEGOqUBBQwujXQGBN%2B0N42674D559Qv8Q9UOpGZNbjiZ3I5rbXY4TwIL7Nt0oPChONHTNUZbDLSrubFnumm9z5sT%2FgrcAmxjyryGBwQimgD7hx%2FpnisRG1UB7TJH7jSlGXgYEwzn7GaCD%2Bn17NLUE5r%2BZW2cZWncgIDA4DelqmCNoEAWks5u2FkJeGkeXG6NOK5gH1HspveE6x5nSXBYjjSGLNO6bGZNfnI&X-Amz-Signature=e9a1f5de370c5222dcadd4087cd8fe3c813390589e292c505320c8ca232796d8&X-Amz-SignedHeaders=host&x-id=GetObject)

- **이더리움 주소 인코딩 프로토콜**
  - 이더리움 주소를 **국제 금융 시스템과 호환 가능하게 인코딩**하기 위한 포맷
  - 이더리움 주소를 Encode 할 수 있고, 이더리움 이름 레지스트리에 등록된 공통 이름도 Encode 가능함
- 주소를 **IBAN 형식**으로 표현해 사용자 식별을 용이하게 함
- ENS(Ethereum Name Service)와도 연결 가능

📌 **비유:**

> ICAP은 이더리움 주소를 "국제 계좌번호(IBAN)" 형식으로 바꾸는 포장지

---

## **📌 7️⃣ 결론: 이더리움 암호학의 의의**

- 이더리움의 모든 신뢰는 **암호학에 기반**
- 공개키 기반 구조는 **검증 가능성과 보안성**을 동시에 제공
- ECC + 해시 + 디지털 서명 조합으로 **신뢰할 수 있는 탈중앙 시스템** 구현

📌 **마무리:**

이더리움의 보안은 단지 코드에 의존하지 않고,

**암호학적 기반 위에 설계된 구조적 안전성**을 통해 유지된다.

이는 사용자 프라이버시, 무결성, 그리고 전체 생태계의 신뢰를 보장하는 핵심 축이다. 🔐

---

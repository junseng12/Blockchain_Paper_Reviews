# 🧬 Platypus_Structure.md

## 📌 시스템 아키텍처 요약

**Platypus**는 전통적 e-Cash 모델과 account-based 시스템을 융합한 **프라이버시 중심 CBDC 구조**이다.

### 🔐 주요 참여자

- **User**: Account-based 계좌와 ZKP를 생성하며 거래 주체로 참여
- **Regulator**: 인증서 발급 및 규제 정보 검증
- **Central Bank**: 거래 무결성 및 상태 커밋 서명

### 🏛️ Trust 모델

- 중앙은행은 **프라이버시에 대해 신뢰할 수 없음**
- 거래의 무결성만 보장하는 역할 수행
- 사용자는 거래 및 커밋 과정에서 익명성 유지

---

## ⚙️ Platypus 거래 흐름 구조 (TX 처리 흐름)

```
[Alice] --- blindTx, vTx --> [Bob] --- zkpi+1, zkpj+1, stateA+1, stateB+1 --> [Central Bank]
                                             ↓                               ↑
                                ↳ TX 커밋 commTx                ↳ ZKP 확인 및 로그 저장
```

### 🔄 TX 처리 단계 요약

1. **Alice (Sender)**

   - 계정 상태 커밋 `stateᵢ` 생성
   - blind factor와 송금액으로 `commTx` 생성
   - `serialᵢ`, `commTx`, `stateᵢ₊₁`, `zkpᵢ₊₁` 생성 후 Bob에게 전달

2. **Bob (Receiver)**

   - commTx로 수신 계정 상태 `stateⱼ₊₁` 생성
   - `zkpⱼ₊₁` 생성
   - 모든 정보 묶어 Central Bank 제출

3. **Central Bank**
   - 두 ZKP와 계정 커밋을 확인하고 서명 (`σA`, `σB`) 반환
   - 공개 로그에 거래 기록

---

## 🧱 핵심 기술 구성 요소

### 🧾 Account State Commitments

- 구성 요소: `(serial, balance, blind)`
- 커밋 방식: `comm = Commit(serial, balance, blind)` (MiMC 해시 기반)
- 공개적으로는 커밋값만 노출되며 내용은 ZKP로만 검증 가능

### 🧠 Zero-Knowledge Proofs (Groth16)

- 각 TX의 ZKP는 **commTx, serial, state transition**의 정당성 증명
- 규제 조건이 있는 경우, 추가 증명 포함
  - `RegInfo`, `updateAux`, `checkOther` 함수 호출 포함

### 🔐 Regulation 관련 요소

- **soft limit**: 신원 및 잔액을 암호화하여 regulator에게 전달
- **hard limit**: 위반 시 증명 자체 생성 불가
- `auxᵢ`, `auxpub` 등을 통해 규제 상태 추적

### 🧩 Aborting Transactions

- 수신자 미응답 시 송신자는 **빈 계정 업데이트 TX** 수행
- 기존 상태를 무효화하며, 잔액 변동 없이 serial 값만 갱신

---

## 🚀 시스템 성능 및 최적화

### ✅ 병렬 ZKP 처리

- blindTx와 vTx 공유 후, 송-수신자 각각 ZKP 병렬 생성 가능
- TX 생성 시간 대폭 단축

### 🔗 샤딩 구조

- serial number의 상위 비트를 기준으로 DB 샤드 분할
- 각 TX는 송/수신자 serial을 기준으로 **최대 2개의 샤드에 접근**
- ZKP 검증과 serial number DB 체크 분리 처리

### 🧠 계정 복구

- 사용자는 memo 필드에 balance, serial, blind, 규제 정보를 암호화 저장
- 복구 시 memo + long-term key 조합으로 상태 복원

---

## 🧠 핵심 설계 철학

- **계정 기반 디자인(account model)**과 **ZKP 기반 개인정보 보호** 결합
- 중앙화된 구조를 기반으로 하면서도 **사용자 프라이버시**와 **규제 가능성**을 양립
- 기존 ZeroCash, UTXO, PRCash와의 차별점:
  - 더 간결한 거래 구조
  - 계정 기반 확장성 확보
  - 실제 정책 구현에 필요한 규제 인터페이스 내장

---

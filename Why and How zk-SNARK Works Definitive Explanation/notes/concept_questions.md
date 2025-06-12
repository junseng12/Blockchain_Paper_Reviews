# 💡 Concept Questions & 개념 구조 정리: SoK - Communication Across Distributed Ledgers

이 문서는 논문 리뷰 과정에서 제기된 질문, 구조 분석, 개념 정의를 중심으로 구성되었습니다.  
각 질문은 실제 읽기 중 궁금했던 내용을 기반으로 하며, 핵심 설계 패턴과 구조를 정리합니다.

---

## 📌 Cross-Chain Communication (CCC)이란?

- 이기종 블록체인 간 자산/데이터의 안전한 전송을 의미
- 기존의 원자적 커밋 모델을 블록체인 간에 확장할 때 생기는 한계 극복 필요

---

## 🔧 CCC 3단계 설계 구조: Commit → Verify → Abort

### 1️⃣ Commit Phase

- 자산을 잠그거나 조건부로 제출하는 단계
- 설계 모델: External Custodian, Escrow, Watchtower 등

### 2️⃣ Verification Phase

- 상대 블록체인의 커밋이 올바른지 검증
- 방법: SPV, Chain Relay, Direct Observation, ZKP

### 3️⃣ Abort Phase (Optional)

- 실패하거나 상대가 응답하지 않는 경우 자산을 회수하기 위한 구조
- 방법: Timelock, Watchtower, Coordinator

---

## 🔁 Symmetric Atomic Swaps란?

- `A → hash(s)` 조건으로 X체인에 자산 잠금
- `B → hash(s)` 동일 조건으로 Y체인에 자산 잠금
- A가 s를 제출해 B의 자산을 수령하면 → B는 공개된 s를 이용해 A의 자산 수령
- 해시락 기반 대칭 구조로 atomicity 보장

---

## 🔒 Escrow와 Watchtower의 차이?

| 구조       | 설명                                                  |
| ---------- | ----------------------------------------------------- |
| Escrow     | 조건부 자산 보관자. 자산을 잠가두고 조건 만족 시 풀림 |
| Watchtower | 자산을 보관하지 않지만 timeout 또는 부정 조건 시 개입 |

---

## 🧠 Synchrony Model의 한계

- 대부분 CCC는 **Crash Fault**나 네트워크 지연에 매우 민감
- 동기화 실패 시 자산이 영구히 잠길 수 있음 → Timelock or Watchtower 필요

---

## 🛡 ZKP + CCC 구조?

- CCC의 검증(Verification) 단계에서 ZKP 사용 시,
- 전체 블록체인 상태를 내려받지 않고도 커밋의 유효성 검증 가능
- 특히 Chain Relay 구조에서 ZKP로 SPV 한계를 극복 가능

---

## 🔄 Exchange vs Migration Protocols

| 항목     | Exchange             | Migration                |
| -------- | -------------------- | ------------------------ |
| 목적     | 자산 교환            | 자산 이동                |
| 구조     | 양방향 / 원자성 강조 | 단방향, 자산 wrapping    |
| TTP 사용 | 최소화 경향          | 일반적으로 존재          |
| 실사례   | HTLC, Arwen, A2L     | tBTC, XCLAIM, Sidechains |

---

## 🔚 결론적 통찰

- CCC 설계는 “신뢰 가정”과 “자동화 구조” 간의 절충
- 구조를 아는 것이 곧 **보안성과 응용성의 핵심**
- 향후 ZKP, Collateral 설계와 연계한 실무형 CCC 모델 연구가 가능

---

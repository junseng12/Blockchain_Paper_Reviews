# 🧩 Section-by-Section Analysis: SoK - Communication Across Distributed Ledgers

논문 전체를 직접 읽고, 구조 및 흐름을 이해하기 위한 섹션별 분석입니다.  
각 섹션에서 제시된 개념, 문제 정의, 해법 프레임워크, 논리적 전개를 중심으로 정리했습니다.

---

## **Section 1. Introduction**

- CCC 문제는 이기종 블록체인 간 통신 및 자산 교환의 신뢰성·확장성·보안성을 다룸
- 기존 Atomic Commit의 한계: 동기화 실패, Crash Fault, 블록체인 네이티브 제약
- 이 논문은 CCC 문제를 일반화된 프레임워크로 공식화하고 이를 기반으로 다양한 구조를 평가 및 분류

---

## **Section 2. CCC Problem Definition**

- CCC는 상태 변경이 여러 체인에 걸쳐 동기적으로 이루어져야 하는 문제
- 공식화:
  - CCC 프로토콜은 Commit → Verify → (Optional Abort) 구조
  - Cross-chain transaction tx가 at least one ledger에서 실행되어야 유효성 만족 (Effectiveness)
- CCC의 핵심 속성: Effectiveness, Atomicity, Fairness

---

## **Section 3. CCC Security Properties**

- **Effectiveness**: 최소한 하나의 체인에서 트랜잭션이 실행돼야 함
- **Atomicity**: 모든 체인에서 commit 또는 abort 되어야 함
- **Fairness**: 어느 한 쪽이 더 많은 정보를 얻거나 자산을 취득하면 안 됨

---

## **Section 4. CCC Design Framework**

### 4.1 Commit Phase

- **모델1**: Trusted Third Party (Custodian, Escrow)
- **모델2**: Synchrony 기반 (Hash Lock, Timelock)
- **모델3**: Hybrid 구조 (Watchtower → timeout 시 개입)

### 4.2 Verification Phase

- **모델1**: External Validator (Notary 기반)
- **모델2**: Synchrony Assumption (직접 관찰, Chain Relay)
- **모델3**: Hybrid: Watchtower + Verifiable Game + Fraud Proofs
- **ZKP 적용 가능성**: succinct proof로 X chain 전체 검증을 Y에 전달

### 4.3 Abort Phase

- Optional 단계로 Exchange 프로토콜에 중요
- Timelock 또는 TTP를 통한 자산 복구 구조
- Absolute vs Relative Timelock 차이점 존재

---

## **Section 5. Classification of Existing CCC Protocols**

- 모든 프로토콜을 Commit/Verify/Abort 기준으로 구조 분해
- 두 가지 프로토콜 유형으로 분류:
  1. **Exchange Protocols**: 양방향 교환 (HTLC, A2L, SPV, Arwen 등)
  2. **Migration Protocols**: 자산 이동 (XCLAIM, tBTC, Sidechains, Sharding)
- 분류표(Table 1)를 통해 신뢰 모델, TTP 유무, 콜래터럴 사용 여부 등을 비교

---

## **Section 6. Challenges and Outlook**

- CCC의 주요 과제: 성능, ZKP 비용, 싱크로니 문제, 보안-편의성 트레이드오프
- 실용적 CCC 설계를 위해선:
  - ZKP, Watchtower, Collateral 등의 하이브리드 설계가 필요
  - 구조적 이해 기반 설계 접근법이 앞으로의 표준이 될 수 있음

---

## ✅ 결론 요약

- CCC는 단순 기술 문제를 넘어 ‘신뢰 모델’과 ‘자동화 구조 설계’의 교차점
- 본 논문은 CCC를 **정의하고 설계하고 평가하는 프레임워크**를 제공
- 연구적 기여 + 실무 적용 가능성이 높은 구조를 제안

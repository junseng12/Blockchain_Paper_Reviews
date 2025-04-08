# 💡 Concept Questions: SoK - Communication Across Distributed Ledgers

이 문서는 논문을 읽으며 떠올랐던 개념 중심 질문들을 바탕으로 개념 정리와 응용 이해를 위한 관찰을 구조화한 것입니다.

---

## 🧭 Cross-Chain Communication (CCC)이란?
- CCC는 이기종 블록체인 간 자산/데이터의 **안전하고 동기화된 이동**을 의미
- 기존 "Atomic Commit" 문제에서 파생됨: 실패 시 전체 롤백 보장 → 블록체인 간에는 적용 어려움

---

## 🔁 CCC의 단계별 구성: Commit / Verify / Abort
- 각 단계마다 TTP / Synchrony / Hybrid 모델 선택 가능
- Watchtower나 Timelock은 **Crash Fault 대응**을 위해 등장
- Verifier는 Chain Relay(SPV) 또는 Consensus Committee 등으로 다양함

---

## 🔒 Atomic Swap (Symmetric Locks) 핵심
- 해시락 기반 거래 → A가 `hash(s)`로 자산 잠금 → B도 같은 조건 잠금
- A가 s 공개하면 B는 동일한 hash 조건으로 자산을 수령
- ‘단방향 해시성’ + 타임락을 활용해 **중간자나 위조 없이** 자산 교환 보장

---

## 🔎 Chain Relay Smart Contract의 한계
- Merkle Proof나 SPV는 **Tx 포함 여부는 검증**하지만,
  → **그 Tx가 유효한지는 블록체인 전체 상태를 알아야 판단** 가능
- ZKP(succinct proof)를 활용하면 **전체 상태 검증 없이도 Tx 유효성 확인 가능**

---

## 🛡️ Watchtower의 역할과 구조
- 기본 CCC는 참여자 간 동기화에 의존함 → Crash나 Delay 발생 시 중단 위험
- Watchtower는 패시브하게 모니터링하다가 **Timeout 시 개입**
  → 사전 설정된 로직을 강제 실행하거나 자산을 보호

---

## 🔄 Migration vs Exchange 프로토콜
- Exchange: **자산 교환** (x from X ↔ y from Y), 자산은 각 체인에 남음
- Migration: 자산을 **다른 체인으로 옮겨서 그곳에서만 유효하게 사용**
- Migration에서는 자산을 잠그거나 소각하고 **Representation token**을 발행
- 보통 TTP가 자산을 보관하거나 발행 권한 가짐 → 보편적 설계

---

## 📌 보완 가능성 및 아이디어
- CCC 단계를 **스마트 컨트랙트 기반으로 자동화**할 수 있다면?
- Watchtower를 **ZKP 기반 오프체인 인프라와 결합**할 수 있을까?
- Overcollateral 구조의 효율성과 경제성 향상 방안은?

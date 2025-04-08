# 📘 SoK: Communication Across Distributed Ledgers - 논문 리뷰

본 저장소는 논문 **"SoK: Communication Across Distributed Ledgers" (IEEE EuroS&P 2023)**에 대한 구조화된 리뷰입니다.  
단순 요약을 넘어서 **논문이 제시하는 문제의식(WHY), 해법의 구조(HOW), 적용 사례 및 기여점(WHAT)**을 중심으로 논리 전개 흐름과 핵심 개념들을 반영하였습니다.

---

## 📌 리뷰 목표

- 블록체인 간 안전한 통신(CCC: Cross-Chain Communication) 문제를 공식화한 논문 구조 완전 이해
- CCC 프로토콜 단계별 설계 방식(Commit, Verify, Abort)과 신뢰 모델 구조 파악
- CCC 설계 방식에 대한 기존/미래 프로토콜 패턴 분류 및 응용 가능성 탐색
- 스마트 컨트랙트, Watchtower, ZKP 기반 자동 검증 등 구조적 패턴 이해

---

## 🧠 논문 핵심 구조 및 논리 흐름

### 🔍 Why: CCC(Cross-Chain Communication)의 필요성과 문제
- 서로 다른 블록체인 간의 자산 이전, 상태 동기화, 프라이버시 보호 등 필요성이 증가
- 기존 원자적 커밋(Atomic Commit) 모델은 블록체인의 네트워크 지연, 실패 가능성 등으로 **그대로 적용 불가**
- 다양한 CCC 프로토콜이 제안되었지만, **공식적인 정의 및 분류 체계가 부재**

### 🛠️ How: 논문이 제안한 설계 방식 및 분류 체계
1. **Section 2:** 일반화된 CCC 프로토콜 정의 (Pre-commit → Commit → Verify → Optional Abort)
2. **Section 3:** CCC 설계 시 만족해야 할 3가지 핵심 속성
   - Effectiveness, Atomicity, Fairness
3. **Section 4:** CCC 단계별 설계 옵션 제시
   - Commit, Verify, Abort 단계별로 TTP / Synchrony / Hybrid 모델 구성
   - Escrow, Watchtower, Chain Relay 등 구조화된 설계 패턴 소개
4. **Section 5:** 이 프레임워크로 기존 프로토콜(Atomic Swap / Migration / Sidechain 등)을 정량적으로 분류

### 🧾 What: 논문의 기여 및 의미
- 최초로 CCC를 **공식화하고**, 단계별로 설계 구조화
- 다양한 실무 프로토콜을 통일된 프레임워크로 비교 가능하게 만듦
- ZKP, Timelock, Chain Relay, Watchtower 등의 **설계 요소에 대한 비교 구조화**
- 향후 설계 및 연구에 있어 **구조 중심 사고 기반의 확장 가능성 제시**

---

## 📂 디렉토리 구조

```
SoK-DistributedLedger-Review/
├── README.md
├── images/
│   ├── atomic_swap_diagram.png
│   ├── hybrid_model_watchtower.png
│   ├── commit_verify_abort_flow.png
│   ├── Abort_Phase(3_scenario_Model).png
│   ├── BlockCreation_Flow&ProofConvey_Flow_Diagram.png
├── notes/
│   ├── concept_questions.md
│   ├── section-by-section-analysis.md
```

---

## ✍️ 리뷰 방식
- 논문 전체 직접 정독
- 섹션별 주요 질문 생성 → ChatGPT를 통한 개념 정리와 구조화
- 구조별 다이어그램 직접 설계하여 학습 시각화
- 이해를 넘어 구조적 재구성 기반으로 정리


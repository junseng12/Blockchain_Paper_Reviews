# 📘 SoK: Communication Across Distributed Ledgers - 논문 리뷰

본 저장소는 논문 **"SoK: Communication Across Distributed Ledgers" (IEEE EuroS&P 2023)**에 대한 체계적이고 연구자 중심의 리뷰 내용을 담고 있습니다.

본 리뷰는 단순 요약이 아닌, **CCC(Cross-Chain Communication)** 구조의 설계 원리, 프로토콜 패턴, 신뢰 모델, 그리고 ZKP와의 연관성까지 깊이 있게 분석하며,  
후속 연구 방향성과 아이디어까지 탐색하는 **연구 기반 리뷰**를 목표로 합니다.

---

## 🎯 리뷰 목적

- 이기종 블록체인 간 커뮤니케이션 구조에 대한 **시스템적 이해 확보**
- 기존 CCC 프로토콜의 구성 요소, 설계 방식, 신뢰 가정 비교
- **ZKP 기반** 데이터 검증, Escrow, Watchtower 등 설계 패턴 분석
- 구조화된 리뷰를 통해 **자신만의 연구 아이디어 도출**

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

## 🧠 리뷰 전략 및 방식

- **WHY → HOW → WHAT** 흐름으로 접근
- 논문 전체 직접 정독하며 질문 기반으로 개념 재정의
- 주요 개념은 ZKP, Atomicity, Synchrony, Watchtower, Escrow, Validator
- CCC의 Commit / Verify / Abort 단계별 설계 패턴 구조화
- 각 구조를 시각화해 **패턴별 장단점 및 적용 조건** 비교

---

## 🛠 사용 기술 및 참고 모델

- 📘 논문: SoK: Communication Across Distributed Ledgers (Zamyatin et al.)
- 📎 시각화 도구: ChatGPT 기반 다이어그램 생성 (PNG)
- 🧠 분석 방식: 능동적 질문 기반 개념 재구성, 구조 비교, 시나리오 설계

---

## 💡 리뷰 완료일: 2025-04-08

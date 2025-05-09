## 🧠 Platypus: A CBDC with Unlinkable Privacy

### 📁 디렉터리 구조

```
Blockchain_Paper_Reviews/
└── Platypus-CBDC-Review/
    ├── README.md
    ├── Platypus_Structure.md
    ├── images/
    │   └── .gitkeep
    └── notes/
        ├── Concept_QnA.md
        └── section-by-section-analysis.md
```

### 🔍 논문 개요

- **논문명**: Platypus: A Central Bank Digital Currency with Unlinkable Transactions
- **핵심 주제**: 블록체인이 아닌 전통 e-cash 스타일을 기반으로 프라이버시 보장과 확장성을 달성하는 CBDC 설계
- **핵심 제안**:

  - 계정 기반(Account-based) e-cash 시스템
  - 완전한 unlinkability와 privacy 보장
  - 규제(AML/KYC)를 위배하지 않는 영지식 증명 기반 프레임워크

### 📐 핵심 문제 정의

- **문제**: 기존 블록체인 기반 설계는 프라이버시, 확장성, 규제 대응을 동시에 충족하지 못함
- **중심 이슈**:

  - 기존 e-cash는 확장성 부족 (e.g., coin 단위 분할 사용, 선형 증가 비용)
  - 기존 account 시스템은 프라이버시 결여
  - Zcash/UTXO 기반은 규제 프레임 적용 어려움

Platypus는 이를 해결하기 위해 **계정 기반의 ZKP 통합형 CBDC 설계**를 제안함

### ⚙️ 시스템 구성 요소

- **중앙은행 (CB)**: 거래 무결성 검증 및 서명

- **규제기관 (Regulator)**: 사용자 등록, 인증서 발급, 규제 준수 확인

- **사용자 (Client)**: 계좌 상태 관리 및 송수신 거래 수행

- **ZKP 기반**: 모든 트랜잭션은 발신자, 수신자 모두의 ZKP로 보호됨

- **커밋 스키마**: 계좌 상태를 커밋(commit)으로 저장하여 privacy 유지

### 🔑 기술 개요

- **Tx 생성**: Alice는 BlindTx와 value를 커밋한 후 Bob에게 전송 → Bob이 상태 업데이트 증명 생성
- **ZKP 검증**: 송수신자 모두 ZKP로 상태 업데이트 정당성 증명
- **RegInfo 시스템**: soft limit 이상 시 신원+잔액을 암호화하여 규제자에게 제공

### 📈 결과 요약 (Table 1 기준)

- Groth16 (BN256, BLS12-381) 기반 구현
- ZKP 생성 시간: 모바일에서 수 초 이내
- 검증 시간: 수십 ms (서버), 많은 트랜잭션 병렬 처리 가능
- 유럽 결제량 대비 17\~25대 머신으로 대응 가능

### 🌐 건축적 의의

- 계정 기반 설계에서 **완전한 unlinkability** 달성
- 정책 적용 범위 확장 (보유한도, 수신한도 등)
- 규제기관과 사용자 간 균형 있는 프라이버시/컴플라이언스 모델

### 📘 참고 정보

- 논문 저자: Bayer, Chatzigiannis, Lueks, Maffei, et al.
- 발표: IEEE S\&P (Security & Privacy) 2023

---

😀 By 이준승 | 아주대학교 사이버보안학과 | GitHub: junseng12

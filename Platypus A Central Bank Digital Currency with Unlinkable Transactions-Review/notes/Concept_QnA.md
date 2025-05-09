# 📚 Concept_QnA: Platypus 논문 핵심 개념 및 질문 응답 정리

본 문서는 Platypus 논문을 읽으며 발생한 주요 질문과 이에 대한 해설을 담았습니다.
ZKP, 계정 상태 커밋, 규제 프레임워크 등 핵심 기술 요소에 대한 이해를 심화하는 데 목적이 있습니다.

---

## 🔐 1. ZKP 생성과 관련한 개념

### Q. Alice가 생성하는 ZKP는 어떤 값을 증명하기 위한 것인가요?

**A.** ZKP는 Alice가 기존 계정 상태(state i)에서 새로운 상태(state i+1)로 업데이트를 정당하게 수행했음을 증명합니다.

- 이 과정에서 사용된 값은 serial, balance, blind (비밀 값)이며,
- 공개된 값(commTx, state i+1, pk 등)과 일치함을 증명합니다.
- 실제 회로화는 Circom 등으로 수행되며, 이를 통해 Groth16 기반 ZKP가 생성됩니다.

### Q. 왜 state i+1과 zkpi+1은 보내지만, serial은 state i 기준인가요?

**A.** serial은 기존 계정 상태(state i)에 대한 유일 식별자입니다.

- 이 serial이 중복되지 않게 하여 **이중 지출을 방지**합니다.
- 따라서 거래 시 사용된 serial 값은 이전 상태 기준이어야 하며, 새 상태(state i+1)는 그 이후 값입니다.

---

## 💳 2. Platypus 거래 흐름 관련

### Q. commTx는 왜 Bob이 생성한 zkpi+1에 재사용되나요?

**A.** commTx는 Alice가 보낸 거래의 핵심 커밋이며, Bob은 이 값이 정당하게 생성되었음을 확인해야 합니다.

- Bob은 이를 입력으로 사용하여 자신의 ZKP를 생성합니다.
- 이는 거래가 연동된다는 구조적 특성을 보여줍니다.

### Q. 중앙은행이 서명한 값을 Bob이 받아 Alice에게 다시 전달하는 이유는?

**A.** 중앙은행이 거래 로그에 서명한 결과는 신뢰의 출처입니다.

- 이를 Bob이 받고, Alice에게 전달함으로써 거래가 정당하게 처리되었음을 서로 확인할 수 있습니다.
- 이는 일종의 **off-chain acknowledgement** 역할을 합니다.

---

## 🏛️ 3. Regulation 관련 개념

### Q. Platypus에서 account state에 어떤 추가 정보(aux)가 저장되나요?

**A.**

- epoch number
- 해당 epoch에서 받은 총 수령 금액
- 인증된 public identity (piU)
- holding limit 정보
- 송수신 정보 관련 정합성 자료

이러한 정보는 regulation ZKP 생성에 사용되며, aux에 커밋되어 영지식으로 증명됩니다.

### Q. checkOther, updateAux, RegInfo 함수의 역할은 무엇인가요?

**A.**

- **updateAux:** 거래가 끝날 때마다 새로운 규제 관련 보조 정보를 업데이트합니다.
- **checkOther:** 규제 조건을 만족했는지 확인합니다 (예: 보유량 초과 여부).
- **RegInfo:** 해당 거래가 조건에 따라 신원, balance 등을 포함하거나 더미값을 반환하여 규제기관에게 보냅니다.

### Q. Soft limit이란 무엇인가요?

**A.**

- Hard limit은 초과 시 아예 거래 불가
- Soft limit은 초과 시 거래는 되지만 → 신원 및 금액을 암호화하여 Regulator에게 전달됨
- 이때 사용하는 암호화 정보는 ZKP로 감춰져 있고, **limit을 넘었는지 여부**만 확인 가능함

---

## 🔍 4. TX 위조 불가능성 & 구분 불가능성

### Q. TX 위조 불가능성은 어떻게 증명되나요?

**A.**

- 공격자는 trapdoor 없이 새로운 유효한 TX를 만들 수 없음 (ZKP soundness)
- 공격자가 커밋을 위조하면 binding 위배
- ZKP 없이 balance를 조작하려 하면 commitment hiding 위배

### Q. TX 구분 불가능성 증명에서 hybrid argument란?

**A.**

- 실제 TX → 완전 랜덤 TX로 점진적으로 변환하며 단계별 차이를 측정
- 삼각 부등식을 통해 "전체 차이가 크다면 중간 단계 중 하나는 구분 가능" → 모순 발생
- 따라서 전체 TX도 구분 불가능함을 증명

---

## 🧠 5. 서명, 시리얼 생성, 회복성

### Q. serial 값 충돌 공격이 왜 어려운가요?

**A.** serial은 의사난수 함수의 반복 적용으로 만들어짐: `serialᵤⁱ = f^i(skᵤ₁)(0)`

- 공격자는 f^j(sk′)(0) = f^i(skᵤ₁)(0)를 만족시키는 sk′, j를 찾아야 함
- 이는 PRF의 pre-image 찾기와 같으며 계산적으로 불가능

### Q. 계정 상태만 복구한 후, memo field는 왜 필요한가요?

**A.**

- account state만으로는 balance, serial, blind, aux 정보가 드러나지 않음
- memo 필드에 암호화하여 저장해두고, 복구 후 이를 복호화하여 사용함
- Zcash의 memo 구조에서 아이디어를 차용

---

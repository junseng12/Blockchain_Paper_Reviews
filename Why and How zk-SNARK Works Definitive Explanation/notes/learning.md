# 📘 zk-SNARK 학습 요약 (2025-05-26)

**범위:** Section 3.1 ~ 3.4 (Polynomial Proofs, Homomorphic Encryption, Polynomial Restriction)  
**출처:** [Why and How zk-SNARK Works (arXiv:1906.07221)](https://arxiv.org/abs/1906.07221)

---

## ✅ 핵심 학습 내용

### 1. Polynomial Evaluation (`3.1`)

- 증명자는 다항식 `p(x)`를 알고 있다고 주장
- 목표는 `p(x) = t(x) * h(x)` 구조가 성립함을 증명
- 검증자는 무작위 `r`을 선택해 t(r) 제공 → `p(r) = t(r) * h(r)` 비교
- ⚠️ 단점: `r`을 안다면 증명자가 거짓 p(x)도 만들 수 있음 → 보안 취약

---

### 2. Homomorphic Encryption (`3.3`)

- 암호화 함수: `E(m) = g^m mod p` (g는 공개된 생성자)
- 동형성 성질:
  - 덧셈: `E(a) * E(b) = E(a + b)`
  - 스칼라곱: `E(a)^k = E(k * a)`
- zk-SNARK에서:
  - 검증자가 `E(s^i) = g^{s^i}` 전달 (s는 비공개)
  - 증명자는 계수 `{c0, c1, c2, ...}`에 따라 계산:
    ```
    E(p(s)) = ∏ E(s^i)^ci = g^{p(s)}
    ```
  - s는 몰라도 `g^{p(s)}`는 계산 가능

---

### 3. Polynomial Restriction (`3.4`)

- 목적: 증명자가 검증자가 제공한 `E(s^i)`만 사용했는지 확인
- 방법:
  - 검증자가 `E(s^i)`와 `E(α * s^i)`도 함께 제공 (α는 검증자만 아는 랜덤값)
  - 증명자는:
    - `gp = g^{p(s)}`
    - `gp' = g^{α * p(s)}`
  - 검증자는 다음 확인:
    ```
    gp^α == gp'
    ```
- 이 관계가 성립하면, 증명자가 제공된 값만 사용했음을 확인할 수 있음

---

## 💡 오늘 중점적으로 고민한 질문 & 개념 정리

| 개념                                          | 주요 질문/이슈                                                |
| --------------------------------------------- | ------------------------------------------------------------- |
| g의 역할                                      | g는 공개된 생성자로, 암호화 대상은 지수 m임                   |
| 증명자는 s를 몰라도 어떻게 p(s)를 계산하는가? | 동형암호 성질을 이용해 `g^{s^i}`를 계수와 곱하여 계산         |
| g^{p(s)}는 무슨 의미?                         | 증명자가 `p(x)`를 알고 있음을 암호화된 상태로 표현한 것       |
| 검증자는 g^{p(s)}로 무엇을 아는가?            | 값 자체는 모르고, 그 계산이 정당한 흐름인지만 검증            |
| gh = g^{h(s)}는 어떻게 만드나?                | `p(x) / t(x)` 다항식 나눗셈을 통해 h(x) 추출 후 g^{h(s)} 계산 |

---

# 📘 zk-SNARK 학습 요약 (2025-06-04)

**범위:** Section 3.5 \~ 4.6.2 (Zero-Knowledge, Trusted Setup, Multi-Operation, Variable Polynomials)
**출처:** [Why and How zk-SNARK Works (arXiv:1906.07221)](https://arxiv.org/abs/1906.07221)

---

## ✅ 핵심 학습 내용

### 1. Zero-Knowledge 성질 부여 (`3.5`)

- 증명값 `g^{p(s)}`만 제공하면, 증명 내용이 유출될 수 있음
- **ZK 보장**을 위해 증명자 임의의 랜덤값 `δ`를 곱함
- 증명자는 다음을 제출:

  ```
  g^{δ·p(s)}, g^{α·δ·p(s)}, g^{δ·h(s)}
  ```

- 검증자는 pairing을 통해 다음 식 확인:

  ```
  e(g^{α·δ·p(s)}, g) = e(g^{δ·p(s)}, g^α)
  e(g^{δ·p(s)}, g) = e(g^{δ·h(s)}, g^{t(s)})
  ```

- ⇒ 암호화된 상태에서 올바른 연산이 이루어졌음을 확인하며, 실제 p(s)는 노출되지 않음

---

### 2. CRS & Trusted Setup (`3.6`)

- **CRS (Common Reference String)**: 미리 계산된 `g^{s^i}`, `g^{α·s^i}` 들의 집합
- 대화형 구조를 비대화형으로 바꾸기 위한 핵심 요소
- `Trusted Setup` 과정에서 증명자와 검증자가 공통의 참조값을 가지게 함

#### 주요 개념 요약:

| 항목            | 설명                                                  |
| --------------- | ----------------------------------------------------- |
| CRS             | `g^s`, `g^{s^2}` 등 고정된 다항식 평가 암호문 집합    |
| Trapdoor        | `s`를 알면 거짓 증명도 가능함 ⇒ 외부에 공개 금지      |
| 다자간 Ceremony | 여러 참가자가 `s_i`를 독립적으로 선택하여 신뢰도 확보 |
| Powers of Tau   | SNARK용 다항식 암호화를 위한 일반적 setup 프로토콜    |

---

### 3. Succinct Non-Interactive Argument (`3.7`)

- zk-SNARK은 결국 다음 식의 암호화된 증명을 목표로 함:

  ```
  p(x) = l(x) * r(x) - o(x)
  p(x) = t(x) * h(x)
  ```

- 각 다항식 `l(x), r(x), o(x)`에 대해 다음 암호문 생성:

  ```
  g^{δ·l(s)}, g^{δ·r(s)}, g^{δ·o(s)}
  g^{α·δ·l(s)}, g^{α·δ·r(s)}, g^{α·δ·o(s)}
  ```

- pairing 기반 검증식으로 제약 조건 확인

---

## 🧮 General-Purpose Proof 구조 (`4.1 ~ 4.4`)

### 4.1 Computation

- 회로의 제약을 다항식으로 표현:

  ```
  l(x)·r(x) = o(x) + t(x)·h(x)
  ```

### 4.2 Single Operation

- 단일 제약에 대해 각각 다항식 구성
- p(x) = l(x)·r(x) − o(x) 형태로 구성 후, pairing을 통해 증명

### 4.3 Enforcing Operation

- p(x) = t(x)·h(x)인지 검증해야 함
- 암호문만으로는 곱셈 불가 ⇒ pairing으로 제한 검증 수행

### 4.4 Proof of Operation

- 증명자는:

  ```
  g^{l(s)}, g^{r(s)}, g^{o(s)}, g^{α·l(s)}, g^{α·r(s)}, g^{α·o(s)}
  ```

  을 제출함

- 검증자는 pairing을 통해 위 다항식의 관계와 동일한 s 사용을 확인
- 알파 시프트(`α`)는 다항식 위조를 막는 역할

---

## 🧮 Multiple Operations & Variable Polynomials (`4.5 ~ 4.6.2`)

### 4.5.1 Polynomial Interpolation

- 여러 연산을 다항식 하나로 통합하려면 `t(x)`의 **근**이 각 연산 위치를 포함해야 함
- 예: 연산이 x=1, 2, 3에서 일어났다면:

  ```
  t(x) = (x - 1)(x - 2)(x - 3)
  ```

### 4.5.2 Multi-Operation Polynomials

- 하나의 다항식으로 여러 연산을 표현 가능하지만, 변수 간 독립성을 침해할 수 있음
- 동일한 `a`값을 모든 연산에서 보장하려면, 다항식의 \*\*비례성(proportion)\*\*만 유지해야 함

  - 즉, `v·l(x)`는 가능하지만 `l(x) + u(x)`는 불가 (pairing 전에 암호화 상태에선 곱셈 안됨)

### 4.6.1 Single-Variable Operand Polynomial

- `l(x)` 다항식이 하나의 변수 `a`만 반영할 때, x=1,2,3 모두 동일한 값 `a`여야 함
- 하지만 prover가 각 위치에서 다른 값을 대입하면 부정확한 증명이 됨 ⇒ 막아야 함
- **해결책**: `g^{l(s)}`와 `g^{α·l(s)}`를 함께 검증하여, 하나의 l(x)에 대해 증명했음을 보장

### 4.6.2 Multi-Variable Operand Polynomial

- 서로 다른 변수 (a, d 등)를 다룰 경우 `l_a(x)`, `l_d(x)` 등의 **변수 다항식**을 개별 정의
- 예:

  - `l_a(x)`는 x=1,2에서 1, 나머지 0
  - `l_d(x)`는 x=3에서 1, 나머지 0

- 각각의 다항식에 값 곱하고 합산하면, 다항식이 전체 연산을 표현함:

  ```
  l(x) = a·l_a(x) + d·l_d(x)
  ```

- 이로써 변수별 독립성과 ZK 보장 유지

---

## 💡 오늘 중점적으로 고민한 질문 & 개념 정리

| 개념                                        | 질문/이슈                                                        |
| ------------------------------------------- | ---------------------------------------------------------------- |
| 왜 g^{a·b}는 계산이 불가능한가?             | 지수의 곱은 일반적인 암호화 연산에서 불가능 → pairing으로 우회함 |
| 왜 증명자는 다항식 계수를 변경할 수 없는가? | α 시프트가 없이는 다항식의 각 항목을 독립적으로 조작 불가함      |
| 왜 동일 변수는 하나의 값을 가져야 하는가?   | 동일 입력에 대해 회로 전체가 하나의 일관된 흐름을 갖기 위해 필요 |
| 왜 u(x)로 곱하면 위험한가?                  | 다항식 비율이 깨지면, 전체 구조를 변경할 수 있어 위조 우려 발생  |
| 변수 분리의 목적은?                         | 다수 연산을 다룰 때, 변수마다 독립적 제약을 부여하기 위함        |

---

## 🧮 Constraint System as Polynomials (`4.7`)

### 4.7.1 Constant Coefficients

- QAP에서 각 Gate 연산을 다항식으로 표현할 때, 변수마다 **상수 계수(coefficient)** 가 정확히 적용되어야 함

- Gate의 위치(x=1,2,3,...)마다 coefficient가 달라지므로, 해당 위치에서 원하는 coefficient가 나오도록 **Lagrange 보간법** 사용

- Gate i에 대해:

  ```
  L(x) = Σ vᵢ ⋅ lᵢ(x)
  ```

  - lᵢ(x)는 Gate 위치 i에서 1, 나머지에서 0을 출력

- 최종 QAP 다항식 검증 구조:

  ```
  P(x) = L(x) × R(x) - O(x) ≡ 0 mod Z(x)
  ```

- 🚩 **핵심 insight**
  Gate별 coefficient는 고정 구조로 구성됨 → Prover는 Witness 값만 넣으면 됨 (coefficient 구성은 고정)

### 4.7.2 Addition for Free

- 덧셈(Addition)은 Multiplication처럼 Gate 비용을 사용하지 않고 **공짜(free)** 로 처리 가능

- 덧셈을 다음과 같이 표현:

  ```
  (Σ cLᵢ ⋅ vᵢ) × 1 = (Σ cOᵢ ⋅ vᵢ)
  ```

- 즉, R(x)는 항상 1로 설정하여 Multiplication 없이 처리

- L(x), O(x)는 덧셈에 필요한 coefficient만 정확히 구성

- 🚩 **핵심 insight**
  덧셈은 QAP에서 R(x)=1로 처리 가능 → 효율적인 회로 설계 가능

### 4.7.3 Addition, Subtraction and Division

- **덧셈(Addition)** 은 4.7.2처럼 free로 처리 가능

- **뺄셈(Subtraction)** 은 Addition과 동일 구조에서 coefficient에 **음수(-)** 를 적용하면 됨

  ```
  (Σ cLᵢ ⋅ vᵢ) × 1 = (Σ cOᵢ ⋅ vᵢ), with negative cLᵢ or cOᵢ
  ```

- **나눗셈(Division)** 은 상수에 대한 나눗셈일 경우 **곱셈의 역수(1/d)** 로 처리 가능

  ```
  Division by d → Multiplication by (1/d)
  ```

- 모든 연산은 (Σ cLᵢ ⋅ vᵢ) × (Σ cRᵢ ⋅ vᵢ) = (Σ cOᵢ ⋅ vᵢ) 형태로 일관되게 구성 가능

- 🚩 **핵심 insight**
  Addition/Subtraction/Division 모두 QAP 구조에 자연스럽게 포함 가능 → 다양한 산술 연산 지원 가능

---

완벽해 —
그럼 아까 네가 주신 패턴 그대로 유지해서
**4.8 전체 (4.8 full 내용 + 네가 질문한 흐름 반영)** 동일 포맷으로 깔끔하게 정리해줄게.

---

## 🧮 Multiple Operations (`4.8`)

### 4.8 Multiple Operations

- 우리가 QAP에서 프로그램을 증명할 때, 특정한 **입력값**을 설정하고 그에 따른 **중간 변수 값**을 계산하여 Witness vector를 구성해야 함

- 논문 예제에서는:

  ```
  입력값: w = 1, a = 3, b = 2
  중간 변수: m = a × b = 6
              v = w(m − a − b) + a + b = 6
  ```

- Witness vector는 다음과 같이 구성됨:

  ```
  v = [1, w, a, b, m, v]
  ```

- 이후, 이 Witness vector의 값들을 L(x), R(x), O(x) 구성 시 coefficient로 사용함

- Gate별로 연산 constraint는 다음과 같은 형태로 QAP에 포함됨:

  ```
  (Σ cLᵢ ⋅ vᵢ) × (Σ cRᵢ ⋅ vᵢ) = (Σ cOᵢ ⋅ vᵢ)
  ```

- Lagrange 보간법을 통해 Gate 위치별로 L(x), R(x), O(x)를 구성

- 여기서 중요한 점:

  - **입력값은 Prover가 임의로 설정 가능** (w, a, b는 원하는 값 사용 가능)
  - **중간 변수는 프로그램 로직에 따라 결정됨** (m, v는 Gate 연산 결과로 고정됨)

- Prover는 L(x), R(x), O(x) 구조만 고정된 상태에서 Witness 값만 정확히 넣어주면 됨

- 결과적으로, 입력값이나 중간 변수 값이 무엇이든 QAP constraint가 만족되면 증명 성공

- 🚩 **핵심 insight**
  L(x), R(x), O(x)는 Gate 구조로 고정됨 → Prover는 Witness 값만 정확히 넣으면 됨
  입력값은 자유롭게 설정 가능 (공개/비공개 input으로 구분 가능)
  중간 변수는 프로그램 흐름에 의해 고정 계산됨 → 이를 기반으로 증명 진행

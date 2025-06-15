# 📘 Witness Vector 개념

## 🔍 정의: Witness Vector란?

**"Prover가 증명하고자 하는 계산 과정의 *모든 변수 값들*을 나열한 벡터."**

- **Witness Vector**는 ZK-SNARK에서 Prover가 알고 있는 값을 하나의 벡터로 정리한 것으로, 증명하고자 하는 연산 회로의 입력값, 중간 계산값, 출력값, 상수값 등을 모두 포함한다.
  → 이 벡터가 **Prover가 알고 있는 '증명 데이터' 전체**임.

이 벡터는 QAP(Quadratic Arithmetic Programs) 기반 증명에서 핵심적으로 사용되며, 다항식 구성과 pairing 검증 구조에 직접 연결된다.

---

## 🧠 WHY: 왜 Witness Vector가 필요한가?

- ZK-SNARK에서는 회로 상의 연산들을 **다항식 제약식(polynomial constraints)** 으로 바꾼 후,
  증명자가 해당 제약식을 만족하는지 증명해야 함.
- 이때 회로의 값들을 통일된 형태로 표현해야 하고, 그게 바로 Witness Vector다.
- 이 벡터는 QAP의 다항식들 $L(x), R(x), O(x)$ 구성에 직접 사용된다.

---

## ⚙️ HOW: 구성 방식

Witness Vector는 아래와 같은 형식으로 구성된다:

```math
\vec{v} = [v_0, v_1, v_2, ..., v_n]
```

- 항상 **첫 번째 원소는 1로 고정** → constant term 지원용.
- 그 뒤에:

  1️⃣ **Public input(s)** → Verifier도 알고 있는 공개 입력 값

  2️⃣ **Private input(s)** → Prover만 아는 비공개 입력 값

  3️⃣ **Intermediate variable(s)** → 프로그램 계산 도중 발생하는 중간 값들 (ex: 곱셈 결과 등)

### 수식적 표현

```math
v = [1, x₁, x₂, ..., xₚ, w₁, w₂, ..., wₖ, z₁, z₂, ..., zₘ]
```

- x₁ \~ xₚ → public inputs
- w₁ \~ wₖ → private inputs
- z₁ \~ zₘ → intermediate variables

## 🧨 구성 방법 - 단계별 구성 흐름

1️⃣ 프로그램을 회로로 변환함 → **Arithmetic Circuit**으로.
(ex: 곱셈/덧셈 Gate로 표현)

2️⃣ Circuit에서 각 Gate를 순서대로 "변수 슬롯"에 배정:

- 입력 변수 → 슬롯 할당
- 중간 변수 → Gate 출력 결과에 슬롯 할당
- Public output → 별도로 public output 슬롯에 할당

3️⃣ 이렇게 해서 **Witness Vector의 각 원소에 대응되는 변수 값**을 정함.

### ✅ 예시

프로그램 흐름:

```plaintext
1. m = a * b
2. v = m + c
```

그에 따른 Witness Vector:

```math
\vec{v} = [1, a, b, m, c, v] = [v_0, v_1, v_2, v_3, v_4, v_5]
```

```python
m = a * b
v = m + c
```

**회로 구조:**

- Gate 1: a \* b → m
- Gate 2: m + c → v

**Gate 1 (x=1): m = a \* b**

→ L(1) = a
→ R(1) = b
→ O(1) = m

Constraint:

```math
a * b - m = 0
```

**Gate 2 (x=2): v = m + c**

→ L(2) = m + c
→ R(2) = 1
→ O(2) = v

Constraint:

```math
(m + c) * 1 - v = 0
```

**Witness Vector 구성:**

```math
v = [1, a, b, c, m, v]
```

→ v₀ = 1
→ v₁ = a
→ v₂ = b
→ v₃ = c
→ v₄ = m = a \* b
→ v₅ = v = m + c

| Index | 내용       | 의미                       |
| ----- | ---------- | -------------------------- |
| v_0   | 1          | 상수항                     |
| v_1   | a          | 입력값                     |
| v_2   | b          | 입력값                     |
| v_3   | m = a \* b | 중간 계산값                |
| v_4   | c          | 중간 입력값 또는 외부 입력 |
| v_5   | v = m + c  | 최종 출력값                |

---

## 🧩 WHAT: Witness Vector는 다항식 구성에 어떻게 연결되는가?

QAP에서는 다음과 같은 방식으로 $L(x), R(x), O(x)$ 다항식을 구성한다:

```math
L(x) = \sum_{i} v_i \cdot L_i(x), \quad R(x) = \sum_{i} v_i \cdot R_i(x), \quad O(x) = \sum_{i} v_i \cdot O_i(x)
```

여기서:

- $v_i$: Witness Vector의 i번째 값
- $L_i(x), R_i(x), O_i(x)$: i번째 변수에 해당하는 선택 다항식 (Selection Polynomial)

---

## ✍️ 구체적 동작 예시 (Gate 단위)

### 예: 첫 번째 Gate에서 연산: $a \cdot b = m$

해당 Gate에서는:

- $L(x) = a$, $R(x) = b$, $O(x) = m$
- 즉,

```math
L(x) = v_1 \cdot L_1(x), \quad R(x) = v_2 \cdot R_2(x), \quad O(x) = v_3 \cdot O_3(x)
```

- 선택 다항식은 다음처럼 구성됨:

  - $L_1(x) = 1$ at x=1, else 0
  - $R_2(x) = 1$ at x=1, else 0
  - $O_3(x) = 1$ at x=1, else 0

- 그러면 이 Gate에서는:

```math
L(1) = a, \quad R(1) = b, \quad O(1) = m
```

⇒ $a \cdot b = m$ 이 성립함을 보일 수 있음.

---

## 🎈 핵심 역할

**Witness Vector가 갖는 의미:**

- **Prover가 "정말로 이 계산을 정확히 수행했는지"를 증명하는 핵심 데이터 구조.**
- Verifier는 Witness Vector 값은 모르지만, L(x), R(x), O(x)에 Prover가 그 Witness를 기반으로 어떻게 값 넣었는지 pairing으로 검증.

**한마디로 말하면:**

> Witness Vector = Prover가 제출하는 "나의 계산 로그 전체 기록"
> → 이 기록을 다항식으로 변환하여 증명으로 넘김.

---

## 🔗 관련 수식 (범용 표현)

```math
\left( \sum_{i=1}^n c_{L,i} \cdot v_i \right) \cdot \left( \sum_{i=1}^n c_{R,i} \cdot v_i \right) = \sum_{i=1}^n c_{O,i} \cdot v_i
```

- 여기서 $c_{L,i}, c_{R,i}, c_{O,i}$ 는 Gate 위치에서 선택 다항식을 평가한 결과값
- 모든 게이트에서 이 관계가 성립되면, 증명자는 연산 전체 흐름이 옳았음을 입증함

---

## 🧠 핵심 요약

| 요소             | 설명                                                     |
| ---------------- | -------------------------------------------------------- |
| Witness vector   | 연산 흐름에 따라 구성된 값들의 배열                      |
| L_i(x), R_i(x)   | 선택 다항식: 특정 위치(Gate)에서 역할 부여               |
| 다항식 구성 방식 | L(x), R(x), O(x)는 모두 $v_i \cdot l_i(x)$ 구조로 구성   |
| 구조적 의미      | 연산 회로를 다항식 기반 QAP 구조로 바꾸는 핵심 연결 고리 |

---

## 🚩 핵심 한 줄 정리

**Witness Vector는 Prover가 알고 있는 "모든 변수 값의 집합"이고, L(x), R(x), O(x) 다항식 구성에 그대로 반영되어 Gate constraint를 만족하도록 구성됨 — zk-SNARK에서 증명 전체의 핵심 재료이다.**

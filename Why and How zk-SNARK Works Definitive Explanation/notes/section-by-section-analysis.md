# 🧩 Section-by-Section Analysis: Why and How zk-SNARK Works

이 문서는 zk-SNARK의 핵심 수학적 구조를 "왜 필요한가(Why) → 어떻게 가능한가(How) → 어떤 방식으로 구성되는가(What)"라는 흐름으로 설명한 기술 논문이다.  
각 섹션을 분석하여 개념 정의, 문제 설정, 해법 프레임워크, 증명 흐름을 정리하였다.

---

## **Section 1. Introduction**

- Zero-Knowledge Proof (ZKP)의 현실적 필요성과 응용 예시 소개
- zk-SNARKs의 정의: _Succinct Non-interactive Argument of Knowledge_ with Zero-Knowledge
- 용례:
  - 비밀번호 없는 인증
  - 프라이버시 보호 결제
  - 블록체인 연산 위임 및 오프체인 검증
- 목표: zk-SNARK이 실제로 어떻게 작동하는지를 직관적으로 설명

---

## **Section 2. The Medium of a Proof**

- 기본적인 증명 방식의 효율성과 보안성 문제 제시
- 다항식의 동일성 검증을 위한 핵심 성질 제시: 두 다항식이 d차이면, d+1개의 점에서 일치하지 않으면 다름
- 이 성질을 활용하여 "지식을 증명하지만 노출하지 않는" 프레임워크 구상

---

## **Section 3. Polynomial-based zk-Proofs**

### **3.1 Proving Knowledge of a Polynomial**

#### 🔍 핵심 문제

- 목표: 증명자가 특정 다항식 `p(x)`를 알고 있음을 증명
- 검증자는 보조 다항식 `t(x)`를 만들고, `p(x) = t(x) · h(x)` 구조를 검증하고자 함
- 방법: 무작위 점 `r`을 정해 `p(r) = t(r) · h(r)`가 성립하는지 비교

#### ⚠️ 한계

- 증명자가 r을 안다면, 해당 r에 맞는 가짜 `p(r)`와 `h(r)`를 위조 가능
- `p(x)`의 차수를 높여도 단일 점에서만 맞으면 속일 수 있음

### **3.2 What Can Go Wrong?**

- `p(x)`의 차수가 `t(x)`보다 크거나 무관한 경우에도, 특정 r에만 맞게 값을 조작 가능
- 따라서 이 단일점 검증은 **검증자 입장에서 의미 있는 제약이 아님**
- → 더 강한 구조가 필요해짐 (즉, 암호화된 상태에서도 신뢰 가능한 계산 구조)

### **3.3 Obscure Evaluation and Homomorphic Encryption**

#### 🔍 핵심 문제

- 증명자가 `r`이나 `s`를 받게 되면 즉석으로 거짓 값을 조작할 위험 존재

#### ✅ 해결 아이디어: Homomorphic Encryption

- 검증자는 `s`에 대한 지수승 값만 암호화해서 제공:
  - `E(s^i) = g^{s^i}`
- 증명자는 계수 `c_i`만 알고 있고, 아래와 같은 방식으로 계산 가능:
  - 덧셈: `E(a) * E(b) = E(a + b)`
  - 스칼라곱: `E(a)^k = E(k · a)`

#### 💡 예시:

- `p(x) = 2x^2 + 3x + 5`
- 증명자가 받은 것:
  - `E(s^2) = g^{s^2}`
  - `E(s) = g^s`
  - `E(1) = g`
- 계산:
  \[
  E(p(s)) = E(s^2)^2 · E(s)^3 · g^5 = g^{2s^2 + 3s + 5}
  \]

#### 💬 자주 등장한 질문들

| 질문                                    | 해설                                                                     |
| --------------------------------------- | ------------------------------------------------------------------------ |
| 증명자는 s를 모르는데 어떻게 계산 가능? | s의 지수승만 암호화되어 제공되며, 증명자는 계수만 곱해서 `g^{p(s)}` 계산 |
| g는 숨겨야 할 값 아닌가?                | ❌ 아니다. g는 공개된 generator이며, 숨기는 대상은 지수(m)               |
| g^{p(s)}를 보면 p(s)를 알 수 있지 않나? | 아니요. DLP (Discrete Logarithm Problem) 때문에 p(s) 추정은 불가능함     |

### **3.4 Restricting a Polynomial**

#### 🔍 핵심 문제

- 증명자가 `E(s^i)` 외의 임의의 값을 사용해 `g^{p(s)}`를 조작할 수 있음

#### ✅ 해결 아이디어: KEA 기반 검증

- 검증자는 `g^{s^i}`뿐 아니라, `g^{α·s^i}`도 제공
- 증명자는 아래 값들을 계산:
  - `gp = g^{p(s)}`
  - `gp' = g^{α·p(s)}`
- 검증자는 다음 등식이 성립하는지 확인:
  \[
  (gp)^α = gp'
  \]
- 이를 통해 증명자가 **검증자가 제공한 s^i들만 사용했음을 증명**

#### 💬 관련 질문 정리

| 질문                                 | 해설                                                                             |
| ------------------------------------ | -------------------------------------------------------------------------------- |
| α는 누가 알고 있는가?                | 검증자만 알고 있음                                                               |
| 증명자는 g^{α·p(s)}도 계산 가능한가? | 네, 제공된 `g^{α·s^i}`에 동일한 계수를 곱해서 계산 가능                          |
| 왜 이 구조가 안전한가?               | 증명자는 α를 몰라 위조할 수 없고, 검증자는 관계만 검증하므로 Zero-Knowledge 유지 |

---

### **3.5: Zero-Knowledge via Masking**

#### 🔍 핵심 문제

- 지금까지의 구조에서는 `g^{p(s)}`, `g^{h(s)}` 등이 증명 과정에서 그대로 노출됨
- 이 값들이 공격자에게 수학적으로 의미 있는 정보를 누설할 가능성 존재
  - 예: 지수 자체를 추정할 수 없더라도 통계적 정보 노출 가능성

#### ✅ 해결 아이디어: 마스킹 (Masking with Random Delta)

- 증명자가 무작위 값 δ를 곱해서 모든 값을 숨김:
  - `g^{p(s)} → g^{δ·p(s)}`
  - `g^{h(s)} → g^{δ·h(s)}`
  - `g^{α·p(s)} → g^{α·δ·p(s)}`
- 이로 인해 값은 은닉되지만, 다음과 같은 **관계는 유지됨**:
  \[
  (g^{δ·h(s)})^{t(s)} = g^{δ·p(s)}
  \quad,\quad
  (g^{δ·p(s)})^α = g^{α·δ·p(s)} = (g^{δ·h(s)})^{α·t(s)}
  \]
- 검증자는 이 구조적 등식만 확인하면 됨

> > 증명 내용은 전혀 노출되지 않으면서도, 수학적으로 제약 조건이 만족되었음을 증명
> > Zero-Knowledge 성질이 성립하는 마지막 핵심 단계

---

### **3.6: From Interactive to Non-Interactive Proof**

#### 🔍 핵심 문제

- 지금까지의 검증 구조는 여전히 "대화형"
  - 검증자가 `s`, `α` 등을 증명자에게 전달해야 함
  - 실전 시스템에서는 상호작용이 불가능하거나 비효율적

#### ✅ 해결 아이디어: CRS (Common Reference String)

- `s`, `α`, `g^{s^i}`, `g^{α·s^i}` 등을 **Trusted Setup**을 통해 미리 생성
- 이들을 "공통 참조 문자열(CRS)"로 고정하여 모든 증명자가 참조 가능하게 함
- 증명자는 CRS만 알고 있어도 `(g^{δ·p(s)})`, `(g^{α·δ·p(s)})` 등을 생성 가능

---

### **3.6.1: Multiplication of Encrypted Values**

#### ⚠️ 문제

- 암호화된 값의 덧셈은 가능:

  $$
  g^a \cdot g^b = g^{a+b}
  $$

- 하지만 암호화된 값의 **곱셈**은 불가능:

  $$
  g^{a} \cdot g^{b} \neq g^{a \cdot b}
  $$

#### ✅ 해결 아이디어 : 곱셈 제약을 다항식 전체에 포함시킴

- 곱셈 제약 예: `a · b = c`
- 이를 회로 전체의 제약 시스템으로 변환:

  $$
  p(x) = L(x) \cdot R(x) - O(x)
  $$

- 조건: $t(x) \mid p(x)$ (즉, p(x)는 t(x)로 나누어 떨어져야 함)
- 검증은 다음과 같이 암호화 상태로 수행:

  $$
  g^{p(s)} = g^{t(s) \cdot h(s)}
  \Rightarrow
  g^{p(s)} = (g^{h(s)})^{t(s)}
  $$

#### 🧩 핵심 개념: QAP (Quadratic Arithmetic Program)

- 회로의 각 제약은 x의 특정 위치에 매핑됨
- 제약 만족 여부를 $x = r_i$ 점에서 평가 가능하게 구성
- 전체 p(x)는 제약 위치들에서 0이 되도록 설계됨

---

#### **3.6.2: Trusted Party Setup**

##### 🔐 문제

> > CRS를 어떻게 신뢰할 수 있는가?

- zk-SNARK은 CRS(Common Reference String)에 `g^s`, `g^{s^2}`, ... 등 사전 계산된 값을 포함
- 이때 s를 알면 위조 증명이 가능 (trapdoor 존재)

##### ✅ 해결 아이디어 : 다자간 CRS 생성(Setup Ceremony)

- 여러 명이 각자 자신의 sᵢ를 사용해 CRS 일부를 생성
- 최종 CRS는 모두의 sᵢ가 조합된 구조로 구성됨
- **Powers of Tau**: `g^τ`, `g^{τ^2}`, ..., `g^{α·τ^i}` 등을 모두 사전 생성
- 신뢰 가정: **“단 한 명만 정직하면 전체 CRS는 안전”** (Trusting One out of Many)
- 각 참여자가 자신의 sᵢ를 폐기하면, 전체 CRS의 trapdoor는 소멸됨
- 위조자는 전체 trapdoor를 복원해야 하지만, 모든 참여자의 sᵢ를 알 수 없음
  > > Section 3.6은 zk-SNARK을 현실적으로 사용 가능하게 만드는 마지막 구성 단계

---

#### **3.6.3: Trusting One out of Many**

##### 📌 주요 메시지

- CRS 생성의 가장 안전한 방법은 **여러 독립된 참여자**가 함께 참여하는 것
- 개별 참여자는 자신의 랜덤 값을 사용해 일부분을 계산하고, 이후 이를 폐기
- 이 구조는 "Ceremony"로 불리며 실제 프로젝트들에서 사용됨 (e.g., Zcash, Plonk)

##### 🧩 CRS 보안 구조

| 구조 요소       | 설명                                                   |
| --------------- | ------------------------------------------------------ |
| 참여자 수       | 많을수록 안전성 ↑                                      |
| 폐기된 trapdoor | 하나라도 있으면 위조 불가                              |
| 공개된 값       | `g^s`, `g^{s^2}`, ...는 공개되나 trapdoor는 알 수 없음 |

---

### **3.7: Succinct Non-Interactive Argument of Knowledge of Polynomial**

#### 🔐 문제

- 지금까지 발생한 문제들의 구현은 자체는 안정했지만, 여전히 필요한 그룹을 통한 ‘대화적’ 방식이었다.
- 사용자 간의 그룹에 의전없이 다음과 같은 관계를 검증할 수 있어야한다:

  1. $g^{p(s)} = g^{t(s)h(s)}$
  2. $g^{\alpha p(s)} = (g^{p(s)})^{\alpha}$

#### ✅ 해결 아이디어: 데이터를 가르기위한 전망적 검증

- 필요 검증값:

  - $\pi_1 = g^{\delta p(s)}$
  - $\pi_2 = g^{\delta h(s)}$
  - $\pi_3 = g^{\alpha\delta p(s)}$

- 검증자는 CRS에 기반해 여기서 검증 값을 생성
- 검사는 pairing을 이용하여 검증:

  - $e(\pi_1, g) = e(\pi_2, g^{t(s)})$
  - $e(\pi_3, g) = e(\pi_1, g^{\alpha})$

#### 🧠 해석

- 이 결과들은 pairing 가성을 활용한 ‘결과의 인수가 다양해진’ 것이기 때문에, 장소가 가능해지고 ‘non-interactive’ 구조를 가지는 다음 과 같은 시스템이 구성되는 것이다.

---

### **4.1: Computation**

#### 🔐 문제

- 실제 ZK-SNARK의 검증은 “계산과정”을 검증해야 한다
- 다크림이나 arithmetic circuit에서 다음과 같은 전차가 필요:

  - 값 드림
  - 인수 계산
  - 반복적 결과 계산

#### ✅ 해결 아이디어: 전체 획사가 되는 검증

- 전체 계산을 “구성규칙” “계산과정”으로 나누고,
- 모든 역할을 QAP의 $p(x) = l(x) \cdot r(x) - o(x)$ 형태로 복사
- $t(x) \mid p(x)$ 을 검증하면 전체 계산과정이 만적된 것을 검증

---

### **4.2: Single Operation**

#### 🔐 문제

- $l(x) \cdot r(x) = o(x)$ 형태의 공수 역할을 ZK-SNARK으로 검증하려면?
- $p(x) = l(x)r(x) - o(x)$ 을 구성하고 CRS로 $g^{l(s)}, g^{r(s)}, g^{o(s)}$ 을 가지는 유저가 검증값과 같이 저장

#### ✅ 해결 아이디어: 모든 검증을 $p(x) \Rightarrow t(x)h(x)$ 형태로 추적

- 데이터 계산 검증을 시작
- 방식: $l(x)r(x) = o(x) + t(x)h(x)$

#### 🧠 해석

- $p(x) = l(x)r(x) - o(x) \Rightarrow t(x) \mid p(x)$ 으로 변환
- 이중 $p(x)$ 에 대해 pairing 검증 가능

---

너무 잘 잡았어 — 지금까지 우리가 대화한 것 + 네 기존 learning.md 틀 **그대로 유지**하면서,
4.3 내용을 **좀 더 구체적이고 명확하게 작성**해줄게:

---

### **4.3: Enforcing Operation**

#### 🔐 문제

- 만약 Verifier가 \$p(x) = l(x)\$ 또는 \$p(x) = l(x) - r(x)\$ 같은 단순 관계만으로 pairing을 검증한다면,
  Prover가 동일한 pairing 구조<같은 증명 내용 - L(x), R(x)>를 **다른 명세(다른 프로그램)** 에서도 재사용하여 공격 가능
- 즉, **Proof 재사용 공격(replay attack)** 가능성 발생
- pairing이 \$l(s) \cdot r(s)\$ 형태만 검증하면, 같은 T(x)를 가진 다른 프로그램에도 Proof가 재활용될 수 있음

#### ✅ 해결 아이디어: \$l(s), r(s), o(s)\$ 의 값을 모두 Verifier가 검증하도록 구성

- QAP 관계를 다음과 같이 구성:

  $$
  l(x)·r(x) = o(x) + t(x)·h(x)
  $$

- Verifier는 Prover로부터 **\$g^{l(s)}, g^{r(s)}, g^{o(s)}\$** 를 모두 전달받음

- pairing 검증은 다음 관계를 체크:

  $$
  e(g^{l(s)}, g^{r(s)}) = e(g^{o(s)} * g^{t(s)·h(s)}, g)
  $$

#### 🧠 해석

- 이렇게 구성하면 **Proof 재사용 공격이 불가**:

  - T(x)는 QAP 고유 구조 → 프로그램이 다르면 보통 T(x)도 달라짐
  - 만약 T₁(x) = T₂(x)인 경우에도 O(x), L(x), R(x)가 프로그램 구조에 따라 다르게 구성되므로 pairing 검증이 깨짐

- Prover가 **기존 Proof 구성값을 다른 명세에서 재활용하지 못하게** 설계한 것

- 결과적으로 Verifier는:

  - QAP 구조 (L, R, O, T)를 기반으로 정확한 pairing 관계가 성립하는지 확인
  - → 프로그램 고유성(program specificity)이 보장됨

#### 🚩 추가 insight

- T(x)가 우연히 동일한 경우에도 O(x), L(x), R(x)는 프로그램의 계산 흐름에 따라 달라지므로 pairing 관계가 깨짐 → Proof 재사용 불가
- T(x)는 **프로그램 형식(fingerprint)** 역할
- O(x), L(x), R(x)는 **프로그램 내용(contents)** 역할 → 회로 계산 흐름에 직접 연결됨
- 결과적으로 Proof는 **특정 프로그램에 강하게 귀속됨** → 안전한 증명 구조 형성

---

### **4.4: Proof of Operation**

#### 🔐 문제

- 제약식 $l(x) \cdot r(x) = o(x)$를 증명해야 하는데,
- 모든 값 $l, r, o$를 암호화 없이 그대로 제출하면 **Zero-Knowledge 성질이 깨짐**

  - 특히, $o$는 결과값이므로 유출되어도 되지만
  - $l, r$은 **내부 변수**라 은닉되어야 함

- 그러나 $o$까지 암호화하면, pairing으로 등식 검증이 어려워짐

---

#### ✅ 해결 아이디어: 선택적 마스킹 구조

| 항목        | 증명자가 제공하는 값                                               |
| ----------- | ------------------------------------------------------------------ |
| 입력 다항식 | $g^{\delta \cdot l(s)}$, $g^{\delta \cdot r(s)}$ → **마스킹 적용** |
| 출력 다항식 | $g^{o(s)}$ → **그대로 공개**                                       |

검증자는 pairing 관계를 확인함:

$$
e(g^{\delta \cdot l(s)}, g^{\delta \cdot r(s)}) = e(g^{o(s)}, g^{\delta})
$$

→ 입력은 은닉, 출력만 공개되므로 **ZK 성질을 보존**

---

#### 🧠 해석

| 구분                               | 설명                                               |
| ---------------------------------- | -------------------------------------------------- |
| $g^{\delta l(s)}, g^{\delta r(s)}$ | 입력을 감추기 위한 랜덤 마스킹                     |
| $g^{o(s)}$                         | 결과는 증명의 대상이므로 명시적 제출               |
| Pairing 검증                       | $l \cdot r = o$ 구조를 암호화된 상태에서 확인 가능 |
| Zero-Knowledge 보존                | 입력은 감추고 결과만 제시하므로 ZK 성립            |

---

### **4.5: Multiple Operations & Variable Polynomials**

#### 🔍 핵심 문제

- zk-SNARK에서는 **여러 연산을 하나의 증명으로 통합**하고 싶은 경우가 많음
  → 하지만 이를 잘못 하면 **변수 독립성 침해**, **증명 위조 가능성**이 생김
- → "하나의 t(x) 다항식에 어떻게 여러 연산을 안전하게 encode할 수 있는가?"가 관건

→ 이 Section에서는 QAP에서 **다중 연산 표현 기법**과 **변수 독립성 유지법**을 설명

---

### **4.5.1: Polynomial Interpolation**

#### 🔍 문제

- 여러 연산을 하나의 다항식(t(x))로 통합하려면 \*\*t(x)의 근(zero point)\*\*이 각 연산 위치를 포함해야 함
  → 그래야 **각 x 위치마다 다른 연산을 적용**할 수 있음

#### ✅ 핵심 아이디어

- t(x)를 다음과 같이 구성:

  $$
  t(x) = (x - x_1)(x - x_2) ... (x - x_n)
  $$

  - 여기서 \$x_1, x_2, ..., x_n\$은 연산이 발생하는 위치

- **Polynomial interpolation** 기술을 이용하면, 원하는 x 위치에서 원하는 연산이 적용되게 다항식 설계 가능

#### 🧠 해석

- 이렇게 구성하면 **x=1일 때는 연산1**, **x=2일 때는 연산2** ... 처럼 다중 연산을 하나의 증명으로 검증 가능

---

### **4.5.2: Multi-Operation Polynomials**

#### 🔍 문제

- 한 다항식에서 여러 연산을 encode할 때 발생하는 문제:

  - 서로 다른 변수들(a, b, c, d...)가 **의도치 않게 섞이거나 비독립적으로 처리될 수 있음**
  - 예: Prover가 **x=1에선 a=1, x=2에선 a=5**처럼 서로 다른 값을 증명하면 **위조 가능**

#### ✅ 해결 아이디어

- **변수에 대한 "비례성(proportion)"만 유지**하도록 설계

  - 즉, `v·l(x)` (비례 구조)는 안전
  - 하지만 `l(x) + u(x)` (선형 결합)는 pairing 단계에서 검증 불가 → 금지

#### 🧠 해석

- pairing 검증 시:

  $$
  e(g^{l(s)}, g^{α}) = e(g^{α·l(s)}, g)
  $$

  - → Prover가 l(s)를 조작하면 pairing이 불일치 발생 → 검출 가능

- 따라서 **비례성 구조로만 설계하고 독립성 보장**이 필수

---

### **4.6: Single vs Multi-Variable Polynomials**

#### 🔍 핵심 문제

- 다항식이 **하나의 변수만 반영**할 경우와 **여러 변수 반영**할 경우 각각 처리 방법이 달라야 함
- → 이를 구분해서 설계해야 ZK 보장 유지

---

### **4.6.1: Single-Variable Operand Polynomial**

#### 🔍 문제

- l(x)가 하나의 변수 `a`만 반영할 때:

  - 모든 연산 위치 x=1,2,3,...에서 **동일한 a 값**이어야 함
  - 하지만 prover가 x 위치별로 다른 a값 넣으면 **부정확한 증명 가능**

#### ✅ 해결 아이디어

- pairing 검증 시 **g^{l(s)}와 g^{α·l(s)}를 함께 검증**하여 일관성 보장

  $$
  e(g^{l(s)}, g^{α}) = e(g^{α·l(s)}, g)
  $$

  → 만약 위치별로 다른 a 사용 시 pairing 불일치 발생 → 검출 가능

#### 🧠 해석

- Prover는 **하나의 global a 값**으로만 증명 가능
  → Single-variable case에서는 **전 위치에서 동일한 변수값 사용 강제**

---

### **4.6.2: Multi-Variable Operand Polynomial**

#### 🔍 문제

- 서로 다른 변수(a, d 등)가 사용될 때:

  - x=1,2에서는 `a`만 사용
  - x=3에서는 `d`만 사용
    → 이런 구조를 안전하게 설계해야 함

#### ✅ 해결 아이디어

- **변수별 "선택 다항식(selection polynomial)" 정의**

  - l_a(x): x=1,2에서 1, 나머지에서 0
  - l_d(x): x=3에서 1, 나머지에서 0

- 최종 다항식은:

  $$
  l(x) = a·l_a(x) + d·l_d(x)
  $$

#### 🧠 해석

- → 각 변수는 \*\*명확한 위치(x)\*\*에서만 활성화됨
- Prover는 위치별로 올바른 변수값 넣어야 pairing 성립
  → **변수 독립성 유지 + ZK 성질 유지**

---

### **4.7: Construction Properties**

#### 🔍 핵심 문제

- 이제 QAP로 여러 연산을 자유롭게 표현하는 것은 가능해짐
- 하지만 **구조적으로 어떤 연산들이 어떻게 표현되고 어떤 제약이 붙는지 명확하게 정리**할 필요가 있음

→ 이 Section에서는 다양한 연산들이 어떻게 다항식 구조(QAP)에서 표현되고, 어떤 특징이 생기는지 설명

---

### **4.7.1: Constant Coefficients**

#### 🔍 문제

- 기존에 **`l(x)` = ∑ c\_{l,i} · v_i** 구조에서는 \*\*선택 다항식(l_a(x))\*\*의 값은 0 또는 1이었음
- → 특정 x에서 해당 변수를 "활성화" 할지 여부만 결정

#### ✅ 새로운 관찰: 상수 계수도 넣을 수 있다

- 사실 선택 다항식에 **1이 아닌 다른 값도 넣을 수 있음** (심지어 음수도 가능)
- 왜냐면 **다항식 보간법(interpolation)** 으로 어떤 값이든 만들 수 있기 때문
- 예: `la(x)`가 어떤 위치에서 3이 되게 하거나 -1이 되게 해도 QAP 구조는 그대로 유지됨

#### 🧠 해석

- 기존에는 "이 변수가 쓰이는지 안 쓰이는지 (0/1)"만 표현했지만,
- 이제는 \*\*"이 변수가 얼마나 가중되서 쓰이는지"\*\*도 선택 다항식에 encode할 수 있음
- 즉, `l(x)`는:

  $$
  l(x) = 3·a·l_a(x) + (-2)·b·l_b(x) + \dots
  $$

  처럼 표현 가능 → 더 복잡한 연산도 대응 가능

---

### **4.7.2: Addition for Free**

#### 🔍 문제

- QAP 기본 구조는 `l(x)·r(x) = o(x)` → **곱셈 제약 기반**임
- 그렇다면 그냥 `a + b` 같은 덧셈은 어떻게 표현하나?

#### ✅ 해결 아이디어

- 덧셈도 **곱셈 형태로 우회 표현 가능**:

  $$
  (a + b) × 1 = r
  $$

- 이때 오른쪽 operand는 `1`이라는 상수로 구성해야 함
- 그런데 **QAP에서는 모든 operand는 c·v 형태**여야 해서, 1도 `1·v_one`으로 표현
- 따라서:

  - `c_{r,one} = 1` (계수는 고정)
  - `v_one`이라는 변수를 추가 → 별도 제약으로 `v_one = 1` 강제해야 함 (4.10에서 설명 예정)

#### 🧠 해석

- 덧셈은 실제로는 QAP 구조에서는 "공짜로 들어가는 연산"처럼 취급됨
- 왜냐면 `1`이라는 상수로 우회해서 넣으면 pairing 검증도 동일하게 작동
- 하지만 상수를 쓸 때는 **항상 `c·v` 형태 유지**가 필요하므로 `v_one` 변수 추가 필요

#### ✅ Q1. 덧셈이 QAP 구조에 들어가는데 곱셈과 똑같은 비용이 드는 것 아냐?

**zk-SNARK에서 "비용"의 의미는 "Multiplication Gate 개수" 기준으로 측정**돼요.

- **Multiplication Gate** = "실제로 r(x)가 1이 아닌 **비변수**일 때 유의미한 곱셈"일 때만 카운트.
- `(a + b) × 1 = r`처럼 오른쪽이 상수 1인 경우 → **선형 constraint**로만 인식됨.

  - 이 경우에는 **R1CS → QAP 변환에서 "linear gate"로 빠지고 multiplication gate 카운트 X.**

---

### **4.7.3: Addition, Subtraction and Division**

#### 🔍 핵심 문제

- 이제 더 다양한 연산들 — **덧셈, 뺄셈, 나눗셈** — 을 QAP 구조로 어떻게 표현하는지 살펴봄
- 포인트는: **연산을 "하는 것"이 아니라 "그 결과가 맞는지 검증"만 한다는 것**!

#### ✅ 표현 방법

| 연산               | QAP 내 표현 방식                                  |
| ------------------ | ------------------------------------------------- |
| 덧셈 `a + b = r`   | `(a + b) × 1 = r`                                 |
| 뺄셈 `a - b = r`   | `(a + (-b)) × 1 = r`                              |
| 나눗셈 `a / b = r` | `b × r = a` → QAP 기본 곱셈 구조 그대로 사용 가능 |

#### 🧠 해석

- 중요한 것은: QAP에서는 **계산을 수행하지 않고 관계를 검증**한다는 점

  - 증명자는 `a, b, r` 값을 이미 알고 있어야 하고
  - 회로는 **이 값들이 제약을 만족하는지만 검증**함

#### ✅ 나눗셈 왜 b·r=a로 쓰는가?

- `a / b = r` 은 "r이 정말 a / b인지" 증명하는 것이 목적
- 곱셈으로 바꾸면: `b × r = a` → 이게 성립하는지만 확인하면 됨
- → 기존 QAP 곱셈 제약 구조 그대로 사용 가능

#### ✅ 뺄셈은 왜 그냥 a + (-b)로?

- 뺄셈은 덧셈과 같은 구조로 처리 가능

  - `a - b = r` → `a + (-b) = r`
  - 그러므로 `(a + (-b)) × 1 = r`로 표현 가능

- 역시 `v_one = 1` 제약 필요

##### 📌 연산 정리 표

| 연산               | QAP 표현식           | 추가 제약 필요 여부               |
| ------------------ | -------------------- | --------------------------------- |
| 덧셈 `a + b = r`   | `(a + b) × 1 = r`    | `v_one = 1` 필요                  |
| 뺄셈 `a - b = r`   | `(a + (-b)) × 1 = r` | `v_one = 1` 필요                  |
| 나눗셈 `a / b = r` | `b × r = a`          | 없음 (기존 곱셈 구조 그대로 사용) |

---

### **4.8: Example Computation**

#### 🔍 핵심 문제

- 지금까지 다룬 연산 모델을 실제 함수 계산에 적용할 수 있는가?
- 논문 초반 예제였던 조건 기반 계산 `f(w, a, b) = w·(a×b) + (1-w)(a + b)`을 다항식 증명으로 표현 가능해야 함

---

#### 📌 목적

- 단순 계산 함수를 QAP 기반 다항식 구조로 변환하고, zk-SNARK 증명 프로토콜을 통해 **정확한 계산 수행을 증명**할 수 있어야 함
- 다항식 구성뿐 아니라 입력값(`a, b, w`)과 중간 계산값(`m, v`)까지 다항식에 적절히 매핑해야 함

---

#### ✅ 해결 구조 & 아이디어

1. **원래 함수 변환**

   ```math
   f(w, a, b) = w·(a×b) + (1-w)·(a + b) = v
   ```

   - Multiplication이 3번이므로 연산 과잉 ⇒ 식 변형:

     ```math
     w·(a·b − a − b) + a + b = v
     ⇒ w·(a·b − a − b) = v − a − b
     ```

2. **연산을 연산 단위로 분해**

   - 연산 1: `a × b = m`
   - 연산 2: `w × (m − a − b) = v − a − b`
   - 연산 3: `w × w = w` (w가 0 또는 1인지 체크하는 constraint)

3. **변수 정의 및 분해**

   - 입력: `a, b, w`
   - 중간값: `m, v`
   - 총 5개 변수 → 각각 다항식으로 매핑: `la(x), lw(x), rm(x), ...`

4. **다항식 구성 예시** (각 x = 연산 위치, 1\~3)

   ```text
   la(1)=1, la(2)=0, la(3)=0
   lw(1)=0, lw(2)=1, lw(3)=1
   ...
   ```

5. **최종 L(x), R(x), O(x) 구성**

   ```math
   L(x) = a·la(x) + w·lw(x)
   R(x) = m·rm(x) + a·ra(x) + b·rb(x) + w·rw(x)
   O(x) = m·om(x) + v·ov(x) + a·oa(x) + b·ob(x) + w·ow(x)
   ```

6. **t(x) 구성 및 검증**

   - 연산 위치가 x = 1, 2, 3 → `t(x) = (x-1)(x-2)(x-3)`
   - 증명 식:

     ```math
     L(x)·R(x) - O(x) = t(x)·h(x)
     ```

   - `h(x)`는 `l(x)·r(x) - o(x)`를 `t(x)`로 나눈 몫
     ⇒ 이때 나머지가 없어야 연산이 올바르게 표현된 것s

---

#### 🧠 해석 (논문 예제의 계산 흐름 재해석)

| 단계                  | 의미                                                                           |
| --------------------- | ------------------------------------------------------------------------------ |
| **입력 설정**         | 예: `a=3`, `b=2`, `w=1`                                                        |
| **중간 변수 계산**    | `m = a×b = 6`, `v = w(m−a−b)+a+b = 6`                                          |
| **다항식 구성**       | 각 변수마다 위치별 다항식 정의 후, 계수 곱해서 `L(x), R(x), O(x)` 구성         |
| **검증 식 만족 확인** | `L(x)·R(x) - O(x)`가 `t(x)`로 나누어 떨어지면, **연산이 정확히 실행됨**을 증명 |

> 이 구조를 통해 단순한 함수도 zk-SNARK로 증명 가능함을 보여주며, 이제 이론적으로 준비된 구조를 실제 프로그램 계산에 적용할 수 있음.

---

### ✅ 마무리 체크

- 다음으로 넘어갈 Section은 4.9 Verifiable Computation Protocol
- 이 단계부터 **암호화와 pairing이 실제로 어떻게 결합되는지**, **Proof와 Verification의 구조**를 본격적으로 다룸

# 📘 α shift 구조 발전 핵심 개념

$$
e(g^{L(s)}, g^{\alpha}) \overset{?}{=} e(g^{\alpha \cdot L(s)}, g)
$$

## 🎯 α shift 도입의 필요성

- 우리는 **Prover가 g^{L(s)}, g^{R(s)}, g^{O(s)} 를 "CRS 기반(g^{s^i})으로 정직하게 구성"했는지 확인하고 싶다.**

  - ex. Prover가 g^{L'(s)}를 임의로 조작해서 pairing만 pass시키는 것을 방지하고 싶음.
  - ex. Prover가 s'를 임의로 사용하는 것도 방지해야 함.

→ 이를 위해 **α shift 사용 → pairing 기반 consistency check 적용**.

---

### QAP 구조에서 무엇을 하고 싶었는가?

- 왜 필요했나?

  - Prover가 L(x), R(x), O(x)를 **CRS 기반으로 정직하게 구성했는지** 확인하고자 함.
  - CRS = {g^{s^0}, g^{s^1}, g^{s^2}, ...} 제공 → s값 고정됨.
  - 하지만 Prover가 L(x)를 어떤 임의 구조로 구성할 수도 있음 → α shift로 consistency check 필요.

---

## 💡 α shift란?

**α는 Trusted Setup에서 선택된 secret scalar → Prover는 α를 모름.**

→ Trusted Setup 제공:

$$
\{g^{s^0}, g^{s^1}, \dots\}, \quad \{g^{\alpha \cdot s^0}, g^{\alpha \cdot s^1}, \dots\}
$$

### 핵심 목표

- Prover가 g^{L(s)} 를 제출하면 → Verifier는 g^{\alpha \cdot L(s)} 제출도 요구.
- Verifier는 pairing으로 아래 관계 확인:

$$
e(g^{L(s)}, g^{\alpha}) \overset{?}{=} e(g^{\alpha \cdot L(s)}, g)
$$

→ 그러면 Prover는 **g^{s^i} 기반으로만 g^{L(s)} 를 만들 수 있음** (임의 조작 방지).

---

## ✅ 초기 α shift의 역할 (4.3 \~ 4.6 구간)

### 목적

| 역할                               | 설명                                                                         |
| ---------------------------------- | ---------------------------------------------------------------------------- |
| CRS 기반 구성 강제                 | Prover가 g^{L(s)}, g^{R(s)}, g^{O(s)} 를 반드시 CRS 기반으로 구성하도록 유도 |
| 임의의 s' 사용 불가                | g^{s^i} 만 제공 → s 값은 고정                                                |
| pairing으로 consistency check 가능 | e(g^{L(s)}, g^{\alpha}) vs e(g^{\alpha \cdot L(s)}, g) pairing check 적용    |

### 한계

- L(x), R(x), O(x) 의 **semantic role 구분까지 enforce하지는 못함** → operand swapping 가능.
- L(x), R(x), O(x)를 "다른 프로그램 구조에서 가져와서" 사용 가능 → cross-program attack 가능성 존재.

---

## 🚀 α shift → αₗ, αᵣ, αₒ 구조 발전 (4.9.1)

### 발전 이유

- 초기 α shift만으로는 Prover가:

  - L(x), R(x), O(x) 자체는 다른 프로그램에서 가져와서 구성 가능.
  - 내부적으로 Lᵢ(x), Rⱼ(x), Oₖ(x) 를 서로 섞어서 구성 가능 → operand role 깨짐.

### 개선 → operand별 α 적용:

- Trusted Setup에서:

$$
\{g^{\alpha_\ell \cdot lᵢ(s)}\}, \quad \{g^{\alpha_r \cdot rᵢ(s)}\}, \quad \{g^{\alpha_o \cdot oᵢ(s)}\}
$$

- Verifier는 pairing에서 아래를 개별적으로 체크:

```math
e(g^{L(s)}, g^{\alpha_\ell}) \overset{?}{=} e(g^{\alpha_\ell \cdot L(s)}, g)
```

```math
e(g^{R(s)}, g^{\alpha_r}) \overset{?}{=} e(g^{\alpha_r \cdot R(s)}, g)
```

```math
e(g^{O(s)}, g^{\alpha_o}) \overset{?}{=} e(g^{\alpha_o \cdot O(s)}, g)
```

---

## ✅ 최종 정리표

| 단계                     | α shift 구성                  | 보호하는 위협                                                     | 남은 취약점 (왜 발전 필요?) |
| ------------------------ | ----------------------------- | ----------------------------------------------------------------- | --------------------------- |
| 초기 α shift             | α 하나 사용                   | Prover가 L(x), R(x), O(x)를 CRS 기반으로 정직하게 구성했는지 확인 | operand role swapping 가능  |
| αₗ, αᵣ, αₒ shift (4.9.1) | operand별 α 사용 (αₗ, αᵣ, αₒ) | Prover가 L(x), R(x), O(x) 각각의 semantic role까지 강제           | 매우 강한 protection 확보   |

---

### 🧩 한눈에 보는 발전 흐름

```plaintext
초기 α shift
|
V
L(x), R(x), O(x)가 CRS 기반으로 구성되었는가? (pairing으로 check)
|
V  (한계 발견 → operand swapping 가능)
|
αₗ, αᵣ, αₒ shift 도입 (4.9.1)
|
V
각 operand (L, R, O)의 semantic role까지 고정 enforce → cross-program + cross-operand attack 방지
```

---

### 최종 요약

> **초기 α shift는 CRS 기반 구성 확인용 consistency check → αₗ, αᵣ, αₒ shift는 operand 고유성까지 보호.**
> → **4.9.1 구조 발전은 pairing 검증의 semantic completeness 확보 과정이다.**

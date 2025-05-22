# 이더리움 지갑(wallet) 개요

이더리움에서 **지갑(Wallet)**은 여러 의미를 가질 수 있지만, 일반적으로 사용자가 이더리움 네트워크와 상호작용하는 소프트웨어 애플리케이션을 의미합니다.

지갑은 개인 키를 관리하고, 주소를 생성하며, 잔액을 추적하고, 거래를 생성 및 서명하는 역할을 합니다. 일부 지갑은 **ERC20 토큰 및 스마트 컨트랙트**와도 상호작용할 수 있습니다.

**Ex. ERC20 토큰 및 스마트 컨트랙트와 상호작용할 수 있는 지갑(각 특징과 지원 범위가 다름)**

- **DApp 연동이 쉬운 지갑** → MetaMask, Trust Wallet
- **스마트 컨트랙트 실행이 강력한 지갑** → MyEtherWallet, MyCrypto
- **하드웨어 보안이 필요한 경우** → Ledger, Trezor
- **모바일 기반 편리함** → Trust Wallet, Klip

### **💡 중요한 개념**

- 이더리움 지갑에는 실제 **이더(ETH)나 토큰이 저장되지 않음**.
  → 모든 자산은 **블록체인**에 기록되며, 지갑은 **개인 키**를 보관하는 도구일 뿐.
- 지갑을 사용하면 **소유권 증명 및 거래 서명**이 가능하며, 다른 지갑으로 쉽게 이전 가능.

## **이더리움 지갑의 유형**

지갑은 **키(개인 키) 관리 방식**에 따라 두 가지 유형으로 나뉩니다.

### **1. 비결정론적 지갑 (Nondeterministic Wallet, JBOK)**

### **✅ JBOK(Just a Bunch of Keys)** 방식:

→ 각각의 키가 **무작위(random)**로 생성되며 서로 관계가 없음.

- 단점: 새로운 주소를 만들 때마다 별도의 **백업 필요**, 관리 어려움.
- 현재는 잘 사용되지 않으며, 대신 **HD 지갑**이 선호됨.

### **📌 Keystore 파일(JSON)**

- 비결정론적 방식에서 가장 많이 사용된 방식 중 하나.
- 개인 키를 **AES-128 암호화** 후 JSON 파일로 저장.
- 추가 보안: **KDF(키 유도 함수)** 적용 → 비밀번호 해킹 공격 방어.

---

### **2. 결정론적 지갑 (Deterministic Wallet)**

- **모든 키를 하나의 마스터 키(Seed)에서 파생**시킴.
- 단 하나의 **Seed만 백업하면 모든 키 복구 가능** → 관리 용이.
- 현재 **대부분의 지갑이 결정론적(HD) 방식 사용**.

### **✅ HD 지갑 (Hierarchical Deterministic Wallet, BIP-32)**

- **BIP-32 표준**에 따라 트리 구조로 키를 생성하는 방식.
- 같은 Seed에서 다수의 키를 생성하여 여러 주소를 관리할 수 있음.
- 지갑을 계층적으로 구성하여 **개인/회사/부서별 계정 분리** 가능.

### **📌 HD 지갑의 장점**

1. **백업이 쉬움** → 단 하나의 Seed만 저장하면 모든 키 복구 가능.
2. **새로운 주소 생성 가능** → 개인 정보 보호 강화.
3. **하위 키(public key)만으로 입금 가능** → 해킹 위험 감소.

## **HD 지갑 구조 (BIP-44)**

- **BIP-44는 BIP-32를 기반으로 다중 코인 및 다중 계정 지원**.
- 트리 구조를 이용하여 여러 개의 코인을 관리 가능.

**HD 지갑 주소 체계 예시:**

```plain text
pgsql
복사편집
m / purpose' / coin_type' / account' / change / address_index
```

예제:

- **m/44'/60'/0'/0/0** → 첫 번째 Ethereum 계정의 첫 번째 주소.
- **m/44'/60'/1'/0/0** → 두 번째 Ethereum 계정의 첫 번째 주소.

### **📌 주요 파라미터**

- `purpose'`: **44'**로 고정 (BIP-44 표준 사용).
- `coin_type'`: **60'** (Ethereum), **0'** (Bitcoin).
- `account'`: 사용자의 개별 계정 구분.
- `change`: 0은 입금용 주소, 1은 잔돈(change) 주소 (Ethereum에서는 항상 0).
- `address_index`: 순차적으로 생성되는 주소 인덱스.

### **니모닉(Mnemonic) 코드 단어(BIP-39)**

결정적 지갑을 유도하는 시드로 사용되는 난수를 인코딩하는 워드 시퀀스

**1. Mnemonic 단어 생성**

니모닉 단어는 BIP-39에 정의된 표준화된 프로세스를 사용하여 지갑에서 자동으로 생성됩니다. 지갑은 엔트로피 소스에서 시작하여 체크섬을 추가한 다음 엔트로피를 단어 목록에 매핑합니다.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c2ba559c-cb6d-4c61-bec3-1760fafc9a92/006a8121-ba79-47e5-b726-4e8ae2c868c6/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667CR47CBJ%2F20250521%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250521T215848Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEA4aCXVzLXdlc3QtMiJGMEQCIBgVA9MBtvdBuxqn1DRPIBussNYVh7Gq0ABZAWSBi3KHAiAlY34d0bXN%2Bpy26ZSqq6aWeACPAPsh%2BDYUt813NklneCqIBAjG%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMPb4sKve7oml8TmAUKtwDsmv5OnL3zgdOZWrQc2LyAs7LjRmYx6QXFOCExRgkPCbqEpiLHZYQ%2BcPzq8Nbunu48XP3eDNgYXle02fe%2Bug841OadDAIZRzPW7jJ04vThh%2BPbocXeCkMN2q0Ei1fzaQ2Hy%2BS9QRTr1Vtk3QmhdL%2FzRszNy87AyHc46Dc99tPkag6fefdyTLoaOcZDh%2BBjpqAPwJSeZ6SYWU1BlWpNI2ThTL4CO%2BoG%2BbGCJQ%2F2mXQksASTzFFepSzSiKHoS3KzABYtjDwiXQFQruHIT0zDKkv9O5ABMujXhKB8kzSysb5kkxOrepA4XUmgHvUljbhf2YHxhHcTcsxU1BnwApCZoHEtQY%2BfWc23%2BspSvGlVXqeTHaW9IZfoXH2UYYYSiVft0Qa2iwIPWHQPeGaRbf4dMm4wnNM6gAeywT%2BmbfO5jLLDSXFm%2FP7O3gRkA5gTeRkx0etFpnOlVBbyi3Jxk5U%2BrtH0pKsykuS3Dr1ccbHVnD3cTuNBHXHQcq9Wa%2Bg%2BSOqK8rwU3r304kT55r%2B2sIe2TQxmKxOfEHftjsqXR8F2QWiJNZ5ydUEpvAOcWIql1PHmGCW01eRkwGfH6D3V9N23M21lXRVQ7wVhYxVtgbHWEMe97p%2FkDzN86Ap%2FvK36FowzIa5wQY6pgEdISU4lNECWTL3bCsDcy3UxNL7Jv4WEfJ4n3DsZDnAW71xvoshZcRh8LI%2BhbmT%2F5xgUpZ1CRgZD3agZ55ZAUmaVTmRN6NDGCGtQncteSq4%2F0q%2F8D2nfrbQMcfzmnVWkQjQaTyPO0GIgX70fCrTt3VUqDZT6H4hbjn4s%2Fzp0mrm8FDPQ80PSY%2BYVkHPszajY94QJh3vj4P2%2Bm1YbKYJD85BR%2Be7Rhq5&X-Amz-Signature=68deafb9fb04c7f01398764cde3d48c02f146e06e2bc434c348a5f3d984e2b94&X-Amz-SignedHeaders=host&x-id=GetObject)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c2ba559c-cb6d-4c61-bec3-1760fafc9a92/30b010c8-c4d7-4f39-8916-cfa321e5bf39/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665QEVP3H3%2F20250521%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250521T215849Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEA4aCXVzLXdlc3QtMiJIMEYCIQC4hJhswgMnu3RL%2F%2FlRcjj%2FpwYi3XmtHjwo69XC1rfruQIhAKaw14yLzeqtyirgeIIJ%2Bd0ynDGc2A6AMxMSBFIE6xicKogECMf%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igyoyd%2Fp%2FLbVXk36E10q3APxynshs7fUiEbtCR19YmlUbC8oX2PVyMZQD%2FGPc0lI4wcxJK6KvR7J0LSxUY5yCLIvl92o9mShWeYGHsKRl0b1jp1VHaFXxx8rs7Urt3Zfj3fmnl7qKg2GUdSds3A%2B0nPqh0yYLw%2FIE2y0AJO9J8XxNmHeVwZJIRDG3w0t4wtT9264FP1Lpm32BSAyj3paXhtmDbILa964euFVvPDzqEYVo0qyFuIWcWfFddHF%2FyibTIQl71LB3jTYuoX6VNUGheH8VUK6JFroyJvo1ss9uk1e42iaFgWNWTrbt32g5R91FcbI78%2BIgBSVEMFjp2%2FfeuCFPNeRAoe2WBr1mC1bt9VOKr5k5%2BMCoEeBzlMVAcWGoKtPn8ijyZGdKldsoA%2BMtaM3ydKtoAMrRHY0wIQuXsINl6Q8cOk%2FmKJjZbFbq5tal%2F2Q35DP2Y8mjx9%2BpRhdCSr8HEgKPQOYHZj1SNGpxygwltN4x6GdbMY80z0hzaC3PPrlM6Waps8Q5j1BnCrFlsYgGx4nSTWIlXysaB64nhyx5J3AlJzV05kOmdoZqMF%2FNA5Zj8DMuJa278geDpQivBVaj8mW%2BpREMtUYwejLDAJIoRiObeqt7DWgeVxg7PHeiq1038FWVLlbrEretDCGmLnBBjqkAQyQKNRtOdvcPqjCkJrbYu%2FptAeC3L5QcXn9BJuoI3jjpoZFDnkg%2FV94M8ROcb2DwbphsXqqiY%2BkpvTQWJdeMnecxFW9n0O34Zy1cZCyG9P%2BP7LlnrCf4L8M%2FDC4K%2B6RUGiipH6ZXL8jarPpMNaWy2SzRKhNkIp33YAjrxbxHwig66thrXWHkaUYThohS49eDLKlkBnTA0gwK9wSZBRUkfwAShHN&X-Amz-Signature=3806e21f31cfa032a617c1dee9c9fc7082dfc2032fdc4492a9f52fcf5aa88a4c&X-Amz-SignedHeaders=host&x-id=GetObject)

1. 128~256비트의 암호화된 난수 시퀀스 S를 생성합니다.
2. S의 SHA-256 해시 값의 첫 번째 길이 ÷ S의 32비트를 구하여 S의 체크섬을 생성합니다.
3. 무작위 시퀀스 S의 끝에 체크섬을 추가합니다.
4. 시퀀스-체크섬 연결을 11비트 섹션으로 나눕니다.
5. 각 11비트 값을 2,048개 단어의 사전 정의된 사전에서 단어로 매핑합니다.
6. 단어의 순서를 유지하면서 단어 시퀀스에서 니모닉 코드를 만듭니다.

**2. Mnemonic ⇒ Seed**

니모닉 단어는 128~256비트 길이의 엔트로피를 나타냅니다. 그런 다음 엔트로피를 사용하여 키 스트레칭 함수 PBKDF2를 사용하여 더 긴(512비트) 시드를 도출합니다. 생성된 시드는 결정적 지갑을 빌드하고 키를 도출하는 데 사용됩니다.

키 스트레칭 함수는 **니모닉**과 **_솔트_** 라는 두 가지 매개변수를 사용합니다 .

**- Salt의 목적**

무차별 대입 공격을 가능하게 하는 조회 테이블을 만드는 것을 어렵게 만드는 것.

시드를 보호하는 추가 보안 요소 역할을 하는 패스프레이즈 도입을 가능하게 해주는 것

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c2ba559c-cb6d-4c61-bec3-1760fafc9a92/61d2e987-6bb1-4ab6-8a5f-be44b0b23c24/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662CMHEVGR%2F20250521%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250521T215848Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEA4aCXVzLXdlc3QtMiJHMEUCIBpggiiC5GluA%2Fkwwg%2B%2Fh%2B%2F%2FA01XB1oYX4PM7Q%2Fnty9AAiEA%2B7tmNijh4mgIIZ3LjGfUp3t1nsV4H47jX5KY8VlJqUcqiAQIxv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDKwipd2A%2F%2BBdODdErircA%2F7R3rl%2BFsjGsp152aj4mgFhCOAGali8TC%2FsXS%2BMD%2FkAkfiZscsIQRBXOwyL6ArcKnGsN3I4apk6r6br2%2BwjB93tulHHnytFi4mQdrf3A0kPen8Ql%2B88zdnS8r8f5RTLQUP3GS2uR%2FbGJ78%2FFLB3hVYtXgTacu7lhDcD%2F3o00mJ4%2BB%2BgTyVxgHDij0qAjUoDuypMWqtwWTcv0TwHHaCc%2Fptl1EQDcgerlGuGDiSSklInM%2FlOtgWAdWvcWC8b2ljvMaWV3H1GvBrAYLfvQK3OMjaaQumtj3JxqhA7WAqq6OOoF%2BXRHfvidAp2e%2F4rAZxcTiIkoqW04s0jr81AloUtFphr1YVYdFfLg2eeqQztX3jxffjqwHcmu5IrZl36tjtyRHNhFBr2EknMUTeWh8a%2FqNOfR7jorLWrC%2Fc23TG5KRc60rPYQ8M6KJC6gSSzrqAiE931stvTYC8%2Bic74PXgSAAr5e9cUv5neuSIckoCbS1YdbpNHdJ7tY6qzDb2ISED1OFOzV8dcQy0dpkL6yiCqcDwZwrzH2QBJl1ucR8MERmViTRhvFzuB%2FHU0rPcSo9FfAFr%2B9vadj0ZpFGX3ek%2F77v9icjBGO%2BKIgGmKS%2BpWiYNrpWW0zmLvKkrFXzVvMOKGucEGOqUB4R78kRGHO3bFaeWgSUK1lw3xZB9spTty5OOot8L%2F4OezKc8DWRawl6J6rTov%2BtqVdz0C05FzWPwXNPuE%2BKzpoGgGumCYJ%2FOX70Qu90h%2Fy46Nc7eX7O1lFyMFat9BAGOZYMRnnKXV3CzDYhYgmOr56ya0P%2B6jB%2FqGbIyYMTnGmKblofCq0r3Vx3ReWzq6LP964hBYRMANl1aXijpt%2FKUJYcEeSiGL&X-Amz-Signature=dcaa672c549033c130151879eaef05475da134f7f5df2d4726b18bf39fdf2036&X-Amz-SignedHeaders=host&x-id=GetObject)

**-이전 섹션에서 설명한 프로세스 이어서**

7. PBKDF2 키 스트레칭 함수의 첫 번째 매개변수는 6단계에서 생성된 *니모닉 입니다.*
8. PBKDF2 키 스트레칭 함수의 두 번째 매개변수는 *salt* 입니다 . salt는 문자열 상수 "mnemonic"과 사용자가 제공한 선택적 암호문구로 연결된 것으로 구성됩니다.
9. PBKDF2는 HMAC-SHA512 알고리즘을 사용하여 2,048라운드의 해싱을 사용하여 니모닉과 솔트 매개변수를 확장하여 최종 출력으로 512비트 값을 생성합니다. 이 512비트 값이 시드입니다.

## **확장 키(Extended Keys)**

- **확장 공개 키(xpub)**: 공개 키에서 파생된 모든 주소를 생성 가능.
- **확장 개인 키(xprv)**: 전체 지갑의 개인 키를 관리.
- **xpub을 서버에 저장하면 해킹당해도 자금 이동 불가능** (단, 거래 기록은 노출됨).

### **📌 xpub vs xprv 비교 정리**

|                  | **확장 공개 키 (xpub)**                                  | **확장 개인 키 (xprv)**                         |
| ---------------- | -------------------------------------------------------- | ----------------------------------------------- |
| **역할**         | 여러 개의 공개 주소(계좌번호) 생성 가능                  | 모든 개인 키 관리 및 서명                       |
| **비유**         | 은행의 "계좌번호 발급 시스템"                            | 계좌에서 돈을 인출할 수 있는 "마스터 PIN 번호"  |
| **저장 위치**    | 온라인 서버에 저장 가능 ✅                               | 절대 온라인에 저장하면 안 됨 ❌ (오프라인 백업) |
| **해킹 시 영향** | 해킹당하면 거래 내역이 노출되지만, 돈을 빼앗길 수는 없음 | 해킹당하면 자금이 모두 탈취될 수 있음           |

---

## **📌 지갑 보안 및 베스트 프랙티스**

- **업계 표준(BIP-32, BIP-39, BIP-44)을 따르는 지갑 사용**.
- **니모닉을 백업하고 안전한 장소에 보관** (전자적 저장 X).
- **하드웨어 지갑(Ledger, Trezor) 사용 권장**.
- **xpub을 이용한 안전한 거래 주소 생성 가능**.

---

## **✅ 결론**

1. **지갑은 개인 키를 관리하는 도구이며, 실제 이더는 블록체인에 저장됨.**
2. **HD 지갑(BIP-32/BIP-44)은 관리와 보안 측면에서 필수적**.
3. **니모닉 코드(BIP-39)는 가장 안전한 백업 방법**.
4. **확장 키(xpub, xprv)를 활용하면 보안성을 높일 수 있음**.
5. **Passphrase 사용으로 추가적인 보안 계층 추가 가능**.

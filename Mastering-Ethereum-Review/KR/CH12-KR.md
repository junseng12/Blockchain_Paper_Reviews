## **📌 1. DApp(분산형 애플리케이션) 개념 정리**

### **🔹 DApp이란?**

- DApp은 **탈중앙화된 애플리케이션**으로, 중앙 서버 없이 **블록체인**과 **P2P 네트워크**를 통해 운영됩니다.
- 전통적인 애플리케이션은 중앙화된 서버에서 데이터를 처리하고 저장하는 방식인 반면, DApp은 **스마트 계약**을 통해 **탈중앙화된 방식으로** 애플리케이션 로직을 처리합니다.
- **스마트 계약**은 **블록체인상에 배포**되고 **변경할 수 없으며**, **탈중앙화된 방식**으로 처리됩니다.

📌 **비유:**

DApp은 **레스토랑**과 같아요. 전통적인 애플리케이션은 **주방장**(서버)이 모든 요리를 준비하지만, DApp은 **자동화된 요리 기계**(스마트 계약)가 모든 음식을 조리하고 제공하는 방식이에요. 고객은 **주문**만 하면, **기계**가 자동으로 요리를 준비하고 제공하죠.

---

## **📌 2. DApp의 핵심 구성 요소**

### **🔹 1) 백엔드(스마트 계약)**

- **스마트 계약**이 **애플리케이션 로직**을 저장하고 관리합니다. 블록체인에 배포되며, **변경 불가능**합니다.
- 스마트 계약은 **가스 비용**이 비싸므로 계산을 최소화해야 합니다. 중요한 것은 **트러스트리스(신뢰 불필요)**와 **탈중앙화된 실행 환경**입니다.

📌 **비유:**

스마트 계약은 **레스토랑의 메뉴판**처럼 작동해요. 메뉴판에 있는 **요리법**(애플리케이션 로직)이 **자동화된 기계**에 의해 처리되고, 그 결과는 **블록체인**에 저장되어 수정할 수 없어요.

---

### **🔹 2) 프론트엔드(웹 사용자 인터페이스)**

- 프론트엔드는 **HTML, CSS, JavaScript** 같은 전통적인 웹 기술로 구축됩니다.
- **MetaMask**와 같은 **웹3 지갑**을 통해 사용자와 블록체인과의 상호작용을 돕습니다.

📌 **비유:**

프론트엔드는 **레스토랑의 홀**이에요. 고객이 메뉴를 보고 주문을 하고, 그 주문을 **기계**(스마트 계약)로 전달하는 역할을 하죠. 사용자는 **MetaMask**라는 **주문서**를 통해 이 기계와 연결되죠.

---

### **🔹 3) 데이터 저장**

- 스마트 계약은 **가스 비용**이 높아서 대량의 데이터를 저장하는 데 적합하지 않습니다.
- 대부분의 DApp은 **IPFS(Inter-Planetary File System)**나 **Swarm** 같은 **분산형 저장소**를 사용하여 **데이터를 외부에 저장**합니다.

📌 **비유:**

스마트 계약은 **요리 기계**로, 요리를 준비할 때 재료를 **저장소**에 두고 가져옵니다. 대량의 재료는 **저장소**(IPFS, Swarm)에 보관하고, 기계는 **필요할 때마다** 필요한 재료만 가져와서 요리를 해요.

---

### **🔹 4) 메시지 통신**

- DApp에서 메시지 통신은 **Whisper** 같은 **P2P 프로토콜**을 사용해 분산된 방식으로 이루어집니다.
- **Whisper**는 DApp 사용자들 간의 안전한 **메시지 교환**을 가능하게 합니다.

📌 **비유:**

메시지 통신은 **레스토랑 직원들 간의 대화**와 같아요. 손님이 주문을 할 때, 모든 대화는 **중앙화된 서버**가 아닌 **직원들 간의 비밀스러운 대화**(Whisper)로 처리돼요.

---

## **📌 3. DApp의 장점**

### **🔹 1) 회복력(Resilience)**

- 스마트 계약은 **블록체인에 배포**되므로 **서버 다운**과 같은 중앙 서버의 문제에 영향을 받지 않습니다.
- **블록체인**은 **탈중앙화**되어 있으므로, 서버가 한 곳에서 다운되더라도 애플리케이션은 계속 운영됩니다.

📌 **비유:**

레스토랑의 **요리 기계**는 **중앙 주방**에 의존하지 않아요. 주방장이 아프거나, 전기가 나가도 **기계**는 계속 작동해요.

---

### **🔹 2) 투명성(Transparency)**

- DApp은 **블록체인 상에서** 모든 트랜잭션을 기록하고, **모든 코드**가 **공개**됩니다.
- 누구나 스마트 계약의 동작을 **검토**할 수 있으며, 그로 인해 **신뢰성**이 높습니다.

📌 **비유:**

레스토랑에서 **요리 기계**가 요리하는 과정은 **투명하게 공개**됩니다. **손님**은 요리가 어떻게 만들어지는지 **모두 알 수** 있습니다.

---

### **🔹 3) 검열 저항성(Censorship Resistance)**

- 블록체인 상에서 실행되는 DApp은 **검열**을 받을 수 없습니다. 스마트 계약의 **코드는 배포 후 변경할 수 없기** 때문에, **중앙화된 권력**이 코드나 운영을 **막을 수 없습니다.**

📌 **비유:**

레스토랑의 **요리 기계**는 **누구의 영향도 받지 않아요**. 만약 어떤 사람이 음식을 못 만들게 하려 해도, **기계**는 **자동으로 작동**하고, **외부의 간섭**은 불가능합니다.

---

## **📌 4. 예시: 경매 DApp 구축**

### **🔹 DApp 예시 - 경매 플랫폼**

이 예시에서는 **ERC721**을 이용한 **토큰화된 자산**(예: 집, 차, 상표)을 **경매**로 판매하는 DApp을 구축합니다.

- **DeedRepository**: 자산을 나타내는 **ERC721 토큰**을 발행하고 관리합니다.
- **AuctionRepository**: 경매를 진행하는 **스마트 계약**입니다.

📌 **비유:**

경매는 **레스토랑의 경매 행사**와 같아요. **손님들**(사용자)은 **서버**(스마트 계약)에 접속하여 **식사를 경매**처럼 **가격을 입찰**합니다. 가장 높은 입찰을 한 **손님**이 **그 요리**(자산)를 가질 수 있죠.

---

## **📌 5. DApp의 보안**

### **🔹 보안 감사 및 취약점 방지**

- DApp은 **블록체인 상에 배포된 스마트 컨트랙트를 사용**하므로 보안이 매우 중요합니다. **취약점**이 발견되면 **상당한 손실**이 발생할 수 있기 때문에, **보안 감사**는 필수입니다.
- 일반적으로 스마트 컨트랙트의 보안 취약점에는 **Reentrancy attack**, **Integer Overflow**, **Access Control** 등이 있습니다. **보안 감사**를 통해 이러한 취약점을 사전에 점검해야 합니다.

📌 **비유:**

DApp의 보안은 **건물**의 **철저한 점검**과 같습니다. 건물을 짓고 나면 **모든 창문과 문이 제대로 잠기고**, **기본 구조가 견고한지** 점검해야 합니다. **보안 감사**는 이러한 점검을 하는 **전문가**와 같습니다.

---

## **📌 6. DApp의 한계와 개선**

### **🔹 DApp의 한계**

- 대부분의 DApp은 아직도 일부 중앙화된 시스템(서버, 데이터베이스 등)을 사용하고 있기 때문에 완전한 탈중앙화가 이루어지지 않았습니다.
- **기술적 한계**로 인해 **모바일 DApp** 개발이 상대적으로 어려운 상황입니다.

📌 **비유:**

레스토랑이 **기계**(스마트 계약)로 요리하는 데는 한계가 있어요. **고객의 주문을 처리하는 직원**(모바일 앱)이 필요하고, 그 직원은 **중앙화된** 방식으로 처리됩니다.

---

### **🔹 DApp의 개선**

- **Swarm**과 **IPFS**와 같은 분산 저장소를 사용해 모든 데이터를 분산시켜 **완전한 탈중앙화**를 실현할 수 있습니다.
- **ENS**(이더리움 이름 서비스)를 사용하여 DApp의 주소를 쉽게 **이해 가능한 이름**으로 바꿀 수 있습니다.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c2ba559c-cb6d-4c61-bec3-1760fafc9a92/973d05dd-b244-48f5-b5a5-d890af8fa230/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665QIMJDI5%2F20250521%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250521T213909Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEA4aCXVzLXdlc3QtMiJHMEUCIHJTt%2BHneNJ%2FAJTIRZoyBZ54grrgzSexqEVEqplW5LJ2AiEAp7BUEYN7%2BNioinPdM%2FwZAT%2FHfFnF9IVKC4fiGMXa4JsqiAQIxv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDFO46DAptCscg%2BifASrcAxXFKxyjh7ZHod%2BGP1CjpJ8HFRvrTDQVF7xFhm%2BfDiPQV4XC2F0DEmYYvc9v5TKOnJoUeKQV%2FjUE3yz3cDBdJ5ZGB0R8dql8zgyjUkIWRd4gSRfkKsgltFrm%2BNWUWlVhj0CzI5HGwlC0Dt2hPyQnsuuuVQCwdIBbIbCgPey9waP7VMTZf%2BenQsfwaJfZ9%2FUilz18xVcg7kzM276zapt7%2BdjgVOfvOnrAenBfEi2g0nJQEF9yQ9L9RGfRoWm0iyg5iQVujGMwpKV8wjRSnzzQE5MHQKj4Wm8adpFD6p1CT4FECa3U4zqbEjyy%2BgD14yHC4%2B08IIId35yAVb0ZjKhdZdX8QLH4q0y0IxujuIgTdxYhomRbML2TNTjI3pUn%2BCdrLTXKPicTUV7zRk3eeAPMe0%2BOYpgCtvUJqeCy1snWaAIo6J0t3BzpN4IsyS05%2Fvv5PSm3AMFnZsquyuE64ZsRVTnTl5HSYim0UsiBDEtuWiTVpza1PnrrYO2Yck2dZUr8Zn4qkU5LxvLTcHdCCV8kJwWT8JOMk7I0xOuafDojGajfKR0XWoiWLfNIz0S9GFuOtmyVaD9%2FYQ6azyGzmSZd6zYkHbpfzz0LezQZ6A3IenHLTagDgE8BJYslNQpNMPiGucEGOqUBbqoKwN11cvgVknxbWz11tGqDLWmlGwjIBYSdJYmOZ2913DfmCXVAIOLyL1QhfNl87kEHUTM5hWWHzTKU8lb0gWcLI0slkPKZ25PXp2FnZh7OnhTvZ3X0qsncb9iOCKNtC%2BYsRpiksMsV9YScJaOT6Q9AKrpQWPPeybD9CttLm1Adc6kw8tQ77%2BQhA9%2FcJf4YFGz8MA6mq%2FhmS2oWVJ81tv2eRxtf&X-Amz-Signature=b29a6cf54633c4b209a24ef7f444851e0b99e4cf5581985b0f35436959d90b30&X-Amz-SignedHeaders=host&x-id=GetObject)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c2ba559c-cb6d-4c61-bec3-1760fafc9a92/afb39e5d-a7a1-4530-8e3b-afd757489c93/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665QIMJDI5%2F20250521%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250521T213909Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEA4aCXVzLXdlc3QtMiJHMEUCIHJTt%2BHneNJ%2FAJTIRZoyBZ54grrgzSexqEVEqplW5LJ2AiEAp7BUEYN7%2BNioinPdM%2FwZAT%2FHfFnF9IVKC4fiGMXa4JsqiAQIxv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDFO46DAptCscg%2BifASrcAxXFKxyjh7ZHod%2BGP1CjpJ8HFRvrTDQVF7xFhm%2BfDiPQV4XC2F0DEmYYvc9v5TKOnJoUeKQV%2FjUE3yz3cDBdJ5ZGB0R8dql8zgyjUkIWRd4gSRfkKsgltFrm%2BNWUWlVhj0CzI5HGwlC0Dt2hPyQnsuuuVQCwdIBbIbCgPey9waP7VMTZf%2BenQsfwaJfZ9%2FUilz18xVcg7kzM276zapt7%2BdjgVOfvOnrAenBfEi2g0nJQEF9yQ9L9RGfRoWm0iyg5iQVujGMwpKV8wjRSnzzQE5MHQKj4Wm8adpFD6p1CT4FECa3U4zqbEjyy%2BgD14yHC4%2B08IIId35yAVb0ZjKhdZdX8QLH4q0y0IxujuIgTdxYhomRbML2TNTjI3pUn%2BCdrLTXKPicTUV7zRk3eeAPMe0%2BOYpgCtvUJqeCy1snWaAIo6J0t3BzpN4IsyS05%2Fvv5PSm3AMFnZsquyuE64ZsRVTnTl5HSYim0UsiBDEtuWiTVpza1PnrrYO2Yck2dZUr8Zn4qkU5LxvLTcHdCCV8kJwWT8JOMk7I0xOuafDojGajfKR0XWoiWLfNIz0S9GFuOtmyVaD9%2FYQ6azyGzmSZd6zYkHbpfzz0LezQZ6A3IenHLTagDgE8BJYslNQpNMPiGucEGOqUBbqoKwN11cvgVknxbWz11tGqDLWmlGwjIBYSdJYmOZ2913DfmCXVAIOLyL1QhfNl87kEHUTM5hWWHzTKU8lb0gWcLI0slkPKZ25PXp2FnZh7OnhTvZ3X0qsncb9iOCKNtC%2BYsRpiksMsV9YScJaOT6Q9AKrpQWPPeybD9CttLm1Adc6kw8tQ77%2BQhA9%2FcJf4YFGz8MA6mq%2FhmS2oWVJ81tv2eRxtf&X-Amz-Signature=52cdf5de4450e4b20b97f29dbeafa6a4760886bf34e7f033585f8e7ff5817265&X-Amz-SignedHeaders=host&x-id=GetObject)

<details>
<summary>**ENS(이더리움 네임 서비스) 구체적인 원리**</summary>

**ENS**는 이더리움 블록체인에서 사용되는 **도메인 이름 시스템(DNS)**에 대한 대안입니다. ENS의 **기본 원리**는 **블록체인** 상에서 **도메인**과 **리소스를 연결**하는 **탈중앙화된 이름 서비스**를 제공하는 것입니다. 간단히 말해서, **ENS는 DNS의 블록체인 버전**입니다.

### **🔹 ENS의 기본 구조**

ENS는 **이더리움 블록체인**을 활용하여 도메인 이름과 다른 리소스를 연결할 수 있게 해줍니다. 예를 들어, `ethereumbook.eth`라는 이름을 이더리움 주소나 특정 리소스에 연결할 수 있습니다.

### **🔹 ENS의 구성 요소**

1. **ENS 루트 노드 (Root Node)**
   - ENS의 **기본 단위**는 **이름**을 **해시**하여 생성된 **노드**(identifier)입니다. `ethereumbook.eth`와 같은 이름은 **이름 해시(Namehash)**를 통해 고유한 노드로 변환됩니다.
2. **이름 해시 (Namehash)**
   - ENS의 이름은 **Namehash**라는 알고리즘을 통해 해시로 변환됩니다. 이 해시 값은 블록체인 상에서 고유한 식별자로 사용됩니다.
   - 예를 들어, `ethereumbook.eth`는 `keccak256` 알고리즘을 사용하여 **고유한 해시** 값으로 변환되며, 이 해시 값은 **노드**로 변환되어 ENS에 저장됩니다.
3. **등록(Registration)**
   - ENS 이름은 **경매 시스템**을 통해 등록됩니다. 이름은 **경매 방식**으로 구매되며, **Vickrey Auction**이라는 방식으로 최고가 입찰자가 도메인을 얻습니다. 이 방식에서는 입찰자가 제시한 **최고가**와 **두 번째 높은 가격**만 공개되고, 최종적으로 **두 번째 가격**만을 지불하게 됩니다.
4. **리졸버(Resolver)**
   - 리졸버는 ENS 이름에 연결된 **실제 데이터**를 반환하는 역할을 합니다. ENS 이름이 블록체인 주소, **Swarm**의 해시, **IPFS** 주소 등과 연결될 수 있도록 돕습니다.
   - 예를 들어, `auction.ethereumbook.eth`라는 서브도메인은 Swarm에 저장된 DApp의 리소스를 **주소로 변환**하여 사용자에게 제공됩니다.
5. **배경 관리 (Governance)**
   - ENS의 이름은 **소유자가 관리**하며, 이름을 갱신하거나 변경할 수 있습니다. ENS에서는 **모든 작업이 탈중앙화**되도록 설정되어 있으며, **중앙 관리자** 없이 **네트워크 참여자**들이 이를 운영합니다.

---

### **📌 ENS 동작 예시**

### **🔹전체 과정 요약**

1. **사용자가 "mydomain.eth"를 경매에 참여하여 등록**.
2. 경매에서 **입찰을 통해 최고가를 제시하고 도메인 이름을 획득**.
3. 도메인 이름을 **Namehash 알고리즘**으로 해시하여 **고유한 식별자** 생성.
4. 생성된 **Namehash 값을 ENS Registry에 저장**.
5. **리졸버**는 이 도메인 이름을 실제 **리소스(예: Swarm 해시 또는 이더리움 주소)**로 변환.
6. 사용자에게 **"mydomain.eth"를 통해 Swarm 또는 이더리움 리소스**에 접근.

---

### **🔹ENS 동작 예시: "mydomain.eth" 등록과 연결**

1. **사용자 도메인 이름 등록 (경매 참여)**

   - 사용자는 **"mydomain.eth"**라는 이름을 등록하고자 합니다. 이 도메인은 경매 시스템을 통해 판매됩니다.
   - ENS는 **Vickrey Auction**이라는 경매 방식을 사용하여 도메인 이름을 판매합니다. 여기서 사용자는 **비공개 입찰**을 통해 가격을 제시하고, **두 번째 높은 가격**을 지불하게 됩니다.

   📌 **비유:**

   경매에서 원하는 물건을 사기 위해 **봉인된 입찰지**를 제출하고, 마지막에 최고가를 기록한 사람에게 판매되지만 실제로 지불하는 금액은 **두 번째 높은 금액**입니다. 이는 비공개 경매에서 참여자의 이익을 보호하는 방식입니다.

2. **이름 해시 (Namehash) 생성**

   - 경매에서 **"mydomain.eth"** 도메인을 획득한 후, ENS 시스템은 **Namehash 알고리즘**을 사용하여 해당 이름을 **해시** 값으로 변환합니다.
     이 해시 값은 **"mydomain.eth"**를 고유한 식별자로 만들어 주며, 블록체인에서 이 이름에 대한 모든 정보를 추적하고 관리할 수 있게 합니다.

   📌 **비유:**

   도메인 이름인 "mydomain.eth"는 **주소록에서 이름을 찾을 수 있는 고유한 번호**로 변환되어, 블록체인 내에서 추적할 수 있는 식별자로 변환됩니다.

3. **ENS Registry에 저장**

   - Namehash로 변환된 **"mydomain.eth"**의 고유한 해시 값은 **ENS Registry**라는 스마트 계약에 저장됩니다.
     ENS Registry는 ENS의 핵심 레지스트리로, 이름을 관리하고 해당 이름이 연결된 리소스(주소, 콘텐츠 등)를 관리합니다.

   📌 **비유:**

   ENS Registry는 **전화번호부**와 같으며, 여기서 각 도메인 이름에 대한 고유한 번호와 관련된 정보를 저장하고 관리합니다.

4. **리졸버(Resolver) 설정**

   - ENS Registry에 등록된 **"mydomain.eth"** 도메인 이름은 **리졸버(Resolver)**와 연결됩니다. 리졸버는 도메인 이름을 실제 리소스 주소로 변환하는 역할을 합니다.
   - 예를 들어, **"mydomain.eth"**가 **Swarm**에 저장된 DApp을 가리킨다면, 리졸버는 해당 DApp의 **Swarm 해시**를 반환합니다. 이를 통해 DApp의 사용자 인터페이스를 쉽게 찾을 수 있습니다.

   📌 **비유:**

   리졸버는 **우체국**에서 주소를 검색하는 사람과 같아서, "mydomain.eth"를 입력하면 **실제 주소**인 Swarm 해시 또는 이더리움 주소를 반환합니다.

5. **Swarm 또는 다른 리소스와 연결**

   - 리졸버가 반환한 정보는 **Swarm**과 같은 분산 스토리지 시스템의 **실제 콘텐츠**(예: DApp의 파일, 이미지 등) 또는 이더리움 주소(예: 스마트 계약 주소)입니다.
   - 예를 들어, **"mydomain.eth"**가 Swarm에 호스팅된 DApp에 연결되면, 이 주소를 통해 사용자는 Swarm에서 DApp의 실제 콘텐츠에 접근할 수 있습니다.

   📌 **비유:**

   "mydomain.eth"를 웹 브라우저에서 입력하면, **주소창에 웹사이트가 나타나는 것처럼** Swarm에 호스팅된 DApp이나 이더리움 주소가 웹사이트로서 나타나게 됩니다.

---

**📌 ENS의 장점**

- **탈중앙화**: ENS는 **블록체인**을 사용하여 도메인 이름을 관리하므로 중앙화된 시스템이 필요 없습니다.
- **유연성**: ENS는 **다양한 리소스**(이더리움 주소, Swarm 해시 등)에 대한 연결을 지원합니다.
- **검열 저항성**: 블록체인 기반이므로 누구도 ENS 시스템을 **검열하거나 제어**할 수 없습니다.

</details>

<details>
<summary>**ENS 내 해시 함수**</summary>

### **1. 해시 함수의 특성**

해시 함수는 **일방향 함수**로, 입력 값에 대해 고유한 출력을 생성하는 것이 일반적인 특성입니다. 즉, **같은 입력에 대해서는 항상 같은 출력을 생성**하지만, **다른 입력에 대해서도 같은 해시값을 가질 수 있는 가능성**이 존재하는 **충돌(collision)**이 이론적으로 발생할 수 있습니다.

### **2. 해시 함수와 ENS에서의 역할**

ENS에서는 해시 함수, 특히 **Namehash**를 사용하여 도메인 이름(예: "ethereumbook.eth")을 **고유한 식별자**로 변환합니다. ENS에서 사용하는 **Namehash**는 여러 단계를 거쳐 **이름을 해시**하고, 그 결과를 **고유한 노드(node)**로 저장하게 됩니다. 이는 **충돌 가능성을 최소화**하도록 설계되어 있습니다.

### **3. 충돌에 대한 걱정은 적은 이유**

ENS에서 사용하는 해시 함수는 **충돌 확률이 매우 낮은 keccak256** 알고리즘입니다. 이 알고리즘은 **암호학적으로 안전**하고 **충돌 가능성을 최소화**하는 방식으로 설계되었습니다. 그래서 다른 입력 값이 같은 해시 값을 생성하는 확률은 매우 낮고, 실제로 발생하기 어렵습니다.

### 📌 **비유:**

Namehash는 마치 **전화번호부에서 각 사람에게 고유한 번호**를 부여하는 것과 같습니다. 비록, 번호가 제한적이라도 **충돌이 일어나지 않도록 충분히 많은 공간을 제공**하여 다른 사람의 번호와 겹칠 확률이 매우 낮도록 보장합니다.

### **4. ENS의 충돌 방지 시스템**

- ENS에서 **Namehash**는 단순한 해시값뿐만 아니라, **각 도메인 이름에 대한 고유한 식별자를 생성**하는 방식으로, 충돌을 최소화합니다.
- ENS의 **경매 시스템**과 **리졸버 시스템**은 **충돌이 발생하지 않도록 설계**되어 있기 때문에, "다른 ENS 이름이 같은 Content를 가리키는 일"은 실제로 발생하지 않도록 조치가 취해집니다.

따라서 **충돌을 방지하고 ENS 시스템이 정상적으로 동작할 수 있도록** 설계되었기 때문에, **각 ENS 도메인은 고유한 콘텐츠**와 연결되며, 동일한 콘텐츠를 가리키는 ENS 이름은 발생하지 않도록 관리됩니다.

### **5. 결론**

- **이론적으로 해시 함수는 충돌 가능성은 있지만, ENS에서는 충돌을 최소화하는 설계와 알고리즘을 사용**하므로, **다른 ENS 도메인이 동일한 콘텐츠를 가리킬 가능성은 매우 낮습니다.**
- **충돌 가능성**을 완전히 배제할 수는 없지만, 실용적인 범위 내에서 ENS는 안전하게 **각 도메인을 고유하게 관리**할 수 있습니다.

따라서 ENS의 **기본 설계는 충분히 안전**하고, 서로 다른 ENS 이름들이 **동일한 콘텐츠를 가리키는 일이 일어나지 않도록 보장**됩니다.

</details>

📌 **비유:**

레스토랑이 **모든 요리 기계**를 **분산된 시스템**(Swarm, IPFS)에서 관리하고, **이름**(ENS)을 쉽게 기억할 수 있는 방식으로 제공합니다.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c2ba559c-cb6d-4c61-bec3-1760fafc9a92/7abfce75-24f0-4b2d-9c63-190c6c1e6c98/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665QIMJDI5%2F20250521%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250521T213909Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEA4aCXVzLXdlc3QtMiJHMEUCIHJTt%2BHneNJ%2FAJTIRZoyBZ54grrgzSexqEVEqplW5LJ2AiEAp7BUEYN7%2BNioinPdM%2FwZAT%2FHfFnF9IVKC4fiGMXa4JsqiAQIxv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDFO46DAptCscg%2BifASrcAxXFKxyjh7ZHod%2BGP1CjpJ8HFRvrTDQVF7xFhm%2BfDiPQV4XC2F0DEmYYvc9v5TKOnJoUeKQV%2FjUE3yz3cDBdJ5ZGB0R8dql8zgyjUkIWRd4gSRfkKsgltFrm%2BNWUWlVhj0CzI5HGwlC0Dt2hPyQnsuuuVQCwdIBbIbCgPey9waP7VMTZf%2BenQsfwaJfZ9%2FUilz18xVcg7kzM276zapt7%2BdjgVOfvOnrAenBfEi2g0nJQEF9yQ9L9RGfRoWm0iyg5iQVujGMwpKV8wjRSnzzQE5MHQKj4Wm8adpFD6p1CT4FECa3U4zqbEjyy%2BgD14yHC4%2B08IIId35yAVb0ZjKhdZdX8QLH4q0y0IxujuIgTdxYhomRbML2TNTjI3pUn%2BCdrLTXKPicTUV7zRk3eeAPMe0%2BOYpgCtvUJqeCy1snWaAIo6J0t3BzpN4IsyS05%2Fvv5PSm3AMFnZsquyuE64ZsRVTnTl5HSYim0UsiBDEtuWiTVpza1PnrrYO2Yck2dZUr8Zn4qkU5LxvLTcHdCCV8kJwWT8JOMk7I0xOuafDojGajfKR0XWoiWLfNIz0S9GFuOtmyVaD9%2FYQ6azyGzmSZd6zYkHbpfzz0LezQZ6A3IenHLTagDgE8BJYslNQpNMPiGucEGOqUBbqoKwN11cvgVknxbWz11tGqDLWmlGwjIBYSdJYmOZ2913DfmCXVAIOLyL1QhfNl87kEHUTM5hWWHzTKU8lb0gWcLI0slkPKZ25PXp2FnZh7OnhTvZ3X0qsncb9iOCKNtC%2BYsRpiksMsV9YScJaOT6Q9AKrpQWPPeybD9CttLm1Adc6kw8tQ77%2BQhA9%2FcJf4YFGz8MA6mq%2FhmS2oWVJ81tv2eRxtf&X-Amz-Signature=b6a67a65d3a21a30b7d20f86a857cd096df914797f73147db5487202f9238d5e&X-Amz-SignedHeaders=host&x-id=GetObject)

안녕하세요. 컴퓨터 네트워크 강의 자료(PDF)를 전부 풀어서 설명해 달라고 요청하셨네요. 슬라이드 형식의 자료는 핵심만 요약되어 있어 흐름을 파악하기 어려울 수 있습니다.

사용자님은 컴퓨터 공학을 전공하고 계시고[USER_CONTEXT], 특히 웹 개발과 배포(DevOps)에 관심이 많으신 것[USER_CONTEXT]을 기억하고 있습니다. 이 자료에 나오는 DHCP, CDN, DNS 개념은 사용자님의 관심 분야인 백엔드 및 인프라 운영에 정말 중요한 기초가 됩니다.

자료의 처음부터 끝까지, 각 슬라이드의 의미를 자세히 풀어서 설명해 드리겠습니다.

### 📜 강의 시작: 5주차 (DHCP, CDN)

[cite_start]이 자료는 '컴퓨터네트워크' [cite: 2] [cite_start]강의의 5주차 내용으로, 주제는 **DHCP와 CDN**입니다[cite: 3]. [cite_start](강의자: 임화정 [cite: 1])

#### 1. 이전 학습 복습 (페이지 2-3)

[cite_start]본격적인 내용에 앞서, 2주차에 배운 '프로토콜'의 개념을 복습합니다[cite: 4].
* [cite_start]당시 다룬 주제는 **애플리케이션 계층(Application Layer)** [cite: 7][cite_start]과 그 예시인 **WWW & HTTP**였습니다[cite: 8]. [cite_start](참고 교재는 Kurose & Ross 9판 또는 8판의 2장이었네요 [cite: 10]).
* [cite_start]애플리케이션 계층의 주요 프로토콜로는 웹 문서를 전송하는 **HTTP** [cite: 14][cite_start], 이메일 관련 **SMTP/POP3/IMAP** [cite: 15][cite_start], 그리고 도메인 이름을 IP 주소로 바꿔주는 **DNS**가 있습니다[cite: 16].

#### 2. 이번 주 학습 동기 (페이지 4-5)

[cite_start]이번 주 내용은 DNS에서 한 단계 더 나아간 **실생활 사례**들입니다[cite: 17].

1.  [cite_start]**DHCP**[cite: 18]: 우리가 인터넷에 접속하려 할 때, 내 컴퓨터는 어떻게 IP 주소를 자동으로 할당받을까요?
2.  [cite_start]**비디오 스트리밍과 CDN** [cite: 20][cite_start]: DNS가 어떻게 유튜브나 넷플릭스 같은 서비스 품질에 영향을 미칠까요? [cite: 19]
3.  [cite_start]**소켓 API** [cite: 21][cite_start]: "내가 동영상을 보거나 서버에 접속할 때, 내 컴퓨터의 애플리케이션(브라우저 등)은 네트워크에 어떻게 요청을 보낼까?" [cite: 22]

[cite_start]이 세 가지(DHCP, CDN, 소켓 API) [cite: 23] [cite_start]모두 **애플리케이션 계층**의 일부로 볼 수 있습니다[cite: 24].

---

### 🔑 1부: DHCP (Dynamic Host Configuration Protocol)

DHCP는 우리가 카페 Wi-Fi에 접속하거나 랜선을 꽂았을 때, 복잡한 설정 없이 바로 인터넷을 쓰게 해주는 핵심 프로토콜입니다.

#### 1. DHCP란 무엇인가? (페이지 6)

* [cite_start]**정의**: Dynamic Host Configuration Protocol의 약자입니다[cite: 26].
* [cite_start]**역할**: IP 네트워크에 접속하는 장치(호스트)에게 **자동으로 필요한 설정**을 제공합니다[cite: 28].
* **제공하는 설정 정보**:
    * [cite_start]**IP 주소**[cite: 29]: 네트워크 상의 내 고유 주소.
    * [cite_start]**서브넷 마스크**[cite: 30]: 내가 속한 네트워크의 범위를 알려줌.
    * [cite_start]**기본 게이트웨이(Default Gateway)**[cite: 31]: 이 네트워크의 '대문' 역할. 외부 인터넷망과 통신할 때 거쳐가는 라우터의 주소.
    * [cite_start]**DNS 서버 주소**[cite: 32]: `google.com` 같은 도메인 이름을 IP 주소로 물어볼 수 있는 서버의 주소.

#### 2. DHCP 4-way Handshake (DORA) (페이지 7)

[cite_start]클라이언트(내 노트북)가 DHCP 서버로부터 IP를 받아오는 과정은 4단계로 이루어집니다[cite: 33]. [cite_start]이 과정을 앞 글자를 따서 **DORA**라고 부릅니다[cite: 34].

1.  [cite_start]**Discover (발견)**[cite: 38]:
    * [cite_start]클라이언트가 "이 네트워크에 DHCP 서버 누구야?"라고 **브로드캐스트** (네트워크 내 모든 장치에) 외칩니다[cite: 39].
2.  [cite_start]**Offer (제안)**[cite: 40]:
    * [cite_start]DHCP 서버(들)가 "내가 서버인데, 이 IP 주소(예: 192.168.1.10) 쓸래?"라고 사용 가능한 IP 정보를 제공합니다[cite: 40].
3.  [cite_start]**Request (요청)**[cite: 41]:
    * [cite_start]클라이언트가 (여러 제안 중 하나를 선택하여) "A 서버님이 제안한 192.168.1.10 주소를 쓰겠습니다"라고 **특정 서버에게** 주소를 요청합니다[cite: 41]. (이것도 브로드캐스트로 보내어 다른 서버들에게 "저 다른 분 거 쓰기로 했어요"라고 알려주는 효과가 있습니다.)
4.  [cite_start]**Acknowledge (승인)**[cite: 42]:
    * [cite_start]해당 서버가 "알겠어. 그 주소 너 써"라고 최종적으로 IP 임대를 승인합니다[cite: 42].

#### 3. DHCP 주요 특징 (페이지 8)

* [cite_start]**포트 번호**[cite: 44]:
    * [cite_start]서버: UDP 67번 포트 [cite: 45]
    * [cite_start]클라이언트: UDP 68번 포트 [cite: 46]
* **할당 방식**:
    * [cite_start]**동적 할당** [cite: 47][cite_start]: 서버가 가진 IP 주소 '풀(pool)'에서 사용 가능한 것을 골라 빌려줍니다 (일반적인 방식)[cite: 48].
    * [cite_start]**고정 할당** [cite: 49][cite_start]: 특정 장치(의 MAC 주소)에게는 항상 똑같은 IP 주소를 고정으로 매핑해줍니다 (예: 사내 프린터 서버)[cite: 51].
* [cite_start]**임대 기간 (Lease)**[cite: 52]:
    * IP 주소는 영구 소유가 아니라 '임대'하는 것입니다. [cite_start]정해진 시간만 사용 가능하며 [cite: 53][cite_start], 계속 쓰려면 **갱신(Renew)**이 필요합니다[cite: 53].

#### 4. DHCP 상태 천이 (State Transition) (페이지 9-16)

클라이언트가 IP를 받고, 사용하고, 갱신하고, 반납하는 전 과정을 '상태(State)'로 관리합니다.

[cite_start]**핵심 타이머 (페이지 9)** [cite: 58]
* [cite_start]IP 임대 기간 동안 3개의 타이머가 관리됩니다[cite: 58].
* [cite_start]**T1 (갱신, Renew)**: 임대 기간의 약 50% 시점[cite: 60].
* [cite_start]**T2 (재연결, Rebind)**: 임대 기간의 약 87.5% 시점[cite: 60].
* **만료 (Expire)**: 임대 기간 종료.
* [cite_start]이 타이머 값들은 DHCP 옵션(코드 58, 59)으로 전달됩니다[cite: 59, 62].

[cite_start]**전체 상태 흐름 (페이지 10)** [cite: 64]
`INIT` → `SELECTING` → `REQUESTING` → `BOUND` → `RENEWING` → `REBINDING` → (만료 시) `INIT`

**각 상태 상세 분석 (페이지 11-16)**

1.  [cite_start]**INIT (초기)** [cite: 73]
    * [cite_start]**트리거**: 호스트(노트북) 부팅 등으로 네트워크 설정이 아예 없는 상태[cite: 75].
    * [cite_start]**동작**: `DHCPDISCOVER` 메시지를 브로드캐스트로 전송 (서버 찾기)[cite: 77].
    * [cite_start]**다음 상태**: 하나 이상의 `DHCPOFFER` (제안)를 받으면 `SELECTING`으로 이동[cite: 79].

2.  [cite_start]**SELECTING (서버 선택)** [cite: 81]
    * [cite_start]**트리거**: 여러 서버로부터 `DHCPOFFER`를 수신한 상태[cite: 83].
    * [cite_start]**동작**: 제안받은 주소, 임대 시간 등을 비교하여 마음에 드는 서버 하나를 선택[cite: 85].
    * [cite_start]**다음 상태**: 선택한 서버에게 `DHCPREQUEST` (요청)를 브로드캐스트로 전송하고 `REQUESTING` 상태로 이동[cite: 87].

3.  [cite_start]**REQUESTING (요청 및 승인 대기)** [cite: 89]
    * [cite_start]**트리거**: 특정 서버를 지정해 `DHCPREQUEST`를 보낸 직후[cite: 91].
    * [cite_start]**동작**: 서버의 최종 응답(`DHCPACK`)을 대기[cite: 93].
    * **다음 상태**:
        * [cite_start]`DHCPACK` (승인) 수신: IP, 게이트웨이, DNS 등 설정을 적용하고 `BOUND` 상태로 진입[cite: 95].
        * `DHCPNAK` (거절) 수신: 주소를 쓸 수 없음. [cite_start]`INIT`로 복귀하여 처음부터 다시 시도[cite: 96].
        * (선택) [cite_start]`DHCPDECLINE` (충돌): 혹시나 IP가 충돌하면(Gratuitous ARP로 탐지), `INIT`로 복귀[cite: 97].

4.  [cite_start]**BOUND (정상 사용)** [cite: 99]
    * [cite_start]**트리거**: `DHCPACK`으로 임대가 확정됨[cite: 101].
    * **동작**: 할당된 IP로 정상 통신. [cite_start]T1, T2 타이머 시작[cite: 103].
    * **다음 상태**:
        * [cite_start]**T1 도달 (임대의 50% 경과)**: `RENEWING` 상태로 진입[cite: 105].
        * [cite_start]**사용자 종료**: 사용자가 연결을 해제하면 `DHCPRELEASE`로 서버에 IP 반납[cite: 106].

5.  [cite_start]**RENEWING (임대 갱신 시도)** [cite: 108]
    * [cite_start]**트리거**: T1 타이머 도달 (아직 임대 유효함)[cite: 110].
    * [cite_start]**동작**: **원래 임대를 준 서버에게만** `DHCPREQUEST`를 **유니캐스트** (1:1 통신)로 전송[cite: 112].
    * **다음 상태**:
        * [cite_start]`DHCPACK` (갱신 승인) 수신: 임대 갱신 성공, `BOUND`로 복귀 (새 T1/T2 설정)[cite: 114].
        * **T2 도달 (임대의 87.5% 경과)**: 원래 서버가 응답 없음. [cite_start]`REBINDING`으로 진입[cite: 115].

6.  [cite_start]**REBINDING (재연결 시도 - 아무 서버나)** [cite: 117]
    * [cite_start]**트리거**: T2에 도달할 때까지 갱신에 실패함 (원래 서버가 다운됐거나 네트워크 경로 문제)[cite: 119].
    * [cite_start]**동작**: **모든 DHCP 서버에게** `DHCPREQUEST`를 **브로드캐스트**로 전송 (아무나 응답해달라는 의미)[cite: 121].
    * **다음 상태**:
        * [cite_start]`DHCPACK` 수신: (다른 서버라도) 임대 연장 성공, `BOUND`로 복귀[cite: 123].
        * [cite_start]**임대 만료 (Expire)**: 끝까지 실패하면 IP 주소 사용을 중단하고 `INIT` 상태로 복귀하여 처음부터 다시 시작[cite: 124, 125].

#### 5. DHCP와 서비스의 연결 (페이지 17)

[cite_start]DHCP는 모든 인터넷 서비스의 **출발점**입니다[cite: 130].
1.  [cite_start]**(DHCP)**로 내 IP 주소와 **DNS 서버 주소**를 받습니다[cite: 127].
2.  **(DNS)**를 이용해 `www.youtube.com`의 IP 주소를 물어봅니다. [cite_start]이때 DNS는 나에게서 가장 가까운 **CDN 서버**의 IP를 알려줍니다[cite: 128].
3.  [cite_start]**(애플리케이션)**은 **소켓 API**를 사용해 해당 CDN 서버 IP와 통신을 시작합니다[cite: 129].

---

### 🎬 2부: 비디오 스트리밍 & CDN (Content Delivery Network)

DHCP로 IP를 받고 DNS 주소를 알았다면, 이제 넷플릭스나 유튜브를 봅니다. 이 서비스들은 어떻게 끊김 없이 영상을 제공할까요?

#### 1. 문제점: 비디오 스트리밍 (페이지 18-24)

* [cite_start]**현황**: 인터넷 트래픽의 대다수는 유튜브, 넷플릭스 같은 비디오 스트리밍입니다[cite: 135, 140].
* [cite_start]**어려움 (Challenges)**[cite: 141]:
    1.  [cite_start]**대규모 사용자**: 수십억 명의 사용자를 감당해야 함[cite: 143].
    2.  [cite_start]**다양한 네트워크**: 유선/무선, 고속/저속 등 환경이 제각각[cite: 144].
    3.  [cite_start]**대역폭 변동**: 네트워크 혼잡(특히 저녁 피크타임)에 따라 가용 전송 속도가 계속 변합니다[cite: 164, 165, 167].
    4.  [cite_start]**패킷 손실 및 지연 (Jitter)**: 패킷이 중간에 사라지거나 [cite: 170] [cite_start]도착 시간이 들쭉날쭉(Jitter) [cite: 192, 193]합니다.
* [cite_start]**결과**: 이 문제들은 영상 끊김, 멈춤, 화질 저하 등 **나쁜 사용자 경험(Poor QoE)**을 유발합니다[cite: 172, 194].

**비디오의 특성 (페이지 19)**
[cite_start]비디오는 단순히 사진(프레임)의 연속 [cite: 148]이 아니라, 효율적 전송을 위해 고도로 **압축**됩니다.
* [cite_start]**공간적 압축**: 한 프레임 내에서 같은 색(보라색 배경)이 반복되면, "보라색 N개"라고 한 번에 보냅니다[cite: 152, 157].
* [cite_start]**시간적 압축**: 이전 프레임과 다음 프레임($i \rightarrow i+1$)의 **차이점(달라진 부분)**만 전송합니다[cite: 153, 154, 161].

**스트리밍의 핵심 제약과 해결책 (페이지 22)**
* [cite_start]**제약 (Continuous Playout Constraint)** [cite: 190][cite_start]: 30fps로 녹화된 영상은 클라이언트에서도 정확히 초당 30프레임으로 재생되어야 합니다[cite: 191].
* [cite_start]**문제**: 하지만 네트워크 지연(Jitter) [cite: 192] 때문에 데이터 도착이 불규칙합니다.
* [cite_start]**해결책 (Client-side buffer)** [cite: 195][cite_start]: 데이터를 미리 받아 **버퍼**에 쌓아두고, 안정적으로 연속 재생합니다[cite: 196]. [cite_start]우리가 보는 "버퍼링 중..." 로딩 화면이 이 과정입니다[cite: 197, 199]. [cite_start](페이지 23의 그래프는 이 버퍼가 어떻게 변동하는 네트워크 지연 [cite: 205][cite_start]을 흡수하여 [cite: 208] [cite_start]일정한 재생 [cite: 207]을 만드는지 보여줍니다.)

#### 2. 해결책 1: DASH (Dynamic Adaptive Streaming over HTTP) (페이지 25-28)

[cite_start]스트리밍 문제를 해결하는 현대적 표준 기술입니다[cite: 228, 270].

* [cite_start]**DASH란?** "Dynamic, Adaptive Streaming over HTTP"의 약자입니다[cite: 232].
* [cite_start]**핵심 아이디어**: 비디오를 잘게 나눈 '청크(Chunk)' 단위로, [cite: 234] [cite_start]현재 네트워크 상황에 맞는 최적의 화질을 선택하여 [cite: 261] **HTTP(웹 프로토콜)**로 가져오는 방식입니다.

**동작 방식:**

* **서버의 역할** (페이지 26):
    1.  [cite_start]**청크 분할**: 원본 비디오를 몇 초 단위(예: 2~10초)의 작은 '청크'로 나눕니다[cite: 234, 235].
    2.  [cite_start]**다중 인코딩**: 각 청크를 4K 고화질, 1080p, 480p 저화질 등 **여러 비트레이트(화질) 버전**으로 미리 인코딩해둡니다[cite: 236, 237].
    3.  [cite_start]**CDN 복제**: 이 청크 파일들을 전 세계 CDN 노드에 복제합니다[cite: 239].
    4.  [cite_start]**Manifest 파일 제공**: "이 비디오는 이런 화질(1080p, 480p...)의 청크들로 구성되어 있고, 각 청크의 URL은 여기(CDN 주소)야"라는 '목록(Manifest File, MPD)'을 제공합니다[cite: 241, 244].

* **클라이언트(플레이어)의 역할** (페이지 27):
    1.  [cite_start]**대역폭 측정**: 주기적으로 서버와 클라이언트 간의 가용 대역폭(네트워크 속도)을 측정합니다[cite: 250, 251].
    2.  [cite_start]**Manifest 참조**: Manifest 파일을 보고 어떤 화질의 청크를 가져올 수 있는지 확인합니다[cite: 252].
    3.  [cite_start]**청크 요청**: **한 번에 하나의 청크만** [cite: 252][cite_start], 현재 내 대역폭으로 감당 가능한 최고 비트레이트(화질)의 청크를 선택하여 [cite: 253] HTTP로 요청합니다.
    4.  **동적 적응 (Adaptive)**:
        * [cite_start]네트워크가 좋아지면(Wi-Fi 빵빵) → 다음 청크는 **고화질(1080p)**로 요청[cite: 255].
        * [cite_start]네트워크가 나빠지면(지하철) → 다음 청크는 **저화질(480p)**로 요청[cite: 256].

**DASH의 장점** (페이지 28):
* [cite_start]**적응성**: 네트워크 품질에 따라 화질이 자동 조정됩니다[cite: 264].
* [cite_start]**HTTP 기반**: 별도 프로토콜이 아닌 HTTP를 쓰므로, 기존 웹 인프라(CDN, 캐시)를 그대로 재활용할 수 있습니다[cite: 265, 266].
* [cite_start]**품질 보장**: 끊김(버퍼링)을 최소화하여 [cite: 268] [cite_start]사용자 경험(QoE)을 극대화합니다[cite: 269].

#### 3. 해결책 2: CDN (Content Delivery Network) (페이지 29-34)

DASH가 '어떤 화질'을 가져올지 결정한다면, CDN은 '어디서' 가져올지 결정합니다.

* [cite_start]**문제**: 전 세계 사용자가 미국에 있는 단일 서버(Origin Server)에 접속하면, 서버가 다운되거나 거리가 먼 사용자는 지연(latency)이 심해집니다[cite: 273, 274].
* [cite_start]**해결책 (CDN)**: 콘텐츠(비디오 청크)를 전 세계 곳곳에 분산된 **캐시 서버**에 미리 복제해두는 것입니다[cite: 275].

**CDN 사례별 비교** (페이지 30-34):

| 서비스 | CDN 방식 | 운영 주체 | 특징 |
| :--- | :--- | :--- | :--- |
| [cite_start]**YouTube** [cite: 331] | [cite_start]**GGC** (Google Global Cache) [cite: 280, 331] | [cite_start]Google [cite: 331] | [cite_start]ISP 네트워크 내/근처에 캐시 서버(GGC)를 설치[cite: 282]. [cite_start]DNS가 가장 가까운 GGC로 안내[cite: 285, 331]. |
| [cite_start]**Netflix** [cite: 331] | [cite_start]**Open Connect (OCA)** [cite: 293, 331] | [cite_start]Netflix [cite: 331] | [cite_start]넷플릭스가 자체 개발한 CDN 장비(OCA) [cite: 295, 296][cite_start]를 **ISP에게 무상 배포**하여 ISP 망 내부에 설치[cite: 300, 331]. |
| [cite_start]**Amazon Prime** [cite: 331] | [cite_start]**AWS CloudFront** [cite: 306, 331] | [cite_start]AWS [cite: 331] | [cite_start]아마존의 글로벌 클라우드 인프라(AWS 엣지 로케이션)를 그대로 활용[cite: 308, 309, 331]. [cite_start]다른 기업들도 이 CDN을 사서 쓸 수 있음[cite: 312]. |
| [cite_start]**Wavve** [cite: 331] | [cite_start]국내 ISP CDN [cite: 319, 331] | [cite_start]SKB/KT/LGU+ [cite: 331] | [cite_start]국내 통신사(ISP)가 구축한 CDN 망을 활용[cite: 319]. [cite_start]국내 망에 최적화[cite: 320, 331]. |
| [cite_start]**TVING** [cite: 331] | [cite_start]국내 ISP CDN + 자체 [cite: 323, 331] | [cite_start]CJ ENM/LGU+ [cite: 331] | [cite_start]국내 ISP CDN을 쓰면서 [cite: 323] [cite_start]실시간 방송 송출에 특화됨[cite: 324, 331]. |
| [cite_start]**Coupang Play** [cite: 331] | [cite_start]**AWS CloudFront** [cite: 327, 331] | [cite_start]AWS/쿠팡 [cite: 331] | [cite_start]Amazon Prime Video와 유사하게 AWS의 글로벌 인프라를 활용[cite: 327, 329, 331]. |

#### 4. 전체 흐름 요약 (페이지 35)

1.  [cite_start]**스트리밍의 핵심**: 클라이언트 **버퍼링** + **DASH**를 통한 적응형 화질 선택[cite: 334, 335].
2.  [cite_start]**CDN의 핵심**: 콘텐츠의 **지리적 분산** + **DNS** 기반으로 사용자에게 가장 가까운 서버 선택[cite: 337, 338].
3.  **최초 연결부터의 흐름**:
    * [cite_start]① (내 노트북) **DHCP**로 IP와 DNS 서버 주소를 받음[cite: 341].
    * ② (내 노트북) DNS에게 "유튜브 주소" 질의.
    * [cite_start]③ (DNS) 내 위치(IP)를 기반으로 가장 가까운 **최적의 CDN 서버 IP**를 응답[cite: 341].
    * [cite_start]④ (내 노트북) 해당 CDN 서버와 통신 시작 (다음 학습 주제: 소켓 API, TCP/UDP)[cite: 342].

---

### 🔬 3부: 실습 (OTT 스트리밍 & CDN 관찰)

[cite_start]이론으로 배운 DHCP, DNS, CDN, DASH가 실제 어떻게 동작하는지 확인하는 실습입니다[cite: 343]. [cite_start](준비물: Wireshark [cite: 346][cite_start], 웹 브라우저 [cite: 352])

#### 1. 실습 1: DNS 질의 확인 (페이지 38-40)

* [cite_start]**목적**: DNS가 어떻게 CDN 노드를 선택해 주는지 원리 이해[cite: 356].
* [cite_start]**방법**: `nslookup` 명령어로 여러 OTT 서비스의 도메인을 질의 [cite: 357-361].
* [cite_start]**예시 결과 분석** [cite: 364-474]:
    * [cite_start]`nslookup www.youtube.com` [cite: 364] [cite_start]→ `youtube-ui.l.google.com` [cite: 367][cite_start]라는 별칭(CNAME)을 거쳐 구글 소유의 IP들(예: `142.250.76.142` [cite: 372])이 나옵니다.
    * [cite_start]`nslookup www.netflix.com` [cite: 385] [cite_start]→ `...amazonaws.com` [cite: 389]이 나옵니다. 넷플릭스 웹사이트 자체는 AWS(Amazon) 인프라 위에서 동작함을 알 수 있습니다.
    * [cite_start]`nslookup play.coupang.com` [cite: 429] [cite_start]→ `...akamaiedge.net` [cite: 433]이 나옵니다. 쿠팡플레이는 Akamai라는 유명 CDN 업체를 사용하네요. [cite_start](앞의 표 [cite: 327] 내용과 실습 결과가 다를 수 있는데, 웹사이트와 실제 영상 스트리밍 서버가 다르거나 CDN 정책이 변경되었을 수 있습니다.)
    * [cite_start]`nslookup www.disneyplus.com` [cite: 466] [cite_start]→ `...akamaiedge.net` [cite: 469]이 나옵니다. 디즈니플러스도 Akamai CDN을 사용합니다.

#### 2. 실습 2: Traceroute로 경로 추적 (페이지 41-42)

* [cite_start]**목적**: 내 컴퓨터에서 서버까지 어떤 라우터(경로)를 거쳐 가는지 확인[cite: 479]. [cite_start]CDN이 이 경로(hop count)를 줄여주는지 확인[cite: 481].
* [cite_start]**방법**: `tracert www.disneyplus.com` (Windows) [cite: 477, 478] [cite_start]또는 `traceroute` (Mac/Linux) [cite: 476] 실행.
* **예시 결과 분석**:
    * [cite_start]`www.disneyplus.com` [cite: 483] [cite_start]추적 시, 마지막에 `a23-49-226-53.deploy.static.akamaitechnologies.com` [cite: 559] (Akamai CDN 서버)에 도달하는 것을 볼 수 있습니다.
    * [cite_start]중간에 `*` (요청 시간이 만료되었습니다) [cite: 538, 542][cite_start]가 뜨는 것은, 해당 라우터가 보안 정책상 ICMP(경로 추적용 신호) 응답을 꺼두었기 때문입니다[cite: 563].

#### 3. 실습 3: Wireshark 패킷 캡처 (페이지 43-49)

* **목적**: 실제 영상 데이터가 CDN에서 오는지, DASH가 어떻게 동작하는지 눈으로 확인.

**Step 1: CDN 도메인 확인 (페이지 43-45)**
* [cite_start]**방법**: Wireshark를 켠 상태로 유튜브 영상 재생[cite: 565].
* **분석 (DNS 로그)**:
    * [cite_start]Wireshark 캡처를 보면, 내 컴퓨터(192.168.1.22)가 `...googlevideo.com` 도메인(예: `rr3---sn-oj3pm5-53.googlevideo.com` [cite: 600, 639])을 DNS에 질의하는 것을 볼 수 있습니다.
    * [cite_start]`ytimg.com` [cite: 643][cite_start]은 썸네일 같은 작은 이미지용 도메인이고, `googlevideo.com` [cite: 644][cite_start]이 실제 대용량 **영상 스트리밍용** 구글 CDN 도메인입니다[cite: 645].
    * [cite_start]DNS 서버는 이 도메인의 실제 IP 주소 (A 레코드), 예를 들어 `74.125.10.195` [cite: 702]를 응답해줍니다.

**Step 2: 실제 영상 트래픽 확인 (페이지 46)**
* **분석 (QUIC/TCP 로그)**:
    * [cite_start]DNS 질의(7247, 7248번 패킷) [cite: 705] 직후,
    * [cite_start]내 컴퓨터(192.168.1.22)가 방금 받은 CDN 서버 IP(`74.125.10.195`)로 **QUIC** 프로토콜 통신을 시작합니다 (7256~7266번 패킷)[cite: 705, 706].
    * [cite_start]**QUIC** [cite: 711]은 구글이 만든 UDP 기반의 빠르고 효율적인 프로토콜로, TCP(HTTP/3)를 대체하고 있습니다. [cite_start]이 QUIC 패킷들(`Protected Payload` [cite: 708][cite_start])을 통해 암호화된 실제 영상 조각(세그먼트) 데이터가 전송됩니다[cite: 710]. [cite_start](Wireshark 필터로 `tcp.port == 443 and ip.dst contains "googlevideo.com"` [cite: 567]를 걸면 TCP(HTTPS) 트래픽만 보이지만, 요즘 유튜브는 QUIC(UDP)를 더 많이 사용합니다.)

**Step 3: DASH 동작 체험 (페이지 47-49)**
* [cite_start]**방법**: 유튜브 플레이어의 '화질' 설정을 1080p [cite: 726][cite_start]에서 144p [cite: 733][cite_start]로, 또는 '자동' [cite: 742][cite_start]으로 바꿔봅니다 [cite: 713-715].
* **결과**:
    * [cite_start]수동으로 화질을 바꾸거나, 네트워크가 불안정할 때 [cite: 716] 자동으로 화질이 변하는 것을 볼 수 있습니다.
    * [cite_start]이것이 바로 **DASH**가 [cite: 717] 작동하는 순간입니다. [cite_start]플레이어(클라이언트)가 네트워크 상황에 맞춰 다른 비트레이트(화질)의 **청크**를 CDN 서버에 요청하는 것입니다[cite: 717].

(페이지 50) [cite_start][cite: 743]
여기까지가 강의 자료의 모든 내용입니다.

---

설명이 잘 되었나요? DHCP로 IP를 할당받는 과정부터, DNS를 통해 CDN 서버를 찾고, DASH 기술을 이용해 내 네트워크 속도에 맞는 영상 청크를 받아오는 전체 흐름이 머릿속에 그려지셨으면 좋겠습니다.

혹시 특정 부분(예: DHCP의 T1/T2 타이머, 또는 QUIC 프로토콜)에 대해 더 궁금한 점이 있으신가요?

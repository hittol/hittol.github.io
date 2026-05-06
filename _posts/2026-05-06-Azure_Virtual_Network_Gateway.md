---
title: "Azure VPN 개념 및 문제진단"
excerpt: "Azure VPN Gateway 정책,Troubleshooting 정리"
date: 2026-05-06
categories: [VPN]
Tags: [VPN]
toc: true
toc_sticky: true
toc_label: "Azure VPNGW 정리"
sidebar_main: true
published: true
header:
   teaser: /assets/images/azure_baner.jpg
---
### 1. Azure VPN Gateway 란?

▶ 공용 인터넷을 통해 Azure VNET 과 On-Premise 간 암호화된 트래픽을 전송하는 데 사용하는 서비스

- 가상 네트워크 게이트웨이를 구성할 때 게이트웨이 유형을 지정하는 설정을 구성
- 하나의 가상 네트워크 당 하나의 VPN Gateway 만 사용할 수 있다.
- 한 VPN Gateway 에서 여러 연결을 생성할 수 있다.
- 가상 네트워크 게이트웨이 구성 시 **VPN 유형**을 지정해 ExpressRoute Gateway 와 구분

**1-1. 가상 네트워크 게이트웨이**

- 사용자가 만드는 Gateway Subnet 에 배포되는 둘 이상의 Azure 관리 VM 으로 구성됨.

- 라우팅 테이블을 포함해 특정 게이트웨이 서비스를 실행

( VPN Gateway 또는 ExpressRoute Gateway 중 선택해서 실행 )

- 한 VNET 에 두 종류의 가상 네트워크 게이트웨이가 있을 수 있다. 
         ( 하나의 VPN Gateway 와 ExpressRoute 가 존재할 수 있음 )

**1-2. Active-Active VPN Gateway**

![image-20250304-021408.png](/assets/images/VPN/image-20250304-021408.png)

- 게이트웨이 VM의 두 인스턴스가 모두 On-premise VPN 장치에서 Site 간 VPN Tunnel 설정.

**● 활성-대기 모드**

- 활성-활성을 지정하지 않는 경우 **활성-대기**의 두 인스턴스로 구성

- **활성-대기** 모드에서 계획된 유지 관리 혹은 계획되지 않은 중단 발생 시 일시적인 연결 중단 발생

→ 중단을 방지하기 위해 활성-활성 모드 사용

**● 특징**

- 각 Azure Gateway 인스턴스에는 고유한 공용 IP 주소가 존재하며 각 인스턴스가 On-premise VPN

디바이스에 대한 IPsec/IKE Site to Site VPN Tunnel 을 설정

- 활성-활성 구성 시 On-premise VPN 이 특정 터널을 선호하더라도 Azure 에서는 두 터널을 통해서

트래픽을 동시에 라우팅

( 단일 TCP , 또는 UDP 흐름의 경우 On-premise 로 패킷 전송 시 동일한 터널을 사용하려고 함 )

**1-3. 연결 유형**

- IKEv2 연결을 사용하는 경로 기반 VPN Gateway 에만 적용 ( IKEv1 사용 시 미적용 )

- 연결 시작 방향을 정의하고 초기 IKE 연결 설정에만 적용

1-3.1. Initiator Only     : Azure 에서 먼저 연결을 시작

1-3.2. Responder Only : On-premise 에서 먼저 연결을 시작

---

### 2. IPSec/IKE

▶ IPSec 프로토콜 모음을 사용하여 기기 또는 사용자 간의 가상 사설망을 구축

**2-1. IPSec  ( Internet Protocol Security )**

- OSI 7 Layer 중 3계층 ( 네트워크 ) 상에서 IP 패킷 단위로 암호화, 인증, 키 관리를 하는 프로토콜 모음

- 안전한 IP 통신을 위한 인터넷 프로토콜들의 모음

 **○ IPSec 동작 모드**

● Tunnel Mode : IP 패킷 전체를 캡슐화 하여 그 위에 전송구간 주소 정보를 담은 새로운 IP 해더를 추가

![image-20250314-082211.png](/assets/images/VPN/image-20250314-082211.png)

- 최초 출발지와 최종 목적지에 대한 트래픽 기밀성 보장

● Transport Mode : 기존 IP 해더 대부분 그대로 이용, TCP 헤더 등 의 상위 프로토콜 데이터만 보호

![image-20250314-082604.png](/assets/images/VPN/image-20250314-082604.png)

- End Point 구간의 IP 패킷 보호 목적으로 사용

**2-2. IKE ( Internet Key Exchange )**

- 500/UDP 포트 사용

- IPSec 프로토콜 에서 보안 협상 ( SA ) 를 위해 사용되는 키 관리 프로토콜

- 상호 개체 간 인증된 보안 통신 채널을 생성

 **2-2.1. 키 교환 모드**

![image-20250317-080859.png](/assets/images/VPN/image-20250317-080859.png)

- ISAKMP SA 를 생성하는 1단계와 실제 IPSec 프로토콜이 사용할 SA 를 정의하는 2단계로 구성

 **2-2.1-1. 1단계 ( ISAKMP SA )**

- VPN 간 안전한 Phase 2 SA 교환을 위한 Phase 1 터널 생성 및 상대방 인증

- 두 VPN Gateway 가 1단계 SA 만료 전에 2단계 협상을 완료하지 못 할 경우 다시 1단계 협상 진행

- 암호화 , 인증 , SA Lifetime , DH Group 가 1단계 변환 시 설정

● Main Mode

-  6개의 메시지 교환

- 상대방의 인증까지 암호화 되어 상대방의 IP 주소를 이용한 인증만 수행 가능

● Agressive Mode

- 3개의 짧은 메시지 교환 ( 협상이 빠른 시간 종료 )
                - 상호 간의 인증이 보호되지 않음

 **2-2.1-2. 2 단계 ( IPSec SA )**

- Packet 의 암호화 알고리즘 결정과 암호화 키 교환

● Quick Mode

- 실질적으로 송수신 되는 Packet 의 암호화 및 인증에 사용되는 IPSec SA 를 결정

- ISAKMP SA 에 의해 메시지 교환이 암호화 되어 보호 ( 1단계 협상 설정 필요 )

 **2-2.1-3. Rekey**

- 새로운 SA를 생성할 때 , 새 키를 생성해 데이터를 다시 암호화 하는 것

- 안정성을 위해 1단계 , 2단계 의 유효 기간이 지날 경우 기존 SA 삭제 후 새로운 SA로 갱신

- 경과 시간 , 송/수신 한 패킷 양으로 설정

 **2-2.2. IKEv2**

          - IKE 속성을 유지하며 효율성, 안정성 , 유연성 등을 증대시키는 방향으로 구성

          - 1단계에서도 IPSec SA 협상이 가능하도록 해 기존 IKEv1 에 비해 빠르게 협상 진행

### 3. IPSec/IKE 정책

![image-20250312-051306.png](/assets/images/VPN/image-20250312-051306.png)

**3-1. 암호화 (Encryption)**

- Azure VPN Gateway 에서는 AES 지원

● AES : 사용 가능한 강력한 암호화 알고리즘 , 128/192/256 비트 길이의 암호화 키 지원 ( 주 사용 )

● DES : 56비트 길이의 암호화 키 사용

● 3DES : DES 기반 암호화 알고리즘 , DES 를 세 번 사용해 데이터 암호화

● GCM ( 갈루아/카운터 모드) : 암호화 및 무결성을 동시에 확인

**3-2. 인증 및 무결성 검증 (Integrity/PRF)**

○ HMAC ( Hash-based Message Authentication Code )

- 데이터가 전송 중에 변경되지 않았음을 보장 , 송신자의 신원 확인

● HMAC-SHA1 : 160비트 메세지 고정 해시 값을 생성

● HMAC-SHA2 : 3가지 비트 (256 , 384 , 512 ) 지원 , SHA1  보다 안전함.

**3-3. Diffie-Hellman ( DH ) 키 교환**

- 안전하지 않은 통신 경로 상에서 비밀키를 안전하게 송수신하기 위한 키 교환 방식

- 두 장치의 암호화 키는 데이터를 암호화하는 대칭 키로 사용

- 키 그룹은 디피-헬만 키 교환에 사용되는 정수 그룹 ( Azure 에서는 1 / 2 / 14 / 24 / 2048 중 사용 )

● PFS Group

- 2단계 협상 시 사용하는 디피-헬만 키 교환 그룹

- Phase 2 에서 별도 키 교환을 수행해 Phase 1 키가 유출되어도 트래픽 해독이 어렵게 함.

**3-4. IPSec SA Lifetime 옵션**

![image-20250312-051139.png](/assets/images/VPN/image-20250312-051139.png)

- 두 옵션 중 하나라도 먼저 도달하는 경우 SA 가 재 생성됨.

 **3-4.1. IPSec SA Lifetime in KiloBytes**

- SA 가 처리할 수 있는 최대 데이터량 지정 ( 지정 값 이상을 전송/수신 시 Rekey 발생 )

- 0 으로 설정 시 데이터량 기준의 제한을 두지 않음

- 0 외에 1024 byte ( 1 KiB ) 에서 2147483647 byte ( 2.14 GiB , 32비트 최대 정수 ) 사이의 값 설정 가능

 **3-4.2. IPSec SA Lifetime in Seconds**

- SA 가 유효한 최대 시간 ( 초 단위 ) 지정

- 지정된 시간이 지나면 SA 가 만료되어 새 키를 교환 ( 재협상 ) 하게 됨

- 300 ( 5분 ) 에서 172799 ( 약 48시간 )사이의 값 설정 가능

### **4. DPD ( Dead Peer Detection )**

**4.1. 사용 목적**

- Tunnel 의 IPSec SA 는 터널이 구성되고 만료 전까지 다시 협상하지 않고 설정한 시간 이후에 만료되어

다시 협상을 시작

- SA 만료 전 네트워크 장애 등으로 인한 문제가 발생해 통신이 비정상적으로 중단 되는 경우 ,

피어는 계속해서 기존 터널을 통해 트래픽을 보내는 문제가 발생

**→ DPD 를 통해 Fail 된 터널을 감지하고 해당 IPSec SA 를 중지**

**4.2. 동작 과정**

1. DPD Timeout 값을 설정해 , 트래픽이 끊긴 이후 메시지를 보낼 시간 설정

2. 설정한 Timeout 값 동안 트래픽이 흐르지 않을 시 양방향 메시지 ( Hello/ACK ) 인 keep-alive 메시지를

상대 피어에 설정한 DPD Delay 간격마다 Hello 발송

3. 설정한 Max retries 값 만큼 반복 후 응답 받지 못하는 경우 연결 중단

**4.3. 동작 확인**

 **4-3.1. DPD 동작**

![image-20250313-004918.png](/assets/images/VPN/image-20250313-004918.png)

- Test 용 Ubuntu StorngSwan VPN 설정에서 DPD ON

![image-20250313-005011.png](/assets/images/VPN/image-20250313-005011.png)

- Test 용 Azure VPN 설정에서 DPD 45초 설정

![image-20250313-005253.png](/assets/images/VPN/image-20250313-005253.png)

- 정상적으로 DPD 요청/응답 메세지를 주고받는 것을 확인

![image-20250313-040811.png](/assets/images/VPN/image-20250313-040811.png)

![image-20250313-040918.png](/assets/images/VPN/image-20250313-040918.png)

→ StrongSwan VPN 에서 네트워크 차단 시켰을 때 45초 이후 터널 종료 시작

( 네트워크 차단 시각 : 04:00:12   DPD Timeout 발생 시각 : 04:01:00 )

 **4-3.2. DPD 미동작**

![image-20250313-062612.png](/assets/images/VPN/image-20250313-062612.png)

- Strongswan 에서 네트워크 차단 ( UTC 05:51:03 )

![image-20250313-062741.png](/assets/images/VPN/image-20250313-062741.png)

- Azure VPN Gateway 로그 확인 시 SA 재협상 시 해당 차단 확인 후 터널 종료 ( UTC 06:19:04 )

- Tunnel 문제 확인 까지 **28분** 소요

**→ 실제 네트워크 장애 등의 비정상적 문제가 발생하는 경우 VPN Gateway 가 활성-활성으로 구성되어**

**있는 경우에도 Tunnel 전환이 빠르게 이루어지지 않는 문제가 발생**

**4.4. Azure 내 DPD 설정**

![image-20250304-065835.png](/assets/images/VPN/image-20250304-065835.png)

- 별도의 On/Off 기능은 없으며 기본적으로 On 상태

- 사용자 정의 정책을 통해 DPD Timeout 값 설정 가능 ( 9~ 3600 사이의 값 가능 )

( 지정한 시간 값 동안 응답 없을 시 peer down 으로 간주 )

<aside>
❌ ※ 주의 사항 : Azure Virtual Network Gateway 에서 IKEv1 을 사용하는 경우

DPD 가 지원되지 않는 경우가 발생.

![스크린샷 2025-03-12 135443-20250312-045812.png](/assets/images/VPN/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-03-12_135443-20250312-045812.png)

● 사진과 같이 IKEv1 으로 Main Mode 협상 중  DPD is turned off for tunnelId 로그가 출력

**→ DPD 옵션 필요한 경우 IKEv2 프로토콜로 IPSec VPN 배포 권장.**

</aside>

---

### 5. VPN Gateway 문제 진단

**5-1. VPN Gateway Log 분석**

- Log Analytics 를 통해 VPN Gateway 의 로그 정보들을 확인할 수 있습니다.
- IPSec/IKE 협상 로그 외에도 터널 연결 로그 , 연결 상태 및 성능 지표 , Gateway 운영 로그 , 보안 이벤트 로그 등의 정보를 확인할 수 있습니다.

 **5-1.1. Log Analytics 작업 영역 생성 및 VPNGateway 연결**

5-1.1-1. Log Analytics 작업 영역 을 선택 후 만들기 를 통해 새 작업 영역을 생성합니다.

![image-20250306-055605.png](/assets/images/VPN/image-20250306-055605.png)

**5-1.1-2. Monitor 에서 진단 설정 으로 이동해 해당 VPN 리소스를 선택**

![image-20250306-064902.png](/assets/images/VPN/image-20250306-064902.png)

**5-1.1-3. 진단 설정 추가 를 선택**

![image-20250306-065100.png](/assets/images/VPN/image-20250306-065100.png)

**5-1.1-4. 원하는 이름 지정 후 , 범주 그룹에서 allLogs 선택 , 대상 세부 정보에서 Log Analytics 작업**

**영역에 보내기를 통해 생성한 작업 영역을 지정 후 저장**

![image-20250306-065308.png](/assets/images/VPN/image-20250306-065308.png)

**5-1.2. Quary 를 통해 로그 확인**

**5-1.2-1. 설정한 VPN Gateway 선택 후 로그 이동**

![image-20250306-074434.png](/assets/images/VPN/image-20250306-074434.png)

**5-1.2-2. 아래 스크립트를 사용해서 협상 로그 확인**

```java
AzureDiagnostics
| where Category == "IKEDiagnosticLog"
| where OperationName == "IKELogEvent"
| where Message contains "확인할 VPN Public IP 값"
| project TimeGenerated, Message, OperationName, instance_s, Resource, ResourceGroup
| order by TimeGenerated desc
```

![image-20250306-074656.png](/assets/images/VPN/image-20250306-074656.png)

**5-2. VPN Gateway Packet Capture**

- VPN Gateway Packet Capture 기능을 사용하여 Virtual Network Gateway 를 지나가는 패킷을 확인할 수 있습니다.
- Storage Account 의 Container 에 캡처한 패킷을 저장해 확인할 수 있습니다.

 **5-2.1. Storage Account 공유 엑세스 토큰 발급**

**5-2.1-1. 패킷 캡처 파일을 저장할 스토리지 계정에서 컨테이너 생성**

![image-20250312-052543.png](/assets/images/VPN/image-20250312-052543.png)

**5-2.1-2. 생성한 컨테이너로 이동 후 설정 - 공유 엑세스 토큰 이동**

![image-20250312-052631.png](/assets/images/VPN/image-20250312-052631.png)

**5-2.1-3. 권한을 읽기, 쓰기 선택 후 시작 과 만료 날짜 지정 , 설정 마무리 후 SAS 토큰 및 URL  생성 선택**

- 이후 생성된 Blob SAS URL 복사

![image-20250312-052835.png](/assets/images/VPN/image-20250312-052835.png)

 **5-2.2. VPN Gateway Packet Capture 동작**

**5-2.2-1. VPN Gateway 블레이드 에서 도움말 - VPN Gateway 패킷 캡처 이동 후 패킷 캡처 시작 클릭**

![image-20250312-052232.png](/assets/images/VPN/image-20250312-052232.png)

**5-2.2-2. 원하는 옵션 지정 후 패킷 캡처 시작 선택**

![image-20250312-052323.png](/assets/images/VPN/image-20250312-052323.png)

 **5-2.3. Packet Capture 중지 후 저장**

**5-2.3-1. 패킷 캡처 중지 선택 - 출력 SAS URL 에 복사한 URL 붙여넣기 후 패킷 캡처 중지 클릭**

![image-20250312-053105.png](/assets/images/VPN/image-20250312-053105.png)

**5-2.3-2. Container 에서 저장된 패킷 캡처 파일 확인**

![image-20250312-053318.png](/assets/images/VPN/image-20250312-053318.png)


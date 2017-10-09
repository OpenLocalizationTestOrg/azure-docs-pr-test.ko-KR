---
title: "예 – aaaDMZ DMZ tooprotect 방화벽과 Nsg로 응용 프로그램을 작성 | Microsoft Docs"
description: "방화벽 및 NSG(네트워크 보안 그룹)를 사용하여 DMZ 빌드"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: c78491c7-54ac-4469-851c-b35bfed0f528
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: 18f116dc3897567bff14a509ae8c13f449182bfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="example-2--build-a-dmz-tooprotect-applications-with-a-firewall-and-nsgs"></a>예제 2 – DMZ tooprotect 방화벽과 Nsg로 응용 프로그램을 작성
[Toohello 보안 모범 사례 페이지 경계를 반환 합니다.][HOME]

이 예에서는 방화벽, 4개의 Windows Server 및 네트워크 보안 그룹이 포함된 DMZ를 만듭니다. 그는 또한 안내 각각 hello 관련 명령 tooprovide의 각 단계에 대 한 깊은 이해가. 이기도 한 트래픽 시나리오 섹션 tooprovide 심층 분석 하는 단계별 트래픽 hello 계층의 철저 한 방어 기능을 통해 진행 방법 hello DMZ 합니다. 마지막으로 hello references 섹션에는 전체 코드 hello 및 명령 toobuild이 환경 tootest 및 다양 한 시나리오와 실험입니다. 

![NVA NSG와 인바운드 DMZ][1]

## <a name="environment-description"></a>환경 설명
이 예제는 hello 다음을 포함 하는 구독:

* 두 클라우드 서비스: "FrontEnd001" 및 "BackEnd001"
* "FrontEnd" 및 "BackEnd"의 두 서브넷을 포함하는 가상 네트워크 "CorpNetwork"
* 적용 된 tooboth 서브넷은 단일 네트워크 보안 그룹
* 이 예제에서는 Barracuda NextGen 방화벽에서 네트워크 가상 어플라이언스 toohello 프런트 엔드 서브넷 연결
* 응용 프로그램 웹 서버("IIS01")를 나타내는 Windows 서버
* 응용 프로그램 백 엔드 서버("AppVM01", "AppVM02")를 나타내는 두 Windows 서버
* DNS 서버("DNS01")를 나타내는 Windows Server

> [!NOTE]
> 이 예제에서는 다양 한 다른 네트워크 가상 어플라이언스를이 예제에 사용 될 수는 hello Barracuda NextGen 방화벽을 사용 하지만 합니다.
> 
> 

아래 hello references 섹션에는 PowerShell 스크립트를 위에서 설명한 hello 환경의 대부분 빌드됩니다 있습니다. 건물 hello Vm 및 가상 네트워크를 hello 예제 스크립트에 의해 수행 하지만이 문서에 자세히 설명에서 하지 설명 되어 있습니다.

toobuild hello 환경:

1. Hello 네트워크 구성 xml 파일 (이름, 위치 및 IP 주소 toomatch hello 주어진 시나리오에 업데이트) hello references 섹션에 포함 된 저장
2. Hello 스크립트 toomatch hello 환경 hello 스크립트의 update hello 사용자 변수는 toobe (구독, 서비스 이름 등)에 대해 실행
3. PowerShell에서 hello 스크립트를 실행 합니다.

**참고**: hello PowerShell 스크립트에서에서 표시 하는 hello 지역 hello 네트워크 구성 xml 파일에서 표시 하는 hello 지역 일치 해야 합니다.

Hello 스크립트가 성공적으로 실행 되 면 이후 스크립트 단계를 수행 하는 hello는 사용할 수 있습니다.

1. 이 이라는 hello 섹션에서 설명 되 hello 방화벽 규칙을 설정,: 방화벽 규칙입니다.
2. 필요에 따라 hello references 섹션에는 두 개의 스크립트 tooset hello 웹 서버와이 DMZ 구성을 테스트 하는 간단한 웹 응용 프로그램 tooallow와 응용 프로그램 서버.

hello 다음 섹션에서는 대부분의 hello 스크립트 문 상대 tooNetwork 보안 그룹을 설명 합니다.

## <a name="network-security-groups-nsg"></a>네트워크 보안 그룹(NSG)
이 예에서는 NSG 그룹을 빌드한 후 6개의 규칙과 함께 로드합니다. 

> [!TIP]
> 일반적으로 특정 "Allow" 규칙을 먼저 만든 하 고 보다 일반적인 "거부" 규칙을 마지막 hello 안됩니다. 우선 순위가 할당 된 hello는 규칙이 먼저 평가 결정 합니다. 트래픽 tooapply tooa 특정 규칙 발견 되 면 더 이상 규칙이 평가 됩니다. NSG 규칙의 hello에 적용할 수 측면에서 볼 hello hello 서브넷의 인바운드 또는 아웃 바운드 방향입니다.
> 
> 

선언적 규칙에 따라 hello 인바운드 트래픽에 대 한 빌드 중인:

1. 내부 DNS 트래픽(포트 53) 허용됨
2. RDP 트래픽 (포트 3389 hello 인터넷 tooany VM에서 에서) 허용 됩니다.
3. Hello 인터넷 toohello NVA (방화벽)에서 HTTP 트래픽 (포트 80)가 허용
4. (모든 포트) IIS01 tooAppVM1에서 모든 트래픽을 허용합니다
5. 전체 VNet (두 서브넷)에서 거부 된 hello 인터넷 toohello에서 모든 트래픽 (모든 포트)
6. Hello 프런트 엔드 서브넷 toohello 백 엔드 서브넷에서 모든 트래픽 (모든 포트) 거부 되었습니다.

이러한 규칙 바인딩된 tooeach 서브넷이 있는 HTTP 요청을 한 hello 인터넷 toohello 웹 서버에서 바인딩된 경우 모두 규칙 3 (허용)이 고 5 (거부) 적용 하는 것을 히 규칙 3 보다 우선 순위가 규칙 5는 하지 고려해 야 하 고 적용 됩니다. 따라서 toohello 방화벽 hello HTTP 요청 허용 합니다. 동일한 트래픽이 해당 tooreach hello DNS01 서버를 시도 하 고, 규칙 5 (거부) hello 첫 번째 tooapply 및 hello 트래픽 toopass toohello 서버 허용 되지 않는 것입니다. (제외 규칙 1 및 4에서에서 허용 된 트래픽) toohello 백 엔드 서브넷 통하게에서 6 (거부) 블록 hello 프런트 엔드 서브넷 규칙, hello 백 엔드 네트워크 보호는 공격자가 손상 hello에서 웹 응용 프로그램 hello 프런트 엔드, hello 공격자가 있을 경우 제한 된 액세스 toohello 백 엔드 "보호" (만 hello AppVM01 서버에서 노출 tooresources) 네트워크.

Toohello 아웃 트래픽을 허용 하는 기본 아웃 바운드 규칙이 인터넷 합니다. 이 예에서는 아웃바운드 트래픽을 허용하고 아웃바운드 규칙을 수정하지 않습니다. 양방향에서 트래픽 아래로 toolock, 사용자 정의 된 라우팅 필수가, hello에서 찾을 수 있는 다른 예에 대해서는이 [주요 보안 경계 문서][HOME]합니다.

위의 설명 hello NSG 규칙에서 매우 유사한 toohello NSG 규칙은 [예제 1-Nsg 간단한 DMZ 빌드][Example1]합니다. 자세히 살펴보려면 각 NSG 규칙 및 해당 특성에 대 한 해당 문서의 hello NSG 설명을 검토 하십시오.

## <a name="firewall-rules"></a>방화벽 규칙
관리 클라이언트에서는 toobe PC toomanage hello 방화벽에 설치 되어 있어야 하 고 필요한 hello 구성을 만듭니다. 어떻게 toomanage hello 장치에 hello 설명서 방화벽 (또는 다른 NVA)에서 공급 업체를 참조 하십시오. 이 섹션의 나머지 부분은 hello hello 공급 업체 관리 클라이언트 (즉, 하지 hello Azure 포털 또는 PowerShell)를 통해 자체 hello 방화벽의 hello 구성에 설명 합니다.

클라이언트 다운로드 및 연결 toohello Barracuda이 예에서 사용에 대 한 지침은 여기: [Barracuda NG 관리자](https://techlib.barracuda.com/NG61/NGAdmin)

Hello 방화벽에서 전달 규칙 toobe 생성 해야 합니다. 하나의 전달 NAT 규칙은이 예에서는 인터넷 트래픽 inbound toohello 방화벽 및 웹 서버 toohello 라우트, 하므로 필요 합니다. 이 예제에서는 hello에 사용 된 Barracuda NextGen 방화벽 hello에 규칙 것 대상 NAT 규칙 ("Dst NAT") toopass이이 트래픽을입니다.

toocreate hello 다음 규칙 (또는 기존 기본 규칙 확인) hello Operational 구성 섹션에서 규칙 집합을 toohello 구성 탭 이동 hello Barracuda NG 관리 클라이언트 대시보드를 시작 합니다. 표 호출 하 여 "Main 규칙" hello 방화벽에 대 한 규칙 활성화 및 비활성화 된 기존 hello를 표시 됩니다. Hello 오른쪽 상단의이 눈금은 작은 녹색 "+" 단추를 클릭이 toocreate 새 규칙 (참고: 방화벽 "잠겨" 변경에 대 한 단추를 "잠글"으로 표시 하 고는 없습니다 toocreate 또는 규칙 편집을 클릭 표시 되 면이 단추 너무 "잠금 해제" hello, ruleset 편집). 기존 규칙 tooedit을 원한다 해당 규칙을 선택, 마우스 오른쪽 단추로 클릭 하 고 편집할 규칙을 선택 합니다.

새 규칙을 만들고 "WebTraffic"과 같은 이름을 제공합니다. 

hello 대상 NAT 규칙 아이콘은 다음과 같습니다: ![대상 NAT 아이콘][2]

자체 hello 규칙 모양은 다음과 같습니다.

![방화벽 규칙][3]

여기 적중 hello 방화벽 tooreach HTTP (포트 80 또는 443을 HTTPS)을 시도 하는 모든 인바운드 주소 전송 방화벽의 "DHCP1 로컬 IP" 인터페이스 및 리디렉션된 toohello hello 10.0.1.5의 IP 주소와 웹 서버 hello 합니다. 포트 80 및 포트 80에서 진행 중인 toohello 웹 서버에서 들어오는 hello 트래픽 이후 포트 변경 안 함이 필요 했습니다. 그러나 hello 대상 목록 했을 수 10.0.1.5:8080 포트 8080 따라서 변환에 웹 서버 수신 대기 하는 경우 인바운드 포트 80 hello 웹 서버에서 방화벽 tooinbound 포트 8080 hello hello 합니다.

연결 방법은 해야도 수 표시를 hello 인터넷에서에서 대상 규칙 hello에 대 한 "동적 SNAT"는 가장 적합 합니다. 

하나의 규칙만 만들어지지만 우선순위가 바르게 설정되는 것이 중요합니다. Hello 방화벽에 대 한 모든 규칙의 hello 그리드에서 ("hello"BLOCKALL"규칙) 아래 hello 아래쪽에 새이 규칙은에 발생 하지 않습니다. 웹 트래픽에 대 한 hello 새로 만든 규칙 hello BLOCKALL 규칙 보다 높은 지 확인 합니다.

해야 hello 규칙을 만든 후 toohello 방화벽 푸시되 며 다음 처리 되 고 활성화, 이렇게 하지 않으면 hello 규칙 변경 내용이 적용 되지 것입니다. hello 푸시 및 활성화 프로세스는 hello 다음 섹션에 설명 되어 있습니다.

## <a name="rule-activation"></a>규칙 활성화
Hello로 ruleset tooadd이이 규칙을 수정 hello ruleset 해야 toohello 방화벽을 업로드 하 고 활성화 합니다.

![방화벽 규칙 활성화][4]

Hello 관리 클라이언트의 오른쪽 상단 모서리 hello 단추의 클러스터가 됩니다. Hello "보낼 변경" 단추 toosend hello 수정 규칙 toohello 방화벽 클릭 hello "활성화" 단추를 클릭 합니다.

이 예에서는 환경 구축 hello 방화벽 규칙 집합의 정품 인증의 hello 완료 되었습니다. 필요에 따라 hello에 hello 후 빌드 스크립트 참조 섹션 수 실행 tooadd 아래의 트래픽 시나리오는 응용 프로그램 toothis 환경 tootest hello 합니다.

> [!IMPORTANT]
> 것이 중요 한 toorealize는 직접 hello 웹 서버를 하지 적중지 것입니다. 브라우저에서 FrontEnd001.CloudApp.Net HTTP 페이지를 요청 하면이 트래픽을 toohello 방화벽 하지 hello hello HTTP 끝점 (포트 80) 전달 웹 서버입니다. 다음 방화벽 hello toohello 웹 서버를 요청 하는 Nat 위에서 만든 toohello 규칙에 따라 합니다.
> 
> 

## <a name="traffic-scenarios"></a>트래픽 시나리오
#### <a name="allowed-web-tooweb-server-through-firewall"></a>(사용 가능) 웹 tooWeb 방화벽을 통해 서버
1. 인터넷 사용자가 FrontEnd001.CloudApp.Net에서 HTTP 페이지를 요청합니다(인터넷 연결 클라우드 서비스).
2. 포트 80 toofirewall 10.0.1.4:80에서 로컬 인터페이스에 대 한 열린 끝점을 통해 클라우드 서비스 전달 트래픽
3. 프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.
   1. Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.
   2. Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.
   3. NSG 규칙 3 (인터넷 tooFirewall)은 적용, 트래픽은 허용, 중지 규칙 처리
4. 트래픽은 hello 방화벽 (10.0.1.4)의 내부 IP 주소에 도달
5. 이 포트 80 트래픽, toohello 웹 서버 IIS01 리디렉션합니다 방화벽 전달 규칙 참조
6. IIS01 웹 트래픽에 대 한 수신이 요청을 수신 하 고 hello 요청 처리를 시작합니다
7. IIS01 정보 AppVM01에 SQL Server hello를 요청
8. 프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.
9. 인바운드 규칙 처리를 시작 하는 hello 백 엔드 서브넷:
   1. Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.
   2. Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.
   3. Toonext 규칙 이동 NSG 규칙 3 (인터넷 tooFirewall) 적용 되지 않습니다
   4. NSG 규칙 4 (IIS01 tooAppVM01)은 적용, 트래픽은 허용, 중지 규칙 처리
10. AppVM01 hello SQL 쿼리를 받아 응답
11. 백 엔드 서브넷 hello 응답 hello에 대 한 없는 아웃 바운드 규칙은 사용할 수 있기 때문
12. 프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.
    1. 사용자에 게 적용 hello NSG 규칙 중 tooInbound 트래픽을 hello 백 엔드 서브넷 toohello 프런트 엔드 서브넷에서 적용 되는 NSG 규칙이 없습니다.
    2. 서브넷 간의 트래픽을 허용 하는 hello 기본 시스템 규칙이이 트래픽을 하면 hello 트래픽이 허용 됩니다.
13. hello IIS 서버 hello SQL 응답을 수신 하 고 hello HTTP 응답을 완료 및 toohello 요청자에 게 보냅니다.
14. Hello 방화벽에 대 한 hello 응답 대상 (처음)은 hello 방화벽에서 NAT 세션 이므로,
15. hello 방화벽 hello 응답 hello 웹 서버에서에서 주고 받는 백 toohello 인터넷 사용자
16. 이어서 hello 프런트 엔드 서브넷 hello 응답에 아웃 바운드 규칙이 없습니다 허용 되 고 hello 인터넷 사용자 hello 웹 페이지 요청을 받습니다.

#### <a name="allowed-rdp-toobackend"></a>(사용 가능) RDP tooBackend
1. 인터넷에서 서버 관리자 요청 BackEnd001.CloudApp.Net:xxxxx 여기서 xxxxx는 RDP tooAppVM01 hello 임의로 할당 된 포트 번호에서 RDP 세션 tooAppVM01 (hello 할당 된 포트를 찾을 수 hello Azure 포털에서 또는 PowerShell을 통해)
2. 방화벽은 hello FrontEnd001.CloudApp.Net 주소 에서만 수신 대기 하는 hello, 이후이 트래픽 흐름에 포함 되지 않은
3. 백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.
   1. Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.
   2. NSG 규칙 2(RDP)가 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.
4. 아웃바운드 규칙이 없는 경우 기본 규칙이 적용되고 반환 트래픽이 허용됩니다.
5. RDP 세션이 사용하도록 설정됩니다.
6. AppVM01에서 사용자 이름과 암호를 묻습니다.

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a>(허용) DNS 서버에서 웹 서버 DNS 조회
1. 웹 www.data.gov 하지만 요구 tooresolve hello 주소에서 데이터 피드 IIS01, 서버 요구 사항입니다.
2. hello 네트워크 구성을 DNS01 hello VNet 목록에 대 한 (hello 백 엔드 서브넷에 10.0.2.4) hello 주 DNS 서버로 IIS01 보냅니다 hello DNS 요청 tooDNS01
3. 프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.
4. 백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.
   1. NSG 규칙 1(DNS)이 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.
5. DNS 서버 hello 요청 수신
6. DNS 서버 캐시 hello 주소 없고 루트 DNS 서버 hello에 요청 인터넷
7. 백 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.
8. 이 세션은 내부적으로 시작 된 이후 인터넷 DNS 서버 응답을 hello 응답이 허용
9. DNS 서버 hello 응답을 캐시 및 toohello 초기 요청 백 tooIIS01 이벤트에 응답
10. 백 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.
11. 프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.
    1. 사용자에 게 적용 hello NSG 규칙 중 tooInbound 트래픽을 hello 백 엔드 서브넷 toohello 프런트 엔드 서브넷에서 적용 되는 NSG 규칙이 없습니다.
    2. hello 트래픽이 허용 됩니다 서브넷 간의 트래픽을 허용 하는 hello 기본 시스템 규칙이이 트래픽은 허용
12. IIS01은 DNS01에서 hello 응답을 받습니다.

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(허용) AppVM01에서 웹 서버가 파일 액세스
1. IIS01은 AppVM01에서 파일을 요청합니다.
2. 프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.
3. 인바운드 규칙 처리를 시작 하는 hello 백 엔드 서브넷:
   1. Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.
   2. Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.
   3. Toonext 규칙 이동 NSG 규칙 3 (인터넷 tooFirewall) 적용 되지 않습니다
   4. NSG 규칙 4 (IIS01 tooAppVM01)은 적용, 트래픽은 허용, 중지 규칙 처리
4. AppVM01은 hello 요청을 받아 파일 (액세스 권한이 부여 가정)를 사용 하 여 응답
5. 백 엔드 서브넷 hello 응답 hello에 대 한 없는 아웃 바운드 규칙은 사용할 수 있기 때문
6. 프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.
   1. 사용자에 게 적용 hello NSG 규칙 중 tooInbound 트래픽을 hello 백 엔드 서브넷 toohello 프런트 엔드 서브넷에서 적용 되는 NSG 규칙이 없습니다.
   2. 서브넷 간의 트래픽을 허용 하는 hello 기본 시스템 규칙이이 트래픽을 하면 hello 트래픽이 허용 됩니다.
7. hello IIS 서버 hello 파일 수신

#### <a name="denied-web-direct-tooweb-server"></a>(거부 됨) 직접 tooWeb 웹 서버
웹 서버 hello, IIS01, 및 hello 방화벽 이후는 hello에 동일한 클라우드 서비스를 공유 hello 동일한 공용 IP 주소입니다. 모든 HTTP 트래픽을 전송할 것 따라서 toohello 방화벽입니다. Hello 요청이 성공적으로 제공 될 것 동안 이동할 수 없습니다 웹 서버 toohello 전달 것을 직접을 정상적으로 hello를 통해 방화벽 먼저 합니다. 참조 hello hello 트래픽 흐름에 대 한이 섹션의 첫 번째 시나리오입니다.

#### <a name="denied-web-toobackend-server"></a>(거부 됨) 웹 tooBackend 서버
1. 인터넷 사용자가 tooaccess hello BackEnd001.CloudApp.Net 서비스를 통해 AppVM01에 있는 파일
2. 파일 공유에 대 한 열린 끝점을 하나도 있을 경우이 hello 클라우드 서비스에 전달 하는 한 hello 서버에 도달 하지
3. NSG 규칙 5 (인터넷 tooVNet)이이 트래픽을 차단는 몇 가지 이유로 hello 끝점 열려 인 경우

#### <a name="denied-web-dns-lookup-on-dns-server"></a>(거부) DNS 서버에서 웹 DNS 조회
1. 인터넷 사용자가 toolookup hello BackEnd001.CloudApp.Net 서비스를 통해 DNS01에 내부 DNS 레코드
2. DNS에 대 한 열린 끝점을 하나도 있을 경우이 hello 클라우드 서비스에 전달 하는 한 hello 서버에 도달 하지
3. NSG 규칙 5 (인터넷 tooVNet)이이 트래픽을 차단는 몇 가지 이유로 hello 끝점 열려 있던 경우 (참고: 규칙 1 (DNS) 같은 두 가지 이유로 적용 되지 않습니다, 첫 번째 hello 소스 주소는 인터넷을 hello,이 규칙은 toohello 적용 됩니다. 또한 지역 VNet으로 hello 원본 이 트래픽이 거부 하지 않습니다 것 이므로 허용 규칙)

#### <a name="denied-web-toosql-access-through-firewall"></a>(거부 됨) 방화벽을 통해 웹 tooSQL 액세스
1. 인터넷 사용자가 FrontEnd001.CloudApp.Net에서 SQL 데이터를 요청합니다(인터넷 연결 클라우드 서비스).
2. SQL에 대 한 열린 끝점을 하나도 있을 경우이 hello 클라우드 서비스에 전달 하는 고 hello 방화벽에 도달 하지 않습니다.
3. 어떤 이유로 끝점 열려 있던 hello 프런트 엔드 서브넷 인바운드 규칙 처리를 시작 합니다.
   1. Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.
   2. Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.
   3. NSG 규칙 2 (인터넷 tooFirewall)은 적용, 트래픽은 허용, 중지 규칙 처리
4. 트래픽은 hello 방화벽 (10.0.1.4)의 내부 IP 주소에 도달
5. SQL에 대 한 전달 규칙에 방화벽 및 삭제 합니다. hello 트래픽

## <a name="conclusion"></a>결론
이 방법은 방화벽 응용 프로그램을 보호 하 고 hello 백 엔드 서브넷 인바운드 트래픽에서 격리의 비교적 간단 합니다.

네트워크 보안 경계에 대한 더 많은 예와 개요는 [여기][HOME]에서 찾을 수 있습니다.

## <a name="references"></a>참조
### <a name="main-script-and-network-config"></a>기본 스크립트 및 네트워크 구성
PowerShell 스크립트 파일에 hello 전체 스크립트를 저장 합니다. Hello 네트워크 구성 "NetworkConf2.xml" 라는 파일에 저장 합니다.
필요에 따라 hello 사용자 정의 변수를 수정 합니다. Hello 스크립트를 실행 한 다음 위의 hello 방화벽 규칙 설정 지침을 따릅니다.

#### <a name="full-script"></a>전체 스크립트
이 스크립트는 hello 사용자 정의 변수를 기반 합니다.

1. Tooan Azure 구독 연결
2. 새 저장소 계정 만들기
3. VNet을 새로 만들고 hello 네트워크 구성 파일에 정의 된 대로 두 서브넷
4. 4개의 Windows Server VM 빌드
5. 다음을 포함하여 NSG 구성
   * NSG 만들기
   * 규칙으로 채우기
   * 바인딩 hello NSG toohello 적절 한 서브넷

이 PowerShell 스크립트를 인터넷 연결된 PC 또는 서버에서 로컬로 실행해야 합니다.

> [!IMPORTANT]
> 이 스크립트를 실행하는 경우 PowerShell에서 경고 또는 기타 정보 메시지가 표시될 수 있습니다. 빨간색 오류 메시지만 심각한 문제입니다.
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and Network Security Groups in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Two new cloud services
       - Two Subnets (FrontEnd and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet (plus hello NVA on hello FrontEnd subnet)
       - Three Servers on hello BackEnd Subnet
       - Network Security Groups tooallow/deny traffic patterns as declared

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Security requirements are different for each use case and can be addressed in a
      myriad of ways. Please be sure that any sensitive data or applications are behind
      hello appropriate layer(s) of protection. This script serves as an example of some
      of hello techniques that can be used, but should not be used for all scenarios. You
      are responsible tooassess your security needs and hello appropriate protections
      needed, and then effectively implement those protections.

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       myFirewall - 10.0.1.4
       IIS01      - 10.0.1.5

      BackEnd Service (BackEnd subnet 10.0.2.0/24)
       DNS01      - 10.0.2.4
       AppVM01    - 10.0.2.5
       AppVM02    - 10.0.2.6

    #>

    # Fixed Variables
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes tooreflect your subscription and services
      # Invalid options will fail in hello validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf2.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure proper NSG Rule creation later in this script:
        #       - hello Web Server must be VM 1
        #       - hello AppVM1 Server must be VM 2
        #       - hello DNS server must be VM 4
        #
        #       Otherwise hello NSG rules in hello last section of this
        #       script will need toobe changed toomatch hello modified
        #       VM array numbers ($i) so hello NSG Rule IP addresses
        #       are aligned toohello associated VM IP addresses.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
            Return}
        Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
              New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

      # Update Subscription Pointer tooNew Storage Account
        Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

    # Build VMs
        $i=0
        $VMName | Foreach {
            Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: Web traffic goes through hello firewall, so we'll need tooset up a HTTP endpoint.
                #       Also, hello firewall will be redirecting web traffic tooa new IP and Port in a
                #       forwarding rule, so hello HTTP endpoint here will have hello same public and local
                #       port and hello firewall will do hello NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                    # Note: A Remote Desktop endpoint is automatically created when each VM is created.
                }
            $i++
        }

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) too$($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 140 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
            -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
            -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
            -Protocol *

        # Assign hello NSG toohello Subnets
            Write-Host "Binding hello NSG tooboth subnets" -ForegroundColor Cyan
            Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
            Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a>네트워크 구성 파일
업데이트 된 위치와이 xml 파일을 저장 하 고 hello 링크 toothis toohello $NetworkConfigFile 변수 위의 hello 스크립트에서 파일을 추가 합니다.

    <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
      <VirtualNetworkConfiguration>
        <Dns>
          <DnsServers>
            <DnsServer name="DNS01" IPAddress="10.0.2.4" />
            <DnsServer name="Level3" IPAddress="209.244.0.3" />
          </DnsServers>
        </Dns>
        <VirtualNetworkSites>
          <VirtualNetworkSite name="CorpNetwork" Location="Central US">
            <AddressSpace>
              <AddressPrefix>10.0.0.0/16</AddressPrefix>
            </AddressSpace>
            <Subnets>
              <Subnet name="FrontEnd">
                <AddressPrefix>10.0.1.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="BackEnd">
                <AddressPrefix>10.0.2.0/24</AddressPrefix>
              </Subnet>
            </Subnets>
            <DnsServersRef>
              <DnsServerRef name="DNS01" />
              <DnsServerRef name="Level3" />
            </DnsServersRef>
          </VirtualNetworkSite>
        </VirtualNetworkSites>
      </VirtualNetworkConfiguration>
    </NetworkConfiguration>

#### <a name="sample-application-scripts"></a>샘플 응용 프로그램 스크립트
Hello 링크에 제공 된다는이 및 다른 DMZ 예제는 예제 응용 프로그램 tooinstall 원하면: [샘플 응용 프로그램 스크립트][SampleApp]

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "NSG와 인바운드 DMZ"
[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "대상 NAT 아이콘"
[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "방화벽 규칙"
[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "방화벽 규칙 활성화"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md

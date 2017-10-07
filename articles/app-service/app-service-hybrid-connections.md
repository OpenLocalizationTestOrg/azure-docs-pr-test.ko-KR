---
title: "aaa \"Azure 앱 서비스 하이브리드 연결 | \"Microsoft Docs"
description: "어떻게 서로 다른 네트워크의 하이브리드 연결 tooaccess 리소스 toocreate 및 사용"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 66774bde-13f5-45d0-9a70-4e9536a4f619
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/22/2017
ms.author: ccompy
ms.openlocfilehash: 61d58068ab0a7c803019e3f0e92bde4273d1a053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-hybrid-connections"></a>Azure App Service 하이브리드 연결 #

## <a name="overview"></a>개요 ##

하이브리드 연결은 모두 Azure에 서비스 뿐만 아니라 hello Azure 앱 서비스의에서 기능입니다.  서비스는 사용 및 hello Azure 앱 서비스에서에서 활용 하는 것 이상의 기능에 있습니다.  하이브리드 연결 및 Azure 앱 서비스를 시작할 수 있습니다 hello 외부에서 사용 하는 방법에 대 한 자세한 toolearn [Azure 릴레이 하이브리드 연결][HCService]

Hello Azure 앱 서비스 내에서 하이브리드 연결에는 다른 네트워크에 사용 되는 tooaccess 응용 프로그램 리소스 수 있습니다. 응용 프로그램 tooan 응용 프로그램 끝점에서 액세스를 제공 합니다.  수 있는 대체 기능 tooaccess 응용 프로그램입니다.  Hello 앱 서비스에서에서 사용 되는, 단일 TCP 호스트 및 포트 조합을 tooa 각 하이브리드 연결에 연관 시킵니다.  즉, 해당 hello 하이브리드 연결 끝점 제공 될 수 있습니다는 운영 체제 및 모든 응용 프로그램에 적중할 TCP 수신 대기 포트. 하이브리드 연결 알고 하거나 어떤 hello 응용 프로그램 프로토콜은 또는 기능에 액세스 하는 중요 하지 않습니다.  단지 네트워크 액세스를 제공합니다.  


## <a name="how-it-works"></a>작동 방법 ##
아웃 바운드 호출을 두 개의 tooService 버스 릴레이의 hello 하이브리드 연결 기능은 구성 됩니다.  Hello 호스트 위치 hello 앱 서비스에서 앱을 실행 하 고, hello 하이브리드 연결 Manager(HCM) tooService 버스 릴레이에서 연결의 라이브러리에서 연결 되어 있습니다.  HCM hello는 hello 네트워크 호스팅 내에서 배포 하는 릴레이 서비스 

Hello를 통해 두 개의 조인 된 연결 응용 프로그램에 TCP 터널 tooa hello HCM의 다른 쪽 hello에 호스트: 포트 조합을 고정 합니다.  보안 및 인증/권한 부여에 대 한 SAS 키에 대 한 TLS 1.2를 사용 하는 hello 연결 합니다.    

![][1]

응용 프로그램에서 DNS 요청 구성 하이브리드 연결 끝점을 일치 하는 다음 hello 아웃 바운드 TCP 트래픽을 hello 하이브리드 연결 아래로 이동 합니다.  

> [!NOTE]
> 이 것이 좋습니다 tooalways 사용 하 여 하이브리드 연결의 DNS 이름을 의미 합니다.  Hello 끝점 IP 주소를 대신 사용 하는 경우 일부 클라이언트 소프트웨어에서 DNS 조회를 수행 하지 않습니다.
>
>

하이브리드 연결을 Azure 릴레이 서비스로 제공 되 고 hello 이전 BizTalk 하이브리드 연결 하는 hello 새 하이브리드 연결의는 다음과 같은 두 종류가 있습니다.  hello 이전 BizTalk 하이브리드 연결은 hello 포털에서 기존 하이브리드 연결 tooas를 참조 합니다.  이 문서의 뒷부분에서 이에 대해 자세히 설명합니다.

### <a name="app-service-hybrid-connection-benefits"></a>App Service 하이브리드 연결의 장점 ###

이점 toohello 하이브리드 연결 기능 등의 여러 가지

- 앱이 온-프레미스 시스템 및 서비스에 안전하게 액세스할 수 있습니다.
- hello 기능에 액세스할 수 있는 인터넷 끝점 필요 하지 않습니다.
- 신속 하 고 쉽게 tooset를  
- 하이브리드 연결 각 일치 tooa 단일 호스트: 포트 조합으로 서 우수한 보안 기능
- 일반적으로 필요 하지 않습니다 방화벽 구멍 hello 연결은 표준 웹 포트를 통해 모든 아웃 바운드
- hello 기능은 hello 끝점에서 사용 하는 응용 프로그램 및 hello 기술에 사용 되는 알 수 없는 toohello 언어에 액세스할 수 있는 네트워크 수준 때문에
- 것이 단일 응용 프로그램에서 여러 네트워크에서 tooprovide 액세스 사용 

### <a name="things-you-cannot-do-with-hybrid-connections"></a>하이브리드 연결로 할 수 없는 작업 ###

하이브리드 연결로 할 수 없는 몇 가지 작업은 다음과 같습니다.

- 드라이브 탑재
- UDP 사용
- FTP 수동 모드 또는 확장 수동 모드 같은 동적 포트를 사용하는 TCP 기반 서비스에 액세스
- LDAP 지원(경우에 따라 UDP가 필요하므로)
- Active Directory 지원

## <a name="adding-and-creating-a-hybrid-connection-in-your-app"></a>앱에서 하이브리드 연결 추가 및 만들기 ##

Hello 앱 포털을 통해 또는 hello 하이브리드 연결 서비스 포털에서 하이브리드 연결을 만들 수 있습니다.  Hello 앱 포털 toocreate hello toouse 앱을 사용 하 여 원하는 하이브리드 연결을 사용 하는 것이 좋습니다.  하이브리드 연결 toocreate 이동 toohello [Azure 포털] [ portal] 하며 앱에 대 한 UI hello로 이동 합니다.  **네트워킹 > 하이브리드 연결 끝점 구성**을 선택합니다.  여기에서 응용 프로그램으로 구성 된 hello 하이브리드 연결을 확인할 수 있습니다.  

![][2]

새 하이브리드 연결을 tooadd 하이브리드 연결 추가 클릭 합니다.  UI가 열리면 hello 이미 만든 hello 하이브리드 연결을 나열 합니다.  그 중 하나 이상의 tooadd tooyour 앱을 클릭 하 고 적중 hello 것 **하이브리드 연결을 선택 하는 추가**합니다.  

![][3]

새 하이브리드 연결을 toocreate 클릭 **새 하이브리드 연결을 만들**합니다.  여기에서 다음을 지정합니다. 

- 끝점 이름
- 끝점 호스트 이름
- 끝점 포트
- 서비스 버스 네임 스페이스 원하는 toouse

![][4]

모든 하이브리드 연결이 동률된 tooa 서비스 버스 네임 스페이스 및 Azure 지역에서 각 서비스 버스 네임 스페이스는 합니다.  서비스 버스 네임 스페이스를 사용 하 여 tootry hello 앱와 동일한 지역 따라서 tooavoid 인 한 네트워크 대기 시간으로 유용 합니다.

앱에서 하이브리드 연결 tooremove 않으려면 마우스 오른쪽 단추로 클릭 하 고 선택 **연결 끊기**합니다.  

하이브리드 연결 tooyour 웹 앱에 추가 되 면 클릭 해도에 세부 정보를 볼 수 있습니다.  

![][5]

## <a name="hybrid-connections-and-app-service-plans"></a>하이브리드 연결 및 App Service 계획 ##

hello만 하이브리드 연결을 사용할 수 있습니다는 hello 새 하이브리드 연결 합니다.  하이브리드 연결은 기본, 표준, 프리미엄 및 격리 요금제 SKU에서만 사용할 수 있습니다.  연결 제한 toohello 계획 가격 책정 있습니다.  

| 요금제 | Hello 계획에서 사용할 수 있는 하이브리드 연결의 수 |
|----|----|
| Basic | 5 |
| Standard | 25 |
| Premium | 200 |
| 격리 | 200 |

또한 UI가 어떤 응용 프로그램 및 hello 하이브리드 연결 수를 사용 하는 것을 보여 주는 앱 서비스 계획의 앱 서비스 계획 제한 사항 때문입니다.  

![][6]

마찬가지로 hello 앱 보기를 볼 수 있습니다 세부 정보에서 하이브리드 연결 클릭 하 여.  Hello 앱 보기에서 사용 했던 모든 hello 정보를 볼 수 있지만 다른 응용 프로그램과 hello에서 확인할 수 여기에 표시 된 hello 속성에서 동일한 앱 서비스 계획 사용 하는 하이브리드 연결에 해당 합니다.

![][7]

앱 서비스 계획에 사용할 수 있는 하이브리드 연결 끝점 hello 수를 제한 하는 동안 개수에 관계 없이 해당 앱 서비스 계획의 앱에서 사용 되는 각 하이브리드 연결을 사용할 수 있습니다.  앱 서비스 계획에 5 개의 별도 앱에서 사용한 하이브리드 연결 1 한다면 되는 여전히 하나만 하이브리드 연결 toosay입니다.

추가 비용 toohybrid 연결 초과 되 고 Basic, Standard, Premium 또는 격리 된 SKU에서 사용할 수 있습니다.  하이브리드 연결 가격 책정에 대한 자세한 내용은 [Service Bus 가격 책정][sbpricing]을 참조하세요.

## <a name="hybrid-connection-manager"></a>하이브리드 연결 관리자 ##

하이브리드 연결 toowork 하려면에서 하이브리드 연결 끝점을 호스트 하는 hello 네트워크에서 릴레이 에이전트를 해야 합니다.  해당 릴레이 에이전트 hello 하이브리드 연결 관리자 (HCM) 라고 합니다.  이 도구는 hello에서 다운로드할 수 있습니다 **네트워킹 > 하이브리드 연결 끝점 구성** hello에서 응용 프로그램에서 사용할 수 있는 UI [Azure 포털][portal]합니다.  

이 도구는 Windows의 Windows Server 2008 R2 이상 버전에서 실행됩니다.  설치가 완료 되 면 hello HCM 서비스를 실행 합니다.  이 서비스는 hello 구성 된 끝점에 따라 tooAzure 서비스 버스 릴레이 연결 합니다.  HCM hello에서 hello 연결 80 및 443 아웃 바운드 tooports 됩니다.    

HCM hello에 UI tooconfigure 것입니다.  Hello HCM 설치 된 후 hello 하이브리드 연결 관리자 설치 디렉터리에서에 있는 HybridConnectionManagerUi.exe hello를 실행 하 여 hello UI 올 수 있습니다.  Windows 10에서는 검색 상자에 *Hybrid Connection Manager UI*를 입력하여 UI에 쉽게 액세스할 수 있습니다.  

참조는 hello HCM UI를 시작 하면 먼저 hello 경우 hello HCM의이 인스턴스와 함께 구성 된 hello 하이브리드 연결을 모두 나열 하는 테이블이 있습니다.  변경 내용을 toomake을 원하는 경우 Azure 사용한 tooauthenticate를 해야 합니다. 

tooadd 하나 또는 자세한 하이브리드 연결 tooyour HCM:

1. Hello HCM UI를 시작 합니다.
1. [Configure another hybrid connection](다른 하이브리드 연결 구성)을 클릭합니다. ![][8]

1. Azure 계정으로 로그인합니다.
1. 구독을 선택합니다.
1. 클릭이 HCM toorelay 원하는 hello 하이브리드 연결![][9]

1. 저장을 클릭합니다.

이 시점에서 추가한 hello 하이브리드 연결을 확인할 수 있습니다.  하이브리드 연결을 구성 하는 hello 클릭 하 고 hello 연결에 대 한 세부 정보를 볼 수도 있습니다.

![][10]

프로그램 HCM toobe 수 toosupport hello 하이브리드 연결의 구성 된 경우 필요 합니다.

- 포트 80 및 443을 통해 액세스 tooAzure TCP
- TCP 액세스 toohello 하이브리드 연결 끝점
- 기능 toodo DNS 모양 ups hello 끝점 호스트와 hello azure 서비스 버스 네임 스페이스에서

HCM hello hello 이전 BizTalk 하이브리드 연결을 새 하이브리드 연결 모두를 지원합니다.

### <a name="redundancy"></a>중복 ###

각 HCM은 여러 하이브리드 연결을 지원할 수 있습니다.  특정 하이브리드 연결이 여러 HCM에서 지원될 수도 있습니다.  hello 기본 동작은 tooround 로빈 트래픽의 hello 분산 지정 된 모든 끝점에 대해 HCMs 구성입니다.  네트워크에서 하이브리드 연결에 대한 고가용성이 필요한 경우에는 개별 컴퓨터에서 여러 HCM을 인스턴스화하면 됩니다. 

### <a name="manually-adding-a-hybrid-connection"></a>수동으로 하이브리드 연결 추가 ###

공유 하기 원하는 경우 다른 사람이 구독 toohost 외부에서 특정된 하이브리드 연결의 HCM 인스턴스 hello hello 하이브리드 연결에 대 한 게이트웨이 연결 문자열입니다.  하이브리드 연결 hello에 대 한 hello 속성에서 볼 수 있습니다 [Azure 포털][portal]합니다. 문자열, toouse 클릭 hello **수동으로 구성** hello HCM 단추를 선택한 hello 게이트웨이 연결 문자열에 붙여 넣습니다.


## <a name="troubleshooting"></a>문제 해결 ##

경우 실행 중인 응용 프로그램으로 하이브리드 연결 설정 된 해당 하이브리드 연결이 구성 되어 있는 하나 이상의 HCM는 힙이고 hello 상태는 예를 들어 **연결 됨** hello 포털에서입니다.  아니면 경우 **연결 됨** 는 앱 다운 되었거나 프로그램 HCM tooAzure 포트 80 또는 443에서 아웃 연결할 수 없는 것입니다.  

hello 클라이언트가 tootheir 끝점을 연결할 수 없습니다는 때문 DNS 이름 대신 IP 주소를 사용 하 여 지정 된 hello 끝점입니다.  응용 프로그램 hello 원하는 끝점에 도달할 수 없는 IP 주소를 사용 하는 경우 toousing hello hello HCM 실행 중인 호스트에 유효한 DNS 이름 전환 합니다.  다른 작업 toocheck 여기서 hello HCM 실행 되 고 hello hello HCM 실행 중인 호스트 toohello 하이브리드 연결 끝점에서에서 연결 하는 hello 호스트에서 해당 hello DNS 이름을 제대로 확인 됩니다.  

Hello tcpping 라는 hello 콘솔에서 호출 될 수 있는 응용 프로그램 서비스에에서는 도구입니다.  이 도구 액세스 tooa TCP 끝점을 포함 하는 경우 하지만 알려주지 않습니다 액세스 tooa 하이브리드 연결 끝점 있는지 알려 줄 수 있습니다.  하이브리드 연결 끝점에 대해 hello 콘솔에 사용 하면, 성공적인 ping만 알려 해당 호스트: 포트 조합 하 여 사용 하는 앱에 대해 구성 된 하이브리드 연결 합니다.  

## <a name="biztalk-hybrid-connections"></a>BizTalk 하이브리드 연결 ##

BizTalk 하이브리드 연결 기능을 이전 hello toofurther BizTalk 하이브리드 연결 만들기 오프 종료 되었습니다.  앱과 기존 BizTalk 하이브리드 연결을 사용 하 여 계속할 수 있지만 toohello 새 서비스를 마이그레이션해야 합니다.  Hello 간에 hello BizTalk 버전에 비해 hello 새 서비스의 이점은 다음과 같습니다.

- 추가 BizTalk 계정이 필요하지 않습니다.
- BizTalk 하이브리드 연결에서 TLS는 1.0이 아닌 1.2입니다.
- 통신은 포트 80 및 443 IP 주소 대신 DNS 이름 tooreach Azure와 추가의 범위를 사용 하 여 다른 포트입니다.  

BizTalk 하이브리드 연결 tooyour 앱, tooadd hello에서는 이동 tooyour app [Azure 포털] [ portal] 클릭 **네트워킹 > 하이브리드 연결 끝점 구성**합니다.  Hello 클래식 하이브리드 연결 테이블에서 클릭 **클래식 하이브리드 연결을 추가할**합니다.  여기에 BizTalk 하이브리드 연결 목록이 표시됩니다.  


<!--Image references-->
[1]: ./media/app-service-hybrid-connections/hybridconn-connectiondiagram.png
[2]: ./media/app-service-hybrid-connections/hybridconn-portal.png
[3]: ./media/app-service-hybrid-connections/hybridconn-addhc.png
[4]: ./media/app-service-hybrid-connections/hybridconn-createhc.png
[5]: ./media/app-service-hybrid-connections/hybridconn-properties.png
[6]: ./media/app-service-hybrid-connections/hybridconn-aspproperties.png
[7]: ./media/app-service-hybrid-connections/hybridconn-hcm.png
[8]: ./media/app-service-hybrid-connections/hybridconn-hcmadd.png
[9]: ./media/app-service-hybrid-connections/hybridconn-hcmadded.png
[10]: ./media/app-service-hybrid-connections/hybridconn-hcmdetails.png

<!--Links-->
[HCService]: http://docs.microsoft.com/azure/service-bus-relay/relay-hybrid-connections-protocol/
[portal]: http://portal.azure.com/
[oldhc]: http://docs.microsoft.com/azure/biztalk-services/integration-hybrid-connection-overview/
[sbpricing]: http://azure.microsoft.com/pricing/details/service-bus/


---
title: "Azure 가상 네트워크를 사용 하 여 앱 aaaIntegrate"
description: "표시 하는 tooconnect Azure 앱 서비스 tooa 새로운 또는 기존 Azure 가상 네트워크에 응용 프로그램"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: 90bc6ec6-133d-4d87-a867-fcf77da75f5a
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: ccompy
ms.openlocfilehash: a93c504481400245b02220b541a008a7c874d10a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-app-with-an-azure-virtual-network"></a>Azure 가상 네트워크에 앱 통합
이 문서는 hello Azure 앱 서비스 가상 네트워크 통합 기능에 설명 하 고 표시 방법을 tooset에서 앱과 파일 작업을 [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)합니다. Azure 가상 네트워크 (Vnet) 모르는 경우 이것이 tooplace에 대 한 다양 한 사용자가 제어 하는 인터넷이 아닌 routeable 네트워크에 Azure 리소스가 액세스를 허용 하는 기능입니다. 이러한 네트워크 연결된 tooyour 온-프레미스 네트워크의 여러 VPN 기술 사용 하 여 수 있습니다. Azure 가상 네트워크에 대 한 자세한 toolearn 여기 정보 hello로 시작: [Azure 가상 네트워크 개요][VNETOverview]합니다. 

hello Azure 앱 서비스에는 다음 두 가지 있습니다. 

1. 가격 책정 모델의 전체 범위 hello 지원 hello 다중 테 넌 트 시스템
2. hello 앱 서비스 환경 (ASE) 프리미엄 기능을 VNet에 배포 합니다. 

이 문서는 App Service 환경이 아니라 VNet 통합 과정에 대해 설명합니다. 여기에 hello 정보로 시작 하는 hello ASE 기능에 대 한 자세한 toolearn 하려는 경우: [앱 서비스 환경 소개][ASEintro]합니다.

VNet 통합 하면 웹 응용 프로그램 액세스 tooresources 가상 네트워크에 있지만 hello 가상 네트워크에서 tooyour 웹 앱 전용 액세스를 부여 하지 않습니다. 개인 사이트 액세스 toomaking만 개인 네트워크와 같은 Azure 가상 네트워크 내에서 액세스할 수 있는 앱을 참조합니다. 개인 사이트 액세스는 ILB(내부 부하 분산 장치)로 ASE가 구성된 상태에서만 사용할 수 있습니다. 에 대 한 내용은 ILB ASE를 사용 하 여, 문서 hello로 시작: [만들기 및 ILB ASE를 사용 하 여][ILBASE]합니다. 

VNet 통합 사용 되는 일반적인 시나리오는 웹 응용 프로그램 tooa 데이터베이스 또는 Azure 가상 네트워크에 가상 컴퓨터에서 실행 되는 웹 서비스에서 액세스를 사용 하도록 설정 합니다. VNet 통합을 VM에 응용 프로그램에 대 한 공용 끝점 tooexpose 필요 하지는 않지만 hello 개인-인터넷 라우팅 가능한 주소를 대신 사용할 수 있습니다. 

hello VNet 통합 기능:

* 표준, 프리미엄 또는 격리 요금제가 필요합니다. 
* 클래식 또는 Resource Manager VNet에서 작동합니다. 
* TCP 및 UDP를 지원합니다.
* 웹, 모바일, API 앱에서 작동합니다.
* 응용 프로그램 tooconnect tooonly 1을 사용 하면 한 번에 VNet
* toofive Vnet toobe에 통합 된 앱 서비스 계획을 사용 하도록 설정 
* 앱 서비스 계획의 여러 앱에서 사용 하는 동일한 VNet toobe hello 허용
* VNet 게이트웨이 hello에서 toohello SLA 인해 SLA는 99.9%를 지원합니다.

VNet 통합이 지원하지 않는 사항에는 다음과 같은 내용이 포함됩니다.

* 드라이브 탑재
* AD 통합 
* NetBios
* 개인 사이트 액세스

### <a name="getting-started"></a>시작
웹 앱 tooa 가상 네트워크를 연결 하기 전에 염두에 일부의 tookeep가:

* VNet 통합은 **표준**, **프리미엄** 또는 **격리** 요금제에 속하는 앱에서만 작동합니다. 계획 가격 책정 hello 기능을 활성화 하 고 다음 지원 되지 않는 한 앱 서비스 계획 tooan 프로그램를 확장 하는 경우 앱 손실 자신의 연결 toohello Vnet을 사용 하는 합니다. 
* 대상 가상 네트워크가 이미 있는 경우 연결 된 tooan 앱 수 전에 동적 라우팅 게이트웨이 통해 사용 하도록 설정 하는 지점-사이트 VPN 있어야 합니다. 게이트웨이가 정적 라우팅을 사용하도록 구성된 경우에는 지점 및 사이트 간 VPN(가상 사설망)을 사용하도록 설정할 수 없습니다.
* hello VNet에에서 있어야 hello 응용 프로그램 서비스 Plan(ASP)와 같은 구독 합니다. 
* VNet와 통합 하는 hello 앱 hello 해당 VNet에 대해 지정 된 DNS를 사용 합니다.
* 기본적으로 통합 앱에 VNet을 VNet에 정의 된 hello 경로에 따라 트래픽을 라우팅합니다. 

## <a name="enabling-vnet-integration"></a>VNet 통합 사용
주로에서 VNet 통합에 대 한 hello Azure 포털을 사용 하 여이 문서는 데 사용 됩니다. PowerShell을 사용 하 여 응용 프로그램과 함께 VNet 통합 tooenable 지시를 따른 hello 여기: [PowerShell을 사용 하 여 응용 프로그램 tooyour 가상 네트워크 연결][IntPowershell]합니다.

Hello 옵션 tooconnect 앱 tooa 새로운 또는 기존 가상 네트워크가 해야합니다. 통합의 일부로 새로운 네트워크를 만들면 다음 또한 VNet hello toojust 만들기, 동적 라우팅 게이트웨이를 미리 구성 된 및 지점 tooSite VPN을 사용 합니다. 

> [!NOTE]
> 새 가상 네트워크를 구성하려면 몇 분 정도 걸릴 수 있습니다. 
> 
> 

VNet 통합 tooenable 앱 설정을 열고 네트워킹을 선택 합니다. UI가 열리면 hello에는 세 가지 네트워킹 선택할 수 있습니다. 이 가이드에서는 VNet 통합에서 하이브리드 연결까지만 다루고 App Service 환경은 이 문서의 뒤쪽에서 다루겠습니다. 

응용 프로그램 계획 가격 책정 올바른 hello에 없는 경우 UI hello 하면 tooscale 높을수록 선택한 계획 가격 책정에 계획 tooa 있습니다.

![][1]

### <a name="enabling-vnet-integration-with-a-pre-existing-vnet"></a>기존 VNet을 사용하여 VNet 통합 사용
hello VNet 통합 UI Vnet의 목록에서 tooselect이 있습니다. hello 클래식 Vnet 괄호 다음 toohello VNet 이름에 "기본" hello 단어로 하 등을 표시 합니다. hello 목록이 정렬는 hello 리소스 관리자 Vnet이 먼저 나열 됩니다. Hello 있습니다 아래에 표시 된 이미지 하나만 VNet을 선택할 수 있습니다. 있음을 알 수 있습니다. VNet이 회색으로 표시되는 이유는 다양하며 다음과 같은 경우가 이유에 포함됩니다.

* 계정에 액세스할 수 있는 다른 구독에는 VNet hello
* hello VNet에 지점 tooSite 사용할 수 없습니다
* hello VNet 동적 라우팅 게이트웨이 없습니다.

![][2]

hello와 toointegrate 원하는 VNet tooenable 통합 클릭 하세요. Hello VNet을 선택한 후 앱 hello 변경 tootake 효과 대 한 자동으로 다시 시작 됩니다. 

##### <a name="enable-point-toosite-in-a-classic-vnet"></a>클래식 VNet에 지점 tooSite를 사용 하도록 설정
VNet에 게이트웨이가 없는 nor 지점 tooSite에, 다음 있으면 tooset 상태는 첫 번째입니다. 클래식 VNet에 대 한이 이동 toodo toohello [Azure 포털] [ AzurePortal] 가상 Networks(classic) 목록이 hello 표시 합니다. 여기에서 hello 네트워크와 toointegrate 누르고 원하는 hello 큰 상자의 Essentials VPN 연결을 호출에서 클릭 합니다. 여기에서 지점 toosite VPN 만들고도 하 게 게이트웨이 만들 수 있습니다. 게이트웨이 만들기 experience와 함께 hello 지점 toosite를 통과 한 후에 준비가 될 때까지 약 30 분입니다. 

![][8]

##### <a name="enabling-point-toosite-in-a-resource-manager-vnet"></a>리소스 관리자 VNet에 지점 tooSite를 사용 하도록 설정
리소스 관리자 VNet 게이트웨이 및 지점 tooSite tooconfigure 사용할 수 있습니다 PowerShell 명시 여기서 [지점 및 사이트 연결 tooa 가상 네트워크 구성 PowerShell을 사용 하 여] [ V2VNETP2S] Azure 포털 hello를 설명 하는 대로 여기 사용 또는 [Azure 포털 hello 지점 및 사이트 연결 tooa VNet 사용 하는 구성][V2VNETPortal]합니다. hello UI tooperform이이 기능은 아직 사용할 수 없는 경우 Note hello 지점 tooSite 구성 toocreate 인증서 필요 합니다. 프로그램 WebApp toohello VNet을 연결할 때 자동으로 구성 됩니다. 

### <a name="creating-a-pre-configured-vnet"></a>미리 구성된 VNet 만들기
하려는 경우 새 VNet 게이트웨이 및 지점-사이트를 사용 하 여 구성한 toocreate hello UI 네트워킹 앱 서비스는 hello 기능 toodo 해당 있지만 리소스 관리자 VNet에 대해서만 합니다. 게이트웨이 통해 클래식 VNet과 지점 및 사이트 toocreate을 원할 경우 다음 해야 toodo이 수동으로 hello 네트워킹 사용자 인터페이스를 통해. 

toocreate hello VNet 통합 UI를 통해 리소스 관리자 VNet 선택 하기만 하면 **새 가상 네트워크 만들기** 하 고 제공 된:

* 가상 네트워크 이름
* 가상 네트워크 주소 블록
* 서브넷 이름
* 서브넷 주소 블록
* 게이트웨이 주소 블록
* Point to Site(지점과 사이트 간) 주소 블록

다른 네트워크가 VNet tooconnect tooany 원하는 이러한 네트워크와 겹치는 IP 주소 공간을 선택 하지 않아야 하 합니다. 

> [!NOTE]
> 게이트웨이 통해 리소스 관리자 VNet 만들기 30 분 정도 소요 이며 현재 응용 프로그램과 함께 hello VNet 통합 되지 않습니다. VNet hello 게이트웨이 사용 하 여 만든 후에 VNet 통합 UI toocome 백 tooyour 앱이 필요한 고 새 VNet을 선택 합니다.
> 
> 

![][3]

Azure VNet은 일반적으로 개인 네트워크 주소 내에 만들어집니다. 기본 hello VNet 통합 하 여 기능에는 VNet에 해당 IP 주소 범위에 대 한 전송 하는 모든 트래픽을 라우팅합니다. hello 개인 IP 주소 범위는.

* -이 hello 동일 10.0.0.0으로-10.0.0.0/8 10.255.255.255
* -이 hello 동일 172.16.0.0로-172.16.0.0/12 172.31.255.255 
* -이 hello 동일 192.168.0.0로-192.168.0.0/16 192.168.255.255

VNet 주소 공간 hello toobe CIDR 표기법으로 지정 해야 합니다. CIDR 표기법에 익숙하지 경우 IP 주소 및 hello 네트워크 마스크를 나타내는 정수를 사용 하 여 주소 블록을 지정 하는 방법을입니다. 참고로, 10.1.0.0/24는 256개의 주소가 되고 10.1.0.0/25는 128개의 주소가 됩니다. /32를 포함하는 IPv4 주소는 1개의 주소입니다. 

여기서 hello DNS 서버 정보를 설정한 경우 VNet에 대 한 설정 됩니다입니다. VNet 생성 후 hello VNet 사용자 환경에서이 정보를 편집할 수 있습니다. Hello hello VNet의 DNS를 변경 하면 tooperform 동기화 네트워크 작업을 할 수 있습니다.

Hello에 VNet 생성 hello VNet 통합 UI를 사용 하 여 클래식 VNet을 만들 때 응용 프로그램으로 동일한 리소스 그룹입니다. 

## <a name="how-hello-system-works"></a>Hello 시스템 작동 하는 방법
Hello에서는이 기능을 기반으로 구축 기술 tooconnect 지점-사이트 VPN 사용자 앱 tooyour VNet입니다. Azure App Service에 속하는 앱은 VNet에서 앱을 바로 프로비저닝 할 수 없도록 하는(가상 컴퓨터를 통해 수행되기 때문에) 다중 테넌트 시스템 아키텍처를 갖습니다. 지점 및 사이트 기술에 구축 하 여 네트워크 액세스 toojust hello 가상 컴퓨터 호스팅 hello 앱 제한. 앱 구성 하 tooaccess hello 네트워크만 액세스할 수 있도록 해당 응용 프로그램 호스트에 액세스 toohello 네트워크 더욱 제한 됩니다. 

![][4]

가상 네트워크와 DNS 서버를 구성 하지 않았으면 앱 toouse IP 주소 tooreach hello VNet의에서 리소스를 해야 합니다. IP 주소를 사용 하는 동안이 기능의 주요 장점은 hello 인지 수 있다는 toouse hello 개인 네트워크 내에서 개인 주소를 기억 합니다. 설정한 경우 toouse 앱 공용 IP 주소, Vm 중 하나에 대 한를 통해 통신 하 고 hello VNet 통합 기능을 사용 하지 않는 한 다음 인터넷 hello 합니다.

## <a name="managing-hello-vnet-integrations"></a>Hello VNet 통합 관리
기능 tooconnect hello 및 tooa VNet이 응용 프로그램 수준에서 연결을 끊습니다. ASP 수준에서 여러 앱에서 VNet 통합 hello에 영향을 줄 수 있는 작업은 합니다. Hello hello 앱 수준에서 표시 되는 UI에서에서 VNet에 세부 정보를 가져올 수 있습니다. 대부분은 동일한 정보는 또한 부분에 표시 된 hello ASP 수준 hello 합니다. 

![][5]

Hello 네트워크 기능 상태 페이지에서 앱에 연결 된 VNet tooyour 인지 확인할 수 있습니다. 무슨 이유로든 VNet 게이트웨이가 다운되어 있으면 연결 안 됨으로 표시됩니다. 

hello 정보 수준 VNet 통합 UI는 동일 hello ASP에서에서 받아야 하는 hello 세부 정보로 hello hello 응용 프로그램에서 사용할 수 있는 tooyou 생깁니다. 해당 항목은 다음과 같습니다.

* VNet 이름-이 링크 hello Azure 가상 네트워크 UI 엽니다.
* 위치 – VNet의 hello 위치를 반영합니다. 것과 다른 위치에 VNet 가능한 toointegrate 합니다.
* 인증서 상태-hello 앱 및 VNet hello 사이 사용 되는 인증서 toosecure hello VPN 연결이 있습니다. 이 동기화 되어 테스트 tooensure를 반영 합니다.
* 게이트웨이 상태-프로그램 게이트웨이 있을 거 야 어떤 이유로 든 다음 응용 프로그램에 액세스할 수 없습니다 hello VNet의에서 리소스입니다. 
* VNet 주소 공간-VNet에 대 한 hello IP 주소 공간입니다. 
* 지점 tooSite 주소 공간-VNet에 대 한 hello 지점 toosite IP 주소 공간입니다. 앱이 주소 공간에서 Ip hello 중 하나에서 오는 것으로 통신을 보여 줍니다. 
* 사이트 toosite 주소 공간-사이트 tooSite Vpn tooconnect 사용할 수 있습니다 VNet tooyour 온-프레미스 리소스 또는 VNet tooother 합니다. 으로 정의 된 hello IP 범위에 VPN 연결 여기 표시 한 다음을 구성 해야 합니다.
* DNS 서버 - DNS 서버에 VNet이 구성되어 있으면 여기에 목록이 표시됩니다.
* Ip toohello VNet-는 VNet에 대해 정의 된 라우팅에 IP 주소의 목록이 라우팅되고 해당 주소 여기에 표시 합니다. 

응용 프로그램에 현재 연결 되어 VNet hello toodisconnect는 하는 hello 작업만에서 VNet 통합의 앱 뷰 hello 취할 수 있습니다. toodo hello 위쪽에이 클릭 하 여 분리 합니다. 이 동작은 VNet을 변경하지 않습니다. VNet hello와 hello 게이트웨이 포함 하 여 해당 구성을 변경 되지 않습니다. 다음 원하는 toodelete VNet 경우 toofirst delete hello 리소스가 hello 게이트웨이 포함 해야 합니다. 

앱 서비스 계획 보기 hello에 추가 작업의 수 있습니다. 그는 또한 다르게 보다 hello 응용 프로그램에서 액세스 합니다. tooreach hello ASP 네트워킹 UI는 단순히 ASP UI 및 아래로 스크롤하여 엽니다. Network Feature Status(네트워크 기능 상태)라는 UI 요소가 있습니다. VNet 통합에 대해 일부 세부 정보를 제공합니다. 이 UI 클릭 하면 네트워크 기능 상태 UI hello를 열립니다. 그런 다음 클릭이 ASP에서 VNet 통합 열립니다 hello를 나열 하는 UI hello on "여기 toomanage"를 클릭 합니다.

![][6]

hello hello ASP 위치가 좋은 tooremember hello와 통합 하는 Vnet의 hello 위치에서 찾을 때입니다. Hello VNet은 다른 위치에서 모두 toosee 대기 시간 문제는 경우가 더 많습니다. 

hello와 통합 하는 Vnet은 앱이이 ASP 및 수 포함 된 개수에 통합 된 개수 Vnet에 미리 알림입니다. 

toosee 각 VNet을 VNet에 관심이 있는 hello 클릭 하기만에 세부 정보를 추가 합니다. 또한 앞에서 기록한 된 toohello 자세히가이 ASP에서 해당 VNet을 사용 하는 hello 앱 목록을 참고할 수 있습니다. 

와 관련 없는 tooactions는 두 개의 기본 작업입니다. hello에는 먼저 앱에서 VNet에 나가는 트래픽에 드라이브는 hello 기능 tooadd 경로입니다. hello 두 번째 동작은 hello 기능 toosync 인증서 및 네트워크 정보 합니다.

![][7]

**라우팅** VNet에 정의 된 hello 경로 앱에서 VNet에 트래픽을 전송 하는 데 사용 되는 것은 설명한 것 처럼 합니다. 고객 풀려면 toosend 추가 아웃 바운드 트래픽이 앱에서 VNet hello 및 하이 기능은 있지만 몇 가지 사용은. 어떤 일이 생기 toohello 트래픽 toohow hello 고객을 한 후 해당 VNet을 구성 합니다. 

**인증서** hello 인증서 상태 hello 앱 서비스 toovalidate hello VPN 연결에 대 한 사용 하는 hello 인증서 여전히 양호한 지에서 수행 중인 검사를 반영 합니다. VNet 통합을 사용 하도록 설정 하면 이것이 hello 첫 번째 통합 toothat VNet이이 ASP에서 모든 앱에서 사용 하는 hello 연결 tooensure hello 보안 인증서에 필요한 교환을. Hello 인증서와 함께 hello DNS 구성, 경로 및 hello 네트워크를 설명 하는 다른 유사한 작업을 확보 했습니다.
이러한 인증서 또는 네트워크 정보를 변경 하는 경우 "동기화 Network" tooclick을 할 수 있습니다. **참고**: “네트워크 동기화”를 클릭하면 앱과 VNet 간의 연결이 잠시 중단됩니다. 응용 프로그램을 다시 시작 하는 동안 연결이 끊어진 hello 사이트 toonot 함수 제대로 발생할 수 있습니다. 

## <a name="accessing-on-premises-resources"></a>온-프레미스 리소스 액세스
Hello VNet 통합 기능의 hello 이점 중 하나입니다는 VNet에 연결 되어 있는 경우 tooyour 온-프레미스 사이트 tooSite VPN 사용 하 여 네트워크 이면 응용 프로그램에서 응용 프로그램에서 tooyour 온-프레미스 리소스에 액세스를 가질 수 있습니다. 이 toowork에 대 한 tooupdate 할 수 있지만 hello로 온-프레미스 VPN 게이트웨이 지점 tooSite IP 범위에 대 한 라우팅합니다. Hello 사이트 tooSite VPN 설정 되 면 먼저 hello 스크립트 사용 tooconfigure 지점 tooSite VPN을 포함 하 여 경로를 설정 해야 합니다. 사용자 사이트 tooSite VPN을 만든 후 hello 지점 tooSite VPN을 추가 하면 다음 필요한 tooupdate hello 경로 수동으로 합니다. 게이트웨이 당 다 없고 되지 않은 toodo 여기서 설명 하는 방법에 대 한 세부 정보입니다. 

> [!NOTE]
> hello VNet 통합 기능에는 express 경로 게이트웨이 된 VNet와 앱을 통합 되지 않습니다. Express 경로 게이트웨이 hello에 구성 된 경우에 [공존 모드] [ VPNERCoex] hello VNet 통합 작동 하지 않습니다. ExpressRoute 연결을 통해 tooaccess 자원이 필요한 경우 사용할 수 있습니다는 [앱 서비스 환경][ASE], VNet에서를 실행 합니다.
> 
> 

## <a name="pricing-details"></a>가격 정보
몇 가지 가격 갖는 hello VNet 통합 기능을 사용할 때 주의 해야 합니다. 3 관련 한 요금이 있습니다 toohello이이 기능을 사용 합니다.

* ASP 가격 책정 계층 요구 사항
* 데이터 전송 비용
* VPN 게이트웨이 비용

앱 toobe 수 toouse에 대 한이 기능에 필요한 표준 또는 프리미엄 앱 서비스 계획에서 toobe 합니다. 해당 비용에 대한 자세한 정보는 [App Service 가격][ASPricing]을 참조하세요. 

Toohello 방식으로 처리 되는 Vpn 지점 tooSite 인해 항상 충전에 대해 싶은 의견이 VNet 통합 연결을 통해 아웃 바운드 데이터 hello VNet에 있더라도 hello 동일 데이터 센터입니다. toosee 이러한 요금, 여기를 보십시오: [데이터 전송 가격 정보][DataPricing]합니다. 

hello 마지막 항목에는 VNet 게이트웨이 hello hello 비용입니다. 사이트 tooSite Vpn 등 다른 작업에 대 한 hello 게이트웨이 필요가 없는 경우 다음 결제 하는 게이트웨이 toosupport hello VNet 통합 기능에 대 한 합니다. 해당 비용에 대한 자세한 정보는 [VPN 게이트웨이 가격][VNETPricing]을 참조하세요. 

## <a name="troubleshooting"></a>문제 해결
Hello 기능을 쉽게 tooset 상태인 동안 경험 무료 문제가 된다는 아닙니다. Tootest 연결 hello 응용 프로그램 콘솔에서 사용할 수는 몇 가지 유틸리티를 있습니다 원하는 끝점에 액세스 하는 문제는 발생할 경우입니다. 두 가지 콘솔 환경을 사용할 수 있습니다. 하나는 hello Kudu 콘솔에서 고 hello 다른는 hello Azure 포털에에서 도달할 수 있는 hello 콘솔. 앱에서 tooget toohello Kudu 콘솔 tooTools Kudu->로 이동 합니다. 동일 너무 이동으로 hello은이 [sitename]. scm.azurewebsites.net 합니다. 해당 열립니다는 toohello 디버그 콘솔 탭 tooget toohello Azure 포털 호스팅된 콘솔 응용 프로그램에서 다음 이동 되 면 tooTools 콘솔-> 합니다. 

#### <a name="tools"></a>도구
도구 ping을 hello, nslookup 및 tracert toosecurity 제약 조건 때문 hello 콘솔을 통해 작동 하지 않습니다. toofill hello void 있는 두 개의 별도 도구 추가 되었습니다. 주문 tootest DNS 기능 nameresolver.exe 라는 도구를 추가 했습니다. hello 구문은 다음과 같습니다.

    nameresolver.exe hostname [optional: DNS Server]

응용 프로그램에 따라 달라 지 nameresolver toocheck hello 호스트 이름을 사용할 수 있습니다. 이러한 방식으로 액세스 tooyour DNS 서버가 없거나 아마도 전혀 DNS를 사용 하 여 잘못 구성 하는 경우 테스트할 수 있습니다.

hello 다음 도구 TCP 연결 tooa 호스트 및 포트 조합에 대 한 tootest이 있습니다. 이 도구는 tcpping.exe 이라고 하며 hello 구문:

    tcpping.exe hostname [optional: port]

특정 호스트 및 포트를 연결할 수 경우 hello tcpping 유틸리티에서 알 수 있습니다. 만 표시할 수 있어 성공 하는 경우: hello 호스트 및 포트 조합에서 수신 대기 하는 응용 프로그램이 고 응용 프로그램 toohello 지정 된 호스트 및 포트에서 네트워크 액세스 권한이 있습니다.

#### <a name="debugging-access-toovnet-hosted-resources"></a>호스트 된 리소스 액세스 tooVNet 디버깅
특정 호스트와 포트에 앱이 도달하지 못하도록 방해할만한 요소는 많이 있습니다. 대부분의 hello 다음 세 가지 작업 중 하나입니다.

* **Hello에 방화벽이 있는 방식으로** hello 방식에서 방화벽이 있는 hello TCP 시간 제한 도달 합니다. 즉, 이 경우 21초입니다. Hello tcpping 도구 tootest 연결 기능을 사용 합니다. TCP 시간 제한 인해 방화벽 외 toomany 작업 수는 있지만 시작 합니다. 
* **DNS에 액세스할 수 없는** hello DNS 제한 시간은 DNS 서버 당 3 초입니다. 두 DNS 서버를 설정한 경우 hello timeout은 6 초입니다. DNS가 작동 하는 경우 nameresolver toosee를 사용 합니다. 기억 hello VNet 구성 된 DNS를 사용 하지 않는 nslookup을 사용할 수 없습니다.
* **잘못 된 P2S IP 범위** hello 지점 toosite IP 범위 toobe hello RFC 1918 개인 IP 범위에 필요한 (10.0.0.0-10.255.255.255 / 172.16.0.0-172.31.255.255 / 192.168.0.0-192.168.255.255). Hello 범위에서는 Ip는 외부에서 작업이 작동 하지 않습니다. 

해당 항목에서 문제를 선택 하지 않는 등의 단순한 작업 hello에 대 한 첫 번째 확인 합니다. 

* Hello 포털에 위쪽에 있는 것으로 표시 되는 게이트웨이 hello?
* 인증서가 동기화된 상태로 표시되나요?
* 모든 사용자가 변경한 hello 네트워크 구성에 영향을 받는 hello Asp "동기화 Network"를 수행 하지 않고? 

게이트웨이가 다운되어 있으면 다시 가동시킵니다. 인증서 동기화 되지 않은 경우 다음의 VNet 통합 toohello ASP 보기 이동한 다음 "동기화 Network"에 도달 합니다. 변경 내용을 tooyour VNet 구성이 되었습니다 및 동기화 되지 않은 것으로 의심 되 면이 때와이 일시적인 가동 중지 VNet 연결 및 앱으로 인해, 다음 이동 toohello ASP 수준의 VNet 통합 및 알림으로 "동기화 Network" Just 적중 Asp, . 

모든 것은 문제가 없지만에 대해서는 조금 더 깊은 toodig이 필요 있습니다.

* 있는 다른 앱에서 VNet 통합 tooreach 리소스를 사용 하 여 hello 동일한 VNet? 
* 수 toohello 응용 프로그램 콘솔 이동 하 고 tcpping tooreach 다른 리소스 VNet에 사용? 

위의 hello 중 하나에 해당할 경우 다음 VNet 통합 괜 찮으 며 hello 문제는 다른 곳입니다. 이 한 양상 toobe 챌린지 중 호스트: 포트를 연결할 수 없는 이유 없는 간단한 방법을 toosee 있기 때문입니다. Hello 원인 중 일부는 다음과 같습니다.

* 지점 toosite IP 범위 내에서 액세스 toohello 응용 프로그램 포트 인해 호스트를 방화벽을 만들 있습니다. 보통 교차 서브넷에는 공용 액세스가 필요합니다.
* 대상 호스트가 다운되었습니다.
* 응용 프로그램이 다운되었습니다.
* hello 잘못 된 IP 또는 호스트 이름에
* 응용 프로그램이 예상치 않은 다른 포트를 수신 대기 중입니다. Hello cmd 프롬프트에서 해당 호스트로 이동 "netstat-aon"를 사용 하 여 확인할 수 있습니다. 이렇게 하면 어떤 포트에 어떤 프로세스 ID가 수신 대기 중인지를 보여줍니다. 
* 액세스 tooyour 응용 프로그램 호스트와 지점 toosite IP 범위 내에서 포트를 방지 하는 방식으로 구성 된 네트워크 보안 그룹

앱 사용 하므로 hello 전체 범위에서 tooallow 액세스 해야 하는 지점 tooSite IP 범위에 어떤 IP를 알지 못하는 기억 합니다. 

추가적인 디버그 단계에는 다음 내용이 포함됩니다.

* 로그온 다른 VM VNet 및 시도 tooreach에서 리소스 호스트: 포트에서. 이러한 용도로 사용할 수 있는 TCP ping 유틸리티가 있고 필요한 경우에는 telnet을 사용할 수도 있습니다. hello 여기서는 정당한 toodetermine 연결에서 다른 VM이 중지 되지 않은 경우입니다. 
* 다른 VM에서 응용 프로그램 (를) 실행 하 고 액세스 toothat 호스트 및 포트 hello 콘솔에서 응용 프로그램에서 테스트

#### <a name="on-premises-resources"></a>온-프레미스 리소스 ####
앱 리소스 온-프레미스에 연결할 수 없으면, 다음 hello가 가장 먼저 확인 해야 하는 경우 VNet의 리소스에 도달할 수 있습니다. 연결이 되 면 hello VNet에에서 VM에서 tooreach hello 온-프레미스 응용 프로그램을 시도 하십시오. telnet 또는 TCP ping 유틸리티를 사용할 수 있습니다. VM에서 온-프레미스 리소스에 접속할 수 없으면 사이트 tooSite VPN 연결이 작동 하는지 확인 합니다. 이 작동 하는 경우에 hello 온-프레미스 게이트웨이 구성 및 상태 뿐만 아니라 앞에서 기록한 작업 hello를 확인 합니다. 

이제 VNet 호스팅되는 경우 VM에는 온-프레미스 시스템에 연결할 수 있지만 hello 이유 hello 다음 중 하나일 것은 응용 프로그램 수 없습니다.

* 프로그램 경로에서 온-프레미스 게이트웨이 지점 toosite IP 범위와 구성 되어 있지 않습니다.
* 네트워크 보안 그룹 지점 tooSite IP 범위에 대 한 액세스 차단
* 온-프레미스 방화벽 지점 tooSite IP 범위에서 트래픽을 차단합니다
* 사용자 정의 Route(UDR) 기반 지점 tooSite 트래픽을 온-프레미스 네트워크에 도달 하지 않도록 설정 하 여 VNet에 있는

## <a name="hybrid-connections-and-app-service-environments"></a>하이브리드 연결 및 앱 서비스 환경
TooVNet 호스트 리소스에 액세스할 수 있도록 하는 세 가지 기능이 있습니다. 아래에 이 계정과 키의 예제가 나와 있습니다.

* VNet 통합
* 하이브리드 연결
* 앱 서비스 환경

하이브리드 연결 tooinstall 릴레이 에이전트 네트워크에 하이브리드 연결 Manager(HCM) hello를 호출 해야 합니다. HCM hello toobe 수 tooconnect tooAzure 및 tooyour 응용 프로그램에 필요합니다. 이 솔루션은 인터넷 액세스가 가능한 끝점을 필요로 하지 않기 때문에, 온-프레미스 네트워크 또는 다른 클라우드 호스팅 네트워크 같은 원격 네트워크에 특히 유용합니다. HCM hello Windows에서 실행 한 tooprovide 고가용성 실행 toofive 인스턴스를 만들 수 있습니다. 하이브리드 연결만 지원 TCP 하지만 하 고 각 hc가 끝점에 toomatch tooa 특정 호스트: 포트 조합입니다. 

hello 앱 서비스 환경 기능 VNet에 toorun hello Azure 앱 서비스의 인스턴스를 허용 합니다. 이를 통해 앱은 추가적인 단계 없이 VNet의 리소스에 액세스할 수 있습니다. 일부의 hello 앱 서비스 환경 이점도로 too14 GB의 RAM을 기반으로 Dv2 근로자를 사용할 수 있습니다. 또 다른 이점은 수를 조정 하 hello 시스템 toomeet 요구 사항입니다. Hello 다중 테 넌 트 환경 위치 하면 ASP 제한 too20 인스턴스, 달리 ASE에 too100 ASP 인스턴스를 확장할 수 있습니다. VNet 통합 하지 않는 ASE를 hello 작업 중 하나는 앱 서비스 환경 ExpressRoute VPN 작업할 수 있는입니다. 

몇 가지 사용 사례 중첩은 이러한 기능 중 바꿀 수 hello 다른 사용자입니다. 어떤 기능 toouse은 동률된 tooyour 요구 사항을 알아야 합니다. 예:

* Azure에서 사이트 toorun 하기를 원할 한 되는 개발자 인 경우 hello 쉬운 일 toouse은 하이브리드 연결 hello 데이터베이스 사용자의 데스크에서 hello 워크스테이션에 액세스 합니다. 
* Tooput를가 하는 대규모 조직에 많은 수 hello 공용 클라우드에서 웹 속성의 네트워크에서이 관리 하는 경우 앱 서비스 환경 hello로 toogo를 할 수 있습니다. 
* 앱 서비스의 많은 경우 응용 프로그램을 호스트 하 고 VNet의 tooaccess 리소스 하기를 원할를 다음 VNet 통합 hello 방식으로 toogo. 

초과 hello 사용 사례는 몇 가지 간단한 설명을 관련 측면입니다. VNet이 이미 연결 되어 있으면 tooyour 온-프레미스 VNet 통합을 사용 하 여 네트워크 또는 앱 서비스 환경 쉬운 방법 tooconsume 온-프레미스 리소스입니다. Hello에 VNet 없으면 다른 손 것이 더 많은 오버 헤드 tooset 사이트 toosite VNet과 VPN hello HCM 설치와 비교 하는 많은 tooyour 온-프레미스 네트워크를 연결 합니다. 

Beyond 기능 차이 hello, 있습니다 차이점 가격도 됩니다. hello 앱 서비스 환경 기능은 프리미엄 서비스 제공 hello 하지만 대부분의 네트워크 구성 가능성 또한 tooother 멋진 기능을 제공 합니다. VNet 통합 Standard 또는 Premium Asp 사용할 수 있으며 안전 하 게 hello 다중 테 넌 트 응용 프로그램 서비스에서에서 VNet의 리소스를 소모에 완벽 합니다. 하이브리드 연결은 현재 있는 시작 가능한 하 고는 점진적으로 비용이 많이 드는 가져온 후 사용료 계정 hello 금액에 따라 BizTalk에 따라 다릅니다. Tooworking 많은 네트워크를 통해 하지만 때는이 하이브리드 연결 100 개 이상의 잘 분리 된 네트워크에 tooaccess 리소스 수 있도록와 같은 다른 기능은 없습니다. 

<!--Image references-->
[1]: ./media/web-sites-integrate-with-vnet/vnetint-upgradeplan.png
[2]: ./media/web-sites-integrate-with-vnet/vnetint-existingvnet.png
[3]: ./media/web-sites-integrate-with-vnet/vnetint-createvnet.png
[4]: ./media/web-sites-integrate-with-vnet/vnetint-howitworks.png
[5]: ./media/web-sites-integrate-with-vnet/vnetint-appmanage.png
[6]: ./media/web-sites-integrate-with-vnet/vnetint-aspmanage.png
[7]: ./media/web-sites-integrate-with-vnet/vnetint-aspmanagedetail.png
[8]: ./media/web-sites-integrate-with-vnet/vnetint-vnetp2s.png

<!--Links-->
[VNETOverview]: http://azure.microsoft.com/documentation/articles/virtual-networks-overview/ 
[AzurePortal]: http://portal.azure.com/
[ASPricing]: http://azure.microsoft.com/pricing/details/app-service/
[VNETPricing]: http://azure.microsoft.com/pricing/details/vpn-gateway/
[DataPricing]: http://azure.microsoft.com/pricing/details/data-transfers/
[V2VNETP2S]: http://azure.microsoft.com/documentation/articles/vpn-gateway-howto-point-to-site-rm-ps/
[IntPowershell]: http://azure.microsoft.com/documentation/articles/app-service-vnet-integration-powershell/
[ASEintro]: http://docs.microsoft.com/azure/app-service/app-service-environment/intro
[ILBASE]: http://docs.microsoft.com/azure/app-service/app-service-environment/create-ilb-ase
[V2VNETPortal]: https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal
[VPNERCoex]: http://docs.microsoft.com/en-us/azure/expressroute/expressroute-howto-coexist-resource-manager
[ASE]: http://docs.microsoft.com/azure/app-service/app-service-environment/intro

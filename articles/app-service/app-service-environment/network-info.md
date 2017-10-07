---
title: "Azure 앱 서비스 환경에 aaaNetworking 고려 사항"
description: "Hello ASE 네트워크 트래픽을 설명 및 방법을 tooset Nsg 및 UDRs 프로그램 ASE와"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 955a4d84-94ca-418d-aa79-b57a5eb8cb85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ccompy
ms.openlocfilehash: d4d3000f4d4d75814b1e6d47079d967334eb1a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="networking-considerations-for-an-app-service-environment"></a>App Service Environment에 대한 네트워킹 고려 사항 #

## <a name="overview"></a>개요 ##

 Azure [App Service Environment][Intro]는 Azure App Service를 Azure VNet(Virtual Network) 내 서브넷에 배포한 것입니다. ASE(App Service Environment)에는 두 가지 배포 유형이 있습니다.

- **외부 ASE**: 노출 hello 인터넷 액세스 가능 IP 주소에 ASE 호스트 앱입니다. 자세한 내용은 [외부 ASE 만들기][MakeExternalASE]를 참조하세요.
- **ILB ASE**: 노출 hello VNet 내 IP 주소에 ASE 호스트 앱. hello 내부 끝점은 내부 부하 분산 ILB (),이 때문에 ILB ASE 라 부릅니다. 자세한 내용은 [ILB ASE 만들기 및 사용][MakeILBASE]을 참조하세요.

현재 App Service Environment에는 두 가지 버전(ASEv1 및 ASEv2)이 있습니다. ASEv1 대 한 자세한 내용은 참조 [소개 tooApp 서비스 환경 v1][ASEv1Intro]합니다. ASEv1은 클래식 또는 Resource Manager VNet에서 배포할 수 있습니다. ASEv2는 Resource Manager VNet에만 배포할 수 있습니다.

모든 호출은 ASE toohello 이동 하는 인터넷 hello ASE hello에 대 한 할당 된 VIP 통해 VNet을 둡니다. hello이 VIP의 공용 IP는 hello 원본 IP toohello 이동 ASE hello에서 모든 호출에 대해 인터넷 합니다. VNet에서 또는 VPN을 통해 호출 tooresources를 확인 하는 프로그램 ASE에 hello 앱, hello 원본 IP은 ASE 프로그램에서 사용 하는 hello 서브넷의 Ip hello 중 하나입니다. Hello ASE hello VNet 내 이기 때문에 추가 구성 없이 hello VNet 내의 리소스에 액세스할 수도 있습니다. 연결 된 tooyour 온-프레미스 네트워크 hello VNet을 사용 하는 경우 앱 프로그램 ASE에도 대 한 액세스 tooresources 있습니다. 않아도 tooconfigure hello ASE 또는 응용 프로그램 모두 추가 됩니다.

![외부 ASE][1] 

외부 ASE를 사용 하도록 설정한 경우 공용 VIP hello ASE 앱 toofor를 해결 하는 hello 끝점 이기도 합니다.

* HTTP/S 
* FTP/S 
* 웹 배포
* 원격 디버깅

![ILB ASE][2]

ILB ASE를 사용 하도록 설정한 경우 hello ILB의 IP 주소 hello은 HTTP/S, FTP/S, 웹 배포 및 원격 디버깅에 대 한 hello 끝점입니다.

hello 일반적인 앱 액세스 포트는 같습니다.

| 사용 | 원본 | 너무|
|----------|---------|-------------|
|  HTTP/HTTPS  | 사용자 구성 가능 |  80, 443 |
|  FTP/FTPS    | 사용자 구성 가능 |  21, 990, 10001-10020 |
|  Visual Studio 원격 디버깅  |  사용자 구성 가능 |  4016, 4018, 4020, 4022 |

외부 ASE를 사용하든, ILB ASE를 사용하든 위 표에 나와 있는 포트가 사용됩니다. 외부 ASE를 사용 하는 경우 공용 VIP hello에서이 포트를 누르면 있습니다. ILB ASE를 사용 하는 경우 ILB hello에서이 포트를 누르면 있습니다. 포트 443 잠근 경우 hello 포털에서 표시 하는 일부 기능에 영향을 줄 수 있습니다. 자세한 내용은 [포털 종속성](#portaldep)을 참조하세요.

## <a name="ase-dependencies"></a>ASE 종속성 ##

ASE 인바운드 액세스 종속성은 다음과 같습니다.

| 사용 | 원본 | 너무|
|-----|------|----|
| 관리 | App Service 관리 주소 | ASE 서브넷: 454, 455 |
|  ASE 내부 통신 | ASE 서브넷: 모든 포트 | ASE 서브넷: 모든 포트
|  Azure Load Balancer 인바운드 허용 | Azure Load Balancer | ASE 서브넷: 모든 포트
|  IP 주소가 할당된 앱 | 주소가 할당된 앱 | ASE 서브넷: 모든 포트

hello 인바운드 트래픽을 제공 명령과 더하기 toosystem 모니터링 hello ASE 제어 합니다. 이 트래픽에 대 한 hello 원본 Ip hello에 나열 된 [ASE 관리 해결] [ ASEManagement] 문서. hello 네트워크 보안 구성에는 모든 Ip 포트 454 및 455에서에서 tooallow 액세스를 해야합니다.

hello ASE 서브넷 내에서 내부 구성 요소 통신에 사용 되는 포트 수 및 변경 될 수 있습니다.  모든 hello 포트에 hello ASE 서브넷 toobe hello ASE 서브넷에서 액세스할 수 있어야합니다. 

Hello Azure 부하 분산 장치 사이의 hello ASE 서브넷 hello 최소한의 포트가 hello 통신에 대 한 열려 해당 필요 toobe은 454, 455 및 16001입니다. hello 16001 포트 hello 부하 분산 장치 및 hello ASE 간 유지 활성 트래픽에 사용 됩니다. ILB ASE를 사용 하는 트래픽을 toojust hello 454, 455, 16001 포트를 잠글 수 있습니다.  외부 ASE를 사용 하는 경우 다음 해야 tootake 계정 hello 일반적인 앱 액세스 포트.  Tooopen 앱 할당 된 주소를 사용 하는 경우 해야 것 tooall 포트입니다.  주소는 tooa 특정 앱에 할당 된 경우 hello 부하 분산 장치 미리 toosend HTTP 및 HTTPS 트래픽 toohello ASE 알 수 없는 포트를 사용 합니다.

응용 프로그램 할당 된 IP 주소를 사용 하는 경우 Ip 할당 tooyour 앱 toohello ASE 서브넷 hello tooallow 트래픽이 전송을 해야 합니다.

아웃 바운드 액세스의 경우 ASE는 여러 외부 시스템에 종속됩니다. 해당 시스템 종속성 DNS 이름으로 정의 되 고 tooa 고정 IP 주소 집합에 매핑하지 마세요. Hello ASE hello ASE 서브넷 tooall에서 아웃 바운드 액세스를 해야 하는 따라서 다양 한 포트의 외부 Ip입니다. ASE hello 아웃 바운드 종속성 뒤에 있습니다.

| 사용 | 원본 | 너무|
|-----|------|----|
| Azure 저장소 | ASE 서브넷 | table.core.windows.net, blob.core.windows.net, queue.core.windows.net, file.core.windows.net: 80, 443, 445(445는 ASEv1의 경우에만 필요함) |
| Azure SQL 데이터베이스 | ASE 서브넷 | database.windows.net: 1433, 11000-11999, 14000-14999(자세한 내용은 [SQL Database V12 포트 사용](../../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md) 참조)|
| Azure 관리 | ASE 서브넷 | management.core.windows.net, management.azure.com: 443 
| SSL 인증서 확인 |  ASE 서브넷            |  ocsp.msocsp.com, mscrl.microsoft.com, crl.microsoft.com: 443
| Azure Active Directory        | ASE 서브넷            |  인터넷: 443
| App Service 관리        | ASE 서브넷            |  인터넷: 443
| Azure DNS                     | ASE 서브넷            |  인터넷: 53
| ASE 내부 통신    | ASE 서브넷: 모든 포트 |  ASE 서브넷: 모든 포트

Hello ASE 끊어지더라도 액세스 toothese 종속성 작동 하지 않습니다. Hello ASE 충분히 긴 이런 경우 일시 중단 됩니다.

### <a name="customer-dns"></a>고객 DNS ###

Hello VNet을 구성 된 경우 사용자가 정의한 DNS 서버를 통해 hello 테 넌 트 작업으로 사용 합니다. hello ASE는 관리 목적을 위해 Azure dns toocommunicate 여전히 필요합니다. 

Hello VNet에 구성 된 경우 DNS 고객과 VPN의 다른 쪽 hello, DNS 서버 hello hello ASE를 포함 하는 hello 서브넷에서 연결할 수 있어야 합니다.

<a name="portaldep"></a>

## <a name="portal-dependencies"></a>포털 종속성 ##

또한 toohello ASE 기능 종속성에서 된 몇 가지 추가 항목이 관련된 toohello 포털 환경입니다. Hello Azure 포털에서에서 hello 기능 중 일부에 직접 액세스 too_SCM 사이트 _에 따라 다릅니다. Azure App Service의 모든 앱에는 URL이 두 개 있습니다. hello 첫 번째 URL은 tooaccess 앱. hello 두 번째 URL은 hello 라고도 함 tooaccess hello SCM 사이트 _Kudu 콘솔_합니다. Hello SCM 사이트를 사용 하는 기능은 다음과 같습니다.

-   웹 작업
-   함수
-   스트리밍 로그
-   Kudu
-   확장
-   Process Explorer
-   콘솔

ILB ASE를 사용 하면 hello SCM 사이트 인터넷 hello VNet 외부에서 액세스할 수 없습니다. 응용 프로그램은 ILB ASE에 호스트 되는 경우 hello 포털에서 일부 기능이 작동 하지 않습니다.  

Hello SCM 사이트에 종속 된 이러한 기능을 대부분 hello Kudu 콘솔에서 직접 사용할 수 있습니다. Tooit hello 포털을 사용 하는 대신 직접 연결할 수 있습니다. 응용 프로그램을 ILB ASE에 호스트 된 경우의 게시 자격 증명 toosign 프로그램을 사용 합니다. ILB ASE에 호스팅되는 앱의 hello URL tooaccess hello SCM 사이트 형식에 따라 hello에 있습니다. 

```
<appname>.scm.<domain name hello ILB ASE was created with> 
```

ILB ASE hello 도메인 이름이 경우 *contoso.net* 앱 이름이 및 *testapp*, hello 앱에서에 도달 하면 *testapp.contoso.net*합니다. 함께 이동 hello SCM 사이트에 도달 하면 *testapp.scm.contoso.net*합니다.

### <a name="functions-and-web-jobs"></a>함수 및 웹 작업 ###

함수와 웹 작업 hello SCM 사이트에 따라 달라 집니다 하지만 경우에 앱 ILB ASE에 브라우저 hello SCM 사이트에 도달할 수으로 hello 포털에서 사용할 수 있습니다.  ILB ASE를 사용 하는 자체 서명 된 인증서 인증서 프로그램 브라우저 tootrust tooenable 해야 합니다.  IE와 hello 인증서를 의미 하는 가장자리에 대 한 저장 hello 컴퓨터 신뢰에서 toobe에 있습니다.  즉, 아마도 hello scm 사이트를 직접 클릭 하 여 이전 hello 브라우저에서 hello 인증서를 수락 하는 다음 Chrome을 사용 하는 경우  hello 최상의 솔루션은 toouse hello 브라우저 신뢰 체인에 있는 상용 인증서입니다.  

## <a name="ase-ip-addresses"></a>ASE IP 주소 ##

ASE에 몇 가지 IP 주소 toobe 알고 있습니다. 아래에 이 계정과 키의 예제가 나와 있습니다.

- **공용 인바운드 IP 주소**: 외부 ASE의 앱 트래픽 및 외부 ASE와 ILB ASE 둘 다의 관리 트래픽에 사용됩니다.
- **아웃 바운드 공용 IP**: hello "IP 에서" hello ASE의 아웃 바운드 연결에 대 한 해당 leave hello VNet VPN 아래로 라우트되 아닌를 사용 합니다.
- **ILB IP 주소**: ILB ASE를 사용하는 경우 사용됩니다.
- **앱에 할당된 IP 기반 SSL 주소**: 외부 ASE를 사용하며 IP 기반 SSL이 구성되어 있을 때만 사용 가능합니다.

이러한 모든 IP 주소는 hello ASE UI에서에서 hello Azure 포털에서에서 ASEv2에서 쉽게 찾을 수 있습니다. ILB ASE를 사용 하도록 설정한 경우 ILB hello에 대 한 hello IP 나열 됩니다.

![IP 주소][3]

### <a name="app-assigned-ip-addresses"></a>앱에 할당된 IP 주소 ###

외부 ASE IP 주소 tooindividual 앱 할당할 수 있습니다. ILB ASE에서는 IP 주소를 할당할 수 없습니다. 방법에 대 한 자세한 내용은 tooconfigure 앱 toohave 자체 IP 주소 참조 [는 기존 사용자 지정 SSL 인증서 tooAzure 웹 앱을 바인딩할](../../app-service-web/app-service-web-tutorial-custom-ssl.md)합니다.

응용 프로그램에 고유한 IP 기반 SSL 주소가, hello ASE 두 개의 포트 toomap toothat IP 주소를 예약 합니다. 한 포트는 HTTP 트래픽의 및 hello 다른 포트는 https의 경우. 이러한 포트는 hello ASE UI hello IP 주소 섹션에서에 나열 됩니다. 트래픽 수 tooreach에서 이러한 포트 여야 합니다 또는 hello 앱의 hello VIP는 액세스할 수 없습니다. 이 요구 사항은 보안 Nsg (네트워크 그룹)를 구성할 때 중요 한 tooremember를입니다.

## <a name="network-security-groups"></a>네트워크 보안 그룹 ##

[네트워크 보안 그룹] [ NSGs] VNet 내 hello 기능 toocontrol 네트워크 액세스를 제공 합니다. Hello 포털을 사용 하 여이 암시적 거부 규칙을 가장 낮은 우선 순위 toodeny hello에서 모든 항목입니다. 허용 규칙은 사용자가 직접 작성합니다.

ASE에 대 한 액세스 toohello 사용 되는 Vm toohost hello ASE 자체 필요는 없습니다. Microsoft에서 관리하는 구독을 통해 이러한 VM에 액세스할 수 있습니다. Hello ASE에서 toorestrict 액세스 toohello 앱 hello ASE 서브넷에 Nsg를 설정 합니다. 이 과정에서 toohello ASE 종속성 주의 주의 해야 합니다. 모든 종속성을 차단 하는 경우 hello ASE 작동이 중단 됩니다.

Nsg은 hello Azure 포털 또는 PowerShell을 통해 구성할 수 있습니다. 여기에 hello 정보 hello Azure 포털을 보여 줍니다. 만들고에서 최상위 리소스로 Nsg hello 포털에서 관리 **네트워킹**합니다.

Hello 인바운드 및 아웃 바운드 요구 사항을 고려 하십시오 hello Nsg 비슷한 toohello Nsg에이 예에서 같아야 합니다. hello VNet 주소 범위는 _192.168.250.0/16_, hello ASE에 있는 hello 서브넷 이며 _192.168.251.128/25_합니다.

hello 처음 두 인바운드 요구 사항에 대 한 hello ASE toofunction hello이 예에서 hello 목록 위쪽에 표시 됩니다. ASE 관리와 고 자신과 hello ASE toocommunicate 허용 합니다. hello 다른 항목은 구성 가능한 모든 테 넌 되며 네트워크 액세스 toohello ASE 호스팅 응용 프로그램을 제어할 수 있습니다. 

![인바운드 보안 규칙][4]

기본 규칙은 hello VNet tootalk toohello ASE 서브넷의 Ip hello 수 있도록 합니다. 다른 기본 규칙 hello 부하 분산 장치를 hello 공용 VIP, ASE hello로 toocommunicate로도 알려져 있습니다. toosee hello 기본 규칙을 선택 **규칙 기본** 다음 toohello **추가** 아이콘입니다. Deny hello NSG 규칙 표시 된 후 나머지 모든 규칙을 두면 hello VIP와 hello ASE 간의 트래픽을 방지 합니다. 들어오는 tooprevent 트래픽을 hello VNet 내 추가 사용자 고유의 규칙 tooallow 인바운드 합니다. 소스 같은 tooAzureLoadBalancer의 대상으로 사용 하 여 **모든** 및 포트 범위의  **\*** 합니다. Hello NSG 규칙이 적용 된 toohello ASE 서브넷 이기 때문에 hello 대상에 toobe 특정이 필요는 없습니다.

IP 주소 tooyour 앱에 할당 한 경우 hello 열린 포트를 유지 해야 합니다. toosee hello 포트 선택 **앱 서비스 환경** > **IP 주소**합니다.  

아웃 바운드 규칙에 따라 hello에 표시 된 모든 hello 항목 hello 마지막 항목 제외 하 고 필요 합니다. 이 문서의 앞부분에서 언급 하는 네트워크 액세스 toohello ASE 종속성 수 있습니다. 이러한 항목 중 하나라도 차단하면 ASE의 작동이 중지됩니다. hello hello 목록의 마지막 항목에는 VNet의 다른 리소스와 사용자 ASE toocommunicate를 수 있습니다.

![아웃바운드 보안 규칙][5]

프로그램 Nsg를 정의한 후 toohello 서브넷에 있는 프로그램 ASE 할당 합니다. Hello ASE VNet 또는 서브넷을 기억 하지 못하는 경우에 hello ASE 관리 포털에서 볼 수 있습니다. tooassign은 NSG tooyour 서브넷 hello toohello 서브넷 UI 이동한 hello NSG를 선택 합니다.

## <a name="routes"></a>경로 ##

경로 문제는 Azure ExpressRoute를 사용하여 VNet을 구성할 때 가장 흔히 발생합니다. VNet에는 세 가지 유형의 경로가 있습니다.

-   시스템 경로
-   BGP 경로
-   UDR(사용자 정의 경로)

BGP 경로는 시스템 경로를 재정의합니다. UDR은 BGP 경로를 재정의합니다. Azure Virtual Networks의 경로에 대한 자세한 내용은 [사용자 정의 경로 개요][UDRs]를 참조하세요.

hello ASE toomanage hello 시스템을 사용 하는 hello Azure SQL 데이터베이스 방화벽을 있습니다. 통신 toooriginate hello ASE 공용 VIP에서에서 필요합니다. Hello ASE에서 연결 toohello SQL 데이터베이스 다운 hello ExpressRoute 연결 및 다른 IP 주소 out 보낼 경우 거부 됩니다.

ExpressRoute hello 아래로 회신 tooincoming 관리 요청을 보내면 hello 회신 주소 hello 원래 대상과 차이가 있습니다. 이 불일치는 hello TCP 통신을 중단합니다.

ASE toowork VNet ExpressRoute를 사용 하는 동안 hello 쉬운 일 toodo는 다음과 같습니다.

-   ExpressRoute tooadvertise 구성 _0.0.0.0/0_합니다. 기본적으로 ExpressRoute는 온-프레미스의 모든 아웃바운드 트래픽을 강제로 터널링합니다.
-   UDR를 만듭니다. Hello ASE의 주소 접두사가 포함 된 toohello 서브넷 적용 _0.0.0.0/0_ 는 다음 홉의 형식 및 _인터넷_합니다.

두 가지 변경 작업을 수행한 경우 hello ASE 서브넷에서 인터넷 대상이 지정 되었으며 트래픽은 works hello ExpressRoute hello ASE 사항과 강제 되지 않습니다. 

> [!IMPORTANT]
> UDR에 정의 된 hello 경로 hello ExpressRoute 구성에서 보급 하는 경로 보다 구체적 tootake 선행 이어야 합니다. hello 앞의 예제 hello 광범위 한 0.0.0.0/0 주소 범위가 사용. 따라서 더 구체적인 주소 범위를 사용하는 경로 보급 알림으로 인해 주소 범위가 잘못 재정의될 가능성이 있습니다.
>
> ASEs 간 알릴 안녕 공용 피어 링 경로 toohello 개인 피어 링 경로에서 경로 ExpressRoute 구성이 지원 되지 않습니다. 공용 피어링이 구성된 ExpressRoute 구성은 Microsoft에서 경로 보급 알림을 받습니다. hello 광고는 다양 한 Microsoft Azure IP 주소 범위를 포함합니다. Hello ASE의 서브넷에서 모든 아웃 바운드 네트워크 패킷을 hello 주소 범위는 hello 개인 피어 링 경로에 크로스 보급을 경우 강제 터널링된 tooa 고객의 온-프레미스 네트워크 인프라 합니다. 이 네트워크 흐름은 현재 ASE에서 지원되지 않습니다. 하나의 솔루션 toothis 문제는 hello 공용 피어 링 경로 toohello 개인 피어 링 경로에서 toostop 간 광고 경로입니다.

toocreate UDR, 다음이 단계를 따르십시오.

1. Azure 포털 toohello를 이동 합니다. **네트워킹** > **경로 테이블**을 선택합니다.

2. Hello에 새 경로 테이블을 만들려면 동일한 지역 VNet으로 합니다.

3. 경로 테이블 UI 내에서 **경로** > **추가**를 선택합니다.

4. 집합 hello **다음 홉 형식** 너무**인터넷** 및 hello **주소 접두사** 너무**0.0.0.0/0**합니다. **저장**을 선택합니다.

    그러면 hello 다음과 같은 내용이 나타납니다.

    ![기능 경로][6]

5. Hello 새로운 경로 테이블을 만든 후에 프로그램 ASE이 포함 된 toohello 서브넷을 이동 합니다. Hello 포털에서 hello 목록에서 경로 테이블을 선택 합니다. Hello 변경을 저장 한 후 hello Nsg 및 서브넷으로 설명 하는 경로 다음 표시 됩니다.

    ![NSG 및 경로][7]

### <a name="deploy-into-existing-azure-virtual-networks-that-are-integrated-with-expressroute"></a>ExpressRoute와 통합된 기존 Azure Virtual Networks에 배포 ###

toodeploy 프로그램 ASE ExpressRoute를 통합 된 VNet에 배포 된 hello ASE 저장할 hello 서브넷 미리 구성 합니다. 다음 사용 하 여 리소스 관리자 템플릿 toodeploy 것입니다. toocreate ASE VNet에 이미 있는 구성 ExpressRoute:

- 서브넷 toohost hello를 ASE를 만듭니다.

    > [!NOTE]
    > Hello 서브넷 하지만 hello ASE만 수행 될 수 있습니다. 있는지 toochoose 이후 성장을 허용 하는 주소 공간 이어야 합니다. 이 설정은 나중에 변경할 수 없습니다. 주소 128개를 포함할 수 있는 `/25` 크기를 사용하는 것이 좋습니다.

- 앞에서 설명한 대로 UDRs (예를 들어 경로 테이블)를 만들고 hello 서브넷에 있는 설정 합니다.
- 에 설명 된 대로 리소스 관리자 템플릿을 사용 하 여 hello ASE 만들 [ASE 리소스 관리자 템플릿을 사용 하 여 만들][MakeASEfromTemplate]합니다.

<!--Image references-->
[1]: ./media/network_considerations_with_an_app_service_environment/networkase-overflow.png
[2]: ./media/network_considerations_with_an_app_service_environment/networkase-overflow2.png
[3]: ./media/network_considerations_with_an_app_service_environment/networkase-ipaddresses.png
[4]: ./media/network_considerations_with_an_app_service_environment/networkase-inboundnsg.png
[5]: ./media/network_considerations_with_an_app_service_environment/networkase-outboundnsg.png
[6]: ./media/network_considerations_with_an_app_service_environment/networkase-udr.png
[7]: ./media/network_considerations_with_an_app_service_environment/networkase-subnet.png

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[ASEManagement]: ./management-addresses.md

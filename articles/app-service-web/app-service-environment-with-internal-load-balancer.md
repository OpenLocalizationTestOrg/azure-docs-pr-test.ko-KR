---
title: "aaaCreating 함께 사용 하는 내부 부하 분산 장치 앱 서비스 환경 | Microsoft Docs"
description: "ILB를 사용하여 ASE 만들기 및 사용"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: ad9a1e00-d5e5-413e-be47-e21e5b285dbf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 20799f260993d6e81499408e5b547a2e21430174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-an-internal-load-balancer-with-an-app-service-environment"></a>앱 서비스 환경에서 내부 부하 분산 장치 사용

> [!NOTE] 
> 앱 서비스 환경 v1 hello에 대 한이 문서는입니다. 최신 버전의 hello 쉽게 toouse 되며 더 강력한 인프라에서 실행 하는 앱 서비스 환경 있습니다. hello로 시작 하는 hello 새 버전에 대 한 자세한 toolearn [소개 toohello 앱 서비스 환경](../app-service/app-service-environment/intro.md)합니다.
>

hello 앱 서비스 환경 (ASE) 기능은 hello 다중 테 넌 트 스탬프에서 제공 되는 향상 된 구성 기능을 제공 하는 Azure 앱 서비스의 프리미엄 서비스 옵션입니다. 기본적으로 hello ASE 기능 hello Azure 가상 Network(VNet)에 Azure 앱 서비스를 배포합니다. 앱 서비스 환경에서 제공 하는 hello 기능의 자세히 이해할 toogain 읽을 hello [앱 서비스 환경 이란] [ WhatisASE] 설명서입니다. VNet에서 같은 hello 이점이 읽을 hello 모르는 경우 [Azure 가상 네트워크 FAQ][virtualnetwork]합니다. 

## <a name="overview"></a>개요
ASE는 VNet의 인터넷 액세스 가능 끝점 또는 IP 주소를 사용하여 배포할 수 있습니다. 순서 tooset hello IP 주소 tooa VNet 주소 toodeploy는 내부 부하 Balancer(ILB)와 프로그램 ASE를 필요 합니다. ASE가 ILB로 구성된 경우 다음을 제공합니다.

* 고유한 도메인 또는 하위 도메인. toomake 것을이 문서에서는 있지만 하위 도메인을 가정 쉽게 구성할 수 어느 쪽. 
* HTTPS에 사용 되는 hello 인증서
* 하위 도메인에 대한 DNS 관리 

결과적으로 다음과 같은 작업을 수행할 수 있습니다.

* hello에 안전 하 게 업무용 응용 프로그램 같은 호스트 인트라넷 응용 프로그램 사이트 tooSite 또는 express 경로 VPN을 통해 액세스는 클라우드
* 공용 DNS 서버에 나열 되지 않은 hello 클라우드에서 호스트 앱
* 프런트 엔드 앱이 안전하게 통합될 수 있는 인터넷 격리 백 엔드 앱 만들기

#### <a name="disabled-functionality"></a>사용되지 않도록 설정된 기능
ILB ASE를 사용하는 경우 수행할 수 없는 작업도 있습니다. 여기에는 다음이 포함됩니다.

* IPSSL 사용
* toospecific 앱 주소 IP 할당
* 구입 하 고 hello 포털을 통해 앱에 인증서를 사용 합니다. 물론 여전히 직접 인증 기관을 사용 하 여 인증서를 얻어 하지 않을 hello Azure 포털을 통해 앱에 사용 합니다.

## <a name="creating-an-ilb-ase"></a>ILB ASE 만들기
ILB ASE를 만드는 과정은 일반적으로 ASE를 만드는 과정과 크게 다르지 않습니다. ASE를 만드는 방법에 대해 자세히 설명에 대 한 읽기 [어떻게 tooCreate 앱 서비스 환경][HowtoCreateASE]합니다. ILB ASE는 hello 프로세스 toocreate hello ASE 만드는 동안 VNet을 만들거나 기존 VNet을 선택 하면 간에 동일 합니다. ILB ASE toocreate: 

1. Azure 포털 선택 hello에 **새로운 웹-> + 모바일 앱 서비스 환경->**
2. 구독 선택
3. 리소스 그룹 선택 또는 만들기
4. VNet 선택 또는 만들기
5. VNet을 선택하는 경우 서브넷 만들기
6. 선택 **가상 네트워크/위치-> VNet 구성** 및 집합 hello VIP 유형 tooInternal
7. 하위 도메인 이름 (이 ASE에서 만든 앱에 사용 되는 hello 하위 도메인 수는)를 제공 합니다.
8. 확인 및 만들기를 차례로 선택

![][1]

가상 네트워크 블레이드 hello 내에서 VNet 구성 옵션이 있습니다. 여기서 외부 VIP 또는 내부 VIP 중에서 선택할 수 있습니다. hello 기본값은 외부입니다. TooExternal에서 설정한 경우 사용자 ASE 인터넷 액세스 가능한 VIP를 사용 합니다. 내부를 선택하는 경우 ASE가 VNet 내의 IP 주소에 있는 ILB로 구성됩니다. 

내부를 선택한 후 hello 기능 tooadd IP 주소가 많을 수록 tooyour ASE 제거 되 고 대신 hello ASE의 tooprovide hello 하위 도메인이 필요 합니다. 외부 VIP hello로 ASE에 hello ASE의 이름이 해당 ASE에서 만든 앱에 대 한 hello 하위 도메인에서 사용 됩니다. 프로그램 ASE가 호출 되 면 ***contosotest*** 해당 ASE에 응용 프로그램이 호출 된 및 ***mytest*** 있으면 hello 하위 도메인 합니다 hello 형식의 ***contosotest.p.azurewebsites.net*** 및 hello 해당 앱에 대 한 URL 것 ***mytest.contosotest.p.azurewebsites.net***합니다. VIP 유형 tooInternal hello로 설정 하면 ASE 이름이 사용 되지 않습니다 hello 하위 도메인에 있는 ASE hello에 대 한. Hello 하위 도메인을 명시적으로 지정합니다. 하위 도메인 되었으면 ***contoso.corp.net*** ASE 라는 한다는 점에서 앱을 변경 하 고 ***timereporting*** 것이 이러한 앱에 대 한 URL을 다음 hello ***timereporting.contoso.corp.net***합니다.

## <a name="apps-in-an-ilb-ase"></a>ILB ASE의 앱
ILB ASE에 응용 프로그램을 만드는 ASE에 일반적으로 응용 프로그램을 만드는 것과 동일한 hello 됩니다. 

1. Azure 포털 선택 hello에 **새로운 웹-> + 모바일 웹->** 또는 **모바일** 또는 **API 앱**
2. 앱 이름 입력
3. 구독 선택
4. 리소스 그룹 선택 또는 만들기
5. ASP(앱 서비스 계획) 선택 또는 만들기. 프로그램 ASE hello 위치와 선택 hello 작업자 풀 선택 한 다음 새 ASP 만들기에서 만든 프로그램 ASP toobe를 사용할 합니다. ASP hello를 만들 때 hello 위치와 hello 작업자 풀 프로그램 ASE를 선택 합니다. Hello 응용 프로그램에서 해당 hello 하위 도메인을 보게의 hello 이름을 지정 하면 응용 프로그램 이름에 ASE에 대 한 hello 하위 도메인으로 바뀝니다. 
6. 만들기를 선택합니다. Hello 선택할지 확실히 **Pin toodashboard** 대시보드를 hello 앱 tooshow 하려는 경우 확인란을 선택 합니다. 

![][2]

Hello 응용 프로그램에서 이름 hello 하위 도메인 이름을 프로그램 ASE의 업데이트 된 tooreflect hello 하위 도메인을 가져옵니다. 

## <a name="post-ilb-ase-creation-validation"></a>ILB ASE 만들기 유효성 검사 게시
ILB ASE 약간 다른 경우 보다 hello 비-ILB ASE 사용자 고유의 DNS toomanage 필요한 및 있습니다 tooprovide HTTPS 연결에 대 한 고유한 인증서 명시 이미 있습니다. 

프로그램 ASE를 만든 후 표시 됩니다는 hello 하위 도메인 hello 하위 도메인 지정한 및 hello에 새 항목이 **설정** 이라는 메뉴가 **ILB 인증서**합니다. hello ASE을 보다 쉽게 tootest HTTPS를 사용 하면 자체 서명 된 인증서를 만듭니다. hello 포털 알려 HTTPS에 대 한 tooprovide 고유의 인증서 필요 하지만이 toodrive toohave 하위 도메인으로 이동 하는 인증서입니다. 

![][3]

시도 하 고 단순히 작업 toocreate 인증서를 사용 하는 방법을 모르는 경우 hello IIS MMC 콘솔 응용 프로그램 toocreate는 자체 서명 된 인증서입니다. 만든 후 다음에.pfx 파일로 내보낼 및 다음 hello ILB 인증서 UI에에서 업로드할 수 있습니다. 때 액세스 브라우저 자체 서명 된 인증서를 사용 하 여 보호 하는 사이트 사이트에 액세스 하는 hello 된다는 경고가 제공 됩니다 toohello 불가능 toovalidate hello 인증서 인해 안전 하지 않습니다. Tooavoid 해당 경고를 원하는 경우 하위 도메인을 일치 하는 브라우저에서 인식 되는 신뢰 체인을 올바르게 서명 된 인증서가 필요 합니다.

![][6]

Tootry hello 자체 인증서 함께 이동 하 고 HTTP 및 HTTPS 액세스 tooyour ASE 테스트:

1. ASE 만들어지면 tooASE UI 이동 **ASE-> 설정-> ILB 인증서**
2. 인증서 pfx 파일을 선택하여 ILB 인증서를 설정하고 암호를 제공합니다. 이 단계에서는 tooprocess 하는 동안 약간 및 크기 조정 작업이 진행 중인 hello 메시지가 표시 됩니다.
3. 프로그램 ASE에 대 한 hello ILB 주소 가져오기 (**ASE 속성-> 가상 IP 주소->**)
4. ASE를 만든 후에 ASE에서 웹앱을 만듭니다. 
5. 해당 VNET에 없는 경우 VM을 만듭니다 (Not in 동일 hello ASE hello 또는 작업 break와 서브넷)
6. 하위 도메인에 대한 DNS를 설정합니다. DNS에 하위 도메인으로 와일드 카드를 사용 하거나 toodo 몇 가지 간단한 테스트를 원하는 경우 VM tooset 웹 응용 프로그램 이름 tooVIP IP 주소에서 호스트 파일 hello를 편집할 수 있습니다. 프로그램 ASE hello 하위 도메인 이름이 경우. mytestapp.ilbase.com으로 해결한 다음 hosts 파일에서 설정 하는 것을 웹 앱 mytestapp hello ilbase.com 하 고 수행 합니다. (Windows hello 호스트 파일은 C:\Windows\System32\drivers\etc\에서)
7. 해당 VM에서 브라우저를 사용 하 고 toohttp://mytestapp.ilbase.com (웹 앱 이름은 무엇이 든 하위 도메인 사용) 이동
8. 해당 VM에서 브라우저를 사용 하 고 자체 서명 된 인증서를 사용 하는 경우 보안 tooaccept hello 부족을 갖습니다 toohttps://mytestapp.ilbase.com를 이동 합니다. 

가상 IP 주소 hello로 hello IP 주소에 ILB 속성에 나열 됩니다.

![][4]

## <a name="using-an-ilb-ase"></a>ILB ASE 사용
#### <a name="network-security-groups"></a>네트워크 보안 그룹
앱에 대 한 ILB ASE 수 있도록 네트워크 격리 hello 앱이 액세스할 수 없거나으로 알려진 인터넷 hello 합니다. 이러한 기능은 LOB(기간 업무) 응용 프로그램과 같은 인트라넷 사이트를 호스트하는 데 아주 적합합니다. Toorestrict 액세스도 필요한 경우 더 이상 사용할 수 있습니다 네트워크 보안 Groups(NSGs) toocontrol 액세스 hello 네트워크 수준입니다. 

Toomake hello 통신을 중단 하지 않도록 선택 되어 있는지 필요 합니다 toouse Nsg toofurther 액세스를 제한 하려는 경우 해당 hello ASE 순서 toooperate에 필요 합니다. HTTP/HTTPS 액세스 hello 이더라도 hello를 통해서만 ILB 사용 hello ASE hello ASE 여전히 hello VNet 외부의 리소스에 따라 달라 집니다. 네트워크 액세스는 toosee에 hello 문서의 hello 정보를 살펴봅니다 필요한 [인바운드 트래픽 제어 tooan 앱 서비스 환경] [ ControlInbound] 및 hello 문서에서 [네트워크 ExpressRoute 사용 하 여 앱 서비스 환경에 대 한 구성 세부 정보][ExpressRoute]합니다. 

tooknow hello IP가 필요한 사용자 Nsg 주소의 tooconfigure Azure toomanage에서 프로그램 ASE를 사용 합니다. 해당 IP 주소에서는 인터넷 요청 하는 경우 아웃 바운드 IP 주소 여 ASE에서 hello 이기도 합니다. hello 프로그램 ASE에 대 한 아웃 바운드 IP 주소 여 ASE 수명의 hello에 대 한 정적 상태로 유지 됩니다. ASE를 삭제하고 다시 만들면 새 IP 주소를 얻게 됩니다. 이 IP 주소 너무 이동 toofind**설정 속성->** hello 및 **아웃 바운드 IP 주소**합니다. 

![][5]

#### <a name="general-ilb-ase-management"></a>일반 ILB ASE 관리
ILB ASE 관리 ASE 일반적으로 관리 하는 동일한 주로 hello 됩니다. HTTP/HTTPS 트래픽 프로그램 프런트 엔드 서버 toohandle 증가 주거나 수직 확장 및 더 많은 ASP 인스턴스를 작업자 풀 toohost tooscale 해야 합니다. ASE의 hello 구성 관리에 대 한 일반적인 정보를 계속 hello 문서를 읽어 [앱 서비스 환경 구성][ASEConfig]합니다. 

hello 추가 관리 항목은 관리 인증서 및 DNS 관리 합니다. ILB ASE를 만든 후 HTTPS에 사용 되는 hello 인증서 업로드 및 만료 되기 전에 대체 tooobtain 필요 합니다. Hello 기본 도메인을 소유 하 고 Azure 외부 VIP와 ASEs에 대 한 인증서를 제공할 수 있습니다. ILB ASE에서 사용 하는 hello 하위 도메인은 모두 사용할 수 있습니다, 때문 tooprovide 고유한 인증서에 필요한 HTTPS입니다. 

#### <a name="dns-configuration"></a>DNS 구성
때 외부 VIP hello DNS를 사용 하 여 Azure에 의해 관리 됩니다. 프로그램 ASE에서 만든 모든 앱 tooAzure 공용 DNS 인 DNS를 자동으로 추가 됩니다. ILB ASE toomanage 고유한 DNS를가 있습니다. Contoso.corp.net 같은 특정된 하위 도메인에 대 한 DNS A 레코드 해당 지점 tooyour ILB 주소를 toocreate가 필요 합니다.

    * 
    *.scm ftp 게시 


## <a name="getting-started"></a>시작
모든 문서와 방법을-hello에서 사용할 수 있는 앱 서비스 환경에 대 한의 하려면 [응용 프로그램 서비스 환경에 대 한 추가 정보](../app-service/app-service-app-service-environments-readme.md)합니다.

앱 서비스 환경 시작 tooget 참조 [소개 tooApp 서비스 환경][WhatisASE]

Azure 앱 서비스 플랫폼 hello에 대 한 자세한 내용은 참조 [Azure 앱 서비스][AzureAppService]합니다.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createilbase.png
[2]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createapp.png
[3]: ./media/app-service-environment-with-internal-load-balancer/ilbase-newase.png
[4]: ./media/app-service-environment-with-internal-load-balancer/ilbase-vip.png
[5]: ./media/app-service-environment-with-internal-load-balancer/ilbase-externalvip.png
[6]: ./media/app-service-environment-with-internal-load-balancer/ilbase-ilbcertificate.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[vnetnsgs]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/

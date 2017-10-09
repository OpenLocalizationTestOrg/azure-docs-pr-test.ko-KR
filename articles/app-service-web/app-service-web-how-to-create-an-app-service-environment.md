---
title: "앱 서비스 환경 v1 aaaHow tooCreate"
description: "App Service Environment v1에 대한 만들기 흐름 설명"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 81bd32cf-7ae5-454b-a0d2-23b57b51af47
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 95feb33854eee5bac02fa68b066e2fc10eb3fede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-app-service-environment-v1"></a>어떻게 앱 서비스 환경 v1 tooCreate 

> [!NOTE]
> 앱 서비스 환경 v1 hello에 대 한이 문서는입니다. 최신 버전의 hello 쉽게 toouse 되며 더 강력한 인프라에서 실행 하는 앱 서비스 환경 있습니다. hello로 시작 하는 hello 새 버전에 대 한 자세한 toolearn [소개 toohello 앱 서비스 환경](../app-service/app-service-environment/intro.md)합니다.
> 

### <a name="overview"></a>개요
앱 서비스 환경 (ASE) hello는 hello 다중 테 넌 트 스탬프에서 제공 되는 향상 된 구성 기능을 제공 하는 Azure 앱 서비스의 프리미엄 서비스 옵션입니다. hello ASE 기능에는 기본적으로 hello Azure 앱 서비스 고객의 가상 네트워크에 배포합니다. 앱 서비스 환경에서 제공 하는 hello 기능의 자세히 이해할 toogain 읽을 hello [앱 서비스 환경 이란] [ WhatisASE] 설명서입니다.

### <a name="before-you-create-your-ase"></a>ASE를 만들기 전에
것이 중요 한 toobe 인식의 hello 작업 변경할 수 없습니다. 만든 후에 ASE를 변경할 수 없는 항목은 다음과 같습니다.

* 위치
* 구독
* 리소스 그룹
* 사용되는 VNet
* 사용되는 서브넷 
* 서브넷 크기

때 VNet을 선택 하 고 서브넷을 지정 하 않은지 충분히 큰 tooaccomodate 향후 성장 됩니다. 

### <a name="creating-an-app-service-environment-v1"></a>App Service Environment v1 만들기
toocreate toosearch 해야 하는 앱 서비스 환경 v1 hello에 대 한 Azure 마켓플레이스 ***앱 서비스 환경 v1***, 새로 만들기를 통해 또는 웹-> + 모바일 앱 서비스 환경-> 합니다. ASEv1 toocreate:

1. 프로그램 ASE의 hello 이름을 제공 합니다. hello ASE에 대해 지정 된 hello 이름 hello ASE에에서 만든 hello 앱에 사용 됩니다. Hello ASE 이름은 appsvcenvdemo hello 하위 도메인 이름이 됩니다. *appsvcenvdemo.p.azurewebsites.net*합니다. 따라서 *mytestapp*이라는 앱을 만든 경우 해당 주소는 *mytestapp.appsvcenvdemo.p.azurewebsites.net*으로 지정될 수 있습니다. 프로그램 ASE의 hello 이름에 공백 문자를 사용할 수 없습니다. Hello 이름에서 대문자를 사용 하는 경우 hello 도메인 이름에 해당 이름의 총 소문자 버전 hello 됩니다. ILB를 사용하는 경우 ASE 이름이 하위 도메인에서 사용되지 않고 대신 ASE를 만드는 동안에 명시적으로 지정됩니다.
   
    ![][1]
2. 사용 중인 구독을 선택합니다. hello 구독 프로그램 ASE에 사용 되는 해당 ASE에서 모든 앱으로 만들 하나 hello 이기도 합니다. 다른 구독에 있는 VNet에 ASE를 배치할 수 없습니다.
3. 새 리소스 그룹을 선택하거나 지정합니다. 프로그램 ASE에 사용 되는 hello 리소스 그룹 VNet에 사용 되는 동일한를 hello 해야 합니다. 기존 VNet을 선택한 다음 hello 리소스 그룹을 선택 하면 ASE에 대 한 업데이트 된 tooreflect 됩니다 VNet의 합니다.
   
    ![][2]
4. 가상 네트워크 및 위치 선택을 확인합니다. 기존 VNet을 선택 하거나 새 VNet toocreate를 선택할 수 있습니다. 새 VNet을 선택하면 이름 및 위치를 지정할 수 있습니다. hello 새 VNet hello 주소 범위 192.168.250.0/23 및 아무런 이라는 서브넷 **기본** 192.168.250.0/24로 이루어집니다. 또한 기존의 클래식 VNet 또는 Resource Manager VNet을 선택할 수 있습니다. hello VIP 유형 선택 hello에서 ASE에 직접 액세스할 수 있으면 확인 (외부) 인터넷 또는 부하 분산 장치 ILB (내부) 사용 하는 경우. 읽기에 대 한 자세한 toolearn [는 내부 부하 분산 장치를 사용 하 여 앱 서비스 환경으로][ILBASE]합니다. 외부 VIP 유형을 선택 하면 수의 외부 IP 주소 hello 시스템 IPSSL 용도로 사용 하 여 만든은 선택할 수 있습니다. 내부를 선택 하 여 ASE ´ ֲ toospecify hello 하위 도메인을 할 수 있습니다. 공용 주소 범위 *또는* RFC1918 주소 공간(즉, 개인 주소) *중 하나*를 사용하는 가상 네트워크에 ASE를 배포할 수 있습니다. 순서 toouse 공용 주소 범위를 사용 하 여 가상 네트워크에서에서 미리 toocreate hello VNet이 필요 합니다. 기존 VNet을 선택 하면 ASE 만드는 동안 새 서브넷 toocreate가 필요 합니다. **Hello 포털에서 미리 생성된 된 서브넷을 사용할 수 없습니다. Resource Manager 템플릿을 사용하여 ASE를 만드는 경우 기존 서브넷으로 ASE를 만들 수 있습니다.** 서식 파일에서 ASE toocreate hello 정보를 여기서 사용할 [템플릿에서 앱 서비스 환경 만들기] [ ILBAseTemplate] 및 여기에서 [템플릿에서ILB앱서비스환경만들기] [ASEfromTemplate].

### <a name="details"></a>세부 정보
ASE는 2개의 프런트 엔드 및 2개의 작업자를 사용하여 생성됩니다. hello 프런트 엔드 역할 hello HTTP/HTTPS 끝점을 하 고 앱을 호스트 하는 hello 역할 toohello 작업자 트래픽을 전송 합니다. ASE 만든 후 hello 수량을 조정할 수 있으며 이러한 리소스 풀에서 자동 크기 조정 규칙을에 설정할 수 있습니다. 수동 확장에 관한 자세한 정보에 대 한 관리 및 모니터링을 앱 서비스 환경 여기로 이동: [어떻게 tooconfigure 앱 서비스 환경][ASEConfig] 

Hello ASE에서 사용 하는 hello 서브넷 hello 하나 ASE만 존재할 수 있습니다. hello 서브넷 hello ASE 외에 사용할 수 없습니다.

### <a name="after-app-service-environment-v1-creation"></a>App Service Environment v1을 만든 이후
ASE를 만든 후 다음을 조정할 수 있습니다.

* 프런트 엔드 수(최소: 2개)
* 작업자 수(최소: 2개)
* IP SSL에 사용 가능한 IP 주소 수
* 프런트 엔드 또는 작업자 hello에서 사용 하는 리소스 크기를 계산 (프런트 엔드 최소 크기는 P2)

수동 관리를 확장 및 앱 서비스 환경에 대 한 모니터링을 여기에 자세한 내용이: [어떻게 tooconfigure 앱 서비스 환경][ASEConfig] 

자동 크기 조정에 대 한 내용은 설명서 여기: [어떻게 앱 서비스 환경에 대 한 tooconfigure 자동 크기 조정][ASEAutoscale]

Hello 데이터베이스 및 저장소와 같은 사용자 지정에 사용할 수 없는 추가 종속성이 있습니다. Azure에서 처리를 hello 시스템 함께 제공 됩니다. hello 시스템 저장소 지원에 대 한 too500 GB hello 전체 앱 서비스 환경 및 hello 데이터베이스를 hello 소수 자릿수로 hello 시스템의 필요에 따라 Azure에 의해 조정 됩니다.

## <a name="getting-started"></a>시작
모든 문서와 방법을-hello에서 사용할 수 있는 앱 서비스 환경에 대 한의 하려면 [응용 프로그램 서비스 환경에 대 한 추가 정보](../app-service/app-service-app-service-environments-readme.md)합니다.

앱 서비스 환경 v1 시작 tooget 참조 [소개 toohello 앱 서비스 환경 v1][WhatisASE]

Azure 앱 서비스 플랫폼 hello에 대 한 자세한 내용은 참조 [Azure 앱 서비스][AzureAppService]합니다.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-basecreateblade.png
[2]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-vnetcreation.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
[ILBAseTemplate]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-create/
[ASEfromTemplate]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-create-ilb-ase-resourcemanager/

---
title: "aaaCreate 외부 Azure 앱 서비스 환경"
description: "에 대해 설명 하는 동안 앱 서비스 환경 toocreate 응용 프로그램 또는 독립 실행형을 만드는 방법"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 94dd0222-b960-469c-85da-7fcb98654241
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: f8619534ddd889ea65063733ac6ec11b206e799c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-external-app-service-environment"></a>외부 App Service Environment 만들기 #

Azure App Service Environment는 Azure App Service를 Azure VNet(Virtual Network)의 서브넷에 배포한 것입니다. 앱 서비스 환경 (ASE)는 두 가지 방법으로 toodeploy:

- 외부 ASE라고도 하는 외부 IP 주소의 VIP 사용
- 내부 IP 주소에 VIP hello로 ILB ASE 때문에 라고도 hello 내부 끝점은 내부 부하 분산 장치 (ILB).

이 문서에서는 어떻게 toocreate 외부 ASE 합니다. Hello ASE의 개요를 참조 하십시오. [소개 toohello 앱 서비스 환경][Intro]합니다. Toocreate 받는 ILB ASE를 확인 하려면 어떻게 해야에 대 한 내용은 [만들고 ILB ASE를 사용 하 여][MakeILBASE]합니다.

## <a name="before-you-create-your-ase"></a>ASE를 만들기 전에 ##

프로그램 ASE를 만든 후 hello 다음을 변경할 수 없습니다.

- 위치
- 구독
- 리소스 그룹
- 사용되는 VNet
- 사용되는 서브넷
- 서브넷 크기

> [!NOTE]
> VNet을 선택 하 고 서브넷을 지정 하는 경우 충분히 큰 tooaccommodate의 향후 데이터 증가 인지 확인 합니다. 주소 128개를 포함할 수 있는 `/25` 크기를 사용하는 것이 좋습니다.
>

## <a name="three-ways-toocreate-an-ase"></a>세 가지 방법으로 toocreate ASE ##

세 가지 방법으로 toocreate ASE 가지가 있습니다.

- **App Service 계획을 만들 때**. 이 메서드는 한 번에 hello ASE 및 hello 앱 서비스 계획을 만듭니다.
- **독립 실행형 작업으로**. 이 메서드는 내부에 아무것도 포함되지 않은 ASE인 독립 실행형 ASE를 만듭니다. 이 방법은 고급 프로세스 toocreate ASE에 설명 합니다. 사용 중인 것 toocreate ASE 받는 ILB 됩니다.
- **Azure Resource Manager 템플릿에서**. 이 메서드는 고급 사용자를 위한 것입니다. 자세한 내용은 [템플릿에서 ASE 만들기][MakeASEfromTemplate]를 참조하세요.

외부 ASE ASE hello에서 모든 HTTP/HTTPS 트래픽을 toohello 앱 인터넷 액세스 가능 IP 주소에 도달 하는 공용 VIP에 있습니다. Ilb는 ASE hello ASE에서 사용 하는 hello 서브넷에서 IP 주소를 있습니다. hello ILB ASE에 호스팅된 앱에서 노출 되지 않습니다 toohello 직접 인터넷 합니다.

## <a name="create-an-ase-and-an-app-service-plan-together"></a>ASE 및 App Service 계획 만들기 ##

앱 서비스 계획 hello는 응용 프로그램의 컨테이너입니다. App Service에서 앱을 만드는 경우 App Service 계획을 선택하거나 만듭니다. hello 컨테이너 모델 환경 앱 서비스 계획을 잡고 앱 서비스 계획을 저장할 응용 프로그램.

앱 서비스 계획을 만드는 동안 ASE toocreate:

1. Hello에 [Azure 포털](https://portal.azure.com/)선택, **새로** > **웹 + 모바일** > **웹 앱**합니다.

    ![웹앱 만들기][1]

2. 사용 중인 구독을 선택합니다. hello 앱 hello ASE에에서 만들어지고는 hello 동일 구독 합니다.

3. 리소스 그룹을 선택하거나 만듭니다. 리소스 그룹을 사용하여 관련된 Azure 리소스를 하나의 단위로 관리할 수 있습니다. 리소스 그룹은 앱에 대해 역할 기반 액세스 제어 규칙을 설정하려는 경우 유용합니다. 자세한 내용은 참조 hello [Azure 리소스 관리자 개요][ARMOverview]합니다.

4. Hello 앱 서비스 계획을 선택한 다음 선택 **새로 만들기**합니다.

    ![새 App Service 계획][2]

5. Hello에 **위치** 드롭 다운 목록, 선택 hello 영역 toocreate hello ASE 합니다. 기존 ASE를 선택하는 경우 새 ASE가 생성되지 않습니다. 앱 서비스 계획 hello hello 선택한 ASE에에서 만들어집니다. 

6. 선택 **가격 책정 계층**, hello 중 하나를 선택 하 고 **격리 됨** Sku 가격입니다. **격리** SKU 카드를 선택하고 ASE가 아닌 위치를 선택하면 새 ASE가 해당 위치에 만들어집니다. toostart hello 프로세스 toocreate는 ASE 선택 **선택**합니다. hello **격리 됨** SKU가 ASE와 함께만에서 사용할 수 있습니다. 또한 **격리**가 아닌 ASE의 다른 가격 책정 SKU를 사용할 수 없습니다.

    ![가격 책정 계층 선택][3]

7. 프로그램 ASE hello 이름을 입력 합니다. 이 이름은 앱에 대 한 주소 지정 가능 이름을 hello에 사용 됩니다. Hello ASE hello 이름이 인 경우 _appsvcenvdemo_, hello 도메인 이름이 *. appsvcenvdemo.p.azurewebsites.net*합니다. *mytestapp*이라는 앱을 만든 경우 mytestapp.appsvcenvdemo.p.azurewebsites.net으로 주소를 지정할 수 있습니다. Hello 이름에 공백을 사용할 수 없습니다. 대문자를 사용 하는 경우 hello 도메인 이름은 해당 이름의 hello 총 소문자 버전입니다.

    ![새 App Service 계획 이름][4]

8. Azure 가상 네트워킹 세부 정보를 지정합니다. **새로 만들기** 또는 **기존 항목 선택** 중 하나를 선택합니다. hello 옵션 tooselect 기존 VNet은 VNet hello 선택한 영역에 있는 경우에 사용할 수 있습니다. 선택 하는 경우 **새로 만들기**, hello VNet에 대 한 이름을 입력 합니다. 해당 이름으로 새로운 Resource Manager VNet이 만들어집니다. Hello 주소 공간을 사용 하 여 `192.168.250.0/23` hello 선택한 지역에 있습니다. **기존 항목 선택**을 선택하는 경우 다음 항목이 필요합니다.

    a. 둘 이상의 hello VNet 주소 블록을 선택 합니다.

    b. 새 서브넷 이름을 입력합니다.

    c. Hello 서브넷의 hello 크기를 선택 합니다. *프로그램 ASE의 크기가 작아 tooaccommodate 향후 성장을 tooselect을 기억 합니다.* 권장되는 크기는 `/25`입니다. 여기에는 128개의 주소가 있고 최대 크기의 ASE를 다룰 수 있습니다. 예를 들어 16개의 주소만을 사용할 수 있기 때문에 `/28`은 권장되지 않습니다. 인프라는 최소 5개의 주소를 사용합니다. `/28` 서브넷에서 11개 인스턴스의 최대 확장이 있습니다.

    d. Hello 서브넷 IP 범위를 선택 합니다.

9. 선택 **만들기** toocreate hello ASE 합니다. 이 프로세스는 또한 hello 앱 서비스 계획 및 hello 앱을 만듭니다. 동일한 구독 hello 및 또한에 동일한를 hello hello ASE, 앱 서비스 계획 및 응용 프로그램 내에서 리소스 그룹입니다. 프로그램 ASE 필요한 별도 리소스 그룹 또는 ILB ASE 해야 할 경우 자체적으로 hello 단계 toocreate를 ASE를 따릅니다.

## <a name="create-an-ase-by-itself"></a>단독으로 ASE 만들기 ##

ASE 독립 실행형을 만드는 경우 내부에는 아무것도 없습니다. 여전히 빈 ASE hello 인프라에 대 한 월별 요금을 부과 됩니다. 이러한 단계 toocreate는 ilb ASE 또는 자체 리소스 그룹에 toocreate ASE 따릅니다. 프로그램 ASE를 만든 후에 hello 일반적인 프로세스를 사용 하 여 앱을 만들 수 있습니다. 새 프로그램 ASE hello 위치로 선택 합니다.

1. 검색에 대 한 Azure 마켓플레이스 hello **앱 서비스 환경**, 선택 또는 **새로** > **웹 모바일** > **앱 서비스 환경**합니다. 

2. 프로그램 ASE hello 이름을 입력 합니다. 이 이름은 hello ASE에에서 만든 hello 앱에 사용 됩니다. Hello 이름이 *mynewdemoase*, hello 하위 도메인 이름이 *. mynewdemoase.p.azurewebsites.net*합니다. *mytestapp*이라는 앱을 만든 경우 mytestapp.mynewdemoase.p.azurewebsites.net으로 주소를 지정할 수 있습니다. Hello 이름에 공백을 사용할 수 없습니다. 대문자를 사용 하는 경우 hello 도메인 이름은 hello hello 이름의 총 소문자 버전입니다. ILB를 사용하는 경우 ASE 이름이 하위 도메인에서 사용되지 않는 대신 ASE를 만드는 동안에 명시적으로 지정됩니다.

    ![ASE 이름 지정][5]

3. 사용 중인 구독을 선택합니다. 이 구독은 하나 ASE hello에서 모든 앱에서 사용 하는 hello 이기도 합니다. 다른 구독에 있는 VNet에 ASE를 배치할 수 없습니다.

4. 새 리소스 그룹을 선택하거나 지정합니다. hello 리소스 그룹에 ASE에 사용 되는 hello VNet에 사용 되는 동일한 1 이어야 합니다. Hello 리소스 그룹을 선택 하면 ASE에 대 한 업데이트 된 tooreflect은 기존 VNet을 선택한 경우 VNet의 합니다. *리소스 관리자 템플릿을 사용 하는 경우에 hello VNet 리소스 그룹에서 다른 리소스 그룹으로 ASE를 만들 수 있습니다.* 템플릿에서 ASE toocreate 참조 [템플릿에서 앱 서비스 환경 만들기][MakeASEfromTemplate]합니다.

    ![리소스 그룹 선택][6]

5. VNet 및 위치를 선택합니다. 새 VNet을 만들거나 기존 VNet을 선택할 수 있습니다. 

    * 새 VNet을 선택하면 이름 및 위치를 지정할 수 있습니다. hello 새 VNet에 hello 주소 범위 192.168.250.0/23 및 default 라는 서브넷 있습니다. hello 서브넷 192.168.250.0/24로 정의 됩니다. Resource Manager VNet만 선택할 수 있습니다. hello **VIP 유형** 선택에 따라 결정 하면 ASE에서 직접 액세스할 수 있는 경우 인터넷 (외부) hello 받는 ILB를 사용 하는 경우 또는 합니다. 이러한 옵션에 대해 자세히 toolearn 참조 [만들기 및 사용 하는 앱 서비스 환경과 내부 부하 분산 장치][MakeILBASE]합니다. 

      * 선택 하는 경우 **외부** hello에 대 한 **VIP 유형**, 개수 외부 IP 주소 hello 시스템은 IP 기반 SSL 위해 사용 하 여 만든 선택할 수 있습니다. 
    
      * 선택 하는 경우 **내부** hello에 대 한 **VIP 유형**, 프로그램 ASE를 사용 하는 hello 도메인을 지정 해야 합니다. 공개 또는 개인 주소 범위를 사용하는 VNet으로 ASE를 배포할 수 있습니다. 공용 주소 범위와 VNet toouse 미리 toocreate hello VNet 필요합니다. 
    
    * 기존 VNet을 선택한 경우에 새 서브넷 hello ASE를 만들 때 만들어집니다. *Hello 포털에서 미리 생성된 된 서브넷을 사용할 수 없습니다. Resource Manager 템플릿을 사용하는 경우 기존 서브넷으로 ASE를 만들 수 있습니다.* 템플릿에서 ASE toocreate 참조 [템플릿에서 앱 서비스 환경 만들기][MakeASEfromTemplate]합니다.

## <a name="app-service-environment-v1"></a>App Service 환경 v1 ##

여전히 hello 첫 번째 버전 앱 서비스 환경 (ASEv1)의 인스턴스를 만들 수 있습니다. 처리, 검색 hello 마켓플레이스 toostart에 대 한 **앱 서비스 환경 v1**합니다. Hello에 hello ASE를 만들면 동일한 방식으로 hello 독립 실행형 ASE를 만들어야 합니다. 완료되면 ASEv1에 두 개의 프런트 엔드 및 두 명의 작업자가 있습니다. ASEv1와 hello 프런트 엔드와 작업자를 관리 해야 합니다. 이는 App Service 계획을 만들 때 자동으로 추가되지 않습니다. hello 프런트 엔드 역할 hello HTTP/HTTPS 끝점을 하 고 toohello 작업자 트래픽을 전송 합니다. hello 작업자는 앱을 호스트 하는 hello 역할입니다. 프로그램 ASE를 만든 후 프런트 엔드 및 근로자의 hello 수량을 조정할 수 있습니다. 

toolearn ASEv1에 대 한 자세한 참조 [소개 toohello 앱 서비스 환경 v1][ASEv1Intro]합니다. 확장에 대 한 자세한 내용은 관리 및 모니터링 ASEv1, 참조 [어떻게 tooconfigure 앱 서비스 환경][ConfigureASEv1]합니다.

<!--Image references-->
[1]: ./media/how_to_create_an_external_app_service_environment/createexternalase-create.png
[2]: ./media/how_to_create_an_external_app_service_environment/createexternalase-aspcreate.png
[3]: ./media/how_to_create_an_external_app_service_environment/createexternalase-pricing.png
[4]: ./media/how_to_create_an_external_app_service_environment/createexternalase-embeddedcreate.png
[5]: ./media/how_to_create_an_external_app_service_environment/createexternalase-standalonecreate.png
[6]: ./media/how_to_create_an_external_app_service_environment/createexternalase-network.png



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

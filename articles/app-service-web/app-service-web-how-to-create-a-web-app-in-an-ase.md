---
title: "앱 서비스 환경 v1의 웹 앱 aaaCreate"
description: "Toocreate 웹 앱 및 앱 서비스 환경 v1에서 앱 서비스 계획 방법에 대해 알아봅니다"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 983ba055-e9e4-495a-9342-fd3708dcc9ac
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 322ef344517c54247b102fb4920e35645986ef98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-an-app-service-environment-v1"></a>App Service Environment v1에서 웹앱 만들기

> [!NOTE]
> 앱 서비스 환경 v1 hello에 대 한이 문서는입니다.  최신 버전의 hello 쉽게 toouse 되며 더 강력한 인프라에서 실행 하는 앱 서비스 환경 있습니다. hello로 시작 하는 hello 새 버전에 대 한 자세한 toolearn [소개 toohello 앱 서비스 환경](../app-service/app-service-environment/intro.md)합니다.
> 

## <a name="overview"></a>개요
이 자습서에서는 어떻게 toocreate 웹 앱 및 앱 서비스 계획에 [앱 서비스 환경 v1](app-service-app-service-environment-intro.md) (ASE). 

> [!NOTE]
> 어떻게 toolearn 사용 하려는 경우 toocreate 웹 응용 프로그램 toodo 필요 하지 않은 있지만 앱 서비스 환경에서 참조 [.NET 웹 앱을 만듭니다](app-service-web-get-started-dotnet.md) 또는 다른 언어 및 프레임 워크에 대 한 자습서 관련 hello 중 하나입니다.
> 
> 

## <a name="prerequisites"></a>필수 조건
이 자습서는 앱 서비스 환경을 만든 적이 있는 개발자를 대상으로 합니다. 만들어 본 적이 없는 경우 [앱 서비스 환경 만들기](app-service-web-how-to-create-an-app-service-environment.md)를 참조하세요. 

## <a name="create-a-web-app"></a>웹앱 만들기
1. Hello에 [Azure 포털](https://portal.azure.com/), 클릭 **새로 만들기 > 웹 + 모바일 > 웹 응용 프로그램**합니다. 
   
    ![][1]
2. 사용 중인 구독을 선택합니다.  
   
    여러 구독이 있는 경우 주의 해야 할 앱 서비스 환경에서 응용 프로그램에서 해당 toocreate, toouse hello hello 환경을 만들 때 사용한 동일한 구독 합니다. 
3. 리소스 그룹을 선택하거나 만듭니다.
   
    *리소스 그룹* toomanage 하면 관련 Azure 리소스를 한 단위로 되며 유용 설정할 때 사용 *역할 기반 액세스 제어* 앱에 대 한 규칙 (RBAC). 자세한 내용은 [Azure Resource Manager 개요][ResourceGroups]를 참조하세요. 
4. 앱 서비스 계획을 선택하거나 만듭니다.
   
    *App Service 계획*은 관리되는 웹앱 집합입니다.  일반적으로 가격을 선택 하면 청구 hello 가격 적용된 toohello toohello 개별 앱 대신 앱 서비스 계획입니다. Hello 계산에 대 한 비용을 지불 ASE에 인스턴스 toohello ASE를 할당 하면 asp 나열 했는지도 대신 합니다.  앱 서비스 계획의 hello 인스턴스를 확장할 tooscale hello 웹 응용 프로그램의 인스턴스 수를 하 고 해당 계획의 hello 웹 앱을 모두 영향을 합니다.  사이트 슬롯 또는 VNET 통합 같은 일부 기능은 hello 계획 내에서 수량 제한 사항을 갖게 됩니다.  자세한 내용은 [Azure App Service 계획 개요](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)를 참조하세요.
   
    Hello 계획 이름 아래에서 설명한 hello 위치를 확인 하 여 프로그램 ASE에 hello 앱 서비스 계획을 식별할 수 있습니다.  
   
    ![][5]
   
    앱 서비스 환경에 이미 존재 하는 앱 서비스 계획 toouse를 원하는 경우 해당 계획을 선택 합니다. Toocreate 새 앱 서비스 계획을 사용 하도록 하려는 경우 다음이 자습서의 단원을 hello 참조 [앱 서비스 환경에 앱 서비스 계획 만들기](#createplan)합니다.
5. 웹 앱에 대 한 hello 이름을 입력 한 다음 클릭 **만들기**합니다. 
   
    프로그램 ASE ASE에 응용 프로그램에 대 한 외부 VIP hello URL을 사용 하는 경우: [*sitename*]. [ *앱 서비스 환경 이름*]. 대신 p.azurewebsites.net [*sitename*]. azurewebsites.net
   
    프로그램 ASE 않다는 ASE 응용 프로그램에 대 한 내부 VIP 다음 hello URL을 사용 하는 경우: [*sitename*]. [ *ASE 만들 때 지정한 하위 도메인*]   
    아래 업데이트 hello 하위 도메인을 보게 ASE 만드는 동안 하면 ASP를 선택한 후 **이름**

## <a name="createplan"></a> 앱 서비스 계획 만들기
앱 서비스 환경에서 앱 서비스 계획을 만들 때 ASE에 공유 작업자가 없기 때문에 작업자 선택이 다릅니다.  toouse 해야 하는 hello 작업자는 hello hello 관리자 toohello ASE 할당 된 것과  즉, 해당 toocreate 새 계획을 통해 모든 해당 작업자 풀에 이미 있는 관리 toohave hello 총 인스턴스 수 보다 더 많은 할당 된 작업자 tooyour ASE 작업자 풀 필요 합니다.  충분 한 작업자에에서 없는 프로그램 ASE 작업자 풀 toocreate 계획을 추가 하 여 ASE admin tooget와 할 toowork 있습니다.

앱 서비스 환경에서 호스트 하는 앱 서비스 계획을 가진 또 다른 차이점은 선택 가격 hello 부족 합니다.  앱 서비스 환경에 있는 경우 hello 시스템에서 사용 하는 계산 리소스에 대 한 부담 하 고 해당 환경에서 추가 된 요금 hello 계획에 대 한 권한이 없습니다.  일반적으로 앱 서비스 계획을 만들 때 청구를 결정하는 가격 책정 계획을 선택합니다.  앱 서비스 환경은 기본적으로 콘텐츠를 만들 수 있는 개인 위치입니다.  콘텐츠 hello 환경과 하지 toohost에 지불합니다.

hello 한 지침은 다음과 hello hello 자습서의 이전 섹션에 설명 된 대로 웹 응용 프로그램을 만드는 동안 toocreate 앱 서비스 계획 하는 방법입니다.

1. 클릭 **새로 만들기** 에 계획 선택 UI hello 하 고 일반적으로 외부 ASE 것 처럼 계획에 대 한 이름을 제공 합니다.
2. 위치 선택에서 toouse 되도록 hello ASE를 선택 합니다.
   
    앱 서비스 환경이 기본적으로 개인 배포 위치이기 때문에 위치에 표시됩니다. 
   
    ![][2]
   
    Hello 위치 선택에서 ASE 선택한 후 hello 앱 서비스 계획 만들기 UI 업데이트합니다.  hello 위치 이제 표시 hello ASE 시스템의 hello 이름과 hello 지역에 고 가격 계획 선택 hello 작업자 풀 선택기 대체 됩니다.  
   
    ![][3]

### <a name="selecting-a-worker-pool"></a>작업자 풀 선택
일반적으로 Azure 앱 서비스 및 앱 서비스 환경 외부에서 전용된 가격 계획의 hello 선택 하 여 사용할 수 있는 3 가지 계산 크기는 합니다.  유사한 방식 ASE에 대 한 정의 too3 풀의 작업자를 하 고 수 해당 작업자 풀에 사용 되는 hello 계산 크기를 지정 합니다.  hello ASE 앱 서비스 계획에 대 한 계산 크기가 요금제를 선택 하는 대신 선택 하는 요청 된 것은 테 넌 트에 대 한 의미를 *작업자 풀*합니다.  

hello 작업자 풀 선택 UI hello 이름 아래에 해당 작업자 풀에 사용 되는 hello 계산 크기를 보여 줍니다.  hello 수 있는 수량 참조 toohow 많은 계산 인스턴스는 해당 풀에서 사용할 수 있습니다.  hello 총 풀이이 값 보다 더 많은 인스턴스를 포함 실제로 될 수도 있지만이 값이 toosimply 참조 개수 사용 하지 않는 합니다.  Tooadjust 해야 할 경우 앱 서비스 환경 tooadd 더 계산 리소스를 참조 하십시오 [앱 서비스 환경 구성](app-service-web-configure-an-app-service-environment.md)합니다.

![][4]

이 예제에서는 사용 가능한 작업자 풀이 두 개뿐인 것을 확인합니다. ASE 관리자에 게 할당 된 호스트를 이러한 두 작업자 풀으로 때문입니다.  hello 셋째 나타납니다 Vm에 할당 된 경우.  

## <a name="after-web-app-creation"></a>웹앱을 만든 후
실행 중인 웹 응용 프로그램 및 toobe 고려를 해야 하는 ASE에 앱 서비스 계획을 관리 하기 위한 몇 가지 고려 사항이 있습니다.  

Hello ASE hello 소유자가 hello 시스템의 hello 크기에 대해 설명한 것 처럼 있으며 결과적으로 책임에 앱 서비스 계획에 필요한 충분 한 용량 toohost hello 지 확인 합니다. 사용 가능한 작업자가 있는 경우는 금지 됩니다 수 toocreate 앱 서비스 계획 수입니다.  웹 앱을 true tooscaling 이기도합니다.  더 많은 인스턴스 필요한 경우 tooget 앱 서비스 환경 관리 tooadd 해야 추가 작업 자가 있습니다.

웹 앱과 앱 서비스 계획을 만든 후 것이 좋습니다 tooscale 설정 합니다.  ASE에 항상 응용 프로그램을 위한 하거나 앱 서비스 계획 tooprovide 내결함성 toohave 2 개 이상 인스턴스를 필요 합니다.  앱 서비스 계획 UI hello를 통해 일반적인 방법으로 동일한 hello ASE에는 계획은 응용 프로그램 서비스를 크기 조정.  를 확장 하는 방법에 대 한 자세한 내용은 [어떻게 tooscale 앱 서비스 환경에 웹 앱](app-service-web-scale-a-web-app-in-an-app-service-environment.md)

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspnewwebapp.png
[2]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createasplocation.png
[3]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspselected.png
[4]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspworkerpool.png
[5]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/selectaspinase.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoScale]: http://azure.microsoft.com/documentation/articles/app-service-web-scale-a-web-app-in-an-app-service-environment
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment
[ResourceGroups]: ../azure-resource-manager/resource-group-overview.md
[AzurePowershell]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/

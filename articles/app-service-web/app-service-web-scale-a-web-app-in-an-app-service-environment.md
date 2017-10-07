---
title: "aaaHow tooScale 앱 서비스 환경에 응용 프로그램"
description: "앱 서비스 환경에서 앱 확장"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: jimbe
ms.assetid: 78eb1e49-4fcd-49e7-b3c7-f1906f0f22e3
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: ccompy
ms.openlocfilehash: 08916eac056c46bf8cb6edffbf96285317b32062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-apps-in-an-app-service-environment"></a>앱 서비스 환경에서 앱 확장
Hello Azure 앱 서비스에서에서 일반적으로 다음 세 가지 크기를 조정할 수 있습니다.

* 가격 계획
* 작업자 크기 
* 인스턴스 수

ASE에 계획 가격 책정 필요 tooselect 또는 변경 hello 있습니다.  기능적인 측면에서 이미 프리미엄 가격 기능 수준이기 때문입니다.  

존중 tooworker 크기 ASE admin 님 안녕하세요 hello 각 작업자 풀에 사용 되는 계산 리소스 toobe의 hello 크기를 지정할 수 있습니다.  따라서 필요한 경우 P4 계산 리소스가 있는 작업자 풀 1과 P1 계산 리소스가 있는 작업자 풀 2를 둘 수 있습니다.  크기 순서로 toobe를 갖지 않습니다.  자세한 내용은 hello 크기와 해당 가격 책정 hello 문서 여기를 참조 하세요. [Azure 앱 서비스 가격 책정][AppServicePricing]합니다.  이러한 컴퓨터는 hello 배율 앱 서비스 환경 toobe에 웹 앱 및 앱 서비스 계획에 대 한 옵션:

* 작업자 풀 선택
* 인스턴스 수

Hello를 통해 이루어집니다 항목 중 하나가 변경 프로그램 ASE 앱 서비스 계획을 호스트에 대해 표시 된 UI 적절 합니다.  

![][1]

Hello 하면 ASP에 있는 hello 작업자 풀의 사용 가능한 계산 리소스 수가 초과 하면 ASP를 확장할 수 없습니다.  해당 작업자 풀의 리소스를 계산 해야 하는 경우 필요한 tooget ASE 관리자 tooadd 해당 합니다.  여기에 hello 정보를 읽을 프로그램 ASE를 다시 구성에 대 한 정보: [어떻게 tooConfigure 앱 서비스 환경][HowtoConfigureASE]합니다.  Hello ASE 자동 크기 조정 기능 tooadd 용량 메트릭 또는 일정에 따라 tootake 활용할을 수도 있습니다.  자체 hello ASE 환경에 대 한 자동 크기 조정 구성에 대 한 자세한 내용은 참조는 tooget [어떻게 앱 서비스 환경에 대 한 자동 크기 조정 tooconfigure][ASEAutoscale]합니다.

여러 응용 프로그램 서비스 계획을 계산 리소스를 사용 하 여 다른 작업자 풀에서 만들거나 사용할 수 있습니다 동일한 작업자 풀 hello 합니다.  예제 (10) 사용할 수 있는 계산 리소스 작업자에 있는 경우 풀 1, (6) 계산 리소스를 사용 하 여 toocreate 하나의 앱 서비스 계획을 선택할 수 있습니다 및 두 번째 응용 프로그램 서비스 계획을 대 (4) 계산 리소스를 사용 합니다.

### <a name="scaling-hello-number-of-instances"></a>인스턴스 크기 조정 hello 수
앱 서비스 환경에서 웹앱을 처음 만드는 경우 1개의 인스턴스로 시작합니다.  컴퓨터 앱에 대 한 리소스를 추가 tooadditional 인스턴스 tooprovide 확장 한 다음 할 수 있습니다.   

ASE의 용량이 충분한 경우에는 매우 간단합니다.  Tooyour tooscale를을 크기 조정 선택 hello 사이트를 보유 하는 앱 서비스 계획 서 합니다.  Hello 하거나 수 있는 수동으로 하면 ASP에 대 한 hello 비율을 설정 하면 ASP에 대 한 자동 크기 조정 규칙을 구성 하는 UI가 열립니다.  앱 설정 하기만 toomanually 배율 ***하 여 확장할*** 너무***수동으로 입력 한 인스턴스 수***합니다.  여기에서 hello 슬라이더 원하는 toohello quantity를 끌어 또는 hello 상자 다음 toohello 슬라이더에 입력 합니다.  

![][2] 

ASE 작업에서는 ASP에 대 한 자동 크기 조정 규칙 hello hello 일반적으로 것과 동일 합니다.  ***확장 기준***에 있는 ***CPU 비율***을 선택하여 CPU 비율에 따라 ASP에 대한 자동 크기 조정 규칙을 만들거나 ***일정 및 성능 규칙***을 사용하여 좀 더 복잡한 규칙을 만들 수 있습니다.  보다 완전 한 자동 크기 조정을 사용 하 여 hello 가이드 여기를 구성 하는 방법에 대 한 세부 정보 toosee [Azure 앱 서비스에서 앱의 크기를 조정][AppScale]합니다. 

### <a name="worker-pool-selection"></a>작업자 풀 선택
앞에서 설명한 대로 hello 작업자 풀 선택 hello ASP UI에서에서 액세스 됩니다.  ASP tooscale 원하고 작업자 풀 선택 hello에 대 한 hello 블레이드를 엽니다.  앱 서비스 환경에 구성 hello 작업자 풀의 모든 표시 됩니다.  하나의 작업자 풀을 보유 하는 경우 다음만 표시 됩니다 hello 하나의 풀이 나열 합니다.  toochange 어떤 작업자 하면 ASP를 풀에 있으면 하 여 앱 서비스 계획 toomove 원하는 hello 작업자 풀을 선택 하기만 하면 됩니다.  

![][3]

하나의 작업자 풀 tooanother에서 하면 ASP를 이동 하기 전에 ASP 프로그램에 대 한 적절 한 용량 했는지 확인 하는 중요 한 toomake 것 합니다.  작업자 풀의 hello 목록의 hello 작업자 풀 이름이 나열 된 뿐만 아니라 해당 작업자 풀에서 작업자 수를 사용할 수 있는 확인할 수 있습니다.  없는지 인스턴스 사용 가능한 toocontain 충분 한 앱 서비스 계획을 확인 합니다.  원하는 ASE 관리자 tooadd를 가져온 후에 toomove hello 작업자 풀의 리소스를 더 계산 해야 하는 경우 해당 합니다.  

> [!NOTE]
> 해당 ASP에서 hello 앱의 시작 하나의 작업자 풀에서 ASP 콜드 하면 이동 합니다.  느린 앱은 새 계산 리소스 hello에서 시작 콜드 요청 toorun을 발생할 수 있습니다.  hello 콜드 시작 방지할 수 있습니다 hello를 사용 하 여 [응용 프로그램 기능 준비] [ AppWarmup] Azure 앱 서비스의 합니다.  hello 문서에서 설명 하는 hello 응용 프로그램 초기화 모듈 hello 초기화 프로세스는 앱에는 추 새 계산 리소스에서 시작 하는 경우에 호출 하기 때문에 콜드 시작에 대해서도 작동 합니다. 
> 
> 

## <a name="getting-started"></a>시작
앱 서비스 환경 시작 tooget 참조 [어떻게 tooCreate An 앱 서비스 환경][HowtoCreateASE]

Azure 앱 서비스 플랫폼 hello에 대 한 자세한 내용은 참조 [Azure 앱 서비스][AzureAppService]합니다.

<!--Image references-->
[1]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-aspblade.png
[2]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-manualscale.png
[3]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-sizescale.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ScaleWebapp]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[CreateWebappinASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-a-web-app-in-an-ase/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[AppScale]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[AppWarmup]: http://ruslany.net/2015/09/how-to-warm-up-azure-web-app-during-deployment-slots-swap/

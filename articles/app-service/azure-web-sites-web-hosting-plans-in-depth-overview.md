---
title: "aaaAzure 앱 서비스 계획 심도 깊은 개요 | Microsoft Docs"
description: "Azure 앱 서비스에 대한 앱 서비스 계획의 작동 방식 및 이러한 계획을 통해 관리 환경을 향상시킬 수 있는 방법을 알아봅니다."
keywords: "앱 서비스, Azure 앱 서비스, 규모, 확장성, 앱 서비스 계획, 앱 서비스 비용"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: b384790d9e69b234ca69ac591164c48a4b6ed210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a>Azure 앱 서비스 계획의 포괄 개요

앱 서비스 계획을 사용 하는 실제 리소스 toohost의 hello 컬렉션 응용을 프로그램을 나타냅니다.

App Service 계획은 다음을 정의합니다.

- 지역(미국 서부, 미국 동부 등)
- 확장 개수(1, 2, 3개 인스턴스 등)
- 인스턴스 크기(소, 중, 대)
- SKU(무료, 공유, 기본, 표준, 프리미엄)

[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)의 Web Apps, Mobile Apps, API Apps, 함수 앱(또는 함수)은 모두 App Service 계획에서 실행됩니다.  앱에서 hello 같은 구독과 지역을 공유할 수 앱 서비스 계획 합니다. 

모든 응용 프로그램 할당 tooan **앱 서비스 계획** 에서 정의한 hello 리소스를 공유 합니다. 따라서 단일 App Service 계획에서 여러 앱을 호스팅할 때 비용을 절감할 수 있습니다.

프로그램 **앱 서비스 계획** 에서 확장할 수 **무료** 및 **Shared** Sku 너무**기본**, **표준**, 및 **프리미엄** toomore 리소스 및 hello 따라 기능을 제공 하는 Sku 액세스 방법입니다.

앱 서비스 계획에 너무 설정 되어 있으면**기본** SKU 또는 그 이상으로 hello를 제어할 수 있습니다 다음 **크기** hello Vm의 수를 크기 조정 하 고 있습니다.

예를 들어 hello standard 서비스 계층에 구성 된 toouse 두 "small" 인스턴스 계획을 사용 하는 경우 해당 계획과 연결 된 모든 앱 인스턴스 모두 실행 됩니다. 앱은 액세스 toohello standard 서비스 계층 기능을 가진 합니다. 앱을 실행 중인 계획 인스턴스는 완전히 관리되며 가용성이 높습니다.

> [!IMPORTANT]
> hello **SKU** 및 **배율** 의 hello 앱 서비스 계획에 호스팅된 앱 hello 비용과 hello 하지 수를 결정 합니다.

이 문서는 hello 키 등의 특성 계층, 앱 서비스 계획의 소수 자릿수 및 앱을 관리 하는 동안 재생 발휘 방법을 탐색 합니다.

## <a name="apps-and-app-service-plans"></a>앱 및 앱 서비스 계획

앱 서비스의 앱은 주어진 시간에 항상 하나의 앱 서비스 계획에만 연결될 수 있습니다.

앱과 계획은 둘 다 **리소스 그룹**에 포함됩니다. 리소스 그룹 내에 있는 모든 리소스에 대 한 hello 수명 주기 경계 역할을 합니다. 있습니다 수 사용 하 여 리소스 그룹 toomanage 응용 프로그램의 모든 hello 조각을.

단일 리소스 그룹에 앱 서비스 계획을 여러 개 있을 수 있지만, 때문에 다양 한 앱을 toodifferent 물리적 리소스 할당할 수 있습니다.

예를 들어 개발, 테스트 및 프로덕션 환경 간에 리소스를 구분할 수 있습니다. 프로덕션 및 개발/테스트에 대해 별도의 환경을 두면 리소스를 격리할 수 있습니다. 이러한 방식으로 새 버전의 앱에 대해 부하 테스트 경합 하지 않습니다 hello에 대 한 동일한 실제 고객의 서비스를 제공는 프로덕션 응용 프로그램으로 리소스에 있습니다.

단일 리소스 그룹에 여러 계획이 있는 경우 지역에 걸쳐 있는 응용 프로그램을 정의할 수도 있습니다.

예를 들어 두 개의 지역에서 실행되는 고가용성 앱에는 각 지역별로 하나씩 두 개 이상의 계획이 포함되고 각 계획과 연결된 앱이 하나씩 포함됩니다. 이러한 경우 hello 응용 프로그램의 모든 hello 복사본 다음 단일 리소스 그룹에 포함 됩니다. 여러 계획 및 여러 앱에서 있는 리소스 그룹을 사용 하면 쉽게 toomanage, 제어 및 hello 응용 프로그램의 hello 상태 보기입니다.

## <a name="create-an-app-service-plan-or-use-existing-one"></a>App Service 계획 만들기 또는 기존 계획 사용

앱을 만들 때 리소스 그룹을 만드는 것을 고려해야 합니다. 이 앱은 더 큰 응용 프로그램에 대 한 구성 요소를 hello에, 해당 더 큰 응용 프로그램에 할당 되는 hello 리소스 그룹 내에 만들어집니다.

Hello 앱은 완전히 새로운 응용 프로그램 또는 큰의 일부 인지 선택할 수 있습니다 toouse는 기존 계획 toohost 것 하거나 새로 만듭니다. 이 선택은 용량과 예상 부하에 따라 결정됩니다.

다음의 경우 새 App Service 계획으로 앱을 격리하는 것이 좋습니다.

- 앱이 리소스를 많이 사용합니다.
- 앱에는 기존 계획에서 호스트 되는 다른 앱에서 hello 다른 배율 인수.
- 앱에 서로 다른 지역의 리소스가 필요합니다.

이 방식을 사용하면 앱에 새 리소스 집합을 할당하고 앱을 더 잘 제어할 수 있습니다.

## <a name="create-an-app-service-plan"></a>App Service 계획 만들기

> [!TIP]
> 앱 서비스 환경을 설정한 경우에 hello 설명서 특정 tooApp 서비스 환경 여기을 검토할 수 있습니다: [앱 서비스 환경에 앱 서비스 계획 만들기](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)

앱 서비스 계획 찾아보기 경험 hello 또는 응용 프로그램 생성의 일환으로 빈 앱 서비스 계획을 만들 수 있습니다.

Hello에 [Azure 포털](https://portal.azure.com), 클릭 **새로** > **웹 + 모바일**, 선택한 후 **웹 앱** 또는 다른 앱 서비스 응용 프로그램 종류입니다.

![Hello Azure 포털에서에서 앱을 만듭니다.][createWebApp]

다음을 선택 하거나 hello hello 새 응용 프로그램에 대 한 앱 서비스 계획을 만들 수 있습니다.

 ![앱 서비스 계획을 만듭니다.][createASP]

toocreate 앱 서비스 계획을 클릭 하 여 **[+] Create New**, 형식 hello **앱 서비스 계획** 이름을 지정 하 고 다음 적절 한 선택 **위치**합니다. 클릭 **가격 책정 계층**, 한 다음 hello 서비스에 대 한 적절 한 가격대를 선택 합니다. 선택 **모든 보기** 더와 같은 옵션, 가격 책정 tooview **무료** 및 **Shared**합니다. Hello 가격 책정 계층을 선택한 후 클릭 hello **선택** 단추입니다.

## <a name="move-an-app-tooa-different-app-service-plan"></a>앱 다른 앱 서비스 계획을 tooa 이동

Hello 앱 tooa 다른 앱 서비스 계획을 이동할 수 [Azure 포털](https://portal.azure.com)합니다. Hello에 hello 계획 되는 응용 프로그램 계획 간에 이동할 수 있습니다 동일한 리소스 그룹 및 지역입니다.

toomove 앱 tooanother 계획:

- 원하는 toomove toohello 응용 프로그램을 이동 합니다.
- Hello에 **메뉴**, hello에 대 한 확인 **앱 서비스 계획** 섹션.
- 선택 **변경 앱 서비스 계획** toostart hello 프로세스입니다.

**앱 서비스 계획 변경** 열립니다 hello **앱 서비스 계획** 선택기입니다. 이 시점에서이 응용 프로그램에는 기존 계획 toomove를 선택할 수 있습니다.

> [!IMPORTANT]
> 앱 서비스 계획을 선택 하는 hello. UI hello 다음 기준으로 필터링 됩니다.
> - 내에 있는 hello 동일한 리소스 그룹
> - 동일한 hello에 있는 지리적 위치 영역
> - 내에 있는 hello 동일한 웹 공간
>
> 웹 공간은 서버 리소스의 그룹화를 정의하는 App Service 내의 논리적 구문입니다. 지역 (예: 미국 서 부) 응용 프로그램 서비스를 사용 하는 순서 tooallocate 고객에서 웹 스페이스에 많은 포함 되어 있습니다. 현재 응용 프로그램 서비스 리소스 수 toobe 웹 스페이스에 간에 이동 되지 않습니다.
>

![앱 서비스 계획 선택기입니다.][change]

각 계획에는 고유한 가격 책정 계층이 있습니다. 예를 들어 tooit toouse hello 기능과 hello 표준 계층의 리소스를 할당 하는 모든 앱을 사용 하면 사이트를 무료 계층 tooa 표준 계층에서에서으로 이동 합니다.

## <a name="clone-an-app-tooa-different-app-service-plan"></a>응용 프로그램 tooa 다른 앱 서비스 계획 복제

Toomove hello 앱 tooa 다른 지역의 경우 하나는 응용 프로그램 복제 합니다. 복제를 수행하면 모든 하위 지역의 새로운 또는 기존 App Service 계획으로 앱이 복사됩니다.

찾을 수 있습니다 **복제 앱** hello에 **개발 도구** hello 메뉴의 섹션입니다.

> [!IMPORTANT]
> 복제에는 몇 가지 제한이 있으며 [Azure 포털을 사용하여 Azure 앱 서비스 앱 복제](../app-service-web/app-service-web-app-cloning-portal.md)에서 이에 대해 읽을 수 있습니다.

## <a name="scale-an-app-service-plan"></a>앱 서비스 계획 크기 조정

세 가지 방법으로 tooscale 계획

- **변경 hello 계획 가격 책정 계층**합니다. 모든 앱 할당 tooit toouse hello 표준 계층의 hello 기능 있으며 hello 기본 계층의 계획에는 변환 된 tooStandard 수 있습니다.
- **Hello 계획의 인스턴스 크기를 변경**합니다. 예를 들어, 작은 인스턴스를 사용 하는 hello 기본 계층의 계획에는 변경 된 toouse 큰 인스턴스 수 있습니다. 에 해당 계획과 연결 된 모든 앱 hello 추가 메모리와 CPU 리소스를 더 큰 인스턴스 크기 제공 hello 사용할 수 있습니다.
- **Hello 계획 인스턴스 수 변경**합니다. 예를 들어 toothree 인스턴스 확장은 표준 계획 크기 조정 된 too10 인스턴스 수 있습니다. 프리미엄 요금제 too20 인스턴스 (제목 tooavailability) 확장할 수 있습니다. 에 해당 계획과 연결 된 모든 앱 hello 추가 메모리와 CPU 리소스를 더 큰 인스턴스 개수 제공 hello에 사용할 수 있습니다.

Hello hello를 클릭 하 여 가격 책정 계층 및 인스턴스 크기를 변경할 수 있습니다 **크기 확장** hello 앱 또는 앱 서비스 계획 hello에 대 한 설정 항목입니다. 변경은 toohello 앱 서비스 계획을 적용 하 고 호스트 되는 모든 앱에 영향을 줍니다.

 ![응용 프로그램을 tooscale 값을 설정 합니다.][pricingtier]

## <a name="app-service-plan-cleanup"></a>App Service 계획 정리

> [!IMPORTANT]
> **앱 서비스 계획** 한 요금은 계속 청구 tooreserve hello 계산 용량을 계속 있으므로 연결 앱 toothem 없습니다.

tooavoid 예기치 않은 요금, 앱 서비스 계획에서 호스트 되는 hello 마지막 앱이 삭제 되 면 hello 결과 비어 있는 앱 서비스 계획도 삭제 됩니다.

## <a name="summary"></a>요약

앱 서비스 계획은 앱 간에 공유할 수 있는 기능 및 용량 집합을 나타냅니다. 앱 서비스 계획은 유연성 tooallocate 특정 앱 tooa 리소스 집합이 hello 및 Azure 리소스 사용률을 최적화할 제공 합니다. 이러한 방식으로 테스트 환경의 toosave money를 원하는 경우 여러 앱 간에 계획을 공유할 수 있습니다. 여러 지역과 계획에 걸쳐 크기를 조정하여 프로덕션 환경의 생산량을 최대화할 수도 있습니다.

## <a name="whats-changed"></a>변경된 내용

- 가이드 toohello 변경 tooApp 웹 사이트 서비스에서에서 참조: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png

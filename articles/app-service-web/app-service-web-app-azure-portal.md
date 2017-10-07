---
title: "hello Azure 포털을 탐색 하기 위한 aaaReference"
description: "Hello 관리 포털 및 Azure 포털 hello 간에 응용 프로그램 서비스 웹 용 hello 다른 사용자 환경에 알아보기"
services: app-service
documentationcenter: 
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: dcf7c1fc17f9a0c31005ad0f2fd53723d2966058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reference-for-navigating-hello-azure-portal"></a>Hello Azure 포털을 탐색 하는 것에 대 한 참조
Azure 웹 사이트를 이제 [앱 서비스 웹앱](http://go.microsoft.com/fwlink/?LinkId=529714)이라고 합니다. त ु म च 모두 우리의 설명서 tooreflect hello Azure 포털에 대 한이 이름 변경 및 tooprovide 지침. 해당 프로세스를 완료 될 때까지 hello Azure 포털에서에서 웹 응용 프로그램 작업에 대 한 지침으로이 문서를 사용할 수 있습니다.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="hello-future-of-hello-azure-classic-portal"></a>hello Azure 클래식 포털의 hello 미래
Hello Azure 클래식 포털의 변경 내용이 브랜딩 hello 알게 될 동안 대체 되 고 hello Azure 포털의 hello 프로세스에서 해당 포털은입니다. Hello 클래식 포털 단계적, 대로 toohello Azure 포털 새로운 개발에 대 한 hello 포커스는 변화 하는 합니다. Hello Azure 포털에서에서 웹 앱에 대 한 예정 된 새로운 기능을 모두 제공 됩니다. 최신이 고 웹 응용 프로그램 toooffer 한지 가장 hello 활용 Azure 포털 tootake hello를 사용 하 여 시작 합니다.

## <a name="layout-differences-between-hello-azure-classic-portal-and-azure-portal"></a>레이아웃 hello Azure 클래식 포털 및 Azure 포털의 차이점
Hello 클래식 포털에서 Azure hello 모든 서비스는 hello 왼쪽에 표시 됩니다. Hello 클래식 포털에서 탐색 hello 서비스에서 시작 하 고 각 요소 트리로 이동 하는 트리 구조를 따릅니다. 이 구조는 독립 구성 요소를 관리할 때 효과적입니다. 그러나 Azure에서 빌드된 응용 프로그램은 상호 연결된 서비스 컬렉션이며 이 트리 구조는 서비스 컬렉션 작업에 적합하지 않습니다. 

Azure 포털 hello 쉽게 toobuild 응용 프로그램에 종단 간 여러 서비스에서 구성 요소와 있습니다. 으로 구성 된 hello 포털 *여정이*합니다. A *여행* 는 일련의 *블레이드*이며 hello에 대 한 컨테이너에는 다른 구성 요소입니다. 예를 들어 자동 크기 조정 웹 앱에 대 한 설정는 *여행* 를 따르세요 여러 블레이드 hello 다음 예제와 같이: hello **웹 사이트** (있는지 블레이드 제목 아직 업데이트 toouse 블레이드 새 용어 hello) hello **설정** 블레이드에서 하 고 hello **확장할** 블레이드입니다. Hello 예제에서는 자동 크기 조정 설정 되 CPU 사용량에 toodepend 이기도 하므로 **CPU 비율** 블레이드입니다. hello 내에서 구성 요소를 hello *블레이드* 라고 *부분*, 타일 모양입니다. 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a>탐색 예제: 웹앱 만들기
새 웹앱을 만드는 작업은 여전히 1-2-3만큼 쉽습니다. 다음 이미지에서는 hello 클래식 포털 및 hello 포털-나란히 toodemonstrate hello 다양 한 단계에서에서 변경 된이 많지 않습니다 hello를 웹 앱 및 실행 tooget 필요 합니다. 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

Hello 포털에서 hello 가장 일반적인 유형의 WordPress와 같은 인기 있는 갤러리 응용 프로그램을 포함 하 여 웹 응용 프로그램에서 선택할 수 있습니다. 사용 가능한 응용 프로그램의 전체 목록을 방문 hello [Azure 마켓플레이스]합니다.

URL을 지정 하는 웹 응용 프로그램을 만들 때 앱 서비스 계획 및 hello 클래식 포털에서와 마찬가지로 hello 포털에 위치 합니다. 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

또한 hello 포털 다른 일반적인 설정을 정의할 수 있습니다. 예를 들어 [리소스 그룹](../azure-resource-manager/resource-group-overview.md) 간단한 toosee 지정 하 고 관련된 Azure 리소스 관리. 

## <a name="navigation-example-settings-and-features"></a>탐색 예제: 설정 및 기능
모든 hello 설정 및 기능 이동할 수 있는 단일 블레이드에서 이제 논리적으로 그룹화 됩니다.

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

클릭 하 여 사용자 지정 도메인을 만들 수는 예를 들어 **사용자 지정 도메인 및 SSL** hello에 **설정을** 블레이드입니다.

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

모니터링 경고를 tooset 클릭 **요청 및 오류** 차례로 **추가 경고**합니다.

![](./media/app-service-web-app-azure-portal/Monitoring.png)

tooenable 진단 클릭 **진단 로그** hello에 **설정을** 블레이드입니다.

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

tooconfigure 응용 프로그램 설정 클릭 **응용 프로그램 설정** hello에 **설정을** 블레이드입니다. 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

Hello 브랜드 이름으로 이외의 hello 포털에서 몇 가지 바뀌었거나 다르게 그룹화 toomake 것 보다 쉽게 toofind 해당 합니다. 예를 들어 응용 프로그램 설정에 대 한 hello 해당 페이지의 스크린샷 같습니다 (**구성**) hello 클래식 포털의.

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a>추가 리소스
[Azure Portal]: https://portal.azure.com
[Azure 마켓플레이스]: /marketplace/

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 

## <a name="whats-changed"></a>변경된 내용
* 웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)


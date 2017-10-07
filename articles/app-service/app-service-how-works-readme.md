---
title: "Azure 앱 서비스의 작동 aaaHow"
description: "앱 서비스 작동 방법 알아보기"
keywords: "앱 서비스, Azure 앱 서비스, 규모, 확장성, 앱 서비스 계획, 앱 서비스 비용"
services: app-service
documentationcenter: 
author: yochay
manager: erikre
editor: 
ms.assetid: ae74fc32-969e-4580-8d61-02c922f1f184
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/23/2017
ms.author: yochayk
ms.openlocfilehash: b20733ec8844773d063e2b6918605c4a48db1f5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-app-service-works"></a>App Service 작동 방법
Azure 앱 서비스는 엔지니어 오늘날 직면 하는 디자인 된 toosolve hello 실제 문제를 클라우드 서비스입니다.
앱 서비스 중점적으로 hello 훼손 하지 않고 상위 개발자의 생산성을 제공 하는 클라우드 범위에서 toodeliver 응용 프로그램이 필요 합니다. 

앱 서비스는 hello 기능 및 엔터프라이즈 기간 업무 응용 프로그램을 만드는 데 필요한 프레임 워크 또한 제공 합니다. 앱 서비스를 사용 하면 가장 인기 있는 개발 언어에서는 Java, PHP, Node.js, Python 및 hello Microsoft.NET 언어를 포함 하 여 앱을 개발할 수 있습니다. App Service를 통해 다음 작업을 수행할 수 있습니다.

* 확장성이 뛰어난 웹앱을 빌드합니다.
* Mobile Apps 백 엔드를 데이터 백 엔드, 사용자 인증 및 푸시 알림과 같은 사용하기 쉬운 모바일 기능 집합으로 신속하게 빌드합니다.
* API Apps을 사용하여 API를 게시, 구현 및 배포합니다.
* 비즈니스 응용 프로그램을 워크플로에 서로 연결하고 논리 앱을 사용하여 데이터를 변환합니다.

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

Hello 확장 가능 하며 유연한 웹 응용 프로그램 플랫폼에 최적화 된 전체 수명 주기는 응용 프로그램 디자인 tooapp 유지 관리에서의 경험이 개발자 toohave 수 있는 모든 응용 프로그램 형식을 사용 합니다. hello 수명 주기 기능 hello 다음 사용:

* **빠른 앱 만들기**. 처음부터 시작 하 하거나 hello Azure Marketplace에서에서 프로그램 operational 지원 시스템 (OS) 패키지를 선택 합니다.
* **연속 배포**. OneDrive 및 DropBox와 같은 온라인 저장소 서비스의 동기화 콘텐츠 및 TFS, GitHub, BitBucket처럼 인기 있는 원본 제어 솔루션에서 자동으로 새 코드를 배포합니다.
* **프로덕션에서 테스트**. 프리 프로덕션 환경은 만들고 hello toothem 일어나는 트래픽 양을 관리 원활 하 게 합니다. 필요한 경우 hello 클라우드에서 디버그 하 고 문제가 발견 되 면에 다시 롤포워드할 키를 누릅니다.
* **비동기 작업 및 배치 작업 실행**. 백그라운드 프로세스에서 코드를 실행하거나 이벤트(예: Azure Storage 큐에 메시지 도착) 및 예약된 시간(CRON)에 따라 코드를 활성화합니다.
* **크기 조정 hello 앱**합니다. 트래픽 및 리소스 사용률에 기반 하는 가로 및 세로로 여러 서비스를 확장할 많은 옵션 tooautomatically 중 하나를 사용 합니다. 전용된 tooyour 앱이 개인 환경을 구성 합니다.   
* **유지 관리 hello 앱**합니다. 많은 hello 디버깅을 사용 하 고 문제 및 tooefficiently 미리 진단 기능 toostay 실시간 (으로 자동 복구 및 라이브 디버깅 하는 등의 기능)에서 해결 하거나 로그 및 메모리를 분석 하 여 hello 팩트 후 덤프 합니다.

전체적으로 신속 하 게 안정적이 고 확장성이 높은 프로덕션 상태가 될 때까지 및 응용 프로그램 서비스 기능 코드에 대 한 개발자 toofocus를 사용 합니다. API 앱 hello 및 논리 앱 기능을 사용 개발자는 비즈니스 솔루션 및 온-프레미스 toocloud 통합 간의 장벽을 브리지 하는 실제 엔터프라이즈 응용 프로그램을 구축할 수 있습니다. 

## <a name="videos"></a>비디오
* [Azure 앱 서비스 아키텍처](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)

## <a name="next-steps"></a>다음 단계

Hello 다음 항목 중 하나에서 응용 프로그램 서비스에 대 한 자세한 정보:

* [Azure 앱 서비스 정의](app-service-value-prop-what-is.md)
  * [웹앱](../app-service-web/app-service-web-overview.md)
  * [모바일 앱](../app-service-mobile/app-service-mobile-value-prop.md)
  * [API 앱](../app-service-api/app-service-api-apps-why-best-platform.md)
* [Azure 앱 서비스 아키텍처(프레젠테이션)](http://www.slideshare.net/maartenba/windows-azure-web-sites-things-they-dont-teach-kids-in-school-comunity-day-2013)
* [Azure 앱 서비스, 클라우드 서비스 및 가상 컴퓨터 비교](../app-service-web/choose-web-site-cloud-service-vm.md)
* [앱 서비스 계획 이해](azure-web-sites-web-hosting-plans-in-depth-overview.md)
* [소개 tooApp 서비스 환경](../app-service-web/app-service-app-service-environment-intro.md)
  * [연습: 앱 서비스 환경 만들기](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [Azure 앱 서비스 개발 스택 지원](https://azure.microsoft.com/blog/windows-azure-websites-development-stacks-support/)




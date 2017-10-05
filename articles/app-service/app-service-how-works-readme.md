---
title: "Azure App Service 작동 방법"
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
ms.openlocfilehash: 2d830963d3d2adba71a6ca99f79eac0fc8cbfb12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-app-service-works"></a>App Service 작동 방법
Azure App Service는 오늘날 엔지니어가 직면한 실제 문제를 해결하기 위해 설계된 클라우드 서비스입니다.
App Service는 응용 프로그램을 클라우드 규모로 전달해야 하는 요구를 존중하면서 우수한 개발자 생산성을 제공하는 데 중점을 둡니다. 

App Service에는 엔터프라이즈 기간 업무 응용 프로그램을 만드는 데 필요한 프레임워크 및 기능도 제공됩니다. App Service를 사용하면 Java, PHP, Node.js, Python 및 Microsoft .NET 언어를 비롯한 가장 인기 있는 개발 언어로 앱을 개발할 수 있습니다. App Service를 통해 다음 작업을 수행할 수 있습니다.

* 확장성이 뛰어난 웹앱을 빌드합니다.
* Mobile Apps 백 엔드를 데이터 백 엔드, 사용자 인증 및 푸시 알림과 같은 사용하기 쉬운 모바일 기능 집합으로 신속하게 빌드합니다.
* API Apps을 사용하여 API를 게시, 구현 및 배포합니다.
* 비즈니스 응용 프로그램을 워크플로에 서로 연결하고 논리 앱을 사용하여 데이터를 변환합니다.

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

모든 앱 형식은 개발자가 앱 설계에서 앱 유지 관리까지의 전체 수명 주기 환경을 최적화하는 확장성과 유연성이 있는 Web Apps 플랫폼을 사용합니다. 수명 주기 기능은 다음을 사용하도록 설정합니다.

* **빠른 앱 만들기**. 처음부터 시작하거나 Azure Marketplace에서 OSS(운영 지원 시스템) 패키지를 선택합니다.
* **연속 배포**. OneDrive 및 DropBox와 같은 온라인 저장소 서비스의 동기화 콘텐츠 및 TFS, GitHub, BitBucket처럼 인기 있는 원본 제어 솔루션에서 자동으로 새 코드를 배포합니다.
* **프로덕션에서 테스트**. 원활하게 사전 프로덕션 환경을 만들고 이 환경으로 이동하는 트래픽의 양을 관리합니다. 필요할 때 클라우드에서 디버깅하고 문제가 발견되면 롤백합니다.
* **비동기 작업 및 배치 작업 실행**. 백그라운드 프로세스에서 코드를 실행하거나 이벤트(예: Azure Storage 큐에 메시지 도착) 및 예약된 시간(CRON)에 따라 코드를 활성화합니다.
* **앱 크기 조정**. 트래픽 및 리소스 사용률에 따라 가로 및 세로 방향으로 자동으로 서비스를 확장하기 위해 여러 옵션 중 하나를 사용합니다. 앱 전용인 개인 환경을 구성합니다.   
* **앱 유지 관리**. 다양한 디버깅 및 진단 기능을 활용하여 효율적으로 문제를 미리 알아차리고 실시간 해결하거나(자동 복구 및 라이브 디버깅 기능 사용) 로그 및 메모리 덤프를 분석하여 사실을 확인한 후 문제를 해결합니다.

전체적으로 App Service 기능을 통해 개발자는 코드 작성에 집중할 수 있으므로 안정적이고 확장성이 뛰어난 프로덕션 상태를 신속하게 만들 수 있습니다. API Apps 및 Logic Apps 기능을 사용하면 개발자는 온-프레미스에서 클라우드 통합 및 비즈니스 솔루션 간에 존재하는 장벽을 연결하는 실제 엔터프라이즈 응용 프로그램을 빌드할 수 있습니다. 

## <a name="videos"></a>비디오
* [Azure 앱 서비스 아키텍처](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)

## <a name="next-steps"></a>다음 단계

App Service에 대한 자세한 내용은 다음 항목을 참조하세요.

* [Azure 앱 서비스 정의](app-service-value-prop-what-is.md)
  * [웹앱](../app-service-web/app-service-web-overview.md)
  * [모바일 앱](../app-service-mobile/app-service-mobile-value-prop.md)
  * [API 앱](../app-service-api/app-service-api-apps-why-best-platform.md)
* [Azure 앱 서비스 아키텍처(프레젠테이션)](http://www.slideshare.net/maartenba/windows-azure-web-sites-things-they-dont-teach-kids-in-school-comunity-day-2013)
* [Azure 앱 서비스, 클라우드 서비스 및 가상 컴퓨터 비교](../app-service-web/choose-web-site-cloud-service-vm.md)
* [앱 서비스 계획 이해](azure-web-sites-web-hosting-plans-in-depth-overview.md)
* [앱 서비스 환경 소개](../app-service-web/app-service-app-service-environment-intro.md)
  * [연습: 앱 서비스 환경 만들기](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [Azure 앱 서비스 개발 스택 지원](https://azure.microsoft.com/blog/windows-azure-websites-development-stacks-support/)




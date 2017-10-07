---
title: "웹, 모바일 및 API 앱에 대 한 앱 서비스 aaaAzure | Microsoft Docs"
description: "Azure 앱 서비스를 사용하여 웹 및 모바일 앱을 개발, 배포 및 관리하는 방법을 알아봅니다."
keywords: "앱 서비스, Azure 앱 서비스, 앱 서비스 비용, 규모, 확장성, 앱 배포, Azure 앱 배포, PaaS, Platform-as-a-Service, 웹사이트, 웹 사이트, 웹, Azure 모바일"
services: app-service
documentationcenter: 
author: omarkmsft
manager: erikre
editor: cephalin
ms.assetid: 979cafa8-eeb6-4d3b-87cf-764a821c3e4f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: 22f414c7d79092d87406a8d3538b946881fb4580
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-app-service"></a>Azure 앱 서비스 정의
*앱 서비스* 는 Microsoft Azure의 PaaS( [platform-as-a-service](https://en.wikipedia.org/wiki/Platform_as_a_service) ) 제품입니다. 플랫폼 및 장치에 웹 및 모바일 앱을 만듭니다. SaaS 솔루션과 앱을 통합하고 온-프레미스 응용 프로그램을 사용하여 연결하고 비즈니스 프로세스를 자동화합니다. Azure는 공유 VM 리소스 또는 전용 VM을 선택하여 완전히 관리되는 VM(가상 컴퓨터)에서 앱을 실행합니다.

앱 서비스는 hello 웹 및 모바일 기능으로 구성에서는 이전에 된 별도로 Azure 웹 사이트 및 Azure 모바일 서비스를 포함 합니다. 또한 비즈니스 프로세스를 자동화하고 클라우드 API를 호스팅하는 새 기능을 포함합니다. 단일 통합 서비스인 앱 서비스를 통해 웹 사이트, 모바일 앱 백 엔드, RESTful API 및 비즈니스 프로세스 등 다양한 구성 요소를 단일 솔루션으로 작성할 수 있습니다.

hello 다음 4 분 분량의 비디오는 간략 한 설명이 제공 응용 프로그램 서비스 tooearlier Azure가 어떻게 관련 서비스와의 새로운 기능입니다.

> [!VIDEO https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/app-service-history-lesson/player]
> 
> 

## <a name="why-use-app-service"></a>앱 서비스를 사용하는 이유는 무엇인가요?
다음은 앱 서비스의 몇 가지 주요 기능입니다.

* **여러 언어 및 프레임워크** - 앱 서비스에서는 ASP.NET, Node.js, Java, PHP 및 Python을 최고 수준으로 지원합니다. 앱 서비스 VM에서 [Windows PowerShell 및 기타 스크립트 또는 실행 파일](../app-service-web/web-sites-create-web-jobs.md) 을 실행할 수도 있습니다.
* **DevOps 최적화** - Visual Studio Team Services, GitHub, BitBucket으로 [연속 통합 및 배포](../app-service-web/app-service-continuous-deployment.md) 를 설정합니다. [테스트 및 스테이징 환경](../app-service-web/web-sites-staged-publishing.md)을 통해 업데이트를 승격합니다. [A/B 테스트](../app-service-web/app-service-web-test-in-production-get-start.md)를 수행합니다. 앱 서비스에서 앱을 사용 하 여 관리 [Azure PowerShell](/powershell/azureps-cmdlets-docs) 또는 hello [플랫폼 간 명령줄 인터페이스 (CLI)](../cli-install-nodejs.md)합니다.
* **고가용성을 가진 글로벌 규모 조정** - 수동 또는 자동으로 규모를 [강화](../app-service-web/web-sites-scale.md) 또는 [확장](../monitoring-and-diagnostics/insights-how-to-scale.md)합니다. Microsoft의 글로벌 데이터 센터 인프라의 아무 곳 이나 앱을 호스트 하 고 응용 프로그램 서비스 hello [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) 고가용성을 약속 합니다.
* **연결 tooSaaS 플랫폼 및 온-프레미스 데이터** -50 개 이상의 중에서 선택할 [커넥터](../connectors/apis-list.md) SaaS 서비스 (예: SAP, Siebel, Oracle) 엔터프라이즈 시스템의 경우 (예: Salesforce 및 Office 365) 및 인터넷 서비스 (예: Facebook 및 Twitter)입니다. [하이브리드 연결](../biztalk-services/integration-hybrid-connection-overview.md) 및 [Azure Virtual Networks](../app-service-web/web-sites-integrate-with-vnet.md)를 사용하여 온-프레미스 데이터에 액세스합니다.
* **보안 및 규정 준수** - 앱 서비스는 [ISO, SOC 및 PCI 규격](https://www.microsoft.com/TrustCenter/)입니다.
* **응용 프로그램 템플릿** -hello에 대 한 서식 파일의 확장 목록에서 선택 [Azure 마켓플레이스](https://azure.microsoft.com/marketplace/) WordPress, Drupal, Joomla와 같은 마법사 tooinstall 인기 있는 오픈 소스 소프트웨어를 사용할 수 있도록 합니다.
* **Visual Studio 통합** -Visual Studio에서 전용된 도구 hello 작업 만들기, 배포 및 디버깅을 간소화 합니다.

## <a name="app-types-in-app-service"></a>앱 서비스의 앱 유형
응용 프로그램 서비스는 여러 *응용 프로그램 형식을*, 각 되어 있는 의도 한 toohost 특정 워크 로드:

* [**Web Apps**](../app-service-web/app-service-web-overview.md) - 웹 사이트와 웹 응용 프로그램을 호스팅합니다.
* [**Mobile Apps**](../app-service-mobile/app-service-mobile-value-prop.md) 모바일 앱 백 엔드를 호스팅합니다.
* [**API Apps**](../app-service-api/app-service-api-apps-why-best-platform.md) - 클라우드 API를 호스팅합니다.
* [**Logic Apps**](../logic-apps/logic-apps-what-are-logic-apps.md) - 비즈니스 프로세스를 자동화하고 코드를 작성하지 않고도 클라우드를 통해 시스템과 데이터를 통합합니다.

단어 hello *앱* 여기 toohello 호스팅 리소스 전용된 toorunning 작업을 참조 합니다. 아마 여러분 예를 들어 "웹 응용 프로그램" 취한 hello 계산 리소스와 응용 프로그램 코드 해당 제공 기능 tooa 브라우저 대로 웹 응용 프로그램의 toothinking 익숙한 합니다. 하지만 응용 프로그램 서비스는 *웹 앱* 는 hello 호스팅 응용 프로그램 코드에 대 한 Azure에서 제공 하는 계산 리소스입니다. 

응용 프로그램은 다른 종류의 여러 앱 서비스 앱으로 구성될 수 있습니다. 예를 들어 응용 프로그램이 웹 프런트 엔드와 RESTful API 백 엔드로 구성되는 경우 다음을 수행할 수 있습니다.

- 모두 (프런트 엔드 및 api)를 배포할 tooa 단일 웹 응용 프로그램  
- 프런트 엔드 코드 tooa 웹 앱과 백 엔드 코드 tooan API 앱을 배포 합니다. 



## <a name="app-service-plans"></a>앱 서비스 계획
[앱 서비스 계획](azure-web-sites-web-hosting-plans-in-depth-overview.md) 앱 사용 하는 실제 리소스 toohost의 hello 컬렉션을 나타냅니다.

App Service 계획은 다음을 정의합니다.

- **지역**(미국 서부, 미국 동부 등)
- **확장 개수**(1, 2, 3개 인스턴스 등)
- **인스턴스 크기**(소, 중, 대)
- **SKU**(무료, 공유, 기본, 표준, 프리미엄)

모든 응용 프로그램 할당 tooan **앱 서비스 계획** toosave 비용 허용 여러 앱을 호스트 하는 경우에서 정의한 hello 리소스를 공유 합니다.

프로그램 **앱 서비스 계획** 에서 확장할 수 **무료** 및 **Shared** Sku 너무**기본**, **표준**, 및 **프리미엄** toomore 리소스 및 hello 따라 기능을 제공 하는 Sku 액세스 방법입니다. 앱 서비스 계획 너무 설정 되 고 나면**기본** 높을수록 제어할 수도 있습니다 hello 또는 **크기** hello Vm의 수를 크기 조정 하 고 있습니다.

hello **SKU** 및 **배율** 의 hello 앱 서비스 계획에 호스팅된 앱 hello 비용과 hello 하지 수를 결정 합니다. 

확장성 및 네트워크 격리가 필요한 경우 [앱 서비스 환경](../app-service-web/app-service-app-service-environment-intro.md)에서 앱을 실행할 수 있습니다.

## <a name="pricing"></a>가격
앱 서비스 비용에 대한 정보는 [앱 서비스 가격 책정](https://azure.microsoft.com/pricing/details/app-service/)을 참조하세요.

## <a name="test-drive-app-service"></a>App Service 시험 사용
[샘플 웹앱, 모바일 앱 또는 논리 앱을 만들고](https://azure.microsoft.com/try/app-service/) 1시간 동안 재생합니다. 신용 카드나 약정, 번거로운 과정도 필요하지 않습니다.

또는 [무료 Azure 계정](https://azure.microsoft.com/pricing/free-trial/)을 열고 시작 자습서 중 하나를 사용해 봅니다.

* [자습서: 웹앱 만들기](../app-service-web/app-service-web-get-started.md)
* [자습서: 모바일 앱 만들기](../app-service-mobile/app-service-mobile-android-get-started.md)
* [자습서: API 앱 만들기](../app-service-api/app-service-api-dotnet-get-started.md)
* [자습서: 논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)


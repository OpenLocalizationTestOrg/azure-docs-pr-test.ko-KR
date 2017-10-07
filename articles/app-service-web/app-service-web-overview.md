---
title: "aaaWeb 앱 개요 | Microsoft Docs"
description: "Azure 앱 서비스로 웹 응용 프로그램을 개발 및 호스팅하는 방법에 대해 알아보세요."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 94af2caf-a2ec-4415-a097-f60694b860b3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 01/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: ce27519bddd62a7fca6ba1fb23c763d0fc378c2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="web-apps-overview"></a>웹앱 개요
*앱 서비스 웹앱* 은 웹 사이트와 웹 응용 프로그램 호스팅을 위해 최적화된 완전히 관리되는 계산 플랫폼입니다. 이 [플랫폼-as a service](https://en.wikipedia.org/wiki/Platform_as_a_service) Microsoft azure 서비스 (PaaS)를 사용 하면 Azure hello 인프라 toorun는 담당 하는 동안 비즈니스 논리에 집중 하 고 앱의 크기를 조정 합니다.

5 분 분량의 비디오를 따라 hello Azure 앱 서비스 웹 앱을 소개 합니다.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Web-Apps-with-Yochay-Kiriaty/player]
>
>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

## <a name="what-is-a-web-app-in-app-service"></a>앱 서비스에서 웹앱은 무엇인가요?
앱 서비스에서 한 *웹 앱* 는 hello 호스팅 웹 사이트 또는 웹 응용 프로그램에 대 한 Azure에서 제공 하는 계산 리소스입니다.  

hello 계산 리소스 공유 또는 전용 (Vm)에 따라 가상 컴퓨터 가격 책정 계층 선택 하는 hello에 있을 수 있습니다. 응용 프로그램 코드는 다른 고객과 격리되는 관리되는 VM에서 실행됩니다.

사용자 코드는 [Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md)(ASP.NET, Node.js, Java, PHP, Python)에서 지원되는 모든 언어 또는 프레임워크일 수 있습니다. 웹앱에서 [PowerShell 및 기타 스크립트 언어](web-sites-create-web-jobs.md#acceptablefiles) 를 사용하는 스크립트를 실행할 수도 있습니다.

참조에 대해 웹 응용 프로그램을 사용할 수 있는 일반적인 응용 프로그램 시나리오의 예제에 대 한 [웹 응용 프로그램 시나리오](https://azure.microsoft.com/documentation/scenarios/web-app/) 및 hello **시나리오 및 권장 사항** 섹션 [Azure 앱 서비스, 가상 컴퓨터, 서비스 패브릭 및 클라우드 서비스 비교](choose-web-site-cloud-service-vm.md#scenarios)합니다.

## <a name="why-use-web-apps"></a>웹앱을 사용하는 이유
TooWeb 앱 적용 되거나 적용 하는 앱 서비스의 주요 기능은 다음과 같습니다.

* **여러 언어 및 프레임워크** - 앱 서비스에서는 ASP.NET, Node.js, Java, PHP 및 Python을 최고 수준으로 지원합니다. 앱 서비스 VM에서 [PowerShell 및 기타 스크립트 또는 실행 파일](web-sites-create-web-jobs.md) 을 실행할 수도 있습니다.
* **DevOps 최적화** - Visual Studio Team Services, GitHub, BitBucket으로 [연속 통합 및 배포](app-service-continuous-deployment.md) 를 설정합니다. [테스트 및 스테이징 환경](web-sites-staged-publishing.md)을 통해 업데이트를 승격합니다. [A/B 테스트](app-service-web-test-in-production-get-start.md)를 수행합니다. 앱 서비스에서 앱을 사용 하 여 관리 [Azure PowerShell](/powershell/azureps-cmdlets-docs) 또는 hello [플랫폼 간 명령줄 인터페이스 (CLI)](../cli-install-nodejs.md)합니다.
* **고가용성을 가진 글로벌 규모 조정** - 수동 또는 자동으로 규모를 [강화](web-sites-scale.md) 또는 [확장](../monitoring-and-diagnostics/insights-how-to-scale.md)합니다. Microsoft의 글로벌 데이터 센터 인프라의 아무 곳 이나 앱을 호스트 하 고 응용 프로그램 서비스 hello [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) 고가용성을 약속 합니다.
* **연결 tooSaaS 플랫폼 및 온-프레미스 데이터** -50 개 이상의 중에서 선택할 [커넥터](../connectors/apis-list.md) SaaS 서비스 (예: SAP, Siebel, Oracle) 엔터프라이즈 시스템의 경우 (예: Salesforce 및 Office 365) 및 인터넷 서비스 (예: Facebook 및 Twitter)입니다. [하이브리드 연결](../biztalk-services/integration-hybrid-connection-overview.md) 및 [Azure Virtual Networks](web-sites-integrate-with-vnet.md)를 사용하여 온-프레미스 데이터에 액세스합니다.
* **보안 및 규정 준수** - 앱 서비스는 [ISO, SOC 및 PCI 규격](https://www.microsoft.com/TrustCenter/)입니다.
* **응용 프로그램 템플릿** -hello에 대 한 응용 프로그램 템플릿 확장 목록에서 선택 [Azure 마켓플레이스](https://azure.microsoft.com/marketplace/) WordPress, Drupal, Joomla와 같은 마법사 tooinstall 인기 있는 오픈 소스 소프트웨어를 사용할 수 있도록 합니다.
* **Visual Studio 통합** -Visual Studio에서 전용된 도구 hello 작업 만들기, 배포 및 디버깅을 간소화 합니다.

또한 웹앱은 [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md)(예: CORS 지원) 및 [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md)(예: 푸시 알림)에서 제공하는 기능을 활용할 수 있습니다. 앱 서비스에서 앱 유형에 대한 자세한 내용은 [Azure 앱 서비스 개요](../app-service/app-service-value-prop-what-is.md)를 참조하세요.

Azure는 앱 서비스의 웹앱 뿐만 아니라 웹 사이트와 웹 응용 프로그램 호스팅에 사용할 수 있는 다른 서비스를 제공합니다. 대부분의 시나리오에 대 한 웹 앱이 hello 가장 좋습니다.  마이크로 서비스 아키텍처에 대 한 고려 [서비스 패브릭](https://azure.microsoft.com/documentation/services/service-fabric), 더 많이 제어할 hello Vm에서 실행 되는 코드는 필요한 경우 고 [Azure 가상 컴퓨터](https://azure.microsoft.com/documentation/services/virtual-machines/)합니다. 방법에 대 한 자세한 내용은 이러한 Azure 서비스 간의 toochoose 참조 [Azure 앱 서비스, 가상 컴퓨터, 서비스 패브릭 및 클라우드 서비스 비교](choose-web-site-cloud-service-vm.md)합니다.

## <a name="getting-started"></a>시작
앱 서비스의 샘플 코드 tooa 새 웹 앱을 배포 하 여 시작 tooget hello 드롭다운 상자 뒤의 hello 자습서 중 하나를 수행 합니다. 무료 Azure 계정이 필요합니다.

> [!div class="op_single_selector"]
> * [첫 번째 여 ASP.NET 웹 응용 프로그램 tooAzure 5 분 이내에 배포](app-service-web-get-started-dotnet.md)
> * [첫 번째 여 PHP 웹 응용 프로그램 tooAzure 5 분 이내에 배포](app-service-web-get-started-php.md)
> * [첫 번째 프로그램 Node.js 웹 응용 프로그램 tooAzure 5 분 이내에 배포](app-service-web-get-started-nodejs.md)
> * [5 분 이내에 첫 번째 Java 웹 응용 프로그램 tooAzure 프로그램 배포](app-service-web-get-started-java.md)
> * [첫 번째 여 Python 웹 응용 프로그램 tooAzure 5 분 이내에 배포](app-service-web-get-started-python.md)
> * [5 분 이내에 첫 번째 HTML 사이트 tooAzure 프로그램 배포](app-service-web-get-started-html.md)
> 
> 

> [!NOTE]
> Azure 계정 없이 [App Service를 체험](https://azure.microsoft.com/try/app-service/)할 수 있습니다. 시작 응용 프로그램 만들기 및 신용 카드가 필요 없는, 없음의 노력과 헌신 함께 tooan 시간-를 재생 합니다.
> 
> 

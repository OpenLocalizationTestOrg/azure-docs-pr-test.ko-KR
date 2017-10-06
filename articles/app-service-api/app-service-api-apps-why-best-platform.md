---
title: "aaaAPI 앱 소개 | Microsoft Docs"
description: "Azure 앱 서비스로 RESTful API를 개발, 호스팅, 소비하는 방법에 대해 알아보세요."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 60049a16-8159-47aa-a34b-110be0d8dab6
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: alkarche
ms.openlocfilehash: f066e96db667d4685480001bc43c2b1bff4ea352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="api-apps-overview"></a>API 앱 개요
Azure 앱 서비스 제품 기능에 쉽게 toodevelop 있도록에서 API 앱 호스팅하고 hello 클라우드 및 온-프레미스 Api를 사용 합니다. API 앱을 사용하면 엔터프라이즈급 보안, 단순 액세스 제어, 하이브리드 연결, 자동 SDK 생성, 그리고 [Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md)와의 원활한 통합이 가능합니다.

[Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md) 는 웹, 모바일 및 통합 시나리오에 대해 완전히 관리되는 플랫폼입니다. API 앱은 [Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md)에서 제공하는 4개의 앱 형식 중 하나입니다.

![Azure 앱 서비스의 앱 유형](./media/app-service-api-apps-why-best-platform/appservicesuite.png)

## <a name="why-use-api-apps"></a>API 앱을 사용하는 이유
API 앱의 몇 가지 주요 기능은 다음과 같습니다.

* **기존 API로 전환-은** -toochange hello의 모든 코드에 없는 API 앱의 기존 Api tootake 있다는 이점이-방금 코드 tooan API 앱을 배포 합니다. API는 ASP.NET 및 C#, Java, PHP, Node.js, Python을 비롯하여 앱 서비스에서 지원하는 모든 언어 또는 프레임워크를 사용할 수 있습니다.
* **쉽게 사용** - 통합된 [Swagger API 메타데이터](http://swagger.io/) 지원을 통해 다양한 클라이언트가 쉽게 API를 사용할 수 있도록 합니다.  C#, Java 및 Javascript를 비롯한 다양한 언어로 API용 클라이언트 코드를 자동으로 생성할 수 있습니다. 코드 변경 없이 [CORS](app-service-api-cors-consume-javascript.md) 를 쉽게 구성합니다. 자세한 내용은 [API 검색 및 코드 생성에 대한 App Service API Apps 메타데이터](app-service-api-metadata.md) 및 [CORS를 사용하여 JavaScript에서 API 앱 사용](app-service-api-cors-consume-javascript.md)을 참조하세요. 
* **단순 액세스 제어** -인증 되지 않은 액세스 변경 내용 tooyour 코드 없이에서 API 앱을 보호 합니다. 기본 제공 인증 서비스는 다른 서비스 또는 사용자를 나타내는 클라이언트에서 액세스에 대해 API를 보호합니다. 지원되는 ID 공급자에는 Azure Active Directory, Facebook, Twitter, Google, Microsoft 계정 등이 있습니다. 클라이언트는 hello 모바일 앱 SDK 또는 Active Directory 인증 라이브러리 (ADAL)에 사용할 수 있습니다. 자세한 내용은 [Azure 앱 서비스의 API 앱에 대한 인증 및 권한 부여](app-service-api-authentication.md)를 참조하세요.
* **Visual Studio 통합** -Visual Studio에서 전용된 도구 hello 작업을 만들고, 배포, 사용, 디버깅, 및 API 앱 관리를 간소화 합니다. 자세한 내용은 참조 [알림 hello 2.8.1 Azure SDK for.NET](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/)합니다.
* **논리 앱과 통합** - 사용자가 만드는 API 앱은 [앱 서비스 논리 앱](../logic-apps/logic-apps-what-are-logic-apps.md)을 통해 사용할 수 있습니다.  자세한 내용은 [논리 앱으로 App Service에서 호스팅되는 사용자 지정 API 사용](../logic-apps/logic-apps-custom-hosted-api.md) 및 [새 스키마 버전 2015-08-01-preview](../logic-apps/logic-apps-schema-2015-08-01.md)를 참조하세요.

또한 API 앱에서는 [Web Apps](../app-service-web/app-service-web-overview.md) 및 [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md)에서 제공하는 기능을 활용할 수 있습니다. 역방향 hello도 마찬가지입니다: 웹 응용 프로그램 또는 모바일 앱 toohost API 사용 하는 경우이 지나야 클라이언트에 대 한 Swagger 메타 데이터와 같은 API 앱 기능을 활용 코드 생성 및 CORS 도메인 간 브라우저 액세스에 대 한 합니다. hello만 차이점 hello 세 개의 응용 프로그램 유형 (API, 웹, 모바일)은 hello 이름 및 hello Azure 포털에서에서 하는 데 사용 되는 아이콘입니다.

## <a name="whats-hello-difference-between-api-apps-and-azure-api-management"></a>API 앱 및 Azure API 관리의 hello 차이점은 무엇입니까?
API 앱 및 [Azure API 관리](../api-management/api-management-key-concepts.md) 는 다음과 같이 보완적인 서비스입니다.

* API 관리는 API를 관리하는 것입니다. API 관리 프런트 엔드 API toomonitor에 및 트래픽 사용량을 제한할 입력 및 출력 조작, 하나의 끝점에 여러 Api 통합할 넣은 등입니다. 아무 곳 이나 hello 관리 되는 Api를 호스팅할 수 있습니다.
* API 앱은 API를 호스팅하는 것입니다. hello 서비스 개발 및 사용 중인 Api를 쉽게 수행할 수 있는 기능을 포함 하지만 일은 hello 모니터링 제한 조작 하거나 API 관리 하다 통합의 종류입니다. API 관리 기능이 필요하지 않은 경우 API 관리를 사용하지 않고 Api 앱에 API를 호스팅할 수 있습니다.

다음은 API 앱 및 기타 위치에 호스팅되는 API에 사용하는 API 관리를 보여주는 다이어그램입니다.

![Azure API 관리 및 API 앱](./media/app-service-api-apps-why-best-platform/apia-apim.png)

API 관리 및 API 앱의 일부 기능에는 유사한 함수가 있습니다.  예를 들어, 두 가지 모두 CORS 지원을 자동화할 수 있습니다. Hello 두 서비스를 함께 사용 하는 경우 프런트 엔드 tooyour API 앱 hello 대로 작동 하므로 CORS에 대 한 API 관리를 사용 합니다. 

## <a name="getting-started"></a>시작
샘플 코드 tooone를 배포 하 여 API 앱 시작 tooget 원하는 나오든 이들 프레임 워크에 대 한 hello 자습서를 참조 하십시오.

* [ASP.NET](app-service-api-dotnet-get-started.md) 
* [Node.JS](app-service-api-nodejs-api-app.md) 
* [Java](app-service-api-java-api-app.md) 

hello에 스레드를 시작 하는 API 앱에 대 한 tooask 질문 [API 앱 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps)합니다. 


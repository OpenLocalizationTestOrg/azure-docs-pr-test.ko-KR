---
title: "흐름, 논리 앱, 함수 및 WebJobs 사이의 aaaChoose | Microsoft Docs"
description: "비교 및 대비에는 Microsoft의 클라우드 통합 서비스에 대 한 hello를 사용 해야 하는 서비스를 결정 합니다."
services: functions,app-service\logic
documentationcenter: na
author: cephalin
manager: wpickett
tags: 
keywords: "Microsoft Flow, Flow, Logic Apps, Azure Functions, Functions, Azure Webjobs, Webjobs, 이벤트 처리, 동적 계산, 서버가 없는 아키텍처"
ms.assetid: e9ccf7ad-efc4-41af-b9d3-584957b1515d
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 6becc1e389698e517924b18295dac4375542d524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-between-flow-logic-apps-functions-and-webjobs"></a>Flow, Logic Apps, Functions 및 WebJobs 중에서 선택
이 문서는 비교 하 고 비즈니스 프로세스의 자동화 및 통합 문제 해결 모두 수 hello Microsoft 클라우드에서 서비스를 수행 하는 hello를 대조:

* [Microsoft Flow](https://flow.microsoft.com/)
* [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/)
* [Azure 기능](https://azure.microsoft.com/services/functions/)
* [Azure App Service WebJobs](../app-service-web/web-sites-create-web-jobs.md)

이러한 모든 서비스는 서로 다른 시스템을 함께 "부착"할 때 유용합니다. 입력, 동작, 조건 및 출력을 모두 정의할 수 있습니다. 각 서비스를 일정이나 트리거에 따라 실행할 수 있습니다. 그러나 각 서비스에 고유한 값을 추가 하 고와 비교 하는 것은 아닙니다 "되는 서비스는 최상의 hello?"의 "이 상황에 가장 적합한 서비스"를 알아낼 수 있습니다. 대개 이러한 서비스의 조합은 hello 가장 좋은 방법은 toorapidly 확장 가능 하 고 전체 기능 갖춘된 통합 솔루션을 빌드합니다.

<a name="flow"></a>

## <a name="flow-vs-logic-apps"></a>Flow 및 Logic Apps
논의할 수 Microsoft 흐름 및 Azure 논리 앱 함께 둘 다 되기 때문에 *구성 중심* integration services는 쉽게 toobuild 프로세스와 워크플로 사용 하면 고 다양 한 SaaS 및 엔터프라이즈 통합 응용 프로그램입니다. 

* Flow는 Logic Apps를 기반으로 빌드됩니다.
* Hello 있는 같은 워크플로 디자이너
* [커넥터](../connectors/apis-list.md) 작업 하나에 다른 hello에서 확대할 수

흐름은 모든 office 작업자 tooperform 간단한 통합 (예: 중요 한 메일에 대 한 SMS 얻기) 개발자를 통하지 않고 또는 IT 합니다. 다른 손 hello, 논리 앱 고급 또는 중요 한 통합 (예: B2B 프로세스) 엔터프라이즈 수준 DevOps 및 보안 사례는 필요한 사용 하도록 설정할 수 있습니다. 중인 비즈니스 워크플로 toogrow에 대 한 일반 복잡성 초과 합니다. 따라서 처음에 흐름에 따라 시작 다음 필요에 따라 tooa 논리 앱 변환 수 있습니다.

hello 다음 표를 사용 하면 흐름 또는 논리 앱 주어진된 통합에 대 한 최상의 되는지 확인 합니다.

|  | 흐름 | 논리 앱 |
| --- | --- | --- |
| 대상 |사무실 작업자, 비즈니스 사용자 |IT 전문가, 개발자 |
| 시나리오 |셀프서비스 |중요 업무용 |
| 디자인 도구 |브라우저 및 모바일 앱에서 UI만 해당 |브라우저 내부 및 [Visual Studio](../logic-apps/logic-apps-deploy-from-vs.md), [코드 보기](../logic-apps/logic-apps-author-definitions.md) 사용 가능 |
| DevOps |애드혹, 프로덕션에서 개발 |소스 제어, 테스트, 지원 및 [Azure 리소스 관리](../logic-apps/logic-apps-arm-provision.md) |
| 관리자 환경 |[https://flow.microsoft.com](https://flow.microsoft.com) |[https://portal.azure.com/](https://portal.azure.com) |
| 보안 |표준 사례: 중요한 데이터에 대한 [데이터 독립성](https://wikipedia.org/wiki/Technological_Sovereignty), [휴지 상태의 암호화](https://wikipedia.org/wiki/Data_at_rest#Encryption) 등 |Azure의 보안 보증: [Azure Security](https://www.microsoft.com/trustcenter/Security/AzureSecurity), [Security Center](https://azure.microsoft.com/services/security-center/), [감사 로그](https://azure.microsoft.com/blog/azure-audit-logs-ux-refresh/) 등 |

<a name="function"></a>

## <a name="functions-vs-webjobs"></a>Functions 및 웹 작업
Azure Functions와 Azure App Service WebJobs는 둘 다 *코드 중심* 통합 서비스이며 개발자용으로 설계되었으므로 함께 설명할 수 있습니다. 사용 하면 스크립트 또는 응답 toovarious 이벤트에 코드 조각을 toorun 같은 [새 저장소 Blob](functions-bindings-storage.md) 또는 [WebHook 요청](functions-bindings-http-webhook.md)합니다. 두 서비스의 유사점은 다음과 같습니다. 

* [Azure App Service](../app-service/app-service-value-prop-what-is.md)에서 빌드되고 [소스 제어](../app-service-web/app-service-continuous-deployment.md), [인증](../app-service/app-service-authentication-overview.md) 및 [모니터링](../app-service-web/web-sites-monitor.md) 등의 기능을 활용합니다.
* 개발자 중심 서비스입니다.
* 표준 스크립팅 및 프로그래밍 언어를 지원합니다.
* NuGet 및 NPM을 지원합니다.

함수는 hello WebJobs의 자연 스런 WebJobs의 가장 큰 이점 hello를 사용 하 고 그에 따라 향상 됩니다. hello 기능 향상은 다음과 같습니다. 

* 간소화 된 개발, 테스트 및 hello 브라우저에서 직접 코드를 실행 합니다.
* 더 많은 Azure 서비스 및 타사 서비스([GitHub WebHooks](https://developer.github.com/webhooks/creating/)등)와 통합을 기본 제공합니다.
* 사용량 기준 과금 기본 사용에 대 한 필요성 toopay 없습니다는 [앱 서비스 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)합니다.
* 자동으로 [동적 크기 조정](functions-scale.md)을 수행합니다.
* 앱 서비스 계획 여전히 가능한 (리소스 사용의 이점은 tootake)에서 실행 되는 응용 프로그램 서비스의 기존 고객 합니다.
* Logic Apps와 통합합니다.

다음 표에 hello 함수 및 WebJobs 간의 hello 차이점을 보여 줍니다.

|  | 함수 | 웹 작업 |
| --- | --- | --- |
| 확장 |구성이 없는 크기 조정 |App Service 계획 크기 조정 |
| 가격 |사용량 과금 또는  App Service 계획의 일부 |App Service 계획의 일부 |
| 실행 형식 |트리거됨, 예약됨(타이머 트리거 사용) |트리거됨, 연속, 예약됨 |
| 트리거 이벤트 |[timer](functions-bindings-timer.md), [Azure Cosmos DB](functions-bindings-documentdb.md), [Azure Event Hubs](functions-bindings-event-hubs.md), [HTTP/WebHook (GitHub, Slack)](functions-bindings-http-webhook.md), [Azure App Service Mobile Apps](functions-bindings-mobile-apps.md), [Azure Notification Hubs](functions-bindings-notification-hubs.md), [Azure Service Bus](functions-bindings-service-bus.md), [Azure Storage](functions-bindings-storage.md) |[Azure Storage](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), [Azure Service Bus](../app-service-web/websites-dotnet-webjobs-sdk-service-bus.md) |
| 브라우저 내부 개발 |지원됨 | 지원되지 않음 |
| Window 스크립팅 |실험적 |지원됨 |
| PowerShell |실험적 |지원됨 |
| C# |지원됨 |지원됨 |
| F# |지원됨 |지원되지 않음 |
| Bash |실험적 |지원됨 |
| PHP |실험적 |지원됨 |
| 파이썬 |실험적 |지원됨 |
| JavaScript |지원됨 |지원됨 |

여부 toouse 함수 또는 WebJobs에 따라 다르며 이미 무엇 앱 서비스와 합니다. Toorun 코드 조각, 원하는 앱 서비스 앱이 있는 toomanage 하려는 경우 동일한 DevOps 환경 hello에 함께, 웹 작업을 사용 해야 합니다. 다른 Azure 서비스 또는 심지어 타사 앱에 대 한 코드 조각 toorun 싶거나 너무 앱 서비스 앱에서 사용자 통합 코드 조각을 별도로 관리 하는 것이 하려는 경우 또는 toocall 논리 앱에서 사용자 코드 조각을 원하는 경우 모든 활용 해야 함수에서 hello 개선 되었습니다.  

<a name="together"></a>

## <a name="flow-logic-apps-and-functions-together"></a>Flow, Logic Apps 및 Functions
위에서 언급 한 대로 상황에 따라 서비스를 적합 한 tooyou 가장 합니다. 

* 간단한 비즈니스 최적화에는 Flow를 사용합니다.
* Flow에는 지나치게 복잡한 통합 시나리오이거나 DevOps 기능 및 보안 정책을 준수해야 하는 경우에는 Logic Apps를 사용합니다.
* 통합 시나리오의 단계에서 고도의 사용자 지정 변환 또는 특수한 코드가 필요한 경우에는 함수 앱을 작성한 다음 논리 앱에서 동작으로 함수를 트리거합니다.

흐름에서 논리 앱을 호출할 수 있습니다. 논리 앱에서 함수를, 함수에서 논리 앱을 호출할 수도 있습니다. 흐름, 논리 앱 및 함수 간의 hello 통합 tooimprove 초과 작업을 계속 합니다. 하나의 서비스에 빌드하고 다른 서비스 hello에 사용 합니다. 따라서 이러한 세 가지 기술로 만드는 노력은 가치가 있습니다.

## <a name="next-steps"></a>다음 단계
시작 각각 hello 서비스의 첫 번째 흐름, 논리 앱, 함수 앱 또는 웹 작업을 만들어 하세요. Hello 다음 링크 중 하나를 클릭 합니다.

* [Microsoft Flow 시작](https://flow.microsoft.com/en-us/documentation/getting-started/)
* [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)
* [첫 번째 Azure Function 만들기](functions-create-first-azure-function.md)
* [Visual Studio를 사용하여 WebJob 배포](../app-service-web/websites-dotnet-deploy-webjobs.md)

또는 이러한 integration services에 대 한 자세한 내용은 링크를 따라 hello로 가져옵니다.

* [Christopher Anderson의 통합 시나리오에 대한 Azure Functions 및 Azure App Service 활용](http://www.biztalk360.com/integrate-2016-resources/leveraging-azure-functions-azure-app-service-integration-scenarios/)
* [Integrations Made Simple by Charles Lamanna](http://www.biztalk360.com/integrate-2016-resources/integrations-made-simple/)
* [Logic Apps Live Webcast](http://aka.ms/logicappslive)
* [Microsoft Flow Frequently asked questions](https://flow.microsoft.com/documentation/frequently-asked-questions/)
* [Azure WebJobs 설명서 리소스](../app-service-web/websites-webjobs-resources.md)


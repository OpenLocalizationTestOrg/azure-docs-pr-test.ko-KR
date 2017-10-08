---
title: "aaaScenario-Azure 서버와 고객 insights 대시보드 만들기 | Microsoft Docs"
description: "방법의 예로 Azure 논리 앱 및 Azure 기능을 피드백, 공유 데이터 등 대시보드 toomanage 고객을 빌드할 수 있습니다."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: jehollan
ms.openlocfilehash: db175e895e37aa795a9c34bf4d65566bf68f8c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a>Azure Logic Apps 및 Azure Functions를 사용하여 실시간 Customer Insights 대시보드 만들기

Azure 서버가 없는 도구 toothink 인프라에 대 한 필요 없이 강력한 기능 tooquickly hello 클라우드에서 구축 및 호스트 응용 프로그램을 제공 합니다.  이 시나리오에서는 대시보드 tootrigger 고객의 의견에, 분석 하는 기계 학습 작업 완료 만들어져 insights Power BI 또는 Azure 데이터 레이크와 같은 원본 게시 합니다.

## <a name="overview-of-hello-scenario-and-tools-used"></a>Hello 시나리오 및 사용 되는 도구 개요

이 솔루션 tooimplement 순서, 서버가 없는 응용 프로그램에서 Azure의 hello 두 핵심 구성 요소 활용 됩니다: [Azure 함수](https://azure.microsoft.com/services/functions/) 및 [Azure 논리 앱](https://azure.microsoft.com/services/logic-apps/)합니다.

논리 앱은 hello 클라우드에서 서버가 없는 워크플로 엔진입니다.  오케스트레이션 서버가 없는 구성 요소에서 제공 하 고 tooover 100 개의 서비스 및 Api를 연결 합니다.  이 시나리오에서는 고객의 의견에 논리 앱 tootrigger를 만듭니다.  Outlook.com, Office 365, 설문 조사 원숭이, Twitter 및 HTTP 요청 포함 하는 데 도움이 되는 응답할 toocustomer 피드백 hello 커넥터의 일부 [web form에서](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/)합니다.  워크플로용으로 hello 아래에서 Twitter hashtag을 모니터링 됩니다.

함수는 hello 클라우드에서 서버가 없는 compute를 제공합니다.  이 시나리오에서는 미리 정의 된 키 단어 들의 계열을 기반으로 하는 고객의 Azure 기능 tooflag 트 윗 사용 합니다.

hello 전체 솔루션 수 [Visual Studio에서 빌드](logic-apps-deploy-from-vs.md) 및 [리소스 템플릿의 일부분으로 배포](logic-apps-create-deploy-template.md)합니다.  Hello 시나리오의 연습 동영상을 보려면 이기도 [Channel 9](http://aka.ms/logicappsdemo)합니다.

## <a name="build-hello-logic-app-tootrigger-on-customer-data"></a>고객 데이터에 hello 논리 앱 tootrigger 빌드

후 [논리 앱을 만들어](logic-apps-create-a-logic-app.md) Visual Studio 또는 hello Azure 포털에서:

1. Twitter에서 **새 트윗**에 대한 트리거 추가
2. 키워드 또는 hashtag hello 트리거 toolisten tootweets를 구성 합니다.

   > [!NOTE]
   > hello 트리거에 대 한 hello 되풀이 속성이 hello 논리 앱 폴링 기반 트리거에 새 항목을 확인 하는 빈도 결정 합니다.

   ![Twitter 트리거의 예][1]

이 앱은 이제 모든 새 트윗에서 실행됩니다.  고 수 있습니다 다음 해당 윗 데이터 더 hello 감성 표현 됩니다.  이 사용 하 여 hello [Azure Cognitive 서비스](https://azure.microsoft.com/services/cognitive-services/) 텍스트의 toodetect 감성 합니다.

1. **새 단계** 클릭
1. Hello을 선택 하거나 검색할 **텍스트 분석** 커넥터
1. 선택 hello **검색 감성** 작업
1. 메시지가 표시 되 면 hello 텍스트 분석 서비스에 대 한 올바른 인식 서비스 키를 입력
1. Hello 추가 **윗 텍스트** 텍스트 tooanalyze hello으로 합니다.

Hello 윗 hello 윗 데이터 및 통찰력을 만들었으므로 이제 해당 다양 한 다른 커넥터 관련 수 있습니다.
* Power BI-행 tooStreaming 데이터 집합 추가: 보기 트 윗 Power BI 대시보드에 실시간으로 합니다.
* Azure 데이터 레이크-파일을 추가할: 고객 데이터 tooan Azure 데이터 레이크 데이터 집합 tooinclude 분석 작업에 추가 합니다.
* SQL - 행 추가: 나중의 검색을 위해 데이터베이스에 데이터를 저장합니다.
* Slack - 메시지 보내기: 작업을 필요로 하는 부정적인 피드백에 대한 Slack 채널을 경고합니다.

Azure 함수에 사용 되는 toodo hello 데이터를 기반으로 더 많은 사용자 지정 계산 될 수도 있습니다.

## <a name="enriching-hello-data-with-an-azure-function"></a>Azure 함수를 사용 하 여 hello 데이터 보강

함수를 만들 수는 Azure 구독에서 toohave 함수 앱 해야 합니다.  Hello 포털에서 Azure 함수를 만드는 방법에 대 한 자세한 정보 수 [여기에서 찾을 수](../azure-functions/functions-create-first-azure-function-azure-portal.md)

논리 앱에서 직접 호출할 함수 toobe에 대 한 해당 요구 toohave HTTP 트리거할 바인딩.  Hello를 사용 하는 것이 좋습니다 **HttpTrigger** 서식 파일입니다.

이 시나리오에서는 hello 요청 본문의 hello Azure 함수 hello 윗 텍스트 것입니다.  Hello 함수 코드에서 단순히 논리를 정의에 키 단어 또는 구를 hello 윗 텍스트에 포함 되어 있는 경우.  간단 하 게 또는 hello 시나리오에 필요에 따라 복잡 한 hello 함수 자체를 유지할 수 없습니다.

Hello 함수 hello 끝 하기만 하면 일부 데이터가 포함 된 응답 toohello 논리 앱을 반환 합니다.  간단한 부울 값(예: `containsKeyword`) 또는 복잡한 개체일 수 있습니다.

![구성된 Azure 함수 단계][2]

> [!TIP]
> 복잡 한 응답에서 논리 앱의 함수에 액세스할 때는 hello JSON을 구문 분석 작업을 사용 합니다.

Hello 함수를 저장 한 후에 위에서 만든 hello 논리 앱에 추가할 수 있습니다.  Hello 논리 앱:

1. Tooadd 클릭는 **새 단계**
1. 선택 hello **Azure 함수** 커넥터
1. Toochoose 기존 함수를 선택 하 고 만든 toohello 함수 찾아보기
1. Hello에 보낼 **윗 텍스트** hello에 대 한 **요청 본문**

## <a name="running-and-monitoring-hello-solution"></a>실행 중 이며 hello 솔루션 모니터링

논리 앱의 서버가 없는 오케스트레이션을 작성의 hello 이점 중 하나에 hello 풍부한 디버그 및 모니터링 기능입니다.  Visual Studio hello Azure 포털 내에서 또는 hello REST API와 Sdk를 통해 모든 실행 (현재 또는 기록)에서 볼 수 있습니다.

Hello를 사용 하는 hello 가장 쉬운 방법으로 tootest 논리 앱 중 하나 **실행** hello 디자이너에서 단추입니다.  클릭 하면 **실행** toopoll hello 트리거 이벤트 감지 되 면 될 때까지 5 초 마다 계속 되며 실행 hello 진행 됨에 따라 라이브 뷰를 제공 합니다.

Hello Azure 포털 또는 Visual Studio 클라우드 탐색기 hello를 사용 하 여 hello 개요 블레이드에서 이전 실행된 기록은 볼 수 있습니다.

## <a name="creating-a-deployment-template-for-automated-deployments"></a>자동화된 배포를 위한 배포 템플릿 만들기

솔루션을 개발한 후 캡처된 하 고 Azure 배포 템플릿 tooany Azure 지역에서 hello world 통해 배포할 수 있습니다.  이 워크플로의 다양한 버전에 대한 매개 변수 수정뿐만 아니라 빌드 및 릴리스 파이프라인에서 이 솔루션을 통합하는 데 유용합니다.  배포 템플릿 만들기에 대한 자세한 내용은 [이 문서에서](logic-apps-create-deploy-template.md) 찾을 수 있습니다.

Azure 기능 통합 될 수도 있지만 hello 배포 템플릿에-단일 템플릿으로 모든 종속성이 있는 hello 전체 솔루션을 관리할 수 있도록 합니다.  함수 템플릿은 배포의 예는 hello에서 확인할 수 있습니다 [Azure 빠른 시작 템플릿 리포지토리](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic)합니다.

## <a name="next-steps"></a>다음 단계

* [Azure Logic Apps 다른 예제 및 시나리오 참조](logic-apps-examples-and-scenarios.md)
* [종단 간 이 솔루션을 만드는 연습 동영상 시청](http://aka.ms/logicappsdemo)
* [자세한 내용은 어떻게 논리 앱 내에서 toohandle 및 catch 예외](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: ./media/logic-apps-scenario-social-serverless/twitter.png
[2]: ./media/logic-apps-scenario-social-serverless/function.png
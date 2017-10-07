---
title: "Azure 클라우드 서비스에 대 한 Insights aaaApplication | Microsoft Docs"
description: "Application Insights를 사용하여 웹 및 작업자 역할을 효과적으로 모니터링"
services: application-insights
documentationcenter: 
keywords: "WAD2AI, Azure 진단"
author: CFreemanwa
manager: carmonm
editor: alancameronwills
ms.assetid: 5c7a5b34-329e-42b7-9330-9dcbb9ff1f88
ms.service: application-insights
ms.devlang: na
ms.tgt_pltfrm: ibiza
ms.topic: get-started-article
ms.workload: tbd
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 6956ce423eea1e2cf387bd98250bae32d9501ed0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-azure-cloud-services"></a>Azure 클라우드 서비스용 Application Insights
[Microsoft Azure Cloud Service 앱](https://azure.microsoft.com/services/cloud-services/)은 Application Insights SDK의 데이터를 Cloud Services의 [Azure 진단](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics) 데이터와 조합하여 [Application Insights][start]로 가용성, 성능, 오류 및 사용 현황을 모니터링할 수 있습니다. 와일드 카드 hello 성능과 hello에서 응용 프로그램의 효율성에 대 한 get hello 피드백을 통해 각 개발 수명 주기의 hello 디자인의 hello 방향에 대 한 선택 가능한 항목을 만들 수 있습니다.

![예제](./media/app-insights-cloudservices/sample.png)

## <a name="before-you-start"></a>시작하기 전에
필요한 사항:

* [Microsoft Azure](http://azure.com)를 구독해야 합니다. Microsoft 계정으로 로그인합니다. Windows, XBox Live 또는 기타 Microsoft 클라우드 서비스의 계정을 사용할 수 있습니다. 
* Microsoft Azure 도구 2.9 이상
* 개발자 분석 도구 7.10 이상

## <a name="quick-start"></a>빠른 시작
Application Insights를 사용 하 여 클라우드 서비스는 서비스 tooAzure 게시 옵션 toochoose 빠르고 쉬운 방법 toomonitor를 hello 합니다.

![예제](./media/app-insights-cloudservices/azure-cloud-application-insights.png)

Toomonitor 요청, 예외 및 성능 뿐 웹 역할에서 종속성을 해야 하는 모든 hello 원격 분석을 제공 하 여 앱 실행 시 카운터 작업자 역할에서이 옵션 수단입니다. 응용 프로그램에 의해 생성 된 모든 진단 추적 tooApplication Insights도 전송 됩니다.

필요한 항목을 모두 얻었으면 작업이 완료된 것입니다. 다음 단계에서는 [앱에서 메트릭을 보고](app-insights-metrics-explorer.md), [분석을 사용하여 데이터를 쿼리하고](app-insights-analytics.md), [대시보드](app-insights-dashboards.md)를 설정합니다. Tooset를 할 수 있습니다 [가용성 테스트](app-insights-monitor-web-app-availability.md) 및 [tooyour 웹 페이지 코드를 추가할](app-insights-javascript.md) hello 브라우저에서 toomonitor 성능입니다.

하지만 더 많은 옵션을 얻을 수 있습니다.

* 다른 구성 요소에서 데이터를 보내고 빌드 tooseparate 리소스를 구성 합니다.
* 앱에서 사용자 지정 원격 분석을 추가합니다.

이러한 옵션을 원하는 tooyou의 경우 계속 읽어 보십시오.

## <a name="sample-application-instrumented-with-application-insights"></a>Application Insights를 사용하여 계측하는 샘플 응용 프로그램
이에 대해 살펴봅니다 [샘플 응용 프로그램](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService) 를 Application Insights와 Azure에서 호스팅되는 두 가지 작업자 역할로 tooa 클라우드 서비스를 추가 합니다. 

뒤에 나오는 설명을 알려 어떻게 tooadapt 직접 클라우드 서비스 프로젝트에서 hello 동일한 방식으로 합니다.

## <a name="plan-resources-and-resource-groups"></a>리소스 및 리소스 그룹 계획
앱에서 원격 분석 hello 저장 하 고 분석 하 고 Application Insights 형식의 Azure 리소스에 표시 됩니다. 

각 리소스 tooa 리소스 그룹을 속해 있습니다. 조정 된 단일 트랜잭션에서 toodeploy 업데이트 및 리소스 그룹 tooteam 멤버 액세스 허용을 위한 비용을 관리 하기 위한 사용 됩니다. 예를 들어 할 수 [스크립트 toodeploy 작성](../azure-resource-manager/resource-group-template-deploy.md) Azure 클라우드 서비스 및 해당 Application Insights를 한 번에 모든 리소스를 모니터링 합니다.

### <a name="resources-for-components"></a>구성 요소에 대한 리소스
hello는 구성표는 각 웹 역할 및 작업자 역할 즉, 응용 프로그램의 각 구성 요소에 대 한 별도 리소스 toocreate 하는 것이 좋습니다. 각 구성 요소를 개별적으로 분석할 수 있지만 만들 수는 [대시보드](app-insights-dashboards.md) 마무리 함께 hello 주요 차트 모든 hello 구성 요소를 비교 하 고 함께 모니터링할 수 있도록 합니다. 

대체 스키마에서 둘 이상의 역할 toohello toosend hello 원격 분석은 동일한 리소스에 있지만 [차원 속성 tooeach 원격 분석 항목을 추가](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer) 의 소스 역할을 식별 하는 합니다. 이 스키마에서는 예외 등 메트릭 차트 정상적으로 표시 hello hello 개수에 대 한 집계를 서로 다른 역할 되지만 hello 역할 식별자 필요할 때 hello 차트를 분할할 수 있습니다. 검색 hello 하 여 필터링 할 수도 있습니다 동일한 차원입니다. 이 대체 좀 더 쉽게 tooview를 사용 하면 시간, 동일 하지만 hello 역할 간에 toosome 혼동 이어질 수도 hello에서 모든 항목입니다.

브라우저 원격 분석 hello에 대체로 포함 되는 서버 쪽 웹 역할로 동일한 리소스입니다.

하나의 리소스 그룹에 hello 서로 다른 구성 요소에 대 한 hello Application Insights 리소스를 배치 합니다. 이렇게 하면 쉽게 toomanage 할 수 있습니다. 

### <a name="separating-development-test-and-production"></a>개발, 테스트 및 프로덕션 구분
을 개발 하는 사용자 지정 이벤트에 다음 기능에 대 한 이전 버전 hello 라이브 상태일 경우 원하는 toosend hello 개발 원격 분석 tooa 별도 Application Insights 리소스입니다. 그렇지 않으면 됩니다 하드 toofind 간에 테스트 원격 분석 hello 라이브 사이트의 트래픽이 hello 모든 합니다.

tooavoid이이 경우 각 빌드 구성 또는 '스탬프' (개발, 테스트, 프로덕션,...)의 시스템에 대 한 별도 리소스를 만듭니다. 별도 리소스 그룹에 각 빌드 구성에 대 한 hello 리소스를 넣습니다. 

toosend hello 원격 분석 toohello 적절 한 리소스를 hello 빌드 구성에 따라 다른 계측 키.wadcfg 있도록 hello Application Insights SDK를 설정할 수 있습니다. 

## <a name="create-an-application-insights-resource-for-each-role"></a>각 역할에 대한 Application Insights 리소스 만들기
Toocreate 각 역할에 대해 별도 리소스를 결정 한 각 빌드 구성-에 대 한 별도 설정 아마도 경우 것이 가장 쉬운 toocreate hello Application Insights 포털에서 모든 해당 합니다. (리소스를 많이 만들어야 하는 경우 다음을 할 수 있습니다 [hello 프로세스를 자동화](app-insights-powershell.md)합니다.

1. Hello에 [Azure 포털][portal], 새 Application Insights 리소스를 만듭니다. 응용 프로그램 유형으로 ASP.NET 앱을 선택합니다. 

    ![새로 만들기, Application Insights 클릭](./media/app-insights-cloudservices/01-new.png)
2. 각 리소스는 계측 키로 식별됩니다. Toomanually 하려는 경우 나중에이 필요할 수 있습니다 구성 하거나 SDK hello hello 구성을 확인 하십시오.

    ![속성을 클릭 hello 키를 선택 하 고 ctrl + C를 누릅니다.](./media/app-insights-cloudservices/02-props.png) 

## <a name="set-up-azure-diagnostics-for-each-role"></a>각 역할에 대한 Azure 진단 설정
이 옵션 toomonitor Application Insights를 사용 하 여 앱을 설정 합니다. 웹 역할의 경우 성능 모니터링, 경고 및 진단과 함께 사용 현황 분석이 제공됩니다. 다른 역할에 대 한 검색 하 고 다시 시작, 성능 카운터 및 호출 tooSystem.Diagnostics.Trace 같은 Azure 진단을 모니터링할 수 있습니다. 

1. Visual Studio 솔루션 탐색기에서 아래 &lt;YourCloudService&gt;, 역할, 각 역할의 hello 속성을 엽니다.
2. **구성**설정, **진단 데이터 tooApplication Insights 보낼** 선택 hello 이전에 만든 적절 한 Application Insights 리소스 및 합니다.

각 빌드 구성에 대 한 별도 Application Insights 리소스 toouse 계획인 경우 먼저 hello 구성을 선택 합니다.

![각 Azure 역할의 hello 속성에서 Application Insights 구성](./media/app-insights-cloudservices/configure-azure-diagnostics.png)

이 hello 라는 hello 파일에 Application Insights 계측 키를 삽입 `ServiceConfiguration.*.cscfg`합니다. ([샘플 코드](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/AzureEmailService/ServiceConfiguration.Cloud.cscfg)).

Toovary hello 수준의 전송 되는 진단 정보 tooApplication 통찰력을 하려는 경우 그렇게 할 수 있습니다 [hello를 편집 하 여 `.cscfg` 파일을 직접](app-insights-azure-diagnostics.md)합니다.

## <a name="sdk"></a>각 프로젝트에 hello SDK 설치
이 옵션 hello 기능 tooadd 사용자 지정 비즈니스 원격 분석 tooany 역할을 하는 응용 프로그램의 사용 방법 및 수행 보다 자세하게 분석을 추가 합니다.

Visual Studio에서 각 클라우드 응용 프로그램 프로젝트에 대 한 hello Application Insights SDK를 구성 합니다.

1. **웹 역할**: hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **Configure Application Insights** 또는 **추가 > Application Insights 원격 분석**합니다.

2. **작업자 역할**: 
 * Hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **Nuget 패키지 관리**합니다.
 * [Windows 서버용 Application Insights](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/)를 추가합니다.

    !["Application Insights" 검색](./media/app-insights-cloudservices/04-ai-nuget.png)

3. Hello SDK toosend 데이터 toohello Application Insights 리소스를 구성 합니다.

    적합 한 시작 함수에서 hello 계측 키를 hello.cscfg 파일에 hello 구성 설정에서 설정 합니다.
 
    ```C#
   
     TelemetryConfiguration.Active.InstrumentationKey = RoleEnvironment.GetConfigurationSettingValue("APPINSIGHTS_INSTRUMENTATIONKEY");
    ```
   
    응용 프로그램에서 각 역할에 대해 이 작업을 수행합니다. Hello 예제를 참조 하십시오.
   
   * [웹 역할](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Global.asax.cs#L27)
   * [작업자 역할](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L232)
   * [웹 페이지](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Views/Shared/_Layout.cshtml#L13) 
4. 집합 hello ApplicationInsights.config 파일 toobe 복사 항상 toohello 출력 디렉터리입니다. 
   
    (Hello.config 파일에 표시 하면 tooplace hello 계측 키 있습니다를 요청 하는 메시지입니다. 그러나 클라우드 응용 프로그램에 대 한 것이 더 나은 tooset hello.cscfg 파일에서 합니다. 이렇게 하면 해당 hello 역할 hello 포털에서 올바르게 식별 됩니다.)

#### <a name="run-and-publish-hello-app"></a>실행 하 고 hello 앱 게시
앱을 실행하고 Azure에 로그인합니다. 열기 hello Application Insights 리소스 생성 하 고 개별 데이터 요소에 나타나는 표시 됩니다 [검색](app-insights-diagnostic-search.md), 집계에서 데이터 및 [메트릭 탐색기](app-insights-metrics-explorer.md)합니다. 

더 많은 원격 분석 추가-아래-hello 섹션을 참조 하 고 응용 프로그램 tooget 라이브 진단 및 사용 현황 의견을 게시 하십시오. 

#### <a name="no-data"></a>데이터가 없나요?
* 열기 hello [검색] [ diagnostic] 타일을 toosee 개별 이벤트입니다.
* 일부 원격 분석을 생성할 수 있도록 각기 다른 페이지를 여는 hello 응용 프로그램을 사용 합니다.
* 몇 초 정도 기다렸다가 새로고침을 클릭합니다.
* [문제 해결][qna]을 참조하세요.

## <a name="view-azure-diagnostic-events"></a>Azure 진단 이벤트 보기
여기서 toofind hello [Azure 진단](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics) Application Insights에서 정보:

* 성능 카운터는 사용자 지정 메트릭으로 표시됩니다. 
* Windows 이벤트 로그는 추적 및 사용자 지정 이벤트로 표시됩니다.
* 응용 프로그램 로그, ETW 로그 및 진단 인프라 로그는 추적으로 표시됩니다.

toosee 성능 카운터 및 이벤트의 개수를 열고 [메트릭 탐색기](app-insights-metrics-explorer.md) 및 새 차트를 추가 합니다.

![Azure 진단 데이터](./media/app-insights-cloudservices/23-wad.png)

사용 하 여 [검색](app-insights-diagnostic-search.md) 또는 [분석 쿼리](app-insights-analytics-tour.md) 걸쳐 다양 한 추적 로그 Azure 진단에서 보낸 hello toosearch 합니다. 예를 들어 역할 toocrash 및 재활용의 원인이 된 처리 되지 않은 예외를 있다고 가정 합니다. 해당 정보 hello 응용 프로그램 채널의 Windows 이벤트 로그에 표시 됩니다. 검색 toolook hello Windows 이벤트 로그 오류에 사용할 수 있으며 hello 예외에 대 한 hello 전체 스택 추적을 가져와야 수 있습니다. Hello 문제의 근본 원인을 hello를 찾는 데 도움이 됩니다입니다.

![Azure 진단 검색](./media/app-insights-cloudservices/25-wad.png)

## <a name="more-telemetry"></a>추가 원격 분석
show 아래 섹션 hello 방법을 응용 프로그램의 여러 측면에서 tooget 추가 원격 분석 합니다.

## <a name="track-requests-from-worker-roles"></a>작업자 역할의 요청 추적
웹 역할에 hello 요청 모듈 자동으로 HTTP 요청에 대 한 데이터를 수집합니다. Hello 참조 [MVCWebRole 샘플](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole) hello 기본 컬렉션 동작을 재정의 하는 방법에 대 한 예제입니다. 

Hello에이 추적 하 여 호출 tooworker 역할의 hello 성능을 캡처할 수 동일한 방식으로 HTTP 요청입니다. Application Insights 요청 원격 분석 유형을 hello 일정 시간이 수 독립적으로 성공 하거나 실패 하는 명명 된 서버 쪽 작업의 단위를 측정 합니다. HTTP 요청은 hello SDK에서 자동으로 캡처되는 동안에 사용자 고유의 코드 tootrack 요청 tooworker 역할을 삽입할 수 있습니다.

Hello 두 샘플 작업자 역할 계측 된 tooreport 요청 참조: [WorkerRoleA](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/WorkerRoleA) 및 [WorkerRoleB](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/WorkerRoleB)

## <a name="exceptions"></a>예외
다른 웹 응용 프로그램 유형에서 처리되지 않은 예외를 수집할 수 있는 방법에 대한 자세한 내용은 [Application Insights에서 예외 모니터링](app-insights-asp-net-exceptions.md)을 참조하세요.

hello 샘플 웹 역할에는 m v c 5 및 Web API 2 컨트롤러에 있습니다. hello hello 2에서에서 처리 되지 않은 예외를 수집 처리기를 다음 hello로 합니다.

* MVC5 컨트롤러에 대해 [여기](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/App_Start/FilterConfig.cs#L12)에서 [AiHandleErrorAttribute](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Telemetry/AiHandleErrorAttribute.cs) 설정
* Web API 2 컨트롤러에 대해 [여기](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/App_Start/WebApiConfig.cs#L25)에서 [AiWebApiExceptionLogger](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Telemetry/AiWebApiExceptionLogger.cs) 설정

작업자 역할에 대 한 두 가지가 tootrack 예외:

* TrackException(ex)
* 사용할 수 있습니다 hello Application Insights 추적 수신기 NuGet 패키지를 추가한 경우 **System.Diagnostics.Trace** toolog 예외입니다. [코드 예제.](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L107)

## <a name="performance-counters"></a>성능 카운터
기본적으로 hello 다음 카운터를 수집 합니다.

    * \Process(??APP_WIN32_PROC??)\% Processor Time
    * \Memory\Available Bytes
    * \.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec
    * \Process(??APP_WIN32_PROC??)\Private Bytes
    * \Process(??APP_WIN32_PROC??)\IO Data Bytes/sec
    * \Processor(_Total)\% Processor Time

웹 역할의 경우 이러한 카운터도 수집됩니다.

    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec
    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time
    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue

[이 예제와 같이](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/ApplicationInsights.config#L14) ApplicationInsights.config를 편집하여 추가 사용자 지정 카운터 또는 기타 windows 성능 카운터를 지정할 수 있습니다.

  ![성능 카운터](./media/app-insights-cloudservices/OLfMo2f.png)

## <a name="correlated-telemetry-for-worker-roles"></a>작업자 역할에 대한 상호 관련된 원격 분석
어떤 실패 led tooa 또는 대기 시간이 긴 요청을 볼 수 있습니다 때 풍부한 진단 환경을 야 합니다. 웹 역할의 경우와 SDK 간 상관 관계를 자동으로 설정 하는 hello 관련 원격 분석 합니다. 작업자 역할에 사용할 수 있습니다는 사용자 지정 원격 분석 이니셜라이저 tooset 공통 Operation.Id 컨텍스트 특성 모든 hello 원격 분석 tooachieve에 대 한 합니다. 이렇게 하면 toosee 기한 tooa 종속성 또는 코드를 한 눈에 hello 대기 시간/실패 문제의 원인은 여부! 

방법은 다음과 같습니다.

* 표시 된 대로 CallContext에 hello 상관 관계 Id를 설정 [여기](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L36)합니다. 이 경우 요청 ID hello hello 상관 관계 id로 사용
* 사용자 지정 TelemetryInitializer 구현 이상으로 설정 하는 tooset hello Operation.Id toohello correlationId를 추가 합니다. 그 예로 [ItemCorrelationTelemetryInitializer](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/Telemetry/ItemCorrelationTelemetryInitializer.cs#L13)를 들 수 있습니다.
* Hello 사용자 지정 원격 분석 이니셜라이저를 추가 합니다. 수행할 수 있습니다 또는 코드를 hello ApplicationInsights.config 파일에 표시 된 것 처럼 [여기](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L233)

이것으로 끝입니다. hello 포털 환경 이미 유선 toohelp를 한 눈에 관련 된 모든 원격 분석 표시:

![상관 관계가 지정된 원격 분석](./media/app-insights-cloudservices/bHxuUhd.png)

## <a name="client-telemetry"></a>클라이언트 원격 분석
[추가 JavaScript SDK tooyour 웹 페이지 hello] [ client] tooget 브라우저 기반 원격 페이지 보기 수, 페이지 로드 시간, 스크립트 예외가 toolet 페이지 스크립트에서 사용자 지정 원격 분석을 작성 등 분석 합니다.

## <a name="availability-tests"></a>가용성 테스트
[웹 테스트 설정] [ availability] toomake 라이브 및 응답성이 뛰어난 응용 프로그램 없이 계속 합니다.

## <a name="display-everything-together"></a>모든 항목을 함께 표시
시스템의 전반적인 tooget 하나에 차트를 함께 모니터링 하는 hello 키를 가져올 수 있습니다 [대시보드](app-insights-dashboards.md)합니다. 예를 들어 hello 요청을 고정할 수 있습니다 및 각 역할의 오류를 계산 합니다. 

시스템에서 스트림 분석과 같은 다른 Azure 서비스를 사용하는 경우 해당 모니터링 차트도 포함합니다. 

클라이언트 모바일 앱이 있는 주요 사용자 작업에 몇 가지 코드 toosend 사용자 지정 이벤트를 삽입 하 고 만들는 [HockeyApp 브리지](app-insights-hockeyapp-bridge-app.md)합니다. 쿼리를 만들 [분석](app-insights-analytics.md) toodisplay 이벤트 수를 hello 및 toohello 대시보드에 고정 합니다.

## <a name="example"></a>예제
[hello 예제](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService) 웹 역할과 작업자 역할을 두 개의 있는 서비스를 모니터링 합니다.

## <a name="exception-method-not-found-on-running-in-azure-cloud-services"></a>Azure 클라우드 서비스에서 실행할 때의 "메서드를 찾을 수 없음" 예외
.NET 4.6용으로 빌드하셨나요? 4.6은 Azure 클라우드 서비스 역할에서 자동으로 지원되지 않습니다. [각 역할에 4.6을 설치](../cloud-services/cloud-services-dotnet-install-dotnet.md) 합니다.

## <a name="video"></a>비디오

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>다음 단계
* [Azure 진단 tooApplication Insights 보내기 구성](app-insights-azure-diagnostics.md)
* [Application Insights 리소스 만들기 자동화](app-insights-powershell.md)
* [Azure 진단 자동화](app-insights-powershell-azure-diagnostics.md)
* [Azure 기능](https://github.com/christopheranderson/azure-functions-app-insights-sample)

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[azure]: app-insights-azure.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[netlogs]: app-insights-asp-net-trace-logs.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md 

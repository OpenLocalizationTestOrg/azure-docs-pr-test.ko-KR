---
title: "Azure 웹 앱 성능 aaaMonitor | Microsoft Docs"
description: "Azure 웹앱에 대한 응용 프로그램 성능 모니터링입니다. 차트 부하 및 응답 시간, 종속성 정보 및 성능에 대한 경고를 설정합니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d1083254e5c504b18f2ac5ae2368610dc2790436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-web-app-performance"></a>Azure 웹앱 성능 모니터링
Hello에 [Azure 포털](https://portal.azure.com) 에 대 한 응용 프로그램 성능 모니터링을 설정할 수 있습니다 프로그램 [Azure 웹 앱](../app-service-web/app-service-web-overview.md)합니다. [Azure Application Insights](app-insights-overview.md) 해당 활동 toohello Application Insights 서비스에 저장 되 고 분석 하는 방법에 대 한 앱 toosend 원격 분석을 계측 합니다. 메트릭 차트 및 검색 도구 사용할 수 있습니다, toohelp 문제를 진단, 성능 향상을 및 사용량 평가 합니다.

## <a name="run-time-or-build-time"></a>실행 시간 또는 빌드 시간
두 가지 방법 중 하나로 hello 응용 프로그램을 계측 하 여 모니터링을 구성할 수 있습니다.

* **런타임** - 웹앱이 이미 라이브 상태인 경우 성능 모니터링 확장을 선택할 수 있습니다. 필요한 toorebuild 아니거나 다시 앱을 설치 합니다. 응답 시간, 성공률, 예외, 종속성 등을 모니터링하는 패키지의 표준 집합을 얻게 됩니다. 
* **빌드 시간** - 개발 중인 앱에서 패키지를 설치할 수 있습니다. 이 옵션은 융통성이 뛰어납니다. 또한 toohello에서 같은 표준 패키지를 작성할 수 있습니다 코드 toocustomize hello 원격 분석 또는 toosend 직접 원격 분석 합니다. 특정 작업 또는 응용 프로그램 도메인의 toohello 의미 체계에 따라 레코드 이벤트를 기록할 수 있습니다. 

## <a name="run-time-instrumentation-with-application-insights"></a>Application Insights를 사용하여 시간 계측 실행
Azure에서 웹앱을 이미 실행 중인 경우 이미 일부 요청 및 오류 비율을 모니터링하고 있습니다. Application Insights tooget 응답 시간, 모니터링 호출 toodependencies, 스마트 검색 및 hello 강력한 로그 분석 쿼리 언어 같은 더 추가 합니다. 

1. **Application Insights 선택** hello Azure 제어판에서 웹 앱에 대 한 합니다.
   
    ![모니터링 아래에서 Application Insights 선택](./media/app-insights-azure-web-apps/05-extend.png)
   
   * 설정 하지 않는 한 이미이 앱에 대 한 Application Insights 리소스 다른 경로 의해 toocreate 새 리소스를 선택 합니다.
2. Application Insights를 설치한 후 **웹앱을 계측**합니다. 
   
    ![웹앱 계측](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   페이지 보기 및 사용자 원격 분석을 위해 **클라이언트 쪽 모니터링을 사용하도록 설정**합니다.

   * 설정 > 응용 프로그램 설정 선택
   * 앱 설정 아래에서 새로운 키 값 쌍을 추가합니다. 
   
    키: `APPINSIGHTS_JAVASCRIPT_ENABLED` 
    
    값: `true`
   * **저장** 설정 hello 및 **다시 시작** 앱.
3. **앱을 모니터링합니다**.  [Expore hello 데이터](#explore-the-data)합니다.

이상에서는 원하는 경우 Application Insights를 사용한 hello 앱을 빌드할 수 있습니다.

*Application Insights를 제거 하거나 toosending tooanother 리소스를 전환 하려면 어떻게 합니까?*

* Azure에서 열기 hello 웹 응용 프로그램 제어 블레이드 및 개발 도구를 열 **확장**합니다. Hello Application Insights 확장을 삭제 합니다. 다음에서 모니터링에서 Application Insights를 선택 하 고 만들기 하거나 hello 자원을 선택 합니다.

## <a name="build-hello-app-with-application-insights"></a>Application Insights를 사용한 hello 앱 빌드
Application Insights는 앱에 SDK를 설치하여 더 자세한 원격 분석을 제공할 수 있습니다. 특히 추적 로그를 수집하고 [사용자 지정 원격 분석을 작성](app-insights-api-custom-events-metrics.md)하고 보다 자세한 예외 보고서를 가져올 수 있습니다.

1. **Visual Studio**(2013 업데이트 2 이상)에서 프로젝트를 위한 Application Insights를 구성합니다.

    Hello 웹 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가 > Application Insights** 또는 **Configure Application Insights**합니다.
   
    ![Hello 웹 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 추가 또는 Application Insights 구성 선택](./media/app-insights-azure-web-apps/03-add.png)
   
    toosign 묻는 경우 Azure 계정에 대 한 hello 자격 증명을 사용 합니다.
   
    hello 작업에는 두 개의 효과가 있습니다.
   
   1. 원격 분석을 저장하고, 분석하고 표시할 수 있는 Azure에서 Application Insights 리소스를 만듭니다.
   2. Hello Application Insights NuGet 패키지 tooyour 코드 (있지 않은 경우 있습니다)를 추가 하 고 toosend 원격 분석 toohello Azure 리소스를 구성 합니다.
2. **Hello 원격 분석 테스트** 여 (F5) 개발 컴퓨터에서 실행 중인 hello 응용 프로그램입니다.
3. **Hello 앱 게시** tooAzure hello에 일반적인 방법입니다. 

*Toosending tooa 다른 Application Insights 리소스를 전환 하는 방법*

* Visual Studio를 마우스 오른쪽 단추로 클릭 hello 프로젝트에서 선택할 **Configure Application Insights** 원하는 hello 리소스를 선택 합니다. 새 리소스를 hello 옵션 toocreate를 가져옵니다. 다시 빌드하고 다시 배포합니다.

## <a name="explore-hello-data"></a>Hello 데이터 탐색
1. 라이브 메트릭, 두 번째 또는 두 개만이 내 요청 및 오류의 보여 주는 웹 앱 제어판의 Application Insights 블레이드에서 hello 표시 발생 합니다. 모든 문제를 즉시 확인할 수 있으므로 앱을 다시 게시하는 경우 매우 유용한 표시입니다.
2. Toohello 완전 한 Application Insights 리소스를 클릭 합니다.

    ![클릭](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    Azure 리소스 탐색에서 직접 이동할 수도 있습니다.

1. 클릭 하 여 모든 차트 tooget 자세히:
   
    ![Hello Application Insights 개요 블레이드에에서 차트를 클릭 합니다.](./media/app-insights-azure-web-apps/07-dependency.png)
   
    [메트릭 블레이드를 사용자 지정](app-insights-metrics-explorer.md)할 수 있습니다.
2. 추가 toosee 개별 이벤트 및 해당 속성을 통해를 클릭 합니다.
   
    ![해당 형식에 검색을 필터링 하는 이벤트 유형을 tooopen 클릭](./media/app-insights-azure-web-apps/08-requests.png)
   
    Hello "..." 링크 tooopen 모든 속성을 확인 합니다.
   
    [검색을 사용자 지정](app-insights-diagnostic-search.md)할 수 있습니다.

원격 분석을 통해 더 강력한 검색에 대 한 hello를 사용 하 여 [로그 분석 쿼리 언어](app-insights-analytics-tour.md)합니다.

## <a name="more-telemetry"></a>추가 원격 분석

* [웹 페이지 로드 데이터](app-insights-javascript.md)
* [사용자 지정 원격 분석](app-insights-api-custom-events-metrics.md)

## <a name="video"></a>비디오

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>다음 단계
* [라이브 앱에서 hello 프로파일러를 실행](app-insights-profiler.md)합니다.
* [Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - Application Insights로 Azure Functions 모니터링
* [Azure 진단을 사용 하도록 설정](app-insights-azure-diagnostics.md) 전송 toobe tooApplication Insights 합니다.
* [서비스 상태 메트릭을 모니터링](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake 서비스를 사용 가능 하 고 응답 합니다.
* 작업 이벤트가 발생하거나 메트릭이 임계값을 초과할 때마다 [경고 알림을 수신](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)합니다.
* 사용 하 여 [JavaScript 앱과 웹 페이지에 대 한 Application Insights](app-insights-javascript.md) 웹 페이지를 방문 하는 hello 브라우저에서 tooget 클라이언트 원격 분석 합니다.
* [가용성 웹 테스트 설정](app-insights-monitor-web-app-availability.md) toobe 사이트가 다운 된 경우 경고를 표시 합니다.


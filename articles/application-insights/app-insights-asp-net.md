---
title: "for Azure Application Insights와 ASP.NET 웹 응용 프로그램 분석을 aaaSet | Microsoft Docs"
description: "Azure 또는 온-프레미스에 호스트되는 ASP.NET 웹 사이트에 대한 성능, 가용성 및 사용 현황 분석을 구성합니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d0eee3c0-b328-448f-8123-f478052751db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 61a3cdce68da48bfb9450b1d296acc1535f50a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a>ASP.NET 웹 사이트용 Application Insights 설정

이 절차에서는 ASP.NET 웹 응용 프로그램 toosend 원격 분석 toohello 구성 [Azure Application Insights](app-insights-overview.md) 서비스입니다. Hello 클라우드 또는 사용자 고유의 IIS 서버에 호스트 되는 ASP.NET 응용 프로그램에 대 한 작동 합니다. 차트를 얻게 하 고 응용 프로그램의 성능을 hello 및 사용 되는 방식을 추가 자동 경고 성능 문제 또는 오류에을 이해 하는 데 도움이 되는 강력한 쿼리 언어입니다. 많은 개발자 들이 이러한 기능 훌륭한는 것만 확장 하 고 하는 경우 hello 원격 분석을 사용자 지정할 수도 있습니다.

Visual Studio에서 설치 프로그램을 몇 번만 클릭하면 됩니다. 원격 분석의 hello 볼륨을 제한 하 여 hello 옵션 tooavoid 요금 해야 합니다. 이렇게 하면 tooexperiment 및 디버그 또는 toomonitor 하지 많은 사용자가 사용 하는 사이트 있습니다. 프로덕션 사이트를 모니터링 하 고 계속 toogo 원하는 결정할 때 쉽게 tooraise hello 제한 나중에 됩니다.

## <a name="before-you-start"></a>시작하기 전에
다음 작업을 수행해야 합니다.

* Visual Studio 2013 업데이트 3 이상 나중일수록 좋습니다.
* 구독 너무[Microsoft Azure](http://azure.com)합니다. 팀 또는 조직에 Azure 구독이 있으면 hello 소유자 추가할 수 있습니다 tooit를 사용 하 여 프로그램 [Microsoft 계정](http://live.com)합니다.

에 관심이 있는 경우에 대체 항목 toolook이 있습니다.

* [런타임 시 웹앱 계측](app-insights-monitor-performance-live-website-now.md)
* [Azure 클라우드 서비스](app-insights-cloudservices.md)

## <a name="ide"></a>1 단계: hello Application Insights SDK 추가

[솔루션 탐색기]에서 웹앱 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **Application Insights 원격 분석...** 또는 **Application Insights 구성**을 선택합니다.

![추가, Application Insights 원격 분석이 강조 표시된 솔루션 탐색기 스크린샷](./media/app-insights-asp-net/appinsights-03-addExisting.png)

(Visual Studio 2015에도 hello 새 프로젝트 대화 상자에서 옵션 tooadd Application Insights.)

Toohello Application Insights 구성 페이지를 계속 진행 합니다.

![Application Insights에 앱 등록 페이지의 스크린샷](./media/app-insights-asp-net/visual-studio-register-dialog.png)

**a.** Hello 계정과 tooaccess Azure를 사용 하는 구독을 선택 합니다.

**b.** 앱에서 toosee hello 데이터를 원하는 Azure의 hello 리소스를 선택 합니다. 일반적으로

* 단일 응용 프로그램의 [여러 구성 요소에 대해 단일 리소스](app-insights-monitor-multi-role-apps.md)를 사용합니다. 
* 관계 없는 응용 프로그램에 대해 별도의 리소스를 만듭니다.
 
Tooset hello 리소스 그룹 또는 hello 위치 데이터가 저장 되어 클릭 **설정을 구성**합니다. 리소스 그룹은 사용 되는 toocontrol 액세스 toodata 합니다. 예를 들어의 일부가 되 여러 응용 프로그램이 있는 경우 hello 동일한 시스템의 Application Insights 데이터를 지정할 수 있습니다 hello 동일한 리소스 그룹입니다.

**c.** Hello 무료 데이터 볼륨도 tooavoid 요금에 한 한도가 설정 합니다. Application Insights는 tooa 확보 특정 양의 원격 분석 합니다. Hello 리소스를 만든 후에 열어 hello 포털에서 선택 사항을 변경할 수 있습니다 **기능 + 가격 책정** > **데이터 볼륨 관리** > **매일 볼륨 cap**합니다.

**d.** 클릭 **등록** toogo 계속 하 고 웹 응용 프로그램에 대 한 Application Insights를 구성 합니다. 원격 분석 전송 toohello 됩니다 [Azure 포털](https://portal.azure.com), 디버깅 하는 동안와 응용 프로그램을 게시 한 후 합니다.

**e.** 되지 않도록 toosend 원격 분석 toohello 포털을 디버깅할 때 hello Application Insights SDK tooyour 앱 추가 hello 포털에서 리소스를 구성 하지 않으면 뿐입니다. 디버깅 하는 동안에 Visual Studio에서 수 toosee 원격 분석 됩니다. 나중 toothis 구성 페이지에서 반환할 수 있습니다 또는 앱을 배포한 후 될 때까지 기다릴 수 있습니다 및 [런타임 시 원격 분석 켜기](app-insights-monitor-performance-live-website-now.md)합니다.


## <a name="run"></a> 2단계: 앱 실행
F5를 사용하여 앱을 실행합니다. 일부 원격 분석 toogenerate 서로 다른 페이지를 엽니다.

Visual Studio에서 기록 된 hello 이벤트의 개수를 표시 합니다.

![Visual Studio의 스크린샷. hello Application Insights 단추 디버깅 하는 동안 표시 됩니다.](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a>3단계: 원격 분석 확인
Visual Studio 또는 hello Application Insights 웹 포털에서 원격 분석을 볼 수 있습니다. 원격 분석 검색 toohelp Visual Studio에서에서 응용 프로그램을 디버깅할 합니다. 시스템은 라이브 때 성능과 hello 웹 포털에서 사용량을 모니터링 합니다. 

### <a name="see-your-telemetry-in-visual-studio"></a>Visual Studio에서 원격 분석 확인

Visual Studio에서 hello Application Insights 창을 엽니다. 두 번 클릭 hello **Application Insights** 단추를 선택 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하거나 **Application Insights**, 클릭 하 고 **라이브 원격 분석 검색**.

Hello Visual Studio Application Insights 검색 창에서 참조 hello **디버그 세션에서 데이터** hello 서버 쪽 응용 프로그램에서 생성 된 원격 분석에 대 한 보기입니다. Hello 필터와 모든 이벤트 toosee 자세히를 클릭 합니다.

![Hello 스크린샷 디버그 세션에서 데이터 hello Application Insights 창에서 봅니다.](./media/app-insights-asp-net/55.png)

> [!NOTE]
> 데이터가 보이지 않으면 hello 시간 범위 올바른지, 그리고 hello 검색 아이콘을 클릭 했는지 확인 합니다.

[Visual Studio의 Application Insights 도구에 대해 자세히 알아봅니다](app-insights-visual-studio.md).

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a>웹 포털에서 원격 분석 확인

(선택 하지 않은 경우 tooinstall만 hello SDK)에 hello Application Insights 웹 포털에서 원격 분석을 볼 수 있습니다. hello 포털에는 차트, 분석 도구 및 Visual Studio 보다 구성 요소 간 보기에 있습니다. 또한 hello 포털 경고를 제공합니다.

Application Insights 리소스를 엽니다. Toohello에 로그인 하거나 [Azure 포털](https://portal.azure.com/) , 또는 오른쪽 클릭 hello 프로젝트 Visual Studio에서 찾아 걸릴 수 있습니다.

![스크린 샷 Visual Studio의 tooopen Application Insights 포털 hello 하는 방법을 보여 주는](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> 액세스 오류가 발생 하는 경우: hello 잘못 된 집합을 사용 하 여 로그인 된 있으며 Microsoft 자격 증명을 둘 이상의 집합 있습니까? Hello 포털에서 로그 아웃 하 고 다시 로그인 합니다.

hello 포털의 응용 프로그램에서 hello 원격 분석 보기에서 열립니다.

![Application Insights 개요 페이지 스크린샷](./media/app-insights-asp-net/66.png)

Hello 포털에서 모든 타일 또는 차트 toosee 자세히 클릭 합니다.

[Application Insights를 사용 하 여 hello Azure 포털에에서 대 한 자세한](app-insights-dashboards.md)합니다.

## <a name="step-4-publish-your-app"></a>4단계: 앱 게시
응용 프로그램 tooyour IIS 서버 또는 tooAzure 게시 합니다. 조사식 [라이브 메트릭 스트림](app-insights-metrics-explorer.md#live-metrics-stream) toomake 모든 실행 되 고 있는지 원활 하 게 합니다.

원격 분석 hello Application Insights 포털에서 메트릭을 모니터링, 원격 분석을 검색 하 고 수 있는 설정 쌓이는 [대시보드](app-insights-dashboards.md)합니다. 사용할 수도 있습니다 hello 강력한 [로그 분석 쿼리 언어](https://docs.loganalytics.io/) tooanalyze 사용 현황 및 성능 또는 toofind 특정 이벤트입니다.

또한 계속 tooanalyze에서 원격 분석 [Visual Studio](app-insights-visual-studio.md), 진단 검색과 같은 도구로 및 [추세](app-insights-visual-studio-trends.md)합니다.

> [!NOTE]
> 응용 프로그램에 충분 한 원격 분석 tooapproach hello 보내는 경우 [조절 제한](app-insights-pricing.md#limits-summary)자동 [샘플링](app-insights-sampling.md) 전환 하는 합니다. 샘플링을 진단 용도로 상호 관련 된 데이터를 유지 하면서 응용 프로그램에서 보낸 원격 분석의 hello 수량을 줄입니다.
>
>

## <a name="land"></a> 모든 설정을 완료했습니다.

축하합니다. 응용 프로그램에서 hello Application Insights 패키지를 설치 하 고 toosend 원격 분석 toohello Application Insights 서비스가 Azure에서 구성 합니다.

![원격 분석의 이동 다이어그램](./media/app-insights-asp-net/01-scheme.png)

앱의 원격 분석을 수신 하는 Azure 리소스 hello로 식별 되는 *계측 키*합니다. Hello ApplicationInsights.config 파일의이 키를 찾을 수 있습니다.


## <a name="upgrade-toofuture-sdk-versions"></a>Toofuture SDK 버전 업그레이드
tooupgrade tooa [hello SDK의 새 릴리스](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases)개방형 hello **NuGet 패키지 관리자** 다시 및 설치 된 패키지에 대 한 필터입니다. **Microsoft.ApplicationInsights.Web**을 선택하고 **업그레이드**를 선택합니다.

모든 사용자 지정 tooApplicationInsights.config을 만든 경우 업그레이드 하기 전에 해당 복사본을 저장 합니다. Hello 새 버전에 변경 내용을 병합 합니다.

## <a name="video"></a>비디오

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>다음 단계

### <a name="more-telemetry"></a>추가 원격 분석

* **[브라우저 및 페이지 로드 데이터](app-insights-javascript.md)** - 웹 페이지에 코드 조각을 삽입합니다.
* **[더 자세한 종속성 및 예외 모니터링 가져오기](app-insights-monitor-performance-live-website-now.md)** - 서버에 상태 모니터를 설치합니다.
* **[사용자 지정 이벤트 코드](app-insights-api-custom-events-metrics.md)**  toocount, 시간, 또는 사용자 작업을 측정 합니다.
* **[로그 데이터 가져오기](app-insights-asp-net-trace-logs.md)** - 로그 데이터와 원격 분석 간에 상관 관계를 지정합니다.

### <a name="analysis"></a>분석

* **[Visual Studio Online에서 Application Insights로 작업](app-insights-visual-studio.md)**<br/>원격 분석을 사용 하 여 디버깅 하는 방법에 대 한 정보를 포함 진단 검색과 toocode 드릴스루 합니다.
* **[Hello Application Insights 포털 작업](app-insights-dashboards.md)**<br/> 대시보드, 강력한 진단 및 분석 도구, 경고, 응용 프로그램의 라이브 종속성 맵 및 원격 분석 내보내기에 대한 정보가 포함되어 있습니다.
* **[분석](app-insights-analytics-tour.md)**  -hello 강력한 쿼리 언어입니다.

### <a name="alerts"></a>경고

* [가용성 테스트](app-insights-monitor-web-app-availability.md): 테스트를 만들고 toomake 사이트 hello 웹에서 화면에 표시 합니다.
* [진단 스마트](app-insights-proactive-diagnostics.md): 이러한 테스트 자동으로 실행 되므로 없는 toodo 어느 것에 tooset를 구성 합니다. 앱이 실패한 요청으로 비정상적인 속도를 보일 경우 알려줍니다.
* [메트릭 경고](app-insights-alerts.md): 이러한 toowarn 설정 메트릭을 임계값을 초과할 경우 있습니다. 앱에 코딩하는 사용자 지정 메트릭에 이러한 경고를 설정할 수 있습니다.

### <a name="automation"></a>Automation

* [Application Insights 리소스 만들기 자동화](app-insights-powershell.md)

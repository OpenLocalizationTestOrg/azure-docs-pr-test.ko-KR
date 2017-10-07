---
title: "aaaMonitor 라이브 ASP.NET 웹 앱 Azure Application Insights로 | Microsoft Docs"
description: "다시 배포하지 않고 웹 사이트의 성능을 모니터링합니다. VM 또는 Azure의 온-프레미스에서 호스트되는 ASP.NET 웹앱으로 작업합니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 0d53f0a59974f40767fae681bafc4f358d1283a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a>Application Insights를 사용한 런타임 시 웹앱 계측


코드를 다시 배포 또는 toomodify 필요 없이 Azure Application insights는 라이브 웹 응용 프로그램을 계측할 수 있습니다. 앱이 온-프레미스 IIS 서버에서 호스트되는 경우 상태 모니터를 설치합니다. Azure VM에서 실행 하거나 Azure 웹 앱 당한, Application Insights 모니터링 hello Azure 제어판에서 전환할 수 있습니다. ([라이브 J2EE 웹앱](app-insights-java-live.md) 및 [Azure Cloud Services](app-insights-cloudservices.md)를 계측하는 방법을 설명하는 별도의 문서도 있습니다.) [Microsoft Azure](http://azure.com) 구독이 필요합니다.

![예제 차트](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

세 경로 tooapply Application Insights tooyour.NET 웹 응용 프로그램의 선택을 해야 합니다.

* **빌드 시간:** [Application Insights SDK 추가 hello] [ greenbrown] tooyour 웹 응용 프로그램 코드입니다.
* **실행 시간:** hello 서버에 웹 앱을 빌드하고 hello 코드를 다시 배포 하지 않고도 아래에 설명 된 대로 계측 합니다.
* **Both:** hello SDK 웹 응용 프로그램 코드를 빌드하고 hello 런타임 확장을 적용 합니다. 두 옵션의 최상의 hello를 가져옵니다.

다음은 각 루트의 장점을 요약한 것입니다.

|  | 빌드 시간 | 실행 시간 |
| --- | --- | --- |
| 요청 및 예외 |예 |예 |
| [자세한 예외 정보](app-insights-asp-net-exceptions.md) | |예 |
| [종속성 진단](app-insights-asp-net-dependencies.md) |.NET 4.6+, 간단히 |예, 전체 세부 정보: 결과 코드, SQL 명령 텍스트, HTTP 동사|
| [시스템 성능 카운터](app-insights-performance-counters.md) |예 |예 |
| [사용자 지정 원격 분석에 대 한 API][api] |예 |아니요 |
| [추적 로그 통합](app-insights-asp-net-trace-logs.md) |예 |아니요 |
| [페이지 보기 및 사용자 데이터](app-insights-javascript.md) |예 |아니요 |
| Toorebuild 코드가 필요 |예 | 아니요 |


## <a name="monitor-a-live-azure-web-app"></a>라이브 Azure 웹앱 모니터링

Azure 웹 서비스로, 여기의 응용 프로그램을 실행 하는 경우 어떻게 tooswitch 모니터링:

* Azure의 hello 응용 프로그램의 제어판에서 Application Insights를 선택 합니다.

    ![Azure 웹앱의 Application Insights 설정](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* Hello Application Insights에 대 한 요약 페이지를 열면 hello 아래쪽 tooopen hello 전체 Application Insights 리소스에 대 한 hello 링크를 클릭 합니다.

    ![Insights tooApplication 클릭 하 여](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

[클라우드 및 VM 앱 모니터링](app-insights-azure.md).

### <a name="enable-client-side-monitoring-in-azure"></a>Azure에서 클라이언트 쪽 모니터링 사용

Azure에서 Application Insights를 사용하도록 설정한 경우 페이지 보기 및 사용자 원격 분석을 추가할 수 있습니다.

1. 설정 > 응용 프로그램 설정 선택
2.  앱 설정 아래에서 새로운 키 값 쌍을 추가합니다. 
   
    키: `APPINSIGHTS_JAVASCRIPT_ENABLED` 
    
    값: `true`
3. **저장** 설정 hello 및 **다시 시작** 앱.

hello Application Insights JavaScript SDK는 이제 각 웹 페이지에 삽입 됩니다.

## <a name="monitor-a-live-iis-web-app"></a>라이브 IIS 웹앱 모니터링

IIS 서버에서 앱이 호스트되는 경우 상태 모니터를 사용하여 Application Insights를 사용하도록 설정합니다.

1. IIS 웹 서버에서 관리자 자격 증명으로 로그인합니다.
2. Application Insights 상태 모니터 아직 설치 되지 않은 경우 다운로드 하 고 hello 실행 [상태 모니터 설치 관리자](http://go.microsoft.com/fwlink/?LinkId=506648) (실행 또는 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx) 에 응용 프로그램 통찰력 상태에 대 한 검색 모니터)입니다.
3. 상태 모니터에서 설치 하는 hello 웹 응용 프로그램 또는 toomonitor 되도록 웹 사이트를 선택 합니다. Azure 자격 증명으로 로그인합니다.

    Hello Application Insights 포털에서 toosee hello 결과 원하는 hello 리소스를 구성 합니다. (일반적으로 것은 최상의 toocreate 새 리소스입니다. 이 앱에 대해 [웹 테스트][availability] 또는 [클라이언트 모니터링][client]이 이미 있으면 기존 리소스를 선택합니다.) 

    ![앱과 리소스를 선택합니다.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. IIS를 다시 시작합니다.

    ![Hello 위쪽 hello 대화에 대 한 다시 시작을 선택 합니다.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    웹 서비스가 잠시 중단됩니다.

## <a name="customize-monitoring-options"></a>모니터링 옵션 사용자 지정

Application Insights를 사용 하면 Dll 및 ApplicationInsights.config 추가 tooyour 웹 앱입니다. 있습니다 수 [hello.config 파일을 편집](app-insights-configuration-with-applicationinsights-config.md) toochange hello 옵션 중 일부입니다.

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a>앱을 다시 게시할 때 Application Insights 다시 활성화

응용 프로그램을 다시 게시 하기 전에 고려해 야 [Visual Studio에서 Application Insights toohello 코드를 추가][greenbrown]합니다. 더 자세한 원격 분석 및 hello 기능 toowrite 사용자 지정 원격 분석을 얻을 수 있습니다.

Toore 하려는 경우-Application Insights toohello 코드를 추가 하지 않고 게시 hello 배포 프로세스는 hello Dll을 삭제할 수 있습니다 및 웹 사이트를 게시 하는 hello에서 ApplicationInsights.config 점에 유의 하세요. 따라서

1. ApplicationInsights.config를 편집한 경우 앱을 다시 게시하기 전에 복사본을 만듭니다.
2. 앱을 다시 게시합니다.
3. Application Insights 모니터링을 다시 활성화합니다. (적절 한 방법을 hello 사용: hello Azure 웹 앱 제어판 또는 IIS 호스트에 hello 상태 모니터입니다.)
4. Hello.config 파일에서 수행 된 모든 편집을 다시 시작 합니다.


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a>Application Insights의 런타임 구성 문제 해결

### <a name="cant-connect-no-telemetry"></a>연결할 수 없나요? 원격 분석이 없나요?

* 열기 [필요한 송신 포트를 hello](app-insights-ip-addresses.md#outgoing-ports) 서버의 방화벽 tooallow 상태 모니터 toowork에 있습니다.

* 상태 모니터를 열고 왼쪽 창에서 응용 프로그램을 선택합니다. Hello "구성 알림" 섹션에서에서이 응용 프로그램에 대 한 모든 진단 메시지가 있는지 확인 합니다.

  ![Hello 성능 블레이드 toosee 요청, 응답 시간, 종속성 및 기타 데이터 열](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* Hello 서버에서 "부족 한 사용 권한"에 대 한 메시지를 표시 하는 경우 hello 다음을 보십시오.
  * IIS 관리자에서 응용 프로그램 풀 선택 열고 **고급 설정**, 아래에서 **프로세스 모델** hello id에 주의 합니다.
  * 컴퓨터 관리 제어판에서이 identity toohello 성능 모니터 사용자 그룹을 추가 합니다.
* 서버에 MMA/SCOM(Systems Center Operations Manager)이 설치된 경우 일부 버전이 충돌할 수 있습니다. SCOM와 상태 모니터를 제거 하 고 다시 hello 최신 버전을 설치 합니다.
* [문제 해결][qna]을 참조하세요.

## <a name="system-requirements"></a>시스템 요구 사항
Server에서 Application Insights 상태 모니터에 대한 OS 지원:

* Windows Server 2008
* Windows Server 2008 R2
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

최신 SP 및 .NET Framework 4.5 포함

Hello 클라이언트 쪽에서:.NET Framework 4.5를 사용 하 여 다시 Windows 7, 8, 8.1 및 10

IIS 지원: IIS 7, 7.5, 8, 8.5(IIS 필요)

## <a name="automation-with-powershell"></a>PowerShell을 사용한 자동화
IIS 서버에서 PowerShell을 사용하여 모니터링을 시작하고 중지할 수 있습니다.

먼저 hello Application Insights 모듈을 가져옵니다.

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

어떤 앱을 모니터링 중인지 확인합니다.

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* `-Name`웹 응용 프로그램의 이름 (선택 사항) hello입니다.
* 이 IIS 서버에 있는 각 웹 응용 프로그램 (또는 hello 라는 응용 프로그램)에 대 한 Application Insights 모니터링 상태를 hello 하는 표시 됩니다.
* 각 앱에 대해 `ApplicationInsightsApplication`을(를) 반환합니다.

  * `SdkState==EnabledAfterDeployment`: 앱 모니터링 되 고 hello 상태 모니터 도구 또는 런타임 시 계측 된 `Start-ApplicationInsightsMonitoring`합니다.
  * `SdkState==Disabled`: hello 앱에 대 한 Application Insights 계측 되지 않습니다. 계측 되지 된 또는 실행 시간 모니터링을 사용할 수 없습니다와 hello 상태 모니터 도구와 `Stop-ApplicationInsightsMonitoring`합니다.
  * `SdkState==EnabledByCodeInstrumentation`: hello 앱 hello SDK toohello 소스 코드를 추가 하 여 계측 되었습니다. 해당 SDK은 업데이트되거나 중지될 수 없습니다.
  * `SdkVersion`이 응용 프로그램 모니터링에 사용 중인 hello 버전을 보여 줍니다.
  * `LatestAvailableSdkVersion`hello NuGet 갤러리에서 현재 사용할 수 있는 hello 버전을 표시 합니다. tooupgrade hello 응용 프로그램 toothis 버전을 사용 하 여 `Update-ApplicationInsightsMonitoring`합니다.

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* `-Name`IIS에서 hello 앱의 hello 이름
* `-InstrumentationKey`Application Insights 리소스를 표시 하는 hello 결과 toobe 저장할 hello의 ikey를 hello 합니다.
* 이 cmdlet은 아직 계측되지 않은 앱에만 영향을 줍니다. 즉, SdkState==NotInstrumented입니다.

    hello cmdlet은 이미 계측 하는 응용 프로그램에 영향을 주지 않습니다. Hello SDK toohello 코드를 추가 하 여 빌드 시 hello 응용 프로그램 계측 된 여부는 중요 하거나에서이 cmdlet 사용 하 여 시간을 실행 하지 않습니다.

    hello SDK 사용 되는 버전 tooinstrument hello 앱 가장 최근에 hello 버전 다운로드 toothis 서버입니다.

    toodownload hello 최신 버전으로 업데이트 ApplicationInsightsVersion 사용 합니다.
* 성공 시 `ApplicationInsightsApplication`을(를) 반환합니다. 실패 한 경우 추적 toostderr을 기록 합니다.

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* `-Name`IIS에서 응용 프로그램의 hello 이름
* `-All` `SdkState==EnabledAfterDeployment`인 이 IIS 서버에서 모든 앱에 대한 모니터링을 중지합니다.
* 앱을 지정 하 고 계측을 제거 하는 hello 모니터링을 중지 합니다. 또한 런타임에 사용 하 여 계측 된 응용 프로그램 상태 모니터링 도구 또는 시작 ApplicationInsightsApplication hello에 대 한 에서만 작동 합니다. (`SdkState==EnabledAfterDeployment`)
* ApplicationInsightsApplication을 반환합니다.

`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]

* `-Name`: IIS의 웹 앱의 hello 이름입니다.
* `-InstrumentationKey`(옵션) 사용이이 toochange hello 리소스 toowhich hello 앱의 원격이 분석 전송 됩니다.
* 이 cmdlet은:
  * 가장 최근에 업그레이드 hello 앱 toohello 버전의 SDK hello 라는 toothis 컴퓨터를 다운로드 합니다. (`SdkState==EnabledAfterDeployment`인 경우에만 작동)
  * 계측 키를 제공 하는 경우 hello 라는 응용 프로그램은 해당 키가 있는 toosend 다시 구성 된 원격 분석 toohello 리소스입니다. ( `SdkState != Disabled`인 경우 작동)

`Update-ApplicationInsightsVersion`

* Hello 최신 Application Insights SDK toohello 서버를 다운로드합니다.

## <a name="questions"></a>상태 모니터에 대한 질문

### <a name="what-is-status-monitor"></a>상태 모니터란?

IIS 웹 서버에 설치한 데스크톱 응용 프로그램입니다. 웹앱을 계측하고 구성하는 데 도움이 됩니다. 

### <a name="when-do-i-use-status-monitor"></a>언제 상태 모니터를 사용하나요?

* 이미 실행 중인 경우에 모든 웹 앱-IIS 서버에서 실행 되는 tooinstrument 합니다.
* 웹 앱에 대 한 추가 원격 분석 tooenable [hello Application Insights SDK를 사용 하 여 빌드한](app-insights-asp-net.md) 컴파일 타임에 있습니다. 

### <a name="can-i-close-it-after-it-runs"></a>실행한 후에 닫을 수 있나요?

예. Hello 웹 사이트를 선택 하면 계측에 그 후에이 닫을 수 있습니다.

자체로 원격 분석을 수집하지 않습니다. 방금 hello 웹 응용 프로그램을 구성 하 고 일부 사용 권한을 설정 합니다.

### <a name="what-does-status-monitor-do"></a>상태 모니터의 기능은 무엇인가요?

상태 모니터 tooinstrument에 대 한 웹 앱 선택:

* 다운로드 하 고 hello Application Insights 어셈블리와.config 파일 hello 웹 응용 프로그램의 이진 파일 폴더에 배치 합니다.
* 수정 `web.config` tooadd hello 응용 프로그램 통찰력 HTTP 추적 모듈입니다.
* CLR toocollect 종속성 호출을 프로 파일링을 사용 하도록 설정 합니다.

### <a name="do-i-need-toorun-status-monitor-whenever-i-update-hello-app"></a>Hello 앱을 업데이트 하려면 때마다 toorun 상태 모니터 필요 합니까?

증분 방식으로 다시 배포하는 경우에는 아닙니다. 

프로세스를 게시 hello에서 hello '기존 파일을 삭제 합니다.' 옵션을 선택 하는 경우, toore 실행 상태 모니터 tooconfigure Application Insights 해야 합니다.

### <a name="what-telemetry-is-collected"></a>어떤 원격 분석이 수집되나요?

상태 모니터를 사용하여 런타임 시에만 계측하는 응용 프로그램의 경우:

* HTTP 요청
* Toodependencies 호출
* 예외
* 성능 카운터

컴파일 시 이미 계측된 응용 프로그램의 경우:

 * 프로세스 카운터
 * 종속성 호출(.NET 4.5); 종속성 호출(.NET 4.6)에 값을 반환합니다.
 * 예외 스택 추적 값

[자세히 알아보기](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a>비디오

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next"></a>다음 단계

원격 분석 보기:

* [메트릭을 탐색](app-insights-metrics-explorer.md) toomonitor 성능 및 사용
* [이벤트 및 로그를 검색할] [ diagnostic] toodiagnose 문제
* [분석](app-insights-analytics.md)을 통해 고급 쿼리를 수행합니다.
* [대시보드를 만듭니다](app-insights-dashboards.md).

원격 분석 더 추가:

* [웹 테스트를 만들] [ availability] toomake 사이트 라이브 유지 합니다.
* [웹 클라이언트 원격 분석 추가] [ usage] 웹 페이지 코드를 삽입 하면 toolet toosee 예외 호출을 추적 합니다.
* [Application Insights SDK tooyour 코드를 추가] [ greenbrown] 추적을 삽입 하 고 호출을 로깅할 수 있도록

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md

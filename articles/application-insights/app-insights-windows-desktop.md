---
title: "aaaMonitoring 사용량 및 Windows 데스크톱 앱에 대 한 성능"
description: "HockeyApp 및 Application Insights를 사용하여 Windows 데스크톱 앱의 사용량 및 성능을 분석합니다."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 19040746-3315-47e7-8c60-4b3000d2ddc4
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/26/2016
ms.author: bwren
ms.openlocfilehash: 73806885a6f0ed3896c0e43308c90ba087007887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a>Windows 데스크톱 앱에서 사용량 및 성능 모니터링


[Azure Application Insights](app-insights-overview.md) 및 [HockeyApp](https://hockeyapp.net)를 사용하면 배포된 응용 프로그램의 사용량 및 성능을 모니터링할 수 있습니다.

> [!IMPORTANT]
> 권장 [HockeyApp](https://hockeyapp.net) toodistribute 및 모니터에서 사용 하는 데스크톱 및 장치 앱. HockeyApp를 사용하면 사용량 및 충돌 보고서를 모니터링할 수 있을 뿐만 아니라 배포, 라이브 테스트 및 사용자 의견을 관리할 수 있습니다. 또한 [분석으로 원격 분석을 내보내고 쿼리](app-insights-hockeyapp-bridge-app.md)할 수 있습니다.
> 
> 도 있지만 원격 분석은 데스크톱 응용 프로그램에서 tooApplication Insights 보낼 수 있습니다,이 주로 실험적 및 디버깅 목적으로 유용 합니다.
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a>Windows 응용 프로그램에서 원격 분석 tooApplication toosend Insights
1. Hello에 [Azure 포털](https://portal.azure.com), [Application Insights 리소스 만들기](app-insights-create-new-resource.md)합니다. 응용 프로그램 유형으로 ASP.NET 앱을 선택합니다.
2. Hello 계측 키의 복사본을 수행 합니다. Hello 키 hello Essentials 드롭 다운 방금 만든 hello 새 리소스를 찾을 합니다. 
3. Visual Studio에서 응용 프로그램 프로젝트의 hello NuGet 패키지를 편집 하 고 Microsoft.ApplicationInsights.WindowsServer를 추가 합니다. (또는 원한다 면 hello 표준 원격 분석 컬렉션 모듈 없이 완전 API hello Microsoft.ApplicationInsights를 선택 합니다.)
4. 사용자 코드에서 hello 계측 키를 설정 합니다.
   
    `TelemetryConfiguration.Active.InstrumentationKey = "` *키* `";` 
   
    또는 ApplicationInsights.config (설치한 hello 표준 원격 분석 패키지 중 하나) 하는 경우:
   
    `<InstrumentationKey>`*키*`</InstrumentationKey>` 
   
    ApplicationInsights.config를 사용 하는 경우 솔루션 탐색기에서 해당 속성을 너무 설정 되어 있는지 확인**빌드 작업 콘텐츠를 복사 tooOutput 디렉터리 = = 복사**합니다.
5. [Hello API를 사용 하 여](app-insights-api-custom-events-metrics.md) toosend 원격 분석 합니다.
6. 응용 프로그램을 실행 하 고 hello Azure 포털에서에서 만든 hello 리소스의 hello 원격 분석을 참조 하십시오.

## <a name="telemetry"></a>예제 코드
```C#

    public partial class Form1 : Form
    {
        private TelemetryClient tc = new TelemetryClient();
        ...
        private void Form1_Load(object sender, EventArgs e)
        {
            // Alternative toosetting ikey in config file:
            tc.InstrumentationKey = "key copied from portal";

            // Set session data:
            tc.Context.User.Id = Environment.UserName;
            tc.Context.Session.Id = Guid.NewGuid().ToString();
            tc.Context.Device.OperatingSystem = Environment.OSVersion.ToString();

            // Log a page view:
            tc.TrackPageView("Form1");
            ...
        }

        protected override void OnClosing(CancelEventArgs e)
        {
            stop = true;
            if (tc != null)
            {
                tc.Flush(); // only for desktop apps

                // Allow time for flushing:
                System.Threading.Thread.Sleep(1000);
            }
            base.OnClosing(e);
        }

```

## <a name="next-steps"></a>다음 단계
* [대시보드 만들기](app-insights-dashboards.md)
* [진단 검색](app-insights-diagnostic-search.md)
* [메트릭 탐색](app-insights-metrics-explorer.md)
* [분석 쿼리 작성](app-insights-analytics.md)


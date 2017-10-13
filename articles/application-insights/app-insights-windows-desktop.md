---
title: "Windows 데스크톱 앱의 사용량 및 성능 모니터링"
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
ms.openlocfilehash: 9d7e2a390adf10cbf5d88dd0084ce09136987309
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a>Windows 데스크톱 앱에서 사용량 및 성능 모니터링


[Azure Application Insights](app-insights-overview.md) 및 [HockeyApp](https://hockeyapp.net)를 사용하면 배포된 응용 프로그램의 사용량 및 성능을 모니터링할 수 있습니다.

> [!IMPORTANT]
> 데스크톱 및 장치 앱을 배포하고 모니터링하는 데 [HockeyApp](https://hockeyapp.net) 을 권장합니다. HockeyApp를 사용하면 사용량 및 충돌 보고서를 모니터링할 수 있을 뿐만 아니라 배포, 라이브 테스트 및 사용자 의견을 관리할 수 있습니다. 또한 [분석으로 원격 분석을 내보내고 쿼리](app-insights-hockeyapp-bridge-app.md)할 수 있습니다.
> 
> 데스크톱 응용 프로그램에서 Application Insights에 원격 분석을 보낼 수 있지만 주로 디버깅 및 실험 목적에 유용합니다.
> 
> 

## <a name="to-send-telemetry-to-application-insights-from-a-windows-application"></a>Windows 응용 프로그램에서 Application Insights에 원격 분석을 전송하려면
1. [Azure Portal](https://portal.azure.com)에서 [Application Insights 리소스를 만듭니다](app-insights-create-new-resource.md). 응용 프로그램 유형으로 ASP.NET 앱을 선택합니다.
2. 계측 키를 복사합니다. 방금 만든 새 리소스의 필수 드롭다운에서 키를 찾습니다. 
3. Visual Studio에서 앱 프로젝트의 NuGet 패키지를 편집하고 Microsoft.ApplicationInsights.WindowsServer를 추가합니다. (또는 표준 원격 분석 수집 모듈 없이 API를 사용하려면 Microsoft.ApplicationInsights를 선택합니다.)
4. 코드에서 계측 키를 설정합니다.
   
    `TelemetryConfiguration.Active.InstrumentationKey = "` *키* `";` 
   
    또는 ApplicationInsights.config에서(표준 원격 분석 패키지 중 하나를 설치한 경우).
   
    `<InstrumentationKey>`*키*`</InstrumentationKey>` 
   
    ApplicationInsights.config를 사용하는 경우 솔루션 탐색기에서 해당 속성이 **빌드 작업 = 콘텐츠, 출력 디렉터리로 복사 = 복사**로 설정되도록 합니다.
5. [API를 사용](app-insights-api-custom-events-metrics.md) 하여 원격 분석을 전송합니다.
6. 앱을 실행하고 Azure 포털에서 만든 리소스의 원격 분석을 참조하세요.

## <a name="telemetry"></a>예제 코드
```C#

    public partial class Form1 : Form
    {
        private TelemetryClient tc = new TelemetryClient();
        ...
        private void Form1_Load(object sender, EventArgs e)
        {
            // Alternative to setting ikey in config file:
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


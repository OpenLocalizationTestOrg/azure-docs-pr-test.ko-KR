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
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a><span data-ttu-id="8da69-103">Windows 데스크톱 앱에서 사용량 및 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="8da69-103">Monitoring usage and performance in Windows Desktop apps</span></span>


<span data-ttu-id="8da69-104">[Azure Application Insights](app-insights-overview.md) 및 [HockeyApp](https://hockeyapp.net)를 사용하면 배포된 응용 프로그램의 사용량 및 성능을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8da69-104">[Azure Application Insights](app-insights-overview.md) and [HockeyApp](https://hockeyapp.net) let you monitor your deployed application for usage and performance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8da69-105">데스크톱 및 장치 앱을 배포하고 모니터링하는 데 [HockeyApp](https://hockeyapp.net) 을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="8da69-105">We recommend [HockeyApp](https://hockeyapp.net) to distribute and monitor desktop and device apps.</span></span> <span data-ttu-id="8da69-106">HockeyApp를 사용하면 사용량 및 충돌 보고서를 모니터링할 수 있을 뿐만 아니라 배포, 라이브 테스트 및 사용자 의견을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8da69-106">With HockeyApp, you can manage distribution, live testing, and user feedback, as well as monitor usage and crash reports.</span></span> <span data-ttu-id="8da69-107">또한 [분석으로 원격 분석을 내보내고 쿼리](app-insights-hockeyapp-bridge-app.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8da69-107">You can also [export and query your telemetry with Analytics](app-insights-hockeyapp-bridge-app.md).</span></span>
> 
> <span data-ttu-id="8da69-108">데스크톱 응용 프로그램에서 Application Insights에 원격 분석을 보낼 수 있지만 주로 디버깅 및 실험 목적에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="8da69-108">Although telemetry can be sent to Application Insights from a desktop application, this is chiefly useful for debugging and experimental purposes.</span></span>
> 
> 

## <a name="to-send-telemetry-to-application-insights-from-a-windows-application"></a><span data-ttu-id="8da69-109">Windows 응용 프로그램에서 Application Insights에 원격 분석을 전송하려면</span><span class="sxs-lookup"><span data-stu-id="8da69-109">To send telemetry to Application Insights from a Windows application</span></span>
1. <span data-ttu-id="8da69-110">[Azure Portal](https://portal.azure.com)에서 [Application Insights 리소스를 만듭니다](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="8da69-110">In the [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="8da69-111">응용 프로그램 유형으로 ASP.NET 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8da69-111">For application type, choose ASP.NET app.</span></span>
2. <span data-ttu-id="8da69-112">계측 키를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8da69-112">Take a copy of the Instrumentation Key.</span></span> <span data-ttu-id="8da69-113">방금 만든 새 리소스의 필수 드롭다운에서 키를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8da69-113">Find the key in the Essentials drop-down of the new resource you just created.</span></span> 
3. <span data-ttu-id="8da69-114">Visual Studio에서 앱 프로젝트의 NuGet 패키지를 편집하고 Microsoft.ApplicationInsights.WindowsServer를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8da69-114">In Visual Studio, edit the NuGet packages of your app project, and add Microsoft.ApplicationInsights.WindowsServer.</span></span> <span data-ttu-id="8da69-115">(또는 표준 원격 분석 수집 모듈 없이 API를 사용하려면 Microsoft.ApplicationInsights를 선택합니다.)</span><span class="sxs-lookup"><span data-stu-id="8da69-115">(Or choose Microsoft.ApplicationInsights if you just want the bare API, without the standard telemetry collection modules.)</span></span>
4. <span data-ttu-id="8da69-116">코드에서 계측 키를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8da69-116">Set the instrumentation key either in your code:</span></span>
   
    <span data-ttu-id="8da69-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *키* `";`</span><span class="sxs-lookup"><span data-stu-id="8da69-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
   
    <span data-ttu-id="8da69-118">또는 ApplicationInsights.config에서(표준 원격 분석 패키지 중 하나를 설치한 경우).</span><span class="sxs-lookup"><span data-stu-id="8da69-118">or in ApplicationInsights.config (if you installed one of the standard telemetry packages):</span></span>
   
    <span data-ttu-id="8da69-119">`<InstrumentationKey>`*키*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="8da69-119">`<InstrumentationKey>`*your key*`</InstrumentationKey>`</span></span> 
   
    <span data-ttu-id="8da69-120">ApplicationInsights.config를 사용하는 경우 솔루션 탐색기에서 해당 속성이 **빌드 작업 = 콘텐츠, 출력 디렉터리로 복사 = 복사**로 설정되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8da69-120">If you use ApplicationInsights.config, make sure its properties in Solution Explorer are set to **Build Action = Content, Copy to Output Directory = Copy**.</span></span>
5. <span data-ttu-id="8da69-121">[API를 사용](app-insights-api-custom-events-metrics.md) 하여 원격 분석을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="8da69-121">[Use the API](app-insights-api-custom-events-metrics.md) to send telemetry.</span></span>
6. <span data-ttu-id="8da69-122">앱을 실행하고 Azure 포털에서 만든 리소스의 원격 분석을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8da69-122">Run your app, and see the telemetry in the resource you created in the Azure Portal.</span></span>

## <span data-ttu-id="8da69-123"><a name="telemetry"></a>예제 코드</span><span class="sxs-lookup"><span data-stu-id="8da69-123"><a name="telemetry"></a>Example code</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="8da69-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8da69-124">Next steps</span></span>
* [<span data-ttu-id="8da69-125">대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="8da69-125">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="8da69-126">진단 검색</span><span class="sxs-lookup"><span data-stu-id="8da69-126">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="8da69-127">메트릭 탐색</span><span class="sxs-lookup"><span data-stu-id="8da69-127">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="8da69-128">분석 쿼리 작성</span><span class="sxs-lookup"><span data-stu-id="8da69-128">Write Analytics queries</span></span>](app-insights-analytics.md)


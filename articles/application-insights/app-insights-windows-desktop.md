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
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a><span data-ttu-id="725c4-103">Windows 데스크톱 앱에서 사용량 및 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="725c4-103">Monitoring usage and performance in Windows Desktop apps</span></span>


<span data-ttu-id="725c4-104">[Azure Application Insights](app-insights-overview.md) 및 [HockeyApp](https://hockeyapp.net)를 사용하면 배포된 응용 프로그램의 사용량 및 성능을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="725c4-104">[Azure Application Insights](app-insights-overview.md) and [HockeyApp](https://hockeyapp.net) let you monitor your deployed application for usage and performance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="725c4-105">권장 [HockeyApp](https://hockeyapp.net) toodistribute 및 모니터에서 사용 하는 데스크톱 및 장치 앱.</span><span class="sxs-lookup"><span data-stu-id="725c4-105">We recommend [HockeyApp](https://hockeyapp.net) toodistribute and monitor desktop and device apps.</span></span> <span data-ttu-id="725c4-106">HockeyApp를 사용하면 사용량 및 충돌 보고서를 모니터링할 수 있을 뿐만 아니라 배포, 라이브 테스트 및 사용자 의견을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="725c4-106">With HockeyApp, you can manage distribution, live testing, and user feedback, as well as monitor usage and crash reports.</span></span> <span data-ttu-id="725c4-107">또한 [분석으로 원격 분석을 내보내고 쿼리](app-insights-hockeyapp-bridge-app.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="725c4-107">You can also [export and query your telemetry with Analytics](app-insights-hockeyapp-bridge-app.md).</span></span>
> 
> <span data-ttu-id="725c4-108">도 있지만 원격 분석은 데스크톱 응용 프로그램에서 tooApplication Insights 보낼 수 있습니다,이 주로 실험적 및 디버깅 목적으로 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="725c4-108">Although telemetry can be sent tooApplication Insights from a desktop application, this is chiefly useful for debugging and experimental purposes.</span></span>
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a><span data-ttu-id="725c4-109">Windows 응용 프로그램에서 원격 분석 tooApplication toosend Insights</span><span class="sxs-lookup"><span data-stu-id="725c4-109">toosend telemetry tooApplication Insights from a Windows application</span></span>
1. <span data-ttu-id="725c4-110">Hello에 [Azure 포털](https://portal.azure.com), [Application Insights 리소스 만들기](app-insights-create-new-resource.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="725c4-110">In hello [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="725c4-111">응용 프로그램 유형으로 ASP.NET 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="725c4-111">For application type, choose ASP.NET app.</span></span>
2. <span data-ttu-id="725c4-112">Hello 계측 키의 복사본을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="725c4-112">Take a copy of hello Instrumentation Key.</span></span> <span data-ttu-id="725c4-113">Hello 키 hello Essentials 드롭 다운 방금 만든 hello 새 리소스를 찾을 합니다.</span><span class="sxs-lookup"><span data-stu-id="725c4-113">Find hello key in hello Essentials drop-down of hello new resource you just created.</span></span> 
3. <span data-ttu-id="725c4-114">Visual Studio에서 응용 프로그램 프로젝트의 hello NuGet 패키지를 편집 하 고 Microsoft.ApplicationInsights.WindowsServer를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="725c4-114">In Visual Studio, edit hello NuGet packages of your app project, and add Microsoft.ApplicationInsights.WindowsServer.</span></span> <span data-ttu-id="725c4-115">(또는 원한다 면 hello 표준 원격 분석 컬렉션 모듈 없이 완전 API hello Microsoft.ApplicationInsights를 선택 합니다.)</span><span class="sxs-lookup"><span data-stu-id="725c4-115">(Or choose Microsoft.ApplicationInsights if you just want hello bare API, without hello standard telemetry collection modules.)</span></span>
4. <span data-ttu-id="725c4-116">사용자 코드에서 hello 계측 키를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="725c4-116">Set hello instrumentation key either in your code:</span></span>
   
    <span data-ttu-id="725c4-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *키* `";`</span><span class="sxs-lookup"><span data-stu-id="725c4-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
   
    <span data-ttu-id="725c4-118">또는 ApplicationInsights.config (설치한 hello 표준 원격 분석 패키지 중 하나) 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="725c4-118">or in ApplicationInsights.config (if you installed one of hello standard telemetry packages):</span></span>
   
    <span data-ttu-id="725c4-119">`<InstrumentationKey>`*키*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="725c4-119">`<InstrumentationKey>`*your key*`</InstrumentationKey>`</span></span> 
   
    <span data-ttu-id="725c4-120">ApplicationInsights.config를 사용 하는 경우 솔루션 탐색기에서 해당 속성을 너무 설정 되어 있는지 확인**빌드 작업 콘텐츠를 복사 tooOutput 디렉터리 = = 복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="725c4-120">If you use ApplicationInsights.config, make sure its properties in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>
5. <span data-ttu-id="725c4-121">[Hello API를 사용 하 여](app-insights-api-custom-events-metrics.md) toosend 원격 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="725c4-121">[Use hello API](app-insights-api-custom-events-metrics.md) toosend telemetry.</span></span>
6. <span data-ttu-id="725c4-122">응용 프로그램을 실행 하 고 hello Azure 포털에서에서 만든 hello 리소스의 hello 원격 분석을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="725c4-122">Run your app, and see hello telemetry in hello resource you created in hello Azure Portal.</span></span>

## <span data-ttu-id="725c4-123"><a name="telemetry"></a>예제 코드</span><span class="sxs-lookup"><span data-stu-id="725c4-123"><a name="telemetry"></a>Example code</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="725c4-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="725c4-124">Next steps</span></span>
* [<span data-ttu-id="725c4-125">대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="725c4-125">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="725c4-126">진단 검색</span><span class="sxs-lookup"><span data-stu-id="725c4-126">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="725c4-127">메트릭 탐색</span><span class="sxs-lookup"><span data-stu-id="725c4-127">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="725c4-128">분석 쿼리 작성</span><span class="sxs-lookup"><span data-stu-id="725c4-128">Write Analytics queries</span></span>](app-insights-analytics.md)


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
# <a name="set-up-application-insights-for-your-aspnet-website"></a><span data-ttu-id="0834e-103">ASP.NET 웹 사이트용 Application Insights 설정</span><span class="sxs-lookup"><span data-stu-id="0834e-103">Set up Application Insights for your ASP.NET website</span></span>

<span data-ttu-id="0834e-104">이 절차에서는 ASP.NET 웹 응용 프로그램 toosend 원격 분석 toohello 구성 [Azure Application Insights](app-insights-overview.md) 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-104">This procedure configures your ASP.NET web app toosend telemetry toohello [Azure Application Insights](app-insights-overview.md) service.</span></span> <span data-ttu-id="0834e-105">Hello 클라우드 또는 사용자 고유의 IIS 서버에 호스트 되는 ASP.NET 응용 프로그램에 대 한 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-105">It works for ASP.NET apps that are hosted either in your own IIS server or in hello Cloud.</span></span> <span data-ttu-id="0834e-106">차트를 얻게 하 고 응용 프로그램의 성능을 hello 및 사용 되는 방식을 추가 자동 경고 성능 문제 또는 오류에을 이해 하는 데 도움이 되는 강력한 쿼리 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-106">You get charts and a powerful query language that help you understand hello performance of your app and how people are using it, plus automatic alerts on failures or performance issues.</span></span> <span data-ttu-id="0834e-107">많은 개발자 들이 이러한 기능 훌륭한는 것만 확장 하 고 하는 경우 hello 원격 분석을 사용자 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-107">Many developers find these features great as they are, but you can also extend and customize hello telemetry if you need to.</span></span>

<span data-ttu-id="0834e-108">Visual Studio에서 설치 프로그램을 몇 번만 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-108">Setup takes just a few clicks in Visual Studio.</span></span> <span data-ttu-id="0834e-109">원격 분석의 hello 볼륨을 제한 하 여 hello 옵션 tooavoid 요금 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-109">You have hello option tooavoid charges by limiting hello volume of telemetry.</span></span> <span data-ttu-id="0834e-110">이렇게 하면 tooexperiment 및 디버그 또는 toomonitor 하지 많은 사용자가 사용 하는 사이트 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-110">This allows you tooexperiment and debug, or toomonitor a site with not many users.</span></span> <span data-ttu-id="0834e-111">프로덕션 사이트를 모니터링 하 고 계속 toogo 원하는 결정할 때 쉽게 tooraise hello 제한 나중에 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-111">When you decide you want toogo ahead and monitor your production site, it's easy tooraise hello limit later.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="0834e-112">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="0834e-112">Before you start</span></span>
<span data-ttu-id="0834e-113">다음 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-113">You need:</span></span>

* <span data-ttu-id="0834e-114">Visual Studio 2013 업데이트 3 이상</span><span class="sxs-lookup"><span data-stu-id="0834e-114">Visual Studio 2013 update 3 or later.</span></span> <span data-ttu-id="0834e-115">나중일수록 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-115">Later is better.</span></span>
* <span data-ttu-id="0834e-116">구독 너무[Microsoft Azure](http://azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-116">A subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="0834e-117">팀 또는 조직에 Azure 구독이 있으면 hello 소유자 추가할 수 있습니다 tooit를 사용 하 여 프로그램 [Microsoft 계정](http://live.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-117">If your team or organization has an Azure subscription, hello owner can add you tooit, by using your [Microsoft account](http://live.com).</span></span>

<span data-ttu-id="0834e-118">에 관심이 있는 경우에 대체 항목 toolook이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-118">There are alternative topics toolook at if you are interested in:</span></span>

* [<span data-ttu-id="0834e-119">런타임 시 웹앱 계측</span><span class="sxs-lookup"><span data-stu-id="0834e-119">Instrumenting a web app at runtime</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="0834e-120">Azure 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="0834e-120">Azure Cloud Services</span></span>](app-insights-cloudservices.md)

## <span data-ttu-id="0834e-121"><a name="ide"></a>1 단계: hello Application Insights SDK 추가</span><span class="sxs-lookup"><span data-stu-id="0834e-121"><a name="ide"></a> Step 1: Add hello Application Insights SDK</span></span>

<span data-ttu-id="0834e-122">[솔루션 탐색기]에서 웹앱 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **Application Insights 원격 분석...** 또는 **Application Insights 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-122">Right-click your web app project in Solution Explorer, and choose **Add** > **Application Insights Telemetry...** or **Configure Application Insights**.</span></span>

![추가, Application Insights 원격 분석이 강조 표시된 솔루션 탐색기 스크린샷](./media/app-insights-asp-net/appinsights-03-addExisting.png)

<span data-ttu-id="0834e-124">(Visual Studio 2015에도 hello 새 프로젝트 대화 상자에서 옵션 tooadd Application Insights.)</span><span class="sxs-lookup"><span data-stu-id="0834e-124">(In Visual Studio 2015, there's also an option tooadd Application Insights in hello New Project dialog.)</span></span>

<span data-ttu-id="0834e-125">Toohello Application Insights 구성 페이지를 계속 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-125">Continue toohello Application Insights configuration page:</span></span>

![Application Insights에 앱 등록 페이지의 스크린샷](./media/app-insights-asp-net/visual-studio-register-dialog.png)

<span data-ttu-id="0834e-127">**a.**</span><span class="sxs-lookup"><span data-stu-id="0834e-127">**a.**</span></span> <span data-ttu-id="0834e-128">Hello 계정과 tooaccess Azure를 사용 하는 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-128">Select hello account and subscription that you use tooaccess Azure.</span></span>

<span data-ttu-id="0834e-129">**b.**</span><span class="sxs-lookup"><span data-stu-id="0834e-129">**b.**</span></span> <span data-ttu-id="0834e-130">앱에서 toosee hello 데이터를 원하는 Azure의 hello 리소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-130">Select hello resource in Azure where you want toosee hello data from your app.</span></span> <span data-ttu-id="0834e-131">일반적으로</span><span class="sxs-lookup"><span data-stu-id="0834e-131">Usually:</span></span>

* <span data-ttu-id="0834e-132">단일 응용 프로그램의 [여러 구성 요소에 대해 단일 리소스](app-insights-monitor-multi-role-apps.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-132">Use a [single resource for different components](app-insights-monitor-multi-role-apps.md) of a single application.</span></span> 
* <span data-ttu-id="0834e-133">관계 없는 응용 프로그램에 대해 별도의 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-133">Create separate resources for unrelated applications.</span></span>
 
<span data-ttu-id="0834e-134">Tooset hello 리소스 그룹 또는 hello 위치 데이터가 저장 되어 클릭 **설정을 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-134">If you want tooset hello resource group or hello location where your data is stored, click **Configure settings**.</span></span> <span data-ttu-id="0834e-135">리소스 그룹은 사용 되는 toocontrol 액세스 toodata 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-135">Resource groups are used toocontrol access toodata.</span></span> <span data-ttu-id="0834e-136">예를 들어의 일부가 되 여러 응용 프로그램이 있는 경우 hello 동일한 시스템의 Application Insights 데이터를 지정할 수 있습니다 hello 동일한 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-136">For example, if you have several apps that form part of hello same system, you might put their Application Insights data in hello same resource group.</span></span>

<span data-ttu-id="0834e-137">**c.**</span><span class="sxs-lookup"><span data-stu-id="0834e-137">**c.**</span></span> <span data-ttu-id="0834e-138">Hello 무료 데이터 볼륨도 tooavoid 요금에 한 한도가 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-138">Set a cap at hello free data volume limit, tooavoid charges.</span></span> <span data-ttu-id="0834e-139">Application Insights는 tooa 확보 특정 양의 원격 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-139">Application Insights is free up tooa certain volume of telemetry.</span></span> <span data-ttu-id="0834e-140">Hello 리소스를 만든 후에 열어 hello 포털에서 선택 사항을 변경할 수 있습니다 **기능 + 가격 책정** > **데이터 볼륨 관리** > **매일 볼륨 cap**합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-140">After hello resource is created, you can change your selection in hello portal by opening  **Features + pricing** > **Data volume management** > **Daily volume cap**.</span></span>

<span data-ttu-id="0834e-141">**d.**</span><span class="sxs-lookup"><span data-stu-id="0834e-141">**d.**</span></span> <span data-ttu-id="0834e-142">클릭 **등록** toogo 계속 하 고 웹 응용 프로그램에 대 한 Application Insights를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-142">Click **Register** toogo ahead and configure Application Insights for your web app.</span></span> <span data-ttu-id="0834e-143">원격 분석 전송 toohello 됩니다 [Azure 포털](https://portal.azure.com), 디버깅 하는 동안와 응용 프로그램을 게시 한 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-143">Telemetry will be sent toohello [Azure portal](https://portal.azure.com), both during debugging and after you have published your app.</span></span>

<span data-ttu-id="0834e-144">**e.**</span><span class="sxs-lookup"><span data-stu-id="0834e-144">**e.**</span></span> <span data-ttu-id="0834e-145">되지 않도록 toosend 원격 분석 toohello 포털을 디버깅할 때 hello Application Insights SDK tooyour 앱 추가 hello 포털에서 리소스를 구성 하지 않으면 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-145">If you don't want toosend telemetry toohello portal while you're debugging, just add hello Application Insights SDK tooyour app but don't configure a resource in hello portal.</span></span> <span data-ttu-id="0834e-146">디버깅 하는 동안에 Visual Studio에서 수 toosee 원격 분석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-146">You will be able toosee telemetry in Visual Studio while you are debugging.</span></span> <span data-ttu-id="0834e-147">나중 toothis 구성 페이지에서 반환할 수 있습니다 또는 앱을 배포한 후 될 때까지 기다릴 수 있습니다 및 [런타임 시 원격 분석 켜기](app-insights-monitor-performance-live-website-now.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-147">Later, you can return toothis configuration page, or you could wait until after you have deployed your app and [switch on telemetry at run time](app-insights-monitor-performance-live-website-now.md).</span></span>


## <span data-ttu-id="0834e-148"><a name="run"></a> 2단계: 앱 실행</span><span class="sxs-lookup"><span data-stu-id="0834e-148"><a name="run"></a> Step 2: Run your app</span></span>
<span data-ttu-id="0834e-149">F5를 사용하여 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-149">Run your app with F5.</span></span> <span data-ttu-id="0834e-150">일부 원격 분석 toogenerate 서로 다른 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-150">Open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="0834e-151">Visual Studio에서 기록 된 hello 이벤트의 개수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-151">In Visual Studio, you see a count of hello events that have been logged.</span></span>

![Visual Studio의 스크린샷.](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a><span data-ttu-id="0834e-154">3단계: 원격 분석 확인</span><span class="sxs-lookup"><span data-stu-id="0834e-154">Step 3: See your telemetry</span></span>
<span data-ttu-id="0834e-155">Visual Studio 또는 hello Application Insights 웹 포털에서 원격 분석을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-155">You can see your telemetry either in Visual Studio or in hello Application Insights web portal.</span></span> <span data-ttu-id="0834e-156">원격 분석 검색 toohelp Visual Studio에서에서 응용 프로그램을 디버깅할 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-156">Search telemetry in Visual Studio toohelp you debug your app.</span></span> <span data-ttu-id="0834e-157">시스템은 라이브 때 성능과 hello 웹 포털에서 사용량을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-157">Monitor performance and usage in hello web portal when your system is live.</span></span> 

### <a name="see-your-telemetry-in-visual-studio"></a><span data-ttu-id="0834e-158">Visual Studio에서 원격 분석 확인</span><span class="sxs-lookup"><span data-stu-id="0834e-158">See your telemetry in Visual Studio</span></span>

<span data-ttu-id="0834e-159">Visual Studio에서 hello Application Insights 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-159">In Visual Studio, open hello Application Insights window.</span></span> <span data-ttu-id="0834e-160">두 번 클릭 hello **Application Insights** 단추를 선택 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하거나 **Application Insights**, 클릭 하 고 **라이브 원격 분석 검색**.</span><span class="sxs-lookup"><span data-stu-id="0834e-160">Either click hello **Application Insights** button, or right-click your project in Solution Explorer, select **Application Insights**, and then click **Search Live Telemetry**.</span></span>

<span data-ttu-id="0834e-161">Hello Visual Studio Application Insights 검색 창에서 참조 hello **디버그 세션에서 데이터** hello 서버 쪽 응용 프로그램에서 생성 된 원격 분석에 대 한 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-161">In hello Visual Studio Application Insights Search window, see hello **Data from Debug session** view for telemetry generated in hello server side of your app.</span></span> <span data-ttu-id="0834e-162">Hello 필터와 모든 이벤트 toosee 자세히를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-162">Experiment with hello filters, and click any event toosee more detail.</span></span>

![Hello 스크린샷 디버그 세션에서 데이터 hello Application Insights 창에서 봅니다.](./media/app-insights-asp-net/55.png)

> [!NOTE]
> <span data-ttu-id="0834e-164">데이터가 보이지 않으면 hello 시간 범위 올바른지, 그리고 hello 검색 아이콘을 클릭 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-164">If you don't see any data, make sure hello time range is correct, and click hello Search icon.</span></span>

<span data-ttu-id="0834e-165">[Visual Studio의 Application Insights 도구에 대해 자세히 알아봅니다](app-insights-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="0834e-165">[Learn more about Application Insights tools in Visual Studio](app-insights-visual-studio.md).</span></span>

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a><span data-ttu-id="0834e-166">웹 포털에서 원격 분석 확인</span><span class="sxs-lookup"><span data-stu-id="0834e-166">See telemetry in web portal</span></span>

<span data-ttu-id="0834e-167">(선택 하지 않은 경우 tooinstall만 hello SDK)에 hello Application Insights 웹 포털에서 원격 분석을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-167">You can also see telemetry in hello Application Insights web portal (unless you chose tooinstall only hello SDK).</span></span> <span data-ttu-id="0834e-168">hello 포털에는 차트, 분석 도구 및 Visual Studio 보다 구성 요소 간 보기에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-168">hello portal has more charts, analytic tools, and cross-component views than Visual Studio.</span></span> <span data-ttu-id="0834e-169">또한 hello 포털 경고를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-169">hello portal also provides alerts.</span></span>

<span data-ttu-id="0834e-170">Application Insights 리소스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-170">Open your Application Insights resource.</span></span> <span data-ttu-id="0834e-171">Toohello에 로그인 하거나 [Azure 포털](https://portal.azure.com/) , 또는 오른쪽 클릭 hello 프로젝트 Visual Studio에서 찾아 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-171">Either sign in toohello [Azure portal](https://portal.azure.com/) and find it there, or right-click hello project in Visual Studio, and let it take you there.</span></span>

![스크린 샷 Visual Studio의 tooopen Application Insights 포털 hello 하는 방법을 보여 주는](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> <span data-ttu-id="0834e-173">액세스 오류가 발생 하는 경우: hello 잘못 된 집합을 사용 하 여 로그인 된 있으며 Microsoft 자격 증명을 둘 이상의 집합 있습니까?</span><span class="sxs-lookup"><span data-stu-id="0834e-173">If you get an access error: Do you have more than one set of Microsoft credentials, and are you signed in with hello wrong set?</span></span> <span data-ttu-id="0834e-174">Hello 포털에서 로그 아웃 하 고 다시 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-174">In hello portal, sign out and sign in again.</span></span>

<span data-ttu-id="0834e-175">hello 포털의 응용 프로그램에서 hello 원격 분석 보기에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-175">hello portal opens on a view of hello telemetry from your app.</span></span>

![Application Insights 개요 페이지 스크린샷](./media/app-insights-asp-net/66.png)

<span data-ttu-id="0834e-177">Hello 포털에서 모든 타일 또는 차트 toosee 자세히 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-177">In hello portal, click any tile or chart toosee more detail.</span></span>

<span data-ttu-id="0834e-178">[Application Insights를 사용 하 여 hello Azure 포털에에서 대 한 자세한](app-insights-dashboards.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-178">[Learn more about using Application Insights in hello Azure portal](app-insights-dashboards.md).</span></span>

## <a name="step-4-publish-your-app"></a><span data-ttu-id="0834e-179">4단계: 앱 게시</span><span class="sxs-lookup"><span data-stu-id="0834e-179">Step 4: Publish your app</span></span>
<span data-ttu-id="0834e-180">응용 프로그램 tooyour IIS 서버 또는 tooAzure 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-180">Publish your app tooyour IIS server or tooAzure.</span></span> <span data-ttu-id="0834e-181">조사식 [라이브 메트릭 스트림](app-insights-metrics-explorer.md#live-metrics-stream) toomake 모든 실행 되 고 있는지 원활 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-181">Watch [Live Metrics Stream](app-insights-metrics-explorer.md#live-metrics-stream) toomake sure everything is running smoothly.</span></span>

<span data-ttu-id="0834e-182">원격 분석 hello Application Insights 포털에서 메트릭을 모니터링, 원격 분석을 검색 하 고 수 있는 설정 쌓이는 [대시보드](app-insights-dashboards.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-182">Your telemetry builds up in hello Application Insights portal, where you can monitor metrics, search your telemetry, and set up [dashboards](app-insights-dashboards.md).</span></span> <span data-ttu-id="0834e-183">사용할 수도 있습니다 hello 강력한 [로그 분석 쿼리 언어](https://docs.loganalytics.io/) tooanalyze 사용 현황 및 성능 또는 toofind 특정 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-183">You can also use hello powerful [Log Analytics query language](https://docs.loganalytics.io/) tooanalyze usage and performance, or toofind specific events.</span></span>

<span data-ttu-id="0834e-184">또한 계속 tooanalyze에서 원격 분석 [Visual Studio](app-insights-visual-studio.md), 진단 검색과 같은 도구로 및 [추세](app-insights-visual-studio-trends.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-184">You can also continue tooanalyze your telemetry in [Visual Studio](app-insights-visual-studio.md), with tools such as diagnostic search and [trends](app-insights-visual-studio-trends.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0834e-185">응용 프로그램에 충분 한 원격 분석 tooapproach hello 보내는 경우 [조절 제한](app-insights-pricing.md#limits-summary)자동 [샘플링](app-insights-sampling.md) 전환 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-185">If your app sends enough telemetry tooapproach hello [throttling limits](app-insights-pricing.md#limits-summary), automatic [sampling](app-insights-sampling.md) switches on.</span></span> <span data-ttu-id="0834e-186">샘플링을 진단 용도로 상호 관련 된 데이터를 유지 하면서 응용 프로그램에서 보낸 원격 분석의 hello 수량을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-186">Sampling reduces hello quantity of telemetry sent from your app, while preserving correlated data for diagnostic purposes.</span></span>
>
>

## <span data-ttu-id="0834e-187"><a name="land"></a> 모든 설정을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-187"><a name="land"></a> You're all set</span></span>

<span data-ttu-id="0834e-188">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-188">Congratulations!</span></span> <span data-ttu-id="0834e-189">응용 프로그램에서 hello Application Insights 패키지를 설치 하 고 toosend 원격 분석 toohello Application Insights 서비스가 Azure에서 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-189">You installed hello Application Insights package in your app, and configured it toosend telemetry toohello Application Insights service on Azure.</span></span>

![원격 분석의 이동 다이어그램](./media/app-insights-asp-net/01-scheme.png)

<span data-ttu-id="0834e-191">앱의 원격 분석을 수신 하는 Azure 리소스 hello로 식별 되는 *계측 키*합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-191">hello Azure resource that receives your app's telemetry is identified by an *instrumentation key*.</span></span> <span data-ttu-id="0834e-192">Hello ApplicationInsights.config 파일의이 키를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-192">You'll find this key in hello ApplicationInsights.config file.</span></span>


## <a name="upgrade-toofuture-sdk-versions"></a><span data-ttu-id="0834e-193">Toofuture SDK 버전 업그레이드</span><span class="sxs-lookup"><span data-stu-id="0834e-193">Upgrade toofuture SDK versions</span></span>
<span data-ttu-id="0834e-194">tooupgrade tooa [hello SDK의 새 릴리스](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases)개방형 hello **NuGet 패키지 관리자** 다시 및 설치 된 패키지에 대 한 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-194">tooupgrade tooa [new release of hello SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), open hello **NuGet package manager** again, and filter on installed packages.</span></span> <span data-ttu-id="0834e-195">**Microsoft.ApplicationInsights.Web**을 선택하고 **업그레이드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-195">Select **Microsoft.ApplicationInsights.Web**, and choose **Upgrade**.</span></span>

<span data-ttu-id="0834e-196">모든 사용자 지정 tooApplicationInsights.config을 만든 경우 업그레이드 하기 전에 해당 복사본을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-196">If you made any customizations tooApplicationInsights.config, save a copy of it before you upgrade.</span></span> <span data-ttu-id="0834e-197">Hello 새 버전에 변경 내용을 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-197">Then, merge your changes into hello new version.</span></span>

## <a name="video"></a><span data-ttu-id="0834e-198">비디오</span><span class="sxs-lookup"><span data-stu-id="0834e-198">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="0834e-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0834e-199">Next steps</span></span>

### <a name="more-telemetry"></a><span data-ttu-id="0834e-200">추가 원격 분석</span><span class="sxs-lookup"><span data-stu-id="0834e-200">More telemetry</span></span>

* <span data-ttu-id="0834e-201">**[브라우저 및 페이지 로드 데이터](app-insights-javascript.md)** - 웹 페이지에 코드 조각을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-201">**[Browser and page load data](app-insights-javascript.md)** - Insert a code snippet in your web pages.</span></span>
* <span data-ttu-id="0834e-202">**[더 자세한 종속성 및 예외 모니터링 가져오기](app-insights-monitor-performance-live-website-now.md)** - 서버에 상태 모니터를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-202">**[Get more detailed dependency and exception monitoring](app-insights-monitor-performance-live-website-now.md)** - Install Status Monitor on your server.</span></span>
* <span data-ttu-id="0834e-203">**[사용자 지정 이벤트 코드](app-insights-api-custom-events-metrics.md)**  toocount, 시간, 또는 사용자 작업을 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-203">**[Code custom events](app-insights-api-custom-events-metrics.md)** toocount, time, or measure user actions.</span></span>
* <span data-ttu-id="0834e-204">**[로그 데이터 가져오기](app-insights-asp-net-trace-logs.md)** - 로그 데이터와 원격 분석 간에 상관 관계를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-204">**[Get log data](app-insights-asp-net-trace-logs.md)** - Correlate log data with your telemetry.</span></span>

### <a name="analysis"></a><span data-ttu-id="0834e-205">분석</span><span class="sxs-lookup"><span data-stu-id="0834e-205">Analysis</span></span>

* <span data-ttu-id="0834e-206">**[Visual Studio Online에서 Application Insights로 작업](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="0834e-206">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="0834e-207">원격 분석을 사용 하 여 디버깅 하는 방법에 대 한 정보를 포함 진단 검색과 toocode 드릴스루 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-207">Includes information about debugging with telemetry, diagnostic search, and drill through toocode.</span></span>
* <span data-ttu-id="0834e-208">**[Hello Application Insights 포털 작업](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="0834e-208">**[Working with hello Application Insights portal](app-insights-dashboards.md)**</span></span><br/> <span data-ttu-id="0834e-209">대시보드, 강력한 진단 및 분석 도구, 경고, 응용 프로그램의 라이브 종속성 맵 및 원격 분석 내보내기에 대한 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-209">Includes information about dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span>
* <span data-ttu-id="0834e-210">**[분석](app-insights-analytics-tour.md)**  -hello 강력한 쿼리 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-210">**[Analytics](app-insights-analytics-tour.md)** - hello powerful query language.</span></span>

### <a name="alerts"></a><span data-ttu-id="0834e-211">경고</span><span class="sxs-lookup"><span data-stu-id="0834e-211">Alerts</span></span>

* <span data-ttu-id="0834e-212">[가용성 테스트](app-insights-monitor-web-app-availability.md): 테스트를 만들고 toomake 사이트 hello 웹에서 화면에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-212">[Availability tests](app-insights-monitor-web-app-availability.md): Create tests toomake sure your site is visible on hello web.</span></span>
* <span data-ttu-id="0834e-213">[진단 스마트](app-insights-proactive-diagnostics.md): 이러한 테스트 자동으로 실행 되므로 없는 toodo 어느 것에 tooset를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-213">[Smart diagnostics](app-insights-proactive-diagnostics.md): These tests run automatically, so you don't have toodo anything tooset them up.</span></span> <span data-ttu-id="0834e-214">앱이 실패한 요청으로 비정상적인 속도를 보일 경우 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-214">They tell you if your app has an unusual rate of failed requests.</span></span>
* <span data-ttu-id="0834e-215">[메트릭 경고](app-insights-alerts.md): 이러한 toowarn 설정 메트릭을 임계값을 초과할 경우 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-215">[Metric alerts](app-insights-alerts.md): Set these toowarn you if a metric crosses a threshold.</span></span> <span data-ttu-id="0834e-216">앱에 코딩하는 사용자 지정 메트릭에 이러한 경고를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-216">You can set them on custom metrics that you code into your app.</span></span>

### <a name="automation"></a><span data-ttu-id="0834e-217">Automation</span><span class="sxs-lookup"><span data-stu-id="0834e-217">Automation</span></span>

* [<span data-ttu-id="0834e-218">Application Insights 리소스 만들기 자동화</span><span class="sxs-lookup"><span data-stu-id="0834e-218">Automate creating an Application Insights resource</span></span>](app-insights-powershell.md)

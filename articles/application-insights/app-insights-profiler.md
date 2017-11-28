---
title: "Application Insights를 사용하여 Azure에서 라이브 웹앱 프로파일링 | Microsoft Docs"
description: "적은 공간의 프로파일러를 사용하여 웹 서버 코드에서 실행 부하 과다 경로를 식별합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: ff39f9a84b86c14859aaee50ee368643fb2848ea
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="profiling-live-azure-web-apps-with-application-insights"></a><span data-ttu-id="ddadd-103">Application Insights를 사용하여 라이브 Azure Web Apps 프로파일링</span><span class="sxs-lookup"><span data-stu-id="ddadd-103">Profiling live Azure web apps with Application Insights</span></span>

<span data-ttu-id="ddadd-104">*Application Insights의 이 기능은 App Services의 경우 GA이고 Compute의 경우 미리 보기에 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="ddadd-104">*This feature of Application Insights is GA for App Services and in preview for Compute.*</span></span>

<span data-ttu-id="ddadd-105">[Azure Application Insights](app-insights-overview.md)의 프로파일링 도구를 사용하여 라이브 웹 응용 프로그램의 각 메서드에서 얼마나 많은 시간이 소요되는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-105">Find out how much time is spent in each method in your live web application by using the profiling tool of [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="ddadd-106">앱에서 제공한 라이브 요청의 자세한 프로필을 보여 주고 가장 많은 시간을 사용하는 '실행 부하 과다 경로'를 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-106">It shows you detailed profiles of live requests that were served by your app, and highlights the 'hot path' that is using the most time.</span></span> <span data-ttu-id="ddadd-107">서로 다른 응답 시간을 갖는 예제를 자동으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-107">It automatically selects examples that have different response times.</span></span> <span data-ttu-id="ddadd-108">프로파일러는 오버헤드를 최소화하기 위해 다양한 기법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-108">The profiler uses various techniques to minimize overhead.</span></span>

<span data-ttu-id="ddadd-109">프로파일러는 현재 최소한 기본 가격 책정 계층의 Azure 앱 서비스에서 실행 중인 ASP.NET 웹앱에 대해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-109">The profiler currently works for ASP.NET web apps running on Azure App Services, in at least the Basic pricing tier.</span></span> 

<a id="installation"></a>
## <a name="enable-the-profiler"></a><span data-ttu-id="ddadd-110">프로파일러 활성화</span><span class="sxs-lookup"><span data-stu-id="ddadd-110">Enable the profiler</span></span>

<span data-ttu-id="ddadd-111">코드에서 [Application Insights를 설치합니다](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="ddadd-111">[Install Application Insights](app-insights-asp-net.md) in your code.</span></span> <span data-ttu-id="ddadd-112">이미 설치된 경우 최신 버전인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-112">If it's already installed, make sure you have the latest version.</span></span> <span data-ttu-id="ddadd-113">(이렇게 하려면 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 NuGet 패키지 관리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-113">(To do this, right-click your project in Solution Explorer, and choose Manage NuGet packages.</span></span> <span data-ttu-id="ddadd-114">업데이트를 선택하고 모든 패키지를 업데이트합니다.) 앱을 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-114">Select Updates and update all packages.) Re-deploy your app.</span></span>

<span data-ttu-id="ddadd-115">*ASP.NET Core를 사용 중입니까? [여기를 확인하세요](#aspnetcore).*</span><span class="sxs-lookup"><span data-stu-id="ddadd-115">*Using ASP.NET Core? [Check here](#aspnetcore).*</span></span>

<span data-ttu-id="ddadd-116">[https://portal.azure.com](https://portal.azure.com)에서 웹앱에 대한 Application Insights 리소스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-116">In [https://portal.azure.com](https://portal.azure.com), open the Application Insights resource for your web app.</span></span> <span data-ttu-id="ddadd-117">**성능**을 열고 **Application Insights 프로파일러 사용...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-117">Open **Performance** and click **Enable Application Insights Profiler...**.</span></span>

![프로파일러 사용 배너 클릭][enable-profiler-banner]

<span data-ttu-id="ddadd-119">또는 항상 **구성**을 클릭하여 상태를 보거나, 프로파일러를 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-119">Alternatively, you can always click **Configure** to view status, enable, or disable the Profiler.</span></span>

![성능 블레이드에서 구성 클릭][performance-blade]

<span data-ttu-id="ddadd-121">Application Insights로 구성된 웹앱은 구성 블레이드에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-121">Web apps that are configured with Application Insights are listed on Configure blade.</span></span> <span data-ttu-id="ddadd-122">필요한 경우 지침에 따라 프로파일러 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-122">Follow instructions to install the Profiler agent if needed.</span></span> <span data-ttu-id="ddadd-123">Application Insights로 구성된 웹앱이 아직 없는 경우 *연결된 앱 추가*를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-123">If no web app is configured with Application Insights yet, click *Add Linked Apps*.</span></span>

<span data-ttu-id="ddadd-124">구성 블레이드에서 *프로파일러 사용* 또는 *프로파일러 사용 안 함* 단추를 사용하여 연결된 모든 웹앱의 프로파일러를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-124">Use the *Enable Profiler* or *Disable Profiler* buttons in the Configure blade to control the Profiler on all your linked web apps.</span></span>



![구성 블레이드][linked app services]

<span data-ttu-id="ddadd-126">개별 App Service 인스턴스에 대해 프로파일러를 중지하거나 다시 시작하려면 **App Service 리소스**의 **웹 작업**에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-126">To stop or restart the profiler for an individual App Service instance, you'll find it **in the App Service resource**, in **Web Jobs**.</span></span> <span data-ttu-id="ddadd-127">삭제하려면 **확장** 아래에서 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-127">To delete it, look under **Extensions**.</span></span>

![웹 작업에 대한 프로파일러 사용 안 함][disable-profiler-webjob]

<span data-ttu-id="ddadd-129">성능 문제를 가능한 한 빨리 검색하려면 모든 웹앱에서 프로파일러를 사용하도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-129">We recommend that you have the Profiler enabled on all your web apps to discover any performance issues as soon as possible.</span></span>

<span data-ttu-id="ddadd-130">WebDeploy를 사용하여 웹 응용 프로그램에 변경 내용을 배포하는 경우 배포하는 동안 **App_Data** 폴더가 삭제되는 것을 제외하도록 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-130">If you use WebDeploy to deploy changes to your web application, ensure that you exclude the **App_Data** folder from being deleted during deployment.</span></span> <span data-ttu-id="ddadd-131">그렇지 않으면 다음에 Azure에 웹 응용 프로그램을 배포할 때 프로파일러 확장의 파일이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-131">Otherwise, the profiler extension's files will be deleted when you next deploy the web application to Azure.</span></span>

### <a name="using-profiler-with-azure-vms-and-compute-resources-preview"></a><span data-ttu-id="ddadd-132">Azure VM 및 Compute 리소스에서 프로파일러 사용(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="ddadd-132">Using profiler with Azure VMs and Compute resources (preview)</span></span>

<span data-ttu-id="ddadd-133">[런타임에 Azure App Services에 대해 Application Insights를 사용하도록 설정](app-insights-azure-web-apps.md#run-time-instrumentation-with-application-insights)하면 프로파일러를 자동으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-133">When you [enable Application Insights for Azure app services at run time](app-insights-azure-web-apps.md#run-time-instrumentation-with-application-insights), Profiler is automatically available.</span></span> <span data-ttu-id="ddadd-134">(리소스에 대해 Application Insights를 이미 사용하도록 설정한 경우 **구성** 마법사를 통해 최신 버전으로 업데이트해야 할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="ddadd-134">(If you already enabled Application Insights for the resource, you might need to update to the lates version through the **Configure** wizard.)</span></span>

<span data-ttu-id="ddadd-135">[Azure Compute 리소스에 대한 미리 보기 버전의 프로파일러](https://go.microsoft.com/fwlink/?linkid=848155)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-135">There is a [preview version of the Profiler for Azure Compute resources](https://go.microsoft.com/fwlink/?linkid=848155).</span></span>


## <a name="limits"></a><span data-ttu-id="ddadd-136">제한</span><span class="sxs-lookup"><span data-stu-id="ddadd-136">Limits</span></span>

<span data-ttu-id="ddadd-137">기본 데이터 보존 기간은 5일입니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-137">The default data retention is 5 days.</span></span> <span data-ttu-id="ddadd-138">매일 최대 10GB가 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-138">Maximum 10 GB ingested per day.</span></span>

<span data-ttu-id="ddadd-139">프로파일러 서비스에는 요금이 부과되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-139">There is no charge for the profiler service.</span></span> <span data-ttu-id="ddadd-140">웹앱은 적어도 App Services의 기본 계층에 호스트되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-140">Your web app must be hosted in at least the Basic tier of App Services.</span></span>

## <a name="viewing-profiler-data"></a><span data-ttu-id="ddadd-141">프로파일러 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="ddadd-141">Viewing profiler data</span></span>

<span data-ttu-id="ddadd-142">성능 블레이드를 열고 작업 목록 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-142">Open the Performance blade and scroll down to the operation list.</span></span>




![Application Insights 성능 블레이드 예제 열][performance-blade-examples]

<span data-ttu-id="ddadd-144">테이블의 열은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-144">The columns in the table are:</span></span>

* <span data-ttu-id="ddadd-145">**수** - 블레이드 시간 범위에서 이러한 요청 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-145">**Count** - The number of these requests in the time range of the blade.</span></span>
* <span data-ttu-id="ddadd-146">**중앙값** - 앱이 요청에 응답하는 데 걸리는 일반적인 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-146">**Median** - The typical time your app takes to respond to a request.</span></span> <span data-ttu-id="ddadd-147">모든 응답의 절반은 이것보다 더 빨랐습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-147">Half of all responses were faster than this.</span></span>
* <span data-ttu-id="ddadd-148">**95 백분위수** 응답의 95%는 이것보다 더 빨랐습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-148">**95th percentile** 95% of responses were faster than this.</span></span> <span data-ttu-id="ddadd-149">이 수치가 중앙값과 전혀 다른 경우 앱에 간헐적 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-149">If this figure is very different from the median, there might be an intermittent problem with your app.</span></span> <span data-ttu-id="ddadd-150">(또는 캐시와 같은 디자인 기능으로 설명될 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="ddadd-150">(Or it might be explained by a design feature such as caching.)</span></span>
* <span data-ttu-id="ddadd-151">**예제** - 아이콘은 프로파일러가 이 작업에 대한 스택 추적을 캡처했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-151">**Examples** - an icon indicates that the profiler has captured stack traces for this operation.</span></span>

<span data-ttu-id="ddadd-152">예제 아이콘을 클릭하여 추적 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-152">Click the Examples icon to open the trace explorer.</span></span> <span data-ttu-id="ddadd-153">탐색기는 응답 시간에 따라 분류된 프로파일러가 캡처한 몇 가지 샘플을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-153">The explorer shows several samples that the profiler has captured, classified by response time.</span></span>

<span data-ttu-id="ddadd-154">샘플을 선택하여 요청을 실행하는 데 걸린 시간의 코드 수준 분석을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-154">Select a sample to show a code-level breakdown of time spent executing the request.</span></span>

![Application Insights 추적 탐색기][trace-explorer]

<span data-ttu-id="ddadd-156">**실행 부하 과다 경로 표시**는 가장 큰 리프 노드 또는 닫힌 것을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-156">**Show hot path** opens the biggest leaf node, or at least something close.</span></span> <span data-ttu-id="ddadd-157">대부분의 경우에서 이 노드는 성능 병목에 인접한 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-157">In most cases this node will be adjacent to a performance bottleneck.</span></span>



* <span data-ttu-id="ddadd-158">**레이블**: 함수 또는 이벤트의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-158">**Label**: The name of the function or event.</span></span> <span data-ttu-id="ddadd-159">트리는 발생한 코드와 이벤트의 혼합을 보여 줍니다(예: SQL 및 http 이벤트).</span><span class="sxs-lookup"><span data-stu-id="ddadd-159">The tree shows a mix of code and events that occurred (such as SQL and http events).</span></span> <span data-ttu-id="ddadd-160">최상위 이벤트는 전체 요청 기간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-160">The top event represents the overall request duration.</span></span>
* <span data-ttu-id="ddadd-161">**경과 시간**: 작업의 시작과 끝 사이의 시간 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-161">**Elapsed**: The time interval between the start of the operation and the end.</span></span>
* <span data-ttu-id="ddadd-162">**때**: 함수/이벤트가 다른 함수와 관련해서 실행된 경우를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-162">**When**: Shows when the function/event was running in relation to other functions.</span></span>

## <a name="how-to-read-performance-data"></a><span data-ttu-id="ddadd-163">성능 데이터를 읽는 방법</span><span class="sxs-lookup"><span data-stu-id="ddadd-163">How to read performance data</span></span>

<span data-ttu-id="ddadd-164">Microsoft 서비스 프로파일러는 샘플링 메서드와 계측의 조합을 사용하여 응용 프로그램의 성능을 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-164">Microsoft service profiler uses a combination of sampling method and instrumentation to analyze the performance of your application.</span></span>
<span data-ttu-id="ddadd-165">자세한 컬렉션이 진행 중인 경우 서비스 프로파일러는 1밀리초 마다 각 컴퓨터 CPU의 명령 포인터를 샘플링합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-165">When detailed collection is in progress, service profiler samples the instruction pointer of each of the machine's CPU in every millisecond.</span></span>
<span data-ttu-id="ddadd-166">각 샘플은 스레드가 상위 및 하위 수준의 추상화에서 수행한 작업에 대한 상세하고 유용한 정보를 제공하는 현재 실행 중인 스레드의 전체 호출 스택을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-166">Each sample captures the complete call stack of the thread currently executing, giving detailed and useful information about what that thread was doing at both high and low levels of abstraction.</span></span> <span data-ttu-id="ddadd-167">서비스 프로파일러는 또한 컨텍스트 스위칭 이벤트, TPL 이벤트 및 스레드 풀 이벤트와 같은 다른 이벤트를 수집하여 활동 상관 관계 및 인과 관계를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-167">Service profiler also collects other events such as context switching events, TPL events, and thread-pool events to track activity correlation and causality.</span></span>

<span data-ttu-id="ddadd-168">타임라인 보기에 표시된 호출 스택은 위의 샘플링 및 계측의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-168">The call stack shown in the timeline view is the result of the above sampling and instrumentation.</span></span> <span data-ttu-id="ddadd-169">각 샘플은 스레드의 전체 호출 스택을 캡처하므로 .NET 프레임워크의 코드 뿐만 아니라 참조하는 다른 프레임워크의 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-169">Because each sample captures the complete call stack of the thread, it includes code from the .NET framework, as well as other frameworks you reference.</span></span>

### <span data-ttu-id="ddadd-170"><a id="jitnewobj"></a>개체 할당(`clr!JIT\_New or clr!JIT\_Newarr1`)</span><span class="sxs-lookup"><span data-stu-id="ddadd-170"><a id="jitnewobj"></a>Object Allocation (`clr!JIT\_New or clr!JIT\_Newarr1`)</span></span>
<span data-ttu-id="ddadd-171">`clr!JIT\_New and clr!JIT\_Newarr1`은 관리되는 힙에서 메모리를 할당하는 .NET 프레임워크 내부의 도우미 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-171">`clr!JIT\_New and clr!JIT\_Newarr1` are helper functions inside .NET framework that allocates memory from managed heap.</span></span> <span data-ttu-id="ddadd-172">개체가 할당되면 `clr!JIT\_New`가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-172">`clr!JIT\_New` is invoked when an object is allocated.</span></span> <span data-ttu-id="ddadd-173">개체 배열이 할당되면 `clr!JIT\_Newarr1`이 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-173">`clr!JIT\_Newarr1` is invoked when an object array is allocated.</span></span> <span data-ttu-id="ddadd-174">이 두 함수는 일반적으로 매우 빠르며 상대적으로 적은 양의 시간을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-174">These two functions are typically very fast and should take relatively small amount of time.</span></span> <span data-ttu-id="ddadd-175">`clr!JIT\_New` 또는 `clr!JIT\_Newarr1`이 타임라인에서 상당한 양의 시간을 사용하는 경우 코드에 많은 개체가 할당되고 많은 양의 메모리가 소비될 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-175">If you see `clr!JIT\_New` or `clr!JIT\_Newarr1` take a substantial amount of time in your timeline, it's an indication that the code may be allocating many objects and consuming significant amount of memory.</span></span>

### <span data-ttu-id="ddadd-176"><a id="theprestub"></a>코드 로드(`clr!ThePreStub`)</span><span class="sxs-lookup"><span data-stu-id="ddadd-176"><a id="theprestub"></a>Loading Code (`clr!ThePreStub`)</span></span>
<span data-ttu-id="ddadd-177">`clr!ThePreStub`은 처음으로 실행할 코드를 준비하는 .NET 프레임워크 내부의 도우미 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-177">`clr!ThePreStub` is a helper function inside .NET framework that prepares the code to execute for the first time.</span></span> <span data-ttu-id="ddadd-178">일반적으로 JIT(Just In Time) 컴파일을 포함하지만 이에 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-178">This typically includes, but not limited to, JIT (Just In Time) compilation.</span></span> <span data-ttu-id="ddadd-179">각 C# 메서드의 경우 `clr!ThePreStub`은 프로세스의 수명 동안 한 번만 호출되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-179">For each C# method, `clr!ThePreStub` should be invoked at most once during the lifetime of a process.</span></span>

<span data-ttu-id="ddadd-180">`clr!ThePreStub`이 요청에 대해 상당한 양의 시간을 사용하는 경우 요청이 해당 메서드를 실행하는 첫 번째 항목이며 해당 메서드를 로드할 .NET 프레임워크 런타임에 대한 시간이 상당한 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-180">If you see `clr!ThePreStub` takes significant amount of time for a request, it indicates that request is the first one that executes that method, and the time for .NET framework runtime to load that method is significant.</span></span> <span data-ttu-id="ddadd-181">사용자가 액세스하기 전에 코드의 해당 부분을 실행하는 준비 프로세스를 고려하거나 어셈블리에서 NGen 실행을 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-181">You can consider a warm-up process that executes that portion of the code before your users access it, or consider running NGen on your assemblies.</span></span>

### <span data-ttu-id="ddadd-182"><a id="lockcontention"></a>잠금 경합(`clr!JITutil\_MonContention` 또는 `clr!JITutil\_MonEnterWorker`)</span><span class="sxs-lookup"><span data-stu-id="ddadd-182"><a id="lockcontention"></a>Lock Contention (`clr!JITutil\_MonContention` or `clr!JITutil\_MonEnterWorker`)</span></span>
<span data-ttu-id="ddadd-183">`clr!JITutil\_MonContention` 또는 `clr!JITutil\_MonEnterWorker`는 현재 스레드가 잠금이 해제되기를 기다리고 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-183">`clr!JITutil\_MonContention` or `clr!JITutil\_MonEnterWorker` indicate the current thread is waiting for a lock to be released.</span></span> <span data-ttu-id="ddadd-184">이는 일반적으로 C# lock 문을 실행하거나 Monitor.Enter 메서드를 호출하거나 MethodImplOptions.Synchronized 특성으로 메서드를 호출할 때 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-184">This typically shows up when executing a C# lock statement, invoking Monitor.Enter method, or invoking a method with MethodImplOptions.Synchronized attribute.</span></span> <span data-ttu-id="ddadd-185">잠금 경합은 일반적으로 스레드 A가 잠금을 획득하고 스레드 B가 스레드 A가 잠금을 해제하기 전에 동일한 잠금을 획득하려고 하는 경우에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-185">Lock contention typically happens when thread A acquires a lock, and thread B tries to acquire the same lock before thread A releases it.</span></span>

### <span data-ttu-id="ddadd-186"><a id="ngencold"></a>코드 로드(`[COLD]`)</span><span class="sxs-lookup"><span data-stu-id="ddadd-186"><a id="ngencold"></a>Loading code (`[COLD]`)</span></span>
<span data-ttu-id="ddadd-187">메서드 이름에 `mscorlib.ni![COLD]System.Reflection.CustomAttribute.IsDefined`와 같은 `[COLD]`를 포함하는 경우 .NET 프레임워크 런타임이 처음으로 <a href="https://msdn.microsoft.com/library/e7k32f4k.aspx">프로필 기반 최적화</a>에 최적화되지 않은 코드를 실행하고 있는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-187">If the method name contains `[COLD]`, such as `mscorlib.ni![COLD]System.Reflection.CustomAttribute.IsDefined`, it means that the .NET framework runtime is executing code that is not optimized by <a href="https://msdn.microsoft.com/library/e7k32f4k.aspx">profile-guided optimization</a> for the first time.</span></span> <span data-ttu-id="ddadd-188">각 메서드의 경우 프로세스의 수명 동안 한 번만 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-188">For each method, it should show up at most once during the lifetime of the process.</span></span>

<span data-ttu-id="ddadd-189">코드 로드에 요청에 대해 상당한 양의 시간이 사용되는 경우 요청이 메서드의 최적화되지 않은 부분을 실행하는 첫 번째 항목임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-189">If loading code takes significant amount of time for a request, it indicates that request is the first one to execute the unoptimized portion of the method.</span></span> <span data-ttu-id="ddadd-190">사용자가 액세스하기 전에 코드의 해당 부분을 실행하는 준비 프로세스를 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-190">You can consider a warm up process that executes that portion of the code before your users access it.</span></span>

### <span data-ttu-id="ddadd-191"><a id="httpclientsend"></a>HTTP 요청 보내기</span><span class="sxs-lookup"><span data-stu-id="ddadd-191"><a id="httpclientsend"></a>Send HTTP Request</span></span>
<span data-ttu-id="ddadd-192">`HttpClient.Send`와 같은 메서드는 코드가 HTTP 요청이 완료되기를 기다리고 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-192">Methods such as `HttpClient.Send` indicate the code is waiting for a HTTP request to complete.</span></span>

### <span data-ttu-id="ddadd-193"><a id="sqlcommand"></a>데이터베이스 작업</span><span class="sxs-lookup"><span data-stu-id="ddadd-193"><a id="sqlcommand"></a>Database Operation</span></span>
<span data-ttu-id="ddadd-194">SqlCommand.Execute와 같은 메서드는 코드가 데이터베이스 작업이 완료되기를 기다리고 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-194">Method such as SqlCommand.Execute indicates the code is waiting for a database operation to complete.</span></span>

### <span data-ttu-id="ddadd-195"><a id="await"></a>대기(`AWAIT\_TIME`)</span><span class="sxs-lookup"><span data-stu-id="ddadd-195"><a id="await"></a>Waiting (`AWAIT\_TIME`)</span></span>
<span data-ttu-id="ddadd-196">`AWAIT\_TIME`은 코드가 다른 작업이 완료되기를 기다리고 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-196">`AWAIT\_TIME` indicates the code is waiting for another task to complete.</span></span> <span data-ttu-id="ddadd-197">이는 일반적으로 C# 'await' 문과 함께 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-197">This typically happens with C# 'await' statement.</span></span> <span data-ttu-id="ddadd-198">코드가 C# 'await'를 수행하는 경우 스레드는 스레드 풀에 대한 컨트롤을 해제 및 반환하고 'await'가 끝나기를 기다리는 것이 차단된 스레드는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-198">When the code does a C# 'await', the thread unwinds and returns control to the thread-pool, and there is no thread that is blocked waiting for the 'await' to finish.</span></span> <span data-ttu-id="ddadd-199">그러나 논리적으로 await를 수행한 스레드는 작업이 완료되길 기다리는 것이 '차단됩니다'.</span><span class="sxs-lookup"><span data-stu-id="ddadd-199">However, logically the thread that did the await is 'blocked' waiting for the operation to complete.</span></span> <span data-ttu-id="ddadd-200">`AWAIT\_TIME`은 작업이 완료되기를 기다리는 차단된 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-200">The `AWAIT\_TIME` indicates the blocked time waiting for the task to complete.</span></span>

### <span data-ttu-id="ddadd-201"><a id="block"></a>차단된 시간</span><span class="sxs-lookup"><span data-stu-id="ddadd-201"><a id="block"></a>Blocked Time</span></span>
<span data-ttu-id="ddadd-202">`BLOCKED_TIME`은 코드가 동기화 개체를 기다리거나 스레드를 사용할 수 있기를 기다리거나 요청이 완료되기를 기다리는 등의 다른 리소스를 사용할 수 있기를 기다리는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-202">`BLOCKED_TIME` indicates the code is waiting for another resource to be available, such as waiting for a synchronization object, waiting for a thread to be available, or waiting for a request to finish.</span></span>

### <span data-ttu-id="ddadd-203"><a id="cpu"></a>CPU 시간</span><span class="sxs-lookup"><span data-stu-id="ddadd-203"><a id="cpu"></a>CPU Time</span></span>
<span data-ttu-id="ddadd-204">CPU는 명령을 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-204">The CPU is busy executing the instructions.</span></span>

### <span data-ttu-id="ddadd-205"><a id="disk"></a>디스크 시간</span><span class="sxs-lookup"><span data-stu-id="ddadd-205"><a id="disk"></a>Disk Time</span></span>
<span data-ttu-id="ddadd-206">응용 프로그램은 디스크 작업을 수행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-206">The application is performing disk operations.</span></span>

### <span data-ttu-id="ddadd-207"><a id="network"></a>네트워크 시간</span><span class="sxs-lookup"><span data-stu-id="ddadd-207"><a id="network"></a>Network Time</span></span>
<span data-ttu-id="ddadd-208">응용 프로그램은 네트워크 작업을 수행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-208">The application is performing network operations.</span></span>

### <span data-ttu-id="ddadd-209"><a id="when"></a>때 열</span><span class="sxs-lookup"><span data-stu-id="ddadd-209"><a id="when"></a>When column</span></span>
<span data-ttu-id="ddadd-210">이는 노드에 대해 수집된 INCLUSIVE 샘플이 시간에 따라 달라지는 방식의 시각화입니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-210">This is a visualization of how the INCLUSIVE samples collected for a node vary over time.</span></span> <span data-ttu-id="ddadd-211">전체 범위 요청은 32시간 버킷으로 나뉘어지고 해당 노드에 대한 포괄 샘플은 이러한 32버킷으로 누적됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-211">The total range of the request is divided into 32 time buckets and the inclusive samples for that node are accumulated into those 32 buckets.</span></span> <span data-ttu-id="ddadd-212">각 버킷은 높이가 크기 조정된 값을 나타내는 막대로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-212">Each bucket is then represented as a bar whose height represents a scaled value.</span></span> <span data-ttu-id="ddadd-213">리소스(cpu, 디스크, 스레드)를 사용하는 확실한 관계가 있는 `CPU_TIME` 또는 `BLOCKED_TIME`으로 표시된 노드의 경우 막대는 해당 버킷의 기간 동안 이러한 리소스 중 하나를 사용함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-213">For nodes marked `CPU_TIME` or `BLOCKED_TIME`, or where there is an obvious relationship of consuming a resource (cpu, disk, thread), the bar represents consuming one of those resources for the period of time of that bucket.</span></span> <span data-ttu-id="ddadd-214">이러한 메트릭의 경우 여러 리소스를 소비하여 100% 이상을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-214">For these metrics you can get greater than 100% by consuming multiple resources.</span></span> <span data-ttu-id="ddadd-215">예를 들어 두 개의 CPU를 사용하는 평균이 간격을 넘는 경우 200%를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-215">For example, if on average you use two CPUs over an interval then you get 200%.</span></span>


## <span data-ttu-id="ddadd-216"><a id="troubleshooting"></a>문제 해결</span><span class="sxs-lookup"><span data-stu-id="ddadd-216"><a id="troubleshooting"></a>Troubleshooting</span></span>

### <a name="how-can-i-know-whether-application-insights-profiler-is-running"></a><span data-ttu-id="ddadd-217">Application Insights Profiler가 실행되고 있는지 어떻게 알 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="ddadd-217">How can I know whether Application Insights profiler is running?</span></span>

<span data-ttu-id="ddadd-218">프로파일러는 웹앱에서 지속형 웹 작업으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-218">The profiler runs as a continuous web job in Web App.</span></span> <span data-ttu-id="ddadd-219">https://portal.azure.com에서 웹앱 리소스를 열고 웹 작업 블레이드에서 "ApplicationInsightsProfiler" 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-219">You can open the Web App resource in https://portal.azure.com and check "ApplicationInsightsProfiler" status in the WebJobs blade.</span></span> <span data-ttu-id="ddadd-220">실행되지 않는 경우 **로그**를 열어 자세한 정보를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-220">If it isn't running, open **Logs** to find out more.</span></span>

### <a name="why-cant-i-find-any-stack-examples-even-though-the-profiler-is-running"></a><span data-ttu-id="ddadd-221">프로파일러가 실행 중인데도 스택 예제를 찾을 수 없는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ddadd-221">Why can't I find any stack examples even though the profiler is running?</span></span>

<span data-ttu-id="ddadd-222">다음 몇 가지 사항으로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-222">Here are a few things you can check.</span></span>

1. <span data-ttu-id="ddadd-223">웹앱 서비스 계획이 기본 계층 이상인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-223">Make sure your Web App Service Plan is Basic tier and above.</span></span>
2. <span data-ttu-id="ddadd-224">웹앱에서 Application Insights SDK 2.2 베타 이상이 활성화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-224">Make sure your Web App has Application Insights SDK 2.2 Beta and above enabled.</span></span>
3. <span data-ttu-id="ddadd-225">웹앱에 Application Insights SDK에서 사용하는 동일한 계측 키를 가진 APPINSIGHTS_INSTRUMENTATIONKEY 설정이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-225">Make sure your Web App has the APPINSIGHTS_INSTRUMENTATIONKEY setting with the same instrumentation key used by Application Insights SDK.</span></span>
4. <span data-ttu-id="ddadd-226">웹앱이 .NET Framework 4.6에서 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-226">Make sure your Web App is running on .Net Framework 4.6.</span></span>
5. <span data-ttu-id="ddadd-227">ASP.NET Core 응용 프로그램인 경우 [필수 종속성](#aspnetcore)도 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-227">If it's an ASP.NET Core application, please also check [the required dependencies](#aspnetcore).</span></span>

<span data-ttu-id="ddadd-228">프로파일러가 시작된 후 프로파일러가 여러 성능 추적을 적극적으로 수집하는 경우 짧은 준비 기간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-228">After the profiler is started, there is a short warm-up period when the profiler actively collects several performance traces.</span></span> <span data-ttu-id="ddadd-229">그런 다음 프로파일러는 매 시간 2분 동안 성능 추적을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-229">After that, the profiler collects performance traces for two minutes in every hour.</span></span>  

### <a name="i-was-using-azure-service-profiler-what-happened-to-it"></a><span data-ttu-id="ddadd-230">Azure Service Profiler를 사용하고 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-230">I was using Azure Service Profiler.</span></span> <span data-ttu-id="ddadd-231">어떻게 된 건가요?</span><span class="sxs-lookup"><span data-stu-id="ddadd-231">What happened to it?</span></span>  

<span data-ttu-id="ddadd-232">Application Insights Profiler를 활성화하면 Azure Service Profiler 에이전트는 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-232">When you enable Application Insights Profiler, Azure Service Profiler agent is disabled.</span></span>

### <span data-ttu-id="ddadd-233"><a id="double-counting"></a>병렬 스레드에서 이중 계산</span><span class="sxs-lookup"><span data-stu-id="ddadd-233"><a id="double-counting"></a>Double counting in parallel threads</span></span>

<span data-ttu-id="ddadd-234">경우에 따라 스택 뷰어의 총 시간 메트릭은 요청의 실제 기간 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-234">In some cases the total time metric in the stack viewer is more than the actual duration of the request.</span></span>

<span data-ttu-id="ddadd-235">병렬로 작업하는 두 개 이상의 스레드가 요청과 연결된 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-235">This can happen when there are two or more threads associated with a request, operating in parallel.</span></span> <span data-ttu-id="ddadd-236">총 스레드 시간은 경과된 시간 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-236">The total thread time is then more than the elapsed time.</span></span> <span data-ttu-id="ddadd-237">대부분의 경우에서 하나의 스레드는 다른 스레드가 완료되기를 기다리고 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-237">In many cases one thread may be waiting on the other to complete.</span></span> <span data-ttu-id="ddadd-238">뷰어는 이를 감지하고 필요하지 않은 대기를 생략하려고 시도하지만 중요한 정보일 수 있는 것을 생략하는 대신 너무 많은 것을 보여 주는 측면의 오류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-238">The viewer tries to detect this and omit the uninteresting wait, but errs on the side of showing too much rather than omitting what may be critical information.</span></span>  

<span data-ttu-id="ddadd-239">추적에 병렬 스레드가 표시되면 요청에 중요한 경로를 결정할 수 있도록 대기 중인 스레드를 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-239">When you see parallel threads in your traces, you need to determine which threads are waiting so you can determine the critical path for the request.</span></span> <span data-ttu-id="ddadd-240">대부분의 경우 대기 상태로 빠르게 전환하는 스레드는 단순히 다른 스레드를 기다리고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-240">In most cases, the thread that quickly goes into a wait state is simply waiting on the other threads.</span></span> <span data-ttu-id="ddadd-241">다른 것에 집중하고 대기 중인 스레드 대기 시간을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-241">Concentrate on the others and ignore the time in the waiting threads.</span></span>

### <span data-ttu-id="ddadd-242"><a id="issue-loading-trace-in-viewer"></a>프로파일링 데이터 없음</span><span class="sxs-lookup"><span data-stu-id="ddadd-242"><a id="issue-loading-trace-in-viewer"></a>No profiling data</span></span>

1. <span data-ttu-id="ddadd-243">보려고 하는 데이터가 몇 주보다 오래된 경우 시간 필터를 제한하고 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-243">If the data you are trying to view is older than a couple of weeks, try limiting your time filter and try again.</span></span>

2. <span data-ttu-id="ddadd-244">프록시 또는 방화벽이 https://gateway.azureserviceprofiler.net에 대한 액세스를 차단하지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-244">Check that proxies or a firewall have not blocked access to https://gateway.azureserviceprofiler.net.</span></span>

3. <span data-ttu-id="ddadd-245">앱에서 사용하는 Application Insights 계측 키가 프로파일링을 활성화한 Application Insights 리소스와 동일한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-245">Check that the Application Insights instrumentation key you are using in your app is the same as the Application Insights resource you've enabled profiling with.</span></span> <span data-ttu-id="ddadd-246">키는 일반적으로 ApplicationInsights.config에 있지만 web.config 또는 app.config에서 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-246">The key is usually in ApplicationInsights.config but can also be found in web.config or app.config.</span></span>

### <a name="error-report-in-the-profiling-viewer"></a><span data-ttu-id="ddadd-247">프로파일링 뷰어의 오류 보고서</span><span class="sxs-lookup"><span data-stu-id="ddadd-247">Error report in the profiling viewer</span></span>

<span data-ttu-id="ddadd-248">포털에서 지원 티켓을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-248">File a support ticket from the portal.</span></span> <span data-ttu-id="ddadd-249">오류 메시지의 상관 관계 ID를 포함하세요.</span><span class="sxs-lookup"><span data-stu-id="ddadd-249">Please include the correlation ID from the error message.</span></span>

## <a name="manual-installation"></a><span data-ttu-id="ddadd-250">수동 설치</span><span class="sxs-lookup"><span data-stu-id="ddadd-250">Manual installation</span></span>

<span data-ttu-id="ddadd-251">프로파일러를 구성하면 웹앱의 설정에 다음 업데이트가 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-251">When you configure the profiler, the following updates are made to the Web App's settings.</span></span> <span data-ttu-id="ddadd-252">환경에 필요한 경우, 예를 들어 응용 프로그램이 ASE(Azure App Service Environment)에서 실행되는 경우 이 작업을 수동으로 직접 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-252">You can do them yourself manually if your environment requires, for example, if your application runs in Azure App Service Environment (ASE):</span></span>

1. <span data-ttu-id="ddadd-253">웹앱 제어 블레이드에서 설정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-253">In the web app control blade, open Settings.</span></span>
2. <span data-ttu-id="ddadd-254">".NET Framework 버전"을 v4.6으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-254">Set ".Net Framework version" to v4.6.</span></span>
3. <span data-ttu-id="ddadd-255">"무중단"을 사용으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-255">Set "Always On" to On.</span></span>
4. <span data-ttu-id="ddadd-256">앱 설정 "__APPINSIGHTS_INSTRUMENTATIONKEY__"를 추가하고 값을 SDK에서 사용한 동일한 계측 키로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-256">Add app setting "__APPINSIGHTS_INSTRUMENTATIONKEY__" and set the value to the same instrumentation key used by the SDK.</span></span>
5. <span data-ttu-id="ddadd-257">고급 도구를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-257">Open Advanced Tools.</span></span>
6. <span data-ttu-id="ddadd-258">“이동”을 클릭하여 Kudu 웹 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-258">Click "Go" to open the Kudu website.</span></span>
7. <span data-ttu-id="ddadd-259">Kudu 웹 사이트에서 “사이트 확장”을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-259">In the Kudu website, select "Site extensions".</span></span>
8. <span data-ttu-id="ddadd-260">갤러리에서 “__Application Insights__”를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-260">Install "__Application Insights__" from Gallery.</span></span>
9. <span data-ttu-id="ddadd-261">웹 앱을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-261">Restart the web app.</span></span>

## <span data-ttu-id="ddadd-262"><a id="aspnetcore"></a>ASP.NET Core 지원</span><span class="sxs-lookup"><span data-stu-id="ddadd-262"><a id="aspnetcore"></a>ASP.NET Core Support</span></span>

<span data-ttu-id="ddadd-263">ASP.NET Core 응용 프로그램을 사용하려면 Microsoft.ApplicationInsights.AspNetCore Nuget 패키지 2.1.0-beta6 이상을 설치하여 프로파일러와 작동하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-263">ASP.NET Core application needs to install Microsoft.ApplicationInsights.AspNetCore Nuget package 2.1.0-beta6 or higher to work with the Profiler.</span></span> <span data-ttu-id="ddadd-264">2017/6/27 이후에는 그보다 하위 버전은 더 이상 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ddadd-264">We no longer support the lower versions after 6/27/2017.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddadd-265">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ddadd-265">Next steps</span></span>

* [<span data-ttu-id="ddadd-266">Visual Studio에서 Application Insights로 작업</span><span class="sxs-lookup"><span data-stu-id="ddadd-266">Working with Application Insights in Visual Studio</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-visual-studio)

[performance-blade]: ./media/app-insights-profiler/performance-blade.png
[performance-blade-examples]: ./media/app-insights-profiler/performance-blade-examples.png
[trace-explorer]: ./media/app-insights-profiler/trace-explorer.png
[trace-explorer-toolbar]: ./media/app-insights-profiler/trace-explorer-toolbar.png
[trace-explorer-hint-tip]: ./media/app-insights-profiler/trace-explorer-hint-tip.png
[trace-explorer-hot-path]: ./media/app-insights-profiler/trace-explorer-hot-path.png
[enable-profiler-banner]: ./media/app-insights-profiler/enable-profiler-banner.png
[disable-profiler-webjob]: ./media/app-insights-profiler/disable-profiler-webjob.png
[linked app services]: ./media/app-insights-profiler/linked-app-services.png

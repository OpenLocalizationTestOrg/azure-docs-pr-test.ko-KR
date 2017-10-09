---
title: "Application Insights를 사용 하 여 Azure에서 aaaProfiling 라이브 웹 앱 | Microsoft Docs"
description: "사용량이 프로파일러를 웹 서버 코드에서 hello 실행 부하 과다 경로 식별 합니다."
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
ms.openlocfilehash: 3c7f21076f19335e0f006327932e13623ec9526b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="profiling-live-azure-web-apps-with-application-insights"></a><span data-ttu-id="cda5c-103">Application Insights를 사용하여 라이브 Azure Web Apps 프로파일링</span><span class="sxs-lookup"><span data-stu-id="cda5c-103">Profiling live Azure web apps with Application Insights</span></span>

<span data-ttu-id="cda5c-104">*Application Insights의 이 기능은 App Services의 경우 GA이고 Compute의 경우 미리 보기에 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="cda5c-104">*This feature of Application Insights is GA for App Services and in preview for Compute.*</span></span>

<span data-ttu-id="cda5c-105">프로 파일링 도구의의 hello를 사용 하 여 라이브 웹 응용 프로그램에서 각 방법의 소요 시간 확인 [Azure Application Insights](app-insights-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-105">Find out how much time is spent in each method in your live web application by using hello profiling tool of [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="cda5c-106">응용 프로그램에서 제공 된 라이브 요청의 자세한 프로필 표시 하 고 hello를 사용 하는 hello 대부분의 시간 ' 실행 부하 과다 경로'를 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-106">It shows you detailed profiles of live requests that were served by your app, and highlights hello 'hot path' that is using hello most time.</span></span> <span data-ttu-id="cda5c-107">서로 다른 응답 시간을 갖는 예제를 자동으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-107">It automatically selects examples that have different response times.</span></span> <span data-ttu-id="cda5c-108">hello 프로파일러는 다양 한 기술을 toominimize 오버 헤드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-108">hello profiler uses various techniques toominimize overhead.</span></span>

<span data-ttu-id="cda5c-109">hello 프로파일러 현재 ASP.NET에 대 한 works 웹 Azure 앱 서비스에서 실행 되는 앱에서 Basic 가격 책정 계층 이상 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-109">hello profiler currently works for ASP.NET web apps running on Azure App Services, in at least hello Basic pricing tier.</span></span> 

<a id="installation"></a>
## <a name="enable-hello-profiler"></a><span data-ttu-id="cda5c-110">Hello 프로파일러를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="cda5c-110">Enable hello profiler</span></span>

<span data-ttu-id="cda5c-111">코드에서 [Application Insights를 설치합니다](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="cda5c-111">[Install Application Insights](app-insights-asp-net.md) in your code.</span></span> <span data-ttu-id="cda5c-112">이미 설치 되어 있으면 hello 최신 버전이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-112">If it's already installed, make sure you have hello latest version.</span></span> <span data-ttu-id="cda5c-113">(toodo이를 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 NuGet 패키지 관리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-113">(toodo this, right-click your project in Solution Explorer, and choose Manage NuGet packages.</span></span> <span data-ttu-id="cda5c-114">업데이트를 선택하고 모든 패키지를 업데이트합니다.) 앱을 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-114">Select Updates and update all packages.) Re-deploy your app.</span></span>

<span data-ttu-id="cda5c-115">*ASP.NET Core를 사용 중입니까? [여기를 확인하세요](#aspnetcore).*</span><span class="sxs-lookup"><span data-stu-id="cda5c-115">*Using ASP.NET Core? [Check here](#aspnetcore).*</span></span>

<span data-ttu-id="cda5c-116">[https://portal.azure.com](https://portal.azure.com), 웹 앱에 대 한 hello Application Insights 리소스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-116">In [https://portal.azure.com](https://portal.azure.com), open hello Application Insights resource for your web app.</span></span> <span data-ttu-id="cda5c-117">**성능**을 열고 **Application Insights 프로파일러 사용...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-117">Open **Performance** and click **Enable Application Insights Profiler...**.</span></span>

![Hello 사용 프로파일러 배너에 클릭][enable-profiler-banner]

<span data-ttu-id="cda5c-119">항상 클릭 해도, **구성** tooview 상태를 사용 하도록 설정 또는 hello 프로파일러를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-119">Alternatively, you can always click **Configure** tooview status, enable, or disable hello Profiler.</span></span>

![Hello 성능 블레이드에서 구성을 클릭합니다][performance-blade]

<span data-ttu-id="cda5c-121">Application Insights로 구성된 웹앱은 구성 블레이드에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-121">Web apps that are configured with Application Insights are listed on Configure blade.</span></span> <span data-ttu-id="cda5c-122">필요한 경우 지침 tooinstall hello 프로파일러 에이전트를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-122">Follow instructions tooinstall hello Profiler agent if needed.</span></span> <span data-ttu-id="cda5c-123">Application Insights로 구성된 웹앱이 아직 없는 경우 *연결된 앱 추가*를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-123">If no web app is configured with Application Insights yet, click *Add Linked Apps*.</span></span>

<span data-ttu-id="cda5c-124">사용 하 여 hello *프로파일러를 사용 하도록 설정* 또는 *프로파일러 사용 하지 않도록 설정* hello 구성 블레이드 toocontrol 단추 모든 연결 된 웹 앱에 프로파일러를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-124">Use hello *Enable Profiler* or *Disable Profiler* buttons in hello Configure blade toocontrol hello Profiler on all your linked web apps.</span></span>



![구성 블레이드][linked app services]

<span data-ttu-id="cda5c-126">개별 응용 프로그램 서비스 인스턴스에 대 한 hello 프로파일러 toostop 또는 다시 시작에서 찾을 수 **hello 응용 프로그램 서비스 리소스에에서**에 **웹 작업이**합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-126">toostop or restart hello profiler for an individual App Service instance, you'll find it **in hello App Service resource**, in **Web Jobs**.</span></span> <span data-ttu-id="cda5c-127">toodelete 것 검토 **확장**합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-127">toodelete it, look under **Extensions**.</span></span>

![웹 작업에 대한 프로파일러 사용 안 함][disable-profiler-webjob]

<span data-ttu-id="cda5c-129">Hello 프로파일러 성능 문제를 가능한 한 빨리 프로그램 모든 웹 앱 toodiscover에서 사용 하도록 설정 해야 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-129">We recommend that you have hello Profiler enabled on all your web apps toodiscover any performance issues as soon as possible.</span></span>

<span data-ttu-id="cda5c-130">WebDeploy toodeploy 변경 tooyour 웹 응용 프로그램을 사용 하는 경우 확인 hello를 제외 하면 **App_Data** 폴더를 배포 하는 동안 삭제 되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-130">If you use WebDeploy toodeploy changes tooyour web application, ensure that you exclude hello **App_Data** folder from being deleted during deployment.</span></span> <span data-ttu-id="cda5c-131">그렇지 않으면 hello 프로파일러 확장의 파일이 삭제 됩니다 hello 웹 응용 프로그램 tooAzure를 다음에 배포 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="cda5c-131">Otherwise, hello profiler extension's files will be deleted when you next deploy hello web application tooAzure.</span></span>

### <a name="using-profiler-with-azure-vms-and-compute-resources-preview"></a><span data-ttu-id="cda5c-132">Azure VM 및 Compute 리소스에서 프로파일러 사용(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="cda5c-132">Using profiler with Azure VMs and Compute resources (preview)</span></span>

<span data-ttu-id="cda5c-133">[런타임에 Azure App Services에 대해 Application Insights를 사용하도록 설정](app-insights-azure-web-apps.md#run-time-instrumentation-with-application-insights)하면 프로파일러를 자동으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-133">When you [enable Application Insights for Azure app services at run time](app-insights-azure-web-apps.md#run-time-instrumentation-with-application-insights), Profiler is automatically available.</span></span> <span data-ttu-id="cda5c-134">(Hello 리소스에 대 한 Application Insights 이미 설정한 경우에 hello 통해 tooupdate toohello lates 버전을 할 수 있습니다 **구성** 마법사.)</span><span class="sxs-lookup"><span data-stu-id="cda5c-134">(If you already enabled Application Insights for hello resource, you might need tooupdate toohello lates version through hello **Configure** wizard.)</span></span>

<span data-ttu-id="cda5c-135">한 [미리 보기 버전의 Azure 계산 리소스에 대 한 프로파일러 hello](https://go.microsoft.com/fwlink/?linkid=848155)합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-135">There is a [preview version of hello Profiler for Azure Compute resources](https://go.microsoft.com/fwlink/?linkid=848155).</span></span>


## <a name="limits"></a><span data-ttu-id="cda5c-136">제한</span><span class="sxs-lookup"><span data-stu-id="cda5c-136">Limits</span></span>

<span data-ttu-id="cda5c-137">hello 기본 데이터 보존은 5 일입니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-137">hello default data retention is 5 days.</span></span> <span data-ttu-id="cda5c-138">매일 최대 10GB가 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-138">Maximum 10 GB ingested per day.</span></span>

<span data-ttu-id="cda5c-139">hello 프로파일러 서비스에 대 한 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-139">There is no charge for hello profiler service.</span></span> <span data-ttu-id="cda5c-140">웹 앱에서 호스트 되어야 합니다 적어도 응용 프로그램 서비스의 기본 계층 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-140">Your web app must be hosted in at least hello Basic tier of App Services.</span></span>

## <a name="viewing-profiler-data"></a><span data-ttu-id="cda5c-141">프로파일러 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="cda5c-141">Viewing profiler data</span></span>

<span data-ttu-id="cda5c-142">Toohello 작업 목록 아래로 스크롤하여 및 hello 성능 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-142">Open hello Performance blade and scroll down toohello operation list.</span></span>




![Application Insights 성능 블레이드 예제 열][performance-blade-examples]

<span data-ttu-id="cda5c-144">hello hello 테이블의 열이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-144">hello columns in hello table are:</span></span>

* <span data-ttu-id="cda5c-145">**Count** -hello hello 블레이드의 hello 시간 범위에서 이러한 요청 수입니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-145">**Count** - hello number of these requests in hello time range of hello blade.</span></span>
* <span data-ttu-id="cda5c-146">**중앙값** -hello 일반적인 시간이 앱 toorespond tooa 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-146">**Median** - hello typical time your app takes toorespond tooa request.</span></span> <span data-ttu-id="cda5c-147">모든 응답의 절반은 이것보다 더 빨랐습니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-147">Half of all responses were faster than this.</span></span>
* <span data-ttu-id="cda5c-148">**95 백분위수** 응답의 95%는 이것보다 더 빨랐습니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-148">**95th percentile** 95% of responses were faster than this.</span></span> <span data-ttu-id="cda5c-149">이 그림 hello 중앙값 매우 다른 경우 응용 프로그램에 일시적인 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-149">If this figure is very different from hello median, there might be an intermittent problem with your app.</span></span> <span data-ttu-id="cda5c-150">(또는 캐시와 같은 디자인 기능으로 설명될 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="cda5c-150">(Or it might be explained by a design feature such as caching.)</span></span>
* <span data-ttu-id="cda5c-151">**예제** -아이콘 hello 프로파일러가이 작업에 대 한 스택 추적 캡처를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-151">**Examples** - an icon indicates that hello profiler has captured stack traces for this operation.</span></span>

<span data-ttu-id="cda5c-152">Hello 예제 아이콘 tooopen hello 추적 탐색기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-152">Click hello Examples icon tooopen hello trace explorer.</span></span> <span data-ttu-id="cda5c-153">프로파일러 hello 몇 가지 예제를 캡처한 hello 탐색기 표시 응답 시간에 따라 분류 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-153">hello explorer shows several samples that hello profiler has captured, classified by response time.</span></span>

<span data-ttu-id="cda5c-154">샘플 tooshow 코드 수준 분석을 실행 중인 데 걸린된 hello 요청이 시간을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-154">Select a sample tooshow a code-level breakdown of time spent executing hello request.</span></span>

![Application Insights 추적 탐색기][trace-explorer]

<span data-ttu-id="cda5c-156">**실행 부하 과다 경로 표시** 열립니다 리프 노드로 서 가장 큰, hello 또는 적어도 무언가 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-156">**Show hot path** opens hello biggest leaf node, or at least something close.</span></span> <span data-ttu-id="cda5c-157">대부분의 경우에서이 노드의 인접 tooa 성능 병목 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-157">In most cases this node will be adjacent tooa performance bottleneck.</span></span>



* <span data-ttu-id="cda5c-158">**레이블**: hello 함수 또는 이벤트의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-158">**Label**: hello name of hello function or event.</span></span> <span data-ttu-id="cda5c-159">hello 트리 코드 및 (예: SQL 및 http 이벤트)에 발생 한 이벤트의 혼합을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-159">hello tree shows a mix of code and events that occurred (such as SQL and http events).</span></span> <span data-ttu-id="cda5c-160">hello 최상위 이벤트 나타내는 hello 전체 기간을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-160">hello top event represents hello overall request duration.</span></span>
* <span data-ttu-id="cda5c-161">**경과 된**: hello 연산의 hello 시작과 hello 끝 사이의 hello 시간 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-161">**Elapsed**: hello time interval between hello start of hello operation and hello end.</span></span>
* <span data-ttu-id="cda5c-162">**때**: hello 함수/이벤트 관계 tooother 함수에서 실행 되는 경우를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-162">**When**: Shows when hello function/event was running in relation tooother functions.</span></span>

## <a name="how-tooread-performance-data"></a><span data-ttu-id="cda5c-163">어떻게 tooread 성능 데이터</span><span class="sxs-lookup"><span data-stu-id="cda5c-163">How tooread performance data</span></span>

<span data-ttu-id="cda5c-164">Microsoft 서비스 프로파일러에서 응용 프로그램의 메서드 및 계측 tooanalyze hello 성능을 샘플링의 조합을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-164">Microsoft service profiler uses a combination of sampling method and instrumentation tooanalyze hello performance of your application.</span></span>
<span data-ttu-id="cda5c-165">자세한 컬렉션 진행에서 되 면 서비스 프로파일러 샘플 hello 모든 밀리초 동안의 hello 컴퓨터의 CPU의 각 명령 포인터입니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-165">When detailed collection is in progress, service profiler samples hello instruction pointer of each of hello machine's CPU in every millisecond.</span></span>
<span data-ttu-id="cda5c-166">각 샘플의 현재 실행, 스레드를 수행 하는지 모두에서 고가 저가의 수준의 추상화에 대 한 상세 하 고 유용한 정보를 제공 하는 hello 스레드 hello 완전 한 호출 스택을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-166">Each sample captures hello complete call stack of hello thread currently executing, giving detailed and useful information about what that thread was doing at both high and low levels of abstraction.</span></span> <span data-ttu-id="cda5c-167">서비스 프로파일러에서 또한 다른 컨텍스트 스위칭 이벤트 등의 이벤트, TPL 이벤트 및 스레드 풀 이벤트 tootrack 활동 상관 관계 및 인과 관계를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-167">Service profiler also collects other events such as context switching events, TPL events, and thread-pool events tootrack activity correlation and causality.</span></span>

<span data-ttu-id="cda5c-168">hello 타임 라인 보기에 표시 된 hello 호출 스택은 샘플링 및 계측 위에 hello hello 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-168">hello call stack shown in hello timeline view is hello result of hello above sampling and instrumentation.</span></span> <span data-ttu-id="cda5c-169">각 샘플 hello 스레드의 전체 호출 스택을 hello를 캡처하므로, 참조할 다른 프레임 워크와 hello.NET framework에서 코드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-169">Because each sample captures hello complete call stack of hello thread, it includes code from hello .NET framework, as well as other frameworks you reference.</span></span>

### <span data-ttu-id="cda5c-170"><a id="jitnewobj"></a>개체 할당(`clr!JIT\_New or clr!JIT\_Newarr1`)</span><span class="sxs-lookup"><span data-stu-id="cda5c-170"><a id="jitnewobj"></a>Object Allocation (`clr!JIT\_New or clr!JIT\_Newarr1`)</span></span>
<span data-ttu-id="cda5c-171">`clr!JIT\_New and clr!JIT\_Newarr1`은 관리되는 힙에서 메모리를 할당하는 .NET 프레임워크 내부의 도우미 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-171">`clr!JIT\_New and clr!JIT\_Newarr1` are helper functions inside .NET framework that allocates memory from managed heap.</span></span> <span data-ttu-id="cda5c-172">개체가 할당되면 `clr!JIT\_New`가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-172">`clr!JIT\_New` is invoked when an object is allocated.</span></span> <span data-ttu-id="cda5c-173">개체 배열이 할당되면 `clr!JIT\_Newarr1`이 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-173">`clr!JIT\_Newarr1` is invoked when an object array is allocated.</span></span> <span data-ttu-id="cda5c-174">이 두 함수는 일반적으로 매우 빠르며 상대적으로 적은 양의 시간을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-174">These two functions are typically very fast and should take relatively small amount of time.</span></span> <span data-ttu-id="cda5c-175">표시 되 면 `clr!JIT\_New` 또는 `clr!JIT\_Newarr1` 일정에서 상당한 양의 시간, 표시 hello 코드 많은 개체를 할당 및 메모리가 많이 소비 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-175">If you see `clr!JIT\_New` or `clr!JIT\_Newarr1` take a substantial amount of time in your timeline, it's an indication that hello code may be allocating many objects and consuming significant amount of memory.</span></span>

### <span data-ttu-id="cda5c-176"><a id="theprestub"></a>코드 로드(`clr!ThePreStub`)</span><span class="sxs-lookup"><span data-stu-id="cda5c-176"><a id="theprestub"></a>Loading Code (`clr!ThePreStub`)</span></span>
<span data-ttu-id="cda5c-177">`clr!ThePreStub`처음으로 hello에 대 한 hello 코드 tooexecute를 준비 하는.NET framework 내 도우미 함수가입니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-177">`clr!ThePreStub` is a helper function inside .NET framework that prepares hello code tooexecute for hello first time.</span></span> <span data-ttu-id="cda5c-178">일반적으로 JIT(Just In Time) 컴파일을 포함하지만 이에 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-178">This typically includes, but not limited to, JIT (Just In Time) compilation.</span></span> <span data-ttu-id="cda5c-179">각 C# 메서드에 대해 `clr!ThePreStub` hello 프로세스 수명 중에 많아야 한 번 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-179">For each C# method, `clr!ThePreStub` should be invoked at most once during hello lifetime of a process.</span></span>

<span data-ttu-id="cda5c-180">표시 되 면 `clr!ThePreStub` 상당한 걸립니다 요청에 대 한 시간의 해당 메서드 및.NET framework 런타임 tooload 메서드는 중요에 대 한 hello 시간을 실행 하는 첫 번째 hello 해당 요청을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-180">If you see `clr!ThePreStub` takes significant amount of time for a request, it indicates that request is hello first one that executes that method, and hello time for .NET framework runtime tooload that method is significant.</span></span> <span data-ttu-id="cda5c-181">사용자가 액세스할 하거나 NGen 어셈블리에서 실행 하기 전에 hello 코드의 해당 부분을 실행 하는 준비 프로세스를 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-181">You can consider a warm-up process that executes that portion of hello code before your users access it, or consider running NGen on your assemblies.</span></span>

### <span data-ttu-id="cda5c-182"><a id="lockcontention"></a>잠금 경합(`clr!JITutil\_MonContention` 또는 `clr!JITutil\_MonEnterWorker`)</span><span class="sxs-lookup"><span data-stu-id="cda5c-182"><a id="lockcontention"></a>Lock Contention (`clr!JITutil\_MonContention` or `clr!JITutil\_MonEnterWorker`)</span></span>
<span data-ttu-id="cda5c-183">`clr!JITutil\_MonContention`또는 `clr!JITutil\_MonEnterWorker` hello 현재 스레드가 해제 잠금 toobe에 대 한 대기를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-183">`clr!JITutil\_MonContention` or `clr!JITutil\_MonEnterWorker` indicate hello current thread is waiting for a lock toobe released.</span></span> <span data-ttu-id="cda5c-184">이는 일반적으로 C# lock 문을 실행하거나 Monitor.Enter 메서드를 호출하거나 MethodImplOptions.Synchronized 특성으로 메서드를 호출할 때 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-184">This typically shows up when executing a C# lock statement, invoking Monitor.Enter method, or invoking a method with MethodImplOptions.Synchronized attribute.</span></span> <span data-ttu-id="cda5c-185">잠금 경합 스레드 A 획득 한 잠금을 했는데 스레드 B가 A 스레드를 해제 하기 전에 잠금 동일 tooacquire hello에 일반적으로 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-185">Lock contention typically happens when thread A acquires a lock, and thread B tries tooacquire hello same lock before thread A releases it.</span></span>

### <span data-ttu-id="cda5c-186"><a id="ngencold"></a>코드 로드(`[COLD]`)</span><span class="sxs-lookup"><span data-stu-id="cda5c-186"><a id="ngencold"></a>Loading code (`[COLD]`)</span></span>
<span data-ttu-id="cda5c-187">Hello 메서드 이름에 포함 되어 있으면 `[COLD]`와 같은 `mscorlib.ni![COLD]System.Reflection.CustomAttribute.IsDefined`,으로 최적화 되지 않은 코드를 실행 하는 hello.NET framework 런타임 의미 <a href="https://msdn.microsoft.com/library/e7k32f4k.aspx">프로필 기반 최적화</a> 처음으로 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-187">If hello method name contains `[COLD]`, such as `mscorlib.ni![COLD]System.Reflection.CustomAttribute.IsDefined`, it means that hello .NET framework runtime is executing code that is not optimized by <a href="https://msdn.microsoft.com/library/e7k32f4k.aspx">profile-guided optimization</a> for hello first time.</span></span> <span data-ttu-id="cda5c-188">각 방법에 대 한 hello 프로세스의 hello 수명 동안 한 번 이하로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-188">For each method, it should show up at most once during hello lifetime of hello process.</span></span>

<span data-ttu-id="cda5c-189">코드를 로드 합니다. 변수를 사용할 경우 상당한 시간이 요청에 대 한 해당 요청은 hello 첫 번째 하나의 tooexecute hello 최적화 되지 않은 부분 hello 메서드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-189">If loading code takes significant amount of time for a request, it indicates that request is hello first one tooexecute hello unoptimized portion of hello method.</span></span> <span data-ttu-id="cda5c-190">사용자에 게 액세스 하기 전에 hello 코드의 해당 부분을 실행 하는 프로세스를 웜을 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-190">You can consider a warm up process that executes that portion of hello code before your users access it.</span></span>

### <span data-ttu-id="cda5c-191"><a id="httpclientsend"></a>HTTP 요청 보내기</span><span class="sxs-lookup"><span data-stu-id="cda5c-191"><a id="httpclientsend"></a>Send HTTP Request</span></span>
<span data-ttu-id="cda5c-192">와 같은 메서드 `HttpClient.Send` hello 코드가 HTTP 요청 toocomplete에 대 한 대기를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-192">Methods such as `HttpClient.Send` indicate hello code is waiting for a HTTP request toocomplete.</span></span>

### <span data-ttu-id="cda5c-193"><a id="sqlcommand"></a>데이터베이스 작업</span><span class="sxs-lookup"><span data-stu-id="cda5c-193"><a id="sqlcommand"></a>Database Operation</span></span>
<span data-ttu-id="cda5c-194">SqlCommand.Execute 같이 hello 코드가 데이터베이스 작업 toocomplete에 대 한 대기를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-194">Method such as SqlCommand.Execute indicates hello code is waiting for a database operation toocomplete.</span></span>

### <span data-ttu-id="cda5c-195"><a id="await"></a>대기(`AWAIT\_TIME`)</span><span class="sxs-lookup"><span data-stu-id="cda5c-195"><a id="await"></a>Waiting (`AWAIT\_TIME`)</span></span>
<span data-ttu-id="cda5c-196">`AWAIT\_TIME`hello 코드가 다른 작업 toocomplete에 대 한 대기를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-196">`AWAIT\_TIME` indicates hello code is waiting for another task toocomplete.</span></span> <span data-ttu-id="cda5c-197">이는 일반적으로 C# 'await' 문과 함께 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-197">This typically happens with C# 'await' statement.</span></span> <span data-ttu-id="cda5c-198">Hello 코드가 수행 하는 경우 C# 'await', hello 스레드 해제 및 제어 toohello 스레드 풀, 반환 및 hello 'await' toofinish 기다리는 차단 된 스레드가 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-198">When hello code does a C# 'await', hello thread unwinds and returns control toohello thread-pool, and there is no thread that is blocked waiting for hello 'await' toofinish.</span></span> <span data-ttu-id="cda5c-199">그러나 스레드는 않은 hello await '' 대기 중인 차단 작업 toocomplete hello에 대 한 논리적으로 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-199">However, logically hello thread that did hello await is 'blocked' waiting for hello operation toocomplete.</span></span> <span data-ttu-id="cda5c-200">`AWAIT\_TIME` hello 작업 toocomplete 기다리는 hello 차단 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-200">The `AWAIT\_TIME` indicates hello blocked time waiting for hello task toocomplete.</span></span>

### <span data-ttu-id="cda5c-201"><a id="block"></a>차단된 시간</span><span class="sxs-lookup"><span data-stu-id="cda5c-201"><a id="block"></a>Blocked Time</span></span>
<span data-ttu-id="cda5c-202">`BLOCKED_TIME`hello 코드가 대기 하는 동기화 개체에 대 한, 사용 가능한 또는 요청 toofinish에 대 한 대기 중인 스레드 toobe 기다리는 같이 사용 가능한 다른 리소스 toobe에 대 한 대기를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-202">`BLOCKED_TIME` indicates hello code is waiting for another resource toobe available, such as waiting for a synchronization object, waiting for a thread toobe available, or waiting for a request toofinish.</span></span>

### <span data-ttu-id="cda5c-203"><a id="cpu"></a>CPU 시간</span><span class="sxs-lookup"><span data-stu-id="cda5c-203"><a id="cpu"></a>CPU Time</span></span>
<span data-ttu-id="cda5c-204">hello CPU는 hello 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-204">hello CPU is busy executing hello instructions.</span></span>

### <span data-ttu-id="cda5c-205"><a id="disk"></a>디스크 시간</span><span class="sxs-lookup"><span data-stu-id="cda5c-205"><a id="disk"></a>Disk Time</span></span>
<span data-ttu-id="cda5c-206">hello 응용 프로그램은 디스크 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-206">hello application is performing disk operations.</span></span>

### <span data-ttu-id="cda5c-207"><a id="network"></a>네트워크 시간</span><span class="sxs-lookup"><span data-stu-id="cda5c-207"><a id="network"></a>Network Time</span></span>
<span data-ttu-id="cda5c-208">hello 응용 프로그램에 네트워크 작업 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-208">hello application is performing network operations.</span></span>

### <span data-ttu-id="cda5c-209"><a id="when"></a>때 열</span><span class="sxs-lookup"><span data-stu-id="cda5c-209"><a id="when"></a>When column</span></span>
<span data-ttu-id="cda5c-210">이 노드에 대 한 수집 hello 포괄 샘플 시간의 경과 따라 어떻게의 시각화는.</span><span class="sxs-lookup"><span data-stu-id="cda5c-210">This is a visualization of how hello INCLUSIVE samples collected for a node vary over time.</span></span> <span data-ttu-id="cda5c-211">hello 요청의 전체 범위 hello 32 시간 버킷으로 나뉘고 hello 포괄 샘플 해당 노드에 대 한 이러한 32 버킷으로 누적 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-211">hello total range of hello request is divided into 32 time buckets and hello inclusive samples for that node are accumulated into those 32 buckets.</span></span> <span data-ttu-id="cda5c-212">각 버킷은 높이가 크기 조정된 값을 나타내는 막대로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-212">Each bucket is then represented as a bar whose height represents a scaled value.</span></span> <span data-ttu-id="cda5c-213">표시 된 노드에 대 한 `CPU_TIME` 또는 `BLOCKED_TIME`, 또는 리소스 (cpu, 디스크, 스레드)를 사용 하는 관계는 확실 한 경우 해당 버킷의 hello 기간 동안 이러한 리소스 중 하나를 사용해 나타내는 막대 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-213">For nodes marked `CPU_TIME` or `BLOCKED_TIME`, or where there is an obvious relationship of consuming a resource (cpu, disk, thread), hello bar represents consuming one of those resources for hello period of time of that bucket.</span></span> <span data-ttu-id="cda5c-214">이러한 메트릭의 경우 여러 리소스를 소비하여 100% 이상을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-214">For these metrics you can get greater than 100% by consuming multiple resources.</span></span> <span data-ttu-id="cda5c-215">예를 들어 두 개의 CPU를 사용하는 평균이 간격을 넘는 경우 200%를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-215">For example, if on average you use two CPUs over an interval then you get 200%.</span></span>


## <span data-ttu-id="cda5c-216"><a id="troubleshooting"></a>문제 해결</span><span class="sxs-lookup"><span data-stu-id="cda5c-216"><a id="troubleshooting"></a>Troubleshooting</span></span>

### <a name="how-can-i-know-whether-application-insights-profiler-is-running"></a><span data-ttu-id="cda5c-217">Application Insights Profiler가 실행되고 있는지 어떻게 알 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="cda5c-217">How can I know whether Application Insights profiler is running?</span></span>

<span data-ttu-id="cda5c-218">hello 프로파일러 웹 앱에서 연속 웹 작업으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-218">hello profiler runs as a continuous web job in Web App.</span></span> <span data-ttu-id="cda5c-219">Https://portal.azure.com의 hello 웹 응용 프로그램 리소스를 열고 hello WebJobs 블레이드에서 "ApplicationInsightsProfiler" 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-219">You can open hello Web App resource in https://portal.azure.com and check "ApplicationInsightsProfiler" status in hello WebJobs blade.</span></span> <span data-ttu-id="cda5c-220">이 실행 중이 아닌 경우 열 **로그** 자세히 toofind 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-220">If it isn't running, open **Logs** toofind out more.</span></span>

### <a name="why-cant-i-find-any-stack-examples-even-though-hello-profiler-is-running"></a><span data-ttu-id="cda5c-221">Hello 프로파일러를 실행 하는 경우에 모든 스택 예제를 찾을 수 없는 이유</span><span class="sxs-lookup"><span data-stu-id="cda5c-221">Why can't I find any stack examples even though hello profiler is running?</span></span>

<span data-ttu-id="cda5c-222">다음 몇 가지 사항으로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-222">Here are a few things you can check.</span></span>

1. <span data-ttu-id="cda5c-223">웹앱 서비스 계획이 기본 계층 이상인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-223">Make sure your Web App Service Plan is Basic tier and above.</span></span>
2. <span data-ttu-id="cda5c-224">웹앱에서 Application Insights SDK 2.2 베타 이상이 활성화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-224">Make sure your Web App has Application Insights SDK 2.2 Beta and above enabled.</span></span>
3. <span data-ttu-id="cda5c-225">웹 앱에 Application Insights SDK에서 동일한 계측 키를 사용 하는 hello로 hello APPINSIGHTS_INSTRUMENTATIONKEY 설정이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-225">Make sure your Web App has hello APPINSIGHTS_INSTRUMENTATIONKEY setting with hello same instrumentation key used by Application Insights SDK.</span></span>
4. <span data-ttu-id="cda5c-226">웹앱이 .NET Framework 4.6에서 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-226">Make sure your Web App is running on .Net Framework 4.6.</span></span>
5. <span data-ttu-id="cda5c-227">ASP.NET Core 응용 프로그램 이면도 확인 하십시오 [hello 필요한 종속성](#aspnetcore)합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-227">If it's an ASP.NET Core application, please also check [hello required dependencies](#aspnetcore).</span></span>

<span data-ttu-id="cda5c-228">Hello 프로파일러 시작 된 후에 다음과 같은 hello 프로파일러 몇 가지 성능 추적 적극적으로 수집 되는 경우 특정 짧은 준비 기간.</span><span class="sxs-lookup"><span data-stu-id="cda5c-228">After hello profiler is started, there is a short warm-up period when hello profiler actively collects several performance traces.</span></span> <span data-ttu-id="cda5c-229">그 후 hello 프로파일러에 1 시간 마다 2 분 동안 성능 추적을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-229">After that, hello profiler collects performance traces for two minutes in every hour.</span></span>  

### <a name="i-was-using-azure-service-profiler-what-happened-tooit"></a><span data-ttu-id="cda5c-230">Azure Service Profiler를 사용하고 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-230">I was using Azure Service Profiler.</span></span> <span data-ttu-id="cda5c-231">발생 했습니다 tooit 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="cda5c-231">What happened tooit?</span></span>  

<span data-ttu-id="cda5c-232">Application Insights Profiler를 활성화하면 Azure Service Profiler 에이전트는 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-232">When you enable Application Insights Profiler, Azure Service Profiler agent is disabled.</span></span>

### <span data-ttu-id="cda5c-233"><a id="double-counting"></a>병렬 스레드에서 이중 계산</span><span class="sxs-lookup"><span data-stu-id="cda5c-233"><a id="double-counting"></a>Double counting in parallel threads</span></span>

<span data-ttu-id="cda5c-234">일부의 경우 hello hello 스택 뷰어에서 총 시간 메트릭은 hello 실제 hello 요청 기간 보다 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-234">In some cases hello total time metric in hello stack viewer is more than hello actual duration of hello request.</span></span>

<span data-ttu-id="cda5c-235">병렬로 작업하는 두 개 이상의 스레드가 요청과 연결된 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-235">This can happen when there are two or more threads associated with a request, operating in parallel.</span></span> <span data-ttu-id="cda5c-236">hello 총 스레드 시간은 다음 hello 경과 된 시간 보다 나중입니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-236">hello total thread time is then more than hello elapsed time.</span></span> <span data-ttu-id="cda5c-237">대부분의 경우에 하나의 스레드를 기다리고 있을 수 있습니다 다른 toocomplete를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-237">In many cases one thread may be waiting on hello other toocomplete.</span></span> <span data-ttu-id="cda5c-238">이 뷰어 시도 toodetect hello 및 hello 필요 하지 않은 대기를 생략 하지만 너무 많은 중요 한 정보가 있을 수 있습니다 어떻게 생략 하는 대신 보여 주는의 hello 측에 않는다는 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-238">hello viewer tries toodetect this and omit hello uninteresting wait, but errs on hello side of showing too much rather than omitting what may be critical information.</span></span>  

<span data-ttu-id="cda5c-239">병렬 스레드 수를 추적에 표시 되 면 hello hello 요청에 대 한 중요 한 경로 확인할 수 있도록 스레드 대기 하 고 있는 toodetermine를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-239">When you see parallel threads in your traces, you need toodetermine which threads are waiting so you can determine hello critical path for hello request.</span></span> <span data-ttu-id="cda5c-240">대부분의 경우에서는에서 단순히 대기 하는 대기 상태에 신속 하 게 hello 스레드가 다른 스레드에서 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-240">In most cases, hello thread that quickly goes into a wait state is simply waiting on hello other threads.</span></span> <span data-ttu-id="cda5c-241">집중 다른 hello 되 고 대기 중인 스레드에 hello에 hello 시간을 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-241">Concentrate on hello others and ignore hello time in hello waiting threads.</span></span>

### <span data-ttu-id="cda5c-242"><a id="issue-loading-trace-in-viewer"></a>프로파일링 데이터 없음</span><span class="sxs-lookup"><span data-stu-id="cda5c-242"><a id="issue-loading-trace-in-viewer"></a>No profiling data</span></span>

1. <span data-ttu-id="cda5c-243">Tooview 몇 주 보다 오래 된 hello 데이터 시도 하 고, 제한 시간 필터 고 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="cda5c-243">If hello data you are trying tooview is older than a couple of weeks, try limiting your time filter and try again.</span></span>

2. <span data-ttu-id="cda5c-244">프록시 또는 방화벽 액세스 toohttps://gateway.azureserviceprofiler.net 차단 되지 않았는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-244">Check that proxies or a firewall have not blocked access toohttps://gateway.azureserviceprofiler.net.</span></span>

3. <span data-ttu-id="cda5c-245">Application Insights 계측 키 응용 프로그램에서 사용 하는 hello와 프로 파일링을 활성화 한 Application Insights 리소스와 동일한 hello 해당 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-245">Check that hello Application Insights instrumentation key you are using in your app is hello same as hello Application Insights resource you've enabled profiling with.</span></span> <span data-ttu-id="cda5c-246">hello 키 일반적으로 ApplicationInsights.config 이지만 web.config 또는 app.config에서 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-246">hello key is usually in ApplicationInsights.config but can also be found in web.config or app.config.</span></span>

### <a name="error-report-in-hello-profiling-viewer"></a><span data-ttu-id="cda5c-247">뷰어를 프로 파일링 하는 hello에서 오류 보고서</span><span class="sxs-lookup"><span data-stu-id="cda5c-247">Error report in hello profiling viewer</span></span>

<span data-ttu-id="cda5c-248">Hello 포털에서 지원 티켓을 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-248">File a support ticket from hello portal.</span></span> <span data-ttu-id="cda5c-249">Hello 오류 메시지에서 hello 상관 관계 ID를 포함 하십시오.</span><span class="sxs-lookup"><span data-stu-id="cda5c-249">Please include hello correlation ID from hello error message.</span></span>

## <a name="manual-installation"></a><span data-ttu-id="cda5c-250">수동 설치</span><span class="sxs-lookup"><span data-stu-id="cda5c-250">Manual installation</span></span>

<span data-ttu-id="cda5c-251">Hello 프로파일러를 구성 하는 경우 hello 다음 업데이트가 이루어지는 toohello 웹 앱 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-251">When you configure hello profiler, hello following updates are made toohello Web App's settings.</span></span> <span data-ttu-id="cda5c-252">환경에 필요한 경우, 예를 들어 응용 프로그램이 ASE(Azure App Service Environment)에서 실행되는 경우 이 작업을 수동으로 직접 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-252">You can do them yourself manually if your environment requires, for example, if your application runs in Azure App Service Environment (ASE):</span></span>

1. <span data-ttu-id="cda5c-253">웹 응용 프로그램 제어 블레이드에서 hello 설정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-253">In hello web app control blade, open Settings.</span></span>
2. <span data-ttu-id="cda5c-254">설정 ".NET Framework 버전" toov4.6 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-254">Set ".Net Framework version" toov4.6.</span></span>
3. <span data-ttu-id="cda5c-255">"Always On" tooOn를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-255">Set "Always On" tooOn.</span></span>
4. <span data-ttu-id="cda5c-256">응용 프로그램 설정을 추가 "__APPINSIGHTS_INSTRUMENTATIONKEY__" 및 집합 hello 값 toohello hello SDK에서 사용 하는 동일한 계측 키입니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-256">Add app setting "__APPINSIGHTS_INSTRUMENTATIONKEY__" and set hello value toohello same instrumentation key used by hello SDK.</span></span>
5. <span data-ttu-id="cda5c-257">고급 도구를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-257">Open Advanced Tools.</span></span>
6. <span data-ttu-id="cda5c-258">Tooopen hello Kudu 웹 사이트 "Go"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-258">Click "Go" tooopen hello Kudu website.</span></span>
7. <span data-ttu-id="cda5c-259">Hello Kudu 웹 사이트에서 "사이트 확장"을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-259">In hello Kudu website, select "Site extensions".</span></span>
8. <span data-ttu-id="cda5c-260">갤러리에서 “__Application Insights__”를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-260">Install "__Application Insights__" from Gallery.</span></span>
9. <span data-ttu-id="cda5c-261">Hello 웹 응용 프로그램을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-261">Restart hello web app.</span></span>

## <span data-ttu-id="cda5c-262"><a id="aspnetcore"></a>ASP.NET Core 지원</span><span class="sxs-lookup"><span data-stu-id="cda5c-262"><a id="aspnetcore"></a>ASP.NET Core Support</span></span>

<span data-ttu-id="cda5c-263">ASP.NET Core 응용 tooinstall Microsoft.ApplicationInsights.AspNetCore Nuget 패키지 2.1.0-beta6 또는 더 높은 toowork hello 프로파일러로 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-263">ASP.NET Core application needs tooinstall Microsoft.ApplicationInsights.AspNetCore Nuget package 2.1.0-beta6 or higher toowork with hello Profiler.</span></span> <span data-ttu-id="cda5c-264">더 이상 후 2017/6/27 hello 더 낮은 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cda5c-264">We no longer support hello lower versions after 6/27/2017.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cda5c-265">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cda5c-265">Next steps</span></span>

* [<span data-ttu-id="cda5c-266">Visual Studio에서 Application Insights로 작업</span><span class="sxs-lookup"><span data-stu-id="cda5c-266">Working with Application Insights in Visual Studio</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-visual-studio)

[performance-blade]: ./media/app-insights-profiler/performance-blade.png
[performance-blade-examples]: ./media/app-insights-profiler/performance-blade-examples.png
[trace-explorer]: ./media/app-insights-profiler/trace-explorer.png
[trace-explorer-toolbar]: ./media/app-insights-profiler/trace-explorer-toolbar.png
[trace-explorer-hint-tip]: ./media/app-insights-profiler/trace-explorer-hint-tip.png
[trace-explorer-hot-path]: ./media/app-insights-profiler/trace-explorer-hot-path.png
[enable-profiler-banner]: ./media/app-insights-profiler/enable-profiler-banner.png
[disable-profiler-webjob]: ./media/app-insights-profiler/disable-profiler-webjob.png
[linked app services]: ./media/app-insights-profiler/linked-app-services.png

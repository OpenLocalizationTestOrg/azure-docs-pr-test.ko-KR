---
title: "Azure Application Insights에서 Docker 응용 프로그램 모니터링 | Microsoft Docs"
description: "Docker 성능 카운터, 이벤트 및 예외는 컨테이너식 앱에서 보낸 원격 분석과 함께 Application Insights에 표시될 수 있습니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: b082e345ca1bb3b12c548e05e699474d3aa9306c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a><span data-ttu-id="6239b-103">Application Insights에서 Docker 응용 프로그램 모니터링</span><span class="sxs-lookup"><span data-stu-id="6239b-103">Monitor Docker applications in Application Insights</span></span>
<span data-ttu-id="6239b-104">[Docker](https://www.docker.com/) 컨테이너의 수명 주기 이벤트 및 성능 카운터를 Application Insights에서 차트로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span></span> <span data-ttu-id="6239b-105">호스트의 컨테이너에 [Application Insights](app-insights-overview.md) 이미지를 설치하면 호스트는 물론 다른 이미지에 대한 성능 카운터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-105">Install the [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for the host, as well as for the other images.</span></span>

<span data-ttu-id="6239b-106">Docker를 사용하여 모든 종속성이 포함된 경량 컨테이너에 앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span></span> <span data-ttu-id="6239b-107">Docker 엔진을 실행하는 모든 호스트 컴퓨터에서 앱이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-107">They'll run on any host machine that runs a Docker Engine.</span></span>

<span data-ttu-id="6239b-108">Docker 호스트에서 [Application Insights 이미지](https://hub.docker.com/r/microsoft/applicationinsights/)를 실행하면 다음과 같은 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-108">When you run the [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span></span>

* <span data-ttu-id="6239b-109">호스트에서 실행하는 모든 컨테이너에 대한 수명 주기 원격 분석 – 시작, 중지 등</span><span class="sxs-lookup"><span data-stu-id="6239b-109">Lifecycle telemetry about all the containers running on the host - start, stop, and so on.</span></span>
* <span data-ttu-id="6239b-110">모든 컨테이너에 대한 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="6239b-110">Performance counters for all the containers.</span></span> <span data-ttu-id="6239b-111">CPU, 메모리, 네트워크 사용량 외 다수</span><span class="sxs-lookup"><span data-stu-id="6239b-111">CPU, memory, network usage, and more.</span></span>
* <span data-ttu-id="6239b-112">컨테이너에서 실행되는 앱에 [Java용 Application Insights SDK를 설치하면](app-insights-java-live.md) 해당 앱에 대한 모든 원격 분석에 컨테이너와 호스트 컴퓨터를 식별하는 추가적인 속성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in the apps running in the containers, all the telemetry of those apps will have additional properties identifying the container and host machine.</span></span> <span data-ttu-id="6239b-113">예를 들어 둘 이상의 호스트에서 실행되는 앱 인스턴스가 있다면 앱 원격 분석을 호스트별로 쉽게 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span></span>

![예제](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a><span data-ttu-id="6239b-115">Application Insights 리소스 설정</span><span class="sxs-lookup"><span data-stu-id="6239b-115">Set up your Application Insights resource</span></span>
1. <span data-ttu-id="6239b-116">[Microsoft Azure Portal](https://azure.com)에 로그인하고 앱에 대한 Application Insights 리소스를 열거나 [새 리소스를 만듭니다](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="6239b-116">Sign into [Microsoft Azure portal](https://azure.com) and open the Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span></span> 
   
    <span data-ttu-id="6239b-117">*어떤 리소스를 사용해야 하나요?*</span><span class="sxs-lookup"><span data-stu-id="6239b-117">*Which resource should I use?*</span></span> <span data-ttu-id="6239b-118">호스트에서 실행하는 앱을 다른 사람이 개발한 경우에는 [새로운 Application Insights 리소스를 만들어야 합니다](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="6239b-118">If the apps that you are running on your host were developed by someone else, then you need to [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="6239b-119">이 리소스에서 원격 분석을 보고 분석하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-119">This is where you view and analyze the telemetry.</span></span> <span data-ttu-id="6239b-120">(앱 형식에 대해 '일반'을 선택합니다.)</span><span class="sxs-lookup"><span data-stu-id="6239b-120">(Select 'General' for the app type.)</span></span>
   
    <span data-ttu-id="6239b-121">해당 앱의 개발자인 경우에는 각 앱에 [Application Insights SDK를 추가](app-insights-java-live.md) 하셨기를 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-121">But if you're the developer of the apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) to each of them.</span></span> <span data-ttu-id="6239b-122">실제로 모든 리소스가 단일 비즈니스 응용 프로그램의 구성 요소라면, 하나의 리소스에 원격 분석을 보내도록 모든 리소스를 구성하고, 동일한 리소스를 사용하여 Docker 수명 주기 및 성능 데이터를 표시하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-122">If they're all really components of a single business application, then you might configure all of them to send telemetry to one resource, and you'll use that same resource to display the Docker lifecycle and performance data.</span></span> 
   
    <span data-ttu-id="6239b-123">세 번째 시나리오는 사용자가 대부분의 앱을 개발했지만 별도의 리소스를 사용하여 앱의 원격 분석을 나타내는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-123">A third scenario is that you developed most of the apps, but you are using separate resources to display their telemetry.</span></span> <span data-ttu-id="6239b-124">대개 이런 경우에는 Docker 데이터에 대해서도 별도의 리소스를 만들려고 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-124">In that case, you probably also want to create a separate resource for the Docker data.</span></span> 
2. <span data-ttu-id="6239b-125">Docker 타일을 추가합니다. **타일 추가**를 선택하고 갤러리에서 Docker 타일을 끌어다 놓은 후 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-125">Add the Docker tile: Choose **Add Tile**, drag the Docker tile from the gallery, and then click **Done**.</span></span> 
   
    ![예제](./media/app-insights-docker/03.png)
3. <span data-ttu-id="6239b-127">**Essentials** 드롭다운을 클릭하고 계측 키를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-127">Click the **Essentials** drop-down and copy the Instrumentation Key.</span></span> <span data-ttu-id="6239b-128">이 키를 사용하여 SDK에 원격 분석을 보낼 위치를 알립니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-128">You use this to tell the SDK where to send its telemetry.</span></span>

    ![예제](./media/app-insights-docker/02-props.png)

<span data-ttu-id="6239b-130">원격 분석을 확인하기 위해 곧 돌아와야 하므로 해당 브라우저 창을 열어둡니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-130">Keep that browser window handy, as you'll come back to it soon to look at your telemetry.</span></span>

## <a name="run-the-application-insights-monitor-on-your-host"></a><span data-ttu-id="6239b-131">호스트에서 Application Insights 모니터링 실행</span><span class="sxs-lookup"><span data-stu-id="6239b-131">Run the Application Insights monitor on your host</span></span>
<span data-ttu-id="6239b-132">원격 분석을 표시할 위치를 확보했으니, 원격 분석 데이터를 수집하고 보낼 컨테이너식 앱을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-132">Now that you've got somewhere to display the telemetry, you can set up the containerized app that will collect and send it.</span></span>

1. <span data-ttu-id="6239b-133">Docker 호스트에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-133">Connect to your Docker host.</span></span> 
2. <span data-ttu-id="6239b-134">계측 키를 아래 명령에 넣어 편집하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-134">Edit your instrumentation key into this command, and then run it:</span></span>
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

<span data-ttu-id="6239b-135">Application Insights 이미지는 Docker 호스트당 하나만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-135">Only one Application Insights image is required per Docker host.</span></span> <span data-ttu-id="6239b-136">응용 프로그램을 여러 개의 Docker 호스트에 표시하는 경우, 이 명령을 호스트마다 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-136">If your application is deployed on multiple Docker hosts, then repeat the command on every host.</span></span>

## <a name="update-your-app"></a><span data-ttu-id="6239b-137">앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="6239b-137">Update your app</span></span>
<span data-ttu-id="6239b-138">응용 프로그램이 [Java용 Application Insights SDK](app-insights-java-get-started.md)를 사용하여 계측되는 경우에는, 프로젝트의 ApplicationInsights.xml 파일에서 `<TelemetryInitializers>` 요소 아래에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-138">If your application is instrumented with the [Application Insights SDK for Java](app-insights-java-get-started.md), add the following line into the ApplicationInsights.xml file in your project, under the `<TelemetryInitializers>` element:</span></span>

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

<span data-ttu-id="6239b-139">이것은 앱에서 보내는 모든 원격 분석 항목에 컨테이너 및 호스트 ID 같은 Docker 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-139">This adds Docker information such as container and host id to every telemetry item sent from your app.</span></span>

## <a name="view-your-telemetry"></a><span data-ttu-id="6239b-140">원격 분석 보기</span><span class="sxs-lookup"><span data-stu-id="6239b-140">View your telemetry</span></span>
<span data-ttu-id="6239b-141">Azure 포털에서 Application Insights 리소스로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-141">Go back to your Application Insights resource in the Azure portal.</span></span>

<span data-ttu-id="6239b-142">Docker 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-142">Click through the Docker tile.</span></span>

<span data-ttu-id="6239b-143">특히 Docker 엔진에서 다른 컨테이너가 실행되고 있는 경우 Docker 앱에서 데이터가 도착하는 것을 곧 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-143">You'll shortly see data arriving from the Docker app, especially if you have other containers running on your Docker engine.</span></span>

<span data-ttu-id="6239b-144">다음은 표시될 수 있는 몇 가지 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-144">Here are some of the views you can get.</span></span>

### <a name="perf-counters-by-host-activity-by-image"></a><span data-ttu-id="6239b-145">호스트별 성능 카운터, 이미지별 활동</span><span class="sxs-lookup"><span data-stu-id="6239b-145">Perf counters by host, activity by image</span></span>
![예제](./media/app-insights-docker/10.png)

![예제](./media/app-insights-docker/11.png)

<span data-ttu-id="6239b-148">자세한 내용을 보려면 호스트 또는 이미지 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-148">Click any host or image name for more detail.</span></span>

<span data-ttu-id="6239b-149">보기를 사용자 지정하려면 차트, 그리드 제목을 차례로 클릭하거나 차트 추가를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-149">To customize the view, click any chart, the grid heading, or use Add Chart.</span></span> 

<span data-ttu-id="6239b-150">[메트릭 탐색기에 대해 자세히 알아봅니다](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="6239b-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span></span>

### <a name="docker-container-events"></a><span data-ttu-id="6239b-151">Docker 컨테이너 이벤트</span><span class="sxs-lookup"><span data-stu-id="6239b-151">Docker container events</span></span>
![예제](./media/app-insights-docker/13.png)

<span data-ttu-id="6239b-153">개별 이벤트를 조사하려면 [검색](app-insights-diagnostic-search.md)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-153">To investigate individual events, click [Search](app-insights-diagnostic-search.md).</span></span> <span data-ttu-id="6239b-154">검색 및 필터링하여 원하는 이벤트를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-154">Search and filter to find the events you want.</span></span> <span data-ttu-id="6239b-155">자세한 내용을 보려면 이벤트를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-155">Click any event to get more detail.</span></span>

### <a name="exceptions-by-container-name"></a><span data-ttu-id="6239b-156">컨테이너 이름별 예외</span><span class="sxs-lookup"><span data-stu-id="6239b-156">Exceptions by container name</span></span>
![예제](./media/app-insights-docker/14.png)

### <a name="docker-context-added-to-app-telemetry"></a><span data-ttu-id="6239b-158">앱 원격 분석에 추가되는 Docker 컨텍스트</span><span class="sxs-lookup"><span data-stu-id="6239b-158">Docker context added to app telemetry</span></span>
<span data-ttu-id="6239b-159">AI SDK를 사용하여 계측되는 응용 프로그램에서 보내는 요청 원격 분석은 Docker 컨텍스트를 사용하여 보강됩니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-159">Request telemetry sent from the application instrumented with AI SDK, enriched with Docker context:</span></span>

![예제](./media/app-insights-docker/16.png)

<span data-ttu-id="6239b-161">프로세서 시간 및 사용 가능한 메모리 성능 카운터는 Docker 컨테이너 이름으로 그룹화되고 보강됩니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span></span>

![예제](./media/app-insights-docker/15.png)

## <a name="q--a"></a><span data-ttu-id="6239b-163">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="6239b-163">Q & A</span></span>
<span data-ttu-id="6239b-164">*Docker에서 얻을 수 없는 어떤 기능을 Application Insights가 제공하나요?*</span><span class="sxs-lookup"><span data-stu-id="6239b-164">*What does Application Insights give me that I can't get from Docker?*</span></span>

* <span data-ttu-id="6239b-165">컨테이너 및 이미지별로 성능 카운터의 자세한 분석 결과를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-165">Detailed breakdown of performance counters by container and image.</span></span>
* <span data-ttu-id="6239b-166">하나의 대시보드에서 컨테이너 및 앱 데이터를 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-166">Integrate container and app data in one dashboard.</span></span>
* <span data-ttu-id="6239b-167">[원격 분석을 내보냅니다](app-insights-export-telemetry.md) .</span><span class="sxs-lookup"><span data-stu-id="6239b-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis to a database, Power BI or other dashboard.</span></span>

<span data-ttu-id="6239b-168">*앱 자체에서 원격 분석을 가져오려면 어떻게 해야 하나요?*</span><span class="sxs-lookup"><span data-stu-id="6239b-168">*How do I get telemetry from the app itself?*</span></span>

* <span data-ttu-id="6239b-169">Application Insights SDK를 앱에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-169">Install the Application Insights SDK in the app.</span></span> <span data-ttu-id="6239b-170">[Java 웹앱](app-insights-java-get-started.md), [Windows 웹앱](app-insights-asp-net.md)에 대한 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6239b-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span></span>

## <a name="video"></a><span data-ttu-id="6239b-171">비디오</span><span class="sxs-lookup"><span data-stu-id="6239b-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="6239b-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6239b-172">Next steps</span></span>

* [<span data-ttu-id="6239b-173">Java용 Application Insights</span><span class="sxs-lookup"><span data-stu-id="6239b-173">Application Insights for Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="6239b-174">Node.js용 Application Insights</span><span class="sxs-lookup"><span data-stu-id="6239b-174">Application Insights for Node.js</span></span>](app-insights-nodejs.md)
* [<span data-ttu-id="6239b-175">ASP.NET용 Application Insights</span><span class="sxs-lookup"><span data-stu-id="6239b-175">Application Insights for ASP.NET</span></span>](app-insights-asp-net.md)

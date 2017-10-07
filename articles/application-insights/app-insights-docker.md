---
title: "Azure Application Insights에서 aaaMonitor Docker 응용 프로그램 | Microsoft Docs"
description: "Docker 성능 카운터, 이벤트 및 예외 hello 컨테이너 화 가능한 응용 프로그램에서 원격 분석 hello 함께 Application Insights에 표시할 수 있습니다."
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
ms.openlocfilehash: 9aaf1076bae25485a396db1bb3dcd13bccd87c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a><span data-ttu-id="3aef8-103">Application Insights에서 Docker 응용 프로그램 모니터링</span><span class="sxs-lookup"><span data-stu-id="3aef8-103">Monitor Docker applications in Application Insights</span></span>
<span data-ttu-id="3aef8-104">[Docker](https://www.docker.com/) 컨테이너의 수명 주기 이벤트 및 성능 카운터를 Application Insights에서 차트로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span></span> <span data-ttu-id="3aef8-105">Hello 설치 [Application Insights](app-insights-overview.md) hello 다른 이미지도로 대 한 호스트에 컨테이너의 이미지 hello 호스트에 대 한 성능 카운터 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-105">Install hello [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for hello host, as well as for hello other images.</span></span>

<span data-ttu-id="3aef8-106">Docker를 사용하여 모든 종속성이 포함된 경량 컨테이너에 앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span></span> <span data-ttu-id="3aef8-107">Docker 엔진을 실행하는 모든 호스트 컴퓨터에서 앱이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-107">They'll run on any host machine that runs a Docker Engine.</span></span>

<span data-ttu-id="3aef8-108">Hello를 실행 하는 경우 [Application Insights 이미지](https://hub.docker.com/r/microsoft/applicationinsights/) Docker 호스트에 이러한 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-108">When you run hello [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span></span>

* <span data-ttu-id="3aef8-109">실행 되는 모든 hello 컨테이너에 대 한 원격 분석 수명 주기-hello 호스트에서 시작, 중지 및 등입니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-109">Lifecycle telemetry about all hello containers running on hello host - start, stop, and so on.</span></span>
* <span data-ttu-id="3aef8-110">모든 hello 컨테이너에 대 한 성능 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-110">Performance counters for all hello containers.</span></span> <span data-ttu-id="3aef8-111">CPU, 메모리, 네트워크 사용량 외 다수</span><span class="sxs-lookup"><span data-stu-id="3aef8-111">CPU, memory, network usage, and more.</span></span>
* <span data-ttu-id="3aef8-112">경우 있습니다 [Java 용 Application Insights SDK를 설치](app-insights-java-live.md) hello hello 컨테이너에서 실행 중인 앱에서이 앱의 모든 hello 원격 분석 hello 컨테이너와 호스트 컴퓨터를 식별 하는 추가 속성이 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in hello apps running in hello containers, all hello telemetry of those apps will have additional properties identifying hello container and host machine.</span></span> <span data-ttu-id="3aef8-113">예를 들어 둘 이상의 호스트에서 실행되는 앱 인스턴스가 있다면 앱 원격 분석을 호스트별로 쉽게 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span></span>

![예제](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a><span data-ttu-id="3aef8-115">Application Insights 리소스 설정</span><span class="sxs-lookup"><span data-stu-id="3aef8-115">Set up your Application Insights resource</span></span>
1. <span data-ttu-id="3aef8-116">에 로그인 [Microsoft Azure 포털](https://azure.com) hello Application Insights 리소스 앱;에 대 한 열 및 또는 [새로 만들](app-insights-create-new-resource.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-116">Sign into [Microsoft Azure portal](https://azure.com) and open hello Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span></span> 
   
    <span data-ttu-id="3aef8-117">*어떤 리소스를 사용해야 하나요?*</span><span class="sxs-lookup"><span data-stu-id="3aef8-117">*Which resource should I use?*</span></span> <span data-ttu-id="3aef8-118">다른 사용자가 호스트에서 실행 중인 hello 앱 개발 된 경우 너무 필요한[새 Application Insights 리소스 만들기](app-insights-create-new-resource.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-118">If hello apps that you are running on your host were developed by someone else, then you need too[create a new Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="3aef8-119">보고와 분석 hello 원격 분석입니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-119">This is where you view and analyze hello telemetry.</span></span> <span data-ttu-id="3aef8-120">('일반' hello 앱 형식에 대 한 선택.)</span><span class="sxs-lookup"><span data-stu-id="3aef8-120">(Select 'General' for hello app type.)</span></span>
   
    <span data-ttu-id="3aef8-121">Hello 앱의 hello 개발자 인 경우 다음 경험을 있습니다 하지만 [Application Insights SDK 추가](app-insights-java-live.md) 그중에서 tooeach 합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-121">But if you're hello developer of hello apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) tooeach of them.</span></span> <span data-ttu-id="3aef8-122">경우 실제로의 모든 구성 요소는 단일 비즈니스 응용 프로그램 모두 toosend 원격 분석 tooone 리소스를 구성할 수 있습니다 하 고이 리소스 toodisplay hello Docker 수명 주기 및 성능 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-122">If they're all really components of a single business application, then you might configure all of them toosend telemetry tooone resource, and you'll use that same resource toodisplay hello Docker lifecycle and performance data.</span></span> 
   
    <span data-ttu-id="3aef8-123">세 번째 시나리오는 대부분의 hello 앱을 개발 하지만 사용 하는 별도 리소스 toodisplay 해당 원격 분석입니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-123">A third scenario is that you developed most of hello apps, but you are using separate resources toodisplay their telemetry.</span></span> <span data-ttu-id="3aef8-124">이 경우 있습니다 것도 원하는 toocreate hello Docker 데이터에 대 한 별도 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-124">In that case, you probably also want toocreate a separate resource for hello Docker data.</span></span> 
2. <span data-ttu-id="3aef8-125">Hello Docker 타일 추가: 선택 **타일 추가**hello Docker 타일 hello 갤러리에서 끌어 놓은 다음 클릭 **수행**합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-125">Add hello Docker tile: Choose **Add Tile**, drag hello Docker tile from hello gallery, and then click **Done**.</span></span> 
   
    ![예제](./media/app-insights-docker/03.png)
3. <span data-ttu-id="3aef8-127">Hello 클릭 **Essentials** 드롭 다운 및 hello 계측 키를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-127">Click hello **Essentials** drop-down and copy hello Instrumentation Key.</span></span> <span data-ttu-id="3aef8-128">이 tootell hello SDK를 사용 하 여 여기서 toosend 해당 원격 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-128">You use this tootell hello SDK where toosend its telemetry.</span></span>

    ![예제](./media/app-insights-docker/02-props.png)

<span data-ttu-id="3aef8-130">브라우저 창을 편리 하므로 계속 하면 다시 돌아오겠습니다 tooit 곧 toolook 원격 분석에서.</span><span class="sxs-lookup"><span data-stu-id="3aef8-130">Keep that browser window handy, as you'll come back tooit soon toolook at your telemetry.</span></span>

## <a name="run-hello-application-insights-monitor-on-your-host"></a><span data-ttu-id="3aef8-131">호스트에서 hello Application Insights 모니터 실행</span><span class="sxs-lookup"><span data-stu-id="3aef8-131">Run hello Application Insights monitor on your host</span></span>
<span data-ttu-id="3aef8-132">이제를 가져온 위치 toodisplay hello 원격 분석을 수집 하 고 보낼 됩니다는 hello 컨테이너 화 된 앱을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-132">Now that you've got somewhere toodisplay hello telemetry, you can set up hello containerized app that will collect and send it.</span></span>

1. <span data-ttu-id="3aef8-133">Tooyour Docker 호스트를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-133">Connect tooyour Docker host.</span></span> 
2. <span data-ttu-id="3aef8-134">계측 키를 아래 명령에 넣어 편집하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-134">Edit your instrumentation key into this command, and then run it:</span></span>
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

<span data-ttu-id="3aef8-135">Application Insights 이미지는 Docker 호스트당 하나만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-135">Only one Application Insights image is required per Docker host.</span></span> <span data-ttu-id="3aef8-136">다음 응용 프로그램을 여러 Docker 호스트에 배포 된 경우에 모든 호스트에 hello 명령을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-136">If your application is deployed on multiple Docker hosts, then repeat hello command on every host.</span></span>

## <a name="update-your-app"></a><span data-ttu-id="3aef8-137">앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="3aef8-137">Update your app</span></span>
<span data-ttu-id="3aef8-138">Hello로 응용 프로그램 파일을 계측 하는 경우 [Java 용 Application Insights SDK](app-insights-java-get-started.md), hello hello에서 프로젝트의 hello ApplicationInsights.xml 파일에 다음 줄 추가 `<TelemetryInitializers>` 요소:</span><span class="sxs-lookup"><span data-stu-id="3aef8-138">If your application is instrumented with hello [Application Insights SDK for Java](app-insights-java-get-started.md), add hello following line into hello ApplicationInsights.xml file in your project, under hello `<TelemetryInitializers>` element:</span></span>

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

<span data-ttu-id="3aef8-139">이 컨테이너와 호스트 id tooevery 원격 분석 항목 응용 프로그램에서 보낸 같은 Docker 정보를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-139">This adds Docker information such as container and host id tooevery telemetry item sent from your app.</span></span>

## <a name="view-your-telemetry"></a><span data-ttu-id="3aef8-140">원격 분석 보기</span><span class="sxs-lookup"><span data-stu-id="3aef8-140">View your telemetry</span></span>
<span data-ttu-id="3aef8-141">Hello Azure 포털에서에서 tooyour Application Insights 리소스를 다시 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-141">Go back tooyour Application Insights resource in hello Azure portal.</span></span>

<span data-ttu-id="3aef8-142">Hello Docker 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-142">Click through hello Docker tile.</span></span>

<span data-ttu-id="3aef8-143">Docker 엔진에서 실행 되는 기타 컨테이너가 있는 경우에 특히 곧 hello Docker 앱에서 데이터를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-143">You'll shortly see data arriving from hello Docker app, especially if you have other containers running on your Docker engine.</span></span>

<span data-ttu-id="3aef8-144">다음은 몇 hello 보기를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-144">Here are some of hello views you can get.</span></span>

### <a name="perf-counters-by-host-activity-by-image"></a><span data-ttu-id="3aef8-145">호스트별 성능 카운터, 이미지별 활동</span><span class="sxs-lookup"><span data-stu-id="3aef8-145">Perf counters by host, activity by image</span></span>
![예제](./media/app-insights-docker/10.png)

![예제](./media/app-insights-docker/11.png)

<span data-ttu-id="3aef8-148">자세한 내용을 보려면 호스트 또는 이미지 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-148">Click any host or image name for more detail.</span></span>

<span data-ttu-id="3aef8-149">toocustomize hello 뷰는 모든 차트, hello 표 머리글을 클릭 또는 추가 차트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-149">toocustomize hello view, click any chart, hello grid heading, or use Add Chart.</span></span> 

<span data-ttu-id="3aef8-150">[메트릭 탐색기에 대해 자세히 알아봅니다](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="3aef8-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span></span>

### <a name="docker-container-events"></a><span data-ttu-id="3aef8-151">Docker 컨테이너 이벤트</span><span class="sxs-lookup"><span data-stu-id="3aef8-151">Docker container events</span></span>
![예제](./media/app-insights-docker/13.png)

<span data-ttu-id="3aef8-153">tooinvestigate 개별 이벤트를 클릭 하 여 [검색](app-insights-diagnostic-search.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-153">tooinvestigate individual events, click [Search](app-insights-diagnostic-search.md).</span></span> <span data-ttu-id="3aef8-154">검색 하 고 원하는 toofind hello 이벤트를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-154">Search and filter toofind hello events you want.</span></span> <span data-ttu-id="3aef8-155">모든 이벤트 tooget 자세히를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-155">Click any event tooget more detail.</span></span>

### <a name="exceptions-by-container-name"></a><span data-ttu-id="3aef8-156">컨테이너 이름별 예외</span><span class="sxs-lookup"><span data-stu-id="3aef8-156">Exceptions by container name</span></span>
![예제](./media/app-insights-docker/14.png)

### <a name="docker-context-added-tooapp-telemetry"></a><span data-ttu-id="3aef8-158">Docker 컨텍스트 tooapp 원격 분석 추가</span><span class="sxs-lookup"><span data-stu-id="3aef8-158">Docker context added tooapp telemetry</span></span>
<span data-ttu-id="3aef8-159">원격 분석 정보와 함께 AI SDK, Docker 컨텍스트를 제공 하도록 향상 hello 응용 프로그램에서 보낸 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-159">Request telemetry sent from hello application instrumented with AI SDK, enriched with Docker context:</span></span>

![예제](./media/app-insights-docker/16.png)

<span data-ttu-id="3aef8-161">프로세서 시간 및 사용 가능한 메모리 성능 카운터는 Docker 컨테이너 이름으로 그룹화되고 보강됩니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span></span>

![예제](./media/app-insights-docker/15.png)

## <a name="q--a"></a><span data-ttu-id="3aef8-163">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="3aef8-163">Q & A</span></span>
<span data-ttu-id="3aef8-164">*Docker에서 얻을 수 없는 어떤 기능을 Application Insights가 제공하나요?*</span><span class="sxs-lookup"><span data-stu-id="3aef8-164">*What does Application Insights give me that I can't get from Docker?*</span></span>

* <span data-ttu-id="3aef8-165">컨테이너 및 이미지별로 성능 카운터의 자세한 분석 결과를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-165">Detailed breakdown of performance counters by container and image.</span></span>
* <span data-ttu-id="3aef8-166">하나의 대시보드에서 컨테이너 및 앱 데이터를 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-166">Integrate container and app data in one dashboard.</span></span>
* <span data-ttu-id="3aef8-167">[원격 분석 내보낼](app-insights-export-telemetry.md) 추가 분석 tooa 데이터베이스, Power BI 또는 다른 대시보드에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis tooa database, Power BI or other dashboard.</span></span>

<span data-ttu-id="3aef8-168">*Hello 앱 자체에서 원격 분석 가져오기*</span><span class="sxs-lookup"><span data-stu-id="3aef8-168">*How do I get telemetry from hello app itself?*</span></span>

* <span data-ttu-id="3aef8-169">Hello 응용 프로그램에서 hello Application Insights SDK를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-169">Install hello Application Insights SDK in hello app.</span></span> <span data-ttu-id="3aef8-170">[Java 웹앱](app-insights-java-get-started.md), [Windows 웹앱](app-insights-asp-net.md)에 대한 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3aef8-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span></span>

## <a name="video"></a><span data-ttu-id="3aef8-171">비디오</span><span class="sxs-lookup"><span data-stu-id="3aef8-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="3aef8-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3aef8-172">Next steps</span></span>

* [<span data-ttu-id="3aef8-173">Java용 Application Insights</span><span class="sxs-lookup"><span data-stu-id="3aef8-173">Application Insights for Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="3aef8-174">Node.js용 Application Insights</span><span class="sxs-lookup"><span data-stu-id="3aef8-174">Application Insights for Node.js</span></span>](app-insights-nodejs.md)
* [<span data-ttu-id="3aef8-175">ASP.NET용 Application Insights</span><span class="sxs-lookup"><span data-stu-id="3aef8-175">Application Insights for ASP.NET</span></span>](app-insights-asp-net.md)

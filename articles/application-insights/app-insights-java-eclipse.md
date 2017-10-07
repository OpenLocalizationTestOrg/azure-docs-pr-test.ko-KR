---
title: "Eclipse에서 Java 통해 Azure Application Insights 시작 aaaGet | Microsoft docs"
description: "Hello Eclipse 플러그 인 tooadd 성능 및 사용량 Application Insights를 사용한 tooyour Java 웹 사이트 모니터링을 사용 하 여"
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: e88c9f53-cd90-4abc-b097-1f170937908e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: 3142a26a9e2d14c2c433882e3d337f2a8c8f2247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a><span data-ttu-id="891d5-103">Eclipse에서 Java를 사용하여 Application Insights 시작하기</span><span class="sxs-lookup"><span data-stu-id="891d5-103">Get started with Application Insights with Java in Eclipse</span></span>
<span data-ttu-id="891d5-104">Application Insights SDK hello 사용과 성능을 분석할 수 있도록 Java 웹 응용 프로그램에서 원격 분석을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-104">hello Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span></span> <span data-ttu-id="891d5-105">hello Eclipse Application Insights에 대 한 플러그 인에 자동으로 설치 hello SDK 프로젝트 hello 상자 원격 분석 및 toowrite 사용자 지정 원격 분석을 사용할 수 있는 API에서 얻을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-105">hello Eclipse plug-in for Application Insights automatically installs hello SDK in your project so that you get out of hello box telemetry, plus an API that you can use toowrite custom telemetry.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="891d5-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="891d5-106">Prerequisites</span></span>
<span data-ttu-id="891d5-107">현재 Maven 프로젝트와 Eclipse에서 동적 웹 프로젝트에 대 한 hello 플러그 인 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-107">Currently hello plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span></span>
<span data-ttu-id="891d5-108">([Application Insights 추가 tooother 유형의 Java 프로젝트][java].)</span><span class="sxs-lookup"><span data-stu-id="891d5-108">([Add Application Insights tooother types of Java project][java].)</span></span>

<span data-ttu-id="891d5-109">필요한 사항:</span><span class="sxs-lookup"><span data-stu-id="891d5-109">You'll need:</span></span>

* <span data-ttu-id="891d5-110">Oracle JRE 1.6 이상</span><span class="sxs-lookup"><span data-stu-id="891d5-110">Oracle JRE 1.6 or later</span></span>
* <span data-ttu-id="891d5-111">구독 너무[Microsoft Azure](https://azure.microsoft.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-111">A subscription too[Microsoft Azure](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="891d5-112">[Java EE Developers용 Eclipse IDE](http://www.eclipse.org/downloads/), Indigo 이상.</span><span class="sxs-lookup"><span data-stu-id="891d5-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span></span>
* <span data-ttu-id="891d5-113">Windows 7 이상 또는 Windows Server 2008 이상</span><span class="sxs-lookup"><span data-stu-id="891d5-113">Windows 7 or later, or Windows Server 2008 or later</span></span>

## <a name="install-hello-sdk-on-eclipse-one-time"></a><span data-ttu-id="891d5-114">Eclipse (한 번)에 hello SDK를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-114">Install hello SDK on Eclipse (one time)</span></span>
<span data-ttu-id="891d5-115">하기만 하면 toodo 컴퓨터 마다 한 번씩이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-115">You only have toodo this one time per machine.</span></span> <span data-ttu-id="891d5-116">이 단계는 hello SDK tooeach 동적 웹 프로젝트를 추가할 수 있는 도구 키트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-116">This step installs a toolkit which can then add hello SDK tooeach Dynamic Web Project.</span></span>

1. <span data-ttu-id="891d5-117">Eclipse에서 도움말, 새 소프트웨어 설치를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-117">In Eclipse, click Help, Install New Software.</span></span>

    ![도움말, 새 소프트웨어 설치](./media/app-insights-java-eclipse/0-plugin.png)
2. <span data-ttu-id="891d5-119">Azure 도구 키트에서 http://dl.microsoft.com/eclipse hello SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-119">hello SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span></span>
3. <span data-ttu-id="891d5-120">**모든 업데이트 사이트 문의...**</span><span class="sxs-lookup"><span data-stu-id="891d5-120">Uncheck **Contact all update sites...**</span></span>

    ![Application Insights SDK의 경우 모든 업데이트 사이트 문의 지우기](./media/app-insights-java-eclipse/1-plugin.png)

<span data-ttu-id="891d5-122">Hello 남아 있는 각 Java 프로젝트에 대 한 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-122">Follow hello remaining steps for each Java project.</span></span>

## <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="891d5-123">Azure에서 Application Insights 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="891d5-123">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="891d5-124">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="891d5-125">새 Application Insights 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-125">Create a new Application Insights resource.</span></span> <span data-ttu-id="891d5-126">Hello 응용 프로그램 종류 tooJava 웹 응용 프로그램을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-126">Set hello application type tooJava web application.</span></span>  

    ![+를 클릭하고 Application Insights 선택](./media/app-insights-java-eclipse/01-create.png)  

4. <span data-ttu-id="891d5-128">Hello 새 리소스의 계측 키를 hello를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-128">Find hello instrumentation key of hello new resource.</span></span> <span data-ttu-id="891d5-129">이것이 필요 합니다 toopaste 코드 프로젝트에 곧 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-129">You'll need toopaste this into your code project shortly.</span></span>  

    ![새 리소스 개요 hello에서에서 속성을 클릭 하 고 hello 계측 키 복사](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-tooyour-project"></a><span data-ttu-id="891d5-131">Application Insights tooyour 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="891d5-131">Add Application Insights tooyour project</span></span>
1. <span data-ttu-id="891d5-132">Java 웹 프로젝트의 hello 상황에 맞는 메뉴에서 Application Insights를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-132">Add Application Insights from hello context menu of your Java web project.</span></span>

    ![새 리소스 개요 hello에서에서 속성을 클릭 하 고 hello 계측 키 복사](./media/app-insights-java-eclipse/02-context-menu.png)
2. <span data-ttu-id="891d5-134">Hello Azure 포털에서에서 가져온 hello 계측 키를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-134">Paste hello instrumentation key that you got from hello Azure portal.</span></span>

    ![새 리소스 개요 hello에서에서 속성을 클릭 하 고 hello 계측 키 복사](./media/app-insights-java-eclipse/03-ikey.png)

<span data-ttu-id="891d5-136">hello 키 원격 분석의 모든 항목이 함께 전송 되 고 Application Insights toodisplay 지시, 리소스에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-136">hello key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>

## <a name="run-hello-application-and-see-metrics"></a><span data-ttu-id="891d5-137">Hello 응용 프로그램을 실행 하 고 메트릭을 확인합니다</span><span class="sxs-lookup"><span data-stu-id="891d5-137">Run hello application and see metrics</span></span>
<span data-ttu-id="891d5-138">응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-138">Run your application.</span></span>

<span data-ttu-id="891d5-139">Microsoft Azure에서 tooyour Application Insights 리소스를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-139">Return tooyour Application Insights resource in Microsoft Azure.</span></span>

<span data-ttu-id="891d5-140">HTTP 요청 데이터는 hello 개요 블레이드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-140">HTTP requests data will appear on hello overview blade.</span></span> <span data-ttu-id="891d5-141">(없는 경우 몇 초 정도 기다린 다음 새로고침을 클릭합니다.)</span><span class="sxs-lookup"><span data-stu-id="891d5-141">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![<span data-ttu-id="891d5-142">서버 응답, 요청 횟수 및 오류</span><span class="sxs-lookup"><span data-stu-id="891d5-142">Server response, request counts, and failures</span></span> ](./media/app-insights-java-eclipse/5-results.png)

<span data-ttu-id="891d5-143">클릭 하 여 더 자세한 메트릭을 통해 모든 차트 toosee 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-143">Click through any chart toosee more detailed metrics.</span></span>

![이름별 요청 수](./media/app-insights-java-eclipse/6-barchart.png)

<span data-ttu-id="891d5-145">[메트릭에 대해 자세히 알아봅니다.][metrics]</span><span class="sxs-lookup"><span data-stu-id="891d5-145">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="891d5-146">요청 hello 속성을 볼 때 요청 및 예외와 같은 연관 된 hello 원격 분석 이벤트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-146">And when viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![이 요청에 대한 모든 추적](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a><span data-ttu-id="891d5-148">클라이언트쪽 원격 분석</span><span class="sxs-lookup"><span data-stu-id="891d5-148">Client-side telemetry</span></span>
<span data-ttu-id="891d5-149">Hello 빠른 시작 블레이드에서 Get 코드 toomonitor 내 웹 페이지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-149">From hello QuickStart blade, click Get code toomonitor my web pages:</span></span>

![응용 프로그램 개요 블레이드를 사용 하 여 빠른 시작을 선택에서 내 웹 페이지 코드 toomonitor 가져오기 합니다.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

<span data-ttu-id="891d5-152">HTML 파일을 hello 헤드에서 hello 코드 조각을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-152">Insert hello code snippet in hello head of your HTML files.</span></span>

#### <a name="view-client-side-data"></a><span data-ttu-id="891d5-153">클라이언트쪽 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="891d5-153">View client-side data</span></span>
<span data-ttu-id="891d5-154">업데이트 된 웹 페이지를 열고 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-154">Open your updated web pages and use them.</span></span> <span data-ttu-id="891d5-155">를 2 분 정도로 기다립니다 다음 tooApplication Insights 및 열기 hello 사용 블레이드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-155">Wait a minute or two, then return tooApplication Insights and open hello usage blade.</span></span> <span data-ttu-id="891d5-156">(Hello 개요 블레이드에서 아래로 스크롤하여 사용을 클릭 합니다.)</span><span class="sxs-lookup"><span data-stu-id="891d5-156">(From hello Overview blade, scroll down and click Usage.)</span></span>

<span data-ttu-id="891d5-157">페이지 보기, 사용자 및 세션 메트릭 hello 사용 블레이드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-157">Page view, user, and session metrics will appear on hello usage blade:</span></span>

![세션, 사용자 및 페이지 보기](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

<span data-ttu-id="891d5-159">[클라이언트 쪽 원격 분석 설정에 대해 자세히 알아봅니다.][usage]</span><span class="sxs-lookup"><span data-stu-id="891d5-159">[Learn more about setting up client-side telemetry.][usage]</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="891d5-160">응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="891d5-160">Publish your application</span></span>
<span data-ttu-id="891d5-161">이제 앱 toohello 서버를 게시, 사용자가을 사용 하 고 hello 포털에 표시 하는 hello 원격 분석을 조사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-161">Now publish your app toohello server, let people use it, and watch hello telemetry show up on hello portal.</span></span>

* <span data-ttu-id="891d5-162">방화벽이 허용 응용 프로그램 toosend 원격 분석 toothese 포트 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-162">Make sure your firewall allows your application toosend telemetry toothese ports:</span></span>

  * <span data-ttu-id="891d5-163">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="891d5-163">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="891d5-164">dc.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="891d5-164">dc.services.visualstudio.com:80</span></span>
  * <span data-ttu-id="891d5-165">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="891d5-165">f5.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="891d5-166">f5.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="891d5-166">f5.services.visualstudio.com:80</span></span>
* <span data-ttu-id="891d5-167">Windows 서버에 다음을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-167">On Windows servers, install:</span></span>

  * [<span data-ttu-id="891d5-168">Microsoft Visual C++ 재배포 가능 패키지</span><span class="sxs-lookup"><span data-stu-id="891d5-168">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="891d5-169">(이를 통해 성능 카운터를 사용할 수 있게 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="891d5-169">(This enables performance counters.)</span></span>

## <a name="exceptions-and-request-failures"></a><span data-ttu-id="891d5-170">예외 및 요청 실패</span><span class="sxs-lookup"><span data-stu-id="891d5-170">Exceptions and request failures</span></span>
<span data-ttu-id="891d5-171">처리되지 않은 예외는 자동으로 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-171">Unhandled exceptions are automatically collected:</span></span>

![](./media/app-insights-java-eclipse/21-exceptions.png)

<span data-ttu-id="891d5-172">다른 예외에서 toocollect 데이터를 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-172">toocollect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="891d5-173">[코드에서 tooTrackException를 호출 하는 insert](app-insights-api-custom-events-metrics.md#trackexception)합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-173">[Insert calls tooTrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span></span>
* <span data-ttu-id="891d5-174">[서버에 hello Java 에이전트 설치](app-insights-java-agent.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-174">[Install hello Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="891d5-175">Toowatch hello 메서드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-175">You specify hello methods you want toowatch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="891d5-176">메서드 호출 및 외부 종속성 모니터링</span><span class="sxs-lookup"><span data-stu-id="891d5-176">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="891d5-177">[Hello Java 에이전트 설치](app-insights-java-agent.md) toolog 지정 내부 메서드 및 타이밍 데이터와 함께 JDBC를 통해 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-177">[Install hello Java Agent](app-insights-java-agent.md) toolog specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="891d5-178">성능 카운터</span><span class="sxs-lookup"><span data-stu-id="891d5-178">Performance counters</span></span>
<span data-ttu-id="891d5-179">개요 블레이드에서 아래로 스크롤하여 클릭 hello **서버** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-179">On your Overview blade, scroll down and click hello  **Servers** tile.</span></span> <span data-ttu-id="891d5-180">다양한 성능 카운터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-180">You'll see a range of performance counters.</span></span>

![Tooclick hello 서버 타일 아래로 스크롤](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="891d5-182">성능 카운터 수집 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="891d5-182">Customize performance counter collection</span></span>
<span data-ttu-id="891d5-183">hello 표준 성능 카운터 집합의 toodisable 컬렉션 hello 코드 hello ApplicationInsights.xml 파일의 hello 루트 노드 아래에서 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-183">toodisable collection of hello standard set of performance counters, add hello following code under hello root node of hello ApplicationInsights.xml file:</span></span>

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="891d5-184">추가 성능 카운터 수집</span><span class="sxs-lookup"><span data-stu-id="891d5-184">Collect additional performance counters</span></span>
<span data-ttu-id="891d5-185">추가 성능 카운터 toobe 수집된을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-185">You can specify additional performance counters toobe collected.</span></span>

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a><span data-ttu-id="891d5-186">JMX 카운터 (hello Java 가상 컴퓨터에 의해 노출 됨)</span><span class="sxs-lookup"><span data-stu-id="891d5-186">JMX counters (exposed by hello Java Virtual Machine)</span></span>

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="891d5-187">`displayName`– hello Application Insights 포털에 표시 된 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-187">`displayName` – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="891d5-188">`objectName`– hello JMX 개체 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-188">`objectName` – hello JMX object name.</span></span>
* <span data-ttu-id="891d5-189">`attribute`– hello JMX 개체 이름 toofetch hello 특성</span><span class="sxs-lookup"><span data-stu-id="891d5-189">`attribute` – hello attribute of hello JMX object name toofetch</span></span>
* <span data-ttu-id="891d5-190">`type`(선택 사항)-JMX 개체의 특성 유형의 hello:</span><span class="sxs-lookup"><span data-stu-id="891d5-190">`type` (optional) - hello type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="891d5-191">기본값: int 또는 long과 같은 단순 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-191">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="891d5-192">`composite`: hello 성능 카운터 데이터는 'Attribute.Data' hello 형식으로 되어</span><span class="sxs-lookup"><span data-stu-id="891d5-192">`composite`: hello perf counter data is in hello format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="891d5-193">`tabular`: hello 성능 카운터 데이터는 테이블 행의 hello 형식</span><span class="sxs-lookup"><span data-stu-id="891d5-193">`tabular`: hello perf counter data is in hello format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="891d5-194">Windows 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="891d5-194">Windows performance counters</span></span>
<span data-ttu-id="891d5-195">각 [Windows 성능 카운터](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) 범주의 멤버인 (hello에서 필드는 클래스의 멤버가 동일한 방식으로).</span><span class="sxs-lookup"><span data-stu-id="891d5-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in hello same way that a field is a member of a class).</span></span> <span data-ttu-id="891d5-196">범주는 전역일 수 있으며, 번호 또는 이름이 지정된 인스턴스를 가질 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-196">Categories can either be global, or can have numbered or named instances.</span></span>

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="891d5-197">displayName hello Application Insights 포털에 표시 된 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-197">displayName – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="891d5-198">categoryName hello 성능 카운터 범주 (성능 개체)이 성능 카운터와 관련 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-198">categoryName – hello performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="891d5-199">counterName hello 성능 카운터의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-199">counterName – hello name of hello performance counter.</span></span>
* <span data-ttu-id="891d5-200">-instanceName hello hello 성능 카운터 범주 인스턴스 이름, 또는 빈 문자열 ("") hello 범주에는 단일 인스턴스가 포함 된 경우.</span><span class="sxs-lookup"><span data-stu-id="891d5-200">instanceName – hello name of hello performance counter category instance, or an empty string (""), if hello category contains a single instance.</span></span> <span data-ttu-id="891d5-201">Hello categoryName 프로세스, and toocollect 원하는 성능 카운터를 hello hello 현재 JVM 프로세스에서 실행 중인 앱을 지정 `"__SELF__"`합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-201">If hello categoryName is Process, and hello performance counter you'd like toocollect is from hello current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="891d5-202">성능 카운터에서가 [메트릭 탐색기][metrics]에서 사용자 지정 메트릭으로 보입니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="891d5-203">Unix 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="891d5-203">Unix performance counters</span></span>
* <span data-ttu-id="891d5-204">[Collectd hello Application Insights 플러그 인 설치](app-insights-java-collectd.md) tooget 다양 한 시스템 및 네트워크 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-204">[Install collectd with hello Application Insights plugin](app-insights-java-collectd.md) tooget a wide variety of system and network data.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="891d5-205">가용성 웹 테스트</span><span class="sxs-lookup"><span data-stu-id="891d5-205">Availability web tests</span></span>
<span data-ttu-id="891d5-206">Application Insights는 사용자가 정기적으로 toocheck 및 잘 응답에서 웹 사이트를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-206">Application Insights can test your website at regular intervals toocheck that it's up and responding well.</span></span> <span data-ttu-id="891d5-207">[tooset][availability], tooclick 가용성 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-207">[tooset up][availability], scroll down tooclick Availability.</span></span>

![아래로 스크롤하여 가용성, 추가 웹 테스트를 차례로 클릭](./media/app-insights-java-eclipse/31-config-web-test.png)

<span data-ttu-id="891d5-209">사이트가 다운되는 경우 응답 시간 차트는 물론 이메일 알림을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-209">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![웹 테스트의 예](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

<span data-ttu-id="891d5-211">[가용성 웹 테스트에 대한 자세히 알아봅니다.][availability]</span><span class="sxs-lookup"><span data-stu-id="891d5-211">[Learn more about availability web tests.][availability]</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="891d5-212">진단 로그</span><span class="sxs-lookup"><span data-stu-id="891d5-212">Diagnostic logs</span></span>
<span data-ttu-id="891d5-213">Log4J 또는 Logback을 사용 중인 경우 (v 1.2 또는 v2.0) 추적을 위한 tooApplication Insights 탐색 하 고 검색 하 수를 자동으로 전송 하 여 추적 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically tooApplication Insights where you can explore and search on them.</span></span>

<span data-ttu-id="891d5-214">[진단 로그에 대해 자세히 알아보기][javalogs]</span><span class="sxs-lookup"><span data-stu-id="891d5-214">[Learn more about diagnostic logs][javalogs]</span></span>

## <a name="custom-telemetry"></a><span data-ttu-id="891d5-215">사용자 지정 원격 분석</span><span class="sxs-lookup"><span data-stu-id="891d5-215">Custom telemetry</span></span>
<span data-ttu-id="891d5-216">함께 수행 하는 사용자가 out는 Java 웹 응용 프로그램 toofind에 몇 줄의 코드를 넣거나 toohelp 문제를 진단 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-216">Insert a few lines of code in your Java web application toofind out what users are doing with it or toohelp diagnose problems.</span></span>

<span data-ttu-id="891d5-217">JavaScript 웹 페이지와 hello 서버 쪽 java에서 코드를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-217">You can insert code both in web page JavaScript and in hello server-side Java.</span></span>

<span data-ttu-id="891d5-218">[사용자 지정 원격 분석에 대해 자세히 알아보기][track]</span><span class="sxs-lookup"><span data-stu-id="891d5-218">[Learn about custom telemetry][track]</span></span>

## <a name="next-steps"></a><span data-ttu-id="891d5-219">다음 단계</span><span class="sxs-lookup"><span data-stu-id="891d5-219">Next steps</span></span>
#### <a name="detect-and-diagnose-issues"></a><span data-ttu-id="891d5-220">문제 감지 및 진단</span><span class="sxs-lookup"><span data-stu-id="891d5-220">Detect and diagnose issues</span></span>
* <span data-ttu-id="891d5-221">[웹 클라이언트 원격 분석 추가] [ usage] hello 웹 클라이언트에서 tooget 성능 원격 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-221">[Add web client telemetry][usage] tooget performance telemetry from hello web client.</span></span>
* <span data-ttu-id="891d5-222">[웹 테스트 설정] [ availability] toomake 라이브 및 응답성이 뛰어난 응용 프로그램 없이 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-222">[Set up web tests][availability] toomake sure your application stays live and responsive.</span></span>
* <span data-ttu-id="891d5-223">[이벤트 및 로그를 검색할] [ diagnostic] toohelp 문제를 진단 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-223">[Search events and logs][diagnostic] toohelp diagnose problems.</span></span>
* <span data-ttu-id="891d5-224">[Log4J 또는 Logback 추적 캡처][javalogs]</span><span class="sxs-lookup"><span data-stu-id="891d5-224">[Capture Log4J or Logback traces][javalogs]</span></span>

#### <a name="track-usage"></a><span data-ttu-id="891d5-225">사용 현황 추적</span><span class="sxs-lookup"><span data-stu-id="891d5-225">Track usage</span></span>
* <span data-ttu-id="891d5-226">[웹 클라이언트 원격 분석 추가] [ usage] 뷰와 기본 사용자 메트릭을 toomonitor 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-226">[Add web client telemetry][usage] toomonitor page views and basic user metrics.</span></span>
* <span data-ttu-id="891d5-227">[사용자 지정 이벤트 및 메트릭을 추적](app-insights-web-track-usage.md) toolearn 응용 프로그램 사용량, hello 클라이언트와 서버 hello에 모두에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="891d5-227">[Track custom events and metrics](app-insights-web-track-usage.md) toolearn about how your application is used, both at hello client and hello server.</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

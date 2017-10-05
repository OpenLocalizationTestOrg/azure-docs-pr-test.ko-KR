---
title: "Eclipse에서 Java를 사용하여 Application Insights 시작하기 | Microsoft 문서"
description: "Application Insights를 사용하여 성능 및 사용량 모니터링을 Java 웹 사이트에 추가하기 위해 Eclipse 플러그인을 사용합니다."
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
ms.openlocfilehash: f2f696a3bbe7893c1f521a3e5588f4f93805d6a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a><span data-ttu-id="cdf38-103">Eclipse에서 Java를 사용하여 Application Insights 시작하기</span><span class="sxs-lookup"><span data-stu-id="cdf38-103">Get started with Application Insights with Java in Eclipse</span></span>
<span data-ttu-id="cdf38-104">Application Insights SDK가 Java 웹 응용 프로그램에서 원격 분석을 전송하므로 사용량 및 성능을 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-104">The Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span></span> <span data-ttu-id="cdf38-105">Application Insights용 Eclipse 플러그인이 프로젝트에 SDK를 자동으로 설치하므로 기본 원격 분석을 이용할 수 있을 뿐 아니라 사용자 지정 원격 분석 작성에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-105">The Eclipse plug-in for Application Insights automatically installs the SDK in your project so that you get out of the box telemetry, plus an API that you can use to write custom telemetry.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="cdf38-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cdf38-106">Prerequisites</span></span>
<span data-ttu-id="cdf38-107">현재 플러그 인은 Eclipse에서 Maven 프로젝트 및 동적 웹 프로젝트에 대해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-107">Currently the plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span></span>
<span data-ttu-id="cdf38-108">([다른 유형의 Java 프로젝트에 Application Insights를 추가합니다][java].)</span><span class="sxs-lookup"><span data-stu-id="cdf38-108">([Add Application Insights to other types of Java project][java].)</span></span>

<span data-ttu-id="cdf38-109">필요한 사항:</span><span class="sxs-lookup"><span data-stu-id="cdf38-109">You'll need:</span></span>

* <span data-ttu-id="cdf38-110">Oracle JRE 1.6 이상</span><span class="sxs-lookup"><span data-stu-id="cdf38-110">Oracle JRE 1.6 or later</span></span>
* <span data-ttu-id="cdf38-111">[Microsoft Azure](https://azure.microsoft.com/)구독.</span><span class="sxs-lookup"><span data-stu-id="cdf38-111">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="cdf38-112">[Java EE Developers용 Eclipse IDE](http://www.eclipse.org/downloads/), Indigo 이상.</span><span class="sxs-lookup"><span data-stu-id="cdf38-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span></span>
* <span data-ttu-id="cdf38-113">Windows 7 이상 또는 Windows Server 2008 이상</span><span class="sxs-lookup"><span data-stu-id="cdf38-113">Windows 7 or later, or Windows Server 2008 or later</span></span>

## <a name="install-the-sdk-on-eclipse-one-time"></a><span data-ttu-id="cdf38-114">Eclipse에 SDK를 설치합니다(한 번).</span><span class="sxs-lookup"><span data-stu-id="cdf38-114">Install the SDK on Eclipse (one time)</span></span>
<span data-ttu-id="cdf38-115">컴퓨터당 한 번씩만 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-115">You only have to do this one time per machine.</span></span> <span data-ttu-id="cdf38-116">이 단계는 SDK를 각 동적 웹 프로젝트에 추가할 수 있는 도구 키트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-116">This step installs a toolkit which can then add the SDK to each Dynamic Web Project.</span></span>

1. <span data-ttu-id="cdf38-117">Eclipse에서 도움말, 새 소프트웨어 설치를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-117">In Eclipse, click Help, Install New Software.</span></span>

    ![도움말, 새 소프트웨어 설치](./media/app-insights-java-eclipse/0-plugin.png)
2. <span data-ttu-id="cdf38-119">SDK는 http://dl.microsoft.com/eclipse의 Azure 도구 키트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-119">The SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span></span>
3. <span data-ttu-id="cdf38-120">**모든 업데이트 사이트 문의...**</span><span class="sxs-lookup"><span data-stu-id="cdf38-120">Uncheck **Contact all update sites...**</span></span>

    ![Application Insights SDK의 경우 모든 업데이트 사이트 문의 지우기](./media/app-insights-java-eclipse/1-plugin.png)

<span data-ttu-id="cdf38-122">각 Java 프로젝트에 대한 나머지 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-122">Follow the remaining steps for each Java project.</span></span>

## <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="cdf38-123">Azure에서 Application Insights 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="cdf38-123">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="cdf38-124">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cdf38-125">새 Application Insights 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-125">Create a new Application Insights resource.</span></span> <span data-ttu-id="cdf38-126">Java 웹 응용 프로그램에 대한 응용 프로그램 종류를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-126">Set the application type to Java web application.</span></span>  

    ![+를 클릭하고 Application Insights 선택](./media/app-insights-java-eclipse/01-create.png)  

4. <span data-ttu-id="cdf38-128">새 리소스의 계측 키를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-128">Find the instrumentation key of the new resource.</span></span> <span data-ttu-id="cdf38-129">코드 프로젝트에 곧바로 붙여넣어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-129">You'll need to paste this into your code project shortly.</span></span>  

    ![새 리소스 개요에서 속성을 클릭하고 계측 키 복사](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-to-your-project"></a><span data-ttu-id="cdf38-131">프로젝트에 Application Insights 추가</span><span class="sxs-lookup"><span data-stu-id="cdf38-131">Add Application Insights to your project</span></span>
1. <span data-ttu-id="cdf38-132">Java 웹 프로젝트의 상황에 맞는 메뉴에서 Application Insights를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-132">Add Application Insights from the context menu of your Java web project.</span></span>

    ![새 리소스 개요에서 속성을 클릭하고 계측 키 복사](./media/app-insights-java-eclipse/02-context-menu.png)
2. <span data-ttu-id="cdf38-134">Azure 포털에서 가져온 계측 키를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-134">Paste the instrumentation key that you got from the Azure portal.</span></span>

    ![새 리소스 개요에서 속성을 클릭하고 계측 키 복사](./media/app-insights-java-eclipse/03-ikey.png)

<span data-ttu-id="cdf38-136">키는 원격 분석의 모든 항목과 함께 전송되고 리소스에서 표시하도록 Application Insights에 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-136">The key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>

## <a name="run-the-application-and-see-metrics"></a><span data-ttu-id="cdf38-137">응용 프로그램을 실행하고 메트릭을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdf38-137">Run the application and see metrics</span></span>
<span data-ttu-id="cdf38-138">응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-138">Run your application.</span></span>

<span data-ttu-id="cdf38-139">Microsoft Azure에서 Application Insights 리소스로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-139">Return to your Application Insights resource in Microsoft Azure.</span></span>

<span data-ttu-id="cdf38-140">HTTP 요청 데이터가 개요 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-140">HTTP requests data will appear on the overview blade.</span></span> <span data-ttu-id="cdf38-141">(없는 경우 몇 초 정도 기다린 다음 새로고침을 클릭합니다.)</span><span class="sxs-lookup"><span data-stu-id="cdf38-141">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![<span data-ttu-id="cdf38-142">서버 응답, 요청 횟수 및 오류</span><span class="sxs-lookup"><span data-stu-id="cdf38-142">Server response, request counts, and failures</span></span> ](./media/app-insights-java-eclipse/5-results.png)

<span data-ttu-id="cdf38-143">차트를 클릭하면 더 자세한 메트릭을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-143">Click through any chart to see more detailed metrics.</span></span>

![이름별 요청 수](./media/app-insights-java-eclipse/6-barchart.png)

<span data-ttu-id="cdf38-145">[메트릭에 대해 자세히 알아봅니다.][metrics]</span><span class="sxs-lookup"><span data-stu-id="cdf38-145">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="cdf38-146">또한 요청 속성 검토 시 요청 및 예외 사항과 관련된 원격 분석 이벤트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![이 요청에 대한 모든 추적](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a><span data-ttu-id="cdf38-148">클라이언트쪽 원격 분석</span><span class="sxs-lookup"><span data-stu-id="cdf38-148">Client-side telemetry</span></span>
<span data-ttu-id="cdf38-149">빠른 시작 블레이드에서 내 웹 페이지를 모니터링하는 코트 가져오기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-149">From the QuickStart blade, click Get code to monitor my web pages:</span></span>

![앱 개요 블레이드에서 빠른 시작, 내 웹 페이지를 모니터링할 코드 가져오기를 선택합니다.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

<span data-ttu-id="cdf38-152">HTML 파일의 헤드에 있는 코드 조각을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-152">Insert the code snippet in the head of your HTML files.</span></span>

#### <a name="view-client-side-data"></a><span data-ttu-id="cdf38-153">클라이언트쪽 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="cdf38-153">View client-side data</span></span>
<span data-ttu-id="cdf38-154">업데이트 된 웹 페이지를 열고 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-154">Open your updated web pages and use them.</span></span> <span data-ttu-id="cdf38-155">1~2분 정도 기다린 후, Application Insights로 돌아가 사용량 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-155">Wait a minute or two, then return to Application Insights and open the usage blade.</span></span> <span data-ttu-id="cdf38-156">(개요 블레이드에서 아래로 스크롤하고 사용량을 클릭합니다.)</span><span class="sxs-lookup"><span data-stu-id="cdf38-156">(From the Overview blade, scroll down and click Usage.)</span></span>

<span data-ttu-id="cdf38-157">페이지 보기, 사용자 및 세션 메트릭이 사용량 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-157">Page view, user, and session metrics will appear on the usage blade:</span></span>

![세션, 사용자 및 페이지 보기](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

<span data-ttu-id="cdf38-159">[클라이언트 쪽 원격 분석 설정에 대해 자세히 알아봅니다.][usage]</span><span class="sxs-lookup"><span data-stu-id="cdf38-159">[Learn more about setting up client-side telemetry.][usage]</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="cdf38-160">응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="cdf38-160">Publish your application</span></span>
<span data-ttu-id="cdf38-161">이제 서버에 앱을 게시하고, 사람들이 사용하게 한 다음 포털에 표시되는 원격 분석을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-161">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span></span>

* <span data-ttu-id="cdf38-162">방화벽에서 응용 프로그램이 다음 포트에 원격 분석을 보내도록 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-162">Make sure your firewall allows your application to send telemetry to these ports:</span></span>

  * <span data-ttu-id="cdf38-163">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="cdf38-163">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="cdf38-164">dc.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="cdf38-164">dc.services.visualstudio.com:80</span></span>
  * <span data-ttu-id="cdf38-165">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="cdf38-165">f5.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="cdf38-166">f5.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="cdf38-166">f5.services.visualstudio.com:80</span></span>
* <span data-ttu-id="cdf38-167">Windows 서버에 다음을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-167">On Windows servers, install:</span></span>

  * [<span data-ttu-id="cdf38-168">Microsoft Visual C++ 재배포 가능 패키지</span><span class="sxs-lookup"><span data-stu-id="cdf38-168">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="cdf38-169">(이를 통해 성능 카운터를 사용할 수 있게 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="cdf38-169">(This enables performance counters.)</span></span>

## <a name="exceptions-and-request-failures"></a><span data-ttu-id="cdf38-170">예외 및 요청 실패</span><span class="sxs-lookup"><span data-stu-id="cdf38-170">Exceptions and request failures</span></span>
<span data-ttu-id="cdf38-171">처리되지 않은 예외는 자동으로 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-171">Unhandled exceptions are automatically collected:</span></span>

![](./media/app-insights-java-eclipse/21-exceptions.png)

<span data-ttu-id="cdf38-172">다른 예외에 대한 데이터를 수집하려면 다음 두 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-172">To collect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="cdf38-173">[사용자 코드에 TrackException에 대한 호출 삽입](app-insights-api-custom-events-metrics.md#trackexception)</span><span class="sxs-lookup"><span data-stu-id="cdf38-173">[Insert calls to TrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span></span>
* <span data-ttu-id="cdf38-174">[서버에 Java 에이전트를 설치합니다](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="cdf38-174">[Install the Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="cdf38-175">감시 방법을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-175">You specify the methods you want to watch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="cdf38-176">메서드 호출 및 외부 종속성 모니터링</span><span class="sxs-lookup"><span data-stu-id="cdf38-176">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="cdf38-177">[Java 에이전트를 설치](app-insights-java-agent.md) 하여 지정된 내부 메서드 및 JDBC를 통해 수행한 호출을 타이밍 데이터와 함께 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-177">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="cdf38-178">성능 카운터</span><span class="sxs-lookup"><span data-stu-id="cdf38-178">Performance counters</span></span>
<span data-ttu-id="cdf38-179">개요 블레이드에서 아래로 스크롤하고 **서버** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-179">On your Overview blade, scroll down and click the  **Servers** tile.</span></span> <span data-ttu-id="cdf38-180">다양한 성능 카운터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-180">You'll see a range of performance counters.</span></span>

![아래로 스크롤하여 서버 타일 클릭](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="cdf38-182">성능 카운터 수집 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="cdf38-182">Customize performance counter collection</span></span>
<span data-ttu-id="cdf38-183">성능 카운터의 표준 집합 수집을 사용하지 않으려면 ApplicationInsights.xml 파일의 루트 노드 아래에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-183">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span></span>

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="cdf38-184">추가 성능 카운터 수집</span><span class="sxs-lookup"><span data-stu-id="cdf38-184">Collect additional performance counters</span></span>
<span data-ttu-id="cdf38-185">추가 성능 카운터가 수집되도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-185">You can specify additional performance counters to be collected.</span></span>

#### <a name="jmx-counters-exposed-by-the-java-virtual-machine"></a><span data-ttu-id="cdf38-186">JMX 카운터(Java 가상 컴퓨터를 통해 노출됨)</span><span class="sxs-lookup"><span data-stu-id="cdf38-186">JMX counters (exposed by the Java Virtual Machine)</span></span>

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="cdf38-187">`displayName` - Application Insights 포털에서 표시되는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-187">`displayName` – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="cdf38-188">`objectName` – JMX 개체 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-188">`objectName` – The JMX object name.</span></span>
* <span data-ttu-id="cdf38-189">`attribute` - 가져올 JMX 개체 이름의 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-189">`attribute` – The attribute of the JMX object name to fetch</span></span>
* <span data-ttu-id="cdf38-190">`type` (선택 사항) - JMX 개체 특성의 유형:</span><span class="sxs-lookup"><span data-stu-id="cdf38-190">`type` (optional) - The type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="cdf38-191">기본값: int 또는 long과 같은 단순 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-191">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="cdf38-192">`composite`: 성능 카운터 데이터는 'Attribute.Data' 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-192">`composite`: the perf counter data is in the format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="cdf38-193">`tabular`: 성능 카운터 데이터는 표 행 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-193">`tabular`: the perf counter data is in the format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="cdf38-194">Windows 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="cdf38-194">Windows performance counters</span></span>
<span data-ttu-id="cdf38-195">각 [Windows 성능 카운터](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) 는 한 범주의 구성원입니다(필드가 클래스의 구성원인 것과 동일한 방식).</span><span class="sxs-lookup"><span data-stu-id="cdf38-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span></span> <span data-ttu-id="cdf38-196">범주는 전역일 수 있으며, 번호 또는 이름이 지정된 인스턴스를 가질 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-196">Categories can either be global, or can have numbered or named instances.</span></span>

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="cdf38-197">displayName - Application Insights 포털에서 표시되는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-197">displayName – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="cdf38-198">categoryName – 이 성능 카운터와 관련된 성능 카운터 범주(성능 개체)입니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-198">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="cdf38-199">counterName – 성능 카운터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-199">counterName – The name of the performance counter.</span></span>
* <span data-ttu-id="cdf38-200">instanceName – 성능 카운터 범주 인스턴스입니다. 또는 범주가 단일 인스턴스를 포함하는 경우 빈 문자열("")의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-200">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span></span> <span data-ttu-id="cdf38-201">categoryName이 프로세스이며 수입하려는 성능 카운터는 앱이 실행 중인 현재 JVM 프로세스에서 오는 경우, `"__SELF__"`을(를) 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-201">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="cdf38-202">성능 카운터에서가 [메트릭 탐색기][metrics]에서 사용자 지정 메트릭으로 보입니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="cdf38-203">Unix 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="cdf38-203">Unix performance counters</span></span>
* <span data-ttu-id="cdf38-204">[Application Insights 플러그 인과 함께 collectd를 설치](app-insights-java-collectd.md) 하여 광범위한 시스템 및 네트워크 데이터를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-204">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="cdf38-205">가용성 웹 테스트</span><span class="sxs-lookup"><span data-stu-id="cdf38-205">Availability web tests</span></span>
<span data-ttu-id="cdf38-206">Application Insights는 일정한 간격으로 웹 사이트를 테스트하여 잘 실행되며 제대로 응답하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-206">Application Insights can test your website at regular intervals to check that it's up and responding well.</span></span> <span data-ttu-id="cdf38-207">[설정하려면][availability] 아래로 스크롤하여 가용성을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-207">[To set up][availability], scroll down to click Availability.</span></span>

![아래로 스크롤하여 가용성, 추가 웹 테스트를 차례로 클릭](./media/app-insights-java-eclipse/31-config-web-test.png)

<span data-ttu-id="cdf38-209">사이트가 다운되는 경우 응답 시간 차트는 물론 이메일 알림을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-209">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![웹 테스트의 예](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

<span data-ttu-id="cdf38-211">[가용성 웹 테스트에 대한 자세히 알아봅니다.][availability]</span><span class="sxs-lookup"><span data-stu-id="cdf38-211">[Learn more about availability web tests.][availability]</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="cdf38-212">진단 로그</span><span class="sxs-lookup"><span data-stu-id="cdf38-212">Diagnostic logs</span></span>
<span data-ttu-id="cdf38-213">추적에 Logback 또는 Log4J(v1.2 또는 v2.0)를 사용하는 경우 추적 로그를 탐색 및 검색할 수 있는 Application Insights에 추적 로그를 자동으로 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically to Application Insights where you can explore and search on them.</span></span>

<span data-ttu-id="cdf38-214">[진단 로그에 대해 자세히 알아보기][javalogs]</span><span class="sxs-lookup"><span data-stu-id="cdf38-214">[Learn more about diagnostic logs][javalogs]</span></span>

## <a name="custom-telemetry"></a><span data-ttu-id="cdf38-215">사용자 지정 원격 분석</span><span class="sxs-lookup"><span data-stu-id="cdf38-215">Custom telemetry</span></span>
<span data-ttu-id="cdf38-216">Java 웹 응용 프로그램에 몇 줄의 코드를 삽입하여 이를 사용하여 해당 작업을 수행하는 사용자를 확인하거나 진단 문제를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-216">Insert a few lines of code in your Java web application to find out what users are doing with it or to help diagnose problems.</span></span>

<span data-ttu-id="cdf38-217">웹 페이지 JavaScript와 서버쪽 Java에 모두 코드를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-217">You can insert code both in web page JavaScript and in the server-side Java.</span></span>

<span data-ttu-id="cdf38-218">[사용자 지정 원격 분석에 대해 자세히 알아보기][track]</span><span class="sxs-lookup"><span data-stu-id="cdf38-218">[Learn about custom telemetry][track]</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdf38-219">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cdf38-219">Next steps</span></span>
#### <a name="detect-and-diagnose-issues"></a><span data-ttu-id="cdf38-220">문제 감지 및 진단</span><span class="sxs-lookup"><span data-stu-id="cdf38-220">Detect and diagnose issues</span></span>
* <span data-ttu-id="cdf38-221">[웹 클라이언트 원격 분석을 추가][usage]하여 웹 클라이언트에서 성능 원격 분석을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-221">[Add web client telemetry][usage] to get performance telemetry from the web client.</span></span>
* <span data-ttu-id="cdf38-222">[웹 테스트를 설정][availability]하여 응용 프로그램이 라이브 상태로 유지되며 응답하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-222">[Set up web tests][availability] to make sure your application stays live and responsive.</span></span>
* <span data-ttu-id="cdf38-223">[이벤트 및 로그를 검색][diagnostic]하여 문제를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-223">[Search events and logs][diagnostic] to help diagnose problems.</span></span>
* <span data-ttu-id="cdf38-224">[Log4J 또는 Logback 추적 캡처][javalogs]</span><span class="sxs-lookup"><span data-stu-id="cdf38-224">[Capture Log4J or Logback traces][javalogs]</span></span>

#### <a name="track-usage"></a><span data-ttu-id="cdf38-225">사용 현황 추적</span><span class="sxs-lookup"><span data-stu-id="cdf38-225">Track usage</span></span>
* <span data-ttu-id="cdf38-226">[웹 클라이언트 원격 분석을 추가][usage]하여 페이지 보기 및 기본 사용자 메트릭을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-226">[Add web client telemetry][usage] to monitor page views and basic user metrics.</span></span>
* <span data-ttu-id="cdf38-227">[사용자 지정 이벤트 및 메트릭을 추적](app-insights-web-track-usage.md)하여 클라이언트와 서버에서 응용 프로그램이 어떻게 사용되는지 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf38-227">[Track custom events and metrics](app-insights-web-track-usage.md) to learn about how your application is used, both at the client and the server.</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

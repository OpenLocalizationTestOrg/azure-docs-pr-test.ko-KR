---
title: "Linux에서 Java 웹앱 성능 모니터링 - Azure | Microsoft Docs"
description: "Application Insights용 CollectD 플러그 인을 사용한 Java 웹 사이트의 포괄적인 응용 프로그램 성능 모니터링"
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 40c68f45-197a-4624-bf89-541eb7323002
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: 4ea917b068e0242bfb88d7357eca032607a43a3f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a><span data-ttu-id="e2a8d-103">collectd: Application Insights에서 Linux 성능 메트릭</span><span class="sxs-lookup"><span data-stu-id="e2a8d-103">collectd: Linux performance metrics in Application Insights</span></span>


<span data-ttu-id="e2a8d-104">Linux 시스템 성능 메트릭을[Application Insights](app-insights-overview.md)에서 탐색하려면 [collectd](http://collectd.org/)와 Application Insights 플러그 인을 함께 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-104">To explore Linux system performance metrics in [Application Insights](app-insights-overview.md), install [collectd](http://collectd.org/), together with its Application Insights plug-in.</span></span> <span data-ttu-id="e2a8d-105">이 오픈 소스 솔루션은 다양한 시스템 및 네트워크 통계를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-105">This open-source solution gathers various system and network statistics.</span></span>

<span data-ttu-id="e2a8d-106">이미 [Application Insights로 Java 웹 서비스를 계측][java]한 경우 일반적으로 collectd를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-106">Typically you'll use collectd if you have already [instrumented your Java web service with Application Insights][java].</span></span> <span data-ttu-id="e2a8d-107">앱의 성능을 향상시키거나 문제를 진단할 수 있도록 더 많은 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-107">It gives you more data to help you to enhance your app's performance or diagnose problems.</span></span> 

![예제 차트](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a><span data-ttu-id="e2a8d-109">계측 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="e2a8d-109">Get your instrumentation key</span></span>
<span data-ttu-id="e2a8d-110">[Microsoft Azure Portal](https://portal.azure.com)에서 데이터를 표시하고 싶은 [Application Insights](app-insights-overview.md) 리소스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-110">In the [Microsoft Azure portal](https://portal.azure.com), open the [Application Insights](app-insights-overview.md) resource where you want the data to appear.</span></span> <span data-ttu-id="e2a8d-111">(또는 [새 리소스를 만듭니다](app-insights-create-new-resource.md).)</span><span class="sxs-lookup"><span data-stu-id="e2a8d-111">(Or [create a new resource](app-insights-create-new-resource.md).)</span></span>

<span data-ttu-id="e2a8d-112">리소스를 식별하는 계측 키의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-112">Take a copy of the instrumentation key, which identifies the resource.</span></span>

![모두 찾아보고, 프로그램 리소스를 연 다음, Essentials 드롭다운 목록에서 계측 키 선택 및 복사](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-the-plug-in"></a><span data-ttu-id="e2a8d-114">Collectd 및 플러그인을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-114">Install collectd and the plug-in</span></span>
<span data-ttu-id="e2a8d-115">Linux 서버 컴퓨터에서:</span><span class="sxs-lookup"><span data-stu-id="e2a8d-115">On your Linux server machines:</span></span>

1. <span data-ttu-id="e2a8d-116">[collectd](http://collectd.org/) 5.4.0 버전 또는 그 이상을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-116">Install [collectd](http://collectd.org/) version 5.4.0 or later.</span></span>
2. <span data-ttu-id="e2a8d-117">[Application Insights collectd 기록기 플러그 인](https://aka.ms/aijavasdk)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-117">Download the [Application Insights collectd writer plugin](https://aka.ms/aijavasdk).</span></span> <span data-ttu-id="e2a8d-118">버전 번호를 메모합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-118">Note the version number.</span></span>
3. <span data-ttu-id="e2a8d-119">플러그인JAR를 `/usr/share/collectd/java`에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-119">Copy the plugin JAR into `/usr/share/collectd/java`.</span></span>
4. <span data-ttu-id="e2a8d-120">편집 `/etc/collectd/collectd.conf`:</span><span class="sxs-lookup"><span data-stu-id="e2a8d-120">Edit `/etc/collectd/collectd.conf`:</span></span>
   * <span data-ttu-id="e2a8d-121">[Java 플러그인](https://collectd.org/wiki/index.php/Plugin:Java) 사용하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-121">Ensure that [the Java plugin](https://collectd.org/wiki/index.php/Plugin:Java) is enabled.</span></span>
   * <span data-ttu-id="e2a8d-122">다음 JAR을 포함하는 java.class.path에 대한 JVMArg를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-122">Update the JVMArg for the java.class.path to include the following JAR.</span></span> <span data-ttu-id="e2a8d-123">다운로드 한 것과 일치하는 버전 번호를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-123">Update the version number to match the one you downloaded:</span></span>
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * <span data-ttu-id="e2a8d-124">리소스에서 계측 키를 사용하여 이 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-124">Add this snippet, using the Instrumentation Key from your resource:</span></span>

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

<span data-ttu-id="e2a8d-125">다음은 샘플 구성 파일의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-125">Here's part of a sample configuration file:</span></span>

```XML

    ...
    # collectd plugins
    LoadPlugin cpu
    LoadPlugin disk
    LoadPlugin load
    ...

    # Enable Java Plugin
    LoadPlugin "java"

    # Configure Java Plugin
    <Plugin "java">
      JVMArg "-verbose:jni"
      JVMArg "-Djava.class.path=/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar:/usr/share/collectd/java/collectd-api.jar"

      # Enabling Application Insights plugin
      LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"

      # Configuring Application Insights plugin
      <Plugin ApplicationInsightsWriter>
        InstrumentationKey "12345678-1234-1234-1234-123456781234"
      </Plugin>

      # Other plugin configurations ...
      ...
    </Plugin>
    ...
```

<span data-ttu-id="e2a8d-126">다른 [collectd 플러그인](https://collectd.org/wiki/index.php/Table_of_Plugins)을 구성하여 다른 원본에서 다양한 데이터를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-126">Configure other [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), which can collect various data from different sources.</span></span>

<span data-ttu-id="e2a8d-127">Collectd를 해당 [설명서](https://collectd.org/wiki/index.php/First_steps)에 따라서 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-127">Restart collectd according to its [manual](https://collectd.org/wiki/index.php/First_steps).</span></span>

## <a name="view-the-data-in-application-insights"></a><span data-ttu-id="e2a8d-128">Application Insights에서 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="e2a8d-128">View the data in Application Insights</span></span>
<span data-ttu-id="e2a8d-129">Application Insights 리소스에서 [메트릭 탐색기 및 차트 추가하기][metrics]를 열고, 사용자 지정 범주에서 보려는 메트릭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-129">In your Application Insights resource, open [Metrics Explorer and add charts][metrics], selecting the metrics you want to see from the Custom category.</span></span>

![](./media/app-insights-java-collectd/result.png)

<span data-ttu-id="e2a8d-130">기본적으로 메트릭을 수집한 모든 호트스 컴퓨터의 메트릭이 집계됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-130">By default, the metrics are aggregated across all host machines from which the metrics were collected.</span></span> <span data-ttu-id="e2a8d-131">차트 세부 정보 블레이드에서 호스트마다 메트릭을 보려면 그룹화를 설정하고 CollectD 호스트별로 그룹화를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-131">To view the metrics per host, in the Chart details blade, turn on Grouping and then choose to group by CollectD-Host.</span></span>

## <a name="to-exclude-upload-of-specific-statistics"></a><span data-ttu-id="e2a8d-132">특정 통계의 업로드를 제외하려면</span><span class="sxs-lookup"><span data-stu-id="e2a8d-132">To exclude upload of specific statistics</span></span>
<span data-ttu-id="e2a8d-133">기본적으로 Application Insights 플러그 인은 모든 사용할 수 있는 collectd ‘읽기’ 플러그 인에 의해 수집된 모든 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-133">By default, the Application Insights plugin sends all the data collected by all the enabled collectd 'read' plugins.</span></span> 

<span data-ttu-id="e2a8d-134">특정 플로그인 또는 데이터 소스의 데이터를 제외하려면:</span><span class="sxs-lookup"><span data-stu-id="e2a8d-134">To exclude data from specific plugins or data sources:</span></span>

* <span data-ttu-id="e2a8d-135">구성 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-135">Edit the configuration file.</span></span> 
* <span data-ttu-id="e2a8d-136">`<Plugin ApplicationInsightsWriter>`에서 다음과 같은 지시문 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-136">In `<Plugin ApplicationInsightsWriter>`, add directive lines like this:</span></span>

| <span data-ttu-id="e2a8d-137">지시문</span><span class="sxs-lookup"><span data-stu-id="e2a8d-137">Directive</span></span> | <span data-ttu-id="e2a8d-138">결과</span><span class="sxs-lookup"><span data-stu-id="e2a8d-138">Effect</span></span> |
| --- | --- |
| `Exclude disk` |<span data-ttu-id="e2a8d-139">`disk` 플러그인에 의해 수집된 모든 데이터를 제외</span><span class="sxs-lookup"><span data-stu-id="e2a8d-139">Exclude all data collected by the `disk` plugin</span></span> |
| `Exclude disk:read,write` |<span data-ttu-id="e2a8d-140">`disk` 플러그인에서 `read`과 `write`라고 명명된 원본을 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-140">Exclude the sources named `read` and `write` from the `disk` plugin.</span></span> |

<span data-ttu-id="e2a8d-141">새 줄을 포함한 별도 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-141">Separate directives with a newline.</span></span>

## <a name="problems"></a><span data-ttu-id="e2a8d-142">문제가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="e2a8d-142">Problems?</span></span>
<span data-ttu-id="e2a8d-143">*포털에 데이터가 표시되지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="e2a8d-143">*I don't see data in the portal*</span></span>

* <span data-ttu-id="e2a8d-144">[검색][diagnostic]을 열고 원시 이벤트가 도착했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-144">Open [Search][diagnostic] to see if the raw events have arrived.</span></span> <span data-ttu-id="e2a8d-145">때로는 메트릭 탐색기에 나타날 때 시간이 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-145">Sometimes they take longer to appear in metrics explorer.</span></span>
* <span data-ttu-id="e2a8d-146">[나가는 데이터에 대한 방화벽 예외를 설정](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="e2a8d-146">You might need to [set firewall exceptions for outgoing data](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="e2a8d-147">Application insights 플러그인에서 추적을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-147">Enable tracing in the Application Insights plugin.</span></span> <span data-ttu-id="e2a8d-148">`<Plugin ApplicationInsightsWriter>`에서 이 줄 추가:</span><span class="sxs-lookup"><span data-stu-id="e2a8d-148">Add this line within `<Plugin ApplicationInsightsWriter>`:</span></span>
  * `SDKLogger true`
* <span data-ttu-id="e2a8d-149">터미널을 열고 세부정보 표시 모드를 시작하여 어떤 문제가 보고되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-149">Open a terminal and start collectd in verbose mode, to see any issues it is reporting:</span></span>
  * `sudo collectd -f`

## <a name="known-issue"></a><span data-ttu-id="e2a8d-150">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="e2a8d-150">Known issue</span></span>

<span data-ttu-id="e2a8d-151">Application Insights 쓰기 플러그 인이 특정 읽기 플러그 인과 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-151">The Application Insights Write plugin is incompatible with certain Read plugins.</span></span> <span data-ttu-id="e2a8d-152">경우에 따라 일부 플러그 인은 Application Insights 플러그 인에서 부동 소수점 숫자를 예상하는 위치로 “NaN”를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-152">Some plugins sometimes send "NaN" where the Application Insights plugin expects a floating-point number.</span></span>

<span data-ttu-id="e2a8d-153">증상: 수집된 로그에 “AI: ... SyntaxError: 예기치 않은 토큰 N”을 포함하는 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-153">Symptom: The collectd log shows errors that include "AI: ... SyntaxError: Unexpected token N".</span></span>

<span data-ttu-id="e2a8d-154">해결 방법: 문제 쓰기 플러그 인에 의해 수집된 데이터를 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a8d-154">Workaround: Exclude data collected by the problem Write plugins.</span></span> 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md



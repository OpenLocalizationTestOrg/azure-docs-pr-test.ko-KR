---
title: "Java 웹 프로젝트에서 Application Insights 문제 해결"
description: "문제 해결 가이드 - Application Insights를 사용하여 라이브 Java 앱을 모니터링합니다."
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: ce46a4f561a273dc340b090a5bf0c8932a308722
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="6d8f5-103">Java용 Application Insights 문제 해결과 질문 및 답변</span><span class="sxs-lookup"><span data-stu-id="6d8f5-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="6d8f5-104">[Java의 Azure Application Insights][java]와 관련된 질문이나 문제가 있나요?</span><span class="sxs-lookup"><span data-stu-id="6d8f5-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="6d8f5-105">다음은 몇 가지 팁입니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="6d8f5-106">빌드 오류</span><span class="sxs-lookup"><span data-stu-id="6d8f5-106">Build errors</span></span>
<span data-ttu-id="6d8f5-107">**Eclipse에서 Maven 또는 Gradle을 통해 Application Insights SDK를 추가할 때 빌드 또는 체크섬 유효성 검사 오류가 표시됩니다.**</span><span class="sxs-lookup"><span data-stu-id="6d8f5-107">**In Eclipse, when adding the Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="6d8f5-108">종속성 <version> 요소가 와일드카드 문자가 포함된 패턴을 사용하는 경우(예: (Maven) `<version>[1.0,)</version>` 또는 (Gradle) `version:'1.0.+'`) `1.0.2`과 같이 특정 버전을 대신 지정해 보세요.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-108">If the dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span></span> <span data-ttu-id="6d8f5-109">최신 버전은 [릴리스 정보](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-109">See the [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for the latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="6d8f5-110">데이터 없음</span><span class="sxs-lookup"><span data-stu-id="6d8f5-110">No data</span></span>
<span data-ttu-id="6d8f5-111">**Application Insights를 추가하고 내 앱을 실행했는데 포털에 데이터가 표시되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="6d8f5-111">**I added Application Insights successfully and ran my app, but I've never seen data in the portal.**</span></span>

* <span data-ttu-id="6d8f5-112">잠시 기다린 후 새로 고침을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="6d8f5-113">차트는 주기적으로 새로 고쳐지지만 수동으로 새로 고칠 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-113">The charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="6d8f5-114">새로 고침 간격은 차트의 시간 범위에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-114">The refresh interval depends on the time range of the chart.</span></span>
* <span data-ttu-id="6d8f5-115">ApplicationInsights.xml 파일(프로젝트의 리소스 폴더에 있음)에 계측 키가 정의되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-115">Check that you have an instrumentation key defined in the ApplicationInsights.xml file (in the resources folder in your project)</span></span>
* <span data-ttu-id="6d8f5-116">xml 파일에 `<DisableTelemetry>true</DisableTelemetry>` 노드가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in the xml file.</span></span>
* <span data-ttu-id="6d8f5-117">방화벽에서 dc.services.visualstudio.com으로 나가는 트래픽에 대해 TCP 포트 80 및 443을 열어야 할 수 있습니다. 최신 버전은 [방화벽 예외의 전체 목록](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="6d8f5-117">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com. See the [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="6d8f5-118">Microsoft Azure 시작 보드에서 서비스 상태 맵을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-118">In the Microsoft Azure start board, look at the service status map.</span></span> <span data-ttu-id="6d8f5-119">어떤 경고 표시가 있는 경우 정상으로 돌아갈 때까지 기다린 후 Application Insights 응용 프로그램 블레이드를 닫고 다시 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-119">If there are some alert indications, wait until they have returned to OK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="6d8f5-120">ApplicationInsights.xml 파일(프로젝트의 리소스 폴더에 있음)의 루트 노드 아래에 `<SDKLogger />` 요소를 추가하여 IDE 콘솔 창에 기록을 켜고 앞에 [Error]가 붙은 항목을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-120">Turn on logging to the IDE console window, by adding an `<SDKLogger />` element under the root node in the ApplicationInsights.xml file (in the resources folder in your project), and check for entries prefaced with [Error].</span></span>
* <span data-ttu-id="6d8f5-121">콘솔의 출력 메시지에서 “구성 파일을 찾았습니다.”라는 문을 찾아 ApplicationInsights.xml 파일이 Java SDK에 의해 성공적으로 로드되었음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-121">Make sure that the correct ApplicationInsights.xml file has been successfully loaded by the Java SDK, by looking at the console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="6d8f5-122">구성 파일이 없으면 출력 메시지를 확인하여 구성 파일이 검색되고 있는 위치를 확인하고, ApplicationInsights.xml이 그러한 검색 위치 중 한 위치에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-122">If the config file is not found, check the output messages to see where the config file is being searched for, and make sure that the ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="6d8f5-123">일반적으로 구성 파일을 Application Insights SDK JAR 주위에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-123">As a rule of thumb, you can place the config file near the Application Insights SDK JARs.</span></span> <span data-ttu-id="6d8f5-124">예: Tomcat에서는 WEB-INF/lib 폴더를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-124">For example: in Tomcat, this would mean the WEB-INF/lib folder.</span></span>

#### <a name="i-used-to-see-data-but-it-has-stopped"></a><span data-ttu-id="6d8f5-125">데이터를 보는 데 중지되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-125">I used to see data, but it has stopped</span></span>
* <span data-ttu-id="6d8f5-126">[상태 블로그](http://blogs.msdn.com/b/applicationinsights-status/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-126">Check the [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="6d8f5-127">데이터 요소의 월간 할당량에 도달했습니까?</span><span class="sxs-lookup"><span data-stu-id="6d8f5-127">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="6d8f5-128">설정/할당량 및 가격을 열어 알아봅니다. 그렇다면 계획을 업그레이드하거나 추가 용량에 대한 비용을 지불할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-128">Open Settings/Quota and Pricing to find out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="6d8f5-129">[가격 체계](https://azure.microsoft.com/pricing/details/application-insights/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-129">See the [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>

#### <a name="i-dont-see-all-the-data-im-expecting"></a><span data-ttu-id="6d8f5-130">기대한 모든 데이터가 표시되지 않는 경우</span><span class="sxs-lookup"><span data-stu-id="6d8f5-130">I don't see all the data I'm expecting</span></span>
* <span data-ttu-id="6d8f5-131">할당량 및 가격 책정 블레이드를 열고 [샘플링](app-insights-sampling.md)이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-131">Open the Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="6d8f5-132">(100% 전송이란 샘플링을 사용하지 않는다는 의미입니다.) Application Insights 서비스는 앱에서 도착하는 원격 분석의 일부만 허용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-132">(100% transmission means that sampling isn't in operation.) The Application Insights service can be set to accept only a fraction of the telemetry that arrives from your app.</span></span> <span data-ttu-id="6d8f5-133">이렇게 하면 원격 분석의 월간 할당량 내로 유지하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-133">This helps you keep within your monthly quota of telemetry.</span></span> 

## <a name="no-usage-data"></a><span data-ttu-id="6d8f5-134">사용 현황 데이터 없음</span><span class="sxs-lookup"><span data-stu-id="6d8f5-134">No usage data</span></span>
<span data-ttu-id="6d8f5-135">**요청 및 응답 시간에 대한 데이터는 표시되는데 페이지 보기, 브라우저 또는 사용자 데이터는 표시되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="6d8f5-135">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="6d8f5-136">서버에서 원격 분석을 보내도록 앱을 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-136">You successfully set up your app to send telemetry from the server.</span></span> <span data-ttu-id="6d8f5-137">이제 다음 단계로 [웹 브라우저에서 원격 분석을 보내도록 웹 페이지를 설정][usage]해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-137">Now your next step is to [set up your web pages to send telemetry from the web browser][usage].</span></span>

<span data-ttu-id="6d8f5-138">또는 클라이언트가 [휴대폰이나 기타 장치][platforms]의 앱인 경우 해당 장치에서 원격 분석을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-138">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="6d8f5-139">동일한 계측 키를 사용하여 클라이언트 및 서버 원격 분석을 둘 다 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-139">Use the same instrumentation key to set up both your client and server telemetry.</span></span> <span data-ttu-id="6d8f5-140">데이터가 동일한 Application Insights 리소스에 표시되며, 클라이언트와 서버의 이벤트에 상관 관계를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-140">The data will appear in the same Application Insights resource, and you'll be able to correlate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="6d8f5-141">원격 분석 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="6d8f5-141">Disabling telemetry</span></span>
<span data-ttu-id="6d8f5-142">**원격 분석 수집을 사용하지 않도록 설정하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="6d8f5-142">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="6d8f5-143">코드:</span><span class="sxs-lookup"><span data-stu-id="6d8f5-143">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="6d8f5-144">**또는**</span><span class="sxs-lookup"><span data-stu-id="6d8f5-144">**Or**</span></span> 

<span data-ttu-id="6d8f5-145">ApplicationInsights.xml(프로젝트의 리소스 폴더에 있음)을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-145">Update ApplicationInsights.xml (in the resources folder in your project).</span></span> <span data-ttu-id="6d8f5-146">루트 노드 아래에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-146">Add the following under the root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="6d8f5-147">XML 메서드를 사용하여 값 변경 시 응용 프로그램을 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-147">Using the XML method, you have to restart the application when you change the value.</span></span>

## <a name="changing-the-target"></a><span data-ttu-id="6d8f5-148">대상 변경</span><span class="sxs-lookup"><span data-stu-id="6d8f5-148">Changing the target</span></span>
<span data-ttu-id="6d8f5-149">**내 프로젝트에서 데이터를 보내는 Azure 리소스를 변경하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="6d8f5-149">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="6d8f5-150">[새 리소스의 계측 키를 가져옵니다.][java]</span><span class="sxs-lookup"><span data-stu-id="6d8f5-150">[Get the instrumentation key of the new resource.][java]</span></span>
* <span data-ttu-id="6d8f5-151">Azure Toolkit for Eclipse를 사용하여 프로젝트에 Application Insights를 추가한 경우 웹 프로젝트를 마우스 오른쪽 단추로 클릭하고**Azure**, **Application Insights 구성**을 차례로 선택한 다음 키를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-151">If you added Application Insights to your project using the Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change the key.</span></span>
* <span data-ttu-id="6d8f5-152">그렇지 않으면 프로젝트의 리소스 폴더에 있는 ApplicationInsights.xml에서 키를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-152">Otherwise, update the key in ApplicationInsights.xml in the resources folder in your project.</span></span>

## <a name="debug-data-from-the-sdk"></a><span data-ttu-id="6d8f5-153">SDK에서 데이터 디버깅</span><span class="sxs-lookup"><span data-stu-id="6d8f5-153">Debug data from the SDK</span></span>

<span data-ttu-id="6d8f5-154">**SDK가 수행하는 작업을 찾는 방법**</span><span class="sxs-lookup"><span data-stu-id="6d8f5-154">**How can I find out what the SDK is doing?**</span></span>

<span data-ttu-id="6d8f5-155">API의 상황에 대한 자세한 정보를 가져오려면 ApplicationInsights.xml 구성 파일의 루트 노드에 `<SDKLogger/>`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-155">To get more information about what's happening in the API, add `<SDKLogger/>` under the root node of the ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="6d8f5-156">파일에 출력하도록 로거에 지시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-156">You can also instruct the logger to output to a file:</span></span>

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

<span data-ttu-id="6d8f5-157">Tomcat 서버의 경우 `%temp%\javasdklogs` 또는 `java.io.tmpdir` 아래에서 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-157">The files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span></span>


## <a name="the-azure-start-screen"></a><span data-ttu-id="6d8f5-158">Azure 시작 화면</span><span class="sxs-lookup"><span data-stu-id="6d8f5-158">The Azure start screen</span></span>
<span data-ttu-id="6d8f5-159">**[Azure Portal](https://portal.azure.com)을 보고 있습니다. 맵에 내 앱에 대한 정보가 표시되나요?**</span><span class="sxs-lookup"><span data-stu-id="6d8f5-159">**I'm looking at [the Azure portal](https://portal.azure.com). Does the map tell me something about my app?**</span></span>

<span data-ttu-id="6d8f5-160">아니요, 전 세계 Azure 서버의 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-160">No, it shows the health of Azure servers around the world.</span></span>

<span data-ttu-id="6d8f5-161">*Azure 시작 보드(홈 화면)에서 내 앱에 대한 데이터를 찾으려면 어떻게 해야 하나요?*</span><span class="sxs-lookup"><span data-stu-id="6d8f5-161">*From the Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="6d8f5-162">[Application Insights에 대해 앱을 설정][java]한 경우 찾아보기를 클릭하고 Application Insights를 선택한 다음 앱을 위해 만든 앱 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-162">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select the app resource you created for your app.</span></span> <span data-ttu-id="6d8f5-163">이후에 더 빨리 액세스하기 위해 앱을 시작 보드에 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-163">To get there faster in future, you can pin your app to the start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="6d8f5-164">인트라넷 서버</span><span class="sxs-lookup"><span data-stu-id="6d8f5-164">Intranet servers</span></span>
<span data-ttu-id="6d8f5-165">**내 인트라넷의 서버를 모니터링할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="6d8f5-165">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="6d8f5-166">예, 서버가 공용 인터넷을 통해 Application Insights 포털에 원격 분석을 보낼 수 있는 경우 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-166">Yes, provided your server can send telemetry to the Application Insights portal through the public internet.</span></span> 

<span data-ttu-id="6d8f5-167">방화벽에서 dc.services.visualstudio.com 및 f5.services.visualstudio.com으로 나가는 트래픽에 대해 TCP 포트 80 및 443을 열어야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-167">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="6d8f5-168">데이터 보존</span><span class="sxs-lookup"><span data-stu-id="6d8f5-168">Data retention</span></span>
<span data-ttu-id="6d8f5-169">**데이터가 포털에 얼마나 오래 보존되나요? 안전한가요?**</span><span class="sxs-lookup"><span data-stu-id="6d8f5-169">**How long is data retained in the portal? Is it secure?**</span></span>

<span data-ttu-id="6d8f5-170">[데이터 보존 및 개인 정보][data]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d8f5-170">See [Data retention and privacy][data].</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d8f5-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6d8f5-171">Next steps</span></span>
<span data-ttu-id="6d8f5-172">**내 Java 서버 앱에 대해 Application Insights를 설정했습니다. 다른 어떤 작업을 할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="6d8f5-172">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="6d8f5-173">[웹 페이지의 가용성 모니터링][availability]</span><span class="sxs-lookup"><span data-stu-id="6d8f5-173">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="6d8f5-174">[웹 페이지 사용 모니터링][usage]</span><span class="sxs-lookup"><span data-stu-id="6d8f5-174">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="6d8f5-175">[장치 앱의 사용 추적 및 문제 진단][platforms]</span><span class="sxs-lookup"><span data-stu-id="6d8f5-175">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="6d8f5-176">[코드를 작성하여 앱의 사용 추적][track]</span><span class="sxs-lookup"><span data-stu-id="6d8f5-176">[Write code to track usage of your app][track]</span></span>
* <span data-ttu-id="6d8f5-177">[진단 로그 캡처][javalogs]</span><span class="sxs-lookup"><span data-stu-id="6d8f5-177">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="6d8f5-178">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="6d8f5-178">Get help</span></span>
* [<span data-ttu-id="6d8f5-179">스택 오버플로</span><span class="sxs-lookup"><span data-stu-id="6d8f5-179">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md


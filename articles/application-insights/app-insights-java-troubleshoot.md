---
title: "Java 웹 프로젝트에서 Application Insights aaaTroubleshoot"
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
ms.openlocfilehash: c274c01b1992971fae194c3e510512ca06ab76b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="1aa34-103">Java용 Application Insights 문제 해결과 질문 및 답변</span><span class="sxs-lookup"><span data-stu-id="1aa34-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="1aa34-104">[Java의 Azure Application Insights][java]와 관련된 질문이나 문제가 있나요?</span><span class="sxs-lookup"><span data-stu-id="1aa34-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="1aa34-105">다음은 몇 가지 팁입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="1aa34-106">빌드 오류</span><span class="sxs-lookup"><span data-stu-id="1aa34-106">Build errors</span></span>
<span data-ttu-id="1aa34-107">**Eclipse에서 Maven 또는 Gradle을 통해 Application Insights SDK hello를 추가 하는 경우 빌드 또는 체크섬 유효성 검사 오류가 발생 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1aa34-107">**In Eclipse, when adding hello Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="1aa34-108">경우 종속성을 hello <version> 요소 와일드 카드 문자가 있는 패턴을 사용 하는 (예: (Maven) `<version>[1.0,)</version>` 또는 (Gradle) `version:'1.0.+'`), 같은 특정 버전을 대신 지정 하십시오 `1.0.2`합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-108">If hello dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span></span> <span data-ttu-id="1aa34-109">Hello 참조 [릴리스 정보](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) hello 최신 버전에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-109">See hello [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for hello latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="1aa34-110">데이터 없음</span><span class="sxs-lookup"><span data-stu-id="1aa34-110">No data</span></span>
<span data-ttu-id="1aa34-111">**Application Insights를 성공적으로 추가 하 고 내 응용 프로그램을 실행 하지만 데이터 hello 포털에서 본 적입니다.**</span><span class="sxs-lookup"><span data-stu-id="1aa34-111">**I added Application Insights successfully and ran my app, but I've never seen data in hello portal.**</span></span>

* <span data-ttu-id="1aa34-112">잠시 기다린 후 새로 고침을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="1aa34-113">hello 차트를 새로 고칠 자체 정기적으로, 있지만 있습니다 또한 수동으로 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-113">hello charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="1aa34-114">hello 새로 고침 간격 hello hello 차트는 시간 범위에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-114">hello refresh interval depends on hello time range of hello chart.</span></span>
* <span data-ttu-id="1aa34-115">Hello ApplicationInsights.xml 파일 (프로젝트의 hello resources 폴더)에 정의 하는 계측 키가 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="1aa34-115">Check that you have an instrumentation key defined in hello ApplicationInsights.xml file (in hello resources folder in your project)</span></span>
* <span data-ttu-id="1aa34-116">확인 없는 `<DisableTelemetry>true</DisableTelemetry>` hello xml 파일에 있는 노드.</span><span class="sxs-lookup"><span data-stu-id="1aa34-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in hello xml file.</span></span>
* <span data-ttu-id="1aa34-117">하려면 방화벽에서 TCP 포트 80 및 443 나가는 트래픽 toodc.services.visualstudio.com tooopen 있을 수 있습니다. Hello 참조 [전체 방화벽 예외 목록](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="1aa34-117">In your firewall, you might have tooopen TCP ports 80 and 443 for outgoing traffic toodc.services.visualstudio.com. See hello [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="1aa34-118">Microsoft Azure hello 시작 보드를 hello 서비스 상태 맵을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-118">In hello Microsoft Azure start board, look at hello service status map.</span></span> <span data-ttu-id="1aa34-119">경고 설명 인은 tooOK 반환한을 Application Insights 응용 프로그램 블레이드를 다시 열 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-119">If there are some alert indications, wait until they have returned tooOK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="1aa34-120">Toohello IDE 콘솔 창에 추가 하 여 로깅을 설정할는 `<SDKLogger />` hello ApplicationInsights.xml 파일 (hello 리소스 폴더에 프로젝트의) 및 [오류] 앞에 추가 하는 항목에 대 한 확인의 hello 루트 노드에 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-120">Turn on logging toohello IDE console window, by adding an `<SDKLogger />` element under hello root node in hello ApplicationInsights.xml file (in hello resources folder in your project), and check for entries prefaced with [Error].</span></span>
* <span data-ttu-id="1aa34-121">해당 hello ApplicationInsights.xml 파일이 성공적으로 로드 된 hello Java SDK에서 "구성 파일이 성공적으로 발견 되었습니다" 문에 대해 hello 콘솔 출력 메시지를 확인 하 여 올바른 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="1aa34-121">Make sure that hello correct ApplicationInsights.xml file has been successfully loaded by hello Java SDK, by looking at hello console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="1aa34-122">Hello 구성 파일이 없으면 hello 출력 메시지 toosee hello 구성 파일, 검색 위치를 확인 하 고 ApplicationInsights.xml 이러한 검색 위치 중 하나에 있는 해당 hello 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-122">If hello config file is not found, check hello output messages toosee where hello config file is being searched for, and make sure that hello ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="1aa34-123">경험상,으로 hello 응용 프로그램 통찰력 SDK 단지 근처 hello 구성 파일을 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-123">As a rule of thumb, you can place hello config file near hello Application Insights SDK JARs.</span></span> <span data-ttu-id="1aa34-124">예: Tomcat에서 이런 경우 웹-INF/lib 폴더 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-124">For example: in Tomcat, this would mean hello WEB-INF/lib folder.</span></span>

#### <a name="i-used-toosee-data-but-it-has-stopped"></a><span data-ttu-id="1aa34-125">중지 된 하지만 toosee 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="1aa34-125">I used toosee data, but it has stopped</span></span>
* <span data-ttu-id="1aa34-126">Hello 확인 [상태 블로그](http://blogs.msdn.com/b/applicationinsights-status/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-126">Check hello [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="1aa34-127">데이터 요소의 월간 할당량에 도달했습니까?</span><span class="sxs-lookup"><span data-stu-id="1aa34-127">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="1aa34-128">설정/할당량 및 가격 책정 toofind 아웃를 엽니다. 그렇다면 계획을 업그레이드하거나 추가 용량에 대한 비용을 지불할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-128">Open Settings/Quota and Pricing toofind out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="1aa34-129">Hello 참조 [가격 체계](https://azure.microsoft.com/pricing/details/application-insights/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-129">See hello [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>

#### <a name="i-dont-see-all-hello-data-im-expecting"></a><span data-ttu-id="1aa34-130">필요한 데 I hello 데이터를 모두 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-130">I don't see all hello data I'm expecting</span></span>
* <span data-ttu-id="1aa34-131">Hello 할당량 및 가격 책정 블레이드 및 확인 여부를 열고 [샘플링](app-insights-sampling.md) 작업에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-131">Open hello Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="1aa34-132">(100% 전송 샘플링 없음을 의미 작업에서 합니다.) Application Insights 서비스 hello 집합 tooaccept 앱에서 들어오는 hello 원격 분석의 일부만 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-132">(100% transmission means that sampling isn't in operation.) hello Application Insights service can be set tooaccept only a fraction of hello telemetry that arrives from your app.</span></span> <span data-ttu-id="1aa34-133">이렇게 하면 원격 분석의 월간 할당량 내로 유지하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-133">This helps you keep within your monthly quota of telemetry.</span></span> 

## <a name="no-usage-data"></a><span data-ttu-id="1aa34-134">사용 현황 데이터 없음</span><span class="sxs-lookup"><span data-stu-id="1aa34-134">No usage data</span></span>
<span data-ttu-id="1aa34-135">**요청 및 응답 시간에 대한 데이터는 표시되는데 페이지 보기, 브라우저 또는 사용자 데이터는 표시되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="1aa34-135">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="1aa34-136">성공적으로 설정한 앱 toosend 원격 분석 hello 서버에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-136">You successfully set up your app toosend telemetry from hello server.</span></span> <span data-ttu-id="1aa34-137">다음 단계는 너무 이제[hello 웹 브라우저에서 웹 페이지 toosend 원격 분석 설정][usage]합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-137">Now your next step is too[set up your web pages toosend telemetry from hello web browser][usage].</span></span>

<span data-ttu-id="1aa34-138">또는 클라이언트가 [휴대폰이나 기타 장치][platforms]의 앱인 경우 해당 장치에서 원격 분석을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-138">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="1aa34-139">사용 하 여 hello 동일한 클라이언트와 서버 원격 분석을 계측 키 tooset 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-139">Use hello same instrumentation key tooset up both your client and server telemetry.</span></span> <span data-ttu-id="1aa34-140">클라이언트와 서버에서 수 toocorrelate 이벤트 수 있게 하 고 동일한 Application Insights 리소스 hello hello 데이터에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-140">hello data will appear in hello same Application Insights resource, and you'll be able toocorrelate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="1aa34-141">원격 분석 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="1aa34-141">Disabling telemetry</span></span>
<span data-ttu-id="1aa34-142">**원격 분석 수집을 사용하지 않도록 설정하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="1aa34-142">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="1aa34-143">코드:</span><span class="sxs-lookup"><span data-stu-id="1aa34-143">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="1aa34-144">**또는**</span><span class="sxs-lookup"><span data-stu-id="1aa34-144">**Or**</span></span> 

<span data-ttu-id="1aa34-145">ApplicationInsights.xml hello 리소스 폴더에서 프로젝트에서를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-145">Update ApplicationInsights.xml (in hello resources folder in your project).</span></span> <span data-ttu-id="1aa34-146">Hello hello 루트 노드에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-146">Add hello following under hello root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="1aa34-147">Hello XML 메서드를 사용 하 여 한 toorestart hello 응용 프로그램 hello 값을 변경 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-147">Using hello XML method, you have toorestart hello application when you change hello value.</span></span>

## <a name="changing-hello-target"></a><span data-ttu-id="1aa34-148">Hello 대상 변경</span><span class="sxs-lookup"><span data-stu-id="1aa34-148">Changing hello target</span></span>
<span data-ttu-id="1aa34-149">**내 프로젝트에서 데이터를 보내는 Azure 리소스를 변경하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="1aa34-149">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="1aa34-150">[Hello 새 리소스의 hello 계측 키를 가져옵니다.][java]</span><span class="sxs-lookup"><span data-stu-id="1aa34-150">[Get hello instrumentation key of hello new resource.][java]</span></span>
* <span data-ttu-id="1aa34-151">Eclipse 용 Azure 도구 키트 hello를 사용 하 여 Application Insights tooyour 프로젝트를 추가한 경우 웹 프로젝트를 마우스 오른쪽 단추로 클릭, 선택 **Azure**, **Configure Application Insights**, hello 키를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-151">If you added Application Insights tooyour project using hello Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change hello key.</span></span>
* <span data-ttu-id="1aa34-152">그렇지 않으면 ApplicationInsights.xml hello 리소스 폴더에 프로젝트의에서 hello 키를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-152">Otherwise, update hello key in ApplicationInsights.xml in hello resources folder in your project.</span></span>

## <a name="debug-data-from-hello-sdk"></a><span data-ttu-id="1aa34-153">Hello SDK에서에서 데이터 디버깅</span><span class="sxs-lookup"><span data-stu-id="1aa34-153">Debug data from hello SDK</span></span>

<span data-ttu-id="1aa34-154">**SDK를 수행 하는 hello 방법을 찾을 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="1aa34-154">**How can I find out what hello SDK is doing?**</span></span>

<span data-ttu-id="1aa34-155">tooget hello API에서에서 일어나는 대 한 자세한 내용은 추가 `<SDKLogger/>` hello ApplicationInsights.xml 구성 파일의 hello 루트 노드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-155">tooget more information about what's happening in hello API, add `<SDKLogger/>` under hello root node of hello ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="1aa34-156">Hello로 거 toooutput tooa 파일을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-156">You can also instruct hello logger toooutput tooa file:</span></span>

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

<span data-ttu-id="1aa34-157">hello 파일에서 찾을 수 있습니다 `%temp%\javasdklogs` 또는 `java.io.tmpdir` Tomcat 서버의 경우.</span><span class="sxs-lookup"><span data-stu-id="1aa34-157">hello files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span></span>


## <a name="hello-azure-start-screen"></a><span data-ttu-id="1aa34-158">hello Azure 시작 화면</span><span class="sxs-lookup"><span data-stu-id="1aa34-158">hello Azure start screen</span></span>
<span data-ttu-id="1aa34-159">**보 니 [Azure 포털 hello](https://portal.azure.com)합니다. hello 맵 항목에 대 한 설명 내 앱?**</span><span class="sxs-lookup"><span data-stu-id="1aa34-159">**I'm looking at [hello Azure portal](https://portal.azure.com). Does hello map tell me something about my app?**</span></span>

<span data-ttu-id="1aa34-160">아니요, hello 전 세계 hello Azure 서버의 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-160">No, it shows hello health of Azure servers around hello world.</span></span>

<span data-ttu-id="1aa34-161">*Hello Azure 시작 보드 (홈 화면)에서 찾으려면 어떻게 해야 합니까 데이터 응용 프로그램의 한?*</span><span class="sxs-lookup"><span data-stu-id="1aa34-161">*From hello Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="1aa34-162">가정 하 고 [Application Insights에 대 한 앱 설정][java], 찾아보기를 클릭, Application Insights를 선택 하 고 응용 프로그램에 대해 만든 hello 응용 프로그램 리소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-162">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select hello app resource you created for your app.</span></span> <span data-ttu-id="1aa34-163">tooget 있습니다 더 빠르게 나중에 고정할 수 있는 앱 toohello 시작 보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-163">tooget there faster in future, you can pin your app toohello start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="1aa34-164">인트라넷 서버</span><span class="sxs-lookup"><span data-stu-id="1aa34-164">Intranet servers</span></span>
<span data-ttu-id="1aa34-165">**내 인트라넷의 서버를 모니터링할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="1aa34-165">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="1aa34-166">예, 공용 인터넷을 hello 서버는 원격 분석 toohello Application Insights 포털을 통해 보낼 수 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-166">Yes, provided your server can send telemetry toohello Application Insights portal through hello public internet.</span></span> 

<span data-ttu-id="1aa34-167">하려면 방화벽에서 TCP 포트 80 및 443 나가는 트래픽 toodc.services.visualstudio.com 및 f5.services.visualstudio.com tooopen 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa34-167">In your firewall, you might have tooopen TCP ports 80 and 443 for outgoing traffic toodc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="1aa34-168">데이터 보존</span><span class="sxs-lookup"><span data-stu-id="1aa34-168">Data retention</span></span>
<span data-ttu-id="1aa34-169">**Hello 포털에서 데이터를 보관 하는 기간 안전한가요?**</span><span class="sxs-lookup"><span data-stu-id="1aa34-169">**How long is data retained in hello portal? Is it secure?**</span></span>

<span data-ttu-id="1aa34-170">[데이터 보존 및 개인 정보][data]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1aa34-170">See [Data retention and privacy][data].</span></span>

## <a name="next-steps"></a><span data-ttu-id="1aa34-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1aa34-171">Next steps</span></span>
<span data-ttu-id="1aa34-172">**내 Java 서버 앱에 대해 Application Insights를 설정했습니다. 다른 어떤 작업을 할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="1aa34-172">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="1aa34-173">[웹 페이지의 가용성 모니터링][availability]</span><span class="sxs-lookup"><span data-stu-id="1aa34-173">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="1aa34-174">[웹 페이지 사용 모니터링][usage]</span><span class="sxs-lookup"><span data-stu-id="1aa34-174">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="1aa34-175">[장치 앱의 사용 추적 및 문제 진단][platforms]</span><span class="sxs-lookup"><span data-stu-id="1aa34-175">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="1aa34-176">[응용 프로그램의 코드 tootrack 사용 작성][track]</span><span class="sxs-lookup"><span data-stu-id="1aa34-176">[Write code tootrack usage of your app][track]</span></span>
* <span data-ttu-id="1aa34-177">[진단 로그 캡처][javalogs]</span><span class="sxs-lookup"><span data-stu-id="1aa34-177">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="1aa34-178">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="1aa34-178">Get help</span></span>
* [<span data-ttu-id="1aa34-179">스택 오버플로</span><span class="sxs-lookup"><span data-stu-id="1aa34-179">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md


---
title: "App Service에서 느린 웹앱 성능 | Microsoft Docs"
description: "이 문서에서는 Azure App Service의 느린 웹앱 성능 문제를 해결하는 데 도움을 줍니다."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "웹앱 성능, 느린 앱, 앱 느림"
ms.assetid: b8783c10-3a4a-4dd6-af8c-856baafbdde5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: cephalin
ms.openlocfilehash: 1cfe7ec37ad8b24a8bd9ab2bf67e95675a57b675
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-slow-web-app-performance-issues-in-azure-app-service"></a><span data-ttu-id="1d3f5-104">Azure App Service에서 느린 웹앱 성능 문제 해결</span><span class="sxs-lookup"><span data-stu-id="1d3f5-104">Troubleshoot slow web app performance issues in Azure App Service</span></span>
<span data-ttu-id="1d3f5-105">이 문서에서는 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)의 느린 웹앱 성능 문제를 해결하는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-105">This article helps you troubleshoot slow web app performance issues in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="1d3f5-106">이 문서의 어디에서든 도움이 필요한 경우 [MSDN Azure 및 스택 오버플로 포럼](https://azure.microsoft.com/support/forums/)에서 Azure 전문가에게 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-106">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="1d3f5-107">또는 Azure 기술 지원 인시던트를 제출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-107">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="1d3f5-108">[Azure 지원 사이트](https://azure.microsoft.com/support/options/) 로 이동한 다음 **지원 받기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-108">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="1d3f5-109">증상</span><span class="sxs-lookup"><span data-stu-id="1d3f5-109">Symptom</span></span>
<span data-ttu-id="1d3f5-110">웹앱을 탐색할 때, 페이지 로딩이 느려지거나 멈춤.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-110">When you browse the web app, the pages load slowly and sometimes timeout.</span></span>

## <a name="cause"></a><span data-ttu-id="1d3f5-111">원인</span><span class="sxs-lookup"><span data-stu-id="1d3f5-111">Cause</span></span>
<span data-ttu-id="1d3f5-112">이 문제는 응용 프로그램 수준 문제가 원인이 되는 경우가 많습니다. 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="1d3f5-112">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="1d3f5-113">긴 네트워크 요청 시간</span><span class="sxs-lookup"><span data-stu-id="1d3f5-113">network requests taking a long time</span></span>
* <span data-ttu-id="1d3f5-114">비효율적인 응용 프로그램 코드 또는 데이터베이스 쿼리</span><span class="sxs-lookup"><span data-stu-id="1d3f5-114">application code or database queries being inefficient</span></span>
* <span data-ttu-id="1d3f5-115">높은 메모리/CPU를 사용하는 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="1d3f5-115">application using high memory/CPU</span></span>
* <span data-ttu-id="1d3f5-116">예외로 인해 충돌하는 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="1d3f5-116">application crashing due to an exception</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="1d3f5-117">문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="1d3f5-117">Troubleshooting steps</span></span>
<span data-ttu-id="1d3f5-118">문제 해결은 해결하는 순서대로 세 가지로 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="1d3f5-119">응용 프로그램 작동을 관찰 및 감시</span><span class="sxs-lookup"><span data-stu-id="1d3f5-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="1d3f5-120">데이터 수집</span><span class="sxs-lookup"><span data-stu-id="1d3f5-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="1d3f5-121">문제 완화</span><span class="sxs-lookup"><span data-stu-id="1d3f5-121">Mitigate the issue</span></span>](#mitigate)

<span data-ttu-id="1d3f5-122">[App Service Web Apps](/services/app-service/web/)는 각 단계별로 다양한 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="1d3f5-123">1. 응용 프로그램 작동을 관찰 및 감시 </span><span class="sxs-lookup"><span data-stu-id="1d3f5-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="1d3f5-124">서비스 상태를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-124">Track Service health</span></span>
<span data-ttu-id="1d3f5-125">Microsoft Azure는 서비스가 중단되거나 성능이 저하될 때마다 경고를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="1d3f5-126">[Azure Portal](https://portal.azure.com/)에서 서비스의 상태를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-126">You can track the health of the service on the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="1d3f5-127">자세한 내용은 [서비스 상태 추적](../monitoring-and-diagnostics/insights-service-health.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="1d3f5-128">웹앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="1d3f5-128">Monitor your web app</span></span>
<span data-ttu-id="1d3f5-129">이 옵션은 응용 프로그램의 문제를 해결할 수 있게 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-129">This option enables you to find out if your application is having any issues.</span></span> <span data-ttu-id="1d3f5-130">웹앱의 블레이드에서 **요청 및 오류** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-130">In your web app’s blade, click the **Requests and errors** tile.</span></span> <span data-ttu-id="1d3f5-131">**메트릭** 블레이드는 추가 가능한 모든 메트릭을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-131">The **Metric** blade shows you all the metrics you can add.</span></span>

<span data-ttu-id="1d3f5-132">모니터링 하고자 하는 웹앱의 일부 메트릭은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-132">Some of the metrics that you might want to monitor for your web app are</span></span>

* <span data-ttu-id="1d3f5-133">평균 메모리 작업 집합</span><span class="sxs-lookup"><span data-stu-id="1d3f5-133">Average memory working set</span></span>
* <span data-ttu-id="1d3f5-134">평균 응답 시간</span><span class="sxs-lookup"><span data-stu-id="1d3f5-134">Average response time</span></span>
* <span data-ttu-id="1d3f5-135">CPU 시간</span><span class="sxs-lookup"><span data-stu-id="1d3f5-135">CPU time</span></span>
* <span data-ttu-id="1d3f5-136">메모리 작업 집합</span><span class="sxs-lookup"><span data-stu-id="1d3f5-136">Memory working set</span></span>
* <span data-ttu-id="1d3f5-137">요청</span><span class="sxs-lookup"><span data-stu-id="1d3f5-137">Requests</span></span>

![웹앱 성능 모니터링](./media/app-service-web-troubleshoot-performance-degradation/1-monitor-metrics.png)

<span data-ttu-id="1d3f5-139">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-139">For more information, see:</span></span>

* [<span data-ttu-id="1d3f5-140">Azure App Service에서 Web Apps 모니터링</span><span class="sxs-lookup"><span data-stu-id="1d3f5-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="1d3f5-141">경고 알림 받기</span><span class="sxs-lookup"><span data-stu-id="1d3f5-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

#### <a name="monitor-web-endpoint-status"></a><span data-ttu-id="1d3f5-142">웹 끝점 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="1d3f5-142">Monitor web endpoint status</span></span>
<span data-ttu-id="1d3f5-143">**표준** 가격 정책에서 Web Apps를 실행할 경우, 3곳의 지리적 위치에서 끝점 2개를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-143">If you are running your web app in the **Standard** pricing tier, Web Apps lets you monitor two endpoints from three geographic locations.</span></span>

<span data-ttu-id="1d3f5-144">끝점 모니터링은 지리적으로 분산된 위치에서 웹 URL의 응답 시간 및 가동 시간을 테스트하는 웹 테스트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-144">Endpoint monitoring configures web tests from geo-distributed locations that test response time and uptime of web URLs.</span></span> <span data-ttu-id="1d3f5-145">테스트는 웹 URL의 HTTP 가져오기 작업을 수행하여 각 위치의 응답 시간 및 가동 시간을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-145">The test performs an HTTP GET operation on the web URL to determine the response time and uptime from each location.</span></span> <span data-ttu-id="1d3f5-146">구성된 각 위치에서는 5분마다 테스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-146">Each configured location runs a test every five minutes.</span></span>

<span data-ttu-id="1d3f5-147">가동 시간은 HTTP 응답 코드를 사용하여 모니터링되며 응답 시간은 밀리초로 측정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-147">Uptime is monitored using HTTP response codes, and response time is measured in milliseconds.</span></span> <span data-ttu-id="1d3f5-148">HTTP 응답 코드가 400 이상이거나 응답에 30초 넘게 걸리는 경우 모니터링 테스트가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-148">A monitoring test fails if the HTTP response code is greater than or equal to 400 or if the response takes more than 30 seconds.</span></span> <span data-ttu-id="1d3f5-149">지정된 모든 위치에서 모니터링 테스트가 성공하는 경우 끝점은 사용 가능한 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-149">An endpoint is considered available if its monitoring tests succeed from all the specified locations.</span></span>

<span data-ttu-id="1d3f5-150">설정하려면 [Azure App Service에서 앱 모니터링](web-sites-monitor.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-150">To set it up, see [Monitor apps in Azure App Service](web-sites-monitor.md).</span></span>

<span data-ttu-id="1d3f5-151">또한, 끝점 모니터링의 비디오에 대해서는 [Azure Websites 가동 및 끝 점 모니터링 - 스테판 스차코우(Stefan Schackow)](https://channel9.msdn.com/Shows/Azure-Friday/Keeping-Azure-Web-Sites-up-plus-Endpoint-Monitoring-with-Stefan-Schackow) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-151">Also, see [Keeping Azure Web Sites up plus Endpoint Monitoring - with Stefan Schackow](https://channel9.msdn.com/Shows/Azure-Friday/Keeping-Azure-Web-Sites-up-plus-Endpoint-Monitoring-with-Stefan-Schackow) for a video on endpoint monitoring.</span></span>

#### <a name="application-performance-monitoring-using-extensions"></a><span data-ttu-id="1d3f5-152">확장을 사용하여 응용 프로그램 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="1d3f5-152">Application performance monitoring using Extensions</span></span>
<span data-ttu-id="1d3f5-153">응용 프로그램 성능을 *사이트 확장*을 사용하여 모니터링 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-153">You can also monitor your application performance by using *site extensions*.</span></span>

<span data-ttu-id="1d3f5-154">각 App Service 웹앱은 사이트 확장처럼 사용할 수 있는 배포된 강력한 도구 집합인 확장 가능한 관리 끝점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-154">Each App Service web app provides an extensible management end point that allows you to use a powerful set of tools deployed as site extensions.</span></span> <span data-ttu-id="1d3f5-155">확장은 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-155">Extensions include:</span></span> 

- <span data-ttu-id="1d3f5-156">[Visual Studio Team Services](https://www.visualstudio.com/products/what-is-visual-studio-online-vs.aspx)와 같은 소스 코드 편집기.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-156">Source code editors like [Visual Studio Team Services](https://www.visualstudio.com/products/what-is-visual-studio-online-vs.aspx).</span></span> 
- <span data-ttu-id="1d3f5-157">웹앱에 연결된 MySQL 데이터베이스와 같은 연결된 리소스에 대한 관리 도구.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-157">Management tools for connected resources such as a MySQL database connected to a web app.</span></span>

<span data-ttu-id="1d3f5-158">[Azure Application Insights](/services/application-insights/) 및 [New Relic](/marketplace/partners/newrelic/newrelic/)은 두 가지 사이트 확장 성능 모니터링이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-158">[Azure Application Insights](/services/application-insights/) and [New Relic](/marketplace/partners/newrelic/newrelic/) are two of the performance monitoring site extensions that are available.</span></span> <span data-ttu-id="1d3f5-159">New Relic을 사용하려면 런타임에 에이전트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-159">To use New Relic, you install an agent at runtime.</span></span> <span data-ttu-id="1d3f5-160">Azure Application Insights를 사용하려면, SDK를 사용하여 코드를 다시 작성해야 하고 추가 데이터 접근을 제공하는 확장 프로그램을 설치해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-160">To use Azure Application Insights, you rebuild your code with an SDK, and you can also install an extension that provides access to additional data.</span></span> <span data-ttu-id="1d3f5-161">SDK를 통해 앱의 사용과 성능을 보다 자세하게 모니터링하기 위한 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-161">The SDK lets you write code to monitor the usage and performance of your app in more detail.</span></span>

<span data-ttu-id="1d3f5-162">Application Insights를 사용하려면 [웹 응용 프로그램에서 모니터 성능](../application-insights/app-insights-web-monitor-performance.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-162">To use Application Insights, see [Monitor performance in web applications](../application-insights/app-insights-web-monitor-performance.md).</span></span>

<span data-ttu-id="1d3f5-163">New Relic을 사용하려면 [Azure에서 New Relic 응용 프로그램 성능 관리](../store-new-relic-cloud-services-dotnet-application-performance-management.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-163">To use New Relic, see [New Relic Application Performance Management on Azure](../store-new-relic-cloud-services-dotnet-application-performance-management.md).</span></span>

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="1d3f5-164">2. 데이터 수집</span><span class="sxs-lookup"><span data-stu-id="1d3f5-164">2. Collect data</span></span>
<span data-ttu-id="1d3f5-165">Web Apps 환경은 웹 서버 및 웹 응용 프로그램 두 곳 모두에서 로깅 정보에 대한 진단 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-165">The Web Apps environment provides diagnostic functionality for logging information from both the web server and the web application.</span></span> <span data-ttu-id="1d3f5-166">이 정보는 웹 서버 진단 및 응용 프로그램 진단으로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-166">The information is separated into web server diagnostics and application diagnostics.</span></span>

#### <a name="enable-web-server-diagnostics"></a><span data-ttu-id="1d3f5-167">웹 서버 진단 사용</span><span class="sxs-lookup"><span data-stu-id="1d3f5-167">Enable web server diagnostics</span></span>
<span data-ttu-id="1d3f5-168">다음과 같은 종류의 로그를 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-168">You can enable or disable the following kinds of logs:</span></span>

* <span data-ttu-id="1d3f5-169">**자세한 오류 로깅** - 오류를 나타내는 HTTP 상태 코드(상태 코드 400 이상)의 자세한 오류 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-169">**Detailed Error Logging** - Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span> <span data-ttu-id="1d3f5-170">여기에는 서버에서 오류 코드를 반환한 이유를 확인하는 데 도움이 되는 정보가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-170">This may contain information that can help determine why the server returned the error code.</span></span>
* <span data-ttu-id="1d3f5-171">**실패한 요청 추적** - 요청을 처리하는 데 사용된 IIS 구성 요소 추적 및 각 구성 요소에 소요된 시간을 포함하여 실패한 요청에 대해 자세한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-171">**Failed Request Tracing** - Detailed information on failed requests, including a trace of the IIS components used to process the request and the time taken in each component.</span></span> <span data-ttu-id="1d3f5-172">이 기능은 웹앱 성능을 개선하거나 특정 HTTP 오류 원인을 격리하려는 경우에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-172">This can be useful if you are attempting to improve web app performance or isolate what is causing a specific HTTP error.</span></span>
* <span data-ttu-id="1d3f5-173">**웹 서버 로깅** - W3C 확장 로그 파일 형식을 사용하는 HTTP 트랜잭션에 대한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-173">**Web Server Logging** - Information about HTTP transactions using the W3C extended log file format.</span></span> <span data-ttu-id="1d3f5-174">이 기능은 처리된 요청의 수 또는 특정 IP 주소에서 넘어온 많은 요청처럼 전반적인 웹앱 메트릭을 결정할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-174">This is useful when determining overall web app metrics, such as the number of requests handled or how many requests are from a specific IP address.</span></span>

#### <a name="enable-application-diagnostics"></a><span data-ttu-id="1d3f5-175">응용 프로그램 진단 사용</span><span class="sxs-lookup"><span data-stu-id="1d3f5-175">Enable application diagnostics</span></span>
<span data-ttu-id="1d3f5-176">Web Apps에서 응용 프로그램 성능 데이터를 수집하고, Visual Studio에서 응용 프로그램 라이브를 프로파일링하거나 자세한 내용 및 추적을 기록하도록 응용 프로그램 코드를 수정하는 다양한 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-176">There are several options to collect application performance data from Web Apps, profile your application live from Visual Studio, or modify your application code to log more information and traces.</span></span> <span data-ttu-id="1d3f5-177">응용 프로그램에 대해 보유한 액세스 양 및 모니터링 도구에서 관찰한 내용에 따라 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-177">You can choose the options based on how much access you have to the application and what you observed from the monitoring tools.</span></span>

##### <a name="use-application-insights-profiler"></a><span data-ttu-id="1d3f5-178">Application Insights Profiler 사용</span><span class="sxs-lookup"><span data-stu-id="1d3f5-178">Use Application Insights Profiler</span></span>
<span data-ttu-id="1d3f5-179">Application Insights Profiler를 활성화하여 자세한 성능 추적 캡처를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-179">You can enable the Application Insights Profiler to start capturing detailed performance traces.</span></span> <span data-ttu-id="1d3f5-180">과거에 발생한 문제를 조사해야 하는 경우 최대 5일 이전에 캡처된 추적에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-180">You can access traces captured up to five days ago when you need to investigate problems happened in the past.</span></span> <span data-ttu-id="1d3f5-181">Azure Portal에서 웹앱의 Application Insights 리소스에 액세스할 수 있는 한 이 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-181">You can choose this option as long as you have access to the web app's Application Insights resource on Azure portal.</span></span>

<span data-ttu-id="1d3f5-182">Application Insights Profiler는 각 웹 호출에 대한 응답 시간 및 느린 응답을 일으키는 코드 줄을 나타내는 추적에 대한 통계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-182">Application Insights Profiler provides statistics on response time for each web call and traces that indicates which line of code caused the slow responses.</span></span> <span data-ttu-id="1d3f5-183">때로는 특정 코드가 성능 기준에 맞게 작성되지 않아 App Service 앱이 느리게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-183">Sometimes the App Service app is slow because certain code is not written in a performant way.</span></span> <span data-ttu-id="1d3f5-184">예를 들어 병렬로 실행될 수 있는 순차 코드와 원하지 않는 데이터베이스 잠금 경합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-184">Examples include sequential code that can be run in parallel and undesired database lock contentions.</span></span> <span data-ttu-id="1d3f5-185">코드에서 이러한 병목 현상을 제거하면 앱 성능이 향상되지만, 정교한 추적과 로그를 설정하지 않으면 감지하기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-185">Removing these bottlenecks in the code increases the app's performance, but they are hard to detect without setting up elaborate traces and logs.</span></span> <span data-ttu-id="1d3f5-186">Application Insights Profiler에 의해 수집된 추적은 응용 프로그램의 속도를 낮추는 코드 줄을 식별하는 데 도움이 되고 App Service 앱에 대한 이 과제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-186">The traces collected by Application Insights Profiler helps identifying the lines of code that slows down the application and overcome this challenge for App Service apps.</span></span>

 <span data-ttu-id="1d3f5-187">자세한 내용은 [Application Insights를 사용하여 라이브 Azure Web Apps 프로파일링](../application-insights/app-insights-profiler.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-187">For more information, see [Profiling live Azure web apps with Application Insights](../application-insights/app-insights-profiler.md).</span></span>

##### <a name="use-remote-profiling"></a><span data-ttu-id="1d3f5-188">원격 프로파일링 사용하기</span><span class="sxs-lookup"><span data-stu-id="1d3f5-188">Use Remote Profiling</span></span>
<span data-ttu-id="1d3f5-189">Azure App Service에서 Web Apps, API Apps 그리고 WebJob을 원격으로 프로파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-189">In Azure App Service, Web Apps, API Apps, and WebJobs can be remotely profiled.</span></span> <span data-ttu-id="1d3f5-190">웹앱 리소스에 대한 액세스가 있고 문제를 재현하는 방법을 알거나 성능 문제가 발생하는 정확한 시간 간격을 알고 있는 경우 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-190">Choose this option if you have access to the web app resource and you know how to reproduce the issue, or if you know the exact time interval the performance issue happens.</span></span>

<span data-ttu-id="1d3f5-191">원격 프로파일링은 프로세스의 CPU 사용량이 높고 프로세스가 예상보다 느리게 실행되거나, HTTP 요청 대기시간이 평상시보다 높은 경우 유용하며, 원격으로 프로세스를 프로파일할 수 있고 프로세스 활동과 코드 hot path를 분석하기 위해 CPU 샘플링 호출 스택을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-191">Remote Profiling is useful if the CPU usage of the process is high and your process is running slower than expected, or the latency of HTTP requests are higher than normal, you can remotely profile your process and get the CPU sampling call stacks to analyze the process activity and code hot paths.</span></span>

<span data-ttu-id="1d3f5-192">자세한 내용은 [Azure App Service에서 원격 프로파일링 지원](https://azure.microsoft.com/blog/remote-profiling-support-in-azure-app-service)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-192">For more information, see [Remote Profiling support in Azure App Service](https://azure.microsoft.com/blog/remote-profiling-support-in-azure-app-service).</span></span>

##### <a name="set-up-diagnostic-traces-manually"></a><span data-ttu-id="1d3f5-193">진단 추적을 수동으로 설정</span><span class="sxs-lookup"><span data-stu-id="1d3f5-193">Set up diagnostic traces manually</span></span>
<span data-ttu-id="1d3f5-194">웹 응용 프로그램 소스 코드에 대한 액세스가 있는 경우 응용 프로그램 진단은 웹 응용 프로그램에서 생성되는 정보를 캡처할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-194">If you have access to the web application source code, Application diagnostics enables you to capture information produced by a web application.</span></span> <span data-ttu-id="1d3f5-195">ASP.NET 응용 프로그램은 정보를 응용 프로그램 진단 로그에 기록하기 위해 `System.Diagnostics.Trace` 클래스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-195">ASP.NET applications can use the `System.Diagnostics.Trace` class to log information to the application diagnostics log.</span></span> <span data-ttu-id="1d3f5-196">그러나 코드를 변경하고 응용 프로그램을 다시 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-196">However, you need to change the code and redeploy your application.</span></span> <span data-ttu-id="1d3f5-197">테스트 환경에서 앱을 실행 중인 경우 이 메서드를 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-197">This method is recommended if your app is running on a testing environment.</span></span>

<span data-ttu-id="1d3f5-198">로깅에 대한 응용 프로그램을 구성하는 방법에 대한 자세한 설명은 [Azure App Service에서 웹앱에 대한 진단 로깅 설정](web-sites-enable-diagnostic-log.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-198">For detailed instructions on how to configure your application for logging, see [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>

#### <a name="use-the-azure-app-service-support-portal"></a><span data-ttu-id="1d3f5-199">Azure App Service 지원 포털 사용</span><span class="sxs-lookup"><span data-stu-id="1d3f5-199">Use the Azure App Service support portal</span></span>
<span data-ttu-id="1d3f5-200">Web Apps는 HTTP 로그, 이벤트 로그, 프로세스 덤프 등등을 확인하여 사용자의 웹앱과 연관된 문제 해결 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-200">Web Apps provides you with the ability to troubleshoot issues related to your web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="1d3f5-201">**http://&lt;your app name>.scm.azurewebsites.net/Support**에서 지원 포털을 사용하여 모든 정보에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-201">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="1d3f5-202">Azure App Service 지원 포털은 일반적인 문제 해결 시나리오의 세 단계를 지원하기 위해 3개의 별도 탭을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-202">The Azure App Service support portal provides you with three separate tabs to support the three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="1d3f5-203">현재 동작을 관찰하기</span><span class="sxs-lookup"><span data-stu-id="1d3f5-203">Observe current behavior</span></span>
2. <span data-ttu-id="1d3f5-204">진단 정보 수집 및 기본 제공 분석기를 실행하여 분석하기</span><span class="sxs-lookup"><span data-stu-id="1d3f5-204">Analyze by collecting diagnostics information and running the built-in analyzers</span></span>
3. <span data-ttu-id="1d3f5-205">완화</span><span class="sxs-lookup"><span data-stu-id="1d3f5-205">Mitigate</span></span>

<span data-ttu-id="1d3f5-206">지금 문제가 발생했다면, **분석** > **진단** > **바로 진단**을 클릭하여 HTTP 로그, 이벤트 뷰어 로그, 메모리 덤프, PHP 오류 로그 및 PHP 보고서를 수집하는 진단 세션을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-206">If the issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** to create a diagnostic session for you, which collects HTTP logs, event viewer logs, memory dumps, PHP error logs, and PHP process report.</span></span>

<span data-ttu-id="1d3f5-207">데이터가 수집되면, 지원 포털은 데이터에 대한 분석을 실행하고 HTML 보고서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-207">Once the data is collected, the support portal runs an analysis on the data and provides you with an HTML report.</span></span>

<span data-ttu-id="1d3f5-208">데이터를 다운로드할 경우 기본적으로 D:\home\data\DaaS folder에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-208">In case you want to download the data, by default, it would be stored in the D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="1d3f5-209">Azure App Service 지원 포털에 대한 자세한 내용은 [Azure Websites의 지원 사이트 확장에 대한 새 업데이트](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-209">For more information on the Azure App Service support portal, see [New Updates to Support Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-the-kudu-debug-console"></a><span data-ttu-id="1d3f5-210">Kudu 디버그 콘솔 사용</span><span class="sxs-lookup"><span data-stu-id="1d3f5-210">Use the Kudu Debug Console</span></span>
<span data-ttu-id="1d3f5-211">Web Apps는 사용자 환경에 대한 정보를 얻을 수 있는 JSON 끝점과 비슷한 디버깅, 탐색, 파일 업로드할 수 있는 디버그 콘솔과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-211">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="1d3f5-212">이 콘솔은 *Kudu 콘솔* 또는 사용자 웹앱에서는 *SCM 대시보드*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-212">This console is called the *Kudu Console* or the *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="1d3f5-213">**https://&lt;Your app name>.scm.azurewebsites.net/** 링크로 이동해서 대시보드에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-213">You can access this dashboard by going to the link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="1d3f5-214">Kudu가 제공하는 것은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-214">Some of the things that Kudu provides are:</span></span>

* <span data-ttu-id="1d3f5-215">응용 프로그램에 대한 환경 설정</span><span class="sxs-lookup"><span data-stu-id="1d3f5-215">environment settings for your application</span></span>
* <span data-ttu-id="1d3f5-216">로그 스트림</span><span class="sxs-lookup"><span data-stu-id="1d3f5-216">log stream</span></span>
* <span data-ttu-id="1d3f5-217">진단 덤프</span><span class="sxs-lookup"><span data-stu-id="1d3f5-217">diagnostic dump</span></span>
* <span data-ttu-id="1d3f5-218">Powershell cmdlet 및 기본 DOS 명령을 실행할 수 있는 콘솔을 디버깅합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-218">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="1d3f5-219">Kudu의 또 다른 유용한 기능은 응용 프로그램에 첫 번째 예외가 발생할 경우, 메모리 덤프를 만들기 위해 Kudu와 SysInternal 도구 Procdump를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-219">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and the SysInternals tool Procdump to create memory dumps.</span></span> <span data-ttu-id="1d3f5-220">메모리 덤프는 프로세스의 스냅숏이며 웹앱의 더욱 복잡한 문제를 해결하는 데 많은 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-220">These memory dumps are snapshots of the process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="1d3f5-221">Kudu에서 사용 가능한 기능에 대한 자세한 내용은 [사용자가 꼭 알아야 할 Azure Websites 팀 서비스 도구](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-221">For more information on features available in Kudu, see [Azure Websites Team Services tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-the-issue"></a><span data-ttu-id="1d3f5-222">3. 문제 완화</span><span class="sxs-lookup"><span data-stu-id="1d3f5-222">3. Mitigate the issue</span></span>
#### <a name="scale-the-web-app"></a><span data-ttu-id="1d3f5-223">웹앱의 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-223">Scale the web app</span></span>
<span data-ttu-id="1d3f5-224">Azure App Service에서 성능과 처리량의 증가를 위해 사용자가 실행하는 응용 프로그램의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-224">In Azure App Service, for increased performance and throughput,  you can adjust the scale at which you are running your application.</span></span> <span data-ttu-id="1d3f5-225">웹앱의 크기를 키우려면 두 가지 사항이 수반됩니다. App Service 계획을 더 높은 가격 책정 계층으로 바꿔야 하며, 높은 가격 계층으로 전환한 후에 특정 설정을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-225">Scaling up a web app involves two related actions: changing your App Service plan to a higher pricing tier, and configuring certain settings after you have switched to the higher pricing tier.</span></span>

<span data-ttu-id="1d3f5-226">크기 조정에 대한 자세한 내용은 [Azure App Service에서 웹앱 크기 조정](web-sites-scale.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-226">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="1d3f5-227">또한 둘 이상의 인스턴스에서 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-227">Additionally, you can choose to run your application on more than one instance.</span></span> <span data-ttu-id="1d3f5-228">크기 확장은 더 많은 처리 기능을 제공할 뿐만 아니라, 어느 정도의 내결함성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-228">Scaling out not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="1d3f5-229">하나의 인스턴스에서 프로세스가 다운되면, 또 다른 인스턴스에서 계속 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-229">If the process goes down on one instance, the other instances continue to serve requests.</span></span>

<span data-ttu-id="1d3f5-230">수동 또는 자동으로 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-230">You can set the scaling to be Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="1d3f5-231">AutoHeal를 사용</span><span class="sxs-lookup"><span data-stu-id="1d3f5-231">Use AutoHeal</span></span>
<span data-ttu-id="1d3f5-232">AutoHeal은 사용자가 선택한 설정(예: 구성 변경, 요청, 메모리 기반 제한 또는 요청을 실행하는데 필요한 시간)에 따라 앱에 대한 작업자 프로세스를 재활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-232">AutoHeal recycles the worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or the time needed to execute a request).</span></span> <span data-ttu-id="1d3f5-233">대부분의 경우에는 프로세스를 재활용하는 방법이 문제를 해결하는 가장 빠른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-233">Most of the time, recycle the process is the fastest way to recover from a problem.</span></span> <span data-ttu-id="1d3f5-234">Azure Portal 내에서 직접 웹앱을 재시작할 수도 있지만, AutoHeal은 자동으로 재시작을 수행하게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-234">Though you can always restart the web app from directly within the Azure portal, AutoHeal does it automatically for you.</span></span> <span data-ttu-id="1d3f5-235">몇 개의 트리거를 웹앱의 root web.config에 추가하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-235">All you need to do is add some triggers in the root web.config for your web app.</span></span> <span data-ttu-id="1d3f5-236">이 설정은 사용자의 응용 프로그램이 .Net 앱이 아니라도 같은 방식으로 작동됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-236">These settings would work in the same way even if your application is not a .Net app.</span></span>

<span data-ttu-id="1d3f5-237">자세한 내용은 [Auto-Healing Azure Websites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-237">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-the-web-app"></a><span data-ttu-id="1d3f5-238">웹앱 재시작</span><span class="sxs-lookup"><span data-stu-id="1d3f5-238">Restart the web app</span></span>
<span data-ttu-id="1d3f5-239">재시작은 일회성 문제를 해결하는 가장 간단한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-239">Restarting is often the simplest way to recover from one-time issues.</span></span> <span data-ttu-id="1d3f5-240">[Azure Portal](https://portal.azure.com/) 또는 웹앱의 블레이드에서 앱을 멈추거나 재시작하는 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-240">On the [Azure portal](https://portal.azure.com/), on your web app’s blade, you have the options to stop or restart your app.</span></span>

 ![웹앱을 다시 시작하여 성능 문제 해결](./media/app-service-web-troubleshoot-performance-degradation/2-restart.png)

<span data-ttu-id="1d3f5-242">또한, Azure Powershell을 사용하여 웹앱을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-242">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="1d3f5-243">자세한 내용은 [Azure 리소스 관리자에서 Azure PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-243">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

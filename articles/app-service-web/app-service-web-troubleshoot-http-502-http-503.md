---
title: "502 잘못된 게이트웨이, 503 서비스를 사용할 수 없음 오류 수정 | Microsoft Docs"
description: "Azure 앱 서비스에서 호스트되는 웹앱의 502 잘못된 게이트웨이 및 503 서비스를 사용할 수 없음 오류를 해결합니다."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "502 잘못된 게이트웨이, 503 서비스를 사용할 수 없음, 오류 503, 오류 502"
ms.assetid: 51cd331a-a3fa-438f-90ef-385e755e50d5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 397a6aaf7dc27adfa0fc0e722b8a2be5cc1d75f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a><span data-ttu-id="56edd-104">Azure 웹앱의 "502 잘못된 게이트웨이" 및 "503 서비스를 사용할 수 없음" HTTP 오류 해결</span><span class="sxs-lookup"><span data-stu-id="56edd-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>
<span data-ttu-id="56edd-105">"502 잘못된 게이트웨이" 및 "503 서비스를 사용할 수 없음" 오류는 [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)에서 호스트되는 웹앱에서 일반적으로 나타나는 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="56edd-106">이 문서는 이러한 오류를 해결하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-106">This article helps you troubleshoot these errors.</span></span>

<span data-ttu-id="56edd-107">이 문서의 어디에서든 도움이 필요한 경우 [MSDN Azure 및 스택 오버플로 포럼](https://azure.microsoft.com/support/forums/)에서 Azure 전문가에게 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-107">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="56edd-108">또는 Azure 기술 지원 인시던트를 제출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-108">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="56edd-109">[Azure 지원 사이트](https://azure.microsoft.com/support/options/) 로 이동한 다음 **지원 받기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-109">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="56edd-110">증상</span><span class="sxs-lookup"><span data-stu-id="56edd-110">Symptom</span></span>
<span data-ttu-id="56edd-111">웹앱을 찾아볼 때 HTTP "502 잘못된 게이트웨이" 또는 HTTP "503 서비스를 사용할 수 없음" 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-111">When you browse to the web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span></span>

## <a name="cause"></a><span data-ttu-id="56edd-112">원인</span><span class="sxs-lookup"><span data-stu-id="56edd-112">Cause</span></span>
<span data-ttu-id="56edd-113">이 문제는 응용 프로그램 수준 문제가 원인이 되는 경우가 많습니다. 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="56edd-113">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="56edd-114">긴 요청 시간</span><span class="sxs-lookup"><span data-stu-id="56edd-114">requests taking a long time</span></span>
* <span data-ttu-id="56edd-115">높은 메모리/CPU를 사용하는 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="56edd-115">application using high memory/CPU</span></span>
* <span data-ttu-id="56edd-116">예외로 인해 충돌하는 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="56edd-116">application crashing due to an exception.</span></span>

## <a name="troubleshooting-steps-to-solve-502-bad-gateway-and-503-service-unavailable-errors"></a><span data-ttu-id="56edd-117">"502 잘못된 게이트웨이" 및 "503 서비스를 사용할 수 없음" 오류를 해결하기 위한 문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="56edd-117">Troubleshooting steps to solve "502 bad gateway" and "503 service unavailable" errors</span></span>
<span data-ttu-id="56edd-118">문제 해결은 해결하는 순서대로 세 가지로 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="56edd-119">응용 프로그램 작동을 관찰 및 감시</span><span class="sxs-lookup"><span data-stu-id="56edd-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="56edd-120">데이터 수집</span><span class="sxs-lookup"><span data-stu-id="56edd-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="56edd-121">문제 완화</span><span class="sxs-lookup"><span data-stu-id="56edd-121">Mitigate the issue</span></span>](#mitigate)

<span data-ttu-id="56edd-122">[App Service Web Apps](/services/app-service/web/)는 각 단계별로 다양한 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="56edd-123">1. 응용 프로그램 작동을 관찰 및 감시 </span><span class="sxs-lookup"><span data-stu-id="56edd-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="56edd-124">서비스 상태를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-124">Track Service health</span></span>
<span data-ttu-id="56edd-125">Microsoft Azure는 서비스가 중단되거나 성능이 저하될 때마다 경고를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="56edd-126">[Azure 포털](https://portal.azure.com/)에서 서비스의 상태를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-126">You can track the health of the service on the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="56edd-127">자세한 내용은 [서비스 상태 추적](../monitoring-and-diagnostics/insights-service-health.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56edd-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="56edd-128">웹앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="56edd-128">Monitor your web app</span></span>
<span data-ttu-id="56edd-129">이 옵션은 응용 프로그램의 문제를 해결할 수 있게 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-129">This option enables you to find out if your application is having any issues.</span></span> <span data-ttu-id="56edd-130">웹앱의 블레이드에서 **요청 및 오류** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-130">In your web app’s blade, click the **Requests and errors** tile.</span></span> <span data-ttu-id="56edd-131">**메트릭** 블레이드는 추가 가능한 모든 메트릭을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-131">The **Metric** blade will show you all the metrics you can add.</span></span>

<span data-ttu-id="56edd-132">모니터링 하고자 하는 웹앱의 일부 메트릭은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-132">Some of the metrics that you might want to monitor for your web app are</span></span>

* <span data-ttu-id="56edd-133">평균 메모리 작업 집합</span><span class="sxs-lookup"><span data-stu-id="56edd-133">Average memory working set</span></span>
* <span data-ttu-id="56edd-134">평균 응답 시간</span><span class="sxs-lookup"><span data-stu-id="56edd-134">Average response time</span></span>
* <span data-ttu-id="56edd-135">CPU 시간</span><span class="sxs-lookup"><span data-stu-id="56edd-135">CPU time</span></span>
* <span data-ttu-id="56edd-136">메모리 작업 집합</span><span class="sxs-lookup"><span data-stu-id="56edd-136">Memory working set</span></span>
* <span data-ttu-id="56edd-137">요청</span><span class="sxs-lookup"><span data-stu-id="56edd-137">Requests</span></span>

![웹앱을 모니터링하여 502 잘못된 게이트웨이 및 503 서비스를 사용할 수 없음 HTTP 오류 해결](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

<span data-ttu-id="56edd-139">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56edd-139">For more information, see:</span></span>

* [<span data-ttu-id="56edd-140">Azure App Service에서 Web Apps 모니터링</span><span class="sxs-lookup"><span data-stu-id="56edd-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="56edd-141">경고 알림 받기</span><span class="sxs-lookup"><span data-stu-id="56edd-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="56edd-142">2. 데이터 수집</span><span class="sxs-lookup"><span data-stu-id="56edd-142">2. Collect data</span></span>
#### <a name="use-the-azure-app-service-support-portal"></a><span data-ttu-id="56edd-143">Azure 앱 서비스 지원 포털 사용</span><span class="sxs-lookup"><span data-stu-id="56edd-143">Use the Azure App Service Support Portal</span></span>
<span data-ttu-id="56edd-144">웹앱은 HTTP 로그, 이벤트 로그, 프로세스 덤프 등등을 확인하여 사용자의 웹앱과 연관된 문제 해결 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-144">Web Apps provides you with the ability to troubleshoot issues related to your web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="56edd-145">**http://&lt;your app name>.scm.azurewebsites.net/Support**에서 지원 포털을 사용하여 모든 정보에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="56edd-146">Azure 앱 서비스 지원 포털은 일반적인 문제 해결 시나리오의 세 단계를 지원하기 위해 3개의 별도 탭을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-146">The Azure App Service Support portal provides you with three separate tabs to support the three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="56edd-147">현재 동작을 관찰하기</span><span class="sxs-lookup"><span data-stu-id="56edd-147">Observe current behavior</span></span>
2. <span data-ttu-id="56edd-148">진단 정보 수집 및 기본 제공 분석기를 실행하여 분석하기</span><span class="sxs-lookup"><span data-stu-id="56edd-148">Analyze by collecting diagnostics information and running the built-in analyzers</span></span>
3. <span data-ttu-id="56edd-149">완화</span><span class="sxs-lookup"><span data-stu-id="56edd-149">Mitigate</span></span>

<span data-ttu-id="56edd-150">지금 문제가 발생했다면, **분석** > **진단** > **바로 진단**을 클릭하여 HTTP 로그, 이벤트 뷰어 로그, 메모리 덤프, PHP 오류 로그 및 PHP 보고서를 수집하는 진단 세션을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-150">If the issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** to create a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span></span>

<span data-ttu-id="56edd-151">데이터가 수집되면, 데이터에 대한 분석하고 HTML 보고서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-151">Once the data is collected, it will also run an analysis on the data and provide you with an HTML report.</span></span>

<span data-ttu-id="56edd-152">데이터를 다운로드할 경우 기본적으로 D:\home\data\DaaS folder에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-152">In case you want to download the data, by default, it would be stored in the D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="56edd-153">Azure 앱 서비스 지원 포털에 대한 자세한 내용은 [Azure 웹 사이트의 지원 사이트 확장에 대한 새 업데이트](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56edd-153">For more information on the Azure App Service Support portal, see [New Updates to Support Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-the-kudu-debug-console"></a><span data-ttu-id="56edd-154">Kudu 디버그 콘솔 사용</span><span class="sxs-lookup"><span data-stu-id="56edd-154">Use the Kudu Debug Console</span></span>
<span data-ttu-id="56edd-155">웹앱은 사용자 환경에 대한 정보를 얻을 수 있는 JSON 끝점과 비슷한 디버깅, 탐색, 파일 업로드할 수 있는 디버그 콘솔과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="56edd-156">이 콘솔은 *Kudu 콘솔* 또는 사용자 웹앱에서는 *SCM 대시보드*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-156">This is called the *Kudu Console* or the *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="56edd-157">**https://&lt;Your app name>.scm.azurewebsites.net/** 링크로 이동해서 대시보드에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-157">You can access this dashboard by going to the link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="56edd-158">Kudu가 제공하는 것은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-158">Some of the things that Kudu provides are:</span></span>

* <span data-ttu-id="56edd-159">응용 프로그램에 대한 환경 설정</span><span class="sxs-lookup"><span data-stu-id="56edd-159">environment settings for your application</span></span>
* <span data-ttu-id="56edd-160">로그 스트림</span><span class="sxs-lookup"><span data-stu-id="56edd-160">log stream</span></span>
* <span data-ttu-id="56edd-161">진단 덤프</span><span class="sxs-lookup"><span data-stu-id="56edd-161">diagnostic dump</span></span>
* <span data-ttu-id="56edd-162">Powershell cmdlet 및 기본 DOS 명령을 실행할 수 있는 콘솔을 디버깅합니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="56edd-163">Kudu의 또 다른 유용한 기능은 응용 프로그램에 첫 번째 예외가 발생할 경우, 메모리 덤프를 만들기 위해 Kudu와 SysInternal 도구 Procdump를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and the SysInternals tool Procdump to create memory dumps.</span></span> <span data-ttu-id="56edd-164">메모리 덤프는 프로세스의 스냅숏이며 웹앱의 더욱 복잡한 문제를 해결하는 데 많은 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-164">These memory dumps are snapshots of the process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="56edd-165">Kudu에서 사용 가능한 기능에 대한 자세한 내용은 [사용자가 꼭 알아야 할 Azure 웹 사이트 온라인 도구](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56edd-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-the-issue"></a><span data-ttu-id="56edd-166">3. 문제 완화</span><span class="sxs-lookup"><span data-stu-id="56edd-166">3. Mitigate the issue</span></span>
#### <a name="scale-the-web-app"></a><span data-ttu-id="56edd-167">웹앱의 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-167">Scale the web app</span></span>
<span data-ttu-id="56edd-168">Azure App Service에서 성능과 처리량의 증가를 위해 사용자가 실행하는 응용 프로그램의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-168">In Azure App Service, for increased performance and throughput,  you can adjust the scale at which you are running your application.</span></span> <span data-ttu-id="56edd-169">웹앱의 크기를 키우려면 두 가지 사항이 수반됩니다. App Service 계획을 더 높은 가격 책정 계층으로 바꿔야 하며, 높은 가격 계층으로 전환한 후에 특정 설정을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-169">Scaling up a web app involves two related actions: changing your App Service plan to a higher pricing tier, and configuring certain settings after you have switched to the higher pricing tier.</span></span>

<span data-ttu-id="56edd-170">크기 조정에 대한 자세한 내용은 [Azure 앱 서비스에서 웹앱 크기 조정](web-sites-scale.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56edd-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="56edd-171">또한 둘 이상의 인스턴스에서 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-171">Additionally, you can choose to run your application on more than one instance .</span></span> <span data-ttu-id="56edd-172">더 많은 처리 기능을 제공할 만 아니라, 어느 정도의 내결함성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="56edd-173">하나의 인스턴스에서 프로세스가 다운되면, 또 다른 인스턴스에서 계속 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-173">If the process goes down on one instance, the other instance will still continue serving requests.</span></span>

<span data-ttu-id="56edd-174">수동 또는 자동으로 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-174">You can set the scaling to be Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="56edd-175">AutoHeal를 사용</span><span class="sxs-lookup"><span data-stu-id="56edd-175">Use AutoHeal</span></span>
<span data-ttu-id="56edd-176">AutoHeal은 사용자가 선택한 설정(예: 구성 변경, 요청, 메모리 기반 제한 또는 요청을 실행하는데 필요한 시간)에 따라 앱에 대한 작업자 프로세스를 재활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-176">AutoHeal recycles the worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or the time needed to execute a request).</span></span> <span data-ttu-id="56edd-177">대부분의 경우에는 프로세스를 재활용하는 방법이 문제를 해결하는 가장 빠른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-177">Most of the time, recycle the process is the fastest way to recover from a problem.</span></span> <span data-ttu-id="56edd-178">Azure 포털 내에서 직접 웹앱을 재시작할 수도 있지만, AutoHeal은 자동으로 재시작을 수행하게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-178">Though you can always restart the web app from directly within the Azure Portal, AutoHeal will do it automatically for you.</span></span> <span data-ttu-id="56edd-179">몇 개의 트리거를 웹앱의 root web.config에 추가하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-179">All you need to do is add some triggers in the root web.config for your web app.</span></span> <span data-ttu-id="56edd-180">이 설정은 사용자의 응용 프로그램이 .Net이 아니라도 같은 방식으로 작동됩니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-180">Note that these settings would work in the same way even if your application is not a .Net one.</span></span>

<span data-ttu-id="56edd-181">자세한 내용은 [Auto-Healing Azure 웹 사이트](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56edd-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-the-web-app"></a><span data-ttu-id="56edd-182">웹앱 재시작</span><span class="sxs-lookup"><span data-stu-id="56edd-182">Restart the web app</span></span>
<span data-ttu-id="56edd-183">이 방법은 일회성 문제를 해결하는 가장 간단한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-183">This is often the simplest way to recover from one-time issues.</span></span> <span data-ttu-id="56edd-184">[Azure 포털](https://portal.azure.com/)또는 웹앱의 블레이드에서 앱을 멈추거나 재시작 하는 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-184">On the [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have the options to stop or restart your app.</span></span>

 ![앱을 다시 시작하여 502 잘못된 게이트웨이 및 503 서비스를 사용할 수 없음 HTTP 오류 해결](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

<span data-ttu-id="56edd-186">또한, Azure Powershell을 사용하여 웹앱을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56edd-186">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="56edd-187">자세한 내용은 [Azure 리소스 관리자에서 Azure PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56edd-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>


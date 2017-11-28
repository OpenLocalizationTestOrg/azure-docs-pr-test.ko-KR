---
title: "잘못 된 게이트웨이 aaaFix 502, 503 서비스 사용할 수 없음 오류 | Microsoft Docs"
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
ms.openlocfilehash: d9d8dcddaac930967a2e8d2bfd8cad09e6824c17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a><span data-ttu-id="92c2b-104">Azure 웹앱의 "502 잘못된 게이트웨이" 및 "503 서비스를 사용할 수 없음" HTTP 오류 해결</span><span class="sxs-lookup"><span data-stu-id="92c2b-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>
<span data-ttu-id="92c2b-105">"502 잘못된 게이트웨이" 및 "503 서비스를 사용할 수 없음" 오류는 [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)에서 호스트되는 웹앱에서 일반적으로 나타나는 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="92c2b-106">이 문서는 이러한 오류를 해결하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-106">This article helps you troubleshoot these errors.</span></span>

<span data-ttu-id="92c2b-107">이 문서에서 언제 든 지 자세한 도움말을 보려는 경우 문의할 수 있습니다에 Azure 전문가 hello [MSDN Azure hello 및 스택 오버플로 포럼 hello](https://azure.microsoft.com/support/forums/)합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-107">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="92c2b-108">또는 Azure 기술 지원 인시던트를 제출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-108">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="92c2b-109">Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/support/options/) 을 클릭할 **Get Support**합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-109">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="92c2b-110">증상</span><span class="sxs-lookup"><span data-stu-id="92c2b-110">Symptom</span></span>
<span data-ttu-id="92c2b-111">HTTP 반환 toohello 웹 앱을 찾아볼 때 "502 잘못 된 게이트웨이" 오류 또는 HTTP "503 서비스를 사용할 수 없음" 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-111">When you browse toohello web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span></span>

## <a name="cause"></a><span data-ttu-id="92c2b-112">원인</span><span class="sxs-lookup"><span data-stu-id="92c2b-112">Cause</span></span>
<span data-ttu-id="92c2b-113">이 문제는 응용 프로그램 수준 문제가 원인이 되는 경우가 많습니다. 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="92c2b-113">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="92c2b-114">긴 요청 시간</span><span class="sxs-lookup"><span data-stu-id="92c2b-114">requests taking a long time</span></span>
* <span data-ttu-id="92c2b-115">높은 메모리/CPU를 사용하는 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="92c2b-115">application using high memory/CPU</span></span>
* <span data-ttu-id="92c2b-116">tooan 예외 인해 충돌 하는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-116">application crashing due tooan exception.</span></span>

## <a name="troubleshooting-steps-toosolve-502-bad-gateway-and-503-service-unavailable-errors"></a><span data-ttu-id="92c2b-117">단계 toosolve "502 잘못 된 게이트웨이" 및 "503 서비스를 사용할 수 없음" 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="92c2b-117">Troubleshooting steps toosolve "502 bad gateway" and "503 service unavailable" errors</span></span>
<span data-ttu-id="92c2b-118">문제 해결은 해결하는 순서대로 세 가지로 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="92c2b-119">응용 프로그램 작동을 관찰 및 감시</span><span class="sxs-lookup"><span data-stu-id="92c2b-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="92c2b-120">데이터 수집</span><span class="sxs-lookup"><span data-stu-id="92c2b-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="92c2b-121">Hello 문제를 완화</span><span class="sxs-lookup"><span data-stu-id="92c2b-121">Mitigate hello issue</span></span>](#mitigate)

<span data-ttu-id="92c2b-122">[App Service Web Apps](/services/app-service/web/)는 각 단계별로 다양한 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="92c2b-123">1. 응용 프로그램 작동을 관찰 및 감시 </span><span class="sxs-lookup"><span data-stu-id="92c2b-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="92c2b-124">서비스 상태를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-124">Track Service health</span></span>
<span data-ttu-id="92c2b-125">Microsoft Azure는 서비스가 중단되거나 성능이 저하될 때마다 경고를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="92c2b-126">Hello에서 hello 서비스의 hello 상태를 추적할 수 있습니다 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-126">You can track hello health of hello service on hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="92c2b-127">자세한 내용은 [서비스 상태 추적](../monitoring-and-diagnostics/insights-service-health.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92c2b-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="92c2b-128">웹앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="92c2b-128">Monitor your web app</span></span>
<span data-ttu-id="92c2b-129">응용 프로그램 문제가 있는 경우 아웃 toofind가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-129">This option enables you toofind out if your application is having any issues.</span></span> <span data-ttu-id="92c2b-130">웹 앱 블레이드 클릭 hello **요청 및 오류** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-130">In your web app’s blade, click hello **Requests and errors** tile.</span></span> <span data-ttu-id="92c2b-131">hello **메트릭을** 블레이드를 추가할 수 있습니다 하는 모든 hello 메트릭이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-131">hello **Metric** blade will show you all hello metrics you can add.</span></span>

<span data-ttu-id="92c2b-132">알았으므로 toomonitor 웹 앱에 대 한 hello 메트릭 중 일부는</span><span class="sxs-lookup"><span data-stu-id="92c2b-132">Some of hello metrics that you might want toomonitor for your web app are</span></span>

* <span data-ttu-id="92c2b-133">평균 메모리 작업 집합</span><span class="sxs-lookup"><span data-stu-id="92c2b-133">Average memory working set</span></span>
* <span data-ttu-id="92c2b-134">평균 응답 시간</span><span class="sxs-lookup"><span data-stu-id="92c2b-134">Average response time</span></span>
* <span data-ttu-id="92c2b-135">CPU 시간</span><span class="sxs-lookup"><span data-stu-id="92c2b-135">CPU time</span></span>
* <span data-ttu-id="92c2b-136">메모리 작업 집합</span><span class="sxs-lookup"><span data-stu-id="92c2b-136">Memory working set</span></span>
* <span data-ttu-id="92c2b-137">요청</span><span class="sxs-lookup"><span data-stu-id="92c2b-137">Requests</span></span>

![웹앱을 모니터링하여 502 잘못된 게이트웨이 및 503 서비스를 사용할 수 없음 HTTP 오류 해결](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

<span data-ttu-id="92c2b-139">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92c2b-139">For more information, see:</span></span>

* [<span data-ttu-id="92c2b-140">Azure App Service에서 Web Apps 모니터링</span><span class="sxs-lookup"><span data-stu-id="92c2b-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="92c2b-141">경고 알림 받기</span><span class="sxs-lookup"><span data-stu-id="92c2b-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="92c2b-142">2. 데이터 수집</span><span class="sxs-lookup"><span data-stu-id="92c2b-142">2. Collect data</span></span>
#### <a name="use-hello-azure-app-service-support-portal"></a><span data-ttu-id="92c2b-143">Azure 앱 서비스 지원 포털 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="92c2b-143">Use hello Azure App Service Support Portal</span></span>
<span data-ttu-id="92c2b-144">웹 앱을 사용 하면 HTTP 로그, 이벤트 로그, 프로세스 덤프 및 자세히 확인 하 여 hello 기능 tootroubleshoot 문제 관련된 tooyour 웹 앱으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-144">Web Apps provides you with hello ability tootroubleshoot issues related tooyour web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="92c2b-145">**http://&lt;your app name>.scm.azurewebsites.net/Support**에서 지원 포털을 사용하여 모든 정보에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="92c2b-146">hello Azure 앱 서비스 지원 포털 세 가지 별도 탭 toosupport hello의 세 단계는 일반적인 문제 해결 시나리오를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-146">hello Azure App Service Support portal provides you with three separate tabs toosupport hello three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="92c2b-147">현재 동작을 관찰하기</span><span class="sxs-lookup"><span data-stu-id="92c2b-147">Observe current behavior</span></span>
2. <span data-ttu-id="92c2b-148">진단 정보 수집 및 기본 제공 분석기 hello를 실행 하 여 분석</span><span class="sxs-lookup"><span data-stu-id="92c2b-148">Analyze by collecting diagnostics information and running hello built-in analyzers</span></span>
3. <span data-ttu-id="92c2b-149">완화</span><span class="sxs-lookup"><span data-stu-id="92c2b-149">Mitigate</span></span>

<span data-ttu-id="92c2b-150">지금 바로 hello 문제 상황을 클릭 하 여 **분석** > **진단** > **이제 진단** toocreate, 진단 세션을 HTTP를 수집 합니다는 기록, 이벤트 뷰어 로그 메모리 덤프, PHP 오류 로그 및 PHP 보고서를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-150">If hello issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** toocreate a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span></span>

<span data-ttu-id="92c2b-151">Hello 데이터 수집 되 면 또한 hello 데이터에 대 한 분석을 실행 하 고 HTML 보고서를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-151">Once hello data is collected, it will also run an analysis on hello data and provide you with an HTML report.</span></span>

<span data-ttu-id="92c2b-152">기본적으로 toodownload hello 데이터를 원하는 경우에 hello D:\home\data\DaaS 폴더에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-152">In case you want toodownload hello data, by default, it would be stored in hello D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="92c2b-153">Azure 앱 서비스 지원 포털 hello에 대 한 자세한 내용은 참조 하십시오. [새 업데이트 tooSupport Azure 웹 사이트에 대 한 사이트 확장](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites)합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-153">For more information on hello Azure App Service Support portal, see [New Updates tooSupport Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-hello-kudu-debug-console"></a><span data-ttu-id="92c2b-154">Hello Kudu 디버그 콘솔을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="92c2b-154">Use hello Kudu Debug Console</span></span>
<span data-ttu-id="92c2b-155">Web Apps는 사용자 환경에 대한 정보를 얻을 수 있는 JSON 끝점과 비슷한 디버깅, 탐색, 파일 업로드할 수 있는 디버그 콘솔과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="92c2b-156">Hello 라고 *Kudu 콘솔* 또는 hello *SCM 대시보드* 웹 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-156">This is called hello *Kudu Console* or hello *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="92c2b-157">Toohello 링크 이동 하 여이 대시보드에 액세스할 수 **https://&lt;응용 프로그램 이름 >.scm.azurewebsites.net/**합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-157">You can access this dashboard by going toohello link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="92c2b-158">Kudu는 제공 하는 hello 것은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-158">Some of hello things that Kudu provides are:</span></span>

* <span data-ttu-id="92c2b-159">응용 프로그램에 대한 환경 설정</span><span class="sxs-lookup"><span data-stu-id="92c2b-159">environment settings for your application</span></span>
* <span data-ttu-id="92c2b-160">로그 스트림</span><span class="sxs-lookup"><span data-stu-id="92c2b-160">log stream</span></span>
* <span data-ttu-id="92c2b-161">진단 덤프</span><span class="sxs-lookup"><span data-stu-id="92c2b-161">diagnostic dump</span></span>
* <span data-ttu-id="92c2b-162">Powershell cmdlet 및 기본 DOS 명령을 실행할 수 있는 콘솔을 디버깅합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="92c2b-163">Kudu의 또 다른 유용한 특징은, 응용 프로그램 첫째 예외를 throw 하는 경우에 대비 Kudu를 사용할 수 있습니다 hello SysInternals 도구 Procdump toocreate 메모리 덤프입니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and hello SysInternals tool Procdump toocreate memory dumps.</span></span> <span data-ttu-id="92c2b-164">이러한 메모리 덤프 hello 프로세스의 스냅숏입니다 및 웹 앱과 함께 보다 복잡 한 문제를 해결 하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-164">These memory dumps are snapshots of hello process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="92c2b-165">Kudu에서 사용 가능한 기능에 대한 자세한 내용은 [사용자가 꼭 알아야 할 Azure 웹 사이트 온라인 도구](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92c2b-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a><span data-ttu-id="92c2b-166">3. Hello 문제를 완화</span><span class="sxs-lookup"><span data-stu-id="92c2b-166">3. Mitigate hello issue</span></span>
#### <a name="scale-hello-web-app"></a><span data-ttu-id="92c2b-167">배율 hello 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="92c2b-167">Scale hello web app</span></span>
<span data-ttu-id="92c2b-168">향상 된 성능 / 처리량에 대 한 Azure 앱 서비스의 응용 프로그램을 실행 하는 hello 눈금을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-168">In Azure App Service, for increased performance and throughput,  you can adjust hello scale at which you are running your application.</span></span> <span data-ttu-id="92c2b-169">두 개의 관련 된 동작에서는 웹 앱 확장: toohello 높은 가격 책정 계층을 전환한 후 특정 설정을 구성 하 고 가격 책정 계층을 더 높은 완료 된 앱 서비스 계획 tooa 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-169">Scaling up a web app involves two related actions: changing your App Service plan tooa higher pricing tier, and configuring certain settings after you have switched toohello higher pricing tier.</span></span>

<span data-ttu-id="92c2b-170">크기 조정에 대한 자세한 내용은 [Azure App Service에서 웹앱 크기 조정](web-sites-scale.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92c2b-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="92c2b-171">또한 둘 이상의 인스턴스에서 응용 프로그램 toorun를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-171">Additionally, you can choose toorun your application on more than one instance .</span></span> <span data-ttu-id="92c2b-172">더 많은 처리 기능을 제공할 만 아니라, 어느 정도의 내결함성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="92c2b-173">Hello 프로세스의 작동이 1 인스턴스에서 hello 다른 인스턴스는 여전히 계속 요청 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-173">If hello process goes down on one instance, hello other instance will still continue serving requests.</span></span>

<span data-ttu-id="92c2b-174">Hello toobe 수동 또는 자동 크기 조정을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-174">You can set hello scaling toobe Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="92c2b-175">AutoHeal를 사용</span><span class="sxs-lookup"><span data-stu-id="92c2b-175">Use AutoHeal</span></span>
<span data-ttu-id="92c2b-176">AutoHeal (예: 구성 변경, 요청, 메모리 기반 제한 또는 hello 시간 tooexecute 요청 필요)를 선택 하는 설정에 따라 응용 프로그램에 대 한 hello 작업자 프로세스를 재활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-176">AutoHeal recycles hello worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or hello time needed tooexecute a request).</span></span> <span data-ttu-id="92c2b-177">대부분의 hello 재활용 hello 프로세스는 문제로 인해 hello 가장 빠른 방법은 toorecover 합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-177">Most of hello time, recycle hello process is hello fastest way toorecover from a problem.</span></span> <span data-ttu-id="92c2b-178">경우에 항상 hello Azure 포털 내에서 직접 hello 웹 앱에서 다시 시작할 수 있습니다, AutoHeal 까 자동으로 드립니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-178">Though you can always restart hello web app from directly within hello Azure Portal, AutoHeal will do it automatically for you.</span></span> <span data-ttu-id="92c2b-179">웹 앱에 대 한 hello 루트 web.config에 몇 가지는 트리거를 추가 하면 toodo 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-179">All you need toodo is add some triggers in hello root web.config for your web app.</span></span> <span data-ttu-id="92c2b-180">참고는 이러한 설정이 작동 하는 hello 동일한 방식으로 된 경우에 응용 프로그램 하나.Net 합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-180">Note that these settings would work in hello same way even if your application is not a .Net one.</span></span>

<span data-ttu-id="92c2b-181">자세한 내용은 [Auto-Healing Azure Websites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92c2b-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-hello-web-app"></a><span data-ttu-id="92c2b-182">Hello 웹 앱을 다시 시작</span><span class="sxs-lookup"><span data-stu-id="92c2b-182">Restart hello web app</span></span>
<span data-ttu-id="92c2b-183">이 일회성 문제에서 가장 간단한 방법은 toorecover hello 자주 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-183">This is often hello simplest way toorecover from one-time issues.</span></span> <span data-ttu-id="92c2b-184">Hello에 [Azure 포털](https://portal.azure.com/), 웹 앱의 블레이드에서 hello 옵션 toostop 했거나 응용 프로그램을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-184">On hello [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have hello options toostop or restart your app.</span></span>

 ![응용 프로그램 toosolve HTTP 오류 502 잘못 된 게이트웨이 및 사용할 수 없는 503 서비스를 다시 시작](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

<span data-ttu-id="92c2b-186">또한, Azure Powershell을 사용하여 웹앱을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92c2b-186">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="92c2b-187">자세한 내용은 [Azure 리소스 관리자에서 Azure PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92c2b-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>


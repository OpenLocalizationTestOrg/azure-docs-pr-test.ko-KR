---
title: "웹 앱 aaaMonitor | Microsoft Docs"
description: "자세한 방법을 tooset 웹 앱에 대 한 모니터링 구성"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: c2f5e9842c732a804f1caee5d67e53dad24e190a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-app-service"></a><span data-ttu-id="77c5b-103">App Service 모니터링</span><span class="sxs-lookup"><span data-stu-id="77c5b-103">Monitor App Service</span></span>
<span data-ttu-id="77c5b-104">이 자습서에서는 응용 프로그램을 모니터링 하 고 발생 하는 경우 기본 제공 플랫폼 도구 toosolve 문제가 hello를 사용 하 여 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-104">This tutorial walks you through monitoring your app and using hello built-in platform tools toosolve problems when they occur.</span></span>

<span data-ttu-id="77c5b-105">이 문서의 각 섹션은 특정 기능을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="77c5b-106">Hello 기능을 함께 사용 하는 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-106">Using hello features together let you:</span></span>
- <span data-ttu-id="77c5b-107">앱 문제 식별</span><span class="sxs-lookup"><span data-stu-id="77c5b-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="77c5b-108">Hello 문제는 코드 또는 hello 플랫폼 인해 발생 하는 시기를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-108">Determining when hello issue is caused by your code or hello platform.</span></span>
- <span data-ttu-id="77c5b-109">Hello 소스 코드에서 hello 문제의 범위를 좁힙니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-109">Narrow down hello source of hello problem in your code.</span></span>
- <span data-ttu-id="77c5b-110">디버깅 하 고 hello 문제를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-110">Debugging and fixing hello issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="77c5b-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="77c5b-111">Before you begin</span></span>
- <span data-ttu-id="77c5b-112">웹 앱 toomonitor 필요 하 고 hello에 따라 단계를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-112">You need a Web App toomonitor and follow hello outlined steps.</span></span>
    - <span data-ttu-id="77c5b-113">Hello에 설명 된 hello 단계 후 응용 프로그램을 만들 수 있습니다 [SQL 데이터베이스를 사용 하 여 Azure에 ASP.NET 응용 프로그램을 만들](app-service-web-tutorial-dotnet-sqldatabase.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-113">You can create an application following hello steps described in hello [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="77c5b-114">Tootry 하려는 경우 **원격 디버깅** Visual Studio 응용 프로그램의 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-114">If you want tootry out **Remote Debugging** of your application, you need Visual Studio.</span></span>
    - <span data-ttu-id="77c5b-115">설치 된 Visual Studio 2017 없는 경우 다운로드 하 고 무료 hello를 사용 하 여 수 [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-115">If you don’t already have Visual Studio 2017 installed, you can download and use hello free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
    - <span data-ttu-id="77c5b-116">사용할 수 있는지 확인 **Azure 개발** hello Visual Studio 설정 중입니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-116">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

## <span data-ttu-id="77c5b-117"><a name="metrics"></a> 1단계 - 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="77c5b-117"><a name="metrics"></a> Step 1 - View metrics</span></span>
<span data-ttu-id="77c5b-118">**메트릭** 유용한 toounderstand 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-118">**Metrics** are useful toounderstand:</span></span>
- <span data-ttu-id="77c5b-119">응용 프로그램 상태</span><span class="sxs-lookup"><span data-stu-id="77c5b-119">Application health</span></span>
- <span data-ttu-id="77c5b-120">앱 성능</span><span class="sxs-lookup"><span data-stu-id="77c5b-120">App performance</span></span>
- <span data-ttu-id="77c5b-121">리소스 사용</span><span class="sxs-lookup"><span data-stu-id="77c5b-121">Resource consumption</span></span>

<span data-ttu-id="77c5b-122">응용 프로그램 문제를 조사할 때 좋은 위치 toostart은 메트릭을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-122">When investigating an application issue, reviewing metrics is a good place toostart.</span></span> <span data-ttu-id="77c5b-123">Azure 포털에 검사를 사용 하 여 응용 프로그램의 hello 메트릭을 신속 하 게 toovisually **Azure 모니터**합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-123">Azure portal has a quick way toovisually inspect hello metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="77c5b-124">메트릭은 앱의 여러 주요 집계에 대한 기록 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="77c5b-125">앱 서비스에서 호스팅되는 모든 앱에 대 한 웹 앱 hello와 hello 앱 서비스 계획 모니터링 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-125">For any app hosted in app service, you should monitor both hello Web App and hello App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="77c5b-126">앱 서비스 계획 사용 하는 실제 리소스 toohost의 hello 컬렉션 응용을 프로그램을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-126">An App Service plan represents hello collection of physical resources used toohost your apps.</span></span> <span data-ttu-id="77c5b-127">앱 서비스 계획 공유 hello 리소스 toosave 비용 허용 여러 앱을 호스트 하는 경우에서 정의한 tooan 할당 하는 모든 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-127">All applications assigned tooan App Service plan share hello resources defined by it allowing you toosave cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="77c5b-128">App Service 계획은 다음을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-128">App Service plans define:</span></span>
> * <span data-ttu-id="77c5b-129">지역: 북유럽, 미국 동부, 동남 아시아 등</span><span class="sxs-lookup"><span data-stu-id="77c5b-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="77c5b-130">인스턴스 크기: 소, 중, 대 등</span><span class="sxs-lookup"><span data-stu-id="77c5b-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="77c5b-131">확장 개수: 1, 2, 3개 인스턴스 등</span><span class="sxs-lookup"><span data-stu-id="77c5b-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="77c5b-132">SKU: 무료, 공유, 기본, 표준, 프리미엄 등</span><span class="sxs-lookup"><span data-stu-id="77c5b-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="77c5b-133">이동 toohello 웹 응용 프로그램에 대 한 메트릭을 tooreview **개요** 블레이드 toomonitor hello 응용 프로그램의 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-133">tooreview metrics for your Web App, go toohello **Overview** blade of hello app you want toomonitor.</span></span> <span data-ttu-id="77c5b-134">여기에서 앱의 메트릭에 대한 차트를 **모니터링 타일**로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="77c5b-135">Hello 타일 tooedit 클릭 어떤 메트릭 tooview를 구성 하 고 시간 범위 toodisplay hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-135">Click hello tile tooedit and configure what metrics tooview and hello time range toodisplay.</span></span>

<span data-ttu-id="77c5b-136">기본 hello 리소스 블레이드도 hello 응용 프로그램 요청에 대 한 뷰 및 지난 1 시간 동안 hello에 대 한 오류를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-136">By default hello resource blade provides a view for hello Application Requests and errors for hello last hour.</span></span>
<span data-ttu-id="77c5b-137">![앱 모니터링](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="77c5b-137">![Monitor App](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="77c5b-138">많은 생성 하는 응용 프로그램이 있다고 hello 예에서 보시 **HTTP 서버 오류**합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-138">As you can see in hello example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="77c5b-139">hello 많은 양의 오류 표시가 hello 첫 번째 tooinvestigate이 응용이 프로그램 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-139">hello high volume of errors is hello first indication we need tooinvestigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="77c5b-140">자세한 정보 Azure 모니터에 대 한 링크를 따라 hello로:</span><span class="sxs-lookup"><span data-stu-id="77c5b-140">Learn more about Azure Monitor with hello following links:</span></span>
> - [<span data-ttu-id="77c5b-141">Azure Monitor 시작</span><span class="sxs-lookup"><span data-stu-id="77c5b-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="77c5b-142">Azure 메트릭</span><span class="sxs-lookup"><span data-stu-id="77c5b-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="77c5b-143">Azure Monitor에서 지원되는 메트릭</span><span class="sxs-lookup"><span data-stu-id="77c5b-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [<span data-ttu-id="77c5b-144">Azure 대시보드</span><span class="sxs-lookup"><span data-stu-id="77c5b-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <span data-ttu-id="77c5b-145"><a name="alerts"></a> 2단계 - 경고 구성</span><span class="sxs-lookup"><span data-stu-id="77c5b-145"><a name="alerts"></a> Step 2 - Configure Alerts</span></span>
<span data-ttu-id="77c5b-146">**경고** 앱에 대 한 특정 조건에 구성 된 tootrigger 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-146">**Alerts** can be configured tootrigger on specific conditions for your app.</span></span>

<span data-ttu-id="77c5b-147">[1 단계-메트릭 확인할](#metrics), hello 응용 프로그램에 오류 수가 있는지에 대해 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-147">In [Step 1 - View metrics](#metrics), we saw that hello application had a high number of errors.</span></span>

<span data-ttu-id="77c5b-148">경고를 구성할 수 있습니다. tooautomatically 오류가 발생 하는 경우 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-148">Lets configure an alert tooautomatically get notified when errors occur.</span></span> <span data-ttu-id="77c5b-149">이 경우 원하는 hello 경고 toosend 하 고 hello HTTP 50 X 오류 수가 특정 임계값을 초과 될 때마다 전자 메일.</span><span class="sxs-lookup"><span data-stu-id="77c5b-149">In this case, we want hello alert toosend and e-mail every time hello number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="77c5b-150">경고, toocreate 너무 이동**모니터링** > **경고** 클릭 **[+], 추가 경고**합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-150">toocreate an alert, navigate too**Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![경고](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="77c5b-152">Hello 경고 구성에 대 한 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-152">Provide values for hello Alert configuration:</span></span>
- <span data-ttu-id="77c5b-153">**리소스:** hello 경고와 사이트 toomonitor hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-153">**Resource:** hello site toomonitor with hello alert.</span></span>
- <span data-ttu-id="77c5b-154">**이름:** 경고의 이름입니다(이 경우 *High HTTP 50X*).</span><span class="sxs-lookup"><span data-stu-id="77c5b-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="77c5b-155">**설명:** 이 경고에 대한 일반 텍스트 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="77c5b-156">**경고 대상:** 경고 대상은 메트릭 또는 이벤트(이 예제에서는 메트릭)가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="77c5b-157">**메트릭:** 이 경우 어떤 메트릭 toomonitor: *HTTP 서버 오류*합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-157">**Metric:** What metric toomonitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="77c5b-158">**조건:** tooalert,이 경우 select hello *보다 큰* 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-158">**Condition:** When tooalert, in this case select hello *greater than* option.</span></span>
- <span data-ttu-id="77c5b-159">**임계값:** 이 경우,에 대 한 값 toolook 사용 이란: *400*합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-159">**Threshold:** What is value toolook for, in this case: *400*.</span></span>
- <span data-ttu-id="77c5b-160">**기간:** 경고 hello는 메트릭의 평균 값을 통해 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-160">**Period:** Alerts operate over hello average value of a metric.</span></span> <span data-ttu-id="77c5b-161">시간이 짧을수록 민감한 경고가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="77c5b-162">이 경우 *5분*입니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-162">in this case we are looking at *5 Minutes*.</span></span>
- <span data-ttu-id="77c5b-163">**메일 소유자 및 참가자:** 이 예에서는 *사용*입니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="77c5b-164">Hello 경고가 만들어지고 전자 메일 했으므로 hello 앱 라인 hello 구성 된 임계값 초과 될 때마다 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-164">Now that hello alert is created an email is sent every time hello app goes over hello configured threshold.</span></span> <span data-ttu-id="77c5b-165">Hello Azure 포털에서에서 활성 경고를 검토할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-165">Active alerts can also be reviewed in hello Azure portal.</span></span>

![트리거된 경고](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="77c5b-167">자세한 정보 Azure 경고에 대 한 링크를 따라 hello로:</span><span class="sxs-lookup"><span data-stu-id="77c5b-167">Learn more about Azure Alerts with hello following links:</span></span>
> - [<span data-ttu-id="77c5b-168">Microsoft Azure의 경고란?</span><span class="sxs-lookup"><span data-stu-id="77c5b-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="77c5b-169">메트릭에 대한 작업</span><span class="sxs-lookup"><span data-stu-id="77c5b-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="77c5b-170">메트릭 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="77c5b-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <span data-ttu-id="77c5b-171"><a name="companion"></a> 3단계 - App Service 도우미</span><span class="sxs-lookup"><span data-stu-id="77c5b-171"><a name="companion"></a> Step 3 - App Service Companion</span></span>
<span data-ttu-id="77c5b-172">**앱 서비스 도우미** 편리 toomonitor 하면 모바일 장치 (iOS 또는 Android)에서 네이티브 환경 사용 하 여 앱을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-172">**App Service companion** offers a convenient way toomonitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="77c5b-173">App Service 도우미를 사용하여 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="77c5b-174">응용 프로그램 메트릭 검토</span><span class="sxs-lookup"><span data-stu-id="77c5b-174">Review application metrics</span></span>
- <span data-ttu-id="77c5b-175">경고 및 권장 사항 검토 및 조치</span><span class="sxs-lookup"><span data-stu-id="77c5b-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="77c5b-176">기본적인 문제 해결 (찾아보기, 시작, 중지, 다시 시작 hello 앱)를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-176">Perform basic troubleshooting (browse, start, stop, restart hello app)</span></span>
- <span data-ttu-id="77c5b-177">중요한 이벤트에 대한 푸시 알림을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-177">Get push notifications for critical events.</span></span>

![App Service 도우미](media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="77c5b-179">[![App Service 도우미 App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service 도우미 Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="77c5b-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="77c5b-180">앱 서비스 도우미 hello에서 설치할 수 있습니다 [앱 스토어](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) 또는 [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="77c5b-180">You can install App Service companion from hello [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <span data-ttu-id="77c5b-181"><a name="diagnose"></a> 4단계 - 문제 진단 및 해결</span><span class="sxs-lookup"><span data-stu-id="77c5b-181"><a name="diagnose"></a> Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="77c5b-182">**문제 진단 및 해결**은 플랫폼 문제와 응용 프로그램 문제를 구분할 수 있도록 도와 줍니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="77c5b-183">웹 앱 백 toohealthy 완화할 수 있는 방법은 tooget를 제안할 수도 것입니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-183">It can also suggest possible mitigations tooget your Web App back toohealthy.</span></span>

![문제 진단 및 해결](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="77c5b-185">Hello 예제 양식 이전 단계를 계속 볼 수 있습니다는 hello 응용 프로그램에 되었습니다 여 고가용성 때 문제가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-185">Continuing with hello example form previous steps, we can see that hello application has been having availably issues.</span></span> <span data-ttu-id="77c5b-186">반면, hello 사용 가능한 플랫폼 100%에서 이동 되지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-186">In contrast, hello platform availability has not moved from 100%.</span></span>

<span data-ttu-id="77c5b-187">때 hello 앱은 문제가 아니며 hello를 플랫폼 유지 되며, 응용 프로그램 문제에 대해 처리 중인 뚜렷한 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-187">When hello app is having issue and hello platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <span data-ttu-id="77c5b-188"><a name="logging"></a>5 단계 - 로깅</span><span class="sxs-lookup"><span data-stu-id="77c5b-188"><a name="logging"></a> Step 5 - Logging</span></span>
<span data-ttu-id="77c5b-189">Hello 오류 tooan 응용 프로그램 문제를 축소 한 우리, 했으므로 자세한 내용은 hello 응용 프로그램 및 서버 로그 tooget에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-189">Now that we have narrowed down hello failures tooan application issue, we can look at hello application and server logs tooget more information.</span></span>

<span data-ttu-id="77c5b-190">로깅을 통해 toocollect 두 **Application Diagnostics** 및 **웹 서버 진단** 웹 앱에 대 한 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-190">Logging allows you toocollect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="77c5b-191">응용 프로그램 진단</span><span class="sxs-lookup"><span data-stu-id="77c5b-191">Application Diagnostics</span></span>
<span data-ttu-id="77c5b-192">응용 프로그램 진단 있습니다 toocapture에서 생성 한 추적 런타임 시 hello 응용 프로그램을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-192">Application diagnostics allows you toocapture traces produced by hello application at runtime.</span></span>

<span data-ttu-id="77c5b-193">추가 추적 tooyour 응용 프로그램 크게 향상 기능 toodebug 및-고정점 문제.</span><span class="sxs-lookup"><span data-stu-id="77c5b-193">Adding tracing tooyour application greatly improves your ability toodebug and pin-point issues.</span></span>

<span data-ttu-id="77c5b-194">Asp.net에서 사용 하 여 응용 프로그램 추적을 기록할 수 있습니다 [System.Diagnostics.Trace 클래스](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) hello 로그 인프라에서 캡처되는 toogenerate 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate events that are captured by hello log infrastructure.</span></span> <span data-ttu-id="77c5b-195">Hello 추적 보다 쉽게 필터링 하는 것에 대 한 hello 심각도 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-195">You can also specify hello severity of hello trace for easier filtering.</span></span>

```csharp
public ActionResult Delete(Guid? id)
{
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id);
    if (id == null)
    {
        System.Diagnostics.Trace.TraceError("/Todos/Delete/ failed, ID is null");
        return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
    }
    Todo todo = db.Todoes.Find(id);
    if (todo == null)
    {
        System.Diagnostics.Trace.TraceWarning("/Todos/Delete/ failed, ID: " + id + " could not be found");
        return HttpNotFound();
    }
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id + "completed successfully");
    return View(todo);
}
```
<span data-ttu-id="77c5b-196">응용 프로그램 로깅 tooenable 너무 이동**모니터링** > **진단 로그** 응용 프로그램 로깅 사용 hello 설정/해제를 사용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-196">tooenable Application logging Go too**Monitoring** > **Diagnostic Logs** and Enable Application Logging using hello toggles.</span></span>

![앱 모니터링](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="77c5b-198">응용 프로그램 로그에는 tooblob 저장소 푸시할 또는 저장된 tooyour 웹 앱의 파일 시스템 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-198">Application logs can be stored tooyour Web App's file system or pushed out tooblob storage.</span></span> <span data-ttu-id="77c5b-199">프로덕션 시나리오 권장된 toouse blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-199">For production scenarios, it's recommended toouse blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77c5b-200">로깅을 사용하도록 설정하면 응용 프로그램 성능과 리소스 사용률에 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="77c5b-201">프로덕션 시나리오에서는 오류 로그를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="77c5b-202">자세한 로깅은 문제를 조사할 때만 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="77c5b-203">웹 서버 진단</span><span class="sxs-lookup"><span data-stu-id="77c5b-203">Web Server Diagnostics</span></span>
<span data-ttu-id="77c5b-204">앱이 계측되지 않는 경우에도 웹 서버 로그는 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="77c5b-205">App Service에서는 세 가지 종류의 서버 로그를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="77c5b-206">**웹 서버 로깅**</span><span class="sxs-lookup"><span data-stu-id="77c5b-206">**Web Server Logging**</span></span>
    - <span data-ttu-id="77c5b-207">Hello를 사용 하 여 HTTP 트랜잭션에 대 한 내용은 [W3C 확장된 로그 파일 형식](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-207">Information about HTTP transactions using hello [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
    - <span data-ttu-id="77c5b-208">특정 IP 주소에서 요청 처리 hello 수 또는 요청 수와 같은 전반적인 사이트 메트릭을 결정할 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-208">Useful when determining overall site metrics such as hello number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="77c5b-209">**자세한 오류 로깅**</span><span class="sxs-lookup"><span data-stu-id="77c5b-209">**Detailed Error Logging**</span></span>
    - <span data-ttu-id="77c5b-210">오류를 나타내는 HTTP 상태 코드(상태 코드 400 이상)의 자세한 오류 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span>
    - [<span data-ttu-id="77c5b-211">자세한 오류 로깅에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="77c5b-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="77c5b-212">**실패한 요청 추적**</span><span class="sxs-lookup"><span data-stu-id="77c5b-212">**Failed Request Tracing**</span></span>
    - <span data-ttu-id="77c5b-213">Tooprocess hello 요청 및 hello 소요 시간 각 구성 요소를 사용 하는 추적의 hello IIS 구성 요소를 포함 하 여 실패 한 요청을 대 한 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="77c5b-213">Detailed information on failed requests, including a trace of hello IIS components used tooprocess hello request and hello time taken in each component.</span></span>
    - <span data-ttu-id="77c5b-214">실패 한 요청 로그는 특정 HTTP 오류 원인을 tooisolate 하려고 할 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-214">Failed request logs are useful when trying tooisolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="77c5b-215">실패한 요청 추적에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="77c5b-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="77c5b-216">tooenable 서버 로깅:</span><span class="sxs-lookup"><span data-stu-id="77c5b-216">tooenable Server logging:</span></span>
- <span data-ttu-id="77c5b-217">너무 이동**모니터링** > **진단 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-217">go too**Monitoring** > **Diagnostic Logs**.</span></span>
- <span data-ttu-id="77c5b-218">Hello 다양 한 유형의 hello 설정/해제를 사용 하 여 웹 서버 진단을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-218">Enable hello different types of Web Server Diagnostics using hello toggles.</span></span>

![앱 모니터링](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="77c5b-220">로깅을 사용하도록 설정하면 응용 프로그램 성능과 리소스 사용률에 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="77c5b-221">프로덕션 시나리오에서는 오류 로그를 사용하는 것이 좋으며, 자세한 로깅은 문제를 조사할 때만 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="77c5b-222">로그 액세스</span><span class="sxs-lookup"><span data-stu-id="77c5b-222">Accessing Logs</span></span>
<span data-ttu-id="77c5b-223">Blob Storage에 저장된 로그에는 Azure Storage Explorer를 사용하여 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="77c5b-224">Hello 웹 앱의 파일 시스템에 저장 된 로그 경로 따라 hello에서 FTP를 통해 액세스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-224">Logs stored in hello Web App's filesystem are accessed through FTP under hello following paths:</span></span>

- <span data-ttu-id="77c5b-225">**응용 프로그램 로그** - `%HOME%/LogFiles/Application/`.</span><span class="sxs-lookup"><span data-stu-id="77c5b-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="77c5b-226">이 폴더에는 응용 프로그램 로깅으로 생성된 정보가 포함된 하나 이상의 텍스트 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="77c5b-227">**실패한 요청 추적** - `%HOME%/LogFiles/W3SVC#########/`.</span><span class="sxs-lookup"><span data-stu-id="77c5b-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span>
    - <span data-ttu-id="77c5b-228">이 폴더에는 하나의 XSL 파일 및 하나 이상의 XML 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-228">This folder contains an XSL file and one or more XML files.</span></span>
- <span data-ttu-id="77c5b-229">**자세한 오류 로그** - `%HOME%/LogFiles/DetailedErrors/`.</span><span class="sxs-lookup"><span data-stu-id="77c5b-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span>
    - <span data-ttu-id="77c5b-230">이 폴더에는 응용 프로그램에서 생성되는 HTTP와 관련된 정보가 광범위하게 포함된 .htm 파일이 하나 이상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="77c5b-231">**웹 서버 로그** - `%HOME%/LogFiles/http/RawLogs`.</span><span class="sxs-lookup"><span data-stu-id="77c5b-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span>
    - <span data-ttu-id="77c5b-232">이 폴더에는 hello W3C 확장된 로그 파일 형식을 사용 하 여 서식이 지정 된 텍스트 파일을 하나 이상 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-232">This folder contains one or more text files formatted using hello W3C extended log file format.</span></span>

## <span data-ttu-id="77c5b-233"><a name="streaming"></a>6 단계 - 스트리밍 로그</span><span class="sxs-lookup"><span data-stu-id="77c5b-233"><a name="streaming"></a> Step 6 - Log Streaming</span></span>
<span data-ttu-id="77c5b-234">스트리밍 로그는 너무 비교 시간을 절약 하므로 응용 프로그램을 디버깅할 때 편리한[hello 로그에 액세스 하](#Accessing-Logs) FTP를 통해.</span><span class="sxs-lookup"><span data-stu-id="77c5b-234">Streaming logs are convenient when debugging an application since it saves time compared too[accessing hello logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="77c5b-235">App Service에서는 **응용 프로그램 로그** 및 **웹 서버 로그**가 생성될 때 스트림할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span>

> [!TIP]
> <span data-ttu-id="77c5b-236">Toostream 로그를 시도 하기 전에 hello에 설명 된 대로 로그 수집 설정 되어 있는지 확인 [로깅](#logging) 섹션.</span><span class="sxs-lookup"><span data-stu-id="77c5b-236">Before trying toostream logs, make sure you have enabled collecting logs as described in hello [Logging](#logging) section.</span></span>

<span data-ttu-id="77c5b-237">toostream 로그 이동 너무**모니터링**> **로그 스트림**합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-237">toostream logs, go too**Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="77c5b-238">원하는 정보에 따라 **응용 프로그램 로그** 또는 **웹 서버 로그**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="77c5b-239">여기에서 일시 중지를 다시 시작 및 hello 버퍼를 지울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-239">From here, you can also pause, restart, and clear hello buffer.</span></span>

![스트리밍 로그](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="77c5b-241">로그는 hello 응용 프로그램에 트래픽을 있는 경우에 생성, 더 많은 이벤트 나 정보 로그 tooget의 hello 자세한 정도 늘릴 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-241">Logs are only generated when there is traffic on hello app, you can also increase hello verbosity of logs tooget more events or information.</span></span>

## <span data-ttu-id="77c5b-242"><a name="remote"></a>7 단계 - 원격 디버깅</span><span class="sxs-lookup"><span data-stu-id="77c5b-242"><a name="remote"></a> Step 7 - Remote Debugging</span></span>
<span data-ttu-id="77c5b-243">사용 하 여 hello pin 기준 소스 hello 응용 프로그램 문제를 만든 후 **원격 디버깅** hello 코드를 통해 toowalk 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-243">Once you have pin-pointed hello source of hello applications problems, use **Remote Debugging** toowalk through hello code.</span></span>

<span data-ttu-id="77c5b-244">원격 디버깅을 사용 하면 연결할 디버거 tooyour 웹 응용 프로그램 hello 클라우드에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-244">Remote debugging lets you attach a debugger tooyour Web App running in hello cloud.</span></span> <span data-ttu-id="77c5b-245">중단점을 설정할 메모리를 직접 조작 및 코드를 단계적 로컬로 실행 되는 앱에 대해 수행 하는 것 처럼 hello 코드 경로 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-245">You can set breakpoints, manipulate memory directly, step through code, and even change hello code path just like you do for an app running locally.</span></span>

<span data-ttu-id="77c5b-246">tooattach hello 디버거 tooyour 앱 hello 클라우드에서 실행 중인:</span><span class="sxs-lookup"><span data-stu-id="77c5b-246">tooattach hello debugger tooyour app running in hello cloud:</span></span>

- <span data-ttu-id="77c5b-247">Visual Studio 2017 년 1 hello 앱에 대 한 솔루션 열기 hello 사용 하 여 원하는 toodebug</span><span class="sxs-lookup"><span data-stu-id="77c5b-247">Using Visual Studio 2017, open hello solution for hello app you want toodebug</span></span>
- <span data-ttu-id="77c5b-248">로컬 개발의 경우와 마찬가지로 중단점을 몇 개 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="77c5b-249">**클라우드 탐색기**를 엽니다(ctr + /, ctrl + x).</span><span class="sxs-lookup"><span data-stu-id="77c5b-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="77c5b-250">필요하면 Azure 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="77c5b-251">원하는 toodebug 찾기 hello 앱</span><span class="sxs-lookup"><span data-stu-id="77c5b-251">Find hello app you want toodebug</span></span>
- <span data-ttu-id="77c5b-252">선택 **디버거 연결** 양식 hello **동작** 창.</span><span class="sxs-lookup"><span data-stu-id="77c5b-252">Select **Attach Debugger** form hello **Actions** pane.</span></span>

![원격 디버깅](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="77c5b-254">Visual Studio 원격 디버깅을 위해 응용 프로그램을 구성 하 고 tooyour 응용 프로그램을 이동 하는 브라우저 창이 실행.</span><span class="sxs-lookup"><span data-stu-id="77c5b-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates tooyour app.</span></span> <span data-ttu-id="77c5b-255">응용 프로그램 tootrigger 중단점 hello 코드를 단계별로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-255">Browse through your app tootrigger break points and step through hello code.</span></span>

> [!WARNING]
> <span data-ttu-id="77c5b-256">프로덕션 사이트에서 디버그 모드로 실행하는 것은 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="77c5b-257">프로덕션 앱 toomultiple 서버 인스턴스에서 아웃 되지 배율 조정 하는 경우 응답 tooother 요청에서 웹 서버 hello 하지 못하도록 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-257">If your production app is not scaled out toomultiple server instances, debugging prevent hello web server from responding tooother requests.</span></span> <span data-ttu-id="77c5b-258">프로덕션 문제를 해결 하 여 가장 적합 한 리소스는 너무[로깅을 구성](#logging) 및 [Application Insights](#insights)합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-258">For troubleshooting production problems, your best resource is too[configure logging](#logging) and [Application Insights](#insights).</span></span>



## <span data-ttu-id="77c5b-259"><a name="explorer"></a> 8단계 - 프로세스 탐색기</span><span class="sxs-lookup"><span data-stu-id="77c5b-259"><a name="explorer"></a> Step 8 - Process Explorer</span></span>
<span data-ttu-id="77c5b-260">응용 프로그램을 하나의 인스턴스가 아닌 toomore 확장할 때 **프로세스 탐색기** 인스턴스 문제를 식별 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-260">When your application is scaled out toomore than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="77c5b-261">**Process Explorer**를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="77c5b-262">앱 서비스 계획의 다른 인스턴스에서 모든 hello 프로세스를 열거 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-262">Enumerate all hello processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="77c5b-263">드릴 다운 하 고 hello 핸들 및 각 프로세스와 관련 된 모듈을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-263">Drill down and view hello handles and modules associated with each process.</span></span>
- <span data-ttu-id="77c5b-264">런어웨이 프로세스를 식별 하는 수준 toohelp를 처리 하는 hello 시 CPU 보기, 작업 집합 및 스레드 수</span><span class="sxs-lookup"><span data-stu-id="77c5b-264">View CPU, Working Set, and Thread count at hello process level toohelp you identify runaway processes</span></span>
- <span data-ttu-id="77c5b-265">열려 있는 파일 핸들을 찾고, 필요하면 특정 프로세스 인스턴스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="77c5b-266">프로세스 탐색기는 **모니터링** > **프로세스 탐색기**에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![Process Explorer](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <span data-ttu-id="77c5b-268"><a name="insights"></a> 9단계 - Application Insights</span><span class="sxs-lookup"><span data-stu-id="77c5b-268"><a name="insights"></a> Step 9 - Application Insights</span></span>
<span data-ttu-id="77c5b-269">**Application Insights**에서는 응용 프로그램에 대한 응용 프로그램 프로파일링 및 고급 모니터링 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span>

<span data-ttu-id="77c5b-270">예외 및 웹 앱의 성능 문제를 진단 및 toodetect Application Insights를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-270">Use Application Insights toodetect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="77c5b-271">**모니터링** > **Application Insights**에서 웹앱에 대해 Application Insights를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span>

> [!NOTE]
> <span data-ttu-id="77c5b-272">Application Insights 데이터 수집 tooinstall hello Application Insights 사이트 확장 toostart를 라는 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-272">Application Insights might prompt you tooinstall hello Application Insights site extension toostart collecting data.</span></span> <span data-ttu-id="77c5b-273">응용 프로그램을 다시 시작을 하면 hello 사이트 확장을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c5b-273">Installing hello site extension causes an application restart.</span></span>

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="77c5b-275">Application Insights에 다양 한 기능 집합, toolearn 더 링크를 따라 hello hello에 포함 된 [다음 단계](#next) 섹션.</span><span class="sxs-lookup"><span data-stu-id="77c5b-275">Application Insights has a rich feature set, toolearn more, follow hello links included in hello [Next Steps](#next) section.</span></span>

## <span data-ttu-id="77c5b-276"><a name="next"></a> 다음 단계</span><span class="sxs-lookup"><span data-stu-id="77c5b-276"><a name="next"></a> Next steps</span></span>

 - [<span data-ttu-id="77c5b-277">Application Insights란?</span><span class="sxs-lookup"><span data-stu-id="77c5b-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="77c5b-278">Application Insights를 사용한 Azure 웹앱 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="77c5b-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="77c5b-279">Application Insights를 사용한 웹 사이트의 가용성 및 응답성 모니터링</span><span class="sxs-lookup"><span data-stu-id="77c5b-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)

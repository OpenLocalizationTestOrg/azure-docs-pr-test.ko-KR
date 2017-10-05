---
title: "웹앱 모니터링 | Microsoft Docs"
description: "웹앱의 모니터링을 설정하는 방법 알아보기"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: 29df824062d00e01b786533033097948c008588f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-app-service"></a><span data-ttu-id="1f6fe-103">App Service 모니터링</span><span class="sxs-lookup"><span data-stu-id="1f6fe-103">Monitor App Service</span></span>
<span data-ttu-id="1f6fe-104">이 자습서에서는 앱을 모니터링하고 내장된 플랫폼 도구를 사용하여 문제가 발생했을 때 이를 해결하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-104">This tutorial walks you through monitoring your app and using the built-in platform tools to solve problems when they occur.</span></span>

<span data-ttu-id="1f6fe-105">이 문서의 각 섹션은 특정 기능을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="1f6fe-106">기능을 함께 사용하면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-106">Using the features together let you:</span></span>
- <span data-ttu-id="1f6fe-107">앱 문제 식별</span><span class="sxs-lookup"><span data-stu-id="1f6fe-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="1f6fe-108">코드 또는 플랫폼으로 인해 문제가 발생한 시기 확인</span><span class="sxs-lookup"><span data-stu-id="1f6fe-108">Determining when the issue is caused by your code or the platform.</span></span>
- <span data-ttu-id="1f6fe-109">코드에서 문제가 발생한 원본 범위 좁히기</span><span class="sxs-lookup"><span data-stu-id="1f6fe-109">Narrow down the source of the problem in your code.</span></span>
- <span data-ttu-id="1f6fe-110">문제 디버깅 및 해결</span><span class="sxs-lookup"><span data-stu-id="1f6fe-110">Debugging and fixing the issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1f6fe-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="1f6fe-111">Before you begin</span></span>
- <span data-ttu-id="1f6fe-112">모니터링할 웹앱을 준비하고 설명된 단계를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-112">You need a Web App to monitor and follow the outlined steps.</span></span>
    - <span data-ttu-id="1f6fe-113">[SQL Database를 사용하여 Azure에서 ASP.NET 응용 프로그램 만들기](app-service-web-tutorial-dotnet-sqldatabase.md) 자습서에 설명된 단계를 따라 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-113">You can create an application following the steps described in the [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="1f6fe-114">응용 프로그램의 **원격 디버깅**을 시험해 보려면 Visual Studio가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-114">If you want to try out **Remote Debugging** of your application, you need Visual Studio.</span></span>
    - <span data-ttu-id="1f6fe-115">Visual Studio 2017이 아직 설치되지 않은 경우 무료 [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)을 다운로드하고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-115">If you don’t already have Visual Studio 2017 installed, you can download and use the free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
    - <span data-ttu-id="1f6fe-116">Visual Studio를 설정하는 동안 **Azure 개발**을 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-116">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

## <span data-ttu-id="1f6fe-117"><a name="metrics"></a> 1단계 - 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="1f6fe-117"><a name="metrics"></a> Step 1 - View metrics</span></span>
<span data-ttu-id="1f6fe-118">**메트릭**을 통해 다음을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-118">**Metrics** are useful to understand:</span></span>
- <span data-ttu-id="1f6fe-119">응용 프로그램 상태</span><span class="sxs-lookup"><span data-stu-id="1f6fe-119">Application health</span></span>
- <span data-ttu-id="1f6fe-120">앱 성능</span><span class="sxs-lookup"><span data-stu-id="1f6fe-120">App performance</span></span>
- <span data-ttu-id="1f6fe-121">리소스 사용</span><span class="sxs-lookup"><span data-stu-id="1f6fe-121">Resource consumption</span></span>

<span data-ttu-id="1f6fe-122">응용 프로그램 문제를 조사할 때는 제일 먼저 메트릭을 검토하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-122">When investigating an application issue, reviewing metrics is a good place to start.</span></span> <span data-ttu-id="1f6fe-123">Azure Portal에서는 **Azure Monitor**를 사용하여 응용 프로그램의 메트릭을 빠르게 보고 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-123">Azure portal has a quick way to visually inspect the metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="1f6fe-124">메트릭은 앱의 여러 주요 집계에 대한 기록 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="1f6fe-125">App Service에서 호스트되는 모든 응용 프로그램의 Web App 및 App Service 계획을 모두 모니터링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-125">For any app hosted in app service, you should monitor both the Web App and the App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="1f6fe-126">App Service 계획은 앱을 호스트하는 데 사용되는 실제 리소스의 컬렉션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-126">An App Service plan represents the collection of physical resources used to host your apps.</span></span> <span data-ttu-id="1f6fe-127">App Service 계획에 할당된 모든 응용 프로그램은 정의된 리소스를 공유하므로 여러 앱을 호스팅할 때 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-127">All applications assigned to an App Service plan share the resources defined by it allowing you to save cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="1f6fe-128">App Service 계획은 다음을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-128">App Service plans define:</span></span>
> * <span data-ttu-id="1f6fe-129">지역: 북유럽, 미국 동부, 동남 아시아 등</span><span class="sxs-lookup"><span data-stu-id="1f6fe-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="1f6fe-130">인스턴스 크기: 소, 중, 대 등</span><span class="sxs-lookup"><span data-stu-id="1f6fe-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="1f6fe-131">확장 개수: 1, 2, 3개 인스턴스 등</span><span class="sxs-lookup"><span data-stu-id="1f6fe-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="1f6fe-132">SKU: 무료, 공유, 기본, 표준, 프리미엄 등</span><span class="sxs-lookup"><span data-stu-id="1f6fe-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="1f6fe-133">Web App에 대한 메트릭을 검토하려면 모니터링할 앱의 **개요** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-133">To review metrics for your Web App, go to the **Overview** blade of the app you want to monitor.</span></span> <span data-ttu-id="1f6fe-134">여기에서 앱의 메트릭에 대한 차트를 **모니터링 타일**로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="1f6fe-135">보고 싶은 메트릭과 표시할 시간 범위를 편집 및 구성하려면 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-135">Click the tile to edit and configure what metrics to view and the time range to display.</span></span>

<span data-ttu-id="1f6fe-136">기본적으로 리소스 블레이드는 지난 1시간 동안의 응용 프로그램 요청 및 오류에 대한 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-136">By default the resource blade provides a view for the Application Requests and errors for the last hour.</span></span>
<span data-ttu-id="1f6fe-137">![앱 모니터링](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="1f6fe-137">![Monitor App](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="1f6fe-138">이 예에서 알 수 있듯이 많은 **HTTP 서버 오류**를 생성하는 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-138">As you can see in the example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="1f6fe-139">많은 오류는 이 응용 프로그램을 조사해야 하는 첫 번째 이유가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-139">The high volume of errors is the first indication we need to investigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="1f6fe-140">다음 링크를 통해 Azure Monitor에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-140">Learn more about Azure Monitor with the following links:</span></span>
> - [<span data-ttu-id="1f6fe-141">Azure Monitor 시작</span><span class="sxs-lookup"><span data-stu-id="1f6fe-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="1f6fe-142">Azure 메트릭</span><span class="sxs-lookup"><span data-stu-id="1f6fe-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="1f6fe-143">Azure Monitor에서 지원되는 메트릭</span><span class="sxs-lookup"><span data-stu-id="1f6fe-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [<span data-ttu-id="1f6fe-144">Azure 대시보드</span><span class="sxs-lookup"><span data-stu-id="1f6fe-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <span data-ttu-id="1f6fe-145"><a name="alerts"></a> 2단계 - 경고 구성</span><span class="sxs-lookup"><span data-stu-id="1f6fe-145"><a name="alerts"></a> Step 2 - Configure Alerts</span></span>
<span data-ttu-id="1f6fe-146">앱의 특정 조건에서 **경고**가 트리거되도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-146">**Alerts** can be configured to trigger on specific conditions for your app.</span></span>

<span data-ttu-id="1f6fe-147">[1단계 - 메트릭 보기](#metrics)에서 응용 프로그램에 많은 오류가 있음을 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-147">In [Step 1 - View metrics](#metrics), we saw that the application had a high number of errors.</span></span>

<span data-ttu-id="1f6fe-148">오류가 발생하면 자동으로 알리도록 경고를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-148">Lets configure an alert to automatically get notified when errors occur.</span></span> <span data-ttu-id="1f6fe-149">이 경우 HTTP 50X 오류 수가 특정 임계값을 초과할 때마다 경고를 보내고 메일로 보내려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-149">In this case, we want the alert to send and e-mail every time the number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="1f6fe-150">경고를 만들려면 **모니터링** > **경고**로 이동하여 **[+] 경고 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-150">To create an alert, navigate to **Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![경고](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="1f6fe-152">경고 구성에 대한 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-152">Provide values for the Alert configuration:</span></span>
- <span data-ttu-id="1f6fe-153">**리소스:** 경고를 모니터링하는 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-153">**Resource:** The site to monitor with the alert.</span></span>
- <span data-ttu-id="1f6fe-154">**이름:** 경고의 이름입니다(이 경우 *High HTTP 50X*).</span><span class="sxs-lookup"><span data-stu-id="1f6fe-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="1f6fe-155">**설명:** 이 경고에 대한 일반 텍스트 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="1f6fe-156">**경고 대상:** 경고 대상은 메트릭 또는 이벤트(이 예제에서는 메트릭)가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="1f6fe-157">**메트릭:** 모니터링할 메트릭(이 경우 *HTTP 서버 오류*)입니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-157">**Metric:** What metric to monitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="1f6fe-158">**조건:** 경고할 시기입니다. 이 예제에서는 *보다 큼* 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-158">**Condition:** When to alert, in this case select the *greater than* option.</span></span>
- <span data-ttu-id="1f6fe-159">**임계값:** 검색할 값(이 경우 *400*)입니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-159">**Threshold:** What is value to look for, in this case: *400*.</span></span>
- <span data-ttu-id="1f6fe-160">**기간:** 경고는 메트릭의 평균값에 대해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-160">**Period:** Alerts operate over the average value of a metric.</span></span> <span data-ttu-id="1f6fe-161">시간이 짧을수록 민감한 경고가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="1f6fe-162">이 경우 *5분*입니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-162">in this case we are looking at *5 Minutes*.</span></span>
- <span data-ttu-id="1f6fe-163">**메일 소유자 및 참가자:** 이 예에서는 *사용*입니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="1f6fe-164">이제 경고가 생성되면 앱이 구성된 임계값을 초과할 때마다 메일이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-164">Now that the alert is created an email is sent every time the app goes over the configured threshold.</span></span> <span data-ttu-id="1f6fe-165">Azure Portal에서 활성 경고를 검토할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-165">Active alerts can also be reviewed in the Azure portal.</span></span>

![트리거된 경고](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="1f6fe-167">다음 링크를 통해 Azure 경고에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-167">Learn more about Azure Alerts with the following links:</span></span>
> - [<span data-ttu-id="1f6fe-168">Microsoft Azure의 경고란?</span><span class="sxs-lookup"><span data-stu-id="1f6fe-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="1f6fe-169">메트릭에 대한 작업</span><span class="sxs-lookup"><span data-stu-id="1f6fe-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="1f6fe-170">메트릭 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="1f6fe-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <span data-ttu-id="1f6fe-171"><a name="companion"></a> 3단계 - App Service 도우미</span><span class="sxs-lookup"><span data-stu-id="1f6fe-171"><a name="companion"></a> Step 3 - App Service Companion</span></span>
<span data-ttu-id="1f6fe-172">**App Service 도우미**를 사용하면 모바일 장치(iOS 또는 Android)의 기본 환경으로 간편하게 앱을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-172">**App Service companion** offers a convenient way to monitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="1f6fe-173">App Service 도우미를 사용하여 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="1f6fe-174">응용 프로그램 메트릭 검토</span><span class="sxs-lookup"><span data-stu-id="1f6fe-174">Review application metrics</span></span>
- <span data-ttu-id="1f6fe-175">경고 및 권장 사항 검토 및 조치</span><span class="sxs-lookup"><span data-stu-id="1f6fe-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="1f6fe-176">기본적인 문제 해결 수행(찾아보기, 시작, 중지, 응용 프로그램 다시 시작)</span><span class="sxs-lookup"><span data-stu-id="1f6fe-176">Perform basic troubleshooting (browse, start, stop, restart the app)</span></span>
- <span data-ttu-id="1f6fe-177">중요한 이벤트에 대한 푸시 알림을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-177">Get push notifications for critical events.</span></span>

![App Service 도우미](media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="1f6fe-179">[![App Service 도우미 App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service 도우미 Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="1f6fe-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="1f6fe-180">App Service 도우미는 [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)나 [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-180">You can install App Service companion from the [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <span data-ttu-id="1f6fe-181"><a name="diagnose"></a> 4단계 - 문제 진단 및 해결</span><span class="sxs-lookup"><span data-stu-id="1f6fe-181"><a name="diagnose"></a> Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="1f6fe-182">**문제 진단 및 해결**은 플랫폼 문제와 응용 프로그램 문제를 구분할 수 있도록 도와 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="1f6fe-183">또한 Web App을 정상적으로 되돌릴 수 있는 완화 방법을 제안할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-183">It can also suggest possible mitigations to get your Web App back to healthy.</span></span>

![문제 진단 및 해결](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="1f6fe-185">이전 단계의 예제를 계속 진행하면 응용 프로그램에 가용성 문제가 있음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-185">Continuing with the example form previous steps, we can see that the application has been having availably issues.</span></span> <span data-ttu-id="1f6fe-186">반면, 플랫폼 가용성은 100%에서 이동되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-186">In contrast, the platform availability has not moved from 100%.</span></span>

<span data-ttu-id="1f6fe-187">앱에 문제가 있고 플랫폼이 작동 중인 경우 응용 프로그램 문제를 다루고 있음을 분명히 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-187">When the app is having issue and the platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <span data-ttu-id="1f6fe-188"><a name="logging"></a>5 단계 - 로깅</span><span class="sxs-lookup"><span data-stu-id="1f6fe-188"><a name="logging"></a> Step 5 - Logging</span></span>
<span data-ttu-id="1f6fe-189">이제 실패의 범위를 응용 프로그램 문제로 좁혔으므로 응용 프로그램 및 서버 로그를 확인하여 자세한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-189">Now that we have narrowed down the failures to an application issue, we can look at the application and server logs to get more information.</span></span>

<span data-ttu-id="1f6fe-190">로깅을 사용하면 웹앱의 **응용 프로그램 진단** 및 **웹 서버 진단** 로그를 모두 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-190">Logging allows you to collect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="1f6fe-191">응용 프로그램 진단</span><span class="sxs-lookup"><span data-stu-id="1f6fe-191">Application Diagnostics</span></span>
<span data-ttu-id="1f6fe-192">응용 프로그램 진단을 사용하면 런타임에 응용 프로그램에서 생성된 추적 정보를 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-192">Application diagnostics allows you to capture traces produced by the application at runtime.</span></span>

<span data-ttu-id="1f6fe-193">응용 프로그램에 추적 기능을 추가하면 문제 디버깅 및 식별 기능이 크게 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-193">Adding tracing to your application greatly improves your ability to debug and pin-point issues.</span></span>

<span data-ttu-id="1f6fe-194">ASP.NET에서는 [System.Diagnostics.Trace 클래스](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx)를 사용하여 로그 인프라에서 캡처되는 이벤트를 생성하면 응용 프로그램 추적 정보를 로깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) to generate events that are captured by the log infrastructure.</span></span> <span data-ttu-id="1f6fe-195">추적 정보의 심각도를 지정하여 필터링을 더 쉽게 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-195">You can also specify the severity of the trace for easier filtering.</span></span>

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
<span data-ttu-id="1f6fe-196">응용 프로그램 로깅을 사용하려면 **모니터링** > **진단 로그**로 이동한 다음 설정/해제를 사용하여 응용 프로그램 로깅을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-196">To enable Application logging Go to **Monitoring** > **Diagnostic Logs** and Enable Application Logging using the toggles.</span></span>

![앱 모니터링](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="1f6fe-198">응용 프로그램 로그는 웹앱의 파일 시스템에 저장하거나 Blob Storage에 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-198">Application logs can be stored to your Web App's file system or pushed out to blob storage.</span></span> <span data-ttu-id="1f6fe-199">프로덕션 시나리오에서는 Blob Storage를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-199">For production scenarios, it's recommended to use blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f6fe-200">로깅을 사용하도록 설정하면 응용 프로그램 성능과 리소스 사용률에 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="1f6fe-201">프로덕션 시나리오에서는 오류 로그를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="1f6fe-202">자세한 로깅은 문제를 조사할 때만 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="1f6fe-203">웹 서버 진단</span><span class="sxs-lookup"><span data-stu-id="1f6fe-203">Web Server Diagnostics</span></span>
<span data-ttu-id="1f6fe-204">앱이 계측되지 않는 경우에도 웹 서버 로그는 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="1f6fe-205">App Service에서는 세 가지 종류의 서버 로그를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="1f6fe-206">**웹 서버 로깅**</span><span class="sxs-lookup"><span data-stu-id="1f6fe-206">**Web Server Logging**</span></span>
    - <span data-ttu-id="1f6fe-207">[W3C 확장 로그 파일 형식](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)을 사용하는 HTTP 트랜잭션에 대한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-207">Information about HTTP transactions using the [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
    - <span data-ttu-id="1f6fe-208">처리된 요청 수, 특정 IP 주소에서 들어온 요청 수 등의 전체 사이트 메트릭을 확인하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-208">Useful when determining overall site metrics such as the number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="1f6fe-209">**자세한 오류 로깅**</span><span class="sxs-lookup"><span data-stu-id="1f6fe-209">**Detailed Error Logging**</span></span>
    - <span data-ttu-id="1f6fe-210">오류를 나타내는 HTTP 상태 코드(상태 코드 400 이상)의 자세한 오류 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span>
    - [<span data-ttu-id="1f6fe-211">자세한 오류 로깅에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="1f6fe-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="1f6fe-212">**실패한 요청 추적**</span><span class="sxs-lookup"><span data-stu-id="1f6fe-212">**Failed Request Tracing**</span></span>
    - <span data-ttu-id="1f6fe-213">요청을 처리하는 데 사용된 IIS 구성 요소 추적 및 각 구성 요소에 소요된 시간을 포함하여 실패한 요청에 대해 자세한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-213">Detailed information on failed requests, including a trace of the IIS components used to process the request and the time taken in each component.</span></span>
    - <span data-ttu-id="1f6fe-214">실패한 요청 로그는 특정 HTTP 오류를 일으키는 조건을 격리하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-214">Failed request logs are useful when trying to isolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="1f6fe-215">실패한 요청 추적에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="1f6fe-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="1f6fe-216">서버 로깅을 사용하도록 설정하려면:</span><span class="sxs-lookup"><span data-stu-id="1f6fe-216">To enable Server logging:</span></span>
- <span data-ttu-id="1f6fe-217">**모니터링** > **진단 로그**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-217">go to **Monitoring** > **Diagnostic Logs**.</span></span>
- <span data-ttu-id="1f6fe-218">설정/해제를 사용하여 다양한 종류의 웹 서버 진단을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-218">Enable the different types of Web Server Diagnostics using the toggles.</span></span>

![앱 모니터링](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="1f6fe-220">로깅을 사용하도록 설정하면 응용 프로그램 성능과 리소스 사용률에 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="1f6fe-221">프로덕션 시나리오에서는 오류 로그를 사용하는 것이 좋으며, 자세한 로깅은 문제를 조사할 때만 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="1f6fe-222">로그 액세스</span><span class="sxs-lookup"><span data-stu-id="1f6fe-222">Accessing Logs</span></span>
<span data-ttu-id="1f6fe-223">Blob Storage에 저장된 로그에는 Azure Storage Explorer를 사용하여 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="1f6fe-224">웹앱의 파일 시스템에 저장된 로그에는 다음 경로로 FTP를 통해 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-224">Logs stored in the Web App's filesystem are accessed through FTP under the following paths:</span></span>

- <span data-ttu-id="1f6fe-225">**응용 프로그램 로그** - `%HOME%/LogFiles/Application/`.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="1f6fe-226">이 폴더에는 응용 프로그램 로깅으로 생성된 정보가 포함된 하나 이상의 텍스트 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="1f6fe-227">**실패한 요청 추적** - `%HOME%/LogFiles/W3SVC#########/`.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span>
    - <span data-ttu-id="1f6fe-228">이 폴더에는 하나의 XSL 파일 및 하나 이상의 XML 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-228">This folder contains an XSL file and one or more XML files.</span></span>
- <span data-ttu-id="1f6fe-229">**자세한 오류 로그** - `%HOME%/LogFiles/DetailedErrors/`.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span>
    - <span data-ttu-id="1f6fe-230">이 폴더에는 응용 프로그램에서 생성되는 HTTP와 관련된 정보가 광범위하게 포함된 .htm 파일이 하나 이상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="1f6fe-231">**웹 서버 로그** - `%HOME%/LogFiles/http/RawLogs`.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span>
    - <span data-ttu-id="1f6fe-232">이 폴더에는 W3C 확장 로그 파일 형식을 사용하여 서식이 지정된 하나 이상의 텍스트 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-232">This folder contains one or more text files formatted using the W3C extended log file format.</span></span>

## <span data-ttu-id="1f6fe-233"><a name="streaming"></a>6 단계 - 스트리밍 로그</span><span class="sxs-lookup"><span data-stu-id="1f6fe-233"><a name="streaming"></a> Step 6 - Log Streaming</span></span>
<span data-ttu-id="1f6fe-234">스트리밍 로그는 FTP를 통해 [로그에 액세스할](#Accessing-Logs) 때보다 시간이 절약되므로 응용 프로그램을 디버깅할 때 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-234">Streaming logs are convenient when debugging an application since it saves time compared to [accessing the logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="1f6fe-235">App Service에서는 **응용 프로그램 로그** 및 **웹 서버 로그**가 생성될 때 스트림할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span>

> [!TIP]
> <span data-ttu-id="1f6fe-236">로그를 스트림하기 전에, [로깅](#logging) 섹션에 설명된 대로 로그 수집을 사용하도록 설정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-236">Before trying to stream logs, make sure you have enabled collecting logs as described in the [Logging](#logging) section.</span></span>

<span data-ttu-id="1f6fe-237">로그를 스트리밍하려면 **모니터링**> **로그 스트림**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-237">To stream logs, go to **Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="1f6fe-238">원하는 정보에 따라 **응용 프로그램 로그** 또는 **웹 서버 로그**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="1f6fe-239">여기에서 버퍼를 일시 중지, 다시 시작하거나 지울 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-239">From here, you can also pause, restart, and clear the buffer.</span></span>

![스트리밍 로그](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="1f6fe-241">로그는 응용 프로그램에 트래픽이 있을 때만 생성되며, 로그를 더 상세하게 설정하면 더 많은 이벤트와 정보를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-241">Logs are only generated when there is traffic on the app, you can also increase the verbosity of logs to get more events or information.</span></span>

## <span data-ttu-id="1f6fe-242"><a name="remote"></a>7 단계 - 원격 디버깅</span><span class="sxs-lookup"><span data-stu-id="1f6fe-242"><a name="remote"></a> Step 7 - Remote Debugging</span></span>
<span data-ttu-id="1f6fe-243">응용 프로그램 문제의 원인을 찾은 후에는 **원격 디버깅**을 사용하여 코드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-243">Once you have pin-pointed the source of the applications problems, use **Remote Debugging** to walk through the code.</span></span>

<span data-ttu-id="1f6fe-244">원격 디버깅을 사용하면 클라우드에서 실행 중인 Web App에 디버거를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-244">Remote debugging lets you attach a debugger to your Web App running in the cloud.</span></span> <span data-ttu-id="1f6fe-245">중단점을 설정하고 메모리를 직접 조작하며 코드를 단계별로 실행하고 심지어는 응용 프로그램을 로컬로 실행할 때처럼 코드 경로를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-245">You can set breakpoints, manipulate memory directly, step through code, and even change the code path just like you do for an app running locally.</span></span>

<span data-ttu-id="1f6fe-246">디버거를 클라우드에서 실행 중인 응용 프로그램에 연결하려면:</span><span class="sxs-lookup"><span data-stu-id="1f6fe-246">To attach the debugger to your app running in the cloud:</span></span>

- <span data-ttu-id="1f6fe-247">Visual Studio 2017을 사용하여 디버그할 응용 프로그램의 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-247">Using Visual Studio 2017, open the solution for the app you want to debug</span></span>
- <span data-ttu-id="1f6fe-248">로컬 개발의 경우와 마찬가지로 중단점을 몇 개 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="1f6fe-249">**클라우드 탐색기**를 엽니다(ctr + /, ctrl + x).</span><span class="sxs-lookup"><span data-stu-id="1f6fe-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="1f6fe-250">필요하면 Azure 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="1f6fe-251">디버그할 응용 프로그램을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-251">Find the app you want to debug</span></span>
- <span data-ttu-id="1f6fe-252">**작업** 창에서 **디버거 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-252">Select **Attach Debugger** form the **Actions** pane.</span></span>

![원격 디버깅](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="1f6fe-254">Visual Studio에서는 응용 프로그램을 원격 디버깅에 적합하게 구성하고 응용 프로그램으로 이동하는 브라우저 창을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates to your app.</span></span> <span data-ttu-id="1f6fe-255">응용 프로그램을 탐색하며 중단점을 트리거하고 코드를 단계별로 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-255">Browse through your app to trigger break points and step through the code.</span></span>

> [!WARNING]
> <span data-ttu-id="1f6fe-256">프로덕션 사이트에서 디버그 모드로 실행하는 것은 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="1f6fe-257">프로덕션 응용 프로그램이 여러 서버 인스턴스로 확장되지 않은 경우 디버깅으로 인해 웹 서버에서 다른 요청에 응답할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-257">If your production app is not scaled out to multiple server instances, debugging prevent the web server from responding to other requests.</span></span> <span data-ttu-id="1f6fe-258">프로덕션 문제를 해결할 때 가장 좋은 리소스는 [로깅 구성](#logging) 및 [Application Insights](#insights)를 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-258">For troubleshooting production problems, your best resource is to [configure logging](#logging) and [Application Insights](#insights).</span></span>



## <span data-ttu-id="1f6fe-259"><a name="explorer"></a> 8단계 - 프로세스 탐색기</span><span class="sxs-lookup"><span data-stu-id="1f6fe-259"><a name="explorer"></a> Step 8 - Process Explorer</span></span>
<span data-ttu-id="1f6fe-260">응용 프로그램이 둘 이상의 인스턴스로 확장되면 **프로세스 탐색기**를 사용하여 인스턴스의 문제를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-260">When your application is scaled out to more than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="1f6fe-261">**Process Explorer**를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="1f6fe-262">App Service 계획의 모든 인스턴스에서 모든 프로세스를 열거합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-262">Enumerate all the processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="1f6fe-263">드릴다운하고 각 프로세스와 연결된 핸들 및 모듈을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-263">Drill down and view the handles and modules associated with each process.</span></span>
- <span data-ttu-id="1f6fe-264">런어웨이 프로세스를 쉽게 식별할 수 있도록 프로세스 수준에서 CPU, 작업 집합 및 스레드 수를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-264">View CPU, Working Set, and Thread count at the process level to help you identify runaway processes</span></span>
- <span data-ttu-id="1f6fe-265">열려 있는 파일 핸들을 찾고, 필요하면 특정 프로세스 인스턴스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="1f6fe-266">프로세스 탐색기는 **모니터링** > **프로세스 탐색기**에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![Process Explorer](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <span data-ttu-id="1f6fe-268"><a name="insights"></a> 9단계 - Application Insights</span><span class="sxs-lookup"><span data-stu-id="1f6fe-268"><a name="insights"></a> Step 9 - Application Insights</span></span>
<span data-ttu-id="1f6fe-269">**Application Insights**에서는 응용 프로그램에 대한 응용 프로그램 프로파일링 및 고급 모니터링 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span>

<span data-ttu-id="1f6fe-270">웹앱에서 예외 및 성능 문제를 감지하고 진단하려면 Application Insights를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-270">Use Application Insights to detect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="1f6fe-271">**모니터링** > **Application Insights**에서 웹앱에 대해 Application Insights를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span>

> [!NOTE]
> <span data-ttu-id="1f6fe-272">Application Insights에서 데이터 수집을 시작하려면 Application Insights 사이트 확장을 설치하라는 메시지를 표시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-272">Application Insights might prompt you to install the Application Insights site extension to start collecting data.</span></span> <span data-ttu-id="1f6fe-273">사이트 확장을 설치하면 응용 프로그램이 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-273">Installing the site extension causes an application restart.</span></span>

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="1f6fe-275">Application Insights에는 풍부한 기능 집합이 있으며, [다음 단계](#next) 섹션의 링크를 이용하면 자세한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f6fe-275">Application Insights has a rich feature set, to learn more, follow the links included in the [Next Steps](#next) section.</span></span>

## <span data-ttu-id="1f6fe-276"><a name="next"></a> 다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f6fe-276"><a name="next"></a> Next steps</span></span>

 - [<span data-ttu-id="1f6fe-277">Application Insights란?</span><span class="sxs-lookup"><span data-stu-id="1f6fe-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="1f6fe-278">Application Insights를 사용한 Azure 웹앱 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="1f6fe-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="1f6fe-279">Application Insights를 사용한 웹 사이트의 가용성 및 응답성 모니터링</span><span class="sxs-lookup"><span data-stu-id="1f6fe-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)

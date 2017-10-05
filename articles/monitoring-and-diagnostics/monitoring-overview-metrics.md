---
title: "Microsoft Azure의 메트릭 개요 | Microsoft Docs"
description: "Microsoft Azure의 메트릭 개요 및 사용"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 405ec51c-0946-4ec9-b535-60f65c4a5bd1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: johnkem
ms.openlocfilehash: 3aff83ab2c157a18f4af6200a79bae7e5d6f0ea2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a><span data-ttu-id="095bc-103">Microsoft Azure의 메트릭 개요</span><span class="sxs-lookup"><span data-stu-id="095bc-103">Overview of metrics in Microsoft Azure</span></span>
<span data-ttu-id="095bc-104">이 문서에서는 Microsoft Azure의 메트릭에 대해 설명하고 그 이점과 사용 방법을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-104">This article describes what metrics are in Microsoft Azure, their benefits, and how to start using them.</span></span>  

## <a name="what-are-metrics"></a><span data-ttu-id="095bc-105">메트릭이 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="095bc-105">What are metrics?</span></span>
<span data-ttu-id="095bc-106">Azure 모니터에서는 원격 분석을 사용하여 Azure에서 워크로드의 상태와 성능에 대한 정보를 구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-106">Azure Monitor enables you to consume telemetry to gain visibility into the performance and health of your workloads on Azure.</span></span> <span data-ttu-id="095bc-107">Azure 원격 분석 데이터의 가장 중요한 유형은 대부분의 Azure 리소스에서 내보내는 메트릭(성능 카운터라고도 함)입니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-107">The most important type of Azure telemetry data is the metrics (also called performance counters) emitted by most Azure resources.</span></span> <span data-ttu-id="095bc-108">Azure Monitor는 모니터링 및 문제 해결을 위해 이러한 메트릭을 구성 및 사용하는 몇 가지 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-108">Azure Monitor provides several ways to configure and consume these metrics for monitoring and troubleshooting.</span></span>

## <a name="what-can-you-do-with-metrics"></a><span data-ttu-id="095bc-109">메트릭으로 무엇을 할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="095bc-109">What can you do with metrics?</span></span>
<span data-ttu-id="095bc-110">메트릭은 원격 분석의 중요한 출처로, 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-110">Metrics are a valuable source of telemetry and enable you to do the following tasks:</span></span>

* <span data-ttu-id="095bc-111">포털 차트에 메트릭을 넣고 해당 차트를 대시보드에 고정하여 리소스(예: VM, 웹 사이트, 논리 앱)의 **성능을 추적**합니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-111">**Track the performance** of your resource (such as a VM, website, or logic app) by plotting its metrics on a portal chart and pinning that chart to a dashboard.</span></span>
* <span data-ttu-id="095bc-112">메트릭이 특정 임계값을 초과할 때 리소스 성능에 영향을 미치는 **문제에 대한 알림을 받습니다**.</span><span class="sxs-lookup"><span data-stu-id="095bc-112">**Get notified of an issue** that impacts the performance of your resource when a metric crosses a certain threshold.</span></span>
* <span data-ttu-id="095bc-113">메트릭이 특정 임계값을 초과할 때 리소스 자동 크기 조정 또는 runbook 실행 등과 같은 **자동화된 작업을 구성합니다**.</span><span class="sxs-lookup"><span data-stu-id="095bc-113">**Configure automated actions**, such as autoscaling a resource or firing a runbook when a metric crosses a certain threshold.</span></span>
* <span data-ttu-id="095bc-114">리소스의 성능 또는 사용 추세에 대한 **고급 분석**이나 보고를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-114">**Perform advanced analytics** or reporting on performance or usage trends of your resource.</span></span>
* <span data-ttu-id="095bc-115">**규정 준수 또는 감사** 목적으로 리소스의 성능 또는 상태 기록을 **보관**합니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-115">**Archive** the performance or health history of your resource **for compliance or auditing** purposes.</span></span>

## <a name="what-are-the-characteristics-of-metrics"></a><span data-ttu-id="095bc-116">메트릭의 특징은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="095bc-116">What are the characteristics of metrics?</span></span>
<span data-ttu-id="095bc-117">메트릭에는 다음과 같은 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-117">Metrics have the following characteristics:</span></span>

* <span data-ttu-id="095bc-118">모든 메트릭은 **1분 빈도**입니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-118">All metrics have **one-minute frequency**.</span></span> <span data-ttu-id="095bc-119">리소스로부터 1분마다 메트릭 값을 받으므로 거의 실시간으로 리소스의 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-119">You receive a metric value every minute from your resource, giving you near real-time visibility into the state and health of your resource.</span></span>
* <span data-ttu-id="095bc-120">메트릭은 **즉시 사용할 수 있습니다**.</span><span class="sxs-lookup"><span data-stu-id="095bc-120">Metrics are **available immediately**.</span></span> <span data-ttu-id="095bc-121">옵트인하거나 추가 진단을 설정하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-121">You don't need to opt in or set up additional diagnostics.</span></span>
* <span data-ttu-id="095bc-122">각 메트릭에 대해 **30일 동안의 기록** 에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-122">You can access **30 days of history** for each metric.</span></span> <span data-ttu-id="095bc-123">리소스의 성능이나 상태에서 최근 및 월별 추세를 신속하게 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-123">You can quickly look at the recent and monthly trends in the performance or health of your resource.</span></span>

<span data-ttu-id="095bc-124">또한 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-124">You can also:</span></span>

* <span data-ttu-id="095bc-125">메트릭이 사용자가 설정한 임계값을 초과하면 **알림을 보내거나 자동 조치를 취하는 메트릭 경고 규칙**을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-125">Configure a metric **alert rule that sends a notification or takes automated action** when the metric crosses the threshold that you have set.</span></span> <span data-ttu-id="095bc-126">자동 크기 조정은 웹 사이트나 계산 리소스에서 들어오는 요청이나 부하에 부합하게 리소스 크기를 조정할 수 있는 특수 자동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-126">Autoscale is a special automated action that enables you to scale out your resource to meet incoming requests or loads on your website or computing resources.</span></span> <span data-ttu-id="095bc-127">임계값을 초과하는 메트릭을 기준으로 자동 크기 조정 설정 규칙을 확대 또는 축소하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-127">You can configure an Autoscale setting rule to scale in or out based on a metric crossing a threshold.</span></span>

* <span data-ttu-id="095bc-128">모든 메트릭 Application Insights 또는 Log Analytics(OMS)를 **라우팅**하여 리소스로부터 받은 메트릭 데이터에 대한 인스턴스 분석, 검색 및 사용자 지정 경고를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-128">**Route** all metrics Application Insights or Log Analytics (OMS) to enable instant analytics, search, and custom alerting on metrics data from your resources.</span></span> <span data-ttu-id="095bc-129">메트릭을 Event Hub로 스트리밍하고 거의 실시간에 가까운 분석을 위해 Azure Stream Analytics나 사용자 지정 앱으로 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-129">You can also stream metrics to an Event Hub, enabling you to then route them to Azure Stream Analytics or to custom apps for near-real time analysis.</span></span> <span data-ttu-id="095bc-130">진단 설정을 사용하여 Event Hub 스트리밍을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-130">You set up Event Hub streaming using diagnostic settings.</span></span>

* <span data-ttu-id="095bc-131">장기 보존을 위해 **메트릭을 저장소에 보관**하거나 오프라인 보고에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-131">**Archive metrics to storage** for longer retention or use them for offline reporting.</span></span> <span data-ttu-id="095bc-132">리소스에 대한 진단 설정을 구성할 때 메트릭을 Azure Blob Storage로 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-132">You can route your metrics to Azure Blob storage when you configure diagnostic settings for your resource.</span></span>

* <span data-ttu-id="095bc-133">Azure 포털을 통해 리소스를 선택하고 메트릭을 차트에 그려서 **모든 메트릭** 간편하게 찾고, 액세스하고, 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-133">Easily discover, access, and **view all metrics** via the Azure portal when you select a resource and plot the metrics on a chart.</span></span>

* <span data-ttu-id="095bc-134">새로운 Azure Monitor REST API를 통해 메트릭을 **사용합니다**.</span><span class="sxs-lookup"><span data-stu-id="095bc-134">**Consume** the metrics via the new Azure Monitor REST APIs.</span></span>

* <span data-ttu-id="095bc-135">PowerShell Cmdlet 또는 크로스 플랫폼 REST API를 사용하여 메트릭을 **쿼리**합니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-135">**Query** metrics by using the PowerShell cmdlets or the Cross-Platform REST API.</span></span>

  ![Azure Monitor의 메트릭 라우팅](./media/monitoring-overview-metrics/Metrics_Overview_v4.png)

## <a name="access-metrics-via-the-portal"></a><span data-ttu-id="095bc-137">포털을 통해 메트릭 액세스</span><span class="sxs-lookup"><span data-stu-id="095bc-137">Access metrics via the portal</span></span>
<span data-ttu-id="095bc-138">다음은 Azure Portal을 통해 메트릭 차트를 만드는 방법에 대한 간단한 연습입니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-138">Following is a quick walkthrough of how to create a metric chart by using the Azure portal.</span></span>

### <a name="to-view-metrics-after-creating-a-resource"></a><span data-ttu-id="095bc-139">리소스를 만든 후 메트릭을 보려면</span><span class="sxs-lookup"><span data-stu-id="095bc-139">To view metrics after creating a resource</span></span>
1. <span data-ttu-id="095bc-140">Azure Portal을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-140">Open the Azure portal.</span></span>
2. <span data-ttu-id="095bc-141">Azure App Service 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-141">Create an Azure App Service website.</span></span>
3. <span data-ttu-id="095bc-142">웹 사이트를 만든 후 웹 사이트의 **개요** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-142">After you create a website, go to the **Overview** blade of the website.</span></span>
4. <span data-ttu-id="095bc-143">**모니터링** 타일로 새 메트릭을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-143">You can view new metrics as a **Monitoring** tile.</span></span> <span data-ttu-id="095bc-144">타일을 편집하고 다른 메트릭을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-144">You can then edit the tile and select more metrics.</span></span>

   ![Azure Monitor의 리소스에 대한 메트릭](./media/monitoring-overview-metrics/MetricsOverview1.png)

### <a name="to-access-all-metrics-in-a-single-place"></a><span data-ttu-id="095bc-146">모든 메트릭을 한 곳에서 액세스하려면</span><span class="sxs-lookup"><span data-stu-id="095bc-146">To access all metrics in a single place</span></span>
1. <span data-ttu-id="095bc-147">Azure Portal을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-147">Open the Azure portal.</span></span>
2. <span data-ttu-id="095bc-148">새 **모니터** 탭으로 이동하고 그 아래에서 **메트릭**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-148">Navigate to the new **Monitor** tab, and then and select the **Metrics** option underneath it.</span></span>
3. <span data-ttu-id="095bc-149">구독, 리소스 그룹 및 리소스의 이름을 드롭다운 목록에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-149">Select your subscription, resource group, and the name of the resource from the drop-down list.</span></span>
4. <span data-ttu-id="095bc-150">사용 가능한 메트릭 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-150">View the available metrics list.</span></span> <span data-ttu-id="095bc-151">그런 다음 관심 있는 메트릭을 선택하고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-151">Then select the metric you are interested in and plot it.</span></span>
5. <span data-ttu-id="095bc-152">오른쪽 위 모서리에 있는 핀을 클릭하여 대시보드에 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-152">You can pin it to the dashboard by clicking the pin on the upper-right corner.</span></span>

   ![Azure Monitor에서 모든 메트릭을 한 곳에서 액세스](./media/monitoring-overview-metrics/MetricsOverview2.png)

> [!NOTE]
> <span data-ttu-id="095bc-154">추가적인 진단 설정 없이 VM(Azure Resource Manager 기반) 및 가상 컴퓨터 확장 집합에서 호스트 설정 메트릭에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-154">You can access host-level metrics from VMs (Azure Resource Manager-based) and virtual machine scale sets without any additional diagnostic setup.</span></span> <span data-ttu-id="095bc-155">이러한 호스트 수준 메트릭은 Windows 및 Linux 인스턴스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-155">These new host-level metrics are available for Windows and Linux instances.</span></span> <span data-ttu-id="095bc-156">이러한 메트릭을 VM 또는 가상 컴퓨터 확장 집합에서 Azure Diagnostics를 사용할 때 액세스할 수 있는 게스트 OS 수준 메트릭과 혼동해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-156">These metrics are not to be confused with the Guest-OS-level metrics that you have access to when you turn on Azure Diagnostics on your VMs or virtual machine scale sets.</span></span> <span data-ttu-id="095bc-157">Diagnostics 구성에 대한 자세한 내용은 [Microsoft Azure 진단이란?](../azure-diagnostics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="095bc-157">To learn more about configuring Diagnostics, see [What is Microsoft Azure Diagnostics](../azure-diagnostics.md).</span></span>
>
>

## <a name="access-metrics-via-the-rest-api"></a><span data-ttu-id="095bc-158">REST API를 통해 메트릭 액세스</span><span class="sxs-lookup"><span data-stu-id="095bc-158">Access metrics via the REST API</span></span>
<span data-ttu-id="095bc-159">Azure Monitor API를 통해 Azure Metrics에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-159">Azure Metrics can be accessed via the Azure Monitor APIs.</span></span> <span data-ttu-id="095bc-160">메트릭 검색 및 액세스에 사용할 수 있는 2가지 API가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-160">There are two APIs that help you discover and access metrics:</span></span>

* <span data-ttu-id="095bc-161">[Azure Monitor 메트릭 정의 REST API](https://msdn.microsoft.com/library/mt743621.aspx)를 사용하여 서비스에 사용 가능한 메트릭 목록에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-161">Use the [Azure Monitor Metric definitions REST API](https://msdn.microsoft.com/library/mt743621.aspx) to access the list of metrics that are available for a service.</span></span>
* <span data-ttu-id="095bc-162">[Azure Monitor 메트릭 REST API](https://msdn.microsoft.com/library/mt743622.aspx)를 사용하여 실제 메트릭 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-162">Use the [Azure Monitor Metrics REST API](https://msdn.microsoft.com/library/mt743622.aspx) to access the actual metrics data.</span></span>

> [!NOTE]
> <span data-ttu-id="095bc-163">이 문서에서는 Azure 리소스에 대해 [메트릭의 새 API](https://msdn.microsoft.com/library/dn931930.aspx) 를 통한 메트릭을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-163">This article covers the metrics via the [new API for metrics](https://msdn.microsoft.com/library/dn931930.aspx) for Azure resources.</span></span> <span data-ttu-id="095bc-164">새 메트릭 정의 API의 API 버전은 2016-03-01이며 메트릭 API에 대한 버전은 2016-09-01입니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-164">The API version for the new metric definitions API is 2016-03-01 and the version for metrics API is 2016-09-01.</span></span> <span data-ttu-id="095bc-165">레거시 메트릭 정의 및 메트릭은 API 버전 2014-04-01로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-165">The legacy metric definitions and metrics can be accessed with the API version 2014-04-01.</span></span>
>
>

<span data-ttu-id="095bc-166">Azure Monitor REST API 사용에 대한 자세한 연습은 [Azure Monitor REST API 연습](monitoring-rest-api-walkthrough.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="095bc-166">For a more detailed walkthrough using the Azure Monitor REST APIs, see [Azure Monitor REST API walkthrough](monitoring-rest-api-walkthrough.md).</span></span>

## <a name="export-metrics"></a><span data-ttu-id="095bc-167">메트릭 내보내기</span><span class="sxs-lookup"><span data-stu-id="095bc-167">Export metrics</span></span>
<span data-ttu-id="095bc-168">**모니터** 탭의 **진단 설정** 블레이드로 이동하여 메트릭의 내보내기 옵션을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-168">You can go to the **Diagnostics settings** blade under the **Monitor** tab and view the export options for metrics.</span></span> <span data-ttu-id="095bc-169">이 문서의 앞에서 설명한 사용 사례에 대해 Blob 저장소, Azure Event Hubs 또는 OMS로 라우팅할 메트릭(및 진단 로드)을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-169">You can select metrics (and diagnostic logs) to be routed to Blob storage, to Azure Event Hubs, or to OMS for use-cases that were mentioned previously in this article.</span></span>

 ![Azure Monitor에서 메트릭에 대한 내보내기 옵션](./media/monitoring-overview-metrics/MetricsOverview3.png)

<span data-ttu-id="095bc-171">Resource Manager 템플릿, [PowerShell](insights-powershell-samples.md), [Azure CLI](insights-cli-samples.md) 또는 [REST APIs](https://msdn.microsoft.com/library/dn931943.aspx)를 통해 이 항목을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-171">You can configure this via Resource Manager templates, [PowerShell](insights-powershell-samples.md), [Azure CLI](insights-cli-samples.md), or [REST APIs](https://msdn.microsoft.com/library/dn931943.aspx).</span></span>

## <a name="take-action-on-metrics"></a><span data-ttu-id="095bc-172">메트릭에 대한 작업</span><span class="sxs-lookup"><span data-stu-id="095bc-172">Take action on metrics</span></span>
<span data-ttu-id="095bc-173">메트릭 데이터에 대해 알림을 받거나 자동 작업을 수행하려면 자동 크기 조정 설정에서 알림 규칙을 구성하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-173">To receive notifications or take automated actions on metric data, you can configure alert rules or Autoscale settings.</span></span>

### <a name="configure-alert-rules"></a><span data-ttu-id="095bc-174">경고 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="095bc-174">Configure alert rules</span></span>
<span data-ttu-id="095bc-175">메트릭에 대해 경고 규칙을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-175">You can configure alert rules on metrics.</span></span> <span data-ttu-id="095bc-176">이러한 경고 규칙으로 메트릭이 특정 임계값을 초과했는지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-176">These alert rules can check if a metric has crossed a certain threshold.</span></span> <span data-ttu-id="095bc-177">그런 다음 전자 메일을 통해 알리거나 사용자 지정 스크립트를 실행하는 데 사용할 수 있는 webhook를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-177">They can then notify you via email or fire a webhook that can be used to run any custom script.</span></span> <span data-ttu-id="095bc-178">webhook를 사용하여 타사 제품 통합을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-178">You can also use the webhook to configure third-party product integrations.</span></span>

 ![Azure Monitor의 메트릭 및 경고 규칙](./media/monitoring-overview-metrics/MetricsOverview4.png)

### <a name="autoscale-your-azure-resources"></a><span data-ttu-id="095bc-180">Azure 리소스에서 자동 크기 조정</span><span class="sxs-lookup"><span data-stu-id="095bc-180">Autoscale your Azure resources</span></span>
<span data-ttu-id="095bc-181">일부 Azure 리소스에서는 워크로드 처리를 위해 여러 인스턴스의 확대 또는 축소를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-181">Some Azure resources support the scaling out or in of multiple instances to handle your workloads.</span></span> <span data-ttu-id="095bc-182">자동 크기 조정은 App Service(Web Apps), 가상 컴퓨터 확장 집합 및 기존 Azure Cloud Services에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-182">Autoscale applies to App Service (Web Apps), virtual machine scale sets, and classic Azure Cloud Services.</span></span> <span data-ttu-id="095bc-183">특정 메트릭이 지정한 임계값을 초과할 때 규모를 확대하거나 축소하도록 자동 크기 조정 규칙을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-183">You can configure Autoscale rules to scale out or in when a certain metric that impacts your workload crosses a threshold that you specify.</span></span> <span data-ttu-id="095bc-184">자세한 내용은 [자동 크기 조정 개요](monitoring-overview-autoscale.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="095bc-184">For more information, see [Overview of autoscaling](monitoring-overview-autoscale.md).</span></span>

 ![Azure Monitor의 메트릭 및 자동 크기 조정](./media/monitoring-overview-metrics/MetricsOverview5.png)

## <a name="learn-about-supported-services-and-metrics"></a><span data-ttu-id="095bc-186">지원되는 서비스 및 메트릭에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="095bc-186">Learn about supported services and metrics</span></span>
<span data-ttu-id="095bc-187">Azure Monitor는 새로운 메트릭 인프라입니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-187">Azure Monitor is a new metrics infrastructure.</span></span> <span data-ttu-id="095bc-188">다음과 같은 Azure Portal의 Azure 서비스 및 새 버전의 Azure Monitor API을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-188">It supports the following Azure services in the Azure portal and the new version of the Azure Monitor API:</span></span>

* <span data-ttu-id="095bc-189">VM(Azure Resource Manager 기반)</span><span class="sxs-lookup"><span data-stu-id="095bc-189">VMs (Azure Resource Manager-based)</span></span>
* <span data-ttu-id="095bc-190">가상 컴퓨터 확장 집합</span><span class="sxs-lookup"><span data-stu-id="095bc-190">Virtual machine scale sets</span></span>
* <span data-ttu-id="095bc-191">Batch</span><span class="sxs-lookup"><span data-stu-id="095bc-191">Batch</span></span>
* <span data-ttu-id="095bc-192">Event Hubs 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="095bc-192">Event Hubs namespace</span></span>
* <span data-ttu-id="095bc-193">서비스 버스 네임스페이스(프리미엄 SKU에만 해당)</span><span class="sxs-lookup"><span data-stu-id="095bc-193">Service Bus namespace (premium SKU only)</span></span>
* <span data-ttu-id="095bc-194">SQL Database(버전 12)</span><span class="sxs-lookup"><span data-stu-id="095bc-194">SQL Database (version 12)</span></span>
* <span data-ttu-id="095bc-195">탄력적인 SQL 풀</span><span class="sxs-lookup"><span data-stu-id="095bc-195">Elastic SQL Pool</span></span>
* <span data-ttu-id="095bc-196">웹 사이트</span><span class="sxs-lookup"><span data-stu-id="095bc-196">Websites</span></span>
* <span data-ttu-id="095bc-197">웹 서버 팜</span><span class="sxs-lookup"><span data-stu-id="095bc-197">Web server farms</span></span>
* <span data-ttu-id="095bc-198">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="095bc-198">Logic Apps</span></span>
* <span data-ttu-id="095bc-199">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="095bc-199">IoT hubs</span></span>
* <span data-ttu-id="095bc-200">Redis 캐시</span><span class="sxs-lookup"><span data-stu-id="095bc-200">Redis Cache</span></span>
* <span data-ttu-id="095bc-201">네트워킹: 응용 프로그램 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="095bc-201">Networking: Application gateways</span></span>
* <span data-ttu-id="095bc-202">Search</span><span class="sxs-lookup"><span data-stu-id="095bc-202">Search</span></span>

<span data-ttu-id="095bc-203">모든 지원되는 서비스 및 메트릭의 상세 목록은 [Azure Monitor 메트릭 - 리소스 유형별 지원 메트릭](monitoring-supported-metrics.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-203">You can view a detailed list of all the supported services and their metrics at [Azure Monitor metrics--supported metrics per resource type](monitoring-supported-metrics.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="095bc-204">다음 단계</span><span class="sxs-lookup"><span data-stu-id="095bc-204">Next steps</span></span>
<span data-ttu-id="095bc-205">이 문서에 있는 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="095bc-205">Refer to the links throughout this article.</span></span> <span data-ttu-id="095bc-206">또한 다음을 학습할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095bc-206">Additionally, learn about:</span></span>  

* [<span data-ttu-id="095bc-207">자동 크기 조정에 대한 공통 메트릭</span><span class="sxs-lookup"><span data-stu-id="095bc-207">Common metrics for autoscaling</span></span>](insights-autoscale-common-metrics.md)
* [<span data-ttu-id="095bc-208">경고 규칙을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="095bc-208">How to create alert rules</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="095bc-209">Azure Storage에서 Log Analytics를 사용하여 로그 분석</span><span class="sxs-lookup"><span data-stu-id="095bc-209">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)

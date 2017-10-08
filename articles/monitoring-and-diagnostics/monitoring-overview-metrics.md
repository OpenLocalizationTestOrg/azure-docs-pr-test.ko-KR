---
title: "Microsoft Azure에서 메트릭 aaaOverview | Microsoft Docs"
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
ms.openlocfilehash: 2b97f51e0554dae95a929241ae1f0e25e5c215ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a><span data-ttu-id="749c0-103">Microsoft Azure의 메트릭 개요</span><span class="sxs-lookup"><span data-stu-id="749c0-103">Overview of metrics in Microsoft Azure</span></span>
<span data-ttu-id="749c0-104">이 문서에서는 Microsoft azure에서 이점 이란 메트릭 설명 방법과 toostart 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-104">This article describes what metrics are in Microsoft Azure, their benefits, and how toostart using them.</span></span>  

## <a name="what-are-metrics"></a><span data-ttu-id="749c0-105">메트릭이 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="749c0-105">What are metrics?</span></span>
<span data-ttu-id="749c0-106">Azure 모니터 hello 성능 및 Azure에서 작업의 상태에 대 한 tooconsume 원격 분석 toogain 가시성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-106">Azure Monitor enables you tooconsume telemetry toogain visibility into hello performance and health of your workloads on Azure.</span></span> <span data-ttu-id="749c0-107">Azure 원격 분석 데이터의 가장 중요 한 형식은 hello에는 대부분의 Azure 리소스에서 내보내는 hello 메트릭 (성능 카운터)입니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-107">hello most important type of Azure telemetry data is hello metrics (also called performance counters) emitted by most Azure resources.</span></span> <span data-ttu-id="749c0-108">여러 가지 방법으로 tooconfigure 제공 하 고 모니터링 및 문제 해결에 대 한 이러한 메트릭을 사용 하는 azure 모니터 합니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-108">Azure Monitor provides several ways tooconfigure and consume these metrics for monitoring and troubleshooting.</span></span>

## <a name="what-can-you-do-with-metrics"></a><span data-ttu-id="749c0-109">메트릭으로 무엇을 할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="749c0-109">What can you do with metrics?</span></span>
<span data-ttu-id="749c0-110">메트릭 원격 분석의 중요 한 소스로 및 toodo hello 다음 작업을 사용 하면:</span><span class="sxs-lookup"><span data-stu-id="749c0-110">Metrics are a valuable source of telemetry and enable you toodo hello following tasks:</span></span>

* <span data-ttu-id="749c0-111">**Hello 성능을 추적** 포털 차트에서 해당 메트릭이 그래프에 표시 및 해당 차트 tooa 대시보드에 고정 하 여 리소스 (예: VM, 웹 사이트 또는 논리 앱).</span><span class="sxs-lookup"><span data-stu-id="749c0-111">**Track hello performance** of your resource (such as a VM, website, or logic app) by plotting its metrics on a portal chart and pinning that chart tooa dashboard.</span></span>
* <span data-ttu-id="749c0-112">**문제의 알림** 된 메트릭이 특정 임계값을 초과할 때 영향을 미치는 리소스의 성능을 hello 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-112">**Get notified of an issue** that impacts hello performance of your resource when a metric crosses a certain threshold.</span></span>
* <span data-ttu-id="749c0-113">메트릭이 특정 임계값을 초과할 때 리소스 자동 크기 조정 또는 runbook 실행 등과 같은 **자동화된 작업을 구성합니다**.</span><span class="sxs-lookup"><span data-stu-id="749c0-113">**Configure automated actions**, such as autoscaling a resource or firing a runbook when a metric crosses a certain threshold.</span></span>
* <span data-ttu-id="749c0-114">리소스의 성능 또는 사용 추세에 대한 **고급 분석**이나 보고를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-114">**Perform advanced analytics** or reporting on performance or usage trends of your resource.</span></span>
* <span data-ttu-id="749c0-115">**보관** 리소스의 성능 또는 상태 기록을 hello **규정 준수 또는 감사에 대 한** 목적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-115">**Archive** hello performance or health history of your resource **for compliance or auditing** purposes.</span></span>

## <a name="what-are-hello-characteristics-of-metrics"></a><span data-ttu-id="749c0-116">메트릭 hello 특성은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="749c0-116">What are hello characteristics of metrics?</span></span>
<span data-ttu-id="749c0-117">메트릭 hello 특성 뒤에</span><span class="sxs-lookup"><span data-stu-id="749c0-117">Metrics have hello following characteristics:</span></span>

* <span data-ttu-id="749c0-118">모든 메트릭은 **1분 빈도**입니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-118">All metrics have **one-minute frequency**.</span></span> <span data-ttu-id="749c0-119">메트릭 값을 1 분 마다에서 받게 리소스를 거의 hello 상태와 리소스의 상태에 대 한 실시간 가시성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-119">You receive a metric value every minute from your resource, giving you near real-time visibility into hello state and health of your resource.</span></span>
* <span data-ttu-id="749c0-120">메트릭은 **즉시 사용할 수 있습니다**.</span><span class="sxs-lookup"><span data-stu-id="749c0-120">Metrics are **available immediately**.</span></span> <span data-ttu-id="749c0-121">Tooopt에 필요 하지 않거나 추가 진단을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-121">You don't need tooopt in or set up additional diagnostics.</span></span>
* <span data-ttu-id="749c0-122">각 메트릭에 대해 **30일 동안의 기록** 에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-122">You can access **30 days of history** for each metric.</span></span> <span data-ttu-id="749c0-123">Hello 최근 및 월별 추세 hello 성능이 나 리소스의 상태를 신속 하 게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-123">You can quickly look at hello recent and monthly trends in hello performance or health of your resource.</span></span>

<span data-ttu-id="749c0-124">또한 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-124">You can also:</span></span>

* <span data-ttu-id="749c0-125">메트릭을 구성 **걸리거나 알림을 전송 하는 규칙 작업을 자동화 하는 경고** hello 메트릭을 설정 된 hello 임계값을 교차 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="749c0-125">Configure a metric **alert rule that sends a notification or takes automated action** when hello metric crosses hello threshold that you have set.</span></span> <span data-ttu-id="749c0-126">자동 크기 조정 tooscale 리소스 toomeet 들어오는 요청을 사용 하거나 웹 사이트 또는 컴퓨팅 리소스를 로드 하는 특별 한 자동화 된 작업이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-126">Autoscale is a special automated action that enables you tooscale out your resource toomeet incoming requests or loads on your website or computing resources.</span></span> <span data-ttu-id="749c0-127">자동 크기 조정 설정 규칙 tooscale 또는 축소 임계값을 교차 하는 메트릭을에 따라 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-127">You can configure an Autoscale setting rule tooscale in or out based on a metric crossing a threshold.</span></span>

* <span data-ttu-id="749c0-128">**경로** 모든 메트릭 Application Insights 또는 로그 분석 (OMS) tooenable 즉시 분석, 검색 및 사용자 지정 리소스의 메트릭 데이터에 대해 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-128">**Route** all metrics Application Insights or Log Analytics (OMS) tooenable instant analytics, search, and custom alerting on metrics data from your resources.</span></span> <span data-ttu-id="749c0-129">메트릭 tooan 이벤트 허브를 스트리밍할 수도, 수 있게 해 주는 toothen 라우팅하 tooAzure Stream Analytics 또는 거의 실시간으로 분석을 위해 toocustom 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-129">You can also stream metrics tooan Event Hub, enabling you toothen route them tooAzure Stream Analytics or toocustom apps for near-real time analysis.</span></span> <span data-ttu-id="749c0-130">진단 설정을 사용하여 Event Hub 스트리밍을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-130">You set up Event Hub streaming using diagnostic settings.</span></span>

* <span data-ttu-id="749c0-131">**메트릭 toostorage 보관** 더 긴 보존에 대 한 오프 라인 보고에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-131">**Archive metrics toostorage** for longer retention or use them for offline reporting.</span></span> <span data-ttu-id="749c0-132">리소스에 대 한 진단 설정을 구성할 때 프로그램 메트릭 tooAzure Blob 저장소를 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-132">You can route your metrics tooAzure Blob storage when you configure diagnostic settings for your resource.</span></span>

* <span data-ttu-id="749c0-133">에 액세스를 쉽게 검색 하 고 **모든 메트릭을 표시** hello 리소스를 선택 하 고 차트에 메트릭을 hello 그릴 경우 Azure 포털을 통해.</span><span class="sxs-lookup"><span data-stu-id="749c0-133">Easily discover, access, and **view all metrics** via hello Azure portal when you select a resource and plot hello metrics on a chart.</span></span>

* <span data-ttu-id="749c0-134">**사용할** hello 메트릭을 통해 hello 새로운 Azure 모니터 REST Api입니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-134">**Consume** hello metrics via hello new Azure Monitor REST APIs.</span></span>

* <span data-ttu-id="749c0-135">**쿼리** 메트릭을 사용 하 여 hello PowerShell cmdlet 또는 플랫폼 간 REST API를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-135">**Query** metrics by using hello PowerShell cmdlets or hello Cross-Platform REST API.</span></span>

  ![Azure Monitor의 메트릭 라우팅](./media/monitoring-overview-metrics/Metrics_Overview_v4.png)

## <a name="access-metrics-via-hello-portal"></a><span data-ttu-id="749c0-137">Hello 포털을 통해 메트릭 액세스</span><span class="sxs-lookup"><span data-stu-id="749c0-137">Access metrics via hello portal</span></span>
<span data-ttu-id="749c0-138">다음은 어떻게 toocreate 메트릭 차트를 사용 하 여 hello Azure 포털의 빠른 연습입니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-138">Following is a quick walkthrough of how toocreate a metric chart by using hello Azure portal.</span></span>

### <a name="tooview-metrics-after-creating-a-resource"></a><span data-ttu-id="749c0-139">리소스를 만든 후 tooview 메트릭</span><span class="sxs-lookup"><span data-stu-id="749c0-139">tooview metrics after creating a resource</span></span>
1. <span data-ttu-id="749c0-140">Azure 포털 hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-140">Open hello Azure portal.</span></span>
2. <span data-ttu-id="749c0-141">Azure App Service 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-141">Create an Azure App Service website.</span></span>
3. <span data-ttu-id="749c0-142">웹 사이트를 만든 후 이동 toohello **개요** hello 웹 사이트의 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-142">After you create a website, go toohello **Overview** blade of hello website.</span></span>
4. <span data-ttu-id="749c0-143">**모니터링** 타일로 새 메트릭을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-143">You can view new metrics as a **Monitoring** tile.</span></span> <span data-ttu-id="749c0-144">그런 다음 hello 타일을 편집 하 고 개의 추가 메트릭 선택 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-144">You can then edit hello tile and select more metrics.</span></span>

   ![Azure Monitor의 리소스에 대한 메트릭](./media/monitoring-overview-metrics/MetricsOverview1.png)

### <a name="tooaccess-all-metrics-in-a-single-place"></a><span data-ttu-id="749c0-146">tooaccess을 한 곳에서 모든 메트릭</span><span class="sxs-lookup"><span data-stu-id="749c0-146">tooaccess all metrics in a single place</span></span>
1. <span data-ttu-id="749c0-147">Azure 포털 hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-147">Open hello Azure portal.</span></span>
2. <span data-ttu-id="749c0-148">새 toohello 이동 **모니터** 탭을 클릭 한 다음 선택한 hello **메트릭** 아래에 있는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-148">Navigate toohello new **Monitor** tab, and then and select hello **Metrics** option underneath it.</span></span>
3. <span data-ttu-id="749c0-149">구독, 리소스 그룹 및 hello 리소스의 hello 이름 hello 드롭 다운 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-149">Select your subscription, resource group, and hello name of hello resource from hello drop-down list.</span></span>
4. <span data-ttu-id="749c0-150">보기 hello 사용 가능한 메트릭 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-150">View hello available metrics list.</span></span> <span data-ttu-id="749c0-151">관심 있는 및 그리는 것 hello 메트릭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-151">Then select hello metric you are interested in and plot it.</span></span>
5. <span data-ttu-id="749c0-152">Hello pin에 hello 오른쪽 위 모퉁이 클릭 하 여 toohello 대시보드 것 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-152">You can pin it toohello dashboard by clicking hello pin on hello upper-right corner.</span></span>

   ![Azure Monitor에서 모든 메트릭을 한 곳에서 액세스](./media/monitoring-overview-metrics/MetricsOverview2.png)

> [!NOTE]
> <span data-ttu-id="749c0-154">추가적인 진단 설정 없이 VM(Azure Resource Manager 기반) 및 가상 컴퓨터 확장 집합에서 호스트 설정 메트릭에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-154">You can access host-level metrics from VMs (Azure Resource Manager-based) and virtual machine scale sets without any additional diagnostic setup.</span></span> <span data-ttu-id="749c0-155">이러한 호스트 수준 메트릭은 Windows 및 Linux 인스턴스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-155">These new host-level metrics are available for Windows and Linux instances.</span></span> <span data-ttu-id="749c0-156">이러한 메트릭은 toobe hello 또는 가상 컴퓨터 크기 집합 Vm에 Azure 진단에서 설정한 액세스 toowhen 있는 게스트 운영 체제 수준 메트릭와 혼동된 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-156">These metrics are not toobe confused with hello Guest-OS-level metrics that you have access toowhen you turn on Azure Diagnostics on your VMs or virtual machine scale sets.</span></span> <span data-ttu-id="749c0-157">진단 구성에 대 한 더 toolearn 참조 [란 Microsoft Azure 진단](../azure-diagnostics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-157">toolearn more about configuring Diagnostics, see [What is Microsoft Azure Diagnostics](../azure-diagnostics.md).</span></span>
>
>

## <a name="access-metrics-via-hello-rest-api"></a><span data-ttu-id="749c0-158">Hello REST API를 통해 메트릭 액세스</span><span class="sxs-lookup"><span data-stu-id="749c0-158">Access metrics via hello REST API</span></span>
<span data-ttu-id="749c0-159">Azure 메트릭 hello Azure 모니터 Api를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-159">Azure Metrics can be accessed via hello Azure Monitor APIs.</span></span> <span data-ttu-id="749c0-160">메트릭 검색 및 액세스에 사용할 수 있는 2가지 API가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-160">There are two APIs that help you discover and access metrics:</span></span>

* <span data-ttu-id="749c0-161">사용 하 여 hello [Azure 모니터 메트릭의 정의 REST API](https://msdn.microsoft.com/library/mt743621.aspx) tooaccess hello 서비스에 사용할 수 있는 메트릭 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-161">Use hello [Azure Monitor Metric definitions REST API](https://msdn.microsoft.com/library/mt743621.aspx) tooaccess hello list of metrics that are available for a service.</span></span>
* <span data-ttu-id="749c0-162">사용 하 여 hello [Azure 모니터 메트릭 REST API](https://msdn.microsoft.com/library/mt743622.aspx) tooaccess hello 실제 메트릭 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-162">Use hello [Azure Monitor Metrics REST API](https://msdn.microsoft.com/library/mt743622.aspx) tooaccess hello actual metrics data.</span></span>

> [!NOTE]
> <span data-ttu-id="749c0-163">이 문서에서는 hello 통해 hello 메트릭 [메트릭에 대 한 새로운 API](https://msdn.microsoft.com/library/dn931930.aspx) Azure 리소스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-163">This article covers hello metrics via hello [new API for metrics](https://msdn.microsoft.com/library/dn931930.aspx) for Azure resources.</span></span> <span data-ttu-id="749c0-164">hello 새 메트릭 정의 API에 대 한 hello API 버전은 2016-03-01 및 API 메트릭 hello 버전은 2016-09-01입니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-164">hello API version for hello new metric definitions API is 2016-03-01 and hello version for metrics API is 2016-09-01.</span></span> <span data-ttu-id="749c0-165">hello 레거시 메트릭 정 및 메트릭을 hello API 버전 2014-04-01로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-165">hello legacy metric definitions and metrics can be accessed with hello API version 2014-04-01.</span></span>
>
>

<span data-ttu-id="749c0-166">Hello Azure 모니터 REST Api를 사용 하 여 보다 자세한 연습을 참조 하십시오. [Azure 모니터 REST API 연습](monitoring-rest-api-walkthrough.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-166">For a more detailed walkthrough using hello Azure Monitor REST APIs, see [Azure Monitor REST API walkthrough](monitoring-rest-api-walkthrough.md).</span></span>

## <a name="export-metrics"></a><span data-ttu-id="749c0-167">메트릭 내보내기</span><span class="sxs-lookup"><span data-stu-id="749c0-167">Export metrics</span></span>
<span data-ttu-id="749c0-168">Toohello 이동할 수 있습니다 **진단 설정을** hello 아래 블레이드 **모니터** 메트릭에 대 한 탭 및 보기 hello 내보내기 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-168">You can go toohello **Diagnostics settings** blade under hello **Monitor** tab and view hello export options for metrics.</span></span> <span data-ttu-id="749c0-169">이 문서의 toobe 라우팅된 tooBlob 저장소나 tooAzure 이벤트 허브 tooOMS 언급 된 사용 사례에 대 한 메트릭 (및 진단 로그)를 이전에 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-169">You can select metrics (and diagnostic logs) toobe routed tooBlob storage, tooAzure Event Hubs, or tooOMS for use-cases that were mentioned previously in this article.</span></span>

 ![Azure Monitor에서 메트릭에 대한 내보내기 옵션](./media/monitoring-overview-metrics/MetricsOverview3.png)

<span data-ttu-id="749c0-171">Resource Manager 템플릿, [PowerShell](insights-powershell-samples.md), [Azure CLI](insights-cli-samples.md) 또는 [REST APIs](https://msdn.microsoft.com/library/dn931943.aspx)를 통해 이 항목을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-171">You can configure this via Resource Manager templates, [PowerShell](insights-powershell-samples.md), [Azure CLI](insights-cli-samples.md), or [REST APIs](https://msdn.microsoft.com/library/dn931943.aspx).</span></span>

## <a name="take-action-on-metrics"></a><span data-ttu-id="749c0-172">메트릭에 대한 작업</span><span class="sxs-lookup"><span data-stu-id="749c0-172">Take action on metrics</span></span>
<span data-ttu-id="749c0-173">tooreceive 알림이나 메트릭 데이터에 대해 자동화 된 take 작업 경고 규칙 또는 자동 크기 조정 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-173">tooreceive notifications or take automated actions on metric data, you can configure alert rules or Autoscale settings.</span></span>

### <a name="configure-alert-rules"></a><span data-ttu-id="749c0-174">경고 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="749c0-174">Configure alert rules</span></span>
<span data-ttu-id="749c0-175">메트릭에 대해 경고 규칙을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-175">You can configure alert rules on metrics.</span></span> <span data-ttu-id="749c0-176">이러한 경고 규칙으로 메트릭이 특정 임계값을 초과했는지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-176">These alert rules can check if a metric has crossed a certain threshold.</span></span> <span data-ttu-id="749c0-177">다음 전자 메일을 통해 알려 하거나 모든 사용자 지정 스크립트 사용된 toorun 일 수 있는 webhook 발생 수입니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-177">They can then notify you via email or fire a webhook that can be used toorun any custom script.</span></span> <span data-ttu-id="749c0-178">또한 hello webhook tooconfigure 타사 제품 통합을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-178">You can also use hello webhook tooconfigure third-party product integrations.</span></span>

 ![Azure Monitor의 메트릭 및 경고 규칙](./media/monitoring-overview-metrics/MetricsOverview4.png)

### <a name="autoscale-your-azure-resources"></a><span data-ttu-id="749c0-180">Azure 리소스에서 자동 크기 조정</span><span class="sxs-lookup"><span data-stu-id="749c0-180">Autoscale your Azure resources</span></span>
<span data-ttu-id="749c0-181">일부 Azure 리소스의 크기 조정을 걸러 내 거 나에서 여러 인스턴스 toohandle 작업 hello를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-181">Some Azure resources support hello scaling out or in of multiple instances toohandle your workloads.</span></span> <span data-ttu-id="749c0-182">자동 크기 조정 tooApp (웹 응용 프로그램) 서비스, 가상 컴퓨터 크기 집합 및 클래식 Azure 클라우드 서비스에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-182">Autoscale applies tooApp Service (Web Apps), virtual machine scale sets, and classic Azure Cloud Services.</span></span> <span data-ttu-id="749c0-183">작업에 영향을 주는 특정 메트릭을 지정 하는 임계값을 초과할 때 자동 크기 조정 규칙 tooscale 걸러 내 거 나에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-183">You can configure Autoscale rules tooscale out or in when a certain metric that impacts your workload crosses a threshold that you specify.</span></span> <span data-ttu-id="749c0-184">자세한 내용은 [자동 크기 조정 개요](monitoring-overview-autoscale.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="749c0-184">For more information, see [Overview of autoscaling](monitoring-overview-autoscale.md).</span></span>

 ![Azure Monitor의 메트릭 및 자동 크기 조정](./media/monitoring-overview-metrics/MetricsOverview5.png)

## <a name="learn-about-supported-services-and-metrics"></a><span data-ttu-id="749c0-186">지원되는 서비스 및 메트릭에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="749c0-186">Learn about supported services and metrics</span></span>
<span data-ttu-id="749c0-187">Azure Monitor는 새로운 메트릭 인프라입니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-187">Azure Monitor is a new metrics infrastructure.</span></span> <span data-ttu-id="749c0-188">Azure 포털 및 hello 새 버전의 hello Azure 모니터 API hello에서 Azure 서비스를 수행 하는 hello를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-188">It supports hello following Azure services in hello Azure portal and hello new version of hello Azure Monitor API:</span></span>

* <span data-ttu-id="749c0-189">VM(Azure Resource Manager 기반)</span><span class="sxs-lookup"><span data-stu-id="749c0-189">VMs (Azure Resource Manager-based)</span></span>
* <span data-ttu-id="749c0-190">가상 컴퓨터 확장 집합</span><span class="sxs-lookup"><span data-stu-id="749c0-190">Virtual machine scale sets</span></span>
* <span data-ttu-id="749c0-191">Batch</span><span class="sxs-lookup"><span data-stu-id="749c0-191">Batch</span></span>
* <span data-ttu-id="749c0-192">Event Hubs 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="749c0-192">Event Hubs namespace</span></span>
* <span data-ttu-id="749c0-193">서비스 버스 네임스페이스(프리미엄 SKU에만 해당)</span><span class="sxs-lookup"><span data-stu-id="749c0-193">Service Bus namespace (premium SKU only)</span></span>
* <span data-ttu-id="749c0-194">SQL Database(버전 12)</span><span class="sxs-lookup"><span data-stu-id="749c0-194">SQL Database (version 12)</span></span>
* <span data-ttu-id="749c0-195">탄력적인 SQL 풀</span><span class="sxs-lookup"><span data-stu-id="749c0-195">Elastic SQL Pool</span></span>
* <span data-ttu-id="749c0-196">웹 사이트</span><span class="sxs-lookup"><span data-stu-id="749c0-196">Websites</span></span>
* <span data-ttu-id="749c0-197">웹 서버 팜</span><span class="sxs-lookup"><span data-stu-id="749c0-197">Web server farms</span></span>
* <span data-ttu-id="749c0-198">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="749c0-198">Logic Apps</span></span>
* <span data-ttu-id="749c0-199">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="749c0-199">IoT hubs</span></span>
* <span data-ttu-id="749c0-200">Redis 캐시</span><span class="sxs-lookup"><span data-stu-id="749c0-200">Redis Cache</span></span>
* <span data-ttu-id="749c0-201">네트워킹: 응용 프로그램 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="749c0-201">Networking: Application gateways</span></span>
* <span data-ttu-id="749c0-202">검색</span><span class="sxs-lookup"><span data-stu-id="749c0-202">Search</span></span>

<span data-ttu-id="749c0-203">모든 지원 되는 hello 서비스와 해당 메트릭을에서 자세한 목록을 볼 수 있습니다 [Azure 모니터 메트릭-리소스 유형 마다 지원 되는 메트릭](monitoring-supported-metrics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-203">You can view a detailed list of all hello supported services and their metrics at [Azure Monitor metrics--supported metrics per resource type](monitoring-supported-metrics.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="749c0-204">다음 단계</span><span class="sxs-lookup"><span data-stu-id="749c0-204">Next steps</span></span>
<span data-ttu-id="749c0-205">이 문서 전체에서 toohello 링크를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="749c0-205">Refer toohello links throughout this article.</span></span> <span data-ttu-id="749c0-206">또한 다음을 학습할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="749c0-206">Additionally, learn about:</span></span>  

* [<span data-ttu-id="749c0-207">자동 크기 조정에 대한 공통 메트릭</span><span class="sxs-lookup"><span data-stu-id="749c0-207">Common metrics for autoscaling</span></span>](insights-autoscale-common-metrics.md)
* [<span data-ttu-id="749c0-208">어떻게 toocreate 경고 규칙</span><span class="sxs-lookup"><span data-stu-id="749c0-208">How toocreate alert rules</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="749c0-209">Azure Storage에서 Log Analytics를 사용하여 로그 분석</span><span class="sxs-lookup"><span data-stu-id="749c0-209">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)

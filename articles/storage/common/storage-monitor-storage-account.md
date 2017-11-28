---
title: "Azure Storage 계정을 모니터링하는 방법 | Microsoft Docs"
description: "Azure 포털을 사용하여 Azure에서 저장소 계정을 모니터링하는 방법에 대해 알아봅니다."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: b83cba7b-4627-4ba7-b5d0-f1039fe30e78
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: marsma
ms.openlocfilehash: e8fbc4ecdffe62806019f494e1412cfedbccf71f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-a-storage-account-in-the-azure-portal"></a><span data-ttu-id="0f008-103">Azure 포털에서 저장소 계정 모니터링</span><span class="sxs-lookup"><span data-stu-id="0f008-103">Monitor a storage account in the Azure portal</span></span>

<span data-ttu-id="0f008-104">[Azure 저장소 분석](../storage-analytics.md)은 모든 저장소 서비스에 대한 메트릭과 Blob, 큐 및 테이블에 대한 로그를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-104">[Azure Storage Analytics](../storage-analytics.md) provides metrics for all storage services, and logs for blobs, queues, and tables.</span></span> <span data-ttu-id="0f008-105">[Azure Portal](https://portal.azure.com)을 사용하여 계정에 기록되는 메트릭 및 로그를 구성하고, 메트릭 데이터를 시각적으로 표현하는 차트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-105">You can use the [Azure portal](https://portal.azure.com) to configure which metrics and logs are recorded for your account, and configure charts that provide visual representations of your metrics data.</span></span>

> [!NOTE]
> <span data-ttu-id="0f008-106">Azure Portal에서 모니터링 데이터를 검사하는 데 관련된 비용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-106">There are costs associated with examining monitoring data in the Azure portal.</span></span> <span data-ttu-id="0f008-107">자세한 내용은 [저장소 분석 및 청구](/rest/api/storageservices/Storage-Analytics-and-Billing)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f008-107">For more information, see [Storage Analytics and Billing](/rest/api/storageservices/Storage-Analytics-and-Billing).</span></span>
>
> <span data-ttu-id="0f008-108">Azure 파일 저장소는 현재 저장소 분석 메트릭을 지원하지만 아직 로깅을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-108">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span></span>
>
> <span data-ttu-id="0f008-109">현재 ZRS(영역 중복 저장소) 복제 유형의 저장소 계정에는 메트릭 또는 로깅 기능을 사용하도록 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-109">Storage accounts with a replication type of Zone-Redundant Storage (ZRS) currently do not have the metrics or logging capability enabled.</span></span>
> 
> <span data-ttu-id="0f008-110">저장소 분석 및 기타 도구를 사용하여 Azure 저장소 관련 문제를 식별, 진단 및 해결하는 방법에 대한 자세한 지침은 [Microsoft Azure 저장소 모니터링, 진단 및 문제 해결](../storage-monitoring-diagnosing-troubleshooting.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f008-110">For an in-depth guide on using Storage Analytics and other tools to identify, diagnose, and troubleshoot Azure Storage-related issues, see [Monitor, diagnose, and troubleshoot Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).</span></span>
>

## <a name="configure-monitoring-for-a-storage-account"></a><span data-ttu-id="0f008-111">저장소 계정에 대한 모니터링 구성</span><span class="sxs-lookup"><span data-stu-id="0f008-111">Configure monitoring for a storage account</span></span>

1. <span data-ttu-id="0f008-112">[Azure Portal](https://portal.azure.com)에서 **저장소 계정**, 저장소 계정 이름을 차례로 선택하여 계정 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-112">In the [Azure portal](https://portal.azure.com), select **Storage accounts**, then the storage account name to open the account dashboard.</span></span>
1. <span data-ttu-id="0f008-113">메뉴 블레이드의 **모니터링** 섹션에서 **진단**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-113">Select **Diagnostics** in the **MONITORING** section of the menu blade.</span></span>

    ![모니터링 옵션](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)

1. <span data-ttu-id="0f008-115">모니터링하려는 각 **서비스**에 대한 메트릭 데이터 **유형**과 데이터에 대한 **보존 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-115">Select the **type** of metrics data for each **service** you wish to monitor, and the **retention policy** for the data.</span></span> <span data-ttu-id="0f008-116">또한 **상태**를 **해제**(Off)로 설정하여 모니터링을 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-116">You can also disable monitoring by setting **Status** to **Off**.</span></span>

    ![모니터링 옵션](./media/storage-monitor-storage-account/stg-enable-metrics-01.png)

   <span data-ttu-id="0f008-118">각 서비스에 사용할 수 있는 메트릭에는 다음 두 가지 유형이 있으며, 둘 다 기본적으로 새 저장소 계정에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-118">There are two types of metrics you can enable for each service, both of which are enabled by default for new storage accounts:</span></span>

   * <span data-ttu-id="0f008-119">**집계**: 수신/송신, 가용성, 대기 시간 및 성공 비율과 같은 메트릭을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-119">**Aggregate**: Collects metrics such as ingress/egress, availability, latency, and success percentages.</span></span> <span data-ttu-id="0f008-120">이러한 메트릭은 Blob, 큐, 테이블 및 파일 서비스에 대해 집계됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-120">These metrics are aggregated for the blob, queue, table, and file services.</span></span>
   * <span data-ttu-id="0f008-121">**API당** - 집계 메트릭 외에도 Azure Storage 서비스 API에서 각 저장소 작업에 대해 동일한 메트릭 집합을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-121">**Per API**: In addition to the aggregate metrics, collects the same set of metrics for each storage operation in the Azure Storage service API.</span></span>

   <span data-ttu-id="0f008-122">데이터 보존 정책을 설정하려면 1-365일 중에서 **보존(일)** 슬라이더를 이동하거나 데이터 보존 기간(일)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-122">To set the data retention policy, move the **Retention (days)** slider or enter the number of days of data to retain, from 1 to 365.</span></span> <span data-ttu-id="0f008-123">새 저장소 계정의 기본값은 7일입니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-123">The default for new storage accounts is seven days.</span></span> <span data-ttu-id="0f008-124">보존 정책을 설정하지 않으려면 0을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-124">If you do not want to set a retention policy, enter zero.</span></span> <span data-ttu-id="0f008-125">보존 정책이 없는 경우 언제든 모니터링 데이터를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-125">If there is no retention policy, it is up to you to delete the monitoring data.</span></span>

   > [!WARNING]
   > <span data-ttu-id="0f008-126">메트릭 데이터를 수동으로 삭제하는 경우 요금이 부과되지만,</span><span class="sxs-lookup"><span data-stu-id="0f008-126">You are charged when you manually delete metrics data.</span></span> <span data-ttu-id="0f008-127">오래된 분석 데이터(보존 정책보다 오래된 데이터)는 무료로 시스템에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-127">Stale analytics data (data older than your retention policy) is deleted by the system at no cost.</span></span> <span data-ttu-id="0f008-128">따라서 계정에 대한 저장소 분석 데이터를 보존할 기간에 따라 보존 정책을 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-128">We recommend setting a retention policy based on how long you want to retain storage analytics data for your account.</span></span> <span data-ttu-id="0f008-129">자세한 내용은 [저장소 메트릭 사용 시 발생하는 요금](../common/storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f008-129">See [What charges do you incur when you enable storage metrics?](../common/storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) for more information.</span></span>
   >

1. <span data-ttu-id="0f008-130">모니터링 구성을 완료하면 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-130">When you finish the monitoring configuration, select **Save**.</span></span>

<span data-ttu-id="0f008-131">기본 메트릭 집합은 개별 서비스 블레이드(Blob, 큐, 테이블 및 파일)뿐만 아니라 저장소 계정 블레이드의 차트에도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-131">A default set of metrics is displayed in charts on the storage account blade, as well as the individual service blades (blob, queue, table, and file).</span></span> <span data-ttu-id="0f008-132">서비스에 대한 메트릭을 사용하도록 설정하면 차트에 데이터를 표시하는 데 최대 1시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-132">Once you've enabled metrics for a service, it may take up to an hour for data to appear in its charts.</span></span> <span data-ttu-id="0f008-133">메트릭 차트에서 **편집**을 선택하여 차트에 표시되는 [메트릭을 구성](#how-to-customize-metrics-charts)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-133">You can select **Edit** on any metric chart to [configure which metrics](#how-to-customize-metrics-charts) are displayed in the chart.</span></span>

<span data-ttu-id="0f008-134">**상태**를 **해제**로 설정하여 메트릭 수집 및 로깅을 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-134">You can disable metrics collection and logging by setting **Status** to **Off**.</span></span>

> [!NOTE]
> <span data-ttu-id="0f008-135">Azure Storage는 [테이블 저장소](../common/storage-introduction.md#table-storage)를 사용하여 저장소 계정에 대한 메트릭을 저장하고, 계정의 테이블에 메트릭을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-135">Azure Storage uses [table storage](../common/storage-introduction.md#table-storage) to store the metrics for your storage account, and stores the metrics in tables in your account.</span></span> <span data-ttu-id="0f008-136">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f008-136">For more information, see.</span></span> <span data-ttu-id="0f008-137">[메트릭 저장 방법](../common/storage-analytics.md#how-metrics-are-stored).</span><span class="sxs-lookup"><span data-stu-id="0f008-137">[How metrics are stored](../common/storage-analytics.md#how-metrics-are-stored).</span></span>
>

## <a name="customize-metrics-charts"></a><span data-ttu-id="0f008-138">메트릭 차트 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="0f008-138">Customize metrics charts</span></span>

<span data-ttu-id="0f008-139">다음 절차를 사용하여 메트릭 차트에 표시할 저장소 메트릭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-139">Use the following procedure to choose which storage metrics to view in a metrics chart.</span></span> 

1. <span data-ttu-id="0f008-140">Azure Portal에서 저장소 메트릭 차트를 표시하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-140">Start by displaying a storage metric chart in the Azure portal.</span></span> <span data-ttu-id="0f008-141">차트는 **저장소 계정 블레이드** 및 개별 서비스(Blob, 큐, 테이블, 파일)의 **메트릭** 블레이드에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-141">You can find charts on the **storage account blade** and in the **Metrics** blade for an individual service (blob, queue, table, file).</span></span>

   <span data-ttu-id="0f008-142">여기서는 **저장소 계정 블레이드**에 나타나는 다음과 같은 차트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-142">In this example, we work with the following chart that appears on the **storage account blade**:</span></span>

   ![Azure Portal에서 차트 선택](./media/storage-monitor-storage-account/stg-customize-chart-00.png)

1. <span data-ttu-id="0f008-144">다음으로 차트의 아무 곳이나 클릭하여 **메트릭** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-144">Next, click anywhere within the chart to open the **Metric** blade.</span></span> <span data-ttu-id="0f008-145">**차트 편집**을 선택하여 **차트 편집** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-145">Select **Edit chart** to open the **Edit Chart** blade.</span></span>

   ![차트 블레이드의 차트 편집 단추](./media/storage-monitor-storage-account/stg-customize-chart-01.png)

1. <span data-ttu-id="0f008-147">**차트 편집** 블레이드에서 차트에 표시할 메트릭의 **시간 범위**와 표시하려는 메트릭의 **서비스**(Blob, 큐, 테이블, 파일)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-147">On the **Edit Chart** blade, select the **Time Range** of the metrics to display in the chart, and the **service** (blob, queue, table, file) whose metrics you wish to display.</span></span> <span data-ttu-id="0f008-148">여기서는 다음과 같이 Blob 서비스에 대한 지난 주의 메트릭을 표시하도록 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-148">Here we've selected to display the past week's metrics for the blob service:</span></span>

   ![차트 편집 블레이드의 시간 범위 및 서비스 선택](./media/storage-monitor-storage-account/stg-customize-chart-02.png)

1. <span data-ttu-id="0f008-150">차트에 표시하려는 개별 **메트릭**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-150">Select the individual **metrics** you'd like displayed in the chart, then click **OK**.</span></span> <span data-ttu-id="0f008-151">예를 들어 여기서는 *ContainerCount* 및 *ObjectCount* 메트릭을 표시하도록 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-151">For example, here we've chosen to display the *ContainerCount* and *ObjectCount* metrics:</span></span>

   ![차트 편집 블레이드의 개별 메트릭 선택](./media/storage-monitor-storage-account/stg-customize-chart-03.png)

<span data-ttu-id="0f008-153">차트 설정은 저장소 계정의 모니터링 데이터 수집, 집계 또는 저장에 영향을 주지 않고 메트릭 데이터만 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-153">Your chart settings do not affect the collection, aggregation, or storage of monitoring data in the storage account, only the viewing of metrics data.</span></span>

### <a name="metrics-availability-in-charts"></a><span data-ttu-id="0f008-154">차트의 메트릭 가용성</span><span class="sxs-lookup"><span data-stu-id="0f008-154">Metrics availability in charts</span></span>

<span data-ttu-id="0f008-155">사용 가능한 메트릭 목록은 드롭다운에서 선택한 서비스와 편집 중인 차트의 단위 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-155">The list of available metrics changes based on which service you've chosen in the drop-down, and the unit type of the chart you're editing.</span></span> <span data-ttu-id="0f008-156">예를 들어 단위를 백분율로 표시하는 차트를 편집하는 경우에만 *PercentNetworkError* 및 *PercentThrottlingError*와 같은 백분율 메트릭을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-156">For example, you can select percentage metrics like *PercentNetworkError* and *PercentThrottlingError* only if you're editing a chart that displays units in percentage:</span></span>

![Azure Portal에서 오류 백분율 차트 요청](./media/storage-monitor-storage-account/stg-customize-chart-04.png)

### <a name="metrics-resolution"></a><span data-ttu-id="0f008-158">메트릭 해상도</span><span class="sxs-lookup"><span data-stu-id="0f008-158">Metrics resolution</span></span>

<span data-ttu-id="0f008-159">진단에서 선택한 메트릭에 따라 계정에서 사용할 수 있는 메트릭의 해상도가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-159">The metrics you selected in Diagnostics determines the resolution of the metrics that are available for your account:</span></span>

* <span data-ttu-id="0f008-160">**집계** 모니터링은 수신/송신, 가용성, 대기 시간 및 성공 비율과 같은 메트릭을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-160">**Aggregate** monitoring provides metrics such as ingress/egress, availability, latency, and success percentages.</span></span> <span data-ttu-id="0f008-161">이러한 메트릭은 Blob, 테이블, 파일 및 큐 서비스에서 집계됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-161">These metrics are aggregated from the blob, table, file, and queue services.</span></span>
* <span data-ttu-id="0f008-162">**API당**은 서비스 수준 집계 외에도 개별 저장소 작업에 사용할 수 있는 메트릭과 함께 보다 세밀한 해상도를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-162">**Per API** provides finer resolution, with metrics available for individual storage operations, in addition to the service-level aggregates.</span></span>

## <a name="configure-metrics-alerts"></a><span data-ttu-id="0f008-163">메트릭 경고 구성</span><span class="sxs-lookup"><span data-stu-id="0f008-163">Configure metrics alerts</span></span>

<span data-ttu-id="0f008-164">저장소 리소스 메트릭의 임계값에 도달하면 사용자에게 알리도록 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-164">You can create alerts to notify you when thresholds have been reached for storage resource metrics.</span></span>

1. <span data-ttu-id="0f008-165">**경고 규칙 블레이드**를 열려면 **메뉴 블레이드**의 **모니터링** 섹션으로 스크롤하여 **경고 규칙**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-165">To open the **Alert rules blade**, scroll down to the **MONITORING** section of the **Menu blade** and select **Alert rules**.</span></span>
1. <span data-ttu-id="0f008-166">**경고 추가**를 선택하여 **경고 규칙 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-166">Select **Add alert** to open the **Add an alert rule** blade</span></span>
1. <span data-ttu-id="0f008-167">드롭다운에서 **리소스**(Blob, 파일, 큐, 테이블)를 선택하고 새 경고 규칙에 대한 **이름** 및 **설명**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-167">Select a **Resource** (blob, file, queue, table) from the drop-down, and enter a **Name** and **Description** for your new alert rule.</span></span>
1. <span data-ttu-id="0f008-168">경고, 경고 **조건** 및 **임계값**을 추가하려는 **메트릭**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-168">Select the **Metric** for which you'd like to add an alert, an alert **Condition**, and a **Threshold**.</span></span> <span data-ttu-id="0f008-169">임계값 단위 유형은 선택한 메트릭에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-169">The threshold unit type changes depending on the metric you've chosen.</span></span> <span data-ttu-id="0f008-170">예를 들어 "개수"는 *ContainerCount*의 단위 유형이지만, "백분율"은 *PercentNetworkError* 메트릭의 단위 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-170">For example, "count" is the unit type for *ContainerCount*, while the unit for the *PercentNetworkError* metric is a percentage.</span></span>
1. <span data-ttu-id="0f008-171">**기간**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-171">Select the **Period**.</span></span> <span data-ttu-id="0f008-172">해당 기간 내에 임계값에 도달하거나 초과하는 메트릭은 경고를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-172">Metrics that reach or exceed the Threshold within the period trigger an alert.</span></span>
1. <span data-ttu-id="0f008-173">(선택 사항) **전자 메일** 및 **웹후크** 알림을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-173">(Optional) Configure **Email** and **Webhook** notifications.</span></span> <span data-ttu-id="0f008-174">웹후크에 대한 자세한 내용은 [Azure 메트릭 경고에 대한 웹후크 구성](../../monitoring-and-diagnostics/insights-webhooks-alerts.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f008-174">For more information on webhooks, see [Configure a webhook on an Azure metric alert](../../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="0f008-175">전자 메일 또는 웹후크 알림을 구성하지 않으면 경고가 Azure Portal에서만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-175">If you do not configure email or webhook notifications, alerts will appear only in the Azure portal.</span></span>

![Azure Portal에서 '경고 규칙 추가' 블레이드 추가](./media/storage-monitor-storage-account/stg-alert-rules-01.png)

## <a name="add-metrics-charts-to-the-portal-dashboard"></a><span data-ttu-id="0f008-177">포털 대시보드에 메트릭 차트 추가</span><span class="sxs-lookup"><span data-stu-id="0f008-177">Add metrics charts to the portal dashboard</span></span>

<span data-ttu-id="0f008-178">저장소 계정에 대한 Azure Storage 메트릭 차트를 포털 대시보드에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-178">You can add Azure Storage metrics charts for any of your storage accounts to your portal dashboard.</span></span>

1. <span data-ttu-id="0f008-179">[Azure Portal](https://portal.azure.com)에서 대시보드를 보면서 **대시보드 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-179">Select click **Edit dashboard** while viewing your dashboard in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="0f008-180">**타일 갤러리**에서 **타일 찾기 기준** > **유형**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-180">In the **Tile Gallery**, select **Find tiles by** > **Type**.</span></span>
1. <span data-ttu-id="0f008-181">**유형** > **저장소 계정**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-181">Select **Type** > **Storage accounts**.</span></span>
1. <span data-ttu-id="0f008-182">**리소스**에서 대시보드에 추가하려는 메트릭의 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-182">In **Resources**, select the storage account whose metrics you wish to add to the dashboard.</span></span>
1. <span data-ttu-id="0f008-183">**범주** > **모니터링**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-183">Select **Categories** > **Monitoring**.</span></span>
1. <span data-ttu-id="0f008-184">표시하려는 메트릭에 대한 차트 타일을 대시보드로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-184">Drag-and-drop the chart tile onto your dashboard for the metric you'd like displayed.</span></span> <span data-ttu-id="0f008-185">대시보드에 표시하려는 모든 메트릭에 대해 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-185">Repeat for all metrics you'd like displayed on the dashboard.</span></span> <span data-ttu-id="0f008-186">다음 이미지에서는 한 예로 "Blob - 총 요청 수" 차트를 강조 표시했지만 모든 차트를 대시보드에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-186">In the following image, the "Blobs - Total requests" chart is highlighted as an example, but all the charts are available for placement on your dashboard.</span></span>

   ![Azure Portal의 타일 갤러리](./media/storage-monitor-storage-account/stg-customize-dashboard-01.png)
1. <span data-ttu-id="0f008-188">차트 추가를 완료했으면 대시보드 위쪽의 **사용자 지정 완료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-188">Select **Done customizing** near the top of the dashboard when you're done adding charts.</span></span>

<span data-ttu-id="0f008-189">대시보드에 차트를 추가하면 [메트릭 차트 사용자 지정](#how-to-customize-metrics-charts)에서 설명한 대로 차트를 추가로 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-189">Once you've added charts to your dashboard, you can further customize them as described in [Customize metrics charts](#how-to-customize-metrics-charts).</span></span>

## <a name="configure-logging"></a><span data-ttu-id="0f008-190">로깅 구성</span><span class="sxs-lookup"><span data-stu-id="0f008-190">Configure logging</span></span>

<span data-ttu-id="0f008-191">Azure Storage에서 Blob, 테이블 및 큐 서비스에 대한 읽기, 쓰기 및 삭제 요청에 대한 진단 로그를 저장하도록 지시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-191">You can instruct Azure Storage to save diagnostics logs for read, write, and delete requests for the blob, table, and queue services.</span></span> <span data-ttu-id="0f008-192">설정한 데이터 보존 정책도 이러한 로그에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-192">The data retention policy you set also applies to these logs.</span></span>

> [!NOTE]
> <span data-ttu-id="0f008-193">Azure 파일 저장소는 현재 저장소 분석 메트릭을 지원하지만 아직 로깅을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-193">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span></span>
>

1. <span data-ttu-id="0f008-194">[Azure Portal](https://portal.azure.com)에서 **저장소 계정**, 저장소 계정 이름을 차례로 선택하여 저장소 계정 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-194">In the [Azure portal](https://portal.azure.com), select **Storage accounts**, then the name of the storage account to open the storage account blade.</span></span>
1. <span data-ttu-id="0f008-195">메뉴 블레이드의 **모니터링** 섹션에서 **진단**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-195">Select **Diagnostics** in the **MONITORING** section of the menu blade.</span></span>

    ![Azure Portal에서 모니터링 아래의 진단 메뉴 항목](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)
    
1. <span data-ttu-id="0f008-197">**상태**가 **사용**(On)으로 설정되어 있는지 확인하고, 로깅을 사용하도록 설정하려는 **서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-197">Ensure **Status** is set to **On**, and select the **services** for which you'd like to enable logging.</span></span>

    ![Azure Portal에서 로깅 구성](./media/storage-monitor-storage-account/stg-enable-logging-01.png)
1. <span data-ttu-id="0f008-199">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-199">Click **Save**.</span></span>

<span data-ttu-id="0f008-200">진단 로그는 저장소 계정의 이름이 $logs인 Blob 컨테이너에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-200">The diagnostics logs are saved in a blob container named $logs in your storage account.</span></span> <span data-ttu-id="0f008-201">[Microsoft 저장소 탐색기](http://storageexplorer.com)와 같은 저장소 탐색기를 사용하거나 저장소 클라이언트 라이브러리 또는 PowerShell을 프로그래밍 방식으로 사용하여 로그 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-201">You can view the log data using a storage explorer like the [Microsoft Storage Explorer](http://storageexplorer.com), or programmatically using the storage client library or PowerShell.</span></span>

<span data-ttu-id="0f008-202">$logs 컨테이너 액세스에 대한 자세한 내용은 [저장소 로깅 사용 및 로그 데이터 액세스](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f008-202">For information about accessing the $logs container, see [Enabling Storage Logging and Accessing Log Data](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f008-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0f008-203">Next steps</span></span>

* <span data-ttu-id="0f008-204">저장소 분석의 [메트릭, 로깅 및 청구](../storage-analytics.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-204">Find more details about [metrics, logging, and billing](../storage-analytics.md) for Storage Analytics.</span></span>
* <span data-ttu-id="0f008-205">PowerShell 및 프로그래밍 방식으로 C#을 사용하여 [Azure Storage 메트릭 사용 및 메트릭 데이터 보기](../storage-enable-and-view-metrics.md)를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0f008-205">[Enable Azure Storage metrics and view metrics data](../storage-enable-and-view-metrics.md) by using PowerShell and programmatically with C#.</span></span>

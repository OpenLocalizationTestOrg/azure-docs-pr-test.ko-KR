---
title: "Log Analytics를 사용하여 Azure 활동 로그 보기 | Microsoft Docs"
description: "Azure 활동 로그 솔루션을 사용하여 모든 Azure 구독에서 Azure 활동 로그를 분석하고 검색할 수 있습니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: dbac4c73-0058-4191-a906-e59aca8e2ee0
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: 1ad56a54f094f3c314596b3a7c9fecd09647d065
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="view-azure-activity-logs"></a><span data-ttu-id="77931-103">Azure 활동 로그 보기</span><span class="sxs-lookup"><span data-stu-id="77931-103">View Azure activity logs</span></span>

![Azure 활동 로그 기호](./media/log-analytics-activity/activity-log-analytics.png)

<span data-ttu-id="77931-105">활동 로그 분석 솔루션은 모든 Azure 구독에서 [Azure 활동 로그](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)를 분석하고 검색할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="77931-105">The Activity Log Analytics solution helps you analyze and search the [Azure activity log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) across all your Azure subscriptions.</span></span> <span data-ttu-id="77931-106">Azure 활동 로그는 구독의 리소스에서 수행된 작업에 대한 자세한 정보를 제공하는 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="77931-106">The Azure Activity Log is a log that offers insights into the operations performed on resources in your subscriptions.</span></span> <span data-ttu-id="77931-107">활동 로그는 구독에 대한 이벤트를 보고하므로 이전에는 *감사 로그* 또는 *작업 로그*라고 했습니다.</span><span class="sxs-lookup"><span data-stu-id="77931-107">The Activity Log was previously known as *Audit Logs* or *Operational Logs* since it reports events for your subscriptions.</span></span>

<span data-ttu-id="77931-108">활동 로그를 통해 구독의 리소스에 대한 모든 쓰기 작업(PUT, POST, DELETE)에서 *무엇을*, *누가*, *언제* 썼는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77931-108">Using the Activity Log, you can determine the *what*, *who*, and *when* for any write operations (PUT, POST, DELETE) made for the resources in your subscription.</span></span> <span data-ttu-id="77931-109">작업과 기타 관련 속성의 상태도 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77931-109">You can also understand the status of the operations and other relevant properties.</span></span> <span data-ttu-id="77931-110">활동 로그에는 읽기(GET) 작업 또는 클래식 배포 모델을 사용하는 리소스에 대한 작업이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="77931-110">The Activity Log does not include read (GET) operations or operations for resources that use the Classic deployment model.</span></span>

<span data-ttu-id="77931-111">Azure 활동 로그를 Log Analytics에 연결하면 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77931-111">When you connect your Azure activity logs to Log Analytics, you can:</span></span>

- <span data-ttu-id="77931-112">미리 정의된 보기를 사용하여 활동 로그 분석</span><span class="sxs-lookup"><span data-stu-id="77931-112">Analyze the activity logs with pre-defined views</span></span>
- <span data-ttu-id="77931-113">여러 Azure 구독의 활동 로그를 분석하고 검색</span><span class="sxs-lookup"><span data-stu-id="77931-113">Analyze and search and activity logs from multiple Azure subscriptions</span></span>
- <span data-ttu-id="77931-114">활동 로그를 90일 이상 보관<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="77931-114">Keep activity logs for longer than 90 days<sup>1</sup></span></span>
- <span data-ttu-id="77931-115">활동 로그와 다른 Azure 플랫폼 및 응용 프로그램 데이터 간에 상관 관계 지정</span><span class="sxs-lookup"><span data-stu-id="77931-115">Correlate activity logs with other Azure platform and application data</span></span>
- <span data-ttu-id="77931-116">상태에 따라 집계된 운영 활동 보기</span><span class="sxs-lookup"><span data-stu-id="77931-116">See operational activities aggregated by status</span></span>
- <span data-ttu-id="77931-117">각 Azure 서비스에서 발생하는 활동의 추세 보기</span><span class="sxs-lookup"><span data-stu-id="77931-117">View trends of activities happening on each of your Azure services</span></span>
- <span data-ttu-id="77931-118">모든 Azure 리소스에 대한 권한 부여 변경 내용 보고</span><span class="sxs-lookup"><span data-stu-id="77931-118">Report on authorization changes on all your Azure resources</span></span>
- <span data-ttu-id="77931-119">리소스에 영향을 미치는 운영 중단 또는 서비스 상태 문제 식별</span><span class="sxs-lookup"><span data-stu-id="77931-119">Identify outage or service health issues impacting your resources</span></span>
- <span data-ttu-id="77931-120">로그 검색을 사용하여 사용자 활동, 자동 크기 조정 작업, 권한 부여 변경, 서비스 상태와 사용자 환경의 다른 로그 또는 메트릭 간에 상관 관계 지정</span><span class="sxs-lookup"><span data-stu-id="77931-120">Use Log Search to correlate user activities, auto-scale operations, authorization changes, and service health to other logs or metrics from your environment</span></span>

<span data-ttu-id="77931-121"><sup>1</sup>기본적으로 Log Analytics는 무료 계층에서도 Azure 활동 로그를 90일 동안 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="77931-121"><sup>1</sup>By default, Log Analytics keeps your Azure activity logs for 90 days, even if you are on the Free tier.</span></span> <span data-ttu-id="77931-122">작업 영역 보존 설정이 90일 미만으로 설정된 경우에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="77931-122">Or, if you have a workspace retention setting of less than 90 days.</span></span> <span data-ttu-id="77931-123">작업 영역 보존 설정이 90일보다 긴 경우 작업 영역의 보존 기간만큼 활동 로그가 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="77931-123">If your workspace has retention that is longer than 90 days, the activity logs are kept for the retention period of your workspace.</span></span>

<span data-ttu-id="77931-124">Log Analytics는 무료로 활동 로그를 수집하고 90일 동안 무료로 로그를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="77931-124">Log Analytics collects activity logs free of charge and stores the logs for 90 days free of charge.</span></span> <span data-ttu-id="77931-125">로그를 90일 이상 저장하는 경우 90일 넘게 저장된 데이터에 대해 데이터 보존 요금이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="77931-125">If you store logs for longer than 90 days, you will incur data retention charges for the data stored longer than 90 days.</span></span>

<span data-ttu-id="77931-126">무료 가격 책정 계층을 사용하는 경우 활동 로그가 일일 데이터 사용량에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="77931-126">When you're on the Free pricing tier, activity logs do not apply to your daily data consumption.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="77931-127">연결된 소스</span><span class="sxs-lookup"><span data-stu-id="77931-127">Connected sources</span></span>

<span data-ttu-id="77931-128">대부분의 다른 Log Analytics 솔루션과는 달리, 에이전트에서 활동 로그에 대한 데이터를 수집하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="77931-128">Unlike most other Log Analytics solutions, data isn't collected for activity logs by agents.</span></span> <span data-ttu-id="77931-129">솔루션에서 사용하는 모든 데이터는 Azure에서 직접 옵니다.</span><span class="sxs-lookup"><span data-stu-id="77931-129">All data used by the solution comes directly from Azure.</span></span>

| <span data-ttu-id="77931-130">연결된 소스</span><span class="sxs-lookup"><span data-stu-id="77931-130">Connected Source</span></span> | <span data-ttu-id="77931-131">지원됨</span><span class="sxs-lookup"><span data-stu-id="77931-131">Supported</span></span> | <span data-ttu-id="77931-132">설명</span><span class="sxs-lookup"><span data-stu-id="77931-132">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="77931-133">Windows 에이전트</span><span class="sxs-lookup"><span data-stu-id="77931-133">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="77931-134">아니요</span><span class="sxs-lookup"><span data-stu-id="77931-134">No</span></span> | <span data-ttu-id="77931-135">솔루션이 Windows 에이전트에서 정보를 수집하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="77931-135">The solution does not collect information from Windows agents.</span></span> |
| [<span data-ttu-id="77931-136">Linux 에이전트</span><span class="sxs-lookup"><span data-stu-id="77931-136">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="77931-137">아니요</span><span class="sxs-lookup"><span data-stu-id="77931-137">No</span></span> | <span data-ttu-id="77931-138">솔루션이 Linux 에이전트에서 정보를 수집하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="77931-138">The solution does not collect information from Linux agents.</span></span> |
| [<span data-ttu-id="77931-139">SCOM 관리 그룹</span><span class="sxs-lookup"><span data-stu-id="77931-139">SCOM management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="77931-140">아니요</span><span class="sxs-lookup"><span data-stu-id="77931-140">No</span></span> | <span data-ttu-id="77931-141">솔루션이 연결된 SCOM 관리 그룹의 에이전트에서 정보를 수집하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="77931-141">The solution does not collect information from agents in a connected SCOM management group.</span></span> |
| [<span data-ttu-id="77931-142">Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="77931-142">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="77931-143">아니요</span><span class="sxs-lookup"><span data-stu-id="77931-143">No</span></span> | <span data-ttu-id="77931-144">솔루션이 Azure 저장소에서 정보를 수집하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="77931-144">The solution does not collect information from Azure storage.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="77931-145">필수 조건</span><span class="sxs-lookup"><span data-stu-id="77931-145">Prerequisites</span></span>

- <span data-ttu-id="77931-146">Azure 활동 로그 정보에 액세스하려면 Azure 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77931-146">To access Azure activity log information, you must have an Azure subscription.</span></span>

## <a name="configuration"></a><span data-ttu-id="77931-147">구성</span><span class="sxs-lookup"><span data-stu-id="77931-147">Configuration</span></span>

<span data-ttu-id="77931-148">다음 단계를 수행하여 작업 영역에 대해 Activity Log Analytics 솔루션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="77931-148">Perform the following steps to configure the Activity Log Analytics solution for your workspaces.</span></span>

1. <span data-ttu-id="77931-149">[Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureActivityOMS?tab=Overview)에서 또는 [솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)에서 설명한 프로세스를 사용하여 Activity Log Analytics 솔루션을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="77931-149">Enable the Activity Log Analytics solution from the [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureActivityOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="77931-150">Log Analytics 작업 영역으로 이동하도록 활동 로그를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="77931-150">Configure activity logs to go to your Log Analytics workspace.</span></span>
    1. <span data-ttu-id="77931-151">Azure Portal에서 작업 영역을 선택한 다음 **Azure 활동 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77931-151">In the Azure portal, select your workspace and then click **Azure Activity log**.</span></span>
    2. <span data-ttu-id="77931-152">각 구독에 대해 구독 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77931-152">For each subscription, click the subscription name.</span></span>  
        ![구독 추가](./media/log-analytics-activity/add-subscription.png)
    3. <span data-ttu-id="77931-154">*SubscriptionName* 블레이드에서 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77931-154">In the *SubscriptionName* blade, click **Connect**.</span></span>  
        <span data-ttu-id="77931-155">![구독 연결](./media/log-analytics-activity/subscription-connect.png)</span><span class="sxs-lookup"><span data-stu-id="77931-155">![connect subscription](./media/log-analytics-activity/subscription-connect.png)</span></span>

<span data-ttu-id="77931-156">OMS 포털을 사용하여 솔루션을 추가하면 다음 타일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="77931-156">If you add the solution using the OMS portal, you'll see the following tile.</span></span> <span data-ttu-id="77931-157">Azure Portal에 로그인하여 Azure 구독을 작업 영역에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="77931-157">Sign in to the Azure portal to connect an Azure subscription to your workspace.</span></span>  
![평가 수행](./media/log-analytics-activity/tile-performing-assessment.png)

## <a name="using-the-solution"></a><span data-ttu-id="77931-159">솔루션 사용</span><span class="sxs-lookup"><span data-stu-id="77931-159">Using the solution</span></span>

<span data-ttu-id="77931-160">Activity Log Analytics 솔루션을 작업 영역에 추가하면 개요 대시보드에 **Azure 활동 로그** 타일이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="77931-160">When you add the Activity Log Analytics solution to your workspace, the **Azure Activity Logs** tile is added to your Overview dashboard.</span></span> <span data-ttu-id="77931-161">이 타일에는 솔루션에서 액세스할 수 있는 Azure 구독의 Azure 활동 레코드 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="77931-161">This tile displays a count of the number of Azure activity records for the Azure subscriptions that the solution has access to.</span></span>

![Azure 활동 로그 타일](./media/log-analytics-activity/azure-activity-logs-tile.png)

### <a name="view-azure-activity-logs"></a><span data-ttu-id="77931-163">Azure 활동 로그 보기</span><span class="sxs-lookup"><span data-stu-id="77931-163">View Azure Activity logs</span></span>

<span data-ttu-id="77931-164">**Azure 활동 로그** 타일을 클릭하여 **Azure 활동 로그** 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="77931-164">Click the **Azure Activity Logs** tile to open the **Azure Activity Logs** dashboard.</span></span> <span data-ttu-id="77931-165">대시보드에는 다음 테이블의 블레이드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77931-165">The dashboard includes the blades in the following table.</span></span> <span data-ttu-id="77931-166">각 블레이드에는 지정된 범위 및 시간 범위에 대한 해당 블레이드의 기준과 일치하는 항목이 최대 10개까지 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="77931-166">Each blade lists up to 10 items matching that blade's criteria for the specified scope and time range.</span></span> <span data-ttu-id="77931-167">블레이드 맨 아래에서 **모두 보기**를 클릭하거나 블레이드 헤더를 클릭하여 모든 레코드를 반환하는 로그 검색을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77931-167">You can run a log search that returns all records by clicking **See all** at the bottom of the blade or by clicking the blade header.</span></span>

<span data-ttu-id="77931-168">활동 로그 데이터는 솔루션으로 이동하도록 활동 로그를 구성한 *후*에만 표시되므로 그 전에는 데이터를 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="77931-168">Activity log data only appears *after* you've configured your activity logs to go to the solution, so you can't view data before then.</span></span>

| <span data-ttu-id="77931-169">블레이드</span><span class="sxs-lookup"><span data-stu-id="77931-169">Blade</span></span> | <span data-ttu-id="77931-170">설명</span><span class="sxs-lookup"><span data-stu-id="77931-170">Description</span></span> |
| --- | --- |
| <span data-ttu-id="77931-171">Azure 활동 로그 항목</span><span class="sxs-lookup"><span data-stu-id="77931-171">Azure Activity Log Entries</span></span> | <span data-ttu-id="77931-172">사용자가 선택한 날짜 범위에 해당하는 상위 Azure 활동 로그 항목 레코드의 가로 막대형 차트를 표시하고 상위 10개 활동 호출자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="77931-172">Shows a bar chart of the top Azure activity log entry record totals for the date range that you have selected and shows a list of the top 10 activity callers.</span></span> <span data-ttu-id="77931-173">가로 막대형 차트에 대 한 로그 검색을 실행 하려면 클릭 <code>Type=AzureActivity</code>합니다.</span><span class="sxs-lookup"><span data-stu-id="77931-173">Click the bar chart to run a log search for <code>Type=AzureActivity</code>.</span></span> <span data-ttu-id="77931-174">호출자 항목을 클릭하면 해당 항목에 대한 모든 활동 로그 항목을 반환하는 로그 검색이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="77931-174">Click a caller item to run a log search returning all activity log entries for that item.</span></span> |
| <span data-ttu-id="77931-175">상태별 활동 로그</span><span class="sxs-lookup"><span data-stu-id="77931-175">Activity Logs by Status</span></span> | <span data-ttu-id="77931-176">사용자가 선택한 날짜 범위에 해당하는 Azure 활동 로그 상태의 도넛형 차트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="77931-176">Shows a doughnut chart for Azure activity log status for the date range that you have selected.</span></span> <span data-ttu-id="77931-177">상위 10개 상태 레코드 목록도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="77931-177">Also shows a list a list of the top ten status records.</span></span> <span data-ttu-id="77931-178">에 대 한 로그 검색을 실행 하려면 차트를 클릭 <code>Type=AzureActivity &#124; measure count() by ActivityStatus</code>합니다.</span><span class="sxs-lookup"><span data-stu-id="77931-178">Click the chart to run a log search for <code>Type=AzureActivity &#124; measure count() by ActivityStatus</code>.</span></span> <span data-ttu-id="77931-179">상태 항목을 클릭하면 해당 상태 레코드에 대한 모든 활동 로그 항목을 반환하는 로그 검색이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="77931-179">Click a status item to run a log search returning all activity log entries for that status record.</span></span> |
| <span data-ttu-id="77931-180">리소스별 활동 로그</span><span class="sxs-lookup"><span data-stu-id="77931-180">Activity Logs by Resource</span></span> | <span data-ttu-id="77931-181">활동 로그와 함께 총 리소스 수를 표시하고 각 리소스에 대한 레코드 수와 함께 상위 10개 리소스를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="77931-181">Shows the total number of resources with activity logs and lists the top ten resources with record counts for each resource.</span></span> <span data-ttu-id="77931-182">에 대 한 로그 검색을 실행 하려면 전체 영역의 클릭 <code>Type=AzureActivity &#124; measure count() by Resource</code>, 솔루션에 사용할 수 있는 모든 Azure 리소스를 보여 주는 합니다.</span><span class="sxs-lookup"><span data-stu-id="77931-182">Click the total area to run a log search for <code>Type=AzureActivity &#124; measure count() by Resource</code>, which shows all Azure resources available to the solution.</span></span> <span data-ttu-id="77931-183">리소스를 클릭하면 해당 리소스에 대한 모든 활동 레코드를 반환하는 로그 검색이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="77931-183">Click a resource to run a log search returning all activity records for that resource.</span></span> |
| <span data-ttu-id="77931-184">리소스 공급자별 활동 로그</span><span class="sxs-lookup"><span data-stu-id="77931-184">Activity Logs by Resource Provider</span></span> | <span data-ttu-id="77931-185">활동 로그를 생성하는 총 리소스 공급자 수를 표시하고 상위 10개 리소스 공급자를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="77931-185">Shows the total number of resource providers that produce activity logs and lists the top ten.</span></span> <span data-ttu-id="77931-186">에 대 한 로그 검색을 실행 하려면 전체 영역의 클릭 <code>Type=AzureActivity &#124; measure count() by ResourceProvider</code>, 모든 Azure 리소스 공급자를 보여 주는 합니다.</span><span class="sxs-lookup"><span data-stu-id="77931-186">Click the total area to run a log search for <code>Type=AzureActivity &#124; measure count() by ResourceProvider</code>, which shows all Azure resource providers.</span></span> <span data-ttu-id="77931-187">리소스 공급자를 클릭하면 해당 공급자에 대한 모든 활동 레코드를 반환하는 로그 검색이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="77931-187">Click a resource provider to run a log search returning all activity records for the provider.</span></span> |

![Azure 활동 로그 대시보드](./media/log-analytics-activity/activity-log-dash.png)

## <a name="next-steps"></a><span data-ttu-id="77931-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="77931-189">Next steps</span></span>

- <span data-ttu-id="77931-190">특정 활동이 발생하면 [경고](log-analytics-alerts-creating.md)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77931-190">Create an [alert](log-analytics-alerts-creating.md) when a specific activity happens.</span></span>
- <span data-ttu-id="77931-191">[로그 검색](log-analytics-log-searches.md)을 사용하여 활동 로그의 자세한 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="77931-191">Use [Log Search](log-analytics-log-searches.md) to view detailed information from your activity logs.</span></span>

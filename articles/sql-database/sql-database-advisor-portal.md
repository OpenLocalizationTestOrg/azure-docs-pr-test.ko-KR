---
title: "성능 권장 사항 적용 - Azure SQL Database | Microsoft Docs"
description: "Azure Portal을 사용하여 Azure SQL Database의 성능을 최적화할 수 있는 성능 권장 사항을 찾거나 워크로드에서 식별된 일부 문제를 수정할 수 있습니다."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 018afaa8b08bd001e55693390e80c8e2c4f33a30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="find-and-apply-performance-recommendations"></a><span data-ttu-id="633d7-103">성능 권장 사항 찾기 및 적용</span><span class="sxs-lookup"><span data-stu-id="633d7-103">Find and apply performance recommendations</span></span>

<span data-ttu-id="633d7-104">Azure Portal을 사용하여 Azure SQL Database의 성능을 최적화할 수 있는 성능 권장 사항을 찾거나 워크로드에서 식별된 일부 문제를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-104">You can use the Azure portal to find performance recommendations that can optimize performance of your Azure SQL Database or to correct some issue identified in your workload.</span></span> <span data-ttu-id="633d7-105">Azure Portal에서 **성능 권장 사항** 페이지를 사용하면 잠재적인 영향에 따라 가지 상위 권장 사항을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-105">**Performance recommendation** page in Azure portal enables you to find the top recommendations based on their potential impact.</span></span> 

## <a name="viewing-recommendations"></a><span data-ttu-id="633d7-106">권장 사항 보기</span><span class="sxs-lookup"><span data-stu-id="633d7-106">Viewing recommendations</span></span>

<span data-ttu-id="633d7-107">성능 권장 사항을 보고 적용하려면 Azure에서 올바른 [역할 기반 액세스 제어](../active-directory/role-based-access-control-what-is.md) 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-107">To view and apply performance recommendations, you need the correct [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions in Azure.</span></span> <span data-ttu-id="633d7-108">권장 사항을 보려면 **읽기 권한자**, **SQL DB 참가자** 권한이 필요하고, 모든 동작(인덱스 만들기 또는 삭제, 인덱스 만들기 취소)을 실행하려면 **소유자**, **SQL DB 참가자** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-108">**Reader**, **SQL DB Contributor** permissions are required to view recommendations, and **Owner**, **SQL DB Contributor** permissions are required to execute any actions; create or drop indexes and cancel index creation.</span></span>

<span data-ttu-id="633d7-109">다음 단계를 사용하여 Azure Portal에서 성능 권장 사항을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-109">Use the following steps to find performance recommendations on Azure portal:</span></span>

1. <span data-ttu-id="633d7-110">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-110">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="633d7-111">**추가 서비스** > **SQL Databases**로 이동하고 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-111">Go to **More services** > **SQL databases**, and select your database.</span></span>
3. <span data-ttu-id="633d7-112">**성능 권장 사항**으로 이동하여 선택된 데이터베이스의 사용 가능한 권장 사항을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-112">Navigate to **Performance recommendation** to view available recommendations for the selected database.</span></span>

<span data-ttu-id="633d7-113">성능 권장 사항은 다음 그림에서 보여주는 표와 비슷하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-113">Performance recommendations are shonw in the table similar to the one shown on the following figure:</span></span>

![추천](./media/sql-database-advisor-portal/recommendations.png)

<span data-ttu-id="633d7-115">권장 사항은 성능의 잠재적 영향 순으로 다음과 같은 카테고리에 정렬됩니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-115">Recommendations are sorted by their potential impact on performance into the following categories:</span></span>

| <span data-ttu-id="633d7-116">영향</span><span class="sxs-lookup"><span data-stu-id="633d7-116">Impact</span></span> | <span data-ttu-id="633d7-117">설명</span><span class="sxs-lookup"><span data-stu-id="633d7-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="633d7-118">높음</span><span class="sxs-lookup"><span data-stu-id="633d7-118">High</span></span> |<span data-ttu-id="633d7-119">높은 영향 권장사항은 가장 중요한 성능 영향을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-119">High impact recommendations should provide the most significant performance impact.</span></span> |
| <span data-ttu-id="633d7-120">중간</span><span class="sxs-lookup"><span data-stu-id="633d7-120">Medium</span></span> |<span data-ttu-id="633d7-121">중간 영향 권장 사항은 성능을 향상시키지만, 크게 향상시키지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-121">Medium impact recommendations should improve performance, but not substantially.</span></span> |
| <span data-ttu-id="633d7-122">낮음</span><span class="sxs-lookup"><span data-stu-id="633d7-122">Low</span></span> |<span data-ttu-id="633d7-123">낮은 영향 권장 사항은 없는 것보다 나은 성능을 제공하지만, 향상된 기능이 눈에 띄지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-123">Low impact recommendations should provide better performance than without, but improvements might not be significant.</span></span> |


> [!NOTE]
> <span data-ttu-id="633d7-124">Azure SQL Database는 일부 권장 사항을 파악하기 위해 적어도 하루 동안 작업을 모니터링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-124">Azure SQL Database needs to monitor activities at least for a day in order to identify some recommendations.</span></span> <span data-ttu-id="633d7-125">Azure SQL Database는 임의적이며 폭발적으로 발생하는 작업보다 일관성 있는 쿼리 패턴을 더욱 쉽게 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-125">The Azure SQL Database can more easily optimize for consistent query patterns than it can for random spotty bursts of activity.</span></span> <span data-ttu-id="633d7-126">현재 권장 사항을 사용할 수 없는 경우 **성능 권장** 페이지에서 원인에 대해 설명하는 메시지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-126">If recommendations are not corrently available, the **Performance recommendation** page provides a message explaining why.</span></span>
> 

<span data-ttu-id="633d7-127">또한 과거 작업의 상태도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-127">You can also view the status of the historical operations.</span></span> <span data-ttu-id="633d7-128">세부 정보를 보려면 권장 사항 또는 상태를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-128">Select a recommendation or status to see  more details.</span></span>

<span data-ttu-id="633d7-129">Azure Portal에서 "인덱스 만들기" 권장 사항의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-129">Here is an example of "Create index" recommendation in the Azure portal.</span></span>

![인덱스 만들기](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a><span data-ttu-id="633d7-131">권장 사항 적용</span><span class="sxs-lookup"><span data-stu-id="633d7-131">Applying recommendations</span></span>
<span data-ttu-id="633d7-132">Azure SQL Database는 다음 세 가지 옵션을 사용하여 권장 사항을 사용하도록 설정하는 방법을 완전히 제어할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-132">Azure SQL Database gives you full control over how recommendations are enabled using any of the following three options:</span></span> 

* <span data-ttu-id="633d7-133">개별 권장 구성을 한 번에 하나씩 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-133">Apply individual recommendations one at a time.</span></span>
* <span data-ttu-id="633d7-134">자동 튜닝을 사용하도록 설정하여 권장 사항을 자동으로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-134">Enable the Automatic tuning to automatically apply recommendations.</span></span>
* <span data-ttu-id="633d7-135">권장 사항을 수동으로 구현하려면 데이터베이스에 대해 권장 T-SQL 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-135">To implement a recommendation manually, run the recommended T-SQL script against your database.</span></span>

<span data-ttu-id="633d7-136">권장 사항을 선택하여 세부 정보를 본 다음 **스크립트 보기** 를 클릭하여 권장 사항이 어떻게 만들어지는지에 대해 정확한 세부 사항을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-136">Select any recommendation to view its details and then click **View script** to review the exact details of how the recommendation is created.</span></span>

<span data-ttu-id="633d7-137">데이터베이스는 성능 권장 사항을 사용하여 권장 사항이 적용되는 동안 온라인 상태로 유지됩니다. 자동 튜닝은 오프라인인 상태인 데이터베이스를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-137">The database remains online while the recommendation is applied -- using performance recommendation or automatic tuning never takes a database offline.</span></span>

### <a name="apply-an-individual-recommendation"></a><span data-ttu-id="633d7-138">개별 권장 구성 적용</span><span class="sxs-lookup"><span data-stu-id="633d7-138">Apply an individual recommendation</span></span>
<span data-ttu-id="633d7-139">권장 구성을 한 번에 하나씩 검토하고 수락할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-139">You can review and accept recommendations one at a time.</span></span>

1. <span data-ttu-id="633d7-140">**권장 사항** 블레이드에서 권장 사항을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-140">On the **Recommendations** blade, select a recommendation.</span></span>
2. <span data-ttu-id="633d7-141">**세부 정보** 블레이드에서 **적용** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-141">On the **Details** blade click **Apply** button.</span></span>
   
    ![권장 구성 적용](./media/sql-database-advisor-portal/apply.png)

<span data-ttu-id="633d7-143">선택한 권장 사항은 데이터베이스에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-143">Selected recommendation will be applied on the database.</span></span>

### <a name="removing-recommendations-from-the-list"></a><span data-ttu-id="633d7-144">목록에서 권장 사항 제거</span><span class="sxs-lookup"><span data-stu-id="633d7-144">Removing recommendations from the list</span></span>
<span data-ttu-id="633d7-145">권장 사항 목록에 목록에서 제거할 항목이 포함된 경우 권장 사항을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-145">If your list of recommendations contains items that you want to remove from the list, you can discard the recommendation:</span></span>

1. <span data-ttu-id="633d7-146">**권장 사항** 목록에서 권장 사항을 선택하여 세부 정보를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-146">Select a recommendation in the list of **Recommendations** to open the details.</span></span>
2. <span data-ttu-id="633d7-147">**세부 정보** 블레이드에서 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-147">Click **Discard** on the **Details** blade.</span></span>

<span data-ttu-id="633d7-148">원하는 경우 삭제된 항목을 **권장 사항** 목록에 다시 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-148">If desired, you can add discarded items back to the **Recommendations** list:</span></span>

1. <span data-ttu-id="633d7-149">**권장 사항** 블레이드에서 **삭제된 항목 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-149">On the **Recommendations** blade click **View discarded**.</span></span>
2. <span data-ttu-id="633d7-150">자세히 보기 목록에서 삭제된 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-150">Select a discarded item from the list to view its details.</span></span>
3. <span data-ttu-id="633d7-151">필요에 따라 **권장 사항**의 기본 목록에 인덱스를 다시 추가하려면 **삭제 취소**를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="633d7-151">Optionally, click **Undo Discard** to add the index back to the main list of **Recommendations**.</span></span>


### <a name="enable-automatic-tuning"></a><span data-ttu-id="633d7-152">자동 조정 사용</span><span class="sxs-lookup"><span data-stu-id="633d7-152">Enable automatic tuning</span></span>
<span data-ttu-id="633d7-153">Azure SQL Database가 권장 사항을 자동으로 구현하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-153">You can set the Azure SQL Database to implement recommendations automatically.</span></span> <span data-ttu-id="633d7-154">권장 구성은 사용할 수 있을 때 자동으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-154">As recommendations become available they will automatically be applied.</span></span> <span data-ttu-id="633d7-155">서비스에서 관리되는 권장 사항처럼 권장 사항이 성능에 좋지 않은 영향을 주는 경우 되돌려집니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-155">As with all recommendations managed by the service if the performance impact is negative the recommendation will be reverted.</span></span>

1. <span data-ttu-id="633d7-156">**권장 사항** 블레이드에서 **자동화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-156">On the **Recommendations** blade, click **Automate**:</span></span>
   
    ![관리자 설정](./media/sql-database-advisor-portal/settings.png)
2. <span data-ttu-id="633d7-158">자동화할 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-158">Select actions to automate:</span></span>
   
    ![권장된 인덱스](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-the-recommended-t-sql-script"></a><span data-ttu-id="633d7-160">권장 T-SQL 스크립트를 수동으로 실행</span><span class="sxs-lookup"><span data-stu-id="633d7-160">Manually run the recommended T-SQL script</span></span>
<span data-ttu-id="633d7-161">권장 사항을 선택한 다음 **스크립트 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-161">Select any recommendation and then click **View script**.</span></span> <span data-ttu-id="633d7-162">권장 구성을 수동으로 적용하도록 데이터베이스에 대해 이 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-162">Run this script against your database to manually apply the recommendation.</span></span>

<span data-ttu-id="633d7-163">*수동으로 실행된 인덱스는 성능에 미치는 서비스 영향에 대해 모니터링하고 유효성 검사를 실시하지 않으므로* 필요한 경우 인덱스 생성 후 인덱스를 성능을 향상시키거나 조절 또는 삭제하기 위해 모니터링하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-163">*Indexes that are manually executed are not monitored and validated for performance impact by the service* so it is suggested that you monitor these indexes after creation to verify they provide performance gains and adjust or delete them if necessary.</span></span> <span data-ttu-id="633d7-164">인덱스 만들기에 대한 세부 정보는 [CREATE INDEX (TRANSACT-SQL)](https://msdn.microsoft.com/library/ms188783.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="633d7-164">For details about creating indexes, see [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span></span>

### <a name="canceling-recommendations"></a><span data-ttu-id="633d7-165">권장 사항 취소</span><span class="sxs-lookup"><span data-stu-id="633d7-165">Canceling recommendations</span></span>
<span data-ttu-id="633d7-166">**보류 중**, **확인 중** 또는 **성공** 상태에 있는 권장 사항은 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-166">Recommendations that are in a **Pending**, **Verifying**, or **Success** status can be canceled.</span></span> <span data-ttu-id="633d7-167">**실행 중** 상태의 권장 사항은 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-167">Recommendations with a status of **Executing** cannot be canceled.</span></span>

1. <span data-ttu-id="633d7-168">**튜닝 기록** 영역에서 권장 사항을 선택하면 **권장 사항 세부 정보** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-168">Select a recommendation in the **Tuning History** area to open the **recommendations details** blade.</span></span>
2. <span data-ttu-id="633d7-169">**취소** 를 클릭하여 권장 사항을 적용하는 과정을 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-169">Click **Cancel** to abort the process of applying the recommendation.</span></span>

## <a name="monitoring-operations"></a><span data-ttu-id="633d7-170">모니터링 작업</span><span class="sxs-lookup"><span data-stu-id="633d7-170">Monitoring operations</span></span>
<span data-ttu-id="633d7-171">권장 구성을 적용해도 즉각적으로 일어나지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-171">Applying a recommendation might not happen instantaneously.</span></span> <span data-ttu-id="633d7-172">포털에서는 권장 사항의 상태에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-172">The portal provides details regarding the status of recommendation.</span></span> <span data-ttu-id="633d7-173">다음은 인덱스 안에 나타날 수 있는 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-173">The following are possible states that an index can be in:</span></span>

| <span data-ttu-id="633d7-174">상태</span><span class="sxs-lookup"><span data-stu-id="633d7-174">Status</span></span> | <span data-ttu-id="633d7-175">설명</span><span class="sxs-lookup"><span data-stu-id="633d7-175">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="633d7-176">Pending</span><span class="sxs-lookup"><span data-stu-id="633d7-176">Pending</span></span> |<span data-ttu-id="633d7-177">권장 사항 적용 명령을 수신했고 실행이 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-177">Apply recommendation command has been received and is scheduled for execution.</span></span> |
| <span data-ttu-id="633d7-178">실행 중</span><span class="sxs-lookup"><span data-stu-id="633d7-178">Executing</span></span> |<span data-ttu-id="633d7-179">권장 사항을 적용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-179">The recommendation is being applied.</span></span> |
| <span data-ttu-id="633d7-180">확인 중</span><span class="sxs-lookup"><span data-stu-id="633d7-180">Verifying</span></span> |<span data-ttu-id="633d7-181">권장 사항이 성공적으로 적용되면 서비스가 성능을 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-181">Recommendation was successfully applied and the service is measuring the benefits.</span></span> |
| <span data-ttu-id="633d7-182">성공</span><span class="sxs-lookup"><span data-stu-id="633d7-182">Success</span></span> |<span data-ttu-id="633d7-183">권장 사항이 성공적으로 적용되면 성능을 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-183">Recommendation was successfully applied and benefits have been measured.</span></span> |
| <span data-ttu-id="633d7-184">오류</span><span class="sxs-lookup"><span data-stu-id="633d7-184">Error</span></span> |<span data-ttu-id="633d7-185">권장 사항을 적용하는 과정 중에 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-185">An error occurred during the process of applying the recommendation.</span></span> <span data-ttu-id="633d7-186">일시적인 문제일 수도 있고, 테이블의 스키마변경 문제일 수도 있고, 스크립트가 더 이상 유효하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-186">This can be a transient issue, or possibly a schema change to the table and the script is no longer valid.</span></span> |
| <span data-ttu-id="633d7-187">되돌리기</span><span class="sxs-lookup"><span data-stu-id="633d7-187">Reverting</span></span> |<span data-ttu-id="633d7-188">권장 사항이 적용되었지만 효율적이지 않은 것으로 간주되어 자동으로 되돌리고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-188">The recommendation was applied, but has been deemed non-performant and is being automatically reverted.</span></span> |
| <span data-ttu-id="633d7-189">되돌림</span><span class="sxs-lookup"><span data-stu-id="633d7-189">Reverted</span></span> |<span data-ttu-id="633d7-190">권장 사항을 되돌렸습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-190">The recommendation was reverted.</span></span> |

<span data-ttu-id="633d7-191">세부 정보를 보려면 목록에서 In Process 권장 구성을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-191">Click an in-process recommendation from the list to see more details:</span></span>

![권장된 인덱스](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a><span data-ttu-id="633d7-193">권장 사항 되돌리기</span><span class="sxs-lookup"><span data-stu-id="633d7-193">Reverting a recommendation</span></span>
<span data-ttu-id="633d7-194">성능 권장 사항을 사용하여 권장 사항을 적용하는 경우(즉, 수동으로 T-SQL 스크립트를 실행하지 않음) 해당 권장 사항이 성능에 좋지 않은 영향을 준다는 점을 확인하면 자동으로 이를 되돌립니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-194">If you used the performance recommendations to apply the recommendation (meaning you did not manually run the T-SQL script) it will automatically revert it if it finds the performance impact to be negative.</span></span> <span data-ttu-id="633d7-195">어떤 이유로든 단순히 권장 사항을 되돌리려면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-195">If for any reason you simply want to revert a recommendation you can do the following:</span></span>

1. <span data-ttu-id="633d7-196">**튜닝 기록** 영역에서 성공적으로 적용된 권장 사항을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-196">Select a successfully applied recommendation in the **Tuning history** area.</span></span>
2. <span data-ttu-id="633d7-197">**권장 사항 세부 정보** 블레이드에서 **되돌리기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-197">Click **Revert** on the **recommendation details** blade.</span></span>

![권장된 인덱스](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a><span data-ttu-id="633d7-199">인덱스 권장 구성의 성능 영향 모니터링</span><span class="sxs-lookup"><span data-stu-id="633d7-199">Monitoring performance impact of index recommendations</span></span>
<span data-ttu-id="633d7-200">권장 사항이 성공적으로 구현된 후(현재는 인덱스 작업 및 쿼리 매개 변수화 권장 사항만) 인덱스 세부 정보 블레이드의 **쿼리 인사이트** 를 클릭하여 [Query Performance Insights](sql-database-query-performance.md) 를 열고 상위 쿼리의 성능 영향을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-200">After recommendations are successfully implemented (currently, index operations and parameterize queries recommendations only) you can click **Query Insights** on the recommendation details blade to open [Query Performance Insights](sql-database-query-performance.md) and see the performance impact of your top queries.</span></span>

![성능에 미치는 영향을 모니터링합니다.](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a><span data-ttu-id="633d7-202">요약</span><span class="sxs-lookup"><span data-stu-id="633d7-202">Summary</span></span>
<span data-ttu-id="633d7-203">Azure SQL Database는 SQL Database 성능을 향상하기 위한 권장 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-203">Azure SQL Database provides recommendations for improving SQL database performance.</span></span> <span data-ttu-id="633d7-204">T-SQL 스크립트를 개별적인 완전 자동으로 제공하여 데이터베이스를 최적화하고 궁극적으로 쿼리 성능을 향상시키도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-204">By providing T-SQL scripts, as well as individual and fully-automatic, you get a helpful assistance in optimizing your database and ultimately improving query performance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="633d7-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="633d7-205">Next steps</span></span>
<span data-ttu-id="633d7-206">권장 사항을 모니터링하고 개선된 성능을 계속 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-206">Monitor your recommendations and continue to apply them to refine performance.</span></span> <span data-ttu-id="633d7-207">데이터베이스 워크로드는 동적 이며 지속적으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-207">Database workloads are dynamic and change continuously.</span></span> <span data-ttu-id="633d7-208">Azure SQL Database는 데이터베이스 성능을 잠재적으로 향상시킬 수 있는 권장 사항을 계속 제공하고 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-208">Azure SQL Database will continue to monitor and provide recommendations that can potentially improve your database's performance.</span></span> 

* <span data-ttu-id="633d7-209">[자동 튜닝](sql-database-automatic-tuning.md)을 참조하여 Azure SQL Database에서 자동 튜닝에 대한 자세한 내용을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="633d7-209">See [Automatic tuning](sql-database-automatic-tuning.md) to learn more about the automatic tuning in Azure SQL Database.</span></span>
* <span data-ttu-id="633d7-210">Azure SQL Database 성능 권장 사항에 대한 개요는 [성능 권장 사항](sql-database-advisor.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="633d7-210">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="633d7-211">상위 쿼리의 성능에 미치는 영향을 알아보려면 [Query Performance Insights](sql-database-query-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="633d7-211">See [Query Performance Insights](sql-database-query-performance.md) to learn about viewing the performance impact of your top queries.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="633d7-212">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="633d7-212">Additional resources</span></span>
* [<span data-ttu-id="633d7-213">쿼리 저장소</span><span class="sxs-lookup"><span data-stu-id="633d7-213">Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx)
* [<span data-ttu-id="633d7-214">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="633d7-214">CREATE INDEX</span></span>](https://msdn.microsoft.com/library/ms188783.aspx)
* [<span data-ttu-id="633d7-215">역할 기반 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="633d7-215">Role-based access control</span></span>](../active-directory/role-based-access-control-what-is.md)


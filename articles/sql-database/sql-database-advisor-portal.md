---
title: "aaaApply 성능 권장 사항-Azure SQL 데이터베이스 | Microsoft Docs"
description: "Toocorrect 또는 Azure SQL 데이터베이스의 성능을 최적화할 수 있는 hello Azure 포털 toofind 성능 권장 사항에서는 작업에서 식별 하는 몇 가지 문제입니다."
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
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a><span data-ttu-id="bb58f-103">성능 권장 사항 찾기 및 적용</span><span class="sxs-lookup"><span data-stu-id="bb58f-103">Find and apply performance recommendations</span></span>

<span data-ttu-id="bb58f-104">Toocorrect 또는 Azure SQL 데이터베이스의 성능을 최적화할 수 있는 hello Azure 포털 toofind 성능 권장 사항에서는 작업에서 식별 하는 몇 가지 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-104">You can use hello Azure portal toofind performance recommendations that can optimize performance of your Azure SQL Database or toocorrect some issue identified in your workload.</span></span> <span data-ttu-id="bb58f-105">**성능 권장 사항** Azure 포털에서 페이지에서는 잠재적인 영향에 따라 toofind hello 최상위 권장 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-105">**Performance recommendation** page in Azure portal enables you toofind hello top recommendations based on their potential impact.</span></span> 

## <a name="viewing-recommendations"></a><span data-ttu-id="bb58f-106">권장 사항 보기</span><span class="sxs-lookup"><span data-stu-id="bb58f-106">Viewing recommendations</span></span>

<span data-ttu-id="bb58f-107">tooview 올바른 hello 필요 하면 성능 권장 사항 적용 [역할 기반 액세스 제어](../active-directory/role-based-access-control-what-is.md) Azure에서 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="bb58f-107">tooview and apply performance recommendations, you need hello correct [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions in Azure.</span></span> <span data-ttu-id="bb58f-108">**판독기**, **SQL DB 참가자** 권한은 필요한 tooview 권장 사항 및 **소유자**, **SQL DB 참가자** 권한은 필요 tooexecute 행위; 만들기 또는 인덱스를 삭제 하 고 인덱스 생성을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-108">**Reader**, **SQL DB Contributor** permissions are required tooview recommendations, and **Owner**, **SQL DB Contributor** permissions are required tooexecute any actions; create or drop indexes and cancel index creation.</span></span>

<span data-ttu-id="bb58f-109">Hello에 나오는 단계 toofind 성능 권장 사항에 따라 Azure 포털을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-109">Use hello following steps toofind performance recommendations on Azure portal:</span></span>

1. <span data-ttu-id="bb58f-110">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-110">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="bb58f-111">너무 이동**더 많은 서비스** > **SQL 데이터베이스**, 해당 데이터베이스를 선택 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-111">Go too**More services** > **SQL databases**, and select your database.</span></span>
3. <span data-ttu-id="bb58f-112">너무 이동**성능 권장 사항** tooview hello 선택한 데이터베이스에 사용할 수 있는 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-112">Navigate too**Performance recommendation** tooview available recommendations for hello selected database.</span></span>

<span data-ttu-id="bb58f-113">성능 권장 사항이 hello 다음 그림에 표시 된 하나 hello 테이블 비슷한 toohello shonw:</span><span class="sxs-lookup"><span data-stu-id="bb58f-113">Performance recommendations are shonw in hello table similar toohello one shown on hello following figure:</span></span>

![권장 사항](./media/sql-database-advisor-portal/recommendations.png)

<span data-ttu-id="bb58f-115">권장 사항 hello 다음 범주에는 성능에 대 한 잠재적인 영향에 따라 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-115">Recommendations are sorted by their potential impact on performance into hello following categories:</span></span>

| <span data-ttu-id="bb58f-116">영향</span><span class="sxs-lookup"><span data-stu-id="bb58f-116">Impact</span></span> | <span data-ttu-id="bb58f-117">설명</span><span class="sxs-lookup"><span data-stu-id="bb58f-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="bb58f-118">높음</span><span class="sxs-lookup"><span data-stu-id="bb58f-118">High</span></span> |<span data-ttu-id="bb58f-119">높은 영향 권장 사항을 hello 가장 중요 한 성능에 영향을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-119">High impact recommendations should provide hello most significant performance impact.</span></span> |
| <span data-ttu-id="bb58f-120">중간</span><span class="sxs-lookup"><span data-stu-id="bb58f-120">Medium</span></span> |<span data-ttu-id="bb58f-121">중간 영향 권장 사항은 성능을 향상시키지만, 크게 향상시키지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-121">Medium impact recommendations should improve performance, but not substantially.</span></span> |
| <span data-ttu-id="bb58f-122">낮음</span><span class="sxs-lookup"><span data-stu-id="bb58f-122">Low</span></span> |<span data-ttu-id="bb58f-123">낮은 영향 권장 사항은 없는 것보다 나은 성능을 제공하지만, 향상된 기능이 눈에 띄지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-123">Low impact recommendations should provide better performance than without, but improvements might not be significant.</span></span> |


> [!NOTE]
> <span data-ttu-id="bb58f-124">Azure SQL 데이터베이스 필요 toomonitor 활동 이상 순서 tooidentify 하루에 몇 가지 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-124">Azure SQL Database needs toomonitor activities at least for a day in order tooidentify some recommendations.</span></span> <span data-ttu-id="bb58f-125">hello Azure SQL 데이터베이스 작업의 임의 연결 상태가 좋지 않은 버스트 수 있습니다에 보다 쉽게 일관 된 쿼리 패턴을 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-125">hello Azure SQL Database can more easily optimize for consistent query patterns than it can for random spotty bursts of activity.</span></span> <span data-ttu-id="bb58f-126">권장 사항을 corrently 사용할 수 없는 경우 hello **성능 권장 사항** 페이지 이유를 설명 하는 메시지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-126">If recommendations are not corrently available, hello **Performance recommendation** page provides a message explaining why.</span></span>
> 

<span data-ttu-id="bb58f-127">Hello 기록 작업의 hello 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-127">You can also view hello status of hello historical operations.</span></span> <span data-ttu-id="bb58f-128">자세한 내용은 권장 사항 또는 상태 toosee를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-128">Select a recommendation or status toosee  more details.</span></span>

<span data-ttu-id="bb58f-129">Hello Azure 포털에서에서 "Create index" 권장 구성의 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-129">Here is an example of "Create index" recommendation in hello Azure portal.</span></span>

![인덱스 만들기](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a><span data-ttu-id="bb58f-131">권장 사항 적용</span><span class="sxs-lookup"><span data-stu-id="bb58f-131">Applying recommendations</span></span>
<span data-ttu-id="bb58f-132">Azure SQL 데이터베이스는 권장 하는 방법에 대 한 모든 권한을 제공 hello 다음 세 가지 옵션 중 하나를 사용 하 여 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-132">Azure SQL Database gives you full control over how recommendations are enabled using any of hello following three options:</span></span> 

* <span data-ttu-id="bb58f-133">개별 권장 구성을 한 번에 하나씩 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-133">Apply individual recommendations one at a time.</span></span>
* <span data-ttu-id="bb58f-134">Enable hello 자동 튜닝 tooautomatically 권장 사항을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-134">Enable hello Automatic tuning tooautomatically apply recommendations.</span></span>
* <span data-ttu-id="bb58f-135">tooimplement 권장 사항을 수동으로 hello 권장 데이터베이스에 대해 T-SQL 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-135">tooimplement a recommendation manually, run hello recommended T-SQL script against your database.</span></span>

<span data-ttu-id="bb58f-136">모든 권장 사항 tooview 세부 정보를 선택한 다음 클릭 **스크립트를 보려면** tooreview hello hello 권장 구성을 만드는 방법에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-136">Select any recommendation tooview its details and then click **View script** tooreview hello exact details of how hello recommendation is created.</span></span>

<span data-ttu-id="bb58f-137">hello 권장 구성이 적용 되는 등의 데이터베이스를 오프 라인 성능 권장 또는 자동 튜닝 하지를 사용 하는 동안 hello 데이터베이스가 온라인 상태로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-137">hello database remains online while hello recommendation is applied -- using performance recommendation or automatic tuning never takes a database offline.</span></span>

### <a name="apply-an-individual-recommendation"></a><span data-ttu-id="bb58f-138">개별 권장 구성 적용</span><span class="sxs-lookup"><span data-stu-id="bb58f-138">Apply an individual recommendation</span></span>
<span data-ttu-id="bb58f-139">권장 구성을 한 번에 하나씩 검토하고 수락할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-139">You can review and accept recommendations one at a time.</span></span>

1. <span data-ttu-id="bb58f-140">Hello에 **권장 사항을** 블레이드의 권장 구성 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-140">On hello **Recommendations** blade, select a recommendation.</span></span>
2. <span data-ttu-id="bb58f-141">Hello에 **세부 정보** 블레이드 클릭 **적용** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-141">On hello **Details** blade click **Apply** button.</span></span>
   
    ![권장 구성 적용](./media/sql-database-advisor-portal/apply.png)

<span data-ttu-id="bb58f-143">선택한 권장 hello 데이터베이스에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-143">Selected recommendation will be applied on hello database.</span></span>

### <a name="removing-recommendations-from-hello-list"></a><span data-ttu-id="bb58f-144">Hello 목록에서 제거 하는 권장 사항</span><span class="sxs-lookup"><span data-stu-id="bb58f-144">Removing recommendations from hello list</span></span>
<span data-ttu-id="bb58f-145">권장 사항 목록에 항목이 tooremove hello 목록에서 원하는 경우 hello 권장 사항을 무시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-145">If your list of recommendations contains items that you want tooremove from hello list, you can discard hello recommendation:</span></span>

1. <span data-ttu-id="bb58f-146">hello 목록에서 권장 구성을 선택 **권장 사항을** tooopen hello 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-146">Select a recommendation in hello list of **Recommendations** tooopen hello details.</span></span>
2. <span data-ttu-id="bb58f-147">클릭 **취소** hello에 **세부 정보** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-147">Click **Discard** on hello **Details** blade.</span></span>

<span data-ttu-id="bb58f-148">원하는 경우 삭제 된 항목을 toohello 다시 추가할 수 있습니다 **권장 사항을** 목록:</span><span class="sxs-lookup"><span data-stu-id="bb58f-148">If desired, you can add discarded items back toohello **Recommendations** list:</span></span>

1. <span data-ttu-id="bb58f-149">Hello에 **권장 사항을** 블레이드 클릭 **보기 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-149">On hello **Recommendations** blade click **View discarded**.</span></span>
2. <span data-ttu-id="bb58f-150">세부 정보 목록 tooview hello에서에서 삭제 한 항목을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-150">Select a discarded item from hello list tooview its details.</span></span>
3. <span data-ttu-id="bb58f-151">필요에 따라 **삭제 취소** tooadd hello 인덱스 백 toohello 기본 목록 **권장 사항을**합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-151">Optionally, click **Undo Discard** tooadd hello index back toohello main list of **Recommendations**.</span></span>


### <a name="enable-automatic-tuning"></a><span data-ttu-id="bb58f-152">자동 조정 사용</span><span class="sxs-lookup"><span data-stu-id="bb58f-152">Enable automatic tuning</span></span>
<span data-ttu-id="bb58f-153">Hello Azure SQL 데이터베이스 tooimplement 권장 사항을 자동으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-153">You can set hello Azure SQL Database tooimplement recommendations automatically.</span></span> <span data-ttu-id="bb58f-154">권장 구성은 사용할 수 있을 때 자동으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-154">As recommendations become available they will automatically be applied.</span></span> <span data-ttu-id="bb58f-155">으로 hello에서 관리 하는 모든 권장 사항이 포함 된 경우 성능에 미치는 영향 hello 음수 hello 권장 사항은 서비스가 되돌립니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-155">As with all recommendations managed by hello service if hello performance impact is negative hello recommendation will be reverted.</span></span>

1. <span data-ttu-id="bb58f-156">Hello에 **권장 사항을** 블레이드에서 클릭 **자동화**:</span><span class="sxs-lookup"><span data-stu-id="bb58f-156">On hello **Recommendations** blade, click **Automate**:</span></span>
   
    ![관리자 설정](./media/sql-database-advisor-portal/settings.png)
2. <span data-ttu-id="bb58f-158">작업 선택 tooautomate:</span><span class="sxs-lookup"><span data-stu-id="bb58f-158">Select actions tooautomate:</span></span>
   
    ![권장된 인덱스](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a><span data-ttu-id="bb58f-160">T-SQL 스크립트를 권장 하는 hello를 수동으로 실행</span><span class="sxs-lookup"><span data-stu-id="bb58f-160">Manually run hello recommended T-SQL script</span></span>
<span data-ttu-id="bb58f-161">권장 사항을 선택한 다음 **스크립트 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-161">Select any recommendation and then click **View script**.</span></span> <span data-ttu-id="bb58f-162">데이터베이스에 대해이 스크립트를 실행 toomanually hello 권장 구성을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-162">Run this script against your database toomanually apply hello recommendation.</span></span>

<span data-ttu-id="bb58f-163">*수동으로 실행 하는 인덱스는 하지 모니터링 하 고 hello 서비스 성능에 미치는 영향에 대 한 유효성을 검사* 하므로 생성 tooverify 후 이러한 인덱스를 모니터링 하는 것이 좋습니다 제공 성능 향상 및 조정 하거나 경우 삭제 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-163">*Indexes that are manually executed are not monitored and validated for performance impact by hello service* so it is suggested that you monitor these indexes after creation tooverify they provide performance gains and adjust or delete them if necessary.</span></span> <span data-ttu-id="bb58f-164">인덱스 만들기에 대한 세부 정보는 [CREATE INDEX (TRANSACT-SQL)](https://msdn.microsoft.com/library/ms188783.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb58f-164">For details about creating indexes, see [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span></span>

### <a name="canceling-recommendations"></a><span data-ttu-id="bb58f-165">권장 사항 취소</span><span class="sxs-lookup"><span data-stu-id="bb58f-165">Canceling recommendations</span></span>
<span data-ttu-id="bb58f-166">**보류 중**, **확인 중** 또는 **성공** 상태에 있는 권장 사항은 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-166">Recommendations that are in a **Pending**, **Verifying**, or **Success** status can be canceled.</span></span> <span data-ttu-id="bb58f-167">**실행 중** 상태의 권장 사항은 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-167">Recommendations with a status of **Executing** cannot be canceled.</span></span>

1. <span data-ttu-id="bb58f-168">Hello에 권장 사항을 선택 **튜닝 기록** 영역 tooopen hello **권장 사항 세부 정보** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-168">Select a recommendation in hello **Tuning History** area tooopen hello **recommendations details** blade.</span></span>
2. <span data-ttu-id="bb58f-169">클릭 **취소** tooabort hello 과정 hello 권장 구성을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-169">Click **Cancel** tooabort hello process of applying hello recommendation.</span></span>

## <a name="monitoring-operations"></a><span data-ttu-id="bb58f-170">모니터링 작업</span><span class="sxs-lookup"><span data-stu-id="bb58f-170">Monitoring operations</span></span>
<span data-ttu-id="bb58f-171">권장 구성을 적용해도 즉각적으로 일어나지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-171">Applying a recommendation might not happen instantaneously.</span></span> <span data-ttu-id="bb58f-172">hello 포털 권장 구성의 hello 상태에 관한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-172">hello portal provides details regarding hello status of recommendation.</span></span> <span data-ttu-id="bb58f-173">hello 다음은 인덱스에 저장할 수 있는 가능한 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-173">hello following are possible states that an index can be in:</span></span>

| <span data-ttu-id="bb58f-174">가동 상태</span><span class="sxs-lookup"><span data-stu-id="bb58f-174">Status</span></span> | <span data-ttu-id="bb58f-175">설명</span><span class="sxs-lookup"><span data-stu-id="bb58f-175">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="bb58f-176">Pending</span><span class="sxs-lookup"><span data-stu-id="bb58f-176">Pending</span></span> |<span data-ttu-id="bb58f-177">권장 사항 적용 명령을 수신했고 실행이 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-177">Apply recommendation command has been received and is scheduled for execution.</span></span> |
| <span data-ttu-id="bb58f-178">실행 중</span><span class="sxs-lookup"><span data-stu-id="bb58f-178">Executing</span></span> |<span data-ttu-id="bb58f-179">hello 권장 구성이 적용 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-179">hello recommendation is being applied.</span></span> |
| <span data-ttu-id="bb58f-180">확인 중</span><span class="sxs-lookup"><span data-stu-id="bb58f-180">Verifying</span></span> |<span data-ttu-id="bb58f-181">권장 사항이 성공적으로 적용 하 고 hello 서비스는 hello 혜택을 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-181">Recommendation was successfully applied and hello service is measuring hello benefits.</span></span> |
| <span data-ttu-id="bb58f-182">성공</span><span class="sxs-lookup"><span data-stu-id="bb58f-182">Success</span></span> |<span data-ttu-id="bb58f-183">권장 사항이 성공적으로 적용되면 성능을 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-183">Recommendation was successfully applied and benefits have been measured.</span></span> |
| <span data-ttu-id="bb58f-184">오류</span><span class="sxs-lookup"><span data-stu-id="bb58f-184">Error</span></span> |<span data-ttu-id="bb58f-185">Hello 과정 hello 권장 구성을 적용 하는 동안 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-185">An error occurred during hello process of applying hello recommendation.</span></span> <span data-ttu-id="bb58f-186">이 일시적인 문제 또는 스키마 변경 toohello 테이블 수 및 hello 스크립트는 더 이상 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-186">This can be a transient issue, or possibly a schema change toohello table and hello script is no longer valid.</span></span> |
| <span data-ttu-id="bb58f-187">되돌리기</span><span class="sxs-lookup"><span data-stu-id="bb58f-187">Reverting</span></span> |<span data-ttu-id="bb58f-188">hello 권장 구성이 적용 된 비 고성능 판단 되는 있고 자동으로 되돌리고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-188">hello recommendation was applied, but has been deemed non-performant and is being automatically reverted.</span></span> |
| <span data-ttu-id="bb58f-189">되돌림</span><span class="sxs-lookup"><span data-stu-id="bb58f-189">Reverted</span></span> |<span data-ttu-id="bb58f-190">hello 권장 되돌려.</span><span class="sxs-lookup"><span data-stu-id="bb58f-190">hello recommendation was reverted.</span></span> |

<span data-ttu-id="bb58f-191">자세한 내용은 in-process에 권장 사항을 hello 목록 toosee에서를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-191">Click an in-process recommendation from hello list toosee more details:</span></span>

![권장된 인덱스](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a><span data-ttu-id="bb58f-193">권장 사항 되돌리기</span><span class="sxs-lookup"><span data-stu-id="bb58f-193">Reverting a recommendation</span></span>
<span data-ttu-id="bb58f-194">Hello 성능 권장 사항 tooapply hello 권장 사항을 사용 하는 경우 (수동으로 hello T-SQL 스크립트를 실행 하지 않은 것을 의미) 자동으로 되돌려집니다 것 찾으면 hello 성능 영향 toobe 음수입니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-194">If you used hello performance recommendations tooapply hello recommendation (meaning you did not manually run hello T-SQL script) it will automatically revert it if it finds hello performance impact toobe negative.</span></span> <span data-ttu-id="bb58f-195">어떤 이유로 든 원할 toorevert 권장 할 수 있습니다 hello 다음:</span><span class="sxs-lookup"><span data-stu-id="bb58f-195">If for any reason you simply want toorevert a recommendation you can do hello following:</span></span>

1. <span data-ttu-id="bb58f-196">Hello에 성공적으로 적용 된 권장 사항을 선택 **기록 튜닝** 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-196">Select a successfully applied recommendation in hello **Tuning history** area.</span></span>
2. <span data-ttu-id="bb58f-197">클릭 **Revert** hello에 **권장 사항 세부 정보** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-197">Click **Revert** on hello **recommendation details** blade.</span></span>

![권장된 인덱스](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a><span data-ttu-id="bb58f-199">인덱스 권장 구성의 성능 영향 모니터링</span><span class="sxs-lookup"><span data-stu-id="bb58f-199">Monitoring performance impact of index recommendations</span></span>
<span data-ttu-id="bb58f-200">권장 사항을 성공적으로 구현 된 후 (현재 작업 인덱스 및 쿼리 권장 구성의 경우에 매개 변수화) 클릭할 수 있는 **쿼리 Insights** hello 권장 사항 세부 정보 블레이드에서 tooopen에 [쿼리 Performance Insight](sql-database-query-performance.md) hello 상위 쿼리의 성능에 영향을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-200">After recommendations are successfully implemented (currently, index operations and parameterize queries recommendations only) you can click **Query Insights** on hello recommendation details blade tooopen [Query Performance Insights](sql-database-query-performance.md) and see hello performance impact of your top queries.</span></span>

![성능에 미치는 영향을 모니터링합니다.](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a><span data-ttu-id="bb58f-202">요약</span><span class="sxs-lookup"><span data-stu-id="bb58f-202">Summary</span></span>
<span data-ttu-id="bb58f-203">Azure SQL Database는 SQL Database 성능을 향상하기 위한 권장 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-203">Azure SQL Database provides recommendations for improving SQL database performance.</span></span> <span data-ttu-id="bb58f-204">T-SQL 스크립트를 개별적인 완전 자동으로 제공하여 데이터베이스를 최적화하고 궁극적으로 쿼리 성능을 향상시키도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-204">By providing T-SQL scripts, as well as individual and fully-automatic, you get a helpful assistance in optimizing your database and ultimately improving query performance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb58f-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bb58f-205">Next steps</span></span>
<span data-ttu-id="bb58f-206">하면 권장 사항을 모니터링 하 고 tooapply 계속 해당 toorefine 성능입니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-206">Monitor your recommendations and continue tooapply them toorefine performance.</span></span> <span data-ttu-id="bb58f-207">데이터베이스 워크로드는 동적 이며 지속적으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-207">Database workloads are dynamic and change continuously.</span></span> <span data-ttu-id="bb58f-208">Azure SQL 데이터베이스는 toomonitor 계속 되 고 데이터베이스의 성능을 향상 시킬 수 있는 권장 사항을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-208">Azure SQL Database will continue toomonitor and provide recommendations that can potentially improve your database's performance.</span></span> 

* <span data-ttu-id="bb58f-209">참조 [자동 튜닝](sql-database-automatic-tuning.md) toolearn에 더 알아봅니다 hello Azure SQL 데이터베이스에서 자동으로 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-209">See [Automatic tuning](sql-database-automatic-tuning.md) toolearn more about hello automatic tuning in Azure SQL Database.</span></span>
* <span data-ttu-id="bb58f-210">Azure SQL Database 성능 권장 사항에 대한 개요는 [성능 권장 사항](sql-database-advisor.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb58f-210">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="bb58f-211">참조 [Query Performance Insight](sql-database-query-performance.md) toolearn hello 상위 쿼리의 성능에 영향을 확인 하는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb58f-211">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bb58f-212">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="bb58f-212">Additional resources</span></span>
* [<span data-ttu-id="bb58f-213">쿼리 저장소</span><span class="sxs-lookup"><span data-stu-id="bb58f-213">Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx)
* [<span data-ttu-id="bb58f-214">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="bb58f-214">CREATE INDEX</span></span>](https://msdn.microsoft.com/library/ms188783.aspx)
* [<span data-ttu-id="bb58f-215">역할 기반 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="bb58f-215">Role-based access control</span></span>](../active-directory/role-based-access-control-what-is.md)


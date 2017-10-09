---
title: "aaaMigrate 기존 Azure 데이터 웨어하우스 toopremium 저장소 | Microsoft Docs"
description: "기존 데이터 웨어하우스 toopremium 저장소로 마이그레이션하기 위한 지침"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a><span data-ttu-id="ea7c2-103">데이터 웨어하우스 toopremium 저장소 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="ea7c2-103">Migrate your data warehouse toopremium storage</span></span>
<span data-ttu-id="ea7c2-104">Azure SQL Data Warehouse는 최근에 도입된 [큰 성능 예측 가능성을 위한 Premium Storage][premium storage for greater performance predictability]입니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-104">Azure SQL Data Warehouse recently introduced [premium storage for greater performance predictability][premium storage for greater performance predictability].</span></span> <span data-ttu-id="ea7c2-105">Toopremium 저장소를 마이그레이션할 하는 기존 데이터 웨어하우스 표준 저장소에 현재 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-105">Existing data warehouses currently on standard storage can now be migrated toopremium storage.</span></span> <span data-ttu-id="ea7c2-106">자동 마이그레이션의 이용할 수 있습니다 toocontrol 선호 하는 경우 또는 때 toomigrate (하는 과정이 가동 중지 시간이)를 할 수 있는 마이그레이션 직접 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-106">You can take advantage of automatic migration, or if you prefer toocontrol when toomigrate (which does involve some downtime), you can do hello migration yourself.</span></span>

<span data-ttu-id="ea7c2-107">둘 이상의 데이터 웨어하우스를 사용 하는 경우 사용 하 여 hello [일정 자동 마이그레이션] [ automatic migration schedule] toodetermine 마이그레이션하면도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-107">If you have more than one data warehouse, use hello [automatic migration schedule][automatic migration schedule] toodetermine when it will also be migrated.</span></span>

## <a name="determine-storage-type"></a><span data-ttu-id="ea7c2-108">저장소 유형 결정</span><span class="sxs-lookup"><span data-stu-id="ea7c2-108">Determine storage type</span></span>
<span data-ttu-id="ea7c2-109">Hello 날짜를 수행 하기 전에 데이터 웨어하우스를 만든 경우 현재 표준 저장소를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-109">If you created a data warehouse before hello following dates, you are currently using standard storage.</span></span>

| <span data-ttu-id="ea7c2-110">**지역**</span><span class="sxs-lookup"><span data-stu-id="ea7c2-110">**Region**</span></span> | <span data-ttu-id="ea7c2-111">**이 날짜 이전에 만든 데이터 웨어하우스**</span><span class="sxs-lookup"><span data-stu-id="ea7c2-111">**Data warehouse created before this date**</span></span> |
|:--- |:--- |
| <span data-ttu-id="ea7c2-112">오스트레일리아 동부</span><span class="sxs-lookup"><span data-stu-id="ea7c2-112">Australia East</span></span> |<span data-ttu-id="ea7c2-113">Premium Storage를 아직 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="ea7c2-113">Premium storage not yet available</span></span> |
| <span data-ttu-id="ea7c2-114">중국 동부</span><span class="sxs-lookup"><span data-stu-id="ea7c2-114">China East</span></span> |<span data-ttu-id="ea7c2-115">2016년 11월 1일</span><span class="sxs-lookup"><span data-stu-id="ea7c2-115">November 1, 2016</span></span> |
| <span data-ttu-id="ea7c2-116">중국 북부</span><span class="sxs-lookup"><span data-stu-id="ea7c2-116">China North</span></span> |<span data-ttu-id="ea7c2-117">2016년 11월 1일</span><span class="sxs-lookup"><span data-stu-id="ea7c2-117">November 1, 2016</span></span> |
| <span data-ttu-id="ea7c2-118">독일 중부</span><span class="sxs-lookup"><span data-stu-id="ea7c2-118">Germany Central</span></span> |<span data-ttu-id="ea7c2-119">2016년 11월 1일</span><span class="sxs-lookup"><span data-stu-id="ea7c2-119">November 1, 2016</span></span> |
| <span data-ttu-id="ea7c2-120">독일 북동부</span><span class="sxs-lookup"><span data-stu-id="ea7c2-120">Germany Northeast</span></span> |<span data-ttu-id="ea7c2-121">2016년 11월 1일</span><span class="sxs-lookup"><span data-stu-id="ea7c2-121">November 1, 2016</span></span> |
| <span data-ttu-id="ea7c2-122">인도 서부</span><span class="sxs-lookup"><span data-stu-id="ea7c2-122">India West</span></span> |<span data-ttu-id="ea7c2-123">Premium Storage를 아직 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="ea7c2-123">Premium storage not yet available</span></span> |
| <span data-ttu-id="ea7c2-124">일본 서부</span><span class="sxs-lookup"><span data-stu-id="ea7c2-124">Japan West</span></span> |<span data-ttu-id="ea7c2-125">Premium Storage를 아직 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="ea7c2-125">Premium storage not yet available</span></span> |
| <span data-ttu-id="ea7c2-126">미국 중북부</span><span class="sxs-lookup"><span data-stu-id="ea7c2-126">North Central US</span></span> |<span data-ttu-id="ea7c2-127">2016년 11월 10일</span><span class="sxs-lookup"><span data-stu-id="ea7c2-127">November 10, 2016</span></span> |

## <a name="automatic-migration-details"></a><span data-ttu-id="ea7c2-128">자동 마이그레이션 세부 정보</span><span class="sxs-lookup"><span data-stu-id="ea7c2-128">Automatic migration details</span></span>
<span data-ttu-id="ea7c2-129">기본적으로 마이그레이션할 예정 데이터베이스를 해당 지역의 현지 시간으로 오전 6 시와 오후 6시 사이 hello 중 [일정 자동 마이그레이션][automatic migration schedule]합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-129">By default, we will migrate your database for you between 6:00 PM and 6:00 AM in your region's local time during hello [automatic migration schedule][automatic migration schedule].</span></span> <span data-ttu-id="ea7c2-130">Hello 마이그레이션하는 동안 기존 데이터 웨어하우스의 사용할 수 없게 됩니다 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-130">Your existing data warehouse will be unusable during hello migration.</span></span> <span data-ttu-id="ea7c2-131">hello 마이그레이션 데이터 웨어하우스 당 저장소 테라바이트 당 약 1 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-131">hello migration will take approximately one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="ea7c2-132">Hello 자동 마이그레이션의 한 부분에 청구 되지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-132">You will not be charged during any portion of hello automatic migration.</span></span>

> [!NOTE]
> <span data-ttu-id="ea7c2-133">Hello 마이그레이션이 완료 되 면 다시 온라인이 고 사용 가능한 데이터 웨어하우스가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-133">When hello migration is complete, your data warehouse will be back online and usable.</span></span>
>
>

<span data-ttu-id="ea7c2-134">Microsoft는 hello 단계 toocomplete hello 마이그레이션 (사용자의 모든 참여 필요 하지 않습니다) 하는 데입니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-134">Microsoft is taking hello following steps toocomplete hello migration (these do not require any involvement on your part).</span></span> <span data-ttu-id="ea7c2-135">이 예제에서는 표준 저장소의 기존 데이터 웨어하우스의 이름이 현재 "MyDW"라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-135">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="ea7c2-136">너무의 이름을 "MyDW" Microsoft "MyDW_DO_NOT_USE_ [타임 스탬프]"입니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-136">Microsoft renames “MyDW” too“MyDW_DO_NOT_USE_[Timestamp].”</span></span>
2. <span data-ttu-id="ea7c2-137">Microsoft는 "MyDW_DO_NOT_USE_[타임스탬프]"를 일시 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-137">Microsoft pauses “MyDW_DO_NOT_USE_[Timestamp].”</span></span> <span data-ttu-id="ea7c2-138">이 시간 동안 백업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-138">During this time, a backup is taken.</span></span> <span data-ttu-id="ea7c2-139">이 과정에서 문제가 발생한 경우 여러 일시 중지 및 다시 시작이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-139">You may see multiple pauses and resumes if we encounter any issues during this process.</span></span>
3. <span data-ttu-id="ea7c2-140">Microsoft "MyDW" 프리미엄 저장소에 hello 백업에서 2 단계에서 수행 되 라는 새 데이터 웨어하우스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-140">Microsoft creates a new data warehouse named “MyDW” on premium storage from hello backup taken in step 2.</span></span> <span data-ttu-id="ea7c2-141">"MyDW" hello 복원이 완료 된 후까지 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-141">“MyDW” will not appear until after hello restore is complete.</span></span>
4. <span data-ttu-id="ea7c2-142">(일시 중지 된 또는 현재) "MyDW" toohello 동일한 데이터 웨어하우스 단위와 상태를 반환 hello 복원이 완료 되 면 hello 마이그레이션을 시작 하기 전에 있었던 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-142">After hello restore is complete, “MyDW” returns toohello same data warehouse units and state (paused or active) that it was before hello migration.</span></span>
5. <span data-ttu-id="ea7c2-143">Hello 마이그레이션이 완료 된 후 Microsoft "MyDW_DO_NOT_USE_ [타임 스탬프]"를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-143">After hello migration is complete, Microsoft deletes “MyDW_DO_NOT_USE_[Timestamp]”.</span></span>

> [!NOTE]
> <span data-ttu-id="ea7c2-144">hello 다음 설정으로 이전 되지 않습니다 hello 마이그레이션의 일환으로:</span><span class="sxs-lookup"><span data-stu-id="ea7c2-144">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="ea7c2-145">Hello 데이터베이스 수준 감사 toobe 다시 활성화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-145">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="ea7c2-146">Hello 데이터베이스 수준 방화벽 규칙 toobe 다시 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-146">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="ea7c2-147">Hello 서버 수준 방화벽 규칙의 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-147">Firewall rules at hello server level are not affected.</span></span>
>
>

### <a name="automatic-migration-schedule"></a><span data-ttu-id="ea7c2-148">자동 마이그레이션 일정</span><span class="sxs-lookup"><span data-stu-id="ea7c2-148">Automatic migration schedule</span></span>
<span data-ttu-id="ea7c2-149">자동 마이그레이션 중단 일정에 따라 hello 중 오후 6시 및 오전 6시 (현지 시간 / 지역당) 간에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-149">Automatic migrations occur between 6:00 PM and 6:00 AM (local time per region) during hello following outage schedule.</span></span>

| <span data-ttu-id="ea7c2-150">**지역**</span><span class="sxs-lookup"><span data-stu-id="ea7c2-150">**Region**</span></span> | <span data-ttu-id="ea7c2-151">**예상된 시작 날짜**</span><span class="sxs-lookup"><span data-stu-id="ea7c2-151">**Estimated start date**</span></span> | <span data-ttu-id="ea7c2-152">**예상된 종료 날짜**</span><span class="sxs-lookup"><span data-stu-id="ea7c2-152">**Estimated end date**</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ea7c2-153">오스트레일리아 동부</span><span class="sxs-lookup"><span data-stu-id="ea7c2-153">Australia East</span></span> |<span data-ttu-id="ea7c2-154">아직 결정되지 않음</span><span class="sxs-lookup"><span data-stu-id="ea7c2-154">Not determined yet</span></span> |<span data-ttu-id="ea7c2-155">아직 결정되지 않음</span><span class="sxs-lookup"><span data-stu-id="ea7c2-155">Not determined yet</span></span> |
| <span data-ttu-id="ea7c2-156">중국 동부</span><span class="sxs-lookup"><span data-stu-id="ea7c2-156">China East</span></span> |<span data-ttu-id="ea7c2-157">2017년 1월 9일</span><span class="sxs-lookup"><span data-stu-id="ea7c2-157">January 9, 2017</span></span> |<span data-ttu-id="ea7c2-158">2017년 1월 13일</span><span class="sxs-lookup"><span data-stu-id="ea7c2-158">January 13, 2017</span></span> |
| <span data-ttu-id="ea7c2-159">중국 북부</span><span class="sxs-lookup"><span data-stu-id="ea7c2-159">China North</span></span> |<span data-ttu-id="ea7c2-160">2017년 1월 9일</span><span class="sxs-lookup"><span data-stu-id="ea7c2-160">January 9, 2017</span></span> |<span data-ttu-id="ea7c2-161">2017년 1월 13일</span><span class="sxs-lookup"><span data-stu-id="ea7c2-161">January 13, 2017</span></span> |
| <span data-ttu-id="ea7c2-162">독일 중부</span><span class="sxs-lookup"><span data-stu-id="ea7c2-162">Germany Central</span></span> |<span data-ttu-id="ea7c2-163">2017년 1월 9일</span><span class="sxs-lookup"><span data-stu-id="ea7c2-163">January 9, 2017</span></span> |<span data-ttu-id="ea7c2-164">2017년 1월 13일</span><span class="sxs-lookup"><span data-stu-id="ea7c2-164">January 13, 2017</span></span> |
| <span data-ttu-id="ea7c2-165">독일 북동부</span><span class="sxs-lookup"><span data-stu-id="ea7c2-165">Germany Northeast</span></span> |<span data-ttu-id="ea7c2-166">2017년 1월 9일</span><span class="sxs-lookup"><span data-stu-id="ea7c2-166">January 9, 2017</span></span> |<span data-ttu-id="ea7c2-167">2017년 1월 13일</span><span class="sxs-lookup"><span data-stu-id="ea7c2-167">January 13, 2017</span></span> |
| <span data-ttu-id="ea7c2-168">인도 서부</span><span class="sxs-lookup"><span data-stu-id="ea7c2-168">India West</span></span> |<span data-ttu-id="ea7c2-169">아직 결정되지 않음</span><span class="sxs-lookup"><span data-stu-id="ea7c2-169">Not determined yet</span></span> |<span data-ttu-id="ea7c2-170">아직 결정되지 않음</span><span class="sxs-lookup"><span data-stu-id="ea7c2-170">Not determined yet</span></span> |
| <span data-ttu-id="ea7c2-171">일본 서부</span><span class="sxs-lookup"><span data-stu-id="ea7c2-171">Japan West</span></span> |<span data-ttu-id="ea7c2-172">아직 결정되지 않음</span><span class="sxs-lookup"><span data-stu-id="ea7c2-172">Not determined yet</span></span> |<span data-ttu-id="ea7c2-173">아직 결정되지 않음</span><span class="sxs-lookup"><span data-stu-id="ea7c2-173">Not determined yet</span></span> |
| <span data-ttu-id="ea7c2-174">미국 중북부</span><span class="sxs-lookup"><span data-stu-id="ea7c2-174">North Central US</span></span> |<span data-ttu-id="ea7c2-175">2017년 1월 9일</span><span class="sxs-lookup"><span data-stu-id="ea7c2-175">January 9, 2017</span></span> |<span data-ttu-id="ea7c2-176">2017년 1월 13일</span><span class="sxs-lookup"><span data-stu-id="ea7c2-176">January 13, 2017</span></span> |

## <a name="self-migration-toopremium-storage"></a><span data-ttu-id="ea7c2-177">자동 마이그레이션 toopremium 저장소</span><span class="sxs-lookup"><span data-stu-id="ea7c2-177">Self-migration toopremium storage</span></span>
<span data-ttu-id="ea7c2-178">작동 중단 시간이 발생 한 경우 toocontrol를 원하는 경우 hello 나오는 단계 toomigrate 기존 데이터 웨어하우스 표준 저장소 toopremium 저장소에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-178">If you want toocontrol when your downtime will occur, you can use hello following steps toomigrate an existing data warehouse on standard storage toopremium storage.</span></span> <span data-ttu-id="ea7c2-179">이 옵션을 선택 하는 경우에 해당 지역에서 hello 자동 마이그레이션을 시작 하기 전에 hello 자체 마이그레이션을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-179">If you choose this option, you must complete hello self-migration before hello automatic migration begins in that region.</span></span> <span data-ttu-id="ea7c2-180">이렇게 하면 hello 자동 마이그레이션 충돌의 위험을 방지 하는 (toohello 참조 [일정 자동 마이그레이션][automatic migration schedule]).</span><span class="sxs-lookup"><span data-stu-id="ea7c2-180">This ensures that you avoid any risk of hello automatic migration causing a conflict (refer toohello [automatic migration schedule][automatic migration schedule]).</span></span>

### <a name="self-migration-instructions"></a><span data-ttu-id="ea7c2-181">자체 마이그레이션 지침</span><span class="sxs-lookup"><span data-stu-id="ea7c2-181">Self-migration instructions</span></span>
<span data-ttu-id="ea7c2-182">데이터 웨어하우스 직접 hello 백업 및 복원 기능 toomigrate 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-182">toomigrate your data warehouse yourself, use hello backup and restore features.</span></span> <span data-ttu-id="ea7c2-183">hello 복원의 hello 마이그레이션 부분이 예상된 tootake 데이터 웨어하우스 당 저장소 테라바이트 당 약 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-183">hello restore portion of hello migration is expected tootake around one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="ea7c2-184">마이그레이션이 완료 된 후 이름과 같은 이름을 tookeep hello 원한다 면 hello에 따라 [마이그레이션하는 동안 단계 toorename][steps toorename during migration]합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-184">If you want tookeep hello same name after migration is complete, follow hello [steps toorename during migration][steps toorename during migration].</span></span>

1. <span data-ttu-id="ea7c2-185">데이터 웨어하우스를 [일시 중지][Pause]합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-185">[Pause][Pause] your data warehouse.</span></span> <span data-ttu-id="ea7c2-186">자동 백업이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-186">This takes an automatic backup.</span></span>
2. <span data-ttu-id="ea7c2-187">가장 최근의 스냅숏에서 [복원][Restore]합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-187">[Restore][Restore] from your most recent snapshot.</span></span>
3. <span data-ttu-id="ea7c2-188">표준 저장소의 기존 데이터 웨어하우스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-188">Delete your existing data warehouse on standard storage.</span></span> <span data-ttu-id="ea7c2-189">**Toodo을이 단계가 실패 하는 경우 데이터 웨어하우스 모두에 대 한 청구 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="ea7c2-189">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>

> [!NOTE]
> <span data-ttu-id="ea7c2-190">hello 다음 설정으로 이전 되지 않습니다 hello 마이그레이션의 일환으로:</span><span class="sxs-lookup"><span data-stu-id="ea7c2-190">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="ea7c2-191">Hello 데이터베이스 수준 감사 toobe 다시 활성화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-191">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="ea7c2-192">Hello 데이터베이스 수준 방화벽 규칙 toobe 다시 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-192">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="ea7c2-193">Hello 서버 수준 방화벽 규칙의 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-193">Firewall rules at hello server level are not affected.</span></span>
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a><span data-ttu-id="ea7c2-194">마이그레이션 중 데이터 웨어하우스의 이름 바꾸기(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="ea7c2-194">Rename data warehouse during migration (optional)</span></span>
<span data-ttu-id="ea7c2-195">두 데이터베이스를 동일한 논리 서버가 하 여야 하는 hello hello 동일한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-195">Two databases on hello same logical server cannot have hello same name.</span></span> <span data-ttu-id="ea7c2-196">SQL 데이터 웨어하우스는 이제 hello 기능 toorename 데이터 웨어하우스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-196">SQL Data Warehouse now supports hello ability toorename a data warehouse.</span></span>

<span data-ttu-id="ea7c2-197">이 예제에서는 표준 저장소의 기존 데이터 웨어하우스의 이름이 현재 "MyDW"라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-197">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="ea7c2-198">"MyDW" hello 다음 ALTER DATABASE 명령을 사용 하 여 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-198">Rename "MyDW" by using hello following ALTER DATABASE command.</span></span> <span data-ttu-id="ea7c2-199">(이 예제에서는 합니다 이름을 바꾸지 "MyDW_BeforeMigration.")  이 명령은 모든 기존 트랜잭션을 중지 하 고 hello master 데이터베이스 toosucceed에서 수행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-199">(In this example, we'll rename it "MyDW_BeforeMigration.")  This command stops all existing transactions, and must be done in hello master database toosucceed.</span></span>
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. <span data-ttu-id="ea7c2-200">"MyDW_BeforeMigration"을 [일시 중지][Pause]합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-200">[Pause][Pause] "MyDW_BeforeMigration."</span></span> <span data-ttu-id="ea7c2-201">자동 백업이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-201">This takes an automatic backup.</span></span>
3. <span data-ttu-id="ea7c2-202">[복원] [ Restore] 가장 최근 스냅숏의 hello 이름으로 새 데이터베이스에서 toobe (예: "MyDW")이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-202">[Restore][Restore] from your most recent snapshot a new database with hello name it used toobe (for example, "MyDW").</span></span>
4. <span data-ttu-id="ea7c2-203">"MyDW_BeforeMigration"을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-203">Delete "MyDW_BeforeMigration."</span></span> <span data-ttu-id="ea7c2-204">**Toodo을이 단계가 실패 하는 경우 데이터 웨어하우스 모두에 대 한 청구 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="ea7c2-204">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>


## <a name="next-steps"></a><span data-ttu-id="ea7c2-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ea7c2-205">Next steps</span></span>
<span data-ttu-id="ea7c2-206">데이터 웨어하우스의 hello 기본 아키텍처에서 데이터베이스 blob 파일의 횟수가 증가 레이블에도, hello로 toopremium 저장소를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-206">With hello change toopremium storage, you also have an increased number of database blob files in hello underlying architecture of your data warehouse.</span></span> <span data-ttu-id="ea7c2-207">이러한 변경의 toomaximize hello 성능 이점을 hello 다음 스크립트를 사용 하 여 클러스터형된 columnstore 인덱스 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-207">toomaximize hello performance benefits of this change, rebuild your clustered columnstore indexes by using hello following script.</span></span> <span data-ttu-id="ea7c2-208">hello 스크립트는 기존 데이터 toohello 추가 blob 중 일부를 강제 적용 하 여 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-208">hello script works by forcing some of your existing data toohello additional blobs.</span></span> <span data-ttu-id="ea7c2-209">조치를 취하지 테이블에 더 많은 데이터를 로드 하는 대로 hello 데이터 시간에 따라 재배포할 자연스럽 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-209">If you take no action, hello data will naturally redistribute over time as you load more data into your tables.</span></span>

<span data-ttu-id="ea7c2-210">**필수 조건:**</span><span class="sxs-lookup"><span data-stu-id="ea7c2-210">**Prerequisites:**</span></span>

- <span data-ttu-id="ea7c2-211">hello 데이터 웨어하우스를 실행할지 (1, 000 데이터 웨어하우스 단위 포함) 이상 (참조 [배율 계산 능력이][scale compute power]).</span><span class="sxs-lookup"><span data-stu-id="ea7c2-211">hello data warehouse should run with 1,000 data warehouse units or higher (see [scale compute power][scale compute power]).</span></span>
- <span data-ttu-id="ea7c2-212">hello hello 스크립트를 실행 하는 사용자에에서 있어야 hello [mediumrc 역할] [ mediumrc role] 이상.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-212">hello user executing hello script should be in hello [mediumrc role][mediumrc role] or higher.</span></span> <span data-ttu-id="ea7c2-213">사용자 toothis 역할 tooadd hello 다음을 실행 합니다.````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span><span class="sxs-lookup"><span data-stu-id="ea7c2-213">tooadd a user toothis role, execute hello following: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span></span>

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

<span data-ttu-id="ea7c2-214">데이터 웨어하우스와 문제가 발생 하는 경우 [지원 티켓을 만드세요] [ create a support ticket] hello 가능한 원인으로 "마이그레이션 toopremium storage"를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea7c2-214">If you encounter any issues with your data warehouse, [create a support ticket][create a support ticket] and reference “migration toopremium storage” as hello possible cause.</span></span>

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com

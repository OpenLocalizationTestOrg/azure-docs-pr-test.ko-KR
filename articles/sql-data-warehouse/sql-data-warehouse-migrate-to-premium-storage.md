---
title: "기존 Azure 데이터 웨어하우스를 Premium Storage로 마이그레이션 | Microsoft Docs"
description: "기존 데이터 웨어하우스를 Premium Storage로 마이그레이션하기 위한 지침"
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
ms.openlocfilehash: 860e50b532b4b0a21d3be54f087730070b0e56bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-data-warehouse-to-premium-storage"></a><span data-ttu-id="d7aa0-103">데이터 웨어하우스를 Premium Storage로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="d7aa0-103">Migrate your data warehouse to premium storage</span></span>
<span data-ttu-id="d7aa0-104">Azure SQL Data Warehouse는 최근에 도입된 [큰 성능 예측 가능성을 위한 Premium Storage][premium storage for greater performance predictability]입니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-104">Azure SQL Data Warehouse recently introduced [premium storage for greater performance predictability][premium storage for greater performance predictability].</span></span> <span data-ttu-id="d7aa0-105">이제 표준 저장소에 있는 기존 데이터 웨어하우스를 Premium Storage로 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-105">Existing data warehouses currently on standard storage can now be migrated to premium storage.</span></span> <span data-ttu-id="d7aa0-106">자동 마이그레이션을 활용하거나, 마이그레이션할 시기를 제어하려면(가동 중지 시간 포함) 직접 마이그레이션할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-106">You can take advantage of automatic migration, or if you prefer to control when to migrate (which does involve some downtime), you can do the migration yourself.</span></span>

<span data-ttu-id="d7aa0-107">둘 이상의 데이터 웨어하우스가 있는 경우 [자동 마이그레이션 일정][automatic migration schedule]을 사용하여 마이그레이션되는 시점을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-107">If you have more than one data warehouse, use the [automatic migration schedule][automatic migration schedule] to determine when it will also be migrated.</span></span>

## <a name="determine-storage-type"></a><span data-ttu-id="d7aa0-108">저장소 유형 결정</span><span class="sxs-lookup"><span data-stu-id="d7aa0-108">Determine storage type</span></span>
<span data-ttu-id="d7aa0-109">다음 날짜 이전에 데이터 웨어하우스를 생성한 경우 현재 표준 저장소를 사용하고 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-109">If you created a data warehouse before the following dates, you are currently using standard storage.</span></span>

| <span data-ttu-id="d7aa0-110">**지역**</span><span class="sxs-lookup"><span data-stu-id="d7aa0-110">**Region**</span></span> | <span data-ttu-id="d7aa0-111">**이 날짜 이전에 만든 데이터 웨어하우스**</span><span class="sxs-lookup"><span data-stu-id="d7aa0-111">**Data warehouse created before this date**</span></span> |
|:--- |:--- |
| <span data-ttu-id="d7aa0-112">오스트레일리아 동부</span><span class="sxs-lookup"><span data-stu-id="d7aa0-112">Australia East</span></span> |<span data-ttu-id="d7aa0-113">Premium Storage를 아직 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="d7aa0-113">Premium storage not yet available</span></span> |
| <span data-ttu-id="d7aa0-114">중국 동부</span><span class="sxs-lookup"><span data-stu-id="d7aa0-114">China East</span></span> |<span data-ttu-id="d7aa0-115">2016년 11월 1일</span><span class="sxs-lookup"><span data-stu-id="d7aa0-115">November 1, 2016</span></span> |
| <span data-ttu-id="d7aa0-116">중국 북부</span><span class="sxs-lookup"><span data-stu-id="d7aa0-116">China North</span></span> |<span data-ttu-id="d7aa0-117">2016년 11월 1일</span><span class="sxs-lookup"><span data-stu-id="d7aa0-117">November 1, 2016</span></span> |
| <span data-ttu-id="d7aa0-118">독일 중부</span><span class="sxs-lookup"><span data-stu-id="d7aa0-118">Germany Central</span></span> |<span data-ttu-id="d7aa0-119">2016년 11월 1일</span><span class="sxs-lookup"><span data-stu-id="d7aa0-119">November 1, 2016</span></span> |
| <span data-ttu-id="d7aa0-120">독일 북동부</span><span class="sxs-lookup"><span data-stu-id="d7aa0-120">Germany Northeast</span></span> |<span data-ttu-id="d7aa0-121">2016년 11월 1일</span><span class="sxs-lookup"><span data-stu-id="d7aa0-121">November 1, 2016</span></span> |
| <span data-ttu-id="d7aa0-122">인도 서부</span><span class="sxs-lookup"><span data-stu-id="d7aa0-122">India West</span></span> |<span data-ttu-id="d7aa0-123">Premium Storage를 아직 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="d7aa0-123">Premium storage not yet available</span></span> |
| <span data-ttu-id="d7aa0-124">일본 서부</span><span class="sxs-lookup"><span data-stu-id="d7aa0-124">Japan West</span></span> |<span data-ttu-id="d7aa0-125">Premium Storage를 아직 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="d7aa0-125">Premium storage not yet available</span></span> |
| <span data-ttu-id="d7aa0-126">미국 중북부</span><span class="sxs-lookup"><span data-stu-id="d7aa0-126">North Central US</span></span> |<span data-ttu-id="d7aa0-127">2016년 11월 10일</span><span class="sxs-lookup"><span data-stu-id="d7aa0-127">November 10, 2016</span></span> |

## <a name="automatic-migration-details"></a><span data-ttu-id="d7aa0-128">자동 마이그레이션 세부 정보</span><span class="sxs-lookup"><span data-stu-id="d7aa0-128">Automatic migration details</span></span>
<span data-ttu-id="d7aa0-129">기본적으로 [자동 마이그레이션 일정][automatic migration schedule] 동안 하위 지역의 현지 시간으로 오후 6시~오전 6시 동안 데이터를 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-129">By default, we will migrate your database for you between 6:00 PM and 6:00 AM in your region's local time during the [automatic migration schedule][automatic migration schedule].</span></span> <span data-ttu-id="d7aa0-130">마이그레이션하는 동안 기존 데이터 웨어하우스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-130">Your existing data warehouse will be unusable during the migration.</span></span> <span data-ttu-id="d7aa0-131">마이그레이션은 데이터 웨어하우스당 1TB의 저장소마다 약 1시간이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-131">The migration will take approximately one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="d7aa0-132">또한 자동 마이그레이션의 어느 부분에서도 비용이 청구되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-132">You will not be charged during any portion of the automatic migration.</span></span>

> [!NOTE]
> <span data-ttu-id="d7aa0-133">마이그레이션이 완료되면 데이터 웨어하우스는 다시 온라인 상태가 되어 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-133">When the migration is complete, your data warehouse will be back online and usable.</span></span>
>
>

<span data-ttu-id="d7aa0-134">Microsoft는 다음 단계에 따라 마이그레이션을 완료하며 사용자는 개입할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-134">Microsoft is taking the following steps to complete the migration (these do not require any involvement on your part).</span></span> <span data-ttu-id="d7aa0-135">이 예제에서는 표준 저장소의 기존 데이터 웨어하우스의 이름이 현재 "MyDW"라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-135">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="d7aa0-136">Microsoft는 "MyDW"를 "MyDW_DO_NOT_USE_[타임스탬프]"로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-136">Microsoft renames “MyDW” to “MyDW_DO_NOT_USE_[Timestamp].”</span></span>
2. <span data-ttu-id="d7aa0-137">Microsoft는 "MyDW_DO_NOT_USE_[타임스탬프]"를 일시 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-137">Microsoft pauses “MyDW_DO_NOT_USE_[Timestamp].”</span></span> <span data-ttu-id="d7aa0-138">이 시간 동안 백업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-138">During this time, a backup is taken.</span></span> <span data-ttu-id="d7aa0-139">이 과정에서 문제가 발생한 경우 여러 일시 중지 및 다시 시작이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-139">You may see multiple pauses and resumes if we encounter any issues during this process.</span></span>
3. <span data-ttu-id="d7aa0-140">Microsoft는 2단계에서 수행된 백업에서 Premium Storage에 "MyDW"라는 새 데이터 웨어하우스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-140">Microsoft creates a new data warehouse named “MyDW” on premium storage from the backup taken in step 2.</span></span> <span data-ttu-id="d7aa0-141">복원이 완료될 때까지 "MyDW"는 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-141">“MyDW” will not appear until after the restore is complete.</span></span>
4. <span data-ttu-id="d7aa0-142">복원이 완료되면 "MyDW"는 동일한 데이터 웨어하우스 단위 및 마이그레이션 이전 상태(일시 중지 또는 활성)로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-142">After the restore is complete, “MyDW” returns to the same data warehouse units and state (paused or active) that it was before the migration.</span></span>
5. <span data-ttu-id="d7aa0-143">마이그레이션이 완료되면 Microsoft는 "MyDW_DO_NOT_USE_[타임스탬프]"를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-143">After the migration is complete, Microsoft deletes “MyDW_DO_NOT_USE_[Timestamp]”.</span></span>

> [!NOTE]
> <span data-ttu-id="d7aa0-144">이러한 설정은 마이그레이션의 일부로 수행되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-144">The following settings do not carry over as part of the migration:</span></span>
>
> * <span data-ttu-id="d7aa0-145">데이터베이스 수준에서 감사를 다시 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-145">Auditing at the database level needs to be re-enabled.</span></span>
> * <span data-ttu-id="d7aa0-146">데이터베이스 수준에서 방화벽 규칙을 다시 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-146">Firewall rules at the database level need to be re-added.</span></span> <span data-ttu-id="d7aa0-147">서버 수준에서 방화벽 규칙은 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-147">Firewall rules at the server level are not affected.</span></span>
>
>

### <a name="automatic-migration-schedule"></a><span data-ttu-id="d7aa0-148">자동 마이그레이션 일정</span><span class="sxs-lookup"><span data-stu-id="d7aa0-148">Automatic migration schedule</span></span>
<span data-ttu-id="d7aa0-149">자동 마이그레이션은 다음 중단 일정 동안 오후 6시 - 오전 6시(하위 지역별 현지 시간)에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-149">Automatic migrations occur between 6:00 PM and 6:00 AM (local time per region) during the following outage schedule.</span></span>

| <span data-ttu-id="d7aa0-150">**지역**</span><span class="sxs-lookup"><span data-stu-id="d7aa0-150">**Region**</span></span> | <span data-ttu-id="d7aa0-151">**예상된 시작 날짜**</span><span class="sxs-lookup"><span data-stu-id="d7aa0-151">**Estimated start date**</span></span> | <span data-ttu-id="d7aa0-152">**예상된 종료 날짜**</span><span class="sxs-lookup"><span data-stu-id="d7aa0-152">**Estimated end date**</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d7aa0-153">오스트레일리아 동부</span><span class="sxs-lookup"><span data-stu-id="d7aa0-153">Australia East</span></span> |<span data-ttu-id="d7aa0-154">아직 결정되지 않음</span><span class="sxs-lookup"><span data-stu-id="d7aa0-154">Not determined yet</span></span> |<span data-ttu-id="d7aa0-155">아직 결정되지 않음</span><span class="sxs-lookup"><span data-stu-id="d7aa0-155">Not determined yet</span></span> |
| <span data-ttu-id="d7aa0-156">중국 동부</span><span class="sxs-lookup"><span data-stu-id="d7aa0-156">China East</span></span> |<span data-ttu-id="d7aa0-157">2017년 1월 9일</span><span class="sxs-lookup"><span data-stu-id="d7aa0-157">January 9, 2017</span></span> |<span data-ttu-id="d7aa0-158">2017년 1월 13일</span><span class="sxs-lookup"><span data-stu-id="d7aa0-158">January 13, 2017</span></span> |
| <span data-ttu-id="d7aa0-159">중국 북부</span><span class="sxs-lookup"><span data-stu-id="d7aa0-159">China North</span></span> |<span data-ttu-id="d7aa0-160">2017년 1월 9일</span><span class="sxs-lookup"><span data-stu-id="d7aa0-160">January 9, 2017</span></span> |<span data-ttu-id="d7aa0-161">2017년 1월 13일</span><span class="sxs-lookup"><span data-stu-id="d7aa0-161">January 13, 2017</span></span> |
| <span data-ttu-id="d7aa0-162">독일 중부</span><span class="sxs-lookup"><span data-stu-id="d7aa0-162">Germany Central</span></span> |<span data-ttu-id="d7aa0-163">2017년 1월 9일</span><span class="sxs-lookup"><span data-stu-id="d7aa0-163">January 9, 2017</span></span> |<span data-ttu-id="d7aa0-164">2017년 1월 13일</span><span class="sxs-lookup"><span data-stu-id="d7aa0-164">January 13, 2017</span></span> |
| <span data-ttu-id="d7aa0-165">독일 북동부</span><span class="sxs-lookup"><span data-stu-id="d7aa0-165">Germany Northeast</span></span> |<span data-ttu-id="d7aa0-166">2017년 1월 9일</span><span class="sxs-lookup"><span data-stu-id="d7aa0-166">January 9, 2017</span></span> |<span data-ttu-id="d7aa0-167">2017년 1월 13일</span><span class="sxs-lookup"><span data-stu-id="d7aa0-167">January 13, 2017</span></span> |
| <span data-ttu-id="d7aa0-168">인도 서부</span><span class="sxs-lookup"><span data-stu-id="d7aa0-168">India West</span></span> |<span data-ttu-id="d7aa0-169">아직 결정되지 않음</span><span class="sxs-lookup"><span data-stu-id="d7aa0-169">Not determined yet</span></span> |<span data-ttu-id="d7aa0-170">아직 결정되지 않음</span><span class="sxs-lookup"><span data-stu-id="d7aa0-170">Not determined yet</span></span> |
| <span data-ttu-id="d7aa0-171">일본 서부</span><span class="sxs-lookup"><span data-stu-id="d7aa0-171">Japan West</span></span> |<span data-ttu-id="d7aa0-172">아직 결정되지 않음</span><span class="sxs-lookup"><span data-stu-id="d7aa0-172">Not determined yet</span></span> |<span data-ttu-id="d7aa0-173">아직 결정되지 않음</span><span class="sxs-lookup"><span data-stu-id="d7aa0-173">Not determined yet</span></span> |
| <span data-ttu-id="d7aa0-174">미국 중북부</span><span class="sxs-lookup"><span data-stu-id="d7aa0-174">North Central US</span></span> |<span data-ttu-id="d7aa0-175">2017년 1월 9일</span><span class="sxs-lookup"><span data-stu-id="d7aa0-175">January 9, 2017</span></span> |<span data-ttu-id="d7aa0-176">2017년 1월 13일</span><span class="sxs-lookup"><span data-stu-id="d7aa0-176">January 13, 2017</span></span> |

## <a name="self-migration-to-premium-storage"></a><span data-ttu-id="d7aa0-177">Premium Storage로 자체 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="d7aa0-177">Self-migration to premium storage</span></span>
<span data-ttu-id="d7aa0-178">가동 중지가 발생하는 시간을 제어하려는 경우 아래 단계를 사용하여 표준 저장소의 기존 데이터 웨어하우스를 Premium Storage로 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-178">If you want to control when your downtime will occur, you can use the following steps to migrate an existing data warehouse on standard storage to premium storage.</span></span> <span data-ttu-id="d7aa0-179">이 옵션을 선택하면 해당 하위 지역에서 자동 마이그레이션을 시작하기 전에 자체 마이그레이션을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-179">If you choose this option, you must complete the self-migration before the automatic migration begins in that region.</span></span> <span data-ttu-id="d7aa0-180">이렇게 하면 자동 마이그레이션이 충돌할 위험을 피할 수 있습니다([자동 마이그레이션 일정][automatic migration schedule] 참조).</span><span class="sxs-lookup"><span data-stu-id="d7aa0-180">This ensures that you avoid any risk of the automatic migration causing a conflict (refer to the [automatic migration schedule][automatic migration schedule]).</span></span>

### <a name="self-migration-instructions"></a><span data-ttu-id="d7aa0-181">자체 마이그레이션 지침</span><span class="sxs-lookup"><span data-stu-id="d7aa0-181">Self-migration instructions</span></span>
<span data-ttu-id="d7aa0-182">데이터 웨어하우스를 직접 마이그레이션하려면 백업 및 복원 기능을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-182">To migrate your data warehouse yourself, use the backup and restore features.</span></span> <span data-ttu-id="d7aa0-183">마이그레이션의 복원 부분은 데이터 웨어하우스당 1TB 저장소마다 약 1시간 정도가 소요될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-183">The restore portion of the migration is expected to take around one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="d7aa0-184">마이그레이션이 완료된 후 동일한 이름을 유지하려는 경우 [마이그레이션 중에 이름을 바꾸기 위한 단계][steps to rename during migration]를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-184">If you want to keep the same name after migration is complete, follow the [steps to rename during migration][steps to rename during migration].</span></span>

1. <span data-ttu-id="d7aa0-185">데이터 웨어하우스를 [일시 중지][Pause]합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-185">[Pause][Pause] your data warehouse.</span></span> <span data-ttu-id="d7aa0-186">자동 백업이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-186">This takes an automatic backup.</span></span>
2. <span data-ttu-id="d7aa0-187">가장 최근의 스냅숏에서 [복원][Restore]합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-187">[Restore][Restore] from your most recent snapshot.</span></span>
3. <span data-ttu-id="d7aa0-188">표준 저장소의 기존 데이터 웨어하우스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-188">Delete your existing data warehouse on standard storage.</span></span> <span data-ttu-id="d7aa0-189">**이 단계의 수행에 실패하면 두 데이터 웨어하우스에 대해 비용이 청구됩니다.**</span><span class="sxs-lookup"><span data-stu-id="d7aa0-189">**If you fail to do this step, you will be charged for both data warehouses.**</span></span>

> [!NOTE]
> <span data-ttu-id="d7aa0-190">이러한 설정은 마이그레이션의 일부로 수행되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-190">The following settings do not carry over as part of the migration:</span></span>
>
> * <span data-ttu-id="d7aa0-191">데이터베이스 수준에서 감사를 다시 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-191">Auditing at the database level needs to be re-enabled.</span></span>
> * <span data-ttu-id="d7aa0-192">데이터베이스 수준에서 방화벽 규칙을 다시 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-192">Firewall rules at the database level need to be re-added.</span></span> <span data-ttu-id="d7aa0-193">서버 수준에서 방화벽 규칙은 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-193">Firewall rules at the server level are not affected.</span></span>
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a><span data-ttu-id="d7aa0-194">마이그레이션 중 데이터 웨어하우스의 이름 바꾸기(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="d7aa0-194">Rename data warehouse during migration (optional)</span></span>
<span data-ttu-id="d7aa0-195">동일한 논리 서버의 두 개의 데이터베이스는 동일한 이름을 가질 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-195">Two databases on the same logical server cannot have the same name.</span></span> <span data-ttu-id="d7aa0-196">이제 SQL Data Warehouse는 데이터 웨어하우스 이름 바꾸기 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-196">SQL Data Warehouse now supports the ability to rename a data warehouse.</span></span>

<span data-ttu-id="d7aa0-197">이 예제에서는 표준 저장소의 기존 데이터 웨어하우스의 이름이 현재 "MyDW"라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-197">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="d7aa0-198">다음 ALTER DATABASE 명령을 사용하여 "MyDW"를 다른 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-198">Rename "MyDW" by using the following ALTER DATABASE command.</span></span> <span data-ttu-id="d7aa0-199">(이 예제에서는 "MyDW_BeforeMigration"으로 이름을 지정합니다.) 이 명령은 기존 트랜잭션을 모두 중지하며, 작업 성공을 위해 master 데이터베이스에서 수행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-199">(In this example, we'll rename it "MyDW_BeforeMigration.")  This command stops all existing transactions, and must be done in the master database to succeed.</span></span>
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. <span data-ttu-id="d7aa0-200">"MyDW_BeforeMigration"을 [일시 중지][Pause]합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-200">[Pause][Pause] "MyDW_BeforeMigration."</span></span> <span data-ttu-id="d7aa0-201">자동 백업이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-201">This takes an automatic backup.</span></span>
3. <span data-ttu-id="d7aa0-202">가장 최근의 스냅숏에서 이전 이름(예: "MyDW")을 갖는 새 데이터베이스로 [복원][Restore]합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-202">[Restore][Restore] from your most recent snapshot a new database with the name it used to be (for example, "MyDW").</span></span>
4. <span data-ttu-id="d7aa0-203">"MyDW_BeforeMigration"을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-203">Delete "MyDW_BeforeMigration."</span></span> <span data-ttu-id="d7aa0-204">**이 단계의 수행에 실패하면 두 데이터 웨어하우스에 대해 비용이 청구됩니다.**</span><span class="sxs-lookup"><span data-stu-id="d7aa0-204">**If you fail to do this step, you will be charged for both data warehouses.**</span></span>


## <a name="next-steps"></a><span data-ttu-id="d7aa0-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d7aa0-205">Next steps</span></span>
<span data-ttu-id="d7aa0-206">Premium Storage로 변경하여 데이터 웨어하우스의 기반 아키텍처에서 데이터베이스 blob 파일 수도 증가시켰습니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-206">With the change to premium storage, you also have an increased number of database blob files in the underlying architecture of your data warehouse.</span></span> <span data-ttu-id="d7aa0-207">이 변경을 통해 성능을 최대한 개선하려면 다음 스크립트를 사용하여 클러스터형 columnstore 인덱스를 다시 작성하세요.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-207">To maximize the performance benefits of this change, rebuild your clustered columnstore indexes by using the following script.</span></span> <span data-ttu-id="d7aa0-208">이 스크립트는 일부 기존 데이터를 추가 Blob에 강제로 적용하여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-208">The script works by forcing some of your existing data to the additional blobs.</span></span> <span data-ttu-id="d7aa0-209">아무 작업도 하지 않으면 자연스럽게 시간이 지나면서 테이블에 더 많은 데이터를 로드함에 따라 데이터가 재배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-209">If you take no action, the data will naturally redistribute over time as you load more data into your tables.</span></span>

<span data-ttu-id="d7aa0-210">**필수 조건:**</span><span class="sxs-lookup"><span data-stu-id="d7aa0-210">**Prerequisites:**</span></span>

- <span data-ttu-id="d7aa0-211">데이터 웨어하우스를 1,000개 이상의 데이터 웨어하우스 단위로 실행해야 합니다([계산 능력 크기 조정][scale compute power] 참조).</span><span class="sxs-lookup"><span data-stu-id="d7aa0-211">The data warehouse should run with 1,000 data warehouse units or higher (see [scale compute power][scale compute power]).</span></span>
- <span data-ttu-id="d7aa0-212">스크립트를 실행하는 사용자가 [mediumrc 역할][mediumrc role] 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-212">The user executing the script should be in the [mediumrc role][mediumrc role] or higher.</span></span> <span data-ttu-id="d7aa0-213">이 역할에 사용자를 추가하려면 다음을 실행합니다. ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span><span class="sxs-lookup"><span data-stu-id="d7aa0-213">To add a user to this role, execute the following: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span></span>

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table to control index rebuild
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
-- Step 2: Execute index rebuilds. If script fails, the below can be re-run to restart where last left off.
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

<span data-ttu-id="d7aa0-214">데이터 웨어하우스에 문제가 발생하는 경우 [지원 티켓을 만들고][create a support ticket] 가능한 원인으로 "Premium Storage로 마이그레이션"을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7aa0-214">If you encounter any issues with your data warehouse, [create a support ticket][create a support ticket] and reference “migration to premium storage” as the possible cause.</span></span>

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration to Premium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps to rename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com

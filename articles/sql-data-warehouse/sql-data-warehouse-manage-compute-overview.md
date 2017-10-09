---
title: "aaaManage 계산 능력이 Azure SQL 데이터 웨어하우스에 (개요) | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스의 성능 확장 기능입니다. Dwu로 조정 하 여 수평 확장 또는 일시 중지 하 고 계산 리소스 toosave 비용이 다시 시작 합니다."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: 1ffbe8d694ac181eaeb6f585a2cee87a570ed7d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a><span data-ttu-id="c8c1e-104">Azure SQL 데이터 웨어하우스의 계산 능력 관리(개요)</span><span class="sxs-lookup"><span data-stu-id="c8c1e-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c8c1e-105">개요</span><span class="sxs-lookup"><span data-stu-id="c8c1e-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="c8c1e-106">포털</span><span class="sxs-lookup"><span data-stu-id="c8c1e-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="c8c1e-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8c1e-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="c8c1e-108">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="c8c1e-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="c8c1e-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="c8c1e-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<span data-ttu-id="c8c1e-110">SQL 데이터 웨어하우스의 hello 아키텍처는 저장소 및 계산의 경우, 각 tooscale를 독립적으로 허용 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-110">hello architecture of SQL Data Warehouse separates storage and compute, allowing each tooscale independently.</span></span> <span data-ttu-id="c8c1e-111">따라서 계산 크기 조정 된 toomeet 성능 요구가 hello 양의 데이터와 무관 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-111">As a result, compute can be scaled toomeet performance demands independent of hello amount of data.</span></span> <span data-ttu-id="c8c1e-112">이 아키텍처의 자연스러운 결과는 계산 및 저장소에 대한 [청구][billed]가 분리되어 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span></span> 

<span data-ttu-id="c8c1e-113">이 개요에서는 설명 작동 하는 SQL 데이터 웨어하우스 및 일시 중지, 다시 시작할 때 및 SQL 데이터 웨어하우스의 확장 기능 tooutilize hello 하는 방법을 어떻게 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-113">This overview describes how scale out works with SQL Data Warehouse and how tooutilize hello pause, resume, and scale capabilities of SQL Data Warehouse.</span></span> <span data-ttu-id="c8c1e-114">Hello 참조 [데이터 웨어하우스 단위 (Dwu)] [ data warehouse units (DWUs)] 페이지 toolearn Dwu와 성능 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-114">Consult hello [data warehouse units (DWUs)][data warehouse units (DWUs)] page toolearn how DWUs and performance are related.</span></span> 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a><span data-ttu-id="c8c1e-115">SQL Data Warehouse에서 계산 관리 작업이 작동하는 방법</span><span class="sxs-lookup"><span data-stu-id="c8c1e-115">How compute management operations work in SQL Data Warehouse</span></span>
<span data-ttu-id="c8c1e-116">SQL 데이터 웨어하우스에 대 한 hello 아키텍처 제어 노드로, 노드 및 hello 저장소 계층 60 분포에 분산을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-116">hello architecture for SQL Data Warehouse consists of a control node, compute nodes, and hello storage layer spread across 60 distributions.</span></span> 

<span data-ttu-id="c8c1e-117">SQL 데이터 웨어하우스에 일반 활성 세션 중에 시스템의 헤드 노드 hello 메타 데이터를 관리 하 고 hello 분산 쿼리 최적화 프로그램을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-117">During a normal active session in SQL Data Warehouse, your system's head node manages hello metadata and contains hello distributed query optimizer.</span></span> <span data-ttu-id="c8c1e-118">이 헤드 노드 아래에는 계산 노드와 저장소 계층이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-118">Beneath this head node are your compute nodes and your storage layer.</span></span> <span data-ttu-id="c8c1e-119">DWU 400의 경우 시스템에 헤드 노드, 4 개의 계산 노드 및 hello 저장소 계층에서 60 배포로 구성 된 하나의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-119">For a DWU 400, your system has one head node, four compute nodes, and hello storage layer, consisting of 60 distributions.</span></span> 

<span data-ttu-id="c8c1e-120">소수 자릿수를 진행 하거나 작업을 일시 중지 hello 시스템 먼저 모든 수신 쿼리를 중지 및 롤백됩니다 트랜잭션을 tooensure 일관 된 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-120">When you undergo a scale or pause operation, hello system first kills all incoming queries and then rolls back transactions tooensure a consistent state.</span></span> <span data-ttu-id="c8c1e-121">크기 조정 작업의 경우 이 트랜잭션 롤백을 완료한 후에만 크기 조정이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span></span> <span data-ttu-id="c8c1e-122">스케일 업 작업에 대 한 hello 시스템 규정 extra 원하는 계산 노드 수를 hello 하 고 hello 계산 노드 toohello 저장소 계층을 다시 연결을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-122">For a scale-up operation, hello system provisions hello extra desired number of compute nodes, and then begins reattaching hello compute nodes toohello storage layer.</span></span> <span data-ttu-id="c8c1e-123">축소 작업에 대 한 hello 불필요 한 노드 해제 되 고 나머지 계산 노드 hello 다시 toohello 적절 한 개수의 배포 첨부 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-123">For a scale-down operation, hello unneeded nodes are released and hello remaining compute nodes reattach themselves toohello appropriate number of distributions.</span></span> <span data-ttu-id="c8c1e-124">일시 중지 작업에 대 한 모든 계산 노드 해제 되 고 시스템 다양 한 메타 데이터 작업 tooleave 안정 된 상태가 최종 시스템 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations tooleave your final system in a stable state.</span></span>

| <span data-ttu-id="c8c1e-125">DWU</span><span class="sxs-lookup"><span data-stu-id="c8c1e-125">DWU</span></span>  | <span data-ttu-id="c8c1e-126">계산 노드 수 \#</span><span class="sxs-lookup"><span data-stu-id="c8c1e-126">\#of compute nodes</span></span> | <span data-ttu-id="c8c1e-127">노드당 배포 수 \#</span><span class="sxs-lookup"><span data-stu-id="c8c1e-127">\# of distributions per node</span></span> |
| ---- | ------------------ | ---------------------------- |
| <span data-ttu-id="c8c1e-128">100</span><span class="sxs-lookup"><span data-stu-id="c8c1e-128">100</span></span>  | <span data-ttu-id="c8c1e-129">1</span><span class="sxs-lookup"><span data-stu-id="c8c1e-129">1</span></span>                  | <span data-ttu-id="c8c1e-130">60</span><span class="sxs-lookup"><span data-stu-id="c8c1e-130">60</span></span>                           |
| <span data-ttu-id="c8c1e-131">200</span><span class="sxs-lookup"><span data-stu-id="c8c1e-131">200</span></span>  | <span data-ttu-id="c8c1e-132">2</span><span class="sxs-lookup"><span data-stu-id="c8c1e-132">2</span></span>                  | <span data-ttu-id="c8c1e-133">30</span><span class="sxs-lookup"><span data-stu-id="c8c1e-133">30</span></span>                           |
| <span data-ttu-id="c8c1e-134">300</span><span class="sxs-lookup"><span data-stu-id="c8c1e-134">300</span></span>  | <span data-ttu-id="c8c1e-135">3</span><span class="sxs-lookup"><span data-stu-id="c8c1e-135">3</span></span>                  | <span data-ttu-id="c8c1e-136">20</span><span class="sxs-lookup"><span data-stu-id="c8c1e-136">20</span></span>                           |
| <span data-ttu-id="c8c1e-137">400</span><span class="sxs-lookup"><span data-stu-id="c8c1e-137">400</span></span>  | <span data-ttu-id="c8c1e-138">4</span><span class="sxs-lookup"><span data-stu-id="c8c1e-138">4</span></span>                  | <span data-ttu-id="c8c1e-139">15</span><span class="sxs-lookup"><span data-stu-id="c8c1e-139">15</span></span>                           |
| <span data-ttu-id="c8c1e-140">500</span><span class="sxs-lookup"><span data-stu-id="c8c1e-140">500</span></span>  | <span data-ttu-id="c8c1e-141">5</span><span class="sxs-lookup"><span data-stu-id="c8c1e-141">5</span></span>                  | <span data-ttu-id="c8c1e-142">12</span><span class="sxs-lookup"><span data-stu-id="c8c1e-142">12</span></span>                           |
| <span data-ttu-id="c8c1e-143">600</span><span class="sxs-lookup"><span data-stu-id="c8c1e-143">600</span></span>  | <span data-ttu-id="c8c1e-144">6</span><span class="sxs-lookup"><span data-stu-id="c8c1e-144">6</span></span>                  | <span data-ttu-id="c8c1e-145">10</span><span class="sxs-lookup"><span data-stu-id="c8c1e-145">10</span></span>                           |
| <span data-ttu-id="c8c1e-146">1000</span><span class="sxs-lookup"><span data-stu-id="c8c1e-146">1000</span></span> | <span data-ttu-id="c8c1e-147">10</span><span class="sxs-lookup"><span data-stu-id="c8c1e-147">10</span></span>                 | <span data-ttu-id="c8c1e-148">6</span><span class="sxs-lookup"><span data-stu-id="c8c1e-148">6</span></span>                            |
| <span data-ttu-id="c8c1e-149">1200</span><span class="sxs-lookup"><span data-stu-id="c8c1e-149">1200</span></span> | <span data-ttu-id="c8c1e-150">12</span><span class="sxs-lookup"><span data-stu-id="c8c1e-150">12</span></span>                 | <span data-ttu-id="c8c1e-151">5</span><span class="sxs-lookup"><span data-stu-id="c8c1e-151">5</span></span>                            |
| <span data-ttu-id="c8c1e-152">1500</span><span class="sxs-lookup"><span data-stu-id="c8c1e-152">1500</span></span> | <span data-ttu-id="c8c1e-153">15</span><span class="sxs-lookup"><span data-stu-id="c8c1e-153">15</span></span>                 | <span data-ttu-id="c8c1e-154">4</span><span class="sxs-lookup"><span data-stu-id="c8c1e-154">4</span></span>                            |
| <span data-ttu-id="c8c1e-155">2000</span><span class="sxs-lookup"><span data-stu-id="c8c1e-155">2000</span></span> | <span data-ttu-id="c8c1e-156">20</span><span class="sxs-lookup"><span data-stu-id="c8c1e-156">20</span></span>                 | <span data-ttu-id="c8c1e-157">3</span><span class="sxs-lookup"><span data-stu-id="c8c1e-157">3</span></span>                            |
| <span data-ttu-id="c8c1e-158">3000</span><span class="sxs-lookup"><span data-stu-id="c8c1e-158">3000</span></span> | <span data-ttu-id="c8c1e-159">30</span><span class="sxs-lookup"><span data-stu-id="c8c1e-159">30</span></span>                 | <span data-ttu-id="c8c1e-160">2</span><span class="sxs-lookup"><span data-stu-id="c8c1e-160">2</span></span>                            |
| <span data-ttu-id="c8c1e-161">6000</span><span class="sxs-lookup"><span data-stu-id="c8c1e-161">6000</span></span> | <span data-ttu-id="c8c1e-162">60</span><span class="sxs-lookup"><span data-stu-id="c8c1e-162">60</span></span>                 | <span data-ttu-id="c8c1e-163">1</span><span class="sxs-lookup"><span data-stu-id="c8c1e-163">1</span></span>                            |

<span data-ttu-id="c8c1e-164">hello 계산을 관리 하기 위한 세 가지 주요 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-164">hello three primary functions for managing compute are:</span></span>

1. <span data-ttu-id="c8c1e-165">일시 중지</span><span class="sxs-lookup"><span data-stu-id="c8c1e-165">Pause</span></span>
2. <span data-ttu-id="c8c1e-166">다시 시작</span><span class="sxs-lookup"><span data-stu-id="c8c1e-166">Resume</span></span>
3. <span data-ttu-id="c8c1e-167">확장</span><span class="sxs-lookup"><span data-stu-id="c8c1e-167">Scale</span></span>

<span data-ttu-id="c8c1e-168">이러한 각 작업 몇 분 toocomplete를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-168">Each of these operations may take several minutes toocomplete.</span></span> <span data-ttu-id="c8c1e-169">자동 크기 조정/일시 중지/재개 됩니다 tooimplement 논리 tooensure 특정 작업이 다른 작업을 진행 하기 전에 완료 된 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-169">If you are scaling/pausing/resuming automatically, you may want tooimplement logic tooensure that certain operations have been completed before proceeding with another action.</span></span> 

<span data-ttu-id="c8c1e-170">다양 한 끝점을 통해 hello 데이터베이스 상태를 확인 하는 중 이러한 작업의 구현 자동화 toocorrectly 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-170">Checking hello database state through various endpoints will allow you toocorrectly implement automation of such operations.</span></span> <span data-ttu-id="c8c1e-171">hello 포털은는 작업과 hello 데이터베이스 현재 상태가 완료 될 때 알림을 제공 되었지만 상태를 프로그래밍 방식으로 검사에 대 한 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-171">hello portal will provide notification upon completion of an operation and hello databases current state but does not allow for programmatic checking of state.</span></span> 

>  [!NOTE]
>
>  <span data-ttu-id="c8c1e-172">모든 끝점에 대한 계산 관리 기능은 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-172">Compute management functionality does not exist across all endpoints.</span></span>
>
>  

|              | <span data-ttu-id="c8c1e-173">일시 중지/다시 시작</span><span class="sxs-lookup"><span data-stu-id="c8c1e-173">Pause/Resume</span></span> | <span data-ttu-id="c8c1e-174">확장</span><span class="sxs-lookup"><span data-stu-id="c8c1e-174">Scale</span></span> | <span data-ttu-id="c8c1e-175">데이터베이스 상태 확인</span><span class="sxs-lookup"><span data-stu-id="c8c1e-175">Check database state</span></span> |
| ------------ | ------------ | ----- | -------------------- |
| <span data-ttu-id="c8c1e-176">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="c8c1e-176">Azure portal</span></span> | <span data-ttu-id="c8c1e-177">예</span><span class="sxs-lookup"><span data-stu-id="c8c1e-177">Yes</span></span>          | <span data-ttu-id="c8c1e-178">예</span><span class="sxs-lookup"><span data-stu-id="c8c1e-178">Yes</span></span>   | <span data-ttu-id="c8c1e-179">**아니요**</span><span class="sxs-lookup"><span data-stu-id="c8c1e-179">**No**</span></span>               |
| <span data-ttu-id="c8c1e-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8c1e-180">PowerShell</span></span>   | <span data-ttu-id="c8c1e-181">예</span><span class="sxs-lookup"><span data-stu-id="c8c1e-181">Yes</span></span>          | <span data-ttu-id="c8c1e-182">예</span><span class="sxs-lookup"><span data-stu-id="c8c1e-182">Yes</span></span>   | <span data-ttu-id="c8c1e-183">예</span><span class="sxs-lookup"><span data-stu-id="c8c1e-183">Yes</span></span>                  |
| <span data-ttu-id="c8c1e-184">REST API</span><span class="sxs-lookup"><span data-stu-id="c8c1e-184">REST API</span></span>     | <span data-ttu-id="c8c1e-185">예</span><span class="sxs-lookup"><span data-stu-id="c8c1e-185">Yes</span></span>          | <span data-ttu-id="c8c1e-186">예</span><span class="sxs-lookup"><span data-stu-id="c8c1e-186">Yes</span></span>   | <span data-ttu-id="c8c1e-187">예</span><span class="sxs-lookup"><span data-stu-id="c8c1e-187">Yes</span></span>                  |
| <span data-ttu-id="c8c1e-188">T-SQL</span><span class="sxs-lookup"><span data-stu-id="c8c1e-188">T-SQL</span></span>        | <span data-ttu-id="c8c1e-189">**아니요**</span><span class="sxs-lookup"><span data-stu-id="c8c1e-189">**No**</span></span>       | <span data-ttu-id="c8c1e-190">예</span><span class="sxs-lookup"><span data-stu-id="c8c1e-190">Yes</span></span>   | <span data-ttu-id="c8c1e-191">예</span><span class="sxs-lookup"><span data-stu-id="c8c1e-191">Yes</span></span>                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="c8c1e-192">계산 조정</span><span class="sxs-lookup"><span data-stu-id="c8c1e-192">Scale compute</span></span>

<span data-ttu-id="c8c1e-193">SQL Data Warehouse의 성능은 CPU, 메모리 및 I/O 대역폭과 같은 계산 리소스를 추상화한 측정값인 [DWU(데이터 웨어하우스 단위)][data warehouse units (DWUs)]로 측정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="c8c1e-194">시스템 성능 tooscale 하려는 사용자는 이렇게 하려면 다양 한 방법을 통해와 같은 hello 포털과 T-SQL, REST Api를 통해 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-194">A user who wishes tooscale their system's performance can do so through various means, such as through hello portal, T-SQL, and REST APIs.</span></span> 

### <a name="how-do-i-scale-compute"></a><span data-ttu-id="c8c1e-195">계산 크기는 어떻게 조정합니까?</span><span class="sxs-lookup"><span data-stu-id="c8c1e-195">How do I scale compute?</span></span>
<span data-ttu-id="c8c1e-196">전원 관리 되 SQL 데이터 웨어하우스 hello DWU 설정을 변경 하 여 계산 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-196">Compute power is managed for you SQL Data Warehouse by changing hello DWU setting.</span></span> <span data-ttu-id="c8c1e-197">특정 작업에 대해 DWU를 더 많이 추가하면 성능이 [선형적으로][linearly] 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span></span>  <span data-ttu-id="c8c1e-198">시스템을 강화하거나 축소할 때 성능이 눈에 띄게 변경되는 DWU 제품을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span></span> 

<span data-ttu-id="c8c1e-199">Dwu tooadjust 개별 이러한 방법 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-199">tooadjust DWUs, you can use any of these individual methods.</span></span>

* <span data-ttu-id="c8c1e-200">[Azure Portal을 사용하여 계산 능력 조정][Scale compute power with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="c8c1e-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span></span>
* <span data-ttu-id="c8c1e-201">[PowerShell을 사용하여 계산 능력 조정][Scale compute power with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="c8c1e-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span></span>
* <span data-ttu-id="c8c1e-202">[REST API를 사용하여 계산 능력 조정][Scale compute power with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="c8c1e-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span></span>
* <span data-ttu-id="c8c1e-203">[TSQL을 사용하여 계산 능력 조정][Scale compute power with TSQL]</span><span class="sxs-lookup"><span data-stu-id="c8c1e-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span></span>

### <a name="how-many-dwus-should-i-use"></a><span data-ttu-id="c8c1e-204">얼마나 많은 DWU를 사용해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="c8c1e-204">How many DWUs should I use?</span></span>

<span data-ttu-id="c8c1e-205">toounderstand 어떤 사용자가 이상적인 DWU 값은 위와 아래로 확장 하 고 데이터를 로드 한 후 몇 가지 쿼리를 실행 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-205">toounderstand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span></span> <span data-ttu-id="c8c1e-206">크기 조정이 빠르기 때문에 1시간 이내에 다양한 성능 수준을 시험해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-206">Since scaling is quick, you can try various performance levels in an hour or less.</span></span> 

> [!Note] 
> <span data-ttu-id="c8c1e-207">SQL 데이터 웨어하우스는 많은 양의 데이터를 설계 된 tooprocess 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-207">SQL Data Warehouse is designed tooprocess large amounts of data.</span></span> <span data-ttu-id="c8c1e-208">toosee 특히 큰 Dwu에서 크기 조정에 대 한 실제 성능이 원하는 toouse에 도달 하거나 1TB를 초과 하는 큰 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-208">toosee its true capabilities for scaling, especially at larger DWUs, you want toouse a large data set which approaches or exceeds 1 TB.</span></span>

<span data-ttu-id="c8c1e-209">찾기에 대 한 권장 작업에 대 한 최상의 DWU hello:</span><span class="sxs-lookup"><span data-stu-id="c8c1e-209">Recommendations for finding hello best DWU for your workload:</span></span>

1. <span data-ttu-id="c8c1e-210">개발 중인 데이터 웨어하우스의 경우 먼저 낮은 DWU 성능 수준을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span></span>  <span data-ttu-id="c8c1e-211">적합한 시작 지점은 DW400 또는 DW200입니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-211">A good starting point is DW400 or DW200.</span></span>
2. <span data-ttu-id="c8c1e-212">응용 프로그램 성능 모니터링, 관찰 하기 toohello 성능 비교 hello 수가 선택한 Dwu 관찰 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-212">Monitor your application performance, observing hello number of DWUs selected compared toohello performance you observe.</span></span>
3. <span data-ttu-id="c8c1e-213">결정 양을 빠르거나 늦게 성능 수준에 대 한 있습니다 tooreach hello 최적의 성능 요구 사항에 대 한 선형 눈금을 가정 하 여.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-213">Determine how much faster or slower performance should be for you tooreach hello optimum performance level for your requirements by assuming linear scale.</span></span>
4. <span data-ttu-id="c8c1e-214">Hello 수를 늘리거나 작업 tooperform 비율 toohow 훨씬 빠르거나 늦게에 dwu로의 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-214">Increase or decrease hello number of DWUs in proportion toohow much faster or slower you want your workload tooperform.</span></span> 
5. <span data-ttu-id="c8c1e-215">비즈니스 요구 사항에 맞는 최적 성능 수준에 도달할 때까지 계속 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c8c1e-216">만 쿼리 성능을 hello 작업 계산 노드 간에 분할 될 수 있습니다 하는 경우 더 많은 병렬화에 따라 카운터가 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-216">Query performance only increases with more parallelization if hello work can be split between compute nodes.</span></span> <span data-ttu-id="c8c1e-217">확장 하면 성능이 변경 되지 않는 경우 데이터 균일 하지 않게 배포 여부 또는 많은 양의 데이터 이동을 도입 하는 경우 문서 toocheck 튜닝 우리의 성능을 모색 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-217">If you find that scaling is not changing your performance, please check out our performance tuning articles toocheck whether your data is unevenly distributed or if you are introducing a large amount of data movement.</span></span> 

### <a name="when-should-i-scale-dwus"></a><span data-ttu-id="c8c1e-218">언제 DWU를 조정해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="c8c1e-218">When should I scale DWUs?</span></span>
<span data-ttu-id="c8c1e-219">다음 중요 한 시나리오 hello 변경 dwu로 확장:</span><span class="sxs-lookup"><span data-stu-id="c8c1e-219">Scaling DWUs alters hello following important scenarios:</span></span>

1. <span data-ttu-id="c8c1e-220">선형 검색, 집계 및 CTAS에는 문을 실행 하는 것에 대 한 hello 시스템의 성능을 변경</span><span class="sxs-lookup"><span data-stu-id="c8c1e-220">Linearly changing performance of hello system for scans, aggregations, and CTAS statements</span></span>
2. <span data-ttu-id="c8c1e-221">Polybase를 로드할 때 판독기 및 작성기 hello 수를 늘리면</span><span class="sxs-lookup"><span data-stu-id="c8c1e-221">Increasing hello number of readers and writers when loading with PolyBase</span></span>
3. <span data-ttu-id="c8c1e-222">동시 쿼리 및 동시성 슬롯의 최대 수</span><span class="sxs-lookup"><span data-stu-id="c8c1e-222">Maximum number of concurrent queries and concurrency slots</span></span>

<span data-ttu-id="c8c1e-223">좋은 경우 tooscale dwu로:</span><span class="sxs-lookup"><span data-stu-id="c8c1e-223">Recommendations for when tooscale DWUs:</span></span>

1. <span data-ttu-id="c8c1e-224">대량의 데이터 로딩 또는 변환 작업을 수행하기 전에 데이터를 더욱 빠르게 사용할 수 있도록 DWU를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span></span>
2. <span data-ttu-id="c8c1e-225">최대 업무 시간 동안 tooaccommodate 다 수의 동시 쿼리를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-225">During peak business hours, scale tooaccommodate larger numbers of concurrent queries.</span></span> 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="c8c1e-226">계산 일시 중지</span><span class="sxs-lookup"><span data-stu-id="c8c1e-226">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="c8c1e-227">데이터베이스 toopause 개별 이러한 방법 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-227">toopause a database, use any of these individual methods.</span></span>

* <span data-ttu-id="c8c1e-228">[Azure Portal을 사용하여 계산 일시 중지][Pause compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="c8c1e-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span></span>
* <span data-ttu-id="c8c1e-229">[PowerShell을 사용하여 계산 일시 중지][Pause compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="c8c1e-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span></span>
* <span data-ttu-id="c8c1e-230">[REST API를 사용하여 계산 일시 중지][Pause compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="c8c1e-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span></span>

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="c8c1e-231">계산 다시 시작</span><span class="sxs-lookup"><span data-stu-id="c8c1e-231">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="c8c1e-232">데이터베이스 tooresume 개별 이러한 방법 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-232">tooresume a database, use any of these individual methods.</span></span>

* <span data-ttu-id="c8c1e-233">[Azure Portal을 사용하여 계산 다시 시작][Resume compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="c8c1e-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span></span>
* <span data-ttu-id="c8c1e-234">[PowerShell을 사용하여 계산 다시 시작][Resume compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="c8c1e-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span></span>
* <span data-ttu-id="c8c1e-235">[REST API를 사용하여 계산 다시 시작][Resume compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="c8c1e-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span></span>

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="c8c1e-236">데이터베이스 상태 확인</span><span class="sxs-lookup"><span data-stu-id="c8c1e-236">Check database state</span></span> 

<span data-ttu-id="c8c1e-237">데이터베이스 tooresume 개별 이러한 방법 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-237">tooresume a database, use any of these individual methods.</span></span>

- <span data-ttu-id="c8c1e-238">[T-SQL을 사용하여 데이터베이스 상태 확인][Check database state with T-SQL]</span><span class="sxs-lookup"><span data-stu-id="c8c1e-238">[Check database state with T-SQL][Check database state with T-SQL]</span></span>
- <span data-ttu-id="c8c1e-239">[PowerShell을 사용하여 데이터베이스 상태 확인][Check database state with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="c8c1e-239">[Check database state with PowerShell][Check database state with PowerShell]</span></span>
- <span data-ttu-id="c8c1e-240">[REST API를 사용하여 데이터베이스 상태 확인][Check database state with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="c8c1e-240">[Check database state with REST APIs][Check database state with REST APIs]</span></span>

## <a name="permissions"></a><span data-ttu-id="c8c1e-241">권한</span><span class="sxs-lookup"><span data-stu-id="c8c1e-241">Permissions</span></span>

<span data-ttu-id="c8c1e-242">크기 조정 hello 데이터베이스에서 설명 하는 hello 사용 권한이 필요 [ALTER DATABASE][ALTER DATABASE]합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-242">Scaling hello database requires hello permissions described in [ALTER DATABASE][ALTER DATABASE].</span></span>  <span data-ttu-id="c8c1e-243">일시 중지 및 다시 시작 필요 hello [SQL DB 참가자] [ SQL DB Contributor] 권한, 특히 Microsoft.Sql/servers/databases/action 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-243">Pause and Resume require hello [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="c8c1e-244">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c8c1e-244">Next steps</span></span>
<span data-ttu-id="c8c1e-245">다음 몇 가지 핵심 성과 추가 개념을 이해 하는 문서 toohelp toohello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c8c1e-245">Refer toohello following articles toohelp you understand some additional key performance concepts:</span></span>

* <span data-ttu-id="c8c1e-246">[워크로드 및 동시성 관리][Workload and concurrency management]</span><span class="sxs-lookup"><span data-stu-id="c8c1e-246">[Workload and concurrency management][Workload and concurrency management]</span></span>
* <span data-ttu-id="c8c1e-247">[테이블 디자인 개요][Table design overview]</span><span class="sxs-lookup"><span data-stu-id="c8c1e-247">[Table design overview][Table design overview]</span></span>
* <span data-ttu-id="c8c1e-248">[테이블 배포][Table distribution]</span><span class="sxs-lookup"><span data-stu-id="c8c1e-248">[Table distribution][Table distribution]</span></span>
* <span data-ttu-id="c8c1e-249">[테이블 인덱싱][Table indexing]</span><span class="sxs-lookup"><span data-stu-id="c8c1e-249">[Table indexing][Table indexing]</span></span>
* <span data-ttu-id="c8c1e-250">[테이블 분할][Table partitioning]</span><span class="sxs-lookup"><span data-stu-id="c8c1e-250">[Table partitioning][Table partitioning]</span></span>
* <span data-ttu-id="c8c1e-251">[테이블 통계][Table statistics]</span><span class="sxs-lookup"><span data-stu-id="c8c1e-251">[Table statistics][Table statistics]</span></span>
* <span data-ttu-id="c8c1e-252">[모범 사례][Best practices]</span><span class="sxs-lookup"><span data-stu-id="c8c1e-252">[Best practices][Best practices]</span></span>

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/

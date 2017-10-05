---
title: "Azure SQL Data Warehouse의 계산 능력 관리(개요) | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스의 성능 확장 기능입니다. 또는 DWU를 조정하거나 계산 리소스를 일지 중지한 다음 다시 시작하여 비용을 절감합니다."
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
ms.openlocfilehash: abe22f542a79714f6e894870872ee6b76ffe7633
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a><span data-ttu-id="f9841-104">Azure SQL 데이터 웨어하우스의 계산 능력 관리(개요)</span><span class="sxs-lookup"><span data-stu-id="f9841-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f9841-105">개요</span><span class="sxs-lookup"><span data-stu-id="f9841-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="f9841-106">포털</span><span class="sxs-lookup"><span data-stu-id="f9841-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="f9841-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9841-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="f9841-108">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="f9841-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="f9841-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="f9841-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<span data-ttu-id="f9841-110">SQL 데이터 웨어하우스는 저장소와 계산을 분리하여 각각의 성능을 독립적으로 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-110">The architecture of SQL Data Warehouse separates storage and compute, allowing each to scale independently.</span></span> <span data-ttu-id="f9841-111">따라서 데이터 양에 관계 없이 성능 요구 사항에 맞게 계산을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-111">As a result, compute can be scaled to meet performance demands independent of the amount of data.</span></span> <span data-ttu-id="f9841-112">이 아키텍처의 자연스러운 결과는 계산 및 저장소에 대한 [청구][billed]가 분리되어 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span></span> 

<span data-ttu-id="f9841-113">이 개요에서는 SQL Data Warehouse에서 규모 확장이 작동하는 방법과 SQL Data Warehouse의 일시 중지, 다시 시작 및 확장 기능을 활용하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-113">This overview describes how scale out works with SQL Data Warehouse and how to utilize the pause, resume, and scale capabilities of SQL Data Warehouse.</span></span> <span data-ttu-id="f9841-114">DWU(데이터 웨어하우스 단위)와 성능 간의 관계에 대해 알아 보려면 [DWU][data warehouse units (DWUs)] 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9841-114">Consult the [data warehouse units (DWUs)][data warehouse units (DWUs)] page to learn how DWUs and performance are related.</span></span> 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a><span data-ttu-id="f9841-115">SQL Data Warehouse에서 계산 관리 작업이 작동하는 방법</span><span class="sxs-lookup"><span data-stu-id="f9841-115">How compute management operations work in SQL Data Warehouse</span></span>
<span data-ttu-id="f9841-116">SQL Data Warehouse의 아키텍처는 제어 노드, 계산 노드 및 60개 배포판으로 분산된 저장소 계층으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-116">The architecture for SQL Data Warehouse consists of a control node, compute nodes, and the storage layer spread across 60 distributions.</span></span> 

<span data-ttu-id="f9841-117">SQL Data Warehouse의 정상적인 활성 세션 동안 메타데이터를 관리하는 시스템의 헤드 노드에는 분산된 쿼리 최적화 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-117">During a normal active session in SQL Data Warehouse, your system's head node manages the metadata and contains the distributed query optimizer.</span></span> <span data-ttu-id="f9841-118">이 헤드 노드 아래에는 계산 노드와 저장소 계층이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-118">Beneath this head node are your compute nodes and your storage layer.</span></span> <span data-ttu-id="f9841-119">400DWU의 경우 시스템에는 하나의 헤드 노드, 네 개의 계산 노드 및 60개의 배포판으로 구성된 저장소 계층이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-119">For a DWU 400, your system has one head node, four compute nodes, and the storage layer, consisting of 60 distributions.</span></span> 

<span data-ttu-id="f9841-120">크기 조정 또는 일시 중지 작업을 수행하는 경우 시스템에서 먼저 들어오는 모든 쿼리를 종료한 다음 트랜잭션을 롤백하여 일관된 상태를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-120">When you undergo a scale or pause operation, the system first kills all incoming queries and then rolls back transactions to ensure a consistent state.</span></span> <span data-ttu-id="f9841-121">크기 조정 작업의 경우 이 트랜잭션 롤백을 완료한 후에만 크기 조정이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span></span> <span data-ttu-id="f9841-122">강화 작업의 경우 시스템에서 추가로 원하는 계산 노드 수를 프로비전한 다음 계산 노드를 저장소 계층에 다시 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-122">For a scale-up operation, the system provisions the extra desired number of compute nodes, and then begins reattaching the compute nodes to the storage layer.</span></span> <span data-ttu-id="f9841-123">규모 축소 작업의 경우 불필요한 노드가 해제되고 나머지 계산 노드는 적절한 수의 배포판에 다시 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-123">For a scale-down operation, the unneeded nodes are released and the remaining compute nodes reattach themselves to the appropriate number of distributions.</span></span> <span data-ttu-id="f9841-124">일시 중지 작업의 경우 모든 계산 노드가 해제되고 시스템에서 다양한 메타데이터 작업을 수행하여 최종 시스템을 안정된 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations to leave your final system in a stable state.</span></span>

| <span data-ttu-id="f9841-125">DWU</span><span class="sxs-lookup"><span data-stu-id="f9841-125">DWU</span></span>  | <span data-ttu-id="f9841-126">계산 노드 수 \#</span><span class="sxs-lookup"><span data-stu-id="f9841-126">\#of compute nodes</span></span> | <span data-ttu-id="f9841-127">노드당 배포 수 \#</span><span class="sxs-lookup"><span data-stu-id="f9841-127">\# of distributions per node</span></span> |
| ---- | ------------------ | ---------------------------- |
| <span data-ttu-id="f9841-128">100</span><span class="sxs-lookup"><span data-stu-id="f9841-128">100</span></span>  | <span data-ttu-id="f9841-129">1</span><span class="sxs-lookup"><span data-stu-id="f9841-129">1</span></span>                  | <span data-ttu-id="f9841-130">60</span><span class="sxs-lookup"><span data-stu-id="f9841-130">60</span></span>                           |
| <span data-ttu-id="f9841-131">200</span><span class="sxs-lookup"><span data-stu-id="f9841-131">200</span></span>  | <span data-ttu-id="f9841-132">2</span><span class="sxs-lookup"><span data-stu-id="f9841-132">2</span></span>                  | <span data-ttu-id="f9841-133">30</span><span class="sxs-lookup"><span data-stu-id="f9841-133">30</span></span>                           |
| <span data-ttu-id="f9841-134">300</span><span class="sxs-lookup"><span data-stu-id="f9841-134">300</span></span>  | <span data-ttu-id="f9841-135">3</span><span class="sxs-lookup"><span data-stu-id="f9841-135">3</span></span>                  | <span data-ttu-id="f9841-136">20</span><span class="sxs-lookup"><span data-stu-id="f9841-136">20</span></span>                           |
| <span data-ttu-id="f9841-137">400</span><span class="sxs-lookup"><span data-stu-id="f9841-137">400</span></span>  | <span data-ttu-id="f9841-138">4</span><span class="sxs-lookup"><span data-stu-id="f9841-138">4</span></span>                  | <span data-ttu-id="f9841-139">15</span><span class="sxs-lookup"><span data-stu-id="f9841-139">15</span></span>                           |
| <span data-ttu-id="f9841-140">500</span><span class="sxs-lookup"><span data-stu-id="f9841-140">500</span></span>  | <span data-ttu-id="f9841-141">5</span><span class="sxs-lookup"><span data-stu-id="f9841-141">5</span></span>                  | <span data-ttu-id="f9841-142">12</span><span class="sxs-lookup"><span data-stu-id="f9841-142">12</span></span>                           |
| <span data-ttu-id="f9841-143">600</span><span class="sxs-lookup"><span data-stu-id="f9841-143">600</span></span>  | <span data-ttu-id="f9841-144">6</span><span class="sxs-lookup"><span data-stu-id="f9841-144">6</span></span>                  | <span data-ttu-id="f9841-145">10</span><span class="sxs-lookup"><span data-stu-id="f9841-145">10</span></span>                           |
| <span data-ttu-id="f9841-146">1000</span><span class="sxs-lookup"><span data-stu-id="f9841-146">1000</span></span> | <span data-ttu-id="f9841-147">10</span><span class="sxs-lookup"><span data-stu-id="f9841-147">10</span></span>                 | <span data-ttu-id="f9841-148">6</span><span class="sxs-lookup"><span data-stu-id="f9841-148">6</span></span>                            |
| <span data-ttu-id="f9841-149">1200</span><span class="sxs-lookup"><span data-stu-id="f9841-149">1200</span></span> | <span data-ttu-id="f9841-150">12</span><span class="sxs-lookup"><span data-stu-id="f9841-150">12</span></span>                 | <span data-ttu-id="f9841-151">5</span><span class="sxs-lookup"><span data-stu-id="f9841-151">5</span></span>                            |
| <span data-ttu-id="f9841-152">1500</span><span class="sxs-lookup"><span data-stu-id="f9841-152">1500</span></span> | <span data-ttu-id="f9841-153">15</span><span class="sxs-lookup"><span data-stu-id="f9841-153">15</span></span>                 | <span data-ttu-id="f9841-154">4</span><span class="sxs-lookup"><span data-stu-id="f9841-154">4</span></span>                            |
| <span data-ttu-id="f9841-155">2000</span><span class="sxs-lookup"><span data-stu-id="f9841-155">2000</span></span> | <span data-ttu-id="f9841-156">20</span><span class="sxs-lookup"><span data-stu-id="f9841-156">20</span></span>                 | <span data-ttu-id="f9841-157">3</span><span class="sxs-lookup"><span data-stu-id="f9841-157">3</span></span>                            |
| <span data-ttu-id="f9841-158">3000</span><span class="sxs-lookup"><span data-stu-id="f9841-158">3000</span></span> | <span data-ttu-id="f9841-159">30</span><span class="sxs-lookup"><span data-stu-id="f9841-159">30</span></span>                 | <span data-ttu-id="f9841-160">2</span><span class="sxs-lookup"><span data-stu-id="f9841-160">2</span></span>                            |
| <span data-ttu-id="f9841-161">6000</span><span class="sxs-lookup"><span data-stu-id="f9841-161">6000</span></span> | <span data-ttu-id="f9841-162">60</span><span class="sxs-lookup"><span data-stu-id="f9841-162">60</span></span>                 | <span data-ttu-id="f9841-163">1</span><span class="sxs-lookup"><span data-stu-id="f9841-163">1</span></span>                            |

<span data-ttu-id="f9841-164">계산 관리를 위한 세 가지 주요 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-164">The three primary functions for managing compute are:</span></span>

1. <span data-ttu-id="f9841-165">일시 중지</span><span class="sxs-lookup"><span data-stu-id="f9841-165">Pause</span></span>
2. <span data-ttu-id="f9841-166">다시 시작</span><span class="sxs-lookup"><span data-stu-id="f9841-166">Resume</span></span>
3. <span data-ttu-id="f9841-167">확장</span><span class="sxs-lookup"><span data-stu-id="f9841-167">Scale</span></span>

<span data-ttu-id="f9841-168">이러한 작업을 각각 완료하는 데에는 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-168">Each of these operations may take several minutes to complete.</span></span> <span data-ttu-id="f9841-169">자동으로 크기 조정/일시 중지/다시 시작하는 경우 다른 작업을 진행하기 전에 특정 작업이 완료되었는지 확인하는 논리를 구현하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-169">If you are scaling/pausing/resuming automatically, you may want to implement logic to ensure that certain operations have been completed before proceeding with another action.</span></span> 

<span data-ttu-id="f9841-170">다양한 끝점을 통해 데이터베이스 상태를 확인하는 경우 이러한 작업의 자동화를 올바르게 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-170">Checking the database state through various endpoints will allow you to correctly implement automation of such operations.</span></span> <span data-ttu-id="f9841-171">포털에서는 작업 완료 시의 알림과 데이터베이스 현재 상태를 제공하지만 프로그래밍 방식으로 상태를 확인할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-171">The portal will provide notification upon completion of an operation and the databases current state but does not allow for programmatic checking of state.</span></span> 

>  [!NOTE]
>
>  <span data-ttu-id="f9841-172">모든 끝점에 대한 계산 관리 기능은 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-172">Compute management functionality does not exist across all endpoints.</span></span>
>
>  

|              | <span data-ttu-id="f9841-173">일시 중지/다시 시작</span><span class="sxs-lookup"><span data-stu-id="f9841-173">Pause/Resume</span></span> | <span data-ttu-id="f9841-174">확장</span><span class="sxs-lookup"><span data-stu-id="f9841-174">Scale</span></span> | <span data-ttu-id="f9841-175">데이터베이스 상태 확인</span><span class="sxs-lookup"><span data-stu-id="f9841-175">Check database state</span></span> |
| ------------ | ------------ | ----- | -------------------- |
| <span data-ttu-id="f9841-176">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="f9841-176">Azure portal</span></span> | <span data-ttu-id="f9841-177">예</span><span class="sxs-lookup"><span data-stu-id="f9841-177">Yes</span></span>          | <span data-ttu-id="f9841-178">예</span><span class="sxs-lookup"><span data-stu-id="f9841-178">Yes</span></span>   | <span data-ttu-id="f9841-179">**아니요**</span><span class="sxs-lookup"><span data-stu-id="f9841-179">**No**</span></span>               |
| <span data-ttu-id="f9841-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9841-180">PowerShell</span></span>   | <span data-ttu-id="f9841-181">예</span><span class="sxs-lookup"><span data-stu-id="f9841-181">Yes</span></span>          | <span data-ttu-id="f9841-182">예</span><span class="sxs-lookup"><span data-stu-id="f9841-182">Yes</span></span>   | <span data-ttu-id="f9841-183">예</span><span class="sxs-lookup"><span data-stu-id="f9841-183">Yes</span></span>                  |
| <span data-ttu-id="f9841-184">REST API</span><span class="sxs-lookup"><span data-stu-id="f9841-184">REST API</span></span>     | <span data-ttu-id="f9841-185">예</span><span class="sxs-lookup"><span data-stu-id="f9841-185">Yes</span></span>          | <span data-ttu-id="f9841-186">예</span><span class="sxs-lookup"><span data-stu-id="f9841-186">Yes</span></span>   | <span data-ttu-id="f9841-187">예</span><span class="sxs-lookup"><span data-stu-id="f9841-187">Yes</span></span>                  |
| <span data-ttu-id="f9841-188">T-SQL</span><span class="sxs-lookup"><span data-stu-id="f9841-188">T-SQL</span></span>        | <span data-ttu-id="f9841-189">**아니요**</span><span class="sxs-lookup"><span data-stu-id="f9841-189">**No**</span></span>       | <span data-ttu-id="f9841-190">예</span><span class="sxs-lookup"><span data-stu-id="f9841-190">Yes</span></span>   | <span data-ttu-id="f9841-191">예</span><span class="sxs-lookup"><span data-stu-id="f9841-191">Yes</span></span>                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="f9841-192">계산 조정</span><span class="sxs-lookup"><span data-stu-id="f9841-192">Scale compute</span></span>

<span data-ttu-id="f9841-193">SQL Data Warehouse의 성능은 CPU, 메모리 및 I/O 대역폭과 같은 계산 리소스를 추상화한 측정값인 [DWU(데이터 웨어하우스 단위)][data warehouse units (DWUs)]로 측정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="f9841-194">시스템 성능을 조정하려는 사용자는 포털, T-SQL 및 REST API와 같은 다양한 방법을 통해 시스템 성능을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-194">A user who wishes to scale their system's performance can do so through various means, such as through the portal, T-SQL, and REST APIs.</span></span> 

### <a name="how-do-i-scale-compute"></a><span data-ttu-id="f9841-195">계산 크기는 어떻게 조정합니까?</span><span class="sxs-lookup"><span data-stu-id="f9841-195">How do I scale compute?</span></span>
<span data-ttu-id="f9841-196">DWU 설정을 변경하여 SQL Data Warehouse에 대한 계산 성능을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-196">Compute power is managed for you SQL Data Warehouse by changing the DWU setting.</span></span> <span data-ttu-id="f9841-197">특정 작업에 대해 DWU를 더 많이 추가하면 성능이 [선형적으로][linearly] 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span></span>  <span data-ttu-id="f9841-198">시스템을 강화하거나 축소할 때 성능이 눈에 띄게 변경되는 DWU 제품을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span></span> 

<span data-ttu-id="f9841-199">DWU를 조정할 경우 다음과 같은 개별 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-199">To adjust DWUs, you can use any of these individual methods.</span></span>

* <span data-ttu-id="f9841-200">[Azure Portal을 사용하여 계산 능력 조정][Scale compute power with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="f9841-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span></span>
* <span data-ttu-id="f9841-201">[PowerShell을 사용하여 계산 능력 조정][Scale compute power with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="f9841-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span></span>
* <span data-ttu-id="f9841-202">[REST API를 사용하여 계산 능력 조정][Scale compute power with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="f9841-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span></span>
* <span data-ttu-id="f9841-203">[TSQL을 사용하여 계산 능력 조정][Scale compute power with TSQL]</span><span class="sxs-lookup"><span data-stu-id="f9841-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span></span>

### <a name="how-many-dwus-should-i-use"></a><span data-ttu-id="f9841-204">얼마나 많은 DWU를 사용해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="f9841-204">How many DWUs should I use?</span></span>

<span data-ttu-id="f9841-205">사용자에게 이상적인 DWU가 무엇인지 파악하기 위해서는 규모를 키우거나 줄이고 데이터를 로드한 후에 몇 가지 쿼리를 실행해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-205">To understand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span></span> <span data-ttu-id="f9841-206">크기 조정이 빠르기 때문에 1시간 이내에 다양한 성능 수준을 시험해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-206">Since scaling is quick, you can try various performance levels in an hour or less.</span></span> 

> [!Note] 
> <span data-ttu-id="f9841-207">SQL Data Warehouse는 많은 양의 데이터를 처리하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-207">SQL Data Warehouse is designed to process large amounts of data.</span></span> <span data-ttu-id="f9841-208">특히 대규모 DWU에서 크기 조정에 대한 실제 기능을 확인하려면 1TB에 가깝거나 초과하는 대용량 데이터 집합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-208">To see its true capabilities for scaling, especially at larger DWUs, you want to use a large data set which approaches or exceeds 1 TB.</span></span>

<span data-ttu-id="f9841-209">워크로드에 가장 적합한 DWU를 찾는 방법에 대한 권장 사항:</span><span class="sxs-lookup"><span data-stu-id="f9841-209">Recommendations for finding the best DWU for your workload:</span></span>

1. <span data-ttu-id="f9841-210">개발 중인 데이터 웨어하우스의 경우 먼저 낮은 DWU 성능 수준을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span></span>  <span data-ttu-id="f9841-211">적합한 시작 지점은 DW400 또는 DW200입니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-211">A good starting point is DW400 or DW200.</span></span>
2. <span data-ttu-id="f9841-212">응용 프로그램 성능을 모니터링하여 선택한 DWU 수와 관찰한 성능을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-212">Monitor your application performance, observing the number of DWUs selected compared to the performance you observe.</span></span>
3. <span data-ttu-id="f9841-213">선형 크기 조정을 가정하여 요구 사항에 맞는 최적 성능 수준을 달성하기 위해 성능이 얼마나 더 빠르거나 느려야 하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-213">Determine how much faster or slower performance should be for you to reach the optimum performance level for your requirements by assuming linear scale.</span></span>
4. <span data-ttu-id="f9841-214">원하는 워크로드 성능에 비례하여 DWU 수를 늘리거나 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-214">Increase or decrease the number of DWUs in proportion to how much faster or slower you want your workload to perform.</span></span> 
5. <span data-ttu-id="f9841-215">비즈니스 요구 사항에 맞는 최적 성능 수준에 도달할 때까지 계속 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span></span>

> [!NOTE]
>
> <span data-ttu-id="f9841-216">계산 노드 간에 작업을 분할할 수 있는 경우 더 많은 병렬 처리를 통해 쿼리 성능만 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-216">Query performance only increases with more parallelization if the work can be split between compute nodes.</span></span> <span data-ttu-id="f9841-217">크기 조정으로 성능이 변경되지 않는다고 확인되면 성능 튜닝 관련 문서를 참조하여 데이터가 균일하게 분산되어 있지 않은지 또는 많은 양의 데이터 이동이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-217">If you find that scaling is not changing your performance, please check out our performance tuning articles to check whether your data is unevenly distributed or if you are introducing a large amount of data movement.</span></span> 

### <a name="when-should-i-scale-dwus"></a><span data-ttu-id="f9841-218">언제 DWU를 조정해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="f9841-218">When should I scale DWUs?</span></span>
<span data-ttu-id="f9841-219">DWU 크기 조정은 다음과 같은 중요한 시나리오를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-219">Scaling DWUs alters the following important scenarios:</span></span>

1. <span data-ttu-id="f9841-220">검색, 집계 및 CTAS 문에 대한 시스템 성능의 선형적 변경</span><span class="sxs-lookup"><span data-stu-id="f9841-220">Linearly changing performance of the system for scans, aggregations, and CTAS statements</span></span>
2. <span data-ttu-id="f9841-221">PolyBase로 로드할 때 판독기 및 기록기 수 증가</span><span class="sxs-lookup"><span data-stu-id="f9841-221">Increasing the number of readers and writers when loading with PolyBase</span></span>
3. <span data-ttu-id="f9841-222">동시 쿼리 및 동시성 슬롯의 최대 수</span><span class="sxs-lookup"><span data-stu-id="f9841-222">Maximum number of concurrent queries and concurrency slots</span></span>

<span data-ttu-id="f9841-223">DWU 성능 조정 시기에 대한 권장 사항:</span><span class="sxs-lookup"><span data-stu-id="f9841-223">Recommendations for when to scale DWUs:</span></span>

1. <span data-ttu-id="f9841-224">대량의 데이터 로딩 또는 변환 작업을 수행하기 전에 데이터를 더욱 빠르게 사용할 수 있도록 DWU를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span></span>
2. <span data-ttu-id="f9841-225">가장 바쁜 업무 시간에서 많은 수의 동시 쿼리를 수용할 수 있도록 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-225">During peak business hours, scale to accommodate larger numbers of concurrent queries.</span></span> 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="f9841-226">계산 일시 중지</span><span class="sxs-lookup"><span data-stu-id="f9841-226">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="f9841-227">데이터베이스를 일시 중지하려면 다음과 같은 개별 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-227">To pause a database, use any of these individual methods.</span></span>

* <span data-ttu-id="f9841-228">[Azure Portal을 사용하여 계산 일시 중지][Pause compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="f9841-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span></span>
* <span data-ttu-id="f9841-229">[PowerShell을 사용하여 계산 일시 중지][Pause compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="f9841-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span></span>
* <span data-ttu-id="f9841-230">[REST API를 사용하여 계산 일시 중지][Pause compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="f9841-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span></span>

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="f9841-231">계산 다시 시작</span><span class="sxs-lookup"><span data-stu-id="f9841-231">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="f9841-232">데이터베이스를 다시 시작하려면 다음과 같은 개별 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-232">To resume a database, use any of these individual methods.</span></span>

* <span data-ttu-id="f9841-233">[Azure Portal을 사용하여 계산 다시 시작][Resume compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="f9841-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span></span>
* <span data-ttu-id="f9841-234">[PowerShell을 사용하여 계산 다시 시작][Resume compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="f9841-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span></span>
* <span data-ttu-id="f9841-235">[REST API를 사용하여 계산 다시 시작][Resume compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="f9841-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span></span>

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="f9841-236">데이터베이스 상태 확인</span><span class="sxs-lookup"><span data-stu-id="f9841-236">Check database state</span></span> 

<span data-ttu-id="f9841-237">데이터베이스를 다시 시작하려면 다음과 같은 개별 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-237">To resume a database, use any of these individual methods.</span></span>

- <span data-ttu-id="f9841-238">[T-SQL을 사용하여 데이터베이스 상태 확인][Check database state with T-SQL]</span><span class="sxs-lookup"><span data-stu-id="f9841-238">[Check database state with T-SQL][Check database state with T-SQL]</span></span>
- <span data-ttu-id="f9841-239">[PowerShell을 사용하여 데이터베이스 상태 확인][Check database state with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="f9841-239">[Check database state with PowerShell][Check database state with PowerShell]</span></span>
- <span data-ttu-id="f9841-240">[REST API를 사용하여 데이터베이스 상태 확인][Check database state with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="f9841-240">[Check database state with REST APIs][Check database state with REST APIs]</span></span>

## <a name="permissions"></a><span data-ttu-id="f9841-241">권한</span><span class="sxs-lookup"><span data-stu-id="f9841-241">Permissions</span></span>

<span data-ttu-id="f9841-242">데이터베이스 크기를 조정하려면 [ALTER DATABASE][ALTER DATABASE]에서 설명하는 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-242">Scaling the database requires the permissions described in [ALTER DATABASE][ALTER DATABASE].</span></span>  <span data-ttu-id="f9841-243">일시 중지 및 다시 시작을 수행하려면 [SQL DB 참가자][SQL DB Contributor] 권한, 특히 Microsoft.Sql/servers/databases/action이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f9841-243">Pause and Resume require the [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="f9841-244">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f9841-244">Next steps</span></span>
<span data-ttu-id="f9841-245">일부 추가적인 주요 성능 개념을 이해하는 데 도움이 되는 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9841-245">Refer to the following articles to help you understand some additional key performance concepts:</span></span>

* <span data-ttu-id="f9841-246">[워크로드 및 동시성 관리][Workload and concurrency management]</span><span class="sxs-lookup"><span data-stu-id="f9841-246">[Workload and concurrency management][Workload and concurrency management]</span></span>
* <span data-ttu-id="f9841-247">[테이블 디자인 개요][Table design overview]</span><span class="sxs-lookup"><span data-stu-id="f9841-247">[Table design overview][Table design overview]</span></span>
* <span data-ttu-id="f9841-248">[테이블 배포][Table distribution]</span><span class="sxs-lookup"><span data-stu-id="f9841-248">[Table distribution][Table distribution]</span></span>
* <span data-ttu-id="f9841-249">[테이블 인덱싱][Table indexing]</span><span class="sxs-lookup"><span data-stu-id="f9841-249">[Table indexing][Table indexing]</span></span>
* <span data-ttu-id="f9841-250">[테이블 분할][Table partitioning]</span><span class="sxs-lookup"><span data-stu-id="f9841-250">[Table partitioning][Table partitioning]</span></span>
* <span data-ttu-id="f9841-251">[테이블 통계][Table statistics]</span><span class="sxs-lookup"><span data-stu-id="f9841-251">[Table statistics][Table statistics]</span></span>
* <span data-ttu-id="f9841-252">[모범 사례][Best practices]</span><span class="sxs-lookup"><span data-stu-id="f9841-252">[Best practices][Best practices]</span></span>

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

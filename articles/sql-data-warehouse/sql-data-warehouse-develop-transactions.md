---
title: "SQL Data Warehouse의 트랜잭션 | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 트랜잭션 구현을 위한 팁"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: ae621788-e575-41f5-8bfe-fa04dc4b0b53
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 29d53e18539f2c24dd64090b2ac6f9dd4c783961
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="transactions-in-sql-data-warehouse"></a><span data-ttu-id="9295d-103">SQL 데이터 웨어하우스의 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="9295d-103">Transactions in SQL Data Warehouse</span></span>
<span data-ttu-id="9295d-104">예상한 것처럼 SQL 데이터 웨어하우스는 데이터 웨어하우스 워크로드의 일부로 트랜잭션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-104">As you would expect, SQL Data Warehouse supports transactions as part of the data warehouse workload.</span></span> <span data-ttu-id="9295d-105">그러나 SQL 데이터 웨어하우스의 성능은 SQL Server와 비교할 때 일부 기능이 제한되는 수준으로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-105">However, to ensure the performance of SQL Data Warehouse is maintained at scale some features are limited when compared to SQL Server.</span></span> <span data-ttu-id="9295d-106">이 문서는 차이점을 강조 표시하고 다른 부분에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-106">This article highlights the differences and lists the others.</span></span> 

## <a name="transaction-isolation-levels"></a><span data-ttu-id="9295d-107">트랜잭션 격리 수준</span><span class="sxs-lookup"><span data-stu-id="9295d-107">Transaction isolation levels</span></span>
<span data-ttu-id="9295d-108">SQL 데이터 웨어하우스는 ACID 트랜잭션을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-108">SQL Data Warehouse implements ACID transactions.</span></span> <span data-ttu-id="9295d-109">그러나, 트랜잭션 지원의 격리는 `READ UNCOMMITTED` 로 제한되며 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-109">However, the Isolation of the transactional support is limited to `READ UNCOMMITTED` and this cannot be changed.</span></span> <span data-ttu-id="9295d-110">다양한 코딩 메서드를 구현하여 더티 읽기를 염려하는 경우 이를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-110">You can implement a number of coding methods to prevent dirty reads of data if this is a concern for you.</span></span> <span data-ttu-id="9295d-111">가장 인기 있는 메서드는 CTAS 및 테이블 파티션 전환(슬라이딩 창 패턴이라고 하는)을 모두 사용하여 사용자 준비 중인 데이터 쿼리를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-111">The most popular methods leverage both CTAS and table partition switching (often known as the sliding window pattern) to prevent users from querying data that is still being prepared.</span></span> <span data-ttu-id="9295d-112">데이터를 사전 필터링하는 뷰가 일반적인 접근 방법이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-112">Views that pre-filter the data is also a popular approach.</span></span>  

## <a name="transaction-size"></a><span data-ttu-id="9295d-113">트랜잭션 크기</span><span class="sxs-lookup"><span data-stu-id="9295d-113">Transaction size</span></span>
<span data-ttu-id="9295d-114">단일 데이터 수정 트랜잭션은 크기가 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-114">A single data modification transaction is limited in size.</span></span> <span data-ttu-id="9295d-115">현재 이러한 제한은 "배포 기준"으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-115">The limit today is applied "per distribution".</span></span> <span data-ttu-id="9295d-116">따라서 제한을 배포 수와 곱하여 전체 할당을 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-116">Therefore, the total allocation can be calculated by multiplying the limit by the distribution count.</span></span> <span data-ttu-id="9295d-117">트랜잭션에 포함된 대략적인 최대 행 수를 구하려면 배포 용량을 각 행의 전체 크기로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-117">To approximate the maximum number of rows in the transaction divide the distribution cap by the total size of each row.</span></span> <span data-ttu-id="9295d-118">가변 길이 열의 경우에는 최대 크기를 사용하는 대신, 평균 열 길이를 사용하는 것을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-118">For variable length columns consider taking an average column length rather than using the maximum size.</span></span>

<span data-ttu-id="9295d-119">아래 표에서는 다음과 같이 가정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-119">In the table below the following assumptions have been made:</span></span>

* <span data-ttu-id="9295d-120">균일한 데이터 분포가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-120">An even distribution of data has occurred</span></span> 
* <span data-ttu-id="9295d-121">평균 행 길이는 250바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-121">The average row length is 250 bytes</span></span>

| <span data-ttu-id="9295d-122">[DWU][DWU]</span><span class="sxs-lookup"><span data-stu-id="9295d-122">[DWU][DWU]</span></span> | <span data-ttu-id="9295d-123">배포당 용량(GiB)</span><span class="sxs-lookup"><span data-stu-id="9295d-123">Cap per distribution (GiB)</span></span> | <span data-ttu-id="9295d-124">배포 수</span><span class="sxs-lookup"><span data-stu-id="9295d-124">Number of Distributions</span></span> | <span data-ttu-id="9295d-125">최대 트랜잭션 크기(GiB)</span><span class="sxs-lookup"><span data-stu-id="9295d-125">MAX transaction size (GiB)</span></span> | <span data-ttu-id="9295d-126">배포 당 행 수</span><span class="sxs-lookup"><span data-stu-id="9295d-126"># Rows per distribution</span></span> | <span data-ttu-id="9295d-127">트랜잭션당 최대 행 수</span><span class="sxs-lookup"><span data-stu-id="9295d-127">Max Rows per transaction</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="9295d-128">DW100</span><span class="sxs-lookup"><span data-stu-id="9295d-128">DW100</span></span> |<span data-ttu-id="9295d-129">1</span><span class="sxs-lookup"><span data-stu-id="9295d-129">1</span></span> |<span data-ttu-id="9295d-130">60</span><span class="sxs-lookup"><span data-stu-id="9295d-130">60</span></span> |<span data-ttu-id="9295d-131">60</span><span class="sxs-lookup"><span data-stu-id="9295d-131">60</span></span> |<span data-ttu-id="9295d-132">4,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-132">4,000,000</span></span> |<span data-ttu-id="9295d-133">240,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-133">240,000,000</span></span> |
| <span data-ttu-id="9295d-134">DW200</span><span class="sxs-lookup"><span data-stu-id="9295d-134">DW200</span></span> |<span data-ttu-id="9295d-135">1.5</span><span class="sxs-lookup"><span data-stu-id="9295d-135">1.5</span></span> |<span data-ttu-id="9295d-136">60</span><span class="sxs-lookup"><span data-stu-id="9295d-136">60</span></span> |<span data-ttu-id="9295d-137">90</span><span class="sxs-lookup"><span data-stu-id="9295d-137">90</span></span> |<span data-ttu-id="9295d-138">6,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-138">6,000,000</span></span> |<span data-ttu-id="9295d-139">360,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-139">360,000,000</span></span> |
| <span data-ttu-id="9295d-140">DW300</span><span class="sxs-lookup"><span data-stu-id="9295d-140">DW300</span></span> |<span data-ttu-id="9295d-141">2.25</span><span class="sxs-lookup"><span data-stu-id="9295d-141">2.25</span></span> |<span data-ttu-id="9295d-142">60</span><span class="sxs-lookup"><span data-stu-id="9295d-142">60</span></span> |<span data-ttu-id="9295d-143">135</span><span class="sxs-lookup"><span data-stu-id="9295d-143">135</span></span> |<span data-ttu-id="9295d-144">9,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-144">9,000,000</span></span> |<span data-ttu-id="9295d-145">540,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-145">540,000,000</span></span> |
| <span data-ttu-id="9295d-146">DW400</span><span class="sxs-lookup"><span data-stu-id="9295d-146">DW400</span></span> |<span data-ttu-id="9295d-147">3</span><span class="sxs-lookup"><span data-stu-id="9295d-147">3</span></span> |<span data-ttu-id="9295d-148">60</span><span class="sxs-lookup"><span data-stu-id="9295d-148">60</span></span> |<span data-ttu-id="9295d-149">180</span><span class="sxs-lookup"><span data-stu-id="9295d-149">180</span></span> |<span data-ttu-id="9295d-150">12,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-150">12,000,000</span></span> |<span data-ttu-id="9295d-151">720,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-151">720,000,000</span></span> |
| <span data-ttu-id="9295d-152">DW500</span><span class="sxs-lookup"><span data-stu-id="9295d-152">DW500</span></span> |<span data-ttu-id="9295d-153">3.75</span><span class="sxs-lookup"><span data-stu-id="9295d-153">3.75</span></span> |<span data-ttu-id="9295d-154">60</span><span class="sxs-lookup"><span data-stu-id="9295d-154">60</span></span> |<span data-ttu-id="9295d-155">225</span><span class="sxs-lookup"><span data-stu-id="9295d-155">225</span></span> |<span data-ttu-id="9295d-156">15,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-156">15,000,000</span></span> |<span data-ttu-id="9295d-157">900,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-157">900,000,000</span></span> |
| <span data-ttu-id="9295d-158">DW600</span><span class="sxs-lookup"><span data-stu-id="9295d-158">DW600</span></span> |<span data-ttu-id="9295d-159">4.5.</span><span class="sxs-lookup"><span data-stu-id="9295d-159">4.5</span></span> |<span data-ttu-id="9295d-160">60</span><span class="sxs-lookup"><span data-stu-id="9295d-160">60</span></span> |<span data-ttu-id="9295d-161">270</span><span class="sxs-lookup"><span data-stu-id="9295d-161">270</span></span> |<span data-ttu-id="9295d-162">18,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-162">18,000,000</span></span> |<span data-ttu-id="9295d-163">1,080,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-163">1,080,000,000</span></span> |
| <span data-ttu-id="9295d-164">DW1000</span><span class="sxs-lookup"><span data-stu-id="9295d-164">DW1000</span></span> |<span data-ttu-id="9295d-165">7.5</span><span class="sxs-lookup"><span data-stu-id="9295d-165">7.5</span></span> |<span data-ttu-id="9295d-166">60</span><span class="sxs-lookup"><span data-stu-id="9295d-166">60</span></span> |<span data-ttu-id="9295d-167">450</span><span class="sxs-lookup"><span data-stu-id="9295d-167">450</span></span> |<span data-ttu-id="9295d-168">30,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-168">30,000,000</span></span> |<span data-ttu-id="9295d-169">1,800,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-169">1,800,000,000</span></span> |
| <span data-ttu-id="9295d-170">DW1200</span><span class="sxs-lookup"><span data-stu-id="9295d-170">DW1200</span></span> |<span data-ttu-id="9295d-171">9</span><span class="sxs-lookup"><span data-stu-id="9295d-171">9</span></span> |<span data-ttu-id="9295d-172">60</span><span class="sxs-lookup"><span data-stu-id="9295d-172">60</span></span> |<span data-ttu-id="9295d-173">540</span><span class="sxs-lookup"><span data-stu-id="9295d-173">540</span></span> |<span data-ttu-id="9295d-174">36,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-174">36,000,000</span></span> |<span data-ttu-id="9295d-175">2,160,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-175">2,160,000,000</span></span> |
| <span data-ttu-id="9295d-176">DW1500</span><span class="sxs-lookup"><span data-stu-id="9295d-176">DW1500</span></span> |<span data-ttu-id="9295d-177">11.25</span><span class="sxs-lookup"><span data-stu-id="9295d-177">11.25</span></span> |<span data-ttu-id="9295d-178">60</span><span class="sxs-lookup"><span data-stu-id="9295d-178">60</span></span> |<span data-ttu-id="9295d-179">675</span><span class="sxs-lookup"><span data-stu-id="9295d-179">675</span></span> |<span data-ttu-id="9295d-180">45,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-180">45,000,000</span></span> |<span data-ttu-id="9295d-181">2,700,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-181">2,700,000,000</span></span> |
| <span data-ttu-id="9295d-182">DW2000</span><span class="sxs-lookup"><span data-stu-id="9295d-182">DW2000</span></span> |<span data-ttu-id="9295d-183">15</span><span class="sxs-lookup"><span data-stu-id="9295d-183">15</span></span> |<span data-ttu-id="9295d-184">60</span><span class="sxs-lookup"><span data-stu-id="9295d-184">60</span></span> |<span data-ttu-id="9295d-185">900</span><span class="sxs-lookup"><span data-stu-id="9295d-185">900</span></span> |<span data-ttu-id="9295d-186">60,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-186">60,000,000</span></span> |<span data-ttu-id="9295d-187">3,600,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-187">3,600,000,000</span></span> |
| <span data-ttu-id="9295d-188">DW3000</span><span class="sxs-lookup"><span data-stu-id="9295d-188">DW3000</span></span> |<span data-ttu-id="9295d-189">22.5</span><span class="sxs-lookup"><span data-stu-id="9295d-189">22.5</span></span> |<span data-ttu-id="9295d-190">60</span><span class="sxs-lookup"><span data-stu-id="9295d-190">60</span></span> |<span data-ttu-id="9295d-191">1,350</span><span class="sxs-lookup"><span data-stu-id="9295d-191">1,350</span></span> |<span data-ttu-id="9295d-192">90,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-192">90,000,000</span></span> |<span data-ttu-id="9295d-193">5,400,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-193">5,400,000,000</span></span> |
| <span data-ttu-id="9295d-194">DW6000</span><span class="sxs-lookup"><span data-stu-id="9295d-194">DW6000</span></span> |<span data-ttu-id="9295d-195">45</span><span class="sxs-lookup"><span data-stu-id="9295d-195">45</span></span> |<span data-ttu-id="9295d-196">60</span><span class="sxs-lookup"><span data-stu-id="9295d-196">60</span></span> |<span data-ttu-id="9295d-197">2,700</span><span class="sxs-lookup"><span data-stu-id="9295d-197">2,700</span></span> |<span data-ttu-id="9295d-198">180,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-198">180,000,000</span></span> |<span data-ttu-id="9295d-199">10,800,000,000</span><span class="sxs-lookup"><span data-stu-id="9295d-199">10,800,000,000</span></span> |

<span data-ttu-id="9295d-200">트랜잭션 또는 작업 기준으로 트랜잭션 크기 제한이 적용되며</span><span class="sxs-lookup"><span data-stu-id="9295d-200">The transaction size limit is applied per transaction or operation.</span></span> <span data-ttu-id="9295d-201">모든 동시 트랜잭션에서 적용되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-201">It is not applied across all concurrent transactions.</span></span> <span data-ttu-id="9295d-202">따라서 각 트랜잭션은 이 크기의 데이터를 로그에 쓰도록 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-202">Therefore each transaction is permitted to write this amount of data to the log.</span></span> 

<span data-ttu-id="9295d-203">로그에 기록된 데이터의 양을 최적화하고 최소화하려면 [트랜잭션 모범 사례][Transactions best practices] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9295d-203">To optimize and minimize the amount of data written to the log please refer to the [Transactions best practices][Transactions best practices] article.</span></span>

> [!WARNING]
> <span data-ttu-id="9295d-204">최대 트랜잭션 크기는 데이터가 균일하게 분산되는 HASH 또는 ROUND_ROBIN 분산 테이블에 대해서만 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-204">The maximum transaction size can only be achieved for HASH or ROUND_ROBIN distributed tables where the spread of the data is even.</span></span> <span data-ttu-id="9295d-205">트랜잭션이 균일하지 않은 분산 방식으로 데이터를 쓰는 경우 최대 트랜잭션 크기에 도달하기 전에 제한에 도달할 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-205">If the transaction is writing data in a skewed fashion to the distributions then the limit is likely to be reached prior to the maximum transaction size.</span></span>
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a><span data-ttu-id="9295d-206">트랜잭션 상태</span><span class="sxs-lookup"><span data-stu-id="9295d-206">Transaction state</span></span>
<span data-ttu-id="9295d-207">SQL 데이터 웨어하우스는 XACT_STATE() 함수를 사용하여 값 -2를 사용하는 실패한 트랜잭션을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-207">SQL Data Warehouse uses the XACT_STATE() function to report a failed transaction using the value -2.</span></span> <span data-ttu-id="9295d-208">트랜잭션이 실패하고 롤백만 표시함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-208">This means that the transaction has failed and is marked for rollback only</span></span>

> [!NOTE]
> <span data-ttu-id="9295d-209">XACT_STATE 함수에서-2 사용은 실패한 트랜잭션이 SQL Server와 다른 동작을 표시함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-209">The use of -2 by the XACT_STATE function to denote a failed transaction represents different behavior to SQL Server.</span></span> <span data-ttu-id="9295d-210">SQL Server는 값 -1를 사용하여 커밋할 수 없는 트랜잭션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-210">SQL Server uses the value -1 to represent an un-committable transaction.</span></span> <span data-ttu-id="9295d-211">SQL Server는 커밋할 수 없음으로 표시하지 않고 트랜잭션 내 일부 오류를 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-211">SQL Server can tolerate some errors inside a transaction without it having to be marked as un-committable.</span></span> <span data-ttu-id="9295d-212">예를 들어 `SELECT 1/0` 은 오류를 발생시키지만 커밋할 수 없는 상태로 트랜잭션을 강제 적용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-212">For example `SELECT 1/0` would cause an error but not force a transaction into an un-committable state.</span></span> <span data-ttu-id="9295d-213">또한 SQL Server는 커밋할 수 없는 트랜잭션에서 읽기를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-213">SQL Server also permits reads in the un-committable transaction.</span></span> <span data-ttu-id="9295d-214">그러나 SQL 데이터 웨어하우스는 이를 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-214">However, SQL Data Warehouse does not let you do this.</span></span> <span data-ttu-id="9295d-215">SQL 데이터 웨어하우스의 트랜잭션 내부에서 오류가 발생하는 경우 자동으로 -2 상태가 되며, 해당 문이 롤백될 때까지 추가 select 문을 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-215">If an error occurs inside a SQL Data Warehouse transaction it will automatically enter the -2 state and you will not be able to make any further select statements until the statement has been rolled back.</span></span> <span data-ttu-id="9295d-216">따라서 코드를 수정해야 할 수 있으므로 XACT_STATE()가 사용되는지 알기 위해 해당 응용 프로그램 코드를 확인하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-216">It is therefore important to check that your application code to see if it uses  XACT_STATE() as you may need to make code modifications.</span></span>
> 
> 

<span data-ttu-id="9295d-217">예를 들어 SQL Server에서 다음과 같은 트랜잭션이 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-217">For example, in SQL Server you might see a transaction that looks like this:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="9295d-218">이 코드를 위와 같이 두면 다음과 같은 오류 메시지가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-218">If you leave your code as it is above then you will get the following error message:</span></span>

<span data-ttu-id="9295d-219">Msg 111233, Level 16, State 1, Line 1 111233, 현재 트랜잭션이 중단되었으며 보류 중인 변경 내용은 롤백되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-219">Msg 111233, Level 16, State 1, Line 1 111233;The current transaction has aborted, and any pending changes have been rolled back.</span></span> <span data-ttu-id="9295d-220">원인: 롤백 전용 상태의 트랜잭션은 DDL, DML 또는 SELECT 문 이전에 명시적으로 롤백되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-220">Cause: A transaction in a rollback-only state was not explicitly rolled back before a DDL, DML or SELECT statement.</span></span>

<span data-ttu-id="9295d-221">또한 ERROR_* 함수의 출력도 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-221">You will also not get the output of the ERROR_* functions.</span></span>

<span data-ttu-id="9295d-222">SQL 데이터 웨어하우스에서는 이 코드를 약간 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-222">In SQL Data Warehouse the code needs to be slightly altered:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;
    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="9295d-223">이제 예상되는 동작이 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-223">The expected behavior is now observed.</span></span> <span data-ttu-id="9295d-224">트랜잭션의 오류가 관리되고 ERROR_* 함수는 예상대로 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-224">The error in the transaction is managed and the ERROR_* functions provide values as expected.</span></span>

<span data-ttu-id="9295d-225">변경된 부분은 트랜잭션의 `ROLLBACK`이 `CATCH` 블록의 오류 정보를 읽기 전에 발생해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-225">All that has changed is that the `ROLLBACK` of the transaction had to happen before the read of the error information in the `CATCH` block.</span></span>

## <a name="errorline-function"></a><span data-ttu-id="9295d-226">Error_Line() 함수</span><span class="sxs-lookup"><span data-stu-id="9295d-226">Error_Line() function</span></span>
<span data-ttu-id="9295d-227">SQL 데이터 웨어하우스가 ERROR_LINE() 함수를 구현하거나 지원하는 것 또한 주목할 가치가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-227">It is also worth noting that SQL Data Warehouse does not implement or support the ERROR_LINE() function.</span></span> <span data-ttu-id="9295d-228">이 코드에 있는 경우 SQL 데이터 웨어하우스와 호환되도록 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-228">If you have this in your code you will need to remove it to be compliant with SQL Data Warehouse.</span></span> <span data-ttu-id="9295d-229">동등한 기능을 구현하는 대신 코드에서 쿼리 레이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-229">Use query labels in your code instead to implement equivalent functionality.</span></span> <span data-ttu-id="9295d-230">이 기능에 대한 자세한 내용은 [LABEL][LABEL] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9295d-230">Please refer to the [LABEL][LABEL] article for more details on this feature.</span></span>

## <a name="using-throw-and-raiserror"></a><span data-ttu-id="9295d-231">THROW 및 RAISERROR 사용</span><span class="sxs-lookup"><span data-stu-id="9295d-231">Using THROW and RAISERROR</span></span>
<span data-ttu-id="9295d-232">THROW는 SQL 데이터 웨어하우스에서 예외를 발생시키기 위한 가장 최신 구현이지만 RAISERROR도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-232">THROW is the more modern implementation for raising exceptions in SQL Data Warehouse but RAISERROR is also supported.</span></span> <span data-ttu-id="9295d-233">그러나 다음 몇 가지 사항에 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-233">There are a few differences that are worth paying attention to however.</span></span>

* <span data-ttu-id="9295d-234">사용자 정의 오류 메시지 번호는 THROW에 대해 100,000 - 150,000 범위에 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-234">User defined error messages numbers cannot be in the 100,000 - 150,000 range for THROW</span></span>
* <span data-ttu-id="9295d-235">RAISERROR 오류 메시지는 50,000으로 고정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-235">RAISERROR error messages are fixed at 50,000</span></span>
* <span data-ttu-id="9295d-236">sys.messages 사용은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-236">Use of sys.messages is not supported</span></span>

## <a name="limitiations"></a><span data-ttu-id="9295d-237">제한 사항</span><span class="sxs-lookup"><span data-stu-id="9295d-237">Limitiations</span></span>
<span data-ttu-id="9295d-238">SQL 데이터 웨어하우스에는 트랜잭션과 관련된 몇 가지 기타 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-238">SQL Data Warehouse does have a few other restrictions that relate to transactions.</span></span>

<span data-ttu-id="9295d-239">다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-239">They are as follows:</span></span>

* <span data-ttu-id="9295d-240">분산된 트랜잭션이 없습니다</span><span class="sxs-lookup"><span data-stu-id="9295d-240">No distributed transactions</span></span>
* <span data-ttu-id="9295d-241">중첩된 트랜잭션이 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-241">No nested transactions permitted</span></span>
* <span data-ttu-id="9295d-242">저장 점수를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-242">No save points allowed</span></span>
* <span data-ttu-id="9295d-243">명명된 트랜잭션이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-243">No named transactions</span></span>
* <span data-ttu-id="9295d-244">표시된 트랜잭션이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-244">No marked transactions</span></span>
* <span data-ttu-id="9295d-245">사용자 정의 트랜잭션 내에 `CREATE TABLE` 과 같은 DDL 지원은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9295d-245">No support for DDL such as `CREATE TABLE` inside a user defined transaction</span></span>

## <a name="next-steps"></a><span data-ttu-id="9295d-246">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9295d-246">Next steps</span></span>
<span data-ttu-id="9295d-247">트랜잭션을 최적화하는 방법에 대한 자세한 내용은 [트랜잭션 모범 사례][Transactions best practices]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9295d-247">To learn more about optimizing transactions, see [Transactions best practices][Transactions best practices].</span></span>  <span data-ttu-id="9295d-248">기타 SQL Data Warehouse 모범 사례에 대해 자세히 알아보려면 [SQL Data Warehouse 모범 사례][SQL Data Warehouse best practices]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9295d-248">To learn about other SQL Data Warehouse best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse best practices].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->

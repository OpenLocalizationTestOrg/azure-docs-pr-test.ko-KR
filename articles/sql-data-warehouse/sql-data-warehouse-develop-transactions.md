---
title: "SQL 데이터 웨어하우스에 aaaTransactions | Microsoft Docs"
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
ms.openlocfilehash: 7c541648553238443b407666612561918096eb61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-in-sql-data-warehouse"></a><span data-ttu-id="b16dd-103">SQL 데이터 웨어하우스의 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="b16dd-103">Transactions in SQL Data Warehouse</span></span>
<span data-ttu-id="b16dd-104">와 마찬가지로, SQL 데이터 웨어하우스 트랜잭션을 hello 데이터 웨어하우스 작업의 일환으로 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-104">As you would expect, SQL Data Warehouse supports transactions as part of hello data warehouse workload.</span></span> <span data-ttu-id="b16dd-105">그러나 SQL 데이터 웨어하우스의 tooensure hello 성능은 비교 tooSQL 서버 일부 기능을 제한 하는 규모에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-105">However, tooensure hello performance of SQL Data Warehouse is maintained at scale some features are limited when compared tooSQL Server.</span></span> <span data-ttu-id="b16dd-106">Hello 차이점을 설명 하는이 문서 및 목록 hello 다른 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-106">This article highlights hello differences and lists hello others.</span></span> 

## <a name="transaction-isolation-levels"></a><span data-ttu-id="b16dd-107">트랜잭션 격리 수준</span><span class="sxs-lookup"><span data-stu-id="b16dd-107">Transaction isolation levels</span></span>
<span data-ttu-id="b16dd-108">SQL 데이터 웨어하우스는 ACID 트랜잭션을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-108">SQL Data Warehouse implements ACID transactions.</span></span> <span data-ttu-id="b16dd-109">그러나 hello hello 트랜잭션 지원의 격리는 너무 제한`READ UNCOMMITTED` 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-109">However, hello Isolation of hello transactional support is limited too`READ UNCOMMITTED` and this cannot be changed.</span></span> <span data-ttu-id="b16dd-110">다양 한 문제가이 경우 데이터의 tooprevent 더티 읽기 코딩 방법 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-110">You can implement a number of coding methods tooprevent dirty reads of data if this is a concern for you.</span></span> <span data-ttu-id="b16dd-111">hello 가장 인기 있는 메서드 및 활용 하 여 모두 CTAS에는 테이블 파티션 전환 (종종 라고도 함 슬라이딩 창 패턴 hello) tooprevent 사용자가 여전히 준비 중인 데이터를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-111">hello most popular methods leverage both CTAS and table partition switching (often known as hello sliding window pattern) tooprevent users from querying data that is still being prepared.</span></span> <span data-ttu-id="b16dd-112">뷰 미리 hello 데이터를 필터링 하는 일반적인 접근 방법 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-112">Views that pre-filter hello data is also a popular approach.</span></span>  

## <a name="transaction-size"></a><span data-ttu-id="b16dd-113">트랜잭션 크기</span><span class="sxs-lookup"><span data-stu-id="b16dd-113">Transaction size</span></span>
<span data-ttu-id="b16dd-114">단일 데이터 수정 트랜잭션은 크기가 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-114">A single data modification transaction is limited in size.</span></span> <span data-ttu-id="b16dd-115">오늘 "배포" 당 hello 제한이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-115">hello limit today is applied "per distribution".</span></span> <span data-ttu-id="b16dd-116">따라서 hello 제한 hello 배포 수로 곱하여 hello 총 할당을 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-116">Therefore, hello total allocation can be calculated by multiplying hello limit by hello distribution count.</span></span> <span data-ttu-id="b16dd-117">tooapproximate hello 최대 행 개수 hello 트랜잭션에서 각 행의 총 크기 hello hello 배포 cap을 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-117">tooapproximate hello maximum number of rows in hello transaction divide hello distribution cap by hello total size of each row.</span></span> <span data-ttu-id="b16dd-118">가변 길이 열에 대 한 hello 최대 크기를 사용 하는 대신 수행 된 평균 열 길이 보십시오.</span><span class="sxs-lookup"><span data-stu-id="b16dd-118">For variable length columns consider taking an average column length rather than using hello maximum size.</span></span>

<span data-ttu-id="b16dd-119">Hello 아래 hello 테이블에 다음과 같은 가정은 적용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-119">In hello table below hello following assumptions have been made:</span></span>

* <span data-ttu-id="b16dd-120">균일한 데이터 분포가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-120">An even distribution of data has occurred</span></span> 
* <span data-ttu-id="b16dd-121">hello 평균 행 길이 250 바이트</span><span class="sxs-lookup"><span data-stu-id="b16dd-121">hello average row length is 250 bytes</span></span>

| <span data-ttu-id="b16dd-122">[DWU][DWU]</span><span class="sxs-lookup"><span data-stu-id="b16dd-122">[DWU][DWU]</span></span> | <span data-ttu-id="b16dd-123">배포당 용량(GiB)</span><span class="sxs-lookup"><span data-stu-id="b16dd-123">Cap per distribution (GiB)</span></span> | <span data-ttu-id="b16dd-124">배포 수</span><span class="sxs-lookup"><span data-stu-id="b16dd-124">Number of Distributions</span></span> | <span data-ttu-id="b16dd-125">최대 트랜잭션 크기(GiB)</span><span class="sxs-lookup"><span data-stu-id="b16dd-125">MAX transaction size (GiB)</span></span> | <span data-ttu-id="b16dd-126">배포 당 행 수</span><span class="sxs-lookup"><span data-stu-id="b16dd-126"># Rows per distribution</span></span> | <span data-ttu-id="b16dd-127">트랜잭션당 최대 행 수</span><span class="sxs-lookup"><span data-stu-id="b16dd-127">Max Rows per transaction</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="b16dd-128">DW100</span><span class="sxs-lookup"><span data-stu-id="b16dd-128">DW100</span></span> |<span data-ttu-id="b16dd-129">1</span><span class="sxs-lookup"><span data-stu-id="b16dd-129">1</span></span> |<span data-ttu-id="b16dd-130">60</span><span class="sxs-lookup"><span data-stu-id="b16dd-130">60</span></span> |<span data-ttu-id="b16dd-131">60</span><span class="sxs-lookup"><span data-stu-id="b16dd-131">60</span></span> |<span data-ttu-id="b16dd-132">4,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-132">4,000,000</span></span> |<span data-ttu-id="b16dd-133">240,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-133">240,000,000</span></span> |
| <span data-ttu-id="b16dd-134">DW200</span><span class="sxs-lookup"><span data-stu-id="b16dd-134">DW200</span></span> |<span data-ttu-id="b16dd-135">1.5</span><span class="sxs-lookup"><span data-stu-id="b16dd-135">1.5</span></span> |<span data-ttu-id="b16dd-136">60</span><span class="sxs-lookup"><span data-stu-id="b16dd-136">60</span></span> |<span data-ttu-id="b16dd-137">90</span><span class="sxs-lookup"><span data-stu-id="b16dd-137">90</span></span> |<span data-ttu-id="b16dd-138">6,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-138">6,000,000</span></span> |<span data-ttu-id="b16dd-139">360,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-139">360,000,000</span></span> |
| <span data-ttu-id="b16dd-140">DW300</span><span class="sxs-lookup"><span data-stu-id="b16dd-140">DW300</span></span> |<span data-ttu-id="b16dd-141">2.25</span><span class="sxs-lookup"><span data-stu-id="b16dd-141">2.25</span></span> |<span data-ttu-id="b16dd-142">60</span><span class="sxs-lookup"><span data-stu-id="b16dd-142">60</span></span> |<span data-ttu-id="b16dd-143">135</span><span class="sxs-lookup"><span data-stu-id="b16dd-143">135</span></span> |<span data-ttu-id="b16dd-144">9,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-144">9,000,000</span></span> |<span data-ttu-id="b16dd-145">540,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-145">540,000,000</span></span> |
| <span data-ttu-id="b16dd-146">DW400</span><span class="sxs-lookup"><span data-stu-id="b16dd-146">DW400</span></span> |<span data-ttu-id="b16dd-147">3</span><span class="sxs-lookup"><span data-stu-id="b16dd-147">3</span></span> |<span data-ttu-id="b16dd-148">60</span><span class="sxs-lookup"><span data-stu-id="b16dd-148">60</span></span> |<span data-ttu-id="b16dd-149">180</span><span class="sxs-lookup"><span data-stu-id="b16dd-149">180</span></span> |<span data-ttu-id="b16dd-150">12,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-150">12,000,000</span></span> |<span data-ttu-id="b16dd-151">720,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-151">720,000,000</span></span> |
| <span data-ttu-id="b16dd-152">DW500</span><span class="sxs-lookup"><span data-stu-id="b16dd-152">DW500</span></span> |<span data-ttu-id="b16dd-153">3.75</span><span class="sxs-lookup"><span data-stu-id="b16dd-153">3.75</span></span> |<span data-ttu-id="b16dd-154">60</span><span class="sxs-lookup"><span data-stu-id="b16dd-154">60</span></span> |<span data-ttu-id="b16dd-155">225</span><span class="sxs-lookup"><span data-stu-id="b16dd-155">225</span></span> |<span data-ttu-id="b16dd-156">15,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-156">15,000,000</span></span> |<span data-ttu-id="b16dd-157">900,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-157">900,000,000</span></span> |
| <span data-ttu-id="b16dd-158">DW600</span><span class="sxs-lookup"><span data-stu-id="b16dd-158">DW600</span></span> |<span data-ttu-id="b16dd-159">4.5.</span><span class="sxs-lookup"><span data-stu-id="b16dd-159">4.5</span></span> |<span data-ttu-id="b16dd-160">60</span><span class="sxs-lookup"><span data-stu-id="b16dd-160">60</span></span> |<span data-ttu-id="b16dd-161">270</span><span class="sxs-lookup"><span data-stu-id="b16dd-161">270</span></span> |<span data-ttu-id="b16dd-162">18,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-162">18,000,000</span></span> |<span data-ttu-id="b16dd-163">1,080,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-163">1,080,000,000</span></span> |
| <span data-ttu-id="b16dd-164">DW1000</span><span class="sxs-lookup"><span data-stu-id="b16dd-164">DW1000</span></span> |<span data-ttu-id="b16dd-165">7.5</span><span class="sxs-lookup"><span data-stu-id="b16dd-165">7.5</span></span> |<span data-ttu-id="b16dd-166">60</span><span class="sxs-lookup"><span data-stu-id="b16dd-166">60</span></span> |<span data-ttu-id="b16dd-167">450</span><span class="sxs-lookup"><span data-stu-id="b16dd-167">450</span></span> |<span data-ttu-id="b16dd-168">30,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-168">30,000,000</span></span> |<span data-ttu-id="b16dd-169">1,800,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-169">1,800,000,000</span></span> |
| <span data-ttu-id="b16dd-170">DW1200</span><span class="sxs-lookup"><span data-stu-id="b16dd-170">DW1200</span></span> |<span data-ttu-id="b16dd-171">9</span><span class="sxs-lookup"><span data-stu-id="b16dd-171">9</span></span> |<span data-ttu-id="b16dd-172">60</span><span class="sxs-lookup"><span data-stu-id="b16dd-172">60</span></span> |<span data-ttu-id="b16dd-173">540</span><span class="sxs-lookup"><span data-stu-id="b16dd-173">540</span></span> |<span data-ttu-id="b16dd-174">36,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-174">36,000,000</span></span> |<span data-ttu-id="b16dd-175">2,160,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-175">2,160,000,000</span></span> |
| <span data-ttu-id="b16dd-176">DW1500</span><span class="sxs-lookup"><span data-stu-id="b16dd-176">DW1500</span></span> |<span data-ttu-id="b16dd-177">11.25</span><span class="sxs-lookup"><span data-stu-id="b16dd-177">11.25</span></span> |<span data-ttu-id="b16dd-178">60</span><span class="sxs-lookup"><span data-stu-id="b16dd-178">60</span></span> |<span data-ttu-id="b16dd-179">675</span><span class="sxs-lookup"><span data-stu-id="b16dd-179">675</span></span> |<span data-ttu-id="b16dd-180">45,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-180">45,000,000</span></span> |<span data-ttu-id="b16dd-181">2,700,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-181">2,700,000,000</span></span> |
| <span data-ttu-id="b16dd-182">DW2000</span><span class="sxs-lookup"><span data-stu-id="b16dd-182">DW2000</span></span> |<span data-ttu-id="b16dd-183">15</span><span class="sxs-lookup"><span data-stu-id="b16dd-183">15</span></span> |<span data-ttu-id="b16dd-184">60</span><span class="sxs-lookup"><span data-stu-id="b16dd-184">60</span></span> |<span data-ttu-id="b16dd-185">900</span><span class="sxs-lookup"><span data-stu-id="b16dd-185">900</span></span> |<span data-ttu-id="b16dd-186">60,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-186">60,000,000</span></span> |<span data-ttu-id="b16dd-187">3,600,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-187">3,600,000,000</span></span> |
| <span data-ttu-id="b16dd-188">DW3000</span><span class="sxs-lookup"><span data-stu-id="b16dd-188">DW3000</span></span> |<span data-ttu-id="b16dd-189">22.5</span><span class="sxs-lookup"><span data-stu-id="b16dd-189">22.5</span></span> |<span data-ttu-id="b16dd-190">60</span><span class="sxs-lookup"><span data-stu-id="b16dd-190">60</span></span> |<span data-ttu-id="b16dd-191">1,350</span><span class="sxs-lookup"><span data-stu-id="b16dd-191">1,350</span></span> |<span data-ttu-id="b16dd-192">90,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-192">90,000,000</span></span> |<span data-ttu-id="b16dd-193">5,400,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-193">5,400,000,000</span></span> |
| <span data-ttu-id="b16dd-194">DW6000</span><span class="sxs-lookup"><span data-stu-id="b16dd-194">DW6000</span></span> |<span data-ttu-id="b16dd-195">45</span><span class="sxs-lookup"><span data-stu-id="b16dd-195">45</span></span> |<span data-ttu-id="b16dd-196">60</span><span class="sxs-lookup"><span data-stu-id="b16dd-196">60</span></span> |<span data-ttu-id="b16dd-197">2,700</span><span class="sxs-lookup"><span data-stu-id="b16dd-197">2,700</span></span> |<span data-ttu-id="b16dd-198">180,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-198">180,000,000</span></span> |<span data-ttu-id="b16dd-199">10,800,000,000</span><span class="sxs-lookup"><span data-stu-id="b16dd-199">10,800,000,000</span></span> |

<span data-ttu-id="b16dd-200">트랜잭션 또는 작업 마다 hello 트랜잭션 크기 제한이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-200">hello transaction size limit is applied per transaction or operation.</span></span> <span data-ttu-id="b16dd-201">모든 동시 트랜잭션에서 적용되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-201">It is not applied across all concurrent transactions.</span></span> <span data-ttu-id="b16dd-202">따라서 각 트랜잭션에이 데이터 toohello 로그이 정도의 toowrite 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-202">Therefore each transaction is permitted toowrite this amount of data toohello log.</span></span> 

<span data-ttu-id="b16dd-203">toooptimize hello toohello 로그에 기록 된 데이터 양을 최소화 하 고 toohello를 참조 하십시오 [트랜잭션을 모범 사례] [ Transactions best practices] 문서.</span><span class="sxs-lookup"><span data-stu-id="b16dd-203">toooptimize and minimize hello amount of data written toohello log please refer toohello [Transactions best practices][Transactions best practices] article.</span></span>

> [!WARNING]
> <span data-ttu-id="b16dd-204">해시에 대 한 트랜잭션 크기를 수행할 수 있습니다 또는 ROUND_ROBIN distributed 테이블의 hello 확산 되는 위치 데이터를 환영 최대 hello 짝수 이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-204">hello maximum transaction size can only be achieved for HASH or ROUND_ROBIN distributed tables where hello spread of hello data is even.</span></span> <span data-ttu-id="b16dd-205">Hello 트랜잭션 쓰는 경우 데이터는 왜곡 된 방식에서 toohello 분포 hello 제한 이면 가능성이 toobe 이전 toohello 최대 트랜잭션 크기에 도달 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-205">If hello transaction is writing data in a skewed fashion toohello distributions then hello limit is likely toobe reached prior toohello maximum transaction size.</span></span>
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a><span data-ttu-id="b16dd-206">트랜잭션 상태</span><span class="sxs-lookup"><span data-stu-id="b16dd-206">Transaction state</span></span>
<span data-ttu-id="b16dd-207">SQL 데이터 웨어하우스는 hello XACT_STATE 함수 tooreport hello 값-2를 사용 하 여 실패 한 트랜잭션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-207">SQL Data Warehouse uses hello XACT_STATE() function tooreport a failed transaction using hello value -2.</span></span> <span data-ttu-id="b16dd-208">즉, hello 트랜잭션이 실패 하 고만 롤백에 대 한 표시</span><span class="sxs-lookup"><span data-stu-id="b16dd-208">This means that hello transaction has failed and is marked for rollback only</span></span>

> [!NOTE]
> <span data-ttu-id="b16dd-209">-2의 실패 한 트랜잭션 나타내는 다른 동작이 tooSQL 서버 hello XACT_STATE 함수 toodenote로 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-209">hello use of -2 by hello XACT_STATE function toodenote a failed transaction represents different behavior tooSQL Server.</span></span> <span data-ttu-id="b16dd-210">SQL Server hello 값-1 toorepresent 커밋할 트랜잭션이 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-210">SQL Server uses hello value -1 toorepresent an un-committable transaction.</span></span> <span data-ttu-id="b16dd-211">SQL Server toobe로 커밋할 표시 없이 트랜잭션 내에서는 몇 가지 오류를 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-211">SQL Server can tolerate some errors inside a transaction without it having toobe marked as un-committable.</span></span> <span data-ttu-id="b16dd-212">예를 들어 `SELECT 1/0` 은 오류를 발생시키지만 커밋할 수 없는 상태로 트랜잭션을 강제 적용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-212">For example `SELECT 1/0` would cause an error but not force a transaction into an un-committable state.</span></span> <span data-ttu-id="b16dd-213">또한 SQL Server는 hello 커밋할 트랜잭션에서 읽기를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-213">SQL Server also permits reads in hello un-committable transaction.</span></span> <span data-ttu-id="b16dd-214">그러나 SQL 데이터 웨어하우스는 이를 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-214">However, SQL Data Warehouse does not let you do this.</span></span> <span data-ttu-id="b16dd-215">Hello-2 상태가 자동으로 전환 됩니다 및 수 toomake 됩니다 SQL 데이터 웨어하우스 트랜잭션 내부에서 오류가 발생 하는 경우 모든 추가 문을 때까지 선택 hello 문을 롤백 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-215">If an error occurs inside a SQL Data Warehouse transaction it will automatically enter hello -2 state and you will not be able toomake any further select statements until hello statement has been rolled back.</span></span> <span data-ttu-id="b16dd-216">따라서 중요 한 toocheck XACT_STATE 때 사용 하는 경우 응용 프로그램 코드 toosee toomake 코드를 수정 해야 할 수는 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-216">It is therefore important toocheck that your application code toosee if it uses  XACT_STATE() as you may need toomake code modifications.</span></span>
> 
> 

<span data-ttu-id="b16dd-217">예를 들어 SQL Server에서 다음과 같은 트랜잭션이 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-217">For example, in SQL Server you might see a transaction that looks like this:</span></span>

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

<span data-ttu-id="b16dd-218">위에 있기 때문에 코드를 그대로 둔 hello 다음과 같은 오류 메시지가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-218">If you leave your code as it is above then you will get hello following error message:</span></span>

<span data-ttu-id="b16dd-219">메시지 111233, 수준 16, 상태 1, 줄 1 111233; 현재 트랜잭션이 중단 및 보류 중인 변경 내용이 롤백 되었다는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-219">Msg 111233, Level 16, State 1, Line 1 111233;hello current transaction has aborted, and any pending changes have been rolled back.</span></span> <span data-ttu-id="b16dd-220">원인: 롤백 전용 상태의 트랜잭션은 DDL, DML 또는 SELECT 문 이전에 명시적으로 롤백되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-220">Cause: A transaction in a rollback-only state was not explicitly rolled back before a DDL, DML or SELECT statement.</span></span>

<span data-ttu-id="b16dd-221">Hello 오류 * 함수 hello 출력 하지 발생 하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-221">You will also not get hello output of hello ERROR_* functions.</span></span>

<span data-ttu-id="b16dd-222">SQL 데이터 웨어하우스 hello 코드 toobe 약간 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-222">In SQL Data Warehouse hello code needs toobe slightly altered:</span></span>

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

<span data-ttu-id="b16dd-223">hello 동작을 따릅니다 이제 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-223">hello expected behavior is now observed.</span></span> <span data-ttu-id="b16dd-224">hello 트랜잭션에서 hello 오류는 관리 하 고 hello 오류 * 함수 예상 대로 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-224">hello error in hello transaction is managed and hello ERROR_* functions provide values as expected.</span></span>

<span data-ttu-id="b16dd-225">변경 된 모든는 해당 hello `ROLLBACK` hello의 트랜잭션 이전의 toohappen hello hello에 대 한 hello 오류 정보의 읽을 `CATCH` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-225">All that has changed is that hello `ROLLBACK` of hello transaction had toohappen before hello read of hello error information in hello `CATCH` block.</span></span>

## <a name="errorline-function"></a><span data-ttu-id="b16dd-226">Error_Line() 함수</span><span class="sxs-lookup"><span data-stu-id="b16dd-226">Error_Line() function</span></span>
<span data-ttu-id="b16dd-227">SQL 데이터 웨어하우스 구현 하거나 hello error_line () 함수를 지원 하지 않는 주목할 만한 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-227">It is also worth noting that SQL Data Warehouse does not implement or support hello ERROR_LINE() function.</span></span> <span data-ttu-id="b16dd-228">Tooremove 해야는 코드에서이 있는 경우 그 toobe SQL 데이터 웨어하우스를 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-228">If you have this in your code you will need tooremove it toobe compliant with SQL Data Warehouse.</span></span> <span data-ttu-id="b16dd-229">레이블을 사용 하 여 쿼리 코드에서 대신 tooimplement 이와 동일한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-229">Use query labels in your code instead tooimplement equivalent functionality.</span></span> <span data-ttu-id="b16dd-230">Toohello를 참조 하십시오 [레이블] [ LABEL] 이 기능에 대 한 자세한 내용은 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-230">Please refer toohello [LABEL][LABEL] article for more details on this feature.</span></span>

## <a name="using-throw-and-raiserror"></a><span data-ttu-id="b16dd-231">THROW 및 RAISERROR 사용</span><span class="sxs-lookup"><span data-stu-id="b16dd-231">Using THROW and RAISERROR</span></span>
<span data-ttu-id="b16dd-232">THROW는 hello SQL 데이터 웨어하우스의 예외를 발생 시키기 위한 최신 구현 하지만 RAISERROR도 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-232">THROW is hello more modern implementation for raising exceptions in SQL Data Warehouse but RAISERROR is also supported.</span></span> <span data-ttu-id="b16dd-233">주의 기울여야 toohowever 가치가 있는 몇 가지 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-233">There are a few differences that are worth paying attention toohowever.</span></span>

* <span data-ttu-id="b16dd-234">사용자 정의 오류 메시지 번호 100000 150000 범위 THROW에 대 한 hello에 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-234">User defined error messages numbers cannot be in hello 100,000 - 150,000 range for THROW</span></span>
* <span data-ttu-id="b16dd-235">RAISERROR 오류 메시지는 50,000으로 고정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-235">RAISERROR error messages are fixed at 50,000</span></span>
* <span data-ttu-id="b16dd-236">sys.messages 사용은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-236">Use of sys.messages is not supported</span></span>

## <a name="limitiations"></a><span data-ttu-id="b16dd-237">제한 사항</span><span class="sxs-lookup"><span data-stu-id="b16dd-237">Limitiations</span></span>
<span data-ttu-id="b16dd-238">SQL 데이터 웨어하우스 tootransactions와 관련 된 몇 가지 제한에는.</span><span class="sxs-lookup"><span data-stu-id="b16dd-238">SQL Data Warehouse does have a few other restrictions that relate tootransactions.</span></span>

<span data-ttu-id="b16dd-239">다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-239">They are as follows:</span></span>

* <span data-ttu-id="b16dd-240">분산된 트랜잭션이 없습니다</span><span class="sxs-lookup"><span data-stu-id="b16dd-240">No distributed transactions</span></span>
* <span data-ttu-id="b16dd-241">중첩된 트랜잭션이 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-241">No nested transactions permitted</span></span>
* <span data-ttu-id="b16dd-242">저장 점수를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-242">No save points allowed</span></span>
* <span data-ttu-id="b16dd-243">명명된 트랜잭션이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-243">No named transactions</span></span>
* <span data-ttu-id="b16dd-244">표시된 트랜잭션이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-244">No marked transactions</span></span>
* <span data-ttu-id="b16dd-245">사용자 정의 트랜잭션 내에 `CREATE TABLE` 과 같은 DDL 지원은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-245">No support for DDL such as `CREATE TABLE` inside a user defined transaction</span></span>

## <a name="next-steps"></a><span data-ttu-id="b16dd-246">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b16dd-246">Next steps</span></span>
<span data-ttu-id="b16dd-247">트랜잭션을 최적화에 대 한 더 toolearn 참조 [트랜잭션을 모범 사례][Transactions best practices]합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-247">toolearn more about optimizing transactions, see [Transactions best practices][Transactions best practices].</span></span>  <span data-ttu-id="b16dd-248">기타 SQL 데이터 웨어하우스 모범 사례에 대 한 toolearn 참조 [SQL 데이터 웨어하우스 모범 사례][SQL Data Warehouse best practices]합니다.</span><span class="sxs-lookup"><span data-stu-id="b16dd-248">toolearn about other SQL Data Warehouse best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse best practices].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->

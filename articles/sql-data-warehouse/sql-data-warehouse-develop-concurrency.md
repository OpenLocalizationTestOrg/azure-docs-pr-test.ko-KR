---
title: "SQL 데이터 웨어하우스에 aaaConcurrency 및 작업 관리 | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 동시성 및 워크로드 관리를 이해합니다."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 08/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: 7f7e77aa687760252aed16573b609817ed9111c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a><span data-ttu-id="580e0-103">SQL 데이터 웨어하우스의 동시성 및 워크로드 관리</span><span class="sxs-lookup"><span data-stu-id="580e0-103">Concurrency and workload management in SQL Data Warehouse</span></span>
<span data-ttu-id="580e0-104">Microsoft Azure SQL 데이터 웨어하우스 규모에 예측 가능한 성능을 toodeliver를 사용 하면 메모리 및 CPU 우선 순위와 같은 리소스 할당 및 동시성 수준을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-104">toodeliver predictable performance at scale, Microsoft Azure SQL Data Warehouse helps you control concurrency levels and resource allocations like memory and CPU prioritization.</span></span> <span data-ttu-id="580e0-105">이 문서는 두 기능이 모두 방법을 구현한 데이터 웨어하우스에서 해당를 제어 하는 방법에 대해 동시성 및 작업 관리 toohello 개념을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-105">This article introduces you toohello concepts of concurrency and workload management, explaining how both features have been implemented and how you can control them in your data warehouse.</span></span> <span data-ttu-id="580e0-106">SQL 데이터 웨어하우스 작업 관리는 의도 한 toohelp 다중 사용자 환경을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-106">SQL Data Warehouse workload management is intended toohelp you support multi-user environments.</span></span> <span data-ttu-id="580e0-107">다중 테넌트 워크로드용은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-107">It is not intended for multi-tenant workloads.</span></span>

## <a name="concurrency-limits"></a><span data-ttu-id="580e0-108">동시성 한도</span><span class="sxs-lookup"><span data-stu-id="580e0-108">Concurrency limits</span></span>
<span data-ttu-id="580e0-109">SQL 데이터 웨어하우스 too1, 024 동시 연결을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-109">SQL Data Warehouse allows up too1,024 concurrent connections.</span></span> <span data-ttu-id="580e0-110">1,024개의 모든 연결을 통해 동시에 쿼리를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-110">All 1,024 connections can submit queries concurrently.</span></span> <span data-ttu-id="580e0-111">그러나 toooptimize 처리량, SQL 데이터 웨어하우스는 각 쿼리는 최소 메모리 부여를 받을 일부 쿼리 tooensure를 대기할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-111">However, toooptimize throughput, SQL Data Warehouse may queue some queries tooensure that each query receives a minimal memory grant.</span></span> <span data-ttu-id="580e0-112">쿼리 실행 시 큐에 대기하기가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-112">Queuing occurs at query execution time.</span></span> <span data-ttu-id="580e0-113">큐 쿼리 별 총 처리량을 활성 쿼리 가져올 액세스 toocritically 되도록 하 여 동시성 제한에 도달 하면 SQL 데이터 웨어하우스를 늘릴 수 메모리 리소스를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-113">By queuing queries when concurrency limits are reached, SQL Data Warehouse can increase total throughput by ensuring that active queries get access toocritically needed memory resources.</span></span>  

<span data-ttu-id="580e0-114">동시성 한도는 *동시 쿼리 수* 및 *동시성 슬롯 수*라는 두 개념에 의해 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-114">Concurrency limits are governed by two concepts: *concurrent queries* and *concurrency slots*.</span></span> <span data-ttu-id="580e0-115">쿼리 tooexecute에 대 한 것 hello 동시성 슬롯 할당와 hello 쿼리 동시성 제한 내에서 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-115">For a query tooexecute, it must execute within both hello query concurrency limit and hello concurrency slot allocation.</span></span>

* <span data-ttu-id="580e0-116">동시 쿼리는 hello hello에 동일한 실행 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-116">Concurrent queries are hello queries executing at hello same time.</span></span> <span data-ttu-id="580e0-117">SQL 데이터 웨어하우스 DWU 크기가 더 커지면 hello에 too32 동시 쿼리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-117">SQL Data Warehouse supports up too32 concurrent queries on hello larger DWU sizes.</span></span>
* <span data-ttu-id="580e0-118">동시성 슬롯은 DWU를 기준으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-118">Concurrency slots are allocated based on DWU.</span></span> <span data-ttu-id="580e0-119">100개의 DWU마다 4개의 동시성 슬롯을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-119">Each 100 DWU provides 4 concurrency slots.</span></span> <span data-ttu-id="580e0-120">예를 들어 DW100은 4개의 동시성 슬롯을 할당하고, DW1000은 40개를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-120">For example, a DW100 allocates 4 concurrency slots and DW1000 allocates 40.</span></span> <span data-ttu-id="580e0-121">하나 이상의 동시성을 슬롯 hello에 종속를 사용 하는 각 쿼리 [리소스 클래스](#resource-classes) hello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-121">Each query consumes one or more concurrency slots, dependent on hello [resource class](#resource-classes) of hello query.</span></span> <span data-ttu-id="580e0-122">Hello smallrc 리소스 클래스에서 실행 되는 쿼리 동시성 슬롯 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-122">Queries running in hello smallrc resource class consume one concurrency slot.</span></span> <span data-ttu-id="580e0-123">상위 리소스 클래스에서 실행되는 쿼리는 더 많은 동시성 슬롯을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-123">Queries running in a higher resource class consume more concurrency slots.</span></span>

<span data-ttu-id="580e0-124">hello 다음 설명 동시 쿼리 및 동시성 슬롯 hello에 모두에 대 한 hello도 다양 한 DWU 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-124">hello following table describes hello limits for both concurrent queries and concurrency slots at hello various DWU sizes.</span></span>

### <a name="concurrency-limits"></a><span data-ttu-id="580e0-125">동시성 한도</span><span class="sxs-lookup"><span data-stu-id="580e0-125">Concurrency limits</span></span>
| <span data-ttu-id="580e0-126">DWU</span><span class="sxs-lookup"><span data-stu-id="580e0-126">DWU</span></span> | <span data-ttu-id="580e0-127">최대 동시 쿼리 수</span><span class="sxs-lookup"><span data-stu-id="580e0-127">Max concurrent queries</span></span> | <span data-ttu-id="580e0-128">할당된 동시성 슬롯 수</span><span class="sxs-lookup"><span data-stu-id="580e0-128">Concurrency slots allocated</span></span> |
|:--- |:---:|:---:|
| <span data-ttu-id="580e0-129">DW100</span><span class="sxs-lookup"><span data-stu-id="580e0-129">DW100</span></span> |<span data-ttu-id="580e0-130">4</span><span class="sxs-lookup"><span data-stu-id="580e0-130">4</span></span> |<span data-ttu-id="580e0-131">4</span><span class="sxs-lookup"><span data-stu-id="580e0-131">4</span></span> |
| <span data-ttu-id="580e0-132">DW200</span><span class="sxs-lookup"><span data-stu-id="580e0-132">DW200</span></span> |<span data-ttu-id="580e0-133">8</span><span class="sxs-lookup"><span data-stu-id="580e0-133">8</span></span> |<span data-ttu-id="580e0-134">8</span><span class="sxs-lookup"><span data-stu-id="580e0-134">8</span></span> |
| <span data-ttu-id="580e0-135">DW300</span><span class="sxs-lookup"><span data-stu-id="580e0-135">DW300</span></span> |<span data-ttu-id="580e0-136">12</span><span class="sxs-lookup"><span data-stu-id="580e0-136">12</span></span> |<span data-ttu-id="580e0-137">12</span><span class="sxs-lookup"><span data-stu-id="580e0-137">12</span></span> |
| <span data-ttu-id="580e0-138">DW400</span><span class="sxs-lookup"><span data-stu-id="580e0-138">DW400</span></span> |<span data-ttu-id="580e0-139">16</span><span class="sxs-lookup"><span data-stu-id="580e0-139">16</span></span> |<span data-ttu-id="580e0-140">16</span><span class="sxs-lookup"><span data-stu-id="580e0-140">16</span></span> |
| <span data-ttu-id="580e0-141">DW500</span><span class="sxs-lookup"><span data-stu-id="580e0-141">DW500</span></span> |<span data-ttu-id="580e0-142">20</span><span class="sxs-lookup"><span data-stu-id="580e0-142">20</span></span> |<span data-ttu-id="580e0-143">20</span><span class="sxs-lookup"><span data-stu-id="580e0-143">20</span></span> |
| <span data-ttu-id="580e0-144">DW600</span><span class="sxs-lookup"><span data-stu-id="580e0-144">DW600</span></span> |<span data-ttu-id="580e0-145">24</span><span class="sxs-lookup"><span data-stu-id="580e0-145">24</span></span> |<span data-ttu-id="580e0-146">24</span><span class="sxs-lookup"><span data-stu-id="580e0-146">24</span></span> |
| <span data-ttu-id="580e0-147">DW1000</span><span class="sxs-lookup"><span data-stu-id="580e0-147">DW1000</span></span> |<span data-ttu-id="580e0-148">32</span><span class="sxs-lookup"><span data-stu-id="580e0-148">32</span></span> |<span data-ttu-id="580e0-149">40</span><span class="sxs-lookup"><span data-stu-id="580e0-149">40</span></span> |
| <span data-ttu-id="580e0-150">DW1200</span><span class="sxs-lookup"><span data-stu-id="580e0-150">DW1200</span></span> |<span data-ttu-id="580e0-151">32</span><span class="sxs-lookup"><span data-stu-id="580e0-151">32</span></span> |<span data-ttu-id="580e0-152">48</span><span class="sxs-lookup"><span data-stu-id="580e0-152">48</span></span> |
| <span data-ttu-id="580e0-153">DW1500</span><span class="sxs-lookup"><span data-stu-id="580e0-153">DW1500</span></span> |<span data-ttu-id="580e0-154">32</span><span class="sxs-lookup"><span data-stu-id="580e0-154">32</span></span> |<span data-ttu-id="580e0-155">60</span><span class="sxs-lookup"><span data-stu-id="580e0-155">60</span></span> |
| <span data-ttu-id="580e0-156">DW2000</span><span class="sxs-lookup"><span data-stu-id="580e0-156">DW2000</span></span> |<span data-ttu-id="580e0-157">32</span><span class="sxs-lookup"><span data-stu-id="580e0-157">32</span></span> |<span data-ttu-id="580e0-158">80</span><span class="sxs-lookup"><span data-stu-id="580e0-158">80</span></span> |
| <span data-ttu-id="580e0-159">DW3000</span><span class="sxs-lookup"><span data-stu-id="580e0-159">DW3000</span></span> |<span data-ttu-id="580e0-160">32</span><span class="sxs-lookup"><span data-stu-id="580e0-160">32</span></span> |<span data-ttu-id="580e0-161">120</span><span class="sxs-lookup"><span data-stu-id="580e0-161">120</span></span> |
| <span data-ttu-id="580e0-162">DW6000</span><span class="sxs-lookup"><span data-stu-id="580e0-162">DW6000</span></span> |<span data-ttu-id="580e0-163">32</span><span class="sxs-lookup"><span data-stu-id="580e0-163">32</span></span> |<span data-ttu-id="580e0-164">240</span><span class="sxs-lookup"><span data-stu-id="580e0-164">240</span></span> |

<span data-ttu-id="580e0-165">이러한 임계값 중 하나가 충족되면 새 쿼리가 큐에 추가되고 선입선출 방식으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-165">When one of these thresholds is met, new queries are queued and executed on a first-in, first-out basis.</span></span>  <span data-ttu-id="580e0-166">쿼리를 완료 하 고 hello 쿼리 및 슬롯 이하가 hello 제한을 큐에 넣은 쿼리에 해제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-166">As a queries finishes and hello number of queries and slots falls below hello limits, queued queries are released.</span></span> 

> [!NOTE]  
> <span data-ttu-id="580e0-167">*선택* 쿼리 실행에 동적 관리 뷰 (Dmv) 또는 카탈로그 뷰는 영향을 받지 않는 hello 동시성 제한 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-167">*Select* queries executing exclusively on dynamic management views (DMVs) or catalog views are not governed by any of hello concurrency limits.</span></span> <span data-ttu-id="580e0-168">Hello에 실행 하는 쿼리 수에 관계 없이 hello 시스템을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-168">You can monitor hello system regardless of hello number of queries executing on it.</span></span>
> 
> 

## <a name="resource-classes"></a><span data-ttu-id="580e0-169">리소스 클래스</span><span class="sxs-lookup"><span data-stu-id="580e0-169">Resource classes</span></span>
<span data-ttu-id="580e0-170">리소스 클래스 메모리 할당 및 tooa 쿼리를 지정 하는 CPU 주기를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-170">Resource classes help you control memory allocation and CPU cycles given tooa query.</span></span> <span data-ttu-id="580e0-171">두 가지 유형의 데이터베이스 역할의 hello 형태로 클래스 tooa 사용자 리소스를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-171">You can assign two types of resource classes tooa user in hello form of database roles.</span></span> <span data-ttu-id="580e0-172">hello 두 형식의 리소스 클래스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-172">hello two types of resource classes are as follows:</span></span>
1. <span data-ttu-id="580e0-173">동적 리소스 클래스 (**smallrc, mediumrc, largerc, xlargerc**) 가변적인 양의 hello에 따라 메모리를 할당할 현재 DWU 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-173">Dynamic Resource Classes (**smallrc, mediumrc, largerc, xlargerc**) allocate a variable amount of memory depending on hello current DWU.</span></span> <span data-ttu-id="580e0-174">즉, tooa 수직 큰 DWU 쿼리에 더 많은 메모리가 자동으로 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-174">This means that when you scale up tooa larger DWU, your queries automatically get more memory.</span></span> 
2. <span data-ttu-id="580e0-175">정적 리소스 클래스 (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) hello 할당 같은 크기에 관계 없이 메모리의 현재 DWU hello (있는 경우 자체 DWU hello 충분 한 메모리가).</span><span class="sxs-lookup"><span data-stu-id="580e0-175">Static Resource Classes (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) allocate hello same amount of memory regardless of hello current DWU (provided that hello DWU itself has enough memory).</span></span> <span data-ttu-id="580e0-176">즉, 더 큰 DWU에서는 각 리소스 클래스에서 동시에 더 많은 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-176">This means that on larger DWUs, you can run more queries in each resource class concurrently.</span></span>

<span data-ttu-id="580e0-177">**smallrc** 및 **staticrc10**의 사용자에게 더 적은 양의 메모리가 주어져 더 높은 동시성을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-177">Users in **smallrc** and **staticrc10** are given a smaller amount of memory and can take advantage of higher concurrency.</span></span> <span data-ttu-id="580e0-178">반면, 너무 사용자에 게 할당**xlargerc** 또는 **staticrc80** 많은 양의 메모리를 제공 및 따라서 적은 수의 쿼리 동시에 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-178">In contrast, users assigned too**xlargerc** or **staticrc80** are given large amounts of memory, and therefore fewer of their queries can run concurrently.</span></span>

<span data-ttu-id="580e0-179">기본적으로 각 사용자는 hello 작은 리소스 클래스의 멤버는 **smallrc**합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-179">By default, each user is a member of hello small resource class, **smallrc**.</span></span> <span data-ttu-id="580e0-180">프로시저 hello `sp_addrolemember` 은 tooincrease hello 리소스 클래스를 사용 하 고 `sp_droprolemember` 은 toodecrease hello 리소스 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-180">hello procedure `sp_addrolemember` is used tooincrease hello resource class, and `sp_droprolemember` is used toodecrease hello resource class.</span></span> <span data-ttu-id="580e0-181">예를 들어이 명령은 늘어나기 loaduser의 hello 리소스 클래스 너무**largerc**:</span><span class="sxs-lookup"><span data-stu-id="580e0-181">For example, this command would increase hello resource class of loaduser too**largerc**:</span></span>

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a><span data-ttu-id="580e0-182">리소스 클래스를 인식하지 않는 쿼리</span><span class="sxs-lookup"><span data-stu-id="580e0-182">Queries that do not honor resource classes</span></span>

<span data-ttu-id="580e0-183">더 큰 메모리를 할당해도 별로 도움이 되지 않는 일부 쿼리 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-183">There are a few types of queries that do not benefit from a larger memory allocation.</span></span> <span data-ttu-id="580e0-184">hello 시스템의 리소스 클래스 할당 건너뛰고 대신 hello 작은 리소스 클래스에서 이러한 쿼리를 항상 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-184">hello system ignores their resource class allocation and always run these queries in hello small resource class instead.</span></span> <span data-ttu-id="580e0-185">이러한 쿼리는 항상 hello 작은 리소스 클래스에서 실행 하는 경우 동시성 슬롯 압력을 받고 있기 하 고 필요한 것 보다 더 많은 슬롯이 사용 되지 않습니다은 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-185">If these queries always run in hello small resource class, they can run when concurrency slots are under pressure and they won't consume more slots than needed.</span></span> <span data-ttu-id="580e0-186">자세한 내용은 [리소스 클래스 예외](#query-exceptions-to-concurrency-limits) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="580e0-186">See [Resource class exceptions](#query-exceptions-to-concurrency-limits) for more information.</span></span>

## <a name="details-on-resource-class-assignment"></a><span data-ttu-id="580e0-187">리소스 클래스 할당에 대한 세부 정보</span><span class="sxs-lookup"><span data-stu-id="580e0-187">Details on resource class assignment</span></span>


<span data-ttu-id="580e0-188">리소스 클래스에 대한 추가적인 몇 가지 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="580e0-188">A few more details on resource class:</span></span>

* <span data-ttu-id="580e0-189">*역할 alter* 권한이 필요 합니다는 사용자의 toochange hello 리소스 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-189">*Alter role* permission is required toochange hello resource class of a user.</span></span>
* <span data-ttu-id="580e0-190">사용자 tooone 또는 그 이상의 hello 더 높은 리소스 클래스를 추가할 수 있지만 동적 리소스 클래스가 정적 리소스 클래스 보다 우선 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-190">Although you can add a user tooone or more of hello higher resource classes, dynamic resource classes take precedence over static resource classes.</span></span> <span data-ttu-id="580e0-191">즉, 사용자 tooboth 지정 되 면 **mediumrc**(동적) 및 **staticrc80**(정적) **mediumrc** 적용 되므로 hello 리소스 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-191">That is, if a user is assigned tooboth **mediumrc**(dynamic) and **staticrc80**(static), **mediumrc** is hello resource class that is honored.</span></span>
 * <span data-ttu-id="580e0-192">사용자는 특정 리소스 클래스 형식 (여러 개의 동적 리소스 클래스 또는 여러 개의 정적 리소스 클래스)에 자원 하나씩 클래스 보다 toomore에 할당 된 hello 가장 높은 리소스 클래스는 인식 됩니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-192">When a user is assigned toomore than one resource class in a specific resource class type (more than one dynamic resource class or more than one static resource class), hello highest resource class is honored.</span></span> <span data-ttu-id="580e0-193">즉, 사용자는 tooboth mediumrc 및 largerc 할당 되 면 hello 더 높은 리소스 클래스 (largerc) 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-193">That is, if a user is assigned tooboth mediumrc and largerc, hello higher resource class (largerc) is honored.</span></span> <span data-ttu-id="580e0-194">경우에 사용자가 할당 tooboth **staticrc20** 및 **statirc80**, **staticrc80** 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-194">And if a user is assigned tooboth **staticrc20** and **statirc80**, **staticrc80** is honored.</span></span>
* <span data-ttu-id="580e0-195">hello 시스템 관리자가 사용자의 hello 리소스 클래스를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-195">hello resource class of hello system administrative user cannot be changed.</span></span>

<span data-ttu-id="580e0-196">자세한 예제는 [사용자 리소스 클래스 변경 예제](#changing-user-resource-class-example)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="580e0-196">For a detailed example, see [Changing user resource class example](#changing-user-resource-class-example).</span></span>

## <a name="memory-allocation"></a><span data-ttu-id="580e0-197">메모리 할당</span><span class="sxs-lookup"><span data-stu-id="580e0-197">Memory allocation</span></span>
<span data-ttu-id="580e0-198">사용자의 리소스 클래스 장점 및 단점 tooincreasing이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-198">There are pros and cons tooincreasing a user's resource class.</span></span> <span data-ttu-id="580e0-199">증가 하는 사용자에 대 한 리소스 클래스를 의미할 수 있습니다. 쿼리 실행 속도가 빨라집니다 액세스 toomore 메모리 쿼리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-199">Increasing a resource class for a user, gives their queries access toomore memory, which may mean queries execute faster.</span></span>  <span data-ttu-id="580e0-200">그러나 더 높은 리소스 클래스 hello를 실행할 수 있는 동시 쿼리 수가 줄일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-200">However, higher resource classes also reduce hello number of concurrent queries that can run.</span></span> <span data-ttu-id="580e0-201">이 hello 기능 손실을 절충 많은 양의 메모리 tooa 단일 쿼리를 할당 하거나 toorun 동시에 메모리 할당 해야 하는 다른 쿼리를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-201">This is hello trade-off between allocating large amounts of memory tooa single query or allowing other queries, which also need memory allocations, toorun concurrently.</span></span> <span data-ttu-id="580e0-202">액세스 toothat 한 명의 사용자 높은 쿼리에 대 한 메모리 할당 인 경우 다른 사용자에 게는 없습니다 동일한 메모리 toorun 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-202">If one user is given high allocations of memory for a query, other users will not have access toothat same memory toorun a query.</span></span>

<span data-ttu-id="580e0-203">다음 표에서 hello tooeach 배포 DWU 및 리소스 클래스에 의해 할당 된 hello 메모리를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-203">hello following table maps hello memory allocated tooeach distribution by DWU and resource class.</span></span>

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a><span data-ttu-id="580e0-204">동적 리소스 클래스에 대한 배포별 메모리 할당(MB)</span><span class="sxs-lookup"><span data-stu-id="580e0-204">Memory allocations per distribution for dynamic resource classes (MB)</span></span>
| <span data-ttu-id="580e0-205">DWU</span><span class="sxs-lookup"><span data-stu-id="580e0-205">DWU</span></span> | <span data-ttu-id="580e0-206">smallrc</span><span class="sxs-lookup"><span data-stu-id="580e0-206">smallrc</span></span> | <span data-ttu-id="580e0-207">mediumrc</span><span class="sxs-lookup"><span data-stu-id="580e0-207">mediumrc</span></span> | <span data-ttu-id="580e0-208">largerc</span><span class="sxs-lookup"><span data-stu-id="580e0-208">largerc</span></span> | <span data-ttu-id="580e0-209">xlargerc</span><span class="sxs-lookup"><span data-stu-id="580e0-209">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="580e0-210">DW100</span><span class="sxs-lookup"><span data-stu-id="580e0-210">DW100</span></span> |<span data-ttu-id="580e0-211">100</span><span class="sxs-lookup"><span data-stu-id="580e0-211">100</span></span> |<span data-ttu-id="580e0-212">100</span><span class="sxs-lookup"><span data-stu-id="580e0-212">100</span></span> |<span data-ttu-id="580e0-213">200</span><span class="sxs-lookup"><span data-stu-id="580e0-213">200</span></span> |<span data-ttu-id="580e0-214">400</span><span class="sxs-lookup"><span data-stu-id="580e0-214">400</span></span> |
| <span data-ttu-id="580e0-215">DW200</span><span class="sxs-lookup"><span data-stu-id="580e0-215">DW200</span></span> |<span data-ttu-id="580e0-216">100</span><span class="sxs-lookup"><span data-stu-id="580e0-216">100</span></span> |<span data-ttu-id="580e0-217">200</span><span class="sxs-lookup"><span data-stu-id="580e0-217">200</span></span> |<span data-ttu-id="580e0-218">400</span><span class="sxs-lookup"><span data-stu-id="580e0-218">400</span></span> |<span data-ttu-id="580e0-219">800</span><span class="sxs-lookup"><span data-stu-id="580e0-219">800</span></span> |
| <span data-ttu-id="580e0-220">DW300</span><span class="sxs-lookup"><span data-stu-id="580e0-220">DW300</span></span> |<span data-ttu-id="580e0-221">100</span><span class="sxs-lookup"><span data-stu-id="580e0-221">100</span></span> |<span data-ttu-id="580e0-222">200</span><span class="sxs-lookup"><span data-stu-id="580e0-222">200</span></span> |<span data-ttu-id="580e0-223">400</span><span class="sxs-lookup"><span data-stu-id="580e0-223">400</span></span> |<span data-ttu-id="580e0-224">800</span><span class="sxs-lookup"><span data-stu-id="580e0-224">800</span></span> |
| <span data-ttu-id="580e0-225">DW400</span><span class="sxs-lookup"><span data-stu-id="580e0-225">DW400</span></span> |<span data-ttu-id="580e0-226">100</span><span class="sxs-lookup"><span data-stu-id="580e0-226">100</span></span> |<span data-ttu-id="580e0-227">400</span><span class="sxs-lookup"><span data-stu-id="580e0-227">400</span></span> |<span data-ttu-id="580e0-228">800</span><span class="sxs-lookup"><span data-stu-id="580e0-228">800</span></span> |<span data-ttu-id="580e0-229">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-229">1,600</span></span> |
| <span data-ttu-id="580e0-230">DW500</span><span class="sxs-lookup"><span data-stu-id="580e0-230">DW500</span></span> |<span data-ttu-id="580e0-231">100</span><span class="sxs-lookup"><span data-stu-id="580e0-231">100</span></span> |<span data-ttu-id="580e0-232">400</span><span class="sxs-lookup"><span data-stu-id="580e0-232">400</span></span> |<span data-ttu-id="580e0-233">800</span><span class="sxs-lookup"><span data-stu-id="580e0-233">800</span></span> |<span data-ttu-id="580e0-234">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-234">1,600</span></span> |
| <span data-ttu-id="580e0-235">DW600</span><span class="sxs-lookup"><span data-stu-id="580e0-235">DW600</span></span> |<span data-ttu-id="580e0-236">100</span><span class="sxs-lookup"><span data-stu-id="580e0-236">100</span></span> |<span data-ttu-id="580e0-237">400</span><span class="sxs-lookup"><span data-stu-id="580e0-237">400</span></span> |<span data-ttu-id="580e0-238">800</span><span class="sxs-lookup"><span data-stu-id="580e0-238">800</span></span> |<span data-ttu-id="580e0-239">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-239">1,600</span></span> |
| <span data-ttu-id="580e0-240">DW1000</span><span class="sxs-lookup"><span data-stu-id="580e0-240">DW1000</span></span> |<span data-ttu-id="580e0-241">100</span><span class="sxs-lookup"><span data-stu-id="580e0-241">100</span></span> |<span data-ttu-id="580e0-242">800</span><span class="sxs-lookup"><span data-stu-id="580e0-242">800</span></span> |<span data-ttu-id="580e0-243">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-243">1,600</span></span> |<span data-ttu-id="580e0-244">3,200</span><span class="sxs-lookup"><span data-stu-id="580e0-244">3,200</span></span> |
| <span data-ttu-id="580e0-245">DW1200</span><span class="sxs-lookup"><span data-stu-id="580e0-245">DW1200</span></span> |<span data-ttu-id="580e0-246">100</span><span class="sxs-lookup"><span data-stu-id="580e0-246">100</span></span> |<span data-ttu-id="580e0-247">800</span><span class="sxs-lookup"><span data-stu-id="580e0-247">800</span></span> |<span data-ttu-id="580e0-248">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-248">1,600</span></span> |<span data-ttu-id="580e0-249">3,200</span><span class="sxs-lookup"><span data-stu-id="580e0-249">3,200</span></span> |
| <span data-ttu-id="580e0-250">DW1500</span><span class="sxs-lookup"><span data-stu-id="580e0-250">DW1500</span></span> |<span data-ttu-id="580e0-251">100</span><span class="sxs-lookup"><span data-stu-id="580e0-251">100</span></span> |<span data-ttu-id="580e0-252">800</span><span class="sxs-lookup"><span data-stu-id="580e0-252">800</span></span> |<span data-ttu-id="580e0-253">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-253">1,600</span></span> |<span data-ttu-id="580e0-254">3,200</span><span class="sxs-lookup"><span data-stu-id="580e0-254">3,200</span></span> |
| <span data-ttu-id="580e0-255">DW2000</span><span class="sxs-lookup"><span data-stu-id="580e0-255">DW2000</span></span> |<span data-ttu-id="580e0-256">100</span><span class="sxs-lookup"><span data-stu-id="580e0-256">100</span></span> |<span data-ttu-id="580e0-257">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-257">1,600</span></span> |<span data-ttu-id="580e0-258">3,200</span><span class="sxs-lookup"><span data-stu-id="580e0-258">3,200</span></span> |<span data-ttu-id="580e0-259">6,400</span><span class="sxs-lookup"><span data-stu-id="580e0-259">6,400</span></span> |
| <span data-ttu-id="580e0-260">DW3000</span><span class="sxs-lookup"><span data-stu-id="580e0-260">DW3000</span></span> |<span data-ttu-id="580e0-261">100</span><span class="sxs-lookup"><span data-stu-id="580e0-261">100</span></span> |<span data-ttu-id="580e0-262">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-262">1,600</span></span> |<span data-ttu-id="580e0-263">3,200</span><span class="sxs-lookup"><span data-stu-id="580e0-263">3,200</span></span> |<span data-ttu-id="580e0-264">6,400</span><span class="sxs-lookup"><span data-stu-id="580e0-264">6,400</span></span> |
| <span data-ttu-id="580e0-265">DW6000</span><span class="sxs-lookup"><span data-stu-id="580e0-265">DW6000</span></span> |<span data-ttu-id="580e0-266">100</span><span class="sxs-lookup"><span data-stu-id="580e0-266">100</span></span> |<span data-ttu-id="580e0-267">3,200</span><span class="sxs-lookup"><span data-stu-id="580e0-267">3,200</span></span> |<span data-ttu-id="580e0-268">6,400</span><span class="sxs-lookup"><span data-stu-id="580e0-268">6,400</span></span> |<span data-ttu-id="580e0-269">12,800</span><span class="sxs-lookup"><span data-stu-id="580e0-269">12,800</span></span> |

<span data-ttu-id="580e0-270">다음 표에서 hello hello 메모리를 할당 된 tooeach 배포 DWU 정적 리소스 클래스에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-270">hello following table maps hello memory allocated tooeach distribution by DWU and static resource class.</span></span> <span data-ttu-id="580e0-271">리소스 클래스 일수록 hello가 메모리 감소 toohonor hello 글로벌 DWU 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-271">Note that hello higher resource classes have their memory reduced toohonor hello global DWU limits.</span></span>

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a><span data-ttu-id="580e0-272">정적 리소스 클래스에 대한 배포별 메모리 할당(MB)</span><span class="sxs-lookup"><span data-stu-id="580e0-272">Memory allocations per distribution for static resource classes (MB)</span></span>
| <span data-ttu-id="580e0-273">DWU</span><span class="sxs-lookup"><span data-stu-id="580e0-273">DWU</span></span> | <span data-ttu-id="580e0-274">staticrc10</span><span class="sxs-lookup"><span data-stu-id="580e0-274">staticrc10</span></span> | <span data-ttu-id="580e0-275">staticrc20</span><span class="sxs-lookup"><span data-stu-id="580e0-275">staticrc20</span></span> | <span data-ttu-id="580e0-276">staticrc30</span><span class="sxs-lookup"><span data-stu-id="580e0-276">staticrc30</span></span> | <span data-ttu-id="580e0-277">staticrc40</span><span class="sxs-lookup"><span data-stu-id="580e0-277">staticrc40</span></span> | <span data-ttu-id="580e0-278">staticrc50</span><span class="sxs-lookup"><span data-stu-id="580e0-278">staticrc50</span></span> | <span data-ttu-id="580e0-279">staticrc60</span><span class="sxs-lookup"><span data-stu-id="580e0-279">staticrc60</span></span> | <span data-ttu-id="580e0-280">staticrc70</span><span class="sxs-lookup"><span data-stu-id="580e0-280">staticrc70</span></span> | <span data-ttu-id="580e0-281">staticrc80</span><span class="sxs-lookup"><span data-stu-id="580e0-281">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="580e0-282">DW100</span><span class="sxs-lookup"><span data-stu-id="580e0-282">DW100</span></span> |<span data-ttu-id="580e0-283">100</span><span class="sxs-lookup"><span data-stu-id="580e0-283">100</span></span> |<span data-ttu-id="580e0-284">200</span><span class="sxs-lookup"><span data-stu-id="580e0-284">200</span></span> |<span data-ttu-id="580e0-285">400</span><span class="sxs-lookup"><span data-stu-id="580e0-285">400</span></span> |<span data-ttu-id="580e0-286">400</span><span class="sxs-lookup"><span data-stu-id="580e0-286">400</span></span> |<span data-ttu-id="580e0-287">400</span><span class="sxs-lookup"><span data-stu-id="580e0-287">400</span></span> |<span data-ttu-id="580e0-288">400</span><span class="sxs-lookup"><span data-stu-id="580e0-288">400</span></span> |<span data-ttu-id="580e0-289">400</span><span class="sxs-lookup"><span data-stu-id="580e0-289">400</span></span> |<span data-ttu-id="580e0-290">400</span><span class="sxs-lookup"><span data-stu-id="580e0-290">400</span></span> |
| <span data-ttu-id="580e0-291">DW200</span><span class="sxs-lookup"><span data-stu-id="580e0-291">DW200</span></span> |<span data-ttu-id="580e0-292">100</span><span class="sxs-lookup"><span data-stu-id="580e0-292">100</span></span> |<span data-ttu-id="580e0-293">200</span><span class="sxs-lookup"><span data-stu-id="580e0-293">200</span></span> |<span data-ttu-id="580e0-294">400</span><span class="sxs-lookup"><span data-stu-id="580e0-294">400</span></span> |<span data-ttu-id="580e0-295">800</span><span class="sxs-lookup"><span data-stu-id="580e0-295">800</span></span> |<span data-ttu-id="580e0-296">800</span><span class="sxs-lookup"><span data-stu-id="580e0-296">800</span></span> |<span data-ttu-id="580e0-297">800</span><span class="sxs-lookup"><span data-stu-id="580e0-297">800</span></span> |<span data-ttu-id="580e0-298">800</span><span class="sxs-lookup"><span data-stu-id="580e0-298">800</span></span> |<span data-ttu-id="580e0-299">800</span><span class="sxs-lookup"><span data-stu-id="580e0-299">800</span></span> |
| <span data-ttu-id="580e0-300">DW300</span><span class="sxs-lookup"><span data-stu-id="580e0-300">DW300</span></span> |<span data-ttu-id="580e0-301">100</span><span class="sxs-lookup"><span data-stu-id="580e0-301">100</span></span> |<span data-ttu-id="580e0-302">200</span><span class="sxs-lookup"><span data-stu-id="580e0-302">200</span></span> |<span data-ttu-id="580e0-303">400</span><span class="sxs-lookup"><span data-stu-id="580e0-303">400</span></span> |<span data-ttu-id="580e0-304">800</span><span class="sxs-lookup"><span data-stu-id="580e0-304">800</span></span> |<span data-ttu-id="580e0-305">800</span><span class="sxs-lookup"><span data-stu-id="580e0-305">800</span></span> |<span data-ttu-id="580e0-306">800</span><span class="sxs-lookup"><span data-stu-id="580e0-306">800</span></span> |<span data-ttu-id="580e0-307">800</span><span class="sxs-lookup"><span data-stu-id="580e0-307">800</span></span> |<span data-ttu-id="580e0-308">800</span><span class="sxs-lookup"><span data-stu-id="580e0-308">800</span></span> |
| <span data-ttu-id="580e0-309">DW400</span><span class="sxs-lookup"><span data-stu-id="580e0-309">DW400</span></span> |<span data-ttu-id="580e0-310">100</span><span class="sxs-lookup"><span data-stu-id="580e0-310">100</span></span> |<span data-ttu-id="580e0-311">200</span><span class="sxs-lookup"><span data-stu-id="580e0-311">200</span></span> |<span data-ttu-id="580e0-312">400</span><span class="sxs-lookup"><span data-stu-id="580e0-312">400</span></span> |<span data-ttu-id="580e0-313">800</span><span class="sxs-lookup"><span data-stu-id="580e0-313">800</span></span> |<span data-ttu-id="580e0-314">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-314">1,600</span></span> |<span data-ttu-id="580e0-315">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-315">1,600</span></span> |<span data-ttu-id="580e0-316">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-316">1,600</span></span> |<span data-ttu-id="580e0-317">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-317">1,600</span></span> |
| <span data-ttu-id="580e0-318">DW500</span><span class="sxs-lookup"><span data-stu-id="580e0-318">DW500</span></span> |<span data-ttu-id="580e0-319">100</span><span class="sxs-lookup"><span data-stu-id="580e0-319">100</span></span> |<span data-ttu-id="580e0-320">200</span><span class="sxs-lookup"><span data-stu-id="580e0-320">200</span></span> |<span data-ttu-id="580e0-321">400</span><span class="sxs-lookup"><span data-stu-id="580e0-321">400</span></span> |<span data-ttu-id="580e0-322">800</span><span class="sxs-lookup"><span data-stu-id="580e0-322">800</span></span> |<span data-ttu-id="580e0-323">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-323">1,600</span></span> |<span data-ttu-id="580e0-324">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-324">1,600</span></span> |<span data-ttu-id="580e0-325">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-325">1,600</span></span> |<span data-ttu-id="580e0-326">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-326">1,600</span></span> |
| <span data-ttu-id="580e0-327">DW600</span><span class="sxs-lookup"><span data-stu-id="580e0-327">DW600</span></span> |<span data-ttu-id="580e0-328">100</span><span class="sxs-lookup"><span data-stu-id="580e0-328">100</span></span> |<span data-ttu-id="580e0-329">200</span><span class="sxs-lookup"><span data-stu-id="580e0-329">200</span></span> |<span data-ttu-id="580e0-330">400</span><span class="sxs-lookup"><span data-stu-id="580e0-330">400</span></span> |<span data-ttu-id="580e0-331">800</span><span class="sxs-lookup"><span data-stu-id="580e0-331">800</span></span> |<span data-ttu-id="580e0-332">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-332">1,600</span></span> |<span data-ttu-id="580e0-333">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-333">1,600</span></span> |<span data-ttu-id="580e0-334">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-334">1,600</span></span> |<span data-ttu-id="580e0-335">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-335">1,600</span></span> |
| <span data-ttu-id="580e0-336">DW1000</span><span class="sxs-lookup"><span data-stu-id="580e0-336">DW1000</span></span> |<span data-ttu-id="580e0-337">100</span><span class="sxs-lookup"><span data-stu-id="580e0-337">100</span></span> |<span data-ttu-id="580e0-338">200</span><span class="sxs-lookup"><span data-stu-id="580e0-338">200</span></span> |<span data-ttu-id="580e0-339">400</span><span class="sxs-lookup"><span data-stu-id="580e0-339">400</span></span> |<span data-ttu-id="580e0-340">800</span><span class="sxs-lookup"><span data-stu-id="580e0-340">800</span></span> |<span data-ttu-id="580e0-341">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-341">1,600</span></span> |<span data-ttu-id="580e0-342">3,200</span><span class="sxs-lookup"><span data-stu-id="580e0-342">3,200</span></span> |<span data-ttu-id="580e0-343">3,200</span><span class="sxs-lookup"><span data-stu-id="580e0-343">3,200</span></span> |<span data-ttu-id="580e0-344">3,200</span><span class="sxs-lookup"><span data-stu-id="580e0-344">3,200</span></span> |
| <span data-ttu-id="580e0-345">DW1200</span><span class="sxs-lookup"><span data-stu-id="580e0-345">DW1200</span></span> |<span data-ttu-id="580e0-346">100</span><span class="sxs-lookup"><span data-stu-id="580e0-346">100</span></span> |<span data-ttu-id="580e0-347">200</span><span class="sxs-lookup"><span data-stu-id="580e0-347">200</span></span> |<span data-ttu-id="580e0-348">400</span><span class="sxs-lookup"><span data-stu-id="580e0-348">400</span></span> |<span data-ttu-id="580e0-349">800</span><span class="sxs-lookup"><span data-stu-id="580e0-349">800</span></span> |<span data-ttu-id="580e0-350">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-350">1,600</span></span> |<span data-ttu-id="580e0-351">3,200</span><span class="sxs-lookup"><span data-stu-id="580e0-351">3,200</span></span> |<span data-ttu-id="580e0-352">3,200</span><span class="sxs-lookup"><span data-stu-id="580e0-352">3,200</span></span> |<span data-ttu-id="580e0-353">3,200</span><span class="sxs-lookup"><span data-stu-id="580e0-353">3,200</span></span> |
| <span data-ttu-id="580e0-354">DW1500</span><span class="sxs-lookup"><span data-stu-id="580e0-354">DW1500</span></span> |<span data-ttu-id="580e0-355">100</span><span class="sxs-lookup"><span data-stu-id="580e0-355">100</span></span> |<span data-ttu-id="580e0-356">200</span><span class="sxs-lookup"><span data-stu-id="580e0-356">200</span></span> |<span data-ttu-id="580e0-357">400</span><span class="sxs-lookup"><span data-stu-id="580e0-357">400</span></span> |<span data-ttu-id="580e0-358">800</span><span class="sxs-lookup"><span data-stu-id="580e0-358">800</span></span> |<span data-ttu-id="580e0-359">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-359">1,600</span></span> |<span data-ttu-id="580e0-360">3,200</span><span class="sxs-lookup"><span data-stu-id="580e0-360">3,200</span></span> |<span data-ttu-id="580e0-361">3,200</span><span class="sxs-lookup"><span data-stu-id="580e0-361">3,200</span></span> |<span data-ttu-id="580e0-362">3,200</span><span class="sxs-lookup"><span data-stu-id="580e0-362">3,200</span></span> |
| <span data-ttu-id="580e0-363">DW2000</span><span class="sxs-lookup"><span data-stu-id="580e0-363">DW2000</span></span> |<span data-ttu-id="580e0-364">100</span><span class="sxs-lookup"><span data-stu-id="580e0-364">100</span></span> |<span data-ttu-id="580e0-365">200</span><span class="sxs-lookup"><span data-stu-id="580e0-365">200</span></span> |<span data-ttu-id="580e0-366">400</span><span class="sxs-lookup"><span data-stu-id="580e0-366">400</span></span> |<span data-ttu-id="580e0-367">800</span><span class="sxs-lookup"><span data-stu-id="580e0-367">800</span></span> |<span data-ttu-id="580e0-368">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-368">1,600</span></span> |<span data-ttu-id="580e0-369">3,200</span><span class="sxs-lookup"><span data-stu-id="580e0-369">3,200</span></span> |<span data-ttu-id="580e0-370">6,400</span><span class="sxs-lookup"><span data-stu-id="580e0-370">6,400</span></span> |<span data-ttu-id="580e0-371">6,400</span><span class="sxs-lookup"><span data-stu-id="580e0-371">6,400</span></span> |
| <span data-ttu-id="580e0-372">DW3000</span><span class="sxs-lookup"><span data-stu-id="580e0-372">DW3000</span></span> |<span data-ttu-id="580e0-373">100</span><span class="sxs-lookup"><span data-stu-id="580e0-373">100</span></span> |<span data-ttu-id="580e0-374">200</span><span class="sxs-lookup"><span data-stu-id="580e0-374">200</span></span> |<span data-ttu-id="580e0-375">400</span><span class="sxs-lookup"><span data-stu-id="580e0-375">400</span></span> |<span data-ttu-id="580e0-376">800</span><span class="sxs-lookup"><span data-stu-id="580e0-376">800</span></span> |<span data-ttu-id="580e0-377">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-377">1,600</span></span> |<span data-ttu-id="580e0-378">3,200</span><span class="sxs-lookup"><span data-stu-id="580e0-378">3,200</span></span> |<span data-ttu-id="580e0-379">6,400</span><span class="sxs-lookup"><span data-stu-id="580e0-379">6,400</span></span> |<span data-ttu-id="580e0-380">6,400</span><span class="sxs-lookup"><span data-stu-id="580e0-380">6,400</span></span> |
| <span data-ttu-id="580e0-381">DW6000</span><span class="sxs-lookup"><span data-stu-id="580e0-381">DW6000</span></span> |<span data-ttu-id="580e0-382">100</span><span class="sxs-lookup"><span data-stu-id="580e0-382">100</span></span> |<span data-ttu-id="580e0-383">200</span><span class="sxs-lookup"><span data-stu-id="580e0-383">200</span></span> |<span data-ttu-id="580e0-384">400</span><span class="sxs-lookup"><span data-stu-id="580e0-384">400</span></span> |<span data-ttu-id="580e0-385">800</span><span class="sxs-lookup"><span data-stu-id="580e0-385">800</span></span> |<span data-ttu-id="580e0-386">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-386">1,600</span></span> |<span data-ttu-id="580e0-387">3,200</span><span class="sxs-lookup"><span data-stu-id="580e0-387">3,200</span></span> |<span data-ttu-id="580e0-388">6,400</span><span class="sxs-lookup"><span data-stu-id="580e0-388">6,400</span></span> |<span data-ttu-id="580e0-389">12,800</span><span class="sxs-lookup"><span data-stu-id="580e0-389">12,800</span></span> |

<span data-ttu-id="580e0-390">Hello 앞에 테이블을 볼 수 있습니다는 hello에 DW2000에서 실행 되는 쿼리 **xlargerc** 리소스 클래스 액세스 too6, 각 hello 60 분산된 데이터베이스 내에서 메모리의 400MB 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-390">From hello preceding table, you can see that a query running on a DW2000 in hello **xlargerc** resource class would have access too6,400 MB of memory within each of hello 60 distributed databases.</span></span>  <span data-ttu-id="580e0-391">SQL 데이터 웨어하우스에는 배포가 60개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-391">In SQL Data Warehouse, there are 60 distributions.</span></span> <span data-ttu-id="580e0-392">따라서 지정 된 리소스 클래스에서 쿼리를 값 위에 hello에 대 한 toocalculate hello 총 메모리 할당이 60을 곱합니다 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-392">Therefore, toocalculate hello total memory allocation for a query in a given resource class, hello above values should be multiplied by 60.</span></span>

### <a name="memory-allocations-system-wide-gb"></a><span data-ttu-id="580e0-393">시스템 전체 메모리 할당(GB)</span><span class="sxs-lookup"><span data-stu-id="580e0-393">Memory allocations system-wide (GB)</span></span>
| <span data-ttu-id="580e0-394">DWU</span><span class="sxs-lookup"><span data-stu-id="580e0-394">DWU</span></span> | <span data-ttu-id="580e0-395">smallrc</span><span class="sxs-lookup"><span data-stu-id="580e0-395">smallrc</span></span> | <span data-ttu-id="580e0-396">mediumrc</span><span class="sxs-lookup"><span data-stu-id="580e0-396">mediumrc</span></span> | <span data-ttu-id="580e0-397">largerc</span><span class="sxs-lookup"><span data-stu-id="580e0-397">largerc</span></span> | <span data-ttu-id="580e0-398">xlargerc</span><span class="sxs-lookup"><span data-stu-id="580e0-398">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="580e0-399">DW100</span><span class="sxs-lookup"><span data-stu-id="580e0-399">DW100</span></span> |<span data-ttu-id="580e0-400">6</span><span class="sxs-lookup"><span data-stu-id="580e0-400">6</span></span> |<span data-ttu-id="580e0-401">6</span><span class="sxs-lookup"><span data-stu-id="580e0-401">6</span></span> |<span data-ttu-id="580e0-402">12</span><span class="sxs-lookup"><span data-stu-id="580e0-402">12</span></span> |<span data-ttu-id="580e0-403">23</span><span class="sxs-lookup"><span data-stu-id="580e0-403">23</span></span> |
| <span data-ttu-id="580e0-404">DW200</span><span class="sxs-lookup"><span data-stu-id="580e0-404">DW200</span></span> |<span data-ttu-id="580e0-405">6</span><span class="sxs-lookup"><span data-stu-id="580e0-405">6</span></span> |<span data-ttu-id="580e0-406">12</span><span class="sxs-lookup"><span data-stu-id="580e0-406">12</span></span> |<span data-ttu-id="580e0-407">23</span><span class="sxs-lookup"><span data-stu-id="580e0-407">23</span></span> |<span data-ttu-id="580e0-408">47</span><span class="sxs-lookup"><span data-stu-id="580e0-408">47</span></span> |
| <span data-ttu-id="580e0-409">DW300</span><span class="sxs-lookup"><span data-stu-id="580e0-409">DW300</span></span> |<span data-ttu-id="580e0-410">6</span><span class="sxs-lookup"><span data-stu-id="580e0-410">6</span></span> |<span data-ttu-id="580e0-411">12</span><span class="sxs-lookup"><span data-stu-id="580e0-411">12</span></span> |<span data-ttu-id="580e0-412">23</span><span class="sxs-lookup"><span data-stu-id="580e0-412">23</span></span> |<span data-ttu-id="580e0-413">47</span><span class="sxs-lookup"><span data-stu-id="580e0-413">47</span></span> |
| <span data-ttu-id="580e0-414">DW400</span><span class="sxs-lookup"><span data-stu-id="580e0-414">DW400</span></span> |<span data-ttu-id="580e0-415">6</span><span class="sxs-lookup"><span data-stu-id="580e0-415">6</span></span> |<span data-ttu-id="580e0-416">23</span><span class="sxs-lookup"><span data-stu-id="580e0-416">23</span></span> |<span data-ttu-id="580e0-417">47</span><span class="sxs-lookup"><span data-stu-id="580e0-417">47</span></span> |<span data-ttu-id="580e0-418">94</span><span class="sxs-lookup"><span data-stu-id="580e0-418">94</span></span> |
| <span data-ttu-id="580e0-419">DW500</span><span class="sxs-lookup"><span data-stu-id="580e0-419">DW500</span></span> |<span data-ttu-id="580e0-420">6</span><span class="sxs-lookup"><span data-stu-id="580e0-420">6</span></span> |<span data-ttu-id="580e0-421">23</span><span class="sxs-lookup"><span data-stu-id="580e0-421">23</span></span> |<span data-ttu-id="580e0-422">47</span><span class="sxs-lookup"><span data-stu-id="580e0-422">47</span></span> |<span data-ttu-id="580e0-423">94</span><span class="sxs-lookup"><span data-stu-id="580e0-423">94</span></span> |
| <span data-ttu-id="580e0-424">DW600</span><span class="sxs-lookup"><span data-stu-id="580e0-424">DW600</span></span> |<span data-ttu-id="580e0-425">6</span><span class="sxs-lookup"><span data-stu-id="580e0-425">6</span></span> |<span data-ttu-id="580e0-426">23</span><span class="sxs-lookup"><span data-stu-id="580e0-426">23</span></span> |<span data-ttu-id="580e0-427">47</span><span class="sxs-lookup"><span data-stu-id="580e0-427">47</span></span> |<span data-ttu-id="580e0-428">94</span><span class="sxs-lookup"><span data-stu-id="580e0-428">94</span></span> |
| <span data-ttu-id="580e0-429">DW1000</span><span class="sxs-lookup"><span data-stu-id="580e0-429">DW1000</span></span> |<span data-ttu-id="580e0-430">6</span><span class="sxs-lookup"><span data-stu-id="580e0-430">6</span></span> |<span data-ttu-id="580e0-431">47</span><span class="sxs-lookup"><span data-stu-id="580e0-431">47</span></span> |<span data-ttu-id="580e0-432">94</span><span class="sxs-lookup"><span data-stu-id="580e0-432">94</span></span> |<span data-ttu-id="580e0-433">188</span><span class="sxs-lookup"><span data-stu-id="580e0-433">188</span></span> |
| <span data-ttu-id="580e0-434">DW1200</span><span class="sxs-lookup"><span data-stu-id="580e0-434">DW1200</span></span> |<span data-ttu-id="580e0-435">6</span><span class="sxs-lookup"><span data-stu-id="580e0-435">6</span></span> |<span data-ttu-id="580e0-436">47</span><span class="sxs-lookup"><span data-stu-id="580e0-436">47</span></span> |<span data-ttu-id="580e0-437">94</span><span class="sxs-lookup"><span data-stu-id="580e0-437">94</span></span> |<span data-ttu-id="580e0-438">188</span><span class="sxs-lookup"><span data-stu-id="580e0-438">188</span></span> |
| <span data-ttu-id="580e0-439">DW1500</span><span class="sxs-lookup"><span data-stu-id="580e0-439">DW1500</span></span> |<span data-ttu-id="580e0-440">6</span><span class="sxs-lookup"><span data-stu-id="580e0-440">6</span></span> |<span data-ttu-id="580e0-441">47</span><span class="sxs-lookup"><span data-stu-id="580e0-441">47</span></span> |<span data-ttu-id="580e0-442">94</span><span class="sxs-lookup"><span data-stu-id="580e0-442">94</span></span> |<span data-ttu-id="580e0-443">188</span><span class="sxs-lookup"><span data-stu-id="580e0-443">188</span></span> |
| <span data-ttu-id="580e0-444">DW2000</span><span class="sxs-lookup"><span data-stu-id="580e0-444">DW2000</span></span> |<span data-ttu-id="580e0-445">6</span><span class="sxs-lookup"><span data-stu-id="580e0-445">6</span></span> |<span data-ttu-id="580e0-446">94</span><span class="sxs-lookup"><span data-stu-id="580e0-446">94</span></span> |<span data-ttu-id="580e0-447">188</span><span class="sxs-lookup"><span data-stu-id="580e0-447">188</span></span> |<span data-ttu-id="580e0-448">375</span><span class="sxs-lookup"><span data-stu-id="580e0-448">375</span></span> |
| <span data-ttu-id="580e0-449">DW3000</span><span class="sxs-lookup"><span data-stu-id="580e0-449">DW3000</span></span> |<span data-ttu-id="580e0-450">6</span><span class="sxs-lookup"><span data-stu-id="580e0-450">6</span></span> |<span data-ttu-id="580e0-451">94</span><span class="sxs-lookup"><span data-stu-id="580e0-451">94</span></span> |<span data-ttu-id="580e0-452">188</span><span class="sxs-lookup"><span data-stu-id="580e0-452">188</span></span> |<span data-ttu-id="580e0-453">375</span><span class="sxs-lookup"><span data-stu-id="580e0-453">375</span></span> |
| <span data-ttu-id="580e0-454">DW6000</span><span class="sxs-lookup"><span data-stu-id="580e0-454">DW6000</span></span> |<span data-ttu-id="580e0-455">6</span><span class="sxs-lookup"><span data-stu-id="580e0-455">6</span></span> |<span data-ttu-id="580e0-456">188</span><span class="sxs-lookup"><span data-stu-id="580e0-456">188</span></span> |<span data-ttu-id="580e0-457">375</span><span class="sxs-lookup"><span data-stu-id="580e0-457">375</span></span> |<span data-ttu-id="580e0-458">750</span><span class="sxs-lookup"><span data-stu-id="580e0-458">750</span></span> |

<span data-ttu-id="580e0-459">이 테이블은 시스템 차원의 메모리 할당을 볼 수 있습니다 hello xlargerc 리소스 클래스에서 DW2000에서 실행 되는 쿼리는 총 메모리의 375 GB가 할당 되는 (6,400 MB * 60 분포 / 1, 024 tooconvert tooGB) hello 전체 SQL 데이터 웨어하우스를 통해 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-459">From this table of system-wide memory allocations, you can see that a query running on a DW2000 in hello xlargerc resource class is allocated a total of 375 GB of memory (6,400 MB * 60 distributions / 1,024 tooconvert tooGB) over hello entirety of your SQL Data Warehouse.</span></span>

<span data-ttu-id="580e0-460">hello 같은 계산 적용 toostatic 리소스 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-460">hello same calculation applies toostatic resource classes.</span></span>
 
## <a name="concurrency-slot-consumption"></a><span data-ttu-id="580e0-461">동시성 슬롯 사용량</span><span class="sxs-lookup"><span data-stu-id="580e0-461">Concurrency slot consumption</span></span>  
<span data-ttu-id="580e0-462">SQL 데이터 웨어하우스 더 높은 리소스 클래스에서 실행 되는 더 많은 메모리 tooqueries 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-462">SQL Data Warehouse grants more memory tooqueries running in higher resource classes.</span></span> <span data-ttu-id="580e0-463">메모리는 고정된 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-463">Memory is a fixed resource.</span></span>  <span data-ttu-id="580e0-464">쿼리를 더 적은 수의 동시 쿼리를 실행할 수는 hello 당 더 많은 메모리 할당 번호 따라서입니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-464">Therefore, hello more memory allocated per query, hello fewer concurrent queries can execute.</span></span> <span data-ttu-id="580e0-465">hello 다음 표에서 reiterates 모든 hello DWU에서 사용할 수 있는 동시성 슬롯 및 각 리소스 클래스에서 사용 하는 hello 슬롯 수를 표시 하는 단일 뷰에서 hello 이전 개념입니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-465">hello following table reiterates all of hello previous concepts in a single view that shows hello number of concurrency slots available by DWU and hello slots consumed by each resource class.</span></span>  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a><span data-ttu-id="580e0-466">동적 리소스 클래스에 대한 동시성 슬롯의 할당 및 사용량</span><span class="sxs-lookup"><span data-stu-id="580e0-466">Allocation and consumption of concurrency slots for dynamic resource classes</span></span>  
| <span data-ttu-id="580e0-467">DWU</span><span class="sxs-lookup"><span data-stu-id="580e0-467">DWU</span></span> | <span data-ttu-id="580e0-468">최대 동시 쿼리 수</span><span class="sxs-lookup"><span data-stu-id="580e0-468">Maximum concurrent queries</span></span> | <span data-ttu-id="580e0-469">할당된 동시성 슬롯 수</span><span class="sxs-lookup"><span data-stu-id="580e0-469">Concurrency slots allocated</span></span> | <span data-ttu-id="580e0-470">smallrc에서 사용되는 슬롯</span><span class="sxs-lookup"><span data-stu-id="580e0-470">Slots used by smallrc</span></span> | <span data-ttu-id="580e0-471">mediumrc에서 사용되는 슬롯</span><span class="sxs-lookup"><span data-stu-id="580e0-471">Slots used by mediumrc</span></span> | <span data-ttu-id="580e0-472">largerc에서 사용되는 슬롯</span><span class="sxs-lookup"><span data-stu-id="580e0-472">Slots used by largerc</span></span> | <span data-ttu-id="580e0-473">xlargerc에서 사용되는 슬롯</span><span class="sxs-lookup"><span data-stu-id="580e0-473">Slots used by xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="580e0-474">DW100</span><span class="sxs-lookup"><span data-stu-id="580e0-474">DW100</span></span> |<span data-ttu-id="580e0-475">4</span><span class="sxs-lookup"><span data-stu-id="580e0-475">4</span></span> |<span data-ttu-id="580e0-476">4</span><span class="sxs-lookup"><span data-stu-id="580e0-476">4</span></span> |<span data-ttu-id="580e0-477">1</span><span class="sxs-lookup"><span data-stu-id="580e0-477">1</span></span> |<span data-ttu-id="580e0-478">1</span><span class="sxs-lookup"><span data-stu-id="580e0-478">1</span></span> |<span data-ttu-id="580e0-479">2</span><span class="sxs-lookup"><span data-stu-id="580e0-479">2</span></span> |<span data-ttu-id="580e0-480">4</span><span class="sxs-lookup"><span data-stu-id="580e0-480">4</span></span> |
| <span data-ttu-id="580e0-481">DW200</span><span class="sxs-lookup"><span data-stu-id="580e0-481">DW200</span></span> |<span data-ttu-id="580e0-482">8</span><span class="sxs-lookup"><span data-stu-id="580e0-482">8</span></span> |<span data-ttu-id="580e0-483">8</span><span class="sxs-lookup"><span data-stu-id="580e0-483">8</span></span> |<span data-ttu-id="580e0-484">1</span><span class="sxs-lookup"><span data-stu-id="580e0-484">1</span></span> |<span data-ttu-id="580e0-485">2</span><span class="sxs-lookup"><span data-stu-id="580e0-485">2</span></span> |<span data-ttu-id="580e0-486">4</span><span class="sxs-lookup"><span data-stu-id="580e0-486">4</span></span> |<span data-ttu-id="580e0-487">8</span><span class="sxs-lookup"><span data-stu-id="580e0-487">8</span></span> |
| <span data-ttu-id="580e0-488">DW300</span><span class="sxs-lookup"><span data-stu-id="580e0-488">DW300</span></span> |<span data-ttu-id="580e0-489">12</span><span class="sxs-lookup"><span data-stu-id="580e0-489">12</span></span> |<span data-ttu-id="580e0-490">12</span><span class="sxs-lookup"><span data-stu-id="580e0-490">12</span></span> |<span data-ttu-id="580e0-491">1</span><span class="sxs-lookup"><span data-stu-id="580e0-491">1</span></span> |<span data-ttu-id="580e0-492">2</span><span class="sxs-lookup"><span data-stu-id="580e0-492">2</span></span> |<span data-ttu-id="580e0-493">4</span><span class="sxs-lookup"><span data-stu-id="580e0-493">4</span></span> |<span data-ttu-id="580e0-494">8</span><span class="sxs-lookup"><span data-stu-id="580e0-494">8</span></span> |
| <span data-ttu-id="580e0-495">DW400</span><span class="sxs-lookup"><span data-stu-id="580e0-495">DW400</span></span> |<span data-ttu-id="580e0-496">16</span><span class="sxs-lookup"><span data-stu-id="580e0-496">16</span></span> |<span data-ttu-id="580e0-497">16</span><span class="sxs-lookup"><span data-stu-id="580e0-497">16</span></span> |<span data-ttu-id="580e0-498">1</span><span class="sxs-lookup"><span data-stu-id="580e0-498">1</span></span> |<span data-ttu-id="580e0-499">4</span><span class="sxs-lookup"><span data-stu-id="580e0-499">4</span></span> |<span data-ttu-id="580e0-500">8</span><span class="sxs-lookup"><span data-stu-id="580e0-500">8</span></span> |<span data-ttu-id="580e0-501">16</span><span class="sxs-lookup"><span data-stu-id="580e0-501">16</span></span> |
| <span data-ttu-id="580e0-502">DW500</span><span class="sxs-lookup"><span data-stu-id="580e0-502">DW500</span></span> |<span data-ttu-id="580e0-503">20</span><span class="sxs-lookup"><span data-stu-id="580e0-503">20</span></span> |<span data-ttu-id="580e0-504">20</span><span class="sxs-lookup"><span data-stu-id="580e0-504">20</span></span> |<span data-ttu-id="580e0-505">1</span><span class="sxs-lookup"><span data-stu-id="580e0-505">1</span></span> |<span data-ttu-id="580e0-506">4</span><span class="sxs-lookup"><span data-stu-id="580e0-506">4</span></span> |<span data-ttu-id="580e0-507">8</span><span class="sxs-lookup"><span data-stu-id="580e0-507">8</span></span> |<span data-ttu-id="580e0-508">16</span><span class="sxs-lookup"><span data-stu-id="580e0-508">16</span></span> |
| <span data-ttu-id="580e0-509">DW600</span><span class="sxs-lookup"><span data-stu-id="580e0-509">DW600</span></span> |<span data-ttu-id="580e0-510">24</span><span class="sxs-lookup"><span data-stu-id="580e0-510">24</span></span> |<span data-ttu-id="580e0-511">24</span><span class="sxs-lookup"><span data-stu-id="580e0-511">24</span></span> |<span data-ttu-id="580e0-512">1</span><span class="sxs-lookup"><span data-stu-id="580e0-512">1</span></span> |<span data-ttu-id="580e0-513">4</span><span class="sxs-lookup"><span data-stu-id="580e0-513">4</span></span> |<span data-ttu-id="580e0-514">8</span><span class="sxs-lookup"><span data-stu-id="580e0-514">8</span></span> |<span data-ttu-id="580e0-515">16</span><span class="sxs-lookup"><span data-stu-id="580e0-515">16</span></span> |
| <span data-ttu-id="580e0-516">DW1000</span><span class="sxs-lookup"><span data-stu-id="580e0-516">DW1000</span></span> |<span data-ttu-id="580e0-517">32</span><span class="sxs-lookup"><span data-stu-id="580e0-517">32</span></span> |<span data-ttu-id="580e0-518">40</span><span class="sxs-lookup"><span data-stu-id="580e0-518">40</span></span> |<span data-ttu-id="580e0-519">1</span><span class="sxs-lookup"><span data-stu-id="580e0-519">1</span></span> |<span data-ttu-id="580e0-520">8</span><span class="sxs-lookup"><span data-stu-id="580e0-520">8</span></span> |<span data-ttu-id="580e0-521">16</span><span class="sxs-lookup"><span data-stu-id="580e0-521">16</span></span> |<span data-ttu-id="580e0-522">32</span><span class="sxs-lookup"><span data-stu-id="580e0-522">32</span></span> |
| <span data-ttu-id="580e0-523">DW1200</span><span class="sxs-lookup"><span data-stu-id="580e0-523">DW1200</span></span> |<span data-ttu-id="580e0-524">32</span><span class="sxs-lookup"><span data-stu-id="580e0-524">32</span></span> |<span data-ttu-id="580e0-525">48</span><span class="sxs-lookup"><span data-stu-id="580e0-525">48</span></span> |<span data-ttu-id="580e0-526">1</span><span class="sxs-lookup"><span data-stu-id="580e0-526">1</span></span> |<span data-ttu-id="580e0-527">8</span><span class="sxs-lookup"><span data-stu-id="580e0-527">8</span></span> |<span data-ttu-id="580e0-528">16</span><span class="sxs-lookup"><span data-stu-id="580e0-528">16</span></span> |<span data-ttu-id="580e0-529">32</span><span class="sxs-lookup"><span data-stu-id="580e0-529">32</span></span> |
| <span data-ttu-id="580e0-530">DW1500</span><span class="sxs-lookup"><span data-stu-id="580e0-530">DW1500</span></span> |<span data-ttu-id="580e0-531">32</span><span class="sxs-lookup"><span data-stu-id="580e0-531">32</span></span> |<span data-ttu-id="580e0-532">60</span><span class="sxs-lookup"><span data-stu-id="580e0-532">60</span></span> |<span data-ttu-id="580e0-533">1</span><span class="sxs-lookup"><span data-stu-id="580e0-533">1</span></span> |<span data-ttu-id="580e0-534">8</span><span class="sxs-lookup"><span data-stu-id="580e0-534">8</span></span> |<span data-ttu-id="580e0-535">16</span><span class="sxs-lookup"><span data-stu-id="580e0-535">16</span></span> |<span data-ttu-id="580e0-536">32</span><span class="sxs-lookup"><span data-stu-id="580e0-536">32</span></span> |
| <span data-ttu-id="580e0-537">DW2000</span><span class="sxs-lookup"><span data-stu-id="580e0-537">DW2000</span></span> |<span data-ttu-id="580e0-538">32</span><span class="sxs-lookup"><span data-stu-id="580e0-538">32</span></span> |<span data-ttu-id="580e0-539">80</span><span class="sxs-lookup"><span data-stu-id="580e0-539">80</span></span> |<span data-ttu-id="580e0-540">1</span><span class="sxs-lookup"><span data-stu-id="580e0-540">1</span></span> |<span data-ttu-id="580e0-541">16</span><span class="sxs-lookup"><span data-stu-id="580e0-541">16</span></span> |<span data-ttu-id="580e0-542">32</span><span class="sxs-lookup"><span data-stu-id="580e0-542">32</span></span> |<span data-ttu-id="580e0-543">64</span><span class="sxs-lookup"><span data-stu-id="580e0-543">64</span></span> |
| <span data-ttu-id="580e0-544">DW3000</span><span class="sxs-lookup"><span data-stu-id="580e0-544">DW3000</span></span> |<span data-ttu-id="580e0-545">32</span><span class="sxs-lookup"><span data-stu-id="580e0-545">32</span></span> |<span data-ttu-id="580e0-546">120</span><span class="sxs-lookup"><span data-stu-id="580e0-546">120</span></span> |<span data-ttu-id="580e0-547">1</span><span class="sxs-lookup"><span data-stu-id="580e0-547">1</span></span> |<span data-ttu-id="580e0-548">16</span><span class="sxs-lookup"><span data-stu-id="580e0-548">16</span></span> |<span data-ttu-id="580e0-549">32</span><span class="sxs-lookup"><span data-stu-id="580e0-549">32</span></span> |<span data-ttu-id="580e0-550">64</span><span class="sxs-lookup"><span data-stu-id="580e0-550">64</span></span> |
| <span data-ttu-id="580e0-551">DW6000</span><span class="sxs-lookup"><span data-stu-id="580e0-551">DW6000</span></span> |<span data-ttu-id="580e0-552">32</span><span class="sxs-lookup"><span data-stu-id="580e0-552">32</span></span> |<span data-ttu-id="580e0-553">240</span><span class="sxs-lookup"><span data-stu-id="580e0-553">240</span></span> |<span data-ttu-id="580e0-554">1</span><span class="sxs-lookup"><span data-stu-id="580e0-554">1</span></span> |<span data-ttu-id="580e0-555">32</span><span class="sxs-lookup"><span data-stu-id="580e0-555">32</span></span> |<span data-ttu-id="580e0-556">64</span><span class="sxs-lookup"><span data-stu-id="580e0-556">64</span></span> |<span data-ttu-id="580e0-557">128</span><span class="sxs-lookup"><span data-stu-id="580e0-557">128</span></span> |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a><span data-ttu-id="580e0-558">정적 리소스 클래스에 대한 동시성 슬롯의 할당 및 사용량</span><span class="sxs-lookup"><span data-stu-id="580e0-558">Allocation and consumption of concurrency slots for static resource classes</span></span>  
| <span data-ttu-id="580e0-559">DWU</span><span class="sxs-lookup"><span data-stu-id="580e0-559">DWU</span></span> | <span data-ttu-id="580e0-560">최대 동시 쿼리 수</span><span class="sxs-lookup"><span data-stu-id="580e0-560">Maximum concurrent queries</span></span> | <span data-ttu-id="580e0-561">할당된 동시성 슬롯 수</span><span class="sxs-lookup"><span data-stu-id="580e0-561">Concurrency slots allocated</span></span> |<span data-ttu-id="580e0-562">staticrc10</span><span class="sxs-lookup"><span data-stu-id="580e0-562">staticrc10</span></span> | <span data-ttu-id="580e0-563">staticrc20</span><span class="sxs-lookup"><span data-stu-id="580e0-563">staticrc20</span></span> | <span data-ttu-id="580e0-564">staticrc30</span><span class="sxs-lookup"><span data-stu-id="580e0-564">staticrc30</span></span> | <span data-ttu-id="580e0-565">staticrc40</span><span class="sxs-lookup"><span data-stu-id="580e0-565">staticrc40</span></span> | <span data-ttu-id="580e0-566">staticrc50</span><span class="sxs-lookup"><span data-stu-id="580e0-566">staticrc50</span></span> | <span data-ttu-id="580e0-567">staticrc60</span><span class="sxs-lookup"><span data-stu-id="580e0-567">staticrc60</span></span> | <span data-ttu-id="580e0-568">staticrc70</span><span class="sxs-lookup"><span data-stu-id="580e0-568">staticrc70</span></span> | <span data-ttu-id="580e0-569">staticrc80</span><span class="sxs-lookup"><span data-stu-id="580e0-569">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="580e0-570">DW100</span><span class="sxs-lookup"><span data-stu-id="580e0-570">DW100</span></span> |<span data-ttu-id="580e0-571">4</span><span class="sxs-lookup"><span data-stu-id="580e0-571">4</span></span> |<span data-ttu-id="580e0-572">4</span><span class="sxs-lookup"><span data-stu-id="580e0-572">4</span></span> |<span data-ttu-id="580e0-573">1</span><span class="sxs-lookup"><span data-stu-id="580e0-573">1</span></span> |<span data-ttu-id="580e0-574">2</span><span class="sxs-lookup"><span data-stu-id="580e0-574">2</span></span> |<span data-ttu-id="580e0-575">4</span><span class="sxs-lookup"><span data-stu-id="580e0-575">4</span></span> |<span data-ttu-id="580e0-576">4</span><span class="sxs-lookup"><span data-stu-id="580e0-576">4</span></span> |<span data-ttu-id="580e0-577">4</span><span class="sxs-lookup"><span data-stu-id="580e0-577">4</span></span> |<span data-ttu-id="580e0-578">4</span><span class="sxs-lookup"><span data-stu-id="580e0-578">4</span></span> |<span data-ttu-id="580e0-579">4</span><span class="sxs-lookup"><span data-stu-id="580e0-579">4</span></span> |<span data-ttu-id="580e0-580">4</span><span class="sxs-lookup"><span data-stu-id="580e0-580">4</span></span> |
| <span data-ttu-id="580e0-581">DW200</span><span class="sxs-lookup"><span data-stu-id="580e0-581">DW200</span></span> |<span data-ttu-id="580e0-582">8</span><span class="sxs-lookup"><span data-stu-id="580e0-582">8</span></span> |<span data-ttu-id="580e0-583">8</span><span class="sxs-lookup"><span data-stu-id="580e0-583">8</span></span> |<span data-ttu-id="580e0-584">1</span><span class="sxs-lookup"><span data-stu-id="580e0-584">1</span></span> |<span data-ttu-id="580e0-585">2</span><span class="sxs-lookup"><span data-stu-id="580e0-585">2</span></span> |<span data-ttu-id="580e0-586">4</span><span class="sxs-lookup"><span data-stu-id="580e0-586">4</span></span> |<span data-ttu-id="580e0-587">8</span><span class="sxs-lookup"><span data-stu-id="580e0-587">8</span></span> |<span data-ttu-id="580e0-588">8</span><span class="sxs-lookup"><span data-stu-id="580e0-588">8</span></span> |<span data-ttu-id="580e0-589">8</span><span class="sxs-lookup"><span data-stu-id="580e0-589">8</span></span> |<span data-ttu-id="580e0-590">8</span><span class="sxs-lookup"><span data-stu-id="580e0-590">8</span></span> |<span data-ttu-id="580e0-591">8</span><span class="sxs-lookup"><span data-stu-id="580e0-591">8</span></span> |
| <span data-ttu-id="580e0-592">DW300</span><span class="sxs-lookup"><span data-stu-id="580e0-592">DW300</span></span> |<span data-ttu-id="580e0-593">12</span><span class="sxs-lookup"><span data-stu-id="580e0-593">12</span></span> |<span data-ttu-id="580e0-594">12</span><span class="sxs-lookup"><span data-stu-id="580e0-594">12</span></span> |<span data-ttu-id="580e0-595">1</span><span class="sxs-lookup"><span data-stu-id="580e0-595">1</span></span> |<span data-ttu-id="580e0-596">2</span><span class="sxs-lookup"><span data-stu-id="580e0-596">2</span></span> |<span data-ttu-id="580e0-597">4</span><span class="sxs-lookup"><span data-stu-id="580e0-597">4</span></span> |<span data-ttu-id="580e0-598">8</span><span class="sxs-lookup"><span data-stu-id="580e0-598">8</span></span> |<span data-ttu-id="580e0-599">8</span><span class="sxs-lookup"><span data-stu-id="580e0-599">8</span></span> |<span data-ttu-id="580e0-600">8</span><span class="sxs-lookup"><span data-stu-id="580e0-600">8</span></span> |<span data-ttu-id="580e0-601">8</span><span class="sxs-lookup"><span data-stu-id="580e0-601">8</span></span> |<span data-ttu-id="580e0-602">8</span><span class="sxs-lookup"><span data-stu-id="580e0-602">8</span></span> |
| <span data-ttu-id="580e0-603">DW400</span><span class="sxs-lookup"><span data-stu-id="580e0-603">DW400</span></span> |<span data-ttu-id="580e0-604">16</span><span class="sxs-lookup"><span data-stu-id="580e0-604">16</span></span> |<span data-ttu-id="580e0-605">16</span><span class="sxs-lookup"><span data-stu-id="580e0-605">16</span></span> |<span data-ttu-id="580e0-606">1</span><span class="sxs-lookup"><span data-stu-id="580e0-606">1</span></span> |<span data-ttu-id="580e0-607">2</span><span class="sxs-lookup"><span data-stu-id="580e0-607">2</span></span> |<span data-ttu-id="580e0-608">4</span><span class="sxs-lookup"><span data-stu-id="580e0-608">4</span></span> |<span data-ttu-id="580e0-609">8</span><span class="sxs-lookup"><span data-stu-id="580e0-609">8</span></span> |<span data-ttu-id="580e0-610">16</span><span class="sxs-lookup"><span data-stu-id="580e0-610">16</span></span> |<span data-ttu-id="580e0-611">16</span><span class="sxs-lookup"><span data-stu-id="580e0-611">16</span></span> |<span data-ttu-id="580e0-612">16</span><span class="sxs-lookup"><span data-stu-id="580e0-612">16</span></span> |<span data-ttu-id="580e0-613">16</span><span class="sxs-lookup"><span data-stu-id="580e0-613">16</span></span> |
| <span data-ttu-id="580e0-614">DW500</span><span class="sxs-lookup"><span data-stu-id="580e0-614">DW500</span></span> | <span data-ttu-id="580e0-615">20</span><span class="sxs-lookup"><span data-stu-id="580e0-615">20</span></span>| <span data-ttu-id="580e0-616">20</span><span class="sxs-lookup"><span data-stu-id="580e0-616">20</span></span>| <span data-ttu-id="580e0-617">1</span><span class="sxs-lookup"><span data-stu-id="580e0-617">1</span></span>| <span data-ttu-id="580e0-618">2</span><span class="sxs-lookup"><span data-stu-id="580e0-618">2</span></span>| <span data-ttu-id="580e0-619">4</span><span class="sxs-lookup"><span data-stu-id="580e0-619">4</span></span>| <span data-ttu-id="580e0-620">8</span><span class="sxs-lookup"><span data-stu-id="580e0-620">8</span></span>| <span data-ttu-id="580e0-621">16</span><span class="sxs-lookup"><span data-stu-id="580e0-621">16</span></span>| <span data-ttu-id="580e0-622">16</span><span class="sxs-lookup"><span data-stu-id="580e0-622">16</span></span>| <span data-ttu-id="580e0-623">16</span><span class="sxs-lookup"><span data-stu-id="580e0-623">16</span></span>| <span data-ttu-id="580e0-624">16</span><span class="sxs-lookup"><span data-stu-id="580e0-624">16</span></span>|
| <span data-ttu-id="580e0-625">DW600</span><span class="sxs-lookup"><span data-stu-id="580e0-625">DW600</span></span> | <span data-ttu-id="580e0-626">24</span><span class="sxs-lookup"><span data-stu-id="580e0-626">24</span></span>| <span data-ttu-id="580e0-627">24</span><span class="sxs-lookup"><span data-stu-id="580e0-627">24</span></span>| <span data-ttu-id="580e0-628">1</span><span class="sxs-lookup"><span data-stu-id="580e0-628">1</span></span>| <span data-ttu-id="580e0-629">2</span><span class="sxs-lookup"><span data-stu-id="580e0-629">2</span></span>| <span data-ttu-id="580e0-630">4</span><span class="sxs-lookup"><span data-stu-id="580e0-630">4</span></span>| <span data-ttu-id="580e0-631">8</span><span class="sxs-lookup"><span data-stu-id="580e0-631">8</span></span>| <span data-ttu-id="580e0-632">16</span><span class="sxs-lookup"><span data-stu-id="580e0-632">16</span></span>| <span data-ttu-id="580e0-633">16</span><span class="sxs-lookup"><span data-stu-id="580e0-633">16</span></span>| <span data-ttu-id="580e0-634">16</span><span class="sxs-lookup"><span data-stu-id="580e0-634">16</span></span>| <span data-ttu-id="580e0-635">16</span><span class="sxs-lookup"><span data-stu-id="580e0-635">16</span></span>|
| <span data-ttu-id="580e0-636">DW1000</span><span class="sxs-lookup"><span data-stu-id="580e0-636">DW1000</span></span> | <span data-ttu-id="580e0-637">32</span><span class="sxs-lookup"><span data-stu-id="580e0-637">32</span></span>| <span data-ttu-id="580e0-638">40</span><span class="sxs-lookup"><span data-stu-id="580e0-638">40</span></span>| <span data-ttu-id="580e0-639">1</span><span class="sxs-lookup"><span data-stu-id="580e0-639">1</span></span>| <span data-ttu-id="580e0-640">2</span><span class="sxs-lookup"><span data-stu-id="580e0-640">2</span></span>| <span data-ttu-id="580e0-641">4</span><span class="sxs-lookup"><span data-stu-id="580e0-641">4</span></span>| <span data-ttu-id="580e0-642">8</span><span class="sxs-lookup"><span data-stu-id="580e0-642">8</span></span>| <span data-ttu-id="580e0-643">16</span><span class="sxs-lookup"><span data-stu-id="580e0-643">16</span></span>| <span data-ttu-id="580e0-644">32</span><span class="sxs-lookup"><span data-stu-id="580e0-644">32</span></span>| <span data-ttu-id="580e0-645">32</span><span class="sxs-lookup"><span data-stu-id="580e0-645">32</span></span>| <span data-ttu-id="580e0-646">32</span><span class="sxs-lookup"><span data-stu-id="580e0-646">32</span></span>|
| <span data-ttu-id="580e0-647">DW1200</span><span class="sxs-lookup"><span data-stu-id="580e0-647">DW1200</span></span> | <span data-ttu-id="580e0-648">32</span><span class="sxs-lookup"><span data-stu-id="580e0-648">32</span></span>| <span data-ttu-id="580e0-649">48</span><span class="sxs-lookup"><span data-stu-id="580e0-649">48</span></span>| <span data-ttu-id="580e0-650">1</span><span class="sxs-lookup"><span data-stu-id="580e0-650">1</span></span>| <span data-ttu-id="580e0-651">2</span><span class="sxs-lookup"><span data-stu-id="580e0-651">2</span></span>| <span data-ttu-id="580e0-652">4</span><span class="sxs-lookup"><span data-stu-id="580e0-652">4</span></span>| <span data-ttu-id="580e0-653">8</span><span class="sxs-lookup"><span data-stu-id="580e0-653">8</span></span>| <span data-ttu-id="580e0-654">16</span><span class="sxs-lookup"><span data-stu-id="580e0-654">16</span></span>| <span data-ttu-id="580e0-655">32</span><span class="sxs-lookup"><span data-stu-id="580e0-655">32</span></span>| <span data-ttu-id="580e0-656">32</span><span class="sxs-lookup"><span data-stu-id="580e0-656">32</span></span>| <span data-ttu-id="580e0-657">32</span><span class="sxs-lookup"><span data-stu-id="580e0-657">32</span></span>|
| <span data-ttu-id="580e0-658">DW1500</span><span class="sxs-lookup"><span data-stu-id="580e0-658">DW1500</span></span> | <span data-ttu-id="580e0-659">32</span><span class="sxs-lookup"><span data-stu-id="580e0-659">32</span></span>| <span data-ttu-id="580e0-660">60</span><span class="sxs-lookup"><span data-stu-id="580e0-660">60</span></span>| <span data-ttu-id="580e0-661">1</span><span class="sxs-lookup"><span data-stu-id="580e0-661">1</span></span>| <span data-ttu-id="580e0-662">2</span><span class="sxs-lookup"><span data-stu-id="580e0-662">2</span></span>| <span data-ttu-id="580e0-663">4</span><span class="sxs-lookup"><span data-stu-id="580e0-663">4</span></span>| <span data-ttu-id="580e0-664">8</span><span class="sxs-lookup"><span data-stu-id="580e0-664">8</span></span>| <span data-ttu-id="580e0-665">16</span><span class="sxs-lookup"><span data-stu-id="580e0-665">16</span></span>| <span data-ttu-id="580e0-666">32</span><span class="sxs-lookup"><span data-stu-id="580e0-666">32</span></span>| <span data-ttu-id="580e0-667">32</span><span class="sxs-lookup"><span data-stu-id="580e0-667">32</span></span>| <span data-ttu-id="580e0-668">32</span><span class="sxs-lookup"><span data-stu-id="580e0-668">32</span></span>|
| <span data-ttu-id="580e0-669">DW2000</span><span class="sxs-lookup"><span data-stu-id="580e0-669">DW2000</span></span> | <span data-ttu-id="580e0-670">32</span><span class="sxs-lookup"><span data-stu-id="580e0-670">32</span></span>| <span data-ttu-id="580e0-671">80</span><span class="sxs-lookup"><span data-stu-id="580e0-671">80</span></span>| <span data-ttu-id="580e0-672">1</span><span class="sxs-lookup"><span data-stu-id="580e0-672">1</span></span>| <span data-ttu-id="580e0-673">2</span><span class="sxs-lookup"><span data-stu-id="580e0-673">2</span></span>| <span data-ttu-id="580e0-674">4</span><span class="sxs-lookup"><span data-stu-id="580e0-674">4</span></span>| <span data-ttu-id="580e0-675">8</span><span class="sxs-lookup"><span data-stu-id="580e0-675">8</span></span>| <span data-ttu-id="580e0-676">16</span><span class="sxs-lookup"><span data-stu-id="580e0-676">16</span></span>| <span data-ttu-id="580e0-677">32</span><span class="sxs-lookup"><span data-stu-id="580e0-677">32</span></span>| <span data-ttu-id="580e0-678">64</span><span class="sxs-lookup"><span data-stu-id="580e0-678">64</span></span>| <span data-ttu-id="580e0-679">64</span><span class="sxs-lookup"><span data-stu-id="580e0-679">64</span></span>|
| <span data-ttu-id="580e0-680">DW3000</span><span class="sxs-lookup"><span data-stu-id="580e0-680">DW3000</span></span> | <span data-ttu-id="580e0-681">32</span><span class="sxs-lookup"><span data-stu-id="580e0-681">32</span></span>| <span data-ttu-id="580e0-682">120</span><span class="sxs-lookup"><span data-stu-id="580e0-682">120</span></span>| <span data-ttu-id="580e0-683">1</span><span class="sxs-lookup"><span data-stu-id="580e0-683">1</span></span>| <span data-ttu-id="580e0-684">2</span><span class="sxs-lookup"><span data-stu-id="580e0-684">2</span></span>| <span data-ttu-id="580e0-685">4</span><span class="sxs-lookup"><span data-stu-id="580e0-685">4</span></span>| <span data-ttu-id="580e0-686">8</span><span class="sxs-lookup"><span data-stu-id="580e0-686">8</span></span>| <span data-ttu-id="580e0-687">16</span><span class="sxs-lookup"><span data-stu-id="580e0-687">16</span></span>| <span data-ttu-id="580e0-688">32</span><span class="sxs-lookup"><span data-stu-id="580e0-688">32</span></span>| <span data-ttu-id="580e0-689">64</span><span class="sxs-lookup"><span data-stu-id="580e0-689">64</span></span>| <span data-ttu-id="580e0-690">64</span><span class="sxs-lookup"><span data-stu-id="580e0-690">64</span></span>|
| <span data-ttu-id="580e0-691">DW6000</span><span class="sxs-lookup"><span data-stu-id="580e0-691">DW6000</span></span> | <span data-ttu-id="580e0-692">32</span><span class="sxs-lookup"><span data-stu-id="580e0-692">32</span></span>| <span data-ttu-id="580e0-693">240</span><span class="sxs-lookup"><span data-stu-id="580e0-693">240</span></span>| <span data-ttu-id="580e0-694">1</span><span class="sxs-lookup"><span data-stu-id="580e0-694">1</span></span>| <span data-ttu-id="580e0-695">2</span><span class="sxs-lookup"><span data-stu-id="580e0-695">2</span></span>| <span data-ttu-id="580e0-696">4</span><span class="sxs-lookup"><span data-stu-id="580e0-696">4</span></span>| <span data-ttu-id="580e0-697">8</span><span class="sxs-lookup"><span data-stu-id="580e0-697">8</span></span>| <span data-ttu-id="580e0-698">16</span><span class="sxs-lookup"><span data-stu-id="580e0-698">16</span></span>| <span data-ttu-id="580e0-699">32</span><span class="sxs-lookup"><span data-stu-id="580e0-699">32</span></span>| <span data-ttu-id="580e0-700">64</span><span class="sxs-lookup"><span data-stu-id="580e0-700">64</span></span>| <span data-ttu-id="580e0-701">128</span><span class="sxs-lookup"><span data-stu-id="580e0-701">128</span></span>|

<span data-ttu-id="580e0-702">이러한 테이블에서 볼 수 있는 것처럼 DW1000으로 실행되는 SQL 데이터 웨어하우스는 최대 32개의 동시 쿼리 및 총 40개의 동시성 슬롯을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-702">From these tables, you can see that SQL Data Warehouse running as DW1000 allocates a maximum of 32 concurrent queries and a total of 40 concurrency slots.</span></span> <span data-ttu-id="580e0-703">모든 사용자가 smallrc에서 실행하는 경우 각 쿼리가 동시성 슬롯 1개를 소비하므로 32개의 동시성 쿼리가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-703">If all users are running in smallrc, 32 concurrent queries would be allowed because each query would consume 1 concurrency slot.</span></span> <span data-ttu-id="580e0-704">모든 사용자는 DW1000에 mediumrc에서 실행 중이 던, 각 쿼리에 쿼리당 47 gb 전체 메모리 할당에 대 한 분포 당 800MB를 할당할 수는 동시성 개이고 경우 제한 too5 사용자 (40 동시성 슬롯 / mediumrc 사용자 당 8 슬롯이).</span><span class="sxs-lookup"><span data-stu-id="580e0-704">If all users on a DW1000 were running in mediumrc, each query would be allocated 800 MB per distribution for a total memory allocation of 47 GB per query, and concurrency would be limited too5 users (40 concurrency slots / 8 slots per mediumrc user).</span></span>

## <a name="selecting-proper-resource-class"></a><span data-ttu-id="580e0-705">적절한 리소스 클래스 선택</span><span class="sxs-lookup"><span data-stu-id="580e0-705">Selecting proper resource class</span></span>  
<span data-ttu-id="580e0-706">일반적으로 해당 리소스 클래스를 변경 하는 대신 toopermanently assign users tooa 리소스 클래스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-706">A good practice is toopermanently assign users tooa resource class rather than changing their resource classes.</span></span> <span data-ttu-id="580e0-707">예를 들어 로드 tooclustered columnstore 테이블 더 많은 메모리를 할당 하는 경우 더 높은 품질 인덱스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-707">For example, loads tooclustered columnstore tables create higher-quality indexes when allocated more memory.</span></span> <span data-ttu-id="580e0-708">tooensure 로드가 toohigher 메모리를 액세스, 사용자 데이터 로드에 맞게를 만들고이 사용자 tooa 더 높은 리소스 클래스를 영구적으로 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-708">tooensure that loads have access toohigher memory, create a user specifically for loading data and permanently assign this user tooa higher resource class.</span></span>
<span data-ttu-id="580e0-709">모범 사례 toofollow 여기에 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-709">There are a couple of best practices toofollow here.</span></span> <span data-ttu-id="580e0-710">위에서 언급한 것처럼 SQL DW에서는 두 가지 유형의 리소스 클래스 형식, 즉 정적 리소스 클래스 및 동적 리소스 클래스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-710">As mentioned above, SQL DW supports two kinds of resource class types: static resource classes and dynamic resource classes.</span></span>
### <a name="loading-best-practices"></a><span data-ttu-id="580e0-711">로드 모범 사례</span><span class="sxs-lookup"><span data-stu-id="580e0-711">Loading best practices</span></span>
1.  <span data-ttu-id="580e0-712">Hello 기대 일반 양의 데이터를 사용 하 여 로드 인 정적 리소스 클래스는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-712">If hello expectations are loads with regular amount of data, a static resource class is a good choice.</span></span> <span data-ttu-id="580e0-713">나중 더 많은 컴퓨팅 기능, 데이터 웨어하우스 hello tooget 수직 확장 수 없게 됩니다 toorun 더 많은 동시 쿼리 기본, 대로 hello 부하 사용자는 더 많은 메모리를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-713">Later, when scaling up tooget more computational power, hello data warehouse will be able toorun more concurrent queries out-of-the-box, as hello load user does not consume more memory.</span></span>
2.  <span data-ttu-id="580e0-714">Hello 기대 인 큰 부하 일부 경우에는 동적 리소스 클래스는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-714">If hello expectations are bigger loads in some occasions, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="580e0-715">이상에서는 tooget, 더 많은 계산 능력이 늘릴 때 hello 부하 사용자가 알 더 많은 메모리-의-즉시 사용, 따라서 hello 부하 tooperform를 더 빠르게 허용.</span><span class="sxs-lookup"><span data-stu-id="580e0-715">Later, when scaling up tooget more computational power, hello load user will get more memory out-of-the-box, hence allowing hello load tooperform faster.</span></span>

<span data-ttu-id="580e0-716">hello 필요한 메모리 tooprocess 로드 효율적으로 hello 특성에 따라 결정 hello 테이블 로드 및 처리 된 데이터 양을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-716">hello memory needed tooprocess loads efficiently depends on hello nature of hello table loaded and hello amount of data processed.</span></span> <span data-ttu-id="580e0-717">예를 들어, CCI 테이블로 데이터 로드 일부 메모리 toolet CCI rowgroup 한 최적 성을 도달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-717">For instance, loading data into CCI tables requires some memory toolet CCI rowgroups reach optimality.</span></span> <span data-ttu-id="580e0-718">자세한 내용은 hello Columnstore 인덱스 데이터 로드 작업 지침을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="580e0-718">For more details, see hello Columnstore indexes - data loading guidance.</span></span>

<span data-ttu-id="580e0-719">모범 사례로, 좋습니다 toouse 최소한 200MB의 메모리 로드를 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-719">As a best practice, we advise you toouse at least 200MB of memory for loads.</span></span>

### <a name="querying-best-practices"></a><span data-ttu-id="580e0-720">쿼리 모범 사례</span><span class="sxs-lookup"><span data-stu-id="580e0-720">Querying best practices</span></span>
<span data-ttu-id="580e0-721">쿼리마다 복잡성에 따라 다른 요구 사항을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-721">Queries have different requirements depending on their complexity.</span></span> <span data-ttu-id="580e0-722">쿼리당 메모리를 늘리거나 hello 동시성은 증가 모두 올바른 방법 tooaugment hello 쿼리 요구에 따라 전체 처리량입니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-722">Increasing memory per query or increasing hello concurrency are both valid ways tooaugment overall throughput depending on hello query needs.</span></span>
1.  <span data-ttu-id="580e0-723">Hello 기대는 정기적이 고 복잡 한 쿼리 하는 경우 (예를 들어, toogenerate 매일 및 매주 보고서) 및 동시성 tootake 활용 필요 하지 않습니다, 동적 리소스 클래스는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-723">If hello expectations are regular, complex queries (for instance, toogenerate daily and weekly reports) and do not need tootake advantage of concurrency, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="580e0-724">Hello 시스템에 더 많은 데이터 tooprocess 경우 hello 데이터 웨어하우스를 확장 합니다. 따라서을 자동으로 제공 더 많은 메모리 toohello 사용자 hello 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-724">If hello system has more data tooprocess, scaling up hello data warehouse will therefore automatically provide more memory toohello user running hello query.</span></span>
2.  <span data-ttu-id="580e0-725">변수 또는 diurnal 동시성 패턴 hello 기대 하는 경우 (예를 들어 웹 광범위 하 게 액세스할 수 있는 UI 통해 hello 데이터베이스를 쿼리 하는 경우), 정적 리소스 클래스는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-725">If hello expectations are variable or diurnal concurrency patterns (for instance if hello database is queried through a web UI broadly accessible), a static resource class is a good choice.</span></span> <span data-ttu-id="580e0-726">이상에서는 toodata 웨어하우스를 확장 하는 경우 hello 정적 리소스 클래스와 관련 된 hello 사용자가을 자동으로 더 많은 동시 쿼리가 수 toorun 될 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-726">Later, when scaling up toodata warehouse, hello user associated with hello static resource class will automatically be able toorun more concurrent queries.</span></span>

<span data-ttu-id="580e0-727">쿼리 hello 요구에 따라 적절 한 메모리 부여를 선택 하는 hello 테이블 스키마 및 다양 한 조인, 선택 영역 및 그룹 조건자의 hello 특성 hello 쿼리, 데이터 양 등의 많은 요인에 의존 하므로 간단한, 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-727">Selecting proper memory grant depending on hello need of your query is non-trivial, as it depends on many factors, such as hello amount of data queried, hello nature of hello table schemas, and various join, selection, and group predicates.</span></span> <span data-ttu-id="580e0-728">쿼리 toocomplete 속도가 더 하면 있지만 높이면 더 많은 메모리 할당 하는 일반 관점에서 전반적인 동시성 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-728">From a general standpoint, allocating more memory will allow queries toocomplete faster, but would reduce hello overall concurrency.</span></span> <span data-ttu-id="580e0-729">동시성이 문제가 되지 않을 경우 메모리를 과도하게 할당해도 괜찮습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-729">If concurrency is not an issue, over-allocating memory does not harm.</span></span> <span data-ttu-id="580e0-730">toofine 조정 처리량, 다양 한 리소스 클래스를 시도 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-730">toofine-tune throughput, trying various flavors of resource classes may be required.</span></span>

<span data-ttu-id="580e0-731">Hello 다음 저장을 사용할 수 있습니다에 지정된 된 SLO 및 hello 가장 가까운 최상의 리소스 클래스에 대 한 메모리 집약적 CCI 작업에 지정 된 리소스 클래스 CCI 테이블 분할 되지 않은 리소스 클래스당 동시성 및 메모리 부여 아웃 toofigure 프로시저:</span><span class="sxs-lookup"><span data-stu-id="580e0-731">You can use hello following stored procedure toofigure out concurrency and memory grant per resource class at a given SLO and hello closest best resource class for memory intensive CCI operations on non-partitioned CCI table at a given resource class:</span></span>

#### <a name="description"></a><span data-ttu-id="580e0-732">설명:</span><span class="sxs-lookup"><span data-stu-id="580e0-732">Description:</span></span>  
<span data-ttu-id="580e0-733">이 저장된 프로시저의 hello 용도 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-733">Here's hello purpose of this stored procedure:</span></span>  
1. <span data-ttu-id="580e0-734">지정 된 SLO에 리소스 클래스당 동시성 및 메모리 부여 아웃 toohelp 사용자 그림입니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-734">toohelp user figure out concurrency and memory grant per resource class at a given SLO.</span></span> <span data-ttu-id="580e0-735">아래 hello 예에 나와 있는 것 처럼 사용자 tooprovide NULL 스키마와 테이블 이름에 대 한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-735">User needs tooprovide NULL for both schema and tablename for this as shown in hello example below.</span></span>  
2. <span data-ttu-id="580e0-736">지정 된 리소스 클래스에서 아닌 분할된 CCI 테이블에 대해 CCI 작업 (로드, 테이블 복사 다시 인덱스 등 빌드) hello 가장 가까운 최상의 리소스에 대 한 클래스 hello 메모리 intensed toohelp 사용자 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-736">toohelp user figure out hello closest best resource class for hello memory intensed CCI operations (load, copy table, rebuild index, etc.) on non partitioned CCI table at a given resource class.</span></span> <span data-ttu-id="580e0-737">테이블 스키마 toofind 아웃 hello 필요한 메모리 부여를 사용 하 여이 대 한 hello 저장 프로시저.</span><span class="sxs-lookup"><span data-stu-id="580e0-737">hello stored proc uses table schema toofind out hello required memory grant for this.</span></span>

#### <a name="dependencies--restrictions"></a><span data-ttu-id="580e0-738">종속성 및 제한 사항:</span><span class="sxs-lookup"><span data-stu-id="580e0-738">Dependencies & Restrictions:</span></span>
- <span data-ttu-id="580e0-739">이 저장된 프로시저 cci를 분할 된 테이블에 대 한 디자인 된 toocalculate 메모리 요구 사항이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-739">This stored proc is not designed toocalculate memory requirement for partitioned-cci table.</span></span>    
- <span data-ttu-id="580e0-740">이 저장된 프로시저의 SELECT/INSERT-CTAS hello SELECT 부분에 대 한 계정으로 메모리 요구 사항이 사용 하지 않습니다 및 toobe 간단한 SELECT를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-740">This stored proc doesn't take memory requirement into account for hello SELECT part of CTAS/INSERT-SELECT and assumes it toobe a simple SELECT.</span></span>
- <span data-ttu-id="580e0-741">이 저장된 프로시저를이 사용할 수 있도록 hello 세션에서이 저장된 프로시저가 생성 된 임시 테이블을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-741">This stored proc uses a temp table so this can be used in hello session where this stored proc was created.</span></span>    
- <span data-ttu-id="580e0-742">이 저장된 프로시저를 hello 현재 제품 (예: 하드웨어 구성, DMS 구성)에 따라 달라 집니다 하 고는 식의 변경 되 면 다음이 저장된 프로시저를 올바르게 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-742">This stored proc depends on hello current offerings (e.g. hardware configuration, DMS config) and if any of that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="580e0-743">이 저장 프로시저는 기존의 제공된 동시성 제한에 의존하므로 이러한 동시성 제한이 변경되면 이 저장 프로시저가 제대로 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-743">This stored proc depends on existing offered concurrency limit and if that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="580e0-744">이 저장 프로시저는 기존에 제공된 리소스 클래스에 의존하므로 이러한 리소스 클래스가 변경되면 이 저장 프로시저가 제대로 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-744">This stored proc depends on existing resource class offerings and if that changes then this stored proc wuold not work correctly.</span></span>  

>  [!NOTE]  
>  <span data-ttu-id="580e0-745">제공된 매개 변수로 저장 프로시저를 실행한 후에 출력이 표시되지 않으면 다음 2가지 경우로 가정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-745">If you are not getting output after executing stored procedure with parameters provided then there could be two cases.</span></span> <br /><span data-ttu-id="580e0-746">1. DW 매개 변수 중 하나에 잘못된 SLO 값이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-746">1. Either DW Parameter contains invalid SLO value</span></span> <br /><span data-ttu-id="580e0-747">2. 또는 테이블 이름이 제공된 경우 CCI 작업에 대해 일치하는 리소스 클래스가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-747">2. OR there are no matching resource class for CCI operation if table name was provided.</span></span> <br /><span data-ttu-id="580e0-748">예를 들어 DW100, 사용 가능한 가장 높은 메모리 부여 400MB 하 고 충분 한 toocross hello 요구 사항은 400mb 테이블 스키마는 넓은 경우.</span><span class="sxs-lookup"><span data-stu-id="580e0-748">For example, at DW100, highest memory grant available is 400MB and if table schema is wide enough toocross hello requirement of 400MB.</span></span>
      
#### <a name="usage-example"></a><span data-ttu-id="580e0-749">사용법 예제:</span><span class="sxs-lookup"><span data-stu-id="580e0-749">Usage example:</span></span>
<span data-ttu-id="580e0-750">구문</span><span class="sxs-lookup"><span data-stu-id="580e0-750">Syntax:</span></span>  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. <span data-ttu-id="580e0-751">@DWU:NULL 매개 변수 tooextract 제공 하거나 hello DW DB에서에서 현재 DWU hello 또는 지원 되는 모든 DWU 'DW100' hello 형태로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-751">@DWU: Either provide a NULL parameter tooextract hello current DWU from hello DW DB or provide any supported DWU in hello form of 'DW100'</span></span>
2. <span data-ttu-id="580e0-752">@SCHEMA_NAME:Hello 테이블의 스키마 이름 제공</span><span class="sxs-lookup"><span data-stu-id="580e0-752">@SCHEMA_NAME: Provide a schema name of hello table</span></span>
3. <span data-ttu-id="580e0-753">@TABLE_NAME:Hello 관심 있는 테이블 이름을 제공합니다</span><span class="sxs-lookup"><span data-stu-id="580e0-753">@TABLE_NAME: Provide a table name of hello interest</span></span>

<span data-ttu-id="580e0-754">이 저장 프로시저 실행 예제:</span><span class="sxs-lookup"><span data-stu-id="580e0-754">Examples executing this stored proc:</span></span>  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

<span data-ttu-id="580e0-755">아래와 같이 hello 위의 예제에서에서 사용 하는 표 1은 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-755">Table1 used in hello above examples could be created as below:</span></span>  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-hello-stored-procedure-definition"></a><span data-ttu-id="580e0-756">Hello 저장 프로시저 정의 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-756">Here's hello stored procedure definition:</span></span>
```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(   @DWU VARCHAR(7),
      @SCHEMA_NAME VARCHAR(128),
       @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for hello current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need toosupply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) toohold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping tootheir corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```

## <a name="query-importance"></a><span data-ttu-id="580e0-757">쿼리 중요도</span><span class="sxs-lookup"><span data-stu-id="580e0-757">Query importance</span></span>
<span data-ttu-id="580e0-758">SQL 데이터 웨어하우스는 워크로드 그룹을 사용하여 리소스 클래스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-758">SQL Data Warehouse implements resource classes by using workload groups.</span></span> <span data-ttu-id="580e0-759">다양 한 DWU 크기 hello에서 hello 리소스 클래스의 hello 동작을 제어 하는 8 개의 작업 그룹의 총 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-759">There are a total of eight workload groups that control hello behavior of hello resource classes across hello various DWU sizes.</span></span> <span data-ttu-id="580e0-760">모든 DWU에 대 한 SQL 데이터 웨어하우스 hello 8 개의 작업 그룹의 4만 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-760">For any DWU, SQL Data Warehouse uses only four of hello eight workload groups.</span></span> <span data-ttu-id="580e0-761">각 작업 그룹의 4 개 리소스 클래스 tooone 지정 되기 때문에 이렇게 하면 의미: smallrc, mediumrc, largerc, 또는 xlargerc 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-761">This makes sense because each workload group is assigned tooone of four resource classes: smallrc, mediumrc, largerc, or xlargerc.</span></span> <span data-ttu-id="580e0-762">hello 이해 hello 작업 그룹의 중요도 이러한 작업 그룹의 일부 설정 된다는 점 toohigher *중요도*합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-762">hello importance of understanding hello workload groups is that some of these workload groups are set toohigher *importance*.</span></span> <span data-ttu-id="580e0-763">중요도가 CPU 예약에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-763">Importance is used for CPU scheduling.</span></span> <span data-ttu-id="580e0-764">높은 중요도를 갖고 실행되는 쿼리는 중간 중요도의 쿼리보다 3배 더 많은 CPU 사이클을 받게 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-764">Queries run with high importance will get three times more CPU cycles than those with medium importance.</span></span> <span data-ttu-id="580e0-765">따라서 동시성 슬롯 매핑은 또한 CPU 우선 순위를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-765">Therefore, concurrency slot mappings also determine CPU priority.</span></span> <span data-ttu-id="580e0-766">쿼리가 16개 이상의 슬롯을 사용할 경우 중요도 높음으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-766">When a query consumes 16 or more slots, it runs as high importance.</span></span>

<span data-ttu-id="580e0-767">hello 다음 표에 각 작업 그룹에 대 한 hello 중요도 매핑이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-767">hello following table shows hello importance mappings for each workload group.</span></span>

### <a name="workload-group-mappings-tooconcurrency-slots-and-importance"></a><span data-ttu-id="580e0-768">작업 그룹 매핑 tooconcurrency 슬롯 및 중요도</span><span class="sxs-lookup"><span data-stu-id="580e0-768">Workload group mappings tooconcurrency slots and importance</span></span>
| <span data-ttu-id="580e0-769">워크로드 그룹</span><span class="sxs-lookup"><span data-stu-id="580e0-769">Workload groups</span></span> | <span data-ttu-id="580e0-770">동시성 슬롯 매핑</span><span class="sxs-lookup"><span data-stu-id="580e0-770">Concurrency slot mapping</span></span> | <span data-ttu-id="580e0-771">MB/배포</span><span class="sxs-lookup"><span data-stu-id="580e0-771">MB / Distribution</span></span> | <span data-ttu-id="580e0-772">중요도 매핑</span><span class="sxs-lookup"><span data-stu-id="580e0-772">Importance mapping</span></span> |
|:--- |:---:|:---:|:--- |
| <span data-ttu-id="580e0-773">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="580e0-773">SloDWGroupC00</span></span> |<span data-ttu-id="580e0-774">1</span><span class="sxs-lookup"><span data-stu-id="580e0-774">1</span></span> |<span data-ttu-id="580e0-775">100</span><span class="sxs-lookup"><span data-stu-id="580e0-775">100</span></span> |<span data-ttu-id="580e0-776">중간</span><span class="sxs-lookup"><span data-stu-id="580e0-776">Medium</span></span> |
| <span data-ttu-id="580e0-777">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="580e0-777">SloDWGroupC01</span></span> |<span data-ttu-id="580e0-778">2</span><span class="sxs-lookup"><span data-stu-id="580e0-778">2</span></span> |<span data-ttu-id="580e0-779">200</span><span class="sxs-lookup"><span data-stu-id="580e0-779">200</span></span> |<span data-ttu-id="580e0-780">중간</span><span class="sxs-lookup"><span data-stu-id="580e0-780">Medium</span></span> |
| <span data-ttu-id="580e0-781">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="580e0-781">SloDWGroupC02</span></span> |<span data-ttu-id="580e0-782">4</span><span class="sxs-lookup"><span data-stu-id="580e0-782">4</span></span> |<span data-ttu-id="580e0-783">400</span><span class="sxs-lookup"><span data-stu-id="580e0-783">400</span></span> |<span data-ttu-id="580e0-784">중간</span><span class="sxs-lookup"><span data-stu-id="580e0-784">Medium</span></span> |
| <span data-ttu-id="580e0-785">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="580e0-785">SloDWGroupC03</span></span> |<span data-ttu-id="580e0-786">8</span><span class="sxs-lookup"><span data-stu-id="580e0-786">8</span></span> |<span data-ttu-id="580e0-787">800</span><span class="sxs-lookup"><span data-stu-id="580e0-787">800</span></span> |<span data-ttu-id="580e0-788">중간</span><span class="sxs-lookup"><span data-stu-id="580e0-788">Medium</span></span> |
| <span data-ttu-id="580e0-789">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="580e0-789">SloDWGroupC04</span></span> |<span data-ttu-id="580e0-790">16</span><span class="sxs-lookup"><span data-stu-id="580e0-790">16</span></span> |<span data-ttu-id="580e0-791">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-791">1,600</span></span> |<span data-ttu-id="580e0-792">높음</span><span class="sxs-lookup"><span data-stu-id="580e0-792">High</span></span> |
| <span data-ttu-id="580e0-793">SloDWGroupC05</span><span class="sxs-lookup"><span data-stu-id="580e0-793">SloDWGroupC05</span></span> |<span data-ttu-id="580e0-794">32</span><span class="sxs-lookup"><span data-stu-id="580e0-794">32</span></span> |<span data-ttu-id="580e0-795">3,200</span><span class="sxs-lookup"><span data-stu-id="580e0-795">3,200</span></span> |<span data-ttu-id="580e0-796">높음</span><span class="sxs-lookup"><span data-stu-id="580e0-796">High</span></span> |
| <span data-ttu-id="580e0-797">SloDWGroupC06</span><span class="sxs-lookup"><span data-stu-id="580e0-797">SloDWGroupC06</span></span> |<span data-ttu-id="580e0-798">64</span><span class="sxs-lookup"><span data-stu-id="580e0-798">64</span></span> |<span data-ttu-id="580e0-799">6,400</span><span class="sxs-lookup"><span data-stu-id="580e0-799">6,400</span></span> |<span data-ttu-id="580e0-800">높음</span><span class="sxs-lookup"><span data-stu-id="580e0-800">High</span></span> |
| <span data-ttu-id="580e0-801">SloDWGroupC07</span><span class="sxs-lookup"><span data-stu-id="580e0-801">SloDWGroupC07</span></span> |<span data-ttu-id="580e0-802">128</span><span class="sxs-lookup"><span data-stu-id="580e0-802">128</span></span> |<span data-ttu-id="580e0-803">12,800</span><span class="sxs-lookup"><span data-stu-id="580e0-803">12,800</span></span> |<span data-ttu-id="580e0-804">높음</span><span class="sxs-lookup"><span data-stu-id="580e0-804">High</span></span> |

<span data-ttu-id="580e0-805">Hello에서 **할당 및 동시성 슬롯의 소비** 차트는 DW500에서는 1, 4, 8 또는 16 동시성 슬롯 smallrc, mediumrc, largerc, 및 xlargerc, 각각을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-805">From hello **Allocation and consumption of concurrency slots** chart, you can see that a DW500 uses 1, 4, 8 or 16 concurrency slots for smallrc, mediumrc, largerc, and xlargerc, respectively.</span></span> <span data-ttu-id="580e0-806">각 리소스 클래스에 대 한 차트 toofind hello 중요도 앞 hello에 해당 값을 조회할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-806">You can look those values up in hello preceding chart toofind hello importance for each resource class.</span></span>

### <a name="dw500-mapping-of-resource-classes-tooimportance"></a><span data-ttu-id="580e0-807">리소스 클래스 tooimportance의 DW500 매핑</span><span class="sxs-lookup"><span data-stu-id="580e0-807">DW500 mapping of resource classes tooimportance</span></span>
| <span data-ttu-id="580e0-808">리소스 클래스</span><span class="sxs-lookup"><span data-stu-id="580e0-808">Resource class</span></span> | <span data-ttu-id="580e0-809">워크로드 그룹</span><span class="sxs-lookup"><span data-stu-id="580e0-809">Workload group</span></span> | <span data-ttu-id="580e0-810">사용된 동시성 슬롯 수</span><span class="sxs-lookup"><span data-stu-id="580e0-810">Concurrency slots used</span></span> | <span data-ttu-id="580e0-811">MB/배포</span><span class="sxs-lookup"><span data-stu-id="580e0-811">MB / Distribution</span></span> | <span data-ttu-id="580e0-812">중요도</span><span class="sxs-lookup"><span data-stu-id="580e0-812">Importance</span></span> |
|:--- |:--- |:---:|:---:|:--- |
| <span data-ttu-id="580e0-813">smallrc</span><span class="sxs-lookup"><span data-stu-id="580e0-813">smallrc</span></span> |<span data-ttu-id="580e0-814">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="580e0-814">SloDWGroupC00</span></span> |<span data-ttu-id="580e0-815">1</span><span class="sxs-lookup"><span data-stu-id="580e0-815">1</span></span> |<span data-ttu-id="580e0-816">100</span><span class="sxs-lookup"><span data-stu-id="580e0-816">100</span></span> |<span data-ttu-id="580e0-817">중간</span><span class="sxs-lookup"><span data-stu-id="580e0-817">Medium</span></span> |
| <span data-ttu-id="580e0-818">mediumrc</span><span class="sxs-lookup"><span data-stu-id="580e0-818">mediumrc</span></span> |<span data-ttu-id="580e0-819">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="580e0-819">SloDWGroupC02</span></span> |<span data-ttu-id="580e0-820">4</span><span class="sxs-lookup"><span data-stu-id="580e0-820">4</span></span> |<span data-ttu-id="580e0-821">400</span><span class="sxs-lookup"><span data-stu-id="580e0-821">400</span></span> |<span data-ttu-id="580e0-822">중간</span><span class="sxs-lookup"><span data-stu-id="580e0-822">Medium</span></span> |
| <span data-ttu-id="580e0-823">largerc</span><span class="sxs-lookup"><span data-stu-id="580e0-823">largerc</span></span> |<span data-ttu-id="580e0-824">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="580e0-824">SloDWGroupC03</span></span> |<span data-ttu-id="580e0-825">8</span><span class="sxs-lookup"><span data-stu-id="580e0-825">8</span></span> |<span data-ttu-id="580e0-826">800</span><span class="sxs-lookup"><span data-stu-id="580e0-826">800</span></span> |<span data-ttu-id="580e0-827">중간</span><span class="sxs-lookup"><span data-stu-id="580e0-827">Medium</span></span> |
| <span data-ttu-id="580e0-828">xlargerc</span><span class="sxs-lookup"><span data-stu-id="580e0-828">xlargerc</span></span> |<span data-ttu-id="580e0-829">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="580e0-829">SloDWGroupC04</span></span> |<span data-ttu-id="580e0-830">16</span><span class="sxs-lookup"><span data-stu-id="580e0-830">16</span></span> |<span data-ttu-id="580e0-831">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-831">1,600</span></span> |<span data-ttu-id="580e0-832">높음</span><span class="sxs-lookup"><span data-stu-id="580e0-832">High</span></span> |
| <span data-ttu-id="580e0-833">staticrc10</span><span class="sxs-lookup"><span data-stu-id="580e0-833">staticrc10</span></span> |<span data-ttu-id="580e0-834">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="580e0-834">SloDWGroupC00</span></span> |<span data-ttu-id="580e0-835">1</span><span class="sxs-lookup"><span data-stu-id="580e0-835">1</span></span> |<span data-ttu-id="580e0-836">100</span><span class="sxs-lookup"><span data-stu-id="580e0-836">100</span></span> |<span data-ttu-id="580e0-837">중간</span><span class="sxs-lookup"><span data-stu-id="580e0-837">Medium</span></span> |
| <span data-ttu-id="580e0-838">staticrc20</span><span class="sxs-lookup"><span data-stu-id="580e0-838">staticrc20</span></span> |<span data-ttu-id="580e0-839">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="580e0-839">SloDWGroupC01</span></span> |<span data-ttu-id="580e0-840">2</span><span class="sxs-lookup"><span data-stu-id="580e0-840">2</span></span> |<span data-ttu-id="580e0-841">200</span><span class="sxs-lookup"><span data-stu-id="580e0-841">200</span></span> |<span data-ttu-id="580e0-842">중간</span><span class="sxs-lookup"><span data-stu-id="580e0-842">Medium</span></span> |
| <span data-ttu-id="580e0-843">staticrc30</span><span class="sxs-lookup"><span data-stu-id="580e0-843">staticrc30</span></span> |<span data-ttu-id="580e0-844">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="580e0-844">SloDWGroupC02</span></span> |<span data-ttu-id="580e0-845">4</span><span class="sxs-lookup"><span data-stu-id="580e0-845">4</span></span> |<span data-ttu-id="580e0-846">400</span><span class="sxs-lookup"><span data-stu-id="580e0-846">400</span></span> |<span data-ttu-id="580e0-847">중간</span><span class="sxs-lookup"><span data-stu-id="580e0-847">Medium</span></span> |
| <span data-ttu-id="580e0-848">staticrc40</span><span class="sxs-lookup"><span data-stu-id="580e0-848">staticrc40</span></span> |<span data-ttu-id="580e0-849">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="580e0-849">SloDWGroupC03</span></span> |<span data-ttu-id="580e0-850">8</span><span class="sxs-lookup"><span data-stu-id="580e0-850">8</span></span> |<span data-ttu-id="580e0-851">800</span><span class="sxs-lookup"><span data-stu-id="580e0-851">800</span></span> |<span data-ttu-id="580e0-852">중간</span><span class="sxs-lookup"><span data-stu-id="580e0-852">Medium</span></span> |
| <span data-ttu-id="580e0-853">staticrc50</span><span class="sxs-lookup"><span data-stu-id="580e0-853">staticrc50</span></span> |<span data-ttu-id="580e0-854">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="580e0-854">SloDWGroupC03</span></span> |<span data-ttu-id="580e0-855">16</span><span class="sxs-lookup"><span data-stu-id="580e0-855">16</span></span> |<span data-ttu-id="580e0-856">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-856">1,600</span></span> |<span data-ttu-id="580e0-857">높음</span><span class="sxs-lookup"><span data-stu-id="580e0-857">High</span></span> |
| <span data-ttu-id="580e0-858">staticrc60</span><span class="sxs-lookup"><span data-stu-id="580e0-858">staticrc60</span></span> |<span data-ttu-id="580e0-859">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="580e0-859">SloDWGroupC03</span></span> |<span data-ttu-id="580e0-860">16</span><span class="sxs-lookup"><span data-stu-id="580e0-860">16</span></span> |<span data-ttu-id="580e0-861">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-861">1,600</span></span> |<span data-ttu-id="580e0-862">높음</span><span class="sxs-lookup"><span data-stu-id="580e0-862">High</span></span> |
| <span data-ttu-id="580e0-863">staticrc70</span><span class="sxs-lookup"><span data-stu-id="580e0-863">staticrc70</span></span> |<span data-ttu-id="580e0-864">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="580e0-864">SloDWGroupC03</span></span> |<span data-ttu-id="580e0-865">16</span><span class="sxs-lookup"><span data-stu-id="580e0-865">16</span></span> |<span data-ttu-id="580e0-866">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-866">1,600</span></span> |<span data-ttu-id="580e0-867">높음</span><span class="sxs-lookup"><span data-stu-id="580e0-867">High</span></span> |
| <span data-ttu-id="580e0-868">staticrc80</span><span class="sxs-lookup"><span data-stu-id="580e0-868">staticrc80</span></span> |<span data-ttu-id="580e0-869">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="580e0-869">SloDWGroupC03</span></span> |<span data-ttu-id="580e0-870">16</span><span class="sxs-lookup"><span data-stu-id="580e0-870">16</span></span> |<span data-ttu-id="580e0-871">1,600</span><span class="sxs-lookup"><span data-stu-id="580e0-871">1,600</span></span> |<span data-ttu-id="580e0-872">높음</span><span class="sxs-lookup"><span data-stu-id="580e0-872">High</span></span> |

<span data-ttu-id="580e0-873">Hello hello 차이 hello 리소스 관리자의 hello 관점 또는 hello 작업 그룹의 현재 및 이제 까지의 사용 tooanalyze 자세히 메모리 리소스 할당에서 DMV 쿼리 toolook 문제를 해결 하려면 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-873">You can use hello following DMV query toolook at hello differences in memory resource allocation in detail from hello perspective of hello resource governor, or tooanalyze active and historic usage of hello workload groups when troubleshooting.</span></span>

```sql
WITH rg
AS
(   SELECT  
     pn.name                        AS node_name
    ,pn.[type]                        AS node_type
    ,pn.pdw_node_id                    AS node_id
    ,rp.name                        AS pool_name
    ,rp.max_memory_kb*1.0/1024                AS pool_max_mem_MB
    ,wg.name                        AS group_name
    ,wg.importance                    AS group_importance
    ,wg.request_max_memory_grant_percent        AS group_request_max_memory_grant_pcnt
    ,wg.max_dop                        AS group_max_dop
    ,wg.effective_max_dop                AS group_effective_max_dop
    ,wg.total_request_count                AS group_total_request_count
    ,wg.total_queued_request_count            AS group_total_queued_request_count
    ,wg.active_request_count                AS group_active_request_count
    ,wg.queued_request_count                AS group_queued_request_count
    FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
    JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    
            ON  wg.pdw_node_id  = rp.pdw_node_id
            AND wg.pool_id      = rp.pool_id
    JOIN    sys.dm_pdw_nodes pn
            ON    wg.pdw_node_id    = pn.pdw_node_id
    WHERE   wg.name like 'SloDWGroup%'
        AND     rp.name = 'SloDWPool'
)
SELECT    pool_name
,        pool_max_mem_MB
,        group_name
,        group_importance
,        (pool_max_mem_MB/100)*group_request_max_memory_grant_pcnt AS max_memory_grant_MB
,        node_name
,        node_type
,       group_total_request_count
,       group_total_queued_request_count
,       group_active_request_count
,       group_queued_request_count
FROM    rg
ORDER BY
    node_name
,    group_request_max_memory_grant_pcnt
,    group_importance
;
```

## <a name="queries-that-honor-concurrency-limits"></a><span data-ttu-id="580e0-874">동시성 한도를 적용하는 쿼리</span><span class="sxs-lookup"><span data-stu-id="580e0-874">Queries that honor concurrency limits</span></span>
<span data-ttu-id="580e0-875">대부분의 쿼리는 리소스 클래스에 의해 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-875">Most queries are governed by resource classes.</span></span> <span data-ttu-id="580e0-876">이러한 쿼리 hello 동시 쿼리와 동시성 슬롯 임계값 내에 맞아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-876">These queries must fit inside both hello concurrent query and concurrency slot thresholds.</span></span> <span data-ttu-id="580e0-877">사용자는 hello 동시성 슬롯 모델에서 tooexclude 쿼리를 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-877">A user cannot choose tooexclude a query from hello concurrency slot model.</span></span>

<span data-ttu-id="580e0-878">tooreiterate, hello 다음 문은 인식 리소스 클래스:</span><span class="sxs-lookup"><span data-stu-id="580e0-878">tooreiterate, hello following statements honor resource classes:</span></span>

* <span data-ttu-id="580e0-879">INSERT-SELECT</span><span class="sxs-lookup"><span data-stu-id="580e0-879">INSERT-SELECT</span></span>
* <span data-ttu-id="580e0-880">UPDATE</span><span class="sxs-lookup"><span data-stu-id="580e0-880">UPDATE</span></span>
* <span data-ttu-id="580e0-881">삭제</span><span class="sxs-lookup"><span data-stu-id="580e0-881">DELETE</span></span>
* <span data-ttu-id="580e0-882">SELECT(사용자 테이블을 쿼리하는 경우)</span><span class="sxs-lookup"><span data-stu-id="580e0-882">SELECT (when querying user tables)</span></span>
* <span data-ttu-id="580e0-883">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="580e0-883">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="580e0-884">ALTER INDEX REORGANIZE</span><span class="sxs-lookup"><span data-stu-id="580e0-884">ALTER INDEX REORGANIZE</span></span>
* <span data-ttu-id="580e0-885">ALTER TABLE REBUILD</span><span class="sxs-lookup"><span data-stu-id="580e0-885">ALTER TABLE REBUILD</span></span>
* <span data-ttu-id="580e0-886">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="580e0-886">CREATE INDEX</span></span>
* <span data-ttu-id="580e0-887">CREATE CLUSTERED COLUMNSTORE INDEX</span><span class="sxs-lookup"><span data-stu-id="580e0-887">CREATE CLUSTERED COLUMNSTORE INDEX</span></span>
* <span data-ttu-id="580e0-888">CREATE TABLE AS SELECT (CTAS)</span><span class="sxs-lookup"><span data-stu-id="580e0-888">CREATE TABLE AS SELECT (CTAS)</span></span>
* <span data-ttu-id="580e0-889">데이터 로드</span><span class="sxs-lookup"><span data-stu-id="580e0-889">Data loading</span></span>
* <span data-ttu-id="580e0-890">Hello 데이터 이동 서비스 (DMS)을 통해 수행 되는 데이터 이동 작업</span><span class="sxs-lookup"><span data-stu-id="580e0-890">Data movement operations conducted by hello Data Movement Service (DMS)</span></span>

## <a name="query-exceptions-tooconcurrency-limits"></a><span data-ttu-id="580e0-891">쿼리 예외 tooconcurrency 제한</span><span class="sxs-lookup"><span data-stu-id="580e0-891">Query exceptions tooconcurrency limits</span></span>
<span data-ttu-id="580e0-892">일부 쿼리 hello 리소스를 인식 하지 못합니다 클래스 toowhich hello 사용자에 게 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-892">Some queries do not honor hello resource class toowhich hello user is assigned.</span></span> <span data-ttu-id="580e0-893">특정 명령에 필요한 hello 메모리 리소스가 부족 한지, 종종 hello 명령은 메타 데이터 작업 이므로 때 이러한 예외 toohello 동시성 제한은 적용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-893">These exceptions toohello concurrency limits are made when hello memory resources needed for a particular command are low, often because hello command is a metadata operation.</span></span> <span data-ttu-id="580e0-894">hello 이들 예외의 ´ ֲ tooavoid 더 큰 메모리 할당에 대 한 쿼리를 활용 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-894">hello goal of these exceptions is tooavoid larger memory allocations for queries that will never need them.</span></span> <span data-ttu-id="580e0-895">이러한 경우 작은 리소스 클래스 (smallrc) hello 실제 리소스 클래스에 관계 없이 항상 사용 하는 hello 기본 toohello 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-895">In these cases, hello default small resource class (smallrc) is always used regardless of hello actual resource class assigned toohello user.</span></span> <span data-ttu-id="580e0-896">예를 들어, `CREATE LOGIN` 은 항상 smallrc에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-896">For example, `CREATE LOGIN` will always run in smallrc.</span></span> <span data-ttu-id="580e0-897">hello 필요한 리소스 toofulfill이이 작업 되므로 매우 낮은 hello 동시성 슬롯 모델에서 의미 tooinclude hello 쿼리를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-897">hello resources required toofulfill this operation are very low, so it does not make sense tooinclude hello query in hello concurrency slot model.</span></span>  <span data-ttu-id="580e0-898">이러한 쿼리는 또한 hello 32 사용자 동시성 제한으로 제한 되지, 이러한 쿼리 무제한 toohello 세션 제한 1, 024 세션을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-898">These queries are also not limited by hello 32 user concurrency limit, an unlimited number of these queries can run up toohello session limit of 1,024 sessions.</span></span>

<span data-ttu-id="580e0-899">다음 조건 hello 리소스 클래스를 인식 하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-899">hello following statements do not honor resource classes:</span></span>

* <span data-ttu-id="580e0-900">CREATE 또는 DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="580e0-900">CREATE or DROP TABLE</span></span>
* <span data-ttu-id="580e0-901">ALTER TABLE ... SWITCH, SPLIT 또는 MERGE PARTITION</span><span class="sxs-lookup"><span data-stu-id="580e0-901">ALTER TABLE ... SWITCH, SPLIT, or MERGE PARTITION</span></span>
* <span data-ttu-id="580e0-902">ALTER INDEX DISABLE</span><span class="sxs-lookup"><span data-stu-id="580e0-902">ALTER INDEX DISABLE</span></span>
* <span data-ttu-id="580e0-903">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="580e0-903">DROP INDEX</span></span>
* <span data-ttu-id="580e0-904">CREATE, UPDATE 또는 DROP STATISTICS</span><span class="sxs-lookup"><span data-stu-id="580e0-904">CREATE, UPDATE, or DROP STATISTICS</span></span>
* <span data-ttu-id="580e0-905">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="580e0-905">TRUNCATE TABLE</span></span>
* <span data-ttu-id="580e0-906">ALTER AUTHORIZATION</span><span class="sxs-lookup"><span data-stu-id="580e0-906">ALTER AUTHORIZATION</span></span>
* <span data-ttu-id="580e0-907">CREATE LOGIN</span><span class="sxs-lookup"><span data-stu-id="580e0-907">CREATE LOGIN</span></span>
* <span data-ttu-id="580e0-908">CREATE, ALTER 또는 DROP USER</span><span class="sxs-lookup"><span data-stu-id="580e0-908">CREATE, ALTER or DROP USER</span></span>
* <span data-ttu-id="580e0-909">CREATE, ALTER 또는 DROP PROCEDURE</span><span class="sxs-lookup"><span data-stu-id="580e0-909">CREATE, ALTER or DROP PROCEDURE</span></span>
* <span data-ttu-id="580e0-910">CREATE 또는 DROP VIEW</span><span class="sxs-lookup"><span data-stu-id="580e0-910">CREATE or DROP VIEW</span></span>
* <span data-ttu-id="580e0-911">INSERT VALUES</span><span class="sxs-lookup"><span data-stu-id="580e0-911">INSERT VALUES</span></span>
* <span data-ttu-id="580e0-912">SELECT(시스템 뷰와 DMV에서)</span><span class="sxs-lookup"><span data-stu-id="580e0-912">SELECT from system views and DMVs</span></span>
* <span data-ttu-id="580e0-913">EXPLAIN</span><span class="sxs-lookup"><span data-stu-id="580e0-913">EXPLAIN</span></span>
* <span data-ttu-id="580e0-914">DBCC</span><span class="sxs-lookup"><span data-stu-id="580e0-914">DBCC</span></span>

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <span data-ttu-id="580e0-915"><a name="changing-user-resource-class-example"></a> 사용자 리소스 클래스 변경 예제</span><span class="sxs-lookup"><span data-stu-id="580e0-915"><a name="changing-user-resource-class-example"></a> Change a user resource class example</span></span>
1. <span data-ttu-id="580e0-916">**로그인을 만듭니다:** 연결 tooyour 열고 **마스터** SQL 데이터 웨어하우스 데이터베이스를 호스팅하는 hello SQL server에서 데이터베이스 및 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-916">**Create login:** Open a connection tooyour **master** database on hello SQL server hosting your SQL Data Warehouse database and execute hello following commands.</span></span>
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > <span data-ttu-id="580e0-917">Azure SQL 데이터 웨어하우스 사용자에 대 한 hello master 데이터베이스 좋습니다 toocreate 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-917">It is a good idea toocreate a user in hello master database for Azure SQL Data Warehouse users.</span></span> <span data-ttu-id="580e0-918">Master에 사용자를 만들면 SSMS와 같은 도구를 사용 하 여 데이터베이스 이름을 지정 하지 않고 사용자 toologin이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-918">Creating a user in master allows a user toologin using tools like SSMS without specifying a database name.</span></span>  <span data-ttu-id="580e0-919">또한 있게 toouse hello 개체 탐색기 tooview에 모든 데이터베이스를 SQL server.</span><span class="sxs-lookup"><span data-stu-id="580e0-919">It also allows them toouse hello object explorer tooview all databases on a SQL server.</span></span>  <span data-ttu-id="580e0-920">사용자를 만들고 관리하는 방법에 대한 자세한 내용은 [SQL Data Warehouse에서 데이터베이스 보호][Secure a database in SQL Data Warehouse]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="580e0-920">For more details about creating and managing users, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>
   > 
   > 
2. <span data-ttu-id="580e0-921">**SQL 데이터 웨어하우스 사용자 만들기:** 연결 toohello 열고 **SQL 데이터 웨어하우스** 데이터베이스 및 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-921">**Create SQL Data Warehouse user:** Open a connection toohello **SQL Data Warehouse** database and execute hello following command.</span></span>
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. <span data-ttu-id="580e0-922">**권한 부여:** 예제 부여 다음 hello `CONTROL` hello에 **SQL 데이터 웨어하우스** 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-922">**Grant permissions:** hello following example grants `CONTROL` on hello **SQL Data Warehouse** database.</span></span> <span data-ttu-id="580e0-923">`CONTROL`hello에 데이터베이스 수준 db_owner SQL Server에서의 해당 하는 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-923">`CONTROL` at hello database level is hello equivalent of db_owner in SQL Server.</span></span>
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW toonewperson;
    ```
4. <span data-ttu-id="580e0-924">**리소스 클래스를 높일:** 사용 하 여 hello 다음 tooadd 사용자 tooa 높은 작업 관리 역할을 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-924">**Increase resource class:** Use hello following query tooadd a user tooa higher workload management role.</span></span>
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. <span data-ttu-id="580e0-925">**리소스 클래스를 줄이려면:** 사용 하 여 hello 다음 tooremove 작업 관리 역할에서 사용자를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-925">**Decrease resource class:** Use hello following query tooremove a user from a workload management role.</span></span>
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="580e0-926">가능한 tooremove smallrc에서 사용자는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-926">It is not possible tooremove a user from smallrc.</span></span>
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a><span data-ttu-id="580e0-927">큐에 대기 중인 쿼리 검색 및 다른 DMV</span><span class="sxs-lookup"><span data-stu-id="580e0-927">Queued query detection and other DMVs</span></span>
<span data-ttu-id="580e0-928">Hello를 사용할 수 있습니다 `sys.dm_pdw_exec_requests` 동시성 큐에서 대기 하는 DMV tooidentify 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-928">You can use hello `sys.dm_pdw_exec_requests` DMV tooidentify queries that are waiting in a concurrency queue.</span></span> <span data-ttu-id="580e0-929">동시성 슬롯을 대기하는 쿼리는 **일시 중단**상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-929">Queries waiting for a concurrency slot will have a status of **suspended**.</span></span>

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

<span data-ttu-id="580e0-930">워크로드 관리 역할은 `sys.database_principals`를 사용하여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-930">Workload management roles can be viewed with `sys.database_principals`.</span></span>

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

<span data-ttu-id="580e0-931">다음 쿼리에서 hello에 할당 된 각 사용자 역할을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-931">hello following query shows which role each user is assigned to.</span></span>

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

<span data-ttu-id="580e0-932">SQL 데이터 웨어하우스 hello 다음을 대기 유형을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-932">SQL Data Warehouse has hello following wait types:</span></span>

* <span data-ttu-id="580e0-933">**LocalQueriesConcurrencyResourceType**: hello 동시성 슬롯 프레임 워크 외부에서 앉아 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-933">**LocalQueriesConcurrencyResourceType**: Queries that sit outside of hello concurrency slot framework.</span></span> <span data-ttu-id="580e0-934">`SELECT @@VERSION` 과 같은 DMV 쿼리 및 시스템 함수는 로컬 쿼리의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-934">DMV queries and system functions such as `SELECT @@VERSION` are examples of local queries.</span></span>
* <span data-ttu-id="580e0-935">**UserConcurrencyResourceType**: hello 동시성 슬롯 프레임 워크 내을 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-935">**UserConcurrencyResourceType**: Queries that sit inside hello concurrency slot framework.</span></span> <span data-ttu-id="580e0-936">최종 사용자 테이블에 대한 쿼리는 이 리소스 형식을 사용하는 예를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-936">Queries against end-user tables represent examples that would use this resource type.</span></span>
* <span data-ttu-id="580e0-937">**DmsConcurrencyResourceType**: 데이터 이동 작업으로 초래된 대기</span><span class="sxs-lookup"><span data-stu-id="580e0-937">**DmsConcurrencyResourceType**: Waits resulting from data movement operations.</span></span>
* <span data-ttu-id="580e0-938">**BackupConcurrencyResourceType**: 이 대기는 데이터베이스가 백업 중임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-938">**BackupConcurrencyResourceType**: This wait indicates that a database is being backed up.</span></span> <span data-ttu-id="580e0-939">이 리소스 종류에 대 한 hello 최대 값은 1입니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-939">hello maximum value for this resource type is 1.</span></span> <span data-ttu-id="580e0-940">여러 백업 hello에 요청 하는 경우 동일한 시간, hello 다른을 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-940">If multiple backups have been requested at hello same time, hello others will queue.</span></span>

<span data-ttu-id="580e0-941">hello `sys.dm_pdw_waits` DMV는 리소스에 대 한 요청을 대기 하는 사용 되는 toosee 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-941">hello `sys.dm_pdw_waits` DMV can be used toosee which resources a request is waiting for.</span></span>

```sql
SELECT  w.[wait_id]
,       w.[session_id]
,       w.[type]            AS Wait_type
,       w.[object_type]
,       w.[object_name]
,       w.[request_id]
,       w.[request_time]
,       w.[acquire_time]
,       w.[state]
,       w.[priority]
,    SESSION_ID()            AS Current_session
,    s.[status]            AS Session_status
,    s.[login_name]
,    s.[query_count]
,    s.[client_id]
,    s.[sql_spid]
,    r.[command]            AS Request_command
,    r.[label]
,    r.[status]            AS Request_status
,    r.[submit_time]
,    r.[start_time]
,    r.[end_compile_time]
,    r.[end_time]
,    DATEDIFF(ms,r.[submit_time],r.[start_time])        AS Request_queue_time_ms
,    DATEDIFF(ms,r.[start_time],r.[end_compile_time])    AS Request_compile_time_ms
,    DATEDIFF(ms,r.[end_compile_time],r.[end_time])        AS Request_execution_time_ms
,    r.[total_elapsed_time]
FROM    sys.dm_pdw_waits w
JOIN    sys.dm_pdw_exec_sessions s  ON w.[session_id] = s.[session_id]
JOIN    sys.dm_pdw_exec_requests r  ON w.[request_id] = r.[request_id]
WHERE    w.[session_id] <> SESSION_ID();
```

<span data-ttu-id="580e0-942">hello `sys.dm_pdw_resource_waits` DMV에서 지정된 된 쿼리에 사용 hello 리소스 대기만 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-942">hello `sys.dm_pdw_resource_waits` DMV shows only hello resource waits consumed by a given query.</span></span> <span data-ttu-id="580e0-943">리소스 대기 시간 측정 제공 하는 리소스 toobe 때까지 대기 하는 hello 시간, SQL 서버 tooschedule hello 쿼리 hello CPU에 기본 hello에 대 한 걸리는 것과 반대로 toosignal 시간 hello 시간을 대기 하는 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-943">Resource wait time only measures hello time waiting for resources toobe provided, as opposed toosignal wait time, which is hello time it takes for hello underlying SQL servers tooschedule hello query onto hello CPU.</span></span>

```sql
SELECT  [session_id]
,       [type]
,       [object_type]
,       [object_name]
,       [request_id]
,       [request_time]
,       [acquire_time]
,       DATEDIFF(ms,[request_time],[acquire_time])  AS acquire_duration_ms
,       [concurrency_slots_used]                    AS concurrency_slots_reserved
,       [resource_class]
,       [wait_id]                                   AS queue_position
FROM    sys.dm_pdw_resource_waits
WHERE    [session_id] <> SESSION_ID();
```

<span data-ttu-id="580e0-944">hello `sys.dm_pdw_wait_stats` DMV 대기 작업의 기록 추세 분석에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-944">hello `sys.dm_pdw_wait_stats` DMV can be used for historic trend analysis of waits.</span></span>

```sql
SELECT    w.[pdw_node_id]
,        w.[wait_name]
,        w.[max_wait_time]
,        w.[request_count]
,        w.[signal_time]
,        w.[completed_count]
,        w.[wait_time]
FROM    sys.dm_pdw_wait_stats w;
```

## <a name="next-steps"></a><span data-ttu-id="580e0-945">다음 단계</span><span class="sxs-lookup"><span data-stu-id="580e0-945">Next steps</span></span>
<span data-ttu-id="580e0-946">데이터베이스 사용자 및 보안을 관리하는 방법에 대한 자세한 내용은 [SQL Data Warehouse에서 데이터베이스 보호][Secure a database in SQL Data Warehouse]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="580e0-946">For more information about managing database users and security, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span> <span data-ttu-id="580e0-947">큰 리소스 클래스에 대 한 자세한 내용은 클러스터형된 columnstore 인덱스 품질을 향상 시킬 수 있습니다, 참조 [tooimprove 세그먼트 품질 인덱스를 다시 작성]합니다.</span><span class="sxs-lookup"><span data-stu-id="580e0-947">For more information about how larger resource classes can improve clustered columnstore index quality, see [Rebuilding indexes tooimprove segment quality].</span></span>

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[tooimprove 세그먼트 품질 인덱스를 다시 작성]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->

---
title: "SQL Data Warehouse의 동시성 및 워크로드 관리 | Microsoft Docs"
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
ms.openlocfilehash: eaf2d43286dbaa52ada1430fbb7ce1e37f41c0d4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a><span data-ttu-id="9ff0a-103">SQL 데이터 웨어하우스의 동시성 및 워크로드 관리</span><span class="sxs-lookup"><span data-stu-id="9ff0a-103">Concurrency and workload management in SQL Data Warehouse</span></span>
<span data-ttu-id="9ff0a-104">예측 가능한 성능을 광범위하게 제공하려는 경우 Microsoft Azure SQL Data Warehouse를 사용하면 동시성 수준 및 리소스 할당(예: 메모리, CPU 우선 순위 지정)을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-104">To deliver predictable performance at scale, Microsoft Azure SQL Data Warehouse helps you control concurrency levels and resource allocations like memory and CPU prioritization.</span></span> <span data-ttu-id="9ff0a-105">이 문서에서는 동시성 및 워크로드 관리 개념을 소개하며, 두 기능 모두 구현된 방법 및 데이터 웨어하우스에서 이들을 제어할 수 있는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-105">This article introduces you to the concepts of concurrency and workload management, explaining how both features have been implemented and how you can control them in your data warehouse.</span></span> <span data-ttu-id="9ff0a-106">SQL 데이터 웨어하우스 워크로드 관리는 다중 사용자 환경을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-106">SQL Data Warehouse workload management is intended to help you support multi-user environments.</span></span> <span data-ttu-id="9ff0a-107">다중 테넌트 워크로드용은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-107">It is not intended for multi-tenant workloads.</span></span>

## <a name="concurrency-limits"></a><span data-ttu-id="9ff0a-108">동시성 한도</span><span class="sxs-lookup"><span data-stu-id="9ff0a-108">Concurrency limits</span></span>
<span data-ttu-id="9ff0a-109">SQL 데이터 웨어하우스를 사용하여 최대 1,024개의 동시 연결을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-109">SQL Data Warehouse allows up to 1,024 concurrent connections.</span></span> <span data-ttu-id="9ff0a-110">1,024개의 모든 연결을 통해 동시에 쿼리를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-110">All 1,024 connections can submit queries concurrently.</span></span> <span data-ttu-id="9ff0a-111">그러나 SQL Data Warehouse는 처리량을 최적화하기 위해 각 쿼리가 최소한의 메모리를 부여받도록 일부 쿼리를 대기시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-111">However, to optimize throughput, SQL Data Warehouse may queue some queries to ensure that each query receives a minimal memory grant.</span></span> <span data-ttu-id="9ff0a-112">쿼리 실행 시 큐에 대기하기가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-112">Queuing occurs at query execution time.</span></span> <span data-ttu-id="9ff0a-113">SQL 데이터 웨어하우스는 동시성 한도에 이른 경우 쿼리를 큐에 대기하도록 하여 활성 쿼리가 긴급하게 필요한 메모리 리소스에 액세스할 수 있게 하여 총 처리량을 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-113">By queuing queries when concurrency limits are reached, SQL Data Warehouse can increase total throughput by ensuring that active queries get access to critically needed memory resources.</span></span>  

<span data-ttu-id="9ff0a-114">동시성 한도는 *동시 쿼리 수* 및 *동시성 슬롯 수*라는 두 개념에 의해 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-114">Concurrency limits are governed by two concepts: *concurrent queries* and *concurrency slots*.</span></span> <span data-ttu-id="9ff0a-115">쿼리가 실행하려면 쿼리 동시성 한도 및 동시성 슬롯 할당 내에서 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-115">For a query to execute, it must execute within both the query concurrency limit and the concurrency slot allocation.</span></span>

* <span data-ttu-id="9ff0a-116">동시 쿼리 수란 동시에 실행하는 쿼리 수입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-116">Concurrent queries are the queries executing at the same time.</span></span> <span data-ttu-id="9ff0a-117">SQL 데이터 웨어하우스는 더 큰 DWU 크기에서 최대 32개의 동시 쿼리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-117">SQL Data Warehouse supports up to 32 concurrent queries on the larger DWU sizes.</span></span>
* <span data-ttu-id="9ff0a-118">동시성 슬롯은 DWU를 기준으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-118">Concurrency slots are allocated based on DWU.</span></span> <span data-ttu-id="9ff0a-119">100개의 DWU마다 4개의 동시성 슬롯을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-119">Each 100 DWU provides 4 concurrency slots.</span></span> <span data-ttu-id="9ff0a-120">예를 들어 DW100은 4개의 동시성 슬롯을 할당하고, DW1000은 40개를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-120">For example, a DW100 allocates 4 concurrency slots and DW1000 allocates 40.</span></span> <span data-ttu-id="9ff0a-121">각 쿼리는 쿼리의 [리소스 클래스](#resource-classes) 에 따라 하나 이상의 동시성 슬롯을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-121">Each query consumes one or more concurrency slots, dependent on the [resource class](#resource-classes) of the query.</span></span> <span data-ttu-id="9ff0a-122">smallrc 리소스 클래스에서 실행되는 쿼리는 하나의 동시성 슬롯을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-122">Queries running in the smallrc resource class consume one concurrency slot.</span></span> <span data-ttu-id="9ff0a-123">상위 리소스 클래스에서 실행되는 쿼리는 더 많은 동시성 슬롯을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-123">Queries running in a higher resource class consume more concurrency slots.</span></span>

<span data-ttu-id="9ff0a-124">다음 테이블에는 다양한 DWU 크기의 동시 쿼리와 동시성 슬롯의 한도가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-124">The following table describes the limits for both concurrent queries and concurrency slots at the various DWU sizes.</span></span>

### <a name="concurrency-limits"></a><span data-ttu-id="9ff0a-125">동시성 한도</span><span class="sxs-lookup"><span data-stu-id="9ff0a-125">Concurrency limits</span></span>
| <span data-ttu-id="9ff0a-126">DWU</span><span class="sxs-lookup"><span data-stu-id="9ff0a-126">DWU</span></span> | <span data-ttu-id="9ff0a-127">최대 동시 쿼리 수</span><span class="sxs-lookup"><span data-stu-id="9ff0a-127">Max concurrent queries</span></span> | <span data-ttu-id="9ff0a-128">할당된 동시성 슬롯 수</span><span class="sxs-lookup"><span data-stu-id="9ff0a-128">Concurrency slots allocated</span></span> |
|:--- |:---:|:---:|
| <span data-ttu-id="9ff0a-129">DW100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-129">DW100</span></span> |<span data-ttu-id="9ff0a-130">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-130">4</span></span> |<span data-ttu-id="9ff0a-131">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-131">4</span></span> |
| <span data-ttu-id="9ff0a-132">DW200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-132">DW200</span></span> |<span data-ttu-id="9ff0a-133">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-133">8</span></span> |<span data-ttu-id="9ff0a-134">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-134">8</span></span> |
| <span data-ttu-id="9ff0a-135">DW300</span><span class="sxs-lookup"><span data-stu-id="9ff0a-135">DW300</span></span> |<span data-ttu-id="9ff0a-136">12</span><span class="sxs-lookup"><span data-stu-id="9ff0a-136">12</span></span> |<span data-ttu-id="9ff0a-137">12</span><span class="sxs-lookup"><span data-stu-id="9ff0a-137">12</span></span> |
| <span data-ttu-id="9ff0a-138">DW400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-138">DW400</span></span> |<span data-ttu-id="9ff0a-139">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-139">16</span></span> |<span data-ttu-id="9ff0a-140">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-140">16</span></span> |
| <span data-ttu-id="9ff0a-141">DW500</span><span class="sxs-lookup"><span data-stu-id="9ff0a-141">DW500</span></span> |<span data-ttu-id="9ff0a-142">20</span><span class="sxs-lookup"><span data-stu-id="9ff0a-142">20</span></span> |<span data-ttu-id="9ff0a-143">20</span><span class="sxs-lookup"><span data-stu-id="9ff0a-143">20</span></span> |
| <span data-ttu-id="9ff0a-144">DW600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-144">DW600</span></span> |<span data-ttu-id="9ff0a-145">24</span><span class="sxs-lookup"><span data-stu-id="9ff0a-145">24</span></span> |<span data-ttu-id="9ff0a-146">24</span><span class="sxs-lookup"><span data-stu-id="9ff0a-146">24</span></span> |
| <span data-ttu-id="9ff0a-147">DW1000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-147">DW1000</span></span> |<span data-ttu-id="9ff0a-148">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-148">32</span></span> |<span data-ttu-id="9ff0a-149">40</span><span class="sxs-lookup"><span data-stu-id="9ff0a-149">40</span></span> |
| <span data-ttu-id="9ff0a-150">DW1200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-150">DW1200</span></span> |<span data-ttu-id="9ff0a-151">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-151">32</span></span> |<span data-ttu-id="9ff0a-152">48</span><span class="sxs-lookup"><span data-stu-id="9ff0a-152">48</span></span> |
| <span data-ttu-id="9ff0a-153">DW1500</span><span class="sxs-lookup"><span data-stu-id="9ff0a-153">DW1500</span></span> |<span data-ttu-id="9ff0a-154">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-154">32</span></span> |<span data-ttu-id="9ff0a-155">60</span><span class="sxs-lookup"><span data-stu-id="9ff0a-155">60</span></span> |
| <span data-ttu-id="9ff0a-156">DW2000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-156">DW2000</span></span> |<span data-ttu-id="9ff0a-157">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-157">32</span></span> |<span data-ttu-id="9ff0a-158">80</span><span class="sxs-lookup"><span data-stu-id="9ff0a-158">80</span></span> |
| <span data-ttu-id="9ff0a-159">DW3000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-159">DW3000</span></span> |<span data-ttu-id="9ff0a-160">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-160">32</span></span> |<span data-ttu-id="9ff0a-161">120</span><span class="sxs-lookup"><span data-stu-id="9ff0a-161">120</span></span> |
| <span data-ttu-id="9ff0a-162">DW6000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-162">DW6000</span></span> |<span data-ttu-id="9ff0a-163">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-163">32</span></span> |<span data-ttu-id="9ff0a-164">240</span><span class="sxs-lookup"><span data-stu-id="9ff0a-164">240</span></span> |

<span data-ttu-id="9ff0a-165">이러한 임계값 중 하나가 충족되면 새 쿼리가 큐에 추가되고 선입선출 방식으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-165">When one of these thresholds is met, new queries are queued and executed on a first-in, first-out basis.</span></span>  <span data-ttu-id="9ff0a-166">쿼리가 완료되고 쿼리 및 슬롯의 수가 한도 밑으로 떨어지면 큐에 저장된 쿼리가 릴리스됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-166">As a queries finishes and the number of queries and slots falls below the limits, queued queries are released.</span></span> 

> [!NOTE]  
> <span data-ttu-id="9ff0a-167">*Select* 쿼리 또는 카탈로그 뷰는 어떠한 동시성 한도에 의해서도 제어되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-167">*Select* queries executing exclusively on dynamic management views (DMVs) or catalog views are not governed by any of the concurrency limits.</span></span> <span data-ttu-id="9ff0a-168">시스템에서 실행하는 쿼리 수에 관계없이 시스템을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-168">You can monitor the system regardless of the number of queries executing on it.</span></span>
> 
> 

## <a name="resource-classes"></a><span data-ttu-id="9ff0a-169">리소스 클래스</span><span class="sxs-lookup"><span data-stu-id="9ff0a-169">Resource classes</span></span>
<span data-ttu-id="9ff0a-170">리소스 클래스는 쿼리에 지정된 메모리 할당 및 CPU 사이클을 제어하는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-170">Resource classes help you control memory allocation and CPU cycles given to a query.</span></span> <span data-ttu-id="9ff0a-171">2가지 유형의 리소스 클래스를 데이터베이스 역할 형태로 사용자에게 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-171">You can assign two types of resource classes to a user in the form of database roles.</span></span> <span data-ttu-id="9ff0a-172">2가지 유형의 리소스 클래스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-172">The two types of resource classes are as follows:</span></span>
1. <span data-ttu-id="9ff0a-173">동적 리소스 클래스(**smallrc, mediumrc, largerc, xlargerc**)는 현재 DWU에 따라 가변 크기의 메모리를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-173">Dynamic Resource Classes (**smallrc, mediumrc, largerc, xlargerc**) allocate a variable amount of memory depending on the current DWU.</span></span> <span data-ttu-id="9ff0a-174">즉, 더 큰 DWU로 확장할 경우 쿼리도 자동으로 더 많은 메모리를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-174">This means that when you scale up to a larger DWU, your queries automatically get more memory.</span></span> 
2. <span data-ttu-id="9ff0a-175">정적 리소스 클래스(**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**)는 현재 DWU에 관계 없이 동일한 양의 메모리를 할당합니다(DWU 자체에 충분한 메모리가 있다고 가정할 경우).</span><span class="sxs-lookup"><span data-stu-id="9ff0a-175">Static Resource Classes (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) allocate the same amount of memory regardless of the current DWU (provided that the DWU itself has enough memory).</span></span> <span data-ttu-id="9ff0a-176">즉, 더 큰 DWU에서는 각 리소스 클래스에서 동시에 더 많은 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-176">This means that on larger DWUs, you can run more queries in each resource class concurrently.</span></span>

<span data-ttu-id="9ff0a-177">**smallrc** 및 **staticrc10**의 사용자에게 더 적은 양의 메모리가 주어져 더 높은 동시성을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-177">Users in **smallrc** and **staticrc10** are given a smaller amount of memory and can take advantage of higher concurrency.</span></span> <span data-ttu-id="9ff0a-178">반면, **xlargerc** 또는 **staticrc80**에 할당된 사용자는 많은 양의 메모리가 주어져 더 적은 쿼리가 동시에 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-178">In contrast, users assigned to **xlargerc** or **staticrc80** are given large amounts of memory, and therefore fewer of their queries can run concurrently.</span></span>

<span data-ttu-id="9ff0a-179">기본적으로 각 사용자는 작은 리소스 클래스인 **smallrc**의 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-179">By default, each user is a member of the small resource class, **smallrc**.</span></span> <span data-ttu-id="9ff0a-180">`sp_addrolemember` 절차는 리소스 클래스를 늘리는 데 사용되고 `sp_droprolemember` 절차는 리소스 클래스를 줄이는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-180">The procedure `sp_addrolemember` is used to increase the resource class, and `sp_droprolemember` is used to decrease the resource class.</span></span> <span data-ttu-id="9ff0a-181">예를 들어 이 명령은 loaduser의 리소스 클래스를 **largerc**로 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-181">For example, this command would increase the resource class of loaduser to **largerc**:</span></span>

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a><span data-ttu-id="9ff0a-182">리소스 클래스를 인식하지 않는 쿼리</span><span class="sxs-lookup"><span data-stu-id="9ff0a-182">Queries that do not honor resource classes</span></span>

<span data-ttu-id="9ff0a-183">더 큰 메모리를 할당해도 별로 도움이 되지 않는 일부 쿼리 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-183">There are a few types of queries that do not benefit from a larger memory allocation.</span></span> <span data-ttu-id="9ff0a-184">시스템은 리소스 클래스 할당을 무시하고, 대신 이러한 쿼리를 항상 작은 리소스 클래스에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-184">The system ignores their resource class allocation and always run these queries in the small resource class instead.</span></span> <span data-ttu-id="9ff0a-185">이러한 쿼리가 항상 작은 리소스 클래스에서 실행되는 경우 동시성 슬롯이 압박 하에서 실행될 수 있으며 필요한 것보다 더 많은 수의 슬롯을 사용하지 않게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-185">If these queries always run in the small resource class, they can run when concurrency slots are under pressure and they won't consume more slots than needed.</span></span> <span data-ttu-id="9ff0a-186">자세한 내용은 [리소스 클래스 예외](#query-exceptions-to-concurrency-limits) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-186">See [Resource class exceptions](#query-exceptions-to-concurrency-limits) for more information.</span></span>

## <a name="details-on-resource-class-assignment"></a><span data-ttu-id="9ff0a-187">리소스 클래스 할당에 대한 세부 정보</span><span class="sxs-lookup"><span data-stu-id="9ff0a-187">Details on resource class assignment</span></span>


<span data-ttu-id="9ff0a-188">리소스 클래스에 대한 추가적인 몇 가지 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-188">A few more details on resource class:</span></span>

* <span data-ttu-id="9ff0a-189">*역할 변경* 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-189">*Alter role* permission is required to change the resource class of a user.</span></span>
* <span data-ttu-id="9ff0a-190">하나 이상의 더 높은 리소스 클래스에 사용자를 추가할 수 있지만 동적 리소스 클래스는 정적 리소스 클래스보다 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-190">Although you can add a user to one or more of the higher resource classes, dynamic resource classes take precedence over static resource classes.</span></span> <span data-ttu-id="9ff0a-191">즉, 사용자가 **mediumrc**(동적) 및 **staticrc80**(정적) 둘 다에 할당되는 경우 **mediumrc**가 적용되는 리소스 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-191">That is, if a user is assigned to both **mediumrc**(dynamic) and **staticrc80**(static), **mediumrc** is the resource class that is honored.</span></span>
 * <span data-ttu-id="9ff0a-192">사용자가 특정 리소스 클래스 형식의 둘 이상의 리소스 클래스(여러 개의 동적 리소스 클래스 또는 여러 개의 정적 리소스 클래스)에 할당되는 경우 가장 높은 리소스 클래스가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-192">When a user is assigned to more than one resource class in a specific resource class type (more than one dynamic resource class or more than one static resource class), the highest resource class is honored.</span></span> <span data-ttu-id="9ff0a-193">즉, 사용자가 mediumrc와 largerc 둘 다에 할당되면 더 높은 리소스 클래스인 largerc가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-193">That is, if a user is assigned to both mediumrc and largerc, the higher resource class (largerc) is honored.</span></span> <span data-ttu-id="9ff0a-194">사용자가 **staticrc20** 및 **statirc80** 둘 다에 할당되면 **staticrc80**이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-194">And if a user is assigned to both **staticrc20** and **statirc80**, **staticrc80** is honored.</span></span>
* <span data-ttu-id="9ff0a-195">시스템 관리 사용자의 리소스 클래스는 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-195">The resource class of the system administrative user cannot be changed.</span></span>

<span data-ttu-id="9ff0a-196">자세한 예제는 [사용자 리소스 클래스 변경 예제](#changing-user-resource-class-example)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-196">For a detailed example, see [Changing user resource class example](#changing-user-resource-class-example).</span></span>

## <a name="memory-allocation"></a><span data-ttu-id="9ff0a-197">메모리 할당</span><span class="sxs-lookup"><span data-stu-id="9ff0a-197">Memory allocation</span></span>
<span data-ttu-id="9ff0a-198">사용자의 리소스 클래스를 늘리는 데 따른 장단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-198">There are pros and cons to increasing a user's resource class.</span></span> <span data-ttu-id="9ff0a-199">사용자에 대한 리소스 클래스를 늘리면 쿼리가 더 많은 메모리에 액세스할 수 있게 되고 이렇게 되면 쿼리가 더 빨리 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-199">Increasing a resource class for a user, gives their queries access to more memory, which may mean queries execute faster.</span></span>  <span data-ttu-id="9ff0a-200">하지만 리소스 클래스가 높아질수록 동시에 실행될 수 있는 쿼리의 수도 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-200">However, higher resource classes also reduce the number of concurrent queries that can run.</span></span> <span data-ttu-id="9ff0a-201">즉, 단일 쿼리에 많은 양의 메모리를 할당하거나 동시 실행을 위해 역시 메모리 할당이 필요한 다른 쿼리를 허용하는 방식 중에서 하나를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-201">This is the trade-off between allocating large amounts of memory to a single query or allowing other queries, which also need memory allocations, to run concurrently.</span></span> <span data-ttu-id="9ff0a-202">한 명의 사용자가 쿼리에 대한 메모리 할당을 높게 받는 경우 다른 사용자들은 쿼리를 실행할 목적으로 동일한 메모리에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-202">If one user is given high allocations of memory for a query, other users will not have access to that same memory to run a query.</span></span>

<span data-ttu-id="9ff0a-203">다음 표는 DWU 및 리소스 클래스에 의해 각 배포에 할당된 메모리를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-203">The following table maps the memory allocated to each distribution by DWU and resource class.</span></span>

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a><span data-ttu-id="9ff0a-204">동적 리소스 클래스에 대한 배포별 메모리 할당(MB)</span><span class="sxs-lookup"><span data-stu-id="9ff0a-204">Memory allocations per distribution for dynamic resource classes (MB)</span></span>
| <span data-ttu-id="9ff0a-205">DWU</span><span class="sxs-lookup"><span data-stu-id="9ff0a-205">DWU</span></span> | <span data-ttu-id="9ff0a-206">smallrc</span><span class="sxs-lookup"><span data-stu-id="9ff0a-206">smallrc</span></span> | <span data-ttu-id="9ff0a-207">mediumrc</span><span class="sxs-lookup"><span data-stu-id="9ff0a-207">mediumrc</span></span> | <span data-ttu-id="9ff0a-208">largerc</span><span class="sxs-lookup"><span data-stu-id="9ff0a-208">largerc</span></span> | <span data-ttu-id="9ff0a-209">xlargerc</span><span class="sxs-lookup"><span data-stu-id="9ff0a-209">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="9ff0a-210">DW100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-210">DW100</span></span> |<span data-ttu-id="9ff0a-211">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-211">100</span></span> |<span data-ttu-id="9ff0a-212">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-212">100</span></span> |<span data-ttu-id="9ff0a-213">200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-213">200</span></span> |<span data-ttu-id="9ff0a-214">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-214">400</span></span> |
| <span data-ttu-id="9ff0a-215">DW200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-215">DW200</span></span> |<span data-ttu-id="9ff0a-216">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-216">100</span></span> |<span data-ttu-id="9ff0a-217">200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-217">200</span></span> |<span data-ttu-id="9ff0a-218">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-218">400</span></span> |<span data-ttu-id="9ff0a-219">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-219">800</span></span> |
| <span data-ttu-id="9ff0a-220">DW300</span><span class="sxs-lookup"><span data-stu-id="9ff0a-220">DW300</span></span> |<span data-ttu-id="9ff0a-221">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-221">100</span></span> |<span data-ttu-id="9ff0a-222">200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-222">200</span></span> |<span data-ttu-id="9ff0a-223">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-223">400</span></span> |<span data-ttu-id="9ff0a-224">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-224">800</span></span> |
| <span data-ttu-id="9ff0a-225">DW400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-225">DW400</span></span> |<span data-ttu-id="9ff0a-226">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-226">100</span></span> |<span data-ttu-id="9ff0a-227">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-227">400</span></span> |<span data-ttu-id="9ff0a-228">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-228">800</span></span> |<span data-ttu-id="9ff0a-229">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-229">1,600</span></span> |
| <span data-ttu-id="9ff0a-230">DW500</span><span class="sxs-lookup"><span data-stu-id="9ff0a-230">DW500</span></span> |<span data-ttu-id="9ff0a-231">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-231">100</span></span> |<span data-ttu-id="9ff0a-232">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-232">400</span></span> |<span data-ttu-id="9ff0a-233">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-233">800</span></span> |<span data-ttu-id="9ff0a-234">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-234">1,600</span></span> |
| <span data-ttu-id="9ff0a-235">DW600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-235">DW600</span></span> |<span data-ttu-id="9ff0a-236">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-236">100</span></span> |<span data-ttu-id="9ff0a-237">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-237">400</span></span> |<span data-ttu-id="9ff0a-238">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-238">800</span></span> |<span data-ttu-id="9ff0a-239">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-239">1,600</span></span> |
| <span data-ttu-id="9ff0a-240">DW1000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-240">DW1000</span></span> |<span data-ttu-id="9ff0a-241">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-241">100</span></span> |<span data-ttu-id="9ff0a-242">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-242">800</span></span> |<span data-ttu-id="9ff0a-243">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-243">1,600</span></span> |<span data-ttu-id="9ff0a-244">3,200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-244">3,200</span></span> |
| <span data-ttu-id="9ff0a-245">DW1200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-245">DW1200</span></span> |<span data-ttu-id="9ff0a-246">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-246">100</span></span> |<span data-ttu-id="9ff0a-247">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-247">800</span></span> |<span data-ttu-id="9ff0a-248">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-248">1,600</span></span> |<span data-ttu-id="9ff0a-249">3,200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-249">3,200</span></span> |
| <span data-ttu-id="9ff0a-250">DW1500</span><span class="sxs-lookup"><span data-stu-id="9ff0a-250">DW1500</span></span> |<span data-ttu-id="9ff0a-251">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-251">100</span></span> |<span data-ttu-id="9ff0a-252">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-252">800</span></span> |<span data-ttu-id="9ff0a-253">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-253">1,600</span></span> |<span data-ttu-id="9ff0a-254">3,200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-254">3,200</span></span> |
| <span data-ttu-id="9ff0a-255">DW2000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-255">DW2000</span></span> |<span data-ttu-id="9ff0a-256">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-256">100</span></span> |<span data-ttu-id="9ff0a-257">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-257">1,600</span></span> |<span data-ttu-id="9ff0a-258">3,200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-258">3,200</span></span> |<span data-ttu-id="9ff0a-259">6,400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-259">6,400</span></span> |
| <span data-ttu-id="9ff0a-260">DW3000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-260">DW3000</span></span> |<span data-ttu-id="9ff0a-261">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-261">100</span></span> |<span data-ttu-id="9ff0a-262">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-262">1,600</span></span> |<span data-ttu-id="9ff0a-263">3,200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-263">3,200</span></span> |<span data-ttu-id="9ff0a-264">6,400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-264">6,400</span></span> |
| <span data-ttu-id="9ff0a-265">DW6000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-265">DW6000</span></span> |<span data-ttu-id="9ff0a-266">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-266">100</span></span> |<span data-ttu-id="9ff0a-267">3,200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-267">3,200</span></span> |<span data-ttu-id="9ff0a-268">6,400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-268">6,400</span></span> |<span data-ttu-id="9ff0a-269">12,800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-269">12,800</span></span> |

<span data-ttu-id="9ff0a-270">다음 표는 DWU 및 정적 리소스 클래스에 의해 각 배포에 할당된 메모리를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-270">The following table maps the memory allocated to each distribution by DWU and static resource class.</span></span> <span data-ttu-id="9ff0a-271">전역 DWU 제한을 준수하기 위해 더 높은 리소스 클래스의 메모리가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-271">Note that the higher resource classes have their memory reduced to honor the global DWU limits.</span></span>

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a><span data-ttu-id="9ff0a-272">정적 리소스 클래스에 대한 배포별 메모리 할당(MB)</span><span class="sxs-lookup"><span data-stu-id="9ff0a-272">Memory allocations per distribution for static resource classes (MB)</span></span>
| <span data-ttu-id="9ff0a-273">DWU</span><span class="sxs-lookup"><span data-stu-id="9ff0a-273">DWU</span></span> | <span data-ttu-id="9ff0a-274">staticrc10</span><span class="sxs-lookup"><span data-stu-id="9ff0a-274">staticrc10</span></span> | <span data-ttu-id="9ff0a-275">staticrc20</span><span class="sxs-lookup"><span data-stu-id="9ff0a-275">staticrc20</span></span> | <span data-ttu-id="9ff0a-276">staticrc30</span><span class="sxs-lookup"><span data-stu-id="9ff0a-276">staticrc30</span></span> | <span data-ttu-id="9ff0a-277">staticrc40</span><span class="sxs-lookup"><span data-stu-id="9ff0a-277">staticrc40</span></span> | <span data-ttu-id="9ff0a-278">staticrc50</span><span class="sxs-lookup"><span data-stu-id="9ff0a-278">staticrc50</span></span> | <span data-ttu-id="9ff0a-279">staticrc60</span><span class="sxs-lookup"><span data-stu-id="9ff0a-279">staticrc60</span></span> | <span data-ttu-id="9ff0a-280">staticrc70</span><span class="sxs-lookup"><span data-stu-id="9ff0a-280">staticrc70</span></span> | <span data-ttu-id="9ff0a-281">staticrc80</span><span class="sxs-lookup"><span data-stu-id="9ff0a-281">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="9ff0a-282">DW100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-282">DW100</span></span> |<span data-ttu-id="9ff0a-283">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-283">100</span></span> |<span data-ttu-id="9ff0a-284">200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-284">200</span></span> |<span data-ttu-id="9ff0a-285">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-285">400</span></span> |<span data-ttu-id="9ff0a-286">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-286">400</span></span> |<span data-ttu-id="9ff0a-287">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-287">400</span></span> |<span data-ttu-id="9ff0a-288">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-288">400</span></span> |<span data-ttu-id="9ff0a-289">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-289">400</span></span> |<span data-ttu-id="9ff0a-290">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-290">400</span></span> |
| <span data-ttu-id="9ff0a-291">DW200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-291">DW200</span></span> |<span data-ttu-id="9ff0a-292">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-292">100</span></span> |<span data-ttu-id="9ff0a-293">200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-293">200</span></span> |<span data-ttu-id="9ff0a-294">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-294">400</span></span> |<span data-ttu-id="9ff0a-295">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-295">800</span></span> |<span data-ttu-id="9ff0a-296">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-296">800</span></span> |<span data-ttu-id="9ff0a-297">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-297">800</span></span> |<span data-ttu-id="9ff0a-298">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-298">800</span></span> |<span data-ttu-id="9ff0a-299">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-299">800</span></span> |
| <span data-ttu-id="9ff0a-300">DW300</span><span class="sxs-lookup"><span data-stu-id="9ff0a-300">DW300</span></span> |<span data-ttu-id="9ff0a-301">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-301">100</span></span> |<span data-ttu-id="9ff0a-302">200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-302">200</span></span> |<span data-ttu-id="9ff0a-303">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-303">400</span></span> |<span data-ttu-id="9ff0a-304">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-304">800</span></span> |<span data-ttu-id="9ff0a-305">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-305">800</span></span> |<span data-ttu-id="9ff0a-306">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-306">800</span></span> |<span data-ttu-id="9ff0a-307">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-307">800</span></span> |<span data-ttu-id="9ff0a-308">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-308">800</span></span> |
| <span data-ttu-id="9ff0a-309">DW400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-309">DW400</span></span> |<span data-ttu-id="9ff0a-310">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-310">100</span></span> |<span data-ttu-id="9ff0a-311">200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-311">200</span></span> |<span data-ttu-id="9ff0a-312">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-312">400</span></span> |<span data-ttu-id="9ff0a-313">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-313">800</span></span> |<span data-ttu-id="9ff0a-314">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-314">1,600</span></span> |<span data-ttu-id="9ff0a-315">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-315">1,600</span></span> |<span data-ttu-id="9ff0a-316">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-316">1,600</span></span> |<span data-ttu-id="9ff0a-317">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-317">1,600</span></span> |
| <span data-ttu-id="9ff0a-318">DW500</span><span class="sxs-lookup"><span data-stu-id="9ff0a-318">DW500</span></span> |<span data-ttu-id="9ff0a-319">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-319">100</span></span> |<span data-ttu-id="9ff0a-320">200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-320">200</span></span> |<span data-ttu-id="9ff0a-321">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-321">400</span></span> |<span data-ttu-id="9ff0a-322">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-322">800</span></span> |<span data-ttu-id="9ff0a-323">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-323">1,600</span></span> |<span data-ttu-id="9ff0a-324">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-324">1,600</span></span> |<span data-ttu-id="9ff0a-325">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-325">1,600</span></span> |<span data-ttu-id="9ff0a-326">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-326">1,600</span></span> |
| <span data-ttu-id="9ff0a-327">DW600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-327">DW600</span></span> |<span data-ttu-id="9ff0a-328">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-328">100</span></span> |<span data-ttu-id="9ff0a-329">200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-329">200</span></span> |<span data-ttu-id="9ff0a-330">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-330">400</span></span> |<span data-ttu-id="9ff0a-331">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-331">800</span></span> |<span data-ttu-id="9ff0a-332">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-332">1,600</span></span> |<span data-ttu-id="9ff0a-333">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-333">1,600</span></span> |<span data-ttu-id="9ff0a-334">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-334">1,600</span></span> |<span data-ttu-id="9ff0a-335">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-335">1,600</span></span> |
| <span data-ttu-id="9ff0a-336">DW1000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-336">DW1000</span></span> |<span data-ttu-id="9ff0a-337">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-337">100</span></span> |<span data-ttu-id="9ff0a-338">200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-338">200</span></span> |<span data-ttu-id="9ff0a-339">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-339">400</span></span> |<span data-ttu-id="9ff0a-340">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-340">800</span></span> |<span data-ttu-id="9ff0a-341">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-341">1,600</span></span> |<span data-ttu-id="9ff0a-342">3,200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-342">3,200</span></span> |<span data-ttu-id="9ff0a-343">3,200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-343">3,200</span></span> |<span data-ttu-id="9ff0a-344">3,200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-344">3,200</span></span> |
| <span data-ttu-id="9ff0a-345">DW1200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-345">DW1200</span></span> |<span data-ttu-id="9ff0a-346">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-346">100</span></span> |<span data-ttu-id="9ff0a-347">200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-347">200</span></span> |<span data-ttu-id="9ff0a-348">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-348">400</span></span> |<span data-ttu-id="9ff0a-349">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-349">800</span></span> |<span data-ttu-id="9ff0a-350">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-350">1,600</span></span> |<span data-ttu-id="9ff0a-351">3,200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-351">3,200</span></span> |<span data-ttu-id="9ff0a-352">3,200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-352">3,200</span></span> |<span data-ttu-id="9ff0a-353">3,200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-353">3,200</span></span> |
| <span data-ttu-id="9ff0a-354">DW1500</span><span class="sxs-lookup"><span data-stu-id="9ff0a-354">DW1500</span></span> |<span data-ttu-id="9ff0a-355">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-355">100</span></span> |<span data-ttu-id="9ff0a-356">200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-356">200</span></span> |<span data-ttu-id="9ff0a-357">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-357">400</span></span> |<span data-ttu-id="9ff0a-358">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-358">800</span></span> |<span data-ttu-id="9ff0a-359">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-359">1,600</span></span> |<span data-ttu-id="9ff0a-360">3,200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-360">3,200</span></span> |<span data-ttu-id="9ff0a-361">3,200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-361">3,200</span></span> |<span data-ttu-id="9ff0a-362">3,200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-362">3,200</span></span> |
| <span data-ttu-id="9ff0a-363">DW2000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-363">DW2000</span></span> |<span data-ttu-id="9ff0a-364">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-364">100</span></span> |<span data-ttu-id="9ff0a-365">200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-365">200</span></span> |<span data-ttu-id="9ff0a-366">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-366">400</span></span> |<span data-ttu-id="9ff0a-367">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-367">800</span></span> |<span data-ttu-id="9ff0a-368">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-368">1,600</span></span> |<span data-ttu-id="9ff0a-369">3,200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-369">3,200</span></span> |<span data-ttu-id="9ff0a-370">6,400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-370">6,400</span></span> |<span data-ttu-id="9ff0a-371">6,400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-371">6,400</span></span> |
| <span data-ttu-id="9ff0a-372">DW3000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-372">DW3000</span></span> |<span data-ttu-id="9ff0a-373">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-373">100</span></span> |<span data-ttu-id="9ff0a-374">200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-374">200</span></span> |<span data-ttu-id="9ff0a-375">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-375">400</span></span> |<span data-ttu-id="9ff0a-376">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-376">800</span></span> |<span data-ttu-id="9ff0a-377">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-377">1,600</span></span> |<span data-ttu-id="9ff0a-378">3,200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-378">3,200</span></span> |<span data-ttu-id="9ff0a-379">6,400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-379">6,400</span></span> |<span data-ttu-id="9ff0a-380">6,400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-380">6,400</span></span> |
| <span data-ttu-id="9ff0a-381">DW6000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-381">DW6000</span></span> |<span data-ttu-id="9ff0a-382">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-382">100</span></span> |<span data-ttu-id="9ff0a-383">200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-383">200</span></span> |<span data-ttu-id="9ff0a-384">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-384">400</span></span> |<span data-ttu-id="9ff0a-385">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-385">800</span></span> |<span data-ttu-id="9ff0a-386">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-386">1,600</span></span> |<span data-ttu-id="9ff0a-387">3,200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-387">3,200</span></span> |<span data-ttu-id="9ff0a-388">6,400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-388">6,400</span></span> |<span data-ttu-id="9ff0a-389">12,800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-389">12,800</span></span> |

<span data-ttu-id="9ff0a-390">이전 테이블에서, **xlargerc** 리소스 클래스의 DW2000에서 실행되는 쿼리는 배포된 60개의 각 데이터베이스 내에서 6,400MB의 메모리에 액세스하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-390">From the preceding table, you can see that a query running on a DW2000 in the **xlargerc** resource class would have access to 6,400 MB of memory within each of the 60 distributed databases.</span></span>  <span data-ttu-id="9ff0a-391">SQL 데이터 웨어하우스에는 배포가 60개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-391">In SQL Data Warehouse, there are 60 distributions.</span></span> <span data-ttu-id="9ff0a-392">따라서, 주어진 리소스 클래스 내의 쿼리에 대한 총 메모리 할당을 계산하려면, 위의 값에 60을 곱해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-392">Therefore, to calculate the total memory allocation for a query in a given resource class, the above values should be multiplied by 60.</span></span>

### <a name="memory-allocations-system-wide-gb"></a><span data-ttu-id="9ff0a-393">시스템 전체 메모리 할당(GB)</span><span class="sxs-lookup"><span data-stu-id="9ff0a-393">Memory allocations system-wide (GB)</span></span>
| <span data-ttu-id="9ff0a-394">DWU</span><span class="sxs-lookup"><span data-stu-id="9ff0a-394">DWU</span></span> | <span data-ttu-id="9ff0a-395">smallrc</span><span class="sxs-lookup"><span data-stu-id="9ff0a-395">smallrc</span></span> | <span data-ttu-id="9ff0a-396">mediumrc</span><span class="sxs-lookup"><span data-stu-id="9ff0a-396">mediumrc</span></span> | <span data-ttu-id="9ff0a-397">largerc</span><span class="sxs-lookup"><span data-stu-id="9ff0a-397">largerc</span></span> | <span data-ttu-id="9ff0a-398">xlargerc</span><span class="sxs-lookup"><span data-stu-id="9ff0a-398">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="9ff0a-399">DW100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-399">DW100</span></span> |<span data-ttu-id="9ff0a-400">6</span><span class="sxs-lookup"><span data-stu-id="9ff0a-400">6</span></span> |<span data-ttu-id="9ff0a-401">6</span><span class="sxs-lookup"><span data-stu-id="9ff0a-401">6</span></span> |<span data-ttu-id="9ff0a-402">12</span><span class="sxs-lookup"><span data-stu-id="9ff0a-402">12</span></span> |<span data-ttu-id="9ff0a-403">23</span><span class="sxs-lookup"><span data-stu-id="9ff0a-403">23</span></span> |
| <span data-ttu-id="9ff0a-404">DW200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-404">DW200</span></span> |<span data-ttu-id="9ff0a-405">6</span><span class="sxs-lookup"><span data-stu-id="9ff0a-405">6</span></span> |<span data-ttu-id="9ff0a-406">12</span><span class="sxs-lookup"><span data-stu-id="9ff0a-406">12</span></span> |<span data-ttu-id="9ff0a-407">23</span><span class="sxs-lookup"><span data-stu-id="9ff0a-407">23</span></span> |<span data-ttu-id="9ff0a-408">47</span><span class="sxs-lookup"><span data-stu-id="9ff0a-408">47</span></span> |
| <span data-ttu-id="9ff0a-409">DW300</span><span class="sxs-lookup"><span data-stu-id="9ff0a-409">DW300</span></span> |<span data-ttu-id="9ff0a-410">6</span><span class="sxs-lookup"><span data-stu-id="9ff0a-410">6</span></span> |<span data-ttu-id="9ff0a-411">12</span><span class="sxs-lookup"><span data-stu-id="9ff0a-411">12</span></span> |<span data-ttu-id="9ff0a-412">23</span><span class="sxs-lookup"><span data-stu-id="9ff0a-412">23</span></span> |<span data-ttu-id="9ff0a-413">47</span><span class="sxs-lookup"><span data-stu-id="9ff0a-413">47</span></span> |
| <span data-ttu-id="9ff0a-414">DW400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-414">DW400</span></span> |<span data-ttu-id="9ff0a-415">6</span><span class="sxs-lookup"><span data-stu-id="9ff0a-415">6</span></span> |<span data-ttu-id="9ff0a-416">23</span><span class="sxs-lookup"><span data-stu-id="9ff0a-416">23</span></span> |<span data-ttu-id="9ff0a-417">47</span><span class="sxs-lookup"><span data-stu-id="9ff0a-417">47</span></span> |<span data-ttu-id="9ff0a-418">94</span><span class="sxs-lookup"><span data-stu-id="9ff0a-418">94</span></span> |
| <span data-ttu-id="9ff0a-419">DW500</span><span class="sxs-lookup"><span data-stu-id="9ff0a-419">DW500</span></span> |<span data-ttu-id="9ff0a-420">6</span><span class="sxs-lookup"><span data-stu-id="9ff0a-420">6</span></span> |<span data-ttu-id="9ff0a-421">23</span><span class="sxs-lookup"><span data-stu-id="9ff0a-421">23</span></span> |<span data-ttu-id="9ff0a-422">47</span><span class="sxs-lookup"><span data-stu-id="9ff0a-422">47</span></span> |<span data-ttu-id="9ff0a-423">94</span><span class="sxs-lookup"><span data-stu-id="9ff0a-423">94</span></span> |
| <span data-ttu-id="9ff0a-424">DW600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-424">DW600</span></span> |<span data-ttu-id="9ff0a-425">6</span><span class="sxs-lookup"><span data-stu-id="9ff0a-425">6</span></span> |<span data-ttu-id="9ff0a-426">23</span><span class="sxs-lookup"><span data-stu-id="9ff0a-426">23</span></span> |<span data-ttu-id="9ff0a-427">47</span><span class="sxs-lookup"><span data-stu-id="9ff0a-427">47</span></span> |<span data-ttu-id="9ff0a-428">94</span><span class="sxs-lookup"><span data-stu-id="9ff0a-428">94</span></span> |
| <span data-ttu-id="9ff0a-429">DW1000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-429">DW1000</span></span> |<span data-ttu-id="9ff0a-430">6</span><span class="sxs-lookup"><span data-stu-id="9ff0a-430">6</span></span> |<span data-ttu-id="9ff0a-431">47</span><span class="sxs-lookup"><span data-stu-id="9ff0a-431">47</span></span> |<span data-ttu-id="9ff0a-432">94</span><span class="sxs-lookup"><span data-stu-id="9ff0a-432">94</span></span> |<span data-ttu-id="9ff0a-433">188</span><span class="sxs-lookup"><span data-stu-id="9ff0a-433">188</span></span> |
| <span data-ttu-id="9ff0a-434">DW1200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-434">DW1200</span></span> |<span data-ttu-id="9ff0a-435">6</span><span class="sxs-lookup"><span data-stu-id="9ff0a-435">6</span></span> |<span data-ttu-id="9ff0a-436">47</span><span class="sxs-lookup"><span data-stu-id="9ff0a-436">47</span></span> |<span data-ttu-id="9ff0a-437">94</span><span class="sxs-lookup"><span data-stu-id="9ff0a-437">94</span></span> |<span data-ttu-id="9ff0a-438">188</span><span class="sxs-lookup"><span data-stu-id="9ff0a-438">188</span></span> |
| <span data-ttu-id="9ff0a-439">DW1500</span><span class="sxs-lookup"><span data-stu-id="9ff0a-439">DW1500</span></span> |<span data-ttu-id="9ff0a-440">6</span><span class="sxs-lookup"><span data-stu-id="9ff0a-440">6</span></span> |<span data-ttu-id="9ff0a-441">47</span><span class="sxs-lookup"><span data-stu-id="9ff0a-441">47</span></span> |<span data-ttu-id="9ff0a-442">94</span><span class="sxs-lookup"><span data-stu-id="9ff0a-442">94</span></span> |<span data-ttu-id="9ff0a-443">188</span><span class="sxs-lookup"><span data-stu-id="9ff0a-443">188</span></span> |
| <span data-ttu-id="9ff0a-444">DW2000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-444">DW2000</span></span> |<span data-ttu-id="9ff0a-445">6</span><span class="sxs-lookup"><span data-stu-id="9ff0a-445">6</span></span> |<span data-ttu-id="9ff0a-446">94</span><span class="sxs-lookup"><span data-stu-id="9ff0a-446">94</span></span> |<span data-ttu-id="9ff0a-447">188</span><span class="sxs-lookup"><span data-stu-id="9ff0a-447">188</span></span> |<span data-ttu-id="9ff0a-448">375</span><span class="sxs-lookup"><span data-stu-id="9ff0a-448">375</span></span> |
| <span data-ttu-id="9ff0a-449">DW3000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-449">DW3000</span></span> |<span data-ttu-id="9ff0a-450">6</span><span class="sxs-lookup"><span data-stu-id="9ff0a-450">6</span></span> |<span data-ttu-id="9ff0a-451">94</span><span class="sxs-lookup"><span data-stu-id="9ff0a-451">94</span></span> |<span data-ttu-id="9ff0a-452">188</span><span class="sxs-lookup"><span data-stu-id="9ff0a-452">188</span></span> |<span data-ttu-id="9ff0a-453">375</span><span class="sxs-lookup"><span data-stu-id="9ff0a-453">375</span></span> |
| <span data-ttu-id="9ff0a-454">DW6000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-454">DW6000</span></span> |<span data-ttu-id="9ff0a-455">6</span><span class="sxs-lookup"><span data-stu-id="9ff0a-455">6</span></span> |<span data-ttu-id="9ff0a-456">188</span><span class="sxs-lookup"><span data-stu-id="9ff0a-456">188</span></span> |<span data-ttu-id="9ff0a-457">375</span><span class="sxs-lookup"><span data-stu-id="9ff0a-457">375</span></span> |<span data-ttu-id="9ff0a-458">750</span><span class="sxs-lookup"><span data-stu-id="9ff0a-458">750</span></span> |

<span data-ttu-id="9ff0a-459">시스템 전체 메모리 할당 테이블에서 보면 xlargerc 리소스 클래스의 DW2000에서 실행되는 쿼리에는 전체 SQL Data Warehouse에 대해 총 375GB(6,400MB * 60개 배포/1,024, 이 결과를 GB로 변환)의 메모리가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-459">From this table of system-wide memory allocations, you can see that a query running on a DW2000 in the xlargerc resource class is allocated a total of 375 GB of memory (6,400 MB * 60 distributions / 1,024 to convert to GB) over the entirety of your SQL Data Warehouse.</span></span>

<span data-ttu-id="9ff0a-460">동일한 계산이 정적 리소스 클래스에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-460">The same calculation applies to static resource classes.</span></span>
 
## <a name="concurrency-slot-consumption"></a><span data-ttu-id="9ff0a-461">동시성 슬롯 사용량</span><span class="sxs-lookup"><span data-stu-id="9ff0a-461">Concurrency slot consumption</span></span>  
<span data-ttu-id="9ff0a-462">SQL 데이터 웨어하우스는 더 많은 리소스 클래스에서 실행되는 쿼리에 더 많은 메모리를 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-462">SQL Data Warehouse grants more memory to queries running in higher resource classes.</span></span> <span data-ttu-id="9ff0a-463">메모리는 고정된 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-463">Memory is a fixed resource.</span></span>  <span data-ttu-id="9ff0a-464">따라서 쿼리당 할당되는 메모리가 많을수록 동시에 실행할 수 있는 쿼리의 수가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-464">Therefore, the more memory allocated per query, the fewer concurrent queries can execute.</span></span> <span data-ttu-id="9ff0a-465">다음 테이블에서는 앞에서 설명한 모든 개념을 단일 보기로 다시 제공합니다. 이 보기에는 DWU에서 사용 가능한 동시성 슬롯의 수와 각 리소스 클래스가 사용하는 슬롯 수가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-465">The following table reiterates all of the previous concepts in a single view that shows the number of concurrency slots available by DWU and the slots consumed by each resource class.</span></span>  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a><span data-ttu-id="9ff0a-466">동적 리소스 클래스에 대한 동시성 슬롯의 할당 및 사용량</span><span class="sxs-lookup"><span data-stu-id="9ff0a-466">Allocation and consumption of concurrency slots for dynamic resource classes</span></span>  
| <span data-ttu-id="9ff0a-467">DWU</span><span class="sxs-lookup"><span data-stu-id="9ff0a-467">DWU</span></span> | <span data-ttu-id="9ff0a-468">최대 동시 쿼리 수</span><span class="sxs-lookup"><span data-stu-id="9ff0a-468">Maximum concurrent queries</span></span> | <span data-ttu-id="9ff0a-469">할당된 동시성 슬롯 수</span><span class="sxs-lookup"><span data-stu-id="9ff0a-469">Concurrency slots allocated</span></span> | <span data-ttu-id="9ff0a-470">smallrc에서 사용되는 슬롯</span><span class="sxs-lookup"><span data-stu-id="9ff0a-470">Slots used by smallrc</span></span> | <span data-ttu-id="9ff0a-471">mediumrc에서 사용되는 슬롯</span><span class="sxs-lookup"><span data-stu-id="9ff0a-471">Slots used by mediumrc</span></span> | <span data-ttu-id="9ff0a-472">largerc에서 사용되는 슬롯</span><span class="sxs-lookup"><span data-stu-id="9ff0a-472">Slots used by largerc</span></span> | <span data-ttu-id="9ff0a-473">xlargerc에서 사용되는 슬롯</span><span class="sxs-lookup"><span data-stu-id="9ff0a-473">Slots used by xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="9ff0a-474">DW100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-474">DW100</span></span> |<span data-ttu-id="9ff0a-475">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-475">4</span></span> |<span data-ttu-id="9ff0a-476">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-476">4</span></span> |<span data-ttu-id="9ff0a-477">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-477">1</span></span> |<span data-ttu-id="9ff0a-478">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-478">1</span></span> |<span data-ttu-id="9ff0a-479">2</span><span class="sxs-lookup"><span data-stu-id="9ff0a-479">2</span></span> |<span data-ttu-id="9ff0a-480">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-480">4</span></span> |
| <span data-ttu-id="9ff0a-481">DW200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-481">DW200</span></span> |<span data-ttu-id="9ff0a-482">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-482">8</span></span> |<span data-ttu-id="9ff0a-483">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-483">8</span></span> |<span data-ttu-id="9ff0a-484">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-484">1</span></span> |<span data-ttu-id="9ff0a-485">2</span><span class="sxs-lookup"><span data-stu-id="9ff0a-485">2</span></span> |<span data-ttu-id="9ff0a-486">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-486">4</span></span> |<span data-ttu-id="9ff0a-487">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-487">8</span></span> |
| <span data-ttu-id="9ff0a-488">DW300</span><span class="sxs-lookup"><span data-stu-id="9ff0a-488">DW300</span></span> |<span data-ttu-id="9ff0a-489">12</span><span class="sxs-lookup"><span data-stu-id="9ff0a-489">12</span></span> |<span data-ttu-id="9ff0a-490">12</span><span class="sxs-lookup"><span data-stu-id="9ff0a-490">12</span></span> |<span data-ttu-id="9ff0a-491">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-491">1</span></span> |<span data-ttu-id="9ff0a-492">2</span><span class="sxs-lookup"><span data-stu-id="9ff0a-492">2</span></span> |<span data-ttu-id="9ff0a-493">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-493">4</span></span> |<span data-ttu-id="9ff0a-494">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-494">8</span></span> |
| <span data-ttu-id="9ff0a-495">DW400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-495">DW400</span></span> |<span data-ttu-id="9ff0a-496">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-496">16</span></span> |<span data-ttu-id="9ff0a-497">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-497">16</span></span> |<span data-ttu-id="9ff0a-498">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-498">1</span></span> |<span data-ttu-id="9ff0a-499">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-499">4</span></span> |<span data-ttu-id="9ff0a-500">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-500">8</span></span> |<span data-ttu-id="9ff0a-501">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-501">16</span></span> |
| <span data-ttu-id="9ff0a-502">DW500</span><span class="sxs-lookup"><span data-stu-id="9ff0a-502">DW500</span></span> |<span data-ttu-id="9ff0a-503">20</span><span class="sxs-lookup"><span data-stu-id="9ff0a-503">20</span></span> |<span data-ttu-id="9ff0a-504">20</span><span class="sxs-lookup"><span data-stu-id="9ff0a-504">20</span></span> |<span data-ttu-id="9ff0a-505">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-505">1</span></span> |<span data-ttu-id="9ff0a-506">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-506">4</span></span> |<span data-ttu-id="9ff0a-507">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-507">8</span></span> |<span data-ttu-id="9ff0a-508">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-508">16</span></span> |
| <span data-ttu-id="9ff0a-509">DW600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-509">DW600</span></span> |<span data-ttu-id="9ff0a-510">24</span><span class="sxs-lookup"><span data-stu-id="9ff0a-510">24</span></span> |<span data-ttu-id="9ff0a-511">24</span><span class="sxs-lookup"><span data-stu-id="9ff0a-511">24</span></span> |<span data-ttu-id="9ff0a-512">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-512">1</span></span> |<span data-ttu-id="9ff0a-513">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-513">4</span></span> |<span data-ttu-id="9ff0a-514">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-514">8</span></span> |<span data-ttu-id="9ff0a-515">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-515">16</span></span> |
| <span data-ttu-id="9ff0a-516">DW1000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-516">DW1000</span></span> |<span data-ttu-id="9ff0a-517">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-517">32</span></span> |<span data-ttu-id="9ff0a-518">40</span><span class="sxs-lookup"><span data-stu-id="9ff0a-518">40</span></span> |<span data-ttu-id="9ff0a-519">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-519">1</span></span> |<span data-ttu-id="9ff0a-520">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-520">8</span></span> |<span data-ttu-id="9ff0a-521">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-521">16</span></span> |<span data-ttu-id="9ff0a-522">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-522">32</span></span> |
| <span data-ttu-id="9ff0a-523">DW1200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-523">DW1200</span></span> |<span data-ttu-id="9ff0a-524">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-524">32</span></span> |<span data-ttu-id="9ff0a-525">48</span><span class="sxs-lookup"><span data-stu-id="9ff0a-525">48</span></span> |<span data-ttu-id="9ff0a-526">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-526">1</span></span> |<span data-ttu-id="9ff0a-527">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-527">8</span></span> |<span data-ttu-id="9ff0a-528">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-528">16</span></span> |<span data-ttu-id="9ff0a-529">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-529">32</span></span> |
| <span data-ttu-id="9ff0a-530">DW1500</span><span class="sxs-lookup"><span data-stu-id="9ff0a-530">DW1500</span></span> |<span data-ttu-id="9ff0a-531">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-531">32</span></span> |<span data-ttu-id="9ff0a-532">60</span><span class="sxs-lookup"><span data-stu-id="9ff0a-532">60</span></span> |<span data-ttu-id="9ff0a-533">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-533">1</span></span> |<span data-ttu-id="9ff0a-534">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-534">8</span></span> |<span data-ttu-id="9ff0a-535">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-535">16</span></span> |<span data-ttu-id="9ff0a-536">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-536">32</span></span> |
| <span data-ttu-id="9ff0a-537">DW2000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-537">DW2000</span></span> |<span data-ttu-id="9ff0a-538">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-538">32</span></span> |<span data-ttu-id="9ff0a-539">80</span><span class="sxs-lookup"><span data-stu-id="9ff0a-539">80</span></span> |<span data-ttu-id="9ff0a-540">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-540">1</span></span> |<span data-ttu-id="9ff0a-541">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-541">16</span></span> |<span data-ttu-id="9ff0a-542">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-542">32</span></span> |<span data-ttu-id="9ff0a-543">64</span><span class="sxs-lookup"><span data-stu-id="9ff0a-543">64</span></span> |
| <span data-ttu-id="9ff0a-544">DW3000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-544">DW3000</span></span> |<span data-ttu-id="9ff0a-545">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-545">32</span></span> |<span data-ttu-id="9ff0a-546">120</span><span class="sxs-lookup"><span data-stu-id="9ff0a-546">120</span></span> |<span data-ttu-id="9ff0a-547">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-547">1</span></span> |<span data-ttu-id="9ff0a-548">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-548">16</span></span> |<span data-ttu-id="9ff0a-549">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-549">32</span></span> |<span data-ttu-id="9ff0a-550">64</span><span class="sxs-lookup"><span data-stu-id="9ff0a-550">64</span></span> |
| <span data-ttu-id="9ff0a-551">DW6000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-551">DW6000</span></span> |<span data-ttu-id="9ff0a-552">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-552">32</span></span> |<span data-ttu-id="9ff0a-553">240</span><span class="sxs-lookup"><span data-stu-id="9ff0a-553">240</span></span> |<span data-ttu-id="9ff0a-554">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-554">1</span></span> |<span data-ttu-id="9ff0a-555">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-555">32</span></span> |<span data-ttu-id="9ff0a-556">64</span><span class="sxs-lookup"><span data-stu-id="9ff0a-556">64</span></span> |<span data-ttu-id="9ff0a-557">128</span><span class="sxs-lookup"><span data-stu-id="9ff0a-557">128</span></span> |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a><span data-ttu-id="9ff0a-558">정적 리소스 클래스에 대한 동시성 슬롯의 할당 및 사용량</span><span class="sxs-lookup"><span data-stu-id="9ff0a-558">Allocation and consumption of concurrency slots for static resource classes</span></span>  
| <span data-ttu-id="9ff0a-559">DWU</span><span class="sxs-lookup"><span data-stu-id="9ff0a-559">DWU</span></span> | <span data-ttu-id="9ff0a-560">최대 동시 쿼리 수</span><span class="sxs-lookup"><span data-stu-id="9ff0a-560">Maximum concurrent queries</span></span> | <span data-ttu-id="9ff0a-561">할당된 동시성 슬롯 수</span><span class="sxs-lookup"><span data-stu-id="9ff0a-561">Concurrency slots allocated</span></span> |<span data-ttu-id="9ff0a-562">staticrc10</span><span class="sxs-lookup"><span data-stu-id="9ff0a-562">staticrc10</span></span> | <span data-ttu-id="9ff0a-563">staticrc20</span><span class="sxs-lookup"><span data-stu-id="9ff0a-563">staticrc20</span></span> | <span data-ttu-id="9ff0a-564">staticrc30</span><span class="sxs-lookup"><span data-stu-id="9ff0a-564">staticrc30</span></span> | <span data-ttu-id="9ff0a-565">staticrc40</span><span class="sxs-lookup"><span data-stu-id="9ff0a-565">staticrc40</span></span> | <span data-ttu-id="9ff0a-566">staticrc50</span><span class="sxs-lookup"><span data-stu-id="9ff0a-566">staticrc50</span></span> | <span data-ttu-id="9ff0a-567">staticrc60</span><span class="sxs-lookup"><span data-stu-id="9ff0a-567">staticrc60</span></span> | <span data-ttu-id="9ff0a-568">staticrc70</span><span class="sxs-lookup"><span data-stu-id="9ff0a-568">staticrc70</span></span> | <span data-ttu-id="9ff0a-569">staticrc80</span><span class="sxs-lookup"><span data-stu-id="9ff0a-569">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="9ff0a-570">DW100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-570">DW100</span></span> |<span data-ttu-id="9ff0a-571">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-571">4</span></span> |<span data-ttu-id="9ff0a-572">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-572">4</span></span> |<span data-ttu-id="9ff0a-573">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-573">1</span></span> |<span data-ttu-id="9ff0a-574">2</span><span class="sxs-lookup"><span data-stu-id="9ff0a-574">2</span></span> |<span data-ttu-id="9ff0a-575">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-575">4</span></span> |<span data-ttu-id="9ff0a-576">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-576">4</span></span> |<span data-ttu-id="9ff0a-577">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-577">4</span></span> |<span data-ttu-id="9ff0a-578">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-578">4</span></span> |<span data-ttu-id="9ff0a-579">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-579">4</span></span> |<span data-ttu-id="9ff0a-580">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-580">4</span></span> |
| <span data-ttu-id="9ff0a-581">DW200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-581">DW200</span></span> |<span data-ttu-id="9ff0a-582">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-582">8</span></span> |<span data-ttu-id="9ff0a-583">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-583">8</span></span> |<span data-ttu-id="9ff0a-584">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-584">1</span></span> |<span data-ttu-id="9ff0a-585">2</span><span class="sxs-lookup"><span data-stu-id="9ff0a-585">2</span></span> |<span data-ttu-id="9ff0a-586">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-586">4</span></span> |<span data-ttu-id="9ff0a-587">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-587">8</span></span> |<span data-ttu-id="9ff0a-588">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-588">8</span></span> |<span data-ttu-id="9ff0a-589">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-589">8</span></span> |<span data-ttu-id="9ff0a-590">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-590">8</span></span> |<span data-ttu-id="9ff0a-591">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-591">8</span></span> |
| <span data-ttu-id="9ff0a-592">DW300</span><span class="sxs-lookup"><span data-stu-id="9ff0a-592">DW300</span></span> |<span data-ttu-id="9ff0a-593">12</span><span class="sxs-lookup"><span data-stu-id="9ff0a-593">12</span></span> |<span data-ttu-id="9ff0a-594">12</span><span class="sxs-lookup"><span data-stu-id="9ff0a-594">12</span></span> |<span data-ttu-id="9ff0a-595">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-595">1</span></span> |<span data-ttu-id="9ff0a-596">2</span><span class="sxs-lookup"><span data-stu-id="9ff0a-596">2</span></span> |<span data-ttu-id="9ff0a-597">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-597">4</span></span> |<span data-ttu-id="9ff0a-598">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-598">8</span></span> |<span data-ttu-id="9ff0a-599">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-599">8</span></span> |<span data-ttu-id="9ff0a-600">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-600">8</span></span> |<span data-ttu-id="9ff0a-601">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-601">8</span></span> |<span data-ttu-id="9ff0a-602">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-602">8</span></span> |
| <span data-ttu-id="9ff0a-603">DW400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-603">DW400</span></span> |<span data-ttu-id="9ff0a-604">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-604">16</span></span> |<span data-ttu-id="9ff0a-605">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-605">16</span></span> |<span data-ttu-id="9ff0a-606">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-606">1</span></span> |<span data-ttu-id="9ff0a-607">2</span><span class="sxs-lookup"><span data-stu-id="9ff0a-607">2</span></span> |<span data-ttu-id="9ff0a-608">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-608">4</span></span> |<span data-ttu-id="9ff0a-609">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-609">8</span></span> |<span data-ttu-id="9ff0a-610">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-610">16</span></span> |<span data-ttu-id="9ff0a-611">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-611">16</span></span> |<span data-ttu-id="9ff0a-612">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-612">16</span></span> |<span data-ttu-id="9ff0a-613">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-613">16</span></span> |
| <span data-ttu-id="9ff0a-614">DW500</span><span class="sxs-lookup"><span data-stu-id="9ff0a-614">DW500</span></span> | <span data-ttu-id="9ff0a-615">20</span><span class="sxs-lookup"><span data-stu-id="9ff0a-615">20</span></span>| <span data-ttu-id="9ff0a-616">20</span><span class="sxs-lookup"><span data-stu-id="9ff0a-616">20</span></span>| <span data-ttu-id="9ff0a-617">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-617">1</span></span>| <span data-ttu-id="9ff0a-618">2</span><span class="sxs-lookup"><span data-stu-id="9ff0a-618">2</span></span>| <span data-ttu-id="9ff0a-619">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-619">4</span></span>| <span data-ttu-id="9ff0a-620">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-620">8</span></span>| <span data-ttu-id="9ff0a-621">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-621">16</span></span>| <span data-ttu-id="9ff0a-622">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-622">16</span></span>| <span data-ttu-id="9ff0a-623">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-623">16</span></span>| <span data-ttu-id="9ff0a-624">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-624">16</span></span>|
| <span data-ttu-id="9ff0a-625">DW600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-625">DW600</span></span> | <span data-ttu-id="9ff0a-626">24</span><span class="sxs-lookup"><span data-stu-id="9ff0a-626">24</span></span>| <span data-ttu-id="9ff0a-627">24</span><span class="sxs-lookup"><span data-stu-id="9ff0a-627">24</span></span>| <span data-ttu-id="9ff0a-628">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-628">1</span></span>| <span data-ttu-id="9ff0a-629">2</span><span class="sxs-lookup"><span data-stu-id="9ff0a-629">2</span></span>| <span data-ttu-id="9ff0a-630">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-630">4</span></span>| <span data-ttu-id="9ff0a-631">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-631">8</span></span>| <span data-ttu-id="9ff0a-632">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-632">16</span></span>| <span data-ttu-id="9ff0a-633">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-633">16</span></span>| <span data-ttu-id="9ff0a-634">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-634">16</span></span>| <span data-ttu-id="9ff0a-635">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-635">16</span></span>|
| <span data-ttu-id="9ff0a-636">DW1000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-636">DW1000</span></span> | <span data-ttu-id="9ff0a-637">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-637">32</span></span>| <span data-ttu-id="9ff0a-638">40</span><span class="sxs-lookup"><span data-stu-id="9ff0a-638">40</span></span>| <span data-ttu-id="9ff0a-639">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-639">1</span></span>| <span data-ttu-id="9ff0a-640">2</span><span class="sxs-lookup"><span data-stu-id="9ff0a-640">2</span></span>| <span data-ttu-id="9ff0a-641">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-641">4</span></span>| <span data-ttu-id="9ff0a-642">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-642">8</span></span>| <span data-ttu-id="9ff0a-643">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-643">16</span></span>| <span data-ttu-id="9ff0a-644">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-644">32</span></span>| <span data-ttu-id="9ff0a-645">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-645">32</span></span>| <span data-ttu-id="9ff0a-646">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-646">32</span></span>|
| <span data-ttu-id="9ff0a-647">DW1200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-647">DW1200</span></span> | <span data-ttu-id="9ff0a-648">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-648">32</span></span>| <span data-ttu-id="9ff0a-649">48</span><span class="sxs-lookup"><span data-stu-id="9ff0a-649">48</span></span>| <span data-ttu-id="9ff0a-650">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-650">1</span></span>| <span data-ttu-id="9ff0a-651">2</span><span class="sxs-lookup"><span data-stu-id="9ff0a-651">2</span></span>| <span data-ttu-id="9ff0a-652">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-652">4</span></span>| <span data-ttu-id="9ff0a-653">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-653">8</span></span>| <span data-ttu-id="9ff0a-654">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-654">16</span></span>| <span data-ttu-id="9ff0a-655">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-655">32</span></span>| <span data-ttu-id="9ff0a-656">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-656">32</span></span>| <span data-ttu-id="9ff0a-657">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-657">32</span></span>|
| <span data-ttu-id="9ff0a-658">DW1500</span><span class="sxs-lookup"><span data-stu-id="9ff0a-658">DW1500</span></span> | <span data-ttu-id="9ff0a-659">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-659">32</span></span>| <span data-ttu-id="9ff0a-660">60</span><span class="sxs-lookup"><span data-stu-id="9ff0a-660">60</span></span>| <span data-ttu-id="9ff0a-661">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-661">1</span></span>| <span data-ttu-id="9ff0a-662">2</span><span class="sxs-lookup"><span data-stu-id="9ff0a-662">2</span></span>| <span data-ttu-id="9ff0a-663">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-663">4</span></span>| <span data-ttu-id="9ff0a-664">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-664">8</span></span>| <span data-ttu-id="9ff0a-665">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-665">16</span></span>| <span data-ttu-id="9ff0a-666">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-666">32</span></span>| <span data-ttu-id="9ff0a-667">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-667">32</span></span>| <span data-ttu-id="9ff0a-668">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-668">32</span></span>|
| <span data-ttu-id="9ff0a-669">DW2000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-669">DW2000</span></span> | <span data-ttu-id="9ff0a-670">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-670">32</span></span>| <span data-ttu-id="9ff0a-671">80</span><span class="sxs-lookup"><span data-stu-id="9ff0a-671">80</span></span>| <span data-ttu-id="9ff0a-672">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-672">1</span></span>| <span data-ttu-id="9ff0a-673">2</span><span class="sxs-lookup"><span data-stu-id="9ff0a-673">2</span></span>| <span data-ttu-id="9ff0a-674">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-674">4</span></span>| <span data-ttu-id="9ff0a-675">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-675">8</span></span>| <span data-ttu-id="9ff0a-676">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-676">16</span></span>| <span data-ttu-id="9ff0a-677">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-677">32</span></span>| <span data-ttu-id="9ff0a-678">64</span><span class="sxs-lookup"><span data-stu-id="9ff0a-678">64</span></span>| <span data-ttu-id="9ff0a-679">64</span><span class="sxs-lookup"><span data-stu-id="9ff0a-679">64</span></span>|
| <span data-ttu-id="9ff0a-680">DW3000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-680">DW3000</span></span> | <span data-ttu-id="9ff0a-681">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-681">32</span></span>| <span data-ttu-id="9ff0a-682">120</span><span class="sxs-lookup"><span data-stu-id="9ff0a-682">120</span></span>| <span data-ttu-id="9ff0a-683">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-683">1</span></span>| <span data-ttu-id="9ff0a-684">2</span><span class="sxs-lookup"><span data-stu-id="9ff0a-684">2</span></span>| <span data-ttu-id="9ff0a-685">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-685">4</span></span>| <span data-ttu-id="9ff0a-686">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-686">8</span></span>| <span data-ttu-id="9ff0a-687">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-687">16</span></span>| <span data-ttu-id="9ff0a-688">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-688">32</span></span>| <span data-ttu-id="9ff0a-689">64</span><span class="sxs-lookup"><span data-stu-id="9ff0a-689">64</span></span>| <span data-ttu-id="9ff0a-690">64</span><span class="sxs-lookup"><span data-stu-id="9ff0a-690">64</span></span>|
| <span data-ttu-id="9ff0a-691">DW6000</span><span class="sxs-lookup"><span data-stu-id="9ff0a-691">DW6000</span></span> | <span data-ttu-id="9ff0a-692">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-692">32</span></span>| <span data-ttu-id="9ff0a-693">240</span><span class="sxs-lookup"><span data-stu-id="9ff0a-693">240</span></span>| <span data-ttu-id="9ff0a-694">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-694">1</span></span>| <span data-ttu-id="9ff0a-695">2</span><span class="sxs-lookup"><span data-stu-id="9ff0a-695">2</span></span>| <span data-ttu-id="9ff0a-696">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-696">4</span></span>| <span data-ttu-id="9ff0a-697">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-697">8</span></span>| <span data-ttu-id="9ff0a-698">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-698">16</span></span>| <span data-ttu-id="9ff0a-699">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-699">32</span></span>| <span data-ttu-id="9ff0a-700">64</span><span class="sxs-lookup"><span data-stu-id="9ff0a-700">64</span></span>| <span data-ttu-id="9ff0a-701">128</span><span class="sxs-lookup"><span data-stu-id="9ff0a-701">128</span></span>|

<span data-ttu-id="9ff0a-702">이러한 테이블에서 볼 수 있는 것처럼 DW1000으로 실행되는 SQL 데이터 웨어하우스는 최대 32개의 동시 쿼리 및 총 40개의 동시성 슬롯을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-702">From these tables, you can see that SQL Data Warehouse running as DW1000 allocates a maximum of 32 concurrent queries and a total of 40 concurrency slots.</span></span> <span data-ttu-id="9ff0a-703">모든 사용자가 smallrc에서 실행하는 경우 각 쿼리가 동시성 슬롯 1개를 소비하므로 32개의 동시성 쿼리가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-703">If all users are running in smallrc, 32 concurrent queries would be allowed because each query would consume 1 concurrency slot.</span></span> <span data-ttu-id="9ff0a-704">DW1000의 모든 사용자가 mediumrc에서 실행하는 경우, 각 쿼리에는 총 메모리 할당량 47GB에서 배포당 800MB가 할당되고 동시성은 5명의 사용자에게 제한됩니다(40개 동시성 슬롯/mediumrc 사용자당 8개 슬롯).</span><span class="sxs-lookup"><span data-stu-id="9ff0a-704">If all users on a DW1000 were running in mediumrc, each query would be allocated 800 MB per distribution for a total memory allocation of 47 GB per query, and concurrency would be limited to 5 users (40 concurrency slots / 8 slots per mediumrc user).</span></span>

## <a name="selecting-proper-resource-class"></a><span data-ttu-id="9ff0a-705">적절한 리소스 클래스 선택</span><span class="sxs-lookup"><span data-stu-id="9ff0a-705">Selecting proper resource class</span></span>  
<span data-ttu-id="9ff0a-706">사용자의 리소스 클래스를 변경하기보다는 사용자를 리소스 클래스에 영구적으로 할당하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-706">A good practice is to permanently assign users to a resource class rather than changing their resource classes.</span></span> <span data-ttu-id="9ff0a-707">예를 들어 클러스터형 Columnstore 테이블에 대한 로드 시에는 리소스를 많이 할당할수록 품질이 보다 뛰어난 인덱스가 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-707">For example, loads to clustered columnstore tables create higher-quality indexes when allocated more memory.</span></span> <span data-ttu-id="9ff0a-708">로드가 더 높은 메모리에 액세스할 수 있도록 하려면 특별히 데이타 로드에 대한 사용자를 만들고 이 사용자를 더 높은 리소스 클래스에 영구적으로 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-708">To ensure that loads have access to higher memory, create a user specifically for loading data and permanently assign this user to a higher resource class.</span></span>
<span data-ttu-id="9ff0a-709">여기에서 준수할 수 있는 몇 가지 모범 사례가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-709">There are a couple of best practices to follow here.</span></span> <span data-ttu-id="9ff0a-710">위에서 언급한 것처럼 SQL DW에서는 두 가지 유형의 리소스 클래스 형식, 즉 정적 리소스 클래스 및 동적 리소스 클래스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-710">As mentioned above, SQL DW supports two kinds of resource class types: static resource classes and dynamic resource classes.</span></span>
### <a name="loading-best-practices"></a><span data-ttu-id="9ff0a-711">로드 모범 사례</span><span class="sxs-lookup"><span data-stu-id="9ff0a-711">Loading best practices</span></span>
1.  <span data-ttu-id="9ff0a-712">보통 크기의 데이터가 로드될 것으로 예상되면 정적 리소스 클래스를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-712">If the expectations are loads with regular amount of data, a static resource class is a good choice.</span></span> <span data-ttu-id="9ff0a-713">나중에 더 많은 계산 능력을 위해 확장할 경우 로드 사용자는 추가 메모리를 소비하지 않으므로 데이터 웨어하우스는 기본적으로 더 많은 동시 쿼리를 실행할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-713">Later, when scaling up to get more computational power, the data warehouse will be able to run more concurrent queries out-of-the-box, as the load user does not consume more memory.</span></span>
2.  <span data-ttu-id="9ff0a-714">경우에 따라 더 큰 로드가 예상될 경우 동적 리소스 클래스를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-714">If the expectations are bigger loads in some occasions, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="9ff0a-715">나중에 더 많은 계산 능력을 위해 확장할 경우 로드 사용자는 기본적으로 더 많은 메모리를 얻게 되므로 로드를 더 빠르게 진행할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-715">Later, when scaling up to get more computational power, the load user will get more memory out-of-the-box, hence allowing the load to perform faster.</span></span>

<span data-ttu-id="9ff0a-716">로드를 효율적으로 처리하는 데 필요한 메모리는 로드된 테이블의 특성과 처리된 데이터의 양에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-716">The memory needed to process loads efficiently depends on the nature of the table loaded and the amount of data processed.</span></span> <span data-ttu-id="9ff0a-717">예를 들어 CCI 테이블로 데이터를 로드하려면 CCI 행 그룹이 최적성에 도달할 수 있도록 하는 데 메모리가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-717">For instance, loading data into CCI tables requires some memory to let CCI rowgroups reach optimality.</span></span> <span data-ttu-id="9ff0a-718">자세한 내용은 Columnstore 인덱스 - 데이터 로드 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-718">For more details, see the Columnstore indexes - data loading guidance.</span></span>

<span data-ttu-id="9ff0a-719">모범 사례로, 로드 시 200MB 이상의 메모리를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-719">As a best practice, we advise you to use at least 200MB of memory for loads.</span></span>

### <a name="querying-best-practices"></a><span data-ttu-id="9ff0a-720">쿼리 모범 사례</span><span class="sxs-lookup"><span data-stu-id="9ff0a-720">Querying best practices</span></span>
<span data-ttu-id="9ff0a-721">쿼리마다 복잡성에 따라 다른 요구 사항을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-721">Queries have different requirements depending on their complexity.</span></span> <span data-ttu-id="9ff0a-722">쿼리당 메모리를 늘리거나 동시성을 늘리면 쿼리 요구에 따라 전체 처리량을 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-722">Increasing memory per query or increasing the concurrency are both valid ways to augment overall throughput depending on the query needs.</span></span>
1.  <span data-ttu-id="9ff0a-723">주기적으로 복잡한 쿼리가 예상되고(예: 매일 및 매주 보고서 생성) 동시성을 활용할 필요가 없는 경우 동적 리소스 클래스를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-723">If the expectations are regular, complex queries (for instance, to generate daily and weekly reports) and do not need to take advantage of concurrency, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="9ff0a-724">시스템에 처리할 더 많은 데이터가 있는 경우 데이터 웨어하우스를 확장하면 쿼리를 실행하는 사용자에게 자동으로 추가 메모리가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-724">If the system has more data to process, scaling up the data warehouse will therefore automatically provide more memory to the user running the query.</span></span>
2.  <span data-ttu-id="9ff0a-725">가변 또는 일별 동시성 패턴이 예상되는 경우(예를 들어 광범위하게 액세스할 수 있는 웹 UI를 통해 데이터베이스를 쿼리하는 경우) 정적 리소스 클래스를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-725">If the expectations are variable or diurnal concurrency patterns (for instance if the database is queried through a web UI broadly accessible), a static resource class is a good choice.</span></span> <span data-ttu-id="9ff0a-726">나중에 데이터 웨어하우스를 확장할 때 정적 리소스 클래스와 관련된 사용자는 자동으로 더 많은 동시 쿼리를 실행할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-726">Later, when scaling up to data warehouse, the user associated with the static resource class will automatically be able to run more concurrent queries.</span></span>

<span data-ttu-id="9ff0a-727">쿼리 요구에 따라 적절한 메모리 권한을 선택하는 작업은 쿼리되는 데이터의 양, 테이블 스키마의 특성, 다양한 조인, 선택 및 그룹 조건자 등에 따라 좌우되므로 복잡할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-727">Selecting proper memory grant depending on the need of your query is non-trivial, as it depends on many factors, such as the amount of data queried, the nature of the table schemas, and various join, selection, and group predicates.</span></span> <span data-ttu-id="9ff0a-728">일반적인 관점에서 볼 때 더 많은 메모리를 할당하면 쿼리를 더 빠르게 완료할 수 있지만 전체적인 동시성은 떨어집니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-728">From a general standpoint, allocating more memory will allow queries to complete faster, but would reduce the overall concurrency.</span></span> <span data-ttu-id="9ff0a-729">동시성이 문제가 되지 않을 경우 메모리를 과도하게 할당해도 괜찮습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-729">If concurrency is not an issue, over-allocating memory does not harm.</span></span> <span data-ttu-id="9ff0a-730">처리량을 자세히 조정하려는 경우 다양한 리소스 클래스 특성이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-730">To fine-tune throughput, trying various flavors of resource classes may be required.</span></span>

<span data-ttu-id="9ff0a-731">다음 저장 프로시저를 사용하여 지정된 SLO에서 리소스 클래스별 동시성 및 메모리 권한을 확인하고 지정된 리소스 클래스의 분할되지 않은 CCI 테이블에 대해 메모리 집약적 CCI 작업을 수행하기 위한 가장 적절한 리소스 클래스를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-731">You can use the following stored procedure to figure out concurrency and memory grant per resource class at a given SLO and the closest best resource class for memory intensive CCI operations on non-partitioned CCI table at a given resource class:</span></span>

#### <a name="description"></a><span data-ttu-id="9ff0a-732">설명:</span><span class="sxs-lookup"><span data-stu-id="9ff0a-732">Description:</span></span>  
<span data-ttu-id="9ff0a-733">이 저장 프로시저의 용도는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-733">Here's the purpose of this stored procedure:</span></span>  
1. <span data-ttu-id="9ff0a-734">사용자가 지정된 SLO에서 리소스 클래스별로 동시성 및 메모리 권한을 파악하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-734">To help user figure out concurrency and memory grant per resource class at a given SLO.</span></span> <span data-ttu-id="9ff0a-735">사용자는 아래 예제에 나와 있는 것처럼 이를 위해 스키마 및 테이블 이름 둘 다에 대해 NULL을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-735">User needs to provide NULL for both schema and tablename for this as shown in the example below.</span></span>  
2. <span data-ttu-id="9ff0a-736">사용자가 지정된 리소스 클래스에서 분할되지 않은 CCI 테이블에 대해 메모리 집약적 CCI 작업(로드, 테이블 복사, 인덱스 다시 작성 등)을 수행하기 위해 가장 적합한 리소스 클래스를 찾아내도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-736">To help user figure out the closest best resource class for the memory intensed CCI operations (load, copy table, rebuild index, etc.) on non partitioned CCI table at a given resource class.</span></span> <span data-ttu-id="9ff0a-737">저장 프로시저는 테이블 스키마를 사용하여 필요한 메모리 권한을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-737">The stored proc uses table schema to find out the required memory grant for this.</span></span>

#### <a name="dependencies--restrictions"></a><span data-ttu-id="9ff0a-738">종속성 및 제한 사항:</span><span class="sxs-lookup"><span data-stu-id="9ff0a-738">Dependencies & Restrictions:</span></span>
- <span data-ttu-id="9ff0a-739">이 저장 프로시저는 분할된 cci 테이블의 메모리 요구 사항을 계산하도록 디자인되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-739">This stored proc is not designed to calculate memory requirement for partitioned-cci table.</span></span>    
- <span data-ttu-id="9ff0a-740">이 저장 프로시저는 CTAS/INSERT-SELECT의 SELECT 부분에 대한 메모리 요구 사항을 고려하지 않으며 간단한 SELECT로 간주합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-740">This stored proc doesn't take memory requirement into account for the SELECT part of CTAS/INSERT-SELECT and assumes it to be a simple SELECT.</span></span>
- <span data-ttu-id="9ff0a-741">이 저장 프로시저는 이 저장 프로시저가 만들어진 세션에서 사용할 수 있도록 임시 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-741">This stored proc uses a temp table so this can be used in the session where this stored proc was created.</span></span>    
- <span data-ttu-id="9ff0a-742">이 저장 프로시저는 현재 제공(예: 하드웨어 구성, DMS 구성)에 의존하므로 제공된 구성이 변경될 경우 이 저장 프로시저가 제대로 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-742">This stored proc depends on the current offerings (e.g. hardware configuration, DMS config) and if any of that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="9ff0a-743">이 저장 프로시저는 기존의 제공된 동시성 제한에 의존하므로 이러한 동시성 제한이 변경되면 이 저장 프로시저가 제대로 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-743">This stored proc depends on existing offered concurrency limit and if that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="9ff0a-744">이 저장 프로시저는 기존에 제공된 리소스 클래스에 의존하므로 이러한 리소스 클래스가 변경되면 이 저장 프로시저가 제대로 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-744">This stored proc depends on existing resource class offerings and if that changes then this stored proc wuold not work correctly.</span></span>  

>  [!NOTE]  
>  <span data-ttu-id="9ff0a-745">제공된 매개 변수로 저장 프로시저를 실행한 후에 출력이 표시되지 않으면 다음 2가지 경우로 가정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-745">If you are not getting output after executing stored procedure with parameters provided then there could be two cases.</span></span> <br /><span data-ttu-id="9ff0a-746">1. DW 매개 변수 중 하나에 잘못된 SLO 값이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-746">1. Either DW Parameter contains invalid SLO value</span></span> <br /><span data-ttu-id="9ff0a-747">2. 또는 테이블 이름이 제공된 경우 CCI 작업에 대해 일치하는 리소스 클래스가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-747">2. OR there are no matching resource class for CCI operation if table name was provided.</span></span> <br /><span data-ttu-id="9ff0a-748">예를 들어 DW100에서 사용할 수 있는 가장 높은 메모리 권한은 400MB이고 테이블 스키마가 400MB의 요구 사항을 충족할 만큼 충분히 넓습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-748">For example, at DW100, highest memory grant available is 400MB and if table schema is wide enough to cross the requirement of 400MB.</span></span>
      
#### <a name="usage-example"></a><span data-ttu-id="9ff0a-749">사용법 예제:</span><span class="sxs-lookup"><span data-stu-id="9ff0a-749">Usage example:</span></span>
<span data-ttu-id="9ff0a-750">구문</span><span class="sxs-lookup"><span data-stu-id="9ff0a-750">Syntax:</span></span>  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. <span data-ttu-id="9ff0a-751">@DWU: NULL 매개 변수를 제공하여 DW DB에서 현재 DWU를 추출하거나 지원되는 모든 DWU를 'DW100' 형식으로 제공</span><span class="sxs-lookup"><span data-stu-id="9ff0a-751">@DWU: Either provide a NULL parameter to extract the current DWU from the DW DB or provide any supported DWU in the form of 'DW100'</span></span>
2. <span data-ttu-id="9ff0a-752">@SCHEMA_NAME: 테이블의 스키마 이름 제공</span><span class="sxs-lookup"><span data-stu-id="9ff0a-752">@SCHEMA_NAME: Provide a schema name of the table</span></span>
3. <span data-ttu-id="9ff0a-753">@TABLE_NAME: 관심 있는 테이블 이름 제공</span><span class="sxs-lookup"><span data-stu-id="9ff0a-753">@TABLE_NAME: Provide a table name of the interest</span></span>

<span data-ttu-id="9ff0a-754">이 저장 프로시저 실행 예제:</span><span class="sxs-lookup"><span data-stu-id="9ff0a-754">Examples executing this stored proc:</span></span>  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

<span data-ttu-id="9ff0a-755">위의 예제에서 사용된 Table1은 아래와 같이 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-755">Table1 used in the above examples could be created as below:</span></span>  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-the-stored-procedure-definition"></a><span data-ttu-id="9ff0a-756">저장 프로시저 정의는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-756">Here's the stored procedure definition:</span></span>
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
-- Selecting proper DWU for the current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need to supply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) to hold mapping info.
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
-- Creating workload mapping to their corresponding slot consumption and default memory grant.
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

## <a name="query-importance"></a><span data-ttu-id="9ff0a-757">쿼리 중요도</span><span class="sxs-lookup"><span data-stu-id="9ff0a-757">Query importance</span></span>
<span data-ttu-id="9ff0a-758">SQL 데이터 웨어하우스는 워크로드 그룹을 사용하여 리소스 클래스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-758">SQL Data Warehouse implements resource classes by using workload groups.</span></span> <span data-ttu-id="9ff0a-759">다양한 DWU 크기의 리소스 클래스 동작을 제어하는 총 8개의 워크로드 그룹이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-759">There are a total of eight workload groups that control the behavior of the resource classes across the various DWU sizes.</span></span> <span data-ttu-id="9ff0a-760">DWU의 경우 SQL 데이터 웨어하우스는 8개의 워크로드 그룹 중 4개만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-760">For any DWU, SQL Data Warehouse uses only four of the eight workload groups.</span></span> <span data-ttu-id="9ff0a-761">각 워크로드 그룹은 4가지 리소스 클래스 smallrc, mediumrc, largerc 또는 xlargerc 중 하나에 할당되기 때문에 이렇게 하는 것이 합리적입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-761">This makes sense because each workload group is assigned to one of four resource classes: smallrc, mediumrc, largerc, or xlargerc.</span></span> <span data-ttu-id="9ff0a-762">이들 워크로드 그룹의 일부가 더 높은 *중요도*로 설정된다는 점 때문에 워크로드 그룹을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-762">The importance of understanding the workload groups is that some of these workload groups are set to higher *importance*.</span></span> <span data-ttu-id="9ff0a-763">중요도가 CPU 예약에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-763">Importance is used for CPU scheduling.</span></span> <span data-ttu-id="9ff0a-764">높은 중요도를 갖고 실행되는 쿼리는 중간 중요도의 쿼리보다 3배 더 많은 CPU 사이클을 받게 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-764">Queries run with high importance will get three times more CPU cycles than those with medium importance.</span></span> <span data-ttu-id="9ff0a-765">따라서 동시성 슬롯 매핑은 또한 CPU 우선 순위를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-765">Therefore, concurrency slot mappings also determine CPU priority.</span></span> <span data-ttu-id="9ff0a-766">쿼리가 16개 이상의 슬롯을 사용할 경우 중요도 높음으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-766">When a query consumes 16 or more slots, it runs as high importance.</span></span>

<span data-ttu-id="9ff0a-767">다음 테이블에서는 각 워크로드 그룹에 대한 중요도 매핑을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-767">The following table shows the importance mappings for each workload group.</span></span>

### <a name="workload-group-mappings-to-concurrency-slots-and-importance"></a><span data-ttu-id="9ff0a-768">동시성 슬롯 및 중요도에 대한 워크로드 그룹 매핑</span><span class="sxs-lookup"><span data-stu-id="9ff0a-768">Workload group mappings to concurrency slots and importance</span></span>
| <span data-ttu-id="9ff0a-769">워크로드 그룹</span><span class="sxs-lookup"><span data-stu-id="9ff0a-769">Workload groups</span></span> | <span data-ttu-id="9ff0a-770">동시성 슬롯 매핑</span><span class="sxs-lookup"><span data-stu-id="9ff0a-770">Concurrency slot mapping</span></span> | <span data-ttu-id="9ff0a-771">MB/배포</span><span class="sxs-lookup"><span data-stu-id="9ff0a-771">MB / Distribution</span></span> | <span data-ttu-id="9ff0a-772">중요도 매핑</span><span class="sxs-lookup"><span data-stu-id="9ff0a-772">Importance mapping</span></span> |
|:--- |:---:|:---:|:--- |
| <span data-ttu-id="9ff0a-773">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="9ff0a-773">SloDWGroupC00</span></span> |<span data-ttu-id="9ff0a-774">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-774">1</span></span> |<span data-ttu-id="9ff0a-775">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-775">100</span></span> |<span data-ttu-id="9ff0a-776">중간</span><span class="sxs-lookup"><span data-stu-id="9ff0a-776">Medium</span></span> |
| <span data-ttu-id="9ff0a-777">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="9ff0a-777">SloDWGroupC01</span></span> |<span data-ttu-id="9ff0a-778">2</span><span class="sxs-lookup"><span data-stu-id="9ff0a-778">2</span></span> |<span data-ttu-id="9ff0a-779">200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-779">200</span></span> |<span data-ttu-id="9ff0a-780">중간</span><span class="sxs-lookup"><span data-stu-id="9ff0a-780">Medium</span></span> |
| <span data-ttu-id="9ff0a-781">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="9ff0a-781">SloDWGroupC02</span></span> |<span data-ttu-id="9ff0a-782">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-782">4</span></span> |<span data-ttu-id="9ff0a-783">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-783">400</span></span> |<span data-ttu-id="9ff0a-784">중간</span><span class="sxs-lookup"><span data-stu-id="9ff0a-784">Medium</span></span> |
| <span data-ttu-id="9ff0a-785">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="9ff0a-785">SloDWGroupC03</span></span> |<span data-ttu-id="9ff0a-786">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-786">8</span></span> |<span data-ttu-id="9ff0a-787">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-787">800</span></span> |<span data-ttu-id="9ff0a-788">중간</span><span class="sxs-lookup"><span data-stu-id="9ff0a-788">Medium</span></span> |
| <span data-ttu-id="9ff0a-789">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="9ff0a-789">SloDWGroupC04</span></span> |<span data-ttu-id="9ff0a-790">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-790">16</span></span> |<span data-ttu-id="9ff0a-791">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-791">1,600</span></span> |<span data-ttu-id="9ff0a-792">높음</span><span class="sxs-lookup"><span data-stu-id="9ff0a-792">High</span></span> |
| <span data-ttu-id="9ff0a-793">SloDWGroupC05</span><span class="sxs-lookup"><span data-stu-id="9ff0a-793">SloDWGroupC05</span></span> |<span data-ttu-id="9ff0a-794">32</span><span class="sxs-lookup"><span data-stu-id="9ff0a-794">32</span></span> |<span data-ttu-id="9ff0a-795">3,200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-795">3,200</span></span> |<span data-ttu-id="9ff0a-796">높음</span><span class="sxs-lookup"><span data-stu-id="9ff0a-796">High</span></span> |
| <span data-ttu-id="9ff0a-797">SloDWGroupC06</span><span class="sxs-lookup"><span data-stu-id="9ff0a-797">SloDWGroupC06</span></span> |<span data-ttu-id="9ff0a-798">64</span><span class="sxs-lookup"><span data-stu-id="9ff0a-798">64</span></span> |<span data-ttu-id="9ff0a-799">6,400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-799">6,400</span></span> |<span data-ttu-id="9ff0a-800">높음</span><span class="sxs-lookup"><span data-stu-id="9ff0a-800">High</span></span> |
| <span data-ttu-id="9ff0a-801">SloDWGroupC07</span><span class="sxs-lookup"><span data-stu-id="9ff0a-801">SloDWGroupC07</span></span> |<span data-ttu-id="9ff0a-802">128</span><span class="sxs-lookup"><span data-stu-id="9ff0a-802">128</span></span> |<span data-ttu-id="9ff0a-803">12,800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-803">12,800</span></span> |<span data-ttu-id="9ff0a-804">높음</span><span class="sxs-lookup"><span data-stu-id="9ff0a-804">High</span></span> |

<span data-ttu-id="9ff0a-805">**동시성 슬롯의 할당 및 사용량** 차트에서는 DW500이 smallrc, mediumrc, largerc 및 xlargerc 각각에 대해 1, 4, 8 또는 16의 동시성 슬롯을 사용한다는 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-805">From the **Allocation and consumption of concurrency slots** chart, you can see that a DW500 uses 1, 4, 8 or 16 concurrency slots for smallrc, mediumrc, largerc, and xlargerc, respectively.</span></span> <span data-ttu-id="9ff0a-806">위의 차트에서 이러한 값을 확인하여 각 리소스 클래스에 대한 중요도를 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-806">You can look those values up in the preceding chart to find the importance for each resource class.</span></span>

### <a name="dw500-mapping-of-resource-classes-to-importance"></a><span data-ttu-id="9ff0a-807">DW500의 리소스 클래스와 중요도 관계</span><span class="sxs-lookup"><span data-stu-id="9ff0a-807">DW500 mapping of resource classes to importance</span></span>
| <span data-ttu-id="9ff0a-808">리소스 클래스</span><span class="sxs-lookup"><span data-stu-id="9ff0a-808">Resource class</span></span> | <span data-ttu-id="9ff0a-809">워크로드 그룹</span><span class="sxs-lookup"><span data-stu-id="9ff0a-809">Workload group</span></span> | <span data-ttu-id="9ff0a-810">사용된 동시성 슬롯 수</span><span class="sxs-lookup"><span data-stu-id="9ff0a-810">Concurrency slots used</span></span> | <span data-ttu-id="9ff0a-811">MB/배포</span><span class="sxs-lookup"><span data-stu-id="9ff0a-811">MB / Distribution</span></span> | <span data-ttu-id="9ff0a-812">중요도</span><span class="sxs-lookup"><span data-stu-id="9ff0a-812">Importance</span></span> |
|:--- |:--- |:---:|:---:|:--- |
| <span data-ttu-id="9ff0a-813">smallrc</span><span class="sxs-lookup"><span data-stu-id="9ff0a-813">smallrc</span></span> |<span data-ttu-id="9ff0a-814">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="9ff0a-814">SloDWGroupC00</span></span> |<span data-ttu-id="9ff0a-815">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-815">1</span></span> |<span data-ttu-id="9ff0a-816">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-816">100</span></span> |<span data-ttu-id="9ff0a-817">중간</span><span class="sxs-lookup"><span data-stu-id="9ff0a-817">Medium</span></span> |
| <span data-ttu-id="9ff0a-818">mediumrc</span><span class="sxs-lookup"><span data-stu-id="9ff0a-818">mediumrc</span></span> |<span data-ttu-id="9ff0a-819">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="9ff0a-819">SloDWGroupC02</span></span> |<span data-ttu-id="9ff0a-820">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-820">4</span></span> |<span data-ttu-id="9ff0a-821">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-821">400</span></span> |<span data-ttu-id="9ff0a-822">중간</span><span class="sxs-lookup"><span data-stu-id="9ff0a-822">Medium</span></span> |
| <span data-ttu-id="9ff0a-823">largerc</span><span class="sxs-lookup"><span data-stu-id="9ff0a-823">largerc</span></span> |<span data-ttu-id="9ff0a-824">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="9ff0a-824">SloDWGroupC03</span></span> |<span data-ttu-id="9ff0a-825">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-825">8</span></span> |<span data-ttu-id="9ff0a-826">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-826">800</span></span> |<span data-ttu-id="9ff0a-827">중간</span><span class="sxs-lookup"><span data-stu-id="9ff0a-827">Medium</span></span> |
| <span data-ttu-id="9ff0a-828">xlargerc</span><span class="sxs-lookup"><span data-stu-id="9ff0a-828">xlargerc</span></span> |<span data-ttu-id="9ff0a-829">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="9ff0a-829">SloDWGroupC04</span></span> |<span data-ttu-id="9ff0a-830">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-830">16</span></span> |<span data-ttu-id="9ff0a-831">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-831">1,600</span></span> |<span data-ttu-id="9ff0a-832">높음</span><span class="sxs-lookup"><span data-stu-id="9ff0a-832">High</span></span> |
| <span data-ttu-id="9ff0a-833">staticrc10</span><span class="sxs-lookup"><span data-stu-id="9ff0a-833">staticrc10</span></span> |<span data-ttu-id="9ff0a-834">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="9ff0a-834">SloDWGroupC00</span></span> |<span data-ttu-id="9ff0a-835">1</span><span class="sxs-lookup"><span data-stu-id="9ff0a-835">1</span></span> |<span data-ttu-id="9ff0a-836">100</span><span class="sxs-lookup"><span data-stu-id="9ff0a-836">100</span></span> |<span data-ttu-id="9ff0a-837">중간</span><span class="sxs-lookup"><span data-stu-id="9ff0a-837">Medium</span></span> |
| <span data-ttu-id="9ff0a-838">staticrc20</span><span class="sxs-lookup"><span data-stu-id="9ff0a-838">staticrc20</span></span> |<span data-ttu-id="9ff0a-839">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="9ff0a-839">SloDWGroupC01</span></span> |<span data-ttu-id="9ff0a-840">2</span><span class="sxs-lookup"><span data-stu-id="9ff0a-840">2</span></span> |<span data-ttu-id="9ff0a-841">200</span><span class="sxs-lookup"><span data-stu-id="9ff0a-841">200</span></span> |<span data-ttu-id="9ff0a-842">중간</span><span class="sxs-lookup"><span data-stu-id="9ff0a-842">Medium</span></span> |
| <span data-ttu-id="9ff0a-843">staticrc30</span><span class="sxs-lookup"><span data-stu-id="9ff0a-843">staticrc30</span></span> |<span data-ttu-id="9ff0a-844">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="9ff0a-844">SloDWGroupC02</span></span> |<span data-ttu-id="9ff0a-845">4</span><span class="sxs-lookup"><span data-stu-id="9ff0a-845">4</span></span> |<span data-ttu-id="9ff0a-846">400</span><span class="sxs-lookup"><span data-stu-id="9ff0a-846">400</span></span> |<span data-ttu-id="9ff0a-847">중간</span><span class="sxs-lookup"><span data-stu-id="9ff0a-847">Medium</span></span> |
| <span data-ttu-id="9ff0a-848">staticrc40</span><span class="sxs-lookup"><span data-stu-id="9ff0a-848">staticrc40</span></span> |<span data-ttu-id="9ff0a-849">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="9ff0a-849">SloDWGroupC03</span></span> |<span data-ttu-id="9ff0a-850">8</span><span class="sxs-lookup"><span data-stu-id="9ff0a-850">8</span></span> |<span data-ttu-id="9ff0a-851">800</span><span class="sxs-lookup"><span data-stu-id="9ff0a-851">800</span></span> |<span data-ttu-id="9ff0a-852">중간</span><span class="sxs-lookup"><span data-stu-id="9ff0a-852">Medium</span></span> |
| <span data-ttu-id="9ff0a-853">staticrc50</span><span class="sxs-lookup"><span data-stu-id="9ff0a-853">staticrc50</span></span> |<span data-ttu-id="9ff0a-854">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="9ff0a-854">SloDWGroupC03</span></span> |<span data-ttu-id="9ff0a-855">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-855">16</span></span> |<span data-ttu-id="9ff0a-856">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-856">1,600</span></span> |<span data-ttu-id="9ff0a-857">높음</span><span class="sxs-lookup"><span data-stu-id="9ff0a-857">High</span></span> |
| <span data-ttu-id="9ff0a-858">staticrc60</span><span class="sxs-lookup"><span data-stu-id="9ff0a-858">staticrc60</span></span> |<span data-ttu-id="9ff0a-859">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="9ff0a-859">SloDWGroupC03</span></span> |<span data-ttu-id="9ff0a-860">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-860">16</span></span> |<span data-ttu-id="9ff0a-861">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-861">1,600</span></span> |<span data-ttu-id="9ff0a-862">높음</span><span class="sxs-lookup"><span data-stu-id="9ff0a-862">High</span></span> |
| <span data-ttu-id="9ff0a-863">staticrc70</span><span class="sxs-lookup"><span data-stu-id="9ff0a-863">staticrc70</span></span> |<span data-ttu-id="9ff0a-864">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="9ff0a-864">SloDWGroupC03</span></span> |<span data-ttu-id="9ff0a-865">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-865">16</span></span> |<span data-ttu-id="9ff0a-866">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-866">1,600</span></span> |<span data-ttu-id="9ff0a-867">높음</span><span class="sxs-lookup"><span data-stu-id="9ff0a-867">High</span></span> |
| <span data-ttu-id="9ff0a-868">staticrc80</span><span class="sxs-lookup"><span data-stu-id="9ff0a-868">staticrc80</span></span> |<span data-ttu-id="9ff0a-869">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="9ff0a-869">SloDWGroupC03</span></span> |<span data-ttu-id="9ff0a-870">16</span><span class="sxs-lookup"><span data-stu-id="9ff0a-870">16</span></span> |<span data-ttu-id="9ff0a-871">1,600</span><span class="sxs-lookup"><span data-stu-id="9ff0a-871">1,600</span></span> |<span data-ttu-id="9ff0a-872">높음</span><span class="sxs-lookup"><span data-stu-id="9ff0a-872">High</span></span> |

<span data-ttu-id="9ff0a-873">다음 DMV 쿼리는 리소스 관리자의 관점에서 메모리 리소스 할당의 차이점을 자세히 살펴보거나, 또는 문제를 해결할 때 워크로드 그룹의 활성 및 사용 기록을 분석하는 데도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-873">You can use the following DMV query to look at the differences in memory resource allocation in detail from the perspective of the resource governor, or to analyze active and historic usage of the workload groups when troubleshooting.</span></span>

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

## <a name="queries-that-honor-concurrency-limits"></a><span data-ttu-id="9ff0a-874">동시성 한도를 적용하는 쿼리</span><span class="sxs-lookup"><span data-stu-id="9ff0a-874">Queries that honor concurrency limits</span></span>
<span data-ttu-id="9ff0a-875">대부분의 쿼리는 리소스 클래스에 의해 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-875">Most queries are governed by resource classes.</span></span> <span data-ttu-id="9ff0a-876">이러한 쿼리는 동시 쿼리 및 동시성 슬롯 임계값 둘 다를 벗어나지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-876">These queries must fit inside both the concurrent query and concurrency slot thresholds.</span></span> <span data-ttu-id="9ff0a-877">사용자는 동시성 슬롯 모델에서 쿼리를 제외하도록 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-877">A user cannot choose to exclude a query from the concurrency slot model.</span></span>

<span data-ttu-id="9ff0a-878">다시 한 번 강조하지만 다음 문은 리소스 클래스를 인식합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-878">To reiterate, the following statements honor resource classes:</span></span>

* <span data-ttu-id="9ff0a-879">INSERT-SELECT</span><span class="sxs-lookup"><span data-stu-id="9ff0a-879">INSERT-SELECT</span></span>
* <span data-ttu-id="9ff0a-880">UPDATE</span><span class="sxs-lookup"><span data-stu-id="9ff0a-880">UPDATE</span></span>
* <span data-ttu-id="9ff0a-881">삭제</span><span class="sxs-lookup"><span data-stu-id="9ff0a-881">DELETE</span></span>
* <span data-ttu-id="9ff0a-882">SELECT(사용자 테이블을 쿼리하는 경우)</span><span class="sxs-lookup"><span data-stu-id="9ff0a-882">SELECT (when querying user tables)</span></span>
* <span data-ttu-id="9ff0a-883">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="9ff0a-883">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="9ff0a-884">ALTER INDEX REORGANIZE</span><span class="sxs-lookup"><span data-stu-id="9ff0a-884">ALTER INDEX REORGANIZE</span></span>
* <span data-ttu-id="9ff0a-885">ALTER TABLE REBUILD</span><span class="sxs-lookup"><span data-stu-id="9ff0a-885">ALTER TABLE REBUILD</span></span>
* <span data-ttu-id="9ff0a-886">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="9ff0a-886">CREATE INDEX</span></span>
* <span data-ttu-id="9ff0a-887">CREATE CLUSTERED COLUMNSTORE INDEX</span><span class="sxs-lookup"><span data-stu-id="9ff0a-887">CREATE CLUSTERED COLUMNSTORE INDEX</span></span>
* <span data-ttu-id="9ff0a-888">CREATE TABLE AS SELECT (CTAS)</span><span class="sxs-lookup"><span data-stu-id="9ff0a-888">CREATE TABLE AS SELECT (CTAS)</span></span>
* <span data-ttu-id="9ff0a-889">데이터 로드</span><span class="sxs-lookup"><span data-stu-id="9ff0a-889">Data loading</span></span>
* <span data-ttu-id="9ff0a-890">DMS(데이터 이동 서비스)에서 수행하는 데이터 이동 작업</span><span class="sxs-lookup"><span data-stu-id="9ff0a-890">Data movement operations conducted by the Data Movement Service (DMS)</span></span>

## <a name="query-exceptions-to-concurrency-limits"></a><span data-ttu-id="9ff0a-891">동시성 제한에 대한 쿼리 예외</span><span class="sxs-lookup"><span data-stu-id="9ff0a-891">Query exceptions to concurrency limits</span></span>
<span data-ttu-id="9ff0a-892">일부 쿼리는 사용자가 할당된 리소스 클래스를 인식하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-892">Some queries do not honor the resource class to which the user is assigned.</span></span> <span data-ttu-id="9ff0a-893">동시성 제한에 대한 이러한 예외는 특정 명령에 필요한 메모리 리소스가 부족할 때(종종 명령이 메타데이터 작업이므로) 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-893">These exceptions to the concurrency limits are made when the memory resources needed for a particular command are low, often because the command is a metadata operation.</span></span> <span data-ttu-id="9ff0a-894">이러한 예외는 필요하지 않은 더 큰 양의 메모리가 쿼리에 할당되는 것을 방지하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-894">The goal of these exceptions is to avoid larger memory allocations for queries that will never need them.</span></span> <span data-ttu-id="9ff0a-895">이러한 경우에는 사용자에게 할당된 실제 리소스 클래스와 상관없이 기본 또는 작은 리소스 클래스(smallrc)가 항상 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-895">In these cases, the default small resource class (smallrc) is always used regardless of the actual resource class assigned to the user.</span></span> <span data-ttu-id="9ff0a-896">예를 들어, `CREATE LOGIN` 은 항상 smallrc에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-896">For example, `CREATE LOGIN` will always run in smallrc.</span></span> <span data-ttu-id="9ff0a-897">이 작업을 수행하는 데 필요한 리소스가 매우 부족하고 따라서 동시성 슬롯 모델에 쿼리를 포함하는 것이 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-897">The resources required to fulfill this operation are very low, so it does not make sense to include the query in the concurrency slot model.</span></span>  <span data-ttu-id="9ff0a-898">이러한 쿼리는 또한 32명의 사용자 동시성 제한으로 제한되지 않으며, 이러한 쿼리를 개수 제한 없이 1,024개의 세션 제한까지 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-898">These queries are also not limited by the 32 user concurrency limit, an unlimited number of these queries can run up to the session limit of 1,024 sessions.</span></span>

<span data-ttu-id="9ff0a-899">다음 문은 리소스 클래스를 인식하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-899">The following statements do not honor resource classes:</span></span>

* <span data-ttu-id="9ff0a-900">CREATE 또는 DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="9ff0a-900">CREATE or DROP TABLE</span></span>
* <span data-ttu-id="9ff0a-901">ALTER TABLE ... SWITCH, SPLIT 또는 MERGE PARTITION</span><span class="sxs-lookup"><span data-stu-id="9ff0a-901">ALTER TABLE ... SWITCH, SPLIT, or MERGE PARTITION</span></span>
* <span data-ttu-id="9ff0a-902">ALTER INDEX DISABLE</span><span class="sxs-lookup"><span data-stu-id="9ff0a-902">ALTER INDEX DISABLE</span></span>
* <span data-ttu-id="9ff0a-903">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="9ff0a-903">DROP INDEX</span></span>
* <span data-ttu-id="9ff0a-904">CREATE, UPDATE 또는 DROP STATISTICS</span><span class="sxs-lookup"><span data-stu-id="9ff0a-904">CREATE, UPDATE, or DROP STATISTICS</span></span>
* <span data-ttu-id="9ff0a-905">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="9ff0a-905">TRUNCATE TABLE</span></span>
* <span data-ttu-id="9ff0a-906">ALTER AUTHORIZATION</span><span class="sxs-lookup"><span data-stu-id="9ff0a-906">ALTER AUTHORIZATION</span></span>
* <span data-ttu-id="9ff0a-907">CREATE LOGIN</span><span class="sxs-lookup"><span data-stu-id="9ff0a-907">CREATE LOGIN</span></span>
* <span data-ttu-id="9ff0a-908">CREATE, ALTER 또는 DROP USER</span><span class="sxs-lookup"><span data-stu-id="9ff0a-908">CREATE, ALTER or DROP USER</span></span>
* <span data-ttu-id="9ff0a-909">CREATE, ALTER 또는 DROP PROCEDURE</span><span class="sxs-lookup"><span data-stu-id="9ff0a-909">CREATE, ALTER or DROP PROCEDURE</span></span>
* <span data-ttu-id="9ff0a-910">CREATE 또는 DROP VIEW</span><span class="sxs-lookup"><span data-stu-id="9ff0a-910">CREATE or DROP VIEW</span></span>
* <span data-ttu-id="9ff0a-911">INSERT VALUES</span><span class="sxs-lookup"><span data-stu-id="9ff0a-911">INSERT VALUES</span></span>
* <span data-ttu-id="9ff0a-912">SELECT(시스템 뷰와 DMV에서)</span><span class="sxs-lookup"><span data-stu-id="9ff0a-912">SELECT from system views and DMVs</span></span>
* <span data-ttu-id="9ff0a-913">EXPLAIN</span><span class="sxs-lookup"><span data-stu-id="9ff0a-913">EXPLAIN</span></span>
* <span data-ttu-id="9ff0a-914">DBCC</span><span class="sxs-lookup"><span data-stu-id="9ff0a-914">DBCC</span></span>

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <span data-ttu-id="9ff0a-915"><a name="changing-user-resource-class-example"></a> 사용자 리소스 클래스 변경 예제</span><span class="sxs-lookup"><span data-stu-id="9ff0a-915"><a name="changing-user-resource-class-example"></a> Change a user resource class example</span></span>
1. <span data-ttu-id="9ff0a-916">**로그인 만들기:** SQL Data Warehouse 데이터베이스를 호스트하는 SQL Server에서 **마스터** 데이터베이스에 대한 연결을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-916">**Create login:** Open a connection to your **master** database on the SQL server hosting your SQL Data Warehouse database and execute the following commands.</span></span>
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > <span data-ttu-id="9ff0a-917">Azure SQL Data Warehouse 사용자에 대해 마스터 데이터베이스에 사용자를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-917">It is a good idea to create a user in the master database for Azure SQL Data Warehouse users.</span></span> <span data-ttu-id="9ff0a-918">마스터에서 사용자를 만들면 데이터베이스 이름을 지정하지 않아도 사용자가 SSMS 등의 도구를 사용하여 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-918">Creating a user in master allows a user to login using tools like SSMS without specifying a database name.</span></span>  <span data-ttu-id="9ff0a-919">또한 개체 탐색기를 사용하여 SQL server의 모든 데이터베이스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-919">It also allows them to use the object explorer to view all databases on a SQL server.</span></span>  <span data-ttu-id="9ff0a-920">사용자를 만들고 관리하는 방법에 대한 자세한 내용은 [SQL Data Warehouse에서 데이터베이스 보호][Secure a database in SQL Data Warehouse]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-920">For more details about creating and managing users, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>
   > 
   > 
2. <span data-ttu-id="9ff0a-921">**SQL Data Warehouse 사용자 만들기:** **SQL Data Warehouse** 데이터베이스에 대한 연결을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-921">**Create SQL Data Warehouse user:** Open a connection to the **SQL Data Warehouse** database and execute the following command.</span></span>
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. <span data-ttu-id="9ff0a-922">**사용 권한 부여:** 다음 예제에서는 **SQL Data Warehouse** 데이터베이스에 `CONTROL`을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-922">**Grant permissions:** The following example grants `CONTROL` on the **SQL Data Warehouse** database.</span></span> <span data-ttu-id="9ff0a-923">데이터베이스 수준에서 `CONTROL`은 SQL Server의 db_owner와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-923">`CONTROL` at the database level is the equivalent of db_owner in SQL Server.</span></span>
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW to newperson;
    ```
4. <span data-ttu-id="9ff0a-924">**리소스 클래스 증가:** 다음 쿼리를 사용하여 더 높은 워크로드 관리 역할에 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-924">**Increase resource class:** Use the following query to add a user to a higher workload management role.</span></span>
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. <span data-ttu-id="9ff0a-925">**리소스 클래스 감소:** 다음 쿼리를 사용하여 워크로드 관리 역할에서 사용자를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-925">**Decrease resource class:** Use the following query to remove a user from a workload management role.</span></span>
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="9ff0a-926">smallrc에서 사용자를 제거하는 것은 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-926">It is not possible to remove a user from smallrc.</span></span>
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a><span data-ttu-id="9ff0a-927">큐에 대기 중인 쿼리 검색 및 다른 DMV</span><span class="sxs-lookup"><span data-stu-id="9ff0a-927">Queued query detection and other DMVs</span></span>
<span data-ttu-id="9ff0a-928">`sys.dm_pdw_exec_requests` DMV는 동시성 큐에 대기 중인 쿼리를 식별하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-928">You can use the `sys.dm_pdw_exec_requests` DMV to identify queries that are waiting in a concurrency queue.</span></span> <span data-ttu-id="9ff0a-929">동시성 슬롯을 대기하는 쿼리는 **일시 중단**상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-929">Queries waiting for a concurrency slot will have a status of **suspended**.</span></span>

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

<span data-ttu-id="9ff0a-930">워크로드 관리 역할은 `sys.database_principals`를 사용하여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-930">Workload management roles can be viewed with `sys.database_principals`.</span></span>

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

<span data-ttu-id="9ff0a-931">다음 쿼리는 각 사용자에게 어떤 역할이 할당되었는지 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-931">The following query shows which role each user is assigned to.</span></span>

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

<span data-ttu-id="9ff0a-932">SQL 데이터 웨어하우스에 다음과 같은 대기 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-932">SQL Data Warehouse has the following wait types:</span></span>

* <span data-ttu-id="9ff0a-933">**LocalQueriesConcurrencyResourceType**: 동시성 슬롯 프레임워크 외부에 존재하는 쿼리.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-933">**LocalQueriesConcurrencyResourceType**: Queries that sit outside of the concurrency slot framework.</span></span> <span data-ttu-id="9ff0a-934">`SELECT @@VERSION` 과 같은 DMV 쿼리 및 시스템 함수는 로컬 쿼리의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-934">DMV queries and system functions such as `SELECT @@VERSION` are examples of local queries.</span></span>
* <span data-ttu-id="9ff0a-935">**UserConcurrencyResourceType**: 동시성 슬롯 프레임워크 내에 존재하는 쿼리.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-935">**UserConcurrencyResourceType**: Queries that sit inside the concurrency slot framework.</span></span> <span data-ttu-id="9ff0a-936">최종 사용자 테이블에 대한 쿼리는 이 리소스 형식을 사용하는 예를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-936">Queries against end-user tables represent examples that would use this resource type.</span></span>
* <span data-ttu-id="9ff0a-937">**DmsConcurrencyResourceType**: 데이터 이동 작업으로 초래된 대기</span><span class="sxs-lookup"><span data-stu-id="9ff0a-937">**DmsConcurrencyResourceType**: Waits resulting from data movement operations.</span></span>
* <span data-ttu-id="9ff0a-938">**BackupConcurrencyResourceType**: 이 대기는 데이터베이스가 백업 중임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-938">**BackupConcurrencyResourceType**: This wait indicates that a database is being backed up.</span></span> <span data-ttu-id="9ff0a-939">이 리소스 유형에 대한 최대값은 1입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-939">The maximum value for this resource type is 1.</span></span> <span data-ttu-id="9ff0a-940">여러 백업을 동시에 요청한 경우 다른 백업 요청은 큐에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-940">If multiple backups have been requested at the same time, the others will queue.</span></span>

<span data-ttu-id="9ff0a-941">`sys.dm_pdw_waits` DMV는 요청이 대기 중인 리소스를 알아내는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-941">The `sys.dm_pdw_waits` DMV can be used to see which resources a request is waiting for.</span></span>

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

<span data-ttu-id="9ff0a-942">`sys.dm_pdw_resource_waits` DMV는 지정된 쿼리에 사용되는 리소스 대기만 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-942">The `sys.dm_pdw_resource_waits` DMV shows only the resource waits consumed by a given query.</span></span> <span data-ttu-id="9ff0a-943">리소스 대기 시간은 기본 SQL Server가 CPU에 대해 쿼리를 예약하는 데 소요되는 대기 시간을 나타내는 것과 달리 리소스가 제공될 때까지 대기하는 시간만 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-943">Resource wait time only measures the time waiting for resources to be provided, as opposed to signal wait time, which is the time it takes for the underlying SQL servers to schedule the query onto the CPU.</span></span>

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

<span data-ttu-id="9ff0a-944">`sys.dm_pdw_wait_stats` DMV는 기록 추세 분석에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-944">The `sys.dm_pdw_wait_stats` DMV can be used for historic trend analysis of waits.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9ff0a-945">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9ff0a-945">Next steps</span></span>
<span data-ttu-id="9ff0a-946">데이터베이스 사용자 및 보안을 관리하는 방법에 대한 자세한 내용은 [SQL Data Warehouse에서 데이터베이스 보호][Secure a database in SQL Data Warehouse]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-946">For more information about managing database users and security, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span> <span data-ttu-id="9ff0a-947">더 큰 리소스 클래스가 클러스터된 columnstore 인덱스 품질을 향상할 방법에 대한 자세한 내용은 [인덱스를 다시 빌드하여 세그먼트 품질 개선]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ff0a-947">For more information about how larger resource classes can improve clustered columnstore index quality, see [Rebuilding indexes to improve segment quality].</span></span>

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[인덱스를 다시 빌드하여 세그먼트 품질 개선]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->

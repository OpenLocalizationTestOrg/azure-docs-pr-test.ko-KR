---
title: "Azure SQL 데이터베이스에서 쿼리 저장소 운영"
description: "Azure SQL 데이터베이스에서 쿼리 저장소를 운영하는 방법 알아보기"
keywords: 
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: 0cccf6bd-1327-44f7-a6f9-8eff0c210463
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: sqldb-performance
ms.workload: data-management
ms.date: 11/08/2016
ms.author: bonova
ms.openlocfilehash: 4e13f265c32037abdba67a68ca5be81e167c01e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="operating-the-query-store-in-azure-sql-database"></a><span data-ttu-id="f6f08-103">Azure SQL 데이터베이스에서 쿼리 저장소 운영</span><span class="sxs-lookup"><span data-stu-id="f6f08-103">Operating the Query Store in Azure SQL Database</span></span>
<span data-ttu-id="f6f08-104">Azure의 쿼리 저장소는 모든 쿼리에 대한 자세한 기록 정보를 지속적으로 수집하고 제공하는, 완전히 관리되는 데이터베이스 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f6f08-104">Query Store in Azure is a fully managed database feature that continuously collects and presents detailed historic information about all queries.</span></span> <span data-ttu-id="f6f08-105">쿼리 저장소는 비행기의 블랙박스와 비슷하게 생각할 수 있으며, 클라우드와 온-프레미스 고객의 쿼리 성능 문제 해결을 상당히 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f08-105">You can think about Query Store as similar to an airplane's flight data recorder that significantly simplifies query performance troubleshooting both for cloud and on-premises customers.</span></span> <span data-ttu-id="f6f08-106">이 문서는 Azure의 쿼리 저장소 운영에 대한 구체적인 측면을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f08-106">This article explains specific aspects of operating Query Store in Azure.</span></span> <span data-ttu-id="f6f08-107">미리 수집된 쿼리 데이터를 사용하면, 성능 문제를 신속하게 진단하고 해결할 수 있기 때문에 업무에 더 많은 시간을 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f08-107">Using this pre-collected query data, you can quickly diagnose and resolve performance problems and thus spend more time focusing on their business.</span></span> 

<span data-ttu-id="f6f08-108">쿼리 저장소는 2015년 11월부터 Azure SQL 데이터베이스에서 [전세계적으로 사용할 수 있습니다](https://azure.microsoft.com/updates/general-availability-azure-sql-database-query-store/) .</span><span class="sxs-lookup"><span data-stu-id="f6f08-108">Query Store has been [globally available](https://azure.microsoft.com/updates/general-availability-azure-sql-database-query-store/) in Azure SQL Database since November, 2015.</span></span> <span data-ttu-id="f6f08-109">쿼리 저장소는 [SQL 데이터베이스 관리자 및 성능 대시보드](https://azure.microsoft.com/updates/sqldatabaseadvisorga/)같은 성능 분석 및 기능 조정을 위한 기반입니다.</span><span class="sxs-lookup"><span data-stu-id="f6f08-109">Query Store is the foundation for performance analysis and tuning features, such as [SQL Database Advisor and Performance Dashboard](https://azure.microsoft.com/updates/sqldatabaseadvisorga/).</span></span> <span data-ttu-id="f6f08-110">이 문서를 게시하는 순간에도, 200,000개가 넘는 Azure의 사용자 데이터베이스에서 쿼리 저장소가 실행 중이며, 쿼리 관련 정보를 몇 달 동안 중단 없이 수집하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f08-110">At the moment of publishing this article, Query Store is running in more than 200,000 user databases in Azure, collecting query-related information for several months, without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6f08-111">Microsoft는 모든 Azure SQL 데이터베이스(기존 및 신규)에 대해 쿼리 저장소를 활성화하는 과정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f08-111">Microsoft is in the process of activating Query Store for all Azure SQL databases (existing and new).</span></span> 
> 
> 

## <a name="optimal-query-store-configuration"></a><span data-ttu-id="f6f08-112">최적인 쿼리 저장소 구성</span><span class="sxs-lookup"><span data-stu-id="f6f08-112">Optimal Query Store Configuration</span></span>
<span data-ttu-id="f6f08-113">이 섹션은 쿼리 저장소는 물론 [SQL 데이터베이스 관리자 및 성능 대시보드](https://azure.microsoft.com/updates/sqldatabaseadvisorga/)등과 같은 종속적인 기능의 안정적인 운영을 보장하기 위해 설계된 최적의 구성 기본값을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f08-113">This section describes optimal configuration defaults that are designed to ensure reliable operation of the Query Store and dependent features, such as [SQL Database Advisor and Performance Dashboard](https://azure.microsoft.com/updates/sqldatabaseadvisorga/).</span></span> <span data-ttu-id="f6f08-114">기본 구성은 지속적인 데이터 수집을 위해 최적화됩니다(예: OFF/READ_ONLY 상태에 소요되는 시간 최소화).</span><span class="sxs-lookup"><span data-stu-id="f6f08-114">Default configuration is optimized for continuous data collection, that is minimal time spent in OFF/READ_ONLY states.</span></span>

| <span data-ttu-id="f6f08-115">구성</span><span class="sxs-lookup"><span data-stu-id="f6f08-115">Configuration</span></span> | <span data-ttu-id="f6f08-116">설명</span><span class="sxs-lookup"><span data-stu-id="f6f08-116">Description</span></span> | <span data-ttu-id="f6f08-117">기본값</span><span class="sxs-lookup"><span data-stu-id="f6f08-117">Default</span></span> | <span data-ttu-id="f6f08-118">주석</span><span class="sxs-lookup"><span data-stu-id="f6f08-118">Comment</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f6f08-119">MAX_STORAGE_SIZE_MB</span><span class="sxs-lookup"><span data-stu-id="f6f08-119">MAX_STORAGE_SIZE_MB</span></span> |<span data-ttu-id="f6f08-120">쿼리 저장소가 사용자 데이터베이스 내부에서 사용하는 데이터 공간에 대한 제한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f08-120">Specifies the limit for the data space that Query Store can take inside z customer database</span></span> |<span data-ttu-id="f6f08-121">100</span><span class="sxs-lookup"><span data-stu-id="f6f08-121">100</span></span> |<span data-ttu-id="f6f08-122">새 데이터베이스에 적용</span><span class="sxs-lookup"><span data-stu-id="f6f08-122">Enforced for new databases</span></span> |
| <span data-ttu-id="f6f08-123">INTERVAL_LENGTH_MINUTES</span><span class="sxs-lookup"><span data-stu-id="f6f08-123">INTERVAL_LENGTH_MINUTES</span></span> |<span data-ttu-id="f6f08-124">쿼리 계획에 대해 수집된 런타임 통계가 집계되고 지속되는 기간의 규모를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f08-124">Defines size of time window during which collected runtime statistics for query plans are aggregated and persisted.</span></span> <span data-ttu-id="f6f08-125">모든 활성 쿼리 계획은 이 구성을 통해 정의된 기간에 대해 최대 하나의 행을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f08-125">Every active query plan has at most one row for a period of time defined with this configuration</span></span> |<span data-ttu-id="f6f08-126">60</span><span class="sxs-lookup"><span data-stu-id="f6f08-126">60</span></span> |<span data-ttu-id="f6f08-127">새 데이터베이스에 적용</span><span class="sxs-lookup"><span data-stu-id="f6f08-127">Enforced for new databases</span></span> |
| <span data-ttu-id="f6f08-128">STALE_QUERY_THRESHOLD_DAYS</span><span class="sxs-lookup"><span data-stu-id="f6f08-128">STALE_QUERY_THRESHOLD_DAYS</span></span> |<span data-ttu-id="f6f08-129">지속되는 런타임 통계 및 비활성 쿼리의 보존 기간을 제어하는 시간 기반 정리 정책</span><span class="sxs-lookup"><span data-stu-id="f6f08-129">Time-based cleanup policy that controls the retention period of persisted runtime statistics and inactive queries</span></span> |<span data-ttu-id="f6f08-130">30</span><span class="sxs-lookup"><span data-stu-id="f6f08-130">30</span></span> |<span data-ttu-id="f6f08-131">새 데이터베이스 및 이전 기본값을 포함하는 데이터베이스에 적용(367)</span><span class="sxs-lookup"><span data-stu-id="f6f08-131">Enforced for new databases and databases with previous default (367)</span></span> |
| <span data-ttu-id="f6f08-132">SIZE_BASED_CLEANUP_MODE</span><span class="sxs-lookup"><span data-stu-id="f6f08-132">SIZE_BASED_CLEANUP_MODE</span></span> |<span data-ttu-id="f6f08-133">쿼리 저장소 데이터 크기가 한도에 접근할 때, 자동 데이터 정리를 수행할지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f08-133">Specifies whether automatic data cleanup takes place when Query Store data size approaches the limit</span></span> |<span data-ttu-id="f6f08-134">AUTO</span><span class="sxs-lookup"><span data-stu-id="f6f08-134">AUTO</span></span> |<span data-ttu-id="f6f08-135">모든 데이터베이스에 적용</span><span class="sxs-lookup"><span data-stu-id="f6f08-135">Enforced for all databases</span></span> |
| <span data-ttu-id="f6f08-136">QUERY_CAPTURE_MODE</span><span class="sxs-lookup"><span data-stu-id="f6f08-136">QUERY_CAPTURE_MODE</span></span> |<span data-ttu-id="f6f08-137">모든 쿼리를 추적할지 또는 쿼리의 하위 집합만 추적할지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f08-137">Specifies whether all queries or only a subset of queries are tracked</span></span> |<span data-ttu-id="f6f08-138">AUTO</span><span class="sxs-lookup"><span data-stu-id="f6f08-138">AUTO</span></span> |<span data-ttu-id="f6f08-139">모든 데이터베이스에 적용</span><span class="sxs-lookup"><span data-stu-id="f6f08-139">Enforced for all databases</span></span> |
| <span data-ttu-id="f6f08-140">FLUSH_INTERVAL_SECONDS</span><span class="sxs-lookup"><span data-stu-id="f6f08-140">FLUSH_INTERVAL_SECONDS</span></span> |<span data-ttu-id="f6f08-141">캡처한 런타임 통계를 디스크에 플러시하기 전에 메모리에 유지하는 최대 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f08-141">Specifies maximum period during which captured runtime statistics are kept in memory, before flushing to disk</span></span> |<span data-ttu-id="f6f08-142">900</span><span class="sxs-lookup"><span data-stu-id="f6f08-142">900</span></span> |<span data-ttu-id="f6f08-143">새 데이터베이스에 적용</span><span class="sxs-lookup"><span data-stu-id="f6f08-143">Enforced for new databases</span></span> |
|  | | | |

> [!IMPORTANT]
> <span data-ttu-id="f6f08-144">이러한 기본값은 모든 Azure SQL 데이터베이스의 쿼리 저장소 활성화 마지막 단계에서 자동으로 적용됩니다(위의 중요 항목 참조).</span><span class="sxs-lookup"><span data-stu-id="f6f08-144">These defaults are automatically applied in the final stage of Query Store activation in all Azure SQL databases (see preceding important note).</span></span> <span data-ttu-id="f6f08-145">이후로, Azure SQL 데이터베이스는 고객이 설정한 구성 값이 기본 워크로드 또는 쿼리 저장소의 안정적인 운영에 부정적인 영향을 미치지 않는 한 고객이 설정한 구성 값을 변경하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f08-145">After this light up, Azure SQL Database won’t be changing configuration values set by customers, unless they negatively impact primary workload or reliable operations of the Query Store.</span></span>
> 
> 

<span data-ttu-id="f6f08-146">사용자 지정 설정을 유지하려는 경우에는, [쿼리 저장소 옵션을 사용하여 ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) 를 사용하여 이전 상태로 구성을 되돌립니다.</span><span class="sxs-lookup"><span data-stu-id="f6f08-146">If you want to stay with your custom settings, use [ALTER DATABASE with Query Store options](https://msdn.microsoft.com/library/bb522682.aspx) to revert configuration to the previous state.</span></span> <span data-ttu-id="f6f08-147">최적의 구성 매개 변수를 선택하는 방법을 알아보려면, [쿼리 저장소 모범 사례](https://msdn.microsoft.com/library/mt604821.aspx) 를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f6f08-147">Check out [Best Practices with the Query Store](https://msdn.microsoft.com/library/mt604821.aspx) in order to learn how top chose optimal configuration parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6f08-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f6f08-148">Next steps</span></span>
[<span data-ttu-id="f6f08-149">SQL 데이터베이스 성능 Insight</span><span class="sxs-lookup"><span data-stu-id="f6f08-149">SQL Database Performance Insight</span></span>](sql-database-performance.md)

## <a name="additional-resources"></a><span data-ttu-id="f6f08-150">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f6f08-150">Additional resources</span></span>
<span data-ttu-id="f6f08-151">자세한 내용은 다음 문서를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f6f08-151">For more information check out the following articles:</span></span>

* [<span data-ttu-id="f6f08-152">데이터베이스에 대한 블랙박스</span><span class="sxs-lookup"><span data-stu-id="f6f08-152">A flight data recorder for your database</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database) 
* [<span data-ttu-id="f6f08-153">쿼리 저장소를 사용한 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="f6f08-153">Monitoring Performance By Using the Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx)
* [<span data-ttu-id="f6f08-154">쿼리 저장소 사용 시나리오</span><span class="sxs-lookup"><span data-stu-id="f6f08-154">Query Store Usage Scenarios</span></span>](https://msdn.microsoft.com/library/mt614796.aspx)
* [<span data-ttu-id="f6f08-155">쿼리 저장소를 사용한 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="f6f08-155">Monitoring Performance By Using the Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx) 


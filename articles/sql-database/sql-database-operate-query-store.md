---
title: "Azure SQL 데이터베이스에서 쿼리 저장소 aaaOperating"
description: "Toooperate Azure SQL 데이터베이스에서 쿼리 저장소를 hello 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: ab741e49685bf6df3bceab219aaf57ea51cdb25d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="operating-hello-query-store-in-azure-sql-database"></a><span data-ttu-id="15ee0-103">운영 hello Azure SQL 데이터베이스에서 쿼리 저장소</span><span class="sxs-lookup"><span data-stu-id="15ee0-103">Operating hello Query Store in Azure SQL Database</span></span>
<span data-ttu-id="15ee0-104">Azure의 쿼리 저장소는 모든 쿼리에 대한 자세한 기록 정보를 지속적으로 수집하고 제공하는, 완전히 관리되는 데이터베이스 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="15ee0-104">Query Store in Azure is a fully managed database feature that continuously collects and presents detailed historic information about all queries.</span></span> <span data-ttu-id="15ee0-105">쿼리 저장소에 대 한 유사한 tooan 비행기 비행 데이터 레코더 크게 간소화 하 쿼리 성능 문제 해결에 대 한 클라우드 둘 다 고 온-프레미스 고객으로 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ee0-105">You can think about Query Store as similar tooan airplane's flight data recorder that significantly simplifies query performance troubleshooting both for cloud and on-premises customers.</span></span> <span data-ttu-id="15ee0-106">이 문서는 Azure의 쿼리 저장소 운영에 대한 구체적인 측면을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="15ee0-106">This article explains specific aspects of operating Query Store in Azure.</span></span> <span data-ttu-id="15ee0-107">미리 수집된 쿼리 데이터를 사용하면, 성능 문제를 신속하게 진단하고 해결할 수 있기 때문에 업무에 더 많은 시간을 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ee0-107">Using this pre-collected query data, you can quickly diagnose and resolve performance problems and thus spend more time focusing on their business.</span></span> 

<span data-ttu-id="15ee0-108">쿼리 저장소는 2015년 11월부터 Azure SQL 데이터베이스에서 [전세계적으로 사용할 수 있습니다](https://azure.microsoft.com/updates/general-availability-azure-sql-database-query-store/) .</span><span class="sxs-lookup"><span data-stu-id="15ee0-108">Query Store has been [globally available](https://azure.microsoft.com/updates/general-availability-azure-sql-database-query-store/) in Azure SQL Database since November, 2015.</span></span> <span data-ttu-id="15ee0-109">쿼리 저장소는 성능 분석과 같은 기능을 튜닝에 대 한 hello foundation [SQL 데이터베이스 관리자 및 성능 대시보드](https://azure.microsoft.com/updates/sqldatabaseadvisorga/)합니다.</span><span class="sxs-lookup"><span data-stu-id="15ee0-109">Query Store is hello foundation for performance analysis and tuning features, such as [SQL Database Advisor and Performance Dashboard](https://azure.microsoft.com/updates/sqldatabaseadvisorga/).</span></span> <span data-ttu-id="15ee0-110">이 문서를 게시의 hello 시점에서 쿼리 저장소가 실행 되 고 azure에서 200, 000 개 이상의 사용자 데이터베이스에 중단 없이 몇 개월 동안와 관련 된 쿼리 정보를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ee0-110">At hello moment of publishing this article, Query Store is running in more than 200,000 user databases in Azure, collecting query-related information for several months, without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="15ee0-111">Microsoft는 모든 Azure SQL 데이터베이스 (기존 및 새)에 대 한 쿼리 저장소 활성화 hello 프로세스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ee0-111">Microsoft is in hello process of activating Query Store for all Azure SQL databases (existing and new).</span></span> 
> 
> 

## <a name="optimal-query-store-configuration"></a><span data-ttu-id="15ee0-112">최적인 쿼리 저장소 구성</span><span class="sxs-lookup"><span data-stu-id="15ee0-112">Optimal Query Store Configuration</span></span>
<span data-ttu-id="15ee0-113">이 섹션에서는 최적의 구성 되는 기본값을 디자인 된 tooensure 안정적으로 작업 한 hello 쿼리 저장소와 종속 기능의 같은 설명 [SQL 데이터베이스 관리자 및 성능 대시보드](https://azure.microsoft.com/updates/sqldatabaseadvisorga/)합니다.</span><span class="sxs-lookup"><span data-stu-id="15ee0-113">This section describes optimal configuration defaults that are designed tooensure reliable operation of hello Query Store and dependent features, such as [SQL Database Advisor and Performance Dashboard](https://azure.microsoft.com/updates/sqldatabaseadvisorga/).</span></span> <span data-ttu-id="15ee0-114">기본 구성은 지속적인 데이터 수집을 위해 최적화됩니다(예: OFF/READ_ONLY 상태에 소요되는 시간 최소화).</span><span class="sxs-lookup"><span data-stu-id="15ee0-114">Default configuration is optimized for continuous data collection, that is minimal time spent in OFF/READ_ONLY states.</span></span>

| <span data-ttu-id="15ee0-115">구성</span><span class="sxs-lookup"><span data-stu-id="15ee0-115">Configuration</span></span> | <span data-ttu-id="15ee0-116">설명</span><span class="sxs-lookup"><span data-stu-id="15ee0-116">Description</span></span> | <span data-ttu-id="15ee0-117">기본값</span><span class="sxs-lookup"><span data-stu-id="15ee0-117">Default</span></span> | <span data-ttu-id="15ee0-118">주석</span><span class="sxs-lookup"><span data-stu-id="15ee0-118">Comment</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="15ee0-119">MAX_STORAGE_SIZE_MB</span><span class="sxs-lookup"><span data-stu-id="15ee0-119">MAX_STORAGE_SIZE_MB</span></span> |<span data-ttu-id="15ee0-120">쿼리 저장소는 z 고객 데이터베이스 내부에서 사용할 수 있는 hello 데이터 공간에 대 한 hello 제한을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ee0-120">Specifies hello limit for hello data space that Query Store can take inside z customer database</span></span> |<span data-ttu-id="15ee0-121">100</span><span class="sxs-lookup"><span data-stu-id="15ee0-121">100</span></span> |<span data-ttu-id="15ee0-122">새 데이터베이스에 적용</span><span class="sxs-lookup"><span data-stu-id="15ee0-122">Enforced for new databases</span></span> |
| <span data-ttu-id="15ee0-123">INTERVAL_LENGTH_MINUTES</span><span class="sxs-lookup"><span data-stu-id="15ee0-123">INTERVAL_LENGTH_MINUTES</span></span> |<span data-ttu-id="15ee0-124">쿼리 계획에 대해 수집된 런타임 통계가 집계되고 지속되는 기간의 규모를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="15ee0-124">Defines size of time window during which collected runtime statistics for query plans are aggregated and persisted.</span></span> <span data-ttu-id="15ee0-125">모든 활성 쿼리 계획은 이 구성을 통해 정의된 기간에 대해 최대 하나의 행을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="15ee0-125">Every active query plan has at most one row for a period of time defined with this configuration</span></span> |<span data-ttu-id="15ee0-126">60</span><span class="sxs-lookup"><span data-stu-id="15ee0-126">60</span></span> |<span data-ttu-id="15ee0-127">새 데이터베이스에 적용</span><span class="sxs-lookup"><span data-stu-id="15ee0-127">Enforced for new databases</span></span> |
| <span data-ttu-id="15ee0-128">STALE_QUERY_THRESHOLD_DAYS</span><span class="sxs-lookup"><span data-stu-id="15ee0-128">STALE_QUERY_THRESHOLD_DAYS</span></span> |<span data-ttu-id="15ee0-129">Hello 지속형된 런타임 통계와 비활성 쿼리의 보존 기간을 제어 하는 시간 기반 정리 정책</span><span class="sxs-lookup"><span data-stu-id="15ee0-129">Time-based cleanup policy that controls hello retention period of persisted runtime statistics and inactive queries</span></span> |<span data-ttu-id="15ee0-130">30</span><span class="sxs-lookup"><span data-stu-id="15ee0-130">30</span></span> |<span data-ttu-id="15ee0-131">새 데이터베이스 및 이전 기본값을 포함하는 데이터베이스에 적용(367)</span><span class="sxs-lookup"><span data-stu-id="15ee0-131">Enforced for new databases and databases with previous default (367)</span></span> |
| <span data-ttu-id="15ee0-132">SIZE_BASED_CLEANUP_MODE</span><span class="sxs-lookup"><span data-stu-id="15ee0-132">SIZE_BASED_CLEANUP_MODE</span></span> |<span data-ttu-id="15ee0-133">쿼리 저장소 데이터 크기가 hello 제한에 도달할 때 자동 데이터 정리 위치를 받는지 여부를 지정합니다</span><span class="sxs-lookup"><span data-stu-id="15ee0-133">Specifies whether automatic data cleanup takes place when Query Store data size approaches hello limit</span></span> |<span data-ttu-id="15ee0-134">AUTO</span><span class="sxs-lookup"><span data-stu-id="15ee0-134">AUTO</span></span> |<span data-ttu-id="15ee0-135">모든 데이터베이스에 적용</span><span class="sxs-lookup"><span data-stu-id="15ee0-135">Enforced for all databases</span></span> |
| <span data-ttu-id="15ee0-136">QUERY_CAPTURE_MODE</span><span class="sxs-lookup"><span data-stu-id="15ee0-136">QUERY_CAPTURE_MODE</span></span> |<span data-ttu-id="15ee0-137">모든 쿼리를 추적할지 또는 쿼리의 하위 집합만 추적할지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="15ee0-137">Specifies whether all queries or only a subset of queries are tracked</span></span> |<span data-ttu-id="15ee0-138">AUTO</span><span class="sxs-lookup"><span data-stu-id="15ee0-138">AUTO</span></span> |<span data-ttu-id="15ee0-139">모든 데이터베이스에 적용</span><span class="sxs-lookup"><span data-stu-id="15ee0-139">Enforced for all databases</span></span> |
| <span data-ttu-id="15ee0-140">FLUSH_INTERVAL_SECONDS</span><span class="sxs-lookup"><span data-stu-id="15ee0-140">FLUSH_INTERVAL_SECONDS</span></span> |<span data-ttu-id="15ee0-141">Toodisk에 플러시하기 전에 캡처된 런타임 통계는 메모리에 보관 되는 최대 기간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ee0-141">Specifies maximum period during which captured runtime statistics are kept in memory, before flushing toodisk</span></span> |<span data-ttu-id="15ee0-142">900</span><span class="sxs-lookup"><span data-stu-id="15ee0-142">900</span></span> |<span data-ttu-id="15ee0-143">새 데이터베이스에 적용</span><span class="sxs-lookup"><span data-stu-id="15ee0-143">Enforced for new databases</span></span> |
|  | | | |

> [!IMPORTANT]
> <span data-ttu-id="15ee0-144">이러한 기본값 hello (이전 중요 한 참고 참조)는 모든 Azure SQL 데이터베이스에서 쿼리 저장소 활성화의 최종 단계에서 자동으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ee0-144">These defaults are automatically applied in hello final stage of Query Store activation in all Azure SQL databases (see preceding important note).</span></span> <span data-ttu-id="15ee0-145">이 표시등이, 이후 Azure SQL 데이터베이스 변경 하지 않으므로 고객에 의해 설정 되는 구성 값 부정적인 영향을 받기 한 기본 워크 로드 또는 hello 쿼리 저장소의 신뢰할 수 있는 작업 하지 않는 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ee0-145">After this light up, Azure SQL Database won’t be changing configuration values set by customers, unless they negatively impact primary workload or reliable operations of hello Query Store.</span></span>
> 
> 

<span data-ttu-id="15ee0-146">사용자 지정 설정으로 toostay 하려는 경우 사용할 [쿼리 저장소 옵션으로 ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) toorevert 구성 toohello 이전 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="15ee0-146">If you want toostay with your custom settings, use [ALTER DATABASE with Query Store options](https://msdn.microsoft.com/library/bb522682.aspx) toorevert configuration toohello previous state.</span></span> <span data-ttu-id="15ee0-147">체크 아웃 [hello 쿼리 저장소로 모범 사례](https://msdn.microsoft.com/library/mt604821.aspx) toolearn 어떻게 상위 순서의 최적 구성 매개 변수를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ee0-147">Check out [Best Practices with hello Query Store](https://msdn.microsoft.com/library/mt604821.aspx) in order toolearn how top chose optimal configuration parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15ee0-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="15ee0-148">Next steps</span></span>
[<span data-ttu-id="15ee0-149">SQL 데이터베이스 성능 Insight</span><span class="sxs-lookup"><span data-stu-id="15ee0-149">SQL Database Performance Insight</span></span>](sql-database-performance.md)

## <a name="additional-resources"></a><span data-ttu-id="15ee0-150">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="15ee0-150">Additional resources</span></span>
<span data-ttu-id="15ee0-151">자세한 내용은 체크아웃 문서 다음 hello에 대 한:</span><span class="sxs-lookup"><span data-stu-id="15ee0-151">For more information check out hello following articles:</span></span>

* [<span data-ttu-id="15ee0-152">데이터베이스에 대한 블랙박스</span><span class="sxs-lookup"><span data-stu-id="15ee0-152">A flight data recorder for your database</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database) 
* [<span data-ttu-id="15ee0-153">Hello 쿼리 저장소를 사용 하 여 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="15ee0-153">Monitoring Performance By Using hello Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx)
* [<span data-ttu-id="15ee0-154">쿼리 저장소 사용 시나리오</span><span class="sxs-lookup"><span data-stu-id="15ee0-154">Query Store Usage Scenarios</span></span>](https://msdn.microsoft.com/library/mt614796.aspx)
* [<span data-ttu-id="15ee0-155">Hello 쿼리 저장소를 사용 하 여 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="15ee0-155">Monitoring Performance By Using hello Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx) 


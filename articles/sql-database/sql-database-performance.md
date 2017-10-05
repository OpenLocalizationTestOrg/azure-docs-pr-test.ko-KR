---
title: "성능 모니터링 및 향상 - Azure SQL Database | Microsoft Docs"
description: "Azure SQL 데이터베이스는 현재 쿼리 성능을 향상시킬 수 있는 영역을 식별하는 데 도움이 되는 성능 도구를 제공합니다."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: a60b75ac-cf27-4d73-8322-ee4d4c448aa2
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2016
ms.author: sstein
ms.openlocfilehash: 522b932ab055978c52f085dbaa36095bb6b77962
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-improve-performance"></a><span data-ttu-id="8fe21-103">성능 모니터링 및 향상</span><span class="sxs-lookup"><span data-stu-id="8fe21-103">Monitor and improve performance</span></span>
<span data-ttu-id="8fe21-104">Azure SQL Database는 데이터베이스의 잠재적 문제를 파악하고 지능형 튜닝 작업 및 권장 사항을 제공하여 워크로드 성능을 높일 수 있는 작업을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-104">Azure SQL Database identifies potential problems in your database and recommends actions that can improve performance of your workload by providing intelligent tuning actions and recommendations.</span></span>

<span data-ttu-id="8fe21-105">데이터베이스 성능을 검토하려면 개요 페이지의 **성능** 타일을 사용하거나 "지원 + 문제 해결" 섹션에서 아래로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-105">To review your database performance, use the **Performance** tile on the Overview page, or navigate down to "Support + troubleshooting" section:</span></span>

   ![성능 보기](./media/sql-database-performance/entries.png)

<span data-ttu-id="8fe21-107">"지원 + 문제 해결" 섹션에서 사용할 수 있는 페이지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-107">In the "Support + troubleshooting" section, you can use the following pages:</span></span>


1. <span data-ttu-id="8fe21-108">[성능 개요](#performance-overview) - 데이터베이스 성능을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-108">[Performance overview](#performance-overview) to monitor performance of your database.</span></span> 
2. <span data-ttu-id="8fe21-109">[성능 권장 사항](#performance-recommendations) - 워크로드 성능을 향상시킬 수 있는 성능 권장 사항을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-109">[Performance recommendations](#performance-recommendations) to find performance recommendations that can improve performance of your workload.</span></span>
3. <span data-ttu-id="8fe21-110">[Query Performance Insight](#query-performance-insight) - 쿼리를 소비하는 상위 리소스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-110">[Query Performance Insight](#query-performance-insight) to find top resource consuming queries.</span></span>
4. <span data-ttu-id="8fe21-111">[자동 튜닝](#automatic-tuning) - Azure SQL Database에서 데이터베이스를 자동으로 최적화하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-111">[Automatic tuning](#automatic-tuning) to let Azure SQL Database automatically optimize your database.</span></span>

## <a name="performance-overview"></a><span data-ttu-id="8fe21-112">성능 개요</span><span class="sxs-lookup"><span data-stu-id="8fe21-112">Performance Overview</span></span>
<span data-ttu-id="8fe21-113">이 보기에서는 데이터베이스 성능에 대한 요약을 제공하여 성능 튜닝 및 문제 해결에 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-113">This view provides a summary of your database performance, and helps you with performance tuning and troubleshooting.</span></span> 

![성능](./media/sql-database-performance/performance.png)

* <span data-ttu-id="8fe21-115">**권장 사항** 타일은 데이터베이스에 대한 튜닝 권장 사항을 분석하여 제공합니다(표시되는 내용이 많은 경우 상위 3가지 권장 사항이 표시됨).</span><span class="sxs-lookup"><span data-stu-id="8fe21-115">The **Recommendations** tile provides a breakdown of tuning recommendations for your database (top three recommendations are shown if there are more).</span></span> <span data-ttu-id="8fe21-116">이 타일을 클릭하면  **[성능 권장 사항](#performance-recommendations)**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-116">Clicking this tile takes you to **[Performance recommendations](#performance-recommendations)**.</span></span> 
* <span data-ttu-id="8fe21-117">**튜닝 활동** 타일은 데이터베이스에 대해 진행 중이고 완료된 튜닝 작업을 제공하여 튜닝 활동의 기록을 간략히 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-117">The **Tuning activity** tile provides a summary of the ongoing and completed tuning actions for your database, giving you a quick view into the history of tuning activity.</span></span> <span data-ttu-id="8fe21-118">이 타일을 클릭하면 데이터베이스에 대한 전체 튜닝 기록 보기로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-118">Clicking this tile takes you to the full tuning history view for your database.</span></span>
* <span data-ttu-id="8fe21-119">**자동 튜닝** 타일은 데이터베이스에 대한 [자동 튜닝 구성](sql-database-automatic-tuning-enable.md)을 보여 줍니다(데이터베이스에 자동으로 적용되는 튜닝 옵션).</span><span class="sxs-lookup"><span data-stu-id="8fe21-119">The **Auto-tuning** tile shows the [auto-tuning configuration](sql-database-automatic-tuning-enable.md) for your database (tuning options that are automatically applied to your database).</span></span> <span data-ttu-id="8fe21-120">이 타일을 클릭하면 자동화 구성 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-120">Clicking this tile opens the automation configuration dialog.</span></span>
* <span data-ttu-id="8fe21-121">**데이터베이스 쿼리** 타일은 데이터베이스에 대한 쿼리 성능 요약을 보여 줍니다(전체 DTU 사용량 및 최상위 리소스 사용 쿼리).</span><span class="sxs-lookup"><span data-stu-id="8fe21-121">The **Database queries** tile shows the summary of the query performance for your database (overall DTU usage and top resource consuming queries).</span></span> <span data-ttu-id="8fe21-122">이 타일을 클릭하면 **[Query Performance Insight](#query-performance-insight)**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-122">Clicking this tile takes you to **[Query Performance Insight](#query-performance-insight)**.</span></span>

## <a name="performance-recommendations"></a><span data-ttu-id="8fe21-123">성능 권장 사항</span><span class="sxs-lookup"><span data-stu-id="8fe21-123">Performance recommendations</span></span>
<span data-ttu-id="8fe21-124">이 페이지는 데이터베이스의 성능을 향상시킬 수 있는 지능형 [튜닝 권장 사항](sql-database-advisor.md)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-124">This page provides intelligent [tuning recommendations](sql-database-advisor.md) that can improve your database's performance.</span></span> <span data-ttu-id="8fe21-125">다음과 같은 유형의 권장 사항이 이 페이지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-125">The following types of recommendations are shown on this page:</span></span>

* <span data-ttu-id="8fe21-126">만들거나 삭제할 인덱스에 대한 권장 사항.</span><span class="sxs-lookup"><span data-stu-id="8fe21-126">Recommendations on which indexes to create or drop.</span></span>
* <span data-ttu-id="8fe21-127">데이터베이스에서 스키마 문제가 확인될 때 권장 사항.</span><span class="sxs-lookup"><span data-stu-id="8fe21-127">Recommendations when schema issues are identified in the database.</span></span>
* <span data-ttu-id="8fe21-128">쿼리가 매개 변수화된 쿼리에서 이점을 얻을 수 있는 경우 권장 사항.</span><span class="sxs-lookup"><span data-stu-id="8fe21-128">Recommendations when queries can benefit from parameterized queries.</span></span>

![성능](./media/sql-database-performance/recommendations.png)

<span data-ttu-id="8fe21-130">또한 이전에 적용되었던 튜닝 작업의 전체 기록을 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-130">You can also find complete history of tuning actions that were applied in the past.</span></span>

<span data-ttu-id="8fe21-131">[성능 권장 사항 찾기 및 적용](sql-database-advisor-portal.md) 문서에서 성능 권장 사항을 찾아 적용하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="8fe21-131">Learn how to find an apply performance recommendations in [Find and apply performance recommendations](sql-database-advisor-portal.md) article.</span></span>

## <a name="automatic-tuning"></a><span data-ttu-id="8fe21-132">자동 조정</span><span class="sxs-lookup"><span data-stu-id="8fe21-132">Automatic tuning</span></span>
<span data-ttu-id="8fe21-133">Azure SQL Database는 자동으로 [성능 권장 사항](sql-database-advisor.md)을 적용하여 데이터베이스 성능을 튜닝할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-133">Azure SQL Databases can automatically tune database performance by applying [performance recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="8fe21-134">자세한 내용은 [자동 튜닝 문서](sql-database-automatic-tuning.md)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="8fe21-134">To learn more, read [Automatic tuning article](sql-database-automatic-tuning.md).</span></span> <span data-ttu-id="8fe21-135">이 기능을 사용하려면 [자동 튜닝 사용 방법](sql-database-automatic-tuning-enable.md)을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="8fe21-135">To enable it, read [how to enable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>

## <a name="query-performance-insight"></a><span data-ttu-id="8fe21-136">Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="8fe21-136">Query Performance Insight</span></span>
<span data-ttu-id="8fe21-137">[Query Performance Insight](sql-database-query-performance.md) 를 통해 다음을 제공하여 데이터베이스 성능 문제 해결 시간을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-137">[Query Performance Insight](sql-database-query-performance.md) allows you to spend less time troubleshooting database performance by providing:</span></span>

* <span data-ttu-id="8fe21-138">데이터베이스 리소스(DTU) 사용에 대한 보다 자세한 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-138">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="8fe21-139">최상위 CPU 사용 쿼리는 향상된 성능을 위해 잠재적으로 조정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-139">The top CPU consuming queries, which can potentially be tuned for improved performance.</span></span> 
* <span data-ttu-id="8fe21-140">쿼리에 대한 세부 정보로 드릴다운할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fe21-140">The ability to drill down into the details of a query.</span></span> 

  ![성능 대시보드](./media/sql-database-query-performance/performance.png)

<span data-ttu-id="8fe21-142">**[Query Performance Insight 사용 방법](sql-database-query-performance.md)** 문서에서 이 페이지에 대한 자세한 내용을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="8fe21-142">Find more information about this page in the article **[How to use Query Performance Insight](sql-database-query-performance.md)**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8fe21-143">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="8fe21-143">Additional resources</span></span>
* [<span data-ttu-id="8fe21-144">단일 데이터베이스의 Azure SQL 데이터베이스 성능 지침</span><span class="sxs-lookup"><span data-stu-id="8fe21-144">Azure SQL Database performance guidance for single databases</span></span>](sql-database-performance-guidance.md)
* [<span data-ttu-id="8fe21-145">탄력적 풀을 사용해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="8fe21-145">When should an elastic pool be used?</span></span>](sql-database-elastic-pool-guidance.md)


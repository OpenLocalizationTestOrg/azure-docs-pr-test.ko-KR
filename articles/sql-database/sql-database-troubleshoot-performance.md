---
title: "모니터링 및 성능 튜닝 - Azure SQL Database | Microsoft Docs"
description: "평가 및 개선을 통한 Azure SQL Database의 성능 튜닝 관련 팁."
services: sql-database
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
keywords: "sql 성능 튜닝, 데이터베이스 성능 튜닝, sql 성능 튜닝 팁, SQL Database 성능 튜닝"
ms.assetid: eb7b3f66-3b33-4e1b-84fb-424a928a6672
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: v-shysun
ms.openlocfilehash: 7a2f1199a56e0bd32eafef9f420879c756673e7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-and-performance-tuning"></a><span data-ttu-id="cc1fa-104">모니터링 및 성능 튜닝</span><span class="sxs-lookup"><span data-stu-id="cc1fa-104">Monitoring and performance tuning</span></span>

<span data-ttu-id="cc1fa-105">Azure SQL Database는 사용량을 쉽게 모니터링하고, 리소스(CPU, 메모리, IO)를 추가 또는 제거하며, 데이터베이스 성능을 향상시킬 수 있는 권장 사항을 찾거나, 데이터베이스가 사용자 워크로드에 맞게 조정되고 성능을 자동으로 최적화할 수 있도록 해주는 자동으로 관리되는 유연한 데이터 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-105">Azure SQL Database is automatically managed and flexible data service where you can easily monitor usage, add or remove resources (CPU, memory, io), find recommendations that can improve performance of your database, or let database adapt to your workload and automatically optimize performance.</span></span>

<span data-ttu-id="cc1fa-106">이 문서에서는 Azure SQL Database에서 제공되는 모니터링 및 성능 튜닝 옵션에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-106">This article provides overview of monitoring and performance tuning options that are available in Azure SQL Database.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="monitoring-and-troubleshooting-database-performance"></a><span data-ttu-id="cc1fa-107">모니터링 및 데이터베이스 성능 문제 해결</span><span class="sxs-lookup"><span data-stu-id="cc1fa-107">Monitoring and troubleshooting database performance</span></span>

<span data-ttu-id="cc1fa-108">Azure SQL Database를 사용하면 데이터베이스 사용량을 쉽게 모니터링하고 성능 문제를 일으킬 수 있는 쿼리를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-108">Azure SQL Database enables you to easily monitor your database usage and identify queries that might cause the performance issues.</span></span> <span data-ttu-id="cc1fa-109">Azure Portal 또는 시스템 뷰를 사용gkdu 데이터베이스 성능을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-109">You can monitor database performance using Azure portal or system views.</span></span> <span data-ttu-id="cc1fa-110">데이터베이스 성능 문제 해결 및 모니터링에 대한 다음과 같은 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-110">You have the following options for monitoring and troubleshooting database performance:</span></span>

1. <span data-ttu-id="cc1fa-111">[Azure Portal](https://portal.azure.com)에서 **SQL Database**를 클릭하고 데이터베이스를 선택한 후 모니터링 차트를 사용하여 최대값에 근접한 리소스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-111">In the [Azure portal](https://portal.azure.com), click **SQL databases**, select the database, and then use the Monitoring chart to look for resources approaching their maximum.</span></span> <span data-ttu-id="cc1fa-112">기본적으로 DTU 사용량이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-112">DTU consumption is shown by default.</span></span> <span data-ttu-id="cc1fa-113">**편집** 을 클릭하여 표시된 시간 범위 및 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-113">Click **Edit** to change the time range and values shown.</span></span>
2. <span data-ttu-id="cc1fa-114">[Query Performance Insight](sql-database-query-performance.md)를 사용하여 가장 많은 리소스를 소비하는 쿼리를 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-114">Use [Query Performance Insight](sql-database-query-performance.md) to identify the queries that spend the most of resources.</span></span>
3. <span data-ttu-id="cc1fa-115">DMV(동적 관리 뷰), 확장 이벤트(`XEvents`) 및 SSMS의 쿼리 저장소를 사용하여 실시간으로 성능 매개 변수를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-115">You can use dynamic management views (DMVs), Extended Events (`XEvents`), and the Query Store in SSMS to get performance parameters in real time.</span></span>

<span data-ttu-id="cc1fa-116">이러한 보고서 또는 뷰를 사용하여 몇 가지 문제를 파악하는 경우 Azure SQL Database의 성능을 향상시키는 데 사용할 수 있는 기술을 찾으려면 [성능 지침 항목](sql-database-performance-guidance.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-116">See the [performance guidance topic](sql-database-performance-guidance.md) to find techniques that you can use to improve performance of Azure SQL Database if you identify some issue using these reports or views.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="cc1fa-117">Microsoft Azure 및 SQL 데이터베이스에 대한 업데이트와 동기화 상태를 유지하려면 항상 최신 버전의 Management Studio를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-117">It is recommended that you always use the latest version of Management Studio to remain synchronized with updates to Microsoft Azure and SQL Database.</span></span> <span data-ttu-id="cc1fa-118">[SQL Server Management Studio를 업데이트합니다](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc1fa-118">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
>

## <a name="optimize-database-to-improve-performance"></a><span data-ttu-id="cc1fa-119">데이터베이스 최적화로 성능 개선</span><span class="sxs-lookup"><span data-stu-id="cc1fa-119">Optimize database to improve performance</span></span>

<span data-ttu-id="cc1fa-120">Azure SQL Database를 사용하면 [성능 튜닝 권장 사항](sql-database-advisor.md)을 검토하여 리소스를 변경하지 않고도 쿼리 성능을 개선 및 최적화하는 기회를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-120">Azure SQL Database enables you to identify opportunities to improve and optimize query performance without changing resources by reviewing [performance tuning recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="cc1fa-121">인덱스 누락 및 최적화되지 않은 쿼리는 데이터베이스 성능을 저하시키는 일반적인 원인입니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-121">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="cc1fa-122">이러한 튜닝 권장 사항을 적용하여 워크로드의 성능을 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-122">You can apply these tuning recommendations to improve performance of your workload.</span></span>
<span data-ttu-id="cc1fa-123">또한 Azure SQL Database를 통해 식별된 모든 권장 사항을 적용하고 이를 통해 데이터베이스 성능이 개선되는지 확인하여 [쿼리의 성능을 자동으로 최적화](sql-database-automatic-tuning.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-123">You can also let Azure SQL database to [automatically optimize performance of your queries](sql-database-automatic-tuning.md) by applying all identified recommendations and verifying that they improve database performance.</span></span> <span data-ttu-id="cc1fa-124">데이터베이스의 성능 향상을 위해 다음 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-124">You can use the following options to improve performance of your database:</span></span>

1. <span data-ttu-id="cc1fa-125">[SQL Database Advisor](sql-database-advisor-portal.md)를 사용하여 인덱스 만들기 및 삭제, 쿼리 매개 변수화, 스키마 문제 해결에 대한 권장 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-125">Use [SQL Database Advisor](sql-database-advisor-portal.md) to view recommendations for creating and dropping indexes, parameterizing queries, and fixing schema issues.</span></span>
2. <span data-ttu-id="cc1fa-126">[자동 튜닝을 사용](sql-database-automatic-tuning-enable.md)하고 Azure SQL Database에서 식별된 성능 문제를 자동으로 수정하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-126">[Enable automatic tuning](sql-database-automatic-tuning-enable.md) and let Azure SQL database automatically fix identified performance issues.</span></span>

## <a name="improving-database-performance-with-more-resources"></a><span data-ttu-id="cc1fa-127">보다 많은 리소스와 함께 데이터베이스 성능 개선</span><span class="sxs-lookup"><span data-stu-id="cc1fa-127">Improving database performance with more resources</span></span>

<span data-ttu-id="cc1fa-128">마지막으로, 데이터베이스의 성능을 향상시킬 수 있는 실행 가능한 항목이 더 없으면 Azure SQL Database에서 사용할 수 있는 리소스의 양을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-128">Finally, if there are no actionable items that can improve performance of your database, you can change the amount of resources available in Azure SQL Database.</span></span> <span data-ttu-id="cc1fa-129">독립 실행형 데이터베이스의 [서비스 계층](sql-database-service-tiers.md)을 변경하여 더 많은 리소스를 할당하거나 탄력적 풀의 eDTU를 언제든지 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-129">You can assign more resources by changing the [service tier](sql-database-service-tiers.md) of a standalone database or increase the eDTUs of an elastic pool at any time.</span></span>
1. <span data-ttu-id="cc1fa-130">독립 실행형 데이터베이스의 경우 필요에 따라 [서비스 계층을 변경](sql-database-service-tiers.md) 하여 데이터베이스 성능을 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-130">For standalone databases, you can [change service tiers](sql-database-service-tiers.md) on-demand to improve database performance.</span></span>
2. <span data-ttu-id="cc1fa-131">여러 데이터베이스의 경우 [탄력적 풀](sql-database-elastic-pool-guidance.md)을 사용하여 자동으로 리소스 규모를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-131">For multiple databases, consider using [elastic pools](sql-database-elastic-pool-guidance.md) to scale resources automatically.</span></span>

## <a name="tune-and-refactor-application-or-database-code"></a><span data-ttu-id="cc1fa-132">응용 프로그램 또는 데이터베이스 코드 조정 및 리팩터링</span><span class="sxs-lookup"><span data-stu-id="cc1fa-132">Tune and refactor application or database code</span></span>

<span data-ttu-id="cc1fa-133">데이터베이스를 보다 최적으로 사용하도록 응용 프로그램 코드를 변경하거나 인덱스를 변경하며 계획을 강제 적용하거나 힌트를 사용하여 사용자 워크로드에 맞게 데이터베이스를 수동으로 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-133">You can change application code to more optimally use the database, change indexes, force plans, or use hints to manually adapt the database to your workload.</span></span> <span data-ttu-id="cc1fa-134">수동 튜닝 및 코드 다시 작성에 대한 몇 가지 지침 및 팁은 [성능 지침 항목](sql-database-performance-guidance.md) 문서에서 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-134">Find some guidance and tips for manual tuning and rewriting the code in the [performance guidance topic](sql-database-performance-guidance.md) article.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cc1fa-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cc1fa-135">Next steps</span></span>

- <span data-ttu-id="cc1fa-136">Azure SQL Database에서 자동 조정을 사용하도록 설정하고 자동 조정 기능으로 작업을 완벽하게 관리하려면 [자동 조정 사용](sql-database-automatic-tuning-enable.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-136">To enable automatic tuning in Azure SQL Database and let automatic tuning feature fully manage your workload, see [Enable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>
- <span data-ttu-id="cc1fa-137">수동 튜닝을 사용하려면 [Azure Portal에서 튜닝 권장 사항](sql-database-advisor-portal.md)을 검토하고 쿼리의 성능을 개선하는 권장 사항을 직접 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-137">To use manual tuning, you can review [Tuning recommendations in Azure portal](sql-database-advisor-portal.md) and manually apply the ones that improve performance of your queries.</span></span>
- <span data-ttu-id="cc1fa-138">[Azure SQL Database 서비스 계층](sql-database-performance-guidance.md)을 변경하여 데이터베이스에 제공되는 리소스를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cc1fa-138">Change resources that are available in your database by changing [Azure SQL Database service tiers](sql-database-performance-guidance.md)</span></span>
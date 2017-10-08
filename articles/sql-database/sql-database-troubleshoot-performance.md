---
title: "aaaMonitoring & 성능 튜닝-Azure SQL 데이터베이스 | Microsoft Docs"
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
ms.openlocfilehash: 9e196831902aa6ea841ef14caf5713e82ebfc62d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-performance-tuning"></a><span data-ttu-id="44761-104">모니터링 및 성능 튜닝</span><span class="sxs-lookup"><span data-stu-id="44761-104">Monitoring and performance tuning</span></span>

<span data-ttu-id="44761-105">Azure SQL 데이터베이스는 자동으로 관리 했는데 하거나 수 있는 쉽게 사용을 모니터링, 추가 리소스 (CPU, 메모리, io)를 제거 하는 유연한 데이터 서비스 tooyour 작업 부하를 조정 하는 데이터베이스를 사용 하거나 사용자 데이터베이스의 성능을 향상 시킬 수 있는 권장 구성 및 자동으로 성능을 최적화 합니다.</span><span class="sxs-lookup"><span data-stu-id="44761-105">Azure SQL Database is automatically managed and flexible data service where you can easily monitor usage, add or remove resources (CPU, memory, io), find recommendations that can improve performance of your database, or let database adapt tooyour workload and automatically optimize performance.</span></span>

<span data-ttu-id="44761-106">이 문서에서는 Azure SQL Database에서 제공되는 모니터링 및 성능 튜닝 옵션에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="44761-106">This article provides overview of monitoring and performance tuning options that are available in Azure SQL Database.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="monitoring-and-troubleshooting-database-performance"></a><span data-ttu-id="44761-107">모니터링 및 데이터베이스 성능 문제 해결</span><span class="sxs-lookup"><span data-stu-id="44761-107">Monitoring and troubleshooting database performance</span></span>

<span data-ttu-id="44761-108">Azure SQL 데이터베이스를 사용 하면 tooeasily 데이터베이스 사용량을 모니터링 하 고 hello 성능 문제를 일으킬 수 있는 쿼리를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="44761-108">Azure SQL Database enables you tooeasily monitor your database usage and identify queries that might cause hello performance issues.</span></span> <span data-ttu-id="44761-109">Azure Portal 또는 시스템 뷰를 사용gkdu 데이터베이스 성능을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44761-109">You can monitor database performance using Azure portal or system views.</span></span> <span data-ttu-id="44761-110">Hello 다음 모니터링 및 데이터베이스 성능 문제 해결에 대 한 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44761-110">You have hello following options for monitoring and troubleshooting database performance:</span></span>

1. <span data-ttu-id="44761-111">Hello에 [Azure 포털](https://portal.azure.com), 클릭 **SQL 데이터베이스**hello 데이터베이스를 선택한 다음 모니터링 차트 toolook hello를 사용 하 여 최대에 근접 하 고 리소스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="44761-111">In hello [Azure portal](https://portal.azure.com), click **SQL databases**, select hello database, and then use hello Monitoring chart toolook for resources approaching their maximum.</span></span> <span data-ttu-id="44761-112">기본적으로 DTU 사용량이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="44761-112">DTU consumption is shown by default.</span></span> <span data-ttu-id="44761-113">클릭 **편집** toochange hello 시간 범위 및 표시 되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="44761-113">Click **Edit** toochange hello time range and values shown.</span></span>
2. <span data-ttu-id="44761-114">사용 하 여 [Query Performance Insight](sql-database-query-performance.md) tooidentify hello 쿼리 소비 하는 가장 hello 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="44761-114">Use [Query Performance Insight](sql-database-query-performance.md) tooidentify hello queries that spend hello most of resources.</span></span>
3. <span data-ttu-id="44761-115">확장 이벤트 동적 관리 뷰 (Dmv)를 사용할 수 있습니다 (`XEvents`), 쿼리 저장소를 실시간으로 SSMS tooget 성능 매개 변수에서 hello 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="44761-115">You can use dynamic management views (DMVs), Extended Events (`XEvents`), and hello Query Store in SSMS tooget performance parameters in real time.</span></span>

<span data-ttu-id="44761-116">Hello 참조 [성능 지침 항목이](sql-database-performance-guidance.md) toofind 기술을 이러한 보고서 또는 뷰를 사용 하 여 몇 가지 문제를 식별 하는 경우 Azure SQL 데이터베이스의 tooimprove 성능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44761-116">See hello [performance guidance topic](sql-database-performance-guidance.md) toofind techniques that you can use tooimprove performance of Azure SQL Database if you identify some issue using these reports or views.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="44761-117">항상 hello를 사용 하는 것이 좋습니다. 최신 버전 tooremain Management Studio의 Azure 및 SQL 데이터베이스 업데이트 tooMicrosoft와 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="44761-117">It is recommended that you always use hello latest version of Management Studio tooremain synchronized with updates tooMicrosoft Azure and SQL Database.</span></span> <span data-ttu-id="44761-118">[SQL Server Management Studio를 업데이트합니다](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="44761-118">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
>

## <a name="optimize-database-tooimprove-performance"></a><span data-ttu-id="44761-119">데이터베이스 tooimprove 성능 최적화</span><span class="sxs-lookup"><span data-stu-id="44761-119">Optimize database tooimprove performance</span></span>

<span data-ttu-id="44761-120">Azure SQL 데이터베이스 tooidentify 기회 tooimprove를 사용 하면 및를 검토 하 여 리소스를 변경 하지 않고 쿼리 성능을 최적화할 [성능 튜닝 권장 구성](sql-database-advisor.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="44761-120">Azure SQL Database enables you tooidentify opportunities tooimprove and optimize query performance without changing resources by reviewing [performance tuning recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="44761-121">인덱스 누락 및 최적화되지 않은 쿼리는 데이터베이스 성능을 저하시키는 일반적인 원인입니다.</span><span class="sxs-lookup"><span data-stu-id="44761-121">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="44761-122">작업의 튜닝 권장 사항을 tooimprove 성능 이러한 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44761-122">You can apply these tuning recommendations tooimprove performance of your workload.</span></span>
<span data-ttu-id="44761-123">수도 있습니다 할 수 있도록된 Azure SQL 데이터베이스 너무[자동으로 쿼리의 성능을 최적화할](sql-database-automatic-tuning.md) 적용 하 여 모든 권장 사항 및 데이터베이스의 성능을 향상 시키는 것을 확인을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="44761-123">You can also let Azure SQL database too[automatically optimize performance of your queries](sql-database-automatic-tuning.md) by applying all identified recommendations and verifying that they improve database performance.</span></span> <span data-ttu-id="44761-124">다음 데이터베이스 옵션 tooimprove 성능 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44761-124">You can use hello following options tooimprove performance of your database:</span></span>

1. <span data-ttu-id="44761-125">사용 하 여 [SQL 데이터베이스 관리자](sql-database-advisor-portal.md) tooview 권장 사항을 생성 하 고 인덱스를 삭제, 쿼리를 매개 변수화 및 스키마 문제를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="44761-125">Use [SQL Database Advisor](sql-database-advisor-portal.md) tooview recommendations for creating and dropping indexes, parameterizing queries, and fixing schema issues.</span></span>
2. <span data-ttu-id="44761-126">[자동 튜닝을 사용](sql-database-automatic-tuning-enable.md)하고 Azure SQL Database에서 식별된 성능 문제를 자동으로 수정하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="44761-126">[Enable automatic tuning](sql-database-automatic-tuning-enable.md) and let Azure SQL database automatically fix identified performance issues.</span></span>

## <a name="improving-database-performance-with-more-resources"></a><span data-ttu-id="44761-127">보다 많은 리소스와 함께 데이터베이스 성능 개선</span><span class="sxs-lookup"><span data-stu-id="44761-127">Improving database performance with more resources</span></span>

<span data-ttu-id="44761-128">마지막으로, 데이터베이스의 성능을 향상 시킬 수 있는 실행 가능한 항목이 더 없으면 hello 양의 Azure SQL 데이터베이스에서 사용할 수 있는 리소스를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44761-128">Finally, if there are no actionable items that can improve performance of your database, you can change hello amount of resources available in Azure SQL Database.</span></span> <span data-ttu-id="44761-129">Hello를 변경 하 여 더 많은 리소스를 할당할 수 있습니다 [서비스 계층](sql-database-service-tiers.md) 독립 실행형의 데이터베이스 또는 언제 든 지 탄력적 풀의 Edtu hello 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="44761-129">You can assign more resources by changing hello [service tier](sql-database-service-tiers.md) of a standalone database or increase hello eDTUs of an elastic pool at any time.</span></span>
1. <span data-ttu-id="44761-130">독립 실행형 데이터베이스에서는 있습니다 [서비스 계층을 변경할](sql-database-service-tiers.md) 주문형 tooimprove 데이터베이스 성능.</span><span class="sxs-lookup"><span data-stu-id="44761-130">For standalone databases, you can [change service tiers](sql-database-service-tiers.md) on-demand tooimprove database performance.</span></span>
2. <span data-ttu-id="44761-131">여러 데이터베이스를 사용 하는 것이 좋습니다 [탄력적 풀](sql-database-elastic-pool-guidance.md) tooscale 리소스 자동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="44761-131">For multiple databases, consider using [elastic pools](sql-database-elastic-pool-guidance.md) tooscale resources automatically.</span></span>

## <a name="tune-and-refactor-application-or-database-code"></a><span data-ttu-id="44761-132">응용 프로그램 또는 데이터베이스 코드 조정 및 리팩터링</span><span class="sxs-lookup"><span data-stu-id="44761-132">Tune and refactor application or database code</span></span>

<span data-ttu-id="44761-133">응용 프로그램 코드 toomore를 최적으로 변경할 수 있습니다 hello 데이터베이스를 사용 하 여, 인덱스 변경, 계획을 강제로 또는 toomanually hello 데이터베이스 tooyour 작업 부하를 조정 하는 힌트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="44761-133">You can change application code toomore optimally use hello database, change indexes, force plans, or use hints toomanually adapt hello database tooyour workload.</span></span> <span data-ttu-id="44761-134">수동 성능 조정 방식 이며 hello에 hello 코드를 다시 작성에 대 한 몇 가지 지침과 정보를 찾을 [성능 지침 항목이](sql-database-performance-guidance.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="44761-134">Find some guidance and tips for manual tuning and rewriting hello code in hello [performance guidance topic](sql-database-performance-guidance.md) article.</span></span>


## <a name="next-steps"></a><span data-ttu-id="44761-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="44761-135">Next steps</span></span>

- <span data-ttu-id="44761-136">Azure SQL 데이터베이스 및 let 자동 튜닝 자동 tooenable 튜닝 기능이 완벽 하 게 작업을 관리할 참조 [자동 조정 기능 사용](sql-database-automatic-tuning-enable.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="44761-136">tooenable automatic tuning in Azure SQL Database and let automatic tuning feature fully manage your workload, see [Enable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>
- <span data-ttu-id="44761-137">수동 튜닝 toouse 검토할 수 있습니다 [튜닝 권장 구성을 Azure 포털에서](sql-database-advisor-portal.md) 수동으로 hello 쿼리의 성능을 개선 하는 것을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="44761-137">toouse manual tuning, you can review [Tuning recommendations in Azure portal](sql-database-advisor-portal.md) and manually apply hello ones that improve performance of your queries.</span></span>
- <span data-ttu-id="44761-138">[Azure SQL Database 서비스 계층](sql-database-performance-guidance.md)을 변경하여 데이터베이스에 제공되는 리소스를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="44761-138">Change resources that are available in your database by changing [Azure SQL Database service tiers](sql-database-performance-guidance.md)</span></span>
---
title: "성능 문제 해결 및 데이터베이스 최적화 | Microsoft Docs"
description: "SQL Database에 성능 권장 사항을 적용하고 데이터베이스에 대해 실행되는 쿼리의 성능에 대한 정보를 얻는 방법을 알아봅니다."
metakeywords: azure sql database performance monitoring recommendation
services: sql-database
documentationcenter: 
manager: jhubbard
author: jan-eng
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,monitor & tune
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: janeng
ms.openlocfilehash: f9ae96cdc80c347593f229cb2fce3f2d4d8e7caf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a><span data-ttu-id="dd1b1-103">성능 문제 해결 및 데이터베이스 최적화</span><span class="sxs-lookup"><span data-stu-id="dd1b1-103">Troubleshoot performance issues and optimize your database</span></span>

<span data-ttu-id="dd1b1-104">인덱스 누락 및 최적화되지 않은 쿼리는 데이터베이스 성능을 저하시키는 일반적인 원인입니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-104">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="dd1b1-105">이 자습서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-105">In this tutorial you learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="dd1b1-106">성능 향상 권장 사항 검토, 적용 및 되돌리기</span><span class="sxs-lookup"><span data-stu-id="dd1b1-106">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="dd1b1-107">높은 리소스 사용률을 나타내는 쿼리 찾기</span><span class="sxs-lookup"><span data-stu-id="dd1b1-107">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="dd1b1-108">장기 실행 쿼리 찾기</span><span class="sxs-lookup"><span data-stu-id="dd1b1-108">Find long running queries</span></span>

> <span data-ttu-id="dd1b1-109">성능 문제(예를 들어, 권장 사항을 받기 위한 인덱스 누락)가 있는 데이터베이스에서 지속적인 워크로드가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-109">You need a continuous workload on a database with performance issues – missing an index for example to receive a recommendation.</span></span>
>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="dd1b1-110">Azure 포털에 로그인</span><span class="sxs-lookup"><span data-stu-id="dd1b1-110">Log in to the Azure portal</span></span>

<span data-ttu-id="dd1b1-111">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-111">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="review-and-apply-a-recommendation"></a><span data-ttu-id="dd1b1-112">권장 사항 검토 및 적용</span><span class="sxs-lookup"><span data-stu-id="dd1b1-112">Review and apply a recommendation</span></span>

<span data-ttu-id="dd1b1-113">다음 단계에 따라 데이터베이스에 대한 시스템에서 권장 사항을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-113">Follow these steps to apply a recommendation from the system for your database:</span></span>

1. <span data-ttu-id="dd1b1-114">데이터베이스 블레이드에서 **쿼리 권장 사항** 메뉴를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-114">Click the **Performance recommendations** menu in the database blade.</span></span>

    ![성능 권장 사항](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. <span data-ttu-id="dd1b1-116">권장 사항 목록에서 사용 중인 권장 사항을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-116">From the list of recommendations, select an active recommendation.</span></span> <span data-ttu-id="dd1b1-117">이 예제에서 인덱스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-117">In this example, Create Index.</span></span>

    ![권장 사항 선택](./media/sql-database-performance-tutorial/create_index.png)

3. <span data-ttu-id="dd1b1-119">**적용** 단추를 클릭하여 권장 사항을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-119">Apply the recommendation by clicking the **Apply** button.</span></span> <span data-ttu-id="dd1b1-120">필요에 따라 권장 사항 정보를 검토하고 **스크립트 보기** 단추를 클릭하여 실행할 T-SQL 스크립트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-120">Optionally, review the recommendation details and see the T-SQL script to  be executed by clicking on **View Script** button.</span></span>

    ![권장 사항 적용](./media/sql-database-performance-tutorial/apply.png)

4. <span data-ttu-id="dd1b1-122">[선택 사항] 권장 사항이 자동으로 적용되도록 하려면 자동 조정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-122">[Optional] Enable automatic tuning for recommendations to be applied automatically.</span></span>

    ![자동 조정](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a><span data-ttu-id="dd1b1-124">권장 사항 되돌리기</span><span class="sxs-lookup"><span data-stu-id="dd1b1-124">Revert a recommendation</span></span>

<span data-ttu-id="dd1b1-125">Database Advisor는 구현된 모든 권장 사항을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-125">The Database Advisor monitors every recommendation implemented.</span></span> <span data-ttu-id="dd1b1-126">권장 사항으로 워크로드가 개선되지 않으면 자동으로 되돌려집니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-126">If a recommendation doesn't improve the workload it will be automatically reverted.</span></span> <span data-ttu-id="dd1b1-127">수동으로 권장 사항 되돌리기가 가능하지만 대부분의 경우 반드시 그런 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-127">Manually reverting a recommendation is possible, but not necessary in most cases.</span></span> <span data-ttu-id="dd1b1-128">권장 사항을 되돌리려면</span><span class="sxs-lookup"><span data-stu-id="dd1b1-128">To revert a recommendation:</span></span>

1. <span data-ttu-id="dd1b1-129">성능 권장 사항 메뉴로 이동하고 적용된 권장 사항 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-129">Go to the performance recommendations menu and select one of the applied recommendations.</span></span>

    ![권장 사항 선택](./media/sql-database-performance-tutorial/select.png)

2. <span data-ttu-id="dd1b1-131">세부 정보 보기에서 **되돌리기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-131">In the details view, click **Revert**.</span></span>

    ![권장 사항 되돌리기](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-the-query-that-consumes-the-most-resources"></a><span data-ttu-id="dd1b1-133">대부분의 리소스를 사용하는 쿼리 찾기</span><span class="sxs-lookup"><span data-stu-id="dd1b1-133">Find the query that consumes the most resources</span></span>

<span data-ttu-id="dd1b1-134">다음 단계에 따라 대부분의 리소스를 사용하는 쿼리를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-134">Follow these steps to find the query consuming the most resources:</span></span>

1. <span data-ttu-id="dd1b1-135">데이터베이스 블레이드에서 **Query Performance Insight** 메뉴를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-135">Click on the **Query Performance Insight** menu in the database blade.</span></span>

    ![쿼리 인사이트](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. <span data-ttu-id="dd1b1-137">리소스 종류를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-137">Select a resource type.</span></span>

    ![쿼리 인사이트](./media/sql-database-performance-tutorial/select_resource_type.png)

3. <span data-ttu-id="dd1b1-139">테이블에서 첫 번째 쿼리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-139">Select the first query in the table.</span></span>

    ![쿼리 인사이트](./media/sql-database-performance-tutorial/select_query.png)

4. <span data-ttu-id="dd1b1-141">쿼리 세부 정보를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-141">Review the query details.</span></span>

    ![쿼리 인사이트](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-the-longest-running-query"></a><span data-ttu-id="dd1b1-143">가장 오래 실행되는 쿼리 찾기</span><span class="sxs-lookup"><span data-stu-id="dd1b1-143">Find the longest running query</span></span>

1. <span data-ttu-id="dd1b1-144">Query Performance Insight로 이동하고 **장기 실행 쿼리** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-144">Go to Query Performance Insight and select the **Long running queries** tab.</span></span>

    ![쿼리 인사이트](./media/sql-database-performance-tutorial/long_running.png)

3. <span data-ttu-id="dd1b1-146">테이블에서 첫 번째 쿼리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-146">Select the first query in the table.</span></span>

    ![쿼리 인사이트](./media/sql-database-performance-tutorial/select_first_query.png)

4. <span data-ttu-id="dd1b1-148">쿼리 세부 정보를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-148">Review the query details.</span></span>

    ![쿼리 인사이트](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a><span data-ttu-id="dd1b1-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dd1b1-150">Next steps</span></span> 
<span data-ttu-id="dd1b1-151">인덱스 누락 및 최적화되지 않은 쿼리는 데이터베이스 성능을 저하시키는 일반적인 원인입니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-151">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="dd1b1-152">이 자습서에서는 다음에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="dd1b1-152">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="dd1b1-153">성능 향상 권장 사항 검토, 적용 및 되돌리기</span><span class="sxs-lookup"><span data-stu-id="dd1b1-153">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="dd1b1-154">높은 리소스 사용률을 나타내는 쿼리 찾기</span><span class="sxs-lookup"><span data-stu-id="dd1b1-154">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="dd1b1-155">장기 실행 쿼리 찾기</span><span class="sxs-lookup"><span data-stu-id="dd1b1-155">Find long running queries</span></span>

[<span data-ttu-id="dd1b1-156">SQL 데이터베이스 성능 튜닝 팁</span><span class="sxs-lookup"><span data-stu-id="dd1b1-156">SQL Database performance tuning tips</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)

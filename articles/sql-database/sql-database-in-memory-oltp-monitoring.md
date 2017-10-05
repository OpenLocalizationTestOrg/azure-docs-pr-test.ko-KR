---
title: "XTP 메모리 내 저장소 모니터링 | Microsoft Docs"
description: "XTP 메모리 내 저장소 사용, 용량을 예측 및 모니터링합니다. 41823 용량 오류를 해결합니다."
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: 5afb2209f18b1ba2aa0a916a439509b01afd80da
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-in-memory-oltp-storage"></a><span data-ttu-id="c7ddd-103">메모리 내 OLTP 저장소 모니터링</span><span class="sxs-lookup"><span data-stu-id="c7ddd-103">Monitor In-Memory OLTP Storage</span></span>
<span data-ttu-id="c7ddd-104">[메모리 내 OLTP](sql-database-in-memory.md)를 사용하는 경우 메모리에 최적화된 테이블 및 테이블 변수에 있는 데이터는 메모리 내 OLTP 저장소에 상주합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ddd-104">When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage.</span></span> <span data-ttu-id="c7ddd-105">각 Premium 서비스 계층은 최대 메모리 내 OLTP 저장소 크기가 있으며 이는 [SQL Database 서비스 계층 문서](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels)에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ddd-105">Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span></span> <span data-ttu-id="c7ddd-106">이 제한이 초과되면 삽입 및 업데이트 작업이 실패(오류 41823)하기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7ddd-106">Once this limit is exceeded, insert and update operations may start failing (with error 41823).</span></span> <span data-ttu-id="c7ddd-107">해당 시점에서 데이터를 삭제하여 하나에 메모리를 회수하거나 데이터베이스의 성능 계층을 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ddd-107">At that point you will need to either delete data to reclaim memory, or upgrade the performance tier of your database.</span></span>

## <a name="determine-whether-data-will-fit-within-the-in-memory-storage-cap"></a><span data-ttu-id="c7ddd-108">데이터가 메모리 내 저장소 용량에 맞는지 여부 결정</span><span class="sxs-lookup"><span data-stu-id="c7ddd-108">Determine whether data will fit within the in-memory storage cap</span></span>
<span data-ttu-id="c7ddd-109">저장소 용량 결정: 다른 Premium 서비스 계층의 저장소 용량은 [SQL Database 서비스 계층 문서](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ddd-109">Determine the storage cap: consult the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for the storage caps of the different Premium service tiers.</span></span>

<span data-ttu-id="c7ddd-110">메모리에 최적화된 테이블에 대한 메모리 요구 사항을 추정하면 Azure SQL 데이터베이스에서 SQL Server가 작동과 동일한 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ddd-110">Estimating memory requirements for a memory-optimized table works the same way for SQL Server as it does in Azure SQL Database.</span></span> <span data-ttu-id="c7ddd-111">[MSDN](https://msdn.microsoft.com/library/dn282389.aspx)의 항목을 검토하는 데 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="c7ddd-111">Take a few minutes to review that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span></span>

<span data-ttu-id="c7ddd-112">테이블 및 테이블 변수 행 뿐만 아니라 인덱스가 사용자 데이터 크기를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ddd-112">Note that the table and table variable rows, as well as indexes, count toward the max user data size.</span></span> <span data-ttu-id="c7ddd-113">또한 ALTER TABLE은 전체 테이블 및 인덱스의 새 버전을 만들기 위해 충분한 공간이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ddd-113">In addition, ALTER TABLE needs enough room to create a new version of the entire table and its indexes.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="c7ddd-114">모니터링 및 경고</span><span class="sxs-lookup"><span data-stu-id="c7ddd-114">Monitoring and alerting</span></span>
<span data-ttu-id="c7ddd-115">메모리 내 저장소 사용량을 Azure [Portal](https://portal.azure.com/)에서 [성능 계층에 대한 저장소 용량](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels)으로 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7ddd-115">You can monitor in-memory storage use as a percentage of the [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in the Azure [portal](https://portal.azure.com/):</span></span> 

* <span data-ttu-id="c7ddd-116">데이터베이스 블레이드에서 리소스 사용률 상자를 찾고 편집을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ddd-116">On the Database blade, locate the Resource utilization box and click on Edit.</span></span>
* <span data-ttu-id="c7ddd-117">그런 다음 메트릭 `In-Memory OLTP Storage percentage`을(를) 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ddd-117">Then select the metric `In-Memory OLTP Storage percentage`.</span></span>
* <span data-ttu-id="c7ddd-118">경고를 추가하려면 리소스 사용률 상자 클릭하여 메트릭 블레이드를 연 다음 경고 추가를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ddd-118">To add an alert, click on the Resource Utilization box to open the Metric blade, then click on Add alert.</span></span>

<span data-ttu-id="c7ddd-119">또는 다음 쿼리를 사용하여 메모리 내 저장소 사용률을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ddd-119">Or use the following query to show the in-memory storage utilization:</span></span>

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a><span data-ttu-id="c7ddd-120">메모리 부족 상황 수정 - 오류 41823</span><span class="sxs-lookup"><span data-stu-id="c7ddd-120">Correct out-of-memory situations - Error 41823</span></span>
<span data-ttu-id="c7ddd-121">메모리가 부족하면 오류 메시지 41823과 함께 삽입, 업데이트 및 만들기 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ddd-121">Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.</span></span>

<span data-ttu-id="c7ddd-122">오류 메시지 41823은 메모리 액세스에 최적화된 테이블 및 테이블 변수가 최대 크기를 초과했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c7ddd-122">Error message 41823 indicates that the memory-optimized tables and table variables have exceeded the maximum size.</span></span>

<span data-ttu-id="c7ddd-123">이 오류를 해결하려면</span><span class="sxs-lookup"><span data-stu-id="c7ddd-123">To resolve this error, either:</span></span>

* <span data-ttu-id="c7ddd-124">잠재적으로 데이터를 기존의 디스크 기반 테이블에 오프로드딩하여 메모리에 최적화된 테이블에서 데이터를 삭제합니다. 또는</span><span class="sxs-lookup"><span data-stu-id="c7ddd-124">Delete data from the memory-optimized tables, potentially offloading the data to traditional, disk-based tables; or,</span></span>
* <span data-ttu-id="c7ddd-125">메모리에 최적화된 테이블에서 유지하는 데 필요한 데이터에 대한 충분한 메모리 내 저장소가 있는 서비스 계층을 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="c7ddd-125">Upgrade the service tier to one with enough in-memory storage for the data you need to keep in memory-optimized tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7ddd-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c7ddd-126">Next steps</span></span>
<span data-ttu-id="c7ddd-127">모니터링 지침은 [동적 관리 뷰를 사용하여 Azure SQL Database 모니터링](sql-database-monitoring-with-dmvs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c7ddd-127">For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).</span></span>

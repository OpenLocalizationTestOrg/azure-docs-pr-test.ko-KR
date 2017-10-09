---
title: "aaaMonitor XTP 메모리 내 저장소 | Microsoft Docs"
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
ms.openlocfilehash: fcb17bd8e9ebef4862d4b55bf5a79b45b9419fca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-in-memory-oltp-storage"></a><span data-ttu-id="2e01a-103">메모리 내 OLTP 저장소 모니터링</span><span class="sxs-lookup"><span data-stu-id="2e01a-103">Monitor In-Memory OLTP Storage</span></span>
<span data-ttu-id="2e01a-104">[메모리 내 OLTP](sql-database-in-memory.md)를 사용하는 경우 메모리에 최적화된 테이블 및 테이블 변수에 있는 데이터는 메모리 내 OLTP 저장소에 상주합니다.</span><span class="sxs-lookup"><span data-stu-id="2e01a-104">When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage.</span></span> <span data-ttu-id="2e01a-105">각 Premium 서비스 계층의 hello에 설명 되어 있는 최대 메모리 내 OLTP 저장소 크기, [SQL 데이터베이스 서비스 계층 문서](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e01a-105">Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in hello [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span></span> <span data-ttu-id="2e01a-106">이 제한이 초과되면 삽입 및 업데이트 작업이 실패(오류 41823)하기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e01a-106">Once this limit is exceeded, insert and update operations may start failing (with error 41823).</span></span> <span data-ttu-id="2e01a-107">해당 지점에서 tooeither delete 데이터 tooreclaim 메모리가 필요를 아니면 데이터베이스의 hello 성능 계층을 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e01a-107">At that point you will need tooeither delete data tooreclaim memory, or upgrade hello performance tier of your database.</span></span>

## <a name="determine-whether-data-will-fit-within-hello-in-memory-storage-cap"></a><span data-ttu-id="2e01a-108">데이터를 메모리 내 저장소 끝 모양 hello 내의 들어가는지 여부 확인</span><span class="sxs-lookup"><span data-stu-id="2e01a-108">Determine whether data will fit within hello in-memory storage cap</span></span>
<span data-ttu-id="2e01a-109">Hello 저장소 cap 결정: hello를 참조 하십시오. [SQL 데이터베이스 서비스 계층 문서](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) hello 다른 Premium 서비스 계층의 hello 저장소 대문자입니다.</span><span class="sxs-lookup"><span data-stu-id="2e01a-109">Determine hello storage cap: consult hello [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for hello storage caps of hello different Premium service tiers.</span></span>

<span data-ttu-id="2e01a-110">그와 SQL Server에 대 한 방법으로 메모리 요구 사항을 작동 하는 메모리 액세스에 최적화 된 테이블에 대 한 hello 동일한 예측 Azure SQL 데이터베이스에서 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e01a-110">Estimating memory requirements for a memory-optimized table works hello same way for SQL Server as it does in Azure SQL Database.</span></span> <span data-ttu-id="2e01a-111">몇 분 tooreview 해당 항목 수행 [MSDN](https://msdn.microsoft.com/library/dn282389.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e01a-111">Take a few minutes tooreview that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span></span>

<span data-ttu-id="2e01a-112">인덱스 뿐만 아니라 hello 테이블 및 테이블 변수 행 hello 사용자 최대 데이터 크기에 대해 계산 하는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e01a-112">Note that hello table and table variable rows, as well as indexes, count toward hello max user data size.</span></span> <span data-ttu-id="2e01a-113">또한 ALTER TABLE 충분 한 공간이 toocreate hello 전체 테이블 인덱스의 새 버전 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2e01a-113">In addition, ALTER TABLE needs enough room toocreate a new version of hello entire table and its indexes.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="2e01a-114">모니터링 및 경고</span><span class="sxs-lookup"><span data-stu-id="2e01a-114">Monitoring and alerting</span></span>
<span data-ttu-id="2e01a-115">Hello에 대 한 백분율로 메모리 내 저장소 사용을 모니터링할 수 [성능 계층에 대 한 저장소 cap](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) hello Azure에서에서 [포털](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="2e01a-115">You can monitor in-memory storage use as a percentage of hello [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in hello Azure [portal](https://portal.azure.com/):</span></span> 

* <span data-ttu-id="2e01a-116">데이터베이스 블레이드에서 hello hello 리소스 사용률 상자 찾아 편집을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e01a-116">On hello Database blade, locate hello Resource utilization box and click on Edit.</span></span>
* <span data-ttu-id="2e01a-117">그런 다음 hello 메트릭을 선택 `In-Memory OLTP Storage percentage`합니다.</span><span class="sxs-lookup"><span data-stu-id="2e01a-117">Then select hello metric `In-Memory OLTP Storage percentage`.</span></span>
* <span data-ttu-id="2e01a-118">경고를 tooadd hello 리소스 사용률 상자 tooopen hello 메트릭 블레이드를 클릭 한 다음 추가 경고를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e01a-118">tooadd an alert, click on hello Resource Utilization box tooopen hello Metric blade, then click on Add alert.</span></span>

<span data-ttu-id="2e01a-119">또는 사용 하 여 hello 다음 쿼리 tooshow hello 메모리 내 저장소 사용:</span><span class="sxs-lookup"><span data-stu-id="2e01a-119">Or use hello following query tooshow hello in-memory storage utilization:</span></span>

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a><span data-ttu-id="2e01a-120">메모리 부족 상황 수정 - 오류 41823</span><span class="sxs-lookup"><span data-stu-id="2e01a-120">Correct out-of-memory situations - Error 41823</span></span>
<span data-ttu-id="2e01a-121">메모리가 부족하면 오류 메시지 41823과 함께 삽입, 업데이트 및 만들기 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="2e01a-121">Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.</span></span>

<span data-ttu-id="2e01a-122">오류 메시지 41823 hello 메모리 액세스에 최적화 된 테이블 및 테이블 변수와 hello 최대 크기를 초과 했습니다 했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2e01a-122">Error message 41823 indicates that hello memory-optimized tables and table variables have exceeded hello maximum size.</span></span>

<span data-ttu-id="2e01a-123">tooresolve이이 오류 중 하나:</span><span class="sxs-lookup"><span data-stu-id="2e01a-123">tooresolve this error, either:</span></span>

* <span data-ttu-id="2e01a-124">Hello 메모리 액세스에 최적화 된 테이블, 잠재적으로 오프 로드 hello 데이터 tootraditional, 디스크 기반 테이블에서 데이터를 삭제 합니다. 또는,</span><span class="sxs-lookup"><span data-stu-id="2e01a-124">Delete data from hello memory-optimized tables, potentially offloading hello data tootraditional, disk-based tables; or,</span></span>
* <span data-ttu-id="2e01a-125">서비스 계층 tooone hello 업그레이드 메모리 액세스에 최적화 된 테이블에 tookeep hello 데이터에 대 한 충분 한 메모리 내 저장소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e01a-125">Upgrade hello service tier tooone with enough in-memory storage for hello data you need tookeep in memory-optimized tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e01a-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2e01a-126">Next steps</span></span>
<span data-ttu-id="2e01a-127">모니터링 지침은 [동적 관리 뷰를 사용하여 Azure SQL Database 모니터링](sql-database-monitoring-with-dmvs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e01a-127">For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).</span></span>

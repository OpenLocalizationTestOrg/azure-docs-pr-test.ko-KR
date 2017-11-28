---
title: "T-SQL: Azure SQL Database 탄력적 풀 관리 | Microsoft Docs"
description: "T-SQL을 사용하여 Azure SQL Database 탄력적 풀을 관리합니다."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 4e288e17-bc3e-4255-9fbe-0a2ac0dbd7dd
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 05/27/2016
ms.author: srinia
ms.openlocfilehash: c6b64e4a7fd91283a37a792b294965064d653003
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a><span data-ttu-id="79c5f-103">Transact-SQL로 탄력적 풀 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="79c5f-103">Monitor and manage an elastic pool with Transact-SQL</span></span>
<span data-ttu-id="79c5f-104">이 항목에서는 Transact-SQL을 사용하여 확장 가능한 [탄력적 풀](sql-database-elastic-pool.md)을 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-104">This topic shows you how to manage scalable [elastic pools](sql-database-elastic-pool.md) with Transact-SQL.</span></span>  <span data-ttu-id="79c5f-105">[Azure Portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), REST API 또는 [C#](sql-database-elastic-pool-manage-csharp.md)을 사용하여 Azure 탄력적 풀을 만들고 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-105">You can also create and manage an Azure elastic pool the [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="79c5f-106">[Transact-SQL](sql-database-elastic-pool-manage-tsql.md)을 사용하여 탄력적 풀을 만들고 여기에 데이터베이스를 넣거나 뺄 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>


<span data-ttu-id="79c5f-107">[데이터베이스 만들기(Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) 및 [데이터베이스 변경(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) 명령을 사용하여 데이터베이스를 만들고 탄력적 풀의 내부 및 외부로 이동시킵니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-107">Use the [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) and [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commands to create and move databases into and out of elastic pools.</span></span> <span data-ttu-id="79c5f-108">탄력적 풀은 이러한 명령을 사용하기 전에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-108">The elastic pool must exist before you can use these commands.</span></span> <span data-ttu-id="79c5f-109">이러한 명령은 데이터베이스에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-109">These commands affect only databases.</span></span> <span data-ttu-id="79c5f-110">새 풀 만들기 및 풀 속성(예: 최소 및 최대 eDTU)의 설정은 T-SQL 명령으로 변경될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-110">Creation of new pools and the setting of pool properties (such as min and max eDTUs) cannot be changed with T-SQL commands.</span></span>

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="79c5f-111">탄력적 풀에 풀링된 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="79c5f-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="79c5f-112">SERVICE_OBJECTIVE 옵션과 함께 데이터베이스 만들기 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-112">Use the CREATE DATABASE command with the SERVICE_OBJECTIVE option.</span></span>   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

<span data-ttu-id="79c5f-113">탄력적 풀에 있는 모든 데이터베이스는 탄력적 풀의 서비스 계층(기본, 표준, 프리미엄)을 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-113">All databases in an elastic pool inherit the service tier of the elastic pool (Basic, Standard, Premium).</span></span> 

## <a name="move-a-database-between-elastic-pools"></a><span data-ttu-id="79c5f-114">탄력적 풀 간에 데이터베이스 이동</span><span class="sxs-lookup"><span data-stu-id="79c5f-114">Move a database between elastic pools</span></span>
<span data-ttu-id="79c5f-115">수정으로 데이터베이스 변경 명령을 사용하고 SERVICE\_OBJECTIVE 옵션을 ELASTIC\_POOL로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-115">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC\_POOL.</span></span> <span data-ttu-id="79c5f-116">이름을 대상 풀의 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-116">Set the name to the name of the target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move the database named db1 to an elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="79c5f-117">탄력적 풀로 데이터베이스 이동</span><span class="sxs-lookup"><span data-stu-id="79c5f-117">Move a database into an elastic pool</span></span>
<span data-ttu-id="79c5f-118">수정으로 데이터베이스 변경 명령을 사용하고 SERVICE\_OBJECTIVE 옵션을 ELASTIC_POOL로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-118">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC_POOL.</span></span> <span data-ttu-id="79c5f-119">이름을 대상 풀의 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-119">Set the name to the name of the target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move the database named db1 to an elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="79c5f-120">탄력적 풀 외부로 데이터베이스 이동</span><span class="sxs-lookup"><span data-stu-id="79c5f-120">Move a database out of an elastic pool</span></span>
<span data-ttu-id="79c5f-121">데이터베이스 변경 명령을 사용하고 성능 수준(예: S0 또는 S1) 중 하나에 SERVICE_OBJECTIVE를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-121">Use the ALTER DATABASE command and set the SERVICE_OBJECTIVE to one of the performance levels (such as S0 or S1).</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes the database into a stand-alone database with the service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="79c5f-122">탄력적 풀에 데이터베이스 나열</span><span class="sxs-lookup"><span data-stu-id="79c5f-122">List databases in an elastic pool</span></span>
<span data-ttu-id="79c5f-123">[sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619)를 사용하여 탄력적 풀의 모든 데이터베이스를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-123">Use the [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) to list all the databases in an elastic pool.</span></span> <span data-ttu-id="79c5f-124">마스터 데이터베이스에 로그인하여 뷰를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-124">Log in to the master database to query the view.</span></span>

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="79c5f-125">탄력적 풀에 대한 리소스 사용량 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="79c5f-125">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="79c5f-126">[sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx)를 사용하여 논리 서버에서 탄력적 풀의 리소스 사용 통계를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-126">Use the [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) to examine the resource usage statistics of an elastic pool on a logical server.</span></span> <span data-ttu-id="79c5f-127">마스터 데이터베이스에 로그인하여 뷰를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-127">Log in to the master database to query the view.</span></span>

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a><span data-ttu-id="79c5f-128">풀링된 데이터베이스에 대한 리소스 사용량 가져오기</span><span class="sxs-lookup"><span data-stu-id="79c5f-128">Get resource usage for a pooled database</span></span>
<span data-ttu-id="79c5f-129">[sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) 또는 [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx)를 사용하여 탄력적 풀에서 데이터베이스의 리소스 사용 통계를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-129">Use the [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) or [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) to examine the resource usage statistics of a database in an elastic pool.</span></span> <span data-ttu-id="79c5f-130">이 프로세스는 단일 데이터베이스에 대한 리소스 사용량을 쿼리하는 경우와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-130">This process is similar to querying resource usage for a single database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79c5f-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="79c5f-131">Next steps</span></span>
<span data-ttu-id="79c5f-132">탄력적 풀을 만든 후에 탄력적 작업을 만들어 풀에 있는 탄력적 데이터베이스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-132">After creating an elastic pool, you can manage elastic databases in the pool by creating elastic jobs.</span></span> <span data-ttu-id="79c5f-133">탄력적 작업을 통해 개수에 관계없이 풀에 있는 데이터베이스에 대해 T-SQL 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-133">Elastic jobs facilitate running T-SQL scripts against any number of databases in the pool.</span></span> <span data-ttu-id="79c5f-134">자세한 내용은 [탄력적 데이터베이스 작업 개요](sql-database-elastic-jobs-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79c5f-134">For more information, see [Elastic database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

<span data-ttu-id="79c5f-135">[Azure SQL 데이터베이스를 사용하여 규모 확장](sql-database-elastic-scale-introduction.md)참조: 탄력적 데이터베이스 도구를 사용하여 규모를 확장하거나 데이터를 이동하거나 쿼리 또는 트랜잭션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="79c5f-135">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic database tools to scale out, move data, query, or create transactions.</span></span>


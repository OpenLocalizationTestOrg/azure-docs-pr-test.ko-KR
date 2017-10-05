---
title: "Azure SQL Data Warehouse의 T-SQL을 사용한 일시 중지, 다시 시작, 크기 조정 | Microsoft Docs"
description: "DWU를 조정하여 성능을 확장하는 Transact-SQL (T-SQL) 작업입니다. 사용량이 많지 않은 시간 동안 다시 조정하여 비용을 절감합니다."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: a970d939-2adf-4856-8a78-d4fe8ab2cceb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/30/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 9221d72ecf8ab2ba8b04e4bc97eeef7157817cca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a><span data-ttu-id="65d8d-104">Azure SQL Data Warehouse의 계산 능력 관리(T-SQL)</span><span class="sxs-lookup"><span data-stu-id="65d8d-104">Manage compute power in Azure SQL Data Warehouse (T-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="65d8d-105">개요</span><span class="sxs-lookup"><span data-stu-id="65d8d-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="65d8d-106">포털</span><span class="sxs-lookup"><span data-stu-id="65d8d-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="65d8d-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="65d8d-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="65d8d-108">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="65d8d-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="65d8d-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="65d8d-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a><span data-ttu-id="65d8d-110">현재 DWU 설정 보기</span><span class="sxs-lookup"><span data-stu-id="65d8d-110">View current DWU settings</span></span>
<span data-ttu-id="65d8d-111">데이터베이스의 현재 DWU 설정을 보려면</span><span class="sxs-lookup"><span data-stu-id="65d8d-111">To view the current DWU settings for your databases:</span></span>

1. <span data-ttu-id="65d8d-112">Visual Studio에서 SQL Server 개체 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="65d8d-112">Open SQL Server Object Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="65d8d-113">논리적 SQL 데이터베이스 서버와 연결된 마스터 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="65d8d-113">Connect to the master database associated with the logical SQL Database server.</span></span>
3. <span data-ttu-id="65d8d-114">sys.database_service_objectives 동적 관리 뷰에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65d8d-114">Select from the sys.database_service_objectives dynamic management view.</span></span> <span data-ttu-id="65d8d-115">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="65d8d-115">Here is an example:</span></span> 

```sql
SELECT
    db.name [Database]
,   ds.edition [Edition]
,   ds.service_objective [Service Objective]
FROM
    sys.database_service_objectives ds
JOIN
    sys.databases db ON ds.database_id = db.database_id
```

<a name="scale-dwu-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="65d8d-116">계산 조정</span><span class="sxs-lookup"><span data-stu-id="65d8d-116">Scale compute</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="65d8d-117">DWU를 변경하려면</span><span class="sxs-lookup"><span data-stu-id="65d8d-117">To change the DWUs:</span></span>

1. <span data-ttu-id="65d8d-118">논리적 SQL 데이터베이스 서버와 연결된 마스터 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="65d8d-118">Connect to the master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="65d8d-119">[ALTER DATABASE][ALTER DATABASE] TSQL 문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="65d8d-119">Use the [ALTER DATABASE][ALTER DATABASE] TSQL statement.</span></span> <span data-ttu-id="65d8d-120">다음 예제에서는 MySQLDW 데이터베이스에 대한 서비스 수준 목표를 DW1000으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="65d8d-120">The following example sets the service level objective to DW1000 for the database MySQLDW.</span></span> 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a><span data-ttu-id="65d8d-121">데이터베이스 상태 및 작업 진행 상태 확인</span><span class="sxs-lookup"><span data-stu-id="65d8d-121">Check database state and operation progress</span></span>

1. <span data-ttu-id="65d8d-122">논리적 SQL 데이터베이스 서버와 연결된 마스터 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="65d8d-122">Connect to the master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="65d8d-123">데이터베이스 상태를 확인하는 쿼리 제출</span><span class="sxs-lookup"><span data-stu-id="65d8d-123">Submit query to check database state</span></span>

```sql
SELECT *
FROM
sys.databases
```

3. <span data-ttu-id="65d8d-124">작업 상태를 확인하는 쿼리 제출</span><span class="sxs-lookup"><span data-stu-id="65d8d-124">Submit query to check status of operation</span></span>

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

<span data-ttu-id="65d8d-125">이 DMV는 SQL Data Warehouse에 대해 작업 및 작업 상태(IN_PROGRESS 또는 COMPLETED)와 같은 다양한 관리 작업에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="65d8d-125">This DMV will return information about various management operations on your SQL Data Warehouse such as the operation and the state of the operation, which will either be IN_PROGRESS or COMPLETED.</span></span>



<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="65d8d-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="65d8d-126">Next steps</span></span>
<span data-ttu-id="65d8d-127">다른 관리 작업은 [관리 개요][Management overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="65d8d-127">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/

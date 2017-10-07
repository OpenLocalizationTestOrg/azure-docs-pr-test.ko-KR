---
title: "aaaPause, 다시 시작 하 고 확장할 수 있는 Azure SQL 데이터 웨어하우스에서 T-SQL | Microsoft Docs"
description: "Dwu로 조정 하 여 작업 tooscale 아웃 성능 TRANSACT-SQL (T-SQL)입니다. 사용량이 많지 않은 시간 동안 다시 조정하여 비용을 절감합니다."
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
ms.openlocfilehash: 84c6868acb673221d8853319ac9a05bb98b2b7c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a><span data-ttu-id="31f60-104">Azure SQL Data Warehouse의 계산 능력 관리(T-SQL)</span><span class="sxs-lookup"><span data-stu-id="31f60-104">Manage compute power in Azure SQL Data Warehouse (T-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="31f60-105">개요</span><span class="sxs-lookup"><span data-stu-id="31f60-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="31f60-106">포털</span><span class="sxs-lookup"><span data-stu-id="31f60-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="31f60-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="31f60-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="31f60-108">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="31f60-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="31f60-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="31f60-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a><span data-ttu-id="31f60-110">현재 DWU 설정 보기</span><span class="sxs-lookup"><span data-stu-id="31f60-110">View current DWU settings</span></span>
<span data-ttu-id="31f60-111">tooview hello 현재 DWU 설정 데이터베이스에 대해:</span><span class="sxs-lookup"><span data-stu-id="31f60-111">tooview hello current DWU settings for your databases:</span></span>

1. <span data-ttu-id="31f60-112">Visual Studio에서 SQL Server 개체 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="31f60-112">Open SQL Server Object Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="31f60-113">Hello 논리 SQL 데이터베이스 서버와 관련 된 toohello master 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="31f60-113">Connect toohello master database associated with hello logical SQL Database server.</span></span>
3. <span data-ttu-id="31f60-114">Hello sys.database_service_objectives 동적 관리 뷰에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="31f60-114">Select from hello sys.database_service_objectives dynamic management view.</span></span> <span data-ttu-id="31f60-115">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="31f60-115">Here is an example:</span></span> 

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

## <a name="scale-compute"></a><span data-ttu-id="31f60-116">계산 조정</span><span class="sxs-lookup"><span data-stu-id="31f60-116">Scale compute</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="31f60-117">toochange hello dwu로:</span><span class="sxs-lookup"><span data-stu-id="31f60-117">toochange hello DWUs:</span></span>

1. <span data-ttu-id="31f60-118">SQL 데이터베이스 논리 서버와 관련 된 toohello master 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="31f60-118">Connect toohello master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="31f60-119">사용 하 여 hello [ALTER DATABASE] [ ALTER DATABASE] TSQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="31f60-119">Use hello [ALTER DATABASE][ALTER DATABASE] TSQL statement.</span></span> <span data-ttu-id="31f60-120">hello 다음 예제에서는 설정 hello 서비스 수준 목표 tooDW1000 MySQLDW hello 데이터베이스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="31f60-120">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW.</span></span> 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a><span data-ttu-id="31f60-121">데이터베이스 상태 및 작업 진행 상태 확인</span><span class="sxs-lookup"><span data-stu-id="31f60-121">Check database state and operation progress</span></span>

1. <span data-ttu-id="31f60-122">SQL 데이터베이스 논리 서버와 관련 된 toohello master 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="31f60-122">Connect toohello master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="31f60-123">Toocheck 데이터베이스 상태 쿼리를 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="31f60-123">Submit query toocheck database state</span></span>

```sql
SELECT *
FROM
sys.databases
```

3. <span data-ttu-id="31f60-124">전송 작업의 쿼리 toocheck 상태</span><span class="sxs-lookup"><span data-stu-id="31f60-124">Submit query toocheck status of operation</span></span>

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

<span data-ttu-id="31f60-125">이 DMV SQL 데이터 웨어하우스 IN_PROGRESS 중 하나가 됩니다 하거나 완료 된 hello 작업의 hello 작업과 hello 상태 등의 다양 한 관리 작업에 대 한 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="31f60-125">This DMV will return information about various management operations on your SQL Data Warehouse such as hello operation and hello state of hello operation, which will either be IN_PROGRESS or COMPLETED.</span></span>



<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="31f60-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="31f60-126">Next steps</span></span>
<span data-ttu-id="31f60-127">다른 관리 작업은 [관리 개요][Management overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31f60-127">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/

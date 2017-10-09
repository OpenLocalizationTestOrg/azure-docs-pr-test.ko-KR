---
title: "aaaPause, 다시 시작 하 고 확장할 수 있는 Azure SQL 데이터 웨어하우스에 저장 된 상태의 | Microsoft Docs"
description: "REST, T-SQL 및 PowerShell을 통해 SQL Data Warehouse에서 계산 능력을 관리합니다."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 21de7337-9356-49bb-a6eb-06c1beeba2c4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 07/25/2017
ms.author: elbutter
ms.openlocfilehash: fc867febb118fb5c86c2637a41b232076021b95d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-rest"></a><span data-ttu-id="8aab6-103">Azure SQL Data Warehouse의 계산 능력 관리(REST)</span><span class="sxs-lookup"><span data-stu-id="8aab6-103">Manage compute power in Azure SQL Data Warehouse (REST)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8aab6-104">개요</span><span class="sxs-lookup"><span data-stu-id="8aab6-104">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="8aab6-105">포털</span><span class="sxs-lookup"><span data-stu-id="8aab6-105">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="8aab6-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8aab6-106">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="8aab6-107">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="8aab6-107">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="8aab6-108">TSQL</span><span class="sxs-lookup"><span data-stu-id="8aab6-108">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="8aab6-109">계산 능력 크기 조정</span><span class="sxs-lookup"><span data-stu-id="8aab6-109">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="8aab6-110">toochange hello dwu로 사용 하 여 hello [만들기 또는 업데이트 데이터베이스] [ Create or Update Database] REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="8aab6-110">toochange hello DWUs, use hello [Create or Update Database][Create or Update Database] REST API.</span></span> <span data-ttu-id="8aab6-111">hello 다음 예제에서는 설정 hello 서비스 수준 목표 tooDW1000 hello MySQLDW 호스팅되는 데이터베이스에 대 한 서버 MyServer에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="8aab6-111">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW which is hosted on server MyServer.</span></span> <span data-ttu-id="8aab6-112">hello 서버 이름이 ResourceGroup1 Azure 리소스 그룹에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8aab6-112">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```
PATCH https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}?api-version=2014-04-01-preview HTTP/1.1
Content-Type: application/json; charset=UTF-8

{
    "properties": {
        "requestedServiceObjectiveName": DW1000
    }
}
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="8aab6-113">계산 일시 중지</span><span class="sxs-lookup"><span data-stu-id="8aab6-113">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="8aab6-114">toopause 데이터베이스를 사용 하 여 hello [일시 중지 데이터베이스] [ Pause Database] REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="8aab6-114">toopause a database, use hello [Pause Database][Pause Database] REST API.</span></span> <span data-ttu-id="8aab6-115">hello 다음 중지 하는 예제 Server01 라는 서버에서 호스팅되는 Database02 라는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="8aab6-115">hello following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="8aab6-116">hello 서버 이름이 ResourceGroup1 Azure 리소스 그룹에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8aab6-116">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/pause?api-version=2014-04-01-preview HTTP/1.1
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="8aab6-117">계산 다시 시작</span><span class="sxs-lookup"><span data-stu-id="8aab6-117">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="8aab6-118">toostart 데이터베이스를 사용 하 여 hello [이력서 데이터베이스] [ Resume Database] REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="8aab6-118">toostart a database, use hello [Resume Database][Resume Database] REST API.</span></span> <span data-ttu-id="8aab6-119">hello 다음 예제에서는 시작 라는 Database02 Server01 라는 서버에서 호스트 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="8aab6-119">hello following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="8aab6-120">hello 서버 이름이 ResourceGroup1 Azure 리소스 그룹에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8aab6-120">hello server is in an Azure resource group named ResourceGroup1.</span></span> 

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/resume?api-version=2014-04-01-preview HTTP/1.1
```

## <a name="check-database-state"></a><span data-ttu-id="8aab6-121">데이터베이스 상태 확인</span><span class="sxs-lookup"><span data-stu-id="8aab6-121">Check database state</span></span>

```
GET https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}?api-version=2014-04-01 HTTP/1.1
```

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="8aab6-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8aab6-122">Next steps</span></span>
<span data-ttu-id="8aab6-123">다른 관리 작업은 [관리 개요][Management overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8aab6-123">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Pause Database]: https://msdn.microsoft.com/library/azure/mt718817.aspx
[Resume Database]: https://msdn.microsoft.com/library/azure/mt718820.aspx
[Create or Update Database]: https://msdn.microsoft.com/library/azure/mt163685.aspx

<!--Other Web references-->

[Azure portal]: http://portal.azure.com/

---
title: "TSQL를 사용하여 SQL Data Warehouse 만들기 | Microsoft Docs"
description: "TSQL를 사용하여 SQL 데이터 웨어하우스를 만드는 방법을 알아봅니다."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: a4e2e68e-aa9c-4dd3-abb0-f7df997d237a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 10d8aa2b3ab8d7d8a9b91e95ffccf03faa89d237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a><span data-ttu-id="7fa9a-103">TRANSACT-SQL(TSQL)를 사용하여 SQL 데이터 웨어하우스 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="7fa9a-103">Create a SQL Data Warehouse database by using Transact-SQL (TSQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7fa9a-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="7fa9a-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="7fa9a-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="7fa9a-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="7fa9a-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7fa9a-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="7fa9a-107">이 문서에서는 T-SQL을 사용하여 SQL 데이터 웨어하우스를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-107">This article shows you how to create a SQL Data Warehouse using T-SQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fa9a-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7fa9a-108">Prerequisites</span></span>
<span data-ttu-id="7fa9a-109">시작하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-109">To get started, you need:</span></span>

* <span data-ttu-id="7fa9a-110">**Azure 계정**: [Azure 무료 평가판][Azure Free Trial] 또는 [MSDN Azure 크레딧][MSDN Azure Credits]을 방문하여 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span></span>
* <span data-ttu-id="7fa9a-111">**Azure SQL server**: [Azure SQL 데이터베이스 논리 서버는 Azure 포털을 만들기]를 참조 [Azure SQL 데이터베이스 논리 서버는 Azure 포털을 만듭니다] [PowerShell을 사용한 Azure SQL 데이터베이스 논리 서버 만들기] 또는 [Azure SQL 만들기 PowerShell과 함께 데이터베이스 논리 서버]에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-111">**Azure SQL server**:  See [Create an Azure SQL Database logical server with the Azure Portal][Create an Azure SQL Database logical server with the Azure Portal] or [Create an Azure SQL Database logical server with PowerShell][Create an Azure SQL Database logical server with PowerShell] for more details.</span></span>
* <span data-ttu-id="7fa9a-112">**리소스 그룹**: Azure SQL Server와 동일한 리소스 그룹을 사용하거나 [리소스 그룹을 만드는 방법][how to create a resource group]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-112">**Resource group**: Either use the same resource group as your Azure SQL server or see [how to create a resource group][how to create a resource group].</span></span>
* <span data-ttu-id="7fa9a-113">**T-SQL을 실행할 환경**: [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd] 또한 [SSMS][SSMS]을 사용하여 T-SQL을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-113">**Environment to execute T-SQL**: You can use [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], or [SSMS][SSMS] to execute T-SQL.</span></span>

> [!NOTE]
> <span data-ttu-id="7fa9a-114">SQL 데이터 웨어하우스를 만들면 새로운 유료 서비스가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-114">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="7fa9a-115">가격 책정에 대한 자세한 내용은 [SQL Data Warehouse 가격 책정][SQL Data Warehouse pricing]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-115">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-database-with-visual-studio"></a><span data-ttu-id="7fa9a-116">Visual Studio를 사용하여 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="7fa9a-116">Create a database with Visual Studio</span></span>
<span data-ttu-id="7fa9a-117">Visual Studio를 처음 접하는 경우 [Azure SQL Data Warehouse 쿼리(Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-117">If you are new to Visual Studio, see the article [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span></span>  <span data-ttu-id="7fa9a-118">시작하려면 Visual Studio에서 SQL Server 개체 탐색기를 열고 SQL 데이터 웨어하우스 데이터베이스를 호스팅할 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-118">To start, open SQL Server Object Explorer in Visual Studio and connect to the server that will host your SQL Data Warehouse database.</span></span>  <span data-ttu-id="7fa9a-119">연결한 후에는 **마스터** 데이터베이스에 대해 다음 SQL 명령을 실행하여 SQL 데이터 웨어하우스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-119">Once connected, you can create a SQL Data Warehouse by running the following SQL command against the **master** database.</span></span>  <span data-ttu-id="7fa9a-120">이 명령은 서비스 목표 DW400이 있는 MySqlDwDb 데이터베이스를 만들고 데이터베이스가 최대 10TB까지 증대될 수 있게 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-120">This command creates the database MySqlDwDb with a Service Objective of DW400 and allow the database to grow to a maximum size of 10 TB.</span></span>

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a><span data-ttu-id="7fa9a-121">sqlcmd로 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="7fa9a-121">Create a database with sqlcmd</span></span>
<span data-ttu-id="7fa9a-122">또는 명령 프롬프트에서 다음을 실행하여 sqlcmd로 동일한 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-122">Alternatively, you can run the same command with sqlcmd by running the following at a command prompt.</span></span>

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

<span data-ttu-id="7fa9a-123">지정되지 않은 경우 기본 데이터 정렬은 COLLATE SQL_Latin1_General_CP1_CI_AS입니다.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-123">The default collation when not specified is COLLATE SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="7fa9a-124">`MAXSIZE` 는 250GB~240TB 사이가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-124">The `MAXSIZE` can be between 250 GB and 240 TB.</span></span>  <span data-ttu-id="7fa9a-125">`SERVICE_OBJECTIVE`는 DW100~DW2000 [DWU][DWU] 사이가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-125">The `SERVICE_OBJECTIVE` can be between DW100 and DW2000 [DWU][DWU].</span></span>  <span data-ttu-id="7fa9a-126">유효한 모든 값의 목록은 [데이터베이스 만들기][CREATE DATABASE]에 대한 MSDN 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-126">For a list of all valid values, see the MSDN documentation for [CREATE DATABASE][CREATE DATABASE].</span></span>  <span data-ttu-id="7fa9a-127">MAXSIZE와 SERVICE_OBJECTIVE는 모두 [ALTER DATABASE][ALTER DATABASE] T-SQL 명령으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-127">Both the MAXSIZE and SERVICE_OBJECTIVE can be changed with an [ALTER DATABASE][ALTER DATABASE] T-SQL command.</span></span>  <span data-ttu-id="7fa9a-128">생성 후에 데이터베이스의 데이터 정렬을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-128">The collation of a database cannot be changed after creation.</span></span>   <span data-ttu-id="7fa9a-129">SERVICE_OBJECTIVE를 변경하면 DWU의 변경으로 인해 서비스가 재시작되어 진행 중인 모든 쿼리가 취소될 수 있으므로 주의가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-129">Caution should be used when changing the SERVICE_OBJECTIVE as changing DWU causes a restart of services, which cancels all queries in flight.</span></span>  <span data-ttu-id="7fa9a-130">MAXSIZE 변경은 간단한 메타데이터 작업이므로 서비스를 다시 시작하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-130">Changing MAXSIZE does not restart services as it is just a simple metadata operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fa9a-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7fa9a-131">Next steps</span></span>
<span data-ttu-id="7fa9a-132">SQL Data Warehouse에서 프로비전을 완료했으면 [샘플 데이터를 로드][load sample data]하거나 [개발][develop], [로드][load] 또는 [마이그레이션][migrate] 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fa9a-132">After your SQL Data Warehouse has finished provisioning you can [load sample data][load sample data] or check out how to [develop][develop], [load][load], or [migrate][migrate].</span></span>

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how to create a SQL Data Warehouse from the Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with the Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how to create a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--MSDN references-->
[CREATE DATABASE]: https://msdn.microsoft.com/library/mt204021.aspx
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F

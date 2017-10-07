---
title: "t s q L로 SQL 데이터 웨어하우스 aaaCreate | Microsoft Docs"
description: "어떻게 toocreate는 Azure SQL 데이터는 t s q l을 웨어하우스에 대해 알아봅니다"
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
ms.openlocfilehash: 81ef59a66c61452ff8a2aca29837f155e87d017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a><span data-ttu-id="6244a-103">TRANSACT-SQL(TSQL)를 사용하여 SQL 데이터 웨어하우스 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="6244a-103">Create a SQL Data Warehouse database by using Transact-SQL (TSQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6244a-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="6244a-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="6244a-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="6244a-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="6244a-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6244a-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="6244a-107">이 문서에서는 어떻게 toocreate SQL 데이터 웨어하우스 T-SQL을 사용 하 여 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6244a-107">This article shows you how toocreate a SQL Data Warehouse using T-SQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6244a-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6244a-108">Prerequisites</span></span>
<span data-ttu-id="6244a-109">시작 tooget를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6244a-109">tooget started, you need:</span></span>

* <span data-ttu-id="6244a-110">**Azure 계정**: 방문 [Azure 무료 평가판] [ Azure Free Trial] 또는 [MSDN Azure 크레딧을] [ MSDN Azure Credits] toocreate 계정.</span><span class="sxs-lookup"><span data-stu-id="6244a-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="6244a-111">**Azure SQL server**: [Azure 포털 hello로 Azure SQL 데이터베이스 논리 서버는 만들기]를 참조 [Azure SQL 데이터베이스 논리 서버 hello Azure 포털으로 만들기] [PowerShell을 사용한 Azure SQL 데이터베이스 논리 서버 만들기] 또는 [Azure SQL 만들기 PowerShell과 함께 데이터베이스 논리 서버]에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="6244a-111">**Azure SQL server**:  See [Create an Azure SQL Database logical server with hello Azure Portal][Create an Azure SQL Database logical server with hello Azure Portal] or [Create an Azure SQL Database logical server with PowerShell][Create an Azure SQL Database logical server with PowerShell] for more details.</span></span>
* <span data-ttu-id="6244a-112">**리소스 그룹**: hello 동일한 리소스와 Azure SQL server 그룹 또는 참조를 사용 하거나 [어떻게 toocreate 리소스 그룹][how toocreate a resource group]합니다.</span><span class="sxs-lookup"><span data-stu-id="6244a-112">**Resource group**: Either use hello same resource group as your Azure SQL server or see [how toocreate a resource group][how toocreate a resource group].</span></span>
* <span data-ttu-id="6244a-113">**환경 tooexecute T-SQL**: 사용할 수 있습니다 [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], 또는 [SSMS] [ SSMS] tooexecute T-SQL 합니다.</span><span class="sxs-lookup"><span data-stu-id="6244a-113">**Environment tooexecute T-SQL**: You can use [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], or [SSMS][SSMS] tooexecute T-SQL.</span></span>

> [!NOTE]
> <span data-ttu-id="6244a-114">SQL 데이터 웨어하우스를 만들면 새로운 유료 서비스가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6244a-114">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="6244a-115">가격 책정에 대한 자세한 내용은 [SQL Data Warehouse 가격 책정][SQL Data Warehouse pricing]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6244a-115">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-database-with-visual-studio"></a><span data-ttu-id="6244a-116">Visual Studio를 사용하여 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="6244a-116">Create a database with Visual Studio</span></span>
<span data-ttu-id="6244a-117">새 tooVisual Studio 인 경우 hello 문서 참조 [Azure SQL 데이터 웨어하우스 쿼리 (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]합니다.</span><span class="sxs-lookup"><span data-stu-id="6244a-117">If you are new tooVisual Studio, see hello article [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span></span>  <span data-ttu-id="6244a-118">toostart, Visual Studio에서 SQL Server 개체 탐색기를 열고 SQL 데이터 웨어하우스 데이터베이스를 호스팅할 toohello 서버에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6244a-118">toostart, open SQL Server Object Explorer in Visual Studio and connect toohello server that will host your SQL Data Warehouse database.</span></span>  <span data-ttu-id="6244a-119">연결 되 면 hello 다음 hello에 대해 SQL 명령을 실행 하 여 SQL 데이터 웨어하우스를 만들 수 있습니다 **마스터** 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="6244a-119">Once connected, you can create a SQL Data Warehouse by running hello following SQL command against hello **master** database.</span></span>  <span data-ttu-id="6244a-120">이 명령은 서비스 DW400 목표와 MySqlDwDb hello 데이터베이스를 만들고 hello 데이터베이스 toogrow tooa의 최대 크기 10TB를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6244a-120">This command creates hello database MySqlDwDb with a Service Objective of DW400 and allow hello database toogrow tooa maximum size of 10 TB.</span></span>

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a><span data-ttu-id="6244a-121">sqlcmd로 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="6244a-121">Create a database with sqlcmd</span></span>
<span data-ttu-id="6244a-122">또는 명령 프롬프트에서 다음을 실행 하 여 sqlcmd와 같은 명령을 hello hello를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6244a-122">Alternatively, you can run hello same command with sqlcmd by running hello following at a command prompt.</span></span>

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

<span data-ttu-id="6244a-123">hello 기본 데이터 정렬을 지정 하지 않은 경우에 COLLATE 정렬은 SQL_Latin1_General_CP1_CI_AS입니다.</span><span class="sxs-lookup"><span data-stu-id="6244a-123">hello default collation when not specified is COLLATE SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="6244a-124">hello `MAXSIZE` 250GB 240 TB 사이일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6244a-124">hello `MAXSIZE` can be between 250 GB and 240 TB.</span></span>  <span data-ttu-id="6244a-125">hello `SERVICE_OBJECTIVE` DW100 DW2000 사이일 수 있습니다 [DWU][DWU]합니다.</span><span class="sxs-lookup"><span data-stu-id="6244a-125">hello `SERVICE_OBJECTIVE` can be between DW100 and DW2000 [DWU][DWU].</span></span>  <span data-ttu-id="6244a-126">유효한 모든 값의 목록에 대 한 hello MSDN 설명서를 참조 하십시오. [CREATE DATABASE][CREATE DATABASE]합니다.</span><span class="sxs-lookup"><span data-stu-id="6244a-126">For a list of all valid values, see hello MSDN documentation for [CREATE DATABASE][CREATE DATABASE].</span></span>  <span data-ttu-id="6244a-127">Hello MAXSIZE와 SERVICE_OBJECTIVE는으로 변경할 수 있습니다는 [ALTER DATABASE] [ ALTER DATABASE] T-SQL 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="6244a-127">Both hello MAXSIZE and SERVICE_OBJECTIVE can be changed with an [ALTER DATABASE][ALTER DATABASE] T-SQL command.</span></span>  <span data-ttu-id="6244a-128">데이터베이스 데이터 정렬 hello를 만든 후 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6244a-128">hello collation of a database cannot be changed after creation.</span></span>   <span data-ttu-id="6244a-129">변경 hello SERVICE_OBJECTIVE DWU를 변경 하는 것 항공편의 모든 쿼리를 취소 된 서비스의 다시 시작 하면 때 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6244a-129">Caution should be used when changing hello SERVICE_OBJECTIVE as changing DWU causes a restart of services, which cancels all queries in flight.</span></span>  <span data-ttu-id="6244a-130">MAXSIZE 변경은 간단한 메타데이터 작업이므로 서비스를 다시 시작하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6244a-130">Changing MAXSIZE does not restart services as it is just a simple metadata operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6244a-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6244a-131">Next steps</span></span>
<span data-ttu-id="6244a-132">SQL 데이터 웨어하우스 하면 프로 비전 완료 된 후 [샘플 데이터를 로드] [ load sample data] 방법에 대해 너무 확인 또는[개발][develop], [로드][load], 또는 [마이그레이션할][migrate]합니다.</span><span class="sxs-lookup"><span data-stu-id="6244a-132">After your SQL Data Warehouse has finished provisioning you can [load sample data][load sample data] or check out how too[develop][develop], [load][load], or [migrate][migrate].</span></span>

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how toocreate a SQL Data Warehouse from hello Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
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

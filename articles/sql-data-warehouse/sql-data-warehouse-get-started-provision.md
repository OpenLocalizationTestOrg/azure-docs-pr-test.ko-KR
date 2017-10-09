---
title: "hello Azure 포털에서에서 SQL 데이터 웨어하우스 aaaCreate | Microsoft Docs"
description: "Toocreate에 Azure SQL 데이터 웨어하우스는 Azure 포털을 hello 하는 방법에 대해 알아봅니다"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 552e496e-d560-419c-9996-6bbc80c521cb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: f5be6e3f2936e3af9d099854a468f8ce66fd8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a><span data-ttu-id="05570-103">Azure SQL 데이터 웨어하우스 만들기</span><span class="sxs-lookup"><span data-stu-id="05570-103">Create an Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="05570-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="05570-104">Azure portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="05570-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="05570-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="05570-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="05570-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="05570-107">이 자습서에서는 Azure 포털 toocreate AdventureWorksDW 예제 데이터베이스를 포함 하는 SQL 데이터 웨어하우스 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05570-107">This tutorial uses hello Azure portal toocreate a SQL Data Warehouse that contains an AdventureWorksDW sample database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05570-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="05570-108">Prerequisites</span></span>
<span data-ttu-id="05570-109">시작 tooget를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05570-109">tooget started, you need:</span></span>

* <span data-ttu-id="05570-110">**Azure 계정**: 방문 [Azure 무료 평가판] [ Azure Free Trial] 또는 [MSDN Azure 크레딧을] [ MSDN Azure Credits] toocreate 계정.</span><span class="sxs-lookup"><span data-stu-id="05570-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="05570-111">**Azure SQL server**: 참조 [hello Azure 포털에서 Azure SQL 데이터베이스 만들기] [ Create an Azure SQL database in hello Azure portal] 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="05570-111">**Azure SQL server**:  See [Create an Azure SQL database with hello Azure portal][Create an Azure SQL database in hello Azure portal] for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="05570-112">SQL 데이터 웨어하우스를 만들면 새로운 유료 서비스가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05570-112">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="05570-113">자세한 내용은 [SQL Data Warehouse 가격 책정][SQL Data Warehouse pricing]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05570-113">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="05570-114">SQL 데이터 웨어하우스 만들기</span><span class="sxs-lookup"><span data-stu-id="05570-114">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="05570-115">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="05570-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="05570-116">**+ 새로 만들기** > **데이터베이스** > **SQL Data Warehouse**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05570-116">Click **+ New** > **Databases** > **SQL Data Warehouse**.</span></span>

    ![생성](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. <span data-ttu-id="05570-118">Hello에 **SQL 데이터 웨어하우스** 블레이드를 필요에 따라 hello 정보를 입력 '만들기' toocreate 다음 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="05570-118">In hello **SQL Data Warehouse** blade, fill in hello information needed, then press 'Create' toocreate.</span></span>

    ![데이터베이스 만들기](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * <span data-ttu-id="05570-120">**서버**: 먼저 서버를 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="05570-120">**Server**: We recommend you select your server first.</span></span>  
   * <span data-ttu-id="05570-121">**데이터베이스 이름**:는 사용 되는 tooreference hello SQL 데이터 웨어하우스 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="05570-121">**Database name**: hello name that is used tooreference hello SQL Data Warehouse.</span></span>  <span data-ttu-id="05570-122">고유 toohello 서버 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05570-122">It must be unique toohello server.</span></span>
   * <span data-ttu-id="05570-123">**성능**: 400[DWUs][DWU]로 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="05570-123">**Performance**: We recommend starting with 400 [DWUs][DWU].</span></span> <span data-ttu-id="05570-124">만든 후 위나 아래로 tooadjust hello 성능 데이터 웨어하우스 또는 소수를 마우스 오른쪽 이나 왼쪽 hello 슬라이더 toohello 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05570-124">You can move hello slider toohello left or right tooadjust hello performance of your data warehouse, or scale up or down after creation.</span></span>  <span data-ttu-id="05570-125">Dwu에 대 한 자세한 toolearn에 우리의 설명서를 참조 하십시오. [배율](sql-data-warehouse-manage-compute-overview.md) 또는 [가격 책정 페이지][SQL Data Warehouse pricing]합니다.</span><span class="sxs-lookup"><span data-stu-id="05570-125">toolearn more about DWUs, see our documentation on [scaling](sql-data-warehouse-manage-compute-overview.md) or our [pricing page][SQL Data Warehouse pricing].</span></span>
   * <span data-ttu-id="05570-126">**구독**: 선택 hello [구독] 있는이 SQL 데이터 웨어하우스를 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05570-126">**Subscription**: Select hello [subscription] that this SQL Data Warehouse will bill to.</span></span>
   * <span data-ttu-id="05570-127">**리소스 그룹**: [리소스 그룹] [ Resource group] Azure 리소스 컬렉션을 관리 하는 컨테이너 설계 toohelp 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05570-127">**Resource group**: [Resource groups][Resource group] are containers designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="05570-128">[리소스 그룹](../azure-resource-manager/resource-group-overview.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="05570-128">Learn more about [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="05570-129">**원본 선택**: **원본 선택** > **샘플**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05570-129">**Select source**: Click **Select source** > **Sample**.</span></span> <span data-ttu-id="05570-130">Azure hello를 자동으로 채우려고 **선택 샘플** AdventureWorksDW 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="05570-130">Azure automatically populates hello **Select sample** option with AdventureWorksDW.</span></span>

   > [!NOTE]
   > <span data-ttu-id="05570-131">SQL 데이터 웨어하우스에 대 한 hello 기본 데이터 정렬은 SQL_Latin1_General_CP1_CI_AS입니다.</span><span class="sxs-lookup"><span data-stu-id="05570-131">hello default collation for a SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS.</span></span> <span data-ttu-id="05570-132">다른 데이터 정렬이 필요한 경우 [T-SQL] [ T-SQL] 서로 다른 데이터 정렬으로 사용 되는 toocreate hello 데이터베이스가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05570-132">If a different collation is needed, [T-SQL][T-SQL] can be used toocreate hello database with a different collation.</span></span>
   >
   >

1. <span data-ttu-id="05570-133">클릭 **만들기** toocreate SQL 데이터 웨어하우스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="05570-133">Click **Create** toocreate your SQL Data Warehouse.</span></span>
2. <span data-ttu-id="05570-134">몇 분 정도 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="05570-134">Wait for a few minutes.</span></span> <span data-ttu-id="05570-135">데이터 웨어하우스 준비 되 면 있습니다 돌아가야 toohello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="05570-135">When your data warehouse is ready, you should be returned toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="05570-136">SQL 데이터 웨어하우스 SQL 데이터베이스를 아래 나열 된 대시보드에서 찾을 수도 있고 hello 리소스에서 해당 사용한 toocreate 그룹 것입니다.</span><span class="sxs-lookup"><span data-stu-id="05570-136">You can find your SQL Data Warehouse on your dashboard, listed under your SQL Databases, or in hello resource group that you used toocreate it.</span></span>

    ![포털 보기](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="05570-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="05570-138">Next steps</span></span>
<span data-ttu-id="05570-139">SQL 데이터 웨어하우스를 만든 준비가 너무[연결](sql-data-warehouse-connect-overview.md) 하 고 쿼리를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="05570-139">Now that you have created a SQL Data Warehouse, you are ready too[Connect](sql-data-warehouse-connect-overview.md) and begin querying.</span></span>

<span data-ttu-id="05570-140">SQL 데이터 웨어하우스로 tooload 데이터 참조 hello [개요 로드](sql-data-warehouse-overview-load.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="05570-140">tooload data into SQL Data Warehouse, see hello [loading overview](sql-data-warehouse-overview-load.md).</span></span>

<span data-ttu-id="05570-141">기존 데이터베이스 tooSQL 데이터 웨어하우스 toomigrate을 시도 하는 경우 참조 hello [마이그레이션 개요](sql-data-warehouse-overview-migrate.md) 사용 또는 [마이그레이션 유틸리티](sql-data-warehouse-migrate-migration-utility.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="05570-141">If you are trying toomigrate an existing database tooSQL Data Warehouse, see hello [Migration overview](sql-data-warehouse-overview-migrate.md) or use [Migration Utility](sql-data-warehouse-migrate-migration-utility.md).</span></span>

<span data-ttu-id="05570-142">Transact-SQL을 사용하여 방화벽 규칙을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05570-142">Firewall rules can also be configured using Transact-SQL.</span></span> <span data-ttu-id="05570-143">자세한 내용은 [sp_set_firewall_rule][sp_set_firewall_rule] 및 [sp_set_database_firewall_rule][sp_set_database_firewall_rule]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05570-143">For more information, see [sp_set_firewall_rule][sp_set_firewall_rule] and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="05570-144">Hello에 좋은 생각 toolook 이기도 [모범 사례][Best practices]합니다.</span><span class="sxs-lookup"><span data-stu-id="05570-144">It's also a great idea toolook at hello [Best practices][Best practices].</span></span>

<!--Article references-->
[Create an Azure SQL database in hello Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
[구독]: ../azure-glossary-cloud-terminology.md#subscription
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F

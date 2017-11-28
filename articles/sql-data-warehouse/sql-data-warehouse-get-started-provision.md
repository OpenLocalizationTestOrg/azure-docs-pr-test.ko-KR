---
title: "Azure 포털에서 SQL Data Warehouse 만들기 | Microsoft Docs"
description: "Azure 포털에서 SQL 데이터 웨어하우스를 만드는 방법을 알아봅니다."
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
ms.openlocfilehash: 24ed2d8bad3090e378acf2a42fb909dee0a8517b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a><span data-ttu-id="2e322-103">Azure SQL 데이터 웨어하우스 만들기</span><span class="sxs-lookup"><span data-stu-id="2e322-103">Create an Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2e322-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2e322-104">Azure portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="2e322-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="2e322-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="2e322-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e322-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="2e322-107">이 자습서에서는 Azure 포털을 사용하여 AdventureWorksDW 샘플 데이터베이스를 포함하는 SQL 데이터 웨어하우스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-107">This tutorial uses the Azure portal to create a SQL Data Warehouse that contains an AdventureWorksDW sample database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e322-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2e322-108">Prerequisites</span></span>
<span data-ttu-id="2e322-109">시작하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-109">To get started, you need:</span></span>

* <span data-ttu-id="2e322-110">**Azure 계정**: [Azure 무료 평가판][Azure Free Trial] 또는 [MSDN Azure 크레딧][MSDN Azure Credits]을 방문하여 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span></span>
* <span data-ttu-id="2e322-111">**Azure SQL Server**: 자세한 내용은 [Azure Portal을 사용하여 Azure SQL Database 만들기][Create an Azure SQL database in the Azure portal]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e322-111">**Azure SQL server**:  See [Create an Azure SQL database with the Azure portal][Create an Azure SQL database in the Azure portal] for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="2e322-112">SQL Data Warehouse를 만들면 새로운 유료 서비스가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-112">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="2e322-113">자세한 내용은 [SQL Data Warehouse 가격 책정][SQL Data Warehouse pricing]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e322-113">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="2e322-114">SQL 데이터 웨어하우스 만들기</span><span class="sxs-lookup"><span data-stu-id="2e322-114">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="2e322-115">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2e322-116">**+ 새로 만들기** > **데이터베이스** > **SQL Data Warehouse**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-116">Click **+ New** > **Databases** > **SQL Data Warehouse**.</span></span>

    ![생성](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. <span data-ttu-id="2e322-118">**SQL 데이터 웨어하우스** 블레이드에 필요한 정보를 입력한 다음 '만들기'를 눌러서 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-118">In the **SQL Data Warehouse** blade, fill in the information needed, then press 'Create' to create.</span></span>

    ![데이터베이스 만들기](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * <span data-ttu-id="2e322-120">**서버**: 먼저 서버를 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-120">**Server**: We recommend you select your server first.</span></span>  
   * <span data-ttu-id="2e322-121">**데이터베이스 이름**: SQL 데이터 웨어하우스를 참조하는 데 사용되는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-121">**Database name**: The name that is used to reference the SQL Data Warehouse.</span></span>  <span data-ttu-id="2e322-122">서버에 대해 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-122">It must be unique to the server.</span></span>
   * <span data-ttu-id="2e322-123">**성능**: 400[DWUs][DWU]로 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-123">**Performance**: We recommend starting with 400 [DWUs][DWU].</span></span> <span data-ttu-id="2e322-124">슬라이더를 왼쪽이나 오른쪽으로 이동하여 데이터 웨어하우스의 성능을 조정하거나, 만든 후에 확장 또는 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-124">You can move the slider to the left or right to adjust the performance of your data warehouse, or scale up or down after creation.</span></span>  <span data-ttu-id="2e322-125">DWU에 대한 자세한 내용은 [확장](sql-data-warehouse-manage-compute-overview.md) 또는 [가격 책정 페이지][SQL Data Warehouse pricing]에서 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e322-125">To learn more about DWUs, see our documentation on [scaling](sql-data-warehouse-manage-compute-overview.md) or our [pricing page][SQL Data Warehouse pricing].</span></span>
   * <span data-ttu-id="2e322-126">**구독**: SQL 데이터 웨어하우스가 청구될 [구독] 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-126">**Subscription**: Select the [subscription] that this SQL Data Warehouse will bill to.</span></span>
   * <span data-ttu-id="2e322-127">**리소스 그룹**: [리소스 그룹][Resource group]은 컨테이너로, Azure 리소스의 컬렉션을 관리할 수 있도록 디자인되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-127">**Resource group**: [Resource groups][Resource group] are containers designed to help you manage a collection of Azure resources.</span></span> <span data-ttu-id="2e322-128">[리소스 그룹](../azure-resource-manager/resource-group-overview.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-128">Learn more about [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="2e322-129">**원본 선택**: **원본 선택** > **샘플**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-129">**Select source**: Click **Select source** > **Sample**.</span></span> <span data-ttu-id="2e322-130">Azure에서는 AdventureWorksDW를 사용하여 **선택 샘플** 옵션을 자동으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-130">Azure automatically populates the **Select sample** option with AdventureWorksDW.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2e322-131">SQL 데이터 웨어하우스에 대한 기본 데이터 정렬은 SQL_Latin1_General_CP1_CI_AS입니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-131">The default collation for a SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS.</span></span> <span data-ttu-id="2e322-132">다른 데이터 정렬이 필요한 경우 다른 데이터 정렬이 포함된 데이터베이스를 만드는 데 [T-SQL][T-SQL]을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-132">If a different collation is needed, [T-SQL][T-SQL] can be used to create the database with a different collation.</span></span>
   >
   >

1. <span data-ttu-id="2e322-133">**만들기** 를 클릭하여 SQL 데이터 웨어하우스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-133">Click **Create** to create your SQL Data Warehouse.</span></span>
2. <span data-ttu-id="2e322-134">몇 분 정도 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-134">Wait for a few minutes.</span></span> <span data-ttu-id="2e322-135">데이터 웨어하우스가 준비되면 [Azure Portal](https://portal.azure.com)로 돌아가야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-135">When your data warehouse is ready, you should be returned to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2e322-136">생성 시 사용한 리소스 그룹 또는 SQL 데이터베이스 아래 나열된, 대시보드에서 SQL 데이터 웨어하우스를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-136">You can find your SQL Data Warehouse on your dashboard, listed under your SQL Databases, or in the resource group that you used to create it.</span></span>

    ![포털 보기](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="2e322-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2e322-138">Next steps</span></span>
<span data-ttu-id="2e322-139">SQL 데이터 웨어하우스를 만들었으므로 [연결](sql-data-warehouse-connect-overview.md) 하여 쿼리할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-139">Now that you have created a SQL Data Warehouse, you are ready to [Connect](sql-data-warehouse-connect-overview.md) and begin querying.</span></span>

<span data-ttu-id="2e322-140">SQL 데이터 웨어하우스로 데이터를 로드하는 경우 [로드 개요](sql-data-warehouse-overview-load.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e322-140">To load data into SQL Data Warehouse, see the [loading overview](sql-data-warehouse-overview-load.md).</span></span>

<span data-ttu-id="2e322-141">기존 데이터베이스를 SQL Data Warehouse로 마이그레이션하려는 경우 [마이그레이션 개요](sql-data-warehouse-overview-migrate.md)를 참조하거나 [마이그레이션 유틸리티](sql-data-warehouse-migrate-migration-utility.md)를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="2e322-141">If you are trying to migrate an existing database to SQL Data Warehouse, see the [Migration overview](sql-data-warehouse-overview-migrate.md) or use [Migration Utility](sql-data-warehouse-migrate-migration-utility.md).</span></span>

<span data-ttu-id="2e322-142">Transact-SQL을 사용하여 방화벽 규칙을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-142">Firewall rules can also be configured using Transact-SQL.</span></span> <span data-ttu-id="2e322-143">자세한 내용은 [sp_set_firewall_rule][sp_set_firewall_rule] 및 [sp_set_database_firewall_rule][sp_set_database_firewall_rule]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e322-143">For more information, see [sp_set_firewall_rule][sp_set_firewall_rule] and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="2e322-144">[모범 사례][Best practices]를 살펴보는 것도 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2e322-144">It's also a great idea to look at the [Best practices][Best practices].</span></span>

<!--Article references-->
[Create an Azure SQL database in the Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
<span data-ttu-id="2e322-145">[구독]: ../azure-glossary-cloud-terminology.md#subscription</span><span class="sxs-lookup"><span data-stu-id="2e322-145">[subscription]: ../azure-glossary-cloud-terminology.md#subscription</span></span>
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F

---
title: "PowerShell을 사용하여 SQL Data Warehouse 만들기 | Microsoft Docs"
description: "PowerShell을 사용하여 SQL 데이터 웨어하우스 만들기"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 97434863-7938-4129-8949-5a119f5949e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: a763f1c600c1a3f37cb565a8eb7db3c3f27dcf75
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-sql-data-warehouse-using-powershell"></a><span data-ttu-id="da255-103">PowerShell을 사용하여 SQL 데이터 웨어하우스 만들기</span><span class="sxs-lookup"><span data-stu-id="da255-103">Create SQL Data Warehouse using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="da255-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="da255-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="da255-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="da255-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="da255-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="da255-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="da255-107">이 문서에서는 PowerShell을 사용하여 SQL 데이터 웨어하우스를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="da255-107">This article shows you how to create a SQL Data Warehouse using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da255-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="da255-108">Prerequisites</span></span>
<span data-ttu-id="da255-109">시작하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="da255-109">To get started, you need:</span></span>

* <span data-ttu-id="da255-110">**Azure 계정**: [Azure 무료 평가판][Azure Free Trial] 또는 [MSDN Azure 크레딧][MSDN Azure Credits]을 방문하여 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da255-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span></span>
* <span data-ttu-id="da255-111">**Azure SQL Server**: 자세한 내용은 [Azure Portal에서 Azure SQL Database 만들기][Create an Azure SQL database in the Azure Portal] 또는 [PowerShell을 사용하여 Azure SQL Database 만들기][Create an Azure SQL database with PowerShell]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da255-111">**Azure SQL server**:  See [Create an Azure SQL database in the Azure Portal][Create an Azure SQL database in the Azure Portal] or [Create an Azure SQL database with PowerShell][Create an Azure SQL database with PowerShell] for more details.</span></span>
* <span data-ttu-id="da255-112">**리소스 그룹**: Azure SQL 서버와 동일한 리소스 그룹을 사용하거나 [리소스 그룹을 만드는 방법](../azure-resource-manager/resource-group-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da255-112">**Resource group**: Either use the same resource group as your Azure SQL server or see [how to create a resource group](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="da255-113">**PowerShell 버전 1.0.3 이상**: **Get-Module -ListAvailable -Name Azure**를 실행하여 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da255-113">**PowerShell version 1.0.3 or greater**:  You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="da255-114">최신 버전은 [Microsoft 웹 플랫폼 설치 관리자][Microsoft Web Platform Installer]를 통해 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da255-114">The latest version can be installed from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="da255-115">최신 버전 설치에 대한 자세한 내용은 [Azure PowerShell 설치 및 구성 방법][How to install and configure Azure PowerShell]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da255-115">For more information on installing the latest version, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>

> [!NOTE]
> <span data-ttu-id="da255-116">SQL 데이터 웨어하우스를 만들면 새로운 유료 서비스가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da255-116">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="da255-117">가격 책정에 대한 자세한 내용은 [SQL Data Warehouse 가격 책정][SQL Data Warehouse pricing]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da255-117">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="da255-118">SQL 데이터 웨어하우스 만들기</span><span class="sxs-lookup"><span data-stu-id="da255-118">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="da255-119">Windows PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="da255-119">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="da255-120">이 cmdlet을 실행하여 Azure 리소스 관리자에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="da255-120">Run this cmdlet to login to Azure Resource Manager.</span></span>

    ```Powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="da255-121">현재 세션에 사용하려는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da255-121">Select the subscription you want to use for your current session.</span></span>

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. <span data-ttu-id="da255-122">데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da255-122">Create database.</span></span> <span data-ttu-id="da255-123">이 예제에서는 서비스 목표 수준이 "DW400"이고 이름이 "mynewsqldw"인 데이터베이스를 만들고, 리소스 그룹 "mywesteuroperesgp1"에 있는 이름이 "sqldwserver1"인 서버에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="da255-123">This example creates a database named "mynewsqldw", with service objective level "DW400", to the server named "sqldwserver1", which is in the resource group named "mywesteuroperesgp1".</span></span>

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

<span data-ttu-id="da255-124">필수 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="da255-124">Required Parameters are:</span></span>

* <span data-ttu-id="da255-125">**RequestedServiceObjectiveName**: 요청 중인 [DWU][DWU]의 양입니다.</span><span class="sxs-lookup"><span data-stu-id="da255-125">**RequestedServiceObjectiveName**: The amount of [DWU][DWU] you are requesting.</span></span>  <span data-ttu-id="da255-126">지원되는 값은 DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 및 DW6000입니다.</span><span class="sxs-lookup"><span data-stu-id="da255-126">Supported values are: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000, and DW6000.</span></span>
* <span data-ttu-id="da255-127">**DatabaseName**: 만들려는 SQL 데이터 웨어하우스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="da255-127">**DatabaseName**: The name of the SQL Data Warehouse that you are creating.</span></span>
* <span data-ttu-id="da255-128">**ServerName**: 만들기에 사용하는 서버의 이름입니다(V12이어야 함).</span><span class="sxs-lookup"><span data-stu-id="da255-128">**ServerName**: The name of the server that you are using for creation (must be V12).</span></span>
* <span data-ttu-id="da255-129">**ResourceGroupName**: 사용 중인 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="da255-129">**ResourceGroupName**: Resource group you are using.</span></span>  <span data-ttu-id="da255-130">구독에서 사용 가능한 리소스 그룹을 찾으려면 Get-AzureResource를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="da255-130">To find available resource groups in your subscription use Get-AzureResource.</span></span>
* <span data-ttu-id="da255-131">**Edition**: SQL 데이터 웨어하우스를 만들려면 "DataWarehouse"여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da255-131">**Edition**: Must be "DataWarehouse" to create a SQL Data Warehouse.</span></span>

<span data-ttu-id="da255-132">선택적 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="da255-132">Optional Parameters are:</span></span>

* <span data-ttu-id="da255-133">**CollationName**: 지정되지 않은 경우 기본 데이터 정렬은 SQL_Latin1_General_CP1_CI_AS입니다.</span><span class="sxs-lookup"><span data-stu-id="da255-133">**CollationName**: The default collation if not specified is SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="da255-134">데이터베이스에서 데이터 정렬을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da255-134">Collation cannot be changed on a database.</span></span>
* <span data-ttu-id="da255-135">**MaxSizeBytes**: 데이터베이스의 기본 최대 크기는 10GB입니다.</span><span class="sxs-lookup"><span data-stu-id="da255-135">**MaxSizeBytes**: The default max size of a database is 10 GB.</span></span>

<span data-ttu-id="da255-136">매개 변수 옵션에 대한 자세한 내용은 [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase] 및 [데이터베이스 만들기(Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da255-136">For more details on the parameter options, see [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase] and [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span></span>

## <a name="next-steps"></a><span data-ttu-id="da255-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="da255-137">Next steps</span></span>
<span data-ttu-id="da255-138">SQL Data Warehouse에서 프로비전을 완료한 후 [샘플 데이터를 로드][loading sample data]하거나 [개발][develop], [로드][load] 또는 [마이그레이션][migrate]을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da255-138">After your SQL Data Warehouse has finished provisioning you may want to try [loading sample data][loading sample data] or check out how to [develop][develop], [load][load], or [migrate][migrate].</span></span>

<span data-ttu-id="da255-139">SQL Data Warehouse를 프로그래밍 방식으로 관리하는 방법에 대한 자세한 내용은 [PowerShell cmdlet 및 REST API][PowerShell cmdlets and REST APIs]사용 방법에 관한 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da255-139">If you're interested in more on how to manage SQL Data Warehouse programmatically, check out our article on how to use [PowerShell cmdlets and REST APIs][PowerShell cmdlets and REST APIs].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how to create a SQL Data Warehouse from the Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in the Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how to create a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F

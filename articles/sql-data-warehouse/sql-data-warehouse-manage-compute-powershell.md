---
title: "Azure SQL Data Warehouse의 계산 능력 관리(PowerShell) | Microsoft Docs"
description: "계산 능력을 관리하는 PowerShell 작업 DWU를 조정하여 계산 리소스 크기를 조정합니다. 또는 계산 리소스를 일지 중지한 다음 다시 시작하여 비용을 절감합니다."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 8354a3c1-4e04-4809-933f-db414a8c74dc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 6a185d96447c2e1b0b463439dd062081e783da5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="b65ea-105">Azure SQL Data Warehouse의 계산 능력 관리(PowerShell)</span><span class="sxs-lookup"><span data-stu-id="b65ea-105">Manage compute power in Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b65ea-106">개요</span><span class="sxs-lookup"><span data-stu-id="b65ea-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="b65ea-107">포털</span><span class="sxs-lookup"><span data-stu-id="b65ea-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="b65ea-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b65ea-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="b65ea-109">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="b65ea-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="b65ea-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="b65ea-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a><span data-ttu-id="b65ea-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="b65ea-111">Before you begin</span></span>
### <a name="install-the-latest-version-of-azure-powershell"></a><span data-ttu-id="b65ea-112">Azure PowerShell 최신 버전 설치</span><span class="sxs-lookup"><span data-stu-id="b65ea-112">Install the latest version of Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="b65ea-113">SQL Data Warehouse에서 Azure PowerShell을 사용하려면 Azure PowerShell 버전 1.0.3 이상을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-113">To use Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="b65ea-114">현재 버전을 확인하려면 **Get-Module -ListAvailable -Name Azure**명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-114">To verify your current version run the command **Get-Module -ListAvailable -Name Azure**.</span></span> <span data-ttu-id="b65ea-115">[Microsoft 웹 플랫폼 설치 관리자][Microsoft Web Platform Installer]를 통해 최신 버전을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-115">You can install the latest version from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="b65ea-116">자세한 내용은 [Azure PowerShell 설치 및 구성 방법][How to install and configure Azure PowerShell]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b65ea-116">For more information, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="b65ea-117">Azure PowerShell Cmdlet 시작</span><span class="sxs-lookup"><span data-stu-id="b65ea-117">Get started with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="b65ea-118">시작하기:</span><span class="sxs-lookup"><span data-stu-id="b65ea-118">To get started:</span></span>

1. <span data-ttu-id="b65ea-119">Azure PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-119">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="b65ea-120">PowerShell 프롬프트에서 다음 명령을 실행하여 Azure Resource Manager에 로그인하고 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-120">At the PowerShell prompt, run these commands to sign in to the Azure Resource Manager and select your subscription.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="b65ea-121">계산 능력 크기 조정</span><span class="sxs-lookup"><span data-stu-id="b65ea-121">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="b65ea-122">DWU를 변경하려면 [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase] PowerShell cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-122">To change the DWUs, use the [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase] PowerShell cmdlet.</span></span> <span data-ttu-id="b65ea-123">다음 예제에서는 MyServer에서 호스팅되는 MySQLDW 데이터베이스에 대한 서비스 수준 목표를 DW1000으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-123">The following example sets the service level objective to DW1000 for the database MySQLDW which is hosted on server MyServer.</span></span>

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="b65ea-124">계산 일시 중지</span><span class="sxs-lookup"><span data-stu-id="b65ea-124">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="b65ea-125">데이터베이스를 일시 중지하려면 [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase] cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-125">To pause a database, use the [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="b65ea-126">다음 예에서는 Server01 서버에서 호스트하는 이름이 Database02인 데이터베이스를 일시 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-126">The following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="b65ea-127">서버는 이름이 ResourceGroup1인 Azure 리소스 그룹 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-127">The server is in an Azure resource group named ResourceGroup1.</span></span>

> [!NOTE]
> <span data-ttu-id="b65ea-128">서버가 foo.database.windows.net인 경우 PowerShell cmdlet의 ServerName으로 "foo"를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-128">Note that if your server is foo.database.windows.net, use "foo" as the -ServerName in the PowerShell cmdlets.</span></span>
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="b65ea-129">다음 예에서는 이를 변형하여 데이터베이스를 $database 개체로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-129">A variation, this next example retrieves the database into the $database object.</span></span> <span data-ttu-id="b65ea-130">그런 다음 개체를 [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]에 파이프합니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-130">It then pipes the object to [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span> <span data-ttu-id="b65ea-131">결과는 resultDatabase 개체에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-131">The results are stored in the object resultDatabase.</span></span> <span data-ttu-id="b65ea-132">마지막 명령은 결과를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-132">The final command shows the results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="b65ea-133">계산 다시 시작</span><span class="sxs-lookup"><span data-stu-id="b65ea-133">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="b65ea-134">데이터베이스를 시작하려면 [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-134">To start a database, use the [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="b65ea-135">다음 예에서는 Server01 서버에서 호스팅되는 이름이 Database02인 데이터베이스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-135">The following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="b65ea-136">서버는 이름이 ResourceGroup1인 Azure 리소스 그룹 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-136">The server is in an Azure resource group named ResourceGroup1.</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="b65ea-137">다음 예에서는 이를 변형하여 데이터베이스를 $database 개체로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-137">A variation, this next example retrieves the database into the $database object.</span></span> <span data-ttu-id="b65ea-138">그런 다음 개체를 [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]에 파이프하고 결과를 $resultDatabase에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-138">It then pipes the object to [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] and stores the results in $resultDatabase.</span></span> <span data-ttu-id="b65ea-139">마지막 명령은 결과를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-139">The final command shows the results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="b65ea-140">데이터베이스 상태 확인</span><span class="sxs-lookup"><span data-stu-id="b65ea-140">Check database state</span></span>

<span data-ttu-id="b65ea-141">위의 예제에서와 같이 [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] cmdlet을 사용하여 데이터베이스에 대한 정보를 가져와서 상태를 확인할 뿐만 아니라 인수로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-141">As shown in the above examples, one can use [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] cmdlet to get information on a database, thereby checking the status, but also to use as an argument.</span></span> 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

<span data-ttu-id="b65ea-142">결과는 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-142">Which will result in something like</span></span> 

```powershell   
ResourceGroupName             : nytrg
ServerName                    : nytsvr
DatabaseName                  : nytdb
Location                      : West US
DatabaseId                    : 86461aae-8e3d-4ded-9389-ac9d4bc69bbb
Edition                       : DataWarehouse
CollationName                 : SQL_Latin1General_CP1CI_AS
CatalogCollation              :
MaxSizeBytes                  : 32212254720
Status                        : Online
CreationDate                  : 10/26/2016 4:33:14 PM
CurrentServiceObjectiveId     : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
CurrentServiceObjectiveName   : System2
RequestedServiceObjectiveId   : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
RequestedServiceObjectiveName :
ElasticPoolName               :
EarliestRestoreDate           : 1/1/0001 12:00:00 AM
```

<span data-ttu-id="b65ea-143">여기서 데이터베이스의 *상태*를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-143">Where you can then check to see the *Status* of the database.</span></span> <span data-ttu-id="b65ea-144">이 경우 이 데이터베이스가 온라인 상태인지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-144">In this case, you can see that this database is online.</span></span> 

<span data-ttu-id="b65ea-145">이 명령을 실행하면 온라인, 일시 중지 중, 다시 시작 중, 크기 조정 및 일시 중지됨의 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b65ea-145">When you run this command, you should receive a Status value of either Online, Pausing, Resuming, Scaling, and Paused.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="b65ea-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b65ea-146">Next steps</span></span>
<span data-ttu-id="b65ea-147">다른 관리 작업은 [관리 개요][Management overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b65ea-147">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Get-AzureRmSqlDatabase]: /powershell/servicemanagement/azure.sqldatabase/v1.6.1/get-azuresqldatabase

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[Azure portal]: http://portal.azure.com/

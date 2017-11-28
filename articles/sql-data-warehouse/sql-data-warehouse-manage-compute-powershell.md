---
title: "aaaManage 계산 능력이 Azure SQL 데이터 웨어하우스 (PowerShell)에서 | Microsoft Docs"
description: "PowerShell 작업 toomanage 전원을 계산 합니다. DWU를 조정하여 계산 리소스 크기를 조정합니다. 또는 일시 중지 및 재개 자원 toosave 비용을 계산 합니다."
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
ms.openlocfilehash: 8b379d4cf89570649767f6896d2c630d4f1111d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="8503f-105">Azure SQL Data Warehouse의 계산 능력 관리(PowerShell)</span><span class="sxs-lookup"><span data-stu-id="8503f-105">Manage compute power in Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8503f-106">개요</span><span class="sxs-lookup"><span data-stu-id="8503f-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="8503f-107">포털</span><span class="sxs-lookup"><span data-stu-id="8503f-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="8503f-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8503f-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="8503f-109">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="8503f-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="8503f-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="8503f-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a><span data-ttu-id="8503f-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="8503f-111">Before you begin</span></span>
### <a name="install-hello-latest-version-of-azure-powershell"></a><span data-ttu-id="8503f-112">Hello 최신 버전의 Azure PowerShell 설치</span><span class="sxs-lookup"><span data-stu-id="8503f-112">Install hello latest version of Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="8503f-113">Azure PowerShell 버전 1.0.3 해야 SQL 데이터 웨어하우스를 사용 하 여 Azure PowerShell toouse 큽니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-113">toouse Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="8503f-114">tooverify 현재 사용 중인 hello 명령을 실행 **Get-module-ListAvailable-Name Azure**합니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-114">tooverify your current version run hello command **Get-Module -ListAvailable -Name Azure**.</span></span> <span data-ttu-id="8503f-115">Hello에서 최신 버전을 설치할 수 있습니다 [Microsoft 웹 플랫폼 설치 관리자][Microsoft Web Platform Installer]합니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-115">You can install hello latest version from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="8503f-116">자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고][How tooinstall and configure Azure PowerShell]합니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-116">For more information, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="8503f-117">Azure PowerShell Cmdlet 시작</span><span class="sxs-lookup"><span data-stu-id="8503f-117">Get started with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="8503f-118">tooget 시작:</span><span class="sxs-lookup"><span data-stu-id="8503f-118">tooget started:</span></span>

1. <span data-ttu-id="8503f-119">Azure PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-119">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="8503f-120">Hello PowerShell 프롬프트에서 이러한 명령을 toosign toohello Azure 리소스 관리자에서에서 실행 하 고 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-120">At hello PowerShell prompt, run these commands toosign in toohello Azure Resource Manager and select your subscription.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="8503f-121">계산 능력 크기 조정</span><span class="sxs-lookup"><span data-stu-id="8503f-121">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="8503f-122">toochange hello dwu로 사용 하 여 hello [집합 AzureRmSqlDatabase] [ Set-AzureRmSqlDatabase] PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8503f-122">toochange hello DWUs, use hello [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase] PowerShell cmdlet.</span></span> <span data-ttu-id="8503f-123">hello 다음 예제에서는 설정 hello 서비스 수준 목표 tooDW1000 hello MySQLDW 호스팅되는 데이터베이스에 대 한 서버 MyServer에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-123">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW which is hosted on server MyServer.</span></span>

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="8503f-124">계산 일시 중지</span><span class="sxs-lookup"><span data-stu-id="8503f-124">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="8503f-125">toopause 데이터베이스를 사용 하 여 hello [Suspend AzureRmSqlDatabase] [ Suspend-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8503f-125">toopause a database, use hello [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="8503f-126">hello 다음 중지 하는 예제 Server01 라는 서버에서 호스팅되는 Database02 라는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-126">hello following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="8503f-127">hello 서버 이름이 ResourceGroup1 Azure 리소스 그룹에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-127">hello server is in an Azure resource group named ResourceGroup1.</span></span>

> [!NOTE]
> <span data-ttu-id="8503f-128">서버가 foo.database.windows.net, 있는 경우 "foo" hello PowerShell cmdlet에-ServerName hello으로 사용 하는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-128">Note that if your server is foo.database.windows.net, use "foo" as hello -ServerName in hello PowerShell cmdlets.</span></span>
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="8503f-129">다음 예제에서는 같은 변형을 hello $database 개체에 hello 데이터베이스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-129">A variation, this next example retrieves hello database into hello $database object.</span></span> <span data-ttu-id="8503f-130">다음 파이프 hello 개체 너무[Suspend AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]합니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-130">It then pipes hello object too[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span> <span data-ttu-id="8503f-131">hello 결과 hello 개체 resultDatabase에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-131">hello results are stored in hello object resultDatabase.</span></span> <span data-ttu-id="8503f-132">마지막 명령은 hello hello 결과 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-132">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="8503f-133">계산 다시 시작</span><span class="sxs-lookup"><span data-stu-id="8503f-133">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="8503f-134">toostart 데이터베이스를 사용 하 여 hello [Resume AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8503f-134">toostart a database, use hello [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="8503f-135">hello 다음 예제에서는 시작 라는 Database02 Server01 라는 서버에서 호스트 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-135">hello following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="8503f-136">hello 서버 이름이 ResourceGroup1 Azure 리소스 그룹에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-136">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="8503f-137">다음 예제에서는 같은 변형을 hello $database 개체에 hello 데이터베이스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-137">A variation, this next example retrieves hello database into hello $database object.</span></span> <span data-ttu-id="8503f-138">파이프 hello 개체 너무[Resume AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] $resultDatabase에 hello 결과 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-138">It then pipes hello object too[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] and stores hello results in $resultDatabase.</span></span> <span data-ttu-id="8503f-139">마지막 명령은 hello hello 결과 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-139">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="8503f-140">데이터베이스 상태 확인</span><span class="sxs-lookup"><span data-stu-id="8503f-140">Check database state</span></span>

<span data-ttu-id="8503f-141">위의 예제는 hello와 같이 하나 צ ְ ײ [Get AzureRmSqlDatabase] [ Get-AzureRmSqlDatabase] 함으로써 hello 상태 뿐만 아니라 인수로 toouse를 검사 하는 데이터베이스에 대 한 cmdlet tooget 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-141">As shown in hello above examples, one can use [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] cmdlet tooget information on a database, thereby checking hello status, but also toouse as an argument.</span></span> 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

<span data-ttu-id="8503f-142">결과는 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-142">Which will result in something like</span></span> 

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

<span data-ttu-id="8503f-143">Toosee hello를 다음 확인할 수 있습니다 *상태* hello 데이터베이스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-143">Where you can then check toosee hello *Status* of hello database.</span></span> <span data-ttu-id="8503f-144">이 경우 이 데이터베이스가 온라인 상태인지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-144">In this case, you can see that this database is online.</span></span> 

<span data-ttu-id="8503f-145">이 명령을 실행하면 온라인, 일시 중지 중, 다시 시작 중, 크기 조정 및 일시 중지됨의 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8503f-145">When you run this command, you should receive a Status value of either Online, Pausing, Resuming, Scaling, and Paused.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="8503f-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8503f-146">Next steps</span></span>
<span data-ttu-id="8503f-147">다른 관리 작업은 [관리 개요][Management overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8503f-147">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Get-AzureRmSqlDatabase]: /powershell/servicemanagement/azure.sqldatabase/v1.6.1/get-azuresqldatabase

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[Azure portal]: http://portal.azure.com/

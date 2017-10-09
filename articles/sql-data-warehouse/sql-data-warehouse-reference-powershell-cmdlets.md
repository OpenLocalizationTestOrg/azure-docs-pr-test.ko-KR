---
title: "Azure SQL 데이터 웨어하우스 용 aaaPowerShell cmdlet"
description: "Azure SQL 데이터 웨어하우스에 대 한 hello 상위 PowerShell cmdlet을 찾을 방법을 비롯 하 여 toopause 하 고 데이터베이스를 다시 시작 합니다."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 6f0d5772-f05f-4cc8-9749-4adb153dfd50
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 84353b56131cf856e0724d338d7ed186fd2ceeaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a><span data-ttu-id="3cb12-103">SQL 데이터 웨어하우스용 PowerShell cmdlet 및 REST API</span><span class="sxs-lookup"><span data-stu-id="3cb12-103">PowerShell cmdlets and REST APIs for SQL Data Warehouse</span></span>
<span data-ttu-id="3cb12-104">많은 SQL 데이터 웨어하우스 관리 작업을 Azure PowerShell cmdlet 또는 REST API를 사용하여 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb12-104">Many SQL Data Warehouse administration tasks can be managed using either Azure PowerShell cmdlets or REST APIs.</span></span>  <span data-ttu-id="3cb12-105">어떻게 toouse PowerShell 명령을 tooautomate 일반 SQL 데이터 웨어하우스 작업의 몇 가지 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb12-105">Below are some examples of how toouse PowerShell commands tooautomate common tasks in your SQL Data Warehouse.</span></span>  <span data-ttu-id="3cb12-106">몇 가지 좋은 REST 예제 hello 문서 참조 [REST 사용 하 여 확장성 관리][Manage scalability with REST]합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb12-106">For some good REST examples, see hello article [Manage scalability with REST][Manage scalability with REST].</span></span>

> [!NOTE]
> <span data-ttu-id="3cb12-107">Azure PowerShell 버전 1.0.3 순서 toouse SQL 데이터 웨어하우스를 사용 하 여 Azure PowerShell에서에서 필요한 큽니다.</span><span class="sxs-lookup"><span data-stu-id="3cb12-107">In order toouse Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="3cb12-108">**Get-Module -ListAvailable -Name Azure**를 실행하여 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cb12-108">You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="3cb12-109">hello 최신 버전에서 설치 [Microsoft 웹 플랫폼 설치 관리자][Microsoft Web Platform Installer]합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb12-109">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="3cb12-110">Hello 최신 버전의 설치에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고][How tooinstall and configure Azure PowerShell]합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb12-110">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="3cb12-111">Azure PowerShell Cmdlet 시작</span><span class="sxs-lookup"><span data-stu-id="3cb12-111">Get started with Azure PowerShell cmdlets</span></span>
1. <span data-ttu-id="3cb12-112">Windows PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3cb12-112">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="3cb12-113">Hello PowerShell 프롬프트에서 이러한 명령을 toosign toohello Azure 리소스 관리자에서에서 실행 하 고 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb12-113">At hello PowerShell prompt, run these commands toosign in toohello Azure Resource Manager and select your subscription.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a><span data-ttu-id="3cb12-114">SQL 데이터 웨어하우스 일시 중지 예제</span><span class="sxs-lookup"><span data-stu-id="3cb12-114">Pause SQL Data Warehouse Example</span></span>
<span data-ttu-id="3cb12-115">"Server01."라는 서버에서 호스트하는 "Database02"라는 데이터베이스를 일시 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb12-115">Pause a database named "Database02" hosted on a server named "Server01."</span></span>  <span data-ttu-id="3cb12-116">hello 라는 "ResourceGroup1"는 Azure 리소스 그룹에는</span><span class="sxs-lookup"><span data-stu-id="3cb12-116">hello server is in an Azure resource group named "ResourceGroup1."</span></span>

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="3cb12-117">변형,이 예제에서는 파이프 검색 hello 개체 너무[Suspend AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb12-117">A variation, this example pipes hello retrieved object too[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span>  <span data-ttu-id="3cb12-118">결과적으로, hello 데이터베이스 일시 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cb12-118">As a result, hello database is paused.</span></span> <span data-ttu-id="3cb12-119">마지막 명령은 hello hello 결과 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3cb12-119">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a><span data-ttu-id="3cb12-120">SQL 데이터 웨어하우스 시작 예제</span><span class="sxs-lookup"><span data-stu-id="3cb12-120">Start SQL Data Warehouse Example</span></span>
<span data-ttu-id="3cb12-121">"Server01."이라는 서버에서 호스트하는 "Database02"라는 데이터베이스의 작동을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb12-121">Resume operation of a database named "Database02" hosted on a server named "Server01."</span></span> <span data-ttu-id="3cb12-122">서버 hello 라는 "ResourceGroup1" 리소스 그룹에 포함 된</span><span class="sxs-lookup"><span data-stu-id="3cb12-122">hello server is contained in a resource group named "ResourceGroup1."</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="3cb12-123">변형인 이 예에서는 "ResourceGroup1."이라는 리소스 그룹에 포함된 "Server01"이라는 서버에서 "Database02"라는 데이터베이스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb12-123">A variation, this example retrieves a database named "Database02" from a server named "Server01" that is contained in a resource group named "ResourceGroup1."</span></span> <span data-ttu-id="3cb12-124">너무 hello 검색 된 개체를 파이프[Resume AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb12-124">It pipes hello retrieved object too[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> <span data-ttu-id="3cb12-125">서버가 foo.database.windows.net, 있는 경우 "foo" hello PowerShell cmdlet에-ServerName hello으로 사용 하는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cb12-125">Note that if your server is foo.database.windows.net, use "foo" as hello -ServerName in hello PowerShell cmdlets.</span></span>
> 
> 

## <a name="other-supported-powershell-cmdlets"></a><span data-ttu-id="3cb12-126">지원되는 기타 PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="3cb12-126">Other supported PowerShell cmdlets</span></span>
<span data-ttu-id="3cb12-127">다음 PowerShell cmdlet은 Azure SQL Data Warehouse에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cb12-127">These PowerShell cmdlets are supported with Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="3cb12-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="3cb12-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="3cb12-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span><span class="sxs-lookup"><span data-stu-id="3cb12-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span></span>
* <span data-ttu-id="3cb12-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span><span class="sxs-lookup"><span data-stu-id="3cb12-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span></span>
* <span data-ttu-id="3cb12-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="3cb12-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="3cb12-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="3cb12-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="3cb12-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="3cb12-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="3cb12-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="3cb12-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="3cb12-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span><span class="sxs-lookup"><span data-stu-id="3cb12-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span></span>
* <span data-ttu-id="3cb12-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="3cb12-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="3cb12-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="3cb12-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cb12-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3cb12-138">Next steps</span></span>
<span data-ttu-id="3cb12-139">더 많은 PowerShell 예제는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3cb12-139">For more PowerShell examples, see:</span></span>

* <span data-ttu-id="3cb12-140">[Powershell을 사용하여 SQL Data Warehouse 만들기][Create a SQL Data Warehouse using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="3cb12-140">[Create a SQL Data Warehouse using PowerShell][Create a SQL Data Warehouse using PowerShell]</span></span>
* <span data-ttu-id="3cb12-141">[데이터베이스 복원][Database restore]</span><span class="sxs-lookup"><span data-stu-id="3cb12-141">[Database restore][Database restore]</span></span>

<span data-ttu-id="3cb12-142">PowerShell로 자동화할 수 있는 다른 작업은 [Azure SQL Database Cmdlet][Azure SQL Database Cmdlets]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3cb12-142">For other tasks which can be automated with PowerShell, see [Azure SQL Database Cmdlets][Azure SQL Database Cmdlets].</span></span> <span data-ttu-id="3cb12-143">모든 Azure SQL Database cmdlet이 Azure SQL Data Warehouse에 대해 지원되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="3cb12-143">Note that not all Azure SQL Database cmdlets are supported for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="3cb12-144">REST로 자동화할 수 있는 작업 목록은 [Azure SQL Database에 대한 작업][Operations for Azure SQL Databases]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3cb12-144">For a list of tasks which can be automated with REST, see [Operations for Azure SQL Databases][Operations for Azure SQL Databases].</span></span>

<!--Image references-->

<!--Article references-->
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Create a SQL Data Warehouse using PowerShell]: ./sql-data-warehouse-get-started-provision-powershell.md
[Database restore]: ./sql-data-warehouse-restore-database-powershell.md
[Manage scalability with REST]: ./sql-data-warehouse-manage-compute-rest-api.md

<!--MSDN references-->
[Azure SQL Database Cmdlets]: https://msdn.microsoft.com/library/mt574084.aspx
[Operations for Azure SQL Databases]: https://msdn.microsoft.com/library/azure/dn505719.aspx
[Get-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt603648.aspx
[Get-AzureRmSqlDeletedDatabaseBackup]: https://msdn.microsoft.com/library/mt693387.aspx
[Get-AzureRmSqlDatabaseRestorePoints]: https://msdn.microsoft.com/library/mt603642.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Remove-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619368.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
<!-- It appears that Select-AzureRmSubscription isn't documented, so this points tooSelect-AzureSubscription -->
[Select-AzureRmSubscription]: https://msdn.microsoft.com/library/dn722499.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps

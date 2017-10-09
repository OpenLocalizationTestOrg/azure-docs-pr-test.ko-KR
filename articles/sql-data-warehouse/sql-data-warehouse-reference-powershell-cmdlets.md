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
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a>SQL 데이터 웨어하우스용 PowerShell cmdlet 및 REST API
많은 SQL 데이터 웨어하우스 관리 작업을 Azure PowerShell cmdlet 또는 REST API를 사용하여 관리할 수 있습니다.  어떻게 toouse PowerShell 명령을 tooautomate 일반 SQL 데이터 웨어하우스 작업의 몇 가지 예는 다음과 같습니다.  몇 가지 좋은 REST 예제 hello 문서 참조 [REST 사용 하 여 확장성 관리][Manage scalability with REST]합니다.

> [!NOTE]
> Azure PowerShell 버전 1.0.3 순서 toouse SQL 데이터 웨어하우스를 사용 하 여 Azure PowerShell에서에서 필요한 큽니다.  **Get-Module -ListAvailable -Name Azure**를 실행하여 버전을 확인할 수 있습니다.  hello 최신 버전에서 설치 [Microsoft 웹 플랫폼 설치 관리자][Microsoft Web Platform Installer]합니다.  Hello 최신 버전의 설치에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고][How tooinstall and configure Azure PowerShell]합니다.
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a>Azure PowerShell Cmdlet 시작
1. Windows PowerShell을 엽니다.
2. Hello PowerShell 프롬프트에서 이러한 명령을 toosign toohello Azure 리소스 관리자에서에서 실행 하 고 구독을 선택 합니다.
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a>SQL 데이터 웨어하우스 일시 중지 예제
"Server01."라는 서버에서 호스트하는 "Database02"라는 데이터베이스를 일시 중지합니다.  hello 라는 "ResourceGroup1"는 Azure 리소스 그룹에는

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
변형,이 예제에서는 파이프 검색 hello 개체 너무[Suspend AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]합니다.  결과적으로, hello 데이터베이스 일시 중지 됩니다. 마지막 명령은 hello hello 결과 보여 줍니다.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a>SQL 데이터 웨어하우스 시작 예제
"Server01."이라는 서버에서 호스트하는 "Database02"라는 데이터베이스의 작동을 다시 시작합니다. 서버 hello 라는 "ResourceGroup1" 리소스 그룹에 포함 된

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

변형인 이 예에서는 "ResourceGroup1."이라는 리소스 그룹에 포함된 "Server01"이라는 서버에서 "Database02"라는 데이터베이스를 검색합니다. 너무 hello 검색 된 개체를 파이프[Resume AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]합니다.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> 서버가 foo.database.windows.net, 있는 경우 "foo" hello PowerShell cmdlet에-ServerName hello으로 사용 하는 참고 합니다.
> 
> 

## <a name="other-supported-powershell-cmdlets"></a>지원되는 기타 PowerShell cmdlet
다음 PowerShell cmdlet은 Azure SQL Data Warehouse에서 지원됩니다.

* [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]
* [Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]
* [Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]
* [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]
* [Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]
* [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]
* [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]
* [Select-AzureRmSubscription][Select-AzureRmSubscription]
* [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]
* [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]

## <a name="next-steps"></a>다음 단계
더 많은 PowerShell 예제는 다음을 참조하세요.

* [Powershell을 사용하여 SQL Data Warehouse 만들기][Create a SQL Data Warehouse using PowerShell]
* [데이터베이스 복원][Database restore]

PowerShell로 자동화할 수 있는 다른 작업은 [Azure SQL Database Cmdlet][Azure SQL Database Cmdlets]을 참조하세요. 모든 Azure SQL Database cmdlet이 Azure SQL Data Warehouse에 대해 지원되는 것은 아닙니다.  REST로 자동화할 수 있는 작업 목록은 [Azure SQL Database에 대한 작업][Operations for Azure SQL Databases]을 참조하세요.

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

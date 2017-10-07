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
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a>Azure SQL Data Warehouse의 계산 능력 관리(PowerShell)
> [!div class="op_single_selector"]
> * [개요](sql-data-warehouse-manage-compute-overview.md)
> * [포털](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST (영문)](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a>시작하기 전에
### <a name="install-hello-latest-version-of-azure-powershell"></a>Hello 최신 버전의 Azure PowerShell 설치
> [!NOTE]
> Azure PowerShell 버전 1.0.3 해야 SQL 데이터 웨어하우스를 사용 하 여 Azure PowerShell toouse 큽니다.  tooverify 현재 사용 중인 hello 명령을 실행 **Get-module-ListAvailable-Name Azure**합니다. Hello에서 최신 버전을 설치할 수 있습니다 [Microsoft 웹 플랫폼 설치 관리자][Microsoft Web Platform Installer]합니다.  자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고][How tooinstall and configure Azure PowerShell]합니다.
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a>Azure PowerShell Cmdlet 시작
tooget 시작:

1. Azure PowerShell을 엽니다.
2. Hello PowerShell 프롬프트에서 이러한 명령을 toosign toohello Azure 리소스 관리자에서에서 실행 하 고 구독을 선택 합니다.

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a>계산 능력 크기 조정
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

toochange hello dwu로 사용 하 여 hello [집합 AzureRmSqlDatabase] [ Set-AzureRmSqlDatabase] PowerShell cmdlet. hello 다음 예제에서는 설정 hello 서비스 수준 목표 tooDW1000 hello MySQLDW 호스팅되는 데이터베이스에 대 한 서버 MyServer에서 합니다.

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>계산 일시 중지
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause 데이터베이스를 사용 하 여 hello [Suspend AzureRmSqlDatabase] [ Suspend-AzureRmSqlDatabase] cmdlet. hello 다음 중지 하는 예제 Server01 라는 서버에서 호스팅되는 Database02 라는 데이터베이스입니다. hello 서버 이름이 ResourceGroup1 Azure 리소스 그룹에 있습니다.

> [!NOTE]
> 서버가 foo.database.windows.net, 있는 경우 "foo" hello PowerShell cmdlet에-ServerName hello으로 사용 하는 참고 합니다.
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
다음 예제에서는 같은 변형을 hello $database 개체에 hello 데이터베이스를 검색합니다. 다음 파이프 hello 개체 너무[Suspend AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]합니다. hello 결과 hello 개체 resultDatabase에 저장 됩니다. 마지막 명령은 hello hello 결과 보여 줍니다.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>계산 다시 시작
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

toostart 데이터베이스를 사용 하 여 hello [Resume AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] cmdlet. hello 다음 예제에서는 시작 라는 Database02 Server01 라는 서버에서 호스트 데이터베이스입니다. hello 서버 이름이 ResourceGroup1 Azure 리소스 그룹에 있습니다.

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

다음 예제에서는 같은 변형을 hello $database 개체에 hello 데이터베이스를 검색합니다. 파이프 hello 개체 너무[Resume AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] $resultDatabase에 hello 결과 저장 합니다. 마지막 명령은 hello hello 결과 보여 줍니다.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a>데이터베이스 상태 확인

위의 예제는 hello와 같이 하나 צ ְ ײ [Get AzureRmSqlDatabase] [ Get-AzureRmSqlDatabase] 함으로써 hello 상태 뿐만 아니라 인수로 toouse를 검사 하는 데이터베이스에 대 한 cmdlet tooget 정보입니다. 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

결과는 다음과 유사합니다. 

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

Toosee hello를 다음 확인할 수 있습니다 *상태* hello 데이터베이스의 합니다. 이 경우 이 데이터베이스가 온라인 상태인지 확인할 수 있습니다. 

이 명령을 실행하면 온라인, 일시 중지 중, 다시 시작 중, 크기 조정 및 일시 중지됨의 상태가 표시됩니다.

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>다음 단계
다른 관리 작업은 [관리 개요][Management overview]를 참조하세요.

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

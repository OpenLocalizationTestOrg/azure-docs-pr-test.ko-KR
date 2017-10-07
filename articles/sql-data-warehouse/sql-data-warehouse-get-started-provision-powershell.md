---
title: "PowerShell을 사용 하 여 SQL 데이터 웨어하우스 aaaCreate | Microsoft Docs"
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
ms.openlocfilehash: d8af29ec285a11285785ab5474e4dfc8c36bc3ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-sql-data-warehouse-using-powershell"></a>PowerShell을 사용하여 SQL 데이터 웨어하우스 만들기
> [!div class="op_single_selector"]
> * [Azure 포털](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

이 문서에 어떻게 toocreate SQL 데이터 웨어하우스 PowerShell을 사용 하 여 보여줍니다.

## <a name="prerequisites"></a>필수 조건
시작 tooget를 해야 합니다.

* **Azure 계정**: 방문 [Azure 무료 평가판] [ Azure Free Trial] 또는 [MSDN Azure 크레딧을] [ MSDN Azure Credits] toocreate 계정.
* **Azure SQL server**: 참조 [hello Azure 포털에서에서 Azure SQL 데이터베이스를 만들] [ Create an Azure SQL database in hello Azure Portal] 또는 [PowerShell을 사용한 Azure SQL 데이터베이스를 만들] [ Create an Azure SQL database with PowerShell] 내용을 확인 합니다.
* **리소스 그룹**: hello 동일한 리소스와 Azure SQL server 그룹 또는 참조를 사용 하거나 [어떻게 toocreate 리소스 그룹](../azure-resource-manager/resource-group-portal.md)합니다.
* **PowerShell 버전 1.0.3 이상**: **Get-Module -ListAvailable -Name Azure**를 실행하여 버전을 확인할 수 있습니다.  hello 최신 버전에서 설치 [Microsoft 웹 플랫폼 설치 관리자][Microsoft Web Platform Installer]합니다.  Hello 최신 버전의 설치에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고][How tooinstall and configure Azure PowerShell]합니다.

> [!NOTE]
> SQL 데이터 웨어하우스를 만들면 새로운 유료 서비스가 발생할 수 있습니다.  가격 책정에 대한 자세한 내용은 [SQL Data Warehouse 가격 책정][SQL Data Warehouse pricing]을 참조하세요.
>
>

## <a name="create-a-sql-data-warehouse"></a>SQL 데이터 웨어하우스 만들기
1. Windows PowerShell을 엽니다.
2. 이 cmdlet toologin tooAzure 리소스 관리자를 실행 합니다.

    ```Powershell
    Login-AzureRmAccount
    ```
3. 현재 세션에 대 한 toouse 원하는 hello 구독을 선택 합니다.

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. 데이터베이스를 만듭니다. 이 예제에서는 "mynewsqldw" 서비스 목표 수준이 "DW400", "mywesteuroperesgp1" 라는 hello 리소스 그룹에는 "sqldwserver1" 라는 toohello 서버 라는 데이터베이스를 만듭니다.

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

필수 매개 변수는 다음과 같습니다.

* **RequestedServiceObjectiveName**: hello 양을 [DWU] [ DWU] 요청 합니다.  지원되는 값은 DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 및 DW6000입니다.
* **DatabaseName**: hello 만들려는 SQL 데이터 웨어하우스의 hello 이름입니다.
* **ServerName**: 만들기에 사용 하는 hello 서버 hello 이름을 (V12 이어야 함).
* **ResourceGroupName**: 사용 중인 리소스 그룹입니다.  구독에서 사용 가능한 리소스 그룹 toofind AzureResource Get을 사용합니다.
* **에디션**: "데이터 웨어하우스" toocreate SQL 데이터 웨어하우스 이어야 합니다.

선택적 매개 변수는 다음과 같습니다.

* **CollationName**: 지정 하지 않은 경우 hello 기본 데이터 정렬은 SQL_Latin1_General_CP1_CI_AS입니다.  데이터베이스에서 데이터 정렬을 변경할 수 없습니다.
* **MaxSizeBytes**: hello 기본 데이터베이스의 최대 크기는 10GB입니다.

Hello 매개 변수 옵션에 대 한 자세한 내용은 참조 하십시오. [새로 AzureRmSqlDatabase] [ New-AzureRmSqlDatabase] 및 [Create Database (Azure SQL 데이터 웨어하우스)][Create Database (Azure SQL Data Warehouse)]합니다.

## <a name="next-steps"></a>다음 단계
SQL 데이터 웨어하우스 완료 된 후 사용자를 프로 비전 하는 경우가 tootry [샘플 데이터를 로드] [ loading sample data] 방법에 대해 너무 확인 또는[개발] [ develop] [로드][load], 또는 [마이그레이션할][migrate]합니다.

방법에 대 한 자세한에 관심이 있다면 SQL 데이터 웨어하우스 toomanage 방법에 프로그래밍 방식으로 확인해 toouse [PowerShell cmdlet 및 REST Api][PowerShell cmdlets and REST APIs]합니다.

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how toocreate a SQL Data Warehouse from hello Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F

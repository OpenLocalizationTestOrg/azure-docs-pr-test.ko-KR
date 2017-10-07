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
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a>TRANSACT-SQL(TSQL)를 사용하여 SQL 데이터 웨어하우스 데이터베이스 만들기
> [!div class="op_single_selector"]
> * [Azure 포털](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

이 문서에서는 어떻게 toocreate SQL 데이터 웨어하우스 T-SQL을 사용 하 여 보여 줍니다.

## <a name="prerequisites"></a>필수 조건
시작 tooget를 해야 합니다.

* **Azure 계정**: 방문 [Azure 무료 평가판] [ Azure Free Trial] 또는 [MSDN Azure 크레딧을] [ MSDN Azure Credits] toocreate 계정.
* **Azure SQL server**: [Azure 포털 hello로 Azure SQL 데이터베이스 논리 서버는 만들기]를 참조 [Azure SQL 데이터베이스 논리 서버 hello Azure 포털으로 만들기] [PowerShell을 사용한 Azure SQL 데이터베이스 논리 서버 만들기] 또는 [Azure SQL 만들기 PowerShell과 함께 데이터베이스 논리 서버]에 대 한 자세한 내용은 합니다.
* **리소스 그룹**: hello 동일한 리소스와 Azure SQL server 그룹 또는 참조를 사용 하거나 [어떻게 toocreate 리소스 그룹][how toocreate a resource group]합니다.
* **환경 tooexecute T-SQL**: 사용할 수 있습니다 [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], 또는 [SSMS] [ SSMS] tooexecute T-SQL 합니다.

> [!NOTE]
> SQL 데이터 웨어하우스를 만들면 새로운 유료 서비스가 발생할 수 있습니다.  가격 책정에 대한 자세한 내용은 [SQL Data Warehouse 가격 책정][SQL Data Warehouse pricing]을 참조하세요.
>
>

## <a name="create-a-database-with-visual-studio"></a>Visual Studio를 사용하여 데이터베이스 만들기
새 tooVisual Studio 인 경우 hello 문서 참조 [Azure SQL 데이터 웨어하우스 쿼리 (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]합니다.  toostart, Visual Studio에서 SQL Server 개체 탐색기를 열고 SQL 데이터 웨어하우스 데이터베이스를 호스팅할 toohello 서버에 연결 합니다.  연결 되 면 hello 다음 hello에 대해 SQL 명령을 실행 하 여 SQL 데이터 웨어하우스를 만들 수 있습니다 **마스터** 데이터베이스입니다.  이 명령은 서비스 DW400 목표와 MySqlDwDb hello 데이터베이스를 만들고 hello 데이터베이스 toogrow tooa의 최대 크기 10TB를 허용 합니다.

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a>sqlcmd로 데이터베이스 만들기
또는 명령 프롬프트에서 다음을 실행 하 여 sqlcmd와 같은 명령을 hello hello를 실행할 수 있습니다.

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

hello 기본 데이터 정렬을 지정 하지 않은 경우에 COLLATE 정렬은 SQL_Latin1_General_CP1_CI_AS입니다.  hello `MAXSIZE` 250GB 240 TB 사이일 수 있습니다.  hello `SERVICE_OBJECTIVE` DW100 DW2000 사이일 수 있습니다 [DWU][DWU]합니다.  유효한 모든 값의 목록에 대 한 hello MSDN 설명서를 참조 하십시오. [CREATE DATABASE][CREATE DATABASE]합니다.  Hello MAXSIZE와 SERVICE_OBJECTIVE는으로 변경할 수 있습니다는 [ALTER DATABASE] [ ALTER DATABASE] T-SQL 명령입니다.  데이터베이스 데이터 정렬 hello를 만든 후 변경할 수 없습니다.   변경 hello SERVICE_OBJECTIVE DWU를 변경 하는 것 항공편의 모든 쿼리를 취소 된 서비스의 다시 시작 하면 때 주의 해야 합니다.  MAXSIZE 변경은 간단한 메타데이터 작업이므로 서비스를 다시 시작하지 않습니다.

## <a name="next-steps"></a>다음 단계
SQL 데이터 웨어하우스 하면 프로 비전 완료 된 후 [샘플 데이터를 로드] [ load sample data] 방법에 대해 너무 확인 또는[개발][develop], [로드][load], 또는 [마이그레이션할][migrate]합니다.

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

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
# <a name="create-an-azure-sql-data-warehouse"></a>Azure SQL 데이터 웨어하우스 만들기
> [!div class="op_single_selector"]
> * [Azure Portal](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

이 자습서에서는 Azure 포털 toocreate AdventureWorksDW 예제 데이터베이스를 포함 하는 SQL 데이터 웨어하우스 hello를 사용 합니다.

## <a name="prerequisites"></a>필수 조건
시작 tooget를 해야 합니다.

* **Azure 계정**: 방문 [Azure 무료 평가판] [ Azure Free Trial] 또는 [MSDN Azure 크레딧을] [ MSDN Azure Credits] toocreate 계정.
* **Azure SQL server**: 참조 [hello Azure 포털에서 Azure SQL 데이터베이스 만들기] [ Create an Azure SQL database in hello Azure portal] 내용을 확인 합니다.

> [!NOTE]
> SQL 데이터 웨어하우스를 만들면 새로운 유료 서비스가 발생할 수 있습니다.  자세한 내용은 [SQL Data Warehouse 가격 책정][SQL Data Warehouse pricing]을 참조하세요.
>
>

## <a name="create-a-sql-data-warehouse"></a>SQL 데이터 웨어하우스 만들기
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. **+ 새로 만들기** > **데이터베이스** > **SQL Data Warehouse**를 차례로 클릭합니다.

    ![생성](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. Hello에 **SQL 데이터 웨어하우스** 블레이드를 필요에 따라 hello 정보를 입력 '만들기' toocreate 다음 키를 누릅니다.

    ![데이터베이스 만들기](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * **서버**: 먼저 서버를 선택하는 것이 좋습니다.  
   * **데이터베이스 이름**:는 사용 되는 tooreference hello SQL 데이터 웨어하우스 hello 이름입니다.  고유 toohello 서버 여야 합니다.
   * **성능**: 400[DWUs][DWU]로 시작하는 것이 좋습니다. 만든 후 위나 아래로 tooadjust hello 성능 데이터 웨어하우스 또는 소수를 마우스 오른쪽 이나 왼쪽 hello 슬라이더 toohello 탐색할 수 있습니다.  Dwu에 대 한 자세한 toolearn에 우리의 설명서를 참조 하십시오. [배율](sql-data-warehouse-manage-compute-overview.md) 또는 [가격 책정 페이지][SQL Data Warehouse pricing]합니다.
   * **구독**: 선택 hello [구독] 있는이 SQL 데이터 웨어하우스를 청구 됩니다.
   * **리소스 그룹**: [리소스 그룹] [ Resource group] Azure 리소스 컬렉션을 관리 하는 컨테이너 설계 toohelp 됩니다. [리소스 그룹](../azure-resource-manager/resource-group-overview.md)에 대해 알아봅니다.
   * **원본 선택**: **원본 선택** > **샘플**을 차례로 클릭합니다. Azure hello를 자동으로 채우려고 **선택 샘플** AdventureWorksDW 옵션입니다.

   > [!NOTE]
   > SQL 데이터 웨어하우스에 대 한 hello 기본 데이터 정렬은 SQL_Latin1_General_CP1_CI_AS입니다. 다른 데이터 정렬이 필요한 경우 [T-SQL] [ T-SQL] 서로 다른 데이터 정렬으로 사용 되는 toocreate hello 데이터베이스가 될 수 있습니다.
   >
   >

1. 클릭 **만들기** toocreate SQL 데이터 웨어하우스에서 합니다.
2. 몇 분 정도 기다립니다. 데이터 웨어하우스 준비 되 면 있습니다 돌아가야 toohello [Azure 포털](https://portal.azure.com)합니다. SQL 데이터 웨어하우스 SQL 데이터베이스를 아래 나열 된 대시보드에서 찾을 수도 있고 hello 리소스에서 해당 사용한 toocreate 그룹 것입니다.

    ![포털 보기](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a>다음 단계
SQL 데이터 웨어하우스를 만든 준비가 너무[연결](sql-data-warehouse-connect-overview.md) 하 고 쿼리를 시작 합니다.

SQL 데이터 웨어하우스로 tooload 데이터 참조 hello [개요 로드](sql-data-warehouse-overview-load.md)합니다.

기존 데이터베이스 tooSQL 데이터 웨어하우스 toomigrate을 시도 하는 경우 참조 hello [마이그레이션 개요](sql-data-warehouse-overview-migrate.md) 사용 또는 [마이그레이션 유틸리티](sql-data-warehouse-migrate-migration-utility.md)합니다.

Transact-SQL을 사용하여 방화벽 규칙을 구성할 수도 있습니다. 자세한 내용은 [sp_set_firewall_rule][sp_set_firewall_rule] 및 [sp_set_database_firewall_rule][sp_set_database_firewall_rule]을 참조하세요.

Hello에 좋은 생각 toolook 이기도 [모범 사례][Best practices]합니다.

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

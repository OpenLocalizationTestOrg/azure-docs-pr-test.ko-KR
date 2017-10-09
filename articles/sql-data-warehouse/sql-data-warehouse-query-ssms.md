---
title: "aaaConnect tooAzure SQL 데이터 웨어하우스-SSMS | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스 SQL Server Management Studio (SSMS) tooconnect tooand 쿼리를 사용 합니다."
services: sql-data-warehouse
documentationcenter: 
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 299e50b3-e68a-471c-8aee-b0b9874781bd
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: bcbaf7139d2e5183b388b8d58c015cf5ad726722
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sql-server-management-studio-ssms"></a>TooSQL 데이터 웨어하우스 SQL Server Management Studio (SSMS)와 연결
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure 기계 학습](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Azure SQL 데이터 웨어하우스 SQL Server Management Studio (SSMS) tooconnect tooand 쿼리를 사용 합니다. 

## <a name="prerequisites"></a>필수 조건
toouse 해야이 자습서에서는:

* 기존 SQL 데이터 웨어하우스. 하나의 toocreate 참조 [SQL 데이터 웨어하우스를 만들][Create a SQL Data Warehouse]합니다.
* SSMS(SQL Server Management Studio) 설치됨. 아직 없는 경우 무료로 [SSMS를 설치][Install SSMS]합니다.
* hello 정규화 된 SQL server 이름입니다. toofind이,이 참조 [tooSQL 데이터 웨어하우스 연결][Connect tooSQL Data Warehouse]합니다.

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1. SQL 데이터 웨어하우스 tooyour 연결
1. SSMS를 엽니다.
2. 개체 탐색기를 엽니다. toodo이,이 선택 **파일** > **개체 탐색기 연결**합니다.
   
    ![SQL Server 개체 탐색기][1]
3. Hello 연결 tooServer 창의 hello 필드를 입력 합니다.
   
    ![TooServer 연결][2]
   
   * **서버 이름**. Hello 입력 **서버 이름** 앞에서 확인 합니다.
   * **인증**. **SQL Server 인증** 또는 **Active Directory 통합 인증**을 선택합니다.
   * **사용자 이름** 및 **암호**. 위에서 SQL Server 인증을 선택한 경우 사용자 이름 및 암호를 입력합니다.
   * **Connect**를 클릭합니다.
4. tooexplore, Azure SQL 서버를 확장 합니다. Hello 서버와 관련 된 hello 데이터베이스를 볼 수 있습니다. 예제 데이터베이스 AdventureWorksDW toosee hello 테이블을 확장 합니다.
   
    ![AdventureWorksDW 탐색하기][3]

## <a name="2-run-a-sample-query"></a>2. 샘플 쿼리 실행
연결에 대 한 설정 된 tooyour 데이터베이스를 수행한 했으므로 쿼리를 작성해 보겠습니다.

1. SQL Server 개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭합니다.
2. **새 쿼리**를 선택합니다. 새 쿼리 창이 열립니다.
   
    ![새 쿼리][4]
3. 이 t s q L 쿼리 hello 쿼리 창에 복사 합니다.
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Hello 쿼리를 실행 합니다. toodo이를 클릭 하이 여 `Execute` 사용 하 여 hello 다음 바로 가기 또는: `F5`합니다.
   
    ![쿼리 실행][5]
5. Hello 쿼리 결과 살펴봅니다. 이 예제에서는 hello FactInternetSales 테이블 60398 행에 있습니다.
   
    ![쿼리 결과][6]

## <a name="next-steps"></a>다음 단계
연결 하 고 쿼리할 수, 하 고 나면 [PowerBI 사용 하 여 hello 데이터 시각화][visualizing hello data with PowerBI]합니다.

Azure Active Directory 인증을 위한 환경 참조 tooconfigure [tooSQL 데이터 웨어하우스를 인증][Authenticate tooSQL Data Warehouse]합니다.

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/en-US/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png

---
title: "aaaConnect tooAzure SQL 데이터 웨어하우스-VSTS | Microsoft Docs"
description: "Visual Studio를 사용하여 SQL 데이터 웨어하우스를 쿼리합니다."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a>Visual Studio와 SSDT를 사용 하 여 데이터 웨어하우스 tooSQL 연결
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure 기계 학습](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

단 몇 분 후에 Visual Studio tooquery Azure SQL 데이터 웨어하우스를 사용 합니다. 이 메서드는 Visual Studio에서 hello SQL Server Data Tools (SSDT) 확장을 사용 합니다. 

## <a name="prerequisites"></a>필수 조건
toouse 해야이 자습서에서는:

* 기존 SQL 데이터 웨어하우스. 하나의 toocreate 참조 [SQL 데이터 웨어하우스를 만들][Create a SQL Data Warehouse]합니다.
* Visual Studio용 SSDT. Visual Studio가 있는 경우 이미 소유하고 있을 것입니다. 설치 지침 및 옵션은 [Visual Studio 및 SSDT 설치][Installing Visual Studio and SSDT]를 참조하세요.
* hello 정규화 된 SQL server 이름입니다. toofind이,이 참조 [tooSQL 데이터 웨어하우스 연결][Connect tooSQL Data Warehouse]합니다.

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1. SQL 데이터 웨어하우스 tooyour 연결
1. Visual Studio 2013 또는 2015 열기
2. SQL Server 개체 탐색기를 엽니다. toodo이,이 선택 **보기** > **SQL Server 개체 탐색기**합니다.
   
    ![SQL Server 개체 탐색기][1]
3. Hello 클릭 **SQL Server 추가** 아이콘입니다.
   
    ![SQL Server 추가][2]
4. Hello 연결 tooServer 창의 hello 필드를 입력 합니다.
   
    ![TooServer 연결][3]
   
   * **서버 이름**. Hello 입력 **서버 이름** 앞에서 확인 합니다.
   * **인증**. **SQL Server 인증** 또는 **Active Directory 통합 인증**을 선택합니다.
   * **사용자 이름** 및 **암호**. 위에서 SQL Server 인증을 선택한 경우 사용자 이름 및 암호를 입력합니다.
   * **Connect**를 클릭합니다.
5. tooexplore, Azure SQL 서버를 확장 합니다. Hello 서버와 관련 된 hello 데이터베이스를 볼 수 있습니다. 예제 데이터베이스 AdventureWorksDW toosee hello 테이블을 확장 합니다.
   
    ![AdventureWorksDW 탐색하기][4]

## <a name="2-run-a-sample-query"></a>2. 샘플 쿼리 실행
연결에 대 한 설정 된 tooyour 데이터베이스를 수행한 했으므로 쿼리를 작성해 보겠습니다.

1. SQL Server 개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭합니다.
2. **새 쿼리**를 선택합니다. 새 쿼리 창이 열립니다.
   
    ![새 쿼리][5]
3. 이 t s q L 쿼리 hello 쿼리 창에 복사 합니다.
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Hello 쿼리를 실행 합니다. toodo hello 녹색 화살표를 클릭 하거나 바로 가기 다음 hello를 사용 하 여이: `CTRL` + `SHIFT` + `E`합니다.
   
    ![쿼리 실행][6]
5. Hello 쿼리 결과 살펴봅니다. 이 예제에서는 hello FactInternetSales 테이블 60398 행에 있습니다.
   
    ![쿼리 결과][7]

## <a name="next-steps"></a>다음 단계
연결 하 고 쿼리할 수, 하 고 나면 [PowerBI 사용 하 여 hello 데이터 시각화][visualizing hello data with PowerBI]합니다.

Azure Active Directory 인증을 위한 환경 참조 tooconfigure [tooSQL 데이터 웨어하우스를 인증][Authenticate tooSQL Data Warehouse]합니다.

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png

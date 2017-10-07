---
title: "Power BI Microsoft Azure를 사용 하 여 SQL 데이터 웨어하우스 데이터 aaaVisualize"
description: "Power BI로 SQL 데이터 웨어하우스 데이터 시각화"
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: d7fb89d1-da1d-4788-a111-68d0e3fda799
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 0425cf5abe7bc001b2a41df4d09bf5f2e42527e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-data-with-power-bi"></a>Power BI를 사용하여 데이터 시각화
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure 기계 학습](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

이 자습서에서는 어떻게 toouse Power BI tooconnect tooSQL 데이터 웨어하우스를 몇 가지 기본 시각화를 만듭니다.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a>필수 조건
이 자습서를 통해 toostep를 해야합니다.

* SQL 데이터 웨어하우스 hello AdventureWorksDW 데이터베이스와 미리 로드 합니다. tooprovision이,이 참조 [SQL 데이터 웨어하우스를 만들] [ Create a SQL Data Warehouse] tooload hello 샘플 데이터를 선택 합니다. 데이터 웨어하우스는 있지만 샘플 데이터가 없는 경우 [샘플 데이터를 수동으로 로드][load sample data manually]할 수 있습니다.

## <a name="1-connect-tooyour-database"></a>1. Tooyour 데이터베이스 연결
Power BI tooopen tooyour AdventureWorksDW 데이터베이스를 연결 합니다.

1. Hello에 로그인 [Azure 포털][Azure portal]합니다.
2. **SQL 데이터베이스** 를 클릭하고 AdventureWorks SQL 데이터 웨어하우스 데이터베이스를 선택합니다.
   
    ![데이터베이스 찾기][1]
3. Hello 'Power BI에서 열기' 단추를 클릭 합니다.
   
    ![Power BI 단추][2]
4. 이제 데이터베이스 웹 주소를 표시 하는 hello SQL 데이터 웨어하우스 연결 페이지를 표시 됩니다. 다음을 클릭합니다.
   
    ![Power BI 연결][3]
5. Azure SQL server 사용자 이름 및 암호를 입력 하 고 완전히 연결 된 tooyour SQL 데이터 웨어하우스 데이터베이스 됩니다.
   
    ![Power BI 로그인][4]
6. Power BI에 로그인 하면 hello 왼쪽 블레이드에서 hello AdventureWorksDW 데이터 집합을 클릭 합니다. Hello 데이터베이스를 열립니다.
   
    ![Power BI AdventureWorksDW 열기][5]

## <a name="2-create-a-report"></a>2. 보고서 만들기
사용자는 이제 준비 toouse Power BI tooanalyze AdventureWorksDW 예제 데이터. tooperform hello 분석 AdventureWorksDW에 AggregateSales 라는 보기가 있습니다. 이 보기에는 hello 회사의 hello 판매를 분석 하는 것에 대 한 주요 메트릭 hello 중 몇 가지 포함 되어 있습니다.

1. toocreate hello 오른쪽 필드 창에서 toopostal 코드에 따라 판매 금액의 맵을 클릭 hello AggregateSales 보기 tooexpand 것입니다. Hello PostalCode 및 SalesAmount 열 tooselect 클릭으로 합니다.
   
    ![Power BI AggregateSales 선택][6]
   
    Power BI는 이를 지리적 데이터로 자동으로 인식하고 지도에 배치합니다.
   
    ![Power BI 맵][7]
2. 이 단계에서는 고객 수익당 매출액을 보여주는 막대 그래프를 만듭니다. toocreate이 이동 toohello AggregateSales 보기를 확장 합니다. Hello SalesAmount 필드를 클릭 합니다. Hello 고객의 소득을 필드 toohello 왼쪽 끌어서 축에 넣습니다.
   
    ![Power BI 축 선택][8]
   
    Hello 가로 막대형 차트 hello 왼쪽 위로 이동 합니다.
   
    ![Power BI 막대형][9]
3. 이 단계에서는 주문 날짜당 판매 금액을 보여주는 꺽은선형 차트를 만듭니다. toocreate이 이동 toohello AggregateSales 보기를 확장 합니다. SalesAmount 및 OrderDate를 클릭합니다. Hello 시각화 열에서 hello 꺾은선형 차트 아이콘;를 클릭 합니다. hello 시각화에서 두 번째 줄에 hello 첫 번째 아이콘입니다.
   
    ![Power BI 꺾은선형 차트 선택][10]
   
    Hello 데이터의 세 가지 각기 다른 시각화를 표시 하는 보고서를 만들었습니다.
   
    ![Power BI 꺾은선형][11]

언제든지 **파일**을 클릭하고 **저장**을 선택하여 진행 상황을 저장할 수 있습니다.

## <a name="next-steps"></a>다음 단계
지금 म 부여한 하면 일부 시간 toowarm hello 샘플 데이터로 하는 방법을 너무 참조[개발][develop], [로드][load], 또는 [ 마이그레이션][migrate]합니다. Hello 살펴보세요 또는 [Power BI 웹사이트][Power BI website]합니다.

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-find-database.png
[2]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-button.png
[3]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-connect-to-azure.png
[4]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-sign-in.png
[5]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-open-adventureworks.png
[6]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-aggregatesales.png
[7]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-map.png
[8]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-chooseaxis.png
[9]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-bar.png
[10]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-prepare-line.png
[11]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-line.png
[12]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-save.png

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[connecting tooSQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/

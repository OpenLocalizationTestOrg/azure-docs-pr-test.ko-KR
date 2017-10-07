---
title: "샘플 데이터를 SQL 데이터 웨어하우스에 aaaLoad | Microsoft Docs"
description: "SQL 데이터 웨어하우스로 샘플 데이터를 로드"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e338ecf8-cfee-419b-b7b6-98108d381c62
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 3459c42f3aae51c27fd35db7874faf99e1e577e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a><span data-ttu-id="8a223-103">SQL 데이터 웨어하우스로 샘플 데이터를 로드</span><span class="sxs-lookup"><span data-stu-id="8a223-103">Load sample data into SQL Data Warehouse</span></span>
<span data-ttu-id="8a223-104">이러한 간단한 단계 tooload 및 쿼리 hello Adventure Works 예제 데이터베이스를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8a223-104">Follow these simple steps tooload and query hello Adventure Works Sample database.</span></span> <span data-ttu-id="8a223-105">이러한 스크립트는 먼저 sqlcmd toorun 테이블 및 뷰를 만드는 SQL을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a223-105">These scripts first use sqlcmd toorun SQL which will create tables and views.</span></span> <span data-ttu-id="8a223-106">테이블을 만든 후 hello 스크립트는 bcp tooload 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a223-106">Once tables have been created, hello scripts will use bcp tooload data.</span></span>  <span data-ttu-id="8a223-107">Sqlcmd 및 bcp 설치를 모를 경우 다음 링크 너무[bcp 설치] [ install bcp] 및 너무[sqlcmd 설치][install sqlcmd]합니다.</span><span class="sxs-lookup"><span data-stu-id="8a223-107">If you don't already have sqlcmd and bcp installed, follow these links too[install bcp][install bcp] and too[install sqlcmd][install sqlcmd].</span></span>

## <a name="load-sample-data"></a><span data-ttu-id="8a223-108">샘플 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="8a223-108">Load sample data</span></span>
1. <span data-ttu-id="8a223-109">Hello 다운로드 [SQL 데이터 웨어하우스에 대 한 Adventure Works 예제 스크립트] [ Adventure Works Sample Scripts for SQL Data Warehouse] zip 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8a223-109">Download hello [Adventure Works Sample Scripts for SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse] zip file.</span></span>
2. <span data-ttu-id="8a223-110">로컬 컴퓨터에 다운로드 한 zip tooa 디렉터리에서 hello 파일을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a223-110">Extract hello files from downloaded zip tooa directory on your local machine.</span></span>
3. <span data-ttu-id="8a223-111">추출 hello 파일 aw_create.bat 편집한 hello hello 파일의 맨 위에 hello에 변수를 다음으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a223-111">Edit hello extracted file aw_create.bat and set hello following variables found at hello top of hello file.</span></span>  <span data-ttu-id="8a223-112">있는지 tooleave hello "=" hello 매개 변수 사이 공백이 없어야 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a223-112">Be sure tooleave no whitespace between hello "=" and hello parameter.</span></span>  <span data-ttu-id="8a223-113">다음은 사용자가 편집한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="8a223-113">Below are examples of how your edits might look.</span></span>
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. <span data-ttu-id="8a223-114">Windows cmd 프롬프트를 편집 하는 hello aw_create.bat를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a223-114">From a Windows cmd prompt, run hello edited aw_create.bat.</span></span>  <span data-ttu-id="8a223-115">Aw_create.bat의 편집 된 버전을 저장 하는 hello 디렉터리에는 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a223-115">Be sure you are in hello directory where you saved your edited version of aw_create.bat.</span></span>
   <span data-ttu-id="8a223-116">이 스크립트는 다음과 같은 기능을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8a223-116">This script will...</span></span>
   
   * <span data-ttu-id="8a223-117">데이터베이스에 존재하는 Adventure Works 테이블 또는 뷰를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="8a223-117">Drop any Adventure Works tables or views that already exist in your database</span></span>
   * <span data-ttu-id="8a223-118">Hello Adventure Works 테이블 및 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="8a223-118">Create hello Adventure Works tables and views</span></span>
   * <span data-ttu-id="8a223-119">bcp를 사용하여 각각의 Adventure Works 테이블을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8a223-119">Load each Adventure Works table using bcp</span></span>
   * <span data-ttu-id="8a223-120">각 Adventure Works 테이블에 대 한 hello 행 개수 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="8a223-120">Validate hello row counts for each Adventure Works table</span></span>
   * <span data-ttu-id="8a223-121">각 Adventure Works 테이블의 모든 열에 대해 통계를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="8a223-121">Collect statistics on every column for each Adventure Works table</span></span>

## <a name="query-sample-data"></a><span data-ttu-id="8a223-122">쿼리 샘플 데이터</span><span class="sxs-lookup"><span data-stu-id="8a223-122">Query sample data</span></span>
<span data-ttu-id="8a223-123">SQL 데이터 웨어하우스로 샘플 데이터를 로드하고 나면, 몇 가지 쿼리를 신속하게 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a223-123">Once you've loaded some sample data into your SQL Data Warehouse, you can quickly run a few queries.</span></span>  <span data-ttu-id="8a223-124">쿼리를 toorun hello에 설명 된 대로 Visual Studio와 SSDT를 사용 하 여 Azure SQL DW에서 새로 만든 tooyour Adventure Works 데이터베이스 연결 [Visual Studio와 함께 쿼리] [ query with Visual Studio] 문서.</span><span class="sxs-lookup"><span data-stu-id="8a223-124">toorun a query, connect tooyour newly created Adventure Works database in Azure SQL DW using Visual Studio and SSDT, as described in hello [query with Visual Studio][query with Visual Studio] document.</span></span>

<span data-ttu-id="8a223-125">간단한 예 문 tooget hello 직원의 모든 hello 정보를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a223-125">Example of simple select statement tooget all hello info of hello employees:</span></span>

```sql
SELECT * FROM DimEmployee;
```

<span data-ttu-id="8a223-126">더 복잡 한 쿼리 구문을 사용 하 여 GROUP BY toolook 같은 hello 총 금액에 모든 판매에 대 한 각 날짜에 대 한 예:</span><span class="sxs-lookup"><span data-stu-id="8a223-126">Example of a more complex query using constructs such as GROUP BY toolook at hello total amount for all sales on each day:</span></span>

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="8a223-127">특정 날짜 이전의 주문은 아웃 WHERE 절 toofilter 사용 하 여 SELECT의 예:</span><span class="sxs-lookup"><span data-stu-id="8a223-127">Example of a SELECT with a WHERE clause toofilter out orders from before a certain date:</span></span>

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="8a223-128">SQL 데이터 웨어하우스는 SQL Server가 지원하는 거의 모든 T-SQL 구문을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8a223-128">SQL Data Warehouse supports almost all T-SQL constructs which SQL Server supports.</span></span>  <span data-ttu-id="8a223-129">차이점은 [코드 마이그레이션][migrate code] 문서에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a223-129">Any differences are documented in our [migrate code][migrate code] documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a223-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8a223-130">Next steps</span></span>
<span data-ttu-id="8a223-131">기회 tootry 샘플 데이터로 일부 쿼리 살펴봤으므로, 이제는 확인 방법에 대해 너무[개발][develop], [로드][load], 또는 [ 마이그레이션] [ migrate] tooSQL 데이터 웨어하우스 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a223-131">Now that you've had a chance tootry some queries with sample data, check out how too[develop][develop], [load][load], or [migrate][migrate] tooSQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[query with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[migrate code]: sql-data-warehouse-migrate-code.md
[install bcp]: sql-data-warehouse-load-with-bcp.md
[install sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--Other Web references-->
[Adventure Works Sample Scripts for SQL Data Warehouse]: https://migrhoststorage.blob.core.windows.net/sqldwsample/AdventureWorksSQLDW2012.zip

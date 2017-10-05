---
title: "샘플 데이터를 SQL Data Warehouse에 로드 | Microsoft Docs"
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
ms.openlocfilehash: 1e0df958a2f18fe1e988168918e5cfd293f84e64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a><span data-ttu-id="fd17e-103">SQL 데이터 웨어하우스로 샘플 데이터를 로드</span><span class="sxs-lookup"><span data-stu-id="fd17e-103">Load sample data into SQL Data Warehouse</span></span>
<span data-ttu-id="fd17e-104">다음의 간단한 단계에 따라 Adventure Works 샘플 데이터베이스를 로드하고 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-104">Follow these simple steps to load and query the Adventure Works Sample database.</span></span> <span data-ttu-id="fd17e-105">이러한 스크립트는 먼저 sqlcmd를 사용하여 테이블 및 뷰를 만드는 SQL을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-105">These scripts first use sqlcmd to run SQL which will create tables and views.</span></span> <span data-ttu-id="fd17e-106">테이블을 만든 후 스크립트는 bcp를 사용하여 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-106">Once tables have been created, the scripts will use bcp to load data.</span></span>  <span data-ttu-id="fd17e-107">sqlcmd 및 bcp가 아직 설치되어 있지 않다면 다음 링크를 따라 [bcp를 설치][install bcp]하고 [sqlcmd를 설치][install sqlcmd]합니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-107">If you don't already have sqlcmd and bcp installed, follow these links to [install bcp][install bcp] and to [install sqlcmd][install sqlcmd].</span></span>

## <a name="load-sample-data"></a><span data-ttu-id="fd17e-108">샘플 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="fd17e-108">Load sample data</span></span>
1. <span data-ttu-id="fd17e-109">[SQL Data Warehouse용 Adventure Works 샘플 스크립트][Adventure Works Sample Scripts for SQL Data Warehouse] Zip 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-109">Download the [Adventure Works Sample Scripts for SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse] zip file.</span></span>
2. <span data-ttu-id="fd17e-110">사용자의 로컬 컴퓨터 디렉터리에 다운로드한 zip 파일의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-110">Extract the files from downloaded zip to a directory on your local machine.</span></span>
3. <span data-ttu-id="fd17e-111">압축을 푼 aw_create.bat 파일을 편집하고 파일 위쪽에서 다음 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-111">Edit the extracted file aw_create.bat and set the following variables found at the top of the file.</span></span>  <span data-ttu-id="fd17e-112">"="와 매개 변수 사이에 공백이 없도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-112">Be sure to leave no whitespace between the "=" and the parameter.</span></span>  <span data-ttu-id="fd17e-113">다음은 사용자가 편집한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-113">Below are examples of how your edits might look.</span></span>
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. <span data-ttu-id="fd17e-114">편집한 aw_create.bat 파일을 Windows cmd 프롬프트에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-114">From a Windows cmd prompt, run the edited aw_create.bat.</span></span>  <span data-ttu-id="fd17e-115">aw_create.bat 파일의 편집 버전을 저장한 디렉터리에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-115">Be sure you are in the directory where you saved your edited version of aw_create.bat.</span></span>
   <span data-ttu-id="fd17e-116">이 스크립트는 다음과 같은 기능을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-116">This script will...</span></span>
   
   * <span data-ttu-id="fd17e-117">데이터베이스에 존재하는 Adventure Works 테이블 또는 뷰를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-117">Drop any Adventure Works tables or views that already exist in your database</span></span>
   * <span data-ttu-id="fd17e-118">Adventure Works 테이블 및 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-118">Create the Adventure Works tables and views</span></span>
   * <span data-ttu-id="fd17e-119">bcp를 사용하여 각각의 Adventure Works 테이블을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-119">Load each Adventure Works table using bcp</span></span>
   * <span data-ttu-id="fd17e-120">각 Adventure Works 테이블의 행 개수를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-120">Validate the row counts for each Adventure Works table</span></span>
   * <span data-ttu-id="fd17e-121">각 Adventure Works 테이블의 모든 열에 대해 통계를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-121">Collect statistics on every column for each Adventure Works table</span></span>

## <a name="query-sample-data"></a><span data-ttu-id="fd17e-122">쿼리 샘플 데이터</span><span class="sxs-lookup"><span data-stu-id="fd17e-122">Query sample data</span></span>
<span data-ttu-id="fd17e-123">SQL 데이터 웨어하우스로 샘플 데이터를 로드하고 나면, 몇 가지 쿼리를 신속하게 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-123">Once you've loaded some sample data into your SQL Data Warehouse, you can quickly run a few queries.</span></span>  <span data-ttu-id="fd17e-124">쿼리를 실행하려면 [Visual Studio를 사용하여 쿼리][query with Visual Studio] 문서의 설명대로, Visual Studio 및 SSDT를 사용하여 Azure SQL DW에 새로 만든 Adventure Works 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-124">To run a query, connect to your newly created Adventure Works database in Azure SQL DW using Visual Studio and SSDT, as described in the [query with Visual Studio][query with Visual Studio] document.</span></span>

<span data-ttu-id="fd17e-125">직원의 모든 정보를 가져오는 간단한 select 문의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-125">Example of simple select statement to get all the info of the employees:</span></span>

```sql
SELECT * FROM DimEmployee;
```

<span data-ttu-id="fd17e-126">각 날짜의 모든 판매에 대한 총 금액을 살펴보기 위해 GROUP BY 같은 구문을 사용하는 더 복잡한 쿼리의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-126">Example of a more complex query using constructs such as GROUP BY to look at the total amount for all sales on each day:</span></span>

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="fd17e-127">특정 날짜 이전의 주문을 필터링하기 위한 SELECT와 WHERE 절의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-127">Example of a SELECT with a WHERE clause to filter out orders from before a certain date:</span></span>

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="fd17e-128">SQL 데이터 웨어하우스는 SQL Server가 지원하는 거의 모든 T-SQL 구문을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-128">SQL Data Warehouse supports almost all T-SQL constructs which SQL Server supports.</span></span>  <span data-ttu-id="fd17e-129">차이점은 [코드 마이그레이션][migrate code] 문서에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-129">Any differences are documented in our [migrate code][migrate code] documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd17e-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fd17e-130">Next steps</span></span>
<span data-ttu-id="fd17e-131">샘플 데이터로 몇 가지 쿼리를 시도해 볼 기회를 가졌으니, SQL Data Warehouse로 [개발][develop], [로드][load] 또는 [마이그레이션][migrate]하는 방법에 대해 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fd17e-131">Now that you've had a chance to try some queries with sample data, check out how to [develop][develop], [load][load], or [migrate][migrate] to SQL Data Warehouse.</span></span>

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

---
title: "Azure SQL Data Warehouse의 T-SQL 루프 활용 | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 Transact-SQL 루프 및 커서 대체를 위한 팁."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f3384b81-b943-431b-bc73-90e47e4c195f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 40a872ff310f48bfd543ac184fe7301b85b50258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="loops-in-sql-data-warehouse"></a><span data-ttu-id="2ac25-103">SQL 데이터 웨어하우스의 루프</span><span class="sxs-lookup"><span data-stu-id="2ac25-103">Loops in SQL Data Warehouse</span></span>
<span data-ttu-id="2ac25-104">SQL Data Warehouse는 문 블록을 반복 실행하기 위한 [WHILE][WHILE] 루프를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac25-104">SQL Data Warehouse supports the [WHILE][WHILE] loop for repeatedly executing statement blocks.</span></span> <span data-ttu-id="2ac25-105">이 루프는 지정한 조건이 true이거나 코드가 `BREAK` 키워드를 사용하여 루프를 명시적으로 종료할 때까지 계속됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ac25-105">This will continue for as long as the specified conditions are true or until the code specifically terminates the loop using the `BREAK` keyword.</span></span> <span data-ttu-id="2ac25-106">루프는 SQL 코드에 정의된 커서를 대체하는 데 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac25-106">Loops are particularly useful for replacing cursors defined in SQL code.</span></span> <span data-ttu-id="2ac25-107">다행히 SQL 코드로 작성된 거의 모든 커서는 빠른 정방향 읽기 전용 변형만 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac25-107">Fortunately, almost all cursors that are written in SQL code are of the fast forward, read only variety.</span></span> <span data-ttu-id="2ac25-108">따라서 [WHILE] 루프는 무언가를 대체해야 하는 경우 좋은 대안입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac25-108">Therefore [WHILE] loops are a great alternative if you find yourself having to replace one.</span></span>

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a><span data-ttu-id="2ac25-109">SQL 데이터 웨어하우스에서 루프 활용 및 커서 대체</span><span class="sxs-lookup"><span data-stu-id="2ac25-109">Leveraging loops and replacing cursors in SQL Data Warehouse</span></span>
<span data-ttu-id="2ac25-110">그러나 계속 진행하기 전에 먼저 스스로 질문해 보아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac25-110">However, before diving in head first you should ask yourself the following question: "Could this cursor be re-written to use set based operations?".</span></span> <span data-ttu-id="2ac25-111">"이 커서를 집합 기반 작업을 사용하도록 다시 작성할 수 있는가?" 대부분의 경우에서 응답은 '그렇다'이며 보통 가장 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac25-111">In many cases the answer will be yes and is often the best approach.</span></span> <span data-ttu-id="2ac25-112">집합 기반 작업은 흔히 행별 반복 접근 방식보다 훨씬 더 빠르게 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ac25-112">A set based operation often performs significantly faster than an iterative, row by row approach.</span></span>

<span data-ttu-id="2ac25-113">빠른 정방향 읽기 전용 커서는 루핑 구성으로 쉽게 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac25-113">Fast forward read-only cursors can be easily replaced with a looping construct.</span></span> <span data-ttu-id="2ac25-114">다음은 간단한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac25-114">Below is a simple example.</span></span> <span data-ttu-id="2ac25-115">이 코드 예제는 데이터베이스의 모든 테이블에 대한 통계를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac25-115">This code example updates the statistics for every table in the database.</span></span> <span data-ttu-id="2ac25-116">루프의 테이블을 반복하여 각 명령을 순차적으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac25-116">By iterating over the tables in the loop we are able to execute each command in sequence.</span></span>

<span data-ttu-id="2ac25-117">첫째, 개별 문을 식별하는 데 사용되는 고유한 행 번호를 포함하는 임시 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ac25-117">First, create a temporary table containing a unique row number used to identify the individual statements:</span></span>

```
CREATE TABLE #tbl
WITH
( DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS Sequence
,       [name]
,       'UPDATE STATISTICS '+QUOTENAME([name]) AS sql_code
FROM    sys.tables
;
```

<span data-ttu-id="2ac25-118">둘째, 루프를 수행하는 데 필요한 변수를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac25-118">Second, initialize the variables required to perform the loop:</span></span>

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

<span data-ttu-id="2ac25-119">이제 문을 반복하여 한 번에 하나씩 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac25-119">Now loop over statements executing them one at a time:</span></span>

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

<span data-ttu-id="2ac25-120">마지막으로 첫 번째 단계에서 만든 임시 테이블을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac25-120">Finally drop the temporary table created in the first step</span></span>

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->

## <a name="next-steps"></a><span data-ttu-id="2ac25-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2ac25-121">Next steps</span></span>
<span data-ttu-id="2ac25-122">더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ac25-122">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
<span data-ttu-id="2ac25-123">[WHILE]: https://msdn.microsoft.com/library/ms178642.aspx</span><span class="sxs-lookup"><span data-stu-id="2ac25-123">[WHILE]: https://msdn.microsoft.com/library/ms178642.aspx</span></span>


<!--Other Web references-->

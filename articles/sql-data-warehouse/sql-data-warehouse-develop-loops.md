---
title: "Azure SQL 데이터 웨어하우스에 aaaLeverage T-SQL 루프 | Microsoft Docs"
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
ms.openlocfilehash: c7e8f71b910d00d0dfc30f6e5eba190fd05014b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="loops-in-sql-data-warehouse"></a><span data-ttu-id="551da-103">SQL 데이터 웨어하우스의 루프</span><span class="sxs-lookup"><span data-stu-id="551da-103">Loops in SQL Data Warehouse</span></span>
<span data-ttu-id="551da-104">SQL 데이터 웨어하우스 지원 hello [동안][동안] 루프를 반복 해 서 문 블록을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="551da-104">SQL Data Warehouse supports hello [WHILE][WHILE] loop for repeatedly executing statement blocks.</span></span> <span data-ttu-id="551da-105">Hello 조건에 지정 된 상태로 또는까지 hello 코드 hello를 사용 하 여 hello 루프를 특별히 종료에 대 한이 계속 됩니다 `BREAK` 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="551da-105">This will continue for as long as hello specified conditions are true or until hello code specifically terminates hello loop using hello `BREAK` keyword.</span></span> <span data-ttu-id="551da-106">루프는 SQL 코드에 정의된 커서를 대체하는 데 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="551da-106">Loops are particularly useful for replacing cursors defined in SQL code.</span></span> <span data-ttu-id="551da-107">다행히 SQL 코드로 작성 된 거의 모든 커서의 빠른 hello 앞으로 읽혀집니다 다양 한만.</span><span class="sxs-lookup"><span data-stu-id="551da-107">Fortunately, almost all cursors that are written in SQL code are of hello fast forward, read only variety.</span></span> <span data-ttu-id="551da-108">따라서 [동안] tooreplace 하나 있는 경우 루프는 대신 사용 하면 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="551da-108">Therefore [WHILE] loops are a great alternative if you find yourself having tooreplace one.</span></span>

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a><span data-ttu-id="551da-109">SQL 데이터 웨어하우스에서 루프 활용 및 커서 대체</span><span class="sxs-lookup"><span data-stu-id="551da-109">Leveraging loops and replacing cursors in SQL Data Warehouse</span></span>
<span data-ttu-id="551da-110">그러나 먼저 h e a d 우선 고려해 야 할 질문 다음 hello: "이이 커서 수 다시 쓰지 toouse 집합 기반 연산은?"입니다.</span><span class="sxs-lookup"><span data-stu-id="551da-110">However, before diving in head first you should ask yourself hello following question: "Could this cursor be re-written toouse set based operations?".</span></span> <span data-ttu-id="551da-111">대부분의 경우에서 hello 응답을 yes 되며 hello 가장 좋은 방법이 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="551da-111">In many cases hello answer will be yes and is often hello best approach.</span></span> <span data-ttu-id="551da-112">집합 기반 작업은 흔히 행별 반복 접근 방식보다 훨씬 더 빠르게 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="551da-112">A set based operation often performs significantly faster than an iterative, row by row approach.</span></span>

<span data-ttu-id="551da-113">빠른 정방향 읽기 전용 커서는 루핑 구성으로 쉽게 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="551da-113">Fast forward read-only cursors can be easily replaced with a looping construct.</span></span> <span data-ttu-id="551da-114">다음은 간단한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="551da-114">Below is a simple example.</span></span> <span data-ttu-id="551da-115">이 코드 예제는 hello 데이터베이스의 모든 테이블에 대 한 hello 통계를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="551da-115">This code example updates hello statistics for every table in hello database.</span></span> <span data-ttu-id="551da-116">Hello 루프의 hello 테이블에서는 반복 하 여 시퀀스의 각 명령이 수 tooexecute 됩니다.</span><span class="sxs-lookup"><span data-stu-id="551da-116">By iterating over hello tables in hello loop we are able tooexecute each command in sequence.</span></span>

<span data-ttu-id="551da-117">먼저, 문을 포함 하는 고유한 행 번호 사용 되는 tooidentify hello 개별 임시 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="551da-117">First, create a temporary table containing a unique row number used tooidentify hello individual statements:</span></span>

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

<span data-ttu-id="551da-118">둘째, hello 변수 필요한 tooperform hello 루프를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="551da-118">Second, initialize hello variables required tooperform hello loop:</span></span>

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

<span data-ttu-id="551da-119">이제 문을 반복하여 한 번에 하나씩 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="551da-119">Now loop over statements executing them one at a time:</span></span>

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

<span data-ttu-id="551da-120">마지막으로 hello 첫 번째 단계에서 만든 hello 임시 테이블을 삭제</span><span class="sxs-lookup"><span data-stu-id="551da-120">Finally drop hello temporary table created in hello first step</span></span>

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a><span data-ttu-id="551da-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="551da-121">Next steps</span></span>
<span data-ttu-id="551da-122">더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="551da-122">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[동안]: https://msdn.microsoft.com/library/ms178642.aspx


<!--Other Web references-->

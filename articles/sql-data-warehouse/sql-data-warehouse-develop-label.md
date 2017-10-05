---
title: "SQL Data Warehouse에서 레이블을 사용하여 쿼리 계측 | Microsoft Docs"
description: "솔루션 개발을 위해 Azure SQL 데이터 웨어하우스에서 레이블을 사용하여 쿼리를 계측하기 위한 팁."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 44988de8-04c1-4fed-92be-e1935661a4e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9e75bbe528a427724a623305fbd45e2277e9d0af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-labels-to-instrument-queries-in-sql-data-warehouse"></a><span data-ttu-id="7295e-103">SQL 데이터 웨어하우스에서 레이블을 사용하여 쿼리 계측</span><span class="sxs-lookup"><span data-stu-id="7295e-103">Use labels to instrument queries in SQL Data Warehouse</span></span>
<span data-ttu-id="7295e-104">SQL 데이터 웨어하우스는 쿼리 레이블이라는 개념을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7295e-104">SQL Data Warehouse supports a concept called query labels.</span></span> <span data-ttu-id="7295e-105">좀더 깊이 들어가기 전에 한 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7295e-105">Before going into any depth let's look at an example of one:</span></span>

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

<span data-ttu-id="7295e-106">이 마지막 줄은 쿼리에 문자열 '내 쿼리 레이블' 태그를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7295e-106">This last line tags the string 'My Query Label' to the query.</span></span> <span data-ttu-id="7295e-107">레이블은 DMV를 통해 쿼리가 가능하므로 이 태그는 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="7295e-107">This is particularly helpful as the label is query-able through the DMVs.</span></span> <span data-ttu-id="7295e-108">이 기능은 문제 쿼리를 추적하는 메커니즘을 제공하며 ETL 실행을 통해 진행률을 식별하는 데에도 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7295e-108">This provides us with a mechanism to track down problem queries and also to help identify progress through an ETL run.</span></span>

<span data-ttu-id="7295e-109">여기서 좋은 명명 규칙이 큰 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7295e-109">A good naming convention really helps here.</span></span> <span data-ttu-id="7295e-110">예를 들어 ' PROJECT : PROCEDURE : STATEMENT : COMMENT' 같은 문은 원본 제어의 모든 코드 중에서 쿼리를 고유하게 식별하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7295e-110">For example something like ' PROJECT : PROCEDURE : STATEMENT : COMMENT' would help to uniquely identify the query in amongst all the code in source control.</span></span>

<span data-ttu-id="7295e-111">레이블 기준으로 검색하려면 동적 관리 보기를 사용하는 다음과 같은 쿼리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7295e-111">To search by label you can use the following query that uses the dynamic management views:</span></span>

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> <span data-ttu-id="7295e-112">쿼리할 때 반드시 단어 레이블을 대괄호 또는 큰따옴표로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7295e-112">It is essential that you wrap square brackets or double quotes around the word label when querying.</span></span> <span data-ttu-id="7295e-113">레이블은 예약어이며 구분하지 않으면 오류를 야기합니다.</span><span class="sxs-lookup"><span data-stu-id="7295e-113">Label is a reserved word and will caused an error if it has not been delimited.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7295e-114">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7295e-114">Next steps</span></span>
<span data-ttu-id="7295e-115">더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7295e-115">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->

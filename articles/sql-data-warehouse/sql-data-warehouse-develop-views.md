---
title: "Azure SQL Data Warehouse의 T-SQL 뷰 사용 | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 Transact-SQL 뷰 사용을 위한 팁"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: b5208f32-8f4a-4056-8788-2adbb253d9fd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: d2a03be810bd7f792876607ec735eb578b65a3b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="views-in-sql-data-warehouse"></a><span data-ttu-id="3a337-103">SQL 데이터 웨어하우스의 뷰</span><span class="sxs-lookup"><span data-stu-id="3a337-103">Views in SQL Data Warehouse</span></span>
<span data-ttu-id="3a337-104">뷰는 SQL 데이터 웨어하우스에서 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-104">Views are particularly useful in SQL Data Warehouse.</span></span> <span data-ttu-id="3a337-105">여러가지 다양한 방법을 사용하여 솔루션의 품질을 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-105">They can be used in a number of different ways to improve the quality of your solution.</span></span>  <span data-ttu-id="3a337-106">이 문서에서는 고려해야 할 제한 사항 뿐만 아니라 뷰를 통해 솔루션을 보완하는 방법의 예도 중점적으로 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-106">This article highlights a few examples of how to enrich your solution with views, as well as the limitations that need to be considered.</span></span>

> [!NOTE]
> <span data-ttu-id="3a337-107">`CREATE VIEW`에 대한 구문은 이 문서에서 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-107">Syntax for `CREATE VIEW` is not discussed in this article.</span></span> <span data-ttu-id="3a337-108">이 참조 정보에 대해서는 MSDN의 [CREATE VIEW][CREATE VIEW] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a337-108">Please refer to the [CREATE VIEW][CREATE VIEW] article on MSDN for this reference information.</span></span>
> 
> 

## <a name="architectural-abstraction"></a><span data-ttu-id="3a337-109">아키텍처 추상화</span><span class="sxs-lookup"><span data-stu-id="3a337-109">Architectural abstraction</span></span>
<span data-ttu-id="3a337-110">매우 일반적인 응용 프로그램 패턴은 CREATE TABLE AS SELECT (CTAS) 뒤에 데이터 로드 중 개체 이름 바꾸기 패턴을 사용하여 테이블을 다시 작성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-110">A very common application pattern is to re-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span></span>

<span data-ttu-id="3a337-111">다음 예제에서는 새 날짜 레코드를 날짜 차원에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-111">The example below adds new date records to a date dimension.</span></span> <span data-ttu-id="3a337-112">먼저 새 테이블 DimDate_New를 만든 다음 이름을 바꾸어 원래 버전의 테이블을 바꾸는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-112">Note how a new tabble, DimDate_New, is first created and then renamed to replace the original version of the table.</span></span>

```sql
CREATE TABLE dbo.DimDate_New
WITH (DISTRIBUTION = ROUND_ROBIN
, CLUSTERED INDEX (DateKey ASC)
)
AS
SELECT *
FROM   dbo.DimDate  AS prod
UNION ALL
SELECT *
FROM   dbo.DimDate_stg AS stg
;

RENAME OBJECT DimDate TO DimDate_Old;
RENAME OBJECT DimDate_New TO DimDate;

```

<span data-ttu-id="3a337-113">그러나 이 방법을 사용하면 뷰에서 테이블이 표시되었다가 사라질 수 있으며 "테이블이 없습니다." 오류 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-113">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span></span> <span data-ttu-id="3a337-114">뷰는 원본 개체의 이름을 바꾸는 동안 일관성 있는 프레젠테이션 계층을 제공하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-114">Views can be used to provide users with a consistent presentation layer whilst the underlying objects are renamed.</span></span> <span data-ttu-id="3a337-115">뷰를 통해 데이터에 액세스할 수 있도록 하기 때문에 사용자에게 기본 테이블이 표시되는지 여부는 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-115">By providing users access to the data through a views, means users don't need to have visibility of the underlying tables.</span></span> <span data-ttu-id="3a337-116">데이터 웨어하우스 설계자가 데이터 모델을 발전시키고 데이터 로드 프로세스 중 CTAS를 사용하여 성능을 극대화할 수 있는지 확인하는 동안 일관된 사용자 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-116">This provides a consistent user experience while ensuring that the data warehouse designers can evolve the data model and maximize performance by using CTAS during the data loading process.</span></span>    

## <a name="performance-optimization"></a><span data-ttu-id="3a337-117">성능 최적화</span><span class="sxs-lookup"><span data-stu-id="3a337-117">Performance optimization</span></span>
<span data-ttu-id="3a337-118">뷰는 테이블 간에 성능 최적화된 조인을 적용하는 데도 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-118">Views can also be utilized to enforce performance optimized joins between tables.</span></span> <span data-ttu-id="3a337-119">예를 들어, 뷰는 데이터 이동을 최소화하는 조인 조건의 일부로 배포 중복 키를 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-119">For example, a view can incorporate a redundant distribution key as part of the joining criteria to minimize data movement.</span></span>  <span data-ttu-id="3a337-120">뷰의 또 다른 장점은 특정 쿼리 또는 조인 힌트를 강제 적용할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-120">Another benefit of a view could be to force a specific query or joining hint.</span></span> <span data-ttu-id="3a337-121">이 방식으로 뷰를 사용하면 조인이 항상 최적의 방식으로 수행되므로 사용자가 자신의 조인에 대한 올바른 구문을 기억해야 할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-121">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding the need for users to remember the correct construct for their joins.</span></span>

## <a name="limitations"></a><span data-ttu-id="3a337-122">제한 사항</span><span class="sxs-lookup"><span data-stu-id="3a337-122">Limitations</span></span>
<span data-ttu-id="3a337-123">SQL 데이터 웨어하우스의 뷰는 메타데이터 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-123">Views in SQL Data Warehouse are metadata only.</span></span>  <span data-ttu-id="3a337-124">따라서 다음 옵션을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-124">Consequently the following options are not available:</span></span>

* <span data-ttu-id="3a337-125">스키마 바인딩 옵션이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-125">There is no schema binding option</span></span>
* <span data-ttu-id="3a337-126">뷰를 통해 기본 테이블을 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-126">Base tables cannot be updated through the view</span></span>
* <span data-ttu-id="3a337-127">임시 테이블에 대해 뷰를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-127">Views cannot be created over temporary tables</span></span>
* <span data-ttu-id="3a337-128">EXPAND / NOEXPAND 힌트에 대한 지원이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-128">There is no support for the EXPAND / NOEXPAND hints</span></span>
* <span data-ttu-id="3a337-129">SQL 데이터 웨어하우스에 인덱싱된 뷰가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a337-129">There are no indexed views in SQL Data Warehouse</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a337-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3a337-130">Next steps</span></span>
<span data-ttu-id="3a337-131">더 많은 개발 팁은 [SQL Data Warehouse 개발 개요][SQL Data Warehouse development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a337-131">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="3a337-132">`CREATE VIEW` 구문에 대해서는 [CREATE VIEW][CREATE VIEW]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a337-132">For `CREATE VIEW` syntax please refer to [CREATE VIEW][CREATE VIEW].</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->

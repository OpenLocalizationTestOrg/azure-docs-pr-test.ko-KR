---
title: "Azure SQL 데이터 웨어하우스에 aaaUsing T-SQL 보기 | Microsoft Docs"
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
ms.openlocfilehash: 3990b133946621691bdfa4b09523d21867470c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-sql-data-warehouse"></a><span data-ttu-id="efec4-103">SQL 데이터 웨어하우스의 뷰</span><span class="sxs-lookup"><span data-stu-id="efec4-103">Views in SQL Data Warehouse</span></span>
<span data-ttu-id="efec4-104">뷰는 SQL 데이터 웨어하우스에서 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-104">Views are particularly useful in SQL Data Warehouse.</span></span> <span data-ttu-id="efec4-105">다양 한 솔루션의 tooimprove hello 품질 다양 한 방법으로에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-105">They can be used in a number of different ways tooimprove hello quality of your solution.</span></span>  <span data-ttu-id="efec4-106">이 문서에는 어떻게 tooenrich toobe 해야 하는 hello 제한 사항 뿐만 아니라 뷰, 솔루션이 것으로 간주 하는 몇 가지 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-106">This article highlights a few examples of how tooenrich your solution with views, as well as hello limitations that need toobe considered.</span></span>

> [!NOTE]
> <span data-ttu-id="efec4-107">`CREATE VIEW`에 대한 구문은 이 문서에서 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-107">Syntax for `CREATE VIEW` is not discussed in this article.</span></span> <span data-ttu-id="efec4-108">Toohello를 참조 하십시오 [CREATE VIEW] [ CREATE VIEW] MSDN이 참조 정보에 대 한 문서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-108">Please refer toohello [CREATE VIEW][CREATE VIEW] article on MSDN for this reference information.</span></span>
> 
> 

## <a name="architectural-abstraction"></a><span data-ttu-id="efec4-109">아키텍처 추상화</span><span class="sxs-lookup"><span data-stu-id="efec4-109">Architectural abstraction</span></span>
<span data-ttu-id="efec4-110">응용 프로그램의 매우 일반적인 패턴은 toore-만드는 테이블 AS 선택 (CTAS) 뒤에 데이터를 로드 하는 동안 패턴 이름을 변경 하는 개체를 사용 하 여 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-110">A very common application pattern is toore-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span></span>

<span data-ttu-id="efec4-111">다음 예제에서는 hello 새 날짜 레코드 tooa date 차원의 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-111">hello example below adds new date records tooa date dimension.</span></span> <span data-ttu-id="efec4-112">새 tabble DimDate_New, 첫 번째를 어떻게 만들고 tooreplace hello 원래 버전의 hello 테이블 이름을 바꾸면 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-112">Note how a new tabble, DimDate_New, is first created and then renamed tooreplace hello original version of hello table.</span></span>

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

RENAME OBJECT DimDate tooDimDate_Old;
RENAME OBJECT DimDate_New tooDimDate;

```

<span data-ttu-id="efec4-113">그러나 이 방법을 사용하면 뷰에서 테이블이 표시되었다가 사라질 수 있으며 "테이블이 없습니다." 오류 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-113">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span></span> <span data-ttu-id="efec4-114">뷰의는 hello 원본 개체의 이름을 바꾼 하는 동안 일관 된 프레젠테이션 레이어 tooprovide 사용 되는 사용자가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-114">Views can be used tooprovide users with a consistent presentation layer whilst hello underlying objects are renamed.</span></span> <span data-ttu-id="efec4-115">사용자가 액세스를 제공 하 여 뷰를 통해 toohello 데이터는 사용자가 hello 원본 테이블의 toohave 가시성 필요 하지 않습니다 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-115">By providing users access toohello data through a views, means users don't need toohave visibility of hello underlying tables.</span></span> <span data-ttu-id="efec4-116">Hello 데이터 웨어하우스 설계자 수 발전 hello 데이터 모델 고 hello 데이터 로드 프로세스 중 CTAS에는 사용 하 여 성능을 최대화 하 여 일관 된 사용자 환경을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-116">This provides a consistent user experience while ensuring that hello data warehouse designers can evolve hello data model and maximize performance by using CTAS during hello data loading process.</span></span>    

## <a name="performance-optimization"></a><span data-ttu-id="efec4-117">성능 최적화</span><span class="sxs-lookup"><span data-stu-id="efec4-117">Performance optimization</span></span>
<span data-ttu-id="efec4-118">뷰는 테이블 간의 성능에 최적화 된 조인을 과소 tooenforce 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-118">Views can also be utilized tooenforce performance optimized joins between tables.</span></span> <span data-ttu-id="efec4-119">예를 들어 뷰 hello 조인 조건을 toominimize 데이터 이동의 일부로 배포에서 중복 키를 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-119">For example, a view can incorporate a redundant distribution key as part of hello joining criteria toominimize data movement.</span></span>  <span data-ttu-id="efec4-120">보기의 또 다른 이점은 tooforce 특정 쿼리 또는 조인 힌트를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-120">Another benefit of a view could be tooforce a specific query or joining hint.</span></span> <span data-ttu-id="efec4-121">이런이 방식으로 뷰를 사용 하 여 조인 항상 사용자 tooremember hello의 조인에 대 한 올바른 구문에 대 한 hello 필요 방지 최적의 방식으로 수행 되도록 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-121">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding hello need for users tooremember hello correct construct for their joins.</span></span>

## <a name="limitations"></a><span data-ttu-id="efec4-122">제한 사항</span><span class="sxs-lookup"><span data-stu-id="efec4-122">Limitations</span></span>
<span data-ttu-id="efec4-123">SQL 데이터 웨어하우스의 뷰는 메타데이터 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-123">Views in SQL Data Warehouse are metadata only.</span></span>  <span data-ttu-id="efec4-124">따라서 다음 옵션 hello 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-124">Consequently hello following options are not available:</span></span>

* <span data-ttu-id="efec4-125">스키마 바인딩 옵션이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-125">There is no schema binding option</span></span>
* <span data-ttu-id="efec4-126">Hello 뷰를 통해 기본 테이블을 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-126">Base tables cannot be updated through hello view</span></span>
* <span data-ttu-id="efec4-127">임시 테이블에 대해 뷰를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-127">Views cannot be created over temporary tables</span></span>
* <span data-ttu-id="efec4-128">Hello 확장에 대 한 지원은 / NOEXPAND 힌트</span><span class="sxs-lookup"><span data-stu-id="efec4-128">There is no support for hello EXPAND / NOEXPAND hints</span></span>
* <span data-ttu-id="efec4-129">SQL 데이터 웨어하우스에 인덱싱된 뷰가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-129">There are no indexed views in SQL Data Warehouse</span></span>

## <a name="next-steps"></a><span data-ttu-id="efec4-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="efec4-130">Next steps</span></span>
<span data-ttu-id="efec4-131">더 많은 개발 팁은 [SQL Data Warehouse 개발 개요][SQL Data Warehouse development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="efec4-131">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="efec4-132">에 대 한 `CREATE VIEW` 구문 너무 참조 하십시오[CREATE VIEW][CREATE VIEW]합니다.</span><span class="sxs-lookup"><span data-stu-id="efec4-132">For `CREATE VIEW` syntax please refer too[CREATE VIEW][CREATE VIEW].</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->

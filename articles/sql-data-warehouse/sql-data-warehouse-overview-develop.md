---
title: "Azure의 데이터 웨어하우스 개발을 위한 리소스 | Microsoft Docs"
description: "SQL 데이터 웨어하우스에 대한 개발 개념, 디자인 결정, 권장 사항 및 코딩 기술입니다."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: barbkess
editor: 
ms.assetid: 996e3afc-c21c-4e21-b9df-997f953f6dfd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: develop
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: b85a4f09e561e429aa5bf46ec680014487fb40c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a><span data-ttu-id="821ee-103">SQL 데이터 웨어하우스에 대한 디자인 결정 및 코딩 기술</span><span class="sxs-lookup"><span data-stu-id="821ee-103">Design decisions and coding techniques for SQL Data Warehouse</span></span>
<span data-ttu-id="821ee-104">SQL 데이터 웨어하우스에 대한 주요 디자인 결정, 권장 사항 및 코딩 기술을 더 잘 이해하려면 이러한 개발 문서를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="821ee-104">Take a look through these development articles to better understand key design decisions, recommendations and coding techniques for SQL Data Warehouse.</span></span>

## <a name="key-design-decisions"></a><span data-ttu-id="821ee-105">주요 디자인 결정</span><span class="sxs-lookup"><span data-stu-id="821ee-105">Key design decisions</span></span>
<span data-ttu-id="821ee-106">다음 문서는 SQL 데이터 웨어하우스를 사용하여 분산된 데이터 웨어하우스를 개발하기 위해 이해해야 하는 일부 주요 개념과 설계 결정을 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="821ee-106">The following articles highlight some of the key concepts and design decisions you will need to understand for the development of your distributed data warehouse using SQL Data Warehouse:</span></span>

* <span data-ttu-id="821ee-107">[연결][connections]</span><span class="sxs-lookup"><span data-stu-id="821ee-107">[connections][connections]</span></span>
* <span data-ttu-id="821ee-108">[동시성][concurrency]</span><span class="sxs-lookup"><span data-stu-id="821ee-108">[concurrency][concurrency]</span></span>
* <span data-ttu-id="821ee-109">[트랜잭션][transactions]</span><span class="sxs-lookup"><span data-stu-id="821ee-109">[transactions][transactions]</span></span>
* <span data-ttu-id="821ee-110">[사용자 정의 스키마][user-defined schemas]</span><span class="sxs-lookup"><span data-stu-id="821ee-110">[user-defined schemas][user-defined schemas]</span></span>
* <span data-ttu-id="821ee-111">[테이블 배포][table distribution]</span><span class="sxs-lookup"><span data-stu-id="821ee-111">[table distribution][table distribution]</span></span>
* <span data-ttu-id="821ee-112">[테이블 인덱스][table indexes]</span><span class="sxs-lookup"><span data-stu-id="821ee-112">[table indexes][table indexes]</span></span>
* <span data-ttu-id="821ee-113">[테이블 파티션][table partitions]</span><span class="sxs-lookup"><span data-stu-id="821ee-113">[table partitions][table partitions]</span></span>
* <span data-ttu-id="821ee-114">[CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="821ee-114">[CTAS][CTAS]</span></span>
* <span data-ttu-id="821ee-115">[통계][statistics]</span><span class="sxs-lookup"><span data-stu-id="821ee-115">[statistics][statistics]</span></span>

## <a name="development-recommendations-and-coding-techniques"></a><span data-ttu-id="821ee-116">개발 권장 사항 및 코딩 기술</span><span class="sxs-lookup"><span data-stu-id="821ee-116">Development recommendations and coding techniques</span></span>
<span data-ttu-id="821ee-117">이러한 문서에는 SQL 데이터 웨어하우스 개발을 위한 구체적인 코딩 기술, 팁 및 권장 사항이 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="821ee-117">These articles highlight specific coding techniques, tips and recommendations for developing your SQL Data Warehouse:</span></span>

* <span data-ttu-id="821ee-118">[저장 프로시저][stored procedures]</span><span class="sxs-lookup"><span data-stu-id="821ee-118">[stored procedures][stored procedures]</span></span>
* <span data-ttu-id="821ee-119">[레이블][labels]</span><span class="sxs-lookup"><span data-stu-id="821ee-119">[labels][labels]</span></span>
* <span data-ttu-id="821ee-120">[뷰][views]</span><span class="sxs-lookup"><span data-stu-id="821ee-120">[views][views]</span></span>
* <span data-ttu-id="821ee-121">[임시 테이블][temporary tables]</span><span class="sxs-lookup"><span data-stu-id="821ee-121">[temporary tables][temporary tables]</span></span>
* <span data-ttu-id="821ee-122">[동적 SQL][dynamic SQL]</span><span class="sxs-lookup"><span data-stu-id="821ee-122">[dynamic SQL][dynamic SQL]</span></span>
* <span data-ttu-id="821ee-123">[반복][looping]</span><span class="sxs-lookup"><span data-stu-id="821ee-123">[looping][looping]</span></span>
* <span data-ttu-id="821ee-124">[옵션으로 그룹화][group by options]</span><span class="sxs-lookup"><span data-stu-id="821ee-124">[group by options][group by options]</span></span>
* <span data-ttu-id="821ee-125">[변수 할당][variable assignment]</span><span class="sxs-lookup"><span data-stu-id="821ee-125">[variable assignment][variable assignment]</span></span>

## <a name="next-steps"></a><span data-ttu-id="821ee-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="821ee-126">Next steps</span></span>
<span data-ttu-id="821ee-127">개발 문서들을 살펴본 후에는 [Transact-SQL 참조][Transact-SQL reference] 페이지에서 SQL Data Warehouse에 대해 지원되는 구문에 대한 자세한 내용을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="821ee-127">Once you have been through the development articles take a look through the [Transact-SQL reference][Transact-SQL reference] page for more details on the supported syntax for SQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->
[concurrency]: ./sql-data-warehouse-develop-concurrency.md
[connections]: ./sql-data-warehouse-connect-overview.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[dynamic SQL]: ./sql-data-warehouse-develop-dynamic-sql.md
[group by options]: ./sql-data-warehouse-develop-group-by-options.md
[labels]: ./sql-data-warehouse-develop-label.md
[looping]: ./sql-data-warehouse-develop-loops.md
[statistics]: ./sql-data-warehouse-tables-statistics.md
[stored procedures]: ./sql-data-warehouse-develop-stored-procedures.md
[table distribution]: ./sql-data-warehouse-tables-distribute.md
[table indexes]: ./sql-data-warehouse-tables-index.md
[table partitions]: ./sql-data-warehouse-tables-partition.md
[temporary tables]: ./sql-data-warehouse-tables-temporary.md
[transactions]: ./sql-data-warehouse-develop-transactions.md
[user-defined schemas]: ./sql-data-warehouse-develop-user-defined-schemas.md
[variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[views]: ./sql-data-warehouse-develop-views.md
[Transact-SQL reference]: ./sql-data-warehouse-overview-reference.md

<!--MSDN references-->
[renaming objects]: https://msdn.microsoft.com/library/mt631611.aspx

<!--Other Web references-->

---
title: "SQL 데이터 웨어하우스에 aaaUser 정의 스키마 | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 Transact-SQL 스키마 사용을 위한 팁"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 52af5bd5-d5d3-4f9b-8704-06829fb924e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c411d6fed68e67c444a5871eab06182eaeb6dbf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a><span data-ttu-id="f74c5-103">SQL 데이터 웨어하우스의 사용자 정의 스키마</span><span class="sxs-lookup"><span data-stu-id="f74c5-103">User-defined schemas in SQL Data Warehouse</span></span>
<span data-ttu-id="f74c5-104">일반적인 데이터 웨어하우스 작업, 도메인 또는 보안을 기반으로 자주 사용 하 여 별도 데이터베이스 toocreate 응용 프로그램 경계입니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-104">Traditional data warehouses often use separate databases toocreate application boundaries based on either workload, domain or security.</span></span> <span data-ttu-id="f74c5-105">예를 들어, 기존의 SQL Server 데이터 웨어하우스는 스테이징 데이터베이스, 데이터 웨어하우스 데이터베이스 및 일부 데이터마트 데이터베이스를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-105">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="f74c5-106">이 토폴로지에서 각 데이터베이스 작업 부하 및 보안 경계 hello 아키텍처에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-106">In this topology each database operates as a workload and security boundary in hello architecture.</span></span>

<span data-ttu-id="f74c5-107">반면, SQL 데이터 웨어하우스 데이터베이스 내에 hello 전체 데이터 웨어하우스 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-107">By contrast, SQL Data Warehouse runs hello entire data warehouse workload within one database.</span></span> <span data-ttu-id="f74c5-108">데이터베이스 간 조인은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-108">Cross database joins are not permitted.</span></span> <span data-ttu-id="f74c5-109">따라서 SQL 데이터 웨어하우스는 hello 웨어하우스 toobe hello 한 데이터베이스에 저장 된 사용 되는 모든 테이블을 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-109">Therefore SQL Data Warehouse expects all tables used by hello warehouse toobe stored within hello one database.</span></span>

> [!NOTE]
> <span data-ttu-id="f74c5-110">SQL 데이터 웨어하우스는 모든 종류의 데이터베이스 간 쿼리를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-110">SQL Data Warehouse does not support cross database queries of any kind.</span></span> <span data-ttu-id="f74c5-111">따라서이 패턴을 활용 하는 데이터 웨어하우스 구현 toobe 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-111">Consequently, data warehouse implementations that leverage this pattern will need toobe revised.</span></span>
> 
> 

## <a name="recommendations"></a><span data-ttu-id="f74c5-112">권장 사항</span><span class="sxs-lookup"><span data-stu-id="f74c5-112">Recommendations</span></span>
<span data-ttu-id="f74c5-113">사용자 정의 스키마를 사용하여 워크로드, 보안, 도메인 및 기능 경계를 통합하기 위한 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-113">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span></span>

1. <span data-ttu-id="f74c5-114">한 SQL 데이터 웨어하우스 데이터베이스 toorun 전체 데이터 웨어하우스 작업 사용</span><span class="sxs-lookup"><span data-stu-id="f74c5-114">Use one SQL Data Warehouse database toorun your entire data warehouse workload</span></span>
2. <span data-ttu-id="f74c5-115">기존 데이터 웨어하우스 환경 toouse 한 SQL 데이터 웨어하우스 데이터베이스를 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-115">Consolidate your existing data warehouse environment toouse one SQL Data Warehouse database</span></span>
3. <span data-ttu-id="f74c5-116">활용 **사용자 정의 스키마** tooprovide hello 경계 이전에 데이터베이스를 사용 하 여를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-116">Leverage **user-defined schemas** tooprovide hello boundary previously implemented using databases.</span></span>

<span data-ttu-id="f74c5-117">사용자 정의 스키마를 이전에 사용하지 않은 경우, 초기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-117">If user-defined schemas have not been used previously then you have a clean slate.</span></span> <span data-ttu-id="f74c5-118">Hello SQL 데이터 웨어하우스 데이터베이스에 사용자 정의 스키마에 대 한 hello 기준으로 이전 데이터베이스 이름을 hello를 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-118">Simply use hello old database name as hello basis for your user-defined schemas in hello SQL Data Warehouse database.</span></span>

<span data-ttu-id="f74c5-119">스키마가 이미 사용된 경우 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-119">If schemas have already been used then you have a few options:</span></span>

1. <span data-ttu-id="f74c5-120">Hello 레거시 스키마 이름을 제거 하 고 새로 시작</span><span class="sxs-lookup"><span data-stu-id="f74c5-120">Remove hello legacy schema names and start fresh</span></span>
2. <span data-ttu-id="f74c5-121">Hello 레거시 스키마 이름에는 미리 보류 중인 hello 레거시 스키마 이름 toohello 테이블 이름으로 유지</span><span class="sxs-lookup"><span data-stu-id="f74c5-121">Retain hello legacy schema names by pre-pending hello legacy schema name toohello table name</span></span>
3. <span data-ttu-id="f74c5-122">추가 스키마 toore에 hello 테이블에 대해 뷰를 구현 하 여 hello 레거시 스키마 이름을 유지-hello 이전 스키마 구조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-122">Retain hello legacy schema names by implementing views over hello table in an extra schema toore-create hello old schema structure.</span></span>

> [!NOTE]
> <span data-ttu-id="f74c5-123">첫 번째 검사에서 옵션 3 hello 가장 매력적인 옵션 처럼 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-123">On first inspection option 3 may seem like hello most appealing option.</span></span> <span data-ttu-id="f74c5-124">그러나 hello 악마 hello 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-124">However, hello devil is in hello detail.</span></span> <span data-ttu-id="f74c5-125">뷰는 SQL 데이터 웨어하우스에서만 읽혀집니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-125">Views are read only in SQL Data Warehouse.</span></span> <span data-ttu-id="f74c5-126">데이터 또는 테이블 수정 하지 않고도 모든 toobe hello 기본 테이블에 대해 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-126">Any data or table modification would need toobe performed against hello base table.</span></span> <span data-ttu-id="f74c5-127">또한 옵션 3은 시스템으로의 뷰 레이어를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-127">Option 3 also introduces a layer of views into your system.</span></span> <span data-ttu-id="f74c5-128">아키텍처의 뷰 이미 사용 중인 경우이 몇 가지 사항을 고려해 야 toogive 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-128">You might want toogive this some additional thought if you are using views in your architecture already.</span></span>
> 
> 

### <a name="examples"></a><span data-ttu-id="f74c5-129">예제:</span><span class="sxs-lookup"><span data-stu-id="f74c5-129">Examples:</span></span>
<span data-ttu-id="f74c5-130">데이터베이스 이름을 기반으로 사용자 정의 스키마를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-130">Implement user-defined schemas based on database names</span></span>

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for hello data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in hello stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in hello edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="f74c5-131">유지 레거시 스키마 폴더 이름을 여 toohello 테이블 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-131">Retain legacy schema names by pre-pending them toohello table name.</span></span> <span data-ttu-id="f74c5-132">Hello 작업 경계에 대 한 스키마를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-132">Use schemas for hello workload boundary.</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines hello data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend hello old schema name toohello table and create in hello staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend hello old schema name toohello table and create in hello data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="f74c5-133">뷰를 사용하여 레거시 스키마 이름을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-133">Retain legacy schema names using views</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines hello data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines hello legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create hello base staging tables in hello staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create hello base data warehouse tables in hello data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in hello legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> <span data-ttu-id="f74c5-134">스키마 전략에 변경 내용을 hello 데이터베이스에 대 한 hello 보안 모델의 검토를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-134">Any change in schema strategy needs a review of hello security model for hello database.</span></span> <span data-ttu-id="f74c5-135">대부분의 경우에서 hello 스키마 수준에서 사용 권한을 할당 하 여 수 toosimplify hello 보안 모델을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-135">In many cases you might be able toosimplify hello security model by assigning permissions at hello schema level.</span></span> <span data-ttu-id="f74c5-136">보다 세부적인 사용 권한이 필요한 경우 데이터베이스 역할을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f74c5-136">If more granular permissions are required then you can use database roles.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f74c5-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f74c5-137">Next steps</span></span>
<span data-ttu-id="f74c5-138">더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f74c5-138">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->

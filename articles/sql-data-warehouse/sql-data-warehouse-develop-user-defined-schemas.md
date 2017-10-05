---
title: "SQL Data Warehouse의 사용자 정의 스키마 | Microsoft Docs"
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
ms.openlocfilehash: dfb58956ad6637cf0f50b4c052ab98fb7c26139d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a><span data-ttu-id="1ba0e-103">SQL 데이터 웨어하우스의 사용자 정의 스키마</span><span class="sxs-lookup"><span data-stu-id="1ba0e-103">User-defined schemas in SQL Data Warehouse</span></span>
<span data-ttu-id="1ba0e-104">일반적인 데이터 웨어하우스는 작업, 도메인 또는 보안에 따라 응용 프로그램 경계를 만들기 위해 별도 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-104">Traditional data warehouses often use separate databases to create application boundaries based on either workload, domain or security.</span></span> <span data-ttu-id="1ba0e-105">예를 들어, 기존의 SQL Server 데이터 웨어하우스는 스테이징 데이터베이스, 데이터 웨어하우스 데이터베이스 및 일부 데이터마트 데이터베이스를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-105">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="1ba0e-106">이 토폴로지에서 각 데이터베이스는 아키텍처에서 워크로드 및 보안 경계로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-106">In this topology each database operates as a workload and security boundary in the architecture.</span></span>

<span data-ttu-id="1ba0e-107">반면, SQL 데이터 웨어하우스는 하나의 데이터베이스 내에서 전체 데이터 웨어하우스 워크로드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-107">By contrast, SQL Data Warehouse runs the entire data warehouse workload within one database.</span></span> <span data-ttu-id="1ba0e-108">데이터베이스 간 조인은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-108">Cross database joins are not permitted.</span></span> <span data-ttu-id="1ba0e-109">따라서 SQL 데이터 웨어하우스는 웨어하우스에서 사용된 모든 테이블을 하나의 데이터베이스 내에 저장할 것으로 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-109">Therefore SQL Data Warehouse expects all tables used by the warehouse to be stored within the one database.</span></span>

> [!NOTE]
> <span data-ttu-id="1ba0e-110">SQL 데이터 웨어하우스는 모든 종류의 데이터베이스 간 쿼리를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-110">SQL Data Warehouse does not support cross database queries of any kind.</span></span> <span data-ttu-id="1ba0e-111">따라서 이 패턴을 활용하는 데이터 웨어하우스 구현을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-111">Consequently, data warehouse implementations that leverage this pattern will need to be revised.</span></span>
> 
> 

## <a name="recommendations"></a><span data-ttu-id="1ba0e-112">추천</span><span class="sxs-lookup"><span data-stu-id="1ba0e-112">Recommendations</span></span>
<span data-ttu-id="1ba0e-113">사용자 정의 스키마를 사용하여 워크로드, 보안, 도메인 및 기능 경계를 통합하기 위한 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-113">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span></span>

1. <span data-ttu-id="1ba0e-114">SQL 데이터 웨어하우스 데이터베이스를 사용하여 전체 데이터 웨어하우스 워크로드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-114">Use one SQL Data Warehouse database to run your entire data warehouse workload</span></span>
2. <span data-ttu-id="1ba0e-115">SQL 데이터 웨어하우스 데이터베이스 하나를 사용하여 기존 데이터 웨어하우스 환경을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-115">Consolidate your existing data warehouse environment to use one SQL Data Warehouse database</span></span>
3. <span data-ttu-id="1ba0e-116">**사용자 정의 스키마** 를 활용하여 데이터베이스를 사용하여 이전에 구현된 경계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-116">Leverage **user-defined schemas** to provide the boundary previously implemented using databases.</span></span>

<span data-ttu-id="1ba0e-117">사용자 정의 스키마를 이전에 사용하지 않은 경우, 초기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-117">If user-defined schemas have not been used previously then you have a clean slate.</span></span> <span data-ttu-id="1ba0e-118">SQL 데이터 웨어하우스 데이터베이스에서 사용자 정의 스키마에 대한 기준으로 이전 데이터베이스 이름을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-118">Simply use the old database name as the basis for your user-defined schemas in the SQL Data Warehouse database.</span></span>

<span data-ttu-id="1ba0e-119">스키마가 이미 사용된 경우 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-119">If schemas have already been used then you have a few options:</span></span>

1. <span data-ttu-id="1ba0e-120">레거시 스키마 이름을 제거하고 새로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-120">Remove the legacy schema names and start fresh</span></span>
2. <span data-ttu-id="1ba0e-121">레거시 스키마 이름을 테이블 이름으로 미리 보류하여 레거시 스키마 이름을 유지합니다</span><span class="sxs-lookup"><span data-stu-id="1ba0e-121">Retain the legacy schema names by pre-pending the legacy schema name to the table name</span></span>
3. <span data-ttu-id="1ba0e-122">이전 스키마 구조를 다시 만들도록 추가 스키마의 테이블 위에 뷰를 구현하여 레거시 스키마 이름을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-122">Retain the legacy schema names by implementing views over the table in an extra schema to re-create the old schema structure.</span></span>

> [!NOTE]
> <span data-ttu-id="1ba0e-123">첫 번째 검사에서 옵션 3은 가장 매력적인 옵션처럼 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-123">On first inspection option 3 may seem like the most appealing option.</span></span> <span data-ttu-id="1ba0e-124">그러나 자세히 보면 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-124">However, the devil is in the detail.</span></span> <span data-ttu-id="1ba0e-125">뷰는 SQL 데이터 웨어하우스에서만 읽혀집니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-125">Views are read only in SQL Data Warehouse.</span></span> <span data-ttu-id="1ba0e-126">기본 테이블에 대해 모든 데이터 또는 테이블을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-126">Any data or table modification would need to be performed against the base table.</span></span> <span data-ttu-id="1ba0e-127">또한 옵션 3은 시스템으로의 뷰 레이어를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-127">Option 3 also introduces a layer of views into your system.</span></span> <span data-ttu-id="1ba0e-128">이미 아키텍처에서 뷰를 사용 중인 경우 추가로 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-128">You might want to give this some additional thought if you are using views in your architecture already.</span></span>
> 
> 

### <a name="examples"></a><span data-ttu-id="1ba0e-129">예제:</span><span class="sxs-lookup"><span data-stu-id="1ba0e-129">Examples:</span></span>
<span data-ttu-id="1ba0e-130">데이터베이스 이름을 기반으로 사용자 정의 스키마를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-130">Implement user-defined schemas based on database names</span></span>

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for the data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in the stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in the edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="1ba0e-131">테이블 이름으로 미리 보류하여 레거시 스키마 이름을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-131">Retain legacy schema names by pre-pending them to the table name.</span></span> <span data-ttu-id="1ba0e-132">워크로드 경계에 대한 스키마를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-132">Use schemas for the workload boundary.</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines the staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines the data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend the old schema name to the table and create in the staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend the old schema name to the table and create in the data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="1ba0e-133">뷰를 사용하여 레거시 스키마 이름을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-133">Retain legacy schema names using views</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines the staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines the data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines the legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create the base staging tables in the staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create the base data warehouse tables in the data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in the legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> <span data-ttu-id="1ba0e-134">스키마 전략의 변경 내용은 데이터베이스에 대한 보안 모델을 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-134">Any change in schema strategy needs a review of the security model for the database.</span></span> <span data-ttu-id="1ba0e-135">대부분의 경우 스키마 수준에서 사용 권한을 할당하여 보안 모델을 단순화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-135">In many cases you might be able to simplify the security model by assigning permissions at the schema level.</span></span> <span data-ttu-id="1ba0e-136">보다 세부적인 사용 권한이 필요한 경우 데이터베이스 역할을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-136">If more granular permissions are required then you can use database roles.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1ba0e-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1ba0e-137">Next steps</span></span>
<span data-ttu-id="1ba0e-138">더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ba0e-138">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->

---
title: "SQL Data Warehouse의 변수 할당 | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 Transact-SQL 변수 할당을 위한 팁"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 81ddc7cf-a6ba-4585-91a3-b6ea50f49227
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 045d5148cd3f12dac63c961ccf7c953d355ed725
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a><span data-ttu-id="ec218-103">SQL 데이터 웨어하우스의 변수 할당</span><span class="sxs-lookup"><span data-stu-id="ec218-103">Assign variables in SQL Data Warehouse</span></span>
<span data-ttu-id="ec218-104">SQL 데이터 웨어하우스의 변수는 `DECLARE` 문 또는 `SET` 문을 사용하여 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec218-104">Variables in SQL Data Warehouse are set using the `DECLARE` statement or the `SET` statement.</span></span>

<span data-ttu-id="ec218-105">다음 모두는 다양한 변수를 설정하는 완벽하게 유효한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ec218-105">All of the following are perfectly valid ways to set a variable value:</span></span>

## <a name="setting-variables-with-declare"></a><span data-ttu-id="ec218-106">DECLARE를 사용하여 변수 설정</span><span class="sxs-lookup"><span data-stu-id="ec218-106">Setting variables with DECLARE</span></span>
<span data-ttu-id="ec218-107">DECLARE를 사용한 변수 초기화는 SQL 데이터 웨어하우스의 변수 값을 설정하는 가장 유연한 방법 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="ec218-107">Initializing variables with DECLARE is one of the most flexible ways to set a variable value in SQL Data Warehouse.</span></span>

```sql
DECLARE @v  int = 0
;
```

<span data-ttu-id="ec218-108">한 번에 둘 이상의 변수를 설정하려면 DECLARE를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec218-108">You can also use DECLARE to set more than one variable at a time.</span></span> <span data-ttu-id="ec218-109">다음을 수행하려면 `SELECT` 또는 `UPDATE`를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec218-109">You cannot use `SELECT` or `UPDATE` to do this:</span></span>

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

<span data-ttu-id="ec218-110">초기화하여 동일한 DECLARE 문에서 변수를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec218-110">You cannot initialise and use a variable in the same DECLARE statement.</span></span> <span data-ttu-id="ec218-111">지점을 설명하기 위해 아래 예에서는 @p1이 동일한 DECLARE 문에서 시작되고 사용되기 때문에 허용되지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="ec218-111">To illustrate the point the example below is **not** allowed as @p1 is both initialized and used in the same DECLARE statement.</span></span> <span data-ttu-id="ec218-112">그러면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ec218-112">This will result in an error.</span></span>

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a><span data-ttu-id="ec218-113">SET을 사용하여 값 설정</span><span class="sxs-lookup"><span data-stu-id="ec218-113">Setting values with SET</span></span>
<span data-ttu-id="ec218-114">집합은 단일 변수를 설정하기 위한 매우 일반적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ec218-114">Set is a very common method for setting a single variable.</span></span>

<span data-ttu-id="ec218-115">아래 예제 모두는 SET을 사용하여 변수를 설정하는 올바른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ec218-115">All of the examples below are valid ways of setting a variable with SET:</span></span>

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

<span data-ttu-id="ec218-116">SET을 사용하여 한 번에 하나의 변수만 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec218-116">You can only set one variable at a time with SET.</span></span> <span data-ttu-id="ec218-117">그러나 위에서 설명한 것처럼 복합 연산자가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec218-117">However, as can be seen above compound operators are permissable.</span></span>

## <a name="limitations"></a><span data-ttu-id="ec218-118">제한 사항</span><span class="sxs-lookup"><span data-stu-id="ec218-118">Limitations</span></span>
<span data-ttu-id="ec218-119">변수 할당에 SELECT 또는 UPDATE를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec218-119">You cannot use SELECT or UPDATE for variable assignment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec218-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ec218-120">Next steps</span></span>
<span data-ttu-id="ec218-121">더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec218-121">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->

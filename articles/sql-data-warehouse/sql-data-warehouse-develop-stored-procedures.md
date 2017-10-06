---
title: "SQL 데이터 웨어하우스의 절차에서는 aaaStored | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 저장 프로시저 구현을 위한 팁"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 9b238789-6efe-4820-bf77-5a5da2afa0e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 416252dd3dea95c66aa5e886860b933b22578002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a><span data-ttu-id="e936a-103">SQL 데이터 웨어하우스의 저장된 프로시저</span><span class="sxs-lookup"><span data-stu-id="e936a-103">Stored procedures in SQL Data Warehouse</span></span>
<span data-ttu-id="e936a-104">SQL 데이터 웨어하우스 SQL Server에서 hello Transact SQL 기능을 많이 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-104">SQL Data Warehouse supports many of hello Transact-SQL features found in SQL Server.</span></span> <span data-ttu-id="e936a-105">더욱 중요 한 확장 솔루션의 tooleverage toomaximize hello 성능을 하겠습니다 특정 기능은 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-105">More importantly there are scale out specific features that we will want tooleverage toomaximize hello performance of your solution.</span></span>

<span data-ttu-id="e936a-106">그러나 toomaintain hello 배율 및 SQL 데이터 웨어하우스 성능은 또한 몇 가지 기능 및 동작의 차이 지원 되지 않는 다른 사용자가 있는 기능.</span><span class="sxs-lookup"><span data-stu-id="e936a-106">However, toomaintain hello scale and performance of SQL Data Warehouse there are also some features and functionality that have behavioral differences and others that are not supported.</span></span>

<span data-ttu-id="e936a-107">이 문서에서는 tooimplement SQL 데이터 웨어하우스 내에서 프로시저를 저장 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-107">This article explains how tooimplement stored procedures within SQL Data Warehouse.</span></span>

## <a name="introducing-stored-procedures"></a><span data-ttu-id="e936a-108">저장된 프로시저 소개</span><span class="sxs-lookup"><span data-stu-id="e936a-108">Introducing stored procedures</span></span>
<span data-ttu-id="e936a-109">저장된 프로시저는 SQL 코드를 캡슐화 하는 데 효과적인 방법 데이터를 저장 하기 닫기 tooyour hello 데이터 웨어하우스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-109">Stored procedures are a great way for encapsulating your SQL code; storing it close tooyour data in hello data warehouse.</span></span> <span data-ttu-id="e936a-110">관리 가능한 단위로 hello 코드를 캡슐화 하 여 저장된 프로시저는 개발자가 솔루션; 모듈화 도움말 코드의 큰 re-usability를 촉진 합니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-110">By encapsulating hello code into manageable units stored procedures help developers modularize their solutions; facilitating greater re-usability of code.</span></span> <span data-ttu-id="e936a-111">각 저장된 프로시저 매개 변수 toomake 그대로 사용할 수도 훨씬 더 유연 합니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-111">Each stored procedure can also accept parameters toomake them even more flexible.</span></span>

<span data-ttu-id="e936a-112">SQL 데이터 웨어하우스는 단순하고 효율적인 저장된 프로시저 구현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-112">SQL Data Warehouse provides a simplified and streamlined stored procedure implementation.</span></span> <span data-ttu-id="e936a-113">hello 가장 큰 차이점 비교 tooSQL 서버는 저장된 프로시저를 hello 하는 미리 컴파일된 코드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-113">hello biggest difference compared tooSQL Server is that hello stored procedure is not pre-compiled code.</span></span> <span data-ttu-id="e936a-114">데이터 웨어하우스에서 hello 컴파일 시간이 일반적으로 고려 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-114">In data warehouses we are generally less concerned with hello compilation time.</span></span> <span data-ttu-id="e936a-115">것이 더 중요 큰 데이터 볼륨에 대해 작동할 때 hello 저장 프로시저 코드 최적화 올바르게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-115">It is more important that hello stored procedure code is correctly optimised when operating against large data volumes.</span></span> <span data-ttu-id="e936a-116">hello 목표 toosave 시간, 분 및 초 하지 밀리초입니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-116">hello goal is toosave hours, minutes and seconds not milliseconds.</span></span> <span data-ttu-id="e936a-117">이 프로토콜은 따라서 저장된 프로시저의 더 유용한 toothink으로 SQL 논리에 대 한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-117">It is therefore more helpful toothink of stored procedures as containers for SQL logic.</span></span>     

<span data-ttu-id="e936a-118">SQL 데이터 웨어하우스를 실행 하는 경우 저장된 프로시저 hello SQL 문의 분석, 변환 및 런타임 시 최적화.</span><span class="sxs-lookup"><span data-stu-id="e936a-118">When SQL Data Warehouse executes your stored procedure hello SQL statements are parsed, translated and optimized at run time.</span></span> <span data-ttu-id="e936a-119">이 프로세스 중 각 문이 분산 쿼리로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-119">During this process each statement is converted into distributed queries.</span></span> <span data-ttu-id="e936a-120">hello hello 데이터에 대해 실제로 실행 되는 SQL 코드는 다른 toohello 쿼리를 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-120">hello SQL code that is actually executed against hello data is different toohello query submitted.</span></span>

## <a name="nesting-stored-procedures"></a><span data-ttu-id="e936a-121">중첩 저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="e936a-121">Nesting stored procedures</span></span>
<span data-ttu-id="e936a-122">때 저장된 프로시저는 다른 저장된 프로시저를 호출 하거나 hello 내부 저장 프로시저 또는 toobe 중첩 된 블록의 코드 호출 이라고 하는 다음 동적 sql을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-122">When stored procedures call other stored procedures or execute dynamic sql then hello inner stored procedure or code invocation is said toobe nested.</span></span>

<span data-ttu-id="e936a-123">SQL 데이터 웨어하우스는 최대 8개의 중첩 수준을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-123">SQL Data Warehouse support a maximum of 8 nesting levels.</span></span> <span data-ttu-id="e936a-124">이 약간 다른 tooSQL 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-124">This is slightly different tooSQL Server.</span></span> <span data-ttu-id="e936a-125">SQL Server의 중첩 수준 hello은 32입니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-125">hello nest level in SQL Server is 32.</span></span>

<span data-ttu-id="e936a-126">hello 상위 수준 저장된 프로시저 호출에는 toonest 수준을 1 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-126">hello top level stored procedure call equates toonest level 1</span></span>

```sql
EXEC prc_nesting
```
<span data-ttu-id="e936a-127">Hello 저장 하는 경우 프로시저를 호출 하는 다른 EXEC을 사용 하면 다음 hello 중첩 수준 too2 늘어납니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-127">If hello stored procedure also makes another EXEC call then this will increase hello nest level too2</span></span>

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
<span data-ttu-id="e936a-128">두 번째 절차 hello 다음 몇 가지 동적 sql을 실행 하는 경우 다음 이렇게 하면 증가 hello 중첩 수준 too3</span><span class="sxs-lookup"><span data-stu-id="e936a-128">If hello second procedure then executes some dynamic sql then this will increase hello nest level too3</span></span>

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

<span data-ttu-id="e936a-129">SQL Data Warehouse는 현재 @@NESTLEVEL을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-129">Note SQL Data Warehouse does not currently support @@NESTLEVEL.</span></span> <span data-ttu-id="e936a-130">사용자가 직접 tookeep 중첩 수준의 트랙을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-130">You will need tookeep a track of your nest level yourself.</span></span> <span data-ttu-id="e936a-131">Hello 8 중첩 수준 제한에 도달 합니다 있지만 있습니다를 수행 하는 경우는 코드 toore 일이 필요 하 고 "개체가 결합"는이 시간 동안 8 가능성이있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-131">It is unlikely you will hit hello 8 nest level limit but if you do you will need toore-work your code and "flatten" it so that it fits within this limit.</span></span>

## <a name="insertexecute"></a><span data-ttu-id="e936a-132">INSERT..EXECUTE</span><span class="sxs-lookup"><span data-stu-id="e936a-132">INSERT..EXECUTE</span></span>
<span data-ttu-id="e936a-133">SQL 데이터 웨어하우스에는 INSERT 문 사용 하는 저장된 프로시저의 tooconsume hello 결과 집합이 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-133">SQL Data Warehouse does not permit you tooconsume hello result set of a stored procedure with an INSERT statement.</span></span> <span data-ttu-id="e936a-134">그러나 대체 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-134">However, there is an alternative approach you can use.</span></span>

<span data-ttu-id="e936a-135">Toohello 다음 문서를 참조 하십시오 [임시 테이블] 방법에 예제를 보려면 toodo이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-135">Please refer toohello following article on [temporary tables] for an example on how toodo this.</span></span>

## <a name="limitations"></a><span data-ttu-id="e936a-136">제한 사항</span><span class="sxs-lookup"><span data-stu-id="e936a-136">Limitations</span></span>
<span data-ttu-id="e936a-137">SQL 데이터 웨어하우스에서 구현되지 않은 TRANSACT-SQL 저장된 프로시저의 일부 측면이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-137">There are some aspects of Transact-SQL stored procedures that are not implemented in SQL Data Warehouse.</span></span>

<span data-ttu-id="e936a-138">아래에 이 계정과 키의 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e936a-138">They are:</span></span>

* <span data-ttu-id="e936a-139">임시 저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="e936a-139">temporary stored procedures</span></span>
* <span data-ttu-id="e936a-140">숫자가 매겨진 저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="e936a-140">numbered stored procedures</span></span>
* <span data-ttu-id="e936a-141">확장된 저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="e936a-141">extended stored procedures</span></span>
* <span data-ttu-id="e936a-142">CLR 저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="e936a-142">CLR stored procedures</span></span>
* <span data-ttu-id="e936a-143">암호화 옵션</span><span class="sxs-lookup"><span data-stu-id="e936a-143">encryption option</span></span>
* <span data-ttu-id="e936a-144">복제 옵션</span><span class="sxs-lookup"><span data-stu-id="e936a-144">replication option</span></span>
* <span data-ttu-id="e936a-145">테이블 반환 매개 변수</span><span class="sxs-lookup"><span data-stu-id="e936a-145">table-valued parameters</span></span>
* <span data-ttu-id="e936a-146">읽기 전용 매개 변수</span><span class="sxs-lookup"><span data-stu-id="e936a-146">read-only parameters</span></span>
* <span data-ttu-id="e936a-147">기본 매개 변수</span><span class="sxs-lookup"><span data-stu-id="e936a-147">default parameters</span></span>
* <span data-ttu-id="e936a-148">실행 컨텍스트</span><span class="sxs-lookup"><span data-stu-id="e936a-148">execution contexts</span></span>
* <span data-ttu-id="e936a-149">return 문</span><span class="sxs-lookup"><span data-stu-id="e936a-149">return statement</span></span>

## <a name="next-steps"></a><span data-ttu-id="e936a-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e936a-150">Next steps</span></span>
<span data-ttu-id="e936a-151">더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e936a-151">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[임시 테이블]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->

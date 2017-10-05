---
title: "메모리 내 OLTP이 SQL txn 성능 개선 | Microsoft Docs"
description: "메모리 내 OLTP를 채택하여 기존 SQL 데이터베이스의 트랜잭션 성능을 향상합니다."
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 50eed9aed417778bd497f55e20c8e732fdae9cf9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-in-memory-oltp-to-improve-your-application-performance-in-sql-database"></a><span data-ttu-id="679c4-103">메모리 내 OLTP를 사용하여 SQL 데이터베이스에서 응용 프로그램의 성능 향상</span><span class="sxs-lookup"><span data-stu-id="679c4-103">Use In-Memory OLTP to improve your application performance in SQL Database</span></span>
<span data-ttu-id="679c4-104">[메모리 내 OLTP](sql-database-in-memory.md)를 사용하면 가격대를 높이지 않고도 [Premium](sql-database-service-tiers.md) Azure SQL 데이터베이스에서 트랜잭션 처리, 데이터 수집 및 일시적인 데이터 시나리오의 성능을 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-104">[In-Memory OLTP](sql-database-in-memory.md) can be used to improve the performance of transaction processing, data ingestion, and transient data scenarios, in  [Premium](sql-database-service-tiers.md) Azure SQL Databases without increasing the pricing tier.</span></span> 

> [!NOTE] 
> <span data-ttu-id="679c4-105">[쿼럼이 SQL Database를 사용하여 DTU를 70% 줄이는 동시에 키 데이터베이스의 워크로드를 두 배로 증가시키는 방법](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="679c4-105">Learn how [Quorum doubles key database’s workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>


<span data-ttu-id="679c4-106">기존 데이터베이스에서 메모리 내 OLTP를 채택하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="679c4-106">Follow these steps to adopt In-Memory OLTP in your existing database.</span></span>

## <a name="step-1-ensure-you-are-using-a-premium-database"></a><span data-ttu-id="679c4-107">1단계: 프리미엄 데이터베이스 사용 확인</span><span class="sxs-lookup"><span data-stu-id="679c4-107">Step 1: Ensure you are using a Premium database</span></span>
<span data-ttu-id="679c4-108">메모리 내 OLTP는 프리미엄 데이터베이스에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-108">In-Memory OLTP is supported only in Premium databases.</span></span> <span data-ttu-id="679c4-109">반환된 결과가 1인 경우(0이 아님) 메모리 내가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-109">In-Memory is supported if the returned result is 1 (not 0):</span></span>

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

<span data-ttu-id="679c4-110">*XTP*는 *고도의 트랜잭션 처리*의 약어입니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-110">*XTP* stands for *Extreme Transaction Processing*</span></span>



## <a name="step-2-identify-objects-to-migrate-to-in-memory-oltp"></a><span data-ttu-id="679c4-111">2단계: 개체를 식별하여 메모리 내 OLTP로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="679c4-111">Step 2: Identify objects to migrate to In-Memory OLTP</span></span>
<span data-ttu-id="679c4-112">SSMS는 활성 워크로드를 사용하여 데이터베이스에 대해 실행할 수 있는 **트랜잭션 성능 분석 개요** 보고서를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-112">SSMS includes a **Transaction Performance Analysis Overview** report that you can run against a database with an active workload.</span></span> <span data-ttu-id="679c4-113">보고서는 메모리 내 OLTP로 마이그레이션하기 위한 후보인 테이블 및 저장된 프로시저를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-113">The report identifies tables and stored procedures that are candidates for migration to In-Memory OLTP.</span></span>

<span data-ttu-id="679c4-114">SSMS에서 보고서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-114">In SSMS, to generate the report:</span></span>

* <span data-ttu-id="679c4-115">**개체 탐색기**에서 데이터베이스 노드를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-115">In the **Object Explorer**, right-click your database node.</span></span>
* <span data-ttu-id="679c4-116">**보고서** > **표준 보고서** > **트랜잭션 성능 분석 개요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-116">Click **Reports** > **Standard Reports** > **Transaction Performance Analysis Overview**.</span></span>

<span data-ttu-id="679c4-117">자세한 내용은 [테이블 또는 저장 프로시저가 메모리 내 OLTP로 이식되어야 하는지 결정](http://msdn.microsoft.com/library/dn205133.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="679c4-117">For more information, see [Determining if a Table or Stored Procedure Should Be Ported to In-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span></span>

## <a name="step-3-create-a-comparable-test-database"></a><span data-ttu-id="679c4-118">3단계: 비교할 수 있는 테스트 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="679c4-118">Step 3: Create a comparable test database</span></span>
<span data-ttu-id="679c4-119">보고서는 데이터베이스에 메모리에 최적화된 테이블로 변환하여 이점을 얻을 수 있는 테이블이 있음을 나타낸다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-119">Suppose the report indicates your database has a table that would benefit from being converted to a memory-optimized table.</span></span> <span data-ttu-id="679c4-120">이를 확인하기 위해 먼저 테스트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-120">We recommend that you first test to confirm the indication by testing.</span></span>

<span data-ttu-id="679c4-121">프로덕션 데이터베이스의 테스트 복사본이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-121">You need a test copy of your production database.</span></span> <span data-ttu-id="679c4-122">테스트 데이터베이스는 프로덕션 데이터베이스와 동일한 서비스 계층 수준에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-122">The test database should be at the same service tier level as your production database.</span></span>

<span data-ttu-id="679c4-123">쉽게 테스트하려면 테스트 데이터베이스를 다음과 같이 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-123">To ease testing, tweak your test database as follows:</span></span>

1. <span data-ttu-id="679c4-124">SSMS를 사용하여 테스트 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-124">Connect to the test database by using SSMS.</span></span>
2. <span data-ttu-id="679c4-125">쿼리에서 WITH(SNAPSHOT) 옵션의 필요를 방지하려면 다음 T-SQL 문에서와 같이 데이터베이스 옵션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-125">To avoid needing the WITH (SNAPSHOT) option in queries, set the database option as shown in the following T-SQL statement:</span></span>
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a><span data-ttu-id="679c4-126">4단계: 테이블 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="679c4-126">Step 4: Migrate tables</span></span>
<span data-ttu-id="679c4-127">테스트하려는 테이블의 메모리에 최적화된 복사본을 만들고 채워야 합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-127">You must create and populate a memory-optimized copy of the table you want to test.</span></span> <span data-ttu-id="679c4-128">다음 중 하나를 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-128">You can create it by using either:</span></span>

* <span data-ttu-id="679c4-129">SSMS의 편리한 메모리 최적화 마법사.</span><span class="sxs-lookup"><span data-stu-id="679c4-129">The handy Memory Optimization Wizard in SSMS.</span></span>
* <span data-ttu-id="679c4-130">수동 T-SQL.</span><span class="sxs-lookup"><span data-stu-id="679c4-130">Manual T-SQL.</span></span>

#### <a name="memory-optimization-wizard-in-ssms"></a><span data-ttu-id="679c4-131">SSMS의 메모리 최적화 마법사.</span><span class="sxs-lookup"><span data-stu-id="679c4-131">Memory Optimization Wizard in SSMS</span></span>
<span data-ttu-id="679c4-132">이 마이그레이션 옵션을 사용하려면.</span><span class="sxs-lookup"><span data-stu-id="679c4-132">To use this migration option:</span></span>

1. <span data-ttu-id="679c4-133">SSMS를 사용하여 테스트 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-133">Connect to the test database with SSMS.</span></span>
2. <span data-ttu-id="679c4-134">**개체 탐색기**에서 테이블을 마우스 오른쪽 단추로 클릭한 다음 **메모리 최적화 관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-134">In the **Object Explorer**, right-click on the table, and then click **Memory Optimization Advisor**.</span></span>
   
   * <span data-ttu-id="679c4-135">**테이블 메모리 최적화 관리자** 마법사가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-135">The **Table Memory Optimizer Advisor** wizard is displayed.</span></span>
3. <span data-ttu-id="679c4-136">마법사에서 **마이그레이션 유효성 검사**(또는 **다음** 단추)을 클릭하여 메모리에 최적화된 테이블에서 지원하지 않는 지원되지 않는 기능이 테이블에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-136">In the wizard, click **Migration validation** (or the **Next** button) to see if the table has any unsupported features that are unsupported in memory-optimized tables.</span></span> <span data-ttu-id="679c4-137">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="679c4-137">For more information, see:</span></span>
   
   * <span data-ttu-id="679c4-138">*메모리 최적화 관리자* 의 [메모리 최적화 검사 목록](http://msdn.microsoft.com/library/dn284308.aspx).</span><span class="sxs-lookup"><span data-stu-id="679c4-138">The *memory optimization checklist* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span></span>
   * <span data-ttu-id="679c4-139">[메모리 내 OLTP에서 지원되지 않는 TRANSACT-SQL 항목](http://msdn.microsoft.com/library/dn246937.aspx).</span><span class="sxs-lookup"><span data-stu-id="679c4-139">[Transact-SQL Constructs Not Supported by In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span></span>
   * <span data-ttu-id="679c4-140">[메모리 내 OLTP로 마이그레이션](http://msdn.microsoft.com/library/dn247639.aspx).</span><span class="sxs-lookup"><span data-stu-id="679c4-140">[Migrating to In-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span></span>
4. <span data-ttu-id="679c4-141">테이블에 지원되지 않는 기능이 없는 경우 관리자는 사용자에게 실제 스키마 및 데이터 마이그레이션을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-141">If the table has no unsupported features, the advisor can perform the actual schema and data migration for you.</span></span>

#### <a name="manual-t-sql"></a><span data-ttu-id="679c4-142">수동 T-SQL</span><span class="sxs-lookup"><span data-stu-id="679c4-142">Manual T-SQL</span></span>
<span data-ttu-id="679c4-143">이 마이그레이션 옵션을 사용하려면.</span><span class="sxs-lookup"><span data-stu-id="679c4-143">To use this migration option:</span></span>

1. <span data-ttu-id="679c4-144">SSMS(또는 유사한 유틸리티)를 사용하여 테스트 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-144">Connect to your test database by using SSMS (or a similar utility).</span></span>
2. <span data-ttu-id="679c4-145">테이블 및 해당 인덱스에 대한 완전한 T-SQL 스크립트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-145">Obtain the complete T-SQL script for your table and its indexes.</span></span>
   
   * <span data-ttu-id="679c4-146">SSMS에서 테이블 노드를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-146">In SSMS, right-click your table node.</span></span>
   * <span data-ttu-id="679c4-147">**테이블 스크립팅** > **CREATE** > **새 쿼리 창**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-147">Click **Script Table As** > **CREATE To** > **New Query Window**.</span></span>
3. <span data-ttu-id="679c4-148">스크립트 창에서 테이블 만들기 문에 WITH (MEMORY_OPTIMIZED = ON)을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-148">In the script window, add WITH (MEMORY_OPTIMIZED = ON) to the CREATE TABLE statement.</span></span>
4. <span data-ttu-id="679c4-149">클러스터형 인덱스가 있을 경우 비클러스터형으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-149">If there is a CLUSTERED index, change it to NONCLUSTERED.</span></span>
5. <span data-ttu-id="679c4-150">SP_RENAME을 사용하여 기존 테이블의 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-150">Rename the existing table by using SP_RENAME.</span></span>
6. <span data-ttu-id="679c4-151">편집된 만들기 테이블 스크립트를 실행하여 테이블의 새 메모리에 최적화된 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-151">Create the new memory-optimized copy of the table by running your edited CREATE TABLE script.</span></span>
7. <span data-ttu-id="679c4-152">삽입을 사용하여 메모리에 최적화된 테이블에 데이터를 복사합니다... *를 다음에 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-152">Copy the data to your memory-optimized table by using INSERT...SELECT * INTO:</span></span>

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a><span data-ttu-id="679c4-153">5단계(선택 사항): 저장 프로시저 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="679c4-153">Step 5 (optional): Migrate stored procedures</span></span>
<span data-ttu-id="679c4-154">또한 메모리 내 기능은 향상된 성능을 위해 저장 프로시저를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-154">The In-Memory feature can also modify a stored procedure for improved performance.</span></span>

### <a name="considerations-with-natively-compiled-stored-procedures"></a><span data-ttu-id="679c4-155">고유하게 컴파일된 저장 프로시저를 사용할 때 고려 사항</span><span class="sxs-lookup"><span data-stu-id="679c4-155">Considerations with natively compiled stored procedures</span></span>
<span data-ttu-id="679c4-156">고유하게 컴파일된 저장 프로시저에는 절이 있는 해당 T-SQL에서 다음 옵션이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-156">A natively compiled stored procedure must have the following options on its T-SQL WITH clause:</span></span>

* <span data-ttu-id="679c4-157">NATIVE_COMPILATION</span><span class="sxs-lookup"><span data-stu-id="679c4-157">NATIVE_COMPILATION</span></span>
* <span data-ttu-id="679c4-158">SCHEMABINDING: 저장 프로시저가 삭제되지 않는 한 스스로에 영향을 주는 방식으로 변경된 해당 열 정의를 가질 수 없는 테이블을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-158">SCHEMABINDING: meaning tables that the stored procedure cannot have their column definitions changed in any way that would affect the stored procedure, unless you drop the stored procedure.</span></span>

<span data-ttu-id="679c4-159">네이티브 모듈은 트랜잭션 관리에 하나의 큰 [ATOMIC 블록](http://msdn.microsoft.com/library/dn452281.aspx) 을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-159">A native module must use one big [ATOMIC blocks](http://msdn.microsoft.com/library/dn452281.aspx) for transaction management.</span></span> <span data-ttu-id="679c4-160">명시적 BEGIN TRANSACTION 또는 ROLLBACK TRANSACTION에 대한 역할이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-160">There is no role for an explicit BEGIN TRANSACTION, or for ROLLBACK TRANSACTION.</span></span> <span data-ttu-id="679c4-161">코드가 비즈니스 규칙 위반을 감지한 경우 [THROW](http://msdn.microsoft.com/library/ee677615.aspx) 문으로 ATOMIC 블록을 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-161">If your code detects a violation of a business rule, it can terminate the atomic block with a [THROW](http://msdn.microsoft.com/library/ee677615.aspx) statement.</span></span>

### <a name="typical-create-procedure-for-natively-compiled"></a><span data-ttu-id="679c4-162">고유하게 컴파일된 일반적인 만들기 프로시저</span><span class="sxs-lookup"><span data-stu-id="679c4-162">Typical CREATE PROCEDURE for natively compiled</span></span>
<span data-ttu-id="679c4-163">고유하게 컴파일된 저장 프로시저를 만드는 T-SQL은 일반적으로 다음 템플릿과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-163">Typically the T-SQL to create a natively compiled stored procedure is similar to the following template:</span></span>

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* <span data-ttu-id="679c4-164">TRANSACTION_ISOLATION_LEVEL의 경우 스냅숏은 고유하게 컴파일된 저장 프로시저에 대한 가장 일반적인 값입니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-164">For the TRANSACTION_ISOLATION_LEVEL, SNAPSHOT is the most common value for the natively compiled stored procedure.</span></span> <span data-ttu-id="679c4-165">그러나 다른 값의 하위 집합에서도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-165">However,  a subset of the other values are also supported:</span></span>
  
  * <span data-ttu-id="679c4-166">반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="679c4-166">REPEATABLE READ</span></span>
  * <span data-ttu-id="679c4-167">직렬화 가능</span><span class="sxs-lookup"><span data-stu-id="679c4-167">SERIALIZABLE</span></span>
* <span data-ttu-id="679c4-168">sys.languages 보기에 언어 값이 나탸나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-168">The LANGUAGE value must be present in the sys.languages view.</span></span>

### <a name="how-to-migrate-a-stored-procedure"></a><span data-ttu-id="679c4-169">저장 프로시저를 마이그레이션하는 방법</span><span class="sxs-lookup"><span data-stu-id="679c4-169">How to migrate a stored procedure</span></span>
<span data-ttu-id="679c4-170">마이그레이션 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-170">The migration steps are:</span></span>

1. <span data-ttu-id="679c4-171">일반적으로 해석된 저장 프로시저에 프로시저 만들기 스크립트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-171">Obtain the CREATE PROCEDURE script to the regular interpreted stored procedure.</span></span>
2. <span data-ttu-id="679c4-172">이전 템플릿에 맞게 해당 헤더를 다시 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-172">Rewrite its header to match the previous template.</span></span>
3. <span data-ttu-id="679c4-173">저장 프로시저 T-SQL 코드가 고유하게 컴파일된 저장 프로시저에 지원하지 않는 기능을 사용하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-173">Ascertain whether the stored procedure T-SQL code uses any features that are not supported for natively compiled stored procedures.</span></span> <span data-ttu-id="679c4-174">필요한 경우 해결 방법을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-174">Implement workarounds if necessary.</span></span>
   
   * <span data-ttu-id="679c4-175">자세한 내용은 [고유하게 컴파일된 저장 프로시저에 대한 마이그레이션 문제](http://msdn.microsoft.com/library/dn296678.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="679c4-175">For details see [Migration Issues for Natively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span></span>
4. <span data-ttu-id="679c4-176">SP_RENAME을 사용하여 이전의 저장 프로시저의 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-176">Rename the old stored procedure by using SP_RENAME.</span></span> <span data-ttu-id="679c4-177">또는 단순히 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-177">Or simply DROP it.</span></span>
5. <span data-ttu-id="679c4-178">편집된 프로시저 T-SQL 만들기 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-178">Run your edited CREATE PROCEDURE T-SQL script.</span></span>

## <a name="step-6-run-your-workload-in-test"></a><span data-ttu-id="679c4-179">6단계: 테스트에서 워크로드 실행</span><span class="sxs-lookup"><span data-stu-id="679c4-179">Step 6: Run your workload in test</span></span>
<span data-ttu-id="679c4-180">프로덕션 데이터베이스에서 실행되는 워크로드와 비슷한 테스트 데이터베이스에서 워크로드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-180">Run a workload in your test database that is similar to the workload that runs in your production database.</span></span> <span data-ttu-id="679c4-181">이 옵션은 테이블 및 저장된 프로시저에 메모리 내 기능을 사용하여 얻는 성능 향상을 드러내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-181">This should reveal the performance gain achieved by your use of the In-Memory feature for tables and stored procedures.</span></span>

<span data-ttu-id="679c4-182">워크로드의 주요 특성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-182">Major attributes of the workload are:</span></span>

* <span data-ttu-id="679c4-183">동시 연결 수.</span><span class="sxs-lookup"><span data-stu-id="679c4-183">Number of concurrent connections.</span></span>
* <span data-ttu-id="679c4-184">읽기/쓰기 비율.</span><span class="sxs-lookup"><span data-stu-id="679c4-184">Read/write ratio.</span></span>

<span data-ttu-id="679c4-185">테스트 워크로드를 조정하고 실행하려면 [여기](sql-database-in-memory.md)에 설명된 편리한 ostress.exe 도구를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-185">To tailor and run the test workload, consider using the handy ostress.exe tool, which illustrated in [here](sql-database-in-memory.md).</span></span>

<span data-ttu-id="679c4-186">네트워크 대기 시간을 최소화하려면 데이터베이스가 있는 동일한 Azure 지리적 지역에 있는 테스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-186">To minimize network latency, run your test in the same Azure geographic region where the database exists.</span></span>

## <a name="step-7-post-implementation-monitoring"></a><span data-ttu-id="679c4-187">7단계: 사후 실현 모니터링</span><span class="sxs-lookup"><span data-stu-id="679c4-187">Step 7: Post-implementation monitoring</span></span>
<span data-ttu-id="679c4-188">프로덕션에서 메모리 내 구현의 성능 효과를 모니터링하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="679c4-188">Consider monitoring the performance effects of your In-Memory implementations in production:</span></span>

* <span data-ttu-id="679c4-189">[메모리 내 저장소 모니터링](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="679c4-189">[Monitor In-Memory Storage](sql-database-in-memory-oltp-monitoring.md).</span></span>
* [<span data-ttu-id="679c4-190">동적 관리 뷰를 사용하여 Azure SQL 데이터베이스 모니터링</span><span class="sxs-lookup"><span data-stu-id="679c4-190">Monitoring Azure SQL Database using dynamic management views</span></span>](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a><span data-ttu-id="679c4-191">관련 링크</span><span class="sxs-lookup"><span data-stu-id="679c4-191">Related links</span></span>
* [<span data-ttu-id="679c4-192">메모리 내 OLTP(메모리 내 최적화)</span><span class="sxs-lookup"><span data-stu-id="679c4-192">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
* [<span data-ttu-id="679c4-193">고유하게 컴파일된 저장 프로시저의 소개</span><span class="sxs-lookup"><span data-stu-id="679c4-193">Introduction to Natively Compiled Stored Procedures</span></span>](http://msdn.microsoft.com/library/dn133184.aspx)
* [<span data-ttu-id="679c4-194">메모리 최적화 관리자</span><span class="sxs-lookup"><span data-stu-id="679c4-194">Memory Optimization Advisor</span></span>](http://msdn.microsoft.com/library/dn284308.aspx)


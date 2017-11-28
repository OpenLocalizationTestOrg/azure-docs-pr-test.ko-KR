---
title: "aaaIn 메모리 내 OLTP SQL txn 성능 향상 | Microsoft Docs"
description: "기존 SQL 데이터베이스의 메모리 내 OLTP를 채택 tooimprove의 트랜잭션 성능입니다."
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
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a><span data-ttu-id="29d8f-103">메모리 내 OLTP를 사용 하 여 tooimprove SQL 데이터베이스에서 응용 프로그램 성능</span><span class="sxs-lookup"><span data-stu-id="29d8f-103">Use In-Memory OLTP tooimprove your application performance in SQL Database</span></span>
<span data-ttu-id="29d8f-104">[메모리 내 OLTP](sql-database-in-memory.md) 에 수 있는 트랜잭션 처리, 데이터 수집 및 임시 데이터 시나리오 사용된 tooimprove hello 성능을 [프리미엄](sql-database-service-tiers.md) 증가 하지 않고 Azure SQL 데이터베이스 가격 책정 계층을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-104">[In-Memory OLTP](sql-database-in-memory.md) can be used tooimprove hello performance of transaction processing, data ingestion, and transient data scenarios, in  [Premium](sql-database-service-tiers.md) Azure SQL Databases without increasing hello pricing tier.</span></span> 

> [!NOTE] 
> <span data-ttu-id="29d8f-105">[쿼럼이 SQL Database를 사용하여 DTU를 70% 줄이는 동시에 키 데이터베이스의 워크로드를 두 배로 증가시키는 방법](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="29d8f-105">Learn how [Quorum doubles key database’s workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>


<span data-ttu-id="29d8f-106">기존 데이터베이스에서 이러한 단계 tooadopt 메모리 내 OLTP를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-106">Follow these steps tooadopt In-Memory OLTP in your existing database.</span></span>

## <a name="step-1-ensure-you-are-using-a-premium-database"></a><span data-ttu-id="29d8f-107">1단계: 프리미엄 데이터베이스 사용 확인</span><span class="sxs-lookup"><span data-stu-id="29d8f-107">Step 1: Ensure you are using a Premium database</span></span>
<span data-ttu-id="29d8f-108">메모리 내 OLTP는 프리미엄 데이터베이스에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-108">In-Memory OLTP is supported only in Premium databases.</span></span> <span data-ttu-id="29d8f-109">메모리 내 hello 결과 1을 반환 하는 경우 지원 됩니다 (0 아님):</span><span class="sxs-lookup"><span data-stu-id="29d8f-109">In-Memory is supported if hello returned result is 1 (not 0):</span></span>

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

<span data-ttu-id="29d8f-110">*XTP*는 *고도의 트랜잭션 처리*의 약어입니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-110">*XTP* stands for *Extreme Transaction Processing*</span></span>



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a><span data-ttu-id="29d8f-111">2 단계: 식별 개체 toomigrate tooIn 메모리 내 OLTP</span><span class="sxs-lookup"><span data-stu-id="29d8f-111">Step 2: Identify objects toomigrate tooIn-Memory OLTP</span></span>
<span data-ttu-id="29d8f-112">SSMS는 활성 워크로드를 사용하여 데이터베이스에 대해 실행할 수 있는 **트랜잭션 성능 분석 개요** 보고서를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-112">SSMS includes a **Transaction Performance Analysis Overview** report that you can run against a database with an active workload.</span></span> <span data-ttu-id="29d8f-113">테이블 및 저장된 프로시저에 적합 한 마이그레이션 hello 보고서 식별 tooIn 메모리 내 OLTP 합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-113">hello report identifies tables and stored procedures that are candidates for migration tooIn-Memory OLTP.</span></span>

<span data-ttu-id="29d8f-114">Ssms에서 toogenerate hello 보고서:</span><span class="sxs-lookup"><span data-stu-id="29d8f-114">In SSMS, toogenerate hello report:</span></span>

* <span data-ttu-id="29d8f-115">Hello에 **개체 탐색기**, 데이터베이스 노드를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-115">In hello **Object Explorer**, right-click your database node.</span></span>
* <span data-ttu-id="29d8f-116">**보고서** > **표준 보고서** > **트랜잭션 성능 분석 개요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-116">Click **Reports** > **Standard Reports** > **Transaction Performance Analysis Overview**.</span></span>

<span data-ttu-id="29d8f-117">자세한 내용은 참조 [테이블 또는 tooIn 메모리 내 OLTP 저장 프로시저를 이식 해야 하는지 확인](http://msdn.microsoft.com/library/dn205133.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-117">For more information, see [Determining if a Table or Stored Procedure Should Be Ported tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span></span>

## <a name="step-3-create-a-comparable-test-database"></a><span data-ttu-id="29d8f-118">3단계: 비교할 수 있는 테스트 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="29d8f-118">Step 3: Create a comparable test database</span></span>
<span data-ttu-id="29d8f-119">hello 보고서 데이터베이스를 나타냅니다. 가정 되 고 이익이 되는 테이블 변환 tooa 메모리 액세스에 최적화 된 테이블.</span><span class="sxs-lookup"><span data-stu-id="29d8f-119">Suppose hello report indicates your database has a table that would benefit from being converted tooa memory-optimized table.</span></span> <span data-ttu-id="29d8f-120">테스트 하 여 tooconfirm hello 표시 먼저 테스트 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-120">We recommend that you first test tooconfirm hello indication by testing.</span></span>

<span data-ttu-id="29d8f-121">프로덕션 데이터베이스의 테스트 복사본이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-121">You need a test copy of your production database.</span></span> <span data-ttu-id="29d8f-122">hello 테스트 데이터베이스 있어야 hello에 동일한 서비스 계층 수준 프로덕션 데이터베이스로 합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-122">hello test database should be at hello same service tier level as your production database.</span></span>

<span data-ttu-id="29d8f-123">tooease 테스트, 테스트 데이터베이스를 다음과 같이 수정할.</span><span class="sxs-lookup"><span data-stu-id="29d8f-123">tooease testing, tweak your test database as follows:</span></span>

1. <span data-ttu-id="29d8f-124">SSMS를 사용 하 여 toohello 테스트 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-124">Connect toohello test database by using SSMS.</span></span>
2. <span data-ttu-id="29d8f-125">tooavoid 쿼리에서 WITH (SNAPSHOT) 옵션 hello, hello T-SQL 문 다음에 표시 된 대로 hello 데이터베이스 옵션을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-125">tooavoid needing hello WITH (SNAPSHOT) option in queries, set hello database option as shown in hello following T-SQL statement:</span></span>
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a><span data-ttu-id="29d8f-126">4단계: 테이블 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="29d8f-126">Step 4: Migrate tables</span></span>
<span data-ttu-id="29d8f-127">만들고 메모리 액세스에 최적화 된 복사본을 채우는 해야 원하는 tootest hello 테이블의 합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-127">You must create and populate a memory-optimized copy of hello table you want tootest.</span></span> <span data-ttu-id="29d8f-128">다음 중 하나를 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-128">You can create it by using either:</span></span>

* <span data-ttu-id="29d8f-129">hello SSMS에서 메모리 최적화 마법사에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-129">hello handy Memory Optimization Wizard in SSMS.</span></span>
* <span data-ttu-id="29d8f-130">수동 T-SQL.</span><span class="sxs-lookup"><span data-stu-id="29d8f-130">Manual T-SQL.</span></span>

#### <a name="memory-optimization-wizard-in-ssms"></a><span data-ttu-id="29d8f-131">SSMS의 메모리 최적화 마법사.</span><span class="sxs-lookup"><span data-stu-id="29d8f-131">Memory Optimization Wizard in SSMS</span></span>
<span data-ttu-id="29d8f-132">toouse이 마이그레이션 옵션:</span><span class="sxs-lookup"><span data-stu-id="29d8f-132">toouse this migration option:</span></span>

1. <span data-ttu-id="29d8f-133">SSMS로 toohello 테스트 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-133">Connect toohello test database with SSMS.</span></span>
2. <span data-ttu-id="29d8f-134">Hello에 **개체 탐색기**hello 테이블을 마우스 오른쪽 단추로 클릭 하 고 클릭 **메모리 최적화 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-134">In hello **Object Explorer**, right-click on hello table, and then click **Memory Optimization Advisor**.</span></span>
   
   * <span data-ttu-id="29d8f-135">hello **테이블 메모리 최적화 관리자** 마법사가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-135">hello **Table Memory Optimizer Advisor** wizard is displayed.</span></span>
3. <span data-ttu-id="29d8f-136">Hello 마법사에서 **마이그레이션 유효성 검사** (또는 hello **다음** 단추) toosee hello 테이블에 있는 경우 지원 되지 않는 메모리 액세스에 최적화 된 테이블에서 지원 되지 않는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-136">In hello wizard, click **Migration validation** (or hello **Next** button) toosee if hello table has any unsupported features that are unsupported in memory-optimized tables.</span></span> <span data-ttu-id="29d8f-137">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29d8f-137">For more information, see:</span></span>
   
   * <span data-ttu-id="29d8f-138">hello *메모리 최적화 검사 목록이* 에 [메모리 최적화 관리자](http://msdn.microsoft.com/library/dn284308.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-138">hello *memory optimization checklist* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span></span>
   * <span data-ttu-id="29d8f-139">[메모리 내 OLTP에서 지원되지 않는 TRANSACT-SQL 항목](http://msdn.microsoft.com/library/dn246937.aspx).</span><span class="sxs-lookup"><span data-stu-id="29d8f-139">[Transact-SQL Constructs Not Supported by In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span></span>
   * <span data-ttu-id="29d8f-140">[마이그레이션 tooIn 메모리 내 OLTP](http://msdn.microsoft.com/library/dn247639.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-140">[Migrating tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span></span>
4. <span data-ttu-id="29d8f-141">Hello 테이블에 지원 되지 않는 기능이 없습니다, hello 관리자는 사용자에 대 한 hello 실제 스키마 및 데이터 마이그레이션을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-141">If hello table has no unsupported features, hello advisor can perform hello actual schema and data migration for you.</span></span>

#### <a name="manual-t-sql"></a><span data-ttu-id="29d8f-142">수동 T-SQL</span><span class="sxs-lookup"><span data-stu-id="29d8f-142">Manual T-SQL</span></span>
<span data-ttu-id="29d8f-143">toouse이 마이그레이션 옵션:</span><span class="sxs-lookup"><span data-stu-id="29d8f-143">toouse this migration option:</span></span>

1. <span data-ttu-id="29d8f-144">SSMS (또는 이와 유사한 유틸리티)을 사용 하 여 tooyour 테스트 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-144">Connect tooyour test database by using SSMS (or a similar utility).</span></span>
2. <span data-ttu-id="29d8f-145">테이블 및 인덱스에 대 한 hello 전체 T-SQL 스크립트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-145">Obtain hello complete T-SQL script for your table and its indexes.</span></span>
   
   * <span data-ttu-id="29d8f-146">SSMS에서 테이블 노드를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-146">In SSMS, right-click your table node.</span></span>
   * <span data-ttu-id="29d8f-147">**테이블 스크립팅** > **CREATE** > **새 쿼리 창**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-147">Click **Script Table As** > **CREATE To** > **New Query Window**.</span></span>
3. <span data-ttu-id="29d8f-148">Hello 스크립트 창에서 추가 WITH (MEMORY_OPTIMIZED = ON) toohello CREATE TABLE 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-148">In hello script window, add WITH (MEMORY_OPTIMIZED = ON) toohello CREATE TABLE statement.</span></span>
4. <span data-ttu-id="29d8f-149">클러스터형 인덱스가 있으면 tooNONCLUSTERED 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-149">If there is a CLUSTERED index, change it tooNONCLUSTERED.</span></span>
5. <span data-ttu-id="29d8f-150">SP_RENAME을 사용 하 여 hello 기존 테이블을 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-150">Rename hello existing table by using SP_RENAME.</span></span>
6. <span data-ttu-id="29d8f-151">편집 된 CREATE TABLE 스크립트를 실행 하 여 hello 테이블의 새 메모리 액세스에 최적화 된 복사본을 hello를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-151">Create hello new memory-optimized copy of hello table by running your edited CREATE TABLE script.</span></span>
7. <span data-ttu-id="29d8f-152">INSERT를 사용 하 여 hello 데이터 tooyour 메모리 액세스에 최적화 된 테이블을 복사 중... 선택 *로:</span><span class="sxs-lookup"><span data-stu-id="29d8f-152">Copy hello data tooyour memory-optimized table by using INSERT...SELECT * INTO:</span></span>

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a><span data-ttu-id="29d8f-153">5단계(선택 사항): 저장 프로시저 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="29d8f-153">Step 5 (optional): Migrate stored procedures</span></span>
<span data-ttu-id="29d8f-154">hello 메모리 내 기능 성능 향상된을 위해 저장된 프로시저를 수정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-154">hello In-Memory feature can also modify a stored procedure for improved performance.</span></span>

### <a name="considerations-with-natively-compiled-stored-procedures"></a><span data-ttu-id="29d8f-155">고유하게 컴파일된 저장 프로시저를 사용할 때 고려 사항</span><span class="sxs-lookup"><span data-stu-id="29d8f-155">Considerations with natively compiled stored procedures</span></span>
<span data-ttu-id="29d8f-156">고유 하 게 컴파일된 저장된 프로시저 hello 다음 옵션은 T-SQL WITH 절에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-156">A natively compiled stored procedure must have hello following options on its T-SQL WITH clause:</span></span>

* <span data-ttu-id="29d8f-157">NATIVE_COMPILATION</span><span class="sxs-lookup"><span data-stu-id="29d8f-157">NATIVE_COMPILATION</span></span>
* <span data-ttu-id="29d8f-158">SCHEMABINDING: 저장된 프로시저를 hello 의미 테이블 hello 저장 프로시저를 삭제 하지 않는 한 hello 저장 프로시저에 영향을 주므로 어떤 식으로든 변경할 열 정의 가질 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-158">SCHEMABINDING: meaning tables that hello stored procedure cannot have their column definitions changed in any way that would affect hello stored procedure, unless you drop hello stored procedure.</span></span>

<span data-ttu-id="29d8f-159">네이티브 모듈은 트랜잭션 관리에 하나의 큰 [ATOMIC 블록](http://msdn.microsoft.com/library/dn452281.aspx) 을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-159">A native module must use one big [ATOMIC blocks](http://msdn.microsoft.com/library/dn452281.aspx) for transaction management.</span></span> <span data-ttu-id="29d8f-160">명시적 BEGIN TRANSACTION 또는 ROLLBACK TRANSACTION에 대한 역할이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-160">There is no role for an explicit BEGIN TRANSACTION, or for ROLLBACK TRANSACTION.</span></span> <span data-ttu-id="29d8f-161">비즈니스 규칙의 위반을 검색 하는 코드를 hello atomic 블록을 종료할 수는 [THROW](http://msdn.microsoft.com/library/ee677615.aspx) 문.</span><span class="sxs-lookup"><span data-stu-id="29d8f-161">If your code detects a violation of a business rule, it can terminate hello atomic block with a [THROW](http://msdn.microsoft.com/library/ee677615.aspx) statement.</span></span>

### <a name="typical-create-procedure-for-natively-compiled"></a><span data-ttu-id="29d8f-162">고유하게 컴파일된 일반적인 만들기 프로시저</span><span class="sxs-lookup"><span data-stu-id="29d8f-162">Typical CREATE PROCEDURE for natively compiled</span></span>
<span data-ttu-id="29d8f-163">일반적으로 hello T-SQL toocreate 고유 하 게 컴파일된 저장된 프로시저는 서식 파일을 다음 유사한 toohello.</span><span class="sxs-lookup"><span data-stu-id="29d8f-163">Typically hello T-SQL toocreate a natively compiled stored procedure is similar toohello following template:</span></span>

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

* <span data-ttu-id="29d8f-164">TRANSACTION_ISOLATION_LEVEL hello에 대 한 스냅숏은 hello 가장 일반적인 고유 하 게 컴파일된 hello에 대 한 값을 저장 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-164">For hello TRANSACTION_ISOLATION_LEVEL, SNAPSHOT is hello most common value for hello natively compiled stored procedure.</span></span> <span data-ttu-id="29d8f-165">그러나의 하위 집합 hello 다른 값도 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-165">However,  a subset of hello other values are also supported:</span></span>
  
  * <span data-ttu-id="29d8f-166">반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="29d8f-166">REPEATABLE READ</span></span>
  * <span data-ttu-id="29d8f-167">직렬화 가능</span><span class="sxs-lookup"><span data-stu-id="29d8f-167">SERIALIZABLE</span></span>
* <span data-ttu-id="29d8f-168">hello sys.languages 뷰에서 hello 언어 값이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-168">hello LANGUAGE value must be present in hello sys.languages view.</span></span>

### <a name="how-toomigrate-a-stored-procedure"></a><span data-ttu-id="29d8f-169">어떻게 toomigrate 저장된 프로시저</span><span class="sxs-lookup"><span data-stu-id="29d8f-169">How toomigrate a stored procedure</span></span>
<span data-ttu-id="29d8f-170">hello 마이그레이션 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-170">hello migration steps are:</span></span>

1. <span data-ttu-id="29d8f-171">Hello CREATE PROCEDURE 스크립트 toohello 일반 해석 된 저장된 프로시저를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-171">Obtain hello CREATE PROCEDURE script toohello regular interpreted stored procedure.</span></span>
2. <span data-ttu-id="29d8f-172">해당 헤더 toomatch hello 이전 서식 파일을 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-172">Rewrite its header toomatch hello previous template.</span></span>
3. <span data-ttu-id="29d8f-173">T-SQL 코드 hello 저장 프로시저가 고유 하 게 컴파일된 저장된 프로시저에 지원 되지 않는 기능이 사용 되는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-173">Ascertain whether hello stored procedure T-SQL code uses any features that are not supported for natively compiled stored procedures.</span></span> <span data-ttu-id="29d8f-174">필요한 경우 해결 방법을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-174">Implement workarounds if necessary.</span></span>
   
   * <span data-ttu-id="29d8f-175">자세한 내용은 [고유하게 컴파일된 저장 프로시저에 대한 마이그레이션 문제](http://msdn.microsoft.com/library/dn296678.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29d8f-175">For details see [Migration Issues for Natively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span></span>
4. <span data-ttu-id="29d8f-176">SP_RENAME을 사용 하 여 hello 이전 저장된 프로시저를 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-176">Rename hello old stored procedure by using SP_RENAME.</span></span> <span data-ttu-id="29d8f-177">또는 단순히 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-177">Or simply DROP it.</span></span>
5. <span data-ttu-id="29d8f-178">편집된 프로시저 T-SQL 만들기 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-178">Run your edited CREATE PROCEDURE T-SQL script.</span></span>

## <a name="step-6-run-your-workload-in-test"></a><span data-ttu-id="29d8f-179">6단계: 테스트에서 워크로드 실행</span><span class="sxs-lookup"><span data-stu-id="29d8f-179">Step 6: Run your workload in test</span></span>
<span data-ttu-id="29d8f-180">프로덕션 데이터베이스에서 실행 되는 비슷한 toohello 작업 하는 테스트 데이터베이스에서 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-180">Run a workload in your test database that is similar toohello workload that runs in your production database.</span></span> <span data-ttu-id="29d8f-181">이 테이블 및 저장된 프로시저에 대 한 hello 메모리 내 기능을 사용 하 여 달성 hello 성능 향상에 도움이 알아낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-181">This should reveal hello performance gain achieved by your use of hello In-Memory feature for tables and stored procedures.</span></span>

<span data-ttu-id="29d8f-182">Hello 워크 로드의 주요 특성은 합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-182">Major attributes of hello workload are:</span></span>

* <span data-ttu-id="29d8f-183">동시 연결 수.</span><span class="sxs-lookup"><span data-stu-id="29d8f-183">Number of concurrent connections.</span></span>
* <span data-ttu-id="29d8f-184">읽기/쓰기 비율.</span><span class="sxs-lookup"><span data-stu-id="29d8f-184">Read/write ratio.</span></span>

<span data-ttu-id="29d8f-185">tootailor 실행된 hello 테스트 작업 사용해봅니다에 나와 있는 hello 편리한 ostress.exe 도구 [여기](sql-database-in-memory.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-185">tootailor and run hello test workload, consider using hello handy ostress.exe tool, which illustrated in [here](sql-database-in-memory.md).</span></span>

<span data-ttu-id="29d8f-186">hello에서 테스트를 실행 toominimize 네트워크 대기 시간이 동일한 Azure 지역 hello 데이터베이스가 있는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-186">toominimize network latency, run your test in hello same Azure geographic region where hello database exists.</span></span>

## <a name="step-7-post-implementation-monitoring"></a><span data-ttu-id="29d8f-187">7단계: 사후 실현 모니터링</span><span class="sxs-lookup"><span data-stu-id="29d8f-187">Step 7: Post-implementation monitoring</span></span>
<span data-ttu-id="29d8f-188">프로덕션 환경에서 메모리 내에 구현의 hello 성능 효과 모니터링 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="29d8f-188">Consider monitoring hello performance effects of your In-Memory implementations in production:</span></span>

* <span data-ttu-id="29d8f-189">[메모리 내 저장소 모니터링](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="29d8f-189">[Monitor In-Memory Storage](sql-database-in-memory-oltp-monitoring.md).</span></span>
* [<span data-ttu-id="29d8f-190">동적 관리 뷰를 사용하여 Azure SQL 데이터베이스 모니터링</span><span class="sxs-lookup"><span data-stu-id="29d8f-190">Monitoring Azure SQL Database using dynamic management views</span></span>](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a><span data-ttu-id="29d8f-191">관련 링크</span><span class="sxs-lookup"><span data-stu-id="29d8f-191">Related links</span></span>
* [<span data-ttu-id="29d8f-192">메모리 내 OLTP(메모리 내 최적화)</span><span class="sxs-lookup"><span data-stu-id="29d8f-192">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
* [<span data-ttu-id="29d8f-193">소개 tooNatively 컴파일 저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="29d8f-193">Introduction tooNatively Compiled Stored Procedures</span></span>](http://msdn.microsoft.com/library/dn133184.aspx)
* [<span data-ttu-id="29d8f-194">메모리 최적화 관리자</span><span class="sxs-lookup"><span data-stu-id="29d8f-194">Memory Optimization Advisor</span></span>](http://msdn.microsoft.com/library/dn284308.aspx)


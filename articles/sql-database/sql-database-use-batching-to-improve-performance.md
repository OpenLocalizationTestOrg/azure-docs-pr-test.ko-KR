---
title: "aaaHow toouse tooimprove Azure SQL 데이터베이스 응용 프로그램 성능 일괄 처리"
description: "hello 항목 증거가 제공는 일괄 처리 데이터베이스 작업을 크게 imroves hello 속도 Azure SQL 데이터베이스 응용 프로그램의 확장성입니다. 이러한 일괄 처리 기법을 모든 SQL Server 데이터베이스에 대해 설명 하지만 hello hello 문서는 Azure에서."
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 124b203ee69c595f0813852ff09ef9ec6841233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a><span data-ttu-id="ab194-104">어떻게 toouse tooimprove SQL 데이터베이스 응용 프로그램 성능 일괄 처리</span><span class="sxs-lookup"><span data-stu-id="ab194-104">How toouse batching tooimprove SQL Database application performance</span></span>
<span data-ttu-id="ab194-105">작업 tooAzure SQL 데이터베이스를 크게 일괄 처리 응용 프로그램의 hello 성능 및 확장성을 향상 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-105">Batching operations tooAzure SQL Database significantly improves hello performance and scalability of your applications.</span></span> <span data-ttu-id="ab194-106">이 문서의 첫 번째 부분 hello 순서 toounderstand hello 이점에 순차적 및 일괄 처리 된 요청 tooa SQL 데이터베이스 비교 하는 몇 가지 샘플 테스트 결과 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-106">In order toounderstand hello benefits, hello first part of this article covers some sample test results that compare sequential and batched requests tooa SQL Database.</span></span> <span data-ttu-id="ab194-107">hello hello 문서의 나머지 부분에서는 표시 hello 기술, 시나리오 및 고려 사항 toohelp toouse Azure 응용 프로그램에서 성공적으로 일괄 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-107">hello remainder of hello article shows hello techniques, scenarios, and considerations toohelp you toouse batching successfully in your Azure applications.</span></span>

## <a name="why-is-batching-important-for-sql-database"></a><span data-ttu-id="ab194-108">SQL 데이터베이스에 일괄 처리가 중요한 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="ab194-108">Why is batching important for SQL Database?</span></span>
<span data-ttu-id="ab194-109">호출 tooa 원격 서비스가 일괄 처리 하는 것은 성능 및 확장성을 높이기 위한 잘 알려진 전략입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-109">Batching calls tooa remote service is a well-known strategy for increasing performance and scalability.</span></span> <span data-ttu-id="ab194-110">고정 비용 tooany 직렬화, 네트워크 전송 및 역직렬화 하는 등의 원격 서비스와의 상호 작용을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-110">There are fixed processing costs tooany interactions with a remote service, such as serialization, network transfer, and deserialization.</span></span> <span data-ttu-id="ab194-111">다수의 분리된 트랜잭션을 하나의 배치로 패키징하면 이러한 비용이 최소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-111">Packaging many separate transactions into a single batch minimizes these costs.</span></span>

<span data-ttu-id="ab194-112">이 문서에서는 다양 한 SQL 데이터베이스 일괄 처리 전략 및 시나리오 tooexamine를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-112">In this paper, we want tooexamine various SQL Database batching strategies and scenarios.</span></span> <span data-ttu-id="ab194-113">이러한 전략 옵션은 SQL Server를 사용 하는 온-프레미스 응용 프로그램에 대 한 중요 한도는 SQL 데이터베이스에 대 한 일괄 처리 hello 사용을 강조 표시에 대 한 몇 가지 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-113">Although these strategies are also important for on-premises applications that use SQL Server, there are several reasons for highlighting hello use of batching for SQL Database:</span></span>

* <span data-ttu-id="ab194-114">SQL 데이터베이스 외부 hello에서 액세스 하는 경우에 특히 SQL 데이터베이스를 액세스 하는 동안 잠재적으로 큰 네트워크 지연이 있는 동일한 Microsoft Azure 데이터 센터입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-114">There is potentially greater network latency in accessing SQL Database, especially if you are accessing SQL Database from outside hello same Microsoft Azure datacenter.</span></span>
* <span data-ttu-id="ab194-115">SQL 데이터베이스 이면 hello 데이터의 효율성을 hello hello 다중 테 넌 트 특성 액세스 레이어 하면서 안정적일 toohello hello 데이터베이스의 전반적인 확장성.</span><span class="sxs-lookup"><span data-stu-id="ab194-115">hello multitenant characteristics of SQL Database means that hello efficiency of hello data access layer correlates toohello overall scalability of hello database.</span></span> <span data-ttu-id="ab194-116">SQL 데이터베이스에서 데이터베이스 리소스 toohello 손해를 끼칠 정도로 다른 테 넌 트를 차지 단일 테 넌 트/사용자를 방지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-116">SQL Database must prevent any single tenant/user from monopolizing database resources toohello detriment of other tenants.</span></span> <span data-ttu-id="ab194-117">미리 정의 된 할당량 초과 응답 toousage, SQL 데이터베이스 처리량이 줄어들 하거나 제한 예외로 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-117">In response toousage in excess of predefined quotas, SQL Database can reduce throughput or respond with throttling exceptions.</span></span> <span data-ttu-id="ab194-118">일괄 처리와 같은 효율성 toodo 하면 이러한 한도 도달 하기 전에 SQL 데이터베이스에서 더 많은 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-118">Efficiencies, such as batching, enable you toodo more work on SQL Database before reaching these limits.</span></span> 
* <span data-ttu-id="ab194-119">일괄 처리는 다수의 데이터베이스(분할)를 사용하는 아키텍처에 대해서도 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-119">Batching is also effective for architectures that use multiple databases (sharding).</span></span> <span data-ttu-id="ab194-120">각 데이터베이스 단위와의 상호 작용의 hello 효율성은 여전히 전체 확장성에서 중요 한 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-120">hello efficiency of your interaction with each database unit is still a key factor in your overall scalability.</span></span> 

<span data-ttu-id="ab194-121">SQL 데이터베이스를 사용 하 여 hello 이점 중 하나는 없는지 toomanage hello 서버 호스트 hello 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-121">One of hello benefits of using SQL Database is that you don’t have toomanage hello servers that host hello database.</span></span> <span data-ttu-id="ab194-122">그러나이 관리 되는 인프라는 데이터베이스 최적화에 대 한 다르게 toothink을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-122">However, this managed infrastructure also means that you have toothink differently about database optimizations.</span></span> <span data-ttu-id="ab194-123">더 이상 tooimprove hello 데이터베이스 하드웨어 또는 네트워크 인프라를 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-123">You can no longer look tooimprove hello database hardware or network infrastructure.</span></span> <span data-ttu-id="ab194-124">Microsoft Azure는 이러한 환경을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-124">Microsoft Azure controls those environments.</span></span> <span data-ttu-id="ab194-125">hello 주 영역 제어할 수 있는 경우 SQL 데이터베이스와 응용 프로그램 상호 작용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ab194-125">hello main area that you can control is how your application interacts with SQL Database.</span></span> <span data-ttu-id="ab194-126">일괄 처리는 이러한 최적화 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-126">Batching is one of these optimizations.</span></span> 

<span data-ttu-id="ab194-127">hello 문서의 첫 번째 부분 hello SQL 데이터베이스를 사용 하는.NET 응용 프로그램에 대 한 다양 한 일괄 처리 기법을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-127">hello first part of hello paper examines various batching techniques for .NET applications that use SQL Database.</span></span> <span data-ttu-id="ab194-128">hello 마지막 두 섹션에서는 일괄 처리 지침 및 시나리오를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-128">hello last two sections cover batching guidelines and scenarios.</span></span>

## <a name="batching-strategies"></a><span data-ttu-id="ab194-129">일괄 처리 전략</span><span class="sxs-lookup"><span data-stu-id="ab194-129">Batching strategies</span></span>
### <a name="note-about-timing-results-in-this-topic"></a><span data-ttu-id="ab194-130">이 문서의 타이밍 결과에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="ab194-130">Note about timing results in this topic</span></span>
> [!NOTE]
> <span data-ttu-id="ab194-131">결과 벤치 마크 하지만 tooshow **상대적인 성능**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-131">Results are not benchmarks but are meant tooshow **relative performance**.</span></span> <span data-ttu-id="ab194-132">타이밍은 평균적으로 최소 10회의 테스트 실행을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-132">Timings are based on an average of at least 10 test runs.</span></span> <span data-ttu-id="ab194-133">작업은 빈 테이블로의 삽입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-133">Operations are inserts into an empty table.</span></span> <span data-ttu-id="ab194-134">새 hello를 사용 하 여 V12 데이터베이스에서 발생할 수 있는 toothroughput 반드시 일치 하지 않는 하 고 이러한 테스트 된 측정 된 V12 이전, [서비스 계층](sql-database-service-tiers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-134">These tests were measured pre-V12, and they do not necessarily correspond toothroughput that you might experience in a V12 database using hello new [service tiers](sql-database-service-tiers.md).</span></span> <span data-ttu-id="ab194-135">hello 상대적 이점의 일괄 처리 기법 hello 비슷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-135">hello relative benefit of hello batching technique should be similar.</span></span>
> 
> 

### <a name="transactions"></a><span data-ttu-id="ab194-136">트랜잭션</span><span class="sxs-lookup"><span data-stu-id="ab194-136">Transactions</span></span>
<span data-ttu-id="ab194-137">이상한 toobegin 트랜잭션을 이야기 하 여 일괄 처리를 살펴볼 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-137">It seems strange toobegin a review of batching by discussing transactions.</span></span> <span data-ttu-id="ab194-138">하지만 클라이언트 쪽 트랜잭션의 hello 사용 성능을 개선 하는 미묘한 서버 쪽 일괄 처리 효과입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-138">But hello use of client-side transactions has a subtle server-side batching effect that improves performance.</span></span> <span data-ttu-id="ab194-139">및 트랜잭션을 순차적 작업의 가장 빠른 방법 tooimprove 성능을 제공 하므로 코드 몇 줄만 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-139">And transactions can be added with only a few lines of code, so they provide a fast way tooimprove performance of sequential operations.</span></span>

<span data-ttu-id="ab194-140">Hello 삽입의 시퀀스를 포함 하는 C# 코드를 다음을 고려 하 고 간단한 테이블에 대 한 작업을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-140">Consider hello following C# code that contains a sequence of insert and update operations on a simple table.</span></span>

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

<span data-ttu-id="ab194-141">ADO.NET 코드를 순차적으로 다음 hello 이러한 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-141">hello following ADO.NET code sequentially performs these operations.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

<span data-ttu-id="ab194-142">hello 가장 좋은 방법은 toooptimize이이 코드는 tooimplement 이러한 호출의 클라이언트 쪽 일괄 처리의 몇 가지 형태입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-142">hello best way toooptimize this code is tooimplement some form of client-side batching of these calls.</span></span> <span data-ttu-id="ab194-143">하지만이 코드의 간단한 방법을 tooincrease hello 성능을 트랜잭션에서 hello 호출 시퀀스를 단순히 래핑하여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-143">But there is a simple way tooincrease hello performance of this code by simply wrapping hello sequence of calls in a transaction.</span></span> <span data-ttu-id="ab194-144">다음은 트랜잭션을 사용 하는 동일한 코드 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-144">Here is hello same code that uses a transaction.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

<span data-ttu-id="ab194-145">트랜잭션이 양쪽 예제에 실제로 사용되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-145">Transactions are actually being used in both of these examples.</span></span> <span data-ttu-id="ab194-146">Hello 첫 번째 예제에서는 각각의 개별 호출이 암시적인 트랜잭션이 며 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-146">In hello first example, each individual call is an implicit transaction.</span></span> <span data-ttu-id="ab194-147">Hello 두 번째 예제에서는 명시적 트랜잭션을 모두 hello 호출을 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-147">In hello second example, an explicit transaction wraps all of hello calls.</span></span> <span data-ttu-id="ab194-148">Hello에 대 한 hello 설명서 당 [미리 쓰기 트랜잭션 로그](https://msdn.microsoft.com/library/ms186259.aspx), hello 트랜잭션이 커밋될 때 플러시된 toohello 디스크를은 로그 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-148">Per hello documentation for hello [write-ahead transaction log](https://msdn.microsoft.com/library/ms186259.aspx), log records are flushed toohello disk when hello transaction commits.</span></span> <span data-ttu-id="ab194-149">따라서 트랜잭션에 많은 호출을 포함할수록 hello toohello 트랜잭션 로그 쓰기 지연 시킬 수 hello 트랜잭션이 커밋될 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-149">So by including more calls in a transaction, hello write toohello transaction log can delay until hello transaction is committed.</span></span> <span data-ttu-id="ab194-150">실제로 사용할 수 있도록 hello 쓰기 toohello 서버의 트랜잭션 로그에 대 한 일괄 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-150">In effect, you are enabling batching for hello writes toohello server’s transaction log.</span></span>

<span data-ttu-id="ab194-151">다음 표에서 hello 몇 가지 임시 테스트 결과 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-151">hello following table shows some ad-hoc testing results.</span></span> <span data-ttu-id="ab194-152">hello 테스트 hello 및 트랜잭션을 사용 하지 않고 동일한 순차적 삽입을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-152">hello tests performed hello same sequential inserts with and without transactions.</span></span> <span data-ttu-id="ab194-153">보다 다양 한 측면에 대 한 hello 첫 번째 테스트 집합은 Microsoft Azure의 랩톱 toohello 데이터베이스에서 원격으로 실행 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-153">For more perspective, hello first set of tests ran remotely from a laptop toohello database in Microsoft Azure.</span></span> <span data-ttu-id="ab194-154">hello 번째 테스트 집합 실행 된 클라우드 서비스와을 둘 다 있는 hello 내에서 동일한 데이터베이스에서 Microsoft Azure 데이터 센터 (West US)입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-154">hello second set of tests ran from a cloud service and database that both resided within hello same Microsoft Azure datacenter (West US).</span></span> <span data-ttu-id="ab194-155">hello 다음 표에 hello 기간 및 트랜잭션을 사용 하지 않고 순차적 삽입 시간 (밀리초)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-155">hello following table shows hello duration in milliseconds of sequential inserts with and without transactions.</span></span>

<span data-ttu-id="ab194-156">**온-프레미스 tooAzure**:</span><span class="sxs-lookup"><span data-stu-id="ab194-156">**On-Premises tooAzure**:</span></span>

| <span data-ttu-id="ab194-157">작업</span><span class="sxs-lookup"><span data-stu-id="ab194-157">Operations</span></span> | <span data-ttu-id="ab194-158">트랜잭션 없음(밀리초)</span><span class="sxs-lookup"><span data-stu-id="ab194-158">No Transaction (ms)</span></span> | <span data-ttu-id="ab194-159">트랜잭션(밀리초)</span><span class="sxs-lookup"><span data-stu-id="ab194-159">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ab194-160">1</span><span class="sxs-lookup"><span data-stu-id="ab194-160">1</span></span> |<span data-ttu-id="ab194-161">130</span><span class="sxs-lookup"><span data-stu-id="ab194-161">130</span></span> |<span data-ttu-id="ab194-162">402</span><span class="sxs-lookup"><span data-stu-id="ab194-162">402</span></span> |
| <span data-ttu-id="ab194-163">10</span><span class="sxs-lookup"><span data-stu-id="ab194-163">10</span></span> |<span data-ttu-id="ab194-164">1208</span><span class="sxs-lookup"><span data-stu-id="ab194-164">1208</span></span> |<span data-ttu-id="ab194-165">1226</span><span class="sxs-lookup"><span data-stu-id="ab194-165">1226</span></span> |
| <span data-ttu-id="ab194-166">100</span><span class="sxs-lookup"><span data-stu-id="ab194-166">100</span></span> |<span data-ttu-id="ab194-167">12662</span><span class="sxs-lookup"><span data-stu-id="ab194-167">12662</span></span> |<span data-ttu-id="ab194-168">10395</span><span class="sxs-lookup"><span data-stu-id="ab194-168">10395</span></span> |
| <span data-ttu-id="ab194-169">1000</span><span class="sxs-lookup"><span data-stu-id="ab194-169">1000</span></span> |<span data-ttu-id="ab194-170">128852</span><span class="sxs-lookup"><span data-stu-id="ab194-170">128852</span></span> |<span data-ttu-id="ab194-171">102917</span><span class="sxs-lookup"><span data-stu-id="ab194-171">102917</span></span> |

<span data-ttu-id="ab194-172">**Azure tooAzure (동일한 데이터 센터)**:</span><span class="sxs-lookup"><span data-stu-id="ab194-172">**Azure tooAzure (same datacenter)**:</span></span>

| <span data-ttu-id="ab194-173">작업</span><span class="sxs-lookup"><span data-stu-id="ab194-173">Operations</span></span> | <span data-ttu-id="ab194-174">트랜잭션 없음(밀리초)</span><span class="sxs-lookup"><span data-stu-id="ab194-174">No Transaction (ms)</span></span> | <span data-ttu-id="ab194-175">트랜잭션(밀리초)</span><span class="sxs-lookup"><span data-stu-id="ab194-175">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ab194-176">1</span><span class="sxs-lookup"><span data-stu-id="ab194-176">1</span></span> |<span data-ttu-id="ab194-177">21</span><span class="sxs-lookup"><span data-stu-id="ab194-177">21</span></span> |<span data-ttu-id="ab194-178">26</span><span class="sxs-lookup"><span data-stu-id="ab194-178">26</span></span> |
| <span data-ttu-id="ab194-179">10</span><span class="sxs-lookup"><span data-stu-id="ab194-179">10</span></span> |<span data-ttu-id="ab194-180">220</span><span class="sxs-lookup"><span data-stu-id="ab194-180">220</span></span> |<span data-ttu-id="ab194-181">56</span><span class="sxs-lookup"><span data-stu-id="ab194-181">56</span></span> |
| <span data-ttu-id="ab194-182">100</span><span class="sxs-lookup"><span data-stu-id="ab194-182">100</span></span> |<span data-ttu-id="ab194-183">2145</span><span class="sxs-lookup"><span data-stu-id="ab194-183">2145</span></span> |<span data-ttu-id="ab194-184">341</span><span class="sxs-lookup"><span data-stu-id="ab194-184">341</span></span> |
| <span data-ttu-id="ab194-185">1000</span><span class="sxs-lookup"><span data-stu-id="ab194-185">1000</span></span> |<span data-ttu-id="ab194-186">21479</span><span class="sxs-lookup"><span data-stu-id="ab194-186">21479</span></span> |<span data-ttu-id="ab194-187">2756</span><span class="sxs-lookup"><span data-stu-id="ab194-187">2756</span></span> |

> [!NOTE]
> <span data-ttu-id="ab194-188">결과가 기준은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-188">Results are not benchmarks.</span></span> <span data-ttu-id="ab194-189">Hello 참조 [이 항목의 타이밍 결과 대 한 참고](#note-about-timing-results-in-this-topic)합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-189">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="ab194-190">Hello 이전 테스트 결과에 따라 실제로 성능이 저하 트랜잭션에서 한 번의 작업을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-190">Based on hello previous test results, wrapping a single operation in a transaction actually decreases performance.</span></span> <span data-ttu-id="ab194-191">하지만 단일 트랜잭션 내에서 작업의 hello 수를 늘리면 hello 성능 향상이 두드러집니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-191">But as you increase hello number of operations within a single transaction, hello performance improvement becomes more marked.</span></span> <span data-ttu-id="ab194-192">hello Microsoft Azure 데이터 센터 내에서 모든 작업을 수행 하면 성능 차이 hello 더욱 분명 하 게 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-192">hello performance difference is also more noticeable when all operations occur within hello Microsoft Azure datacenter.</span></span> <span data-ttu-id="ab194-193">hello 외부 hello Microsoft Azure 데이터 센터에서 SQL 데이터베이스를 사용 하 여 대기 시간이 증가 이점 보다 커집니다 트랜잭션을 사용 하 여 hello 성능 향상을.</span><span class="sxs-lookup"><span data-stu-id="ab194-193">hello increased latency of using SQL Database from outside hello Microsoft Azure datacenter overshadows hello performance gain of using transactions.</span></span>

<span data-ttu-id="ab194-194">트랜잭션의 hello 사용 성능을 향상 시킬 수, 계속 너무[트랜잭션 및 연결에 대 한 모범 사례](https://msdn.microsoft.com/library/ms187484.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-194">Although hello use of transactions can increase performance, continue too[observe best practices for transactions and connections](https://msdn.microsoft.com/library/ms187484.aspx).</span></span> <span data-ttu-id="ab194-195">Hello 작업 완료 된 후 hello 트랜잭션을 짧게 및 닫기 hello 데이터베이스 연결을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-195">Keep hello transaction as short as possible, and close hello database connection after hello work completes.</span></span> <span data-ttu-id="ab194-196">문을 사용 하 여 hello 이전 예제에는 hello hello 이후 코드 블록이 완료 되 면 hello 연결 닫았는지 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-196">hello using statement in hello previous example assures that hello connection is closed when hello subsequent code block completes.</span></span>

<span data-ttu-id="ab194-197">hello 이전 예제에서는 두 개의 줄이 포함 된 로컬 트랜잭션을 tooany ADO.NET 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-197">hello previous example demonstrates that you can add a local transaction tooany ADO.NET code with two lines.</span></span> <span data-ttu-id="ab194-198">트랜잭션을 빠르게 tooimprove hello 성능을 순차적 하는 코드를 삽입, 업데이트 및 삭제 작업을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-198">Transactions offer a quick way tooimprove hello performance of code that makes sequential insert, update, and delete operations.</span></span> <span data-ttu-id="ab194-199">그러나 hello 빠른 성능을 변경 hello 코드 tootake의 장점은 테이블 반환 매개 변수와 같은 클라이언트 쪽 일괄 처리를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-199">However, for hello fastest performance, consider changing hello code further tootake advantage of client-side batching, such as table-valued parameters.</span></span>

<span data-ttu-id="ab194-200">ADO.NET의 트랜잭션에 대한 자세한 내용은 [ADO.NET의 로컬 트랜잭션](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab194-200">For more information about transactions in ADO.NET, see [Local Transactions in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span></span>

### <a name="table-valued-parameters"></a><span data-ttu-id="ab194-201">테이블 반환 매개 변수</span><span class="sxs-lookup"><span data-stu-id="ab194-201">Table-valued parameters</span></span>
<span data-ttu-id="ab194-202">테이블 반환 매개 변수는 Transact-SQL 문, 저장 프로시저, 함수의 매개 변수로 사용자 정의 테이블 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-202">Table-valued parameters support user-defined table types as parameters in Transact-SQL statements, stored procedures, and functions.</span></span> <span data-ttu-id="ab194-203">이 클라이언트 쪽 일괄 처리 기법 있습니다 toosend hello 테이블 반환 매개 변수 내에서 데이터의 여러 행입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-203">This client-side batching technique allows you toosend multiple rows of data within hello table-valued parameter.</span></span> <span data-ttu-id="ab194-204">toouse 테이블 반환 매개 변수는 먼저 테이블 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-204">toouse table-valued parameters, first define a table type.</span></span> <span data-ttu-id="ab194-205">hello Transact SQL 문 다음에 명명 된 테이블 형식을 만듭니다 **MyTableType**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-205">hello following Transact-SQL statement creates a table type named **MyTableType**.</span></span>

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


<span data-ttu-id="ab194-206">코드에서 만듭니다는 **DataTable** hello로 정확히 동일한 이름 및 유형의 hello 테이블 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-206">In code, you create a **DataTable** with hello exact same names and types of hello table type.</span></span> <span data-ttu-id="ab194-207">**DataTable** 을 저장 프로시저 호출 또는 텍스트 쿼리의 매개 변수로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-207">Pass this **DataTable** in a parameter in a text query or stored procedure call.</span></span> <span data-ttu-id="ab194-208">hello 다음 예제에서는 이러한 기법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-208">hello following example shows this technique:</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. hello following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

<span data-ttu-id="ab194-209">Hello 이전 예에서 hello **SqlCommand** 개체는 테이블 반환 매개 변수에서 행을 삽입  **@TestTvp** 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-209">In hello previous example, hello **SqlCommand** object inserts rows from a table-valued parameter, **@TestTvp**.</span></span> <span data-ttu-id="ab194-210">이전에 만든 hello **DataTable** 개체가 hello로 toothis 매개 변수를 할당 된 **SqlCommand.Parameters.Add** 메서드.</span><span class="sxs-lookup"><span data-stu-id="ab194-210">hello previously created **DataTable** object is assigned toothis parameter with hello **SqlCommand.Parameters.Add** method.</span></span> <span data-ttu-id="ab194-211">하나의 일괄 처리 hello 삽입 호출 크게 증가 hello 성능 순차적 삽입을 통해 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-211">Batching hello inserts in one call significantly increases hello performance over sequential inserts.</span></span>

<span data-ttu-id="ab194-212">tooimprove hello 이전 예에서 좀더 나아가, 텍스트 기반 명령 대신 저장된 프로시저를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-212">tooimprove hello previous example further, use a stored procedure instead of a text-based command.</span></span> <span data-ttu-id="ab194-213">다음 TRANSACT-SQL 명령을 hello hello를 사용 하는 저장된 프로시저를 만듭니다. **SimpleTestTableType** 테이블 반환 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-213">hello following Transact-SQL command creates a stored procedure that takes hello **SimpleTestTableType** table-valued parameter.</span></span>

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

<span data-ttu-id="ab194-214">다음 hello 변경 **SqlCommand** 개체 hello 이전 코드 예제에서는 toohello 다음에 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-214">Then change hello **SqlCommand** object declaration in hello previous code example toohello following.</span></span>

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

<span data-ttu-id="ab194-215">대부분의 경우 테이블 반환 매개 변수는 다른 일괄 처리 기법과 동등하거나 그 보다 뛰어난 성능을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-215">In most cases, table-valued parameters have equivalent or better performance than other batching techniques.</span></span> <span data-ttu-id="ab194-216">테이블 반환 매개 변수는 다른 옵션에 비해 융통성이 많기 때문에 더 좋을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-216">Table-valued parameters are often preferable, because they are more flexible than other options.</span></span> <span data-ttu-id="ab194-217">예를 들어, SQL 대량 복사 등의 다른 방법은 집합이 새로운 행 hello 삽입만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-217">For example, other techniques, such as SQL bulk copy, only permit hello insertion of new rows.</span></span> <span data-ttu-id="ab194-218">테이블 반환 매개 변수를 저장 하는 hello 프로시저 toodetermine 어떤 행이 업데이트에에서 논리를 사용할 수 있고 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-218">But with table-valued parameters, you can use logic in hello stored procedure toodetermine which rows are updates and which are inserts.</span></span> <span data-ttu-id="ab194-219">hello 테이블 형식이 수정된 toocontain hello 지정 행은 삽입, 업데이트 또는 삭제 여부를 나타내는 "작업" 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-219">hello table type can also be modified toocontain an “Operation” column that indicates whether hello specified row should be inserted, updated, or deleted.</span></span>

<span data-ttu-id="ab194-220">다음 표는 hello 밀리초에서 hello 테이블 반환 매개 변수 사용에 대 한 임시 테스트 결과 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-220">hello following table shows ad-hoc test results for hello use of table-valued parameters in milliseconds.</span></span>

| <span data-ttu-id="ab194-221">작업</span><span class="sxs-lookup"><span data-stu-id="ab194-221">Operations</span></span> | <span data-ttu-id="ab194-222">온-프레미스 tooAzure (ms)</span><span class="sxs-lookup"><span data-stu-id="ab194-222">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="ab194-223">Azure 동일한 데이터 센터(밀리초)</span><span class="sxs-lookup"><span data-stu-id="ab194-223">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ab194-224">1</span><span class="sxs-lookup"><span data-stu-id="ab194-224">1</span></span> |<span data-ttu-id="ab194-225">124</span><span class="sxs-lookup"><span data-stu-id="ab194-225">124</span></span> |<span data-ttu-id="ab194-226">32</span><span class="sxs-lookup"><span data-stu-id="ab194-226">32</span></span> |
| <span data-ttu-id="ab194-227">10</span><span class="sxs-lookup"><span data-stu-id="ab194-227">10</span></span> |<span data-ttu-id="ab194-228">131</span><span class="sxs-lookup"><span data-stu-id="ab194-228">131</span></span> |<span data-ttu-id="ab194-229">25</span><span class="sxs-lookup"><span data-stu-id="ab194-229">25</span></span> |
| <span data-ttu-id="ab194-230">100</span><span class="sxs-lookup"><span data-stu-id="ab194-230">100</span></span> |<span data-ttu-id="ab194-231">338</span><span class="sxs-lookup"><span data-stu-id="ab194-231">338</span></span> |<span data-ttu-id="ab194-232">51</span><span class="sxs-lookup"><span data-stu-id="ab194-232">51</span></span> |
| <span data-ttu-id="ab194-233">1000</span><span class="sxs-lookup"><span data-stu-id="ab194-233">1000</span></span> |<span data-ttu-id="ab194-234">2615</span><span class="sxs-lookup"><span data-stu-id="ab194-234">2615</span></span> |<span data-ttu-id="ab194-235">382</span><span class="sxs-lookup"><span data-stu-id="ab194-235">382</span></span> |
| <span data-ttu-id="ab194-236">10000</span><span class="sxs-lookup"><span data-stu-id="ab194-236">10000</span></span> |<span data-ttu-id="ab194-237">23830</span><span class="sxs-lookup"><span data-stu-id="ab194-237">23830</span></span> |<span data-ttu-id="ab194-238">3586</span><span class="sxs-lookup"><span data-stu-id="ab194-238">3586</span></span> |

> [!NOTE]
> <span data-ttu-id="ab194-239">결과가 기준은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-239">Results are not benchmarks.</span></span> <span data-ttu-id="ab194-240">Hello 참조 [이 항목의 타이밍 결과 대 한 참고](#note-about-timing-results-in-this-topic)합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-240">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="ab194-241">일괄 처리에서 hello 성능 이점이 즉시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-241">hello performance gain from batching is immediately apparent.</span></span> <span data-ttu-id="ab194-242">이전의 순차적 테스트 hello에에서 1000 개으 작업 외부 hello 데이터 센터 및 hello 데이터 센터 내에서 21 초가 129 초가 소요 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-242">In hello previous sequential test, 1000 operations took 129 seconds outside hello datacenter and 21 seconds from within hello datacenter.</span></span> <span data-ttu-id="ab194-243">하지만 테이블 반환 매개 변수를 가진 1000 개으 작업 사용만 hello 데이터 센터 외부 2.6 초 않으며 0.4 초만 hello 데이터 센터 내에서.</span><span class="sxs-lookup"><span data-stu-id="ab194-243">But with table-valued parameters, 1000 operations take only 2.6 seconds outside hello datacenter and 0.4 seconds within hello datacenter.</span></span>

<span data-ttu-id="ab194-244">테이블 반환 매개 변수에 대한 자세한 내용은 [테이블 반환 매개 변수](https://msdn.microsoft.com/library/bb510489.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab194-244">For more information on table-valued parameters, see [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

### <a name="sql-bulk-copy"></a><span data-ttu-id="ab194-245">SQL 대량 복사</span><span class="sxs-lookup"><span data-stu-id="ab194-245">SQL bulk copy</span></span>
<span data-ttu-id="ab194-246">SQL 대량 복사는 또 다른 방법은 tooinsert 많은 양의 데이터를 대상 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-246">SQL bulk copy is another way tooinsert large amounts of data into a target database.</span></span> <span data-ttu-id="ab194-247">.NET 응용 프로그램에서는 hello **SqlBulkCopy** 클래스 tooperform 대량 삽입 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-247">.NET applications can use hello **SqlBulkCopy** class tooperform bulk insert operations.</span></span> <span data-ttu-id="ab194-248">**SqlBulkCopy** 함수 toohello 명령줄 도구에서 비슷한 **Bcp.exe**, 또는 TRANSACT-SQL 문의 hello **BULK INSERT**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-248">**SqlBulkCopy** is similar in function toohello command-line tool, **Bcp.exe**, or hello Transact-SQL statement, **BULK INSERT**.</span></span> <span data-ttu-id="ab194-249">hello 다음 코드 예제에서는 toobulk 복사 hello hello 소스에서 행을 어떻게 **DataTable**, 테이블, SQL server에서는 MyTable toohello 대상 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-249">hello following code example shows how toobulk copy hello rows in hello source **DataTable**, table, toohello destination table in SQL Server, MyTable.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

<span data-ttu-id="ab194-250">테이블 반환 매개 변수보다 대량 복사를 선호하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-250">There are some cases where bulk copy is preferred over table-valued parameters.</span></span> <span data-ttu-id="ab194-251">BULK INSERT 작업 hello 항목의 테이블 반환 매개 변수 hello 비교 표를 참조 하십시오. [테이블 반환 매개 변수](https://msdn.microsoft.com/library/bb510489.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-251">See hello comparison table of Table-Valued parameters versus BULK INSERT operations in hello topic [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

<span data-ttu-id="ab194-252">hello 다음 임시 테스트 결과 표시 hello 사용한 일괄 처리 성능 **SqlBulkCopy** (밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-252">hello following ad-hoc test results show hello performance of batching with **SqlBulkCopy** in milliseconds.</span></span>

| <span data-ttu-id="ab194-253">작업</span><span class="sxs-lookup"><span data-stu-id="ab194-253">Operations</span></span> | <span data-ttu-id="ab194-254">온-프레미스 tooAzure (ms)</span><span class="sxs-lookup"><span data-stu-id="ab194-254">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="ab194-255">Azure 동일한 데이터 센터(밀리초)</span><span class="sxs-lookup"><span data-stu-id="ab194-255">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ab194-256">1</span><span class="sxs-lookup"><span data-stu-id="ab194-256">1</span></span> |<span data-ttu-id="ab194-257">433</span><span class="sxs-lookup"><span data-stu-id="ab194-257">433</span></span> |<span data-ttu-id="ab194-258">57</span><span class="sxs-lookup"><span data-stu-id="ab194-258">57</span></span> |
| <span data-ttu-id="ab194-259">10</span><span class="sxs-lookup"><span data-stu-id="ab194-259">10</span></span> |<span data-ttu-id="ab194-260">441</span><span class="sxs-lookup"><span data-stu-id="ab194-260">441</span></span> |<span data-ttu-id="ab194-261">32</span><span class="sxs-lookup"><span data-stu-id="ab194-261">32</span></span> |
| <span data-ttu-id="ab194-262">100</span><span class="sxs-lookup"><span data-stu-id="ab194-262">100</span></span> |<span data-ttu-id="ab194-263">636</span><span class="sxs-lookup"><span data-stu-id="ab194-263">636</span></span> |<span data-ttu-id="ab194-264">53</span><span class="sxs-lookup"><span data-stu-id="ab194-264">53</span></span> |
| <span data-ttu-id="ab194-265">1000</span><span class="sxs-lookup"><span data-stu-id="ab194-265">1000</span></span> |<span data-ttu-id="ab194-266">2535</span><span class="sxs-lookup"><span data-stu-id="ab194-266">2535</span></span> |<span data-ttu-id="ab194-267">341</span><span class="sxs-lookup"><span data-stu-id="ab194-267">341</span></span> |
| <span data-ttu-id="ab194-268">10000</span><span class="sxs-lookup"><span data-stu-id="ab194-268">10000</span></span> |<span data-ttu-id="ab194-269">21605</span><span class="sxs-lookup"><span data-stu-id="ab194-269">21605</span></span> |<span data-ttu-id="ab194-270">2737</span><span class="sxs-lookup"><span data-stu-id="ab194-270">2737</span></span> |

> [!NOTE]
> <span data-ttu-id="ab194-271">결과가 기준은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-271">Results are not benchmarks.</span></span> <span data-ttu-id="ab194-272">Hello 참조 [이 항목의 타이밍 결과 대 한 참고](#note-about-timing-results-in-this-topic)합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-272">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="ab194-273">일괄 처리 크기가 작을수록 hello 사용 하 여 테이블 반환 매개 변수는 hello 성능이 **SqlBulkCopy** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-273">In smaller batch sizes, hello use table-valued parameters outperformed hello **SqlBulkCopy** class.</span></span> <span data-ttu-id="ab194-274">그러나 **SqlBulkCopy** 1, 000, 10, 000 행의 hello 테스트에 대 한 12-31% 테이블 반환 매개 변수 보다 더 빠르게 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-274">However, **SqlBulkCopy** performed 12-31% faster than table-valued parameters for hello tests of 1,000 and 10,000 rows.</span></span> <span data-ttu-id="ab194-275">테이블 반환 매개 변수를 같은 **SqlBulkCopy** 특히 비교 했을 때 일괄 처리 삽입을 위해 적합 한 옵션은 일괄 처리 되지 않은 작업의 toohello 성능을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-275">Like table-valued parameters, **SqlBulkCopy** is a good option for batched inserts, especially when compared toohello performance of non-batched operations.</span></span>

<span data-ttu-id="ab194-276">ADO.NET에서 대량 복사에 대한 자세한 내용은 [SQL Server에서의 대량 복사 작업](https://msdn.microsoft.com/library/7ek5da1a.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab194-276">For more information on bulk copy in ADO.NET, see [Bulk Copy Operations in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span></span>

### <a name="multiple-row-parameterized-insert-statements"></a><span data-ttu-id="ab194-277">여러 행의 매개 변수가 있는 INSERT 문</span><span class="sxs-lookup"><span data-stu-id="ab194-277">Multiple-row Parameterized INSERT statements</span></span>
<span data-ttu-id="ab194-278">작은 일괄 처리에 대 한 대안은 tooconstruct 큰 INSERT 문에 여러 행을 삽입 하는 매개 변수가 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-278">One alternative for small batches is tooconstruct a large parameterized INSERT statement that inserts multiple rows.</span></span> <span data-ttu-id="ab194-279">다음 코드 예제는 hello이이 기술을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-279">hello following code example demonstrates this technique.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


<span data-ttu-id="ab194-280">이 예제에서는 tooshow hello에 대 한 기본 개념을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-280">This example is meant tooshow hello basic concept.</span></span> <span data-ttu-id="ab194-281">보다 실제적인 시나리오는 동시에 필요한 hello 엔터티 tooconstruct hello 쿼리 문자열 및 hello 명령 매개 변수를 통해 루프 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-281">A more realistic scenario would loop through hello required entities tooconstruct hello query string and hello command parameters simultaneously.</span></span> <span data-ttu-id="ab194-282">제한 되 지도 tooa 총 2100 쿼리 매개 변수를 이런이 방식으로 처리할 수 있는 행의 총 hello 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-282">You are limited tooa total of 2100 query parameters, so this limits hello total number of rows that can be processed in this manner.</span></span>

<span data-ttu-id="ab194-283">이러한 종류의 insert 문이 밀리초에서의 임시 테스트 결과 표시 hello 성능 다음 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-283">hello following ad-hoc test results show hello performance of this type of insert statement in milliseconds.</span></span>

| <span data-ttu-id="ab194-284">작업</span><span class="sxs-lookup"><span data-stu-id="ab194-284">Operations</span></span> | <span data-ttu-id="ab194-285">테이블 반환 매개 변수(밀리초)</span><span class="sxs-lookup"><span data-stu-id="ab194-285">Table-valued parameters (ms)</span></span> | <span data-ttu-id="ab194-286">단일 문 INSERT(밀리초)</span><span class="sxs-lookup"><span data-stu-id="ab194-286">Single-statement INSERT (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ab194-287">1</span><span class="sxs-lookup"><span data-stu-id="ab194-287">1</span></span> |<span data-ttu-id="ab194-288">32</span><span class="sxs-lookup"><span data-stu-id="ab194-288">32</span></span> |<span data-ttu-id="ab194-289">20</span><span class="sxs-lookup"><span data-stu-id="ab194-289">20</span></span> |
| <span data-ttu-id="ab194-290">10</span><span class="sxs-lookup"><span data-stu-id="ab194-290">10</span></span> |<span data-ttu-id="ab194-291">30</span><span class="sxs-lookup"><span data-stu-id="ab194-291">30</span></span> |<span data-ttu-id="ab194-292">25</span><span class="sxs-lookup"><span data-stu-id="ab194-292">25</span></span> |
| <span data-ttu-id="ab194-293">100</span><span class="sxs-lookup"><span data-stu-id="ab194-293">100</span></span> |<span data-ttu-id="ab194-294">33</span><span class="sxs-lookup"><span data-stu-id="ab194-294">33</span></span> |<span data-ttu-id="ab194-295">51</span><span class="sxs-lookup"><span data-stu-id="ab194-295">51</span></span> |

> [!NOTE]
> <span data-ttu-id="ab194-296">결과가 기준은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-296">Results are not benchmarks.</span></span> <span data-ttu-id="ab194-297">Hello 참조 [이 항목의 타이밍 결과 대 한 참고](#note-about-timing-results-in-this-topic)합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-297">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="ab194-298">이 방법은 행이 100개 미만인 배치에 대해 약간 더 빠를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-298">This approach can be slightly faster for batches that are less than 100 rows.</span></span> <span data-ttu-id="ab194-299">Hello 향상 폭이 작지만, 있지만이 방법은 특정 응용 프로그램 시나리오에서 잘 수 있는 또 다른 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-299">Although hello improvement is small, this technique is another option that might work well in your specific application scenario.</span></span>

### <a name="dataadapter"></a><span data-ttu-id="ab194-300">DataAdapter</span><span class="sxs-lookup"><span data-stu-id="ab194-300">DataAdapter</span></span>
<span data-ttu-id="ab194-301">hello **DataAdapter** 클래스 있습니다 toomodify는 **DataSet** 개체를 삽입, 업데이트 및 삭제 작업으로 hello 변경 전송할 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-301">hello **DataAdapter** class allows you toomodify a **DataSet** object and then submit hello changes as INSERT, UPDATE, and DELETE operations.</span></span> <span data-ttu-id="ab194-302">Hello를 사용 하는 경우 **DataAdapter** 이런 방식으로 반드시 toonote 별도로 호출 하는 각각의 고유 작업에 대해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-302">If you are using hello **DataAdapter** in this manner, it is important toonote that separate calls are made for each distinct operation.</span></span> <span data-ttu-id="ab194-303">tooimprove 성능, 사용 하 여 hello **UpdateBatchSize** 속성 toohello 수가 한 번에 일괄 처리 해야 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-303">tooimprove performance, use hello **UpdateBatchSize** property toohello number of operations that should be batched at a time.</span></span> <span data-ttu-id="ab194-304">자세한 내용은 [DataAdapters를 사용하여 배치 작업 수행](https://msdn.microsoft.com/library/aadf8fk2.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab194-304">For more information, see [Performing Batch Operations Using DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span></span>

### <a name="entity-framework"></a><span data-ttu-id="ab194-305">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="ab194-305">Entity framework</span></span>
<span data-ttu-id="ab194-306">Entity Framework는 현재 일괄 처리를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-306">Entity Framework does not currently support batching.</span></span> <span data-ttu-id="ab194-307">Hello 커뮤니티에서 다른 개발자가 재정의 hello 같은 toodemonstrate 해결 방법을 시도 **SaveChanges** 메서드.</span><span class="sxs-lookup"><span data-stu-id="ab194-307">Different developers in hello community have attempted toodemonstrate workarounds, such as override hello **SaveChanges** method.</span></span> <span data-ttu-id="ab194-308">하지만 hello 솔루션은 일반적으로 복잡 하 고 사용자 지정 된 toohello 응용 프로그램 및 데이터 모델.</span><span class="sxs-lookup"><span data-stu-id="ab194-308">But hello solutions are typically complex and customized toohello application and data model.</span></span> <span data-ttu-id="ab194-309">hello Entity Framework codeplex 프로젝트는이 기능 요청에 대 한 토론 페이지가 현재에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-309">hello Entity Framework codeplex project currently has a discussion page on this feature request.</span></span> <span data-ttu-id="ab194-310">tooview이이 설명에서는 참조 [디자인 회의 노트-2012 년 8 월 2 일](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012)합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-310">tooview this discussion, see [Design Meeting Notes - August 2, 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span></span>

### <a name="xml"></a><span data-ttu-id="ab194-311">XML</span><span class="sxs-lookup"><span data-stu-id="ab194-311">XML</span></span>
<span data-ttu-id="ab194-312">완성도 높이기 위해 XML 일괄 처리 전략에 대 한 중요 한 tootalk 인지 생각 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-312">For completeness, we feel that it is important tootalk about XML as a batching strategy.</span></span> <span data-ttu-id="ab194-313">그러나 XML hello 사용에 다른 방법에 비해 큰 이점이 없으며 및 몇 가지 단점도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-313">However, hello use of XML has no advantages over other methods and several disadvantages.</span></span> <span data-ttu-id="ab194-314">hello 방법은 유사 tootable 반환 매개 변수, 하지만 XML 파일 또는 문자열이 사용자 정의 테이블 대신 tooa 저장 프로시저에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-314">hello approach is similar tootable-valued parameters, but an XML file or string is passed tooa stored procedure instead of a user-defined table.</span></span> <span data-ttu-id="ab194-315">hello 저장 프로시저 hello 저장 프로시저에서 hello 명령을 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-315">hello stored procedure parses hello commands in hello stored procedure.</span></span>

<span data-ttu-id="ab194-316">몇 가지 단점 toothis 접근 방식</span><span class="sxs-lookup"><span data-stu-id="ab194-316">There are several disadvantages toothis approach:</span></span>

* <span data-ttu-id="ab194-317">XML 작업은 번거롭고 오류 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-317">Working with XML can be cumbersome and error prone.</span></span>
* <span data-ttu-id="ab194-318">Hello 데이터베이스의 XML 구문 분석 hello CPU를 많이 사용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-318">Parsing hello XML on hello database can be CPU-intensive.</span></span>
* <span data-ttu-id="ab194-319">대부분의 경우 이 방법은 테이블 반환 매개 변수보다 느립니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-319">In most cases, this method is slower than table-valued parameters.</span></span>

<span data-ttu-id="ab194-320">이러한 이유로, 일괄 처리 쿼리에 대 한 XML의 hello 사용 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-320">For these reasons, hello use of XML for batch queries is not recommended.</span></span>

## <a name="batching-considerations"></a><span data-ttu-id="ab194-321">일괄 처리 고려 사항</span><span class="sxs-lookup"><span data-stu-id="ab194-321">Batching considerations</span></span>
<span data-ttu-id="ab194-322">다음 섹션 hello hello 사용 하 여 SQL 데이터베이스 응용 프로그램에서 일괄 처리에 대 한 자세한 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-322">hello following sections provide more guidance for hello use of batching in SQL Database applications.</span></span>

### <a name="tradeoffs"></a><span data-ttu-id="ab194-323">균형 유지</span><span class="sxs-lookup"><span data-stu-id="ab194-323">Tradeoffs</span></span>
<span data-ttu-id="ab194-324">아키텍처에 따라서 일괄 처리는 성능과 복원력 사이에서 균형을 유지해야 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-324">Depending on your architecture, batching can involve a tradeoff between performance and resiliency.</span></span> <span data-ttu-id="ab194-325">예를 들어 hello 시나리오를 사용자 역할이 예기치 않게 중단 되는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-325">For example, consider hello scenario where your role unexpectedly goes down.</span></span> <span data-ttu-id="ab194-326">한 행의 데이터가 손실 된 경우 hello 영향 제출 되지 않은 행의 큰 일괄 처리의 hello 영향 보다 작습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-326">If you lose one row of data, hello impact is smaller than hello impact of losing a large batch of unsubmitted rows.</span></span> <span data-ttu-id="ab194-327">지정된 된 기간 내에 toohello 데이터베이스를 보내기 전에 행을 버퍼링 할 때에 훨씬 더 위험 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-327">There is a greater risk when you buffer rows before sending them toohello database in a specified time window.</span></span>

<span data-ttu-id="ab194-328">이러한 상충 관계 때문에 해당 하면 일괄 처리 작업의 hello 유형에 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-328">Because of this tradeoff, evaluate hello type of operations that you batch.</span></span> <span data-ttu-id="ab194-329">덜 중요한 데이터는 보다 적극적으로(배치 규모는 더 크게 기간은 더 길게) 일괄 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-329">Batch more aggressively (larger batches and longer time windows) with data that is less critical.</span></span>

### <a name="batch-size"></a><span data-ttu-id="ab194-330">배치 크기</span><span class="sxs-lookup"><span data-stu-id="ab194-330">Batch size</span></span>
<span data-ttu-id="ab194-331">자사의 테스트에 따르면 이점은 toobreaking 큰 일괄 처리가 더 작은 청크로 일반적으로 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-331">In our tests, there was typically no advantage toobreaking large batches into smaller chunks.</span></span> <span data-ttu-id="ab194-332">실제로 이러한 세분화가 큰 배치 하나를 제출하는 것보다 성능을 느리게 하는 결과를 초래하기도 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-332">In fact, this subdivision often resulted in slower performance than submitting a single large batch.</span></span> <span data-ttu-id="ab194-333">예를 들어 tooinsert 1000 개의 행을 원하는 위치 하는 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-333">For example, consider a scenario where you want tooinsert 1000 rows.</span></span> <span data-ttu-id="ab194-334">hello 다음 표에 시간 toouse 테이블 반환 매개 변수를 더 작은 일괄 처리로 나누었을 때 tooinsert 1000 행 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-334">hello following table shows how long it takes toouse table-valued parameters tooinsert 1000 rows when divided into smaller batches.</span></span>

| <span data-ttu-id="ab194-335">배치 크기</span><span class="sxs-lookup"><span data-stu-id="ab194-335">Batch size</span></span> | <span data-ttu-id="ab194-336">반복 횟수</span><span class="sxs-lookup"><span data-stu-id="ab194-336">Iterations</span></span> | <span data-ttu-id="ab194-337">테이블 반환 매개 변수(밀리초)</span><span class="sxs-lookup"><span data-stu-id="ab194-337">Table-valued parameters (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ab194-338">1000</span><span class="sxs-lookup"><span data-stu-id="ab194-338">1000</span></span> |<span data-ttu-id="ab194-339">1</span><span class="sxs-lookup"><span data-stu-id="ab194-339">1</span></span> |<span data-ttu-id="ab194-340">347</span><span class="sxs-lookup"><span data-stu-id="ab194-340">347</span></span> |
| <span data-ttu-id="ab194-341">500</span><span class="sxs-lookup"><span data-stu-id="ab194-341">500</span></span> |<span data-ttu-id="ab194-342">2</span><span class="sxs-lookup"><span data-stu-id="ab194-342">2</span></span> |<span data-ttu-id="ab194-343">355</span><span class="sxs-lookup"><span data-stu-id="ab194-343">355</span></span> |
| <span data-ttu-id="ab194-344">100</span><span class="sxs-lookup"><span data-stu-id="ab194-344">100</span></span> |<span data-ttu-id="ab194-345">10</span><span class="sxs-lookup"><span data-stu-id="ab194-345">10</span></span> |<span data-ttu-id="ab194-346">465</span><span class="sxs-lookup"><span data-stu-id="ab194-346">465</span></span> |
| <span data-ttu-id="ab194-347">50</span><span class="sxs-lookup"><span data-stu-id="ab194-347">50</span></span> |<span data-ttu-id="ab194-348">20</span><span class="sxs-lookup"><span data-stu-id="ab194-348">20</span></span> |<span data-ttu-id="ab194-349">630</span><span class="sxs-lookup"><span data-stu-id="ab194-349">630</span></span> |

> [!NOTE]
> <span data-ttu-id="ab194-350">결과가 기준은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-350">Results are not benchmarks.</span></span> <span data-ttu-id="ab194-351">Hello 참조 [이 항목의 타이밍 결과 대 한 참고](#note-about-timing-results-in-this-topic)합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-351">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="ab194-352">1000 개 행에 대 한 최상의 성능을 hello toosubmit 임을 확인할 수 있습니다 동시에 모두 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-352">You can see that hello best performance for 1000 rows is toosubmit them all at once.</span></span> <span data-ttu-id="ab194-353">(여기 표시 되지 않음) 하는 다른 테스트에서 했습니다 약간의 성능 향상 toobreak 10000 행 일괄 처리를 5000의 두 개의 일괄 처리로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-353">In other tests (not shown here) there was a small performance gain toobreak a 10000 row batch into two batches of 5000.</span></span> <span data-ttu-id="ab194-354">하지만 이러한 테스트에 대 한 hello 테이블 스키마는 비교적 간단 테스트 하 여 수행 해야 하므로 특정 데이터 및 일괄 처리 크기 tooverify이 결과.</span><span class="sxs-lookup"><span data-stu-id="ab194-354">But hello table schema for these tests is relatively simple, so you should perform tests on your specific data and batch sizes tooverify these findings.</span></span>

<span data-ttu-id="ab194-355">다른 요소 tooconsider은 hello 총 일괄 처리가 너무 커지면, SQL 데이터베이스 수 제한 toocommit hello 일괄 처리를 거부 하도록입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-355">Another factor tooconsider is that if hello total batch becomes too large, SQL Database might throttle and refuse toocommit hello batch.</span></span> <span data-ttu-id="ab194-356">최상의 결과 얻으려면 hello에 대 한 이상적인 일괄 처리 크기를 사용 하는 경우 특정 시나리오 toodetermine를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-356">For hello best results, test your specific scenario toodetermine if there is an ideal batch size.</span></span> <span data-ttu-id="ab194-357">성능 또는 오류에 따라 런타임 tooenable 빠르게 조정할에서 구성 가능한 hello 일괄 처리 크기를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-357">Make hello batch size configurable at runtime tooenable quick adjustments based on performance or errors.</span></span>

<span data-ttu-id="ab194-358">마지막으로, 일괄 처리와 관련 된 hello에 위험이 있는 hello hello 일괄 처리 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-358">Finally, balance hello size of hello batch with hello risks associated with batching.</span></span> <span data-ttu-id="ab194-359">일시적인 오류가 않았거나 hello 역할 실패 하면 hello 일괄 처리의 hello 데이터 손실 또는 hello 작업을 다시 시도의 hello 결과 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-359">If there are transient errors or hello role fails, consider hello consequences of retrying hello operation or of losing hello data in hello batch.</span></span>

### <a name="parallel-processing"></a><span data-ttu-id="ab194-360">병렬 처리</span><span class="sxs-lookup"><span data-stu-id="ab194-360">Parallel processing</span></span>
<span data-ttu-id="ab194-361">경우에 어떻게 hello 접근 방식을 hello 일괄 처리 크기를 줄이는 데 걸린 하지만 여러 스레드 tooexecute hello 작업 사용?</span><span class="sxs-lookup"><span data-stu-id="ab194-361">What if you took hello approach of reducing hello batch size but used multiple threads tooexecute hello work?</span></span> <span data-ttu-id="ab194-362">앞서 언급했지만, 테스트에 따르면 여러 개의 소형 다중 스레드 배치는 일반적으로 하나의 대형 배치보다 성능이 낮았습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-362">Again, our tests showed that several smaller multithreaded batches typically performed worse than a single larger batch.</span></span> <span data-ttu-id="ab194-363">hello 다음 테스트에서는 하나 이상의 병렬 일괄 처리에 행이 1000 개 tooinsert 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-363">hello following test attempts tooinsert 1000 rows in one or more parallel batches.</span></span> <span data-ttu-id="ab194-364">이 테스트는 동시에 실행되는 배치가 많아질수록 실제로 성능이 어떻게 감소되는가를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-364">This test shows how more simultaneous batches actually decreased performance.</span></span>

| <span data-ttu-id="ab194-365">배치 크기[반복 횟수]</span><span class="sxs-lookup"><span data-stu-id="ab194-365">Batch size [Iterations]</span></span> | <span data-ttu-id="ab194-366">스레드 2개(밀리초)</span><span class="sxs-lookup"><span data-stu-id="ab194-366">Two threads (ms)</span></span> | <span data-ttu-id="ab194-367">스레드 4개(밀리초)</span><span class="sxs-lookup"><span data-stu-id="ab194-367">Four threads (ms)</span></span> | <span data-ttu-id="ab194-368">스레드 6개(밀리초)</span><span class="sxs-lookup"><span data-stu-id="ab194-368">Six threads (ms)</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ab194-369">1000 [1]</span><span class="sxs-lookup"><span data-stu-id="ab194-369">1000 [1]</span></span> |<span data-ttu-id="ab194-370">277</span><span class="sxs-lookup"><span data-stu-id="ab194-370">277</span></span> |<span data-ttu-id="ab194-371">315</span><span class="sxs-lookup"><span data-stu-id="ab194-371">315</span></span> |<span data-ttu-id="ab194-372">266</span><span class="sxs-lookup"><span data-stu-id="ab194-372">266</span></span> |
| <span data-ttu-id="ab194-373">500 [2]</span><span class="sxs-lookup"><span data-stu-id="ab194-373">500 [2]</span></span> |<span data-ttu-id="ab194-374">548</span><span class="sxs-lookup"><span data-stu-id="ab194-374">548</span></span> |<span data-ttu-id="ab194-375">278</span><span class="sxs-lookup"><span data-stu-id="ab194-375">278</span></span> |<span data-ttu-id="ab194-376">256</span><span class="sxs-lookup"><span data-stu-id="ab194-376">256</span></span> |
| <span data-ttu-id="ab194-377">250 [4]</span><span class="sxs-lookup"><span data-stu-id="ab194-377">250 [4]</span></span> |<span data-ttu-id="ab194-378">405</span><span class="sxs-lookup"><span data-stu-id="ab194-378">405</span></span> |<span data-ttu-id="ab194-379">329</span><span class="sxs-lookup"><span data-stu-id="ab194-379">329</span></span> |<span data-ttu-id="ab194-380">265</span><span class="sxs-lookup"><span data-stu-id="ab194-380">265</span></span> |
| <span data-ttu-id="ab194-381">100 [10]</span><span class="sxs-lookup"><span data-stu-id="ab194-381">100 [10]</span></span> |<span data-ttu-id="ab194-382">488</span><span class="sxs-lookup"><span data-stu-id="ab194-382">488</span></span> |<span data-ttu-id="ab194-383">439</span><span class="sxs-lookup"><span data-stu-id="ab194-383">439</span></span> |<span data-ttu-id="ab194-384">391</span><span class="sxs-lookup"><span data-stu-id="ab194-384">391</span></span> |

> [!NOTE]
> <span data-ttu-id="ab194-385">결과가 기준은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-385">Results are not benchmarks.</span></span> <span data-ttu-id="ab194-386">Hello 참조 [이 항목의 타이밍 결과 대 한 참고](#note-about-timing-results-in-this-topic)합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-386">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="ab194-387">성능 저하 hello에 대 한 잠재적인 다음과 같은 경우 due tooparallelism:</span><span class="sxs-lookup"><span data-stu-id="ab194-387">There are several potential reasons for hello degradation in performance due tooparallelism:</span></span>

* <span data-ttu-id="ab194-388">동시에 실행되는 네트워크 호출이 하나가 아니라 여러 개입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-388">There are multiple simultaneous network calls instead of one.</span></span>
* <span data-ttu-id="ab194-389">단일 테이블에 대해 여러 개의 작업이 수행되면 경합과 차단이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-389">Multiple operations against a single table can result in contention and blocking.</span></span>
* <span data-ttu-id="ab194-390">멀티 스레드와 관련된 오버헤드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-390">There are overheads associated with multithreading.</span></span>
* <span data-ttu-id="ab194-391">hello 비용에 여러 개의 연결을 hello 병렬 처리 이점을 보다 큽니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-391">hello expense of opening multiple connections outweighs hello benefit of parallel processing.</span></span>

<span data-ttu-id="ab194-392">다른 테이블 또는 데이터베이스를 대상 경우 가능한 toosee 일부 성능 향상이 전략입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-392">If you target different tables or databases, it is possible toosee some performance gain with this strategy.</span></span> <span data-ttu-id="ab194-393">데이터베이스 분할 또는 페더레이션은 이런 방법에 대한 시나리오가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-393">Database sharding or federations would be a scenario for this approach.</span></span> <span data-ttu-id="ab194-394">여러 데이터베이스와 경로가 다른 데이터 tooeach 데이터베이스 분할을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-394">Sharding uses multiple databases and routes different data tooeach database.</span></span> <span data-ttu-id="ab194-395">되는 경우 각 작은 일괄 처리 tooa 다른 데이터베이스를 다음 hello 작업을 병렬로 수행 더 효율적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-395">If each small batch is going tooa different database, then performing hello operations in parallel can be more efficient.</span></span> <span data-ttu-id="ab194-396">그러나 hello 성능 향상에 도움이 않습니다 만큼 중요 한 toouse 솔루션의 의사 결정 toouse 데이터베이스 분할에 대 한 hello 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-396">However, hello performance gain is not significant enough toouse as hello basis for a decision toouse database sharding in your solution.</span></span>

<span data-ttu-id="ab194-397">일부 디자인의 경우, 소형 배치의 병렬 실행으로 인해 부하가 걸린 시스템 내에서 요청 처리량이 향상되기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-397">In some designs, parallel execution of smaller batches can result in improved throughput of requests in a system under load.</span></span> <span data-ttu-id="ab194-398">이 경우 더 빠른 tooprocess 하나의 큰 일괄 처리 인 경우에 동시에 여러 개의 일괄 처리 더 효율적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-398">In this case, even though it is quicker tooprocess a single larger batch, processing multiple batches in parallel might be more efficient.</span></span>

<span data-ttu-id="ab194-399">병렬 실행을 사용할 경우 제어 hello 최대 작업자 스레드 수를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-399">If you do use parallel execution, consider controlling hello maximum number of worker threads.</span></span> <span data-ttu-id="ab194-400">숫자가 작을수록 경합이 줄어들고 실행 시간은 빨라집니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-400">A smaller number might result in less contention and a faster execution time.</span></span> <span data-ttu-id="ab194-401">또한, 이렇게 하면 hello 대상 데이터베이스 연결 및 트랜잭션 모두에 hello 추가 부하를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-401">Also, consider hello additional load that this places on hello target database both in connections and transactions.</span></span>

### <a name="related-performance-factors"></a><span data-ttu-id="ab194-402">관련된 성능 요인</span><span class="sxs-lookup"><span data-stu-id="ab194-402">Related performance factors</span></span>
<span data-ttu-id="ab194-403">데이터 베이스 성능에 대한 전형적인 지침은 일괄 처리에도 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-403">Typical guidance on database performance also affects batching.</span></span> <span data-ttu-id="ab194-404">예를 들어, 기본 키가 크거나 비클러스터형 인덱스가 많은 테이블에 대한 삽입 성능은 감소됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-404">For example, insert performance is reduced for tables that have a large primary key or many nonclustered indexes.</span></span>

<span data-ttu-id="ab194-405">테이블 반환 매개 변수는 저장된 프로시저를 사용 하는 경우에 hello 명령을 사용할 수 **SET NOCOUNT ON** hello 프로시저의 hello 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-405">If table-valued parameters use a stored procedure, you can use hello command **SET NOCOUNT ON** at hello beginning of hello procedure.</span></span> <span data-ttu-id="ab194-406">이 문은 hello hello hello 절차의 hello 영향을 받는 행 수를 반환을 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-406">This statement suppresses hello return of hello count of hello affected rows in hello procedure.</span></span> <span data-ttu-id="ab194-407">그러나이 테스트에서 사용 하 여 hello **SET NOCOUNT ON** 성능이 저하 또는 영향을 주지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-407">However, in our tests, hello use of **SET NOCOUNT ON** either had no effect or decreased performance.</span></span> <span data-ttu-id="ab194-408">hello 테스트 저장 프로시저는 간단한 형태 였습니다 단일 **삽입** hello 테이블 반환 매개 변수에서 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-408">hello test stored procedure was simple with a single **INSERT** command from hello table-valued parameter.</span></span> <span data-ttu-id="ab194-409">이 명령문은 더 복잡한 저장 프로시저에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-409">It is possible that more complex stored procedures would benefit from this statement.</span></span> <span data-ttu-id="ab194-410">하지만 추가 가정 하지 마십시오 **SET NOCOUNT ON** tooyour 저장 프로시저에는 자동으로 성능이 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-410">But don’t assume that adding **SET NOCOUNT ON** tooyour stored procedure automatically improves performance.</span></span> <span data-ttu-id="ab194-411">toounderstand 효과 hello, 저장된 프로시저를와 hello 없는 테스트 **SET NOCOUNT ON** 문.</span><span class="sxs-lookup"><span data-stu-id="ab194-411">toounderstand hello effect, test your stored procedure with and without hello **SET NOCOUNT ON** statement.</span></span>

## <a name="batching-scenarios"></a><span data-ttu-id="ab194-412">일괄 처리 시나리오</span><span class="sxs-lookup"><span data-stu-id="ab194-412">Batching scenarios</span></span>
<span data-ttu-id="ab194-413">hello 다음 섹션에서는 설명 방법을 세 개의 응용 프로그램 시나리오에서 테이블 반환 매개 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-413">hello following sections describe how toouse table-valued parameters in three application scenarios.</span></span> <span data-ttu-id="ab194-414">hello 첫 번째 시나리오에서는 버퍼링 및 일괄 처리 수 연동 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-414">hello first scenario shows how buffering and batching can work together.</span></span> <span data-ttu-id="ab194-415">hello 두 번째 시나리오에는 단일 저장된 프로시저 호출에서 마스터-세부 작업을 수행 하 여 성능이 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-415">hello second scenario improves performance by performing master-detail operations in a single stored procedure call.</span></span> <span data-ttu-id="ab194-416">마지막 시나리오에서는 hello 방법을 toouse 테이블 반환 매개 변수는 "UPSERT" 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-416">hello final scenario shows how toouse table-valued parameters in an “UPSERT” operation.</span></span>

### <a name="buffering"></a><span data-ttu-id="ab194-417">버퍼링</span><span class="sxs-lookup"><span data-stu-id="ab194-417">Buffering</span></span>
<span data-ttu-id="ab194-418">일괄 처리가 확실히 적합할 만한 시나리오가 있기는 하지만 지연 처리를 통한 일괄 처리를 활용할 수 있는 시나리오는 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-418">Although there are some scenarios that are obvious candidate for batching, there are many scenarios that could take advantage of batching by delayed processing.</span></span> <span data-ttu-id="ab194-419">그러나 지연 된 처리도 예기치 않은 오류의 hello 이벤트 시 hello 데이터가 손실 더 큰 위험을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-419">However, delayed processing also carries a greater risk that hello data is lost in hello event of an unexpected failure.</span></span> <span data-ttu-id="ab194-420">중요 한 toounderstand이이 위험 이며 hello 결과 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-420">It is important toounderstand this risk and consider hello consequences.</span></span>

<span data-ttu-id="ab194-421">각 사용자의 hello 탐색 기록을 추적 하는 웹 응용 프로그램을 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-421">For example, consider a web application that tracks hello navigation history of each user.</span></span> <span data-ttu-id="ab194-422">각 페이지 요청에 hello 응용 프로그램 데이터베이스 호출 toorecord hello 사용자의 페이지 보기를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-422">On each page request, hello application could make a database call toorecord hello user’s page view.</span></span> <span data-ttu-id="ab194-423">하지만 더 높은 성능과 확장성 hello 사용자의 탐색 활동 버퍼링 및 일괄 처리에이 데이터 toohello 데이터베이스를 보내는 여 실현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-423">But higher performance and scalability can be achieved by buffering hello users’ navigation activities and then sending this data toohello database in batches.</span></span> <span data-ttu-id="ab194-424">경과 된 시간 및/또는 버퍼 크기에 따라 hello 데이터베이스 업데이트를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-424">You can trigger hello database update by elapsed time and/or buffer size.</span></span> <span data-ttu-id="ab194-425">예를 들어 20 초 또는 hello 버퍼 항목 수가 1000 개일 때 후 처리 되어야 해당 hello 일괄 처리 규칙을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-425">For example, a rule could specify that hello batch should be processed after 20 seconds or when hello buffer reaches 1000 items.</span></span>

<span data-ttu-id="ab194-426">hello 다음 코드 예제에서는 [Reactive Extensions-Rx](https://msdn.microsoft.com/data/gg577609) tooprocess 모니터링 클래스에 의해 발생 한 이벤트를 버퍼링 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-426">hello following code example uses [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess buffered events raised by a monitoring class.</span></span> <span data-ttu-id="ab194-427">버퍼가 가득 찰 경우 hello 또는 시간 제한에 도달 하면, 사용자 데이터의 hello 일괄 처리가 테이블 반환 매개 변수를 사용 하 여 toohello 데이터베이스에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-427">When hello buffer fills or a timeout is reached, hello batch of user data is sent toohello database with a table-valued parameter.</span></span>

<span data-ttu-id="ab194-428">hello 다음 NavHistoryData 클래스 모델 hello 사용자 탐색 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-428">hello following NavHistoryData class models hello user navigation details.</span></span> <span data-ttu-id="ab194-429">Hello 사용자 식별자와 같은 기본 정보를 포함, hello URL에 액세스 하 고 hello 액세스 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-429">It contains basic information such as hello user identifier, hello URL accessed, and hello access time.</span></span>

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

<span data-ttu-id="ab194-430">hello NavHistoryDataMonitor 클래스는 hello 사용자 탐색 데이터 toohello 데이터베이스를 버퍼링 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-430">hello NavHistoryDataMonitor class is responsible for buffering hello user navigation data toohello database.</span></span> <span data-ttu-id="ab194-431">**OnAdded** 이벤트가 발생하면 응답하는RecordUserNavigationEntry라는 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-431">It contains a method, RecordUserNavigationEntry, which responds by raising an **OnAdded** event.</span></span> <span data-ttu-id="ab194-432">hello 다음 코드에서는 Rx toocreate를 사용 하는 hello 생성자 논리 hello 이벤트를 기준으로 observable 컬렉션</span><span class="sxs-lookup"><span data-stu-id="ab194-432">hello following code shows hello constructor logic that uses Rx toocreate an observable collection based on hello event.</span></span> <span data-ttu-id="ab194-433">그런 다음 hello 버퍼 메서드로 toothis observable 컬렉션을 구독합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-433">It then subscribes toothis observable collection with hello Buffer method.</span></span> <span data-ttu-id="ab194-434">hello 오버 로드는 20 초 마다 또는 1000 개 항목 해당 hello 버퍼를 전송 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-434">hello overload specifies that hello buffer should be sent every 20 seconds or 1000 entries.</span></span>

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

<span data-ttu-id="ab194-435">hello 버퍼링 된 항목의 모든 테이블 반환 형식으로 변환 하 고 해당 프로세스 hello 일괄 처리가 형식 tooa 저장 프로시저를 전달 하는 hello 처리기 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-435">hello handler converts all of hello buffered items into a table-valued type and then passes this type tooa stored procedure that processes hello batch.</span></span> <span data-ttu-id="ab194-436">hello 다음 코드에서는 hello NavHistoryDataEventArgs hello와 hello NavHistoryDataMonitor 클래스에 대 한 완료 정의</span><span class="sxs-lookup"><span data-stu-id="ab194-436">hello following code shows hello complete definition for both hello NavHistoryDataEventArgs and hello NavHistoryDataMonitor classes.</span></span>

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

<span data-ttu-id="ab194-437">toouse이 버퍼링 클래스 hello 응용 프로그램에 정적 NavHistoryDataMonitor 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-437">toouse this buffering class, hello application creates a static NavHistoryDataMonitor object.</span></span> <span data-ttu-id="ab194-438">사용자가 페이지에 액세스할 때마다 hello 응용 프로그램 hello NavHistoryDataMonitor.RecordUserNavigationEntry 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-438">Each time a user accesses a page, hello application calls hello NavHistoryDataMonitor.RecordUserNavigationEntry method.</span></span> <span data-ttu-id="ab194-439">버퍼링 논리 hello 이러한 항목 toohello 데이터베이스 일괄 처리로 보내는 care of tootake 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-439">hello buffering logic proceeds tootake care of sending these entries toohello database in batches.</span></span>

### <a name="master-detail"></a><span data-ttu-id="ab194-440">마스터-세부 정보</span><span class="sxs-lookup"><span data-stu-id="ab194-440">Master detail</span></span>
<span data-ttu-id="ab194-441">테이블 반환 매개 변수는 간단한 INSERT 시나리오에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-441">Table-valued parameters are useful for simple INSERT scenarios.</span></span> <span data-ttu-id="ab194-442">그러나 테이블이 하나 이상 포함 된 가장 까다로운 toobatch 삽입이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-442">However, it can be more challenging toobatch inserts that involve more than one table.</span></span> <span data-ttu-id="ab194-443">hello "마스터/세부" 시나리오는 좋은 예입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-443">hello “master/detail” scenario is a good example.</span></span> <span data-ttu-id="ab194-444">hello 마스터 테이블 hello 주 엔터티를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-444">hello master table identifies hello primary entity.</span></span> <span data-ttu-id="ab194-445">하나 이상의 세부 테이블 hello 엔터티에 대 한 더 많은 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-445">One or more detail tables store more data about hello entity.</span></span> <span data-ttu-id="ab194-446">이 시나리오에서는 외래 키 관계의 세부 정보 tooa 고유 마스터 엔터티에 hello 관계를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-446">In this scenario, foreign key relationships enforce hello relationship of details tooa unique master entity.</span></span> <span data-ttu-id="ab194-447">PurchaseOrder 테이블의 간소화된 버전 및 그와 연결된 OrderDetail 테이블을 생각해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-447">Consider a simplified version of a PurchaseOrder table and its associated OrderDetail table.</span></span> <span data-ttu-id="ab194-448">다음 TRANSACT-SQL hello 4 개의 열이 있는 hello PurchaseOrder 테이블을 만듭니다: 주문 Id, 주문 날짜, CustomerID 및 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-448">hello following Transact-SQL creates hello PurchaseOrder table with four columns: OrderID, OrderDate, CustomerID, and Status.</span></span>

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

<span data-ttu-id="ab194-449">각각의 주문은 하나 이상의 제품 구매를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-449">Each order contains one or more product purchases.</span></span> <span data-ttu-id="ab194-450">이 정보는 hello PurchaseOrderDetail 테이블에서 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-450">This information is captured in hello PurchaseOrderDetail table.</span></span> <span data-ttu-id="ab194-451">다음 TRANSACT-SQL hello 5 개의 열이 있는 hello PurchaseOrderDetail 테이블을 만듭니다: OrderID, OrderDetailID, ProductID, UnitPrice, 및 OrderQty 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-451">hello following Transact-SQL creates hello PurchaseOrderDetail table with five columns: OrderID, OrderDetailID, ProductID, UnitPrice, and OrderQty.</span></span>

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

<span data-ttu-id="ab194-452">hello PurchaseOrderDetail 테이블의 OrderID 열 hello hello PurchaseOrder 테이블에서 주문을 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-452">hello OrderID column in hello PurchaseOrderDetail table must reference an order from hello PurchaseOrder table.</span></span> <span data-ttu-id="ab194-453">외래 키의 정의 다음 hello이 제약이 조건을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-453">hello following definition of a foreign key enforces this constraint.</span></span>

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

<span data-ttu-id="ab194-454">순서 toouse 테이블 반환 매개 변수에서 각 대상 테이블에 대 한 하나의 사용자 정의 테이블 형식이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-454">In order toouse table-valued parameters, you must have one user-defined table type for each target table.</span></span>

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

<span data-ttu-id="ab194-455">그 후 이런 형식의 테이블을 허용하는 저장 프로시저를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-455">Then define a stored procedure that accepts tables of these types.</span></span> <span data-ttu-id="ab194-456">이 절차를 사용 하면 응용 프로그램 toolocally 일괄 일련의 주문 및 주문 세부 정보 한 번의 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-456">This procedure allows an application toolocally batch a set of orders and order details in a single call.</span></span> <span data-ttu-id="ab194-457">hello 다음 TRANSACT-SQL hello 완전 한 저장된 프로시저 선언을 제공이 구매 주문 예제에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-457">hello following Transact-SQL provides hello complete stored procedure declaration for this purchase order example.</span></span>

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects hello order identifiers in hello @orders
    -- table with hello actual order identifiers in hello PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders toohello PurchaseOrder table, storing hello actual
    -- order identifiers in hello @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match hello passed-in order identifiers with hello actual identifiers
    -- and complete hello @IdentityLink table for use with inserting hello details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert hello order details into hello PurchaseOrderDetail table, 
          -- using hello actual order identifiers of hello master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

<span data-ttu-id="ab194-458">이 예제에서는 로컬에서 정의 된 hello @IdentityLink 테이블 hello hello 새로 삽입 된 행의 실제 OrderID 값을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-458">In this example, hello locally defined @IdentityLink table stores hello actual OrderID values from hello newly inserted rows.</span></span> <span data-ttu-id="ab194-459">이러한 주문 식별자는 hello에 hello 임시 OrderID 값과 다를 @orders 및 @details 테이블 반환 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-459">These order identifiers are different from hello temporary OrderID values in hello @orders and @details table-valued parameters.</span></span> <span data-ttu-id="ab194-460">이러한 이유로 hello @IdentityLink 연결한 후 hello OrderID 값 테이블에서 hello @orders hello hello PurchaseOrder 테이블에 새 행에 대 한 매개 변수 toohello 실제 OrderID 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-460">For this reason, hello @IdentityLink table then connects hello OrderID values from hello @orders parameter toohello real OrderID values for hello new rows in hello PurchaseOrder table.</span></span> <span data-ttu-id="ab194-461">이 단계를 hello @IdentityLink 테이블 삽입 hello orderdetails hello로으로 기여할 수 hello 외래 키 제약 조건을 만족 하는 실제 OrderID 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-461">After this step, hello @IdentityLink table can facilitate inserting hello order details with hello actual OrderID that satisfies hello foreign key constraint.</span></span>

<span data-ttu-id="ab194-462">저장된 프로시저는 코드 또는 기타 Transact-SQL 호출에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-462">This stored procedure can be used from code or from other Transact-SQL calls.</span></span> <span data-ttu-id="ab194-463">코드 예제를 보려면이 문서의 hello 테이블 반환 매개 변수 섹션을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ab194-463">See hello table-valued parameters section of this paper for a code example.</span></span> <span data-ttu-id="ab194-464">다음 TRANSACT-SQL hello toocall sp_InsertOrdersBatch hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-464">hello following Transact-SQL shows how toocall hello sp_InsertOrdersBatch.</span></span>

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

<span data-ttu-id="ab194-465">이 솔루션을 사용 하면 각 일괄 처리 toouse 1부터 시작 하는 주문 Id 값의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-465">This solution allows each batch toouse a set of OrderID values that begin at 1.</span></span> <span data-ttu-id="ab194-466">이러한 임시 OrderID 값 hello 일괄 처리의 hello 관계를 설명 하지만 실제 OrderID 값 hello hello 삽입 작업의 hello 시 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-466">These temporary OrderID values describe hello relationships in hello batch, but hello actual OrderID values are determined at hello time of hello insert operation.</span></span> <span data-ttu-id="ab194-467">Hello 동일한 문을 hello 이전 예제에서 반복 해 서 실행할 수 있으며 hello 데이터베이스에서 고유한 순서를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-467">You can run hello same statements in hello previous example repeatedly and generate unique orders in hello database.</span></span> <span data-ttu-id="ab194-468">이런 이유 때문에 일괄 처리 기법을 사용할 때는 중복 주문을 방지하는 코드 또는 데이터베이스 논리를 더 추가하는 것을 고려하는 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-468">For this reason, consider adding more code or database logic that prevents duplicate orders when using this batching technique.</span></span>

<span data-ttu-id="ab194-469">이 예제는 훨씬 더 복잡한 데이터베이스 작업(예: 마스터-세부 정보 작업)도 테이블 반환 매개 변수를 사용하여 일괄 처리가 가능하다는 것을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-469">This example demonstrates that even more complex database operations, such as master-detail operations, can be batched using table-valued parameters.</span></span>

### <a name="upsert"></a><span data-ttu-id="ab194-470">UPSERT</span><span class="sxs-lookup"><span data-stu-id="ab194-470">UPSERT</span></span>
<span data-ttu-id="ab194-471">다른 일괄 작업 시나리오는 동시에 기존 행을 업데이트하고 새 행을 삽입하는 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-471">Another batching scenario involves simultaneously updating existing rows and inserting new rows.</span></span> <span data-ttu-id="ab194-472">이 작업은 경우에 따라 참조 tooas "UPSERT" (update + insert) 작업이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-472">This operation is sometimes referred tooas an “UPSERT” (update + insert) operation.</span></span> <span data-ttu-id="ab194-473">별도 호출이 tooINSERT 및 업데이트를 수행 하는 대신 hello MERGE 문이 가장 적합 한 toothis 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-473">Rather than making separate calls tooINSERT and UPDATE, hello MERGE statement is best suited toothis task.</span></span> <span data-ttu-id="ab194-474">MERGE 문의 hello 업데이트 작업을 한 번만 호출 및 두 삽입을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-474">hello MERGE statement can perform both insert and update operations in a single call.</span></span>

<span data-ttu-id="ab194-475">Hello MERGE 문 tooperform 업데이트 및 삽입 테이블 반환 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-475">Table-valued parameters can be used with hello MERGE statement tooperform updates and inserts.</span></span> <span data-ttu-id="ab194-476">예를 들어 hello 다음 열을 포함 하는 간소화 된 직원 테이블: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span><span class="sxs-lookup"><span data-stu-id="ab194-476">For example, consider a simplified Employee table that contains hello following columns: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span></span>

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

<span data-ttu-id="ab194-477">이 예제에서는 해당 hello SocialSecurityNumber 고유 tooperform 여러 직원의 병합은 hello 팩트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-477">In this example, you can use hello fact that hello SocialSecurityNumber is unique tooperform a MERGE of multiple employees.</span></span> <span data-ttu-id="ab194-478">첫째, hello 사용자 정의 테이블 형식을 만들려면</span><span class="sxs-lookup"><span data-stu-id="ab194-478">First, create hello user-defined table type:</span></span>

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

<span data-ttu-id="ab194-479">저장된 프로시저를 만든 다음에 사용 하 여 MERGE 문의 tooperform hello 업데이트 hello 및이 삽입 하는 코드를 작성 하거나 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-479">Next, create a stored procedure or write code that uses hello MERGE statement tooperform hello update and insert.</span></span> <span data-ttu-id="ab194-480">hello 다음 예제에서는 문을 사용 하 여 hello 병합 테이블 반환 매개 변수에서 @employees, EmployeeTableType 형식의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-480">hello following example uses hello MERGE statement on a table-valued parameter, @employees, of type EmployeeTableType.</span></span> <span data-ttu-id="ab194-481">hello의 내용을 hello @employees 테이블 여기 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-481">hello contents of hello @employees table are not shown here.</span></span>

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

<span data-ttu-id="ab194-482">자세한 내용은 hello 설명서 및 MERGE 문의 hello에 대 한 예제를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ab194-482">For more information, see hello documentation and examples for hello MERGE statement.</span></span> <span data-ttu-id="ab194-483">여러 단계에서 동일한 작업을 수행할 수는 hello 저장 되지만 별도 삽입 및 업데이트 작업을 사용 하 여 프로시저 호출, hello MERGE 문이 보다 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-483">Although hello same work could be performed in a multiple-step stored procedure call with separate INSERT and UPDATE operations, hello MERGE statement is more efficient.</span></span> <span data-ttu-id="ab194-484">데이터베이스 코드는 INSERT 및 UPDATE에 대 한 데이터베이스에 대 한 두 호출을 받지 않고 직접 hello MERGE 문을 사용 하는 TRANSACT-SQL 호출을 만들 수도 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-484">Database code can also construct Transact-SQL calls that use hello MERGE statement directly without requiring two database calls for INSERT and UPDATE.</span></span>

## <a name="recommendation-summary"></a><span data-ttu-id="ab194-485">권장 사항 요약</span><span class="sxs-lookup"><span data-stu-id="ab194-485">Recommendation summary</span></span>
<span data-ttu-id="ab194-486">hello 다음 목록은이 항목에서 설명 하는 권장 사항을 일괄 처리 하는 hello에 대 한 요약:</span><span class="sxs-lookup"><span data-stu-id="ab194-486">hello following list provides a summary of hello batching recommendations discussed in this topic:</span></span>

* <span data-ttu-id="ab194-487">버퍼링 및 SQL 데이터베이스 응용 프로그램의 tooincrease hello 성능 및 확장성을 일괄 처리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-487">Use buffering and batching tooincrease hello performance and scalability of SQL Database applications.</span></span>
* <span data-ttu-id="ab194-488">일괄 처리/버퍼링 및 탄력성 사이의 hello 장단점을 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-488">Understand hello tradeoffs between batching/buffering and resiliency.</span></span> <span data-ttu-id="ab194-489">역할 오류 시 hello 손실 될 위험을 일괄 처리 하는 처리 되지 않은 비즈니스에 중요 한 데이터의 일괄 처리의 hello 성능 이점 보다 클 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-489">During a role failure, hello risk of losing an unprocessed batch of business-critical data might outweigh hello performance benefit of batching.</span></span>
* <span data-ttu-id="ab194-490">단일 데이터 센터 tooreduce 대기 시간 내에 있는 모든 호출 toohello 데이터베이스 tookeep를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-490">Attempt tookeep all calls toohello database within a single datacenter tooreduce latency.</span></span>
* <span data-ttu-id="ab194-491">단일 일괄 처리 기법을 선택 하면 테이블 반환 매개 변수 hello 최상의 성능 및 유연성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-491">If you choose a single batching technique, table-valued parameters offer hello best performance and flexibility.</span></span>
* <span data-ttu-id="ab194-492">가장 빠른 hello에 대 한 삽입 성능 같은 일반적인 지침 따르지만 시나리오 테스트 하 여:</span><span class="sxs-lookup"><span data-stu-id="ab194-492">For hello fastest insert performance, follow these general guidelines but test your scenario:</span></span>
  * <span data-ttu-id="ab194-493">행이 100개 미만이면 단일 매개 변수가 있는 INSERT 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-493">For < 100 rows, use a single parameterized INSERT command.</span></span>
  * <span data-ttu-id="ab194-494">행이 1000개 미만이면 테이블 반환 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-494">For < 1000 rows, use table-valued parameters.</span></span>
  * <span data-ttu-id="ab194-495">행이 1000개 이상이면 SqlBulkCopy를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-495">For >= 1000 rows, use SqlBulkCopy.</span></span>
* <span data-ttu-id="ab194-496">에 대 한 업데이트 및 삭제 작업, hello hello 테이블 매개 변수에서 각 행에서 올바른 동작을 결정 하는 저장된 프로시저 논리와 테이블 반환 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-496">For update and delete operations, use table-valued parameters with stored procedure logic that determines hello correct operation on each row in hello table parameter.</span></span>
* <span data-ttu-id="ab194-497">배치 크기 지침:</span><span class="sxs-lookup"><span data-stu-id="ab194-497">Batch size guidelines:</span></span>
  * <span data-ttu-id="ab194-498">응용 프로그램 및 비즈니스 요구 사항에 대 한 의미 있는 hello 가장 큰 일괄 처리 크기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-498">Use hello largest batch sizes that make sense for your application and business requirements.</span></span>
  * <span data-ttu-id="ab194-499">큰 일괄 처리는 임시 또는 치명적인 오류가의 hello에 위험이 있는 균형 hello 성능의 향상.</span><span class="sxs-lookup"><span data-stu-id="ab194-499">Balance hello performance gain of large batches with hello risks of temporary or catastrophic failures.</span></span> <span data-ttu-id="ab194-500">다시 시도의 결과 hello 또는 hello 일괄 처리의 hello 데이터의 손실을 란?</span><span class="sxs-lookup"><span data-stu-id="ab194-500">What is hello consequence of retries or loss of hello data in hello batch?</span></span> 
  * <span data-ttu-id="ab194-501">Hello 가장 큰 일괄 처리 크기 tooverify는 SQL 데이터베이스에서 거부 되지를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-501">Test hello largest batch size tooverify that SQL Database does not reject it.</span></span>
  * <span data-ttu-id="ab194-502">해당 일괄 처리를 제어 hello 일괄 처리 크기 또는 hello 버퍼링 시간과 같은 구성 설정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-502">Create configuration settings that control batching, such as hello batch size or hello buffering time window.</span></span> <span data-ttu-id="ab194-503">이러한 설정은 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-503">These settings provide flexibility.</span></span> <span data-ttu-id="ab194-504">Hello hello 클라우드 서비스를 다시 배포 하지 않고 일괄 처리 되는 프로덕션 환경에서 동작을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-504">You can change hello batching behavior in production without redeploying hello cloud service.</span></span>
* <span data-ttu-id="ab194-505">단일 데이터베이스의 단일 테이블에서 작동하는 배치를 병렬로 실행하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-505">Avoid parallel execution of batches that operate on a single table in one database.</span></span> <span data-ttu-id="ab194-506">여러 작업자 스레드에 대해 단일 일괄 처리 toodivide를 선택 않으면, 테스트 toodetermine hello 스레드의 이상적인 개수를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-506">If you do choose toodivide a single batch across multiple worker threads, run tests toodetermine hello ideal number of threads.</span></span> <span data-ttu-id="ab194-507">스레드가 지정되지 않으면 더 많은 스레드가 성능을 높이기 보다는 감소시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-507">After an unspecified threshold, more threads will decrease performance rather than increase it.</span></span>
* <span data-ttu-id="ab194-508">보다 많은 시나리오에 일괄 처리를 구현하는 방법으로 크기 및 시간에 따른 버퍼링을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-508">Consider buffering on size and time as a way of implementing batching for more scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab194-509">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ab194-509">Next steps</span></span>
<span data-ttu-id="ab194-510">데이터베이스 디자인과 코딩 방법을 toobatching와 관련 된 초점을이 문서에는 응용 프로그램 성능 및 확장성 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-510">This article focused on how database design and coding techniques related toobatching can improve your application performance and scalability.</span></span> <span data-ttu-id="ab194-511">하지만 이것은 사용자의 전반적인 전략 중 한 가지 요소에 불과합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-511">But this is just one factor in your overall strategy.</span></span> <span data-ttu-id="ab194-512">자세한 방법으로 tooimprove 성능 및 확장성에 대 한 참조 [단일 데이터베이스에 대 한 Azure SQL 데이터베이스 성능 지침](sql-database-performance-guidance.md) 및 [탄력적 풀의 가격 및 성능 고려 사항은](sql-database-elastic-pool-guidance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ab194-512">For more ways tooimprove performance and scalability, see [Azure SQL Database performance guidance for single databases](sql-database-performance-guidance.md) and [Price and performance considerations for an elastic pool](sql-database-elastic-pool-guidance.md).</span></span>


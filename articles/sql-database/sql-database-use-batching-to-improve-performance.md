---
title: "Azure SQL 데이터베이스 응용 프로그램 성능을 개선하기 위해 일괄 처리를 사용하는 방법"
description: "이 문서는 데이터베이스 작업을 일괄 처리하면 Azure SQL 데이터베이스 응용 프로그램의 속도와 확장성이 매우 향상된다는 증거를 제공합니다. 이러한 일괄 처리 기법은 SQL Server 데이터베이스에 적용되지만 이 문서는 Azure에 중점을 두었습니다."
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
ms.openlocfilehash: 22cff47444306e599325ba3035d83a0266d69c72
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-batching-to-improve-sql-database-application-performance"></a><span data-ttu-id="97901-104">SQL 데이터베이스 응용 프로그램 성능을 개선하기 위해 일괄 처리를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="97901-104">How to use batching to improve SQL Database application performance</span></span>
<span data-ttu-id="97901-105">Azure SQL 데이터베이스에 대한 일괄 처리 작업은 응용 프로그램의 성능 및 확장성을 상당히 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="97901-105">Batching operations to Azure SQL Database significantly improves the performance and scalability of your applications.</span></span> <span data-ttu-id="97901-106">장점을 이해할 수 있도록, 이 문서의 첫 번째 부분에서는 SQL 데이터베이스에 대한 순차적인 요청과 일괄 처리된 요청을 비교하는 샘플 테스트 결과를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-106">In order to understand the benefits, the first part of this article covers some sample test results that compare sequential and batched requests to a SQL Database.</span></span> <span data-ttu-id="97901-107">문서의 나머지 부분은 Azure 응용 프로그램에서 일괄 처리를 성공적으로 사용하는데 도움이 되는 기법, 시나리오, 고려 사항을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="97901-107">The remainder of the article shows the techniques, scenarios, and considerations to help you to use batching successfully in your Azure applications.</span></span>

## <a name="why-is-batching-important-for-sql-database"></a><span data-ttu-id="97901-108">SQL 데이터베이스에 일괄 처리가 중요한 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="97901-108">Why is batching important for SQL Database?</span></span>
<span data-ttu-id="97901-109">원격 서비스에 대한 호출 일괄 처리는 성능 및 확장성 향상을 위해 잘 알려진 전략입니다.</span><span class="sxs-lookup"><span data-stu-id="97901-109">Batching calls to a remote service is a well-known strategy for increasing performance and scalability.</span></span> <span data-ttu-id="97901-110">직렬화, 네트워크 전송, 역직렬화 같은 원격 서비스와의 모든 트랜잭션에는 고정 처리 비용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-110">There are fixed processing costs to any interactions with a remote service, such as serialization, network transfer, and deserialization.</span></span> <span data-ttu-id="97901-111">다수의 분리된 트랜잭션을 하나의 배치로 패키징하면 이러한 비용이 최소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="97901-111">Packaging many separate transactions into a single batch minimizes these costs.</span></span>

<span data-ttu-id="97901-112">이 문서에서는 다양한 SQL 데이터베이스 일괄 처리 전략 및 시나리오를 살펴보려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-112">In this paper, we want to examine various SQL Database batching strategies and scenarios.</span></span> <span data-ttu-id="97901-113">이러한 전략은 SQL Server를 사용하는 온-프레미스 응용 프로그램에도 중요하지만 SQL 데이터베이스에 대한 일괄 처리 사용을 강조하는 이유가 몇 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-113">Although these strategies are also important for on-premises applications that use SQL Server, there are several reasons for highlighting the use of batching for SQL Database:</span></span>

* <span data-ttu-id="97901-114">SQL 데이터베이스 액세스는 잠재적으로 네트워크 대기 시간이 길고, 동일한 Microsoft Azure 데이터 센터의 외부에서 SQL 데이터베이스에 액세스하는 경우에는 특히 대기 시간이 깁니다.</span><span class="sxs-lookup"><span data-stu-id="97901-114">There is potentially greater network latency in accessing SQL Database, especially if you are accessing SQL Database from outside the same Microsoft Azure datacenter.</span></span>
* <span data-ttu-id="97901-115">SQL 데이터베이스의 다중 테넌트 특징은 데이터 액세스 계층의 효율이 데이터베이스의 전반적인 확장성과 상관 관계가 있다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-115">The multitenant characteristics of SQL Database means that the efficiency of the data access layer correlates to the overall scalability of the database.</span></span> <span data-ttu-id="97901-116">SQL 데이터베이스는 단일 테넌트/사용자가 데이터베이스 리소스를 독점하여 다른 테넌트에 손해를 주지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-116">SQL Database must prevent any single tenant/user from monopolizing database resources to the detriment of other tenants.</span></span> <span data-ttu-id="97901-117">미리 정의된 할당량을 초과하는 사용량에 대해 SQL 데이터베이스는 처리량을 낮추거나 제한 예외로 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-117">In response to usage in excess of predefined quotas, SQL Database can reduce throughput or respond with throttling exceptions.</span></span> <span data-ttu-id="97901-118">일괄 처리와 같은 효율성은 이러한 한도에 도달하기 전에 SQL 데이터베이스에서 더 많은 작업을 할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-118">Efficiencies, such as batching, enable you to do more work on SQL Database before reaching these limits.</span></span> 
* <span data-ttu-id="97901-119">일괄 처리는 다수의 데이터베이스(분할)를 사용하는 아키텍처에 대해서도 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="97901-119">Batching is also effective for architectures that use multiple databases (sharding).</span></span> <span data-ttu-id="97901-120">각 데이터베이스 단위와의 상호 작용 효율은 전반적인 확장성에 있어 여전히 주요 요인입니다.</span><span class="sxs-lookup"><span data-stu-id="97901-120">The efficiency of your interaction with each database unit is still a key factor in your overall scalability.</span></span> 

<span data-ttu-id="97901-121">SQL 데이터베이스를 사용하는 장점 중 하나는 데이터베이스를 호스팅하는 서버를 관리하지 않아도 된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="97901-121">One of the benefits of using SQL Database is that you don’t have to manage the servers that host the database.</span></span> <span data-ttu-id="97901-122">하지만 관리되는 인프라는 사용자가 데이터베이스 최적화에 대해 달리 생각해봐야 한다는 것을 의미하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-122">However, this managed infrastructure also means that you have to think differently about database optimizations.</span></span> <span data-ttu-id="97901-123">더 이상은 데이터베이스 하드웨어 또는 네트워크 인프라 개선에만 기대를 걸 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-123">You can no longer look to improve the database hardware or network infrastructure.</span></span> <span data-ttu-id="97901-124">Microsoft Azure는 이러한 환경을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-124">Microsoft Azure controls those environments.</span></span> <span data-ttu-id="97901-125">사용자가 제어할 수 있는 주요 영역은 응용 프로그램이 SQL 데이터베이스와 상호 작용하는 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="97901-125">The main area that you can control is how your application interacts with SQL Database.</span></span> <span data-ttu-id="97901-126">일괄 처리는 이러한 최적화 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="97901-126">Batching is one of these optimizations.</span></span> 

<span data-ttu-id="97901-127">문서의 첫 번째 부분에서는 SQL 데이터베이스를 사용하는 .NET 응용 프로그램의 다양한 일괄 처리 기법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="97901-127">The first part of the paper examines various batching techniques for .NET applications that use SQL Database.</span></span> <span data-ttu-id="97901-128">마지막 두 세션은 일괄 처리 지침 및 시나리오를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-128">The last two sections cover batching guidelines and scenarios.</span></span>

## <a name="batching-strategies"></a><span data-ttu-id="97901-129">일괄 처리 전략</span><span class="sxs-lookup"><span data-stu-id="97901-129">Batching strategies</span></span>
### <a name="note-about-timing-results-in-this-topic"></a><span data-ttu-id="97901-130">이 문서의 타이밍 결과에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="97901-130">Note about timing results in this topic</span></span>
> [!NOTE]
> <span data-ttu-id="97901-131">결과가 기준은 아니며 **상대적인 성능**을 표시하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="97901-131">Results are not benchmarks but are meant to show **relative performance**.</span></span> <span data-ttu-id="97901-132">타이밍은 평균적으로 최소 10회의 테스트 실행을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-132">Timings are based on an average of at least 10 test runs.</span></span> <span data-ttu-id="97901-133">작업은 빈 테이블로의 삽입니다.</span><span class="sxs-lookup"><span data-stu-id="97901-133">Operations are inserts into an empty table.</span></span> <span data-ttu-id="97901-134">테스트는 V12 이전 버전에서 측정되었으며, 새로운 [서비스 계층](sql-database-service-tiers.md)을 사용하는 V12 데이터베이스에서 경험하는 처리량과 일치하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-134">These tests were measured pre-V12, and they do not necessarily correspond to throughput that you might experience in a V12 database using the new [service tiers](sql-database-service-tiers.md).</span></span> <span data-ttu-id="97901-135">일괄 처리 기법의 상대적인 장점은 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-135">The relative benefit of the batching technique should be similar.</span></span>
> 
> 

### <a name="transactions"></a><span data-ttu-id="97901-136">트랜잭션</span><span class="sxs-lookup"><span data-stu-id="97901-136">Transactions</span></span>
<span data-ttu-id="97901-137">일괄 작업에 대한 검토를 트랜잭션에 대한 얘기로 시작하는 것이 생소해 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-137">It seems strange to begin a review of batching by discussing transactions.</span></span> <span data-ttu-id="97901-138">하지만 클라이언트 쪽 트랜잭션 사용은 서버 쪽 일괄 처리에 성능을 향상시키는 미묘한 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="97901-138">But the use of client-side transactions has a subtle server-side batching effect that improves performance.</span></span> <span data-ttu-id="97901-139">트랜잭션은 단지 몇 줄의 코드만으로 추가될 수 있으며, 순차적인 작업의 성능을 향상시키는 빠른 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-139">And transactions can be added with only a few lines of code, so they provide a fast way to improve performance of sequential operations.</span></span>

<span data-ttu-id="97901-140">다음 C# 코드는 간단한 테이블에 삽입 및 업데이트 작업 시퀀스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-140">Consider the following C# code that contains a sequence of insert and update operations on a simple table.</span></span>

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

<span data-ttu-id="97901-141">다음 ADO.NET 코드는 이러한 작업을 순차적으로 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-141">The following ADO.NET code sequentially performs these operations.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

<span data-ttu-id="97901-142">이 코드를 최적화하는 최고의 방법은 이러한 호출의 클라이언트 쪽 일괄 처리 형식을 구현하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="97901-142">The best way to optimize this code is to implement some form of client-side batching of these calls.</span></span> <span data-ttu-id="97901-143">하지만 호출 시퀀스를 하나의 트랜잭션에 래핑하는 것만으로 이 코드의 성능을 높이는 간단한 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-143">But there is a simple way to increase the performance of this code by simply wrapping the sequence of calls in a transaction.</span></span> <span data-ttu-id="97901-144">다음은 트랜잭션을 사용하는 동일한 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="97901-144">Here is the same code that uses a transaction.</span></span>

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

<span data-ttu-id="97901-145">트랜잭션이 양쪽 예제에 실제로 사용되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-145">Transactions are actually being used in both of these examples.</span></span> <span data-ttu-id="97901-146">첫 번째 예제에서 각각의 개별 호출은 암시적 트랜잭션입니다.</span><span class="sxs-lookup"><span data-stu-id="97901-146">In the first example, each individual call is an implicit transaction.</span></span> <span data-ttu-id="97901-147">두 번째 예제에서 명시적 트랜잭션이 모든 호출을 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-147">In the second example, an explicit transaction wraps all of the calls.</span></span> <span data-ttu-id="97901-148">[미리 쓰기 트랜잭션 로그](https://msdn.microsoft.com/library/ms186259.aspx)에 대한 설명서에 따라, 로그 레코드는 트랜잭션이 커밋할 때 디스크에 플러시됩니다.</span><span class="sxs-lookup"><span data-stu-id="97901-148">Per the documentation for the [write-ahead transaction log](https://msdn.microsoft.com/library/ms186259.aspx), log records are flushed to the disk when the transaction commits.</span></span> <span data-ttu-id="97901-149">따라서 트랜잭션에 더 많은 호출을 포함시켜서, 트랜잭션 로그에 대한 쓰기를 트랜잭션이 커밋될 때까지 지연시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-149">So by including more calls in a transaction, the write to the transaction log can delay until the transaction is committed.</span></span> <span data-ttu-id="97901-150">사실상, 서버의 트랜잭션 로그에 대한 쓰기에 일괄 처리를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="97901-150">In effect, you are enabling batching for the writes to the server’s transaction log.</span></span>

<span data-ttu-id="97901-151">다음 테이블은 임시 테스팅 결과를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="97901-151">The following table shows some ad-hoc testing results.</span></span> <span data-ttu-id="97901-152">테스트는 동일한 순차적 삽입을 트랜잭션을 포함한 상태와 그렇지 않은 상태로 수행하였습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-152">The tests performed the same sequential inserts with and without transactions.</span></span> <span data-ttu-id="97901-153">보다 다양한 견해를 위해, 첫 번째 테스트는 랩톱에서 Microsoft Azure의 데이터베이스에 대해 원격으로 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-153">For more perspective, the first set of tests ran remotely from a laptop to the database in Microsoft Azure.</span></span> <span data-ttu-id="97901-154">두 번째 테스트는 동일한 Microsoft Azure 데이터 센터(미국 서부) 내에 상주하는 클라우드 서비스 및 데이터베이스에서 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-154">The second set of tests ran from a cloud service and database that both resided within the same Microsoft Azure datacenter (West US).</span></span> <span data-ttu-id="97901-155">다음 테이블은 트랜잭션 유 무 상태에서 순차적인 삽입의 소요 시간(밀리초)를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="97901-155">The following table shows the duration in milliseconds of sequential inserts with and without transactions.</span></span>

<span data-ttu-id="97901-156">**온-프레미스에서 Azure**:</span><span class="sxs-lookup"><span data-stu-id="97901-156">**On-Premises to Azure**:</span></span>

| <span data-ttu-id="97901-157">작업</span><span class="sxs-lookup"><span data-stu-id="97901-157">Operations</span></span> | <span data-ttu-id="97901-158">트랜잭션 없음(밀리초)</span><span class="sxs-lookup"><span data-stu-id="97901-158">No Transaction (ms)</span></span> | <span data-ttu-id="97901-159">트랜잭션(밀리초)</span><span class="sxs-lookup"><span data-stu-id="97901-159">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="97901-160">1</span><span class="sxs-lookup"><span data-stu-id="97901-160">1</span></span> |<span data-ttu-id="97901-161">130</span><span class="sxs-lookup"><span data-stu-id="97901-161">130</span></span> |<span data-ttu-id="97901-162">402</span><span class="sxs-lookup"><span data-stu-id="97901-162">402</span></span> |
| <span data-ttu-id="97901-163">10</span><span class="sxs-lookup"><span data-stu-id="97901-163">10</span></span> |<span data-ttu-id="97901-164">1208</span><span class="sxs-lookup"><span data-stu-id="97901-164">1208</span></span> |<span data-ttu-id="97901-165">1226</span><span class="sxs-lookup"><span data-stu-id="97901-165">1226</span></span> |
| <span data-ttu-id="97901-166">100</span><span class="sxs-lookup"><span data-stu-id="97901-166">100</span></span> |<span data-ttu-id="97901-167">12662</span><span class="sxs-lookup"><span data-stu-id="97901-167">12662</span></span> |<span data-ttu-id="97901-168">10395</span><span class="sxs-lookup"><span data-stu-id="97901-168">10395</span></span> |
| <span data-ttu-id="97901-169">1000</span><span class="sxs-lookup"><span data-stu-id="97901-169">1000</span></span> |<span data-ttu-id="97901-170">128852</span><span class="sxs-lookup"><span data-stu-id="97901-170">128852</span></span> |<span data-ttu-id="97901-171">102917</span><span class="sxs-lookup"><span data-stu-id="97901-171">102917</span></span> |

<span data-ttu-id="97901-172">**Azure에서Azure(동일한 데이터 센터)**:</span><span class="sxs-lookup"><span data-stu-id="97901-172">**Azure to Azure (same datacenter)**:</span></span>

| <span data-ttu-id="97901-173">작업</span><span class="sxs-lookup"><span data-stu-id="97901-173">Operations</span></span> | <span data-ttu-id="97901-174">트랜잭션 없음(밀리초)</span><span class="sxs-lookup"><span data-stu-id="97901-174">No Transaction (ms)</span></span> | <span data-ttu-id="97901-175">트랜잭션(밀리초)</span><span class="sxs-lookup"><span data-stu-id="97901-175">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="97901-176">1</span><span class="sxs-lookup"><span data-stu-id="97901-176">1</span></span> |<span data-ttu-id="97901-177">21</span><span class="sxs-lookup"><span data-stu-id="97901-177">21</span></span> |<span data-ttu-id="97901-178">26</span><span class="sxs-lookup"><span data-stu-id="97901-178">26</span></span> |
| <span data-ttu-id="97901-179">10</span><span class="sxs-lookup"><span data-stu-id="97901-179">10</span></span> |<span data-ttu-id="97901-180">220</span><span class="sxs-lookup"><span data-stu-id="97901-180">220</span></span> |<span data-ttu-id="97901-181">56</span><span class="sxs-lookup"><span data-stu-id="97901-181">56</span></span> |
| <span data-ttu-id="97901-182">100</span><span class="sxs-lookup"><span data-stu-id="97901-182">100</span></span> |<span data-ttu-id="97901-183">2145</span><span class="sxs-lookup"><span data-stu-id="97901-183">2145</span></span> |<span data-ttu-id="97901-184">341</span><span class="sxs-lookup"><span data-stu-id="97901-184">341</span></span> |
| <span data-ttu-id="97901-185">1000</span><span class="sxs-lookup"><span data-stu-id="97901-185">1000</span></span> |<span data-ttu-id="97901-186">21479</span><span class="sxs-lookup"><span data-stu-id="97901-186">21479</span></span> |<span data-ttu-id="97901-187">2756</span><span class="sxs-lookup"><span data-stu-id="97901-187">2756</span></span> |

> [!NOTE]
> <span data-ttu-id="97901-188">결과가 기준은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="97901-188">Results are not benchmarks.</span></span> <span data-ttu-id="97901-189">[이 문서의 타이밍 결과에 대한 정보](#note-about-timing-results-in-this-topic)를 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="97901-189">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="97901-190">이전 테스트 결과에 따르면, 단일 작업을 트랜잭션에 래핑하면 성능이 실제로 감소합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-190">Based on the previous test results, wrapping a single operation in a transaction actually decreases performance.</span></span> <span data-ttu-id="97901-191">하지만 단일 트랜잭션에 포함하는 작업의 수를 증가시키면, 성능 향상이 더 두드러집니다.</span><span class="sxs-lookup"><span data-stu-id="97901-191">But as you increase the number of operations within a single transaction, the performance improvement becomes more marked.</span></span> <span data-ttu-id="97901-192">모든 작업이 Microsoft Azure 데이터 센터 내에서 발생하는 경우에는 성능 차이가 더 현저하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="97901-192">The performance difference is also more noticeable when all operations occur within the Microsoft Azure datacenter.</span></span> <span data-ttu-id="97901-193">Microsoft Azure 데이터 센터 외부에서 SQL 데이터베이스를 사용하여 증가되는 대기 시간은 트랜잭션 사용으로 인한 성능 향상을 무색하게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97901-193">The increased latency of using SQL Database from outside the Microsoft Azure datacenter overshadows the performance gain of using transactions.</span></span>

<span data-ttu-id="97901-194">트랜잭션 사용이 성능을 향상시킬 수 있지만 [트랜잭션 및 연결에 대한 모범 사례를 지속적으로 관찰](https://msdn.microsoft.com/library/ms187484.aspx)하는 것이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-194">Although the use of transactions can increase performance, continue to [observe best practices for transactions and connections](https://msdn.microsoft.com/library/ms187484.aspx).</span></span> <span data-ttu-id="97901-195">트랜잭션을 최대한 짧게 유지하고 작업이 완료된 후에는 데이터베이스 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-195">Keep the transaction as short as possible, and close the database connection after the work completes.</span></span> <span data-ttu-id="97901-196">이전 예제의 using 문은 후속 코드 블록이 완료되면 연결이 닫히도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-196">The using statement in the previous example assures that the connection is closed when the subsequent code block completes.</span></span>

<span data-ttu-id="97901-197">이전 예제는 로컬 트랜잭션을 모든 ADO.NET 코드에 두 줄로 추가할 수 있다는 것을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="97901-197">The previous example demonstrates that you can add a local transaction to any ADO.NET code with two lines.</span></span> <span data-ttu-id="97901-198">트랜잭션은 순차적인 삽입, 업데이트, 삭제 작업을 생성하는 코드의 성능을 향상시키는 신속한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-198">Transactions offer a quick way to improve the performance of code that makes sequential insert, update, and delete operations.</span></span> <span data-ttu-id="97901-199">하지만 가장 빠른 성능의 경우에는, 클라이언트 쪽 일괄 처리의 장점(예: 테이블 반환 매개 변수)을 활용하기 위한 코드 변경을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-199">However, for the fastest performance, consider changing the code further to take advantage of client-side batching, such as table-valued parameters.</span></span>

<span data-ttu-id="97901-200">ADO.NET의 트랜잭션에 대한 자세한 내용은 [ADO.NET의 로컬 트랜잭션](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97901-200">For more information about transactions in ADO.NET, see [Local Transactions in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span></span>

### <a name="table-valued-parameters"></a><span data-ttu-id="97901-201">테이블 반환 매개 변수</span><span class="sxs-lookup"><span data-stu-id="97901-201">Table-valued parameters</span></span>
<span data-ttu-id="97901-202">테이블 반환 매개 변수는 Transact-SQL 문, 저장 프로시저, 함수의 매개 변수로 사용자 정의 테이블 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-202">Table-valued parameters support user-defined table types as parameters in Transact-SQL statements, stored procedures, and functions.</span></span> <span data-ttu-id="97901-203">클라이언트 쪽 일괄 처리 기법을 사용하면 여러 행의 데이터를 테이블 반환 변수 내에서 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-203">This client-side batching technique allows you to send multiple rows of data within the table-valued parameter.</span></span> <span data-ttu-id="97901-204">테이블 반환 매개 변수를 사용하려면 우선 테이블 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-204">To use table-valued parameters, first define a table type.</span></span> <span data-ttu-id="97901-205">다음 Transact-SQL 문은 **MyTableType**이라는 이름의 테이블 형식을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97901-205">The following Transact-SQL statement creates a table type named **MyTableType**.</span></span>

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


<span data-ttu-id="97901-206">코드에서 테이블 형식과 이름과 형식이 정확이 같은 **DataTable** 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97901-206">In code, you create a **DataTable** with the exact same names and types of the table type.</span></span> <span data-ttu-id="97901-207">**DataTable** 을 저장 프로시저 호출 또는 텍스트 쿼리의 매개 변수로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-207">Pass this **DataTable** in a parameter in a text query or stored procedure call.</span></span> <span data-ttu-id="97901-208">다음 예제는 이러한 기법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="97901-208">The following example shows this technique:</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. The following is a simple example.
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

<span data-ttu-id="97901-209">이전 예제에서 **SqlCommand** 개체는 테이블 반환 매개 변수 **@TestTvp**의 행을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-209">In the previous example, the **SqlCommand** object inserts rows from a table-valued parameter, **@TestTvp**.</span></span> <span data-ttu-id="97901-210">이전에 만든 **DataTable** 개체는 **SqlCommand.Parameters.Add** 메서드로 이 매개 변수에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="97901-210">The previously created **DataTable** object is assigned to this parameter with the **SqlCommand.Parameters.Add** method.</span></span> <span data-ttu-id="97901-211">삽입을 하나의 호출로 일괄 처리하면 순차적인 삽입의 성능을 상당히 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="97901-211">Batching the inserts in one call significantly increases the performance over sequential inserts.</span></span>

<span data-ttu-id="97901-212">이전 예제를 더욱 향상시키려면 텍스트 기반 명령 대신 저장 프로시저를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-212">To improve the previous example further, use a stored procedure instead of a text-based command.</span></span> <span data-ttu-id="97901-213">다음 Transact-SQL 명령은 **SimpleTestTableType** 테이블 반환 매개 변수를 받아들이는 저장 프로시저를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97901-213">The following Transact-SQL command creates a stored procedure that takes the **SimpleTestTableType** table-valued parameter.</span></span>

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

<span data-ttu-id="97901-214">그 후 이전 코드 예제의 **SqlCommand** 개체 선언을 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-214">Then change the **SqlCommand** object declaration in the previous code example to the following.</span></span>

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

<span data-ttu-id="97901-215">대부분의 경우 테이블 반환 매개 변수는 다른 일괄 처리 기법과 동등하거나 그 보다 뛰어난 성능을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-215">In most cases, table-valued parameters have equivalent or better performance than other batching techniques.</span></span> <span data-ttu-id="97901-216">테이블 반환 매개 변수는 다른 옵션에 비해 융통성이 많기 때문에 더 좋을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-216">Table-valued parameters are often preferable, because they are more flexible than other options.</span></span> <span data-ttu-id="97901-217">예를 들어 SQL 대량 복사와 같은 다른 기법은 새 행의 삽입만을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-217">For example, other techniques, such as SQL bulk copy, only permit the insertion of new rows.</span></span> <span data-ttu-id="97901-218">하지만 테이블 반환 매개 변수를 사용하면 저장 프로시저의 논리를 사용하여 업데이트되는 행과 삽입되는 행을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-218">But with table-valued parameters, you can use logic in the stored procedure to determine which rows are updates and which are inserts.</span></span> <span data-ttu-id="97901-219">지정된 행이 삽입될지, 업데이트될지 또는 삭제될지를 나타내는 “작업” 열을 포함하도록 테이블 형식이 수정될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-219">The table type can also be modified to contain an “Operation” column that indicates whether the specified row should be inserted, updated, or deleted.</span></span>

<span data-ttu-id="97901-220">다음 테이블은 테이블 반환 매개 변수 사용에 대한 임시 테스트 결과를 밀리초 단위로 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="97901-220">The following table shows ad-hoc test results for the use of table-valued parameters in milliseconds.</span></span>

| <span data-ttu-id="97901-221">작업</span><span class="sxs-lookup"><span data-stu-id="97901-221">Operations</span></span> | <span data-ttu-id="97901-222">온-프레미스에서 Azure(밀리초)</span><span class="sxs-lookup"><span data-stu-id="97901-222">On-Premises to Azure (ms)</span></span> | <span data-ttu-id="97901-223">Azure 동일한 데이터 센터(밀리초)</span><span class="sxs-lookup"><span data-stu-id="97901-223">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="97901-224">1</span><span class="sxs-lookup"><span data-stu-id="97901-224">1</span></span> |<span data-ttu-id="97901-225">124</span><span class="sxs-lookup"><span data-stu-id="97901-225">124</span></span> |<span data-ttu-id="97901-226">32</span><span class="sxs-lookup"><span data-stu-id="97901-226">32</span></span> |
| <span data-ttu-id="97901-227">10</span><span class="sxs-lookup"><span data-stu-id="97901-227">10</span></span> |<span data-ttu-id="97901-228">131</span><span class="sxs-lookup"><span data-stu-id="97901-228">131</span></span> |<span data-ttu-id="97901-229">25</span><span class="sxs-lookup"><span data-stu-id="97901-229">25</span></span> |
| <span data-ttu-id="97901-230">100</span><span class="sxs-lookup"><span data-stu-id="97901-230">100</span></span> |<span data-ttu-id="97901-231">338</span><span class="sxs-lookup"><span data-stu-id="97901-231">338</span></span> |<span data-ttu-id="97901-232">51</span><span class="sxs-lookup"><span data-stu-id="97901-232">51</span></span> |
| <span data-ttu-id="97901-233">1000</span><span class="sxs-lookup"><span data-stu-id="97901-233">1000</span></span> |<span data-ttu-id="97901-234">2615</span><span class="sxs-lookup"><span data-stu-id="97901-234">2615</span></span> |<span data-ttu-id="97901-235">382</span><span class="sxs-lookup"><span data-stu-id="97901-235">382</span></span> |
| <span data-ttu-id="97901-236">10000</span><span class="sxs-lookup"><span data-stu-id="97901-236">10000</span></span> |<span data-ttu-id="97901-237">23830</span><span class="sxs-lookup"><span data-stu-id="97901-237">23830</span></span> |<span data-ttu-id="97901-238">3586</span><span class="sxs-lookup"><span data-stu-id="97901-238">3586</span></span> |

> [!NOTE]
> <span data-ttu-id="97901-239">결과가 기준은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="97901-239">Results are not benchmarks.</span></span> <span data-ttu-id="97901-240">[이 문서의 타이밍 결과에 대한 정보](#note-about-timing-results-in-this-topic)를 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="97901-240">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="97901-241">일괄 처리를 통한 성능 향상은 바로 식별이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-241">The performance gain from batching is immediately apparent.</span></span> <span data-ttu-id="97901-242">이전의 순차 테스트에서 1000개 작업이 데이터센터 외부에서는 129초가 소요되었고 데이터센터 내부에서는 21초가 소요되었습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-242">In the previous sequential test, 1000 operations took 129 seconds outside the datacenter and 21 seconds from within the datacenter.</span></span> <span data-ttu-id="97901-243">하지만 테이블 반환 변수를 사용하면 1000개 작업이 데이터센터 외부에서는 2.6초, 데이터센터 내부에서는 0.4초밖에 걸리지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-243">But with table-valued parameters, 1000 operations take only 2.6 seconds outside the datacenter and 0.4 seconds within the datacenter.</span></span>

<span data-ttu-id="97901-244">테이블 반환 매개 변수에 대한 자세한 내용은 [테이블 반환 매개 변수](https://msdn.microsoft.com/library/bb510489.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97901-244">For more information on table-valued parameters, see [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

### <a name="sql-bulk-copy"></a><span data-ttu-id="97901-245">SQL 대량 복사</span><span class="sxs-lookup"><span data-stu-id="97901-245">SQL bulk copy</span></span>
<span data-ttu-id="97901-246">SQL 대량 복사는 대량의 데이터를 대상 데이터베이스에 삽입하는 또 다른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="97901-246">SQL bulk copy is another way to insert large amounts of data into a target database.</span></span> <span data-ttu-id="97901-247">NET 응용 프로그램은 **SqlBulkCopy** 클래스를 사용하여 대량 삽입 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-247">.NET applications can use the **SqlBulkCopy** class to perform bulk insert operations.</span></span> <span data-ttu-id="97901-248">**SqlBulkCopy**는 명령줄 도구 **Bcp.exe** 또는 Transact-SQL 문 **BULK INSERT**와 기능면에서 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-248">**SqlBulkCopy** is similar in function to the command-line tool, **Bcp.exe**, or the Transact-SQL statement, **BULK INSERT**.</span></span> <span data-ttu-id="97901-249">다음 코드 예제는 원본 **DataTable**테이블의 행을 SQL Server의 MyTable이라는 대상 테이블로 대량 복사하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="97901-249">The following code example shows how to bulk copy the rows in the source **DataTable**, table, to the destination table in SQL Server, MyTable.</span></span>

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

<span data-ttu-id="97901-250">테이블 반환 매개 변수보다 대량 복사를 선호하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-250">There are some cases where bulk copy is preferred over table-valued parameters.</span></span> <span data-ttu-id="97901-251">[테이블 반환 매개 변수](https://msdn.microsoft.com/library/bb510489.aspx)문서에서 테이블 반환 매개 변수와 BULK INSERT 작업의 비교 테이블을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="97901-251">See the comparison table of Table-Valued parameters versus BULK INSERT operations in the topic [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

<span data-ttu-id="97901-252">다음 임시 테스트 결과는 **SqlBulkCopy** 를 통한 일괄 처리 성능을 밀리초 단위로 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="97901-252">The following ad-hoc test results show the performance of batching with **SqlBulkCopy** in milliseconds.</span></span>

| <span data-ttu-id="97901-253">작업</span><span class="sxs-lookup"><span data-stu-id="97901-253">Operations</span></span> | <span data-ttu-id="97901-254">온-프레미스에서 Azure(밀리초)</span><span class="sxs-lookup"><span data-stu-id="97901-254">On-Premises to Azure (ms)</span></span> | <span data-ttu-id="97901-255">Azure 동일한 데이터 센터(밀리초)</span><span class="sxs-lookup"><span data-stu-id="97901-255">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="97901-256">1</span><span class="sxs-lookup"><span data-stu-id="97901-256">1</span></span> |<span data-ttu-id="97901-257">433</span><span class="sxs-lookup"><span data-stu-id="97901-257">433</span></span> |<span data-ttu-id="97901-258">57</span><span class="sxs-lookup"><span data-stu-id="97901-258">57</span></span> |
| <span data-ttu-id="97901-259">10</span><span class="sxs-lookup"><span data-stu-id="97901-259">10</span></span> |<span data-ttu-id="97901-260">441</span><span class="sxs-lookup"><span data-stu-id="97901-260">441</span></span> |<span data-ttu-id="97901-261">32</span><span class="sxs-lookup"><span data-stu-id="97901-261">32</span></span> |
| <span data-ttu-id="97901-262">100</span><span class="sxs-lookup"><span data-stu-id="97901-262">100</span></span> |<span data-ttu-id="97901-263">636</span><span class="sxs-lookup"><span data-stu-id="97901-263">636</span></span> |<span data-ttu-id="97901-264">53</span><span class="sxs-lookup"><span data-stu-id="97901-264">53</span></span> |
| <span data-ttu-id="97901-265">1000</span><span class="sxs-lookup"><span data-stu-id="97901-265">1000</span></span> |<span data-ttu-id="97901-266">2535</span><span class="sxs-lookup"><span data-stu-id="97901-266">2535</span></span> |<span data-ttu-id="97901-267">341</span><span class="sxs-lookup"><span data-stu-id="97901-267">341</span></span> |
| <span data-ttu-id="97901-268">10000</span><span class="sxs-lookup"><span data-stu-id="97901-268">10000</span></span> |<span data-ttu-id="97901-269">21605</span><span class="sxs-lookup"><span data-stu-id="97901-269">21605</span></span> |<span data-ttu-id="97901-270">2737</span><span class="sxs-lookup"><span data-stu-id="97901-270">2737</span></span> |

> [!NOTE]
> <span data-ttu-id="97901-271">결과가 기준은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="97901-271">Results are not benchmarks.</span></span> <span data-ttu-id="97901-272">[이 문서의 타이밍 결과에 대한 정보](#note-about-timing-results-in-this-topic)를 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="97901-272">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="97901-273">소규모 배치에서는, 테이블 반환 매개 변수가 **SqlBulkCopy** 클래스보다 성능이 뛰어납니다.</span><span class="sxs-lookup"><span data-stu-id="97901-273">In smaller batch sizes, the use table-valued parameters outperformed the **SqlBulkCopy** class.</span></span> <span data-ttu-id="97901-274">하지만 1,000개 및 10,000개 행에 대한 테스트의 경우 **SqlBulkCopy** 가 테이블 반환 매개 변수보다 12-31% 더 빠르게 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="97901-274">However, **SqlBulkCopy** performed 12-31% faster than table-valued parameters for the tests of 1,000 and 10,000 rows.</span></span> <span data-ttu-id="97901-275">테이블 반환 매개 변수처럼 **SqlBulkCopy** 역시 일괄 처리된 삽입의 좋은 옵션이며, 비일괄 처리 작업의 성능과 비교하면 특히 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-275">Like table-valued parameters, **SqlBulkCopy** is a good option for batched inserts, especially when compared to the performance of non-batched operations.</span></span>

<span data-ttu-id="97901-276">ADO.NET에서 대량 복사에 대한 자세한 내용은 [SQL Server에서의 대량 복사 작업](https://msdn.microsoft.com/library/7ek5da1a.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97901-276">For more information on bulk copy in ADO.NET, see [Bulk Copy Operations in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span></span>

### <a name="multiple-row-parameterized-insert-statements"></a><span data-ttu-id="97901-277">여러 행의 매개 변수가 있는 INSERT 문</span><span class="sxs-lookup"><span data-stu-id="97901-277">Multiple-row Parameterized INSERT statements</span></span>
<span data-ttu-id="97901-278">소규모 배치에 대한 한 가지 대안은 여러 행을 삽입하는 매개 변수가 있는 대량 INSERT 문을 생성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="97901-278">One alternative for small batches is to construct a large parameterized INSERT statement that inserts multiple rows.</span></span> <span data-ttu-id="97901-279">다음 코드 예제는 이러한 기법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="97901-279">The following code example demonstrates this technique.</span></span>

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


<span data-ttu-id="97901-280">이 예제는 기본적인 개념을 보여주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="97901-280">This example is meant to show the basic concept.</span></span> <span data-ttu-id="97901-281">보다 현실적인 시나리오는 필요한 엔터티를 이어서 쿼리 문자열과 명령 매개 변수를 동시에 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-281">A more realistic scenario would loop through the required entities to construct the query string and the command parameters simultaneously.</span></span> <span data-ttu-id="97901-282">쿼리 매개 변수는 총 2100개로 제한되기 때문에, 이러한 방식으로 처리되는 행의 총 수가 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="97901-282">You are limited to a total of 2100 query parameters, so this limits the total number of rows that can be processed in this manner.</span></span>

<span data-ttu-id="97901-283">다음 임시 테스트 결과는 이런 형식으로 된 Insert 문의 성능을 밀리초 단위로 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="97901-283">The following ad-hoc test results show the performance of this type of insert statement in milliseconds.</span></span>

| <span data-ttu-id="97901-284">작업</span><span class="sxs-lookup"><span data-stu-id="97901-284">Operations</span></span> | <span data-ttu-id="97901-285">테이블 반환 매개 변수(밀리초)</span><span class="sxs-lookup"><span data-stu-id="97901-285">Table-valued parameters (ms)</span></span> | <span data-ttu-id="97901-286">단일 문 INSERT(밀리초)</span><span class="sxs-lookup"><span data-stu-id="97901-286">Single-statement INSERT (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="97901-287">1</span><span class="sxs-lookup"><span data-stu-id="97901-287">1</span></span> |<span data-ttu-id="97901-288">32</span><span class="sxs-lookup"><span data-stu-id="97901-288">32</span></span> |<span data-ttu-id="97901-289">20</span><span class="sxs-lookup"><span data-stu-id="97901-289">20</span></span> |
| <span data-ttu-id="97901-290">10</span><span class="sxs-lookup"><span data-stu-id="97901-290">10</span></span> |<span data-ttu-id="97901-291">30</span><span class="sxs-lookup"><span data-stu-id="97901-291">30</span></span> |<span data-ttu-id="97901-292">25</span><span class="sxs-lookup"><span data-stu-id="97901-292">25</span></span> |
| <span data-ttu-id="97901-293">100</span><span class="sxs-lookup"><span data-stu-id="97901-293">100</span></span> |<span data-ttu-id="97901-294">33</span><span class="sxs-lookup"><span data-stu-id="97901-294">33</span></span> |<span data-ttu-id="97901-295">51</span><span class="sxs-lookup"><span data-stu-id="97901-295">51</span></span> |

> [!NOTE]
> <span data-ttu-id="97901-296">결과가 기준은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="97901-296">Results are not benchmarks.</span></span> <span data-ttu-id="97901-297">[이 문서의 타이밍 결과에 대한 정보](#note-about-timing-results-in-this-topic)를 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="97901-297">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="97901-298">이 방법은 행이 100개 미만인 배치에 대해 약간 더 빠를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-298">This approach can be slightly faster for batches that are less than 100 rows.</span></span> <span data-ttu-id="97901-299">이 기법은 향상 폭은 작지만 사용자의 특정 응용 프로그램 시나리오에서 잘 작동할만한 또 다른 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="97901-299">Although the improvement is small, this technique is another option that might work well in your specific application scenario.</span></span>

### <a name="dataadapter"></a><span data-ttu-id="97901-300">DataAdapter</span><span class="sxs-lookup"><span data-stu-id="97901-300">DataAdapter</span></span>
<span data-ttu-id="97901-301">**DataAdapter** 클래스를 사용하면 **DataSet** 개체를 수정한 후 INSERT, UPDATE, DELETE 작업으로 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-301">The **DataAdapter** class allows you to modify a **DataSet** object and then submit the changes as INSERT, UPDATE, and DELETE operations.</span></span> <span data-ttu-id="97901-302">**DataAdapter** 를 이런 방식으로 사용하는 경우, 각각의 고유한 작업에 대해 개별 호출이 생성된다는 점에 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-302">If you are using the **DataAdapter** in this manner, it is important to note that separate calls are made for each distinct operation.</span></span> <span data-ttu-id="97901-303">성능을 향상시키려면 한 번에 일괄 처리되어야 하는 작업의 수에 대해 **UpdateBatchSize** 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-303">To improve performance, use the **UpdateBatchSize** property to the number of operations that should be batched at a time.</span></span> <span data-ttu-id="97901-304">자세한 내용은 [DataAdapters를 사용하여 배치 작업 수행](https://msdn.microsoft.com/library/aadf8fk2.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97901-304">For more information, see [Performing Batch Operations Using DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span></span>

### <a name="entity-framework"></a><span data-ttu-id="97901-305">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="97901-305">Entity framework</span></span>
<span data-ttu-id="97901-306">Entity Framework는 현재 일괄 처리를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-306">Entity Framework does not currently support batching.</span></span> <span data-ttu-id="97901-307">커뮤니티의 다른 개발자들은 **SaveChanges** 메서드 오버라이드와 같은 차선책을 설명하려는 시도를 했습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-307">Different developers in the community have attempted to demonstrate workarounds, such as override the **SaveChanges** method.</span></span> <span data-ttu-id="97901-308">하지만 솔루션이 대체적으로 복잡하고 응용 프로그램 및 데이터 모델에 맞게 사용자 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="97901-308">But the solutions are typically complex and customized to the application and data model.</span></span> <span data-ttu-id="97901-309">Entity Framework CodePlex 프로젝트에는 기능 요청에 관한 토론 페이지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-309">The Entity Framework codeplex project currently has a discussion page on this feature request.</span></span> <span data-ttu-id="97901-310">토론 페이지를 보려면 [Design Meeting Notes – August 2, 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012)(디자인 모임 메모 - 2012년 8월 2일)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97901-310">To view this discussion, see [Design Meeting Notes - August 2, 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span></span>

### <a name="xml"></a><span data-ttu-id="97901-311">XML</span><span class="sxs-lookup"><span data-stu-id="97901-311">XML</span></span>
<span data-ttu-id="97901-312">완벽함을 기하기 위해 일괄 처리 전략의 하나로 XML에 대해 얘기하는 것이 중요하다고 생각합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-312">For completeness, we feel that it is important to talk about XML as a batching strategy.</span></span> <span data-ttu-id="97901-313">하지만 XML 사용이 다른 메서드에 비해 이점이 없고 몇 가지 불편한 점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-313">However, the use of XML has no advantages over other methods and several disadvantages.</span></span> <span data-ttu-id="97901-314">접근 방법은 테이블 반환 매개 변수와 유사하지만 사용자 정의된 테이블 대신 XML 파일 또는 문자열이 저장 프로시저로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="97901-314">The approach is similar to table-valued parameters, but an XML file or string is passed to a stored procedure instead of a user-defined table.</span></span> <span data-ttu-id="97901-315">저장 프로시저는 저장 프로시저로 명령을 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-315">The stored procedure parses the commands in the stored procedure.</span></span>

<span data-ttu-id="97901-316">이러한 접근 방법에는 몇 가지 불편한 점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-316">There are several disadvantages to this approach:</span></span>

* <span data-ttu-id="97901-317">XML 작업은 번거롭고 오류 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-317">Working with XML can be cumbersome and error prone.</span></span>
* <span data-ttu-id="97901-318">데이터베이스에서 XML 구문 분석은 CPU를 많이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-318">Parsing the XML on the database can be CPU-intensive.</span></span>
* <span data-ttu-id="97901-319">대부분의 경우 이 방법은 테이블 반환 매개 변수보다 느립니다.</span><span class="sxs-lookup"><span data-stu-id="97901-319">In most cases, this method is slower than table-valued parameters.</span></span>

<span data-ttu-id="97901-320">이런 이유로 인해서 배치 쿼리에 XML을 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-320">For these reasons, the use of XML for batch queries is not recommended.</span></span>

## <a name="batching-considerations"></a><span data-ttu-id="97901-321">일괄 처리 고려 사항</span><span class="sxs-lookup"><span data-stu-id="97901-321">Batching considerations</span></span>
<span data-ttu-id="97901-322">다음 섹션은 SQL 데이터베이스 응용 프로그램에서 일괄 처리를 사용하는 것에 대해 더 많은 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-322">The following sections provide more guidance for the use of batching in SQL Database applications.</span></span>

### <a name="tradeoffs"></a><span data-ttu-id="97901-323">균형 유지</span><span class="sxs-lookup"><span data-stu-id="97901-323">Tradeoffs</span></span>
<span data-ttu-id="97901-324">아키텍처에 따라서 일괄 처리는 성능과 복원력 사이에서 균형을 유지해야 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-324">Depending on your architecture, batching can involve a tradeoff between performance and resiliency.</span></span> <span data-ttu-id="97901-325">사용자의 역할이 예상치 않게 중단되는 시나리오를 예로 들어보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-325">For example, consider the scenario where your role unexpectedly goes down.</span></span> <span data-ttu-id="97901-326">데이터 행을 하나만 손실하는 것이, 제출하지 않은 일괄 처리 행을 대량으로 손실하는 것보다 충격이 적습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-326">If you lose one row of data, the impact is smaller than the impact of losing a large batch of unsubmitted rows.</span></span> <span data-ttu-id="97901-327">행을 데이터베이스에 보내기 전에 일정 시간 동안 버퍼에 보류하면 큰 위험이 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="97901-327">There is a greater risk when you buffer rows before sending them to the database in a specified time window.</span></span>

<span data-ttu-id="97901-328">이렇게 균형 유지가 필요하기 때문에 일괄 처리하는 작업의 유형을 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-328">Because of this tradeoff, evaluate the type of operations that you batch.</span></span> <span data-ttu-id="97901-329">덜 중요한 데이터는 보다 적극적으로(배치 규모는 더 크게 기간은 더 길게) 일괄 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-329">Batch more aggressively (larger batches and longer time windows) with data that is less critical.</span></span>

### <a name="batch-size"></a><span data-ttu-id="97901-330">배치 크기</span><span class="sxs-lookup"><span data-stu-id="97901-330">Batch size</span></span>
<span data-ttu-id="97901-331">테스트에 따르면 대량의 배치를 작은 청크로 나누는 장점은 대체적으로 거의 없었습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-331">In our tests, there was typically no advantage to breaking large batches into smaller chunks.</span></span> <span data-ttu-id="97901-332">실제로 이러한 세분화가 큰 배치 하나를 제출하는 것보다 성능을 느리게 하는 결과를 초래하기도 했습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-332">In fact, this subdivision often resulted in slower performance than submitting a single large batch.</span></span> <span data-ttu-id="97901-333">예를 들어, 행 1000개를 삽입하는 시나리오를 생각해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-333">For example, consider a scenario where you want to insert 1000 rows.</span></span> <span data-ttu-id="97901-334">다음 테이블은 테이블 반환 매개 변수를 사용하여 행 1000개를 소규모 배치로 나누어  삽입하는데 소요되는 시간을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="97901-334">The following table shows how long it takes to use table-valued parameters to insert 1000 rows when divided into smaller batches.</span></span>

| <span data-ttu-id="97901-335">배치 크기</span><span class="sxs-lookup"><span data-stu-id="97901-335">Batch size</span></span> | <span data-ttu-id="97901-336">반복 횟수</span><span class="sxs-lookup"><span data-stu-id="97901-336">Iterations</span></span> | <span data-ttu-id="97901-337">테이블 반환 매개 변수(밀리초)</span><span class="sxs-lookup"><span data-stu-id="97901-337">Table-valued parameters (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="97901-338">1000</span><span class="sxs-lookup"><span data-stu-id="97901-338">1000</span></span> |<span data-ttu-id="97901-339">1</span><span class="sxs-lookup"><span data-stu-id="97901-339">1</span></span> |<span data-ttu-id="97901-340">347</span><span class="sxs-lookup"><span data-stu-id="97901-340">347</span></span> |
| <span data-ttu-id="97901-341">500</span><span class="sxs-lookup"><span data-stu-id="97901-341">500</span></span> |<span data-ttu-id="97901-342">2</span><span class="sxs-lookup"><span data-stu-id="97901-342">2</span></span> |<span data-ttu-id="97901-343">355</span><span class="sxs-lookup"><span data-stu-id="97901-343">355</span></span> |
| <span data-ttu-id="97901-344">100</span><span class="sxs-lookup"><span data-stu-id="97901-344">100</span></span> |<span data-ttu-id="97901-345">10</span><span class="sxs-lookup"><span data-stu-id="97901-345">10</span></span> |<span data-ttu-id="97901-346">465</span><span class="sxs-lookup"><span data-stu-id="97901-346">465</span></span> |
| <span data-ttu-id="97901-347">50</span><span class="sxs-lookup"><span data-stu-id="97901-347">50</span></span> |<span data-ttu-id="97901-348">20</span><span class="sxs-lookup"><span data-stu-id="97901-348">20</span></span> |<span data-ttu-id="97901-349">630</span><span class="sxs-lookup"><span data-stu-id="97901-349">630</span></span> |

> [!NOTE]
> <span data-ttu-id="97901-350">결과가 기준은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="97901-350">Results are not benchmarks.</span></span> <span data-ttu-id="97901-351">[이 문서의 타이밍 결과에 대한 정보](#note-about-timing-results-in-this-topic)를 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="97901-351">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="97901-352">1000개 행에 대한 최고의 성능은 모두를 한꺼번에 제출하는 것이라는 사실을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-352">You can see that the best performance for 1000 rows is to submit them all at once.</span></span> <span data-ttu-id="97901-353">다른 테스트(여기에 표시되지 않은)에서는 10000개 행의 배치 하나를 5000개 행의 배치 2개로 나눈 경우에 작은 성능 향상이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-353">In other tests (not shown here) there was a small performance gain to break a 10000 row batch into two batches of 5000.</span></span> <span data-ttu-id="97901-354">하지만 이 테스트에 대한 테이블 스키마가 상대적으로 간단하기 때문에, 이러한 결론을 검증하기 위해서는 사용자의 데이터 및 배치 크기에 대한 테스트를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-354">But the table schema for these tests is relatively simple, so you should perform tests on your specific data and batch sizes to verify these findings.</span></span>

<span data-ttu-id="97901-355">또 다른 요인 고려 사항은 전체 배치가 너무 커지면 SQL 데이터베이스가 흐름을 제한하고 배치 커밋을 거부할 수 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="97901-355">Another factor to consider is that if the total batch becomes too large, SQL Database might throttle and refuse to commit the batch.</span></span> <span data-ttu-id="97901-356">최고의 결과를 위해서는 사용자의 특정한 시나리오를 테스트하여 이상적인 배치 규모가 있는가를 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-356">For the best results, test your specific scenario to determine if there is an ideal batch size.</span></span> <span data-ttu-id="97901-357">런타임에 배치 규모를 구성할 수 있도록 하여 성능 또는 오류를 기반으로 신속한 조정이 가능하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-357">Make the batch size configurable at runtime to enable quick adjustments based on performance or errors.</span></span>

<span data-ttu-id="97901-358">마지막으로 배치의 규모를 일괄 처리와 관련된 위험과 비교 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-358">Finally, balance the size of the batch with the risks associated with batching.</span></span> <span data-ttu-id="97901-359">일시적인 오류 또는 역할 실패가 발생하는 경우에는 작업을 재시도하거나 배치의 데이터가 손실되어 발생하는 결과를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-359">If there are transient errors or the role fails, consider the consequences of retrying the operation or of losing the data in the batch.</span></span>

### <a name="parallel-processing"></a><span data-ttu-id="97901-360">병렬 처리</span><span class="sxs-lookup"><span data-stu-id="97901-360">Parallel processing</span></span>
<span data-ttu-id="97901-361">배치의 규모는 줄이면서 다수의 스레드를 사용하여 작업을 실행하는 방법을 취하면 어떨까요?</span><span class="sxs-lookup"><span data-stu-id="97901-361">What if you took the approach of reducing the batch size but used multiple threads to execute the work?</span></span> <span data-ttu-id="97901-362">앞서 언급했지만, 테스트에 따르면 여러 개의 소형 다중 스레드 배치는 일반적으로 하나의 대형 배치보다 성능이 낮았습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-362">Again, our tests showed that several smaller multithreaded batches typically performed worse than a single larger batch.</span></span> <span data-ttu-id="97901-363">다음 테스트는 1000개의 행을 하나 이상의 병렬 배치에 삽입하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-363">The following test attempts to insert 1000 rows in one or more parallel batches.</span></span> <span data-ttu-id="97901-364">이 테스트는 동시에 실행되는 배치가 많아질수록 실제로 성능이 어떻게 감소되는가를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="97901-364">This test shows how more simultaneous batches actually decreased performance.</span></span>

| <span data-ttu-id="97901-365">배치 크기[반복 횟수]</span><span class="sxs-lookup"><span data-stu-id="97901-365">Batch size [Iterations]</span></span> | <span data-ttu-id="97901-366">스레드 2개(밀리초)</span><span class="sxs-lookup"><span data-stu-id="97901-366">Two threads (ms)</span></span> | <span data-ttu-id="97901-367">스레드 4개(밀리초)</span><span class="sxs-lookup"><span data-stu-id="97901-367">Four threads (ms)</span></span> | <span data-ttu-id="97901-368">스레드 6개(밀리초)</span><span class="sxs-lookup"><span data-stu-id="97901-368">Six threads (ms)</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="97901-369">1000 [1]</span><span class="sxs-lookup"><span data-stu-id="97901-369">1000 [1]</span></span> |<span data-ttu-id="97901-370">277</span><span class="sxs-lookup"><span data-stu-id="97901-370">277</span></span> |<span data-ttu-id="97901-371">315</span><span class="sxs-lookup"><span data-stu-id="97901-371">315</span></span> |<span data-ttu-id="97901-372">266</span><span class="sxs-lookup"><span data-stu-id="97901-372">266</span></span> |
| <span data-ttu-id="97901-373">500 [2]</span><span class="sxs-lookup"><span data-stu-id="97901-373">500 [2]</span></span> |<span data-ttu-id="97901-374">548</span><span class="sxs-lookup"><span data-stu-id="97901-374">548</span></span> |<span data-ttu-id="97901-375">278</span><span class="sxs-lookup"><span data-stu-id="97901-375">278</span></span> |<span data-ttu-id="97901-376">256</span><span class="sxs-lookup"><span data-stu-id="97901-376">256</span></span> |
| <span data-ttu-id="97901-377">250 [4]</span><span class="sxs-lookup"><span data-stu-id="97901-377">250 [4]</span></span> |<span data-ttu-id="97901-378">405</span><span class="sxs-lookup"><span data-stu-id="97901-378">405</span></span> |<span data-ttu-id="97901-379">329</span><span class="sxs-lookup"><span data-stu-id="97901-379">329</span></span> |<span data-ttu-id="97901-380">265</span><span class="sxs-lookup"><span data-stu-id="97901-380">265</span></span> |
| <span data-ttu-id="97901-381">100 [10]</span><span class="sxs-lookup"><span data-stu-id="97901-381">100 [10]</span></span> |<span data-ttu-id="97901-382">488</span><span class="sxs-lookup"><span data-stu-id="97901-382">488</span></span> |<span data-ttu-id="97901-383">439</span><span class="sxs-lookup"><span data-stu-id="97901-383">439</span></span> |<span data-ttu-id="97901-384">391</span><span class="sxs-lookup"><span data-stu-id="97901-384">391</span></span> |

> [!NOTE]
> <span data-ttu-id="97901-385">결과가 기준은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="97901-385">Results are not benchmarks.</span></span> <span data-ttu-id="97901-386">[이 문서의 타이밍 결과에 대한 정보](#note-about-timing-results-in-this-topic)를 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="97901-386">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="97901-387">병렬 처리로 인한 성능의 저하에는 몇 가지 잠재적인 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-387">There are several potential reasons for the degradation in performance due to parallelism:</span></span>

* <span data-ttu-id="97901-388">동시에 실행되는 네트워크 호출이 하나가 아니라 여러 개입니다.</span><span class="sxs-lookup"><span data-stu-id="97901-388">There are multiple simultaneous network calls instead of one.</span></span>
* <span data-ttu-id="97901-389">단일 테이블에 대해 여러 개의 작업이 수행되면 경합과 차단이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-389">Multiple operations against a single table can result in contention and blocking.</span></span>
* <span data-ttu-id="97901-390">멀티 스레드와 관련된 오버헤드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-390">There are overheads associated with multithreading.</span></span>
* <span data-ttu-id="97901-391">다수의 연결을 여는 비용이 병렬 처리의 이점을 능가합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-391">The expense of opening multiple connections outweighs the benefit of parallel processing.</span></span>

<span data-ttu-id="97901-392">다른 테이블이나 데이터베이스를 대상으로 하는 경우에는 이러한 전략을 통해 얼마간 성능 향상을 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-392">If you target different tables or databases, it is possible to see some performance gain with this strategy.</span></span> <span data-ttu-id="97901-393">데이터베이스 분할 또는 페더레이션은 이런 방법에 대한 시나리오가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-393">Database sharding or federations would be a scenario for this approach.</span></span> <span data-ttu-id="97901-394">분할은 여러 개의 데이터베이스를 사용하며 각각의 데이터베이스에 다른 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="97901-394">Sharding uses multiple databases and routes different data to each database.</span></span> <span data-ttu-id="97901-395">각각의 소형 배치가 다른 데이터베이스로 가는 경우에는 병렬로 작업을 수행하는 것이 더 효율적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-395">If each small batch is going to a different database, then performing the operations in parallel can be more efficient.</span></span> <span data-ttu-id="97901-396">하지만 솔루션에 데이터베이스 분할을 사용하자는 결정을 내리는 근거로 사용할 정도로 성능 향상이 현저하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-396">However, the performance gain is not significant enough to use as the basis for a decision to use database sharding in your solution.</span></span>

<span data-ttu-id="97901-397">일부 디자인의 경우, 소형 배치의 병렬 실행으로 인해 부하가 걸린 시스템 내에서 요청 처리량이 향상되기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-397">In some designs, parallel execution of smaller batches can result in improved throughput of requests in a system under load.</span></span> <span data-ttu-id="97901-398">이런 경우, 하나의 대형 배치를 처리하는 것이 더 빠르더라도 다수의 배치를 병렬로 처리하는 것이 더 효율적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-398">In this case, even though it is quicker to process a single larger batch, processing multiple batches in parallel might be more efficient.</span></span>

<span data-ttu-id="97901-399">병렬 실행을 사용하는 경우에는 최대 작업자 스레드 수에 대한 제어를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-399">If you do use parallel execution, consider controlling the maximum number of worker threads.</span></span> <span data-ttu-id="97901-400">숫자가 작을수록 경합이 줄어들고 실행 시간은 빨라집니다.</span><span class="sxs-lookup"><span data-stu-id="97901-400">A smaller number might result in less contention and a faster execution time.</span></span> <span data-ttu-id="97901-401">또한 이를 통해 연결 및 트랜잭션이 대상 데이터베이스에 부과하는 추가적인 부하를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-401">Also, consider the additional load that this places on the target database both in connections and transactions.</span></span>

### <a name="related-performance-factors"></a><span data-ttu-id="97901-402">관련된 성능 요인</span><span class="sxs-lookup"><span data-stu-id="97901-402">Related performance factors</span></span>
<span data-ttu-id="97901-403">데이터 베이스 성능에 대한 전형적인 지침은 일괄 처리에도 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="97901-403">Typical guidance on database performance also affects batching.</span></span> <span data-ttu-id="97901-404">예를 들어, 기본 키가 크거나 비클러스터형 인덱스가 많은 테이블에 대한 삽입 성능은 감소됩니다.</span><span class="sxs-lookup"><span data-stu-id="97901-404">For example, insert performance is reduced for tables that have a large primary key or many nonclustered indexes.</span></span>

<span data-ttu-id="97901-405">테이블 반환 매개 변수가 저장 프로시저를 사용하는 경우에는 프로시저의 시작에 **SET NOCOUNT ON** 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-405">If table-valued parameters use a stored procedure, you can use the command **SET NOCOUNT ON** at the beginning of the procedure.</span></span> <span data-ttu-id="97901-406">이 명령문은 프로시저에서 영향을 받은 행의 수에 대한 반환을 억제합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-406">This statement suppresses the return of the count of the affected rows in the procedure.</span></span> <span data-ttu-id="97901-407">하지만 테스트에서는 **SET NOCOUNT ON** 의 사용이 효과가 없거나 성능을 감소시켰습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-407">However, in our tests, the use of **SET NOCOUNT ON** either had no effect or decreased performance.</span></span> <span data-ttu-id="97901-408">테스트 저장 프로시저는 간단하게 테이블 반환 매개 변수의 **INSERT** 명령 하나만 포함했습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-408">The test stored procedure was simple with a single **INSERT** command from the table-valued parameter.</span></span> <span data-ttu-id="97901-409">이 명령문은 더 복잡한 저장 프로시저에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-409">It is possible that more complex stored procedures would benefit from this statement.</span></span> <span data-ttu-id="97901-410">하지만 저장 프로시저에 **SET NOCOUNT ON** 을 추가한다고 해서 자동으로 성능이 향상될 것이라고 가정하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="97901-410">But don’t assume that adding **SET NOCOUNT ON** to your stored procedure automatically improves performance.</span></span> <span data-ttu-id="97901-411">효과를 이해하려면 **SET NOCOUNT ON** 문을 포함한 상태와 그렇지 않은 상태로 사용자의 저장 프로시저를 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-411">To understand the effect, test your stored procedure with and without the **SET NOCOUNT ON** statement.</span></span>

## <a name="batching-scenarios"></a><span data-ttu-id="97901-412">일괄 처리 시나리오</span><span class="sxs-lookup"><span data-stu-id="97901-412">Batching scenarios</span></span>
<span data-ttu-id="97901-413">다음 섹션은 세 개의 응용 프로그램 시나리오에서 테이블 반환 매개 변수를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-413">The following sections describe how to use table-valued parameters in three application scenarios.</span></span> <span data-ttu-id="97901-414">첫 번째 시나리오는 버퍼링과 일괄 처리가 함께 작업할 수 있는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="97901-414">The first scenario shows how buffering and batching can work together.</span></span> <span data-ttu-id="97901-415">두 번째 시나리오는 하나의 저장 프로시저 호출로 마스터-세부 정보 작업 수행하여 성능을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="97901-415">The second scenario improves performance by performing master-detail operations in a single stored procedure call.</span></span> <span data-ttu-id="97901-416">마지막 시나리오는 “UPSERT” 작업에서 테이블 반환 매개 변수를 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="97901-416">The final scenario shows how to use table-valued parameters in an “UPSERT” operation.</span></span>

### <a name="buffering"></a><span data-ttu-id="97901-417">버퍼링</span><span class="sxs-lookup"><span data-stu-id="97901-417">Buffering</span></span>
<span data-ttu-id="97901-418">일괄 처리가 확실히 적합할 만한 시나리오가 있기는 하지만 지연 처리를 통한 일괄 처리를 활용할 수 있는 시나리오는 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-418">Although there are some scenarios that are obvious candidate for batching, there are many scenarios that could take advantage of batching by delayed processing.</span></span> <span data-ttu-id="97901-419">하지만 지연 처리는 예기치 않은 오류가 발생하면 데이터가 손실되는 등의 큰 위험이 수반됩니다.</span><span class="sxs-lookup"><span data-stu-id="97901-419">However, delayed processing also carries a greater risk that the data is lost in the event of an unexpected failure.</span></span> <span data-ttu-id="97901-420">이러한 위험을 이해하고 그에 따른 결과를 고려하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-420">It is important to understand this risk and consider the consequences.</span></span>

<span data-ttu-id="97901-421">예를 들어, 각 사용자의 탐색 내역을 추적하는 응용 프로그램을 생각해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-421">For example, consider a web application that tracks the navigation history of each user.</span></span> <span data-ttu-id="97901-422">각 페이지 요청에 대해, 응용 프로그램은 사용자의 페이지 보기를 기록하기 위한 데이터베이스 호출을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-422">On each page request, the application could make a database call to record the user’s page view.</span></span> <span data-ttu-id="97901-423">하지만 사용자의 탐색 활동을 버퍼링한 후 이 데이터를 데이터베이스에 일괄 처리해서 보내면 보다 높은 성능과 확장성을 달성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-423">But higher performance and scalability can be achieved by buffering the users’ navigation activities and then sending this data to the database in batches.</span></span> <span data-ttu-id="97901-424">경과 시간 및/또는 버퍼 크기에 따라서 데이터베이스 업데이트를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-424">You can trigger the database update by elapsed time and/or buffer size.</span></span> <span data-ttu-id="97901-425">예를 들어, 20초 후에 배치가 처리되도록 하거나 버퍼의 항목이 1000개에 도달하면 배치가 처리되도록 규칙을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-425">For example, a rule could specify that the batch should be processed after 20 seconds or when the buffer reaches 1000 items.</span></span>

<span data-ttu-id="97901-426">다음 코드 예제는 모니터링 클래스에 의해 발생한 버퍼 이벤트를 처리하기 위해 [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-426">The following code example uses [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) to process buffered events raised by a monitoring class.</span></span> <span data-ttu-id="97901-427">버퍼가 차거나 제한 시간에 도달하면, 사용자 데이터 배치는 테이블 반환 매개 변수와 함께 데이터베이스로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="97901-427">When the buffer fills or a timeout is reached, the batch of user data is sent to the database with a table-valued parameter.</span></span>

<span data-ttu-id="97901-428">다음 NavHistoryData 클래스는 사용자 탐색 세부 정보를 모델링합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-428">The following NavHistoryData class models the user navigation details.</span></span> <span data-ttu-id="97901-429">사용자 ID, 액세스한 URL, 액세스 시간을 비롯한 기본 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-429">It contains basic information such as the user identifier, the URL accessed, and the access time.</span></span>

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

<span data-ttu-id="97901-430">NavHistoryDataMonitor 클래스는 사용자 탐색 데이터를 데이터베이스로 버퍼링하는 것을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-430">The NavHistoryDataMonitor class is responsible for buffering the user navigation data to the database.</span></span> <span data-ttu-id="97901-431">**OnAdded** 이벤트가 발생하면 응답하는RecordUserNavigationEntry라는 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-431">It contains a method, RecordUserNavigationEntry, which responds by raising an **OnAdded** event.</span></span> <span data-ttu-id="97901-432">다음 코드는 Rx를 사용하여 이벤트를 기반으로 관측 가능한 컬렉션을 만드는 생성자 논리를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="97901-432">The following code shows the constructor logic that uses Rx to create an observable collection based on the event.</span></span> <span data-ttu-id="97901-433">그 후 Buffer 메서드와 함께 관측 가능한 컬렉션을 구독합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-433">It then subscribes to this observable collection with the Buffer method.</span></span> <span data-ttu-id="97901-434">오버로드는 20초마다 또는 항목이 1000개가 될 때마다 버퍼가 전송되어야 한다는 것을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-434">The overload specifies that the buffer should be sent every 20 seconds or 1000 entries.</span></span>

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

<span data-ttu-id="97901-435">처리기는 버퍼링된 모든 항목을 테이블 반환 형식으로 변환한 후 이 형식을 배치를 처리하는 저장 프로시저로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-435">The handler converts all of the buffered items into a table-valued type and then passes this type to a stored procedure that processes the batch.</span></span> <span data-ttu-id="97901-436">다음 코드는 NavHistoryDataEventArgs 및 NavHistoryDataMonitor 클래스에 대한 전체 정의를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="97901-436">The following code shows the complete definition for both the NavHistoryDataEventArgs and the NavHistoryDataMonitor classes.</span></span>

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

<span data-ttu-id="97901-437">이 버퍼링 클래스를 사용하기 위해서 응용 프로그램은 정적 NavHistoryDataMonitor 개체를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-437">To use this buffering class, the application creates a static NavHistoryDataMonitor object.</span></span> <span data-ttu-id="97901-438">사용자가 페이지에 액세스할 때마다 응용 프로그램은 NavHistoryDataMonitor.RecordUserNavigationEntry 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-438">Each time a user accesses a page, the application calls the NavHistoryDataMonitor.RecordUserNavigationEntry method.</span></span> <span data-ttu-id="97901-439">버퍼링 논리는 이러한 항목의 데이터베이스에 대한 일괄 전송을 처리하도록 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="97901-439">The buffering logic proceeds to take care of sending these entries to the database in batches.</span></span>

### <a name="master-detail"></a><span data-ttu-id="97901-440">마스터-세부 정보</span><span class="sxs-lookup"><span data-stu-id="97901-440">Master detail</span></span>
<span data-ttu-id="97901-441">테이블 반환 매개 변수는 간단한 INSERT 시나리오에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-441">Table-valued parameters are useful for simple INSERT scenarios.</span></span> <span data-ttu-id="97901-442">하지만 두 개 이상의 테이블이 연관되는 일괄 처리 삽입은 더 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-442">However, it can be more challenging to batch inserts that involve more than one table.</span></span> <span data-ttu-id="97901-443">“마스터/세부 정보” 시나리오가 좋은 예입니다.</span><span class="sxs-lookup"><span data-stu-id="97901-443">The “master/detail” scenario is a good example.</span></span> <span data-ttu-id="97901-444">마스터 테이블은 기본 엔터티를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-444">The master table identifies the primary entity.</span></span> <span data-ttu-id="97901-445">하나 이상의 세부 정보 테이블은 엔터티에 대한 데이터를 더 많이 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-445">One or more detail tables store more data about the entity.</span></span> <span data-ttu-id="97901-446">이 시나리오에서 외래 키 관계는 고유 마스터 엔터티에 세부 정보의 관계를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-446">In this scenario, foreign key relationships enforce the relationship of details to a unique master entity.</span></span> <span data-ttu-id="97901-447">PurchaseOrder 테이블의 간소화된 버전 및 그와 연결된 OrderDetail 테이블을 생각해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-447">Consider a simplified version of a PurchaseOrder table and its associated OrderDetail table.</span></span> <span data-ttu-id="97901-448">다음 Transact-SQL은 4개의 열 즉 OrderID, OrderDate, CustomerID, Status를 포함하는 PurchaseOrder 테이블을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-448">The following Transact-SQL creates the PurchaseOrder table with four columns: OrderID, OrderDate, CustomerID, and Status.</span></span>

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

<span data-ttu-id="97901-449">각각의 주문은 하나 이상의 제품 구매를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-449">Each order contains one or more product purchases.</span></span> <span data-ttu-id="97901-450">이 정보는 PurchaseOrderDetail 테이블에 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="97901-450">This information is captured in the PurchaseOrderDetail table.</span></span> <span data-ttu-id="97901-451">다음 Transact-SQL은 5개의 열 즉, OrderID, OrderDetailID, ProductID, UnitPrice, OrderQty를 포함하는 PurchaseOrderDetail 테이블을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-451">The following Transact-SQL creates the PurchaseOrderDetail table with five columns: OrderID, OrderDetailID, ProductID, UnitPrice, and OrderQty.</span></span>

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

<span data-ttu-id="97901-452">PurchaseOrderDetail 테이블의 OrderID 열은 PurchaseOrder 테이블에서 주문을 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-452">The OrderID column in the PurchaseOrderDetail table must reference an order from the PurchaseOrder table.</span></span> <span data-ttu-id="97901-453">외래 키에 대한 다음 정의가 이 제약 조건에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="97901-453">The following definition of a foreign key enforces this constraint.</span></span>

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

<span data-ttu-id="97901-454">테이블 반환 매개 변수를 사용하려면 각 대상 테이블에 대해 하나의 사용자 정의 테이블 형식이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-454">In order to use table-valued parameters, you must have one user-defined table type for each target table.</span></span>

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

<span data-ttu-id="97901-455">그 후 이런 형식의 테이블을 허용하는 저장 프로시저를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-455">Then define a stored procedure that accepts tables of these types.</span></span> <span data-ttu-id="97901-456">이 프로시저는 응용 프로그램이 단일 호출로 주문 집합 및 주문 세부 정보를 로컬에서 일괄 처리하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-456">This procedure allows an application to locally batch a set of orders and order details in a single call.</span></span> <span data-ttu-id="97901-457">다음 Transact-SQL은 이 구매 주문 예제에 대한 저장 프로시저 선언 전체를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-457">The following Transact-SQL provides the complete stored procedure declaration for this purchase order example.</span></span>

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects the order identifiers in the @orders
    -- table with the actual order identifiers in the PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders to the PurchaseOrder table, storing the actual
    -- order identifiers in the @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match the passed-in order identifiers with the actual identifiers
    -- and complete the @IdentityLink table for use with inserting the details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert the order details into the PurchaseOrderDetail table, 
          -- using the actual order identifiers of the master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

<span data-ttu-id="97901-458">이 예제에서 로컬에 정의된 @IdentityLink 테이블은 새로 삽입된 행의 실제 OrderID 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-458">In this example, the locally defined @IdentityLink table stores the actual OrderID values from the newly inserted rows.</span></span> <span data-ttu-id="97901-459">이 주문 ID는 @orders 및 @details 테이블 반환 매개 변수의 임시 OrderID 값과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="97901-459">These order identifiers are different from the temporary OrderID values in the @orders and @details table-valued parameters.</span></span> <span data-ttu-id="97901-460">이런 이유 때문에 @IdentityLink 테이블은 @orders 매개 변수의 OrderID 값을 PurchaseOrder 테이블의 새로운 행에 대한 실제 OrderID 값에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-460">For this reason, the @IdentityLink table then connects the OrderID values from the @orders parameter to the real OrderID values for the new rows in the PurchaseOrder table.</span></span> <span data-ttu-id="97901-461">이 단계에서 @IdentityLink 테이블은 외래 키 제약 조건을 충족하는 실제 OrderID로 주문 세부 정보를 삽입하는데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-461">After this step, the @IdentityLink table can facilitate inserting the order details with the actual OrderID that satisfies the foreign key constraint.</span></span>

<span data-ttu-id="97901-462">저장된 프로시저는 코드 또는 기타 Transact-SQL 호출에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-462">This stored procedure can be used from code or from other Transact-SQL calls.</span></span> <span data-ttu-id="97901-463">코드 예제는 이 문서의 테이블 반환 매개 변수 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97901-463">See the table-valued parameters section of this paper for a code example.</span></span> <span data-ttu-id="97901-464">다음 Transact-SQL은 sp_InsertOrdersBatch를 호출하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="97901-464">The following Transact-SQL shows how to call the sp_InsertOrdersBatch.</span></span>

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

<span data-ttu-id="97901-465">이 솔루션은 각 배치가 1로 시작하는 OrderID 값 집합을 사용하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-465">This solution allows each batch to use a set of OrderID values that begin at 1.</span></span> <span data-ttu-id="97901-466">임시 OrderID 값은 이 배치의 관계를 설명하지만 실제 OrderID 값은 삽입 작업 시에 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="97901-466">These temporary OrderID values describe the relationships in the batch, but the actual OrderID values are determined at the time of the insert operation.</span></span> <span data-ttu-id="97901-467">이전 예제와 같은 명령문을 반복해서 실행하고 데이터베이스에 고유한 주문을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-467">You can run the same statements in the previous example repeatedly and generate unique orders in the database.</span></span> <span data-ttu-id="97901-468">이런 이유 때문에 일괄 처리 기법을 사용할 때는 중복 주문을 방지하는 코드 또는 데이터베이스 논리를 더 추가하는 것을 고려하는 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-468">For this reason, consider adding more code or database logic that prevents duplicate orders when using this batching technique.</span></span>

<span data-ttu-id="97901-469">이 예제는 훨씬 더 복잡한 데이터베이스 작업(예: 마스터-세부 정보 작업)도 테이블 반환 매개 변수를 사용하여 일괄 처리가 가능하다는 것을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="97901-469">This example demonstrates that even more complex database operations, such as master-detail operations, can be batched using table-valued parameters.</span></span>

### <a name="upsert"></a><span data-ttu-id="97901-470">UPSERT</span><span class="sxs-lookup"><span data-stu-id="97901-470">UPSERT</span></span>
<span data-ttu-id="97901-471">다른 일괄 작업 시나리오는 동시에 기존 행을 업데이트하고 새 행을 삽입하는 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-471">Another batching scenario involves simultaneously updating existing rows and inserting new rows.</span></span> <span data-ttu-id="97901-472">이 작업은 “UPSERT”(update + insert) 작업이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-472">This operation is sometimes referred to as an “UPSERT” (update + insert) operation.</span></span> <span data-ttu-id="97901-473">이 작업에 INSERT 및 UPDATE에 대한 호출을 따로 생성하기 보다는 MERGE 문이 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-473">Rather than making separate calls to INSERT and UPDATE, the MERGE statement is best suited to this task.</span></span> <span data-ttu-id="97901-474">MERGE 문은 삽입과 업데이트 작업을 단일 호출로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-474">The MERGE statement can perform both insert and update operations in a single call.</span></span>

<span data-ttu-id="97901-475">테이블 반환 매개 변수가 MERGE 문과 함께 사용되어 업데이트와 삽입을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-475">Table-valued parameters can be used with the MERGE statement to perform updates and inserts.</span></span> <span data-ttu-id="97901-476">예를 들어 EmployeeID, FirstName, LastName, SocialSecurityNumber 열을 포함하는 간소화된 Employee 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-476">For example, consider a simplified Employee table that contains the following columns: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span></span>

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

<span data-ttu-id="97901-477">이 예제에서 여러 직원의 MERGE를 수행하기 위해 SocialSecurityNumber 가 고유하다는 사실을 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-477">In this example, you can use the fact that the SocialSecurityNumber is unique to perform a MERGE of multiple employees.</span></span> <span data-ttu-id="97901-478">우선, 사용자 정의 테이블 형식을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97901-478">First, create the user-defined table type:</span></span>

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

<span data-ttu-id="97901-479">다음으로, 업데이트 및 삽입을 수행하기 위해 MERGE 문을 사용하는 코드를 작성하거나 저장 프로시저를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97901-479">Next, create a stored procedure or write code that uses the MERGE statement to perform the update and insert.</span></span> <span data-ttu-id="97901-480">다음 예제는 EmployeeTableType 형식의 @employees 테이블 반환 매개 변수에 MERGE 문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-480">The following example uses the MERGE statement on a table-valued parameter, @employees, of type EmployeeTableType.</span></span> <span data-ttu-id="97901-481">@employees 테이블의 내용은 여기에 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-481">The contents of the @employees table are not shown here.</span></span>

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

<span data-ttu-id="97901-482">자세한 내용은 MERGE 문에 대한 설명서 또는 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97901-482">For more information, see the documentation and examples for the MERGE statement.</span></span> <span data-ttu-id="97901-483">동일한 작업이 별도의 INSERT 및 UPDATE 작업을 포함하는 여러 단계의 저장 프로시저로 수행될 수 있지만 MERGE 문이 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="97901-483">Although the same work could be performed in a multiple-step stored procedure call with separate INSERT and UPDATE operations, the MERGE statement is more efficient.</span></span> <span data-ttu-id="97901-484">데이터베이스 코드는 INSERT 및 UPDATE에 대한 두 개의 데이터베이스 호출 없이도 MERGE 문을 바로 사용하는 Transact-SQL 호출을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-484">Database code can also construct Transact-SQL calls that use the MERGE statement directly without requiring two database calls for INSERT and UPDATE.</span></span>

## <a name="recommendation-summary"></a><span data-ttu-id="97901-485">권장 사항 요약</span><span class="sxs-lookup"><span data-stu-id="97901-485">Recommendation summary</span></span>
<span data-ttu-id="97901-486">다음 목록은 이 문서에 논의된 일괄 작업 권장 사항에 대한 요약을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-486">The following list provides a summary of the batching recommendations discussed in this topic:</span></span>

* <span data-ttu-id="97901-487">SQL 데이터베이스 응용 프로그램의 성능과 확장성을 높이려면 버퍼링 및 일괄 처리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-487">Use buffering and batching to increase the performance and scalability of SQL Database applications.</span></span>
* <span data-ttu-id="97901-488">일괄 처리/버퍼링과 복원력 사이의 균형 유지(상쇄)를 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-488">Understand the tradeoffs between batching/buffering and resiliency.</span></span> <span data-ttu-id="97901-489">역할에 오류가 발생하면, 중요한 비즈니스 데이터를 처리하지 않은 배치 파일을 손실할 위험이 일괄 처리 성능의 이점을 능가합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-489">During a role failure, the risk of losing an unprocessed batch of business-critical data might outweigh the performance benefit of batching.</span></span>
* <span data-ttu-id="97901-490">대기 시간을 줄이기 위해 단일 데이터 센터 내에 데이터베이스에 대한 모든 호출을 유지하도록 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-490">Attempt to keep all calls to the database within a single datacenter to reduce latency.</span></span>
* <span data-ttu-id="97901-491">단일 일괄 처리 기법을 선택하는 경우, 테이블 반환 매개 변수가 최고의 성능 및 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-491">If you choose a single batching technique, table-valued parameters offer the best performance and flexibility.</span></span>
* <span data-ttu-id="97901-492">최고의 삽입 성능을 위해 아래의 일반적인 지침을 따르되 사용자의 시나리오를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-492">For the fastest insert performance, follow these general guidelines but test your scenario:</span></span>
  * <span data-ttu-id="97901-493">행이 100개 미만이면 단일 매개 변수가 있는 INSERT 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-493">For < 100 rows, use a single parameterized INSERT command.</span></span>
  * <span data-ttu-id="97901-494">행이 1000개 미만이면 테이블 반환 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-494">For < 1000 rows, use table-valued parameters.</span></span>
  * <span data-ttu-id="97901-495">행이 1000개 이상이면 SqlBulkCopy를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-495">For >= 1000 rows, use SqlBulkCopy.</span></span>
* <span data-ttu-id="97901-496">업데이트 및 삭제 작업의 경우 테이블 매개 변수의 각 행에 대해 올바른 작업을 결정하는 저장 프로시저 논리와 함께 테이블 반환 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-496">For update and delete operations, use table-valued parameters with stored procedure logic that determines the correct operation on each row in the table parameter.</span></span>
* <span data-ttu-id="97901-497">배치 크기 지침:</span><span class="sxs-lookup"><span data-stu-id="97901-497">Batch size guidelines:</span></span>
  * <span data-ttu-id="97901-498">사용자의 응용 프로그램 및 비즈니스 요구 사항에 합당한 최대 배치 크기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-498">Use the largest batch sizes that make sense for your application and business requirements.</span></span>
  * <span data-ttu-id="97901-499">대형 배치의 성능 향상과 임시 오류 또는 치명적인 오류의 위험 사이에서 균형을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-499">Balance the performance gain of large batches with the risks of temporary or catastrophic failures.</span></span> <span data-ttu-id="97901-500">재시도 또는 배치 파일에 포함된 데이터 손실의 결과(대가)는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="97901-500">What is the consequence of retries or loss of the data in the batch?</span></span> 
  * <span data-ttu-id="97901-501">SQL 데이터베이스가 배치를 거부하지 않는지 확인하기 위해 큰 규모의 배치를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-501">Test the largest batch size to verify that SQL Database does not reject it.</span></span>
  * <span data-ttu-id="97901-502">배치 크기 또는 버퍼링 시간대와 같이 일괄 처리를 제어하는 구성 설정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97901-502">Create configuration settings that control batching, such as the batch size or the buffering time window.</span></span> <span data-ttu-id="97901-503">이러한 설정은 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-503">These settings provide flexibility.</span></span> <span data-ttu-id="97901-504">클라우드 서비스를 다시 배포하지 않고도 프로덕션에서 일괄 처리 동작을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-504">You can change the batching behavior in production without redeploying the cloud service.</span></span>
* <span data-ttu-id="97901-505">단일 데이터베이스의 단일 테이블에서 작동하는 배치를 병렬로 실행하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-505">Avoid parallel execution of batches that operate on a single table in one database.</span></span> <span data-ttu-id="97901-506">그렇게 하는 경우에는 여러 작업자 스레드의 단일 배치를 나누고 테스트를 실행하여 이상적인 스레드의 개수를 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-506">If you do choose to divide a single batch across multiple worker threads, run tests to determine the ideal number of threads.</span></span> <span data-ttu-id="97901-507">스레드가 지정되지 않으면 더 많은 스레드가 성능을 높이기 보다는 감소시킵니다.</span><span class="sxs-lookup"><span data-stu-id="97901-507">After an unspecified threshold, more threads will decrease performance rather than increase it.</span></span>
* <span data-ttu-id="97901-508">보다 많은 시나리오에 일괄 처리를 구현하는 방법으로 크기 및 시간에 따른 버퍼링을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-508">Consider buffering on size and time as a way of implementing batching for more scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97901-509">다음 단계</span><span class="sxs-lookup"><span data-stu-id="97901-509">Next steps</span></span>
<span data-ttu-id="97901-510">이 문서는 일괄 처리와 관련된 데이터베이스 디자인과 코딩 기법이 응용 프로그램 성능과 확장성을 향상시킬 수 있는 방법에 중점을 두고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97901-510">This article focused on how database design and coding techniques related to batching can improve your application performance and scalability.</span></span> <span data-ttu-id="97901-511">하지만 이것은 사용자의 전반적인 전략 중 한 가지 요소에 불과합니다.</span><span class="sxs-lookup"><span data-stu-id="97901-511">But this is just one factor in your overall strategy.</span></span> <span data-ttu-id="97901-512">성능과 확장성을 개선하는 방법을 더 보려면 [단일 데이터베이스의 Azure SQL Database 성능 지침](sql-database-performance-guidance.md) 및 [탄력적 풀의 가격 및 성능 고려 사항](sql-database-elastic-pool-guidance.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97901-512">For more ways to improve performance and scalability, see [Azure SQL Database performance guidance for single databases](sql-database-performance-guidance.md) and [Price and performance considerations for an elastic pool](sql-database-elastic-pool-guidance.md).</span></span>


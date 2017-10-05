---
title: "SQL 연결 오류 해결, 일시적 오류 | Microsoft Azure Docs"
description: "SQL 연결 오류 또는 Azure SQL 데이터베이스의 일시적 오류를 해결, 진단 및 방지하는 방법을 알아봅니다. "
keywords: "SQL 연결, 연결 문자열, 연결 문제, 일시적인 오류, 연결 오류"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: efb35451-3fed-4264-bf86-72b350f67d50
ms.service: sql-database
ms.custom: develop apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: ae081fc0432e36bf9f4d4f06f289386ddce37990
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a><span data-ttu-id="053ec-104">SQL 연결 오류와 일시적 SQL 데이터베이스 오류의 문제 해결, 진단 및 예방</span><span class="sxs-lookup"><span data-stu-id="053ec-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span></span>
<span data-ttu-id="053ec-105">이 문서에서는 클라이언트 응용 프로그램이 Azure SQL 데이터베이스와 상호 작용할 때 발생하는 연결 오류 및 일시적 오류를 방지, 해결, 진단, 완화하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-105">This article describes how to prevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span></span> <span data-ttu-id="053ec-106">재시도 논리를 구성하고 연결 문자열을 빌드하며 타 연결 설정을 조정하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-106">Learn how to configure retry logic, build the connection string, and adjust other connection settings.</span></span>

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a><span data-ttu-id="053ec-107">일시적인 오류(일시 장애)</span><span class="sxs-lookup"><span data-stu-id="053ec-107">Transient errors (transient faults)</span></span>
<span data-ttu-id="053ec-108">일시적인 오류(일시 결함)에는 자체적으로 신속히 환익되는 원인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-108">A transient error - also, transient fault - has an underlying cause that will soon resolve itself.</span></span> <span data-ttu-id="053ec-109">일시적 오류가 발생하는 이유는 가끔 Azure 시스템에서 다양한 워크로드의 부하를 더 효율적으로 분산하기 위해 하드웨어를 신속하게 변경하는 경우가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-109">An occasional cause of transient errors is when the Azure system quickly shifts hardware resources to better load-balance various workloads.</span></span> <span data-ttu-id="053ec-110">이러한 재구성 이벤트는 대부분 60초 이내에 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-110">Most of these reconfiguration events often complete in less than 60 seconds.</span></span> <span data-ttu-id="053ec-111">이 재구성 기간 중에는 Azure SQL 데이터베이스에 대한 연결에 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-111">During this reconfiguration time span, you may have connectivity issues to Azure SQL Database.</span></span> <span data-ttu-id="053ec-112">Azure SQL 데이터베이스에 연결되는 응용 프로그램은 이러한 일시적인 오류를 예상하고 사용자에게 응용 프로그램 오류로 표시하는 대신 코드에 재시도 논리를 구현하여 처리하도록 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-112">Applications connecting to Azure SQL Database should be built to expect these transient errors, handle them by implementing retry logic in their code instead of surfacing them to users as application errors.</span></span>

<span data-ttu-id="053ec-113">클라이언트 프로그램에서 ADO.NET을 사용하는 경우 사용자 프로그램에 **SqlException**이 throw되어 일시적 오류가 발생했다는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-113">If your client program is using ADO.NET, your program is told about the transient error by the throw of an **SqlException**.</span></span> <span data-ttu-id="053ec-114">**숫자** 속성을 본 항목 윗부분의 [SQL 데이터베이스 클라이언트 응용 프로그램의 SQL 오류 메시지](sql-database-develop-error-messages.md)에서 나열된 일시적 오류 목록과 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-114">The **Number** property can be compared against the list of transient errors near the top of the topic: [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="053ec-115">연결과 명령 비교</span><span class="sxs-lookup"><span data-stu-id="053ec-115">Connection versus command</span></span>
<span data-ttu-id="053ec-116">다음에 따라, SQL 연결을 다시 시도하거나 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-116">You'll retry the SQL connection or establish it again, depending on the following:</span></span>

* <span data-ttu-id="053ec-117">**연결 시도 중 일시적 오류가 발생할 경우**: 몇 초 지연한 후에 연결을 다시 시도해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-117">**A transient error occurs during a connection try**: The connection should be retried after delaying for several seconds.</span></span>
* <span data-ttu-id="053ec-118">**SQL 쿼리 명령 중에 일시적 오류가 발생할 경우**: 명령을 즉시 다시 시도하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-118">**A transient error occurs during a SQL query command**: The command should not be immediately retried.</span></span> <span data-ttu-id="053ec-119">대신, 지연 후에 연결을 새로 고쳐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-119">Instead, after a delay, the connection should be freshly established.</span></span> <span data-ttu-id="053ec-120">그런 다음 명령을 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-120">Then the command can be retried.</span></span>

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a><span data-ttu-id="053ec-121">일시적인 오류에 대한 재시도 논리</span><span class="sxs-lookup"><span data-stu-id="053ec-121">Retry logic for transient errors</span></span>
<span data-ttu-id="053ec-122">간혹 일시적 오류가 발생하는 클라이언트 프로그램에 재시도 논리가 포함된 경우 더욱 견고해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-122">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span></span>

<span data-ttu-id="053ec-123">프로그램이 타사 미들웨어를 통해 Azure SQL 데이터베이스와 통신하는 경우 공급업체에 문의하여 미들웨어에 일시적 오류에 대한 재시도 논리가 포함되어 있는지 여부를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-123">When your program communicates with Azure SQL Database through a 3rd party middleware, inquire with the vendor whether the middleware contains retry logic for transient errors.</span></span>

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a><span data-ttu-id="053ec-124">재시도 원칙</span><span class="sxs-lookup"><span data-stu-id="053ec-124">Principles for retry</span></span>
* <span data-ttu-id="053ec-125">오류가 일시적인 경우 연결을 다시 시도해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-125">An attempt to open a connection should be retried if the error is transient.</span></span>
* <span data-ttu-id="053ec-126">일시적 오류로 실패하는 SQL SELECT 문은 직접 다시 시도하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-126">A SQL SELECT statement that fails with a transient error should not be retried directly.</span></span>
  
  * <span data-ttu-id="053ec-127">대신, 새로 연결한 다음 SELECT를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-127">Instead, establish a fresh connection, and then retry the SELECT.</span></span>
* <span data-ttu-id="053ec-128">일시적 오류로 인해 SQL UPDATE 문이 실패할 경우 UPDATE를 다시 시도하기 전에 새로 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-128">When a SQL UPDATE statement fails with a transient error, a fresh connection should be established before the UPDATE is retried.</span></span>
  
  * <span data-ttu-id="053ec-129">재시도 논리는 전체 데이터베이스 트랜잭션이 완료되었는지 또는 전체 트랜잭션이 롤백되었는지 여부를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-129">The retry logic must ensure that either the entire database transaction completed, or that the entire transaction is rolled back.</span></span>

#### <a name="other-considerations-for-retry"></a><span data-ttu-id="053ec-130">재시도에 대한 기타 고려 사항</span><span class="sxs-lookup"><span data-stu-id="053ec-130">Other considerations for retry</span></span>
* <span data-ttu-id="053ec-131">업무 시간 후 자동으로 시작되어 아침 전까지 완료되는 배치 프로그램은 재시도 간격을 길게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-131">A batch program that is automatically started after work hours, and which will complete before morning, can afford to very patient with long time intervals between its retry attempts.</span></span>
* <span data-ttu-id="053ec-132">사용자 인터페이스 프로그램은 기다리는 시간이 길 때 사용자가 포기하는 경향이 있는지를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-132">A user interface program should account for the human tendency to give up after too long a wait.</span></span>
  
  * <span data-ttu-id="053ec-133">하지만 몇 초마다 재시도하는 정책을 사용할 경우 시스템의 요청 수가 너무 많아지므로 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-133">However, the solution must not be to retry every few seconds, because that policy can flood the system with requests.</span></span>

#### <a name="interval-increase-between-retries"></a><span data-ttu-id="053ec-134">재시도 간격 증가</span><span class="sxs-lookup"><span data-stu-id="053ec-134">Interval increase between retries</span></span>
<span data-ttu-id="053ec-135">첫 번째 재시도 전에 5초간 지연하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-135">We recommend that you delay for 5 seconds before your first retry.</span></span> <span data-ttu-id="053ec-136">5초보다 짧은 지연 후 재시도는 클라우드 서비스에 많은 위험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-136">Retrying after a delay shorter than 5 seconds risks overwhelming the cloud service.</span></span> <span data-ttu-id="053ec-137">각 후속 재시도에 대해 지연 시간은 최대 60초까지 기하급수적으로 증가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-137">For each subsequent retry the delay should grow exponentially, up to a maximum of 60 seconds.</span></span>

<span data-ttu-id="053ec-138">ADO.NET을 사용하는 클라이언트에 대한 *차단 기간* 의 설명은 [SQL Server 연결 풀링(ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx)에서 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-138">A discussion of the *blocking period* for clients that use ADO.NET is available in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span></span>

<span data-ttu-id="053ec-139">또한 프로그램이 자체적으로 종료하기 전까지 최대 재시도 횟수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-139">You might also want to set a maximum number of retries before the program self-terminates.</span></span>

#### <a name="code-samples-with-retry-logic"></a><span data-ttu-id="053ec-140">재시도 논리가 포함된 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="053ec-140">Code samples with retry logic</span></span>
<span data-ttu-id="053ec-141">재시도 논리가 포함된 코드 샘플은 다음에서 다양한 언어로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-141">Code samples with retry logic, in a variety of programming languages, are available at:</span></span>

* [<span data-ttu-id="053ec-142">SQL 데이터베이스 및 SQL Server용 연결 라이브러리</span><span class="sxs-lookup"><span data-stu-id="053ec-142">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a><span data-ttu-id="053ec-143">재시도 논리 테스트</span><span class="sxs-lookup"><span data-stu-id="053ec-143">Test your retry logic</span></span>
<span data-ttu-id="053ec-144">재시도 논리를 테스트하려면 프로그램이 실행 중인 동안 수정할 수 있는 오류를 일으키거나 시뮬레이션해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-144">To test your retry logic, you must simulate or cause an error than can be corrected while your program is still running.</span></span>

##### <a name="test-by-disconnecting-from-the-network"></a><span data-ttu-id="053ec-145">네트워크에서 연결을 끊고 테스트</span><span class="sxs-lookup"><span data-stu-id="053ec-145">Test by disconnecting from the network</span></span>
<span data-ttu-id="053ec-146">재시도 논리를 테스트할 수 있는 한 가지 방법은 프로그램이 실행되는 동안 네트워크에서 클라이언트 컴퓨터 연결을 끊는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-146">One way you can test your retry logic is to disconnect your client computer from the network while the program is running.</span></span> <span data-ttu-id="053ec-147">오류는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-147">The error will be:</span></span>

* <span data-ttu-id="053ec-148">**SqlException.Number** = 11001</span><span class="sxs-lookup"><span data-stu-id="053ec-148">**SqlException.Number** = 11001</span></span>
* <span data-ttu-id="053ec-149">메시지: "해당 호스트가 없습니다"</span><span class="sxs-lookup"><span data-stu-id="053ec-149">Message: "No such host is known"</span></span>

<span data-ttu-id="053ec-150">프로그램은 첫 번째 재시도 중 오타를 수정한 다음 연결을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-150">As part of the first retry attempt, your program can correct the misspelling, and then attempt to connect.</span></span>

<span data-ttu-id="053ec-151">실제로 이 방법을 사용하려면 프로그램을 시작하기 전에 네트워크와 컴퓨터 간 케이블을 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-151">To make this practical, you unplug your computer from the network before you start your program.</span></span> <span data-ttu-id="053ec-152">그러면 프로그램에서 프로그램이 다음과 같이 작동하는 런타임 매개 변수를 인식합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-152">Then your program recognizes a run time parameter that causes the program to:</span></span>

1. <span data-ttu-id="053ec-153">오류 목록에 일시적 오류로 간주하기 위해 11001을 일시적으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-153">Temporarily add 11001 to its list of errors to consider as transient.</span></span>
2. <span data-ttu-id="053ec-154">평상 시와 같이 첫 번째 연결을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-154">Attempt its first connection as usual.</span></span>
3. <span data-ttu-id="053ec-155">오류가 확인되면 목록에서 11001을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-155">After the error is caught, remove 11001 from the list.</span></span>
4. <span data-ttu-id="053ec-156">사용자에게 컴퓨터를 네트워크에 연결하라는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-156">Display a message telling the user to plug the computer into the network.</span></span>
   * <span data-ttu-id="053ec-157">**Console.ReadLine** 메서드 또는 확인 단추가 포함된 대화 상자를 사용하여 추가 실행을 일시 정지합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-157">Pause further execution by using either the **Console.ReadLine** method or a dialog with an OK button.</span></span> <span data-ttu-id="053ec-158">사용자가 컴퓨터와 네트워크 간 케이블을 연결한 다음 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-158">The user presses the Enter key after the computer plugged into the network.</span></span>
5. <span data-ttu-id="053ec-159">다시 연결을 시도합니다. 정상적으로 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-159">Attempt again to connect, expecting success.</span></span>

##### <a name="test-by-misspelling-the-database-name-when-connecting"></a><span data-ttu-id="053ec-160">연결 시 틀린 철자의 데이터베이스 이름을 사용하여 테스트</span><span class="sxs-lookup"><span data-stu-id="053ec-160">Test by misspelling the database name when connecting</span></span>
<span data-ttu-id="053ec-161">프로그램이 첫 번째 연결 시도 전에 의도적으로 사용자 이름의 철자를 잘못 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-161">Your program can purposely misspell the user name before the first connection attempt.</span></span> <span data-ttu-id="053ec-162">오류는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-162">The error will be:</span></span>

* <span data-ttu-id="053ec-163">**SqlException.Number** = 18456</span><span class="sxs-lookup"><span data-stu-id="053ec-163">**SqlException.Number** = 18456</span></span>
* <span data-ttu-id="053ec-164">메시지: "사용자 'WRONG_MyUserName'에 대한 로그인에 실패했습니다."</span><span class="sxs-lookup"><span data-stu-id="053ec-164">Message: "Login failed for user 'WRONG_MyUserName'."</span></span>

<span data-ttu-id="053ec-165">프로그램은 첫 번째 재시도 중 오타를 수정한 다음 연결을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-165">As part of the first retry attempt, your program can correct the misspelling, and then attempt to connect.</span></span>

<span data-ttu-id="053ec-166">실제로 이 방법을 사용하기 위해 프로그램에서 프로그램이 다음과 같이 작동하는 런타임 매개 변수를 인식할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-166">To make this practical, your program could recognize a run time parameter that causes the program to:</span></span>

1. <span data-ttu-id="053ec-167">오류 목록에 일시적 오류로 간주하기 위해 18456을 일시적으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-167">Temporarily add 18456 to its list of errors to consider as transient.</span></span>
2. <span data-ttu-id="053ec-168">사용자 이름에 의도적으로 'WRONG_'을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-168">Purposely add 'WRONG_' to the user name.</span></span>
3. <span data-ttu-id="053ec-169">오류가 확인되면 목록에서 18456을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-169">After the error is caught, remove 18456 from the list.</span></span>
4. <span data-ttu-id="053ec-170">사용자 이름에서 'WRONG_'을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-170">Remove 'WRONG_' from the user name.</span></span>
5. <span data-ttu-id="053ec-171">다시 연결을 시도합니다. 정상적으로 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-171">Attempt again to connect, expecting success.</span></span>

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a><span data-ttu-id="053ec-172">연결 다시 시도에 대한 .NET SqlConnection 매개 변수</span><span class="sxs-lookup"><span data-stu-id="053ec-172">.NET SqlConnection parameters for connection retry</span></span>
<span data-ttu-id="053ec-173">클라이언트 프로그램이 .NET Framework 클래스 **System.Data.SqlClient.SqlConnection**를 사용하여 Azure SQL 데이터베이스에 연결되면 .NET 4.6.1 이상((또는 .NET Core)을 사용해야 하므로 해당 연결 다시 시도 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-173">If your client program connects to to Azure SQL Database by using the .NET Framework class **System.Data.SqlClient.SqlConnection**, you should use .NET 4.6.1 or later (or .NET Core) so you can leverage its connection retry feature.</span></span> <span data-ttu-id="053ec-174">기능의 자세한 내용은 [여기](http://go.microsoft.com/fwlink/?linkid=393996)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-174">Details of the feature are [here](http://go.microsoft.com/fwlink/?linkid=393996).</span></span>

<!--
2015-11-30, FwLink 393996 points to dn632678.aspx, which links to a downloadable .docx related to SqlClient and SQL Server 2014.
-->


<span data-ttu-id="053ec-175">[SqlConnection](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) 개체에 대한 **연결 문자열** 을 작성하는 경우 다음 매개 변수 중에서 값을 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-175">When you build the [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, you should coordinate the values among the following parameters:</span></span>

* <span data-ttu-id="053ec-176">ConnectRetryCount&nbsp;&nbsp;*(기본값은 1입니다.) 범위는 0에서 255입니다.)*</span><span class="sxs-lookup"><span data-stu-id="053ec-176">ConnectRetryCount &nbsp;&nbsp;*(Default is 1. Range is 0 through 255.)*</span></span>
* <span data-ttu-id="053ec-177">ConnectRetryInterval&nbsp;&nbsp;*(기본값은 1초입니다. 범위는 1에서 60입니다.)*</span><span class="sxs-lookup"><span data-stu-id="053ec-177">ConnectRetryInterval &nbsp;&nbsp;*(Default is 1 second. Range is 1 through 60.)*</span></span>
* <span data-ttu-id="053ec-178">연결 제한 시간&nbsp;&nbsp;*(기본값은 15초입니다. 범위는 0에서 2147483647입니다.)*</span><span class="sxs-lookup"><span data-stu-id="053ec-178">Connection Timeout &nbsp;&nbsp;*(Default is 15 seconds. Range is 0 through 2147483647)*</span></span>

<span data-ttu-id="053ec-179">특히 선택한 값은 다음 같음을 true로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-179">Specifically, your chosen values should make the following equality true:</span></span>

* <span data-ttu-id="053ec-180">연결 제한 시간 = ConnectRetryCount * ConnectionRetryInterval</span><span class="sxs-lookup"><span data-stu-id="053ec-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span></span>

<span data-ttu-id="053ec-181">예를 들어 개수 = 3 및 간격 = 10초인 경우 시간 제한이 29초이면 연결의 3번째 및 마지막 재시도에 대해 시스템에 충분한 시간을 제공하지 않게 됩니다. 29 < 3 * 10입니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-181">For example, if the count = 3, and interval = 10 seconds, a timeout of only 29 seconds would not quite give the system enough time for its 3rd and final retry at connecting: 29 < 3 * 10.</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="053ec-182">연결과 명령 비교</span><span class="sxs-lookup"><span data-stu-id="053ec-182">Connection versus command</span></span>
<span data-ttu-id="053ec-183">**ConnectRetryCount** 및 **ConnectRetryInterval** 매개 변수를 사용하면 **SqlConnection** 개체는 프로그램에 제어를 반환하는 등 프로그램에 전달하거나 신경 쓰지 않고 연결 작업을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-183">The **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry the connect operation without telling or bothering your program, such as returning control to your program.</span></span> <span data-ttu-id="053ec-184">다시 시도는 다음과 같은 상황에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-184">The retries can occur in the following situations:</span></span>

* <span data-ttu-id="053ec-185">mySqlConnection.Open 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="053ec-185">mySqlConnection.Open method call</span></span>
* <span data-ttu-id="053ec-186">mySqlConnection.Execute 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="053ec-186">mySqlConnection.Execute method call</span></span>

<span data-ttu-id="053ec-187">미묘한 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-187">There is a subtlety.</span></span> <span data-ttu-id="053ec-188">임시 오류가 발생할 경우 *쿼리* 가 실행되는 동안 **SqlConnection** 개체는 연결 작업을 다시 시도하지 않고 확실히 쿼리를 다시 시도하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-188">If a transient error occurs while your *query* is being executed, your **SqlConnection** object does not retry the connect operation, and it certainly does not retry your query.</span></span> <span data-ttu-id="053ec-189">그러나 **SqlConnection** 는 매우 신속하게 실행에 쿼리를 보내기 전에 연결을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-189">However, **SqlConnection** very quickly checks the connection before sending your query for execution.</span></span> <span data-ttu-id="053ec-190">빠른 검사가 연결 문제를 감지하면 **SqlConnection** 은 연결 작업을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-190">If the quick check detects a connection problem, **SqlConnection** retries the connect operation.</span></span> <span data-ttu-id="053ec-191">다시 시도가 성공하면 쿼리는 실행을 위해 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-191">If the retry succeeds, you query is sent for execution.</span></span>

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a><span data-ttu-id="053ec-192">ConnectRetryCount가 응용 프로그램 다시 시도 논리와 결합해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="053ec-192">Should ConnectRetryCount be combined with application retry logic?</span></span>
<span data-ttu-id="053ec-193">응용 프로그램에는 강력한 사용자 지정 다시 시도 논리가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-193">Suppose your application has robust custom retry logic.</span></span> <span data-ttu-id="053ec-194">연결 작업을 4번 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-194">It might retry the connect operation 4 times.</span></span> <span data-ttu-id="053ec-195">**ConnectRetryInterval** 및 **ConnectRetryCount** =3을 연결 문자열에 추가하는 경우 다시 시도 횟수가 4 * 3 = 12로 늘어납니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-195">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 to your connection string, you will increase the retry count to 4 * 3 = 12 retries.</span></span> <span data-ttu-id="053ec-196">이러한 많은 수의 다시 시도를 할 의도가 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-196">You might not intend such a high number of retries.</span></span>

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-to-azure-sql-database"></a><span data-ttu-id="053ec-197">Azure SQL 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="053ec-197">Connections to Azure SQL Database</span></span>
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a><span data-ttu-id="053ec-198">연결: 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="053ec-198">Connection: Connection string</span></span>
<span data-ttu-id="053ec-199">Azure SQL 데이터베이스에 연결하는 데 필요한 연결 문자열은 Microsoft SQL Server에 연결하기 위한 문자열과 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-199">The connection string necessary for connecting to Azure SQL Database is slightly different from the string for connecting to Microsoft SQL Server.</span></span> <span data-ttu-id="053ec-200">[Azure Portal](https://portal.azure.com/)에서 데이터베이스에 대한 연결 문자열을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-200">You can copy the connection string for your database from the [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a><span data-ttu-id="053ec-201">연결: IP 주소</span><span class="sxs-lookup"><span data-stu-id="053ec-201">Connection: IP address</span></span>
<span data-ttu-id="053ec-202">SQL 데이터베이스 서버가 사용자의 클라이언트 프로그램을 호스팅하는 컴퓨터의 IP 주소의 통신을 수락하도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-202">You must configure the SQL Database server to accept communication from the IP address of the computer that hosts your client program.</span></span> <span data-ttu-id="053ec-203">이 작업은 [Azure Portal](https://portal.azure.com/)에서 방화벽 설정을 편집하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-203">You do this by editing the firewall settings through the [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="053ec-204">IP 주소를 구성하지 않을 경우 프로그램이 실패하고 간단한 오류 메시지로 필요한 IP 주소를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-204">If you forget to configure the IP address, your program will fail with a handy error message that states the necessary IP address.</span></span>

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

<span data-ttu-id="053ec-205">자세한 내용은 [방법: SQL 데이터베이스에 방화벽 설정 구성](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="053ec-205">For more information, see: [How to: Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md)</span></span>

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a><span data-ttu-id="053ec-206">연결: 포트</span><span class="sxs-lookup"><span data-stu-id="053ec-206">Connection: Ports</span></span>
<span data-ttu-id="053ec-207">일반적으로 클라이언트 프로그램을 호스팅하는 컴퓨터에서 포트 1433이 아웃바운드 통신에 개방되어 있는지 여부만 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-207">Typically you only need to ensure that port 1433 is open for outbound communication, on the computer that hosts you client program.</span></span>

<span data-ttu-id="053ec-208">예를 들어 클라이언트 프로그램이 Windows 컴퓨터에 호스팅된 경우 호스트의 Windows 방화벽에서 포트 1433을 열 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-208">For example, when your client program is hosted on a Windows computer, the Windows Firewall on the host enables you to open port 1433:</span></span>

1. <span data-ttu-id="053ec-209">제어판</span><span class="sxs-lookup"><span data-stu-id="053ec-209">Open the Control Panel</span></span>
2. <span data-ttu-id="053ec-210">&gt; 모든 제어판 항목</span><span class="sxs-lookup"><span data-stu-id="053ec-210">&gt; All Control Panel Items</span></span>
3. <span data-ttu-id="053ec-211">&gt; Windows 방화벽</span><span class="sxs-lookup"><span data-stu-id="053ec-211">&gt; Windows Firewall</span></span>
4. <span data-ttu-id="053ec-212">&gt; 고급 설정</span><span class="sxs-lookup"><span data-stu-id="053ec-212">&gt; Advanced Settings</span></span>
5. <span data-ttu-id="053ec-213">&gt; 아웃바운드 규칙</span><span class="sxs-lookup"><span data-stu-id="053ec-213">&gt; Outbound Rules</span></span>
6. <span data-ttu-id="053ec-214">&gt; 작업</span><span class="sxs-lookup"><span data-stu-id="053ec-214">&gt; Actions</span></span>
7. <span data-ttu-id="053ec-215">&gt; 새 규칙</span><span class="sxs-lookup"><span data-stu-id="053ec-215">&gt; New Rule</span></span>

<span data-ttu-id="053ec-216">클라이언트 프로그램이 Azure VM(가상 컴퓨터)에 호스팅된 경우 </span><span class="sxs-lookup"><span data-stu-id="053ec-216">If your client program is hosted on an Azure virtual machine (VM), you should read:</span></span><br/><span data-ttu-id="053ec-217">[ADO.NET 4.5 및 SQL Database에 대한 1433 이외의 포트](sql-database-develop-direct-route-ports-adonet-v12.md)</span><span class="sxs-lookup"><span data-stu-id="053ec-217">[Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

<span data-ttu-id="053ec-218">포트 및 IP 주소 구성에 대한 배경 정보는 [Azure SQL 데이터베이스 방화벽](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="053ec-218">For background information about cofiguration of ports and IP address, see: [Azure SQL Database firewall](sql-database-firewall-configure.md)</span></span>

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a><span data-ttu-id="053ec-219">연결: ADO.NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="053ec-219">Connection: ADO.NET 4.6.1</span></span>
<span data-ttu-id="053ec-220">프로그램이 Azure SQL 데이터베이스에 연결하는 데 **System.Data.SqlClient.SqlConnection** 과 같은 ADO.NET 클래스를 사용할 경우 버전 4.6.1 이상의 .NET Framework를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** to connect to Azure SQL Database, we recommend that you use .NET Framework version 4.6.1 or higher.</span></span>

<span data-ttu-id="053ec-221">ADO.NET 4.6.1:</span><span class="sxs-lookup"><span data-stu-id="053ec-221">ADO.NET 4.6.1:</span></span>

* <span data-ttu-id="053ec-222">Azure SQL 데이터베이스의 경우 **SqlConnection.Open** 메서드를 사용하여 연결을 열 때 안정성 향상이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-222">For Azure SQL Database, there is improved reliability when you open a connection by using the **SqlConnection.Open** method.</span></span> <span data-ttu-id="053ec-223">**Open** 메서드는 이제 연결 제한 시간 내에 특정 오류에 대해 일시적인 오류에 대한 응답으로 최적의 재시도 메커니즘을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-223">The **Open** method now incorporates best effort retry mechanisms in response to transient faults, for certain errors within the Connection Timeout period.</span></span>
* <span data-ttu-id="053ec-224">연결 풀링을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-224">Supports connection pooling.</span></span> <span data-ttu-id="053ec-225">또한 프로그램에 제공하는 연결 개체가 올바르게 작동하는지를 효율적으로 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-225">This includes an efficient verification that the connection object it gives your program is functioning.</span></span>

<span data-ttu-id="053ec-226">연결 풀에서 연결 개체를 사용할 경우 바로 연결을 사용하지 않을 때 프로그램에서 연결을 일시적으로 닫는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-226">When you use a connection object from a connection pool, we recommend that your program temporarily close the connection when not immediately using it.</span></span> <span data-ttu-id="053ec-227">연결을 다시 열 경우 새로 연결하는 것만큼 많은 비용이 들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-227">Re-opening a connection is not expensive the way creating a new connection is.</span></span>

<span data-ttu-id="053ec-228">ADO.NET 4.0 이전 버전을 사용할 경우 최신 ADO.NET으로 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-228">If you are using ADO.NET 4.0 or earlier, we recommend that you upgrade to the latest ADO.NET.</span></span>

* <span data-ttu-id="053ec-229">2015년 11월 현재 [ADO.NET 4.6.1을 다운로드](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-229">As of November 2015, you can [download ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span></span>

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a><span data-ttu-id="053ec-230">진단</span><span class="sxs-lookup"><span data-stu-id="053ec-230">Diagnostics</span></span>
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a><span data-ttu-id="053ec-231">진단: 유틸리티에서 연결할 수 있는지 여부 테스트</span><span class="sxs-lookup"><span data-stu-id="053ec-231">Diagnostics: Test whether utilities can connect</span></span>
<span data-ttu-id="053ec-232">프로그램에서 Azure SQL 데이터베이스에 연결할 수 없을 경우 한 가지 진단 방법으로 유틸리티 프로그램에 연결해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-232">If your program is failing to connect to Azure SQL Database, one diagnostic option is to try to connect with a utility program.</span></span> <span data-ttu-id="053ec-233">유틸리티는 프로그램에서 사용하는 것과 동일한 라이브러리를 사용하여 연결하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-233">Ideally the utility would connect by using the same library that your program uses.</span></span>

<span data-ttu-id="053ec-234">모든 Windows 컴퓨터에서 이러한 유틸리티를 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-234">On any Windows computer, you can try these utilities:</span></span>

* <span data-ttu-id="053ec-235">ADO.NET을 사용하여 연결하는 SQL Server Management Studio(ssms.exe).</span><span class="sxs-lookup"><span data-stu-id="053ec-235">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET.</span></span>
* <span data-ttu-id="053ec-236">[ODBC](http://msdn.microsoft.com/library/jj730308.aspx)를 사용하여 연결하는 sqlcmd.exe.</span><span class="sxs-lookup"><span data-stu-id="053ec-236">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span></span>

<span data-ttu-id="053ec-237">연결된 후에는 짧은 SQL SELECT 쿼리가 작동하는지 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-237">Once connected, test whether a short SQL SELECT query works.</span></span>

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-the-open-ports"></a><span data-ttu-id="053ec-238">진단: 개방 포트 점검</span><span class="sxs-lookup"><span data-stu-id="053ec-238">Diagnostics: Check the open ports</span></span>
<span data-ttu-id="053ec-239">연결 시도가 실패하는 이유가 포트 문제 때문인 것으로 의심되는 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-239">Suppose you suspect that connection attempts are failing due to port issues.</span></span> <span data-ttu-id="053ec-240">컴퓨터에서 포트 구성에 대해 보고하는 유틸리티를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-240">On your computer you can run a utility that reports on the port configurations.</span></span>

<span data-ttu-id="053ec-241">Linux에서 다음 유틸리티는 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-241">On Linux the following utilities might be helpful:</span></span>

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * <span data-ttu-id="053ec-242">(IP 주소가 되도록 예제 값을 변경합니다.)</span><span class="sxs-lookup"><span data-stu-id="053ec-242">(Change the example value to be your IP address.)</span></span>

<span data-ttu-id="053ec-243">Windows에서는 [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) 유틸리티가 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-243">On Windows the [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span></span> <span data-ttu-id="053ec-244">다음은 Azure SQL 데이터베이스 서버에서 포트 상황에 대해 쿼리하기 위해 노트북 컴퓨터에서 실행한 실행 프로그램 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-244">Here is an example execution that queried the port situation on an Azure SQL Database server, and which was run on a laptop computer:</span></span>

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting to resolve name to IP address...
Name resolved to 23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a><span data-ttu-id="053ec-245">진단: 오류 기록</span><span class="sxs-lookup"><span data-stu-id="053ec-245">Diagnostics: Log your errors</span></span>
<span data-ttu-id="053ec-246">간헐적 문제는 며칠 또는 몇 주간 일반 패턴을 발견하여 진단하는 것이 가장 좋은 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span></span>

<span data-ttu-id="053ec-247">클라이언트에서 발생한 모든 오류를 기록하면 진단에 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-247">Your client can assist in a diagnosis by logging all errors it encounters.</span></span> <span data-ttu-id="053ec-248">로그 항목과 Azure SQL 데이터베이스에서 내부적으로 기록하는 오류 데이터의 상관 관계를 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-248">You might be able to correlate the log entries with error data that Azure SQL Database logs itself internally.</span></span>

<span data-ttu-id="053ec-249">Enterprise Library 6(EntLib60)은 로깅을 지원하기 위해 .NET 관리 클래스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-249">Enterprise Library 6 (EntLib60) offers .NET managed classes to assist with logging:</span></span>

* [<span data-ttu-id="053ec-250">5 - 간단한 응용 프로그램 블록 로깅 사용</span><span class="sxs-lookup"><span data-stu-id="053ec-250">5 - As Easy As Falling Off a Log: Using the Logging Application Block</span></span>](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a><span data-ttu-id="053ec-251">진단: 시스템 로그에서 오류 확인</span><span class="sxs-lookup"><span data-stu-id="053ec-251">Diagnostics: Examine system logs for errors</span></span>
<span data-ttu-id="053ec-252">다음은 오류 및 기타 정보를 쿼리하는 몇 가지 Transact-SQL SELECT 문입니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-252">Here are some Transact-SQL SELECT statements that query logs of error and other information.</span></span>

| <span data-ttu-id="053ec-253">로그 쿼리</span><span class="sxs-lookup"><span data-stu-id="053ec-253">Query of log</span></span> | <span data-ttu-id="053ec-254">설명</span><span class="sxs-lookup"><span data-stu-id="053ec-254">Description</span></span> |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |<span data-ttu-id="053ec-255">[sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) 보기는 일시적인 오류 또는 연결 실패를 일으킬 수 있는 일부를 포함하 여 개별 이벤트에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-255">The [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, including some that can cause transient errors or connectivity failures.</span></span><br/><br/><span data-ttu-id="053ec-256">이상적으로 **start_time** 또는 **end_time** 값을 클라이언트 프로그램에 문제가 발생하는 방법에 대한 정보와 함께 상호 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-256">Ideally you can correlate the **start_time** or **end_time** values with information about when your client program experienced problems.</span></span><br/><br/><span data-ttu-id="053ec-257">**팁:** **마스터** 데이터베이스에 연결하여 이를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-257">**TIP:** You must connect to the **master** database to run this.</span></span> |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |<span data-ttu-id="053ec-258">[sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) 보기는 추가 진단을 위해 이벤트 유형별로 집계된 개수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-258">The [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types, for additional diagnostics.</span></span><br/><br/><span data-ttu-id="053ec-259">**팁:** **마스터** 데이터베이스에 연결하여 이를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-259">**TIP:** You must connect to the **master** database to run this.</span></span> |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-the-sql-database-log"></a><span data-ttu-id="053ec-260">진단: SQL 데이터베이스 로그에서 문제 이벤트 검색</span><span class="sxs-lookup"><span data-stu-id="053ec-260">Diagnostics: Search for problem events in the SQL Database log</span></span>
<span data-ttu-id="053ec-261">Azure SQL 데이터베이스 로그에서 문제 이벤트에 대한 항목을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-261">You can search for entries about problem events in the log of Azure SQL Database.</span></span> <span data-ttu-id="053ec-262">**마스터** 데이터베이스에서 다음 Transact-SQL SELECT 문을 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="053ec-262">Try the following Transact-SQL SELECT statement in the **master** database:</span></span>

```
SELECT
   object_name
  ,CAST(f.event_data as XML).value
      ('(/event/@timestamp)[1]', 'datetime2')                      AS [timestamp]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="error"]/value)[1]', 'int')             AS [error]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="state"]/value)[1]', 'int')             AS [state]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="is_success"]/value)[1]', 'bit')        AS [is_success]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="database_name"]/value)[1]', 'sysname') AS [database_name]
FROM
  sys.fn_xe_telemetry_blob_target_read_file('el', null, null, null) AS f
WHERE
  object_name != 'login_event'  -- Login events are numerous.
  and
  '2015-06-21' < CAST(f.event_data as XML).value
        ('(/event/@timestamp)[1]', 'datetime2')
ORDER BY
  [timestamp] DESC
;
```


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a><span data-ttu-id="053ec-263">sys.fn_xe_telemetry_blob_target_read_file에서 반환된 몇 개 행</span><span class="sxs-lookup"><span data-stu-id="053ec-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span></span>
<span data-ttu-id="053ec-264">다음은 반환된 행을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-264">Next is what a returned row might look like.</span></span> <span data-ttu-id="053ec-265">여기에 표시된 null 값은 다른 행에서 null이 아닌 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-265">The null values shown are often not null in other rows.</span></span>

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a><span data-ttu-id="053ec-266">Enterprise Library 6</span><span class="sxs-lookup"><span data-stu-id="053ec-266">Enterprise Library 6</span></span>
<span data-ttu-id="053ec-267">Enterprise Library 6(EntLib60)은 Azure SQL 데이터베이스를 포함한 견고한 클라우드 서비스 클라이언트를 구현할 수 있는 .NET 클래스의 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is the Azure SQL Database service.</span></span> <span data-ttu-id="053ec-268">가장 먼저 다음을 참조하여 EntLib60을 이용할 수 있는 각 영역에 해당하는 항목을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-268">You can locate topics dedicated to each area in which EntLib60 can assist by first visiting:</span></span>

* [<span data-ttu-id="053ec-269">Enterprise Library 6 – 2013년 4월</span><span class="sxs-lookup"><span data-stu-id="053ec-269">Enterprise Library 6 - April 2013</span></span>](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

<span data-ttu-id="053ec-270">일시적 오류 처리에 대한 재시도 논리는 EntLib60을 이용할 수 있는 한 가지 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-270">Retry logic for handling transient errors is one area in which EntLib60 can assist:</span></span>

* [<span data-ttu-id="053ec-271">4 - 모든 성공의 인내와 비밀: 일시적 오류 처리 응용 프로그램 블록 사용</span><span class="sxs-lookup"><span data-stu-id="053ec-271">4 - Perseverance, Secret of All Triumphs: Using the Transient Fault Handling Application Block</span></span>](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> <span data-ttu-id="053ec-272">EntLib60에 대한 소스 코드는 공용 [다운로드](http://go.microsoft.com/fwlink/p/?LinkID=290898)에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-272">The source code for EntLib60 is available for public [download](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span></span> <span data-ttu-id="053ec-273">Microsoft는 EntLib에 추가 기능 또는 유지 관리를 업데이트할 계획이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-273">Microsoft has no plans to make further feature updates or maintenance updates to EntLib.</span></span>
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a><span data-ttu-id="053ec-274">일시적 오류 및 재시도용 EntLib60 클래스</span><span class="sxs-lookup"><span data-stu-id="053ec-274">EntLib60 classes for transient errors and retry</span></span>
<span data-ttu-id="053ec-275">다음 EntLib60 클래스는 특히 재시도 논리에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-275">The following EntLib60 classes are particularly useful for retry logic.</span></span> <span data-ttu-id="053ec-276">이러한 클래스는 모두 **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling** 네임스페이스에 있으며, 여기에 추가 클래스가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-276">All these  are in, or are further under, the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span></span>

<span data-ttu-id="053ec-277">**Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling** *네임스페이스:*</span><span class="sxs-lookup"><span data-stu-id="053ec-277">*In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span></span>

* <span data-ttu-id="053ec-278">**RetryPolicy** 클래스</span><span class="sxs-lookup"><span data-stu-id="053ec-278">**RetryPolicy** class</span></span>
  
  * <span data-ttu-id="053ec-279">**ExecuteAction** 메서드</span><span class="sxs-lookup"><span data-stu-id="053ec-279">**ExecuteAction** method</span></span>
* <span data-ttu-id="053ec-280">**ExponentialBackoff** 클래스</span><span class="sxs-lookup"><span data-stu-id="053ec-280">**ExponentialBackoff** class</span></span>
* <span data-ttu-id="053ec-281">**SqlDatabaseTransientErrorDetectionStrategy** 클래스</span><span class="sxs-lookup"><span data-stu-id="053ec-281">**SqlDatabaseTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="053ec-282">**ReliableSqlConnection** 클래스</span><span class="sxs-lookup"><span data-stu-id="053ec-282">**ReliableSqlConnection** class</span></span>
  
  * <span data-ttu-id="053ec-283">**ExecuteCommand** 메서드</span><span class="sxs-lookup"><span data-stu-id="053ec-283">**ExecuteCommand** method</span></span>

<span data-ttu-id="053ec-284">**Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**네임스페이스의</span><span class="sxs-lookup"><span data-stu-id="053ec-284">In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span></span>

* <span data-ttu-id="053ec-285">**AlwaysTransientErrorDetectionStrategy** 클래스</span><span class="sxs-lookup"><span data-stu-id="053ec-285">**AlwaysTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="053ec-286">**NeverTransientErrorDetectionStrategy** 클래스</span><span class="sxs-lookup"><span data-stu-id="053ec-286">**NeverTransientErrorDetectionStrategy** class</span></span>

<span data-ttu-id="053ec-287">다음은 EntLib60에 대한 정보의 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-287">Here are links to information about EntLib60:</span></span>

* <span data-ttu-id="053ec-288">무료 [책 다운로드: Microsoft Enterprise Library에 대한 개발자 가이드, 2판](http://www.microsoft.com/download/details.aspx?id=41145)</span><span class="sxs-lookup"><span data-stu-id="053ec-288">Free [Book Download: Developer's Guide to Microsoft Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span></span>
* <span data-ttu-id="053ec-289">모범 사례: [재시도 일반 지침](../best-practices-retry-general.md) 에서 재시도 논리에 대해 깊이 있게 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-289">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span></span>
* <span data-ttu-id="053ec-290">[Enterprise Library - 일시적 오류 처리 응용 프로그램 블록 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span><span class="sxs-lookup"><span data-stu-id="053ec-290">NuGet download of [Enterprise Library - Transient Fault Handling application block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span></span>

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-the-logging-block"></a><span data-ttu-id="053ec-291">EntLib60: 로깅 블록</span><span class="sxs-lookup"><span data-stu-id="053ec-291">EntLib60: The logging block</span></span>
* <span data-ttu-id="053ec-292">로깅 블록은 다음 작업을 할 수 있는 매우 유연한 맞춤형 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-292">The Logging block is a highly flexible and configurable solution that allows you to:</span></span>
  
  * <span data-ttu-id="053ec-293">다양한 위치에서 메시지를 만들고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-293">Create and store log messages in a wide variety of locations.</span></span>
  * <span data-ttu-id="053ec-294">메시지를 분류 및 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-294">Categorize and filter messages.</span></span>
  * <span data-ttu-id="053ec-295">디버깅, 추적, 감사 및 일반 로깅 요구 사항에 유용한 문맥 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-295">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span></span>
* <span data-ttu-id="053ec-296">로깅 블록은 대상 로깅 저장소의 위치 및 유형과 상관없이 응용 프로그램 코드의 일관성을 유지하도록 로그 대상에서 로깅 기능을 추상화합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-296">The Logging block abstracts the logging functionality from the log destination so that the application code is consistent, irrespective of the location and type of the target logging store.</span></span>

<span data-ttu-id="053ec-297">자세한 내용은 : [5 - 간단한 응용 프로그램 블록 로깅 사용](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="053ec-297">For details see: [5 - As Easy As Falling Off a Log: Using the Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span></span>

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a><span data-ttu-id="053ec-298">EntLib60 IsTransient 메서드 소스 코드</span><span class="sxs-lookup"><span data-stu-id="053ec-298">EntLib60 IsTransient method source code</span></span>
<span data-ttu-id="053ec-299">다음으로, **SqlDatabaseTransientErrorDetectionStrategy** 클래스에는 **IsTransient** 메서드에 대한 C# 소스 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-299">Next, from the **SqlDatabaseTransientErrorDetectionStrategy** class, is the C# source code for the **IsTransient** method.</span></span> <span data-ttu-id="053ec-300">소스 코드는 2013년 4월처럼 일시적 오류로 간주할 오류와 재시도할 만한 오류를 명확히 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-300">The source code clarifies which errors were considered to be transient and worthy of retry, as of April 2013.</span></span>

<span data-ttu-id="053ec-301">이 복사본에서 가독성을 위해 많은 **//** 줄이 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-301">Numerous **//comment** lines have been removed from this copy to emphasize readability.</span></span>

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in the exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // The service is currently busy. Retry the request after 10 seconds.
            // Code: (reason code to be decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode the reason code from the error message to
            // determine the grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach the decoded values as additional attributes to
            // the original SQL exception.
            sqlException.Data[condition.ThrottlingMode.GetType().Name] =
              condition.ThrottlingMode.ToString();
            sqlException.Data[condition.GetType().Name] = condition;

            return true;

          case 10928:
          case 10929:
          case 10053:
          case 10054:
          case 10060:
          case 40197:
          case 40540:
          case 40613:
          case 40143:
          case 233:
          case 64:
            // DBNETLIB Error Code: 20
            // The instance of SQL Server you attempted to connect to
            // does not support encryption.
          case (int)ProcessNetLibErrorCode.EncryptionNotSupported:
            return true;
        }
      }
    }
    else if (ex is TimeoutException)
    {
      return true;
    }
    else
    {
      EntityException entityException;
      if ((entityException = ex as EntityException) != null)
      {
        return this.IsTransient(entityException.InnerException);
      }
    }
  }

  return false;
}
```


## <a name="next-steps"></a><span data-ttu-id="053ec-302">다음 단계</span><span class="sxs-lookup"><span data-stu-id="053ec-302">Next steps</span></span>
* <span data-ttu-id="053ec-303">다른 일반적인 Azure SQL 데이터베이스 연결 문제를 해결하는 경우, [Azure SQL 데이터베이스에 대한 연결 문제 해결](sql-database-troubleshoot-common-connection-issues.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="053ec-303">For troubleshooting other common Azure SQL Database connection issues, visit [Troubleshoot connection issues to Azure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span></span>
* [<span data-ttu-id="053ec-304">SQL Server 연결 풀링(ADO.NET)</span><span class="sxs-lookup"><span data-stu-id="053ec-304">SQL Server Connection Pooling (ADO.NET)</span></span>](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [<span data-ttu-id="053ec-305">*Retrying*은 임의 항목에 재시도 동작을 추가하는 작업을 간소화하기 위해 Apache 2.0 라이선스 하에 **Python**으로 작성한 일반 목적의 재시도 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="053ec-305">*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in **Python**, to simplify the task of adding retry behavior to just about anything.</span></span>](https://pypi.python.org/pypi/retrying)


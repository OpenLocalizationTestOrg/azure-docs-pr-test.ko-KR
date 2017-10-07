---
title: "일시적인 오류 aaaFix SQL 연결 오류, | Microsoft Docs"
description: "Tootroubleshoot, 진단, 하 고 SQL 연결 오류 또는 Azure SQL 데이터베이스의 일시적 오류를 방지 하는 방법에 대해 알아봅니다. "
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
ms.openlocfilehash: d225e610b9e88170ab53ca16d615bd07220603cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a><span data-ttu-id="7cd13-104">SQL 연결 오류와 일시적 SQL 데이터베이스 오류의 문제 해결, 진단 및 예방</span><span class="sxs-lookup"><span data-stu-id="7cd13-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span></span>
<span data-ttu-id="7cd13-105">이 문서에서는 tooprevent를 문제 해결, 진단 및 연결 오류와 클라이언트 응용 프로그램에서 Azure SQL 데이터베이스와 상호 작용할 때 직면할 수 있는 일시적인 오류를 완화 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-105">This article describes how tooprevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span></span> <span data-ttu-id="7cd13-106">Tooconfigure를 재시도 논리, hello 연결 문자열을 빌드 및 기타 연결 설정을 조정 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-106">Learn how tooconfigure retry logic, build hello connection string, and adjust other connection settings.</span></span>

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a><span data-ttu-id="7cd13-107">일시적인 오류(일시 장애)</span><span class="sxs-lookup"><span data-stu-id="7cd13-107">Transient errors (transient faults)</span></span>
<span data-ttu-id="7cd13-108">일시적인 오류(일시 결함)에는 자체적으로 신속히 환익되는 원인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-108">A transient error - also, transient fault - has an underlying cause that will soon resolve itself.</span></span> <span data-ttu-id="7cd13-109">가끔 일시적인 오류의 원인은 hello Azure 시스템 빠르게 이동 하면 하드웨어 리소스 toobetter 부하를 분산 다양 한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-109">An occasional cause of transient errors is when hello Azure system quickly shifts hardware resources toobetter load-balance various workloads.</span></span> <span data-ttu-id="7cd13-110">이러한 재구성 이벤트는 대부분 60초 이내에 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-110">Most of these reconfiguration events often complete in less than 60 seconds.</span></span> <span data-ttu-id="7cd13-111">이 재구성 기간 동안 연결을 할 수 있습니다 tooAzure SQL 데이터베이스를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-111">During this reconfiguration time span, you may have connectivity issues tooAzure SQL Database.</span></span> <span data-ttu-id="7cd13-112">SQL 데이터베이스 있어야 tooAzure 연결 응용 프로그램 작성 tooexpect 이러한 일시적인 오류를 구현 하 여 해당 재시도 논리를 응용 프로그램 오류로 toousers에서 표시가 대신 하 여 코드의 핸들입니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-112">Applications connecting tooAzure SQL Database should be built tooexpect these transient errors, handle them by implementing retry logic in their code instead of surfacing them toousers as application errors.</span></span>

<span data-ttu-id="7cd13-113">프로그램의 hello throw 하 여 hello 일시적인 오류에 대 한 지시 클라이언트 프로그램이 ADO.NET를 사용 하는 경우는 **SqlException**합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-113">If your client program is using ADO.NET, your program is told about hello transient error by hello throw of an **SqlException**.</span></span> <span data-ttu-id="7cd13-114">hello **번호** hello 목록 hello 항목의 hello 위쪽 일시적인 오류에 대해 속성을 비교할 수 있습니다: [SQL 데이터베이스 클라이언트 응용 프로그램에 대 한 SQL 오류 코드](sql-database-develop-error-messages.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-114">hello **Number** property can be compared against hello list of transient errors near hello top of hello topic: [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="7cd13-115">연결과 명령 비교</span><span class="sxs-lookup"><span data-stu-id="7cd13-115">Connection versus command</span></span>
<span data-ttu-id="7cd13-116">Hello SQL 연결을 다시 시도 하거나 hello 다음에 따라 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-116">You'll retry hello SQL connection or establish it again, depending on hello following:</span></span>

* <span data-ttu-id="7cd13-117">**연결 시도 중에 일시적인 오류가 발생**: hello 연결을 몇 초 동안 지연 한 후 다시 시도해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-117">**A transient error occurs during a connection try**: hello connection should be retried after delaying for several seconds.</span></span>
* <span data-ttu-id="7cd13-118">**일시적인 오류가 발생 하는 SQL 쿼리 명령 중**: hello 명령 하지 즉시 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7cd13-118">**A transient error occurs during a SQL query command**: hello command should not be immediately retried.</span></span> <span data-ttu-id="7cd13-119">대신, 지연 후 hello 새로 연결 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-119">Instead, after a delay, hello connection should be freshly established.</span></span> <span data-ttu-id="7cd13-120">그런 다음 hello 명령은 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-120">Then hello command can be retried.</span></span>

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a><span data-ttu-id="7cd13-121">일시적인 오류에 대한 재시도 논리</span><span class="sxs-lookup"><span data-stu-id="7cd13-121">Retry logic for transient errors</span></span>
<span data-ttu-id="7cd13-122">간혹 일시적 오류가 발생하는 클라이언트 프로그램에 재시도 논리가 포함된 경우 더욱 견고해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-122">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span></span>

<span data-ttu-id="7cd13-123">프로그램 3rd 파티 미들웨어를 통해 Azure SQL 데이터베이스와 통신할 경우 hello 미들웨어 일시적인 오류에 대 한 재시도 논리를 포함 하는지 여부를 hello 공급 업체에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-123">When your program communicates with Azure SQL Database through a 3rd party middleware, inquire with hello vendor whether hello middleware contains retry logic for transient errors.</span></span>

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a><span data-ttu-id="7cd13-124">재시도 원칙</span><span class="sxs-lookup"><span data-stu-id="7cd13-124">Principles for retry</span></span>
* <span data-ttu-id="7cd13-125">Hello 오류가 일시적인 이면 시도 tooopen 한 연결을 다시 시도해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-125">An attempt tooopen a connection should be retried if hello error is transient.</span></span>
* <span data-ttu-id="7cd13-126">일시적 오류로 실패하는 SQL SELECT 문은 직접 다시 시도하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-126">A SQL SELECT statement that fails with a transient error should not be retried directly.</span></span>
  
  * <span data-ttu-id="7cd13-127">대신 새 연결을 설정 하 고 hello 선택을 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7cd13-127">Instead, establish a fresh connection, and then retry hello SELECT.</span></span>
* <span data-ttu-id="7cd13-128">SQL UPDATE 문에서 일시적인 오류로 실패 하면 새 연결 hello 업데이트를 다시 시도 하기 전에 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-128">When a SQL UPDATE statement fails with a transient error, a fresh connection should be established before hello UPDATE is retried.</span></span>
  
  * <span data-ttu-id="7cd13-129">hello 재시도 논리가 완료 되 면 hello 전체 데이터베이스 transaction 또는 해당 hello 전체 트랜잭션이 롤백 되 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-129">hello retry logic must ensure that either hello entire database transaction completed, or that hello entire transaction is rolled back.</span></span>

#### <a name="other-considerations-for-retry"></a><span data-ttu-id="7cd13-130">재시도에 대한 기타 고려 사항</span><span class="sxs-lookup"><span data-stu-id="7cd13-130">Other considerations for retry</span></span>
* <span data-ttu-id="7cd13-131">일괄 처리 프로그램 근무 시간이 지난 후 자동으로 시작 하 고 있는 아침, 하기 전에 완료 됩니다 toovery 환자 긴 해당 시도 간의 시간 간격으로 더 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-131">A batch program that is automatically started after work hours, and which will complete before morning, can afford toovery patient with long time intervals between its retry attempts.</span></span>
* <span data-ttu-id="7cd13-132">사용자 인터페이스 프로그램 너무 오래 대기 후 hello 경향 toogive를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-132">A user interface program should account for hello human tendency toogive up after too long a wait.</span></span>
  
  * <span data-ttu-id="7cd13-133">그러나 hello 솔루션 아니어야 tooretry 몇 초 마다 해당 정책을 요청으로 hello 시스템 넘쳐나 게 수 때문에 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-133">However, hello solution must not be tooretry every few seconds, because that policy can flood hello system with requests.</span></span>

#### <a name="interval-increase-between-retries"></a><span data-ttu-id="7cd13-134">재시도 간격 증가</span><span class="sxs-lookup"><span data-stu-id="7cd13-134">Interval increase between retries</span></span>
<span data-ttu-id="7cd13-135">첫 번째 재시도 전에 5초간 지연하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-135">We recommend that you delay for 5 seconds before your first retry.</span></span> <span data-ttu-id="7cd13-136">5 초 보다 짧은 지연 후 다시 시도 hello 클라우드 서비스를 진행 하기가 매우 될 위험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-136">Retrying after a delay shorter than 5 seconds risks overwhelming hello cloud service.</span></span> <span data-ttu-id="7cd13-137">각 후속 재시도 대 한 hello 지연 증가 하도록 기하급수적으로 tooa를 최대 60 초입니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-137">For each subsequent retry hello delay should grow exponentially, up tooa maximum of 60 seconds.</span></span>

<span data-ttu-id="7cd13-138">Hello에 대 한 내용은 *차단 기간* ADO.NET을 사용 하는 클라이언트에서 사용할 수는 [SQL Server 연결 풀링 (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-138">A discussion of hello *blocking period* for clients that use ADO.NET is available in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span></span>

<span data-ttu-id="7cd13-139">Hello 프로그램은 자체 종료 전에 tooset 최대 재시도 횟수 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-139">You might also want tooset a maximum number of retries before hello program self-terminates.</span></span>

#### <a name="code-samples-with-retry-logic"></a><span data-ttu-id="7cd13-140">재시도 논리가 포함된 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="7cd13-140">Code samples with retry logic</span></span>
<span data-ttu-id="7cd13-141">재시도 논리가 포함된 코드 샘플은 다음에서 다양한 언어로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-141">Code samples with retry logic, in a variety of programming languages, are available at:</span></span>

* [<span data-ttu-id="7cd13-142">SQL 데이터베이스 및 SQL Server용 연결 라이브러리</span><span class="sxs-lookup"><span data-stu-id="7cd13-142">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a><span data-ttu-id="7cd13-143">재시도 논리 테스트</span><span class="sxs-lookup"><span data-stu-id="7cd13-143">Test your retry logic</span></span>
<span data-ttu-id="7cd13-144">tootest 재시도 논리를 시뮬레이션 하거나 해야 프로그램 실행 중에 수정할 수 있는 것 보다는 오류를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-144">tootest your retry logic, you must simulate or cause an error than can be corrected while your program is still running.</span></span>

##### <a name="test-by-disconnecting-from-hello-network"></a><span data-ttu-id="7cd13-145">Hello 네트워크에서 연결을 해제 하 여 테스트</span><span class="sxs-lookup"><span data-stu-id="7cd13-145">Test by disconnecting from hello network</span></span>
<span data-ttu-id="7cd13-146">재시도 논리를 테스트할 수 있습니다는 한 가지 방법은 toodisconnect hello 프로그램을 실행 하는 동안 hello 사용 하 여 클라이언트 컴퓨터 네트워크는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-146">One way you can test your retry logic is toodisconnect your client computer from hello network while hello program is running.</span></span> <span data-ttu-id="7cd13-147">hello 오류가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-147">hello error will be:</span></span>

* <span data-ttu-id="7cd13-148">**SqlException.Number** = 11001</span><span class="sxs-lookup"><span data-stu-id="7cd13-148">**SqlException.Number** = 11001</span></span>
* <span data-ttu-id="7cd13-149">메시지: "해당 호스트가 없습니다"</span><span class="sxs-lookup"><span data-stu-id="7cd13-149">Message: "No such host is known"</span></span>

<span data-ttu-id="7cd13-150">먼저 hello의 일부를 다시 시도 횟수,으로 프로그램 hello 맞춤법 오류를 해결 하 고 tooconnect를 매핑한 다음 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-150">As part of hello first retry attempt, your program can correct hello misspelling, and then attempt tooconnect.</span></span>

<span data-ttu-id="7cd13-151">이 실용적인 toomake를 분리 하면 hello 네트워크에서 컴퓨터 프로그램을 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="7cd13-151">toomake this practical, you unplug your computer from hello network before you start your program.</span></span> <span data-ttu-id="7cd13-152">그런 다음 프로그램 hello 프로그램을 발생 시키는 런타임 매개 변수를 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-152">Then your program recognizes a run time parameter that causes hello program to:</span></span>

1. <span data-ttu-id="7cd13-153">임시로 11001 tooits 목록이 오류 tooconsider 임시로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-153">Temporarily add 11001 tooits list of errors tooconsider as transient.</span></span>
2. <span data-ttu-id="7cd13-154">평상 시와 같이 첫 번째 연결을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-154">Attempt its first connection as usual.</span></span>
3. <span data-ttu-id="7cd13-155">Hello 오류 걸러진 후 11001 hello 목록에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-155">After hello error is caught, remove 11001 from hello list.</span></span>
4. <span data-ttu-id="7cd13-156">Hello 네트워크로 hello 사용자 tooplug hello 컴퓨터를 알리는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-156">Display a message telling hello user tooplug hello computer into hello network.</span></span>
   * <span data-ttu-id="7cd13-157">실행을 일시 중지 추가 하거나 hello를 사용 하 여 **Console.ReadLine** 메서드나 확인 단추가 있는 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="7cd13-157">Pause further execution by using either hello **Console.ReadLine** method or a dialog with an OK button.</span></span> <span data-ttu-id="7cd13-158">hello 사용자 hello 컴퓨터 hello 네트워크에 연결 하는 후 hello Enter 키를 누를 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-158">hello user presses hello Enter key after hello computer plugged into hello network.</span></span>
5. <span data-ttu-id="7cd13-159">성공 예상 tooconnect 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-159">Attempt again tooconnect, expecting success.</span></span>

##### <a name="test-by-misspelling-hello-database-name-when-connecting"></a><span data-ttu-id="7cd13-160">연결할 때 잘못 된 철자 hello 데이터베이스 이름으로 테스트</span><span class="sxs-lookup"><span data-stu-id="7cd13-160">Test by misspelling hello database name when connecting</span></span>
<span data-ttu-id="7cd13-161">프로그램은 hello 첫 번째 연결 시도 하기 전에 hello 사용자 이름을 잘못 입력 의도적으로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-161">Your program can purposely misspell hello user name before hello first connection attempt.</span></span> <span data-ttu-id="7cd13-162">hello 오류가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-162">hello error will be:</span></span>

* <span data-ttu-id="7cd13-163">**SqlException.Number** = 18456</span><span class="sxs-lookup"><span data-stu-id="7cd13-163">**SqlException.Number** = 18456</span></span>
* <span data-ttu-id="7cd13-164">메시지: "사용자 'WRONG_MyUserName'에 대한 로그인에 실패했습니다."</span><span class="sxs-lookup"><span data-stu-id="7cd13-164">Message: "Login failed for user 'WRONG_MyUserName'."</span></span>

<span data-ttu-id="7cd13-165">먼저 hello의 일부를 다시 시도 횟수,으로 프로그램 hello 맞춤법 오류를 해결 하 고 tooconnect를 매핑한 다음 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-165">As part of hello first retry attempt, your program can correct hello misspelling, and then attempt tooconnect.</span></span>

<span data-ttu-id="7cd13-166">toomake 실용적이, 프로그램 런타임 매개 변수를 사용 하면 프로그램이 hello를 인식할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-166">toomake this practical, your program could recognize a run time parameter that causes hello program to:</span></span>

1. <span data-ttu-id="7cd13-167">임시로 18456 tooits 목록이 오류 tooconsider 임시로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-167">Temporarily add 18456 tooits list of errors tooconsider as transient.</span></span>
2. <span data-ttu-id="7cd13-168">의도적으로 'WRONG_' toohello 사용자 이름을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-168">Purposely add 'WRONG_' toohello user name.</span></span>
3. <span data-ttu-id="7cd13-169">Hello 오류 걸러진 후 18456 hello 목록에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-169">After hello error is caught, remove 18456 from hello list.</span></span>
4. <span data-ttu-id="7cd13-170">'WRONG_' hello 사용자 이름에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-170">Remove 'WRONG_' from hello user name.</span></span>
5. <span data-ttu-id="7cd13-171">성공 예상 tooconnect 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-171">Attempt again tooconnect, expecting success.</span></span>

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a><span data-ttu-id="7cd13-172">연결 다시 시도에 대한 .NET SqlConnection 매개 변수</span><span class="sxs-lookup"><span data-stu-id="7cd13-172">.NET SqlConnection parameters for connection retry</span></span>
<span data-ttu-id="7cd13-173">클라이언트 프로그램 hello.NET Framework 클래스를 사용 하 여 tootooAzure SQL 데이터베이스를 연결 하는 경우 **System.Data.SqlClient.SqlConnection**,.NET 4.6.1을 사용 해야 또는 이후 (또는.NET Core) 하므로 해당 연결 다시 시도 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-173">If your client program connects tootooAzure SQL Database by using hello .NET Framework class **System.Data.SqlClient.SqlConnection**, you should use .NET 4.6.1 or later (or .NET Core) so you can leverage its connection retry feature.</span></span> <span data-ttu-id="7cd13-174">Hello 기능에 대 한 자세한 내용은 [여기](http://go.microsoft.com/fwlink/?linkid=393996)합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-174">Details of hello feature are [here](http://go.microsoft.com/fwlink/?linkid=393996).</span></span>

<!--
2015-11-30, FwLink 393996 points toodn632678.aspx, which links tooa downloadable .docx related tooSqlClient and SQL Server 2014.
-->


<span data-ttu-id="7cd13-175">Hello를 작성 하는 경우 [연결 문자열](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) 에 대 한 프로그램 **SqlConnection** 개체를 매개 변수 뒤 hello 사이의 hello 값을 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-175">When you build hello [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, you should coordinate hello values among hello following parameters:</span></span>

* <span data-ttu-id="7cd13-176">ConnectRetryCount&nbsp;&nbsp;*(기본값은 1입니다.) 범위는 0에서 255입니다.)*</span><span class="sxs-lookup"><span data-stu-id="7cd13-176">ConnectRetryCount &nbsp;&nbsp;*(Default is 1. Range is 0 through 255.)*</span></span>
* <span data-ttu-id="7cd13-177">ConnectRetryInterval&nbsp;&nbsp;*(기본값은 1초입니다. 범위는 1에서 60입니다.)*</span><span class="sxs-lookup"><span data-stu-id="7cd13-177">ConnectRetryInterval &nbsp;&nbsp;*(Default is 1 second. Range is 1 through 60.)*</span></span>
* <span data-ttu-id="7cd13-178">연결 제한 시간&nbsp;&nbsp;*(기본값은 15초입니다. 범위는 0에서 2147483647입니다.)*</span><span class="sxs-lookup"><span data-stu-id="7cd13-178">Connection Timeout &nbsp;&nbsp;*(Default is 15 seconds. Range is 0 through 2147483647)*</span></span>

<span data-ttu-id="7cd13-179">특히, 선택한 값 hello 같음 true 다음 사항을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-179">Specifically, your chosen values should make hello following equality true:</span></span>

* <span data-ttu-id="7cd13-180">연결 제한 시간 = ConnectRetryCount * ConnectionRetryInterval</span><span class="sxs-lookup"><span data-stu-id="7cd13-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span></span>

<span data-ttu-id="7cd13-181">예를 들어 hello 계산할 = 3, 및 간격 = 10 초, 시간 제한이 29 초 제공 하지 않는 것 매우 hello 시스템에서 연결의 3 번째 및 마지막 재시도 대 한 충분 한 시간에만: 29 < 3 * 10입니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-181">For example, if hello count = 3, and interval = 10 seconds, a timeout of only 29 seconds would not quite give hello system enough time for its 3rd and final retry at connecting: 29 < 3 * 10.</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="7cd13-182">연결과 명령 비교</span><span class="sxs-lookup"><span data-stu-id="7cd13-182">Connection versus command</span></span>
<span data-ttu-id="7cd13-183">hello **ConnectRetryCount** 및 **ConnectRetryInterval** 매개 변수를 사용 하면 **SqlConnection** 내용의 또는 하지 않은 연결 작업을 다시 시도 hello 개체 프로그램 프로그램 제어 tooyour 프로그램을 반환 하는 등입니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-183">hello **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry hello connect operation without telling or bothering your program, such as returning control tooyour program.</span></span> <span data-ttu-id="7cd13-184">hello 재시도 hello 다음 상황에서에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-184">hello retries can occur in hello following situations:</span></span>

* <span data-ttu-id="7cd13-185">mySqlConnection.Open 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="7cd13-185">mySqlConnection.Open method call</span></span>
* <span data-ttu-id="7cd13-186">mySqlConnection.Execute 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="7cd13-186">mySqlConnection.Execute method call</span></span>

<span data-ttu-id="7cd13-187">미묘한 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-187">There is a subtlety.</span></span> <span data-ttu-id="7cd13-188">일시적인 오류가 발생 하는 경우 동안 프로그램 *쿼리* 실행 중인 프로그램 **SqlConnection** 개체 hello를 다시 시도 하지 작업, 연결 및 확실히 쿼리 재시도 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-188">If a transient error occurs while your *query* is being executed, your **SqlConnection** object does not retry hello connect operation, and it certainly does not retry your query.</span></span> <span data-ttu-id="7cd13-189">그러나 **SqlConnection** 매우 신속 하 게 검사 hello 실행에 대 한 쿼리를 보내기 전에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-189">However, **SqlConnection** very quickly checks hello connection before sending your query for execution.</span></span> <span data-ttu-id="7cd13-190">연결 문제를 검색 하는 hello 신속 하 게 확인 하는 경우 **SqlConnection** 연결 작업을 다시 시도 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-190">If hello quick check detects a connection problem, **SqlConnection** retries hello connect operation.</span></span> <span data-ttu-id="7cd13-191">Hello 다시 시도 성공 하면 쿼리 실행을 위해 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-191">If hello retry succeeds, you query is sent for execution.</span></span>

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a><span data-ttu-id="7cd13-192">ConnectRetryCount가 응용 프로그램 다시 시도 논리와 결합해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="7cd13-192">Should ConnectRetryCount be combined with application retry logic?</span></span>
<span data-ttu-id="7cd13-193">응용 프로그램에는 강력한 사용자 지정 다시 시도 논리가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-193">Suppose your application has robust custom retry logic.</span></span> <span data-ttu-id="7cd13-194">Hello를 다시 시도 수 연결 작업을 4 번입니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-194">It might retry hello connect operation 4 times.</span></span> <span data-ttu-id="7cd13-195">추가 하는 경우 **ConnectRetryInterval** 및 **ConnectRetryCount** 3 tooyour 연결 문자열 = hello 재시도 횟수 too4 늘어납니다 * 3 = 12를 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-195">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 tooyour connection string, you will increase hello retry count too4 * 3 = 12 retries.</span></span> <span data-ttu-id="7cd13-196">이러한 많은 수의 다시 시도를 할 의도가 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-196">You might not intend such a high number of retries.</span></span>

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-tooazure-sql-database"></a><span data-ttu-id="7cd13-197">연결 tooAzure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="7cd13-197">Connections tooAzure SQL Database</span></span>
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a><span data-ttu-id="7cd13-198">연결: 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="7cd13-198">Connection: Connection string</span></span>
<span data-ttu-id="7cd13-199">hello 연결 문자열 tooAzure 연결 하기 위해 필요한 SQL 데이터베이스는 SQL Server tooMicrosoft 연결 하기 위한 문자열 hello와에서 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-199">hello connection string necessary for connecting tooAzure SQL Database is slightly different from hello string for connecting tooMicrosoft SQL Server.</span></span> <span data-ttu-id="7cd13-200">Hello에서 데이터베이스에 대 한 연결 문자열 hello를 복사할 수 있습니다 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-200">You can copy hello connection string for your database from hello [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a><span data-ttu-id="7cd13-201">연결: IP 주소</span><span class="sxs-lookup"><span data-stu-id="7cd13-201">Connection: IP address</span></span>
<span data-ttu-id="7cd13-202">Hello SQL 데이터베이스 서버 tooaccept 통신 hello IP 주소에서 클라이언트 프로그램을 호스트 하는 hello 컴퓨터의 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-202">You must configure hello SQL Database server tooaccept communication from hello IP address of hello computer that hosts your client program.</span></span> <span data-ttu-id="7cd13-203">Hello 통해 hello 방화벽 설정을 편집 하 여이 작업을 수행 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-203">You do this by editing hello firewall settings through hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="7cd13-204">Tooconfigure hello IP 주소를 잊은 경우 프로그램 hello 필요한 IP 주소를 나타내는 편리한 오류 메시지와 함께 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-204">If you forget tooconfigure hello IP address, your program will fail with a handy error message that states hello necessary IP address.</span></span>

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

<span data-ttu-id="7cd13-205">자세한 내용은 [방법: SQL 데이터베이스에 방화벽 설정 구성](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="7cd13-205">For more information, see: [How to: Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md)</span></span>

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a><span data-ttu-id="7cd13-206">연결: 포트</span><span class="sxs-lookup"><span data-stu-id="7cd13-206">Connection: Ports</span></span>
<span data-ttu-id="7cd13-207">일반적으로 포트 1433은 클라이언트 프로그램을 호스팅하는 hello 컴퓨터에서 아웃 바운드 통신을 위해 열려 tooensure만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-207">Typically you only need tooensure that port 1433 is open for outbound communication, on hello computer that hosts you client program.</span></span>

<span data-ttu-id="7cd13-208">예를 들어, 클라이언트 프로그램은 Windows 컴퓨터에서 호스트 되는 경우 hello 호스트에서 Windows 방화벽 hello가 있습니다 tooopen 포트를 1433.</span><span class="sxs-lookup"><span data-stu-id="7cd13-208">For example, when your client program is hosted on a Windows computer, hello Windows Firewall on hello host enables you tooopen port 1433:</span></span>

1. <span data-ttu-id="7cd13-209">Hello 제어판을 열으십시오</span><span class="sxs-lookup"><span data-stu-id="7cd13-209">Open hello Control Panel</span></span>
2. <span data-ttu-id="7cd13-210">&gt; 모든 제어판 항목</span><span class="sxs-lookup"><span data-stu-id="7cd13-210">&gt; All Control Panel Items</span></span>
3. <span data-ttu-id="7cd13-211">&gt; Windows 방화벽</span><span class="sxs-lookup"><span data-stu-id="7cd13-211">&gt; Windows Firewall</span></span>
4. <span data-ttu-id="7cd13-212">&gt; 고급 설정</span><span class="sxs-lookup"><span data-stu-id="7cd13-212">&gt; Advanced Settings</span></span>
5. <span data-ttu-id="7cd13-213">&gt; 아웃바운드 규칙</span><span class="sxs-lookup"><span data-stu-id="7cd13-213">&gt; Outbound Rules</span></span>
6. <span data-ttu-id="7cd13-214">&gt; 작업</span><span class="sxs-lookup"><span data-stu-id="7cd13-214">&gt; Actions</span></span>
7. <span data-ttu-id="7cd13-215">&gt; 새 규칙</span><span class="sxs-lookup"><span data-stu-id="7cd13-215">&gt; New Rule</span></span>

<span data-ttu-id="7cd13-216">클라이언트 프로그램이 Azure VM(가상 컴퓨터)에 호스팅된 경우 </span><span class="sxs-lookup"><span data-stu-id="7cd13-216">If your client program is hosted on an Azure virtual machine (VM), you should read:</span></span><br/><span data-ttu-id="7cd13-217">[ADO.NET 4.5 및 SQL Database에 대한 1433 이외의 포트](sql-database-develop-direct-route-ports-adonet-v12.md)</span><span class="sxs-lookup"><span data-stu-id="7cd13-217">[Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

<span data-ttu-id="7cd13-218">포트 및 IP 주소 구성에 대한 배경 정보는 [Azure SQL 데이터베이스 방화벽](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="7cd13-218">For background information about cofiguration of ports and IP address, see: [Azure SQL Database firewall](sql-database-firewall-configure.md)</span></span>

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a><span data-ttu-id="7cd13-219">연결: ADO.NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="7cd13-219">Connection: ADO.NET 4.6.1</span></span>
<span data-ttu-id="7cd13-220">프로그램이 같은 ADO.NET 클래스를 사용 하면 **System.Data.SqlClient.SqlConnection** tooconnect tooAzure SQL 데이터베이스는 권장 하면.NET Framework 버전 4.6.1 이상.</span><span class="sxs-lookup"><span data-stu-id="7cd13-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** tooconnect tooAzure SQL Database, we recommend that you use .NET Framework version 4.6.1 or higher.</span></span>

<span data-ttu-id="7cd13-221">ADO.NET 4.6.1:</span><span class="sxs-lookup"><span data-stu-id="7cd13-221">ADO.NET 4.6.1:</span></span>

* <span data-ttu-id="7cd13-222">Azure SQL 데이터베이스는 향상 된 안정성 hello를 사용 하 여 한 연결을 열 때 **SqlConnection.Open** 메서드.</span><span class="sxs-lookup"><span data-stu-id="7cd13-222">For Azure SQL Database, there is improved reliability when you open a connection by using hello **SqlConnection.Open** method.</span></span> <span data-ttu-id="7cd13-223">hello **열려** 메서드는 이제 hello 연결 제한 시간 내에 특정 오류에 대 한 응답 tootransient 오류에 최상의 노력 재시도 메커니즘을 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-223">hello **Open** method now incorporates best effort retry mechanisms in response tootransient faults, for certain errors within hello Connection Timeout period.</span></span>
* <span data-ttu-id="7cd13-224">연결 풀링을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-224">Supports connection pooling.</span></span> <span data-ttu-id="7cd13-225">Hello 연결 하는 효율적인 확인 프로그램을 제공 하는 개체 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-225">This includes an efficient verification that hello connection object it gives your program is functioning.</span></span>

<span data-ttu-id="7cd13-226">연결 풀에서 연결 개체를 사용 하 여 프로그램을 일시적으로 닫습니다 hello 연결 즉시 사용 하는 경우는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-226">When you use a connection object from a connection pool, we recommend that your program temporarily close hello connection when not immediately using it.</span></span> <span data-ttu-id="7cd13-227">비용이 많이 들지 않습니다 다시 연결을 열어 새 연결을 만들어 hello 방법은입니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-227">Re-opening a connection is not expensive hello way creating a new connection is.</span></span>

<span data-ttu-id="7cd13-228">Toohello를 업그레이드 하는 권장 이전 버전에서는 또는 ADO.NET 4.0을 사용 하는 경우 최신 ADO.NET 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-228">If you are using ADO.NET 4.0 or earlier, we recommend that you upgrade toohello latest ADO.NET.</span></span>

* <span data-ttu-id="7cd13-229">2015년 11월 현재 [ADO.NET 4.6.1을 다운로드](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-229">As of November 2015, you can [download ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span></span>

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a><span data-ttu-id="7cd13-230">진단</span><span class="sxs-lookup"><span data-stu-id="7cd13-230">Diagnostics</span></span>
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a><span data-ttu-id="7cd13-231">진단: 유틸리티에서 연결할 수 있는지 여부 테스트</span><span class="sxs-lookup"><span data-stu-id="7cd13-231">Diagnostics: Test whether utilities can connect</span></span>
<span data-ttu-id="7cd13-232">프로그램 tooconnect tooAzure SQL 데이터베이스에 실패할 경우 한 가지 진단 방법은 tootry tooconnect 유틸리티 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-232">If your program is failing tooconnect tooAzure SQL Database, one diagnostic option is tootry tooconnect with a utility program.</span></span> <span data-ttu-id="7cd13-233">Hello를 사용 하 여 hello 유틸리티는 연결 하는 것이 가장 좋습니다 위해 프로그램에서 사용 하는 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-233">Ideally hello utility would connect by using hello same library that your program uses.</span></span>

<span data-ttu-id="7cd13-234">모든 Windows 컴퓨터에서 이러한 유틸리티를 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-234">On any Windows computer, you can try these utilities:</span></span>

* <span data-ttu-id="7cd13-235">ADO.NET을 사용하여 연결하는 SQL Server Management Studio(ssms.exe).</span><span class="sxs-lookup"><span data-stu-id="7cd13-235">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET.</span></span>
* <span data-ttu-id="7cd13-236">[ODBC](http://msdn.microsoft.com/library/jj730308.aspx)를 사용하여 연결하는 sqlcmd.exe.</span><span class="sxs-lookup"><span data-stu-id="7cd13-236">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span></span>

<span data-ttu-id="7cd13-237">연결된 후에는 짧은 SQL SELECT 쿼리가 작동하는지 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-237">Once connected, test whether a short SQL SELECT query works.</span></span>

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-hello-open-ports"></a><span data-ttu-id="7cd13-238">진단: hello 열린 포트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-238">Diagnostics: Check hello open ports</span></span>
<span data-ttu-id="7cd13-239">가정 tooport 문제 인해 연결 시도가 실패 한 의심 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-239">Suppose you suspect that connection attempts are failing due tooport issues.</span></span> <span data-ttu-id="7cd13-240">컴퓨터에 hello 포트 구성에 대해 보고 하는 유틸리티를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-240">On your computer you can run a utility that reports on hello port configurations.</span></span>

<span data-ttu-id="7cd13-241">Linux hello에서 다음 유틸리티 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-241">On Linux hello following utilities might be helpful:</span></span>

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * <span data-ttu-id="7cd13-242">(Hello 예제 값 toobe IP 주소를 변경 합니다.)</span><span class="sxs-lookup"><span data-stu-id="7cd13-242">(Change hello example value toobe your IP address.)</span></span>

<span data-ttu-id="7cd13-243">Windows hello에서 [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) 유틸리티 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-243">On Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span></span> <span data-ttu-id="7cd13-244">예제 실행 하는 Azure SQL 데이터베이스 서버에서 포트 상황 hello 쿼리되고 랩톱 컴퓨터에서 실행 된는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-244">Here is an example execution that queried hello port situation on an Azure SQL Database server, and which was run on a laptop computer:</span></span>

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting tooresolve name tooIP address...
Name resolved too23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a><span data-ttu-id="7cd13-245">진단: 오류 기록</span><span class="sxs-lookup"><span data-stu-id="7cd13-245">Diagnostics: Log your errors</span></span>
<span data-ttu-id="7cd13-246">간헐적 문제는 며칠 또는 몇 주간 일반 패턴을 발견하여 진단하는 것이 가장 좋은 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span></span>

<span data-ttu-id="7cd13-247">클라이언트에서 발생한 모든 오류를 기록하면 진단에 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-247">Your client can assist in a diagnosis by logging all errors it encounters.</span></span> <span data-ttu-id="7cd13-248">Azure SQL 데이터베이스 자체를 내부적으로 기록 된 오류 데이터로 수 toocorrelate hello 로그 항목을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-248">You might be able toocorrelate hello log entries with error data that Azure SQL Database logs itself internally.</span></span>

<span data-ttu-id="7cd13-249">Enterprise Library 6 (EntLib60)는.NET 관리 되는 클래스 tooassist 로깅 사용 하 여 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-249">Enterprise Library 6 (EntLib60) offers .NET managed classes tooassist with logging:</span></span>

* [<span data-ttu-id="7cd13-250">5-쉽게으로 떨어질 때 해제 정도 로그로: hello 로깅 응용 프로그램 블록을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="7cd13-250">5 - As Easy As Falling Off a Log: Using hello Logging Application Block</span></span>](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a><span data-ttu-id="7cd13-251">진단: 시스템 로그에서 오류 확인</span><span class="sxs-lookup"><span data-stu-id="7cd13-251">Diagnostics: Examine system logs for errors</span></span>
<span data-ttu-id="7cd13-252">다음은 오류 및 기타 정보를 쿼리하는 몇 가지 Transact-SQL SELECT 문입니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-252">Here are some Transact-SQL SELECT statements that query logs of error and other information.</span></span>

| <span data-ttu-id="7cd13-253">로그 쿼리</span><span class="sxs-lookup"><span data-stu-id="7cd13-253">Query of log</span></span> | <span data-ttu-id="7cd13-254">설명</span><span class="sxs-lookup"><span data-stu-id="7cd13-254">Description</span></span> |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |<span data-ttu-id="7cd13-255">hello [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) 보기 일시적인 오류 또는 연결 실패를 일으킬 수 있는 일부를 포함 하 여 개별 이벤트에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-255">hello [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, including some that can cause transient errors or connectivity failures.</span></span><br/><br/><span data-ttu-id="7cd13-256">Hello 간에 상관 관계 수 이상적 **start_time** 또는 **end_time** 때 클라이언트 프로그램에 문제가 발생 하는 방법에 대 한 정보가 포함 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-256">Ideally you can correlate hello **start_time** or **end_time** values with information about when your client program experienced problems.</span></span><br/><br/><span data-ttu-id="7cd13-257">**팁:** toohello 연결 해야 **마스터** toorun이 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-257">**TIP:** You must connect toohello **master** database toorun this.</span></span> |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |<span data-ttu-id="7cd13-258">hello [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) 보기는 추가 진단에 대 한 이벤트 유형 집계 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-258">hello [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types, for additional diagnostics.</span></span><br/><br/><span data-ttu-id="7cd13-259">**팁:** toohello 연결 해야 **마스터** toorun이 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-259">**TIP:** You must connect toohello **master** database toorun this.</span></span> |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-hello-sql-database-log"></a><span data-ttu-id="7cd13-260">Hello SQL 데이터베이스 로그에서 이벤트 문제를 진단: 검색</span><span class="sxs-lookup"><span data-stu-id="7cd13-260">Diagnostics: Search for problem events in hello SQL Database log</span></span>
<span data-ttu-id="7cd13-261">Azure SQL 데이터베이스의 hello 로그에 문제 이벤트에 대 한 항목에 대 한 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-261">You can search for entries about problem events in hello log of Azure SQL Database.</span></span> <span data-ttu-id="7cd13-262">Hello hello에서 TRANSACT-SQL SELECT 문 다음 시도 **마스터** 데이터베이스:</span><span class="sxs-lookup"><span data-stu-id="7cd13-262">Try hello following Transact-SQL SELECT statement in hello **master** database:</span></span>

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


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a><span data-ttu-id="7cd13-263">sys.fn_xe_telemetry_blob_target_read_file에서 반환된 몇 개 행</span><span class="sxs-lookup"><span data-stu-id="7cd13-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span></span>
<span data-ttu-id="7cd13-264">다음은 반환된 행을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-264">Next is what a returned row might look like.</span></span> <span data-ttu-id="7cd13-265">표시 하는 hello null 값은 다른 행에 null 없는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-265">hello null values shown are often not null in other rows.</span></span>

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a><span data-ttu-id="7cd13-266">Enterprise Library 6</span><span class="sxs-lookup"><span data-stu-id="7cd13-266">Enterprise Library 6</span></span>
<span data-ttu-id="7cd13-267">Enterprise Library 6 (EntLib60)는.NET 클래스의 클라우드 서비스의 강력한 클라이언트를 구현 하는 데 도움이 되는 hello Azure SQL 데이터베이스 서비스 중 하나는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is hello Azure SQL Database service.</span></span> <span data-ttu-id="7cd13-268">EntLib60 처음 방문 하 여 지원할 수 있는 항목 전용된 tooeach 영역을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-268">You can locate topics dedicated tooeach area in which EntLib60 can assist by first visiting:</span></span>

* [<span data-ttu-id="7cd13-269">Enterprise Library 6 – 2013년 4월</span><span class="sxs-lookup"><span data-stu-id="7cd13-269">Enterprise Library 6 - April 2013</span></span>](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

<span data-ttu-id="7cd13-270">일시적 오류 처리에 대한 재시도 논리는 EntLib60을 이용할 수 있는 한 가지 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-270">Retry logic for handling transient errors is one area in which EntLib60 can assist:</span></span>

* [<span data-ttu-id="7cd13-271">4-해냈다, 모든의 전리품이 야의 암호: hello 일시적인 오류 처리 응용 프로그램 블록을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="7cd13-271">4 - Perseverance, Secret of All Triumphs: Using hello Transient Fault Handling Application Block</span></span>](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> <span data-ttu-id="7cd13-272">hello EntLib60에 대 한 소스 코드는 사용할 수 있는 공용 [다운로드](http://go.microsoft.com/fwlink/p/?LinkID=290898)합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-272">hello source code for EntLib60 is available for public [download](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span></span> <span data-ttu-id="7cd13-273">Microsoft는 계획 toomake 추가 기능이 없기 tooEntLib 업데이트 하는 업데이트 또는 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-273">Microsoft has no plans toomake further feature updates or maintenance updates tooEntLib.</span></span>
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a><span data-ttu-id="7cd13-274">일시적 오류 및 재시도용 EntLib60 클래스</span><span class="sxs-lookup"><span data-stu-id="7cd13-274">EntLib60 classes for transient errors and retry</span></span>
<span data-ttu-id="7cd13-275">아래의 EntLib60 클래스가 hello는 재시도 논리에 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-275">hello following EntLib60 classes are particularly useful for retry logic.</span></span> <span data-ttu-id="7cd13-276">이 경로 in, 또는을 더 이상 모든 네임 스페이스를 hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span><span class="sxs-lookup"><span data-stu-id="7cd13-276">All these  are in, or are further under, hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span></span>

<span data-ttu-id="7cd13-277">*Hello 네임 스페이스에서 **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span><span class="sxs-lookup"><span data-stu-id="7cd13-277">*In hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span></span>

* <span data-ttu-id="7cd13-278">**RetryPolicy** 클래스</span><span class="sxs-lookup"><span data-stu-id="7cd13-278">**RetryPolicy** class</span></span>
  
  * <span data-ttu-id="7cd13-279">**ExecuteAction** 메서드</span><span class="sxs-lookup"><span data-stu-id="7cd13-279">**ExecuteAction** method</span></span>
* <span data-ttu-id="7cd13-280">**ExponentialBackoff** 클래스</span><span class="sxs-lookup"><span data-stu-id="7cd13-280">**ExponentialBackoff** class</span></span>
* <span data-ttu-id="7cd13-281">**SqlDatabaseTransientErrorDetectionStrategy** 클래스</span><span class="sxs-lookup"><span data-stu-id="7cd13-281">**SqlDatabaseTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="7cd13-282">**ReliableSqlConnection** 클래스</span><span class="sxs-lookup"><span data-stu-id="7cd13-282">**ReliableSqlConnection** class</span></span>
  
  * <span data-ttu-id="7cd13-283">**ExecuteCommand** 메서드</span><span class="sxs-lookup"><span data-stu-id="7cd13-283">**ExecuteCommand** method</span></span>

<span data-ttu-id="7cd13-284">Hello 네임 스페이스에서 **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span><span class="sxs-lookup"><span data-stu-id="7cd13-284">In hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span></span>

* <span data-ttu-id="7cd13-285">**AlwaysTransientErrorDetectionStrategy** 클래스</span><span class="sxs-lookup"><span data-stu-id="7cd13-285">**AlwaysTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="7cd13-286">**NeverTransientErrorDetectionStrategy** 클래스</span><span class="sxs-lookup"><span data-stu-id="7cd13-286">**NeverTransientErrorDetectionStrategy** class</span></span>

<span data-ttu-id="7cd13-287">EntLib60에 대 한 링크 tooinformation 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-287">Here are links tooinformation about EntLib60:</span></span>

* <span data-ttu-id="7cd13-288">무료 [책 다운로드: 개발자 가이드 tooMicrosoft Enterprise Library 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span><span class="sxs-lookup"><span data-stu-id="7cd13-288">Free [Book Download: Developer's Guide tooMicrosoft Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span></span>
* <span data-ttu-id="7cd13-289">모범 사례: [재시도 일반 지침](../best-practices-retry-general.md) 에서 재시도 논리에 대해 깊이 있게 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-289">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span></span>
* <span data-ttu-id="7cd13-290">[Enterprise Library - 일시적 오류 처리 응용 프로그램 블록 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span><span class="sxs-lookup"><span data-stu-id="7cd13-290">NuGet download of [Enterprise Library - Transient Fault Handling application block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span></span>

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-hello-logging-block"></a><span data-ttu-id="7cd13-291">EntLib60: hello 로깅 블록</span><span class="sxs-lookup"><span data-stu-id="7cd13-291">EntLib60: hello logging block</span></span>
* <span data-ttu-id="7cd13-292">hello 로깅 블록은 매우 유연 하 게 구성 가능한 솔루션을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-292">hello Logging block is a highly flexible and configurable solution that allows you to:</span></span>
  
  * <span data-ttu-id="7cd13-293">다양한 위치에서 메시지를 만들고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-293">Create and store log messages in a wide variety of locations.</span></span>
  * <span data-ttu-id="7cd13-294">메시지를 분류 및 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-294">Categorize and filter messages.</span></span>
  * <span data-ttu-id="7cd13-295">디버깅, 추적, 감사 및 일반 로깅 요구 사항에 유용한 문맥 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-295">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span></span>
* <span data-ttu-id="7cd13-296">hello 로깅 블록 hello hello 응용 프로그램 코드는 hello 위치 및 hello 대상 로깅 저장소의 유형에 관계 없이 일관 되도록 기능 hello 로그 대상에서 로그를 추상화 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-296">hello Logging block abstracts hello logging functionality from hello log destination so that hello application code is consistent, irrespective of hello location and type of hello target logging store.</span></span>

<span data-ttu-id="7cd13-297">자세한 내용은 참조 하십시오: [5-으로 쉽게으로 떨어질 때 해제 정도 로그: 응용 프로그램 블록 로깅 hello를 사용 하 여](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="7cd13-297">For details see: [5 - As Easy As Falling Off a Log: Using hello Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span></span>

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a><span data-ttu-id="7cd13-298">EntLib60 IsTransient 메서드 소스 코드</span><span class="sxs-lookup"><span data-stu-id="7cd13-298">EntLib60 IsTransient method source code</span></span>
<span data-ttu-id="7cd13-299">그런 다음, hello에서 **SqlDatabaseTransientErrorDetectionStrategy** 클래스, hello에 대 한 hello C# 소스 코드는 **IsTransient** 메서드.</span><span class="sxs-lookup"><span data-stu-id="7cd13-299">Next, from hello **SqlDatabaseTransientErrorDetectionStrategy** class, is hello C# source code for hello **IsTransient** method.</span></span> <span data-ttu-id="7cd13-300">hello 소스 코드는 오류는 된 것으로 간주 toobe 일시적이 지 가치가 2013 년 4 월을 기준으로 다시 시도 하는 명확히 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-300">hello source code clarifies which errors were considered toobe transient and worthy of retry, as of April 2013.</span></span>

<span data-ttu-id="7cd13-301">다양 한 **//comment** 줄이 복사 tooemphasize 가독성에서 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-301">Numerous **//comment** lines have been removed from this copy tooemphasize readability.</span></span>

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in hello exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // hello service is currently busy. Retry hello request after 10 seconds.
            // Code: (reason code toobe decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode hello reason code from hello error message to
            // determine hello grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach hello decoded values as additional attributes to
            // hello original SQL exception.
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
            // hello instance of SQL Server you attempted tooconnect to
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


## <a name="next-steps"></a><span data-ttu-id="7cd13-302">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7cd13-302">Next steps</span></span>
* <span data-ttu-id="7cd13-303">다른 일반적인 Azure SQL 데이터베이스 연결 문제 문제 해결을 위해 방문 [문제 해결 연결 tooAzure SQL 데이터베이스 문제](sql-database-troubleshoot-common-connection-issues.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-303">For troubleshooting other common Azure SQL Database connection issues, visit [Troubleshoot connection issues tooAzure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span></span>
* [<span data-ttu-id="7cd13-304">SQL Server 연결 풀링(ADO.NET)</span><span class="sxs-lookup"><span data-stu-id="7cd13-304">SQL Server Connection Pooling (ADO.NET)</span></span>](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [<span data-ttu-id="7cd13-305">*다시 시도* 은 사용이 허가 하는 Apache 2.0 범용로 작성 된 라이브러리를 다시 시도 **Python**, toosimplify hello 추가 작업을 다시 시도 동작 toojust 있다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd13-305">*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in **Python**, toosimplify hello task of adding retry behavior toojust about anything.</span></span>](https://pypi.python.org/pypi/retrying)


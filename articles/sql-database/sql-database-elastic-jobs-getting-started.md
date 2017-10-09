---
title: "탄력적 데이터베이스 작업 aaaGetting 시작 | Microsoft Docs"
description: "어떻게 toouse 탄력적 데이터베이스 작업"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 2540de0e-2235-4cdd-9b6a-b841adba00e5
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: bc5894d2df4235738ab961db4f69c11cdf786cc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-elastic-database-jobs"></a><span data-ttu-id="34a1b-103">탄력적 데이터베이스 작업 시작</span><span class="sxs-lookup"><span data-stu-id="34a1b-103">Getting started with Elastic Database jobs</span></span>
<span data-ttu-id="34a1b-104">탄력적 데이터베이스 작업 (미리 보기) Azure SQL 데이터베이스 있습니다 tooreliability을 자동으로 재시도 하는 동안 여러 데이터베이스에 걸쳐 있는 T-SQL 스크립트를 실행 하 고 최종 완료 제공 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-104">Elastic Database jobs (preview) for Azure SQL Database allows you tooreliability execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees.</span></span> <span data-ttu-id="34a1b-105">Hello 탄력적 데이터베이스 작업 기능에 대 한 자세한 내용은 hello를 참조 하십시오 [기능 개요 페이지](sql-database-elastic-jobs-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-105">For more information about hello Elastic Database job feature, please see hello [feature overview page](sql-database-elastic-jobs-overview.md).</span></span>

<span data-ttu-id="34a1b-106">이 항목에는 hello 샘플 확장 [탄력적 데이터베이스 도구 시작](sql-database-elastic-scale-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-106">This topic extends hello sample found in [Getting started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span> <span data-ttu-id="34a1b-107">완료 되 면 됩니다: 자세한 방법을 toocreate 및 관련 된 데이터베이스의 그룹을 관리 하는 작업을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-107">When completed, you will: learn how toocreate and manage jobs that manage a group of related databases.</span></span> <span data-ttu-id="34a1b-108">순서 tootake 활용 hello 활용 탄력적 작업의에서 필수 toouse hello 탄력적인 크기 조정 도구는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-108">It is not required toouse hello Elastic Scale tools in order tootake advantage of hello benefits of Elastic jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34a1b-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="34a1b-109">Prerequisites</span></span>
<span data-ttu-id="34a1b-110">다운로드 및 실행 hello [탄력적 데이터베이스 도구 샘플 시작](sql-database-elastic-scale-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-110">Download and run hello [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a><span data-ttu-id="34a1b-111">분할 맵 hello 샘플 응용 프로그램을 사용 하 여 관리자 만들기</span><span class="sxs-lookup"><span data-stu-id="34a1b-111">Create a shard map manager using hello sample app</span></span>
<span data-ttu-id="34a1b-112">여기에서는 만듭니다 분할 맵은 다음 데이터 삽입 hello 분할 된 데이터베이스를 여러 분할 영역 함께 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-112">Here you will create a shard map manager along with several shards, followed by insertion of data into hello shards.</span></span> <span data-ttu-id="34a1b-113">이미 분할 된 데이터베이스에 분할 된 데이터를 사용 하 여 설정 하는 경우 단계를 수행 하는 hello 건너뛰고 toohello 다음 섹션을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-113">If you already have shards set up with sharded data in them, you can skip hello following steps and move toohello next section.</span></span>

1. <span data-ttu-id="34a1b-114">빌드 및 실행 hello **탄력적 데이터베이스 도구 시작** 샘플 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-114">Build and run hello **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="34a1b-115">Hello 섹션에는 7 단계까지 hello 단계에 따라 [다운로드 하 고 hello 샘플 응용 프로그램을 실행](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app)합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-115">Follow hello steps until step 7 in hello section [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="34a1b-116">7 단계의 hello 끝 hello 명령 프롬프트에 다음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-116">At hello end of Step 7, you will see hello following command prompt:</span></span>

   ![명령 프롬프트](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. <span data-ttu-id="34a1b-118">Hello 명령 창에서 "1"을 입력 한 키를 누릅니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-118">In hello command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="34a1b-119">Hello shard map manager 만들고 두 명의 분할 된 데이터베이스 toohello 서버에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-119">This creates hello shard map manager, and adds two shards toohello server.</span></span> <span data-ttu-id="34a1b-120">그런 다음 "3"을 입력하고 **Enter** 키를 누릅니다. 이 작업을 4번 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-120">Then type "3" and press **Enter**; repeat this action four times.</span></span> <span data-ttu-id="34a1b-121">이 명령은 분할된 데이터베이스에 샘플 데이터행을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-121">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="34a1b-122">hello [Azure 포털](https://portal.azure.com) 세 개의 새 데이터베이스가 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-122">hello [Azure Portal](https://portal.azure.com) should show three new databases:</span></span>

   ![Visual Studio 확인](./media/sql-database-elastic-query-getting-started/portal.png)

   <span data-ttu-id="34a1b-124">이 시점에서 분할 맵은 hello에서 모든 hello 데이터베이스를 반영 하는 사용자 지정 데이터베이스 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-124">At this point, we will create a custom database collection that reflects all hello databases in hello shard map.</span></span> <span data-ttu-id="34a1b-125">이 toocreate 수 있도록 허용 하 고 분할 된 데이터베이스에서 새 테이블을 추가 하는 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-125">This will allow us toocreate and execute a job that add a new table across shards.</span></span>

<span data-ttu-id="34a1b-126">여기에서는 일반적으로 해지기 분할 맵 대상 hello를 사용 하 여 **새로 AzureSqlJobTarget** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="34a1b-126">Here we would usually create a shard map target, using hello **New-AzureSqlJobTarget** cmdlet.</span></span> <span data-ttu-id="34a1b-127">hello shard map manager 데이터베이스는 데이터베이스 대상으로 설정 해야 하 고 hello 특정 분할 맵은 대상으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-127">hello shard map manager database must be set as a database target and then hello specific shard map is specified as a target.</span></span> <span data-ttu-id="34a1b-128">대신, 진행 중인 tooenumerate 모든 hello에에서는 데이터베이스가 hello 서버 하 고 hello 데이터베이스 toohello 새 사용자 지정 컬렉션 master 데이터베이스의 hello 예외를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-128">Instead, we are going tooenumerate all hello databases in hello server and add hello databases toohello new custom collection with hello exception of master database.</span></span>

## <a name="creates-a-custom-collection-and-add-all-databases-in-hello-server-toohello-custom-collection-target-with-hello-exception-of-master"></a><span data-ttu-id="34a1b-129">사용자 지정 컬렉션을 만들고 마스터의 hello 예외로 hello 서버 toohello 사용자 지정 컬렉션을 대상에 모든 데이터베이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-129">Creates a custom collection and add all databases in hello server toohello custom collection target with hello exception of master.</span></span>
   ```
    $customCollectionName = "dbs_in_server"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $ResourceGroupName = "ddove_samples"
    $ServerName = "samples"
    $dbsinserver = Get-AzureRMSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName
    $dbsinserver | %{
    $currentdb = $_.DatabaseName
    $ErrorActionPreference = "Stop"
    Write-Output ""

    Try
    {
       New-AzureSqlJobTarget -ServerName $ServerName -DatabaseName $currentdb | Write-Output
    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already a database target."
        }

        else
        {
            throw $_
        }

    }

    Try
    {
        if ($currentdb -eq "master")
        {
            Write-Host $currentdb "will not be added custom collection target" $CustomCollectionName "."
        }

        else
        {
            Add-AzureSqlJobChildTarget -CustomCollectionName $CustomCollectionName -ServerName $ServerName -DatabaseName $currentdb
            Write-Host $currentdb "was added to" $CustomCollectionName "."
        }

    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already in hello custom collection target" $CustomCollectionName"."
        }

        else
        {
            throw $_
        }
    }
    $ErrorActionPreference = "Continue"
   }
   ```
## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="34a1b-130">데이터베이스에서 실행할 T-SQL 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="34a1b-130">Create a T-SQL Script for execution across databases</span></span>
   ```
    $scriptName = "NewTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'Test')
    BEGIN
        CREATE TABLE Test(
            TestId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO Test(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script
   ```

## <a name="create-hello-job-tooexecute-a-script-across-hello-custom-group-of-databases"></a><span data-ttu-id="34a1b-131">데이터베이스의 사용자 지정 그룹 hello에 걸쳐 hello 작업 tooexecute 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="34a1b-131">Create hello job tooexecute a script across hello custom group of databases</span></span>

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-hello-job"></a><span data-ttu-id="34a1b-132">Hello 작업 실행</span><span class="sxs-lookup"><span data-stu-id="34a1b-132">Execute hello job</span></span>
<span data-ttu-id="34a1b-133">PowerShell 스크립트 뒤 hello 사용된 tooexecute 기존 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-133">hello following PowerShell script can be used tooexecute an existing job:</span></span>

<span data-ttu-id="34a1b-134">다음 실행 하는 변수 tooreflect hello 원하는 작업 이름 toohave hello를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-134">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="34a1b-135">단일 작업 실행의 hello 상태를 검색</span><span class="sxs-lookup"><span data-stu-id="34a1b-135">Retrieve hello state of a single job execution</span></span>
<span data-ttu-id="34a1b-136">사용 하 여 hello 동일 **Get AzureSqlJobExecution** hello 사용 하 여 cmdlet **includechildren를 실행** 자식 작업 실행의 매개 변수 tooview hello 상태 각각에 대해 각 작업 실행에 대 한 특정 상태를 즉 hello hello 작업의 대상인 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-136">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-hello-state-across-multiple-job-executions"></a><span data-ttu-id="34a1b-137">여러 작업 실행 간에 hello 상태 보기</span><span class="sxs-lookup"><span data-stu-id="34a1b-137">View hello state across multiple job executions</span></span>
<span data-ttu-id="34a1b-138">hello **Get AzureSqlJobExecution** cmdlet에 사용 되는 toodisplay 일 수 있는 여러 선택적 매개 변수가 제공 hello 매개 변수를 통해 필터링, 작업 실행이 여러 개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-138">hello **Get-AzureSqlJobExecution** cmdlet has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="34a1b-139">hello 다음 hello 가지가 toouse Get AzureSqlJobExecution의 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-139">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="34a1b-140">모든 활성 최상위 작업 실행을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-140">Retrieve all active top level job executions:</span></span>

   ```
    Get-AzureSqlJobExecution
   ```

<span data-ttu-id="34a1b-141">비활성 작업 실행을 포함하여 모든 최상위 작업 실행을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-141">Retrieve all top level job executions, including inactive job executions:</span></span>

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

<span data-ttu-id="34a1b-142">비활성 작업 실행을 포함하여 제공된 작업 실행 ID의 모든 자식 작업 실행을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-142">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

<span data-ttu-id="34a1b-143">비활성 작업을 포함하여 일정/작업 조합으로 만든 모든 작업 실행을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-143">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

<span data-ttu-id="34a1b-144">비활성 작업을 포함하여 지정된 분할된 데이터베이스 맵을 대상으로 하는 모든 작업을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-144">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="34a1b-145">비활성 작업을 포함하여 지정된 사용자 지정 컬렉션을 대상으로 하는 모든 작업을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-145">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="34a1b-146">특정 작업 실행 내에서 작업 태스크 실행의 hello 목록 검색:</span><span class="sxs-lookup"><span data-stu-id="34a1b-146">Retrieve hello list of job task executions within a specific job execution:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

<span data-ttu-id="34a1b-147">작업 태스크 실행 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-147">Retrieve job task execution details:</span></span>

<span data-ttu-id="34a1b-148">hello PowerShell 스크립트 뒤의 실행 실패를 디버깅할 때 매우 유용 작업 작업 실행을 사용 하는 tooview hello 세부 정보 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-148">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a><span data-ttu-id="34a1b-149">작업 태스크 실행 내의 오류 검색</span><span class="sxs-lookup"><span data-stu-id="34a1b-149">Retrieve failures within job task executions</span></span>
<span data-ttu-id="34a1b-150">hello JobTaskExecution 개체에 hello 메시지 속성과 함께 hello 작업의 수명 주기에 대 한 속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-150">hello JobTaskExecution object includes a property for hello Lifecycle of hello task along with a Message property.</span></span> <span data-ttu-id="34a1b-151">작업 작업 실행이 실패 hello 수명 주기 속성이 설정 됩니다 너무*실패* toohello 결과 예외 메시지 및 스택 hello 메시지 속성이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-151">If a job task execution failed, hello Lifecycle property will be set too*Failed* and hello Message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="34a1b-152">작업이 수행 되지 않은 경우 지정된 된 작업에 대 한 실패 작업 실행 태스크가의 중요 한 tooview hello 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-152">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions)
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }
   ```

## <a name="waiting-for-a-job-execution-toocomplete"></a><span data-ttu-id="34a1b-153">작업 실행 toocomplete 대기 중</span><span class="sxs-lookup"><span data-stu-id="34a1b-153">Waiting for a job execution toocomplete</span></span>
<span data-ttu-id="34a1b-154">PowerShell 스크립트 뒤 hello 작업 작업 toocomplete에 대 한 사용된 toowait 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-154">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="34a1b-155">사용자 지정 실행 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="34a1b-155">Create a custom execution policy</span></span>
<span data-ttu-id="34a1b-156">탄력적 데이터베이스 작업은 작업을 시작할 때 적용할 수 있는 사용자 지정 실행 정책 만들기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-156">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="34a1b-157">실행 정책은 현재 다음과 같은 정의를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-157">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="34a1b-158">Hello 실행 정책에 대 한 이름: 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-158">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="34a1b-159">작업 시간 제한: 탄력적 데이터베이스 작업에 의해 작업이 취소되기 전의 총 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-159">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="34a1b-160">첫 번째 다시 시도 하기 전에 초기 다시 시도 간격: 간격 toowait 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-160">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="34a1b-161">다시 시도 간격 toouse의 최대 다시 시도 간격: 상한입니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-161">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="34a1b-162">다시 시도 간격 백오프 계수: 계수가 toocalculate hello 다음 재시도 간격을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-162">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="34a1b-163">hello 다음 수식을 사용 하는: (초기 재시도 간격) * Math.pow ((계수 백오프 간격) (다시 시도 횟수)-2).</span><span class="sxs-lookup"><span data-stu-id="34a1b-163">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span>
* <span data-ttu-id="34a1b-164">작업 내에서 다시 시도 횟수 tooperform의 최대 시도 횟수: hello의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-164">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="34a1b-165">hello 기본 실행 정책은 다음 값에는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-165">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="34a1b-166">이름: 기본 실행 정책</span><span class="sxs-lookup"><span data-stu-id="34a1b-166">Name: Default execution policy</span></span>
* <span data-ttu-id="34a1b-167">작업 시간 제한: 1주</span><span class="sxs-lookup"><span data-stu-id="34a1b-167">Job Timeout: 1 week</span></span>
* <span data-ttu-id="34a1b-168">초기 재시도 간격: 100밀리초</span><span class="sxs-lookup"><span data-stu-id="34a1b-168">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="34a1b-169">최대 재시도 간격: 30분</span><span class="sxs-lookup"><span data-stu-id="34a1b-169">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="34a1b-170">재시도 간격 계수: 2</span><span class="sxs-lookup"><span data-stu-id="34a1b-170">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="34a1b-171">최대 시도 횟수: 2,147,483,647</span><span class="sxs-lookup"><span data-stu-id="34a1b-171">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="34a1b-172">원하는 hello 실행 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-172">Create hello desired execution policy:</span></span>

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy
   ```

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="34a1b-173">사용자 지정 실행 정책 업데이트</span><span class="sxs-lookup"><span data-stu-id="34a1b-173">Update a custom execution policy</span></span>
<span data-ttu-id="34a1b-174">원하는 hello 실행 정책 tooupdate를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-174">Update hello desired execution policy tooupdate:</span></span>

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy
   ```

## <a name="cancel-a-job"></a><span data-ttu-id="34a1b-175">작업 취소</span><span class="sxs-lookup"><span data-stu-id="34a1b-175">Cancel a job</span></span>
<span data-ttu-id="34a1b-176">탄력적 데이터베이스 작업은 작업 취소 요청을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-176">Elastic Database Jobs supports jobs cancellation requests.</span></span>  <span data-ttu-id="34a1b-177">탄력적 데이터베이스 작업에서 현재 실행 중인 작업에 대 한 취소 요청을 감지한 경우 toostop hello 작업을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-177">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="34a1b-178">탄력적 데이터베이스 작업이 취소를 수행할 수 있는 방법에는 다음 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-178">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="34a1b-179">현재 실행 취소 작업: 작업이 현재 실행 되는 동안 취소가 검색 되 면 취소가 현재 hello 작업의 측면을 실행 하는 hello 내에서 시도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-179">Canceling Currently Executing Tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="34a1b-180">예를 들어: 시도가 toocancel hello 쿼리 됩니다는 장기 실행 쿼리는 취소 하려고 할 때 현재 수행 중인 경우.</span><span class="sxs-lookup"><span data-stu-id="34a1b-180">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="34a1b-181">태스크 다시 시도 취소 하는 중: 취소가 실행에 대 한 태스크를 시작 하기 전에 hello 제어 스레드에 의해 검색 되 면 hello 제어 스레드 됩니다 하지 않도록 hello 작업을 시작 하 고 취소 됨으로 hello 요청을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-181">Canceling Task Retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="34a1b-182">부모 작업에 대 한 작업 취소가 요청 하 고 모든 해당 자식 작업에 대 한 hello 부모 작업에 대 한 hello 취소 요청이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-182">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="34a1b-183">toosubmit 취소 요청을 사용 하 여 hello **중지 AzureSqlJobExecution** cmdlet 및 집합 hello **JobExecutionId** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-183">toosubmit a cancellation request, use hello **Stop-AzureSqlJobExecution** cmdlet and set hello **JobExecutionId** parameter.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-hello-jobs-history"></a><span data-ttu-id="34a1b-184">작업 이름 및 hello 작업 기록 삭제</span><span class="sxs-lookup"><span data-stu-id="34a1b-184">Delete a job by name and hello job's history</span></span>
<span data-ttu-id="34a1b-185">탄력적 데이터베이스 작업은 비동기 작업 삭제를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-185">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="34a1b-186">작업을 삭제 하도록 표시할 수 있습니다 및 hello 작업에 대 한 모든 작업 실행 완료 된 후 hello 시스템 hello 작업 및 모든 작업 기록을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-186">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="34a1b-187">hello 시스템 활성 작업 실행 될 때 자동으로 취소 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-187">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="34a1b-188">대신, 중지 AzureSqlJobExecution 호출 된 toocancel 활성 작업 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-188">Instead, Stop-AzureSqlJobExecution must be invoked toocancel active job executions.</span></span>

<span data-ttu-id="34a1b-189">tootrigger 작업 삭제를 사용 하 여 hello **제거 AzureSqlJob** cmdlet 및 집합 hello **JobName** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-189">tootrigger job deletion, use hello **Remove-AzureSqlJob** cmdlet and set hello **JobName** parameter.</span></span>

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a><span data-ttu-id="34a1b-190">사용자 지정 데이터베이스 대상 만들기</span><span class="sxs-lookup"><span data-stu-id="34a1b-190">Create a custom database target</span></span>
<span data-ttu-id="34a1b-191">실행에 직접 사용하거나 사용자 지정 데이터베이스 그룹에 포함할 수 있는 탄력적 데이터베이스 작업에서 사용자 지정 데이터베이스 대상을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-191">Custom database targets can be defined in Elastic Database jobs which can be used either for execution directly or for inclusion within a custom database group.</span></span> <span data-ttu-id="34a1b-192">이후 **탄력적 풀** 아직 직접 사용할 수 없습니다 hello PowerShell Api를 통해 단순히 만들면 사용자 지정 데이터베이스 대상과 hello 풀에서 모든 hello 데이터베이스를 포괄 하는 사용자 지정 데이터베이스 컬렉션 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-192">Since **elastic pools** are not yet directly supported via hello PowerShell APIs, you simply create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="34a1b-193">Hello 다음 변수 tooreflect hello 필요한 데이터베이스 정보를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-193">Set hello following variables tooreflect hello desired database information:</span></span>

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a><span data-ttu-id="34a1b-194">사용자 지정 데이터베이스 컬렉션 대상 만들기</span><span class="sxs-lookup"><span data-stu-id="34a1b-194">Create a custom database collection target</span></span>
<span data-ttu-id="34a1b-195">사용자 지정 데이터베이스 컬렉션 대상이 여러 개 정의 된 데이터베이스 대상 정의 tooenable 실행 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-195">A custom database collection target can be defined tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="34a1b-196">데이터베이스 그룹을 만든 후 데이터베이스 관련된 toohello 사용자 지정 컬렉션 대상이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-196">After a database group is created, databases can be associated toohello custom collection target.</span></span>

<span data-ttu-id="34a1b-197">같은 변수 tooreflect hello 원하는 사용자 지정 컬렉션 대상 구성이 hello를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-197">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="34a1b-198">데이터베이스 tooa 사용자 지정 데이터베이스 컬렉션 대상 추가</span><span class="sxs-lookup"><span data-stu-id="34a1b-198">Add databases tooa custom database collection target</span></span>
<span data-ttu-id="34a1b-199">데이터베이스 대상 사용자 지정 데이터베이스 컬렉션 대상 toocreate 데이터베이스 그룹을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-199">Database targets can be associated with custom database collection targets toocreate a group of databases.</span></span> <span data-ttu-id="34a1b-200">대상 사용자 지정 데이터베이스 컬렉션 대상 작업을 만들 때마다 실행의 hello 시간에서 확장된 tootarget hello 데이터베이스 관련된 toohello 그룹 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-200">Whenever a job is created that targets a custom database collection target, it will be expanded tootarget hello databases associated toohello group at hello time of execution.</span></span>

<span data-ttu-id="34a1b-201">원하는 hello 데이터베이스 tooa 특정 사용자 지정 컬렉션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-201">Add hello desired database tooa specific custom collection:</span></span>

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="34a1b-202">사용자 지정 데이터베이스 컬렉션 대상 내에서 데이터베이스를 hello 검토</span><span class="sxs-lookup"><span data-stu-id="34a1b-202">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="34a1b-203">사용 하 여 hello **Get AzureSqlJobTarget** cmdlet tooretrieve hello 자식 데이터베이스 사용자 지정 데이터베이스 컬렉션 대상 내에서.</span><span class="sxs-lookup"><span data-stu-id="34a1b-203">Use hello **Get-AzureSqlJobTarget** cmdlet tooretrieve hello child databases within a custom database collection target.</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="34a1b-204">사용자 지정 데이터베이스 수집 대상에서 작업 tooexecute 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="34a1b-204">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="34a1b-205">사용 하 여 hello **새로 AzureSqlJob** cmdlet toocreate 그룹 사용자 지정 데이터베이스 컬렉션 대상에 의해 정의 된 데이터베이스에 대해 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-205">Use hello **New-AzureSqlJob** cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="34a1b-206">탄력적 데이터베이스 작업을 각각 해당 tooa 데이터베이스 hello 사용자 지정 데이터베이스 컬렉션 대상과 연결 된 및 hello 스크립트 각 데이터베이스에 대해 실행 되도록 확인 여러 자식 작업으로 hello 작업으로 확장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-206">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="34a1b-207">마찬가지로 스크립트 idempotent toobe 탄력적인 tooretries 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-207">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a><span data-ttu-id="34a1b-208">데이터베이스에서 데이터 수집</span><span class="sxs-lookup"><span data-stu-id="34a1b-208">Data collection across databases</span></span>
<span data-ttu-id="34a1b-209">**탄력적 데이터베이스 작업** 데이터베이스 그룹에 대해 쿼리 실행을 지원 하 고 hello 결과 tooa 지정 된 데이터베이스의 테이블을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-209">**Elastic Database jobs** supports executing a query across a group of databases and sends hello results tooa specified database’s table.</span></span> <span data-ttu-id="34a1b-210">각 데이터베이스의 hello 팩트 toosee hello 쿼리 결과 후 hello 테이블을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-210">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="34a1b-211">이 쿼리를 제공 비동기 메커니즘 tooexecute 많은 데이터베이스에 걸쳐 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-211">This provides an asynchronous mechanism tooexecute a query across many databases.</span></span> <span data-ttu-id="34a1b-212">일시적으로 사용할 수 없게 하는 hello 데이터베이스 중 하 나와 같은 오류가 발생할 경우 재시도 통해 자동으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-212">Failure cases such as one of hello databases being temporarily unavailable are handled automatically via retries.</span></span>

<span data-ttu-id="34a1b-213">아직 존재 하지 않는 경우 hello 지정 된 대상 테이블이 자동으로 생성 됩니다, 그리고 일치 하는 hello 스키마 hello의 결과 집합을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-213">hello specified destination table will be automatically created if it does not yet exist, matching hello schema of hello returned result set.</span></span> <span data-ttu-id="34a1b-214">스크립트를 실행 하는 여러 결과 집합을 반환 하는 경우 탄력적 데이터베이스 작업 hello 첫 번째 하나의 toohello 제공 된 대상 테이블에만 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-214">If a script execution returns multiple result sets, Elastic Database jobs will only send hello first one toohello provided destination table.</span></span>

<span data-ttu-id="34a1b-215">PowerShell 스크립트 뒤 hello 사용된 tooexecute 지정된 된 테이블에 결과 수집 하는 스크립트 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-215">hello following PowerShell script can be used tooexecute a script collecting its results into a specified table.</span></span> <span data-ttu-id="34a1b-216">이 스크립트는 단일 결과 집합을 출력하는 T-SQL 스크립트가 생성되었으며 사용자 지정 데이터베이스 컬렉션 대상이 생성되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-216">This script assumes that a T-SQL script has been created which outputs a single result set and a custom database collection target has been created.</span></span>

<span data-ttu-id="34a1b-217">Hello tooreflect hello 필요한 스크립트, 자격 증명 및 실행 대상 다음을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-217">Set hello following tooreflect hello desired script, credentials, and execution target:</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="34a1b-218">데이터 수집 시나리오에 대한 작업 만들기 및 시작</span><span class="sxs-lookup"><span data-stu-id="34a1b-218">Create and start a job for data collection scenarios</span></span>
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a><span data-ttu-id="34a1b-219">작업 트리거를 사용하여 작업 실행 일정 만들기</span><span class="sxs-lookup"><span data-stu-id="34a1b-219">Create a schedule for job execution using a job trigger</span></span>
<span data-ttu-id="34a1b-220">PowerShell 스크립트 뒤 hello 사용된 toocreate 되풀이 해야 일정 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-220">hello following PowerShell script can be used toocreate a reoccurring schedule.</span></span> <span data-ttu-id="34a1b-221">이 스크립트는 1분 간격을 사용하지만 New-AzureSqlJobSchedule은 -DayInterval, -HourInterval, -MonthInterval 및 -WeekInterval 매개 변수도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-221">This script uses a one minute interval, but New-AzureSqlJobSchedule also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="34a1b-222">-OneTime을 전달하여 한 번만 실행되는 일정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-222">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="34a1b-223">새 일정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-223">Create a new schedule:</span></span>
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-toohave-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="34a1b-224">작업 트리거 toohave 된 일정에서 실행 되는 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="34a1b-224">Create a job trigger toohave a job executed on a time schedule</span></span>
<span data-ttu-id="34a1b-225">작업 트리거는 정의 된 실행 작업에 따라 tooa 시간 일정 toohave 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-225">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="34a1b-226">PowerShell 스크립트 뒤 hello 사용된 toocreate 작업 트리거 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-226">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="34a1b-227">변수 toocorrespond toohello 원하는 작업을 수행 하는 hello를 설정 하 고 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-227">Set hello following variables toocorrespond toohello desired job and schedule:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="34a1b-228">일정에 따라 실행 예약 된 연결 toostop 작업을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-228">Remove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="34a1b-229">작업 트리거 hello 작업 트리거를 통해 작업 실행을 다시 발생 toodiscontinue는 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-229">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span>
<span data-ttu-id="34a1b-230">실행 되는 작업의 작업 트리거 toostop 제거 hello를 사용 하 여 따라 tooa 일정 **제거 AzureSqlJobTrigger** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="34a1b-230">Remove a job trigger toostop a job from being executed according tooa schedule using hello **Remove-AzureSqlJobTrigger** cmdlet.</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-tooexcel"></a><span data-ttu-id="34a1b-231">탄력적 데이터베이스 쿼리 결과 tooExcel 가져오기</span><span class="sxs-lookup"><span data-stu-id="34a1b-231">Import elastic database query results tooExcel</span></span>
 <span data-ttu-id="34a1b-232">쿼리 tooan Excel 파일의 hello 결과를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-232">You can import hello results from of a query tooan Excel file.</span></span>

1. <span data-ttu-id="34a1b-233">Excel 2013을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-233">Launch Excel 2013.</span></span>
2. <span data-ttu-id="34a1b-234">Toohello 이동 **데이터** 리본.</span><span class="sxs-lookup"><span data-stu-id="34a1b-234">Navigate toohello **Data** ribbon.</span></span>
3. <span data-ttu-id="34a1b-235">**기타 원본에서**을 클릭하고 **SQL Server에서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-235">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![다른 원본에서 Excel 가져오기](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. <span data-ttu-id="34a1b-237">Hello에 **데이터 연결 마법사** hello 서버 이름 및 로그인 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-237">In hello **Data Connection Wizard** type hello server name and login credentials.</span></span> <span data-ttu-id="34a1b-238">그런 후 **Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-238">Then click **Next**.</span></span>
5. <span data-ttu-id="34a1b-239">Hello 대화 상자에서 **원하는 hello 데이터가 들어 있는 Select hello 데이터베이스**선택, hello **ElasticDBQuery** 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-239">In hello dialog box **Select hello database that contains hello data you want**, select hello **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="34a1b-240">선택 hello **고객** hello 목록 뷰에서 테이블 마우스 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-240">Select hello **Customers** table in hello list view and click **Next**.</span></span> <span data-ttu-id="34a1b-241">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-241">Then click **Finish**.</span></span>
7. <span data-ttu-id="34a1b-242">Hello에 **데이터 가져오기** 양식의 **표시할 방법을 선택 tooview이이 데이터 통합 문서에서**선택, **테이블** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-242">In hello **Import Data** form, under **Select how you want tooview this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="34a1b-243">행을 hello 모든 **고객** 다른 분할 영역에 저장 된 테이블을 채우는 hello Excel 시트입니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-243">All hello rows from **Customers** table, stored in different shards populate hello Excel sheet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34a1b-244">다음 단계</span><span class="sxs-lookup"><span data-stu-id="34a1b-244">Next steps</span></span>
<span data-ttu-id="34a1b-245">이제 Excel의 데이터 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-245">You can now use Excel’s data functions.</span></span> <span data-ttu-id="34a1b-246">연결 문자열 hello를 사용 하 여을 서버 이름으로, 데이터베이스 이름 및 tooconnect BI와 데이터 통합 도구 toohello 탄력적 쿼리 데이터베이스 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-246">Use hello connection string with your server name, database name and credentials tooconnect your BI and data integration tools toohello elastic query database.</span></span> <span data-ttu-id="34a1b-247">SQL Server 도구에 대한 데이터 소스로 지원 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-247">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="34a1b-248">Toohello 탄력적 쿼리 데이터베이스와 다른 SQL Server 데이터베이스와 마찬가지로 외부 테이블 및 SQL Server 테이블을 연결 하는 toowith 하는 도구를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="34a1b-248">Refer toohello elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect toowith your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="34a1b-249">비용</span><span class="sxs-lookup"><span data-stu-id="34a1b-249">Cost</span></span>
<span data-ttu-id="34a1b-250">Hello 탄력적 데이터베이스 쿼리 기능을 사용 하는 것에 대 한 추가 비용 없이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-250">There is no additional charge for using hello Elastic Database query feature.</span></span> <span data-ttu-id="34a1b-251">그러나이 현재가이 기능은 premium 데이터베이스 에서만 사용할 수는 끝점으로 되지만 모든 서비스 계층의 hello 분할 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34a1b-251">However, at this time this feature is available only on premium databases as an end point, but hello shards can be of any service tier.</span></span>

<span data-ttu-id="34a1b-252">가격 정보는 [SQL 데이터베이스 가격 정보](https://azure.microsoft.com/pricing/details/sql-database/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34a1b-252">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->

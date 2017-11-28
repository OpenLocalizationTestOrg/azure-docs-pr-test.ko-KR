---
title: "Elastic Database 작업 시작 | Microsoft Docs"
description: "탄력적 데이터베이스 작업을 사용하는 방법"
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
ms.openlocfilehash: 05c20e880d4eb1eacdecc0c4c7e7491dfe1e6a89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-elastic-database-jobs"></a><span data-ttu-id="641a6-103">탄력적 데이터베이스 작업 시작</span><span class="sxs-lookup"><span data-stu-id="641a6-103">Getting started with Elastic Database jobs</span></span>
<span data-ttu-id="641a6-104">Azure SQL 데이터베이스에 대한 탄력적 데이터베이스 작업(미리 보기)을 사용하면 자동으로 다시 시도하여 최종 완료를 보장하는 동시에 여러 데이터베이스에 걸친 T-SQL 스크립트를 안정적으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-104">Elastic Database jobs (preview) for Azure SQL Database allows you to reliability execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees.</span></span> <span data-ttu-id="641a6-105">탄력적 데이터베이스 작업 기능에 대한 자세한 내용은 [기능 개요 페이지](sql-database-elastic-jobs-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="641a6-105">For more information about the Elastic Database job feature, please see the [feature overview page](sql-database-elastic-jobs-overview.md).</span></span>

<span data-ttu-id="641a6-106">이 항목에 확장 샘플은 [탄력적 데이터베이스 도구 시작](sql-database-elastic-scale-get-started.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-106">This topic extends the sample found in [Getting started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span> <span data-ttu-id="641a6-107">완료되면 관련 데이터베이스 그룹을 관리하는 작업을 만들고 관리하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-107">When completed, you will: learn how to create and manage jobs that manage a group of related databases.</span></span> <span data-ttu-id="641a6-108">탄력적 작업의 이점을 활용하기 위해 탄력적 확장 도구를 사용할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-108">It is not required to use the Elastic Scale tools in order to take advantage of the benefits of Elastic jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="641a6-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="641a6-109">Prerequisites</span></span>
<span data-ttu-id="641a6-110">[탄력적 데이터베이스 도구 샘플 시작](sql-database-elastic-scale-get-started.md)을 다운로드하고 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="641a6-110">Download and run the [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-the-sample-app"></a><span data-ttu-id="641a6-111">샘플 응용 프로그램을 사용하여 분할된 데이터베이스 맵 관리자 만들기</span><span class="sxs-lookup"><span data-stu-id="641a6-111">Create a shard map manager using the sample app</span></span>
<span data-ttu-id="641a6-112">분할된 데이터베이스 안의 삽입된 데이터에 따라 여느 분할된 데이터 베이스와 마찬가지로 분할된 데이터 베이스 관리자를 만들수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-112">Here you will create a shard map manager along with several shards, followed by insertion of data into the shards.</span></span> <span data-ttu-id="641a6-113">이미 분할된 데이터가 설치되어 있는 분할된 데이터베이스가 있다면, 다음 단계들을 건너뛰고 다음 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-113">If you already have shards set up with sharded data in them, you can skip the following steps and move to the next section.</span></span>

1. <span data-ttu-id="641a6-114">**탄력적 데이터베이스 도구 응용 프로그램** 을 빌드하고 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="641a6-114">Build and run the **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="641a6-115">[샘플 앱 다운로드 및 실행](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app)섹션에서 7단계까지 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-115">Follow the steps until step 7 in the section [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="641a6-116">7단계를 끝내면 다음 명령 프롬프트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-116">At the end of Step 7, you will see the following command prompt:</span></span>

   ![명령 프롬프트](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. <span data-ttu-id="641a6-118">명령 창에 "1"을 입력하고 **Enter**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-118">In the command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="641a6-119">이 명령은 분할된 데이터베이스 관리자를 생성 및 두 분할된 데이터베이스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-119">This creates the shard map manager, and adds two shards to the server.</span></span> <span data-ttu-id="641a6-120">그런 다음 "3"을 입력하고 **Enter** 키를 누릅니다. 이 작업을 4번 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-120">Then type "3" and press **Enter**; repeat this action four times.</span></span> <span data-ttu-id="641a6-121">이 명령은 분할된 데이터베이스에 샘플 데이터행을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-121">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="641a6-122">[Azure Portal](https://portal.azure.com)에서 다음 3개의 새 데이터베이스가 보여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-122">The [Azure Portal](https://portal.azure.com) should show three new databases:</span></span>

   ![Visual Studio 확인](./media/sql-database-elastic-query-getting-started/portal.png)

   <span data-ttu-id="641a6-124">이 시점에서 분할된 데이터베이스 맵에 있는 모든 데이터베이스를 반영하는 사용자 지정 데이터베이스 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-124">At this point, we will create a custom database collection that reflects all the databases in the shard map.</span></span> <span data-ttu-id="641a6-125">그러면 분할된 데이터베이스에서 새 테이블을 추가하는 작업을 만들고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-125">This will allow us to create and execute a job that add a new table across shards.</span></span>

<span data-ttu-id="641a6-126">일반적으로 여기서 **New-AzureSqlJobTarget** cmdlet을 사용하여 분할된 데이터베이스 맵 대상을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-126">Here we would usually create a shard map target, using the **New-AzureSqlJobTarget** cmdlet.</span></span> <span data-ttu-id="641a6-127">분할된 데이터베이스 맵 관리자 데이터베이스를 데이터베이스 대상으로 설정해야 하며, 그러면 분할된 특정 데이터베이스 맵이 대상으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-127">The shard map manager database must be set as a database target and then the specific shard map is specified as a target.</span></span> <span data-ttu-id="641a6-128">대신, 서버에 있는 모든 데이터베이스를 열거하고 master 데이터베이스 이외의 데이터베이스를 새 사용자 지정 컬렉션에 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-128">Instead, we are going to enumerate all the databases in the server and add the databases to the new custom collection with the exception of master database.</span></span>

## <a name="creates-a-custom-collection-and-add-all-databases-in-the-server-to-the-custom-collection-target-with-the-exception-of-master"></a><span data-ttu-id="641a6-129">사용자 지정 컬렉션을 만들고 마스터를 제외한 서버의 모든 데이터베이스를 사용자 지정 컬렉션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-129">Creates a custom collection and add all databases in the server to the custom collection target with the exception of master.</span></span>
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
             Write-Host $currentdb "is already in the custom collection target" $CustomCollectionName"."
        }

        else
        {
            throw $_
        }
    }
    $ErrorActionPreference = "Continue"
   }
   ```
## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="641a6-130">데이터베이스에서 실행할 T-SQL 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="641a6-130">Create a T-SQL Script for execution across databases</span></span>
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

## <a name="create-the-job-to-execute-a-script-across-the-custom-group-of-databases"></a><span data-ttu-id="641a6-131">사용자 지정 데이터베이스 그룹에서 스크립트를 실행하는 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-131">Create the job to execute a script across the custom group of databases</span></span>

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-the-job"></a><span data-ttu-id="641a6-132">작업 실행</span><span class="sxs-lookup"><span data-stu-id="641a6-132">Execute the job</span></span>
<span data-ttu-id="641a6-133">다음 PowerShell 스크립트를 사용하여 기존 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-133">The following PowerShell script can be used to execute an existing job:</span></span>

<span data-ttu-id="641a6-134">실행하려는 작업 이름이 반영되도록 다음 변수를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-134">Update the following variable to reflect the desired job name to have executed:</span></span>

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-the-state-of-a-single-job-execution"></a><span data-ttu-id="641a6-135">단일 작업 실행 상태 검색</span><span class="sxs-lookup"><span data-stu-id="641a6-135">Retrieve the state of a single job execution</span></span>
<span data-ttu-id="641a6-136">**IncludeChildren** 매개 변수와 함께 동일한 **Get-AzureSqlJobExecution cmdlet**을 사용하여 자식 작업 실행 상태, 즉 작업 대상인 각 데이터베이스에 대한 각 작업 실행의 특정 상태를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-136">Use the same **Get-AzureSqlJobExecution** cmdlet with the **IncludeChildren** parameter to view the state of child job executions, namely the specific state for each job execution against each database targeted by the job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-the-state-across-multiple-job-executions"></a><span data-ttu-id="641a6-137">여러 작업 실행 간에 상태 보기</span><span class="sxs-lookup"><span data-stu-id="641a6-137">View the state across multiple job executions</span></span>
<span data-ttu-id="641a6-138">**Get-AzureSqlJobExecution** cmdlet에는 제공된 매개 변수를 통해 필터링되는 여러 작업 실행을 표시하는 데 사용할 수 있는 여러 선택적 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-138">The **Get-AzureSqlJobExecution** cmdlet has multiple optional parameters that can be used to display multiple job executions, filtered through the provided parameters.</span></span> <span data-ttu-id="641a6-139">아래에서는 Get-AzureSqlJobExecution을 사용할 수 있는 여러 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-139">The following demonstrates some of the possible ways to use Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="641a6-140">모든 활성 최상위 작업 실행을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-140">Retrieve all active top level job executions:</span></span>

   ```
    Get-AzureSqlJobExecution
   ```

<span data-ttu-id="641a6-141">비활성 작업 실행을 포함하여 모든 최상위 작업 실행을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-141">Retrieve all top level job executions, including inactive job executions:</span></span>

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

<span data-ttu-id="641a6-142">비활성 작업 실행을 포함하여 제공된 작업 실행 ID의 모든 자식 작업 실행을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-142">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

<span data-ttu-id="641a6-143">비활성 작업을 포함하여 일정/작업 조합으로 만든 모든 작업 실행을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-143">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

<span data-ttu-id="641a6-144">비활성 작업을 포함하여 지정된 분할된 데이터베이스 맵을 대상으로 하는 모든 작업을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-144">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="641a6-145">비활성 작업을 포함하여 지정된 사용자 지정 컬렉션을 대상으로 하는 모든 작업을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-145">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="641a6-146">특정 작업 실행 내의 작업 태스크 실행 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-146">Retrieve the list of job task executions within a specific job execution:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

<span data-ttu-id="641a6-147">작업 태스크 실행 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-147">Retrieve job task execution details:</span></span>

<span data-ttu-id="641a6-148">다음 PowerShell 스크립트를 사용하여 실행 실패를 디버그할 때 특히 유용한 작업 태스크 실행 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-148">The following PowerShell script can be used to view the details of a job task execution, which is particularly useful when debugging execution failures.</span></span>
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a><span data-ttu-id="641a6-149">작업 태스크 실행 내의 오류 검색</span><span class="sxs-lookup"><span data-stu-id="641a6-149">Retrieve failures within job task executions</span></span>
<span data-ttu-id="641a6-150">JobTaskExecution 개체에는 Message 속성과 함께 Lifecycle 주기에 대한 속성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-150">The JobTaskExecution object includes a property for the Lifecycle of the task along with a Message property.</span></span> <span data-ttu-id="641a6-151">작업 태스크 실행에 실패한 경우 Lifecycle 속성이 *실패* 로 설정되고 Message 속성은 결과 예외 메시지 및 해당 스택으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-151">If a job task execution failed, the Lifecycle property will be set to *Failed* and the Message property will be set to the resulting exception message and its stack.</span></span> <span data-ttu-id="641a6-152">작업이 수행되지 않은 경우 지정된 작업에 대해 실패한 작업 태스크 세부 정보를 보는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-152">If a job did not succeed, it is important to view the details of job tasks that did not succeed for a given job.</span></span>

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

## <a name="waiting-for-a-job-execution-to-complete"></a><span data-ttu-id="641a6-153">작업 실행이 완료될 때까지 대기</span><span class="sxs-lookup"><span data-stu-id="641a6-153">Waiting for a job execution to complete</span></span>
<span data-ttu-id="641a6-154">다음 PowerShell 스크립트를 사용하여 작업 태스크가 완료될 때까지 기다릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-154">The following PowerShell script can be used to wait for a job task to complete:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="641a6-155">사용자 지정 실행 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="641a6-155">Create a custom execution policy</span></span>
<span data-ttu-id="641a6-156">탄력적 데이터베이스 작업은 작업을 시작할 때 적용할 수 있는 사용자 지정 실행 정책 만들기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-156">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="641a6-157">실행 정책은 현재 다음과 같은 정의를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-157">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="641a6-158">이름: 실행 정책의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-158">Name: Identifier for the execution policy.</span></span>
* <span data-ttu-id="641a6-159">작업 시간 제한: 탄력적 데이터베이스 작업에 의해 작업이 취소되기 전의 총 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-159">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="641a6-160">초기 재시도 간격: 첫 번째 재시도 전에 대기할 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-160">Initial Retry Interval: Interval to wait before first retry.</span></span>
* <span data-ttu-id="641a6-161">최대 재시도 간격: 사용할 재시도 간격의 최대값입니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-161">Maximum Retry Interval: Cap of retry intervals to use.</span></span>
* <span data-ttu-id="641a6-162">재시도 간격 백오프 계수: 재시도 사이의 다음 간격을 계산하는 데 사용되는 계수입니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-162">Retry Interval Backoff Coefficient: Coefficient used to calculate the next interval between retries.</span></span>  <span data-ttu-id="641a6-163">(초기 재시도 간격) * Math.pow((계수 백오프 간격), (재시도 횟수) - 2) 수식이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-163">The following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span>
* <span data-ttu-id="641a6-164">최대 시도 횟수: 작업 내에서 수행할 최대 재시도 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-164">Maximum Attempts: The maximum number of retry attempts to perform within a job.</span></span>

<span data-ttu-id="641a6-165">기본 실행 정책은 다음 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-165">The default execution policy uses the following values:</span></span>

* <span data-ttu-id="641a6-166">이름: 기본 실행 정책</span><span class="sxs-lookup"><span data-stu-id="641a6-166">Name: Default execution policy</span></span>
* <span data-ttu-id="641a6-167">작업 시간 제한: 1주</span><span class="sxs-lookup"><span data-stu-id="641a6-167">Job Timeout: 1 week</span></span>
* <span data-ttu-id="641a6-168">초기 재시도 간격: 100밀리초</span><span class="sxs-lookup"><span data-stu-id="641a6-168">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="641a6-169">최대 재시도 간격: 30분</span><span class="sxs-lookup"><span data-stu-id="641a6-169">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="641a6-170">재시도 간격 계수: 2</span><span class="sxs-lookup"><span data-stu-id="641a6-170">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="641a6-171">최대 시도 횟수: 2,147,483,647</span><span class="sxs-lookup"><span data-stu-id="641a6-171">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="641a6-172">원하는 실행 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-172">Create the desired execution policy:</span></span>

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

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="641a6-173">사용자 지정 실행 정책 업데이트</span><span class="sxs-lookup"><span data-stu-id="641a6-173">Update a custom execution policy</span></span>
<span data-ttu-id="641a6-174">업데이트하려는 실행 정책을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-174">Update the desired execution policy to update:</span></span>

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

## <a name="cancel-a-job"></a><span data-ttu-id="641a6-175">작업 취소</span><span class="sxs-lookup"><span data-stu-id="641a6-175">Cancel a job</span></span>
<span data-ttu-id="641a6-176">탄력적 데이터베이스 작업은 작업 취소 요청을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-176">Elastic Database Jobs supports jobs cancellation requests.</span></span>  <span data-ttu-id="641a6-177">탄력적 데이터베이스 작업이 현재 실행 중인 작업에 대한 취소 요청을 감지하는 경우 작업을 중지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-177">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt to stop the job.</span></span>

<span data-ttu-id="641a6-178">탄력적 데이터베이스 작업이 취소를 수행할 수 있는 방법에는 다음 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-178">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="641a6-179">현재 실행 중인 작업 취소: 작업이 현재 실행되는 동안 취소가 감지되면 현재 실행 중인 작업 측면 내에서 취소가 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-179">Canceling Currently Executing Tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within the currently executing aspect of the task.</span></span>  <span data-ttu-id="641a6-180">예를 들어 현재 장기 실행 쿼리를 수행하는 동안 취소가 시도되면 쿼리를 취소하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-180">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt to cancel the query.</span></span>
2. <span data-ttu-id="641a6-181">작업 재시도 취소: 작업 실행이 시작되기 전에 제어 스레드에서 취소가 감지되면 제어 스레드는 작업을 시작하지 않고 요청을 취소된 것으로 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-181">Canceling Task Retries: If a cancellation is detected by the control thread before a task is launched for execution, the control thread will avoid launching the task and declare the request as canceled.</span></span>

<span data-ttu-id="641a6-182">부모 작업에 대해 작업 취소가 요청된 경우 부모 작업 및 모든 자식 작업에 대해 취소 요청이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-182">If a job cancellation is requested for a parent job, the cancellation request will be honored for the parent job and for all of its child jobs.</span></span>

<span data-ttu-id="641a6-183">취소 요청을 제출하려면 **Stop-AzureSqlJobExecution** cmdlet을 사용하고 을 사용하고 **JobExecutionId** 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-183">To submit a cancellation request, use the **Stop-AzureSqlJobExecution** cmdlet and set the **JobExecutionId** parameter.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-the-jobs-history"></a><span data-ttu-id="641a6-184">이름 및 작업 기록으로 작업 삭제</span><span class="sxs-lookup"><span data-stu-id="641a6-184">Delete a job by name and the job's history</span></span>
<span data-ttu-id="641a6-185">탄력적 데이터베이스 작업은 비동기 작업 삭제를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-185">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="641a6-186">작업을 삭제되도록 표시할 수 있으며, 작업에 대한 모든 작업 실행이 완료된 후 작업 및 모든 작업 기록이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-186">A job can be marked for deletion and the system will delete the job and all its job history after all job executions have completed for the job.</span></span> <span data-ttu-id="641a6-187">활성 작업 실행은 자동으로 취소되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-187">The system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="641a6-188">활성 작업 실행을 취소하려면 Stop-AzureSqlJobExecution을 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-188">Instead, Stop-AzureSqlJobExecution must be invoked to cancel active job executions.</span></span>

<span data-ttu-id="641a6-189">작업 삭제를 트리거하려면 **Remove-AzureSqlJob** cmdlet을 사용하고 **JobName** 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-189">To trigger job deletion, use the **Remove-AzureSqlJob** cmdlet and set the **JobName** parameter.</span></span>

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a><span data-ttu-id="641a6-190">사용자 지정 데이터베이스 대상 만들기</span><span class="sxs-lookup"><span data-stu-id="641a6-190">Create a custom database target</span></span>
<span data-ttu-id="641a6-191">실행에 직접 사용하거나 사용자 지정 데이터베이스 그룹에 포함할 수 있는 탄력적 데이터베이스 작업에서 사용자 지정 데이터베이스 대상을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-191">Custom database targets can be defined in Elastic Database jobs which can be used either for execution directly or for inclusion within a custom database group.</span></span> <span data-ttu-id="641a6-192">**탄력적 풀** 은 PowerShell API를 통해 직접 지원되지 않으므로 풀에 있는 모든 데이터베이스를 포함하는 사용자 지정 데이터베이스 컬렉션 대상 및 사용자 지정 데이터베이스 대상을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-192">Since **elastic pools** are not yet directly supported via the PowerShell APIs, you simply create a custom database target and custom database collection target which encompasses all the databases in the pool.</span></span>

<span data-ttu-id="641a6-193">원하는 데이터베이스 정보가 반영되도록 다음 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-193">Set the following variables to reflect the desired database information:</span></span>

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a><span data-ttu-id="641a6-194">사용자 지정 데이터베이스 컬렉션 대상 만들기</span><span class="sxs-lookup"><span data-stu-id="641a6-194">Create a custom database collection target</span></span>
<span data-ttu-id="641a6-195">정의된 여러 데이터베이스 대상에서 실행할 수 있도록 사용자 지정 데이터베이스 컬렉션 대상을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-195">A custom database collection target can be defined to enable execution across multiple defined database targets.</span></span> <span data-ttu-id="641a6-196">데이터베이스 그룹을 만든 후 사용자 지정 컬렉션 대상에 데이터베이스를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-196">After a database group is created, databases can be associated to the custom collection target.</span></span>

<span data-ttu-id="641a6-197">원하는 사용자 지정 컬렉션 대상 구성이 반영되도록 다음 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-197">Set the following variables to reflect the desired custom collection target configuration:</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-to-a-custom-database-collection-target"></a><span data-ttu-id="641a6-198">사용자 지정 데이터베이스 컬렉션 대상에 데이터베이스 추가</span><span class="sxs-lookup"><span data-stu-id="641a6-198">Add databases to a custom database collection target</span></span>
<span data-ttu-id="641a6-199">데이터베이스 대상을 사용자 지정 데이터베이스 컬렉션 대상에 연결하여 데이터베이스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-199">Database targets can be associated with custom database collection targets to create a group of databases.</span></span> <span data-ttu-id="641a6-200">사용자 지정 데이터베이스 컬렉션 대상을 대상으로 하는 작업을 만들 때마다 실행 시 그룹에 연결된 데이터베이스를 대상으로 하도록 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-200">Whenever a job is created that targets a custom database collection target, it will be expanded to target the databases associated to the group at the time of execution.</span></span>

<span data-ttu-id="641a6-201">특정 사용자 지정 컬렉션에 원하는 데이터베이스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-201">Add the desired database to a specific custom collection:</span></span>

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-the-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="641a6-202">사용자 지정 데이터베이스 컬렉션 대상 내의 데이터베이스 검토</span><span class="sxs-lookup"><span data-stu-id="641a6-202">Review the databases within a custom database collection target</span></span>
<span data-ttu-id="641a6-203">**Get-AzureSqlJobTarget** cmdlet을 사용하여 사용자 지정 데이터베이스 컬렉션 대상 내의 자식 데이터베이스를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-203">Use the **Get-AzureSqlJobTarget** cmdlet to retrieve the child databases within a custom database collection target.</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-to-execute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="641a6-204">사용자 지정 데이터베이스 컬렉션 대상에서 스크립트를 실행하는 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="641a6-204">Create a job to execute a script across a custom database collection target</span></span>
<span data-ttu-id="641a6-205">**New-AzureSqlJob** cmdlet을 사용하여 사용자 지정 데이터베이스 컬렉션 대상에서 정의된 데이터베이스 그룹에 대한 작업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-205">Use the **New-AzureSqlJob** cmdlet to create a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="641a6-206">탄력적 데이터베이스 작업은 각각 사용자 지정 데이터베이스 컬렉션 대상과 연결된 데이터베이스에 해당하는 여러 자식 작업으로 작업을 확장하고 각 데이터베이스에 대해 스크립트가 실행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-206">Elastic Database jobs will expand the job into multiple child jobs each corresponding to a database associated with the custom database collection target and ensure that the script is executed against each database.</span></span> <span data-ttu-id="641a6-207">스크립트는 재시도 복구에 대해 idempotent여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-207">Again, it is important that scripts are idempotent to be resilient to retries.</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a><span data-ttu-id="641a6-208">데이터베이스에서 데이터 수집</span><span class="sxs-lookup"><span data-stu-id="641a6-208">Data collection across databases</span></span>
<span data-ttu-id="641a6-209">**탄력적 데이터베이스 작업** 은 데이터베이스 그룹에 대한 쿼리 실행을 지원하고 지정된 데이터베이스 테이블에 결과를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-209">**Elastic Database jobs** supports executing a query across a group of databases and sends the results to a specified database’s table.</span></span> <span data-ttu-id="641a6-210">각 데이터베이스의 쿼리 결과를 볼 수 있으면 테이블을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-210">The table can be queried after the fact to see the query’s results from each database.</span></span> <span data-ttu-id="641a6-211">이는 많은 데이터베이스에서 쿼리를 실행하는 비동기 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-211">This provides an asynchronous mechanism to execute a query across many databases.</span></span> <span data-ttu-id="641a6-212">데이터베이스 중 하나를 일시적으로 사용할 수 없는 경우와 같은 오류 사례는 재시도를 통해 자동으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-212">Failure cases such as one of the databases being temporarily unavailable are handled automatically via retries.</span></span>

<span data-ttu-id="641a6-213">반환된 결과 집합의 스키마와 일치하는 지정된 대상 테이블이 아직 없는 경우 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-213">The specified destination table will be automatically created if it does not yet exist, matching the schema of the returned result set.</span></span> <span data-ttu-id="641a6-214">스크립트 실행에서 여러 결과 집합이 반환되는 경우 탄력적 데이터베이스 작업은 제공된 대상 테이블에 첫 번째 결과 집합만 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-214">If a script execution returns multiple result sets, Elastic Database jobs will only send the first one to the provided destination table.</span></span>

<span data-ttu-id="641a6-215">다음 PowerShell 스크립트를 사용하여 지정된 테이블에 결과를 수집하는 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-215">The following PowerShell script can be used to execute a script collecting its results into a specified table.</span></span> <span data-ttu-id="641a6-216">이 스크립트는 단일 결과 집합을 출력하는 T-SQL 스크립트가 생성되었으며 사용자 지정 데이터베이스 컬렉션 대상이 생성되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-216">This script assumes that a T-SQL script has been created which outputs a single result set and a custom database collection target has been created.</span></span>

<span data-ttu-id="641a6-217">원하는 스크립트, 자격 증명 및 실행 대상이 반영되도록 다음을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-217">Set the following to reflect the desired script, credentials, and execution target:</span></span>

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

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="641a6-218">데이터 수집 시나리오에 대한 작업 만들기 및 시작</span><span class="sxs-lookup"><span data-stu-id="641a6-218">Create and start a job for data collection scenarios</span></span>
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a><span data-ttu-id="641a6-219">작업 트리거를 사용하여 작업 실행 일정 만들기</span><span class="sxs-lookup"><span data-stu-id="641a6-219">Create a schedule for job execution using a job trigger</span></span>
<span data-ttu-id="641a6-220">다음 PowerShell 스크립트를 사용하여 되풀이 일정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-220">The following PowerShell script can be used to create a reoccurring schedule.</span></span> <span data-ttu-id="641a6-221">이 스크립트는 1분 간격을 사용하지만 New-AzureSqlJobSchedule은 -DayInterval, -HourInterval, -MonthInterval 및 -WeekInterval 매개 변수도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-221">This script uses a one minute interval, but New-AzureSqlJobSchedule also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="641a6-222">-OneTime을 전달하여 한 번만 실행되는 일정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-222">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="641a6-223">새 일정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-223">Create a new schedule:</span></span>
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-to-have-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="641a6-224">시간 일정에 따라 작업을 실행하는 작업 트리거 만들기</span><span class="sxs-lookup"><span data-stu-id="641a6-224">Create a job trigger to have a job executed on a time schedule</span></span>
<span data-ttu-id="641a6-225">시간 일정에 따라 작업을 실행하는 작업 트리거를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-225">A job trigger can be defined to have a job executed according to a time schedule.</span></span> <span data-ttu-id="641a6-226">다음 PowerShell 스크립트를 사용하여 작업 트리거를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-226">The following PowerShell script can be used to create a job trigger.</span></span>

<span data-ttu-id="641a6-227">원하는 작업 및 일정에 맞게 다음 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-227">Set the following variables to correspond to the desired job and schedule:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-to-stop-job-from-executing-on-schedule"></a><span data-ttu-id="641a6-228">일정에 따라 작업이 실행되지 않도록 예약된 연결 제거</span><span class="sxs-lookup"><span data-stu-id="641a6-228">Remove a scheduled association to stop job from executing on schedule</span></span>
<span data-ttu-id="641a6-229">작업 트리거를 통한 되풀이 작업 실행을 중단하려면 작업 트리거를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-229">To discontinue reoccurring job execution through a job trigger, the job trigger can be removed.</span></span>
<span data-ttu-id="641a6-230">**Remove-AzureSqlJobTrigger** cmdlet을 사용하여 일정에 따라 작업이 실행되지 않도록 작업 트리거를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-230">Remove a job trigger to stop a job from being executed according to a schedule using the **Remove-AzureSqlJobTrigger** cmdlet.</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-to-excel"></a><span data-ttu-id="641a6-231">탄력적 데이터베이스 쿼리 결과를 Excel로 가져오기</span><span class="sxs-lookup"><span data-stu-id="641a6-231">Import elastic database query results to Excel</span></span>
 <span data-ttu-id="641a6-232">쿼리의 결과를 엑셀파일로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-232">You can import the results from of a query to an Excel file.</span></span>

1. <span data-ttu-id="641a6-233">Excel 2013을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-233">Launch Excel 2013.</span></span>
2. <span data-ttu-id="641a6-234">**데이터** 리본을 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-234">Navigate to the **Data** ribbon.</span></span>
3. <span data-ttu-id="641a6-235">**기타 원본에서**을 클릭하고 **SQL Server에서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-235">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![다른 원본에서 Excel 가져오기](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. <span data-ttu-id="641a6-237">**데이터 연결 마법사** 에서 서버 이름 및 로그인 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-237">In the **Data Connection Wizard** type the server name and login credentials.</span></span> <span data-ttu-id="641a6-238">그런 후 **Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-238">Then click **Next**.</span></span>
5. <span data-ttu-id="641a6-239">대화 상자에서 **원하는 데이터를 포함하는 데이터베이스를 선택**하고 **ElasticDBQuery** 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-239">In the dialog box **Select the database that contains the data you want**, select the **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="641a6-240">목록 보기에서 **사용자**테이블을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-240">Select the **Customers** table in the list view and click **Next**.</span></span> <span data-ttu-id="641a6-241">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-241">Then click **Finish**.</span></span>
7. <span data-ttu-id="641a6-242">**데이터 가져오기** 양식에서, **통합 문서에서 원하는 데이터를 보는 방법을 선택**하고 **테이블**을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-242">In the **Import Data** form, under **Select how you want to view this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="641a6-243">다른 분할된 데이터베이스에 저장된 **Customers** 테이블의 모든 행으로 Excel 시트를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-243">All the rows from **Customers** table, stored in different shards populate the Excel sheet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="641a6-244">다음 단계</span><span class="sxs-lookup"><span data-stu-id="641a6-244">Next steps</span></span>
<span data-ttu-id="641a6-245">이제 Excel의 데이터 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-245">You can now use Excel’s data functions.</span></span> <span data-ttu-id="641a6-246">탄력적 쿼리 데이터 베이스의 데이터 통합 도구 및 BI과 연결하기 위해 서버 이름, 데이터베이스 이름, 자격 증명과 연결 문자열을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-246">Use the connection string with your server name, database name and credentials to connect your BI and data integration tools to the elastic query database.</span></span> <span data-ttu-id="641a6-247">SQL Server 도구에 대한 데이터 소스로 지원 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-247">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="641a6-248">탄력적 쿼리 데이터베이스 및 기타 SQL Server 데이터베이스와 마찬가지로 외부 테이블 및 도구와 연결할 수 있는 SQL Server 테이블을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-248">Refer to the elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect to with your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="641a6-249">비용</span><span class="sxs-lookup"><span data-stu-id="641a6-249">Cost</span></span>
<span data-ttu-id="641a6-250">탄력적 데이터베이스 쿼리 기능을 사용 하는 것은 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-250">There is no additional charge for using the Elastic Database query feature.</span></span> <span data-ttu-id="641a6-251">그러나, 지금 이 기능은 분할된 데이터베이스처럼 모든 서비스계층에서만 사용 가능한게 아니라, 끝점처럼 프리미엄 데이터베이스에서만 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="641a6-251">However, at this time this feature is available only on premium databases as an end point, but the shards can be of any service tier.</span></span>

<span data-ttu-id="641a6-252">가격 정보는 [SQL 데이터베이스 가격 정보](https://azure.microsoft.com/pricing/details/sql-database/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="641a6-252">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->

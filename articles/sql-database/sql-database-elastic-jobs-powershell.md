---
title: "PowerShell을 사용하여 탄력적 작업 만들기 및 관리 | Microsoft Docs"
description: "Azure SQL 데이터베이스 풀을 관리하는데 사용되는 PowerShell"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: b4c97e8f51581f9a3f7c5a8d8e82562255fe7b48
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a><span data-ttu-id="eb678-103">PowerShell을 사용하여 SQL Database 탄력적 작업 만들기 및 관리(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="eb678-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span></span>

<span data-ttu-id="eb678-104">**탄력적 데이터베이스 작업** (미리 보기)에 PowerShell API를 사용하면 스크립트를 실행할 데이터베이스 그룹을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-104">The PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span></span> <span data-ttu-id="eb678-105">이 문서는 PowerShell cmdlet을 사용하여 **탄력적 데이터베이스 작업** 을 만들고 관리하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-105">This article shows how to create and manage **Elastic Database jobs** using PowerShell cmdlets.</span></span> <span data-ttu-id="eb678-106">[탄력적 작업 개요](sql-database-elastic-jobs-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb678-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="eb678-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="eb678-107">Prerequisites</span></span>
* <span data-ttu-id="eb678-108">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="eb678-108">An Azure subscription.</span></span> <span data-ttu-id="eb678-109">무료 평가판에 대한 내용은 [무료 1개월 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb678-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="eb678-110">탄력적 데이터베이스 도구로 만든 데이터 집합.</span><span class="sxs-lookup"><span data-stu-id="eb678-110">A set of databases created with the Elastic Database tools.</span></span> <span data-ttu-id="eb678-111">[탄력적 데이터베이스 도구 시작하기](sql-database-elastic-scale-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb678-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="eb678-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eb678-112">Azure PowerShell.</span></span> <span data-ttu-id="eb678-113">자세한 내용은 [Azure PowerShell을 설치 및 구성하는 방법](https://docs.microsoft.com/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb678-113">For detailed information, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
* <span data-ttu-id="eb678-114">**탄력적 데이터베이스 작업** PowerShell 패키지: [Installing 탄력적 데이터베이스 작업](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="eb678-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span></span>

### <a name="select-your-azure-subscription"></a><span data-ttu-id="eb678-115">Azure 구독 선택</span><span class="sxs-lookup"><span data-stu-id="eb678-115">Select your Azure subscription</span></span>
<span data-ttu-id="eb678-116">구독을 선택하려면 구독 ID**-SubscriptionId** 또는 구독 이름(**-SubscriptionName**이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-116">To select the subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span></span> <span data-ttu-id="eb678-117">구독이 여러 개일 경우 **Get-AzureRmSubscription** cmdlet을 실행하고 결과 집합에서 원하는 구독 정보를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-117">If you have multiple subscriptions you can run the **Get-AzureRmSubscription** cmdlet and copy the desired subscription information from the result set.</span></span> <span data-ttu-id="eb678-118">구독 정보가 준비되면 다음 commandlet을 실행하여 이 구독을 기본값, 즉 작업을 만들고 관리하기 위한 대상으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-118">Once you have your subscription information, run the following commandlet to set this subscription as the default, namely the target for creating and managing jobs:</span></span>

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

<span data-ttu-id="eb678-119">[PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) 를 사용하여 탄력적 데이터베이스 작업에 대한 PowerShell 스크립트를 개발 및 실행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-119">The [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage to develop and execute PowerShell scripts against the Elastic Database jobs.</span></span>

## <a name="elastic-database-jobs-objects"></a><span data-ttu-id="eb678-120">탄력적 데이터베이스 작업 개체</span><span class="sxs-lookup"><span data-stu-id="eb678-120">Elastic Database jobs objects</span></span>
<span data-ttu-id="eb678-121">다음 표에서는 **탄력적 데이터베이스 작업** 의 모든 개체 유형과 해당 설명 및 관련된 PowerShell API를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-121">The following table lists out all the object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="eb678-122">개체 유형</span><span class="sxs-lookup"><span data-stu-id="eb678-122">Object Type</span></span></th>
    <th><span data-ttu-id="eb678-123">설명</span><span class="sxs-lookup"><span data-stu-id="eb678-123">Description</span></span></th>
    <th><span data-ttu-id="eb678-124">관련된 PowerShell API</span><span class="sxs-lookup"><span data-stu-id="eb678-124">Related PowerShell APIs</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="eb678-125">자격 증명</span><span class="sxs-lookup"><span data-stu-id="eb678-125">Credential</span></span></td>
    <td><span data-ttu-id="eb678-126">PACPAC 응용 프로그램 또는 스크립트 실행을 위해 데이터베이스에 연결할 때 사용할 사용자 이름 및 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-126">Username and password to use when connecting to databases for execution of scripts or application of DACPACs.</span></span> <p><span data-ttu-id="eb678-127">탄력적 데이터베이스 작업 데이터베이스로 보내고 저장하기 전에 암호가 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-127">The password is encrypted before sending to and storing in the Elastic Database Jobs database.</span></span>  <span data-ttu-id="eb678-128">설치 스크립트에서 생성 및 업로드된 자격 증명을 통해 탄력적 데이터베이스 작업 서비스에서 암호를 해독합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-128">The password is decrypted by the Elastic Database Jobs service via the credential created and uploaded from the installation script.</span></span></td>
    <td><p><span data-ttu-id="eb678-129">Get-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="eb678-129">Get-AzureSqlJobCredential</span></span></p>
    <p><span data-ttu-id="eb678-130">New-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="eb678-130">New-AzureSqlJobCredential</span></span></p><p><span data-ttu-id="eb678-131">Set-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="eb678-131">Set-AzureSqlJobCredential</span></span></p></td></td>
  </tr>

  <tr>
    <td><span data-ttu-id="eb678-132">스크립트</span><span class="sxs-lookup"><span data-stu-id="eb678-132">Script</span></span></td>
    <td><span data-ttu-id="eb678-133">데이터베이스에서 실행하는 데 사용할 TRANSACT-SQL 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-133">Transact-SQL script to be used for execution across databases.</span></span>  <span data-ttu-id="eb678-134">실패 시 서비스에서 스크립트 실행을 다시 시도하므로 스크립트를 idempotent로 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-134">The script should be authored to be idempotent since the service will retry execution of the script upon failures.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="eb678-135">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="eb678-135">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="eb678-136">Get-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="eb678-136">Get-AzureSqlJobContentDefinition</span></span></p>
    <p><span data-ttu-id="eb678-137">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="eb678-137">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="eb678-138">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="eb678-138">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>

  <tr>
    <td><span data-ttu-id="eb678-139">DACPAC</span><span class="sxs-lookup"><span data-stu-id="eb678-139">DACPAC</span></span></td>
    <td><span data-ttu-id="eb678-140">데이터베이스에서 적용할 <a href="https://msdn.microsoft.com/library/ee210546.aspx">데이터 계층 응용 프로그램</a> 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package to be applied across databases.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="eb678-141">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="eb678-141">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="eb678-142">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="eb678-142">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="eb678-143">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="eb678-143">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="eb678-144">데이터베이스 대상</span><span class="sxs-lookup"><span data-stu-id="eb678-144">Database Target</span></span></td>
    <td><span data-ttu-id="eb678-145">Azure SQL 데이터베이스를 가리키는 데이터베이스 및 서버 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-145">Database and server name pointing to an Azure SQL Database.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="eb678-146">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="eb678-146">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="eb678-147">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="eb678-147">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="eb678-148">분할된 데이터베이스 맵 대상</span><span class="sxs-lookup"><span data-stu-id="eb678-148">Shard Map Target</span></span></td>
    <td><span data-ttu-id="eb678-149">탄력적 데이터베이스 분할된 데이터베이스 맵 내에 저장된 정보를 확인하는 데 사용할 자격 증명 및 데이터베이스 대상의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-149">Combination of a database target and a credential to be used to determine information stored within an Elastic Database shard map.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="eb678-150">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="eb678-150">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="eb678-151">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="eb678-151">New-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="eb678-152">Set-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="eb678-152">Set-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="eb678-153">사용자 지정 컬렉션 대상</span><span class="sxs-lookup"><span data-stu-id="eb678-153">Custom Collection Target</span></span></td>
    <td><span data-ttu-id="eb678-154">전체적으로 실행하는 데 사용할 정의된 데이터베이스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-154">Defined group of databases to collectively use for execution.</span></span></td>
    <td>
    <p><span data-ttu-id="eb678-155">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="eb678-155">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="eb678-156">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="eb678-156">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="eb678-157">사용자 지정 컬렉션 자식 대상</span><span class="sxs-lookup"><span data-stu-id="eb678-157">Custom Collection Child Target</span></span></td>
    <td><span data-ttu-id="eb678-158">사용자 지정 컬렉션에서 참조되는 데이터베이스 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-158">Database target that is referenced from a custom collection.</span></span></td>
    <td>
    <p><span data-ttu-id="eb678-159">Add-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="eb678-159">Add-AzureSqlJobChildTarget</span></span></p>
    <p><span data-ttu-id="eb678-160">Remove-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="eb678-160">Remove-AzureSqlJobChildTarget</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="eb678-161">작업</span><span class="sxs-lookup"><span data-stu-id="eb678-161">Job</span></span></td>
    <td>
    <p><span data-ttu-id="eb678-162">실행을 트리거하거나 일정을 이행하는 데 사용할 수 있는 작업에 대한 매개 변수 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-162">Definition of parameters for a job that can be used to trigger execution or to fulfill a schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="eb678-163">Get-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="eb678-163">Get-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="eb678-164">New-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="eb678-164">New-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="eb678-165">Set-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="eb678-165">Set-AzureSqlJob</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="eb678-166">작업 실행</span><span class="sxs-lookup"><span data-stu-id="eb678-166">Job Execution</span></span></td>
    <td>
    <p><span data-ttu-id="eb678-167">실행 정책에 따라 오류를 처리하고 데이터베이스 연결에 자격 증명을 사용하여 스크립트 실행 또는 대상에 DACPAC 적용을 이행하는 데 필요한 작업의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-167">Container of tasks necessary to fulfill either executing a script or applying a DACPAC to a target using credentials for database connections with failures handled in accordance to an execution policy.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="eb678-168">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="eb678-168">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="eb678-169">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="eb678-169">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="eb678-170">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="eb678-170">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="eb678-171">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="eb678-171">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="eb678-172">작업 태스크 실행</span><span class="sxs-lookup"><span data-stu-id="eb678-172">Job Task Execution</span></span></td>
    <td>
    <p><span data-ttu-id="eb678-173">작업을 이행하는 단일 작업 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-173">Single unit of work to fulfill a job.</span></span></p>
    <p><span data-ttu-id="eb678-174">작업 태스크를 성공적으로 실행할 수 없는 경우 결과 예외 메시지가 기록되고 지정된 실행 정책에 따라 일치하는 새 작업 태스크가 생성 및 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-174">If a job task is not able to successfully execute, the resulting exception message will be logged and a new matching job task will be created and executed in accordance to the specified execution policy.</span></span></p></p>
    </td>
    <td>
    <p><span data-ttu-id="eb678-175">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="eb678-175">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="eb678-176">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="eb678-176">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="eb678-177">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="eb678-177">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="eb678-178">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="eb678-178">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="eb678-179">작업 실행 정책</span><span class="sxs-lookup"><span data-stu-id="eb678-179">Job Execution Policy</span></span></td>
    <td>
    <p><span data-ttu-id="eb678-180">작업 실행 시간 제한, 재시도 제한 및 재시도 간격을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-180">Controls job execution timeouts, retry limits and intervals between retries.</span></span></p>
    <p><span data-ttu-id="eb678-181">탄력적 데이터베이스 작업에는 각 재시도 간격의 지수 백오프를 통해 작업 태스크 실패의 무기한 재시도를 발생시키는 기본 작업 실행 정책이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="eb678-182">Get-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="eb678-182">Get-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="eb678-183">New-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="eb678-183">New-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="eb678-184">Set-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="eb678-184">Set-AzureSqlJobExecutionPolicy</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="eb678-185">일정</span><span class="sxs-lookup"><span data-stu-id="eb678-185">Schedule</span></span></td>
    <td>
    <p><span data-ttu-id="eb678-186">되풀이 간격 또는 한 번 수행할 실행에 대한 시간 기반 지정입니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-186">Time based specification for execution to take place either on a reoccurring interval or at a single time.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="eb678-187">Get-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="eb678-187">Get-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="eb678-188">New-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="eb678-188">New-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="eb678-189">Set-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="eb678-189">Set-AzureSqlJobSchedule</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="eb678-190">작업 트리거</span><span class="sxs-lookup"><span data-stu-id="eb678-190">Job Triggers</span></span></td>
    <td>
    <p><span data-ttu-id="eb678-191">일정에 따라 작업 실행을 트리거할 작업과 일정 간의 매핑입니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-191">A mapping between a job and a schedule to trigger job execution according to the schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="eb678-192">New-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="eb678-192">New-AzureSqlJobTrigger</span></span></p>
    <p><span data-ttu-id="eb678-193">Remove-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="eb678-193">Remove-AzureSqlJobTrigger</span></span></p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a><span data-ttu-id="eb678-194">지원되는 탄력적 데이터베이스 작업 그룹 유형</span><span class="sxs-lookup"><span data-stu-id="eb678-194">Supported Elastic Database jobs group types</span></span>
<span data-ttu-id="eb678-195">이 작업은 데이터베이스 그룹에 대해 DACPAC 응용 프로그램 또는 Transact-SQL(T-SQL) 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-195">The job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span></span> <span data-ttu-id="eb678-196">데이터베이스 그룹에 대해 실행할 작업이 제출되면 작업은 자식 작업으로 "확장"되며 여기에서 각 자식 작업은 그룹의 단일 데이터베이스에 대해 요청된 실행을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-196">When a job is submitted to be executed across a group of databases, the job “expands” the into child jobs where each performs the requested execution against a single database in the group.</span></span> 

<span data-ttu-id="eb678-197">두 가지 형식의 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-197">There are two types of groups that you can create:</span></span> 

* <span data-ttu-id="eb678-198">[분할된 데이터베이스 맵](sql-database-elastic-scale-shard-map-management.md) 그룹: 분할된 데이터베이스 맵을 대상으로 하는 작업이 제출되면 해당 작업은 분할된 데이터베이스 맵을 쿼리하여 분할된 데이터베이스의 현재 집합을 확인한 다음 분할된 데이터베이스 맵의 각 분할된 데이터베이스에 대한 자식 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted to target a shard map, the job queries the shard map to determine its current set of shards, and then creates child jobs for each shard in the shard map.</span></span>
* <span data-ttu-id="eb678-199">사용자 지정 컬렉션 그룹: 사용자 지정 데이터베이스 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-199">Custom Collection group: A custom defined set of databases.</span></span> <span data-ttu-id="eb678-200">작업이 사용자 지정 컬렉션을 대상으로 하는 경우 사용자 지정 컬렉션에서 현재 각 데이터베이스에 대한 자식 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-200">When a job targets a custom collection, it creates child jobs for each database currently in the custom collection.</span></span>

## <a name="to-set-the-elastic-database-jobs-connection"></a><span data-ttu-id="eb678-201">탄력적 데이터베이스 작업 연결을 설정하려면</span><span class="sxs-lookup"><span data-stu-id="eb678-201">To set the Elastic Database jobs connection</span></span>
<span data-ttu-id="eb678-202">작업 API를 사용하기 전에 작업 *제어 데이터베이스* 에 대한 연결을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-202">A connection needs to be set to the jobs *control database* prior to using the jobs APIs.</span></span> <span data-ttu-id="eb678-203">이 cmdlet을 실행하면 자격 증명 창이 트리거되어 탄력적 데이터베이스 작업을 설치할 때 만든 사용자 이름 및 암호를 요청하는 팝업이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-203">Running this cmdlet triggers a credential window to pop up requesting the user name and password created when installing Elastic Database jobs.</span></span> <span data-ttu-id="eb678-204">이 항목에 제공된 모든 예제에서는 이 첫 번째 단계가 이미 수행되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-204">All examples provided within this topic assume that this first step has already been performed.</span></span>

<span data-ttu-id="eb678-205">탄력적 데이터베이스 작업에 대한 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-205">Open a connection to the Elastic Database jobs:</span></span>

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-the-elastic-database-jobs"></a><span data-ttu-id="eb678-206">탄력적 데이터베이스 작업 내의 암호화된 자격 증명</span><span class="sxs-lookup"><span data-stu-id="eb678-206">Encrypted credentials within the Elastic Database jobs</span></span>
<span data-ttu-id="eb678-207">암호를 암호화하여 작업 *제어 데이터베이스*에 데이터베이스 자격 증명을 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-207">Database credentials can be inserted into the jobs *control database*  with its password encrypted.</span></span> <span data-ttu-id="eb678-208">나중에 작업을 실행할 수 있도록 자격 증명을 저장해야 합니다(작업 일정 사용).</span><span class="sxs-lookup"><span data-stu-id="eb678-208">It is necessary to store credentials to enable jobs to be executed at a later time, (using job schedules).</span></span>

<span data-ttu-id="eb678-209">암호화는 설치 스크립트의 일부로 생성된 인증서를 통해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-209">Encryption works through a certificate created as part of the installation script.</span></span> <span data-ttu-id="eb678-210">설치 스크립트는 저장된 암호화된 암호 해독을 위해 인증서를 만들고 Azure 클라우드 서비스에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-210">The installation script creates and uploads the certificate into the Azure Cloud Service for decryption of the stored encrypted passwords.</span></span> <span data-ttu-id="eb678-211">Azure 클라우드 서비스는 나중에 작업 *제어 데이터베이스* 내에 공개 키를 저장합니다. 그러면 PowerShell API 또는 Azure 클래식 포털 인터페이스에서 인증서를 로컬에 설치하도록 요구하지 않고 제공된 암호를 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-211">The Azure Cloud Service later stores the public key within the jobs *control database* which enables the PowerShell API or Azure Classic Portal interface to encrypt a provided password without requiring the certificate to be locally installed.</span></span>

<span data-ttu-id="eb678-212">자격 증명 암호가 암호화되고 탄력적 데이터베이스 작업 개체에 대한 읽기 전용 액세스 권한이 있는 사용자로부터 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-212">The credential passwords are encrypted and secure from users with read-only access to Elastic Database jobs objects.</span></span> <span data-ttu-id="eb678-213">하지만 탄력적 데이터베이스 작업 개체에 대한 읽기-쓰기 액세스 권한이 있는 악의적인 사용자가 암호를 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-213">But it is possible for a malicious user with read-write access to Elastic Database Jobs objects to extract a password.</span></span> <span data-ttu-id="eb678-214">자격 증명은 작업 실행 간에 다시 사용되도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-214">Credentials are designed to be reused across job executions.</span></span> <span data-ttu-id="eb678-215">연결을 설정할 때 자격 증명이 대상 데이터베이스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-215">Credentials are passed to target databases when establishing connections.</span></span> <span data-ttu-id="eb678-216">현재 각 자격 증명에 사용되는 대상 데이터베이스에 제한이 없으며 악의적인 사용자는 자신이 제어할 수 있는 데이터베이스에 대한 데이터베이스 대상을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-216">There are currently no restrictions on the target databases used for each credential, malicious user could add a database target for a database under the malicious user's control.</span></span> <span data-ttu-id="eb678-217">사용자는 이후 이 데이터베이스를 대상으로 작업을 시작하여 자격 증명의 암호를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-217">The user could subsequently start a job targeting this database to gain the credential's password.</span></span>

<span data-ttu-id="eb678-218">탄력적 데이터베이스 작업에 대한 보안 모범 사례는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-218">Security best practices for Elastic Database jobs include:</span></span>

* <span data-ttu-id="eb678-219">API 사용을 신뢰할 수 있는 개인으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-219">Limit usage of the APIs to trusted individuals.</span></span>
* <span data-ttu-id="eb678-220">자격 증명에 작업 태스크를 수행하는 데 필요한 최소한의 권한만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-220">Credentials should have the least privileges necessary to perform the job task.</span></span>  <span data-ttu-id="eb678-221">자세한 내용은 이 [권한 부여 및 사용 권한](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN 문서에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span></span>

### <a name="to-create-an-encrypted-credential-for-job-execution-across-databases"></a><span data-ttu-id="eb678-222">데이터베이스에 대한 작업 실행을 위한 암호화된 자격 증명을 만들려면</span><span class="sxs-lookup"><span data-stu-id="eb678-222">To create an encrypted credential for job execution across databases</span></span>
<span data-ttu-id="eb678-223">새 암호화된 자격 증명을 만들기 위해 [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx)에서 [**New-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential)에 전달할 수 있는 사용자 이름 및 암호를 묻는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-223">To create a new encrypted credential, the [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed to the [**New-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span></span>

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="to-update-credentials"></a><span data-ttu-id="eb678-224">자격 증명을 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="eb678-224">To update credentials</span></span>
<span data-ttu-id="eb678-225">암호가 변경될 때 [**Set-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential)을 사용하고 **CredentialName** 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-225">When passwords change, use the [**Set-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) and set the **CredentialName** parameter.</span></span>

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="to-define-an-elastic-database-shard-map-target"></a><span data-ttu-id="eb678-226">탄력적 데이터베이스 분할된 데이터베이스 맵 대상을 정의하려면</span><span class="sxs-lookup"><span data-stu-id="eb678-226">To define an Elastic Database shard map target</span></span>
<span data-ttu-id="eb678-227">[탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md)를 통해 만든 분할된 데이터베이스 집합의 모든 데이터베이스에 대해 작업을 실행하려면 분할된 데이터베이스 맵을 데이터베이스 대상으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-227">To execute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as the database target.</span></span> <span data-ttu-id="eb678-228">이 예제에서는 탄력적 데이터베이스 클라이언트 라이브러리를 사용하여 만든 분할된 데이터베이스 응용 프로그램이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-228">This example requires a sharded application created using the Elastic Database client library.</span></span> <span data-ttu-id="eb678-229">[탄력적 데이터베이스 도구 샘플 시작](sql-database-elastic-scale-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb678-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

<span data-ttu-id="eb678-230">분할된 데이터베이스 맵 관리자 데이터베이스를 데이터베이스 대상으로 설정한 후 분할된 특정 데이터베이스 맵을 대상으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-230">The shard map manager database must be set as a database target and then the specific shard map must be specified as a target.</span></span>

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="eb678-231">데이터베이스에서 실행할 T-SQL 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="eb678-231">Create a T-SQL Script for execution across databases</span></span>
<span data-ttu-id="eb678-232">실행할 T-SQL 스크립트를 만드는 경우 [idempotent](https://en.wikipedia.org/wiki/Idempotence) 이고 오류로부터 복구되도록 작성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-232">When creating T-SQL scripts for execution, it is highly recommended to build them to be [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span></span> <span data-ttu-id="eb678-233">탄력적 데이터베이스 작업은 실행이 실패할 때마다 오류 분류에 관계없이 스크립트 실행을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of the classification of the failure.</span></span>

<span data-ttu-id="eb678-234">[**New-AzureSqlJobContent cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent)을 사용하여 실행할 스크립트를 만들고 저장한 다음 **-ContentName** 및 **-CommandText** 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-234">Use the [**New-AzureSqlJobContent cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) to create and save a script for execution and set the **-ContentName** and **-CommandText** parameters.</span></span>

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a><span data-ttu-id="eb678-235">파일에서 새 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="eb678-235">Create a new script from a file</span></span>
<span data-ttu-id="eb678-236">T-SQL 스크립트가 파일 내에서 정의된 경우 다음을 사용하여 스크립트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-236">If the T-SQL script is defined within a file, use this to import the script:</span></span>

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path to SQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="to-update-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="eb678-237">데이터베이스에서 실행되도록 T-SQL 스크립트를 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="eb678-237">To update a T-SQL script for execution across databases</span></span>
<span data-ttu-id="eb678-238">이 PowerShell 스크립트는 기존 스크립트에 대한 T-SQL 명령 텍스트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-238">This PowerShell script updates the T-SQL command text for an existing script.</span></span>

<span data-ttu-id="eb678-239">설정하려는 스크립트 정의가 반영되도록 다음 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-239">Set the following variables to reflect the desired script definition to be set:</span></span>

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column to TestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="to-update-the-definition-to-an-existing-script"></a><span data-ttu-id="eb678-240">기존 스크립트에 대한 정의를 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="eb678-240">To update the definition to an existing script</span></span>
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="to-create-a-job-to-execute-a-script-across-a-shard-map"></a><span data-ttu-id="eb678-241">분할된 데이터베이스 맵에서 스크립트를 실행하는 작업을 만들려면</span><span class="sxs-lookup"><span data-stu-id="eb678-241">To create a job to execute a script across a shard map</span></span>
<span data-ttu-id="eb678-242">이 PowerShell 스크립트는 탄력적 확장 분할된 데이터베이스 맵의 각 분할된 데이터베이스에서 스크립트를 실행하는 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span></span>

<span data-ttu-id="eb678-243">원하는 스크립트 및 대상이 반영되도록 다음 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-243">Set the following variables to reflect the desired script and target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="to-execute-a-job"></a><span data-ttu-id="eb678-244">작업을 실행하려면</span><span class="sxs-lookup"><span data-stu-id="eb678-244">To execute a job</span></span>
<span data-ttu-id="eb678-245">이 PowerShell 스크립트는 기존 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-245">This PowerShell script executes an existing job:</span></span>

<span data-ttu-id="eb678-246">실행하려는 작업 이름이 반영되도록 다음 변수를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-246">Update the following variable to reflect the desired job name to have executed:</span></span>

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="to-retrieve-the-state-of-a-single-job-execution"></a><span data-ttu-id="eb678-247">단일 작업 실행의 상태를 검색하려면</span><span class="sxs-lookup"><span data-stu-id="eb678-247">To retrieve the state of a single job execution</span></span>
<span data-ttu-id="eb678-248">[**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution)을 사용하고 **JobExecutionId** 매개 변수를 설정하여 작업 실행의 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-248">Use the [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) and set the **JobExecutionId** parameter to view the state of job execution.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

<span data-ttu-id="eb678-249">**IncludeChildren** 매개 변수와 함께 동일한 **Get-AzureSqlJobExecution cmdlet**을 사용하여 자식 작업 실행 상태, 즉 작업 대상인 각 데이터베이스에 대한 각 작업 실행의 특정 상태를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-249">Use the same **Get-AzureSqlJobExecution** cmdlet with the **IncludeChildren** parameter to view the state of child job executions, namely the specific state for each job execution against each database targeted by the job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="to-view-the-state-across-multiple-job-executions"></a><span data-ttu-id="eb678-250">여러 작업 실행 간에 상태를 보려면</span><span class="sxs-lookup"><span data-stu-id="eb678-250">To view the state across multiple job executions</span></span>
<span data-ttu-id="eb678-251">[**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob)에는 제공된 매개 변수를 통해 필터링되는 여러 작업 실행을 표시하는 데 사용할 수 있는 여러 선택적 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-251">The [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) has multiple optional parameters that can be used to display multiple job executions, filtered through the provided parameters.</span></span> <span data-ttu-id="eb678-252">아래에서는 Get-AzureSqlJobExecution을 사용할 수 있는 여러 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-252">The following demonstrates some of the possible ways to use Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="eb678-253">모든 활성 최상위 작업 실행을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-253">Retrieve all active top level job executions:</span></span>

    Get-AzureSqlJobExecution

<span data-ttu-id="eb678-254">비활성 작업 실행을 포함하여 모든 최상위 작업 실행을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-254">Retrieve all top level job executions, including inactive job executions:</span></span>

    Get-AzureSqlJobExecution -IncludeInactive

<span data-ttu-id="eb678-255">비활성 작업 실행을 포함하여 제공된 작업 실행 ID의 모든 자식 작업 실행을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

<span data-ttu-id="eb678-256">비활성 작업을 포함하여 일정/작업 조합으로 만든 모든 작업 실행을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

<span data-ttu-id="eb678-257">비활성 작업을 포함하여 지정된 분할된 데이터베이스 맵을 대상으로 하는 모든 작업을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="eb678-258">비활성 작업을 포함하여 지정된 사용자 지정 컬렉션을 대상으로 하는 모든 작업을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="eb678-259">특정 작업 실행 내의 작업 태스크 실행 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-259">Retrieve the list of job task executions within a specific job execution:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

<span data-ttu-id="eb678-260">작업 태스크 실행 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-260">Retrieve job task execution details:</span></span>

<span data-ttu-id="eb678-261">다음 PowerShell 스크립트를 사용하여 실행 실패를 디버그할 때 특히 유용한 작업 태스크 실행 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-261">The following PowerShell script can be used to view the details of a job task execution, which is particularly useful when debugging execution failures.</span></span>

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="to-retrieve-failures-within-job-task-executions"></a><span data-ttu-id="eb678-262">작업 태스크 실행 내의 오류를 검색하려면</span><span class="sxs-lookup"><span data-stu-id="eb678-262">To retrieve failures within job task executions</span></span>
<span data-ttu-id="eb678-263">**JobTaskExecution 개체** 에는 메시지 속성과 함께 작업의 수명 주기에 대한 속성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-263">The **JobTaskExecution object** includes a property for the lifecycle of the task along with a message property.</span></span> <span data-ttu-id="eb678-264">작업 태스크 실행에 실패한 경우 수명 주기 속성이 *Failed* 로 설정되고 메시지 속성은 결과 예외 메시지 및 해당 스택으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-264">If a job task execution failed, the lifecycle property will be set to *Failed* and the message property will be set to the resulting exception message and its stack.</span></span> <span data-ttu-id="eb678-265">작업이 수행되지 않은 경우 지정된 작업에 대해 실패한 작업 태스크 세부 정보를 보는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-265">If a job did not succeed, it is important to view the details of job tasks that did not succeed for a given job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="to-wait-for-a-job-execution-to-complete"></a><span data-ttu-id="eb678-266">작업 실행이 완료될 때까지 대기하려면</span><span class="sxs-lookup"><span data-stu-id="eb678-266">To wait for a job execution to complete</span></span>
<span data-ttu-id="eb678-267">다음 PowerShell 스크립트를 사용하여 작업 태스크가 완료될 때까지 기다릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-267">The following PowerShell script can be used to wait for a job task to complete:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="eb678-268">사용자 지정 실행 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="eb678-268">Create a custom execution policy</span></span>
<span data-ttu-id="eb678-269">탄력적 데이터베이스 작업은 작업을 시작할 때 적용할 수 있는 사용자 지정 실행 정책 만들기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="eb678-270">실행 정책은 현재 다음과 같은 정의를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-270">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="eb678-271">이름: 실행 정책의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-271">Name: Identifier for the execution policy.</span></span>
* <span data-ttu-id="eb678-272">작업 시간 제한: 탄력적 데이터베이스 작업에 의해 작업이 취소되기 전의 총 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="eb678-273">초기 재시도 간격: 첫 번째 재시도 전에 대기할 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-273">Initial Retry Interval: Interval to wait before first retry.</span></span>
* <span data-ttu-id="eb678-274">최대 재시도 간격: 사용할 재시도 간격의 최대값입니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-274">Maximum Retry Interval: Cap of retry intervals to use.</span></span>
* <span data-ttu-id="eb678-275">재시도 간격 백오프 계수: 재시도 사이의 다음 간격을 계산하는 데 사용되는 계수입니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-275">Retry Interval Backoff Coefficient: Coefficient used to calculate the next interval between retries.</span></span>  <span data-ttu-id="eb678-276">(초기 재시도 간격) * Math.pow((계수 백오프 간격), (재시도 횟수) - 2) 수식이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-276">The following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span> 
* <span data-ttu-id="eb678-277">최대 시도 횟수: 작업 내에서 수행할 최대 재시도 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-277">Maximum Attempts: The maximum number of retry attempts to perform within a job.</span></span>

<span data-ttu-id="eb678-278">기본 실행 정책은 다음 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-278">The default execution policy uses the following values:</span></span>

* <span data-ttu-id="eb678-279">이름: 기본 실행 정책</span><span class="sxs-lookup"><span data-stu-id="eb678-279">Name: Default execution policy</span></span>
* <span data-ttu-id="eb678-280">작업 시간 제한: 1주</span><span class="sxs-lookup"><span data-stu-id="eb678-280">Job Timeout: 1 week</span></span>
* <span data-ttu-id="eb678-281">초기 재시도 간격: 100밀리초</span><span class="sxs-lookup"><span data-stu-id="eb678-281">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="eb678-282">최대 재시도 간격: 30분</span><span class="sxs-lookup"><span data-stu-id="eb678-282">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="eb678-283">재시도 간격 계수: 2</span><span class="sxs-lookup"><span data-stu-id="eb678-283">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="eb678-284">최대 시도 횟수: 2,147,483,647</span><span class="sxs-lookup"><span data-stu-id="eb678-284">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="eb678-285">원하는 실행 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-285">Create the desired execution policy:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="eb678-286">사용자 지정 실행 정책 업데이트</span><span class="sxs-lookup"><span data-stu-id="eb678-286">Update a custom execution policy</span></span>
<span data-ttu-id="eb678-287">업데이트하려는 실행 정책을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-287">Update the desired execution policy to update:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a><span data-ttu-id="eb678-288">작업 취소</span><span class="sxs-lookup"><span data-stu-id="eb678-288">Cancel a job</span></span>
<span data-ttu-id="eb678-289">탄력적 데이터베이스 작업은 작업 취소 요청을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-289">Elastic Database Jobs supports cancellation requests of jobs.</span></span>  <span data-ttu-id="eb678-290">탄력적 데이터베이스 작업이 현재 실행 중인 작업에 대한 취소 요청을 감지하는 경우 작업을 중지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt to stop the job.</span></span>

<span data-ttu-id="eb678-291">탄력적 데이터베이스 작업이 취소를 수행할 수 있는 방법에는 다음 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="eb678-292">현재 실행 중인 태스크 취소: 태스크가 현재 실행되는 동안 취소가 감지되면 현재 실행 중인 태스크 측면 내에서 취소가 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within the currently executing aspect of the task.</span></span>  <span data-ttu-id="eb678-293">예를 들어 현재 장기 실행 쿼리를 수행하는 동안 취소가 시도되면 쿼리를 취소하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt to cancel the query.</span></span>
2. <span data-ttu-id="eb678-294">태스크 재시도 취소: 태스크 실행이 시작되기 전에 제어 스레드에서 취소가 감지되면 제어 스레드는 태스크를 시작하지 않고 요청을 취소된 것으로 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-294">Canceling task retries: If a cancellation is detected by the control thread before a task is launched for execution, the control thread will avoid launching the task and declare the request as canceled.</span></span>

<span data-ttu-id="eb678-295">부모 작업에 대해 작업 취소가 요청된 경우 부모 작업 및 모든 자식 작업에 대해 취소 요청이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-295">If a job cancellation is requested for a parent job, the cancellation request will be honored for the parent job and for all of its child jobs.</span></span>

<span data-ttu-id="eb678-296">취소 요청을 제출하려면 [**Stop-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution)을 사용하고 **JobExecutionId** 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-296">To submit a cancellation request, use the [**Stop-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) and set the **JobExecutionId** parameter.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="to-delete-a-job-and-job-history-asynchronously"></a><span data-ttu-id="eb678-297">비동기적으로 작업 기록 및 작업을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="eb678-297">To delete a job and job history asynchronously</span></span>
<span data-ttu-id="eb678-298">탄력적 데이터베이스 작업은 비동기 작업 삭제를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-298">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="eb678-299">작업을 삭제되도록 표시할 수 있으며, 작업에 대한 모든 작업 실행이 완료된 후 작업 및 모든 작업 기록이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-299">A job can be marked for deletion and the system will delete the job and all its job history after all job executions have completed for the job.</span></span> <span data-ttu-id="eb678-300">활성 작업 실행은 자동으로 취소되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-300">The system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="eb678-301">활성 작업 실행을 취소하려면 [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution)을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-301">Invoke [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) to cancel active job executions.</span></span>

<span data-ttu-id="eb678-302">작업 삭제를 트리거하려면 [**Remove-AzureSqlJob cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob)을 사용하고 **JobName** 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-302">To trigger job deletion, use the [**Remove-AzureSqlJob cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) and set the **JobName** parameter.</span></span>

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="to-create-a-custom-database-target"></a><span data-ttu-id="eb678-303">사용자 지정 데이터베이스 대상을 만들려면</span><span class="sxs-lookup"><span data-stu-id="eb678-303">To create a custom database target</span></span>
<span data-ttu-id="eb678-304">직접 실행하거나 사용자 지정 데이터베이스 그룹 내에 포함할 사용자 지정 데이터베이스 대상을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span></span> <span data-ttu-id="eb678-305">예를 들어, **탄력적 풀**은 PowerShell API를 사용하여 직접 지원되지 않으므로 풀에 있는 모든 데이터베이스를 포함하는 사용자 지정 데이터베이스 컬렉션 대상 및 사용자 지정 데이터베이스 대상을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all the databases in the pool.</span></span>

<span data-ttu-id="eb678-306">원하는 데이터베이스 정보가 반영되도록 다음 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-306">Set the following variables to reflect the desired database information:</span></span>

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="to-create-a-custom-database-collection-target"></a><span data-ttu-id="eb678-307">사용자 지정 데이터베이스 컬렉션 대상을 만들려면</span><span class="sxs-lookup"><span data-stu-id="eb678-307">To create a custom database collection target</span></span>
<span data-ttu-id="eb678-308">[**New-AzureSqlJobTarget cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget)을 사용하여 정의된 여러 데이터베이스 대상에서 실행할 수 있도록 사용자 지정 데이터베이스 컬렉션 대상을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-308">Use the [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet to define a custom database collection target to enable execution across multiple defined database targets.</span></span> <span data-ttu-id="eb678-309">데이터베이스 그룹을 만든 후 사용자 지정 컬렉션 대상에 데이터베이스를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-309">After creating a database group, databases can be associated with the custom collection target.</span></span>

<span data-ttu-id="eb678-310">원하는 사용자 지정 컬렉션 대상 구성이 반영되도록 다음 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-310">Set the following variables to reflect the desired custom collection target configuration:</span></span>

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="to-add-databases-to-a-custom-database-collection-target"></a><span data-ttu-id="eb678-311">사용자 지정 데이터베이스 컬렉션 대상에 데이터베이스를 추가하려면</span><span class="sxs-lookup"><span data-stu-id="eb678-311">To add databases to a custom database collection target</span></span>
<span data-ttu-id="eb678-312">특정 사용자 지정 컬렉션에 데이터베이스를 추가하려면 [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-312">To add a database to a specific custom collection use the [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span></span>

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-the-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="eb678-313">사용자 지정 데이터베이스 컬렉션 대상 내의 데이터베이스 검토</span><span class="sxs-lookup"><span data-stu-id="eb678-313">Review the databases within a custom database collection target</span></span>
<span data-ttu-id="eb678-314">[**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet을 사용하여 사용자 지정 데이터베이스 컬렉션 대상 내의 자식 데이터베이스를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-314">Use the [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet to retrieve the child databases within a custom database collection target.</span></span> 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-to-execute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="eb678-315">사용자 지정 데이터베이스 컬렉션 대상에서 스크립트를 실행하는 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="eb678-315">Create a job to execute a script across a custom database collection target</span></span>
<span data-ttu-id="eb678-316">[**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet을 사용하여 사용자 지정 데이터베이스 컬렉션 대상에서 정의된 데이터베이스 그룹에 대한 작업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-316">Use the [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet to create a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="eb678-317">탄력적 데이터베이스 작업은 각각 사용자 지정 데이터베이스 컬렉션 대상과 연결된 데이터베이스에 해당하는 여러 자식 작업으로 작업을 확장하고 각 데이터베이스에 대해 스크립트가 실행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-317">Elastic Database jobs will expand the job into multiple child jobs each corresponding to a database associated with the custom database collection target and ensure that the script is executed against each database.</span></span> <span data-ttu-id="eb678-318">스크립트는 재시도 복구에 대해 idempotent여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-318">Again, it is important that scripts are idempotent to be resilient to retries.</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a><span data-ttu-id="eb678-319">데이터베이스에서 데이터 수집</span><span class="sxs-lookup"><span data-stu-id="eb678-319">Data collection across databases</span></span>
<span data-ttu-id="eb678-320">작업을 사용하여 데이터베이스 그룹에서 쿼리를 실행하고 결과를 특정 테이블에 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-320">You can use a job to execute a query across a group of databases and send the results to a specific table.</span></span> <span data-ttu-id="eb678-321">각 데이터베이스의 쿼리 결과를 볼 수 있으면 테이블을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-321">The table can be queried after the fact to see the query’s results from each database.</span></span> <span data-ttu-id="eb678-322">이는 많은 데이터베이스에서 쿼리를 실행하는 비동기 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-322">This provides an asynchronous method to execute a query across many databases.</span></span> <span data-ttu-id="eb678-323">실패한 시도는 재시도를 통해 자동으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-323">Failed attempts are handled automatically via retries.</span></span>

<span data-ttu-id="eb678-324">지정된 대상 테이블이 아직 없는 경우 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-324">The specified destination table will be automatically created if it does not yet exist.</span></span> <span data-ttu-id="eb678-325">새 테이블은 반환된 결과 집합의 스키마와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-325">The new table matches the schema of the returned result set.</span></span> <span data-ttu-id="eb678-326">스크립트에서 여러 결과 집합이 반환되는 경우 탄력적 데이터베이스 작업은 대상 테이블에 첫 번째 결과 집합만 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-326">If a script returns multiple result sets, Elastic Database jobs will only send the first to the destination table.</span></span>

<span data-ttu-id="eb678-327">다음 PowerShell 스크립트는 스크립트를 실행하고 지정된 테이블에 결과를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-327">The following PowerShell script executes a script and collects its results into a specified table.</span></span> <span data-ttu-id="eb678-328">이 스크립트는 단일 결과 집합을 출력하는 T-SQL 스크립트가 생성되었으며 사용자 지정 데이터베이스 컬렉션 대상이 생성되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span></span>

<span data-ttu-id="eb678-329">이 스크립트는 [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-329">This script uses the [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span></span> <span data-ttu-id="eb678-330">스크립트, 자격 증명 및 실행 대상에 대한 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-330">Set the parameters for script, credentials, and execution target:</span></span>

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

### <a name="to-create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="eb678-331">데이터 수집 시나리오에 대한 작업을 만들고 시작하려면</span><span class="sxs-lookup"><span data-stu-id="eb678-331">To create and start a job for data collection scenarios</span></span>
<span data-ttu-id="eb678-332">이 스크립트는 [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-332">This script uses the [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span></span>

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="to-schedule-a-job-execution-trigger"></a><span data-ttu-id="eb678-333">작업 실행 트리거를 예약하려면</span><span class="sxs-lookup"><span data-stu-id="eb678-333">To schedule a job execution trigger</span></span>
<span data-ttu-id="eb678-334">다음 PowerShell 스크립트를 사용하여 되풀이 일정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-334">The following PowerShell script can be used to create a recurring schedule.</span></span> <span data-ttu-id="eb678-335">이 스크립트는 분 간격을 사용하지만 [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule)은 -DayInterval, -HourInterval, -MonthInterval 및 -WeekInterval 매개 변수도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="eb678-336">-OneTime을 전달하여 한 번만 실행되는 일정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-336">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="eb678-337">새 일정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-337">Create a new schedule:</span></span>

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="to-trigger-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="eb678-338">시간 일정에 따라 실행되는 작업을 트리거하려면</span><span class="sxs-lookup"><span data-stu-id="eb678-338">To trigger a job executed on a time schedule</span></span>
<span data-ttu-id="eb678-339">시간 일정에 따라 작업을 실행하는 작업 트리거를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-339">A job trigger can be defined to have a job executed according to a time schedule.</span></span> <span data-ttu-id="eb678-340">다음 PowerShell 스크립트를 사용하여 작업 트리거를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-340">The following PowerShell script can be used to create a job trigger.</span></span>

<span data-ttu-id="eb678-341">[New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) 를 사용하고 원하는 작업 및 일정에 맞게 다음 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-341">Use [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) and set the following variables to correspond to the desired job and schedule:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="to-remove-a-scheduled-association-to-stop-job-from-executing-on-schedule"></a><span data-ttu-id="eb678-342">일정에 따라 작업이 실행되지 않도록 예약된 연결을 제거하려면</span><span class="sxs-lookup"><span data-stu-id="eb678-342">To remove a scheduled association to stop job from executing on schedule</span></span>
<span data-ttu-id="eb678-343">작업 트리거를 통한 되풀이 작업 실행을 중단하려면 작업 트리거를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-343">To discontinue reoccurring job execution through a job trigger, the job trigger can be removed.</span></span> <span data-ttu-id="eb678-344">[**Remove-AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger)을 사용하여 일정에 따라 작업이 실행되지 않도록 작업 트리거를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-344">Remove a job trigger to stop a job from being executed according to a schedule using the [**Remove-AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-to-a-time-schedule"></a><span data-ttu-id="eb678-345">시간 일정에 바인딩된 작업 트리거 검색</span><span class="sxs-lookup"><span data-stu-id="eb678-345">Retrieve job triggers bound to a time schedule</span></span>
<span data-ttu-id="eb678-346">다음 PowerShell 스크립트를 사용하여 특정 시간 일정에 등록된 작업 트리거를 가져오고 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-346">The following PowerShell script can be used to obtain and display the job triggers registered to a particular time schedule.</span></span>

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="to-retrieve-job-triggers-bound-to-a-job"></a><span data-ttu-id="eb678-347">작업에 바인딩된 작업 트리거를 검색하려면</span><span class="sxs-lookup"><span data-stu-id="eb678-347">To retrieve job triggers bound to a job</span></span>
<span data-ttu-id="eb678-348">[Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) 를 사용하여 등록된 작업을 포함하는 일정을 가져오고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) to obtain and display schedules containing a registered job.</span></span>

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="to-create-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="eb678-349">데이터베이스에서 실행할 DACPAC(데이터 계층 응용 프로그램)를 만들려면</span><span class="sxs-lookup"><span data-stu-id="eb678-349">To create a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="eb678-350">DACPAC를 만들려면 [데이터 계층 응용 프로그램](https://msdn.microsoft.com/library/ee210546.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb678-350">To create a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span></span> <span data-ttu-id="eb678-351">DACPAC를 배포하려면 [New-AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-351">To deploy a DACPAC, use the [New-AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span></span> <span data-ttu-id="eb678-352">DACPAC는 서비스에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-352">The DACPAC must be accessible to the service.</span></span> <span data-ttu-id="eb678-353">생성된 DACPAC를 Azure 저장소에 업로드하고 DACPAC에 대한 서 [공유 액세스 서명](../storage/common/storage-dotnet-shared-access-signature-part-1.md) 을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-353">It is recommended to upload a created DACPAC to Azure Storage and create a [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for the DACPAC.</span></span>

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="to-update-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="eb678-354">데이터베이스에서 실행할 DACPAC(데이터 계층 응용 프로그램)를 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="eb678-354">To update a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="eb678-355">탄력적 데이터베이스 작업 내에 등록된 기존 DACPAC를 새 URI를 가리키도록 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-355">Existing DACPACs registered within Elastic Database Jobs can be updated to point to new URIs.</span></span> <span data-ttu-id="eb678-356">[**Set-AzureSqlJobContentDefinition cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition)을 사용하여 기존에 등록된 DACPAC에서 DACPAC URI를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-356">Use the [**Set-AzureSqlJobContentDefinition cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) to update the DACPAC URI on an existing registered DACPAC:</span></span>

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="to-create-a-job-to-apply-a-data-tier-application-dacpac-across-databases"></a><span data-ttu-id="eb678-357">데이터베이스에 DACPAC(데이터 계층 응용 프로그램)를 적용하는 작업을 만들려면</span><span class="sxs-lookup"><span data-stu-id="eb678-357">To create a job to apply a data-tier application (DACPAC) across databases</span></span>
<span data-ttu-id="eb678-358">탄력적 데이터베이스 작업 내에서 DACPAC를 만든 후 데이터베이스 그룹에 DACPAC를 적용하는 작업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created to apply the DACPAC across a group of databases.</span></span> <span data-ttu-id="eb678-359">다음 PowerShell 스크립트를 사용하여 사용자 지정 데이터베이스 컬렉션에 대한 DACPAC 작업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb678-359">The following PowerShell script can be used to create a DACPAC job across a custom collection of databases:</span></span>

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->

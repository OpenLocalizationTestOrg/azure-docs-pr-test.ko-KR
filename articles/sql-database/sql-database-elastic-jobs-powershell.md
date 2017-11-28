---
title: "aaaCreate 탄력적 작업 PowerShell을 사용 하 고 관리 | Microsoft Docs"
description: "PowerShell은 toomanage Azure SQL 데이터베이스 풀 사용"
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
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a><span data-ttu-id="c3f3b-103">PowerShell을 사용하여 SQL Database 탄력적 작업 만들기 및 관리(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="c3f3b-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span></span>

<span data-ttu-id="c3f3b-104">hello PowerShell Api에 대 한 **탄력적 데이터베이스 작업** (미리 보기)에서 스크립트 실행 될 데이터베이스 그룹을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-104">hello PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span></span> <span data-ttu-id="c3f3b-105">이 문서에서는 어떻게 toocreate 및 관리 **탄력적 데이터베이스 작업** PowerShell cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-105">This article shows how toocreate and manage **Elastic Database jobs** using PowerShell cmdlets.</span></span> <span data-ttu-id="c3f3b-106">[탄력적 작업 개요](sql-database-elastic-jobs-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c3f3b-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c3f3b-107">Prerequisites</span></span>
* <span data-ttu-id="c3f3b-108">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-108">An Azure subscription.</span></span> <span data-ttu-id="c3f3b-109">무료 평가판에 대한 내용은 [무료 1개월 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c3f3b-110">집합 hello 탄력적 데이터베이스 도구를 사용 하 여 만든 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-110">A set of databases created with hello Elastic Database tools.</span></span> <span data-ttu-id="c3f3b-111">[탄력적 데이터베이스 도구 시작하기](sql-database-elastic-scale-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="c3f3b-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-112">Azure PowerShell.</span></span> <span data-ttu-id="c3f3b-113">자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](https://docs.microsoft.com/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-113">For detailed information, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
* <span data-ttu-id="c3f3b-114">**탄력적 데이터베이스 작업** PowerShell 패키지: [Installing 탄력적 데이터베이스 작업](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="c3f3b-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span></span>

### <a name="select-your-azure-subscription"></a><span data-ttu-id="c3f3b-115">Azure 구독 선택</span><span class="sxs-lookup"><span data-stu-id="c3f3b-115">Select your Azure subscription</span></span>
<span data-ttu-id="c3f3b-116">구독 Id를 필요한 tooselect hello 구독 (**-SubscriptionId**) 또는 구독 이름 (**-SubscriptionName**).</span><span class="sxs-lookup"><span data-stu-id="c3f3b-116">tooselect hello subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span></span> <span data-ttu-id="c3f3b-117">여러 구독이 있는 경우에 hello을 실행할 수 있습니다 **Get AzureRmSubscription** cmdlet 및 복사 hello hello 결과 집합에서 구독 정보를 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-117">If you have multiple subscriptions you can run hello **Get-AzureRmSubscription** cmdlet and copy hello desired subscription information from hello result set.</span></span> <span data-ttu-id="c3f3b-118">구독 정보를 사용 하는 후 hello 기본값으로 commandlet tooset 다음 hello이이 구독을 실행, 즉 대상 만들기 및 작업 관리에 대 한 hello:</span><span class="sxs-lookup"><span data-stu-id="c3f3b-118">Once you have your subscription information, run hello following commandlet tooset this subscription as hello default, namely hello target for creating and managing jobs:</span></span>

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

<span data-ttu-id="c3f3b-119">hello [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) hello 탄력적 데이터베이스 작업에 대 한 PowerShell 스크립트를 실행 하 고 사용 현황 toodevelop에 대 한 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-119">hello [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage toodevelop and execute PowerShell scripts against hello Elastic Database jobs.</span></span>

## <a name="elastic-database-jobs-objects"></a><span data-ttu-id="c3f3b-120">탄력적 데이터베이스 작업 개체</span><span class="sxs-lookup"><span data-stu-id="c3f3b-120">Elastic Database jobs objects</span></span>
<span data-ttu-id="c3f3b-121">다음 표에 모든 hello 개체 형식을 hello **탄력적 데이터베이스 작업** 해당 설명 및 관련 PowerShell Api와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-121">hello following table lists out all hello object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="c3f3b-122">개체 유형</span><span class="sxs-lookup"><span data-stu-id="c3f3b-122">Object Type</span></span></th>
    <th><span data-ttu-id="c3f3b-123">설명</span><span class="sxs-lookup"><span data-stu-id="c3f3b-123">Description</span></span></th>
    <th><span data-ttu-id="c3f3b-124">관련된 PowerShell API</span><span class="sxs-lookup"><span data-stu-id="c3f3b-124">Related PowerShell APIs</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="c3f3b-125">자격 증명</span><span class="sxs-lookup"><span data-stu-id="c3f3b-125">Credential</span></span></td>
    <td><span data-ttu-id="c3f3b-126">Dacpac의 응용 프로그램 또는 스크립트의 실행에 대 한 toodatabases 연결할 때의 사용자 이름 및 암호 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-126">Username and password toouse when connecting toodatabases for execution of scripts or application of DACPACs.</span></span> <p><span data-ttu-id="c3f3b-127">hello 암호 tooand hello 탄력적 데이터베이스 작업을 데이터베이스에 저장을 보내기 전에 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-127">hello password is encrypted before sending tooand storing in hello Elastic Database Jobs database.</span></span>  <span data-ttu-id="c3f3b-128">hello 암호 hello 만들어지고 hello 설치 스크립트에서 업로드 한 hello 자격 증명을 통해 탄력적 데이터베이스 작업 서비스에서 암호가 해독 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-128">hello password is decrypted by hello Elastic Database Jobs service via hello credential created and uploaded from hello installation script.</span></span></td>
    <td><p><span data-ttu-id="c3f3b-129">Get-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="c3f3b-129">Get-AzureSqlJobCredential</span></span></p>
    <p><span data-ttu-id="c3f3b-130">New-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="c3f3b-130">New-AzureSqlJobCredential</span></span></p><p><span data-ttu-id="c3f3b-131">Set-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="c3f3b-131">Set-AzureSqlJobCredential</span></span></p></td></td>
  </tr>

  <tr>
    <td><span data-ttu-id="c3f3b-132">스크립트</span><span class="sxs-lookup"><span data-stu-id="c3f3b-132">Script</span></span></td>
    <td><span data-ttu-id="c3f3b-133">Transact SQL 스크립트 toobe 데이터베이스에 걸쳐 실행에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-133">Transact-SQL script toobe used for execution across databases.</span></span>  <span data-ttu-id="c3f3b-134">hello 스크립트는 hello 서비스는 실패 시 hello 스크립트의 실행을 다시 시도 하므로 작성된 toobe idempotent 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-134">hello script should be authored toobe idempotent since hello service will retry execution of hello script upon failures.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="c3f3b-135">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="c3f3b-135">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="c3f3b-136">Get-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="c3f3b-136">Get-AzureSqlJobContentDefinition</span></span></p>
    <p><span data-ttu-id="c3f3b-137">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="c3f3b-137">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="c3f3b-138">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="c3f3b-138">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>

  <tr>
    <td><span data-ttu-id="c3f3b-139">DACPAC</span><span class="sxs-lookup"><span data-stu-id="c3f3b-139">DACPAC</span></span></td>
    <td><span data-ttu-id="c3f3b-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">데이터 계층 응용 프로그램 </a> 패키지 toobe 데이터베이스에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package toobe applied across databases.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="c3f3b-141">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="c3f3b-141">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="c3f3b-142">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="c3f3b-142">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="c3f3b-143">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="c3f3b-143">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="c3f3b-144">데이터베이스 대상</span><span class="sxs-lookup"><span data-stu-id="c3f3b-144">Database Target</span></span></td>
    <td><span data-ttu-id="c3f3b-145">데이터베이스 및 서버 포인팅 tooan Azure SQL 데이터베이스 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-145">Database and server name pointing tooan Azure SQL Database.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="c3f3b-146">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="c3f3b-146">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="c3f3b-147">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="c3f3b-147">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="c3f3b-148">분할된 데이터베이스 맵 대상</span><span class="sxs-lookup"><span data-stu-id="c3f3b-148">Shard Map Target</span></span></td>
    <td><span data-ttu-id="c3f3b-149">데이터베이스 대상과 자격 증명 toobe의 조합이 탄력적 데이터베이스 분할 맵을에 저장 된 toodetermine 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-149">Combination of a database target and a credential toobe used toodetermine information stored within an Elastic Database shard map.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="c3f3b-150">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="c3f3b-150">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="c3f3b-151">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="c3f3b-151">New-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="c3f3b-152">Set-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="c3f3b-152">Set-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="c3f3b-153">사용자 지정 컬렉션 대상</span><span class="sxs-lookup"><span data-stu-id="c3f3b-153">Custom Collection Target</span></span></td>
    <td><span data-ttu-id="c3f3b-154">정의 된 그룹의 데이터베이스 toocollectively 실행에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-154">Defined group of databases toocollectively use for execution.</span></span></td>
    <td>
    <p><span data-ttu-id="c3f3b-155">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="c3f3b-155">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="c3f3b-156">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="c3f3b-156">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="c3f3b-157">사용자 지정 컬렉션 자식 대상</span><span class="sxs-lookup"><span data-stu-id="c3f3b-157">Custom Collection Child Target</span></span></td>
    <td><span data-ttu-id="c3f3b-158">사용자 지정 컬렉션에서 참조되는 데이터베이스 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-158">Database target that is referenced from a custom collection.</span></span></td>
    <td>
    <p><span data-ttu-id="c3f3b-159">Add-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="c3f3b-159">Add-AzureSqlJobChildTarget</span></span></p>
    <p><span data-ttu-id="c3f3b-160">Remove-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="c3f3b-160">Remove-AzureSqlJobChildTarget</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="c3f3b-161">작업</span><span class="sxs-lookup"><span data-stu-id="c3f3b-161">Job</span></span></td>
    <td>
    <p><span data-ttu-id="c3f3b-162">사용 되는 tootrigger 실행 또는 toofulfill 일정을 지정할 수 있는 작업에 대 한 매개 변수 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-162">Definition of parameters for a job that can be used tootrigger execution or toofulfill a schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="c3f3b-163">Get-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="c3f3b-163">Get-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="c3f3b-164">New-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="c3f3b-164">New-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="c3f3b-165">Set-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="c3f3b-165">Set-AzureSqlJob</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="c3f3b-166">작업 실행</span><span class="sxs-lookup"><span data-stu-id="c3f3b-166">Job Execution</span></span></td>
    <td>
    <p><span data-ttu-id="c3f3b-167">스크립트를 실행 하거나 실패 하 여 데이터베이스 연결에 대 한 자격 증명을 사용 하 여 DACPAC tooa 대상 적용 필요한 toofulfill 작업의 컨테이너에 따라 tooan 실행 정책에서 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-167">Container of tasks necessary toofulfill either executing a script or applying a DACPAC tooa target using credentials for database connections with failures handled in accordance tooan execution policy.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="c3f3b-168">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="c3f3b-168">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="c3f3b-169">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="c3f3b-169">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="c3f3b-170">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="c3f3b-170">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="c3f3b-171">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="c3f3b-171">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="c3f3b-172">작업 태스크 실행</span><span class="sxs-lookup"><span data-stu-id="c3f3b-172">Job Task Execution</span></span></td>
    <td>
    <p><span data-ttu-id="c3f3b-173">작업 toofulfill 작업의 단일 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-173">Single unit of work toofulfill a job.</span></span></p>
    <p><span data-ttu-id="c3f3b-174">작업 태스크 toosuccessfully 수 없는 경우 실행, hello 결과 예외 메시지가 기록 되 고 새 일치 하는 작업 작업을 만들고 지정에 따라 toohello에서 실행 정책을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-174">If a job task is not able toosuccessfully execute, hello resulting exception message will be logged and a new matching job task will be created and executed in accordance toohello specified execution policy.</span></span></p></p>
    </td>
    <td>
    <p><span data-ttu-id="c3f3b-175">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="c3f3b-175">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="c3f3b-176">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="c3f3b-176">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="c3f3b-177">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="c3f3b-177">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="c3f3b-178">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="c3f3b-178">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="c3f3b-179">작업 실행 정책</span><span class="sxs-lookup"><span data-stu-id="c3f3b-179">Job Execution Policy</span></span></td>
    <td>
    <p><span data-ttu-id="c3f3b-180">작업 실행 시간 제한, 재시도 제한 및 재시도 간격을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-180">Controls job execution timeouts, retry limits and intervals between retries.</span></span></p>
    <p><span data-ttu-id="c3f3b-181">탄력적 데이터베이스 작업에는 각 재시도 간격의 지수 백오프를 통해 작업 태스크 실패의 무기한 재시도를 발생시키는 기본 작업 실행 정책이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="c3f3b-182">Get-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="c3f3b-182">Get-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="c3f3b-183">New-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="c3f3b-183">New-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="c3f3b-184">Set-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="c3f3b-184">Set-AzureSqlJobExecutionPolicy</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="c3f3b-185">일정</span><span class="sxs-lookup"><span data-stu-id="c3f3b-185">Schedule</span></span></td>
    <td>
    <p><span data-ttu-id="c3f3b-186">시간 간격을 되풀이 해야 하거나 한 번에 실행 tootake 위치에 대 한 사양을 기반합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-186">Time based specification for execution tootake place either on a reoccurring interval or at a single time.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="c3f3b-187">Get-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="c3f3b-187">Get-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="c3f3b-188">New-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="c3f3b-188">New-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="c3f3b-189">Set-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="c3f3b-189">Set-AzureSqlJobSchedule</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="c3f3b-190">작업 트리거</span><span class="sxs-lookup"><span data-stu-id="c3f3b-190">Job Triggers</span></span></td>
    <td>
    <p><span data-ttu-id="c3f3b-191">작업과 일정 tootrigger 작업 실행과 toohello 일정에 따라 간의 매핑.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-191">A mapping between a job and a schedule tootrigger job execution according toohello schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="c3f3b-192">New-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="c3f3b-192">New-AzureSqlJobTrigger</span></span></p>
    <p><span data-ttu-id="c3f3b-193">Remove-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="c3f3b-193">Remove-AzureSqlJobTrigger</span></span></p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a><span data-ttu-id="c3f3b-194">지원되는 탄력적 데이터베이스 작업 그룹 유형</span><span class="sxs-lookup"><span data-stu-id="c3f3b-194">Supported Elastic Database jobs group types</span></span>
<span data-ttu-id="c3f3b-195">hello 작업 그룹 데이터베이스에 대 한 TRANSACT-SQL (T-SQL) 스크립트 또는 Dacpac의 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-195">hello job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span></span> <span data-ttu-id="c3f3b-196">작업이 제출 된 toobe에서 실행 되 면 데이터베이스의 hello 작업 "확장" hello hello을 수행 각 자식 작업으로 그룹 hello 그룹에서 단일 데이터베이스에 대해 실행을 요청 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-196">When a job is submitted toobe executed across a group of databases, hello job “expands” hello into child jobs where each performs hello requested execution against a single database in hello group.</span></span> 

<span data-ttu-id="c3f3b-197">두 가지 형식의 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-197">There are two types of groups that you can create:</span></span> 

* <span data-ttu-id="c3f3b-198">[분할 맵은](sql-database-elastic-scale-shard-map-management.md) 그룹: 작업 제출 된 tootarget 분할 맵을 이면 hello 작업 hello shard map toodetermine 열의 현재 집합이 분할 된 데이터베이스를 쿼리 하 한 다음 hello 분할 맵을 자식 각 분할에 대 한 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted tootarget a shard map, hello job queries hello shard map toodetermine its current set of shards, and then creates child jobs for each shard in hello shard map.</span></span>
* <span data-ttu-id="c3f3b-199">사용자 지정 컬렉션 그룹: 사용자 지정 데이터베이스 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-199">Custom Collection group: A custom defined set of databases.</span></span> <span data-ttu-id="c3f3b-200">사용자 지정 컬렉션을 대상으로 하는 작업, 경우에 생성 됩니다 자식 각 데이터베이스에 대 한 작업 현재 hello 사용자 지정 컬렉션.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-200">When a job targets a custom collection, it creates child jobs for each database currently in hello custom collection.</span></span>

## <a name="tooset-hello-elastic-database-jobs-connection"></a><span data-ttu-id="c3f3b-201">tooset hello 탄력적 데이터베이스 작업 연결</span><span class="sxs-lookup"><span data-stu-id="c3f3b-201">tooset hello Elastic Database jobs connection</span></span>
<span data-ttu-id="c3f3b-202">연결이 필요한 toobe toohello 작업 설정 *제어 데이터베이스* 이전 toousing hello Api 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-202">A connection needs toobe set toohello jobs *control database* prior toousing hello jobs APIs.</span></span> <span data-ttu-id="c3f3b-203">이 cmdlet을 실행 한 자격 증명 창 toopop을 hello 사용자 이름 및 암호를 탄력적 데이터베이스 작업을 설치할 때 만든 요청을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-203">Running this cmdlet triggers a credential window toopop up requesting hello user name and password created when installing Elastic Database jobs.</span></span> <span data-ttu-id="c3f3b-204">이 항목에 제공된 모든 예제에서는 이 첫 번째 단계가 이미 수행되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-204">All examples provided within this topic assume that this first step has already been performed.</span></span>

<span data-ttu-id="c3f3b-205">연결 toohello 탄력적 데이터베이스 작업을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-205">Open a connection toohello Elastic Database jobs:</span></span>

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a><span data-ttu-id="c3f3b-206">Hello 탄력적 데이터베이스 작업 내에서 암호화 된 자격 증명</span><span class="sxs-lookup"><span data-stu-id="c3f3b-206">Encrypted credentials within hello Elastic Database jobs</span></span>
<span data-ttu-id="c3f3b-207">데이터베이스 자격 증명 hello 작업에 삽입할 수 *제어 데이터베이스* 암호화의 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-207">Database credentials can be inserted into hello jobs *control database*  with its password encrypted.</span></span> <span data-ttu-id="c3f3b-208">필요한 toostore 자격 증명 tooenable 작업 toobe는 나중에 실행 (작업 일정 사용) 이며</span><span class="sxs-lookup"><span data-stu-id="c3f3b-208">It is necessary toostore credentials tooenable jobs toobe executed at a later time, (using job schedules).</span></span>

<span data-ttu-id="c3f3b-209">암호화는 hello 설치 스크립트의 일부분으로 만든 인증서를 통해 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-209">Encryption works through a certificate created as part of hello installation script.</span></span> <span data-ttu-id="c3f3b-210">hello 설치 스크립트를 만들고 hello의 암호 해독에 대 한 hello Azure 클라우드 서비스에 업로드 hello 인증서는 암호화 된 암호를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-210">hello installation script creates and uploads hello certificate into hello Azure Cloud Service for decryption of hello stored encrypted passwords.</span></span> <span data-ttu-id="c3f3b-211">hello hello 작업 내에서 공개 키를 저장 하는 나중에 Azure 클라우드 서비스 hello *제어 데이터베이스* hello 인증서를 요구 하지 않고 hello PowerShell API 또는 Azure 클래식 포털 인터페이스 tooencrypt 제공 된 암호 수 toobe 로컬로 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-211">hello Azure Cloud Service later stores hello public key within hello jobs *control database* which enables hello PowerShell API or Azure Classic Portal interface tooencrypt a provided password without requiring hello certificate toobe locally installed.</span></span>

<span data-ttu-id="c3f3b-212">hello 자격 증명 암호 암호화 되 고 읽기 전용 액세스 tooElastic 데이터베이스 작업 개체는 사용자 로부터 안전한 는합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-212">hello credential passwords are encrypted and secure from users with read-only access tooElastic Database jobs objects.</span></span> <span data-ttu-id="c3f3b-213">하지만 읽기 / 쓰기 액세스 tooElastic 데이터베이스 작업을 개체 tooextract 암호를 가진 악의적인 사용자에 대 한 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-213">But it is possible for a malicious user with read-write access tooElastic Database Jobs objects tooextract a password.</span></span> <span data-ttu-id="c3f3b-214">자격 증명은 작업 실행에서 다시 디자인 된 toobe.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-214">Credentials are designed toobe reused across job executions.</span></span> <span data-ttu-id="c3f3b-215">연결을 설정할 때 자격 증명 tootarget 데이터베이스를 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-215">Credentials are passed tootarget databases when establishing connections.</span></span> <span data-ttu-id="c3f3b-216">현재 각 자격 증명에 대해 사용 하는 hello 대상 데이터베이스에 제한이 없습니다, 악의적인 사용자는 hello 악의적인 사용자가 제어 데이터베이스에 대 한 데이터베이스 대상을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-216">There are currently no restrictions on hello target databases used for each credential, malicious user could add a database target for a database under hello malicious user's control.</span></span> <span data-ttu-id="c3f3b-217">hello 사용자는이 데이터베이스 toogain hello 자격 증명의이 암호를 대상으로 하는 작업을 시작 이후에 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-217">hello user could subsequently start a job targeting this database toogain hello credential's password.</span></span>

<span data-ttu-id="c3f3b-218">탄력적 데이터베이스 작업에 대한 보안 모범 사례는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-218">Security best practices for Elastic Database jobs include:</span></span>

* <span data-ttu-id="c3f3b-219">Hello Api tootrusted 개인의 사용을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-219">Limit usage of hello APIs tootrusted individuals.</span></span>
* <span data-ttu-id="c3f3b-220">자격 증명 hello 있어야 합니다. 최소 권한이 필요한 tooperform hello 작업 태스크입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-220">Credentials should have hello least privileges necessary tooperform hello job task.</span></span>  <span data-ttu-id="c3f3b-221">자세한 내용은 이 [권한 부여 및 사용 권한](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN 문서에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span></span>

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a><span data-ttu-id="c3f3b-222">데이터베이스에 걸쳐 작업 실행에는 암호화 된 자격 증명 toocreate</span><span class="sxs-lookup"><span data-stu-id="c3f3b-222">toocreate an encrypted credential for job execution across databases</span></span>
<span data-ttu-id="c3f3b-223">새 암호화 toocreate 자격 증명, hello [ **Get-credential cmdlet** ](https://technet.microsoft.com/library/hh849815.aspx) 사용자 이름 및 toohello 전달 될 수 있는 암호를 묻는 [ **AzureSqlJobCredential 새로 만들기 cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-223">toocreate a new encrypted credential, hello [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed toohello [**New-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span></span>

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a><span data-ttu-id="c3f3b-224">tooupdate 자격 증명</span><span class="sxs-lookup"><span data-stu-id="c3f3b-224">tooupdate credentials</span></span>
<span data-ttu-id="c3f3b-225">암호 변경 될 때 사용 하 여 hello [ **집합 AzureSqlJobCredential cmdlet** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) 집합 hello 및 **CredentialName** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-225">When passwords change, use hello [**Set-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) and set hello **CredentialName** parameter.</span></span>

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a><span data-ttu-id="c3f3b-226">toodefine 탄력적 데이터베이스 분할 맵 대상</span><span class="sxs-lookup"><span data-stu-id="c3f3b-226">toodefine an Elastic Database shard map target</span></span>
<span data-ttu-id="c3f3b-227">분할 집합의 모든 데이터베이스에 대해 작업 tooexecute (사용 하 여 만든 [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md)), hello 데이터베이스 대상 분할 맵을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-227">tooexecute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as hello database target.</span></span> <span data-ttu-id="c3f3b-228">이 예제는 hello 탄력적 데이터베이스 클라이언트 라이브러리를 사용 하 여 만든 분할 응용 프로그램이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-228">This example requires a sharded application created using hello Elastic Database client library.</span></span> <span data-ttu-id="c3f3b-229">[탄력적 데이터베이스 도구 샘플 시작](sql-database-elastic-scale-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

<span data-ttu-id="c3f3b-230">hello shard map manager 데이터베이스는 데이터베이스 대상으로 설정 해야 하 고 hello 특정 분할 맵은 대상으로 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-230">hello shard map manager database must be set as a database target and then hello specific shard map must be specified as a target.</span></span>

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="c3f3b-231">데이터베이스에서 실행할 T-SQL 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="c3f3b-231">Create a T-SQL Script for execution across databases</span></span>
<span data-ttu-id="c3f3b-232">실행에 대 한 T-SQL 스크립트를 만들 때이 가장 좋습니다 toobuild 해당 toobe [idempotent](https://en.wikipedia.org/wiki/Idempotence) 및 오류에 대 한 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-232">When creating T-SQL scripts for execution, it is highly recommended toobuild them toobe [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span></span> <span data-ttu-id="c3f3b-233">탄력적 데이터베이스 작업 실행 hello 오류의 hello 분류에 관계 없이 오류가 발생할 때마다 스크립트의 실행을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of hello classification of hello failure.</span></span>

<span data-ttu-id="c3f3b-234">사용 하 여 hello [ **새로 AzureSqlJobContent cmdlet** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate 및 실행에 대 한 스크립트를 저장 하 고 hello 설정할 **-ContentName** 및 **-CommandText**매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-234">Use hello [**New-AzureSqlJobContent cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate and save a script for execution and set hello **-ContentName** and **-CommandText** parameters.</span></span>

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

### <a name="create-a-new-script-from-a-file"></a><span data-ttu-id="c3f3b-235">파일에서 새 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="c3f3b-235">Create a new script from a file</span></span>
<span data-ttu-id="c3f3b-236">Hello T-SQL 스크립트 파일 내에서 정의 된 경우이 tooimport hello 스크립트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-236">If hello T-SQL script is defined within a file, use this tooimport hello script:</span></span>

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="c3f3b-237">데이터베이스에 걸쳐 실행에 사용 되는 T-SQL tooupdate 스크립트</span><span class="sxs-lookup"><span data-stu-id="c3f3b-237">tooupdate a T-SQL script for execution across databases</span></span>
<span data-ttu-id="c3f3b-238">이 PowerShell 스크립트 업데이트 hello 기존 스크립트에 대 한 T-SQL 명령 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-238">This PowerShell script updates hello T-SQL command text for an existing script.</span></span>

<span data-ttu-id="c3f3b-239">변수 tooreflect 원하는 hello 스크립트 정의 toobe 집합을 추적 하는 집합 hello:</span><span class="sxs-lookup"><span data-stu-id="c3f3b-239">Set hello following variables tooreflect hello desired script definition toobe set:</span></span>

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
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

### <a name="tooupdate-hello-definition-tooan-existing-script"></a><span data-ttu-id="c3f3b-240">tooupdate hello 정의 tooan 기존 스크립트</span><span class="sxs-lookup"><span data-stu-id="c3f3b-240">tooupdate hello definition tooan existing script</span></span>
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a><span data-ttu-id="c3f3b-241">toocreate 작업 tooexecute 분할 맵을 통해 스크립트</span><span class="sxs-lookup"><span data-stu-id="c3f3b-241">toocreate a job tooexecute a script across a shard map</span></span>
<span data-ttu-id="c3f3b-242">이 PowerShell 스크립트는 탄력적 확장 분할된 데이터베이스 맵의 각 분할된 데이터베이스에서 스크립트를 실행하는 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span></span>

<span data-ttu-id="c3f3b-243">다음 변수 tooreflect hello 집합 hello 필요한 스크립트 및 대상:</span><span class="sxs-lookup"><span data-stu-id="c3f3b-243">Set hello following variables tooreflect hello desired script and target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a><span data-ttu-id="c3f3b-244">tooexecute 작업</span><span class="sxs-lookup"><span data-stu-id="c3f3b-244">tooexecute a job</span></span>
<span data-ttu-id="c3f3b-245">이 PowerShell 스크립트는 기존 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-245">This PowerShell script executes an existing job:</span></span>

<span data-ttu-id="c3f3b-246">다음 실행 하는 변수 tooreflect hello 원하는 작업 이름 toohave hello를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-246">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="c3f3b-247">단일 작업 실행 tooretrieve hello 상태</span><span class="sxs-lookup"><span data-stu-id="c3f3b-247">tooretrieve hello state of a single job execution</span></span>
<span data-ttu-id="c3f3b-248">사용 하 여 hello [ **Get AzureSqlJobExecution cmdlet** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) 및 집합 hello **JobExecutionId** 작업 실행의 매개 변수 tooview hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-248">Use hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) and set hello **JobExecutionId** parameter tooview hello state of job execution.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

<span data-ttu-id="c3f3b-249">사용 하 여 hello 동일 **Get AzureSqlJobExecution** hello 사용 하 여 cmdlet **includechildren를 실행** 자식 작업 실행의 매개 변수 tooview hello 상태 각각에 대해 각 작업 실행에 대 한 특정 상태를 즉 hello hello 작업의 대상인 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-249">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a><span data-ttu-id="c3f3b-250">여러 작업 실행 간에 tooview hello 상태</span><span class="sxs-lookup"><span data-stu-id="c3f3b-250">tooview hello state across multiple job executions</span></span>
<span data-ttu-id="c3f3b-251">hello [ **Get AzureSqlJobExecution cmdlet** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) 에 사용 되는 toodisplay 일 수 있는 여러 선택적 매개 변수 hello 제공 된 매개 변수를 통해 필터링, 작업 실행이 여러 개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-251">hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="c3f3b-252">hello 다음 hello 가지가 toouse Get AzureSqlJobExecution의 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-252">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="c3f3b-253">모든 활성 최상위 작업 실행을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-253">Retrieve all active top level job executions:</span></span>

    Get-AzureSqlJobExecution

<span data-ttu-id="c3f3b-254">비활성 작업 실행을 포함하여 모든 최상위 작업 실행을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-254">Retrieve all top level job executions, including inactive job executions:</span></span>

    Get-AzureSqlJobExecution -IncludeInactive

<span data-ttu-id="c3f3b-255">비활성 작업 실행을 포함하여 제공된 작업 실행 ID의 모든 자식 작업 실행을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

<span data-ttu-id="c3f3b-256">비활성 작업을 포함하여 일정/작업 조합으로 만든 모든 작업 실행을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

<span data-ttu-id="c3f3b-257">비활성 작업을 포함하여 지정된 분할된 데이터베이스 맵을 대상으로 하는 모든 작업을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="c3f3b-258">비활성 작업을 포함하여 지정된 사용자 지정 컬렉션을 대상으로 하는 모든 작업을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="c3f3b-259">특정 작업 실행 내에서 작업 태스크 실행의 hello 목록 검색:</span><span class="sxs-lookup"><span data-stu-id="c3f3b-259">Retrieve hello list of job task executions within a specific job execution:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

<span data-ttu-id="c3f3b-260">작업 태스크 실행 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-260">Retrieve job task execution details:</span></span>

<span data-ttu-id="c3f3b-261">hello PowerShell 스크립트 뒤의 실행 실패를 디버깅할 때 매우 유용 작업 작업 실행을 사용 하는 tooview hello 세부 정보 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-261">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a><span data-ttu-id="c3f3b-262">작업 작업 실행 내에서 tooretrieve 오류</span><span class="sxs-lookup"><span data-stu-id="c3f3b-262">tooretrieve failures within job task executions</span></span>
<span data-ttu-id="c3f3b-263">hello **JobTaskExecution 개체** 메시지 속성과 함께 hello 작업의 수명 주기 hello에 대 한 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-263">hello **JobTaskExecution object** includes a property for hello lifecycle of hello task along with a message property.</span></span> <span data-ttu-id="c3f3b-264">Hello 수명 주기 속성은 너무 설정 작업 태스크 실행에 실패 한 경우*실패* toohello 결과 예외 메시지 및 스택 hello 메시지 속성이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-264">If a job task execution failed, hello lifecycle property will be set too*Failed* and hello message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="c3f3b-265">작업이 수행 되지 않은 경우 지정된 된 작업에 대 한 실패 작업 실행 태스크가의 중요 한 tooview hello 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-265">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a><span data-ttu-id="c3f3b-266">작업 실행 toocomplete에 대 한 toowait</span><span class="sxs-lookup"><span data-stu-id="c3f3b-266">toowait for a job execution toocomplete</span></span>
<span data-ttu-id="c3f3b-267">PowerShell 스크립트 뒤 hello 작업 작업 toocomplete에 대 한 사용된 toowait 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-267">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="c3f3b-268">사용자 지정 실행 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="c3f3b-268">Create a custom execution policy</span></span>
<span data-ttu-id="c3f3b-269">탄력적 데이터베이스 작업은 작업을 시작할 때 적용할 수 있는 사용자 지정 실행 정책 만들기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="c3f3b-270">실행 정책은 현재 다음과 같은 정의를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-270">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="c3f3b-271">Hello 실행 정책에 대 한 이름: 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-271">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="c3f3b-272">작업 시간 제한: 탄력적 데이터베이스 작업에 의해 작업이 취소되기 전의 총 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="c3f3b-273">첫 번째 다시 시도 하기 전에 초기 다시 시도 간격: 간격 toowait 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-273">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="c3f3b-274">다시 시도 간격 toouse의 최대 다시 시도 간격: 상한입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-274">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="c3f3b-275">다시 시도 간격 백오프 계수: 계수가 toocalculate hello 다음 재시도 간격을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-275">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="c3f3b-276">hello 다음 수식을 사용 하는: (초기 재시도 간격) * Math.pow ((계수 백오프 간격) (다시 시도 횟수)-2).</span><span class="sxs-lookup"><span data-stu-id="c3f3b-276">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span> 
* <span data-ttu-id="c3f3b-277">작업 내에서 다시 시도 횟수 tooperform의 최대 시도 횟수: hello의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-277">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="c3f3b-278">hello 기본 실행 정책은 다음 값에는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-278">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="c3f3b-279">이름: 기본 실행 정책</span><span class="sxs-lookup"><span data-stu-id="c3f3b-279">Name: Default execution policy</span></span>
* <span data-ttu-id="c3f3b-280">작업 시간 제한: 1주</span><span class="sxs-lookup"><span data-stu-id="c3f3b-280">Job Timeout: 1 week</span></span>
* <span data-ttu-id="c3f3b-281">초기 재시도 간격: 100밀리초</span><span class="sxs-lookup"><span data-stu-id="c3f3b-281">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="c3f3b-282">최대 재시도 간격: 30분</span><span class="sxs-lookup"><span data-stu-id="c3f3b-282">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="c3f3b-283">재시도 간격 계수: 2</span><span class="sxs-lookup"><span data-stu-id="c3f3b-283">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="c3f3b-284">최대 시도 횟수: 2,147,483,647</span><span class="sxs-lookup"><span data-stu-id="c3f3b-284">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="c3f3b-285">원하는 hello 실행 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-285">Create hello desired execution policy:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="c3f3b-286">사용자 지정 실행 정책 업데이트</span><span class="sxs-lookup"><span data-stu-id="c3f3b-286">Update a custom execution policy</span></span>
<span data-ttu-id="c3f3b-287">원하는 hello 실행 정책 tooupdate를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-287">Update hello desired execution policy tooupdate:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a><span data-ttu-id="c3f3b-288">작업 취소</span><span class="sxs-lookup"><span data-stu-id="c3f3b-288">Cancel a job</span></span>
<span data-ttu-id="c3f3b-289">탄력적 데이터베이스 작업은 작업 취소 요청을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-289">Elastic Database Jobs supports cancellation requests of jobs.</span></span>  <span data-ttu-id="c3f3b-290">탄력적 데이터베이스 작업에서 현재 실행 중인 작업에 대 한 취소 요청을 감지한 경우 toostop hello 작업을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="c3f3b-291">탄력적 데이터베이스 작업이 취소를 수행할 수 있는 방법에는 다음 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="c3f3b-292">현재 실행 중인 작업이 취소: 작업이 현재 실행 되는 동안 취소가 검색 되 면 취소가 현재 hello 작업의 측면을 실행 하는 hello 내에서 시도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="c3f3b-293">예를 들어: 시도가 toocancel hello 쿼리 됩니다는 장기 실행 쿼리는 취소 하려고 할 때 현재 수행 중인 경우.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="c3f3b-294">태스크 다시 시도 취소: hello 제어 스레드 hello 작업을 시작 하지 않도록 하 고 취소 됨으로 hello 요청 선언 됩니다 취소가 실행에 대 한 태스크를 시작 하기 전에 hello 제어 스레드에 의해 검색 되 면 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-294">Canceling task retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="c3f3b-295">부모 작업에 대 한 작업 취소가 요청 하 고 모든 해당 자식 작업에 대 한 hello 부모 작업에 대 한 hello 취소 요청이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-295">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="c3f3b-296">toosubmit 취소 요청을 사용 하 여 hello [ **중지 AzureSqlJobExecution cmdlet** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) 및 집합 hello **JobExecutionId** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-296">toosubmit a cancellation request, use hello [**Stop-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) and set hello **JobExecutionId** parameter.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a><span data-ttu-id="c3f3b-297">toodelete 작업을 비동기적으로 작업 기록 및</span><span class="sxs-lookup"><span data-stu-id="c3f3b-297">toodelete a job and job history asynchronously</span></span>
<span data-ttu-id="c3f3b-298">탄력적 데이터베이스 작업은 비동기 작업 삭제를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-298">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="c3f3b-299">작업을 삭제 하도록 표시할 수 있습니다 및 hello 작업에 대 한 모든 작업 실행 완료 된 후 hello 시스템 hello 작업 및 모든 작업 기록을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-299">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="c3f3b-300">hello 시스템 활성 작업 실행 될 때 자동으로 취소 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-300">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="c3f3b-301">호출 [ **중지 AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel 활성 작업 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-301">Invoke [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel active job executions.</span></span>

<span data-ttu-id="c3f3b-302">tootrigger 작업 삭제를 사용 하 여 hello [ **제거 AzureSqlJob cmdlet** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) 및 집합 hello **JobName** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-302">tootrigger job deletion, use hello [**Remove-AzureSqlJob cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) and set hello **JobName** parameter.</span></span>

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a><span data-ttu-id="c3f3b-303">사용자 지정 데이터베이스 대상 toocreate</span><span class="sxs-lookup"><span data-stu-id="c3f3b-303">toocreate a custom database target</span></span>
<span data-ttu-id="c3f3b-304">직접 실행하거나 사용자 지정 데이터베이스 그룹 내에 포함할 사용자 지정 데이터베이스 대상을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span></span> <span data-ttu-id="c3f3b-305">예를 들어 있으므로 **탄력적 풀** 는 아직 직접 지원 PowerShell Api를 사용 하 여 만들 수 있습니다는 사용자 지정 데이터베이스 대상과 hello 풀에서 모든 hello 데이터베이스를 포괄 하는 사용자 지정 데이터베이스 컬렉션 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="c3f3b-306">Hello 다음 변수 tooreflect hello 필요한 데이터베이스 정보를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-306">Set hello following variables tooreflect hello desired database information:</span></span>

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a><span data-ttu-id="c3f3b-307">toocreate 사용자 지정 데이터베이스 수집 대상</span><span class="sxs-lookup"><span data-stu-id="c3f3b-307">toocreate a custom database collection target</span></span>
<span data-ttu-id="c3f3b-308">사용 하 여 hello [ **새로 AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine 여러 정의 된 데이터베이스 대상 사용자 지정 데이터베이스 컬렉션 대상 tooenable 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-308">Use hello [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine a custom database collection target tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="c3f3b-309">데이터베이스 그룹을 만든 후 데이터베이스 사용자 지정 컬렉션을 대상 hello와 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-309">After creating a database group, databases can be associated with hello custom collection target.</span></span>

<span data-ttu-id="c3f3b-310">같은 변수 tooreflect hello 원하는 사용자 지정 컬렉션 대상 구성이 hello를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-310">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="c3f3b-311">tooadd 데이터베이스 tooa 사용자 지정 데이터베이스 수집 대상</span><span class="sxs-lookup"><span data-stu-id="c3f3b-311">tooadd databases tooa custom database collection target</span></span>
<span data-ttu-id="c3f3b-312">특정 사용자 지정 컬렉션 tooa 데이터베이스 tooadd hello를 사용 하 여 [ **추가 AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-312">tooadd a database tooa specific custom collection use hello [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span></span>

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="c3f3b-313">사용자 지정 데이터베이스 컬렉션 대상 내에서 데이터베이스를 hello 검토</span><span class="sxs-lookup"><span data-stu-id="c3f3b-313">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="c3f3b-314">사용 하 여 hello [ **Get AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve hello 자식 데이터베이스 사용자 지정 데이터베이스 컬렉션 대상 내에서.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-314">Use hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve hello child databases within a custom database collection target.</span></span> 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="c3f3b-315">사용자 지정 데이터베이스 수집 대상에서 작업 tooexecute 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="c3f3b-315">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="c3f3b-316">사용 하 여 hello [ **새로 AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate 그룹 사용자 지정 데이터베이스 컬렉션 대상에 의해 정의 된 데이터베이스에 대해 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-316">Use hello [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="c3f3b-317">탄력적 데이터베이스 작업을 각각 해당 tooa 데이터베이스 hello 사용자 지정 데이터베이스 컬렉션 대상과 연결 된 및 hello 스크립트 각 데이터베이스에 대해 실행 되도록 확인 여러 자식 작업으로 hello 작업으로 확장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-317">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="c3f3b-318">마찬가지로 스크립트 idempotent toobe 탄력적인 tooretries 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-318">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a><span data-ttu-id="c3f3b-319">데이터베이스에서 데이터 수집</span><span class="sxs-lookup"><span data-stu-id="c3f3b-319">Data collection across databases</span></span>
<span data-ttu-id="c3f3b-320">데이터베이스의 그룹에 걸쳐 작업 tooexecute 쿼리를 사용 하 여 한 hello 결과 tooa 특정 테이블을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-320">You can use a job tooexecute a query across a group of databases and send hello results tooa specific table.</span></span> <span data-ttu-id="c3f3b-321">각 데이터베이스의 hello 팩트 toosee hello 쿼리 결과 후 hello 테이블을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-321">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="c3f3b-322">이 쿼리를 제공 비동기 메서드 tooexecute 많은 데이터베이스에 걸쳐 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-322">This provides an asynchronous method tooexecute a query across many databases.</span></span> <span data-ttu-id="c3f3b-323">실패한 시도는 재시도를 통해 자동으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-323">Failed attempts are handled automatically via retries.</span></span>

<span data-ttu-id="c3f3b-324">아직 존재 하지 않는 경우 hello 지정 된 대상 테이블이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-324">hello specified destination table will be automatically created if it does not yet exist.</span></span> <span data-ttu-id="c3f3b-325">hello 새 테이블의 결과 집합을 반환 하는 hello hello 스키마와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-325">hello new table matches hello schema of hello returned result set.</span></span> <span data-ttu-id="c3f3b-326">스크립트에서 여러 결과 집합을 반환 하는 경우 탄력적 데이터베이스 작업 hello 첫 번째 toohello 대상 테이블에만 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-326">If a script returns multiple result sets, Elastic Database jobs will only send hello first toohello destination table.</span></span>

<span data-ttu-id="c3f3b-327">hello 다음 PowerShell 스크립트는 스크립트를 실행 하 고 수집 결과 지정된 된 테이블에 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-327">hello following PowerShell script executes a script and collects its results into a specified table.</span></span> <span data-ttu-id="c3f3b-328">이 스크립트는 단일 결과 집합을 출력하는 T-SQL 스크립트가 생성되었으며 사용자 지정 데이터베이스 컬렉션 대상이 생성되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span></span>

<span data-ttu-id="c3f3b-329">이 스크립트 hello를 사용 하 여 [ **Get AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-329">This script uses hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span></span> <span data-ttu-id="c3f3b-330">스크립트, 자격 증명 및 실행 대상에 대 한 hello 매개 변수 설정:</span><span class="sxs-lookup"><span data-stu-id="c3f3b-330">Set hello parameters for script, credentials, and execution target:</span></span>

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

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="c3f3b-331">toocreate 및 데이터 컬렉션 시나리오에 대 한 작업 시작</span><span class="sxs-lookup"><span data-stu-id="c3f3b-331">toocreate and start a job for data collection scenarios</span></span>
<span data-ttu-id="c3f3b-332">이 스크립트 hello를 사용 하 여 [ **시작 AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-332">This script uses hello [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span></span>

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

## <a name="tooschedule-a-job-execution-trigger"></a><span data-ttu-id="c3f3b-333">작업 실행 트리거 tooschedule</span><span class="sxs-lookup"><span data-stu-id="c3f3b-333">tooschedule a job execution trigger</span></span>
<span data-ttu-id="c3f3b-334">PowerShell 스크립트 뒤 hello 사용된 toocreate 되풀이 일정 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-334">hello following PowerShell script can be used toocreate a recurring schedule.</span></span> <span data-ttu-id="c3f3b-335">이 스크립트는 분 간격을 사용하지만 [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule)은 -DayInterval, -HourInterval, -MonthInterval 및 -WeekInterval 매개 변수도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="c3f3b-336">-OneTime을 전달하여 한 번만 실행되는 일정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-336">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="c3f3b-337">새 일정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-337">Create a new schedule:</span></span>

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="c3f3b-338">tootrigger 된 일정에서 실행 되는 작업</span><span class="sxs-lookup"><span data-stu-id="c3f3b-338">tootrigger a job executed on a time schedule</span></span>
<span data-ttu-id="c3f3b-339">작업 트리거는 정의 된 실행 작업에 따라 tooa 시간 일정 toohave 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-339">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="c3f3b-340">PowerShell 스크립트 뒤 hello 사용된 toocreate 작업 트리거 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-340">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="c3f3b-341">사용 하 여 [새로 AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) 집합 hello 변수 toocorrespond toohello 원하는 작업 및 일정에 따라:</span><span class="sxs-lookup"><span data-stu-id="c3f3b-341">Use [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) and set hello following variables toocorrespond toohello desired job and schedule:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="c3f3b-342">tooremove 일정에 따라 실행 되는 예약 된 연결 toostop 작업</span><span class="sxs-lookup"><span data-stu-id="c3f3b-342">tooremove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="c3f3b-343">작업 트리거 hello 작업 트리거를 통해 작업 실행을 다시 발생 toodiscontinue는 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-343">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span> <span data-ttu-id="c3f3b-344">실행 되는 작업의 작업 트리거 toostop 제거 hello를 사용 하 여 따라 tooa 일정 [ **제거 AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-344">Remove a job trigger toostop a job from being executed according tooa schedule using hello [**Remove-AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a><span data-ttu-id="c3f3b-345">작업 트리거 바인딩된 tooa 시간 일정을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-345">Retrieve job triggers bound tooa time schedule</span></span>
<span data-ttu-id="c3f3b-346">PowerShell 스크립트 뒤 hello 사용된 tooobtain를 수 있으며 hello 작업 트리거 tooa 등록 된 특정 시간 일정이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-346">hello following PowerShell script can be used tooobtain and display hello job triggers registered tooa particular time schedule.</span></span>

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a><span data-ttu-id="c3f3b-347">작업 트리거 tooretrieve 바인딩된 tooa 작업</span><span class="sxs-lookup"><span data-stu-id="c3f3b-347">tooretrieve job triggers bound tooa job</span></span>
<span data-ttu-id="c3f3b-348">사용 하 여 [Get AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) 등록 된 작업을 포함 하는 일정을 tooobtain 및 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain and display schedules containing a registered job.</span></span>

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="c3f3b-349">데이터베이스에 걸쳐 실행에 대 한 데이터 계층 응용 프로그램 (DACPAC) toocreate</span><span class="sxs-lookup"><span data-stu-id="c3f3b-349">toocreate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="c3f3b-350">DACPAC를 toocreate 참조 [데이터 계층 응용 프로그램](https://msdn.microsoft.com/library/ee210546.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-350">toocreate a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span></span> <span data-ttu-id="c3f3b-351">toodeploy DACPAC를 사용 하 여 hello [새로 AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-351">toodeploy a DACPAC, use hello [New-AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span></span> <span data-ttu-id="c3f3b-352">hello DACPAC에 액세스할 수 있는 toohello 서비스 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-352">hello DACPAC must be accessible toohello service.</span></span> <span data-ttu-id="c3f3b-353">만들고 생성된 된 DACPAC tooAzure 저장소 tooupload 권장 한 [공유 액세스 서명을](../storage/common/storage-dotnet-shared-access-signature-part-1.md) hello DACPAC에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-353">It is recommended tooupload a created DACPAC tooAzure Storage and create a [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for hello DACPAC.</span></span>

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="c3f3b-354">데이터베이스에 걸쳐 실행에 대 한 데이터 계층 응용 프로그램 (DACPAC) tooupdate</span><span class="sxs-lookup"><span data-stu-id="c3f3b-354">tooupdate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="c3f3b-355">탄력적 데이터베이스 작업 내에 등록 하는 기존 Dacpac 업데이트 toopoint toonew Uri 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-355">Existing DACPACs registered within Elastic Database Jobs can be updated toopoint toonew URIs.</span></span> <span data-ttu-id="c3f3b-356">사용 하 여 hello [ **집합 AzureSqlJobContentDefinition cmdlet** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) 기존 tooupdate hello DACPAC URI DACPAC를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-356">Use hello [**Set-AzureSqlJobContentDefinition cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI on an existing registered DACPAC:</span></span>

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a><span data-ttu-id="c3f3b-357">toocreate 작업 tooapply 데이터베이스 간에 데이터 계층 응용 프로그램 (DACPAC)</span><span class="sxs-lookup"><span data-stu-id="c3f3b-357">toocreate a job tooapply a data-tier application (DACPAC) across databases</span></span>
<span data-ttu-id="c3f3b-358">탄력적 데이터베이스 작업 내에서 DACPAC를 만든 후 작업은 데이터베이스 그룹에 걸쳐 tooapply hello DACPAC 만들 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created tooapply hello DACPAC across a group of databases.</span></span> <span data-ttu-id="c3f3b-359">PowerShell 스크립트 뒤 hello 데이터베이스의 사용자 지정 컬렉션에서 사용 되는 toocreate DACPAC 작업이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3b-359">hello following PowerShell script can be used toocreate a DACPAC job across a custom collection of databases:</span></span>

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

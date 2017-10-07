---
title: Azure Analysis Services powershell aaaManage | Microsoft Docs
description: "PowerShell 사용한 Azure Analysis Services 관리입니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: owend
ms.openlocfilehash: bc4250bf77b5a0d86c1049ee57493bcf2a1f0c1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-analysis-services-with-powershell"></a><span data-ttu-id="b98f2-103">PowerShell을 사용하여 Azure Analysis Services 관리</span><span class="sxs-lookup"><span data-stu-id="b98f2-103">Manage Azure Analysis Services with PowerShell</span></span>

<span data-ttu-id="b98f2-104">이 문서에서는 PowerShell cmdlet 사용 tooperform Azure Analysis Services 서버 및 데이터베이스 관리 작업을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-104">This article describes PowerShell cmdlets used tooperform Azure Analysis Services server and database management tasks.</span></span> 

<span data-ttu-id="b98f2-105">서버 관리 작업 만들기 또는 서버를 삭제, 일시 중단 또는 서버 작업을 다시 시작 또는 변경 hello 서비스 수준 (계층)와 같은 Azure 리소스 관리자 (AzureRM) cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-105">Server management tasks such as creating or deleting a server, suspending or resuming server operations, or changing hello service level (tier) use Azure Resource Manager (AzureRM) cmdlets.</span></span> <span data-ttu-id="b98f2-106">다른 작업 추가 또는 역할 멤버를 제거, 처리 또는 cmdlet 사용 하 여 분할에 포함 된 같은 데이터베이스 관리를 위한 SQL Server Analysis Services와 동일한 sql Server 모듈을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-106">Other tasks for managing databases such as adding or removing role members, processing, or partitioning use cmdlets included in hello same SqlServer module as SQL Server Analysis Services.</span></span>

## <a name="permissions"></a><span data-ttu-id="b98f2-107">권한</span><span class="sxs-lookup"><span data-stu-id="b98f2-107">Permissions</span></span>
<span data-ttu-id="b98f2-108">대부분의 PowerShell 작업 관리 하는 hello Analysis Services 서버에 대 한 관리자 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-108">Most PowerShell tasks require you have Admin privileges on hello Analysis Services server you are managing.</span></span> <span data-ttu-id="b98f2-109">예약된 PowerShell 작업은 무인 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-109">Scheduled PowerShell tasks are unattended operations.</span></span> <span data-ttu-id="b98f2-110">hello 스케줄러를 실행 하는 hello 계정 hello Analysis Services 서버에는 관리자 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-110">hello account running hello scheduler must have Admin privileges on hello Analysis Services server.</span></span> 

<span data-ttu-id="b98f2-111">AzureRm cmdlet을 사용 하 여 서버 작업에 대 한 계정 또는 스케줄러를 실행 하는 hello 계정에 속해 있어야 hello 리소스에 대 한 소유자 역할 toohello [신속히 알아봅니다 액세스 제어 (RBAC)](../active-directory/role-based-access-control-what-is.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-111">For server operations using AzureRm cmdlets, your account or hello account running scheduler must also belong toohello Owner role for hello resource in [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> 

## <a name="server-operations"></a><span data-ttu-id="b98f2-112">서버 작업</span><span class="sxs-lookup"><span data-stu-id="b98f2-112">Server operations</span></span> 
<span data-ttu-id="b98f2-113">Azure Analysis Services cmdlet hello에 포함 된 [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) 모듈 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-113">Azure Analysis Services cmdlets are included in hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) component module.</span></span> <span data-ttu-id="b98f2-114">tooinstall AzureRM cmdlet 모듈 참조 [Azure 리소스 관리자 cmdlet](/powershell/azure/overview) hello PowerShell 갤러리에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-114">tooinstall AzureRM cmdlet modules, see [Azure Resource Manager cmdlets](/powershell/azure/overview) in hello PowerShell Gallery.</span></span>

|<span data-ttu-id="b98f2-115">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="b98f2-115">Cmdlet</span></span>|<span data-ttu-id="b98f2-116">설명</span><span class="sxs-lookup"><span data-stu-id="b98f2-116">Description</span></span>| 
|------------|-----------------| 
|[<span data-ttu-id="b98f2-117">Export-AzureAnalysisServicesInstance</span><span class="sxs-lookup"><span data-stu-id="b98f2-117">Export-AzureAnalysisServicesInstance</span></span>](/powershell/module/azurerm.analysisservices/export-azureanalysisservicesinstancelog)|<span data-ttu-id="b98f2-118">내보내기 로그 toofile입니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-118">Exports log toofile.</span></span>| 
|[<span data-ttu-id="b98f2-119">Get-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="b98f2-119">Get-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/get-azurermanalysisservicesserver)|<span data-ttu-id="b98f2-120">서버 인스턴스에 대한 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-120">Gets details of a server instance.</span></span>|  
|[<span data-ttu-id="b98f2-121">New-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="b98f2-121">New-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver)|<span data-ttu-id="b98f2-122">서버 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-122">Creates a server instance.</span></span>|
|[<span data-ttu-id="b98f2-123">Remove-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="b98f2-123">Remove-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/remove-azurermanalysisservicesserver)|<span data-ttu-id="b98f2-124">서버 인스턴스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-124">Removes a server instance.</span></span>|  
|[<span data-ttu-id="b98f2-125">Suspend-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="b98f2-125">Suspend-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/suspend-azurermanalysisservicesserver)|<span data-ttu-id="b98f2-126">서버 인스턴스를 일시 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-126">Suspends a server instance.</span></span>| 
|[<span data-ttu-id="b98f2-127">Resume-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="b98f2-127">Resume-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/resume-azurermanalysisservicesserver)|<span data-ttu-id="b98f2-128">서버 인스턴스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-128">Resumes a server instance.</span></span>|  
|[<span data-ttu-id="b98f2-129">Set-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="b98f2-129">Set-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/set-azurermanalysisservicesserver)|<span data-ttu-id="b98f2-130">서버 인스턴스를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-130">Modifies a server instance.</span></span>|   
|[<span data-ttu-id="b98f2-131">Test-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="b98f2-131">Test-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/test-azurermanalysisservicesserver)|<span data-ttu-id="b98f2-132">서버 인스턴스의 hello 존재 여부를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-132">Tests hello existence of a server  instance.</span></span>| 

## <a name="database-operations"></a><span data-ttu-id="b98f2-133">데이터베이스 작업</span><span class="sxs-lookup"><span data-stu-id="b98f2-133">Database operations</span></span>

<span data-ttu-id="b98f2-134">Azure Analysis Services를 사용 하 여 데이터베이스 작업 같은 hello [SqlServer](https://www.powershellgallery.com/packages/SqlServer) SQL Server Analysis Services와 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-134">Azure Analysis Services database operations use hello same [SqlServer](https://www.powershellgallery.com/packages/SqlServer) module as SQL Server Analysis Services.</span></span> <span data-ttu-id="b98f2-135">그러나 모든 cmdlet이 Azure Analysis Services에서 지원되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-135">However, not all cmdlets are supported for Azure Analysis Services.</span></span> 

<span data-ttu-id="b98f2-136">hello SqlServer 모듈 작업별 데이터베이스 관리 cmdlet는 TMSL Tabular Model Scripting Language ()를 허용 하는 hello 범용 Invoke-ascmd cmdlet 뿐만 아니라 쿼리 또는 스크립트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-136">hello SqlServer module provides task-specific database management cmdlets as well as hello general purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="b98f2-137">hello hello SqlServer 모듈의 다음 cmdlet은 지원 Azure Analysis Services에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-137">hello following cmdlets in hello SqlServer module are supported for Azure Analysis Services.</span></span>

  
|<span data-ttu-id="b98f2-138">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="b98f2-138">Cmdlet</span></span>|<span data-ttu-id="b98f2-139">설명</span><span class="sxs-lookup"><span data-stu-id="b98f2-139">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="b98f2-140">Add-RoleMember</span><span class="sxs-lookup"><span data-stu-id="b98f2-140">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="b98f2-141">Tooa 데이터베이스 역할 구성원을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-141">Add a member tooa database role.</span></span>| 
|[<span data-ttu-id="b98f2-142">Backup-ASDatabase</span><span class="sxs-lookup"><span data-stu-id="b98f2-142">Backup-ASDatabase</span></span>](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet)|<span data-ttu-id="b98f2-143">Analysis Services 데이터베이스를 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-143">Backup an Analysis Services database.</span></span>|  
|[<span data-ttu-id="b98f2-144">Remove-RoleMember</span><span class="sxs-lookup"><span data-stu-id="b98f2-144">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="b98f2-145">데이터베이스 역할에서 구성원을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-145">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="b98f2-146">Invoke-ASCmd</span><span class="sxs-lookup"><span data-stu-id="b98f2-146">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="b98f2-147">TMSL 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-147">Execute a TMSL script.</span></span>|
|[<span data-ttu-id="b98f2-148">Invoke-ProcessASDatabase</span><span class="sxs-lookup"><span data-stu-id="b98f2-148">Invoke-ProcessASDatabase</span></span>](https://msdn.microsoft.com/library/mt651773.aspx)|<span data-ttu-id="b98f2-149">데이터베이스를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-149">Process a database.</span></span>|  
|[<span data-ttu-id="b98f2-150">Invoke-ProcessPartition</span><span class="sxs-lookup"><span data-stu-id="b98f2-150">Invoke-ProcessPartition</span></span>](https://msdn.microsoft.com/library/hh510164.aspx)|<span data-ttu-id="b98f2-151">파티션을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-151">Process a partition.</span></span>| 
|[<span data-ttu-id="b98f2-152">Invoke-ProcessTable</span><span class="sxs-lookup"><span data-stu-id="b98f2-152">Invoke-ProcessTable</span></span>](https://msdn.microsoft.com/library/mt651774.aspx)|<span data-ttu-id="b98f2-153">테이블을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-153">Process a table.</span></span>|  
|[<span data-ttu-id="b98f2-154">Merge-Partition</span><span class="sxs-lookup"><span data-stu-id="b98f2-154">Merge-Partition</span></span>](https://msdn.microsoft.com/library/hh479576.aspx)|<span data-ttu-id="b98f2-155">파티션을 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-155">Merge a partition.</span></span>|  
|[<span data-ttu-id="b98f2-156">Restore-ASDatabase</span><span class="sxs-lookup"><span data-stu-id="b98f2-156">Restore-ASDatabase</span></span>](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet)|<span data-ttu-id="b98f2-157">Analysis Services 데이터베이스를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="b98f2-157">Restore an Analysis Services database.</span></span>| 
  

## <a name="related-information"></a><span data-ttu-id="b98f2-158">관련 정보</span><span class="sxs-lookup"><span data-stu-id="b98f2-158">Related information</span></span>

* [<span data-ttu-id="b98f2-159">SQL Server PowerShell 모듈 다운로드</span><span class="sxs-lookup"><span data-stu-id="b98f2-159">Download SQL Server PowerShell Module</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-ps-module)   
* [<span data-ttu-id="b98f2-160">SSMS 다운로드</span><span class="sxs-lookup"><span data-stu-id="b98f2-160">Download SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)   
* <span data-ttu-id="b98f2-161">[SqlServer module in PowerShell Gallery](https://www.powershellgallery.com/packages/SqlServer)(PowerShell 갤러리의 SqlServer 모듈)</span><span class="sxs-lookup"><span data-stu-id="b98f2-161">[SqlServer module in PowerShell Gallery](https://www.powershellgallery.com/packages/SqlServer)</span></span>    
* <span data-ttu-id="b98f2-162">[Tabular Model Programming for Compatibility Level 1200 and higher](https://msdn.microsoft.com/library/mt712541.aspx)(호환성 수준 1200 이상에 대한 테이블 형식 모델 프로그래밍)</span><span class="sxs-lookup"><span data-stu-id="b98f2-162">[Tabular Model Programming for Compatibility Level 1200 and higher](https://msdn.microsoft.com/library/mt712541.aspx)</span></span>

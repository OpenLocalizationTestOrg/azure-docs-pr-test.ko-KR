---
title: "PowerShell을 사용하여 Azure Analysis Services 관리 | Microsoft Docs"
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
ms.openlocfilehash: 95593053950f96a83e093c29516e9f66ebad53bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-analysis-services-with-powershell"></a><span data-ttu-id="399a6-103">PowerShell을 사용하여 Azure Analysis Services 관리</span><span class="sxs-lookup"><span data-stu-id="399a6-103">Manage Azure Analysis Services with PowerShell</span></span>

<span data-ttu-id="399a6-104">이 문서에서는 Azure Analysis Services 서버 및 데이터베이스 관리 작업을 수행하는 데 사용되는 PowerShell cmdlet에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-104">This article describes PowerShell cmdlets used to perform Azure Analysis Services server and database management tasks.</span></span> 

<span data-ttu-id="399a6-105">서버 만들기 또는 삭제, 서버 작업 일시 중단 또는 다시 시작 또는 서비스 수준(계층) 변경과 같은 서버 관리 작업은 AzureRM(Azure Resource Manager) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-105">Server management tasks such as creating or deleting a server, suspending or resuming server operations, or changing the service level (tier) use Azure Resource Manager (AzureRM) cmdlets.</span></span> <span data-ttu-id="399a6-106">역할 멤버 추가 또는 제거, 처리 또는 분할과 같은 기타 데이터베이스 관리 작업에서는 SQL Server Analysis Services와 동일한 SqlServer 모듈에 포함된 cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-106">Other tasks for managing databases such as adding or removing role members, processing, or partitioning use cmdlets included in the same SqlServer module as SQL Server Analysis Services.</span></span>

## <a name="permissions"></a><span data-ttu-id="399a6-107">권한</span><span class="sxs-lookup"><span data-stu-id="399a6-107">Permissions</span></span>
<span data-ttu-id="399a6-108">대부분의 PowerShell 작업에는 관리하는 Analysis Services 서버에 대해 관리자 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-108">Most PowerShell tasks require you have Admin privileges on the Analysis Services server you are managing.</span></span> <span data-ttu-id="399a6-109">예약된 PowerShell 작업은 무인 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-109">Scheduled PowerShell tasks are unattended operations.</span></span> <span data-ttu-id="399a6-110">스케줄러를 실행하는 계정에는 Analysis Services 서버에 대해 관리자 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-110">The account running the scheduler must have Admin privileges on the Analysis Services server.</span></span> 

<span data-ttu-id="399a6-111">AzureRm cmdlet을 사용하여 서버를 운영하려면 사용자의 계정 또는 스케줄러를 실행하는 계정이 [Azure 역할 기반 액세스 제어(RBAC)](../active-directory/role-based-access-control-what-is.md)의 리소스에 대한 소유자 역할에도 속해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-111">For server operations using AzureRm cmdlets, your account or the account running scheduler must also belong to the Owner role for the resource in [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> 

## <a name="server-operations"></a><span data-ttu-id="399a6-112">서버 작업</span><span class="sxs-lookup"><span data-stu-id="399a6-112">Server operations</span></span> 
<span data-ttu-id="399a6-113">Azure Analysis Services cmdlet은 [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) 구성 요소 모듈에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-113">Azure Analysis Services cmdlets are included in the [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) component module.</span></span> <span data-ttu-id="399a6-114">AzureRM cmdlet 모듈을 설치하려면 PowerShell 갤러리의 [Azure Resource Manager cmdlet](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="399a6-114">To install AzureRM cmdlet modules, see [Azure Resource Manager cmdlets](/powershell/azure/overview) in the PowerShell Gallery.</span></span>

|<span data-ttu-id="399a6-115">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="399a6-115">Cmdlet</span></span>|<span data-ttu-id="399a6-116">설명</span><span class="sxs-lookup"><span data-stu-id="399a6-116">Description</span></span>| 
|------------|-----------------| 
|[<span data-ttu-id="399a6-117">Export-AzureAnalysisServicesInstance</span><span class="sxs-lookup"><span data-stu-id="399a6-117">Export-AzureAnalysisServicesInstance</span></span>](/powershell/module/azurerm.analysisservices/export-azureanalysisservicesinstancelog)|<span data-ttu-id="399a6-118">로그를 파일에 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-118">Exports log to file.</span></span>| 
|[<span data-ttu-id="399a6-119">Get-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="399a6-119">Get-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/get-azurermanalysisservicesserver)|<span data-ttu-id="399a6-120">서버 인스턴스에 대한 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-120">Gets details of a server instance.</span></span>|  
|[<span data-ttu-id="399a6-121">New-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="399a6-121">New-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver)|<span data-ttu-id="399a6-122">서버 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-122">Creates a server instance.</span></span>|
|[<span data-ttu-id="399a6-123">Remove-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="399a6-123">Remove-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/remove-azurermanalysisservicesserver)|<span data-ttu-id="399a6-124">서버 인스턴스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-124">Removes a server instance.</span></span>|  
|[<span data-ttu-id="399a6-125">Suspend-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="399a6-125">Suspend-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/suspend-azurermanalysisservicesserver)|<span data-ttu-id="399a6-126">서버 인스턴스를 일시 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-126">Suspends a server instance.</span></span>| 
|[<span data-ttu-id="399a6-127">Resume-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="399a6-127">Resume-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/resume-azurermanalysisservicesserver)|<span data-ttu-id="399a6-128">서버 인스턴스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-128">Resumes a server instance.</span></span>|  
|[<span data-ttu-id="399a6-129">Set-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="399a6-129">Set-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/set-azurermanalysisservicesserver)|<span data-ttu-id="399a6-130">서버 인스턴스를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-130">Modifies a server instance.</span></span>|   
|[<span data-ttu-id="399a6-131">Test-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="399a6-131">Test-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/test-azurermanalysisservicesserver)|<span data-ttu-id="399a6-132">서버 인스턴스의 존재 여부를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-132">Tests the existence of a server  instance.</span></span>| 

## <a name="database-operations"></a><span data-ttu-id="399a6-133">데이터베이스 작업</span><span class="sxs-lookup"><span data-stu-id="399a6-133">Database operations</span></span>

<span data-ttu-id="399a6-134">Azure Analysis Services 데이터베이스 작업에서는 SQL Server Analysis Services와 동일한 [SqlServer](https://www.powershellgallery.com/packages/SqlServer) 모듈을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-134">Azure Analysis Services database operations use the same [SqlServer](https://www.powershellgallery.com/packages/SqlServer) module as SQL Server Analysis Services.</span></span> <span data-ttu-id="399a6-135">그러나 모든 cmdlet이 Azure Analysis Services에서 지원되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-135">However, not all cmdlets are supported for Azure Analysis Services.</span></span> 

<span data-ttu-id="399a6-136">SqlServer 모듈은 TMSL(테이블 형식 모델 스크립트 언어) 쿼리 또는 스크립트를 허용하는 범용 Invoke-ASCmd cmdlet뿐만 아니라 작업 관련 데이터베이스 관리 cmdlet도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-136">The SqlServer module provides task-specific database management cmdlets as well as the general purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="399a6-137">SqlServer 모듈의 다음 cmdlet은 Azure Analysis Services에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-137">The following cmdlets in the SqlServer module are supported for Azure Analysis Services.</span></span>

  
|<span data-ttu-id="399a6-138">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="399a6-138">Cmdlet</span></span>|<span data-ttu-id="399a6-139">설명</span><span class="sxs-lookup"><span data-stu-id="399a6-139">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="399a6-140">Add-RoleMember</span><span class="sxs-lookup"><span data-stu-id="399a6-140">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="399a6-141">데이터베이스 역할에 구성원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-141">Add a member to a database role.</span></span>| 
|[<span data-ttu-id="399a6-142">Backup-ASDatabase</span><span class="sxs-lookup"><span data-stu-id="399a6-142">Backup-ASDatabase</span></span>](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet)|<span data-ttu-id="399a6-143">Analysis Services 데이터베이스를 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-143">Backup an Analysis Services database.</span></span>|  
|[<span data-ttu-id="399a6-144">Remove-RoleMember</span><span class="sxs-lookup"><span data-stu-id="399a6-144">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="399a6-145">데이터베이스 역할에서 구성원을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-145">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="399a6-146">Invoke-ASCmd</span><span class="sxs-lookup"><span data-stu-id="399a6-146">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="399a6-147">TMSL 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-147">Execute a TMSL script.</span></span>|
|[<span data-ttu-id="399a6-148">Invoke-ProcessASDatabase</span><span class="sxs-lookup"><span data-stu-id="399a6-148">Invoke-ProcessASDatabase</span></span>](https://msdn.microsoft.com/library/mt651773.aspx)|<span data-ttu-id="399a6-149">데이터베이스를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-149">Process a database.</span></span>|  
|[<span data-ttu-id="399a6-150">Invoke-ProcessPartition</span><span class="sxs-lookup"><span data-stu-id="399a6-150">Invoke-ProcessPartition</span></span>](https://msdn.microsoft.com/library/hh510164.aspx)|<span data-ttu-id="399a6-151">파티션을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-151">Process a partition.</span></span>| 
|[<span data-ttu-id="399a6-152">Invoke-ProcessTable</span><span class="sxs-lookup"><span data-stu-id="399a6-152">Invoke-ProcessTable</span></span>](https://msdn.microsoft.com/library/mt651774.aspx)|<span data-ttu-id="399a6-153">테이블을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-153">Process a table.</span></span>|  
|[<span data-ttu-id="399a6-154">Merge-Partition</span><span class="sxs-lookup"><span data-stu-id="399a6-154">Merge-Partition</span></span>](https://msdn.microsoft.com/library/hh479576.aspx)|<span data-ttu-id="399a6-155">파티션을 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-155">Merge a partition.</span></span>|  
|[<span data-ttu-id="399a6-156">Restore-ASDatabase</span><span class="sxs-lookup"><span data-stu-id="399a6-156">Restore-ASDatabase</span></span>](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet)|<span data-ttu-id="399a6-157">Analysis Services 데이터베이스를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="399a6-157">Restore an Analysis Services database.</span></span>| 
  

## <a name="related-information"></a><span data-ttu-id="399a6-158">관련 정보</span><span class="sxs-lookup"><span data-stu-id="399a6-158">Related information</span></span>

* [<span data-ttu-id="399a6-159">SQL Server PowerShell 모듈 다운로드</span><span class="sxs-lookup"><span data-stu-id="399a6-159">Download SQL Server PowerShell Module</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-ps-module)   
* [<span data-ttu-id="399a6-160">SSMS 다운로드</span><span class="sxs-lookup"><span data-stu-id="399a6-160">Download SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)   
* <span data-ttu-id="399a6-161">[SqlServer module in PowerShell Gallery](https://www.powershellgallery.com/packages/SqlServer)(PowerShell 갤러리의 SqlServer 모듈)</span><span class="sxs-lookup"><span data-stu-id="399a6-161">[SqlServer module in PowerShell Gallery](https://www.powershellgallery.com/packages/SqlServer)</span></span>    
* <span data-ttu-id="399a6-162">[Tabular Model Programming for Compatibility Level 1200 and higher](https://msdn.microsoft.com/library/mt712541.aspx)(호환성 수준 1200 이상에 대한 테이블 형식 모델 프로그래밍)</span><span class="sxs-lookup"><span data-stu-id="399a6-162">[Tabular Model Programming for Compatibility Level 1200 and higher](https://msdn.microsoft.com/library/mt712541.aspx)</span></span>

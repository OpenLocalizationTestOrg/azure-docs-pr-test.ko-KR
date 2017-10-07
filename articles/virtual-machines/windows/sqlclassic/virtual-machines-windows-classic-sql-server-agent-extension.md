---
title: "SQL Vm (클래식)에서 관리 작업 aaaAutomate | Microsoft Docs"
description: "이 항목에서는 toomanage 특정 SQL Server 관리 작업을 자동화 하는 SQL Server 에이전트 확장과 hello 하는 방법을 설명 합니다. 여기에는 자동화된 백업, 자동화된 패치 적용 및 Azure 주요 자격 증명 모음 통합이 포함됩니다. 이 항목 hello 클래식 배포 모드를 사용합니다."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1dc011e0526845701eaf0c365007938f9ee32ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a><span data-ttu-id="277de-105">SQL Server 에이전트 확장 (클래식) hello로 Azure 가상 컴퓨터에서 관리 작업을 자동화</span><span class="sxs-lookup"><span data-stu-id="277de-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="277de-106">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="277de-106">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="277de-107">클래식</span><span class="sxs-lookup"><span data-stu-id="277de-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
>
 
<span data-ttu-id="277de-108">SQL Server IaaS 에이전트 확장 (SQLIaaSAgent) hello tooautomate 관리 작업을 Azure 가상 컴퓨터에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="277de-108">hello SQL Server IaaS Agent Extension (SQLIaaSAgent) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="277de-109">이 항목에서는 설치, 상태 및 제거 하기 위한 지침 뿐만 아니라 hello 확장에서 지 원하는 hello 서비스의 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="277de-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="277de-110">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="277de-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="277de-111">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="277de-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="277de-112">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="277de-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="277de-113">이 문서의 tooview hello 리소스 관리자 버전 참조 [SQL Server 에이전트 확장에 대 한 SQL Server Vm 리소스 관리자](../sql/virtual-machines-windows-sql-server-agent-extension.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="277de-113">tooview hello Resource Manager version of this article, see [SQL Server Agent Extension for SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="277de-114">지원되는 서비스</span><span class="sxs-lookup"><span data-stu-id="277de-114">Supported services</span></span>
<span data-ttu-id="277de-115">SQL Server IaaS 에이전트 확장 hello hello 다음 관리 작업을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="277de-115">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="277de-116">관리 기능</span><span class="sxs-lookup"><span data-stu-id="277de-116">Administration feature</span></span> | <span data-ttu-id="277de-117">설명</span><span class="sxs-lookup"><span data-stu-id="277de-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="277de-118">**SQL 자동화된 백업**</span><span class="sxs-lookup"><span data-stu-id="277de-118">**SQL Automated Backup**</span></span> |<span data-ttu-id="277de-119">Hello hello VM에서에서 SQL Server의 기본 인스턴스 hello에 대 한 모든 데이터베이스에 대 한 백업 예약을 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="277de-119">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="277de-120">자세한 내용은 [Azure 가상 컴퓨터에서 SQL Server에 대한 자동화된 백업(클래식)](../classic/sql-automated-backup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="277de-120">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-backup.md).</span></span> |
| <span data-ttu-id="277de-121">**SQL 자동화된 패치**</span><span class="sxs-lookup"><span data-stu-id="277de-121">**SQL Automated Patching**</span></span> |<span data-ttu-id="277de-122">작업에 대 한 사용량이 높은 시간 동안 업데이트를 방지할 수 있으므로 업데이트 중 VM이 지나야 tooyour도, 유지 관리 기간을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="277de-122">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="277de-123">자세한 내용은 [Azure 가상 컴퓨터에서 SQL Server에 대한 자동화된 패치(클래식)](../classic/sql-automated-patching.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="277de-123">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-patching.md).</span></span> |
| <span data-ttu-id="277de-124">**Azure Key Vault 통합**</span><span class="sxs-lookup"><span data-stu-id="277de-124">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="277de-125">Tooautomatically 있습니다 설치 하 고 SQL Server VM에 Azure 키 자격 증명 모음을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="277de-125">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="277de-126">자세한 내용은 [Azure VM에서 SQL Server에 대한 Azure 주요 자격 증명 모음 통합 구성(클래식)](../classic/ps-sql-keyvault.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="277de-126">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Classic)](../classic/ps-sql-keyvault.md).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="277de-127">필수 조건</span><span class="sxs-lookup"><span data-stu-id="277de-127">Prerequisites</span></span>
<span data-ttu-id="277de-128">VM에 SQL Server IaaS 에이전트 확장 toouse hello 요구 사항:</span><span class="sxs-lookup"><span data-stu-id="277de-128">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

### <a name="operating-system"></a><span data-ttu-id="277de-129">운영 체제:</span><span class="sxs-lookup"><span data-stu-id="277de-129">Operating System:</span></span>
* <span data-ttu-id="277de-130">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="277de-130">Windows Server 2012</span></span>
* <span data-ttu-id="277de-131">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="277de-131">Windows Server 2012 R2</span></span>
* <span data-ttu-id="277de-132">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="277de-132">Windows Server 2016</span></span>

### <a name="sql-server-versions"></a><span data-ttu-id="277de-133">SQL Server 버전:</span><span class="sxs-lookup"><span data-stu-id="277de-133">SQL Server versions:</span></span>
* <span data-ttu-id="277de-134">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="277de-134">SQL Server 2012</span></span>
* <span data-ttu-id="277de-135">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="277de-135">SQL Server 2014</span></span>
* <span data-ttu-id="277de-136">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="277de-136">SQL Server 2016</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="277de-137">Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="277de-137">Azure PowerShell:</span></span>
<span data-ttu-id="277de-138">[다운로드 하 고 hello 최신 Azure PowerShell 명령을 구성](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="277de-138">[Download and configure hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="277de-139">Windows PowerShell을 시작 하 고 hello로 tooyour Azure 구독을 연결 **Add-azureaccount** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="277de-139">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

    Add-AzureAccount

<span data-ttu-id="277de-140">여러 구독이 있는 경우 사용 하 여 **Select-azuresubscription** 대상에 포함 된 tooselect hello 구독 클래식 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="277de-140">If you have multiple subscriptions, use **Select-AzureSubscription** tooselect hello subscription that contains your target classic VM.</span></span>

    Select-AzureSubscription -SubscriptionName <subscriptionname>

<span data-ttu-id="277de-141">Hello 클래식 가상 컴퓨터 및 관련된 서비스 이름을 hello로의 목록을 가져올 수는 시점에서 **Get-azurevm** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="277de-141">At this point, you can get a list of hello classic virtual machines and their associated service names with hello **Get-AzureVM** command.</span></span>

    Get-AzureVM

## <a name="installation"></a><span data-ttu-id="277de-142">설치</span><span class="sxs-lookup"><span data-stu-id="277de-142">Installation</span></span>
<span data-ttu-id="277de-143">클래식 Vm에 대 한 PowerShell tooinstall hello SQL Server IaaS Agent 확장을 사용 하 고 이와 관련 된 서비스를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="277de-143">For classic VMs, you must use PowerShell tooinstall hello SQL Server IaaS Agent Extension and configure its associated services.</span></span> <span data-ttu-id="277de-144">사용 하 여 hello **집합 AzureVMSqlServerExtension** PowerShell cmdlet tooinstall hello 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="277de-144">Use hello **Set-AzureVMSqlServerExtension** PowerShell cmdlet tooinstall hello extension.</span></span> <span data-ttu-id="277de-145">예를 들어 다음 명령을 hello (클래식)는 Windows Server VM에 hello 확장을 설치 하 고 "SQLIaaSExtension" 라는 이름을 합니다.</span><span class="sxs-lookup"><span data-stu-id="277de-145">For example, hello following command installs hello extension on a Windows Server VM (classic) and names it "SQLIaaSExtension".</span></span>

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

<span data-ttu-id="277de-146">Toohello 최신 버전의 hello SQL IaaS Agent 확장을 업데이트 하는 경우 hello 확장을 업데이트 한 후 가상 컴퓨터를 다시 시작 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="277de-146">If you update toohello latest version of hello SQL IaaS Agent Extension, you must restart your virtual machine after updating hello extension.</span></span>

> [!NOTE]
> <span data-ttu-id="277de-147">클래식 가상 컴퓨터 옵션 tooinstall 없고 hello 포털을 통해 hello SQL IaaS Agent 확장을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="277de-147">Classic virtual machines do not have an option tooinstall and configure hello SQL IaaS Agent Extension through hello portal.</span></span>
> 
> 

## <a name="status"></a><span data-ttu-id="277de-148">가동 상태</span><span class="sxs-lookup"><span data-stu-id="277de-148">Status</span></span>
<span data-ttu-id="277de-149">Hello 확장이 설치 되는 한 가지 방법은 tooverify hello Azure 포털에서에서 tooview hello 에이전트 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="277de-149">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="277de-150">Hello 가상 컴퓨터 블레이드에 나열 된 가상 컴퓨터를 선택 하 고 클릭 한 다음 **확장**합니다.</span><span class="sxs-lookup"><span data-stu-id="277de-150">Select a virtual machine listed in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="277de-151">Hello 표시 되어야 **SQLIaaSAgent** 확장 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="277de-151">You should see hello **SQLIaaSAgent** extension listed.</span></span>

![Azure Portal의 SQL Server IaaS 에이전트 확장](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

<span data-ttu-id="277de-153">Hello를 사용할 수도 있습니다 **Get AzureVMSqlServerExtension** Azure Powershell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="277de-153">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a><span data-ttu-id="277de-154">제거</span><span class="sxs-lookup"><span data-stu-id="277de-154">Removal</span></span>
<span data-ttu-id="277de-155">Hello Azure 포털에서에서 hello에 hello 줄임표를 클릭 하 여 hello 확장을 제거할 수 있습니다 **확장** 가상 컴퓨터 속성의 블레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="277de-155">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="277de-156">그런 후 **제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="277de-156">Then click **Uninstall**.</span></span>

![Hello Azure 포털에서 SQL Server IaaS 에이전트 확장 제거](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="277de-158">Hello를 사용할 수도 있습니다 **제거 AzureVMSqlServerExtension** Powershell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="277de-158">You can also use hello **Remove-AzureVMSqlServerExtension** Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="277de-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="277de-159">Next Steps</span></span>
<span data-ttu-id="277de-160">Hello 확장 프로그램에서 지원 되는 hello 서비스 중 하나를 사용 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="277de-160">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="277de-161">자세한 내용은 hello에서 참조 한 hello 항목을 참조 하십시오. [서비스 지원](#supported-services) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="277de-161">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="277de-162">Azure 가상 컴퓨터의 SQL Server 실행에 대한 자세한 내용은 [Azure Virtual Machines의 SQL Server 개요](../sql/virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="277de-162">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>


---
title: "SQL VM에서 관리 작업 자동화(클래식) | Microsoft 문서"
description: "이 항목에서는 특정 SQL Server 관리 작업을 자동화하는 SQL Server 에이전트 확장을 관리하는 방법을 설명합니다. 여기에는 자동화된 백업, 자동화된 패치 및 Azure 주요 자격 증명 모음 통합이 포함됩니다. 이 항목에서는 클래식 배포 모드를 사용합니다."
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
ms.openlocfilehash: 30fa9128cd51a7498449c991b58500ad9acdd3d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-the-sql-server-agent-extension-classic"></a><span data-ttu-id="c031f-105">SQL Server 에이전트 확장을 사용하여 Azure Virtual Machines에서 관리 작업 자동화(클래식)</span><span class="sxs-lookup"><span data-stu-id="c031f-105">Automate management tasks on Azure Virtual Machines with the SQL Server Agent Extension (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c031f-106">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="c031f-106">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="c031f-107">클래식</span><span class="sxs-lookup"><span data-stu-id="c031f-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
>
 
<span data-ttu-id="c031f-108">관리 작업을 자동화하기 위해 Azure 가상 컴퓨터에서 SQL Server IaaS 에이전트 확장(SQLIaaSAgent)을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-108">The SQL Server IaaS Agent Extension (SQLIaaSAgent) runs on Azure virtual machines to automate administration tasks.</span></span> <span data-ttu-id="c031f-109">이 항목에서는 설치, 상태 및 제거에 대한 지침뿐만 아니라 확장에 의해 지원되는 서비스의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-109">This topic provides an overview of the services supported by the extension as well as instructions for installation, status, and removal.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="c031f-110">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c031f-111">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-111">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="c031f-112">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-112">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="c031f-113">이 문서의 Resource Manager 버전을 보려면 [SQL Server VM Resource Manager에 대한 SQL Server 에이전트 확장](../sql/virtual-machines-windows-sql-server-agent-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c031f-113">To view the Resource Manager version of this article, see [SQL Server Agent Extension for SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="c031f-114">지원되는 서비스</span><span class="sxs-lookup"><span data-stu-id="c031f-114">Supported services</span></span>
<span data-ttu-id="c031f-115">SQL Server IaaS 에이전트 확장은 다음 관리 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-115">The SQL Server IaaS Agent Extension supports the following administration tasks:</span></span>

| <span data-ttu-id="c031f-116">관리 기능</span><span class="sxs-lookup"><span data-stu-id="c031f-116">Administration feature</span></span> | <span data-ttu-id="c031f-117">설명</span><span class="sxs-lookup"><span data-stu-id="c031f-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c031f-118">**SQL 자동화된 백업**</span><span class="sxs-lookup"><span data-stu-id="c031f-118">**SQL Automated Backup**</span></span> |<span data-ttu-id="c031f-119">VM에 있는 SQL Server의 기본 인스턴스에 대한 모든 데이터베이스 백업 예약을 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-119">Automates the scheduling of backups for all databases for the default instance of SQL Server in the VM.</span></span> <span data-ttu-id="c031f-120">자세한 내용은 [Azure 가상 컴퓨터에서 SQL Server에 대한 자동화된 백업(클래식)](../classic/sql-automated-backup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c031f-120">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-backup.md).</span></span> |
| <span data-ttu-id="c031f-121">**SQL 자동화된 패치**</span><span class="sxs-lookup"><span data-stu-id="c031f-121">**SQL Automated Patching**</span></span> |<span data-ttu-id="c031f-122">워크로드가 가장 많은 시간에 업데이트하지 않도록 VM에 대한 업데이트가 수행될 유지 관리 기간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-122">Configures a maintenance window during which updates to your VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="c031f-123">자세한 내용은 [Azure 가상 컴퓨터에서 SQL Server에 대한 자동화된 패치(클래식)](../classic/sql-automated-patching.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c031f-123">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-patching.md).</span></span> |
| <span data-ttu-id="c031f-124">**Azure 주요 자격 증명 모음 통합**</span><span class="sxs-lookup"><span data-stu-id="c031f-124">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="c031f-125">SQL Server VM에서 Azure 주요 자격 증명 모음을 자동으로 설치하고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-125">Enables you to automatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="c031f-126">자세한 내용은 [Azure VM에서 SQL Server에 대한 Azure 주요 자격 증명 모음 통합 구성(클래식)](../classic/ps-sql-keyvault.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c031f-126">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Classic)](../classic/ps-sql-keyvault.md).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="c031f-127">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c031f-127">Prerequisites</span></span>
<span data-ttu-id="c031f-128">VM에서 SQL Server IaaS 에이전트 확장을 사용하기 위한 요구 사항:</span><span class="sxs-lookup"><span data-stu-id="c031f-128">Requirements to use the SQL Server IaaS Agent Extension on your VM:</span></span>

### <a name="operating-system"></a><span data-ttu-id="c031f-129">운영 체제:</span><span class="sxs-lookup"><span data-stu-id="c031f-129">Operating System:</span></span>
* <span data-ttu-id="c031f-130">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="c031f-130">Windows Server 2012</span></span>
* <span data-ttu-id="c031f-131">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="c031f-131">Windows Server 2012 R2</span></span>
* <span data-ttu-id="c031f-132">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c031f-132">Windows Server 2016</span></span>

### <a name="sql-server-versions"></a><span data-ttu-id="c031f-133">SQL Server 버전:</span><span class="sxs-lookup"><span data-stu-id="c031f-133">SQL Server versions:</span></span>
* <span data-ttu-id="c031f-134">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="c031f-134">SQL Server 2012</span></span>
* <span data-ttu-id="c031f-135">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="c031f-135">SQL Server 2014</span></span>
* <span data-ttu-id="c031f-136">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="c031f-136">SQL Server 2016</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="c031f-137">Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c031f-137">Azure PowerShell:</span></span>
<span data-ttu-id="c031f-138">[최신 Azure PowerShell 명령 다운로드 및 구성](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="c031f-138">[Download and configure the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="c031f-139">Windows PowerShell을 시작하고 **Add-AzureAccount** 명령을 사용하여 Azure 구독에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-139">Start Windows PowerShell, and connect it to your Azure subscription with the **Add-AzureAccount** command.</span></span>

    Add-AzureAccount

<span data-ttu-id="c031f-140">구독이 여러 개인 경우 **Select-AzureSubscription** 을 사용하여 대상 클래식 VM이 포함된 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-140">If you have multiple subscriptions, use **Select-AzureSubscription** to select the subscription that contains your target classic VM.</span></span>

    Select-AzureSubscription -SubscriptionName <subscriptionname>

<span data-ttu-id="c031f-141">이때 **Get-AzureVM** 명령을 사용하여 클래식 가상 컴퓨터 및 연결된 해당 서비스 이름 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-141">At this point, you can get a list of the classic virtual machines and their associated service names with the **Get-AzureVM** command.</span></span>

    Get-AzureVM

## <a name="installation"></a><span data-ttu-id="c031f-142">설치</span><span class="sxs-lookup"><span data-stu-id="c031f-142">Installation</span></span>
<span data-ttu-id="c031f-143">클래식 VM의 경우 PowerShell을 사용하여 SQL Server IaaS 에이전트 확장을 설치하고 관련 서비스를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-143">For classic VMs, you must use PowerShell to install the SQL Server IaaS Agent Extension and configure its associated services.</span></span> <span data-ttu-id="c031f-144">**Set-AzureVMSqlServerExtension** PowerShell cmdlet을 사용하여 확장을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-144">Use the **Set-AzureVMSqlServerExtension** PowerShell cmdlet to install the extension.</span></span> <span data-ttu-id="c031f-145">예를 들어 다음 명령은 Windows Server VM(클래식)에 확장을 설치한 후 "SQLIaaSExtension"이라고 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-145">For example, the following command installs the extension on a Windows Server VM (classic) and names it "SQLIaaSExtension".</span></span>

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

<span data-ttu-id="c031f-146">SQL IaaS 에이전트 확장의 최신 버전으로 업데이트하는 경우 확장을 업데이트한 후 가상 컴퓨터를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-146">If you update to the latest version of the SQL IaaS Agent Extension, you must restart your virtual machine after updating the extension.</span></span>

> [!NOTE]
> <span data-ttu-id="c031f-147">클래식 가상 컴퓨터에는 포털을 통해 SQL IaaS 에이전트 확장을 설치 및 구성하기 위한 옵션이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-147">Classic virtual machines do not have an option to install and configure the SQL IaaS Agent Extension through the portal.</span></span>
> 
> 

## <a name="status"></a><span data-ttu-id="c031f-148">가동 상태</span><span class="sxs-lookup"><span data-stu-id="c031f-148">Status</span></span>
<span data-ttu-id="c031f-149">확장이 설치되어 있는지 확인하는 한 가지 방법은 Azure 포털에서 에이전트 상태를 확인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-149">One way to verify that the extension is installed is to view the agent status in the Azure Portal.</span></span> <span data-ttu-id="c031f-150">가상 컴퓨터 블레이드에서 나열된 가상 컴퓨터를 선택하고 **확장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-150">Select a virtual machine listed in the virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="c031f-151">목록에 **SQLIaaSAgent** 확장이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-151">You should see the **SQLIaaSAgent** extension listed.</span></span>

![Azure 포털에서 SQL Server IaaS 에이전트 확장](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

<span data-ttu-id="c031f-153">**Get-AzureVMSqlServerExtension** Azure Powershell cmdlet을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-153">You can also use the **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a><span data-ttu-id="c031f-154">제거</span><span class="sxs-lookup"><span data-stu-id="c031f-154">Removal</span></span>
<span data-ttu-id="c031f-155">Azure 포털에서 가상 컴퓨터 속성의 **확장** 블레이드에서 줄임표를 클릭하여 확장을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-155">In the Azure Portal, you can uninstall the extension by clicking the ellipsis on the **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="c031f-156">그런 후 **제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-156">Then click **Uninstall**.</span></span>

![Azure 포털에서 SQL Server IaaS 에이전트 확장 제거](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="c031f-158">**Remove-AzureVMSqlServerExtension** Powershell cmdlet을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-158">You can also use the **Remove-AzureVMSqlServerExtension** Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="c031f-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c031f-159">Next Steps</span></span>
<span data-ttu-id="c031f-160">확장에 의해 지원되는 서비스 중 하나를 사용하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c031f-160">Begin using one of the services supported by the extension.</span></span> <span data-ttu-id="c031f-161">자세한 내용은 이 문서의 [지원되는 서비스](#supported-services) 섹션에 참조된 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c031f-161">For more details, see the topics referenced in the [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="c031f-162">Azure 가상 컴퓨터의 SQL Server 실행에 대한 자세한 내용은 [Azure Virtual Machines의 SQL Server 개요](../sql/virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c031f-162">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>


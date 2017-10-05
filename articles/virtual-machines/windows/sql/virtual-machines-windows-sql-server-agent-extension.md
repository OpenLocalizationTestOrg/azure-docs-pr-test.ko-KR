---
title: "SQL VM에서 관리 작업 자동화(Resource Manager) | Microsoft 문서"
description: "이 항목에서는 특정 SQL Server 관리 작업을 자동화하는 SQL Server 에이전트 확장을 관리하는 방법을 설명합니다. 여기에는 자동화된 백업, 자동화된 패치 적용 및 Azure 주요 자격 증명 모음 통합이 포함됩니다. 이 항목에서는 리소스 관리자 배포 모드를 사용합니다."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: effe4e2f-35b5-490a-b5ef-b06746083da4
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7152d184bb6d1d4b81aeb47e2c7c9160ada36023
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-the-sql-server-agent-extension-resource-manager"></a><span data-ttu-id="fe659-105">SQL Server 에이전트 확장을 사용하여 Azure Virtual Machines에서 관리 작업 자동화(Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="fe659-105">Automate management tasks on Azure Virtual Machines with the SQL Server Agent Extension (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe659-106">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="fe659-106">Resource Manager</span></span>](virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="fe659-107">클래식</span><span class="sxs-lookup"><span data-stu-id="fe659-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
> 

<span data-ttu-id="fe659-108">SQL Server IaaS 에이전트 확장(SQLIaaSExtension)은 관리 작업을 자동화하기 위해 Azure 가상 컴퓨터에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-108">The SQL Server IaaS Agent Extension (SQLIaaSExtension) runs on Azure virtual machines to automate administration tasks.</span></span> <span data-ttu-id="fe659-109">이 항목에서는 설치, 상태 및 제거에 대한 지침뿐만 아니라 확장에 의해 지원되는 서비스의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-109">This topic provides an overview of the services supported by the extension as well as instructions for installation, status, and removal.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="fe659-110">이 문서의 클래식 버전을 보려면 [SQL Server VM에 대한 SQL Server 에이전트 확장 클래식](../classic/sql-server-agent-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe659-110">To view the classic version of this article, see [SQL Server Agent Extension for SQL Server VMs Classic](../classic/sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="fe659-111">지원되는 서비스</span><span class="sxs-lookup"><span data-stu-id="fe659-111">Supported services</span></span>
<span data-ttu-id="fe659-112">SQL Server IaaS 에이전트 확장은 다음 관리 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-112">The SQL Server IaaS Agent Extension supports the following administration tasks:</span></span>

| <span data-ttu-id="fe659-113">관리 기능</span><span class="sxs-lookup"><span data-stu-id="fe659-113">Administration feature</span></span> | <span data-ttu-id="fe659-114">설명</span><span class="sxs-lookup"><span data-stu-id="fe659-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fe659-115">**SQL 자동화된 백업**</span><span class="sxs-lookup"><span data-stu-id="fe659-115">**SQL Automated Backup**</span></span> |<span data-ttu-id="fe659-116">VM에 있는 SQL Server의 기본 인스턴스에 대한 모든 데이터베이스 백업 예약을 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-116">Automates the scheduling of backups for all databases for the default instance of SQL Server in the VM.</span></span> <span data-ttu-id="fe659-117">자세한 내용은 [Azure Virtual Machines에서 SQL Server에 대한 자동화된 백업(리소스 관리자)](virtual-machines-windows-sql-automated-backup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe659-117">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span></span> |
| <span data-ttu-id="fe659-118">**SQL 자동화된 패치**</span><span class="sxs-lookup"><span data-stu-id="fe659-118">**SQL Automated Patching**</span></span> |<span data-ttu-id="fe659-119">워크로드가 가장 많은 시간에 업데이트하지 않도록 VM에 대한 업데이트가 수행될 유지 관리 기간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-119">Configures a maintenance window during which updates to your VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="fe659-120">자세한 내용은 [Azure Virtual Machines에서 SQL Server에 대한 자동화된 패치(리소스 관리자)](virtual-machines-windows-sql-automated-patching.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe659-120">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span></span> |
| <span data-ttu-id="fe659-121">**Azure 주요 자격 증명 모음 통합**</span><span class="sxs-lookup"><span data-stu-id="fe659-121">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="fe659-122">이 서비스를 통해 SQL Server VM에서 Azure Key Vault를 자동으로 설치 및 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-122">Enables you to automatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="fe659-123">자세한 내용은 [Azure VM에서 SQL Server에 대한 Azure Key Vault 통합 구성(리소스 매니저)](virtual-machines-windows-ps-sql-keyvault.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe659-123">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span></span> |

<span data-ttu-id="fe659-124">SQL Server IaaS 에이전트 확장을 설치하고 실행하면 Azure Portal, SQL Server Marketplace 이미지에 대한 Azure PowerShell, 확장 수동 설치를 위한 Azure PowerShell을 통해 가상 컴퓨터의 SQL Server 패널에서 이러한 관리 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-124">Once installed and running, the SQL Server IaaS Agent Extension makes these administration features available on the SQL Server panel of the virtual machine in the Azure Portal and through Azure PowerShell for SQL Server marketplace images, and through Azure PowerShell for manual installations of the extension.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fe659-125">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fe659-125">Prerequisites</span></span>
<span data-ttu-id="fe659-126">VM에서 SQL Server IaaS 에이전트 확장을 사용하기 위한 요구 사항:</span><span class="sxs-lookup"><span data-stu-id="fe659-126">Requirements to use the SQL Server IaaS Agent Extension on your VM:</span></span>

<span data-ttu-id="fe659-127">**운영 체제**:</span><span class="sxs-lookup"><span data-stu-id="fe659-127">**Operating System**:</span></span>

* <span data-ttu-id="fe659-128">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="fe659-128">Windows Server 2012</span></span>
* <span data-ttu-id="fe659-129">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="fe659-129">Windows Server 2012 R2</span></span>
* <span data-ttu-id="fe659-130">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="fe659-130">Windows Server 2016</span></span>

<span data-ttu-id="fe659-131">**SQL Server 버전**:</span><span class="sxs-lookup"><span data-stu-id="fe659-131">**SQL Server versions**:</span></span>

* <span data-ttu-id="fe659-132">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="fe659-132">SQL Server 2012</span></span>
* <span data-ttu-id="fe659-133">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="fe659-133">SQL Server 2014</span></span>
* <span data-ttu-id="fe659-134">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="fe659-134">SQL Server 2016</span></span>

<span data-ttu-id="fe659-135">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="fe659-135">**Azure PowerShell**:</span></span>

* [<span data-ttu-id="fe659-136">최신 Azure PowerShell 명령 다운로드 및 구성</span><span class="sxs-lookup"><span data-stu-id="fe659-136">Download and configure the latest Azure PowerShell commands</span></span>](/powershell/azure/overview)

## <a name="installation"></a><span data-ttu-id="fe659-137">설치</span><span class="sxs-lookup"><span data-stu-id="fe659-137">Installation</span></span>
<span data-ttu-id="fe659-138">SQL Server IaaS 에이전트 확장은 SQL Server 가상 컴퓨터 갤러리 이미지 중 하나를 프로비전할 때 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-138">The SQL Server IaaS Agent Extension is automatically installed when you provision one of the SQL Server virtual machine gallery images.</span></span> <span data-ttu-id="fe659-139">이러한 SQL Server VM 중 하나에서 확장을 수동으로 다시 설치해야 하는 경우 다음 PowerShell 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-139">If you need to reinstall the extension manually on one of these SQL Server VMs, use the following PowerShell command:</span></span>

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

<span data-ttu-id="fe659-140">OS 전용 Windows Server 가상 컴퓨터에 SQL Server IaaS 에이전트 확장을 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-140">It is also possible to install the SQL Server IaaS Agent Extension on an OS-only Windows Server virtual machine.</span></span> <span data-ttu-id="fe659-141">이러한 방식은 해당 컴퓨터에서 SQL Server를 수동으로 설치한 경우에만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-141">This is only supported if you have also manually installed SQL Server on that machine.</span></span> <span data-ttu-id="fe659-142">그런 후 동일한 **Set-AzureVMSqlServerExtension** PowerShell cmdlet을 사용하여 확장을 수동으로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-142">Then install the extension manually by using the same **Set-AzureVMSqlServerExtension** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="fe659-143">OS 전용 Windows Server VM에서 SQL Server IaaS 에이전트 확장을 수동으로 설치하는 경우 Azure Portal을 통해 SQL Server 구성 설정을 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-143">If you manually install the SQL Server IaaS Agent Extension on an OS-only Windows Server VM, you can not manage the SQL Server configuration settings through the Azure portal.</span></span> <span data-ttu-id="fe659-144">이 시나리오에서는 모든 변경 작업을 PowerShell로 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-144">In this scenario, you must make all changes with PowerShell.</span></span>

## <a name="status"></a><span data-ttu-id="fe659-145">가동 상태</span><span class="sxs-lookup"><span data-stu-id="fe659-145">Status</span></span>
<span data-ttu-id="fe659-146">확장이 설치되어 있는지 확인하는 한 가지 방법은 Azure Portal에서 에이전트 상태를 확인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-146">One way to verify that the extension is installed is to view the agent status in the Azure Portal.</span></span> <span data-ttu-id="fe659-147">가상 컴퓨터 블레이드에서 **모든 설정**을 선택하고 **확장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-147">Select **All settings** in the virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="fe659-148">**SQLIaaSExtension** 확장이 나열되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-148">You should see the **SQLIaaSExtension** extension listed.</span></span>

![Azure Portal의 SQL Server IaaS 에이전트 확장](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

<span data-ttu-id="fe659-150">**Get-AzureVMSqlServerExtension** Azure Powershell cmdlet을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-150">You can also use the **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

<span data-ttu-id="fe659-151">이전 명령은 에이전트가 설치되어 있는지 확인하고 일반적인 상태 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-151">The previous command confirms the agent is installed and provides general status information.</span></span> <span data-ttu-id="fe659-152">다음 명령을 사용하여 자동화된 백업 및 패치에 대한 특정 상태 정보를 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-152">You can also get specific status information about Automated Backup and Patching with the following commands.</span></span>

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a><span data-ttu-id="fe659-153">제거</span><span class="sxs-lookup"><span data-stu-id="fe659-153">Removal</span></span>
<span data-ttu-id="fe659-154">Azure Portal에서 가상 컴퓨터 속성의 **확장** 블레이드에서 줄임표를 클릭하여 확장을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-154">In the Azure Portal, you can uninstall the extension by clicking the ellipsis on the **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="fe659-155">그런 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-155">Then click **Delete**.</span></span>

![Azure Portal에서 SQL Server IaaS 에이전트 확장 제거](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="fe659-157">**Remove-AzureRmVMSqlServerExtension** Powershell cmdlet을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-157">You can also use the **Remove-AzureRmVMSqlServerExtension** Powershell cmdlet.</span></span>

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a><span data-ttu-id="fe659-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fe659-158">Next Steps</span></span>
<span data-ttu-id="fe659-159">확장에 의해 지원되는 서비스 중 하나를 사용하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fe659-159">Begin using one of the services supported by the extension.</span></span> <span data-ttu-id="fe659-160">자세한 내용은 이 문서의 [지원되는 서비스](#supported-services) 섹션에 참조된 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe659-160">For more details, see the topics referenced in the [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="fe659-161">Azure 가상 컴퓨터의 SQL Server 실행에 대한 자세한 내용은 [Azure Virtual Machines의 SQL Server 개요](virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe659-161">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>


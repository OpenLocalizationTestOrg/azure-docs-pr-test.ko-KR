---
title: "SQL Vm (리소스 관리자)에서 관리 작업 aaaAutomate | Microsoft Docs"
description: "이 항목에서는 toomanage 특정 SQL Server 관리 작업을 자동화 하는 SQL Server 에이전트 확장과 hello 하는 방법을 설명 합니다. 여기에는 자동화된 백업, 자동화된 패치 적용 및 Azure 주요 자격 증명 모음 통합이 포함됩니다. 이 항목에서는 hello 리소스 관리자 배포 모드를 사용 합니다."
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
ms.openlocfilehash: ae917612c4af59f12c0b083440673bdc555e9d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-resource-manager"></a><span data-ttu-id="a7dc0-105">Hello SQL Server 에이전트 확장 (리소스 관리자)가 있는 Azure 가상 컴퓨터에서 관리 작업을 자동화</span><span class="sxs-lookup"><span data-stu-id="a7dc0-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a7dc0-106">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="a7dc0-106">Resource Manager</span></span>](virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="a7dc0-107">클래식</span><span class="sxs-lookup"><span data-stu-id="a7dc0-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
> 

<span data-ttu-id="a7dc0-108">SQL Server IaaS 에이전트 확장 (SQLIaaSExtension) hello tooautomate 관리 작업을 Azure 가상 컴퓨터에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-108">hello SQL Server IaaS Agent Extension (SQLIaaSExtension) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="a7dc0-109">이 항목에서는 설치, 상태 및 제거 하기 위한 지침 뿐만 아니라 hello 확장에서 지 원하는 hello 서비스의 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="a7dc0-110">이 문서의 tooview hello 클래식 버전 참조 [SQL Server 클래식 Vm에 대 한 SQL Server 에이전트 확장](../classic/sql-server-agent-extension.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-110">tooview hello classic version of this article, see [SQL Server Agent Extension for SQL Server VMs Classic](../classic/sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="a7dc0-111">지원되는 서비스</span><span class="sxs-lookup"><span data-stu-id="a7dc0-111">Supported services</span></span>
<span data-ttu-id="a7dc0-112">SQL Server IaaS 에이전트 확장 hello hello 다음 관리 작업을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-112">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="a7dc0-113">관리 기능</span><span class="sxs-lookup"><span data-stu-id="a7dc0-113">Administration feature</span></span> | <span data-ttu-id="a7dc0-114">설명</span><span class="sxs-lookup"><span data-stu-id="a7dc0-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a7dc0-115">**SQL 자동화된 백업**</span><span class="sxs-lookup"><span data-stu-id="a7dc0-115">**SQL Automated Backup**</span></span> |<span data-ttu-id="a7dc0-116">Hello hello VM에서에서 SQL Server의 기본 인스턴스 hello에 대 한 모든 데이터베이스에 대 한 백업 예약을 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-116">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="a7dc0-117">자세한 내용은 [Azure Virtual Machines에서 SQL Server에 대한 자동화된 백업(리소스 관리자)](virtual-machines-windows-sql-automated-backup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-117">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span></span> |
| <span data-ttu-id="a7dc0-118">**SQL 자동화된 패치**</span><span class="sxs-lookup"><span data-stu-id="a7dc0-118">**SQL Automated Patching**</span></span> |<span data-ttu-id="a7dc0-119">작업에 대 한 사용량이 높은 시간 동안 업데이트를 방지할 수 있으므로 업데이트 중 VM이 지나야 tooyour도, 유지 관리 기간을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-119">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="a7dc0-120">자세한 내용은 [Azure Virtual Machines에서 SQL Server에 대한 자동화된 패치(리소스 관리자)](virtual-machines-windows-sql-automated-patching.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-120">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span></span> |
| <span data-ttu-id="a7dc0-121">**Azure Key Vault 통합**</span><span class="sxs-lookup"><span data-stu-id="a7dc0-121">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="a7dc0-122">Tooautomatically 있습니다 설치 하 고 SQL Server VM에 Azure 키 자격 증명 모음을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-122">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="a7dc0-123">자세한 내용은 [Azure VM에서 SQL Server에 대한 Azure Key Vault 통합 구성(리소스 매니저)](virtual-machines-windows-ps-sql-keyvault.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-123">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span></span> |

<span data-ttu-id="a7dc0-124">설치 하 고 실행 되 면 hello SQL Server IaaS 에이전트 확장 하면 이러한 관리 기능에서 사용할 수 hello 가상 컴퓨터의 hello Azure 포털 및 Azure PowerShell을 통해 SQL Server 마켓플레이스 이미지에 대 한 및 통해 hello SQL Server 패널 Hello 확장의 수동 설치에 대 한 azure PowerShell입니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-124">Once installed and running, hello SQL Server IaaS Agent Extension makes these administration features available on hello SQL Server panel of hello virtual machine in hello Azure Portal and through Azure PowerShell for SQL Server marketplace images, and through Azure PowerShell for manual installations of hello extension.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a7dc0-125">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a7dc0-125">Prerequisites</span></span>
<span data-ttu-id="a7dc0-126">VM에 SQL Server IaaS 에이전트 확장 toouse hello 요구 사항:</span><span class="sxs-lookup"><span data-stu-id="a7dc0-126">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

<span data-ttu-id="a7dc0-127">**운영 체제**:</span><span class="sxs-lookup"><span data-stu-id="a7dc0-127">**Operating System**:</span></span>

* <span data-ttu-id="a7dc0-128">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="a7dc0-128">Windows Server 2012</span></span>
* <span data-ttu-id="a7dc0-129">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="a7dc0-129">Windows Server 2012 R2</span></span>
* <span data-ttu-id="a7dc0-130">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="a7dc0-130">Windows Server 2016</span></span>

<span data-ttu-id="a7dc0-131">**SQL Server 버전**:</span><span class="sxs-lookup"><span data-stu-id="a7dc0-131">**SQL Server versions**:</span></span>

* <span data-ttu-id="a7dc0-132">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="a7dc0-132">SQL Server 2012</span></span>
* <span data-ttu-id="a7dc0-133">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="a7dc0-133">SQL Server 2014</span></span>
* <span data-ttu-id="a7dc0-134">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="a7dc0-134">SQL Server 2016</span></span>

<span data-ttu-id="a7dc0-135">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="a7dc0-135">**Azure PowerShell**:</span></span>

* [<span data-ttu-id="a7dc0-136">다운로드 하 고 hello 최신 Azure PowerShell 명령 구성</span><span class="sxs-lookup"><span data-stu-id="a7dc0-136">Download and configure hello latest Azure PowerShell commands</span></span>](/powershell/azure/overview)

## <a name="installation"></a><span data-ttu-id="a7dc0-137">설치</span><span class="sxs-lookup"><span data-stu-id="a7dc0-137">Installation</span></span>
<span data-ttu-id="a7dc0-138">SQL Server IaaS 에이전트 확장 hello는 hello SQL Server 가상 컴퓨터 갤러리 이미지 중 하나로 프로 비전 할 때 자동으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-138">hello SQL Server IaaS Agent Extension is automatically installed when you provision one of hello SQL Server virtual machine gallery images.</span></span> <span data-ttu-id="a7dc0-139">이러한 SQL Server Vm 중 하나에서 수동으로 tooreinstall hello 확장 해야 할 경우 다음 PowerShell 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-139">If you need tooreinstall hello extension manually on one of these SQL Server VMs, use hello following PowerShell command:</span></span>

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

<span data-ttu-id="a7dc0-140">Windows Server 운영 체제 전용 가상 컴퓨터에서 SQL Server IaaS 에이전트 확장 가능한 tooinstall hello 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-140">It is also possible tooinstall hello SQL Server IaaS Agent Extension on an OS-only Windows Server virtual machine.</span></span> <span data-ttu-id="a7dc0-141">이러한 방식은 해당 컴퓨터에서 SQL Server를 수동으로 설치한 경우에만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-141">This is only supported if you have also manually installed SQL Server on that machine.</span></span> <span data-ttu-id="a7dc0-142">사용 하 여 수동으로 설치 hello 확장 hello 동일 다음 **집합 AzureVMSqlServerExtension** PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-142">Then install hello extension manually by using hello same **Set-AzureVMSqlServerExtension** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="a7dc0-143">운영 체제 전용 Windows Server VM에서 SQL Server IaaS 에이전트 확장 hello 수동으로 설치한 경우 하지 hello Azure 포털을 통해 hello SQL Server 구성 설정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-143">If you manually install hello SQL Server IaaS Agent Extension on an OS-only Windows Server VM, you can not manage hello SQL Server configuration settings through hello Azure portal.</span></span> <span data-ttu-id="a7dc0-144">이 시나리오에서는 모든 변경 작업을 PowerShell로 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-144">In this scenario, you must make all changes with PowerShell.</span></span>

## <a name="status"></a><span data-ttu-id="a7dc0-145">가동 상태</span><span class="sxs-lookup"><span data-stu-id="a7dc0-145">Status</span></span>
<span data-ttu-id="a7dc0-146">Hello 확장이 설치 되는 한 가지 방법은 tooverify hello Azure 포털에서에서 tooview hello 에이전트 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-146">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="a7dc0-147">선택 **모든 설정을** 에서 가상 컴퓨터 블레이드 hello 하 고 클릭 한 다음 **확장**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-147">Select **All settings** in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="a7dc0-148">Hello 표시 되어야 **SQLIaaSExtension** 확장 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-148">You should see hello **SQLIaaSExtension** extension listed.</span></span>

![Azure Portal의 SQL Server IaaS 에이전트 확장](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

<span data-ttu-id="a7dc0-150">Hello를 사용할 수도 있습니다 **Get AzureVMSqlServerExtension** Azure Powershell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-150">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

<span data-ttu-id="a7dc0-151">hello 이전 명령은 hello 에이전트가 설치 되 고 일반적인 상태 정보를 제공 합니다. 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-151">hello previous command confirms hello agent is installed and provides general status information.</span></span> <span data-ttu-id="a7dc0-152">또한 다음 명령을 hello로 자동화 된 백업 및 패치 적용 하는 방법에 대 한 특정 상태 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-152">You can also get specific status information about Automated Backup and Patching with hello following commands.</span></span>

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a><span data-ttu-id="a7dc0-153">제거</span><span class="sxs-lookup"><span data-stu-id="a7dc0-153">Removal</span></span>
<span data-ttu-id="a7dc0-154">Hello Azure 포털에서에서 hello에 hello 줄임표를 클릭 하 여 hello 확장을 제거할 수 있습니다 **확장** 가상 컴퓨터 속성의 블레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-154">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="a7dc0-155">그런 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-155">Then click **Delete**.</span></span>

![Hello Azure 포털에서 SQL Server IaaS 에이전트 확장 제거](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="a7dc0-157">Hello를 사용할 수도 있습니다 **제거 AzureRmVMSqlServerExtension** Powershell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-157">You can also use hello **Remove-AzureRmVMSqlServerExtension** Powershell cmdlet.</span></span>

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a><span data-ttu-id="a7dc0-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a7dc0-158">Next Steps</span></span>
<span data-ttu-id="a7dc0-159">Hello 확장 프로그램에서 지원 되는 hello 서비스 중 하나를 사용 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-159">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="a7dc0-160">자세한 내용은 hello에서 참조 한 hello 항목을 참조 하십시오. [서비스 지원](#supported-services) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-160">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="a7dc0-161">Azure 가상 컴퓨터의 SQL Server 실행에 대한 자세한 내용은 [Azure Virtual Machines의 SQL Server 개요](virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7dc0-161">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>


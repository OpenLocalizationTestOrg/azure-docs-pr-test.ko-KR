---
title: "SQL Server VM에 대한 자동화된 패치(리소스 관리자) | Microsoft Docs"
description: "리소스 관리자를 사용하여 Azure에서 실행 중인 SQL Server 가상 컴퓨터에 대한 자동화된 패치 기능에 대해 설명합니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 58232e92-318f-456b-8f0a-2201a541e08d
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 7d501ab45a85010a8dbfd6135d77f18f1743354e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a><span data-ttu-id="3ad89-103">Azure 가상 컴퓨터에서 SQL Server의 자동화된 패치(리소스 관리자)</span><span class="sxs-lookup"><span data-stu-id="3ad89-103">Automated Patching for SQL Server in Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ad89-104">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="3ad89-104">Resource Manager</span></span>](virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="3ad89-105">클래식</span><span class="sxs-lookup"><span data-stu-id="3ad89-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="3ad89-106">자동화된 패치는 SQL Server를 실행하는 Azure 가상 컴퓨터에 대한 유지 관리 기간을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="3ad89-107">이 유지 관리 기간 동안만 자동화된 업데이트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="3ad89-108">SQL Server의 경우 이러한 제한을 통해 시스템 업데이트 및 관련 재시작 작업이 데이터베이스에 대해 가장 적절한 시간에 수행되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-108">For SQL Server, this rescriction ensures that system updates and any associated restarts occur at the best possible time for the database.</span></span> <span data-ttu-id="3ad89-109">자동화된 패치는 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-109">Automated Patching depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="3ad89-110">이 문서의 클래식 버전을 보려면 [Azure Virtual Machines에서 SQL Server의 자동화된 패치(클래식)](../classic/sql-automated-patching.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ad89-110">To view the classic version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Classic](../classic/sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ad89-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3ad89-111">Prerequisites</span></span>
<span data-ttu-id="3ad89-112">자동화된 패치를 사용하려면 다음 필수 조건을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="3ad89-112">To use Automated Patching, consider the following prerequisites:</span></span>

<span data-ttu-id="3ad89-113">**운영 체제**:</span><span class="sxs-lookup"><span data-stu-id="3ad89-113">**Operating System**:</span></span>

* <span data-ttu-id="3ad89-114">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="3ad89-114">Windows Server 2012</span></span>
* <span data-ttu-id="3ad89-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3ad89-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="3ad89-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="3ad89-116">Windows Server 2016</span></span>

<span data-ttu-id="3ad89-117">**SQL Server 버전**:</span><span class="sxs-lookup"><span data-stu-id="3ad89-117">**SQL Server version**:</span></span>

* <span data-ttu-id="3ad89-118">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="3ad89-118">SQL Server 2012</span></span>
* <span data-ttu-id="3ad89-119">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="3ad89-119">SQL Server 2014</span></span>
* <span data-ttu-id="3ad89-120">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="3ad89-120">SQL Server 2016</span></span>

<span data-ttu-id="3ad89-121">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="3ad89-121">**Azure PowerShell**:</span></span>

* <span data-ttu-id="3ad89-122">[최신 Azure PowerShell 명령을 설치합니다](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="3ad89-122">[Install the latest Azure PowerShell commands](/powershell/azure/overview) if you plan to configure Automated Patching with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="3ad89-123">자동화된 패치는 SQL Server IaaS 에이전트 확장에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-123">Automated Patching relies on the SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="3ad89-124">현재 SQL 가상 컴퓨터 갤러리 이미지는 기본적으로 이 확장을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-124">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="3ad89-125">자세한 내용은 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ad89-125">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>
> 
> 

## <a name="settings"></a><span data-ttu-id="3ad89-126">설정</span><span class="sxs-lookup"><span data-stu-id="3ad89-126">Settings</span></span>
<span data-ttu-id="3ad89-127">다음 표에서는 자동화된 패치에 대해 구성할 수 있는 옵션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-127">The following table describes the options that can be configured for Automated Patching.</span></span> <span data-ttu-id="3ad89-128">실제 구성 단계는 Azure 포털 또는 Azure Windows PowerShell 명령 사용 여부에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-128">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="3ad89-129">설정</span><span class="sxs-lookup"><span data-stu-id="3ad89-129">Setting</span></span> | <span data-ttu-id="3ad89-130">가능한 값</span><span class="sxs-lookup"><span data-stu-id="3ad89-130">Possible values</span></span> | <span data-ttu-id="3ad89-131">설명</span><span class="sxs-lookup"><span data-stu-id="3ad89-131">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3ad89-132">**자동화된 패치**</span><span class="sxs-lookup"><span data-stu-id="3ad89-132">**Automated Patching**</span></span> |<span data-ttu-id="3ad89-133">사용/사용 안 함(사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="3ad89-133">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="3ad89-134">Azure 가상 컴퓨터에 대한 자동화된 패치를 사용 또는 사용 안 함으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-134">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="3ad89-135">**유지 관리 일정**</span><span class="sxs-lookup"><span data-stu-id="3ad89-135">**Maintenance schedule**</span></span> |<span data-ttu-id="3ad89-136">매일, 월요일, 화요일, 수요일, 목요일, 금요일, 토요일, 일요일</span><span class="sxs-lookup"><span data-stu-id="3ad89-136">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="3ad89-137">가상 컴퓨터에 대한 Windows, SQL Server 및 Microsoft 업데이트 다운로드 및 설치에 대한 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-137">The schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="3ad89-138">**유지 관리 시작 시간**</span><span class="sxs-lookup"><span data-stu-id="3ad89-138">**Maintenance start hour**</span></span> |<span data-ttu-id="3ad89-139">0-24</span><span class="sxs-lookup"><span data-stu-id="3ad89-139">0-24</span></span> |<span data-ttu-id="3ad89-140">가상 컴퓨터를 업데이트할 로컬 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-140">The local start time to update the virtual machine.</span></span> |
| <span data-ttu-id="3ad89-141">**유지 관리 기간**</span><span class="sxs-lookup"><span data-stu-id="3ad89-141">**Maintenance window duration**</span></span> |<span data-ttu-id="3ad89-142">30-180</span><span class="sxs-lookup"><span data-stu-id="3ad89-142">30-180</span></span> |<span data-ttu-id="3ad89-143">업데이트 다운로드 및 설치를 완료하는데 허용된 시간(분)입니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-143">The number of minutes permitted to complete the download and installation of updates.</span></span> |
| <span data-ttu-id="3ad89-144">**패치 범주**</span><span class="sxs-lookup"><span data-stu-id="3ad89-144">**Patch Category**</span></span> |<span data-ttu-id="3ad89-145">중요</span><span class="sxs-lookup"><span data-stu-id="3ad89-145">Important</span></span> |<span data-ttu-id="3ad89-146">다운로드 및 설치할 업데이트의 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-146">The category of updates to download and install.</span></span> |

## <a name="configuration-in-the-portal"></a><span data-ttu-id="3ad89-147">포털에서 구성</span><span class="sxs-lookup"><span data-stu-id="3ad89-147">Configuration in the Portal</span></span>
<span data-ttu-id="3ad89-148">Azure 포털을 사용하여 프로비전 중에 또는 기존 VM에 대해 자동화된 패치를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-148">You can use the Azure portal to configure Automated Patching during provisioning or for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="3ad89-149">새 VM</span><span class="sxs-lookup"><span data-stu-id="3ad89-149">New VMs</span></span>
<span data-ttu-id="3ad89-150">Azure 포털을 사용하여 Resource Manager 배포 모델에서 새 SQL Server 가상 컴퓨터를 만들 때 자동화된 패치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-150">Use the Azure portal to configure Automated Patching when you create a new SQL Server Virtual Machine in the Resource Manager deployment model.</span></span>

<span data-ttu-id="3ad89-151">**SQL Server 설정** 블레이드에서 **자동화된 패치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-151">In the **SQL Server settings** blade, select **Automated patching**.</span></span> <span data-ttu-id="3ad89-152">다음 Azure 포털 스크린샷은 **SQL 자동화된 패치** 블레이드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-152">The following Azure portal screenshot shows the **SQL Automated Patching** blade.</span></span>

![Azure 포털에서 SQL 자동화된 패치](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

<span data-ttu-id="3ad89-154">컨텍스트의 경우 [Azure에서 SQL Server 가상 컴퓨터 프로비전](virtual-machines-windows-portal-sql-server-provision.md)의 전체 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ad89-154">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="3ad89-155">기존 VM</span><span class="sxs-lookup"><span data-stu-id="3ad89-155">Existing VMs</span></span>
<span data-ttu-id="3ad89-156">기존 SQL Server 가상 컴퓨터에 대한 해당 SQL Server 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-156">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="3ad89-157">그런 다음 **설정** 블레이드의 **SQL Server 구성** 섹션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-157">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![기존 VM에 대한 SQL 자동 패치](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

<span data-ttu-id="3ad89-159">**SQL Server 구성** 블레이드에서 자동화된 패치 섹션의 **편집** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-159">In the **SQL Server configuration** blade, click the **Edit** button in the Automated patching section.</span></span>

![기존 VM에 대한 SQL 자동 패치 구성](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

<span data-ttu-id="3ad89-161">완료되면 **SQL Server 구성** 블레이드 아래쪽의 **확인** 단추를 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-161">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

<span data-ttu-id="3ad89-162">처음으로 자동화된 패치를 사용 설정할 경우 Azure에서 백그라운드로 SQL Server IaaS 에이전트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-162">If you are enabling Automated Patching for the first time, Azure configures the SQL Server IaaS Agent in the background.</span></span> <span data-ttu-id="3ad89-163">이 시간 동안에는 구성된 자동화된 패치가 Azure 포털에 표시되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-163">During this time, the Azure portal might not show that Automated Patching is configured.</span></span> <span data-ttu-id="3ad89-164">에이전트가 설치 및 구성될 때까지 몇 분 정도 기다리세요.</span><span class="sxs-lookup"><span data-stu-id="3ad89-164">Wait several minutes for the agent to be installed, configured.</span></span> <span data-ttu-id="3ad89-165">그 후 Azure 포털에는 새 설정이 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-165">After that the Azure portal reflects the new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="3ad89-166">또한 템플릿을 사용하여 자동화된 패치를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-166">You can also configure Automated Patching using a template.</span></span> <span data-ttu-id="3ad89-167">자세한 내용은 [자동화된 패치에 대한 Azure 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ad89-167">For more information, see [Azure quickstart template for Automated Patching](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span></span>
> 
> 

## <a name="configuration-with-powershell"></a><span data-ttu-id="3ad89-168">PowerShell을 사용하여 구성</span><span class="sxs-lookup"><span data-stu-id="3ad89-168">Configuration with PowerShell</span></span>
<span data-ttu-id="3ad89-169">SQL VM을 프로비전한 후 PowerShell을 사용하여 자동화된 패치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-169">After provisioning your SQL VM, use PowerShell to configure Automated Patching.</span></span>

<span data-ttu-id="3ad89-170">다음 예제에서는 PowerShell을 사용하여 기존 SQL Server VM에 대해 자동화된 패치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-170">In the following example, PowerShell is used to configure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="3ad89-171">**AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** 명령은 자동 업데이트에 대한 새 유지 관리 기간을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-171">The **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

<span data-ttu-id="3ad89-172">이 예제를 바탕으로 다음 표에서는 대상 Azure VM에 미치는 실질적인 영향을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-172">Based on this example, the following table describes the practical effect on the target Azure VM:</span></span>

| <span data-ttu-id="3ad89-173">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3ad89-173">Parameter</span></span> | <span data-ttu-id="3ad89-174">결과</span><span class="sxs-lookup"><span data-stu-id="3ad89-174">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="3ad89-175">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="3ad89-175">**DayOfWeek**</span></span> |<span data-ttu-id="3ad89-176">매주 목요일마다 패치가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-176">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="3ad89-177">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="3ad89-177">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="3ad89-178">오전 11시에 업데이트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-178">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="3ad89-179">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="3ad89-179">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="3ad89-180">120분 이내에 패치를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-180">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="3ad89-181">시작 시간을 기준으로 오후 1시까지 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-181">Based on the start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="3ad89-182">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="3ad89-182">**PatchCategory**</span></span> |<span data-ttu-id="3ad89-183">이 매개 변수에 대해서는 **중요**설정만 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-183">The only possible setting for this parameter is **Important**.</span></span> |

<span data-ttu-id="3ad89-184">SQL Server IaaS 에이전트를 설치하고 구성하는 데는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-184">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="3ad89-185">자동화된 패치를 사용하지 않으려면 동일한 스크립트를 **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**에 대해 **-Enable** 매개 변수 없이 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-185">To disable Automated Patching, run the same script without the **-Enable** parameter to the **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span></span> <span data-ttu-id="3ad89-186">**-Enable** 매개 변수가 없는 경우 기능을 해제하는 명령을 신호로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3ad89-186">The absence of the **-Enable** parameter signals the command to disable the feature.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ad89-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3ad89-187">Next steps</span></span>
<span data-ttu-id="3ad89-188">사용 가능한 다른 자동화 작업에 대한 내용은 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ad89-188">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="3ad89-189">Azure VM의 SQL Server 실행에 대한 자세한 내용은 [Azure 가상 컴퓨터의 SQL Server 개요](virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ad89-189">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>


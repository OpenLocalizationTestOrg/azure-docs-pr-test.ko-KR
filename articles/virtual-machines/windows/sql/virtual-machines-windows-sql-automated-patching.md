---
title: "aaaAutomated SQL Server Vm (리소스 관리자)에 대 한 패치 | Microsoft Docs"
description: "에 대 한 SQL Server 가상 컴퓨터 리소스 관리자를 사용 하 여 Azure에서 실행 중인 hello 자동화 된 패치 적용 기능에 설명 합니다."
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
ms.openlocfilehash: 8bb8d0fb265e69d7bbf1fa047f5ceef02e7c56fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a><span data-ttu-id="d4f3f-103">Azure 가상 컴퓨터에서 SQL Server의 자동화된 패치(리소스 관리자)</span><span class="sxs-lookup"><span data-stu-id="d4f3f-103">Automated Patching for SQL Server in Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d4f3f-104">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="d4f3f-104">Resource Manager</span></span>](virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="d4f3f-105">클래식</span><span class="sxs-lookup"><span data-stu-id="d4f3f-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="d4f3f-106">자동화된 패치는 SQL Server를 실행하는 Azure 가상 컴퓨터에 대한 유지 관리 기간을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="d4f3f-107">이 유지 관리 기간 동안만 자동화된 업데이트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="d4f3f-108">SQL Server,이 rescriction 시스템 업데이트 및 모든 서버가 다시 시작 시 hello 최상의 가능한 hello 데이터베이스에 대 한 수행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-108">For SQL Server, this rescriction ensures that system updates and any associated restarts occur at hello best possible time for hello database.</span></span> <span data-ttu-id="d4f3f-109">자동화 된 패치 적용 hello에 따라 달라 집니다 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-109">Automated Patching depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="d4f3f-110">이 문서의 tooview hello 클래식 버전 참조 [Azure 클래식 가상 컴퓨터의 SQL Server에 대 한 자동화 된 패치 적용](../classic/sql-automated-patching.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-110">tooview hello classic version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Classic](../classic/sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4f3f-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d4f3f-111">Prerequisites</span></span>
<span data-ttu-id="d4f3f-112">toouse hello 다음 필수 구성 요소를 고려 자동화 된 패치 적용:</span><span class="sxs-lookup"><span data-stu-id="d4f3f-112">toouse Automated Patching, consider hello following prerequisites:</span></span>

<span data-ttu-id="d4f3f-113">**운영 체제**:</span><span class="sxs-lookup"><span data-stu-id="d4f3f-113">**Operating System**:</span></span>

* <span data-ttu-id="d4f3f-114">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="d4f3f-114">Windows Server 2012</span></span>
* <span data-ttu-id="d4f3f-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d4f3f-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="d4f3f-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="d4f3f-116">Windows Server 2016</span></span>

<span data-ttu-id="d4f3f-117">**SQL Server 버전**:</span><span class="sxs-lookup"><span data-stu-id="d4f3f-117">**SQL Server version**:</span></span>

* <span data-ttu-id="d4f3f-118">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="d4f3f-118">SQL Server 2012</span></span>
* <span data-ttu-id="d4f3f-119">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="d4f3f-119">SQL Server 2014</span></span>
* <span data-ttu-id="d4f3f-120">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="d4f3f-120">SQL Server 2016</span></span>

<span data-ttu-id="d4f3f-121">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="d4f3f-121">**Azure PowerShell**:</span></span>

* <span data-ttu-id="d4f3f-122">[설치 hello 최신 Azure PowerShell 명령을](/powershell/azure/overview) tooconfigure 하려는 경우 PowerShell과 함께 자동화 된 패치 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-122">[Install hello latest Azure PowerShell commands](/powershell/azure/overview) if you plan tooconfigure Automated Patching with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="d4f3f-123">자동화 된 패치 적용은 SQL Server IaaS 에이전트 확장 hello를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-123">Automated Patching relies on hello SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="d4f3f-124">현재 SQL 가상 컴퓨터 갤러리 이미지는 기본적으로 이 확장을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-124">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="d4f3f-125">자세한 내용은 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-125">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>
> 
> 

## <a name="settings"></a><span data-ttu-id="d4f3f-126">설정</span><span class="sxs-lookup"><span data-stu-id="d4f3f-126">Settings</span></span>
<span data-ttu-id="d4f3f-127">hello 다음 설명 자동화 된 패치 적용을 구성할 수 있는 hello 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-127">hello following table describes hello options that can be configured for Automated Patching.</span></span> <span data-ttu-id="d4f3f-128">hello 실제 구성 단계는 hello Azure 포털 또는 Azure Windows PowerShell 명령을 사용 하는지에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-128">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="d4f3f-129">설정</span><span class="sxs-lookup"><span data-stu-id="d4f3f-129">Setting</span></span> | <span data-ttu-id="d4f3f-130">가능한 값</span><span class="sxs-lookup"><span data-stu-id="d4f3f-130">Possible values</span></span> | <span data-ttu-id="d4f3f-131">설명</span><span class="sxs-lookup"><span data-stu-id="d4f3f-131">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d4f3f-132">**자동화된 패치**</span><span class="sxs-lookup"><span data-stu-id="d4f3f-132">**Automated Patching**</span></span> |<span data-ttu-id="d4f3f-133">사용/사용 안 함(사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="d4f3f-133">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="d4f3f-134">Azure 가상 컴퓨터에 대한 자동화된 패치를 사용 또는 사용 안 함으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-134">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="d4f3f-135">**유지 관리 일정**</span><span class="sxs-lookup"><span data-stu-id="d4f3f-135">**Maintenance schedule**</span></span> |<span data-ttu-id="d4f3f-136">매일, 월요일, 화요일, 수요일, 목요일, 금요일, 토요일, 일요일</span><span class="sxs-lookup"><span data-stu-id="d4f3f-136">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="d4f3f-137">가상 컴퓨터에 대 한 Windows, SQL Server 및 Microsoft 업데이트 다운로드 및 설치에 대 한 hello 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-137">hello schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="d4f3f-138">**유지 관리 시작 시간**</span><span class="sxs-lookup"><span data-stu-id="d4f3f-138">**Maintenance start hour**</span></span> |<span data-ttu-id="d4f3f-139">0-24</span><span class="sxs-lookup"><span data-stu-id="d4f3f-139">0-24</span></span> |<span data-ttu-id="d4f3f-140">hello 로컬 시작 시간 tooupdate hello 가상 컴퓨터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-140">hello local start time tooupdate hello virtual machine.</span></span> |
| <span data-ttu-id="d4f3f-141">**유지 관리 기간**</span><span class="sxs-lookup"><span data-stu-id="d4f3f-141">**Maintenance window duration**</span></span> |<span data-ttu-id="d4f3f-142">30-180</span><span class="sxs-lookup"><span data-stu-id="d4f3f-142">30-180</span></span> |<span data-ttu-id="d4f3f-143">hello 시간 (분) toocomplete hello 다운로드 및 업데이트의 설치를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-143">hello number of minutes permitted toocomplete hello download and installation of updates.</span></span> |
| <span data-ttu-id="d4f3f-144">**패치 범주**</span><span class="sxs-lookup"><span data-stu-id="d4f3f-144">**Patch Category**</span></span> |<span data-ttu-id="d4f3f-145">중요</span><span class="sxs-lookup"><span data-stu-id="d4f3f-145">Important</span></span> |<span data-ttu-id="d4f3f-146">업데이트 toodownload 및 설치의 hello 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-146">hello category of updates toodownload and install.</span></span> |

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="d4f3f-147">Hello 포털의 구성</span><span class="sxs-lookup"><span data-stu-id="d4f3f-147">Configuration in hello Portal</span></span>
<span data-ttu-id="d4f3f-148">Azure 포털 tooconfigure hello에서는 프로 비전 하는 동안 또는 기존 Vm에 대 한 자동화 된 패치 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-148">You can use hello Azure portal tooconfigure Automated Patching during provisioning or for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="d4f3f-149">새 VM</span><span class="sxs-lookup"><span data-stu-id="d4f3f-149">New VMs</span></span>
<span data-ttu-id="d4f3f-150">사용 하 여 hello Azure 포털 tooconfigure hello 리소스 관리자 배포 모델에서 새 SQL Server 가상 컴퓨터를 만들 때 자동화 된 패치 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-150">Use hello Azure portal tooconfigure Automated Patching when you create a new SQL Server Virtual Machine in hello Resource Manager deployment model.</span></span>

<span data-ttu-id="d4f3f-151">Hello에 **SQL Server 설정을** 블레이드를 **자동화 된 패치 적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-151">In hello **SQL Server settings** blade, select **Automated patching**.</span></span> <span data-ttu-id="d4f3f-152">hello 다음 Azure 포털 스크린샷은 hello **SQL 자동화 된 패치 적용** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-152">hello following Azure portal screenshot shows hello **SQL Automated Patching** blade.</span></span>

![Azure 포털에서 SQL 자동화된 패치](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

<span data-ttu-id="d4f3f-154">컨텍스트에 대해 hello 전체 항목에 참조 [Azure에서 SQL Server 가상 컴퓨터 프로 비전](virtual-machines-windows-portal-sql-server-provision.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-154">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="d4f3f-155">기존 VM</span><span class="sxs-lookup"><span data-stu-id="d4f3f-155">Existing VMs</span></span>
<span data-ttu-id="d4f3f-156">기존 SQL Server 가상 컴퓨터에 대한 해당 SQL Server 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-156">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="d4f3f-157">다음 hello 선택 **SQL Server 구성** hello 섹션 **설정** 블레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-157">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![기존 VM에 대한 SQL 자동 패치](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

<span data-ttu-id="d4f3f-159">Hello에 **SQL Server 구성** 블레이드에서 hello 클릭 **편집** hello 단추 자동 패치 섹션.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-159">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated patching section.</span></span>

![기존 VM에 대한 SQL 자동 패치 구성](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

<span data-ttu-id="d4f3f-161">완료 되 면 hello 클릭 **확인** hello hello 하단에서 단추 **SQL Server 구성** 블레이드 toosave 변경 내용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-161">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="d4f3f-162">설정 하는 경우 자동화 된 패치 적용 hello에 대 한 처음으로, Azure hello 백그라운드에서 hello SQL Server IaaS 에이전트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-162">If you are enabling Automated Patching for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="d4f3f-163">이 시간 동안 hello Azure 포털 수 자동화 된 패치 적용 구성 되어 있는지으로 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-163">During this time, hello Azure portal might not show that Automated Patching is configured.</span></span> <span data-ttu-id="d4f3f-164">Hello 에이전트 toobe 설치에 대 일 분 정도 기다린 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-164">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="d4f3f-165">해당 hello Azure 후 포털 hello 새 설정이 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-165">After that hello Azure portal reflects hello new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="d4f3f-166">또한 템플릿을 사용하여 자동화된 패치를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-166">You can also configure Automated Patching using a template.</span></span> <span data-ttu-id="d4f3f-167">자세한 내용은 [자동화된 패치에 대한 Azure 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-167">For more information, see [Azure quickstart template for Automated Patching](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span></span>
> 
> 

## <a name="configuration-with-powershell"></a><span data-ttu-id="d4f3f-168">PowerShell을 사용하여 구성</span><span class="sxs-lookup"><span data-stu-id="d4f3f-168">Configuration with PowerShell</span></span>
<span data-ttu-id="d4f3f-169">SQL VM에서 프로 비전 후 PowerShell tooconfigure를 사용 하 여 자동화 된 패치 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-169">After provisioning your SQL VM, use PowerShell tooconfigure Automated Patching.</span></span>

<span data-ttu-id="d4f3f-170">다음 예제는 hello에서 PowerShell이 사용 되는 tooconfigure 기존 SQL Server VM에서 자동화 된 패치 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-170">In hello following example, PowerShell is used tooconfigure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="d4f3f-171">hello **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig** 명령은 자동 업데이트를 위한 새 유지 관리 기간을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-171">hello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

<span data-ttu-id="d4f3f-172">이 예제에 따라, hello 다음 표에서 설명 hello hello 대상 Azure VM에 실제로 미치는 영향:</span><span class="sxs-lookup"><span data-stu-id="d4f3f-172">Based on this example, hello following table describes hello practical effect on hello target Azure VM:</span></span>

| <span data-ttu-id="d4f3f-173">매개 변수</span><span class="sxs-lookup"><span data-stu-id="d4f3f-173">Parameter</span></span> | <span data-ttu-id="d4f3f-174">결과</span><span class="sxs-lookup"><span data-stu-id="d4f3f-174">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="d4f3f-175">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="d4f3f-175">**DayOfWeek**</span></span> |<span data-ttu-id="d4f3f-176">매주 목요일마다 패치가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-176">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="d4f3f-177">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="d4f3f-177">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="d4f3f-178">오전 11시에 업데이트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-178">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="d4f3f-179">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="d4f3f-179">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="d4f3f-180">120분 이내에 패치를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-180">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="d4f3f-181">Hello 시작 시간에 따라, 오후 1시 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-181">Based on hello start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="d4f3f-182">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="d4f3f-182">**PatchCategory**</span></span> |<span data-ttu-id="d4f3f-183">이 매개 변수는 변수에 가능한 설정은 hello **중요**합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-183">hello only possible setting for this parameter is **Important**.</span></span> |

<span data-ttu-id="d4f3f-184">몇 분 tooinstall 수행 하 고 hello SQL Server IaaS 에이전트를 구성할 수 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-184">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="d4f3f-185">toodisable 자동화 된 패치 적용, hello 하지 않고 동일한 스크립트 실행된 hello **-사용 하도록 설정** 매개 변수 toohello **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig**합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-185">toodisable Automated Patching, run hello same script without hello **-Enable** parameter toohello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span></span> <span data-ttu-id="d4f3f-186">hello 없을 경우 hello **-사용 하도록 설정** 매개 변수가 신호 hello 명령 toodisable hello 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-186">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4f3f-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d4f3f-187">Next steps</span></span>
<span data-ttu-id="d4f3f-188">사용 가능한 다른 자동화 작업에 대한 내용은 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-188">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="d4f3f-189">Azure VM의 SQL Server 실행에 대한 자세한 내용은 [Azure 가상 컴퓨터의 SQL Server 개요](virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4f3f-189">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>


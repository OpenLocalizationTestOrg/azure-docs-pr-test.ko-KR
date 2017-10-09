---
title: "aaaAutomated SQL Server Vm (클래식)에 대 한 패치 | Microsoft Docs"
description: "에 대 한 SQL Server 가상 컴퓨터 hello 클래식 배포 모드를 사용 하 여 Azure에서 실행 중인 hello 자동화 된 패치 적용 기능에 설명 합니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 737b2f65-08b9-4f54-b867-e987730265a8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 2ef06b95705fc457605d6eb2fbc0afd490321843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="d75b8-103">Azure 가상 컴퓨터에서 SQL Server의 자동화된 패치(클래식)</span><span class="sxs-lookup"><span data-stu-id="d75b8-103">Automated Patching for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d75b8-104">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="d75b8-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="d75b8-105">클래식</span><span class="sxs-lookup"><span data-stu-id="d75b8-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="d75b8-106">자동화된 패치는 SQL Server를 실행하는 Azure 가상 컴퓨터에 대한 유지 관리 기간을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="d75b8-107">이 유지 관리 기간 동안만 자동화된 업데이트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="d75b8-108">SQL Server, 시스템 업데이트 및 모든 서버가 다시 시작 시 hello 최상의 가능한 hello 데이터베이스에 대 한 수행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-108">For SQL Server, this ensures that system updates and any associated restarts occur at hello best possible time for hello database.</span></span> <span data-ttu-id="d75b8-109">자동화 된 패치 적용 hello에 따라 달라 집니다 [SQL Server IaaS 에이전트 확장](../classic/sql-server-agent-extension.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-109">Automated Patching depends on hello [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="d75b8-110">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d75b8-111">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="d75b8-112">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="d75b8-113">이 문서의 tooview hello 리소스 관리자 버전 참조 [Azure 가상 컴퓨터 리소스 관리자에서 SQL Server에 대 한 자동화 된 패치 적용](../sql/virtual-machines-windows-sql-automated-patching.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-113">tooview hello Resource Manager version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d75b8-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d75b8-114">Prerequisites</span></span>
<span data-ttu-id="d75b8-115">toouse hello 다음 필수 구성 요소를 고려 자동화 된 패치 적용:</span><span class="sxs-lookup"><span data-stu-id="d75b8-115">toouse Automated Patching, consider hello following prerequisites:</span></span>

<span data-ttu-id="d75b8-116">**운영 체제**:</span><span class="sxs-lookup"><span data-stu-id="d75b8-116">**Operating System**:</span></span>

* <span data-ttu-id="d75b8-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="d75b8-117">Windows Server 2012</span></span>
* <span data-ttu-id="d75b8-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d75b8-118">Windows Server 2012 R2</span></span>
* <span data-ttu-id="d75b8-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="d75b8-119">Windows Server 2016</span></span>

<span data-ttu-id="d75b8-120">**SQL Server 버전**:</span><span class="sxs-lookup"><span data-stu-id="d75b8-120">**SQL Server version**:</span></span>

* <span data-ttu-id="d75b8-121">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="d75b8-121">SQL Server 2012</span></span>
* <span data-ttu-id="d75b8-122">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="d75b8-122">SQL Server 2014</span></span>
* <span data-ttu-id="d75b8-123">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="d75b8-123">SQL Server 2016</span></span>

<span data-ttu-id="d75b8-124">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="d75b8-124">**Azure PowerShell**:</span></span>

* <span data-ttu-id="d75b8-125">[설치 hello 최신 Azure PowerShell 명령을](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-125">[Install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="d75b8-126">**SQL Server IaaS 확장**:</span><span class="sxs-lookup"><span data-stu-id="d75b8-126">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="d75b8-127">[SQL Server IaaS 확장 hello 설치](../classic/sql-server-agent-extension.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-127">[Install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="d75b8-128">설정</span><span class="sxs-lookup"><span data-stu-id="d75b8-128">Settings</span></span>
<span data-ttu-id="d75b8-129">hello 다음 설명 자동화 된 패치 적용을 구성할 수 있는 hello 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-129">hello following table describes hello options that can be configured for Automated Patching.</span></span> <span data-ttu-id="d75b8-130">클래식 Vm에 대 한 PowerShell tooconfigure를 이러한 설정을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-130">For classic VMs, you must use PowerShell tooconfigure these settings.</span></span>

| <span data-ttu-id="d75b8-131">설정</span><span class="sxs-lookup"><span data-stu-id="d75b8-131">Setting</span></span> | <span data-ttu-id="d75b8-132">가능한 값</span><span class="sxs-lookup"><span data-stu-id="d75b8-132">Possible values</span></span> | <span data-ttu-id="d75b8-133">설명</span><span class="sxs-lookup"><span data-stu-id="d75b8-133">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d75b8-134">**자동화된 패치**</span><span class="sxs-lookup"><span data-stu-id="d75b8-134">**Automated Patching**</span></span> |<span data-ttu-id="d75b8-135">사용/사용 안 함(사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="d75b8-135">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="d75b8-136">Azure 가상 컴퓨터에 대한 자동화된 패치를 사용 또는 사용 안 함으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-136">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="d75b8-137">**유지 관리 일정**</span><span class="sxs-lookup"><span data-stu-id="d75b8-137">**Maintenance schedule**</span></span> |<span data-ttu-id="d75b8-138">매일, 월요일, 화요일, 수요일, 목요일, 금요일, 토요일, 일요일</span><span class="sxs-lookup"><span data-stu-id="d75b8-138">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="d75b8-139">가상 컴퓨터에 대 한 Windows, SQL Server 및 Microsoft 업데이트 다운로드 및 설치에 대 한 hello 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-139">hello schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="d75b8-140">**유지 관리 시작 시간**</span><span class="sxs-lookup"><span data-stu-id="d75b8-140">**Maintenance start hour**</span></span> |<span data-ttu-id="d75b8-141">0-24</span><span class="sxs-lookup"><span data-stu-id="d75b8-141">0-24</span></span> |<span data-ttu-id="d75b8-142">hello 로컬 시작 시간 tooupdate hello 가상 컴퓨터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-142">hello local start time tooupdate hello virtual machine.</span></span> |
| <span data-ttu-id="d75b8-143">**유지 관리 기간**</span><span class="sxs-lookup"><span data-stu-id="d75b8-143">**Maintenance window duration**</span></span> |<span data-ttu-id="d75b8-144">30-180</span><span class="sxs-lookup"><span data-stu-id="d75b8-144">30-180</span></span> |<span data-ttu-id="d75b8-145">hello 시간 (분) toocomplete hello 다운로드 및 업데이트의 설치를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-145">hello number of minutes permitted toocomplete hello download and installation of updates.</span></span> |
| <span data-ttu-id="d75b8-146">**패치 범주**</span><span class="sxs-lookup"><span data-stu-id="d75b8-146">**Patch Category**</span></span> |<span data-ttu-id="d75b8-147">중요</span><span class="sxs-lookup"><span data-stu-id="d75b8-147">Important</span></span> |<span data-ttu-id="d75b8-148">업데이트 toodownload 및 설치의 hello 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-148">hello category of updates toodownload and install.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="d75b8-149">PowerShell을 사용하여 구성</span><span class="sxs-lookup"><span data-stu-id="d75b8-149">Configuration with PowerShell</span></span>
<span data-ttu-id="d75b8-150">다음 예제는 hello에서 PowerShell이 사용 되는 tooconfigure 기존 SQL Server VM에서 자동화 된 패치 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-150">In hello following example, PowerShell is used tooconfigure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="d75b8-151">hello **New-azurevmsqlserverautopatchingconfig** 명령은 자동 업데이트를 위한 새 유지 관리 기간을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-151">hello **New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

<span data-ttu-id="d75b8-152">이 예제에 따라, hello 다음 표에서 설명 hello hello 대상 Azure VM에 실제로 미치는 영향:</span><span class="sxs-lookup"><span data-stu-id="d75b8-152">Based on this example, hello following table describes hello practical effect on hello target Azure VM:</span></span>

| <span data-ttu-id="d75b8-153">매개 변수</span><span class="sxs-lookup"><span data-stu-id="d75b8-153">Parameter</span></span> | <span data-ttu-id="d75b8-154">결과</span><span class="sxs-lookup"><span data-stu-id="d75b8-154">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="d75b8-155">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="d75b8-155">**DayOfWeek**</span></span> |<span data-ttu-id="d75b8-156">매주 목요일마다 패치가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-156">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="d75b8-157">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="d75b8-157">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="d75b8-158">오전 11시에 업데이트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-158">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="d75b8-159">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="d75b8-159">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="d75b8-160">120분 이내에 패치를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-160">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="d75b8-161">Hello 시작 시간에 따라, 오후 1시 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-161">Based on hello start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="d75b8-162">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="d75b8-162">**PatchCategory**</span></span> |<span data-ttu-id="d75b8-163">hello 가능한 설정을이 매개 변수는 "중요"입니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-163">hello only possible setting for this parameter is “Important”.</span></span> |

<span data-ttu-id="d75b8-164">몇 분 tooinstall 수행 하 고 hello SQL Server IaaS 에이전트를 구성할 수 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-164">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="d75b8-165">toodisable 자동화 된 패치 적용을 하지 않고 동일한 스크립트 실행된 hello hello-Enable 매개 변수 toohello New-azurevmsqlserverautopatchingconfig 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-165">toodisable Automated Patching, run hello same script without hello -Enable parameter toohello New-AzureVMSqlServerAutoPatchingConfig.</span></span> <span data-ttu-id="d75b8-166">몇 분 toodisable 걸릴 수 있습니다 설치의 경우와 같이 자동화 된 패치 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d75b8-166">As with installation, it can take several minutes toodisable Automated Patching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d75b8-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d75b8-167">Next steps</span></span>
<span data-ttu-id="d75b8-168">사용 가능한 다른 자동화 작업에 대한 내용은 [SQL Server IaaS 에이전트 확장](../classic/sql-server-agent-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d75b8-168">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="d75b8-169">Azure VM의 SQL Server 실행에 대한 자세한 내용은 [Azure 가상 컴퓨터의 SQL Server 개요](../sql/virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d75b8-169">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>


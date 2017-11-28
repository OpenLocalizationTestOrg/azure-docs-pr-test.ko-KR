---
title: "SQL Server VM의 자동화된 패치(클래식) | Microsoft Docs"
description: "클래식 배포 모드를 사용하여 Azure에서 실행 중인 SQL Server 가상 컴퓨터에 대한 자동화된 패치 기능에 대해 설명합니다."
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
ms.openlocfilehash: 1959871141f196ba80ffd7b37e62e5ea5b42dba3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="1a79e-103">Azure 가상 컴퓨터에서 SQL Server의 자동화된 패치(클래식)</span><span class="sxs-lookup"><span data-stu-id="1a79e-103">Automated Patching for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1a79e-104">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="1a79e-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="1a79e-105">클래식</span><span class="sxs-lookup"><span data-stu-id="1a79e-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="1a79e-106">자동화된 패치는 SQL Server를 실행하는 Azure 가상 컴퓨터에 대한 유지 관리 기간을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="1a79e-107">이 유지 관리 기간 동안만 자동화된 업데이트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="1a79e-108">SQL Server의 경우 이를 통해 시스템 업데이트 및 관련 재시작 작업이 데이터베이스에 대해 가장 적절한 시간에 수행되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-108">For SQL Server, this ensures that system updates and any associated restarts occur at the best possible time for the database.</span></span> <span data-ttu-id="1a79e-109">자동화된 패치는 [SQL Server IaaS 에이전트 확장](../classic/sql-server-agent-extension.md)에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-109">Automated Patching depends on the [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="1a79e-110">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1a79e-111">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-111">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="1a79e-112">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-112">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="1a79e-113">이 문서의 Resource Manager 버전을 보려면 [Azure 가상 컴퓨터 Resource Manager에서 SQL Server의 자동화된 패치](../sql/virtual-machines-windows-sql-automated-patching.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a79e-113">To view the Resource Manager version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a79e-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1a79e-114">Prerequisites</span></span>
<span data-ttu-id="1a79e-115">자동화된 패치를 사용하려면 다음 필수 조건을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="1a79e-115">To use Automated Patching, consider the following prerequisites:</span></span>

<span data-ttu-id="1a79e-116">**운영 체제**:</span><span class="sxs-lookup"><span data-stu-id="1a79e-116">**Operating System**:</span></span>

* <span data-ttu-id="1a79e-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="1a79e-117">Windows Server 2012</span></span>
* <span data-ttu-id="1a79e-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="1a79e-118">Windows Server 2012 R2</span></span>
* <span data-ttu-id="1a79e-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="1a79e-119">Windows Server 2016</span></span>

<span data-ttu-id="1a79e-120">**SQL Server 버전**:</span><span class="sxs-lookup"><span data-stu-id="1a79e-120">**SQL Server version**:</span></span>

* <span data-ttu-id="1a79e-121">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="1a79e-121">SQL Server 2012</span></span>
* <span data-ttu-id="1a79e-122">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="1a79e-122">SQL Server 2014</span></span>
* <span data-ttu-id="1a79e-123">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="1a79e-123">SQL Server 2016</span></span>

<span data-ttu-id="1a79e-124">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="1a79e-124">**Azure PowerShell**:</span></span>

* <span data-ttu-id="1a79e-125">[최신 Azure PowerShell cmdlet을 설치합니다](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1a79e-125">[Install the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="1a79e-126">**SQL Server IaaS 확장**:</span><span class="sxs-lookup"><span data-stu-id="1a79e-126">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="1a79e-127">[SQL Server IaaS 확장을 설치합니다](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="1a79e-127">[Install the SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="1a79e-128">설정</span><span class="sxs-lookup"><span data-stu-id="1a79e-128">Settings</span></span>
<span data-ttu-id="1a79e-129">다음 표에서는 자동화된 패치에 대해 구성할 수 있는 옵션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-129">The following table describes the options that can be configured for Automated Patching.</span></span> <span data-ttu-id="1a79e-130">클래식 VM의 경우 이러한 설정을 구성하려면 PowerShell을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-130">For classic VMs, you must use PowerShell to configure these settings.</span></span>

| <span data-ttu-id="1a79e-131">설정</span><span class="sxs-lookup"><span data-stu-id="1a79e-131">Setting</span></span> | <span data-ttu-id="1a79e-132">가능한 값</span><span class="sxs-lookup"><span data-stu-id="1a79e-132">Possible values</span></span> | <span data-ttu-id="1a79e-133">설명</span><span class="sxs-lookup"><span data-stu-id="1a79e-133">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a79e-134">**자동화된 패치**</span><span class="sxs-lookup"><span data-stu-id="1a79e-134">**Automated Patching**</span></span> |<span data-ttu-id="1a79e-135">사용/사용 안 함(사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="1a79e-135">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="1a79e-136">Azure 가상 컴퓨터에 대한 자동화된 패치를 사용 또는 사용 안 함으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-136">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="1a79e-137">**유지 관리 일정**</span><span class="sxs-lookup"><span data-stu-id="1a79e-137">**Maintenance schedule**</span></span> |<span data-ttu-id="1a79e-138">매일, 월요일, 화요일, 수요일, 목요일, 금요일, 토요일, 일요일</span><span class="sxs-lookup"><span data-stu-id="1a79e-138">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="1a79e-139">가상 컴퓨터에 대한 Windows, SQL Server 및 Microsoft 업데이트 다운로드 및 설치에 대한 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-139">The schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="1a79e-140">**유지 관리 시작 시간**</span><span class="sxs-lookup"><span data-stu-id="1a79e-140">**Maintenance start hour**</span></span> |<span data-ttu-id="1a79e-141">0-24</span><span class="sxs-lookup"><span data-stu-id="1a79e-141">0-24</span></span> |<span data-ttu-id="1a79e-142">가상 컴퓨터를 업데이트할 로컬 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-142">The local start time to update the virtual machine.</span></span> |
| <span data-ttu-id="1a79e-143">**유지 관리 기간**</span><span class="sxs-lookup"><span data-stu-id="1a79e-143">**Maintenance window duration**</span></span> |<span data-ttu-id="1a79e-144">30-180</span><span class="sxs-lookup"><span data-stu-id="1a79e-144">30-180</span></span> |<span data-ttu-id="1a79e-145">업데이트 다운로드 및 설치를 완료하는데 허용된 시간(분)입니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-145">The number of minutes permitted to complete the download and installation of updates.</span></span> |
| <span data-ttu-id="1a79e-146">**패치 범주**</span><span class="sxs-lookup"><span data-stu-id="1a79e-146">**Patch Category**</span></span> |<span data-ttu-id="1a79e-147">중요</span><span class="sxs-lookup"><span data-stu-id="1a79e-147">Important</span></span> |<span data-ttu-id="1a79e-148">다운로드 및 설치할 업데이트의 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-148">The category of updates to download and install.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="1a79e-149">PowerShell을 사용하여 구성</span><span class="sxs-lookup"><span data-stu-id="1a79e-149">Configuration with PowerShell</span></span>
<span data-ttu-id="1a79e-150">다음 예제에서는 PowerShell을 사용하여 기존 SQL Server VM에 대해 자동화된 패치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-150">In the following example, PowerShell is used to configure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="1a79e-151">**New-AzureVMSqlServerAutoPatchingConfig** 명령은 자동 업데이트에 대한 새 유지 관리 기간을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-151">The **New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

<span data-ttu-id="1a79e-152">이 예제를 바탕으로 다음 표에서는 대상 Azure VM에 미치는 실질적인 영향을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-152">Based on this example, the following table describes the practical effect on the target Azure VM:</span></span>

| <span data-ttu-id="1a79e-153">매개 변수</span><span class="sxs-lookup"><span data-stu-id="1a79e-153">Parameter</span></span> | <span data-ttu-id="1a79e-154">결과</span><span class="sxs-lookup"><span data-stu-id="1a79e-154">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="1a79e-155">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="1a79e-155">**DayOfWeek**</span></span> |<span data-ttu-id="1a79e-156">매주 목요일마다 패치가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-156">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="1a79e-157">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="1a79e-157">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="1a79e-158">오전 11시에 업데이트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-158">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="1a79e-159">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="1a79e-159">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="1a79e-160">120분 이내에 패치를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-160">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="1a79e-161">시작 시간을 기준으로 오후 1시까지 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-161">Based on the start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="1a79e-162">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="1a79e-162">**PatchCategory**</span></span> |<span data-ttu-id="1a79e-163">이 매개 변수에 대해서는 "중요" 설정만 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-163">The only possible setting for this parameter is “Important”.</span></span> |

<span data-ttu-id="1a79e-164">SQL Server IaaS 에이전트를 설치하고 구성하는 데는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-164">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="1a79e-165">자동 패치를 사용하지 않으려면 동일한 스크립트를 New-AzureVMSqlServerAutoPatchingConfig에 대해 -Enable 매개 변수 없이 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-165">To disable Automated Patching, run the same script without the -Enable parameter to the New-AzureVMSqlServerAutoPatchingConfig.</span></span> <span data-ttu-id="1a79e-166">설치와 마찬가지로 자동화된 패치를 사용하지 않도록 설정하는 데도 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a79e-166">As with installation, it can take several minutes to disable Automated Patching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a79e-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1a79e-167">Next steps</span></span>
<span data-ttu-id="1a79e-168">사용 가능한 다른 자동화 작업에 대한 내용은 [SQL Server IaaS 에이전트 확장](../classic/sql-server-agent-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a79e-168">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="1a79e-169">Azure VM의 SQL Server 실행에 대한 자세한 내용은 [Azure 가상 컴퓨터의 SQL Server 개요](../sql/virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a79e-169">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>


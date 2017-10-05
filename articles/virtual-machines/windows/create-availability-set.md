---
title: "Azure에서 VM 가용성 집합 만들기 | Microsoft Docs"
description: "Resource Manager 배포 모델에서 Azure PowerShell 또는 포털을 사용하여 가상 컴퓨터에 대한 관리 가용성 집합 또는 비관리 가용성 집합을 만드는 방법에 대해 알아봅니다."
keywords: "가용성 집합"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a3db8659-ace8-4e78-8b8c-1e75c04c042c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e813ade8e105169f21138ed8a8eafda1ff39f42e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a><span data-ttu-id="dea6d-104">Azure 가용성 집합을 만들어 VM 가용성 향상</span><span class="sxs-lookup"><span data-stu-id="dea6d-104">Increase VM availability by creating an Azure availability set</span></span> 
<span data-ttu-id="dea6d-105">가용성 집합은 응용 프로그램에 중복성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-105">Availability sets provide redundancy to your application.</span></span> <span data-ttu-id="dea6d-106">둘 이상의 가상 컴퓨터를 가용성 집합으로 그룹화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-106">We recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="dea6d-107">이 구성은 계획된 유지 관리 또는 계획되지 않은 유지 관리 이벤트 중에 적어도 하나의 가상 컴퓨터를 사용할 수 있고 99.95% Azure SLA가 충족되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-107">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine will be available and meet the 99.95% Azure SLA.</span></span> <span data-ttu-id="dea6d-108">자세한 내용은 [가상 컴퓨터에 대한 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dea6d-108">For more information, see the [SLA for Virtual Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dea6d-109">가용성 집합과 동일한 리소스 그룹에 VM을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-109">VMs must be created in the same resource group as the availability set.</span></span>
> 

<span data-ttu-id="dea6d-110">VM을 가용성 집합에 포함하려면 가용성 집합을 먼저 만들거나 집합에 첫 번째 VM을 만들 때 가용성 집합을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-110">If you want your VM to be part of an availability set, you need to create the availability set first or while you are creating your first VM in the set.</span></span> <span data-ttu-id="dea6d-111">VM에서 관리 디스크를 사용하게 될 경우 가용성 집합을 관리 가용성 집합으로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-111">If your VM will be using Managed Disks, the availability set must be created as a managed availability set.</span></span>

<span data-ttu-id="dea6d-112">가용성 집합을 만들고 사용하는 방법에 대한 자세한 내용은 [가상 컴퓨터의 가용성 관리](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dea6d-112">For more information about creating and using availability sets, see [Manage the availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="use-the-portal-to-create-an-availability-set-before-creating-your-vms"></a><span data-ttu-id="dea6d-113">VM을 만들기 전에 포털을 사용하여 가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="dea6d-113">Use the portal to create an availability set before creating your VMs</span></span>
1. <span data-ttu-id="dea6d-114">허브 메뉴에서 **찾아보기**를 클릭하고 **가용성 집합**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-114">In the hub menu, click **Browse** and select **Availability sets**.</span></span>
2. <span data-ttu-id="dea6d-115">**가용성 집합 블레이드**에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-115">On the **Availability sets blade**, click **Add**.</span></span>
   
    ![새로운 가용성 집합을 만들기 위한 추가 단추를 보여 주는 스크린샷](./media/create-availability-set/add-availability-set.png)
3. <span data-ttu-id="dea6d-117">**가용성 집합 만들기** 블레이드에서 해당 집합에 대한 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-117">On the **Create availability set** blade, complete the information for your set.</span></span>
   
    ![가용성 집합을 만들기 위해 입력해야 할 정보를 보여 주는 스크린샷](./media/create-availability-set/create-availability-set.png)
   
   * <span data-ttu-id="dea6d-119">**이름** - 이름은 숫자, 문자, 마침표, 밑줄 및 대시로 구성되며 1~ 80자 이내여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-119">**Name** - the name should be 1-80 characters made up of numbers, letters, periods, underscores and dashes.</span></span> <span data-ttu-id="dea6d-120">첫 번째 문자는 문자 또는 숫자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-120">The first character must be a letter or number.</span></span> <span data-ttu-id="dea6d-121">마지막 문자는 문자, 숫자 또는 밑줄이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-121">The last character must be a letter, number or underscore.</span></span>
   * <span data-ttu-id="dea6d-122">**장애 도메인** - 장애 도메인은 공통 전원과 네트워크 스위치를 공유하는 가상 컴퓨터 그룹을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-122">**Fault domains** - fault domains define the group of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="dea6d-123">기본적으로 VM은 최대 3개의 장애 도메인에 분산되어 있으며 장애 도메인 수는 1~3개 사이로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-123">By default, the VMs  are separated across up to three fault domains and can be changed to between 1 and 3.</span></span>
   * <span data-ttu-id="dea6d-124">**업데이트 도메인** - 5개의 업데이트 도메인이 기본적으로 할당되며 1~20개 사이로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-124">**Update domains** -  five update domains are assigned by default and this can be set to between 1 and 20.</span></span> <span data-ttu-id="dea6d-125">업데이트 도메인은 동시에 다시 부팅할 수 있는 가상 컴퓨터 그룹과 기본 물리적 하드웨어를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-125">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="dea6d-126">예를 들어 5개의 업데이트 도메인을 지정하며 단일 가용성 집합 내에 5개를 넘는 가상 컴퓨터를 구성한 경우 6번째 가상 컴퓨터는 동일한 업데이트 도메인에 첫 번째 가상 컴퓨터로 배치되고, 7번째 가상 컴퓨터는 동일한 UD에 두 번째 가상 컴퓨터로 배치되는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-126">For example, if we specify five update domains, when more than five virtual machines are configured within a single Availability Set, the sixth virtual machine will be placed into the same update domain as the first virtual machine, the seventh in the same UD as the second virtual machine, and so on.</span></span> <span data-ttu-id="dea6d-127">다시 부팅 순서는 순차적이지 않을 수 있지만 한 번에 하나의 업데이트 도메인만 다시 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-127">The order of the reboots may not be sequential, but only one update domain will be rebooted at a time.</span></span>
   * <span data-ttu-id="dea6d-128">**구독** - 둘 이상의 구독이 있는 경우 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-128">**Subscription** - select the subscription to use if you have more than one.</span></span>
   * <span data-ttu-id="dea6d-129">**리소스 그룹** -화살표를 클릭하고 드롭다운에서 리소스 그룹을 선택하여 기존 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-129">**Resource group** - select an existing resource group by clicking the arrow and selecting a resource group from the drop down.</span></span> <span data-ttu-id="dea6d-130">또한 이름을 입력하여 새 리소스 그룹을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-130">You can also create a new resource group by typing in a name.</span></span> <span data-ttu-id="dea6d-131">이름에는 문자, 숫자, 마침표, 대시, 밑줄 및 여는 괄호 또는 닫는 괄호가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-131">The name can contain any of the following characters: letters, numbers, periods, dashes, underscores and opening or closing parenthesis.</span></span> <span data-ttu-id="dea6d-132">이름이 마침표로 끝날 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-132">The name cannot end in a period.</span></span> <span data-ttu-id="dea6d-133">가용성 그룹의 모든 VM은 가용성 집합과 동일한 리소스 그룹에 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-133">All of the VMs in the availability group need to be created in the same resource group as the availability set.</span></span>
   * <span data-ttu-id="dea6d-134">**위치** - 드롭다운 목록에서 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-134">**Location** - select a location from the drop-down.</span></span>
   * <span data-ttu-id="dea6d-135">**관리** - 저장소에 Managed Disks를 사용하는 VM과 함께 사용할 관리 가용성 집합을 만들려면 *예*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-135">**Managed** - select *Yes* to create a managed availability set to use with VMs that use Managed Disks for storage.</span></span> <span data-ttu-id="dea6d-136">집합에 포함될 VM이 저장소 계정에 비관리 디스크를 사용하는 경우 **아니요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-136">Select **No** if the VMs that will be in the set use unmanaged disks in a storage account.</span></span>
   
4. <span data-ttu-id="dea6d-137">정보를 다 입력했으면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-137">When you are done entering the information, click **Create**.</span></span> 

## <a name="use-the-portal-to-create-a-virtual-machine-and-an-availability-set-at-the-same-time"></a><span data-ttu-id="dea6d-138">포털을 사용하여 가상 컴퓨터와 가용성 집합을 동시에 만들기</span><span class="sxs-lookup"><span data-stu-id="dea6d-138">Use the portal to create a virtual machine and an availability set at the same time</span></span>
<span data-ttu-id="dea6d-139">포털을 사용하여 새 VM을 만드는 경우 집합의 첫 번째 VM을 만드는 동안 VM에 대한 새 가용성 집합도 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-139">If you are creating a new VM using the portal, you can also create a new availability set for the VM while you create the first VM in the set.</span></span> <span data-ttu-id="dea6d-140">VM에 Managed Disks를 사용하기로 선택하면 관리 가용성 집합이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-140">If you choose to use Managed Disks for your VM, a managed availability set will be created.</span></span>

![VM을 만드는 동안 새로운 가용성 집합을 만드는 프로세스를 보여 주는 스크린샷](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-to-an-existing-availability-set-in-the-portal"></a><span data-ttu-id="dea6d-142">포털에서 기존 가용성 집합에 새 VM 추가</span><span class="sxs-lookup"><span data-stu-id="dea6d-142">Add a new VM to an existing availability set in the portal</span></span>
<span data-ttu-id="dea6d-143">집합에 포함하기 위해 만드는 각 VM을 동일한 **리소스 그룹** 에 만들어야 하며 3단계에서 기존 가용성 집합을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-143">For each additional VM that you create that should belong in the set, make sure that you create it in the same **resource group** and then select the existing availability set in Step 3.</span></span> 

![VM에 사용할 기존 가용성 집합을 선택하는 방법을 보여 주는 스크린샷](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-to-create-an-availability-set"></a><span data-ttu-id="dea6d-145">PowerShell을 사용하여 가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="dea6d-145">Use PowerShell to create an availability set</span></span>
<span data-ttu-id="dea6d-146">이 예제에서는 **미국 서부** 위치의 **myResourceGroup** 리소스 그룹에 **myAvailabilitySet**이라는 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-146">This example creates an availability set named **myAvailabilitySet** in the **myResourceGroup** resource group in the **West US** location.</span></span> <span data-ttu-id="dea6d-147">집합에 포함될 첫 번째 VM을 만들기 전에 이 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-147">This needs to be done before you create the first VM that will be in the set.</span></span>

<span data-ttu-id="dea6d-148">시작하기 전에 AzureRM.Compute PowerShell 모듈이 최신 버전인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-148">Before you begin, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="dea6d-149">다음 명령을 실행하여 PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-149">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="dea6d-150">자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dea6d-150">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


<span data-ttu-id="dea6d-151">VM에 관리 디스크를 사용하는 경우 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-151">If you are using managed disks for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

<span data-ttu-id="dea6d-152">VM에 사용자 고유의 저장소 계정을 사용하는 경우 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-152">If you are using your own storage accounts for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

<span data-ttu-id="dea6d-153">자세한 내용은 [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dea6d-153">For more information, see [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="dea6d-154">문제 해결</span><span class="sxs-lookup"><span data-stu-id="dea6d-154">Troubleshooting</span></span>
* <span data-ttu-id="dea6d-155">VM을 만들 때 원하는 가용성 집합이 포털의 드롭다운 목록에 없는 경우 다른 리소스 그룹에 만들었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-155">When you create a VM, if the availability set you want isn't in the drop-down list in the portal you may have created it in a different resource group.</span></span> <span data-ttu-id="dea6d-156">가용성 집합에 대한 리소스 그룹을 모르는 경우 허브 메뉴로 이동한 후 찾아보기 > 가용성 집합을 클릭하여 가용성 집합 및 해당 집합이 속하는 리소스 그룹 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-156">If you don't know the resource group for your availability set, go to the hub menu and click Browse > Availability sets to see a list of your availability sets and which resource groups they belong to.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dea6d-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dea6d-157">Next steps</span></span>
<span data-ttu-id="dea6d-158">[데이터 디스크](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 더 추가하여 VM에 저장소를 좀 더 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dea6d-158">Add additional storage to your VM by adding an additional [data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


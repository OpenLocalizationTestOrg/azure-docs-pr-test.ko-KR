---
title: "Azure에서 VM 가용성 aaaCreate 설정 | Microsoft Docs"
description: "어떻게 toocreate 관리 되는 가용성 설정 하거나 관리 되지 않는 가용성 Azure PowerShell을 사용 하 여 가상 컴퓨터에 대 한 설정 또는 hello hello 리소스 관리자 배포 모델에서 포털에 알아봅니다."
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
ms.openlocfilehash: eadcdfcd28bb2fa21a4647f207b390c33e022ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a><span data-ttu-id="a5f1f-104">Azure 가용성 집합을 만들어 VM 가용성 향상</span><span class="sxs-lookup"><span data-stu-id="a5f1f-104">Increase VM availability by creating an Azure availability set</span></span> 
<span data-ttu-id="a5f1f-105">가용성 집합 중복 tooyour 응용 프로그램을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-105">Availability sets provide redundancy tooyour application.</span></span> <span data-ttu-id="a5f1f-106">둘 이상의 가상 컴퓨터를 가용성 집합으로 그룹화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-106">We recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="a5f1f-107">이 구성을 통해 계획 되거나 계획 되지 않은 유지 관리 이벤트 중 하나에서 가상 컴퓨터를 하나 이상 있게 되며, 사용 가능 하 고 충족 hello 99.95% Azure SLA 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-107">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine will be available and meet hello 99.95% Azure SLA.</span></span> <span data-ttu-id="a5f1f-108">자세한 내용은 참조 hello [가상 컴퓨터에 대 한 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-108">For more information, see hello [SLA for Virtual Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a5f1f-109">Vm에에서 만들어야 hello 동일 hello 가용성 집합으로 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-109">VMs must be created in hello same resource group as hello availability set.</span></span>
> 

<span data-ttu-id="a5f1f-110">가용성 집합의 VM toobe 파트를 표시할 경우 toocreate hello 가용성 설정 하는 동안 첫 번째 또는 첫 번째 VM에에서 만드는 hello 집합.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-110">If you want your VM toobe part of an availability set, you need toocreate hello availability set first or while you are creating your first VM in hello set.</span></span> <span data-ttu-id="a5f1f-111">VM 디스크 관리를 사용 하는 경우 hello 가용성 집합 관리 되는 가용성 집합으로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-111">If your VM will be using Managed Disks, hello availability set must be created as a managed availability set.</span></span>

<span data-ttu-id="a5f1f-112">만들기 및 가용성 집합을 사용 하는 방법에 대 한 자세한 내용은 참조 [관리 가상 컴퓨터의 가용성을 hello](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-112">For more information about creating and using availability sets, see [Manage hello availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="use-hello-portal-toocreate-an-availability-set-before-creating-your-vms"></a><span data-ttu-id="a5f1f-113">Hello 포털 toocreate 가용성 집합에 Vm을 만들기 전에 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a5f1f-113">Use hello portal toocreate an availability set before creating your VMs</span></span>
1. <span data-ttu-id="a5f1f-114">Hello 허브 메뉴에서 클릭 **찾아보기** 선택 **가용성 집합**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-114">In hello hub menu, click **Browse** and select **Availability sets**.</span></span>
2. <span data-ttu-id="a5f1f-115">Hello에 **가용성 집합 블레이드**, 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-115">On hello **Availability sets blade**, click **Add**.</span></span>
   
    ![새 가용성 집합을 만들기 위한 단추를 추가 하는 hello를 보여 주는 스크린 샷.](./media/create-availability-set/add-availability-set.png)
3. <span data-ttu-id="a5f1f-117">Hello에 **가용성 집합 만들기** 블레이드, 사용자 집합에 대 한 전체 hello 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-117">On hello **Create availability set** blade, complete hello information for your set.</span></span>
   
    ![Hello tooenter toocreate hello 가용성 필요한 정보를 표시 하는 스크린 샷 설정 합니다.](./media/create-availability-set/create-availability-set.png)
   
   * <span data-ttu-id="a5f1f-119">**이름** -hello 이름은 숫자, 문자, 마침표, 밑줄 및 대시만 구성 하는 1-80 자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-119">**Name** - hello name should be 1-80 characters made up of numbers, letters, periods, underscores and dashes.</span></span> <span data-ttu-id="a5f1f-120">hello 첫 번째 문자는 문자 또는 숫자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-120">hello first character must be a letter or number.</span></span> <span data-ttu-id="a5f1f-121">hello 마지막 문자는 문자, 숫자 또는 밑줄 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-121">hello last character must be a letter, number or underscore.</span></span>
   * <span data-ttu-id="a5f1f-122">**오류 도메인** -오류 도메인 공통 전원 원본과 네트워크 스위치를 공유 하는 가상 컴퓨터의 hello 그룹을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-122">**Fault domains** - fault domains define hello group of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="a5f1f-123">기본적으로 hello Vm toothree 오류 도메인에 걸쳐 분리 되어 및 변경 된 toobetween 1 및 3 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-123">By default, hello VMs  are separated across up toothree fault domains and can be changed toobetween 1 and 3.</span></span>
   * <span data-ttu-id="a5f1f-124">**업데이트 도메인** -5 개의 업데이트 도메인이 기본적으로 할당 되 고 1에서 20 toobetween 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-124">**Update domains** -  five update domains are assigned by default and this can be set toobetween 1 and 20.</span></span> <span data-ttu-id="a5f1f-125">업데이트 도메인 hello에서 다시 부팅 해야 하는 기본 실제 하드웨어와 가상 컴퓨터 그룹을 나타내는 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-125">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="a5f1f-126">예를 들어 5 개의 업데이트 도메인을 6 개 이상의 가상 컴퓨터는 단일 가용 세트 hello 여섯 번째 가상 컴퓨터 내에서 구성 된 경우에 배치 됨 hello hello 첫 번째 가상 컴퓨터와 동일한 업데이트 도메인 hello 일곱 번째에서 지정 하는 경우 hello 동일 두 번째 가상 컴퓨터 hello 등으로 UD 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-126">For example, if we specify five update domains, when more than five virtual machines are configured within a single Availability Set, hello sixth virtual machine will be placed into hello same update domain as hello first virtual machine, hello seventh in hello same UD as hello second virtual machine, and so on.</span></span> <span data-ttu-id="a5f1f-127">hello 재부팅 hello 순서 순차적, 되지 않을 수 있지만 한 번에 하나의 업데이트 도메인을 다시 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-127">hello order of hello reboots may not be sequential, but only one update domain will be rebooted at a time.</span></span>
   * <span data-ttu-id="a5f1f-128">**구독** -선택 hello 구독 toouse 여러 개 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-128">**Subscription** - select hello subscription toouse if you have more than one.</span></span>
   * <span data-ttu-id="a5f1f-129">**리소스 그룹** -hello 화살표를 클릭 하 고 hello에서 리소스 그룹을 선택 하 여 기존 리소스 그룹의 드롭다운 목록 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-129">**Resource group** - select an existing resource group by clicking hello arrow and selecting a resource group from hello drop down.</span></span> <span data-ttu-id="a5f1f-130">또한 이름을 입력하여 새 리소스 그룹을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-130">You can also create a new resource group by typing in a name.</span></span> <span data-ttu-id="a5f1f-131">hello 이름에 포함할 수 있는 문자 hello: 문자, 숫자, 마침표, 대시, 밑줄 및 opening 또는 닫는 괄호입니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-131">hello name can contain any of hello following characters: letters, numbers, periods, dashes, underscores and opening or closing parenthesis.</span></span> <span data-ttu-id="a5f1f-132">hello 이름은 마침표로 끝날 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-132">hello name cannot end in a period.</span></span> <span data-ttu-id="a5f1f-133">모든 hello 가용성 그룹에 Vm hello 필요 toobe hello에서 만든 가용성 집합 hello와 동일한 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-133">All of hello VMs in hello availability group need toobe created in hello same resource group as hello availability set.</span></span>
   * <span data-ttu-id="a5f1f-134">**위치** -hello 드롭다운 목록에서 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-134">**Location** - select a location from hello drop-down.</span></span>
   * <span data-ttu-id="a5f1f-135">**관리 되는** -선택 *예* toocreate 관리 되는 가용성 집합 관리 하는 디스크 저장소를 사용 하는 Vm과 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-135">**Managed** - select *Yes* toocreate a managed availability set toouse with VMs that use Managed Disks for storage.</span></span> <span data-ttu-id="a5f1f-136">선택 **아니요** hello Vm hello 집합에 있는 경우 저장소 계정에 관리 되지 않는 디스크를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-136">Select **No** if hello VMs that will be in hello set use unmanaged disks in a storage account.</span></span>
   
4. <span data-ttu-id="a5f1f-137">Hello 정보를 모두 입력 작업을 완료 하면 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-137">When you are done entering hello information, click **Create**.</span></span> 

## <a name="use-hello-portal-toocreate-a-virtual-machine-and-an-availability-set-at-hello-same-time"></a><span data-ttu-id="a5f1f-138">가상 컴퓨터와 가용성 동일 하 게 설정 hello에 hello 포털 toocreate를 사용 하 여 시간</span><span class="sxs-lookup"><span data-stu-id="a5f1f-138">Use hello portal toocreate a virtual machine and an availability set at hello same time</span></span>
<span data-ttu-id="a5f1f-139">Hello 포털을 사용 하 여 새 VM을 만들면 hello를 만드는 동안 hello VM에 대해 설정할 새 가용성 만들 수도 있습니다 hello 집합의 첫 번째 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-139">If you are creating a new VM using hello portal, you can also create a new availability set for hello VM while you create hello first VM in hello set.</span></span> <span data-ttu-id="a5f1f-140">VM에 대 한 toouse 관리 하는 디스크를 선택 하면 관리 되는 가용성 집합 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-140">If you choose toouse Managed Disks for your VM, a managed availability set will be created.</span></span>

![새 유지를 hello VM을 만드는 동안 설정 hello 프로세스를 보여 주는 스크린 샷](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-tooan-existing-availability-set-in-hello-portal"></a><span data-ttu-id="a5f1f-142">새 VM tooan 기존 가용성 집합 hello 포털에서 추가</span><span class="sxs-lookup"><span data-stu-id="a5f1f-142">Add a new VM tooan existing availability set in hello portal</span></span>
<span data-ttu-id="a5f1f-143">각 VM에 대해 추가 만들면 hello 집합에 속하는, 만드는 것에 있는지 확인 해야 하는 동일한 hello **리소스 그룹** 다음 선택 hello 3 단계에서에서 설정 하는 기존 가용성 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-143">For each additional VM that you create that should belong in hello set, make sure that you create it in hello same **resource group** and then select hello existing availability set in Step 3.</span></span> 

![기존 가용성 tooselect toouse VM에 대 한 설정 하는 방법을 보여 주는 스크린샷](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-toocreate-an-availability-set"></a><span data-ttu-id="a5f1f-145">PowerShell toocreate 가용성을 사용 하 여 설정</span><span class="sxs-lookup"><span data-stu-id="a5f1f-145">Use PowerShell toocreate an availability set</span></span>
<span data-ttu-id="a5f1f-146">이 예에서는 가용성 명명 된 집합을 만듭니다 **myAvailabilitySet** hello에 **myResourceGroup** hello의 리소스 그룹 **West US** 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-146">This example creates an availability set named **myAvailabilitySet** in hello **myResourceGroup** resource group in hello **West US** location.</span></span> <span data-ttu-id="a5f1f-147">이 테스트 toobe hello를 만들기 전에 수행 해야 hello 집합에 있는 첫 번째 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-147">This needs toobe done before you create hello first VM that will be in hello set.</span></span>

<span data-ttu-id="a5f1f-148">시작 하기 전에 hello hello AzureRM.Compute PowerShell 모듈의 최신 버전이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-148">Before you begin, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="a5f1f-149">실행 명령 tooinstall 다음 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-149">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="a5f1f-150">자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-150">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


<span data-ttu-id="a5f1f-151">VM에 관리 디스크를 사용하는 경우 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-151">If you are using managed disks for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

<span data-ttu-id="a5f1f-152">VM에 사용자 고유의 저장소 계정을 사용하는 경우 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-152">If you are using your own storage accounts for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

<span data-ttu-id="a5f1f-153">자세한 내용은 [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-153">For more information, see [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="a5f1f-154">문제 해결</span><span class="sxs-lookup"><span data-stu-id="a5f1f-154">Troubleshooting</span></span>
* <span data-ttu-id="a5f1f-155">만들 때 VM에 사용할 가용성 집합을 hello hello 포털에서 hello 드롭 다운 목록에 없으면 만들었을 수 것 다른 리소스 그룹에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-155">When you create a VM, if hello availability set you want isn't in hello drop-down list in hello portal you may have created it in a different resource group.</span></span> <span data-ttu-id="a5f1f-156">가능 여부에 대 한 hello 리소스 그룹 설정 toohello 허브 메뉴를 이동 하 고 찾아보기를 클릭 하 여 알 수 없는 경우 > 가용성 집합 toosee 목록이 가능 여부를 설정 하 고 있는 리소스 그룹에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-156">If you don't know hello resource group for your availability set, go toohello hub menu and click Browse > Availability sets toosee a list of your availability sets and which resource groups they belong to.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5f1f-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a5f1f-157">Next steps</span></span>
<span data-ttu-id="a5f1f-158">추가 추가 하 여 추가 저장소 tooyour VM을 추가할 [데이터 디스크](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="a5f1f-158">Add additional storage tooyour VM by adding an additional [data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


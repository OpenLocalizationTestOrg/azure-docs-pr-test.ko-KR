---
title: "Azure PowerShell hello 사용 하 여 사용자 지정 VM 이미지를 aaaCreate | Microsoft Docs"
description: "자습서-hello Azure PowerShell을 사용 하 여 사용자 지정 VM 이미지를 만듭니다."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 3a759fe1b7e7b72f531399b0f4a99e341713c6a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a><span data-ttu-id="68051-103">PowerShell을 사용하여 Azure VM의 사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="68051-103">Create a custom image of an Azure VM using PowerShell</span></span>

<span data-ttu-id="68051-104">사용자 지정 이미지는 Marketplace 이미지와 같지만 직접 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68051-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="68051-105">사용자 지정 이미지에는 응용 프로그램, 응용 프로그램 구성 및 기타 운영 체제 구성을 미리 로드 하는 등 사용된 toobootstrap 구성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68051-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="68051-106">이 자습서에서는 Azure Virtual Machines의 사용자 지정 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68051-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="68051-107">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="68051-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="68051-108">VM Sysprep 및 일반화</span><span class="sxs-lookup"><span data-stu-id="68051-108">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="68051-109">사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="68051-109">Create a custom image</span></span>
> * <span data-ttu-id="68051-110">사용자 지정 이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="68051-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="68051-111">구독에서 모든 hello 이미지 나열</span><span class="sxs-lookup"><span data-stu-id="68051-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="68051-112">이미지 삭제</span><span class="sxs-lookup"><span data-stu-id="68051-112">Delete an image</span></span>

<span data-ttu-id="68051-113">이 자습서는 Azure PowerShell 모듈 버전 3.6 이상 hello가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="68051-114">실행 ` Get-Module -ListAvailable AzureRM` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="68051-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="68051-115">Tooupgrade 필요한 경우 참조 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="68051-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="68051-116">Before you begin</span></span>

<span data-ttu-id="68051-117">다음 hello 단계 tootake 기존 VM 및 설정에 재사용 가능한 사용자 지정 이미지를 toocreate 새 VM 인스턴스 사용 방법을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="68051-118">이 자습서에서는 toocomplete hello 예제에서는 기존 가상 컴퓨터 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="68051-119">필요한 경우 이 [스크립트 샘플](../scripts/virtual-machines-windows-powershell-sample-create-vm.md)을 사용하여 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68051-119">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="68051-120">Hello 자습서를 통해 작업 대체 필요한 경우 hello 리소스 그룹 및 VM 이름 합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="prepare-vm"></a><span data-ttu-id="68051-121">VM 준비</span><span class="sxs-lookup"><span data-stu-id="68051-121">Prepare VM</span></span>

<span data-ttu-id="68051-122">가상 컴퓨터의 이미지 toocreate tooprepare hello VM 일반화 hello VM 할당 해제, 한 다음 Azure에서 일반화 된 것과 같이 VM hello 소스를 표시 하 여 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-122">toocreate an image of a virtual machine, you need tooprepare hello VM by generalizing hello VM, deallocating, and then marking hello source VM as generalized in Azure.</span></span>

### <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="68051-123">일반화 hello Sysprep를 사용 하 여 Windows VM</span><span class="sxs-lookup"><span data-stu-id="68051-123">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="68051-124">Sysprep는 특히, 모든 개인 계정 정보를 제거 하 고 이미지 형식으로 사용 되는 hello 컴퓨터 toobe를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-124">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="68051-125">Sysprep에 대 한 세부 정보를 참조 하십시오. [어떻게 tooUse Sysprep: 소개](http://technet.microsoft.com/library/bb457073.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-125">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>


1. <span data-ttu-id="68051-126">Toohello 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-126">Connect toohello virtual machine.</span></span>
2. <span data-ttu-id="68051-127">Hello 명령 프롬프트 창을 관리자 권한으로 엽니다.</span><span class="sxs-lookup"><span data-stu-id="68051-127">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="68051-128">Hello 디렉터리도 변경*%windir%\system32\sysprep*, 한 다음 실행 *sysprep.exe*합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-128">Change hello directory too*%windir%\system32\sysprep*, and then run *sysprep.exe*.</span></span>
3. <span data-ttu-id="68051-129">Hello에 **시스템 준비 도구** 대화 상자에서 *입력 시스템을 기본 OOBE (Experience)*, 해당 hello 있는지 확인 하 고 *일반화* 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-129">In hello **System Preparation Tool** dialog box, select *Enter System Out-of-Box Experience (OOBE)*, and make sure that hello *Generalize* check box is selected.</span></span>
4. <span data-ttu-id="68051-130">**종료 옵션**에서 *종료*를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-130">In **Shutdown Options**, select *Shutdown* and then click **OK**.</span></span>
5. <span data-ttu-id="68051-131">Sysprep이 완료 된 hello 가상 컴퓨터를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-131">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="68051-132">**Hello VM 다시 시작 하지 않으면**합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-132">**Do not restart hello VM**.</span></span>

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="68051-133">할당을 취소 하 고 hello VM 일반화 된 대로 표시</span><span class="sxs-lookup"><span data-stu-id="68051-133">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="68051-134">이미지 toocreate hello VM toobe 할당 취소 되 고 Azure에서 일반화 한 것으로 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-134">toocreate an image, hello VM needs toobe deallocated and marked as generalized in Azure.</span></span>

<span data-ttu-id="68051-135">사용 하 여 할당 취소 된 hello VM [중지 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm)합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-135">Deallocated hello VM using [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

<span data-ttu-id="68051-136">Hello 가상 컴퓨터의 hello 상태를 너무 설정`-Generalized` 를 사용 하 여 [집합 AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm)합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-136">Set hello status of hello virtual machine too`-Generalized` using [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span></span> 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a><span data-ttu-id="68051-137">Hello 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="68051-137">Create hello image</span></span>

<span data-ttu-id="68051-138">이제를 사용 하 여 hello VM의 이미지를 만들 수 [새로 AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) 및 [새로 AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage)합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-138">Now you can create an image of hello VM by using [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) and [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span></span> <span data-ttu-id="68051-139">hello 다음 예제에서는 명명 된 이미지 *myImage* 라는 VM에서 *myVM*합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-139">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>

<span data-ttu-id="68051-140">Hello 가상 컴퓨터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="68051-140">Get hello virtual machine.</span></span> 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

<span data-ttu-id="68051-141">Hello 이미지 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68051-141">Create hello image configuration.</span></span>

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

<span data-ttu-id="68051-142">Hello 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68051-142">Create hello image.</span></span>

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="68051-143">Hello 이미지에서 Vm 만들기</span><span class="sxs-lookup"><span data-stu-id="68051-143">Create VMs from hello image</span></span>

<span data-ttu-id="68051-144">이미지를가지고 hello 이미지에서 하나 이상의 새 Vm을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68051-144">Now that you have an image, you can create one or more new VMs from hello image.</span></span> <span data-ttu-id="68051-145">사용자 지정 이미지에서 VM 만들기는 매우 유사한 toocreating 마켓플레이스 이미지를 사용 하는 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="68051-145">Creating a VM from a custom image is very similar toocreating a VM using a Marketplace image.</span></span> <span data-ttu-id="68051-146">마켓플레이스 이미지를 사용 하면 hello 이미지, 이미지 공급자, 제품, SKU 및 버전에 대 한 tooinformation을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-146">When you use a Marketplace image, you have tooinformation about hello image, image provider, offer, SKU and version.</span></span> <span data-ttu-id="68051-147">사용자 지정 이미지를 사용 하기만 하면 hello 사용자 지정 이미지 리소스의 tooprovide hello ID입니다.</span><span class="sxs-lookup"><span data-stu-id="68051-147">With a custom image, you just need tooprovide hello ID of hello custom image resource.</span></span> 

<span data-ttu-id="68051-148">다음 스크립트는 hello, 변수 만듭니다 *$image* toostore hello 사용자 지정 이미지를 사용 하는 방법은 [Get AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) 데 사용 되는 다음 [집합-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)hello를 사용 하 여 hello ID를 지정 하 고 *$image* 변수 방금 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-148">In hello following script, we create a variable *$image* toostore information about hello custom image using [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) and then we use [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) and specify hello ID using hello *$image* variable we just created.</span></span> 

<span data-ttu-id="68051-149">hello 스크립트 라는 VM 만듭니다 *myVMfromImage* 라는 새 리소스 그룹에는 사용자 지정 이미지에서 *myResourceGroupFromImage* hello에 *West US* 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-149">hello script creates a VM named *myVMfromImage* from our custom image in a new resource group named *myResourceGroupFromImage* in hello *West US* location.</span></span>


```powershell
$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

New-AzureRmResourceGroup -Name myResourceGroupFromImage -Location EastUS

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name "mypublicdns$(Get-Random)" `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4

  $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

  $nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$vmConfig = New-AzureRmVMConfig `
    -VMName myVMfromImage `
    -VMSize Standard_D1 | Set-AzureRmVMOperatingSystem -Windows `
        -ComputerName myComputer `
        -Credential $cred 

# Here is where we create a variable toostore information about hello image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want toocreate hello VM from and image and provide hello image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a><span data-ttu-id="68051-150">이미지 관리</span><span class="sxs-lookup"><span data-stu-id="68051-150">Image management</span></span> 

<span data-ttu-id="68051-151">다음은 일반 관리 이미지 작업의 몇 가지 예제와 방법을 toocomplete PowerShell을 사용 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-151">Here are some examples of common management image tasks and how toocomplete them using PowerShell.</span></span>

<span data-ttu-id="68051-152">이름별로 모든 이미지를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-152">List all images by name.</span></span>

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

<span data-ttu-id="68051-153">이미지 삭제를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-153">Delete an image.</span></span> <span data-ttu-id="68051-154">이 예에서는 삭제 hello 라는 이미지 *myOldImage* hello에서 *myResourceGroup*합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-154">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="68051-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="68051-155">Next steps</span></span>

<span data-ttu-id="68051-156">이 자습서에서는 사용자 지정 VM 이미지를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="68051-156">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="68051-157">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="68051-157">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="68051-158">VM Sysprep 및 일반화</span><span class="sxs-lookup"><span data-stu-id="68051-158">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="68051-159">사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="68051-159">Create a custom image</span></span>
> * <span data-ttu-id="68051-160">사용자 지정 이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="68051-160">Create a VM from a custom image</span></span>
> * <span data-ttu-id="68051-161">구독에서 모든 hello 이미지 나열</span><span class="sxs-lookup"><span data-stu-id="68051-161">List all hello images in your subscription</span></span>
> * <span data-ttu-id="68051-162">이미지 삭제</span><span class="sxs-lookup"><span data-stu-id="68051-162">Delete an image</span></span>

<span data-ttu-id="68051-163">어떻게 항상 사용 가능한 가상 컴퓨터에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68051-163">Advance toohello next tutorial toolearn about how highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="68051-164">항상 사용 가능한 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="68051-164">Create highly available VMs</span></span>](tutorial-availability-sets.md)




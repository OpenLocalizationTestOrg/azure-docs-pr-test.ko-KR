---
title: "Azure PowerShell을 사용하여 사용자 지정 VM 이미지 만들기 | Microsoft Docs"
description: "자습서 - Azure PowerShell을 사용하여 사용자 지정 VM 이미지 만들기"
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
ms.openlocfilehash: 96be2872a902a7d7063bf1dff7b4ca209a5b67c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a><span data-ttu-id="ab742-103">PowerShell을 사용하여 Azure VM의 사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="ab742-103">Create a custom image of an Azure VM using PowerShell</span></span>

<span data-ttu-id="ab742-104">사용자 지정 이미지는 Marketplace 이미지와 같지만 직접 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="ab742-105">응용 프로그램 사전 로드, 응용 프로그램 구성 및 기타 OS 구성과 같은 부트스트랩 구성에 사용자 지정 이미지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-105">Custom images can be used to bootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="ab742-106">이 자습서에서는 Azure Virtual Machines의 사용자 지정 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="ab742-107">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ab742-108">VM Sysprep 및 일반화</span><span class="sxs-lookup"><span data-stu-id="ab742-108">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="ab742-109">사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="ab742-109">Create a custom image</span></span>
> * <span data-ttu-id="ab742-110">사용자 지정 이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="ab742-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="ab742-111">구독에 모든 이미지 나열</span><span class="sxs-lookup"><span data-stu-id="ab742-111">List all the images in your subscription</span></span>
> * <span data-ttu-id="ab742-112">이미지 삭제</span><span class="sxs-lookup"><span data-stu-id="ab742-112">Delete an image</span></span>

<span data-ttu-id="ab742-113">이 자습서에는 Azure PowerShell 모듈 버전 3.6 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="ab742-114">` Get-Module -ListAvailable AzureRM`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="ab742-115">업그레이드해야 하는 경우 [Azure PowerShell 모듈 설치](/powershell/azure/install-azurerm-ps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab742-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ab742-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="ab742-116">Before you begin</span></span>

<span data-ttu-id="ab742-117">아래 단계에서는 기존 VM을 가져와서 새 VM 인스턴스를 만드는 데 사용할 수 있는 재사용 가능 사용자 지정 이미지로 변환하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-117">The steps below detail how to take an existing VM and turn it into a re-usable custom image that you can use to create new VM instances.</span></span>

<span data-ttu-id="ab742-118">이 자습서의 예제를 완료하려면 기존 가상 컴퓨터가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-118">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="ab742-119">필요한 경우 이 [스크립트 샘플](../scripts/virtual-machines-windows-powershell-sample-create-vm.md)을 사용하여 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-119">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="ab742-120">이 자습서를 진행할 때 필요한 경우 리소스 그룹 및 VM 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-120">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

## <a name="prepare-vm"></a><span data-ttu-id="ab742-121">VM 준비</span><span class="sxs-lookup"><span data-stu-id="ab742-121">Prepare VM</span></span>

<span data-ttu-id="ab742-122">가상 컴퓨터의 이미지를 만들려면 VM을 일반화하고 할당을 취소한 후 Azure에서 원본 VM을 일반화된 것으로 표시하여 VM을 준비해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-122">To create an image of a virtual machine, you need to prepare the VM by generalizing the VM, deallocating, and then marking the source VM as generalized in Azure.</span></span>

### <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="ab742-123">Sysprep을 사용하여 Windows VM 일반화</span><span class="sxs-lookup"><span data-stu-id="ab742-123">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="ab742-124">Sysprep은 여러 정보 중에서 모든 개인 계정 정보를 제거하고 이미지로 사용할 컴퓨터를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-124">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="ab742-125">Sysprep에 대한 자세한 내용은 [Sysprep 사용 방법: 소개](http://technet.microsoft.com/library/bb457073.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab742-125">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>


1. <span data-ttu-id="ab742-126">가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-126">Connect to the virtual machine.</span></span>
2. <span data-ttu-id="ab742-127">관리자로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-127">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="ab742-128">디렉터리를 *%windir%\system32\sysprep*로 변경한 후 *sysprep.exe*를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-128">Change the directory to *%windir%\system32\sysprep*, and then run *sysprep.exe*.</span></span>
3. <span data-ttu-id="ab742-129">**시스템 준비 도구** 대화 상자에서 *시스템 OOBE(첫 실행 경험) 입력*을 선택하고 *일반화* 확인란을 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-129">In the **System Preparation Tool** dialog box, select *Enter System Out-of-Box Experience (OOBE)*, and make sure that the *Generalize* check box is selected.</span></span>
4. <span data-ttu-id="ab742-130">**종료 옵션**에서 *종료*를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-130">In **Shutdown Options**, select *Shutdown* and then click **OK**.</span></span>
5. <span data-ttu-id="ab742-131">Sysprep이 완료되면 가상 컴퓨터를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-131">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="ab742-132">**VM을 다시 시작하지 마세요**.</span><span class="sxs-lookup"><span data-stu-id="ab742-132">**Do not restart the VM**.</span></span>

### <a name="deallocate-and-mark-the-vm-as-generalized"></a><span data-ttu-id="ab742-133">할당을 취소하고 VM을 일반화된 것으로 표시</span><span class="sxs-lookup"><span data-stu-id="ab742-133">Deallocate and mark the VM as generalized</span></span>

<span data-ttu-id="ab742-134">이미지를 만들려면 VM의 할당을 취소하고 Azure에서 일반화된 것으로 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-134">To create an image, the VM needs to be deallocated and marked as generalized in Azure.</span></span>

<span data-ttu-id="ab742-135">[Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm)을 사용하여 VM의 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-135">Deallocated the VM using [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

<span data-ttu-id="ab742-136">[Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm)을 사용하여 가상 컴퓨터의 상태를 `-Generalized`으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-136">Set the status of the virtual machine to `-Generalized` using [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span></span> 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-the-image"></a><span data-ttu-id="ab742-137">이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="ab742-137">Create the image</span></span>

<span data-ttu-id="ab742-138">이제 [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) 및 [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage)를 사용하여 VM 이미지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-138">Now you can create an image of the VM by using [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) and [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span></span> <span data-ttu-id="ab742-139">다음 예제에서는 *myVM*이라는 VM에서 *myImage*라는 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-139">The following example creates an image named *myImage* from a VM named *myVM*.</span></span>

<span data-ttu-id="ab742-140">가상 컴퓨터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-140">Get the virtual machine.</span></span> 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

<span data-ttu-id="ab742-141">이미지 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-141">Create the image configuration.</span></span>

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

<span data-ttu-id="ab742-142">이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-142">Create the image.</span></span>

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-the-image"></a><span data-ttu-id="ab742-143">이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="ab742-143">Create VMs from the image</span></span>

<span data-ttu-id="ab742-144">이미지가 생겼으니, 이 이미지에서 하나 이상의 새 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-144">Now that you have an image, you can create one or more new VMs from the image.</span></span> <span data-ttu-id="ab742-145">사용자 지정 이미지에서 VM을 만드는 방법은 Marketplace 이미지를 사용하여 VM을 만드는 방법과 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-145">Creating a VM from a custom image is very similar to creating a VM using a Marketplace image.</span></span> <span data-ttu-id="ab742-146">Marketplace 이미지를 사용하는 경우 이미지, 이미지 공급자, 제품, SKU 및 버전에 대한 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-146">When you use a Marketplace image, you have to information about the image, image provider, offer, SKU and version.</span></span> <span data-ttu-id="ab742-147">사용자 지정 이미지를 사용하는 경우 사용자 지정 이미지 리소스의 ID만 제공하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-147">With a custom image, you just need to provide the ID of the custom image resource.</span></span> 

<span data-ttu-id="ab742-148">다음 스크립트에서는 [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage)를 사용하여 사용자 지정 이미지에 대한 정보를 저장하는 *$image* 변수를 만든 다음 [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)를 사용하고 방금 만든 *$image* 변수를 사용하여 ID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-148">In the following script, we create a variable *$image* to store information about the custom image using [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) and then we use [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) and specify the ID using the *$image* variable we just created.</span></span> 

<span data-ttu-id="ab742-149">이 스크립트는 *미국 서부* 위치의 새 리소스 그룹 *myResourceGroupFromImage*에 있는 사용자 지정 이미지로 *myVMfromImage*라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-149">The script creates a VM named *myVMfromImage* from our custom image in a new resource group named *myResourceGroupFromImage* in the *West US* location.</span></span>


```powershell
$cred = Get-Credential -Message "Enter a username and password for the virtual machine."

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

# Here is where we create a variable to store information about the image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want to create the VM from and image and provide the image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a><span data-ttu-id="ab742-150">이미지 관리</span><span class="sxs-lookup"><span data-stu-id="ab742-150">Image management</span></span> 

<span data-ttu-id="ab742-151">일반적인 이미지 관리 작업의 몇 가지 예제와 PowerShell을 사용하여 완료하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-151">Here are some examples of common management image tasks and how to complete them using PowerShell.</span></span>

<span data-ttu-id="ab742-152">이름별로 모든 이미지를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-152">List all images by name.</span></span>

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

<span data-ttu-id="ab742-153">이미지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-153">Delete an image.</span></span> <span data-ttu-id="ab742-154">이 예제에서는 *myResourceGroup*에서 *myOldImage*라는 이미지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-154">This example deletes the image named *myOldImage* from the *myResourceGroup*.</span></span>

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="ab742-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ab742-155">Next steps</span></span>

<span data-ttu-id="ab742-156">이 자습서에서는 사용자 지정 VM 이미지를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-156">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="ab742-157">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-157">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ab742-158">VM Sysprep 및 일반화</span><span class="sxs-lookup"><span data-stu-id="ab742-158">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="ab742-159">사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="ab742-159">Create a custom image</span></span>
> * <span data-ttu-id="ab742-160">사용자 지정 이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="ab742-160">Create a VM from a custom image</span></span>
> * <span data-ttu-id="ab742-161">구독에 모든 이미지 나열</span><span class="sxs-lookup"><span data-stu-id="ab742-161">List all the images in your subscription</span></span>
> * <span data-ttu-id="ab742-162">이미지 삭제</span><span class="sxs-lookup"><span data-stu-id="ab742-162">Delete an image</span></span>

<span data-ttu-id="ab742-163">고가용성 Virtual Machines에 대해 자세히 알아보려면 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ab742-163">Advance to the next tutorial to learn about how highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ab742-164">항상 사용 가능한 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="ab742-164">Create highly available VMs</span></span>](tutorial-availability-sets.md)




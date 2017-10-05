---
title: "Azure에서 여러 NIC를 사용하는 Windows VM 만들기 및 관리 | Microsoft Docs"
description: "Azure PowerShell 또는 Resource Manager 템플릿을 사용하여 여러 NIC가 연결된 Windows VM을 만들고 관리하는 방법을 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 3bd99a67dae41de3533d7f6e244eb7ee3ecc4049
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a><span data-ttu-id="0d674-103">여러 NIC가 있는 Windows 가상 컴퓨터 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="0d674-103">Create and manage a Windows virtual machine that has multiple NICs</span></span>
<span data-ttu-id="0d674-104">Azure의 VM(가상 컴퓨터)에는 여러 가상 NIC(네트워크 인터페이스 카드)가 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-104">Virtual machines (VMs) in Azure can have multiple virtual network interface cards (NICs) attached to them.</span></span> <span data-ttu-id="0d674-105">일반적인 시나리오는 프런트 엔드 및 백 엔드 연결에 다른 서브넷을 사용하거나 모니터링 또는 백업 솔루션 전용 네트워크를 두는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="0d674-106">이 문서에서는 여러 NIC가 연결된 VM을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-106">This article details how to create a VM that has multiple NICs attached to it.</span></span> <span data-ttu-id="0d674-107">또한 기존 VM에서 NIC를 추가하거나 제거하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-107">You also learn how to add or remove NICs from an existing VM.</span></span> <span data-ttu-id="0d674-108">[VM 크기](sizes.md) 가 다르면 다양한 NIC가 지원되므로 그에 따라 VM 크기를 지정하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="0d674-109">자체 PowerShell 스크립트 내에서 여러 NIC를 만드는 방법을 비롯한 자세한 내용은 [다중 NIC VM 배포](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d674-109">For detailed information, including how to create multiple NICs within your own PowerShell scripts, see [deploying multiple-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d674-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0d674-110">Prerequisites</span></span>
<span data-ttu-id="0d674-111">먼저 [최신 버전의 Azure PowerShell을 설치 및 구성](/powershell/azure/overview)했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-111">Make sure that you have the [latest Azure PowerShell version installed and configured](/powershell/azure/overview).</span></span>

<span data-ttu-id="0d674-112">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-112">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="0d674-113">예제 매개 변수 이름에는 *myResourceGroup*, *myVnet*, *myVM*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-113">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>


## <a name="create-a-vm-with-multiple-nics"></a><span data-ttu-id="0d674-114">여러 NIC를 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="0d674-114">Create a VM with multiple NICs</span></span>
<span data-ttu-id="0d674-115">먼저 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-115">First, create a resource group.</span></span> <span data-ttu-id="0d674-116">다음 예제에서는 *EastUs* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-116">The following example creates a resource group named *myResourceGroup* in the *EastUs* location:</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a><span data-ttu-id="0d674-117">가상 네트워크 및 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="0d674-117">Create virtual network and subnets</span></span>
<span data-ttu-id="0d674-118">일반적인 시나리오는 가상 네트워크에 두 개 이상의 서브넷이 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-118">A common scenario is for a virtual network to have two or more subnets.</span></span> <span data-ttu-id="0d674-119">하나의 서브넷은 프런트 엔드 트래픽용이고, 다른 서브넷은 백 엔드 트래픽용일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-119">One subnet may be for front-end traffic, the other for back-end traffic.</span></span> <span data-ttu-id="0d674-120">두 서브넷 모두에 연결하려면 VM에서 여러 NIC를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-120">To connect to both subnets, you then use multiple NICs on your VM.</span></span>

1. <span data-ttu-id="0d674-121">[New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig)를 사용하여 두 개의 가상 네트워크 서브넷을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-121">Define two virtual network subnets with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="0d674-122">다음 예제에서는 *mySubnetFrontEnd* 및 *mySubnetBackEnd*에 대한 서브넷을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-122">The following example defines the subnets for *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. <span data-ttu-id="0d674-123">[New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork)를 사용하여 가상 네트워크 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-123">Create your virtual network and subnets with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="0d674-124">다음 예제에서는 *myVnet*이라는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-124">The following example creates a virtual network named *myVnet*:</span></span>

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a><span data-ttu-id="0d674-125">여러 NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="0d674-125">Create multiple NICs</span></span>
<span data-ttu-id="0d674-126">[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface)를 사용하여 두 개의 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-126">Create two NICs with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="0d674-127">하나의 NIC를 프런트 엔드 서브넷에, 다른 NIC를 백 엔드 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-127">Attach one NIC to the front-end subnet and one NIC to the back-end subnet.</span></span> <span data-ttu-id="0d674-128">다음 예제에서는 *myNIC1* 및 *myNIC2*라는 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-128">The following example creates NICs named *myNic1* and *myNic2*:</span></span>

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic1" `
    -Location "EastUs" `
    -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic2" `
    -Location "EastUs" `
    -SubnetId $backEnd.Id
```

<span data-ttu-id="0d674-129">또한 일반적으로 [네트워크 보안 그룹](../../virtual-network/virtual-networks-nsg.md) 또는 [부하 분산 장치](../../load-balancer/load-balancer-overview.md)를 만들어 VM에서 트래픽을 관리하고 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-129">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="0d674-130">[좀 더 자세한 다중 NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) 문서에서 네트워크 보안 그룹 생성 및 NIC 할당에 대해 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-130">The [more detailed multiple-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a network security group and assigning NICs.</span></span>

### <a name="create-the-virtual-machine"></a><span data-ttu-id="0d674-131">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="0d674-131">Create the virtual machine</span></span>
<span data-ttu-id="0d674-132">이제 VM 구성 빌드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-132">Now start to build your VM configuration.</span></span> <span data-ttu-id="0d674-133">VM 크기마다 VM에 추가할 수 있는 NIC의 총수가 제한되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-133">Each VM size has a limit for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="0d674-134">자세한 내용은 [Windows VM 크기](sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d674-134">For more information, see [Windows VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="0d674-135">다음과 같이 `$cred` 변수에 VM 자격 증명을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-135">Set your VM credentials to the `$cred` variable as follows:</span></span>

    ```powershell
    $cred = Get-Credential
    ```

2. <span data-ttu-id="0d674-136">[New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig)를 사용하여 VM을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-136">Define your VM with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span></span> <span data-ttu-id="0d674-137">다음 예제에서는 *myVM*이라는 VM을 정의하고 2개 이상의 NIC를 지원하는 VM 크기(*Standard_DS3_v2*)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-137">The following example defines a VM named *myVM* and uses a VM size that supports more than two NICs (*Standard_DS3_v2*):</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. <span data-ttu-id="0d674-138">[Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) 및 [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)를 사용하여 나머지 VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-138">Create the rest of your VM configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) and [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span></span> <span data-ttu-id="0d674-139">다음 예제에서는 Windows Server 2016 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-139">The following example creates a Windows Server 2016 VM:</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
        -Windows `
        -ComputerName "myVM" `
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
        -PublisherName "MicrosoftWindowsServer" `
        -Offer "WindowsServer" `
        -Skus "2016-Datacenter" `
        -Version "latest"
   ```

4. <span data-ttu-id="0d674-140">[Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface)를 사용하여 이전에 만든 두 NIC를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-140">Attach the two NICs that you previously created with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. <span data-ttu-id="0d674-141">마지막으로 [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)을 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-141">Finally, create your VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-to-an-existing-vm"></a><span data-ttu-id="0d674-142">기존 VM에 NIC 추가</span><span class="sxs-lookup"><span data-stu-id="0d674-142">Add a NIC to an existing VM</span></span>
<span data-ttu-id="0d674-143">기존 VM에 가상 NIC를 추가하고 VM을 할당 취소하고 가상 NIC를 추가한 다음 VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-143">To add a virtual NIC to an existing VM, you deallocate the VM, add the virtual NIC, then start the VM.</span></span>

1. <span data-ttu-id="0d674-144">[Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm)을 사용하여 VM을 할당 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-144">Deallocate the VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="0d674-145">다음 예제에서는 *myResourceGroup*에서 *myVM*이라는 VM의 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-145">The following example deallocates the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="0d674-146">[Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm)을 사용하여 VM의 기존 구성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-146">Get the existing configuration of the VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="0d674-147">다음 예제에서는 *myResourceGroup*에서 *myVM*이라는 VM에 대한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-147">The following example gets information for the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="0d674-148">다음 예제에서는 *mySubnetBackEnd*에 연결된 *myNIC3*이라는 [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface)를 사용하여 가상 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-148">The following example creates a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) named *myNic3* that is attached to *mySubnetBackEnd*.</span></span> <span data-ttu-id="0d674-149">그런 다음 [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface)를 사용하여 *myResourceGroup*에서 *myVM*이라는 VM에 가상 NIC를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-149">The virtual NIC is then attached to the VM named *myVM* in *myResourceGroup* with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    # Get info for the back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get the ID of the new virtual NIC and add to VM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a><span data-ttu-id="0d674-150">기본 가상 NIC</span><span class="sxs-lookup"><span data-stu-id="0d674-150">Primary virtual NICs</span></span>
    <span data-ttu-id="0d674-151">다중 NIC VM의 NIC 중 하나는 기본 NIC여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-151">One of the NICs on a multi-NIC VM needs to be primary.</span></span> <span data-ttu-id="0d674-152">VM의 기존 가상 NIC 중 하나가 이미 기본 NIC로 설정되어 있는 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-152">If one of the existing virtual NICs on the VM is already set as primary, you can skip this step.</span></span> <span data-ttu-id="0d674-153">다음 예제에서는 VM에 두 개의 가상 NIC가 있고 첫 번째 NIC(`[0]`)를 기본 NIC로 추가하려고 하는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-153">The following example assumes that two virtual NICs are now present on a VM and you wish to add the first NIC (`[0]`) as the primary:</span></span>
        
    ```powershell
    # List existing NICs on the VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 to be primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update the VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. <span data-ttu-id="0d674-154">[Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm)을 사용하여 VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-154">Start the VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a><span data-ttu-id="0d674-155">기존 VM에서 NIC 제거</span><span class="sxs-lookup"><span data-stu-id="0d674-155">Remove a NIC from an existing VM</span></span>
<span data-ttu-id="0d674-156">기존 VM에서 가상 NIC를 제거하고 VM을 할당 취소하고 가상 NIC를 제거한 다음 VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-156">To remove a virtual NIC from an existing VM, you deallocate the VM, remove the virtual NIC, then start the VM.</span></span>

1. <span data-ttu-id="0d674-157">[Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm)을 사용하여 VM을 할당 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-157">Deallocate the VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="0d674-158">다음 예제에서는 *myResourceGroup*에서 *myVM*이라는 VM의 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-158">The following example deallocates the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="0d674-159">[Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm)을 사용하여 VM의 기존 구성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-159">Get the existing configuration of the VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="0d674-160">다음 예제에서는 *myResourceGroup*에서 *myVM*이라는 VM에 대한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-160">The following example gets information for the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="0d674-161">[Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface)를 사용하여 NIC에 대한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-161">Get information about the NIC remove with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span></span> <span data-ttu-id="0d674-162">다음 예제에서는 *myNic3*에 대한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-162">The following example gets information about *myNic3*:</span></span>

    ```powershell
    # List existing NICs on the VM if you need to determine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. <span data-ttu-id="0d674-163">[Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface)를 사용하여 NIC를 제거하고 [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm)을 사용하여 VM을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-163">Remove the NIC with [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) and then update the VM with [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span></span> <span data-ttu-id="0d674-164">다음 예제에서는 이전 단계에서 `$nicId`를 사용하여 가져온 *myNic3*을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-164">The following example removes *myNic3* as obtained by `$nicId` in the preceding step:</span></span>

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. <span data-ttu-id="0d674-165">[Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm)을 사용하여 VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-165">Start the VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a><span data-ttu-id="0d674-166">템플릿을 사용하여 여러 NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="0d674-166">Create multiple NICs with templates</span></span>
<span data-ttu-id="0d674-167">Azure Resource Manager 템플릿은 여러 NIC를 만드는 것과 같이 배포하는 동안 리소스의 여러 인스턴스를 만드는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-167">Azure Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="0d674-168">Resource Manager 템플릿은 선언적 JSON 파일을 사용하여 환경을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-168">Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="0d674-169">자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d674-169">For more information, see [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="0d674-170">*복사* 를 사용하여 만들 인스턴스 수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-170">You can use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="0d674-171">자세한 내용은 [*copy*를 사용하여 여러 인스턴스 만들기](../../resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d674-171">For more information, see [creating multiple instances by using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="0d674-172">`copyIndex()`를 사용하여 리소스 이름에 숫자를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-172">You can also use `copyIndex()` to append a number to a resource name.</span></span> <span data-ttu-id="0d674-173">그런 다음 *myNic1*, *MyNic2* 등을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-173">You can then create *myNic1*, *MyNic2* and so on.</span></span> <span data-ttu-id="0d674-174">다음 코드는 인덱스 값을 추가하는 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-174">The following code shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="0d674-175">[Resource Manager 템플릿을 사용하여 여러 NIC 만들기](../../virtual-network/virtual-network-deploy-multinic-arm-template.md)의 전체 예제를 읽어볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-175">You can read a complete example of [creating multiple NICs by using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d674-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0d674-176">Next steps</span></span>
<span data-ttu-id="0d674-177">여러 NIC가 있는 VM을 만들 때 [Windows VM 크기](sizes.md)를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-177">Review [Windows VM sizes](sizes.md) when you're trying to create a VM that has multiple NICs.</span></span> <span data-ttu-id="0d674-178">각 VM 크기가 지원하는 NIC의 최대 수에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="0d674-178">Pay attention to the maximum number of NICs that each VM size supports.</span></span> 



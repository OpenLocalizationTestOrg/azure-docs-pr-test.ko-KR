---
title: "aaaCreate 여러 Nic를 사용 하는 Azure에서 Windows Vm 관리 및 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate 및 Azure PowerShell 또는 리소스 관리자 템플릿을 사용 하 여 여러 Nic 연결 된 tooit가 있는 Windows VM을 관리 합니다."
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
ms.openlocfilehash: c3c7d7569aca6f047238146d84b2ffccf05d4079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a><span data-ttu-id="ed0ec-103">여러 NIC가 있는 Windows 가상 컴퓨터 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="ed0ec-103">Create and manage a Windows virtual machine that has multiple NICs</span></span>
<span data-ttu-id="ed0ec-104">Azure의 가상 컴퓨터 (Vm)에 여러 가상 네트워크 인터페이스 카드 (Nic) 연결 된 toothem이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-104">Virtual machines (VMs) in Azure can have multiple virtual network interface cards (NICs) attached toothem.</span></span> <span data-ttu-id="ed0ec-105">일반적인 시나리오는 toohave 프런트 엔드 및 백 엔드 연결에 대 한 서로 다른 서브넷 또는 네트워크를 전용 tooa 모니터링 또는 백업 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="ed0ec-106">이 문서는 여러 Nic가 있는 VM으로 toocreate tooit를 연결 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-106">This article details how toocreate a VM that has multiple NICs attached tooit.</span></span> <span data-ttu-id="ed0ec-107">또한 학습 방법을 기존 VM에서 Nic tooadd 또는 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-107">You also learn how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="ed0ec-108">[VM 크기](sizes.md) 가 다르면 다양한 NIC가 지원되므로 그에 따라 VM 크기를 지정하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="ed0ec-109">자세한 내용은 toocreate 사용자만 PowerShell 스크립트 내에서 여러 Nic를 확인 하려면 어떻게 비롯 한 [다중 NIC Vm을 배포](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-109">For detailed information, including how toocreate multiple NICs within your own PowerShell scripts, see [deploying multiple-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed0ec-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ed0ec-110">Prerequisites</span></span>
<span data-ttu-id="ed0ec-111">Hello 갖도록 [최신 Azure PowerShell 버전 설치 및 구성](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-111">Make sure that you have hello [latest Azure PowerShell version installed and configured](/powershell/azure/overview).</span></span>

<span data-ttu-id="ed0ec-112">Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="ed0ec-113">예제 매개 변수 이름에는 *myResourceGroup*, *myVnet*, *myVM*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-113">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>


## <a name="create-a-vm-with-multiple-nics"></a><span data-ttu-id="ed0ec-114">여러 NIC를 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="ed0ec-114">Create a VM with multiple NICs</span></span>
<span data-ttu-id="ed0ec-115">먼저 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-115">First, create a resource group.</span></span> <span data-ttu-id="ed0ec-116">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *EastUs* 위치:</span><span class="sxs-lookup"><span data-stu-id="ed0ec-116">hello following example creates a resource group named *myResourceGroup* in hello *EastUs* location:</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a><span data-ttu-id="ed0ec-117">가상 네트워크 및 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="ed0ec-117">Create virtual network and subnets</span></span>
<span data-ttu-id="ed0ec-118">가상 네트워크 toohave에 대 한 일반적인 시나리오는 두 개 이상의 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-118">A common scenario is for a virtual network toohave two or more subnets.</span></span> <span data-ttu-id="ed0ec-119">백 엔드 트래픽에 대 한 다른 hello 프런트 엔드 트래픽용 서브넷 1 개 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-119">One subnet may be for front-end traffic, hello other for back-end traffic.</span></span> <span data-ttu-id="ed0ec-120">tooconnect tooboth 서브넷 있습니다 다음 사용 하 여 여러 Nic VM에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-120">tooconnect tooboth subnets, you then use multiple NICs on your VM.</span></span>

1. <span data-ttu-id="ed0ec-121">[New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig)를 사용하여 두 개의 가상 네트워크 서브넷을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-121">Define two virtual network subnets with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="ed0ec-122">hello 다음 예제에서는 정의 대 한 hello 서브넷 *mySubnetFrontEnd* 및 *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="ed0ec-122">hello following example defines hello subnets for *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. <span data-ttu-id="ed0ec-123">[New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork)를 사용하여 가상 네트워크 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-123">Create your virtual network and subnets with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="ed0ec-124">hello 다음 예제에서는 가상 네트워크를 만들어 명명 된 *myVnet*:</span><span class="sxs-lookup"><span data-stu-id="ed0ec-124">hello following example creates a virtual network named *myVnet*:</span></span>

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a><span data-ttu-id="ed0ec-125">여러 NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="ed0ec-125">Create multiple NICs</span></span>
<span data-ttu-id="ed0ec-126">[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface)를 사용하여 두 개의 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-126">Create two NICs with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="ed0ec-127">NIC toohello 프런트 엔드 서브넷과 NIC toohello 백 엔드 서브넷이 둘을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-127">Attach one NIC toohello front-end subnet and one NIC toohello back-end subnet.</span></span> <span data-ttu-id="ed0ec-128">hello 다음 예제에서는 명명 된 Nic *myNic1* 및 *myNic2*:</span><span class="sxs-lookup"><span data-stu-id="ed0ec-128">hello following example creates NICs named *myNic1* and *myNic2*:</span></span>

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

<span data-ttu-id="ed0ec-129">또한 만들 일반적으로 [네트워크 보안 그룹](../../virtual-network/virtual-networks-nsg.md) 또는 [부하 분산 장치](../../load-balancer/load-balancer-overview.md) toohelp 관리 하 고 Vm에 트래픽을 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-129">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="ed0ec-130">hello [다중 NIC VM 상세](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) 문서를 안내 하는 네트워크 보안 그룹을 만들고 Nic에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-130">hello [more detailed multiple-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a network security group and assigning NICs.</span></span>

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="ed0ec-131">Hello 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="ed0ec-131">Create hello virtual machine</span></span>
<span data-ttu-id="ed0ec-132">이제 toobuild VM 구성을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-132">Now start toobuild your VM configuration.</span></span> <span data-ttu-id="ed0ec-133">각 VM 크기 hello tooa VM을 추가할 수 있는 Nic의 총 수에 대 한 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-133">Each VM size has a limit for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="ed0ec-134">자세한 내용은 [Windows VM 크기](sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-134">For more information, see [Windows VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="ed0ec-135">VM 자격 증명 toohello 설정 `$cred` 다음과 같이 변수:</span><span class="sxs-lookup"><span data-stu-id="ed0ec-135">Set your VM credentials toohello `$cred` variable as follows:</span></span>

    ```powershell
    $cred = Get-Credential
    ```

2. <span data-ttu-id="ed0ec-136">[New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig)를 사용하여 VM을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-136">Define your VM with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span></span> <span data-ttu-id="ed0ec-137">hello 다음 예제에서는 정의 라는 VM *myVM* 지 원하는 Nic 두 개 이상의 VM 크기를 사용 하 여 (*Standard_DS3_v2*):</span><span class="sxs-lookup"><span data-stu-id="ed0ec-137">hello following example defines a VM named *myVM* and uses a VM size that supports more than two NICs (*Standard_DS3_v2*):</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. <span data-ttu-id="ed0ec-138">사용 하 여 VM 구성의 hello 나머지 만들기 [집합 AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) 및 [집합 AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-138">Create hello rest of your VM configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) and [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span></span> <span data-ttu-id="ed0ec-139">다음 예제는 hello는 Windows Server 2016 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-139">hello following example creates a Windows Server 2016 VM:</span></span>

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

4. <span data-ttu-id="ed0ec-140">사용 하 여 이전에 만든 hello 두 Nic 연결 [추가 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="ed0ec-140">Attach hello two NICs that you previously created with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. <span data-ttu-id="ed0ec-141">마지막으로 [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)을 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-141">Finally, create your VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a><span data-ttu-id="ed0ec-142">기존 VM NIC tooan 추가</span><span class="sxs-lookup"><span data-stu-id="ed0ec-142">Add a NIC tooan existing VM</span></span>
<span data-ttu-id="ed0ec-143">VM을 hello deallocate VM 기존 가상 NIC tooan, tooadd 추가 hello 가상 NIC를 다음 hello VM을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-143">tooadd a virtual NIC tooan existing VM, you deallocate hello VM, add hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="ed0ec-144">Deallocate의 VM hello [중지 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-144">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="ed0ec-145">hello 다음 예제에서는 할당 취소 hello 라는 VM *myVM* 에 *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="ed0ec-145">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="ed0ec-146">Hello hello VM의 기존 구성을 가져올와 [Get AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-146">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="ed0ec-147">hello 다음 예제에서는 가져옵니다 hello 라는 VM에 대 한 정보 *myVM* 에 *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="ed0ec-147">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="ed0ec-148">hello 다음 예제에서는 가상 NIC와 [새로 AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) 라는 *myNic3* 너무 연결 된*mySubnetBackEnd*합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-148">hello following example creates a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) named *myNic3* that is attached too*mySubnetBackEnd*.</span></span> <span data-ttu-id="ed0ec-149">가상 NIC가 다음 hello toohello 라는 VM 연결 *myVM* 에 *myResourceGroup* 와 [추가 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="ed0ec-149">hello virtual NIC is then attached toohello VM named *myVM* in *myResourceGroup* with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    # Get info for hello back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get hello ID of hello new virtual NIC and add tooVM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a><span data-ttu-id="ed0ec-150">기본 가상 NIC</span><span class="sxs-lookup"><span data-stu-id="ed0ec-150">Primary virtual NICs</span></span>
    <span data-ttu-id="ed0ec-151">다중 NIC VM에서 Nic hello 중 toobe 주가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-151">One of hello NICs on a multi-NIC VM needs toobe primary.</span></span> <span data-ttu-id="ed0ec-152">기존 가상 Nic를 hello 중 하나에 hello VM 이미 설정 되어 기본으로,이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-152">If one of hello existing virtual NICs on hello VM is already set as primary, you can skip this step.</span></span> <span data-ttu-id="ed0ec-153">hello 다음 예에서는 가정 두 개의 가상 Nic가 VM에 있으면 이제 및 tooadd 원하는 첫 번째 NIC hello (`[0]`) 기본 hello로:</span><span class="sxs-lookup"><span data-stu-id="ed0ec-153">hello following example assumes that two virtual NICs are now present on a VM and you wish tooadd hello first NIC (`[0]`) as hello primary:</span></span>
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. <span data-ttu-id="ed0ec-154">시작의 VM hello [시작 AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="ed0ec-154">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a><span data-ttu-id="ed0ec-155">기존 VM에서 NIC 제거</span><span class="sxs-lookup"><span data-stu-id="ed0ec-155">Remove a NIC from an existing VM</span></span>
<span data-ttu-id="ed0ec-156">가상 NIC tooremove 기존 VM에서 VM hello 할당을 취소 하면,이 hello 제거 가상 NIC를 다음 시작 hello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-156">tooremove a virtual NIC from an existing VM, you deallocate hello VM, remove hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="ed0ec-157">Deallocate의 VM hello [중지 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-157">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="ed0ec-158">hello 다음 예제에서는 할당 취소 hello 라는 VM *myVM* 에 *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="ed0ec-158">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="ed0ec-159">Hello hello VM의 기존 구성을 가져올와 [Get AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-159">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="ed0ec-160">hello 다음 예제에서는 가져옵니다 hello 라는 VM에 대 한 정보 *myVM* 에 *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="ed0ec-160">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="ed0ec-161">Hello와 NIC를 제거 하는 방법에 대 한 정보를 가져올 [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-161">Get information about hello NIC remove with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span></span> <span data-ttu-id="ed0ec-162">hello 다음 정보를 가져오는 예제에 대 한 *myNic3*:</span><span class="sxs-lookup"><span data-stu-id="ed0ec-162">hello following example gets information about *myNic3*:</span></span>

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. <span data-ttu-id="ed0ec-163">제거 인 NIC와 hello [제거 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) 및 hello 사용 하 여 VM을 업데이트 합니다 [업데이트 AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-163">Remove hello NIC with [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) and then update hello VM with [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span></span> <span data-ttu-id="ed0ec-164">hello 다음 예제에서는 제거 *myNic3* 여 얻어지는 `$nicId` hello 앞 단계에서에서:</span><span class="sxs-lookup"><span data-stu-id="ed0ec-164">hello following example removes *myNic3* as obtained by `$nicId` in hello preceding step:</span></span>

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. <span data-ttu-id="ed0ec-165">시작의 VM hello [시작 AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="ed0ec-165">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a><span data-ttu-id="ed0ec-166">템플릿을 사용하여 여러 NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="ed0ec-166">Create multiple NICs with templates</span></span>
<span data-ttu-id="ed0ec-167">Azure 리소스 관리자 템플릿 방식으로 toocreate 리소스의 여러 인스턴스가 여러 Nic를 만들 때 처럼 배포 하는 동안 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-167">Azure Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="ed0ec-168">리소스 관리자 템플릿을 선언적 JSON 파일 toodefine 환경의 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-168">Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="ed0ec-169">자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-169">For more information, see [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="ed0ec-170">사용할 수 있습니다 *복사* 인스턴스 toocreate toospecify hello 수:</span><span class="sxs-lookup"><span data-stu-id="ed0ec-170">You can use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="ed0ec-171">자세한 내용은 [*copy*를 사용하여 여러 인스턴스 만들기](../../resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-171">For more information, see [creating multiple instances by using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="ed0ec-172">사용할 수도 있습니다 `copyIndex()` tooappend 번호 tooa 리소스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-172">You can also use `copyIndex()` tooappend a number tooa resource name.</span></span> <span data-ttu-id="ed0ec-173">그런 다음 *myNic1*, *MyNic2* 등을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-173">You can then create *myNic1*, *MyNic2* and so on.</span></span> <span data-ttu-id="ed0ec-174">hello 다음 코드 예제를 hello 인덱스 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-174">hello following code shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="ed0ec-175">[Resource Manager 템플릿을 사용하여 여러 NIC 만들기](../../virtual-network/virtual-network-deploy-multinic-arm-template.md)의 전체 예제를 읽어볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-175">You can read a complete example of [creating multiple NICs by using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed0ec-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ed0ec-176">Next steps</span></span>
<span data-ttu-id="ed0ec-177">검토 [Windows VM 크기](sizes.md) toocreate 여러 Nic가 VM을 시도 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-177">Review [Windows VM sizes](sizes.md) when you're trying toocreate a VM that has multiple NICs.</span></span> <span data-ttu-id="ed0ec-178">주의 기울여야 toohello 최대 있는 Nic 수가 각 VM 크기를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0ec-178">Pay attention toohello maximum number of NICs that each VM size supports.</span></span> 



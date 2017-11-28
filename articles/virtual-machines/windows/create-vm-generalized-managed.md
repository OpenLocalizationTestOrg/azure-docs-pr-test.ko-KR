---
title: "Azure에서 관리 VM 이미지로 VM 만들기 | Microsoft Docs"
description: "Resource Manager 배포 모델에서 Azure PowerShell을 사용하여 일반화된 관리 VM 이미지로 Windows 가상 컴퓨터를 만듭니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 2bb2d66271178a64ec0f4642e46b23f5618a56d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-vm-from-a-managed-image"></a><span data-ttu-id="a744f-103">관리되는 이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="a744f-103">Create a VM from a managed image</span></span>

<span data-ttu-id="a744f-104">Azure에서 관리 VM 이미지로 여러 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-104">You can create multiple VMs from a managed VM image in Azure.</span></span> <span data-ttu-id="a744f-105">관리 VM 이미지는 OS 및 데이터 디스크를 비롯하여 VM을 만드는 데 필요한 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-105">A managed VM image contains the information necessary to create a VM, including the OS and data disks.</span></span> <span data-ttu-id="a744f-106">OS 디스크와 데이터 디스크를 포함하여 이미지를 구성하는 VHD는 관리 디스크로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-106">The VHDs that make up the image, including both the OS disks and any data disks, are stored as managed disks.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="a744f-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a744f-107">Prerequisites</span></span>

<span data-ttu-id="a744f-108">새 VM을 만들려면 [만들어 놓은 관리 VM 이미지가 있어야 합니다](capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="a744f-108">You need to have already [created a managed VM image](capture-image-resource.md) to use for creating the new VM.</span></span> 

<span data-ttu-id="a744f-109">최신 버전의 AzureRM.Compute 및 AzureRM.Network PowerShell 모듈을 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-109">Make sure that you have the latest versions of the AzureRM.Compute and AzureRM.Network PowerShell modules.</span></span> <span data-ttu-id="a744f-110">관리자 권한으로 PowerShell 프롬프트를 열고 다음 명령을 실행하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-110">Open a PowerShell prompt as an Administrator and run the following command to install them.</span></span>

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
<span data-ttu-id="a744f-111">자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a744f-111">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>



## <a name="collect-information-about-the-image"></a><span data-ttu-id="a744f-112">이미지에 대한 정보 수집</span><span class="sxs-lookup"><span data-stu-id="a744f-112">Collect information about the image</span></span>

<span data-ttu-id="a744f-113">먼저 이미지에 대한 기본 정보를 수집하고 이미지의 변수를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-113">First we need to gather basic information about the image and create a variable for the image.</span></span> <span data-ttu-id="a744f-114">이 예제에서는 **미국 중서부** 위치의 **myResourceGroup** 리소스 그룹에 있는 **myImage**라는 관리되는 VM 이미지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-114">This example uses a managed VM image named **myImage** that is in the **myResourceGroup** resource group in the **West Central US** location.</span></span> 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="a744f-115">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="a744f-115">Create a virtual network</span></span>
<span data-ttu-id="a744f-116">[가상 네트워크](../../virtual-network/virtual-networks-overview.md)의 vNet 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-116">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="a744f-117">서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-117">Create the subnet.</span></span> <span data-ttu-id="a744f-118">이 예제에서는 주소 접두사로 **10.0.0.0/24**를 사용하는 **mySubnet**이라는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-118">This example creates a subnet named **mySubnet** with the address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="a744f-119">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="a744f-119">Create the virtual network.</span></span> <span data-ttu-id="a744f-120">이 예제에서는 주소 접두사로 **10.0.0.0/16**을 사용하는 **myVnet**이라는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-120">This example creates a virtual network named **myVnet** with the address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="a744f-121">공용 IP 주소 및 네트워크 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="a744f-121">Create a public IP address and network interface</span></span>

<span data-ttu-id="a744f-122">가상 네트워크에서 가상 컴퓨터와 통신하려면 [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) 및 네트워크 인터페이스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-122">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="a744f-123">공용 IP 주소 만들기.</span><span class="sxs-lookup"><span data-stu-id="a744f-123">Create a public IP address.</span></span> <span data-ttu-id="a744f-124">이 예에서는 **myPip**라는 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-124">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="a744f-125">NIC 만들기.</span><span class="sxs-lookup"><span data-stu-id="a744f-125">Create the NIC.</span></span> <span data-ttu-id="a744f-126">이 예에서는 **myNic**라는 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-126">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="a744f-127">네트워크 보안 그룹 및 RDP 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="a744f-127">Create the network security group and an RDP rule</span></span>

<span data-ttu-id="a744f-128">RDP를 사용하여 VM에 로그인할 수 있으려면 포트 3389에 대한 RDP 액세스를 허용하는 NSG(네트워크 보안 규칙)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-128">To be able to log in to your VM using RDP, you need to have a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="a744f-129">이 예에서는 포트 3389를 통한 RDP 트래픽을 허용하는 **myRdpRule**이라는 규칙을 포함하는 **myNsg**로 명명된 NSG를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-129">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="a744f-130">NSG에 대한 자세한 내용은 [PowerShell을 사용하여 Azure에서 VM으로 포트 열기](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a744f-130">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="a744f-131">가상 네트워크에 대한 변수 만들기</span><span class="sxs-lookup"><span data-stu-id="a744f-131">Create a variable for the virtual network</span></span>

<span data-ttu-id="a744f-132">완료된 가상 네트워크에 대한 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-132">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-the-credentials-for-the-vm"></a><span data-ttu-id="a744f-133">VM에 대한 자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="a744f-133">Get the credentials for the VM</span></span>

<span data-ttu-id="a744f-134">다음 cmdlet을 사용하면 VM에 원격으로 액세스하기 위해 로컬 관리자 계정으로 사용할 새 사용자 이름 및 암호를 입력할 수 있는 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-134">The following cmdlet will open a window where you will enter a new user name and password to use as the local administrator account for remotely accessing the VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-the-vm-name-computer-name-and-the-size-of-the-vm"></a><span data-ttu-id="a744f-135">VM 이름, 컴퓨터 이름 및 VM 크기에 대한 변수 설정</span><span class="sxs-lookup"><span data-stu-id="a744f-135">Set variables for the VM name, computer name and the size of the VM</span></span>

1. <span data-ttu-id="a744f-136">VM 이름 및 컴퓨터 이름에 대한 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-136">Create variables for the VM name and computer name.</span></span> <span data-ttu-id="a744f-137">이 예제에서는 VM 이름을 **myVM**으로 설정하고 컴퓨터 이름을 **myComputer**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-137">This example sets the VM name as **myVM** and the computer name as **myComputer**.</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. <span data-ttu-id="a744f-138">가상 컴퓨터의 크기를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-138">Set the size of the virtual machine.</span></span> <span data-ttu-id="a744f-139">이 예제에서는 **Standard_DS1_v2** 크기의 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-139">This example creates **Standard_DS1_v2** sized VM.</span></span> <span data-ttu-id="a744f-140">자세한 내용은 [VM 크기](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a744f-140">See the [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span></span>

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. <span data-ttu-id="a744f-141">VM 구성에 VM의 이름과 크기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-141">Add the VM name and size to the VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-the-vm-image-as-source-image-for-the-new-vm"></a><span data-ttu-id="a744f-142">새 VM에 대한 원본 이미지로 VM 이미지 설정</span><span class="sxs-lookup"><span data-stu-id="a744f-142">Set the VM image as source image for the new VM</span></span>

<span data-ttu-id="a744f-143">관리되는 VM 이미지의 ID를 사용하여 원본 이미지를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-143">Set the source image using the ID of the managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-the-os-configuration-and-add-the-nic"></a><span data-ttu-id="a744f-144">OS 구성을 설정하고 NIC를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-144">Set the OS configuration and add the NIC.</span></span>

<span data-ttu-id="a744f-145">저장소 유형(PremiumLRS 또는 StandardLRS) 및 OS 디스크의 크기를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-145">Enter the storage type (PremiumLRS or StandardLRS) and the size of the OS disk.</span></span> <span data-ttu-id="a744f-146">이 예제에서는 계정 유형을 **PremiumLRS**로, 디스크 크기를 **128GB**로, 디스크 캐싱을 **ReadWrite**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-146">This example sets the account type to **PremiumLRS**, the disk size to **128 GB** and disk caching to **ReadWrite**.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-the-vm"></a><span data-ttu-id="a744f-147">VM 만들기</span><span class="sxs-lookup"><span data-stu-id="a744f-147">Create the VM</span></span>

<span data-ttu-id="a744f-148">이전에 작성하여 **$vm** 변수에 저장한 구성을 사용하여 새 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-148">Create the new Vm using the configuration that we have built and stored in the **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="a744f-149">VM이 만들어졌는지 확인</span><span class="sxs-lookup"><span data-stu-id="a744f-149">Verify that the VM was created</span></span>
<span data-ttu-id="a744f-150">완료되면 새로 만든 VM은 [Azure 포털](https://portal.azure.com)에서 **찾아보기** > **가상 컴퓨터**에 표시되며 다음 PowerShell 명령을 사용해도 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a744f-150">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="a744f-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a744f-151">Next steps</span></span>
<span data-ttu-id="a744f-152">Azure PowerShell을 사용하여 새 가상 컴퓨터를 관리하려면 [Azure PowerShell 모듈을 사용하여 Windows VM 만들기 및 관리](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a744f-152">To manage your new virtual machine with Azure PowerShell, see [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


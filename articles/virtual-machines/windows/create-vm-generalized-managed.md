---
title: "Azure에서 관리 되는 VM 이미지에서 VM aaaCreate | Microsoft Docs"
description: "Hello 리소스 관리자 배포 모델에서 Azure PowerShell을 사용 하는 일반화 된 관리 되는 VM 이미지에서 Windows 가상 컴퓨터를 만듭니다."
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
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a><span data-ttu-id="f8353-103">관리되는 이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="f8353-103">Create a VM from a managed image</span></span>

<span data-ttu-id="f8353-104">Azure에서 관리 VM 이미지로 여러 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-104">You can create multiple VMs from a managed VM image in Azure.</span></span> <span data-ttu-id="f8353-105">관리 되는 VM 이미지 hello 정보 필요한 toocreate hello OS 및 데이터 디스크를 포함 하 여 VM을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-105">A managed VM image contains hello information necessary toocreate a VM, including hello OS and data disks.</span></span> <span data-ttu-id="f8353-106">hello Vhd hello 운영 체제 디스크와 모든 데이터 디스크를 포함 하는 hello 이미지를 구성 하는 관리 되는 디스크도 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-106">hello VHDs that make up hello image, including both hello OS disks and any data disks, are stored as managed disks.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="f8353-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f8353-107">Prerequisites</span></span>

<span data-ttu-id="f8353-108">이미 toohave 필요한 [관리 되는 VM 이미지를 만들어](capture-image-resource.md) 작성용 toouse hello 새 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-108">You need toohave already [created a managed VM image](capture-image-resource.md) toouse for creating hello new VM.</span></span> 

<span data-ttu-id="f8353-109">Hello hello AzureRM.Compute 및 AzureRM.Network PowerShell 모듈의 최신 버전이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-109">Make sure that you have hello latest versions of hello AzureRM.Compute and AzureRM.Network PowerShell modules.</span></span> <span data-ttu-id="f8353-110">관리자 권한으로 PowerShell 프롬프트를 열고 다음 명령 tooinstall hello를 실행 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-110">Open a PowerShell prompt as an Administrator and run hello following command tooinstall them.</span></span>

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
<span data-ttu-id="f8353-111">자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8353-111">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>



## <a name="collect-information-about-hello-image"></a><span data-ttu-id="f8353-112">Hello 이미지에 대 한 정보를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-112">Collect information about hello image</span></span>

<span data-ttu-id="f8353-113">먼저 toogather hello 이미지에 대 한 기본 정보가 필요 하 고 hello 이미지에 대 한 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-113">First we need toogather basic information about hello image and create a variable for hello image.</span></span> <span data-ttu-id="f8353-114">이 예에서는 이라는 관리 되는 VM 이미지를 사용 하 여 **myImage** 에 hello 즉 **myResourceGroup** hello의 리소스 그룹 **중앙 미국 서 부** 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-114">This example uses a managed VM image named **myImage** that is in hello **myResourceGroup** resource group in hello **West Central US** location.</span></span> 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="f8353-115">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="f8353-115">Create a virtual network</span></span>
<span data-ttu-id="f8353-116">Hello vNet 및 hello의 서브넷을 만들 [가상 네트워크](../../virtual-network/virtual-networks-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-116">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="f8353-117">Hello 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-117">Create hello subnet.</span></span> <span data-ttu-id="f8353-118">이 예에서는 이라는 서브넷을 만듭니다 **mySubnet** hello 주소 접두사와 **10.0.0.0/24**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-118">This example creates a subnet named **mySubnet** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="f8353-119">Hello 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-119">Create hello virtual network.</span></span> <span data-ttu-id="f8353-120">이 예제에서는 명명 된 가상 네트워크를 만들어 **myVnet** hello 주소 접두사와 **10.0.0.0/16**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-120">This example creates a virtual network named **myVnet** with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="f8353-121">공용 IP 주소 및 네트워크 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="f8353-121">Create a public IP address and network interface</span></span>

<span data-ttu-id="f8353-122">필요한 tooenable hello 가상 네트워크의 hello 가상 컴퓨터와의 통신을는 [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) 및 네트워크 인터페이스.</span><span class="sxs-lookup"><span data-stu-id="f8353-122">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="f8353-123">공용 IP 주소 만들기.</span><span class="sxs-lookup"><span data-stu-id="f8353-123">Create a public IP address.</span></span> <span data-ttu-id="f8353-124">이 예에서는 **myPip**라는 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-124">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="f8353-125">Hello NIC. 만들기</span><span class="sxs-lookup"><span data-stu-id="f8353-125">Create hello NIC.</span></span> <span data-ttu-id="f8353-126">이 예에서는 **myNic**라는 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-126">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="f8353-127">Hello 네트워크 보안 그룹 및 RDP 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="f8353-127">Create hello network security group and an RDP rule</span></span>

<span data-ttu-id="f8353-128">toobe 수 toolog tooyour에서 RDP를 사용 하 여 VM을 toohave RDP 포트 3389에 대 한 액세스를 허용 하는 네트워크 보안 규칙 (NSG) 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-128">toobe able toolog in tooyour VM using RDP, you need toohave a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="f8353-129">이 예에서는 포트 3389를 통한 RDP 트래픽을 허용하는 **myRdpRule**이라는 규칙을 포함하는 **myNsg**로 명명된 NSG를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-129">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="f8353-130">Nsg에 대 한 자세한 내용은 참조 [PowerShell을 사용 하 여 Azure에서 VM 포트 tooa 여](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-130">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

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


## <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="f8353-131">Hello 가상 네트워크에 대 한 변수 만들기</span><span class="sxs-lookup"><span data-stu-id="f8353-131">Create a variable for hello virtual network</span></span>

<span data-ttu-id="f8353-132">가상 네트워크를 완료 하는 hello에 대 한 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-132">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a><span data-ttu-id="f8353-133">Hello VM에 대 한 hello 자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="f8353-133">Get hello credentials for hello VM</span></span>

<span data-ttu-id="f8353-134">hello 다음 cmdlet이 열립니다 입력할 수 있는 새 사용자 이름 및 암호 toouse hello 로컬 관리자 계정으로 원격으로 hello VM에 액세스 하기 위한 창.</span><span class="sxs-lookup"><span data-stu-id="f8353-134">hello following cmdlet will open a window where you will enter a new user name and password toouse as hello local administrator account for remotely accessing hello VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a><span data-ttu-id="f8353-135">Hello VM에 대 한 설정 변수 이름, 컴퓨터 이름 및 hello hello VM의 크기</span><span class="sxs-lookup"><span data-stu-id="f8353-135">Set variables for hello VM name, computer name and hello size of hello VM</span></span>

1. <span data-ttu-id="f8353-136">Hello VM 이름 및 컴퓨터 이름에 대 한 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-136">Create variables for hello VM name and computer name.</span></span> <span data-ttu-id="f8353-137">Hello VM 이름으로 설정 하는이 예제 **myVM** 및 컴퓨터 이름으로 hello **myComputer**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-137">This example sets hello VM name as **myVM** and hello computer name as **myComputer**.</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. <span data-ttu-id="f8353-138">Hello 가상 컴퓨터의 hello 크기를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-138">Set hello size of hello virtual machine.</span></span> <span data-ttu-id="f8353-139">이 예제에서는 **Standard_DS1_v2** 크기의 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-139">This example creates **Standard_DS1_v2** sized VM.</span></span> <span data-ttu-id="f8353-140">Hello 참조 [VM 크기](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) 자세한 정보에 대 한 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-140">See hello [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span></span>

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. <span data-ttu-id="f8353-141">Hello VM 이름 및 크기 toohello VM 구성에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-141">Add hello VM name and size toohello VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a><span data-ttu-id="f8353-142">Hello에 대 한 원본 이미지로 집합 hello VM 이미지 새 VM</span><span class="sxs-lookup"><span data-stu-id="f8353-142">Set hello VM image as source image for hello new VM</span></span>

<span data-ttu-id="f8353-143">관리 되는 hello VM 이미지의 hello ID를 사용 하 여 hello 소스 이미지를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-143">Set hello source image using hello ID of hello managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a><span data-ttu-id="f8353-144">운영 체제 구성 hello를 설정 하 고 hello NIC. 추가</span><span class="sxs-lookup"><span data-stu-id="f8353-144">Set hello OS configuration and add hello NIC.</span></span>

<span data-ttu-id="f8353-145">Hello 저장소 유형 (PremiumLRS 또는 StandardLRS)와 hello OS 디스크의 hello 크기를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-145">Enter hello storage type (PremiumLRS or StandardLRS) and hello size of hello OS disk.</span></span> <span data-ttu-id="f8353-146">이 예에서는 설정 hello 계정 유형 너무**PremiumLRS**, 디스크 크기를 너무 hello**128GB** 및 디스크 캐싱에 너무**ReadWrite**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-146">This example sets hello account type too**PremiumLRS**, hello disk size too**128 GB** and disk caching too**ReadWrite**.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a><span data-ttu-id="f8353-147">Hello VM 만들기</span><span class="sxs-lookup"><span data-stu-id="f8353-147">Create hello VM</span></span>

<span data-ttu-id="f8353-148">만들 작성 했으며 hello에 저장 하는 hello 구성을 사용 하 여 새 Vm hello **$vm** 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-148">Create hello new Vm using hello configuration that we have built and stored in hello **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="f8353-149">VM이 생성 되었고 해당 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-149">Verify that hello VM was created</span></span>
<span data-ttu-id="f8353-150">새로 만든 VM의 hello hello 나타나야 완료 되 면 [Azure 포털](https://portal.azure.com) 아래 **찾아보기** > **가상 컴퓨터**, 또는 hello 다음을 사용 하 여 PowerShell 명령:</span><span class="sxs-lookup"><span data-stu-id="f8353-150">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="f8353-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f8353-151">Next steps</span></span>
<span data-ttu-id="f8353-152">Azure PowerShell을 사용한 새 가상 컴퓨터에 참조 toomanage [만들기 hello Azure PowerShell 모듈을 사용 하 여 Windows Vm을 관리 하 고](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8353-152">toomanage your new virtual machine with Azure PowerShell, see [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


---
title: "Azure PowerShell 모듈을 사용하여 Windows VM 만들기 및 관리 | Microsoft Docs"
description: "자습서 - Azure PowerShell 모듈을 사용하여 Windows VM 만들기 및 관리"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ec1bb7834beb66dc28dd5b1db764bd358243292c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-windows-vms-with-the-azure-powershell-module"></a><span data-ttu-id="8a6d0-103">Azure PowerShell 모듈을 사용하여 Windows VM 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="8a6d0-103">Create and Manage Windows VMs with the Azure PowerShell module</span></span>

<span data-ttu-id="8a6d0-104">Azure Virtual Machines는 완전히 구성 가능하고 유연한 컴퓨팅 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="8a6d0-105">이 자습서에서는 VM 크기 선택, VM 이미지 선택 및 VM 배포 등 기본적인 Azure Virtual Machines 배포 항목에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="8a6d0-106">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8a6d0-107">VM 만들기 및 연결</span><span class="sxs-lookup"><span data-stu-id="8a6d0-107">Create and connect to a VM</span></span>
> * <span data-ttu-id="8a6d0-108">VM 이미지 선택 및 사용</span><span class="sxs-lookup"><span data-stu-id="8a6d0-108">Select and use VM images</span></span>
> * <span data-ttu-id="8a6d0-109">특정 VM 크기 보기 및 사용</span><span class="sxs-lookup"><span data-stu-id="8a6d0-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="8a6d0-110">VM 크기 조정</span><span class="sxs-lookup"><span data-stu-id="8a6d0-110">Resize a VM</span></span>
> * <span data-ttu-id="8a6d0-111">VM 상태 보기 및 이해</span><span class="sxs-lookup"><span data-stu-id="8a6d0-111">View and understand VM state</span></span>

<span data-ttu-id="8a6d0-112">이 자습서에는 Azure PowerShell 모듈 버전 3.6 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-112">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="8a6d0-113">` Get-Module -ListAvailable AzureRM`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-113">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="8a6d0-114">업그레이드해야 하는 경우 [Azure PowerShell 모듈 설치](/powershell/azure/install-azurerm-ps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-114">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="8a6d0-115">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="8a6d0-115">Create resource group</span></span>

<span data-ttu-id="8a6d0-116">[New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 명령으로 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-116">Create a resource group with the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> 

<span data-ttu-id="8a6d0-117">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="8a6d0-118">가상 컴퓨터보다 먼저 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="8a6d0-119">이 예제에서는 *EastUS* 지역에 *myResourceGroupVM*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-119">In this example, a resource group named *myResourceGroupVM* is created in the *EastUS* region.</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

<span data-ttu-id="8a6d0-120">리소스 그룹은 VM을 만들거나 수정할 때 지정되며 이 자습서 전체에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-120">The resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="8a6d0-121">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="8a6d0-121">Create virtual machine</span></span>

<span data-ttu-id="8a6d0-122">가상 컴퓨터는 가상 네트워크에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-122">A virtual machine must be connected to a virtual network.</span></span> <span data-ttu-id="8a6d0-123">가상 컴퓨터와는 공용 IP 주소를 사용하여 네트워크 인터페이스 카드를 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-123">You communicate with the virtual machine using a public IP address through a network interface card.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="8a6d0-124">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="8a6d0-124">Create virtual network</span></span>

<span data-ttu-id="8a6d0-125">[New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig)를 사용하여 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-125">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="8a6d0-126">[New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork)를 사용하여 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-126">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a><span data-ttu-id="8a6d0-127">공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="8a6d0-127">Create public IP address</span></span>

<span data-ttu-id="8a6d0-128">[New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)를 사용하여 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-128">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a><span data-ttu-id="8a6d0-129">네트워크 인터페이스 카드 만들기</span><span class="sxs-lookup"><span data-stu-id="8a6d0-129">Create network interface card</span></span>

<span data-ttu-id="8a6d0-130">[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface)를 사용하여 네트워크 인터페이스 카드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-130">Create a network interface card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a><span data-ttu-id="8a6d0-131">네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="8a6d0-131">Create network security group</span></span>

<span data-ttu-id="8a6d0-132">Azure NSG([네트워크 보안 그룹](../../virtual-network/virtual-networks-nsg.md))는 하나 또는 여러 가상 컴퓨터에 대한 인바운드 및 아웃바운드 트래픽을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-132">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="8a6d0-133">네트워크 보안 그룹 규칙은 특정 포트 또는 포트 범위에 대한 네트워크 트래픽을 허용하거나 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-133">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="8a6d0-134">이러한 규칙에는 미리 정의된 원본에서 시작되는 트래픽만 가상 컴퓨터와 통신할 수 있도록 원본 주소 접두사가 포함될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-134">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span> <span data-ttu-id="8a6d0-135">설치하는 IIS 웹 서버에 액세스하려면 인바운드 NSG 규칙을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-135">To access the IIS webserver that you are installing, you must add an inbound NSG rule.</span></span>

<span data-ttu-id="8a6d0-136">인바운드 NSG 규칙을 만들려면 [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-136">To create an inbound NSG rule, use [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="8a6d0-137">다음 예제는 이름이 *myNSGRule*이고 가상 컴퓨터에 대해 포트 *3389*를 여는 NSG 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-137">The following example creates an NSG rule named *myNSGRule* that opens port *3389* for the virtual machine:</span></span>

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow
```

<span data-ttu-id="8a6d0-138">[New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup)을 통해 *myNSGRule*을 사용하여 NSG를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-138">Create the NSG using *myNSGRule* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

<span data-ttu-id="8a6d0-139">[Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)를 사용하여 가상 네트워크의 서브넷에 NSG를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-139">Add the NSG to the subnet in the virtual network with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="8a6d0-140">[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork)를 사용하여 가상 네트워크를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-140">Update the virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a><span data-ttu-id="8a6d0-141">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="8a6d0-141">Create virtual machine</span></span>

<span data-ttu-id="8a6d0-142">가상 컴퓨터를 만들 때 운영 체제 이미지, 디스크 크기 조정 및 관리 자격 증명 등의 몇 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-142">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="8a6d0-143">이 예제에서는 최신 버전의 Windows Server 2016 Datacenter를 실행하는 가상 컴퓨터가 *myVM*이라는 이름으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-143">In this example, a virtual machine is created with a name of *myVM* running the latest version of Windows Server 2016 Datacenter.</span></span>

<span data-ttu-id="8a6d0-144">[Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential)을 사용하여 가상 컴퓨터의 관리자 계정에 필요한 사용자 이름 및 암호를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-144">Set the username and password needed for the administrator account on the virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="8a6d0-145">[New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig)를 사용하여 가상 컴퓨터에 대한 초기 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-145">Create the initial configuration for the virtual machine with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

<span data-ttu-id="8a6d0-146">[Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem)을 사용하여 운영 체제 정보를 가상 컴퓨터 구성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-146">Add the operating system information to the virtual machine configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span></span>

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="8a6d0-147">[Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)를 사용하여 이미지 정보를 가상 컴퓨터 구성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-147">Add the image information to the virtual machine configuration with [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

<span data-ttu-id="8a6d0-148">[Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk)를 사용하여 운영 체제 디스크 설정을 가상 컴퓨터 구성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-148">Add the operating system disk settings to the virtual machine configuration with [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

<span data-ttu-id="8a6d0-149">[Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface)를 사용하여 이전에 만든 네트워크 인터페이스 카드를 가상 컴퓨터 구성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-149">Add the network interface card that you previously created to the virtual machine configuration with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="8a6d0-150">[New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)을 사용하여 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-150">Create the virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-to-vm"></a><span data-ttu-id="8a6d0-151">VM에 연결</span><span class="sxs-lookup"><span data-stu-id="8a6d0-151">Connect to VM</span></span>

<span data-ttu-id="8a6d0-152">배포가 완료된 후 가상 컴퓨터에 대한 원격 데스크톱 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-152">After the deployment has completed, create a remote desktop connection with the virtual machine.</span></span>

<span data-ttu-id="8a6d0-153">다음 명령을 실행하여 가상 컴퓨터의 공용 IP 주소를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-153">Run the following commands to return the public IP address of the virtual machine.</span></span> <span data-ttu-id="8a6d0-154">다음 단계에서 웹 연결을 테스트하기 위해 브라우저와 연결할 수 있도록 이 IP 주소를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-154">Take note of this IP Address so you can connect to it with your browser to test web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

<span data-ttu-id="8a6d0-155">다음 명령을 사용하여 가상 컴퓨터와의 원격 데스크톱 세션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-155">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="8a6d0-156">해당 IP 주소를 가상 컴퓨터의 *publicIPAddress*로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-156">Replace the IP address with the *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="8a6d0-157">가상 컴퓨터를 만들 때 사용되는 자격 증명을 묻는 메시지가 표시되면 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-157">When prompted, enter the credentials used when creating the virtual machine.</span></span>

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a><span data-ttu-id="8a6d0-158">VM 이미지 이해</span><span class="sxs-lookup"><span data-stu-id="8a6d0-158">Understand VM images</span></span>

<span data-ttu-id="8a6d0-159">Azure Marketplace에는 새 가상 컴퓨터를 만드는 데 사용할 수 있는 여러 가상 컴퓨터 이미지가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-159">The Azure marketplace includes many virtual machine images that can be used to create a new virtual machine.</span></span> <span data-ttu-id="8a6d0-160">이전 단계에서는 Windows Server 2016-Datacenter 이미지를 사용하여 가상 컴퓨터를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-160">In the previous steps, a virtual machine was created using the Windows Server 2016-Datacenter image.</span></span> <span data-ttu-id="8a6d0-161">이번 단계에서는 PowerShell 모듈을 사용하여 Marketplace에서 새 VM의 기반이 될 수도 있는 다른 Windows 이미지를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-161">In this step, the PowerShell module is used to search the marketplace for other Windows images, which can also as a base for new VMs.</span></span> <span data-ttu-id="8a6d0-162">이 프로세스는 게시자, 제안 및 이미지 이름(SKU) 검색으로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-162">This process consists of finding the publisher, offer, and the image name (Sku).</span></span> 

<span data-ttu-id="8a6d0-163">이미지 게시자 목록을 반환하려면 [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-163">Use the [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) command to return a list of image publishers.</span></span>  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

<span data-ttu-id="8a6d0-164">이미지 제안 목록을 반환하려면 [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-164">Use the [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) to return a list of image offers.</span></span> <span data-ttu-id="8a6d0-165">이 명령을 사용하면 반환된 목록이 지정된 게시자를 기준으로 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-165">With this command, the returned list is filtered on the specified publisher.</span></span> 

```powershell
Get-AzureRmVMImageOffer -Location "EastUS" -PublisherName "MicrosoftWindowsServer"
```

```powershell
Offer             PublisherName          Location
-----             -------------          -------- 
Windows-HUB       MicrosoftWindowsServer EastUS 
WindowsServer     MicrosoftWindowsServer EastUS   
WindowsServer-HUB MicrosoftWindowsServer EastUS   
```

<span data-ttu-id="8a6d0-166">그런 다음 [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) 명령으로 게시자 및 제안 이름을 기준으로 필터링하여 이미지 이름 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-166">The [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) command will then filter on the publisher and offer name to return a list of image names.</span></span>

```powershell
Get-AzureRmVMImageSku -Location "EastUS" -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"
```

```powershell
Skus                            Offer         PublisherName          Location
----                            -----         -------------          --------
2008-R2-SP1                     WindowsServer MicrosoftWindowsServer EastUS  
2008-R2-SP1-BYOL                WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter-BYOL            WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter              WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter-BYOL         WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-Server-Core     WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-with-Containers WindowsServer MicrosoftWindowsServer EastUS  
2016-Nano-Server                WindowsServer MicrosoftWindowsServer EastUS
```

<span data-ttu-id="8a6d0-167">이 정보를 사용하여 특정 이미지가 있는 VM을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-167">This information can be used to deploy a VM with a specific image.</span></span> <span data-ttu-id="8a6d0-168">이 예제에서는 VM 개체에서 이미지 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-168">This example sets the image name on the VM object.</span></span> <span data-ttu-id="8a6d0-169">배포 단계를 완료하려면 이 자습서의 이전 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-169">Refer to the previous examples in this tutorial for complete deployment steps.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="8a6d0-170">VM 크기 이해</span><span class="sxs-lookup"><span data-stu-id="8a6d0-170">Understand VM sizes</span></span>

<span data-ttu-id="8a6d0-171">가상 컴퓨터 크기에 따라 CPU, GPU, 메모리 등 가상 컴퓨터에 사용할 수 있는 계산 리소스의 양이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-171">A virtual machine size determines the amount of compute resources such as CPU, GPU, and memory that are made available to the virtual machine.</span></span> <span data-ttu-id="8a6d0-172">Virtual Machines는 예상되는 워크로드에 맞는 크기로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-172">Virtual machines need to be created with a size appropriate for the expect work load.</span></span> <span data-ttu-id="8a6d0-173">워크로드가 증가할 경우 기존 가상 컴퓨터의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-173">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="8a6d0-174">VM 크기</span><span class="sxs-lookup"><span data-stu-id="8a6d0-174">VM Sizes</span></span>

<span data-ttu-id="8a6d0-175">다음 표에서는 크기를 사용 사례로 분류합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-175">The following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="8a6d0-176">형식</span><span class="sxs-lookup"><span data-stu-id="8a6d0-176">Type</span></span>                     | <span data-ttu-id="8a6d0-177">크기</span><span class="sxs-lookup"><span data-stu-id="8a6d0-177">Sizes</span></span>           |    <span data-ttu-id="8a6d0-178">설명</span><span class="sxs-lookup"><span data-stu-id="8a6d0-178">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8a6d0-179">범용 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="8a6d0-179">General purpose</span></span>         |<span data-ttu-id="8a6d0-180">DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="8a6d0-180">DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="8a6d0-181">CPU 대 메모리 비율이 적당합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-181">Balanced CPU-to-memory.</span></span> <span data-ttu-id="8a6d0-182">개발/테스트와 소규모에서 중간 정도의 응용 프로그램 및 데이터 솔루션에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-182">Ideal for dev / test and small to medium applications and data solutions.</span></span>  |
| <span data-ttu-id="8a6d0-183">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="8a6d0-183">Compute optimized</span></span>      | <span data-ttu-id="8a6d0-184">Fs, F</span><span class="sxs-lookup"><span data-stu-id="8a6d0-184">Fs, F</span></span>             | <span data-ttu-id="8a6d0-185">CPU 대 메모리 비율이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-185">High CPU-to-memory.</span></span> <span data-ttu-id="8a6d0-186">트래픽이 중간 정도인 응용 프로그램, 네트워크 어플라이언스 및 일괄 처리 프로세스에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-186">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| <span data-ttu-id="8a6d0-187">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="8a6d0-187">Memory optimized</span></span>       | <span data-ttu-id="8a6d0-188">GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="8a6d0-188">GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="8a6d0-189">메모리 대 코어 비율이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-189">High memory-to-core.</span></span> <span data-ttu-id="8a6d0-190">관계형 데이터베이스, 중대형 캐시 및 메모리 내 분석에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-190">Great for relational databases, medium to large caches, and in-memory analytics.</span></span>                 |
| <span data-ttu-id="8a6d0-191">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="8a6d0-191">Storage optimized</span></span>       | <span data-ttu-id="8a6d0-192">Ls</span><span class="sxs-lookup"><span data-stu-id="8a6d0-192">Ls</span></span>                | <span data-ttu-id="8a6d0-193">높은 디스크 처리량 및 IO</span><span class="sxs-lookup"><span data-stu-id="8a6d0-193">High disk throughput and IO.</span></span> <span data-ttu-id="8a6d0-194">빅 데이터, SQL, NoSQL 데이터베이스에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-194">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| <span data-ttu-id="8a6d0-195">GPU</span><span class="sxs-lookup"><span data-stu-id="8a6d0-195">GPU</span></span>           | <span data-ttu-id="8a6d0-196">NV, NC</span><span class="sxs-lookup"><span data-stu-id="8a6d0-196">NV, NC</span></span>            | <span data-ttu-id="8a6d0-197">대량의 그래픽 렌더링 및 비디오 편집에 적합한 전문 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-197">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| <span data-ttu-id="8a6d0-198">고성능</span><span class="sxs-lookup"><span data-stu-id="8a6d0-198">High performance</span></span> | <span data-ttu-id="8a6d0-199">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="8a6d0-199">H, A8-11</span></span>          | <span data-ttu-id="8a6d0-200">당사의 가장 강력한 CPU VM으로, 필요한 경우 처리량이 높은 네트워크 인터페이스(RDMA)도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-200">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="8a6d0-201">사용 가능한 VM 크기 찾기</span><span class="sxs-lookup"><span data-stu-id="8a6d0-201">Find available VM sizes</span></span>

<span data-ttu-id="8a6d0-202">특정 영역에서 사용할 수 있는 VM 크기의 목록을 보려면 [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-202">To see a list of VM sizes available in a particular region, use the [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command.</span></span>

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a><span data-ttu-id="8a6d0-203">VM 크기 조정</span><span class="sxs-lookup"><span data-stu-id="8a6d0-203">Resize a VM</span></span>

<span data-ttu-id="8a6d0-204">VM을 배포한 후에 크기를 조정하여 리소스 할당을 늘리거나 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-204">After a VM has been deployed, it can be resized to increase or decrease resource allocation.</span></span>

<span data-ttu-id="8a6d0-205">VM의 크기를 조정하기 전에 원하는 크기를 현재 VM 클러스터에서 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-205">Before resizing a VM, check if the desired size is available on the current VM cluster.</span></span> <span data-ttu-id="8a6d0-206">[Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) 명령은 크기 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-206">The [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command returns a list of sizes.</span></span> 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

<span data-ttu-id="8a6d0-207">원하는 크기를 사용할 수 있는 경우 전원이 켜진 상태에서 VM 크기를 조정할 수 있지만 작업 중 다시 부팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-207">If the desired size is available, the VM can be resized from a powered-on state, however it is rebooted during the operation.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

<span data-ttu-id="8a6d0-208">원하는 크기가 현재 클러스터에 없는 경우 크기 조정 작업 전에 VM 할당을 취소해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-208">If the desired size is not on the current cluster, the VM needs to be deallocated before the resize operation can occur.</span></span> <span data-ttu-id="8a6d0-209">VM의 전원이 다시 켜지면 임시 디스크의 모든 데이터가 제거되고 고정 IP 주소를 사용하지 않는 한 공용 IP 주소가 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-209">Note, when the VM is powered back on, any data on the temp disk are removed, and the public IP address change unless a static IP address is being used.</span></span> 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a><span data-ttu-id="8a6d0-210">VM 전원 상태</span><span class="sxs-lookup"><span data-stu-id="8a6d0-210">VM power states</span></span>

<span data-ttu-id="8a6d0-211">Azure VM의 전원 상태는 여러 상태 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-211">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="8a6d0-212">이 상태는 하이퍼바이저의 관점에서 VM의 현재 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-212">This state represents the current state of the VM from the standpoint of the hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="8a6d0-213">전원 상태</span><span class="sxs-lookup"><span data-stu-id="8a6d0-213">Power states</span></span>

| <span data-ttu-id="8a6d0-214">전원 상태</span><span class="sxs-lookup"><span data-stu-id="8a6d0-214">Power State</span></span> | <span data-ttu-id="8a6d0-215">설명</span><span class="sxs-lookup"><span data-stu-id="8a6d0-215">Description</span></span>
|----|----|
| <span data-ttu-id="8a6d0-216">Starting</span><span class="sxs-lookup"><span data-stu-id="8a6d0-216">Starting</span></span> | <span data-ttu-id="8a6d0-217">가상 컴퓨터가 시작되고 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-217">Indicates the virtual machine is being started.</span></span> |
| <span data-ttu-id="8a6d0-218">실행 중</span><span class="sxs-lookup"><span data-stu-id="8a6d0-218">Running</span></span> | <span data-ttu-id="8a6d0-219">가상 컴퓨터가 실행되고 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-219">Indicates that the virtual machine is running.</span></span> |
| <span data-ttu-id="8a6d0-220">중지 중</span><span class="sxs-lookup"><span data-stu-id="8a6d0-220">Stopping</span></span> | <span data-ttu-id="8a6d0-221">가상 컴퓨터가 중지되고 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-221">Indicates that the virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="8a6d0-222">중지됨</span><span class="sxs-lookup"><span data-stu-id="8a6d0-222">Stopped</span></span> | <span data-ttu-id="8a6d0-223">가상 컴퓨터가 중지되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-223">Indicates that the virtual machine is stopped.</span></span> <span data-ttu-id="8a6d0-224">중지됨 상태의 Virtual Machines에도 여전히 계산 요금이 발생됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-224">Note that virtual machines in the stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="8a6d0-225">할당 취소 중</span><span class="sxs-lookup"><span data-stu-id="8a6d0-225">Deallocating</span></span> | <span data-ttu-id="8a6d0-226">가상 컴퓨터의 할당이 취소되고 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-226">Indicates that the virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="8a6d0-227">할당 취소됨</span><span class="sxs-lookup"><span data-stu-id="8a6d0-227">Deallocated</span></span> | <span data-ttu-id="8a6d0-228">가상 컴퓨터가 하이퍼바이저에서 완전히 제거되었지만 제어 영역에서 계속 사용할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-228">Indicates that the virtual machine is completely removed from the hypervisor but still available in the control plane.</span></span> <span data-ttu-id="8a6d0-229">할당 취소됨 상태의 Virtual Machines에는 계산 요금이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-229">Virtual machines in the Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="8a6d0-230">가상 컴퓨터의 전원 상태가 알 수 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-230">Indicates that the power state of the virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="8a6d0-231">전원 상태 찾기</span><span class="sxs-lookup"><span data-stu-id="8a6d0-231">Find power state</span></span>

<span data-ttu-id="8a6d0-232">특정 VM의 상태를 검색하려면 [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-232">To retrieve the state of a particular VM, use the [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span> <span data-ttu-id="8a6d0-233">가상 컴퓨터 및 리소스 그룹에 대한 올바른 이름을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-233">Be sure to specify a valid name for a virtual machine and resource group.</span></span> 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

<span data-ttu-id="8a6d0-234">출력:</span><span class="sxs-lookup"><span data-stu-id="8a6d0-234">Output:</span></span>

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a><span data-ttu-id="8a6d0-235">관리 작업</span><span class="sxs-lookup"><span data-stu-id="8a6d0-235">Management tasks</span></span>

<span data-ttu-id="8a6d0-236">가상 컴퓨터의 수명 주기 동안 가상 컴퓨터 시작, 중지 또는 삭제 등의 관리 작업을 실행하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-236">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="8a6d0-237">또한 반복적이거나 복잡한 작업을 자동화하는 스크립트를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-237">Additionally, you may want to create scripts to automate repetitive or complex tasks.</span></span> <span data-ttu-id="8a6d0-238">Azure PowerShell을 사용하면 명령줄이나 스크립트로 여러 가지 일반적인 관리 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-238">Using Azure PowerShell, many common management tasks can be run from the command line or in scripts.</span></span>

### <a name="stop-virtual-machine"></a><span data-ttu-id="8a6d0-239">가상 컴퓨터 중지</span><span class="sxs-lookup"><span data-stu-id="8a6d0-239">Stop virtual machine</span></span>

<span data-ttu-id="8a6d0-240">[Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm)을 사용하여 가상 컴퓨터를 중지하고 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-240">Stop and deallocate a virtual machine with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

<span data-ttu-id="8a6d0-241">가상 컴퓨터를 프로비전된 상태로 유지하려면 -StayProvisioned 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-241">If you want to keep the virtual machine in a provisioned state, use the -StayProvisioned parameter.</span></span>

### <a name="start-virtual-machine"></a><span data-ttu-id="8a6d0-242">가상 컴퓨터 시작</span><span class="sxs-lookup"><span data-stu-id="8a6d0-242">Start virtual machine</span></span>

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="8a6d0-243">리소스 그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="8a6d0-243">Delete resource group</span></span>

<span data-ttu-id="8a6d0-244">리소스 그룹을 삭제하면 그 안에 포함된 리소스도 모두 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-244">Deleting a resource group also deletes all resources contained within.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a><span data-ttu-id="8a6d0-245">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8a6d0-245">Next steps</span></span>

<span data-ttu-id="8a6d0-246">이 자습서에서는 다음 방법과 같이 기본 VM을 만들고 관리하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-246">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8a6d0-247">VM 만들기 및 연결</span><span class="sxs-lookup"><span data-stu-id="8a6d0-247">Create and connect to a VM</span></span>
> * <span data-ttu-id="8a6d0-248">VM 이미지 선택 및 사용</span><span class="sxs-lookup"><span data-stu-id="8a6d0-248">Select and use VM images</span></span>
> * <span data-ttu-id="8a6d0-249">특정 VM 크기 보기 및 사용</span><span class="sxs-lookup"><span data-stu-id="8a6d0-249">View and use specific VM sizes</span></span>
> * <span data-ttu-id="8a6d0-250">VM 크기 조정</span><span class="sxs-lookup"><span data-stu-id="8a6d0-250">Resize a VM</span></span>
> * <span data-ttu-id="8a6d0-251">VM 상태 보기 및 이해</span><span class="sxs-lookup"><span data-stu-id="8a6d0-251">View and understand VM state</span></span>

<span data-ttu-id="8a6d0-252">VM 디스크에 대해 자세히 알아보려면 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8a6d0-252">Advance to the next tutorial to learn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="8a6d0-253">VM 디스크 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="8a6d0-253">Create and Manage VM disks</span></span>](./tutorial-manage-data-disk.md)

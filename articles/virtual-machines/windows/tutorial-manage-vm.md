---
title: "Windows Vm을 관리 하 고 aaaCreate hello Azure PowerShell 모듈 | Microsoft Docs"
description: "자습서-만들고와 Windows Vm 관리 hello Azure PowerShell 모듈"
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
ms.openlocfilehash: 20adcb673ef4de683e6ad82d048a9625a1dc838c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-with-hello-azure-powershell-module"></a><span data-ttu-id="1fc67-103">만들고 있는 Windows Vm 관리 hello Azure PowerShell 모듈</span><span class="sxs-lookup"><span data-stu-id="1fc67-103">Create and Manage Windows VMs with hello Azure PowerShell module</span></span>

<span data-ttu-id="1fc67-104">Azure 가상 컴퓨터는 완전히 구성 가능하고 유연한 컴퓨팅 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="1fc67-105">이 자습서에서는 VM 크기 선택, VM 이미지 선택 및 VM 배포 등 기본적인 Azure Virtual Machines 배포 항목에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="1fc67-106">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1fc67-107">만들고 tooa VM 연결</span><span class="sxs-lookup"><span data-stu-id="1fc67-107">Create and connect tooa VM</span></span>
> * <span data-ttu-id="1fc67-108">VM 이미지 선택 및 사용</span><span class="sxs-lookup"><span data-stu-id="1fc67-108">Select and use VM images</span></span>
> * <span data-ttu-id="1fc67-109">특정 VM 크기 보기 및 사용</span><span class="sxs-lookup"><span data-stu-id="1fc67-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="1fc67-110">VM 크기 조정</span><span class="sxs-lookup"><span data-stu-id="1fc67-110">Resize a VM</span></span>
> * <span data-ttu-id="1fc67-111">VM 상태 보기 및 이해</span><span class="sxs-lookup"><span data-stu-id="1fc67-111">View and understand VM state</span></span>

<span data-ttu-id="1fc67-112">이 자습서는 Azure PowerShell 모듈 버전 3.6 이상 hello가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-112">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="1fc67-113">실행 ` Get-Module -ListAvailable AzureRM` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-113">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="1fc67-114">Tooupgrade 필요한 경우 참조 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-114">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="1fc67-115">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="1fc67-115">Create resource group</span></span>

<span data-ttu-id="1fc67-116">Hello로 리소스 그룹 만들기 [새로 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-116">Create a resource group with hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> 

<span data-ttu-id="1fc67-117">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="1fc67-118">가상 컴퓨터보다 먼저 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="1fc67-119">이 예제에서는 리소스 그룹 이름이 *myResourceGroupVM* hello에서 만든 *EastUS* 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-119">In this example, a resource group named *myResourceGroupVM* is created in hello *EastUS* region.</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

<span data-ttu-id="1fc67-120">hello 리소스 그룹은 생성 하거나이 자습서 전체에서 볼 수 있는 VM을 수정할 때 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-120">hello resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="1fc67-121">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="1fc67-121">Create virtual machine</span></span>

<span data-ttu-id="1fc67-122">가상 컴퓨터 가상 네트워크에 연결 된 tooa 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-122">A virtual machine must be connected tooa virtual network.</span></span> <span data-ttu-id="1fc67-123">네트워크 인터페이스 카드를 통해 공용 IP 주소를 사용 하 여 hello 가상 컴퓨터와 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-123">You communicate with hello virtual machine using a public IP address through a network interface card.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="1fc67-124">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="1fc67-124">Create virtual network</span></span>

<span data-ttu-id="1fc67-125">[New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig)를 사용하여 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-125">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="1fc67-126">[New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork)를 사용하여 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-126">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a><span data-ttu-id="1fc67-127">공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="1fc67-127">Create public IP address</span></span>

<span data-ttu-id="1fc67-128">[New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)를 사용하여 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-128">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a><span data-ttu-id="1fc67-129">네트워크 인터페이스 카드 만들기</span><span class="sxs-lookup"><span data-stu-id="1fc67-129">Create network interface card</span></span>

<span data-ttu-id="1fc67-130">[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface)를 사용하여 네트워크 인터페이스 카드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-130">Create a network interface card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a><span data-ttu-id="1fc67-131">네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="1fc67-131">Create network security group</span></span>

<span data-ttu-id="1fc67-132">Azure NSG([네트워크 보안 그룹](../../virtual-network/virtual-networks-nsg.md))는 하나 또는 여러 가상 컴퓨터에 대한 인바운드 및 아웃바운드 트래픽을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-132">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="1fc67-133">네트워크 보안 그룹 규칙은 특정 포트 또는 포트 범위에 대한 네트워크 트래픽을 허용하거나 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-133">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="1fc67-134">이러한 규칙에는 미리 정의된 원본에서 시작되는 트래픽만 가상 컴퓨터와 통신할 수 있도록 원본 주소 접두사가 포함될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-134">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span> <span data-ttu-id="1fc67-135">tooaccess hello IIS 웹 서버를 설치 하는, 인바운드 NSG 규칙을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-135">tooaccess hello IIS webserver that you are installing, you must add an inbound NSG rule.</span></span>

<span data-ttu-id="1fc67-136">toocreate 인바운드 NSG 규칙을 사용 하 여 [추가 AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-136">toocreate an inbound NSG rule, use [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="1fc67-137">hello 다음 규칙을 만드는 예제는 NSG 라는 *myNSGRule* 하는 포트를 엽니다. *3389* hello 가상 컴퓨터에 대해:</span><span class="sxs-lookup"><span data-stu-id="1fc67-137">hello following example creates an NSG rule named *myNSGRule* that opens port *3389* for hello virtual machine:</span></span>

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

<span data-ttu-id="1fc67-138">사용 하 여 hello NSG 만들기 *myNSGRule* 와 [새로 AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="1fc67-138">Create hello NSG using *myNSGRule* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

<span data-ttu-id="1fc67-139">사용 하 여 가상 네트워크 hello hello NSG toohello 서브넷을 추가 [집합 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="1fc67-139">Add hello NSG toohello subnet in hello virtual network with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="1fc67-140">업데이트 된 가상 네트워크 hello [집합 AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="1fc67-140">Update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a><span data-ttu-id="1fc67-141">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="1fc67-141">Create virtual machine</span></span>

<span data-ttu-id="1fc67-142">가상 컴퓨터를 만들 때 운영 체제 이미지, 디스크 크기 조정 및 관리 자격 증명 등의 몇 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-142">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="1fc67-143">이 예제에서는 가상 컴퓨터의 이름으로 만들어질 *myVM* hello 최신 버전 Windows Server 2016 datacenter를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-143">In this example, a virtual machine is created with a name of *myVM* running hello latest version of Windows Server 2016 Datacenter.</span></span>

<span data-ttu-id="1fc67-144">Hello 사용자 이름 및 암호 사용 hello 가상 컴퓨터에서 hello 관리자 계정에 필요한 설정 [Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="1fc67-144">Set hello username and password needed for hello administrator account on hello virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="1fc67-145">Hello hello 사용 하는 가상 컴퓨터에 대 한 초기 구성을 만드는 [새로 AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span><span class="sxs-lookup"><span data-stu-id="1fc67-145">Create hello initial configuration for hello virtual machine with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

<span data-ttu-id="1fc67-146">인 hello 운영 체제 정보 toohello 가상 컴퓨터 구성 추가 [집합 AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span><span class="sxs-lookup"><span data-stu-id="1fc67-146">Add hello operating system information toohello virtual machine configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span></span>

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="1fc67-147">인 hello 이미지 정보 toohello 가상 컴퓨터 구성 추가 [집합 AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span><span class="sxs-lookup"><span data-stu-id="1fc67-147">Add hello image information toohello virtual machine configuration with [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

<span data-ttu-id="1fc67-148">Hello 운영 체제 디스크 설정을 toohello 인 가상 컴퓨터 구성 추가 [집합 AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span><span class="sxs-lookup"><span data-stu-id="1fc67-148">Add hello operating system disk settings toohello virtual machine configuration with [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

<span data-ttu-id="1fc67-149">이전에 만든 인 가상 컴퓨터 구성 toohello 추가 hello 네트워크 인터페이스 카드 [추가 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="1fc67-149">Add hello network interface card that you previously created toohello virtual machine configuration with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="1fc67-150">Hello 가상 컴퓨터를 만들 [새로 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-150">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-toovm"></a><span data-ttu-id="1fc67-151">TooVM 연결</span><span class="sxs-lookup"><span data-stu-id="1fc67-151">Connect tooVM</span></span>

<span data-ttu-id="1fc67-152">Hello 배포 완료 되 면 hello 가상 컴퓨터와 원격 데스크톱 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-152">After hello deployment has completed, create a remote desktop connection with hello virtual machine.</span></span>

<span data-ttu-id="1fc67-153">Hello 다음 hello 가상 컴퓨터의 명령 tooreturn hello 공용 IP 주소를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-153">Run hello following commands tooreturn hello public IP address of hello virtual machine.</span></span> <span data-ttu-id="1fc67-154">다음 단계에서의 사용자 브라우저 tootest 웹 연결 tooit를 연결할 수 있도록이이 IP 주소를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-154">Take note of this IP Address so you can connect tooit with your browser tootest web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

<span data-ttu-id="1fc67-155">사용 하 여 hello 다음 명령은 toocreate hello 가상 컴퓨터와 원격 데스크톱 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-155">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="1fc67-156">Hello로 hello IP 주소를 교체 *publicIPAddress* 의 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="1fc67-156">Replace hello IP address with hello *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="1fc67-157">메시지가 표시 되 면 hello 가상 컴퓨터를 만들 때 사용 하는 hello 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-157">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a><span data-ttu-id="1fc67-158">VM 이미지 이해</span><span class="sxs-lookup"><span data-stu-id="1fc67-158">Understand VM images</span></span>

<span data-ttu-id="1fc67-159">새 가상 컴퓨터를 사용 하는 toocreate 일 수 있는 많은 가상 컴퓨터 이미지를 포함 하는 hello Azure 마켓플레이스에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-159">hello Azure marketplace includes many virtual machine images that can be used toocreate a new virtual machine.</span></span> <span data-ttu-id="1fc67-160">Hello 이전 단계에서 가상 컴퓨터를 Windows Server 2016 데이터 센터 내 이미지 hello를 사용 하 여 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-160">In hello previous steps, a virtual machine was created using hello Windows Server 2016-Datacenter image.</span></span> <span data-ttu-id="1fc67-161">이 단계에서는 hello PowerShell 모듈이 새 Vm에 대 한 기반으로 수도 있는 다른 Windows 이미지에 대 한 사용 되는 toosearch hello 마켓플레이스 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-161">In this step, hello PowerShell module is used toosearch hello marketplace for other Windows images, which can also as a base for new VMs.</span></span> <span data-ttu-id="1fc67-162">이 프로세스는 hello 게시자, 제품, 및 hello 이미지 이름 (Sku) 찾기 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-162">This process consists of finding hello publisher, offer, and hello image name (Sku).</span></span> 

<span data-ttu-id="1fc67-163">사용 하 여 hello [Get AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) 명령 tooreturn 이미지 게시자 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-163">Use hello [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) command tooreturn a list of image publishers.</span></span>  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

<span data-ttu-id="1fc67-164">사용 하 여 hello [Get AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn 이미지 제안 목록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-164">Use hello [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn a list of image offers.</span></span> <span data-ttu-id="1fc67-165">이 명령을 사용 하 여 hello 반환 목록을 hello 지정 된 게시자에서 필터링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-165">With this command, hello returned list is filtered on hello specified publisher.</span></span> 

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

<span data-ttu-id="1fc67-166">hello [Get AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) 이미지 이름의 목록을 명령은 다음 hello 게시자와 제품 이름 tooreturn에 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-166">hello [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) command will then filter on hello publisher and offer name tooreturn a list of image names.</span></span>

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

<span data-ttu-id="1fc67-167">이 정보에 사용 되는 toodeploy 특정 이미지를 사용 하 여 VM 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-167">This information can be used toodeploy a VM with a specific image.</span></span> <span data-ttu-id="1fc67-168">이 예제에서는 hello VM 개체에 hello 이미지 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-168">This example sets hello image name on hello VM object.</span></span> <span data-ttu-id="1fc67-169">완전 한 배포 단계에 대 한이 자습서에서는 toohello 앞의 예제를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="1fc67-169">Refer toohello previous examples in this tutorial for complete deployment steps.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="1fc67-170">VM 크기 이해</span><span class="sxs-lookup"><span data-stu-id="1fc67-170">Understand VM sizes</span></span>

<span data-ttu-id="1fc67-171">가상 컴퓨터 크기는 hello 양의 toohello 사용 가능한 가상 컴퓨터에 적용 된 메모리, CPU 및 GPU, 등 계산 리소스를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-171">A virtual machine size determines hello amount of compute resources such as CPU, GPU, and memory that are made available toohello virtual machine.</span></span> <span data-ttu-id="1fc67-172">가상 컴퓨터가 사용 하 여 만든 크기를 적절 한 hello 예상 작업 부하에 대 한 toobe를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-172">Virtual machines need toobe created with a size appropriate for hello expect work load.</span></span> <span data-ttu-id="1fc67-173">워크로드가 증가할 경우 기존 가상 컴퓨터의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-173">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="1fc67-174">VM 크기</span><span class="sxs-lookup"><span data-stu-id="1fc67-174">VM Sizes</span></span>

<span data-ttu-id="1fc67-175">다음 표에서 hello 사용 사례에 크기를 분류 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-175">hello following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="1fc67-176">형식</span><span class="sxs-lookup"><span data-stu-id="1fc67-176">Type</span></span>                     | <span data-ttu-id="1fc67-177">크기</span><span class="sxs-lookup"><span data-stu-id="1fc67-177">Sizes</span></span>           |    <span data-ttu-id="1fc67-178">설명</span><span class="sxs-lookup"><span data-stu-id="1fc67-178">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1fc67-179">범용 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="1fc67-179">General purpose</span></span>         |<span data-ttu-id="1fc67-180">DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="1fc67-180">DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="1fc67-181">CPU 대 메모리 비율이 적당합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-181">Balanced CPU-to-memory.</span></span> <span data-ttu-id="1fc67-182">개발에 대 한 이상적인 / 테스트 및 소규모 toomedium 응용 프로그램 및 데이터 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-182">Ideal for dev / test and small toomedium applications and data solutions.</span></span>  |
| <span data-ttu-id="1fc67-183">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="1fc67-183">Compute optimized</span></span>      | <span data-ttu-id="1fc67-184">Fs, F</span><span class="sxs-lookup"><span data-stu-id="1fc67-184">Fs, F</span></span>             | <span data-ttu-id="1fc67-185">CPU 대 메모리 비율이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-185">High CPU-to-memory.</span></span> <span data-ttu-id="1fc67-186">트래픽이 중간 정도인 응용 프로그램, 네트워크 어플라이언스 및 일괄 처리 프로세스에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-186">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| <span data-ttu-id="1fc67-187">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="1fc67-187">Memory optimized</span></span>       | <span data-ttu-id="1fc67-188">GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="1fc67-188">GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="1fc67-189">메모리 대 코어 비율이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-189">High memory-to-core.</span></span> <span data-ttu-id="1fc67-190">관계형 데이터베이스, 중간 toolarge 캐시 및 메모리 내 분석에 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-190">Great for relational databases, medium toolarge caches, and in-memory analytics.</span></span>                 |
| <span data-ttu-id="1fc67-191">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="1fc67-191">Storage optimized</span></span>       | <span data-ttu-id="1fc67-192">Ls</span><span class="sxs-lookup"><span data-stu-id="1fc67-192">Ls</span></span>                | <span data-ttu-id="1fc67-193">높은 디스크 처리량 및 IO</span><span class="sxs-lookup"><span data-stu-id="1fc67-193">High disk throughput and IO.</span></span> <span data-ttu-id="1fc67-194">빅 데이터, SQL, NoSQL 데이터베이스에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-194">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| <span data-ttu-id="1fc67-195">GPU</span><span class="sxs-lookup"><span data-stu-id="1fc67-195">GPU</span></span>           | <span data-ttu-id="1fc67-196">NV, NC</span><span class="sxs-lookup"><span data-stu-id="1fc67-196">NV, NC</span></span>            | <span data-ttu-id="1fc67-197">대량의 그래픽 렌더링 및 비디오 편집에 적합한 전문 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-197">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| <span data-ttu-id="1fc67-198">고성능</span><span class="sxs-lookup"><span data-stu-id="1fc67-198">High performance</span></span> | <span data-ttu-id="1fc67-199">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="1fc67-199">H, A8-11</span></span>          | <span data-ttu-id="1fc67-200">당사의 가장 강력한 CPU VM으로, 필요한 경우 처리량이 높은 네트워크 인터페이스(RDMA)도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-200">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="1fc67-201">사용 가능한 VM 크기 찾기</span><span class="sxs-lookup"><span data-stu-id="1fc67-201">Find available VM sizes</span></span>

<span data-ttu-id="1fc67-202">특정 지역에 toosee VM 목록을 사용할 수 있는 크기, hello를 사용 하 여 [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-202">toosee a list of VM sizes available in a particular region, use hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command.</span></span>

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a><span data-ttu-id="1fc67-203">VM 크기 조정</span><span class="sxs-lookup"><span data-stu-id="1fc67-203">Resize a VM</span></span>

<span data-ttu-id="1fc67-204">VM을 배포한 후 크기가 조정 된 tooincrease 하거나 이동할 수 있습니다 리소스 할당을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-204">After a VM has been deployed, it can be resized tooincrease or decrease resource allocation.</span></span>

<span data-ttu-id="1fc67-205">VM의 크기를 조정 하기 전에 hello 원하는 크기는 hello 현재 VM 클러스터에서 사용할 수 있는 경우를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-205">Before resizing a VM, check if hello desired size is available on hello current VM cluster.</span></span> <span data-ttu-id="1fc67-206">hello [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) 명령은 크기의 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-206">hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command returns a list of sizes.</span></span> 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

<span data-ttu-id="1fc67-207">Hello 원하는 크기는 사용할 수 있는 경우 hello VM 크기를 조정할 수 전원이 켜진 상태에서 있지만 hello 작업 동안 다시 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-207">If hello desired size is available, hello VM can be resized from a powered-on state, however it is rebooted during hello operation.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

<span data-ttu-id="1fc67-208">Hello 크기를 원하는 경우에 없습니다 hello 현재 클러스터에 VM hello 요구 hello 크기 조정 작업 전에 할당 취소 toobe 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-208">If hello desired size is not on hello current cluster, hello VM needs toobe deallocated before hello resize operation can occur.</span></span> <span data-ttu-id="1fc67-209">Note hello VM의 전원이 켜져 다시, hello 임시 디스크의 모든 데이터가 제거 되 고 고정 IP 주소를 사용 하는 경우가 아니면 hello 공용 IP 주소를 변경 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="1fc67-209">Note, when hello VM is powered back on, any data on hello temp disk are removed, and hello public IP address change unless a static IP address is being used.</span></span> 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a><span data-ttu-id="1fc67-210">VM 전원 상태</span><span class="sxs-lookup"><span data-stu-id="1fc67-210">VM power states</span></span>

<span data-ttu-id="1fc67-211">Azure VM의 전원 상태는 여러 상태 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-211">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="1fc67-212">이 상태를 hello 하이퍼바이저의 hello 관점에서 hello hello VM의 현재 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-212">This state represents hello current state of hello VM from hello standpoint of hello hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="1fc67-213">전원 상태</span><span class="sxs-lookup"><span data-stu-id="1fc67-213">Power states</span></span>

| <span data-ttu-id="1fc67-214">전원 상태</span><span class="sxs-lookup"><span data-stu-id="1fc67-214">Power State</span></span> | <span data-ttu-id="1fc67-215">설명</span><span class="sxs-lookup"><span data-stu-id="1fc67-215">Description</span></span>
|----|----|
| <span data-ttu-id="1fc67-216">시작 중</span><span class="sxs-lookup"><span data-stu-id="1fc67-216">Starting</span></span> | <span data-ttu-id="1fc67-217">Hello 가상 컴퓨터가 시작 되 고 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-217">Indicates hello virtual machine is being started.</span></span> |
| <span data-ttu-id="1fc67-218">실행 중</span><span class="sxs-lookup"><span data-stu-id="1fc67-218">Running</span></span> | <span data-ttu-id="1fc67-219">Hello 가상 컴퓨터 실행 중임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-219">Indicates that hello virtual machine is running.</span></span> |
| <span data-ttu-id="1fc67-220">중지 중</span><span class="sxs-lookup"><span data-stu-id="1fc67-220">Stopping</span></span> | <span data-ttu-id="1fc67-221">Hello 가상 컴퓨터를 중지 하 고 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-221">Indicates that hello virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="1fc67-222">중지됨</span><span class="sxs-lookup"><span data-stu-id="1fc67-222">Stopped</span></span> | <span data-ttu-id="1fc67-223">Hello 가상 컴퓨터 중지 되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-223">Indicates that hello virtual machine is stopped.</span></span> <span data-ttu-id="1fc67-224">Note hello 중지 상태의 가상 컴퓨터에 여전히 컴퓨팅 요금이 부과 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-224">Note that virtual machines in hello stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="1fc67-225">할당 취소 중</span><span class="sxs-lookup"><span data-stu-id="1fc67-225">Deallocating</span></span> | <span data-ttu-id="1fc67-226">Hello 가상 컴퓨터를 할당 취소 되 고이 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-226">Indicates that hello virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="1fc67-227">할당 취소됨</span><span class="sxs-lookup"><span data-stu-id="1fc67-227">Deallocated</span></span> | <span data-ttu-id="1fc67-228">Hello 가상 컴퓨터 hello 제어 평면에서 계속 제공 되지만 hello 하이퍼바이저에서 완전히 제거 됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-228">Indicates that hello virtual machine is completely removed from hello hypervisor but still available in hello control plane.</span></span> <span data-ttu-id="1fc67-229">Hello 할당 취소 됨 상태에서에서 가상 컴퓨터 계산 비용이 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-229">Virtual machines in hello Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="1fc67-230">Hello 가상 컴퓨터의 전원 상태 hello 알려진 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-230">Indicates that hello power state of hello virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="1fc67-231">전원 상태 찾기</span><span class="sxs-lookup"><span data-stu-id="1fc67-231">Find power state</span></span>

<span data-ttu-id="1fc67-232">특정 VM 사용 하 여 hello의 tooretrieve hello 상태 [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-232">tooretrieve hello state of a particular VM, use hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span> <span data-ttu-id="1fc67-233">있는지 toospecify 가상 컴퓨터 및 리소스 그룹에 대 한 올바른 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-233">Be sure toospecify a valid name for a virtual machine and resource group.</span></span> 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

<span data-ttu-id="1fc67-234">출력:</span><span class="sxs-lookup"><span data-stu-id="1fc67-234">Output:</span></span>

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a><span data-ttu-id="1fc67-235">관리 작업</span><span class="sxs-lookup"><span data-stu-id="1fc67-235">Management tasks</span></span>

<span data-ttu-id="1fc67-236">가상 컴퓨터의 hello 수명 주기 동안 시작, 중지, 또는 가상 컴퓨터를 삭제 하는 등의 toorun 관리 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-236">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="1fc67-237">또한 toocreate 스크립트 tooautomate 반복적 복잡 한 작업을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-237">Additionally, you may want toocreate scripts tooautomate repetitive or complex tasks.</span></span> <span data-ttu-id="1fc67-238">Azure PowerShell을 사용 하 여, 여러 가지 일반적인 관리 작업 또는 실행할 수 있는 hello 명령줄에서 스크립트에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-238">Using Azure PowerShell, many common management tasks can be run from hello command line or in scripts.</span></span>

### <a name="stop-virtual-machine"></a><span data-ttu-id="1fc67-239">가상 컴퓨터 중지</span><span class="sxs-lookup"><span data-stu-id="1fc67-239">Stop virtual machine</span></span>

<span data-ttu-id="1fc67-240">[Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm)을 사용하여 가상 컴퓨터를 중지하고 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-240">Stop and deallocate a virtual machine with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

<span data-ttu-id="1fc67-241">Tookeep hello 가상 컴퓨터 프로 비전 된 상태에서 원하는 hello-StayProvisioned 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-241">If you want tookeep hello virtual machine in a provisioned state, use hello -StayProvisioned parameter.</span></span>

### <a name="start-virtual-machine"></a><span data-ttu-id="1fc67-242">가상 컴퓨터 시작</span><span class="sxs-lookup"><span data-stu-id="1fc67-242">Start virtual machine</span></span>

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="1fc67-243">리소스 그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="1fc67-243">Delete resource group</span></span>

<span data-ttu-id="1fc67-244">리소스 그룹을 삭제하면 그 안에 포함된 리소스도 모두 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-244">Deleting a resource group also deletes all resources contained within.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a><span data-ttu-id="1fc67-245">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1fc67-245">Next steps</span></span>

<span data-ttu-id="1fc67-246">이 자습서에서는 다음 방법과 같이 기본 VM을 만들고 관리하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-246">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1fc67-247">만들고 tooa VM 연결</span><span class="sxs-lookup"><span data-stu-id="1fc67-247">Create and connect tooa VM</span></span>
> * <span data-ttu-id="1fc67-248">VM 이미지 선택 및 사용</span><span class="sxs-lookup"><span data-stu-id="1fc67-248">Select and use VM images</span></span>
> * <span data-ttu-id="1fc67-249">특정 VM 크기 보기 및 사용</span><span class="sxs-lookup"><span data-stu-id="1fc67-249">View and use specific VM sizes</span></span>
> * <span data-ttu-id="1fc67-250">VM 크기 조정</span><span class="sxs-lookup"><span data-stu-id="1fc67-250">Resize a VM</span></span>
> * <span data-ttu-id="1fc67-251">VM 상태 보기 및 이해</span><span class="sxs-lookup"><span data-stu-id="1fc67-251">View and understand VM state</span></span>

<span data-ttu-id="1fc67-252">VM 디스크에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc67-252">Advance toohello next tutorial toolearn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="1fc67-253">VM 디스크 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="1fc67-253">Create and Manage VM disks</span></span>](./tutorial-manage-data-disk.md)

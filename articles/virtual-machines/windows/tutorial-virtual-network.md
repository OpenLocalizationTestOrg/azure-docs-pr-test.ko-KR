---
title: "Azure Virtual Network 및 Windows Virtual Machines | Microsoft Docs"
description: "자습서 - Azure PowerShell을 사용하여 Azure Virtual Network 및 Windows Virtual Machines 관리"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: c71c07f8ecd123a7e27848ba5043d46e315fcf03
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a><span data-ttu-id="75391-103">Azure PowerShell을 사용하여 Azure Virtual Network 및 Windows Virtual Machines 관리</span><span class="sxs-lookup"><span data-stu-id="75391-103">Manage Azure Virtual Networks and Windows Virtual Machines with Azure PowerShell</span></span>

<span data-ttu-id="75391-104">Azure Virtual Machines는 내부 및 외부 네트워크 통신에서 Azure 네트워킹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="75391-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="75391-105">이 자습서에서는 가상 네트워크에 여러 VM(가상 컴퓨터)을 만들고 이러한 컴퓨터 간에 네트워크 연결을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="75391-105">In this tutorial, you create multiple virtual machines (VMs) in a virtual network and configure network connectivity between them.</span></span> <span data-ttu-id="75391-106">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="75391-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="75391-107">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="75391-107">Create a virtual network</span></span>
> * <span data-ttu-id="75391-108">가상 네트워크 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="75391-108">Create virtual network subnets</span></span>
> * <span data-ttu-id="75391-109">네트워크 보안 그룹을 사용하여 네트워크 트래픽 제어</span><span class="sxs-lookup"><span data-stu-id="75391-109">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="75391-110">트래픽 규칙의 실제 동작 보기</span><span class="sxs-lookup"><span data-stu-id="75391-110">View traffic rules in action</span></span>

<span data-ttu-id="75391-111">이 자습서에는 Azure PowerShell 모듈 버전 3.6 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="75391-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="75391-112">` Get-Module -ListAvailable AzureRM`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="75391-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="75391-113">업그레이드해야 하는 경우 [Azure PowerShell 모듈 설치](/powershell/azure/install-azurerm-ps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75391-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-vnet"></a><span data-ttu-id="75391-114">VNet 만들기</span><span class="sxs-lookup"><span data-stu-id="75391-114">Create VNet</span></span>

<span data-ttu-id="75391-115">VNet은 클라우드의 사용자 네트워크를 나타내는 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="75391-115">A VNet is a representation of your own network in the cloud.</span></span> <span data-ttu-id="75391-116">구독 전용 Azure 클라우드를 논리적으로 격리한 것이 VNet입니다.</span><span class="sxs-lookup"><span data-stu-id="75391-116">A VNet is a logical isolation of the Azure cloud dedicated to your subscription.</span></span> <span data-ttu-id="75391-117">VNet 내에서 서브넷, 해당 서브넷에 대한 연결 규칙 및 VM에서 서브넷으로의 연결을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="75391-117">Within a VNet, you find subnets, rules for connectivity to those subnets, and connections from the VMs to the subnets.</span></span>

<span data-ttu-id="75391-118">다른 Azure 리소스를 만들려면 먼저 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)을 사용하여 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75391-118">Before you can create any other Azure resources, you need to create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="75391-119">다음 예제에서는 *EastUS* 위치에 *myRGNetwork*라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75391-119">The following example creates a resource group named *myRGNetwork* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

<span data-ttu-id="75391-120">서브넷은 VNet의 자식 리소스이며, IP 주소 접두사를 사용하여 CIDR 블록 내의 주소 공간 세그먼트를 정의하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75391-120">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="75391-121">NIC는 서브넷에 추가하고 VM에 연결하여 다양한 워크로드에 대한 연결을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75391-121">NICs can be added to subnets, and connected to VMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="75391-122">[New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig)를 사용하여 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75391-122">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="75391-123">[New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) 명령을 통해 *myFrontendSubnet*을 사용하여 *myVNet*이라는 VNET을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75391-123">Create a VNET named *myVNet* using *myFrontendSubnet* with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a><span data-ttu-id="75391-124">프런트 엔드 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="75391-124">Create front-end VM</span></span>

<span data-ttu-id="75391-125">VM이 VNet에서 통신하려면 가상 네트워크 인터페이스(NIC)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="75391-125">For a VM to communicate in a VNet, it needs a virtual network interface (NIC).</span></span> <span data-ttu-id="75391-126">*myFrontendVM*은 인터넷에서 액세스되므로 공용 IP 주소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="75391-126">The *myFrontendVM* is accessed from the internet, so it also needs a public IP address.</span></span> 

<span data-ttu-id="75391-127">[New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)를 사용하여 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75391-127">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

<span data-ttu-id="75391-128">[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface)를 사용하여 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75391-128">Create a NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

<span data-ttu-id="75391-129">[Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential)을 사용하여 VM의 컴퓨터의 관리자 계정에 필요한 사용자 이름 및 암호를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="75391-129">Set the username and password needed for the administrator account on the VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="75391-130">[New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) 및 [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)을 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75391-130">Create the VMs with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> 

```powershell
$frontendVM = New-AzureRmVMConfig `
    -VMName myFrontendVM `
    -VMSize Standard_D1
$frontendVM = Set-AzureRmVMOperatingSystem `
    -VM $frontendVM `
    -Windows `
    -ComputerName myFrontendVM `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
$frontendVM = Set-AzureRmVMSourceImage `
    -VM $frontendVM `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
$frontendVM = Set-AzureRmVMOSDisk `
    -VM $frontendVM `
    -Name myFrontendOSDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
$frontendVM = Add-AzureRmVMNetworkInterface `
    -VM $frontendVM `
    -Id $frontendNic.Id
New-AzureRmVM `
    -ResourceGroupName myRGNetwork `
    -Location EastUS `
    -VM $frontendVM
```

## <a name="install-web-server"></a><span data-ttu-id="75391-131">웹 서버 설치</span><span class="sxs-lookup"><span data-stu-id="75391-131">Install web server</span></span>

<span data-ttu-id="75391-132">원격 데스크톱 세션을 사용하여 *myFrontendVM*에 IIS를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75391-132">You can install IIS on *myFrontendVM* by using a remote desktop session.</span></span> <span data-ttu-id="75391-133">액세스하려면 VM의 공용 IP 주소를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75391-133">You need to get the public IP address of the VM to access it.</span></span>

<span data-ttu-id="75391-134">[Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)를 사용하여 *myFrontendVM*의 공용 IP 주소를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75391-134">You can get the public IP address of *myFrontendVM* with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="75391-135">다음 예제에서는 앞서 만든 *myPublicIPAddress*의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="75391-135">The following example obtains the IP address for *myPublicIPAddress* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

<span data-ttu-id="75391-136">이후 단계에서 사용할 수 있도록 이 IP 주소를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="75391-136">Take note of this IP Address so you can use it in future steps.</span></span>

<span data-ttu-id="75391-137">다음 명령을 사용하여 *myFrontendVM*과의 원격 데스크톱 세션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75391-137">Use the following command to create a remote desktop session with *myFrontendVM*.</span></span> <span data-ttu-id="75391-138">*<publicIPAddress>*를 이전에 기록한 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="75391-138">Replace *<publicIPAddress>* with the address that you previously recorded.</span></span> <span data-ttu-id="75391-139">VM을 만들 때 사용되는 자격 증명을 묻는 메시지가 표시되면 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="75391-139">When prompted, enter the credentials used when you created the VM.</span></span>

```
mstsc /v:<publicIpAddress>
``` 

<span data-ttu-id="75391-140">이제 *myFrontendVM*에 로그인했으므로 PowerShell 한 줄로 IIS를 설치하고 웹 트래픽을 허용하도록 로컬 방화벽 규칙을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75391-140">Now that you have logged in to *myFrontendVM*, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="75391-141">PowerShell 프롬프트를 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="75391-141">Open a PowerShell prompt and run the following command:</span></span>

<span data-ttu-id="75391-142">[Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature)를 사용하여 IIS 웹 서버를 설치하는 사용자 지정 스크립트 확장을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="75391-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) to run the custom script extension that installs the IIS webserver:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="75391-143">이제 공용 IP 주소를 통해 VM으로 이동하여 IIS 사이트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75391-143">Now you can use the public IP address to browse to the VM to see the IIS site.</span></span>

![IIS 기본 사이트](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a><span data-ttu-id="75391-145">인터넷 트래픽 관리</span><span class="sxs-lookup"><span data-stu-id="75391-145">Manage internal traffic</span></span>

<span data-ttu-id="75391-146">NSG(네트워크 보안 그룹)에는 VNet에 연결된 리소스에 대한 네트워크 트래픽을 허용하거나 거부하는 보안 규칙 목록이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75391-146">A network security group (NSG) contains a list of security rules that allow or deny network traffic to resources connected to a VNet.</span></span> <span data-ttu-id="75391-147">NSG는 서브넷 또는 VM에 연결된 개별 NIC에 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75391-147">NSGs can be associated to subnets or individual NICs attached to VMs.</span></span> <span data-ttu-id="75391-148">포트를 통한 VM에 대한 액세스 열기 또는 닫기는 NSG 규칙을 사용하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="75391-148">Opening or closing access to VMs through ports is done using NSG rules.</span></span> <span data-ttu-id="75391-149">*myFrontendVM*을 만들 때 RDP 연결에 대해 인바운드 포트 3389가 자동으로 열렸습니다.</span><span class="sxs-lookup"><span data-stu-id="75391-149">When you created *myFrontendVM*, inbound port 3389 was automatically opened for RDP connectivity.</span></span>

<span data-ttu-id="75391-150">VM의 내부 통신은 NSG를 사용하여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75391-150">Internal communication of VMs can be configured using an NSG.</span></span> <span data-ttu-id="75391-151">이 섹션에서는 네트워크에서 추가 서브넷을 만들고 NSG를 서브넷에 할당하여 포트 1433의 *myFrontendVM*에서 *myBackendVM*으로 연결할 수 있도록 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="75391-151">In this section, you learn how to create an additional subnet in the network and assign an NSG to it to allow a connection from *myFrontendVM* to *myBackendVM* on port 1433.</span></span> <span data-ttu-id="75391-152">그러면 서브넷이 만들어질 때 VM에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="75391-152">The subnet is then assigned to the VM when it is created.</span></span>

<span data-ttu-id="75391-153">백 엔드 서브넷에 대한 NSG를 만들어 *myFrontendVM*에서만 *myBackendVM*으로 내부 트래픽을 보내도록 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75391-153">You can limit internal traffic to *myBackendVM* from only *myFrontendVM* by creating an NSG for the back-end subnet.</span></span> <span data-ttu-id="75391-154">다음 예제에서는 [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig)를 사용하여 *myBackendNSGRule*이라는 NSG 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75391-154">The following example creates an NSG rule named *myBackendNSGRule* with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span></span>

```powershell
$nsgBackendRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myBackendNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 100 `
  -SourceAddressPrefix 10.0.0.0/24 `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 1433 `
  -Access Allow
```

<span data-ttu-id="75391-155">[New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup)을 사용하여 *myBackendNSG*라는 네트워크 보안 그룹을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="75391-155">Add a network security group named *myBackendNSG* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a><span data-ttu-id="75391-156">백 엔드 서브넷 추가</span><span class="sxs-lookup"><span data-stu-id="75391-156">Add back-end subnet</span></span>

<span data-ttu-id="75391-157">[Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig)를 사용하여 *myBackEndSubnet*을 *myVNet*에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="75391-157">Add *myBackEndSubnet* to *myVNet* with [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -VirtualNetwork $vnet `
  -AddressPrefix 10.0.1.0/24 `
  -NetworkSecurityGroup $nsgBackend
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Name myVNet
```

## <a name="create-back-end-vm"></a><span data-ttu-id="75391-158">백 엔드 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="75391-158">Create back-end VM</span></span>

<span data-ttu-id="75391-159">백 엔드 VM을 만드는 가장 쉬운 방법은 SQL Server 이미지를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="75391-159">The easiest way to create the back-end VM is by using a SQL Server image.</span></span> <span data-ttu-id="75391-160">이 자습서에서는 데이터베이스 서버를 사용하여 VM을 만들기만 하며 데이터베이스에 액세스하는 방법에 대한 정보는 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75391-160">This tutorial only creates the VM with the database server, but doesn't provide information about accessing the database.</span></span>

<span data-ttu-id="75391-161">*myBackendNic*을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75391-161">Create *myBackendNic*:</span></span>

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

<span data-ttu-id="75391-162">Get-Credential을 사용하여 가상 컴퓨터의 관리자 계정에 필요한 사용자 이름 및 암호를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="75391-162">Set the username and password needed for the administrator account on the VM with Get-Credential:</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="75391-163">*myBackendVM*을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75391-163">Create *myBackendVM*:</span></span>

```powershell
$backendVM = New-AzureRmVMConfig `
  -VMName myBackendVM `
  -VMSize Standard_D1
$backendVM = Set-AzureRmVMOperatingSystem `
  -VM $backendVM `
  -Windows `
  -ComputerName myBackendVM `
  -Credential $cred `
  -ProvisionVMAgent `
  -EnableAutoUpdate
$backendVM = Set-AzureRmVMSourceImage `
  -VM $backendVM `
  -PublisherName MicrosoftSQLServer `
  -Offer SQL2016SP1-WS2016 `
  -Skus Enterprise `
  -Version latest
$backendVM = Set-AzureRmVMOSDisk `
  -VM $backendVM `
  -Name myBackendOSDisk `
  -DiskSizeInGB 128 `
  -CreateOption FromImage `
  -Caching ReadWrite
$backendVM = Add-AzureRmVMNetworkInterface `
  -VM $backendVM `
  -Id $backendNic.Id
New-AzureRmVM `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -VM $backendVM
```

<span data-ttu-id="75391-164">사용되는 이미지에는 SQL Server가 설치되어 있지만 이 자습서에서는 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75391-164">The image that is used has SQL Server installed, but is not used in this tutorial.</span></span> <span data-ttu-id="75391-165">여기서는 웹 트래픽을 처리하도록 VM을 구성하는 방법 및 데이터베이스 관리를 처리하도록 VM을 구성하는 방법을 보여 주기 위해 포함되었습니다.</span><span class="sxs-lookup"><span data-stu-id="75391-165">It is included to show you how you can configure a VM to handle web traffic and a VM to handle database management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75391-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="75391-166">Next steps</span></span>

<span data-ttu-id="75391-167">이 자습서에서는 가상 컴퓨터와 관련된 Azure Networks를 만들고 보호했습니다.</span><span class="sxs-lookup"><span data-stu-id="75391-167">In this tutorial, you created and secured Azure networks as related to virtual machines.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="75391-168">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="75391-168">Create a virtual network</span></span>
> * <span data-ttu-id="75391-169">가상 네트워크 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="75391-169">Create virtual network subnets</span></span>
> * <span data-ttu-id="75391-170">네트워크 보안 그룹을 사용하여 네트워크 트래픽 제어</span><span class="sxs-lookup"><span data-stu-id="75391-170">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="75391-171">트래픽 규칙의 실제 동작 보기</span><span class="sxs-lookup"><span data-stu-id="75391-171">View traffic rules in action</span></span>

<span data-ttu-id="75391-172">다음 자습서로 이동하여 Azure Backup을 사용하는 가상 컴퓨터의 데이터 보안 모니터링에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="75391-172">Advance to the next tutorial to learn about monitoring securing data on virtual machines using Azure backup.</span></span> <span data-ttu-id="75391-173">을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75391-173">.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="75391-174">Azure에서 Windows 가상 컴퓨터 백업</span><span class="sxs-lookup"><span data-stu-id="75391-174">Back up Windows virtual machines in Azure</span></span>](./tutorial-backup-vms.md)

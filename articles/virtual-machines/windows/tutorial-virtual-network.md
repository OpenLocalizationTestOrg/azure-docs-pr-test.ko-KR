---
title: "aaaAzure 가상 네트워크와 Windows 가상 컴퓨터 | Microsoft Docs"
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
ms.openlocfilehash: ed77d9d5873e849fcb2aaf15e41899d7ad8c781a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a><span data-ttu-id="bc406-103">Azure PowerShell을 사용하여 Azure Virtual Network 및 Windows Virtual Machines 관리</span><span class="sxs-lookup"><span data-stu-id="bc406-103">Manage Azure Virtual Networks and Windows Virtual Machines with Azure PowerShell</span></span>

<span data-ttu-id="bc406-104">Azure Virtual Machines는 내부 및 외부 네트워크 통신에서 Azure 네트워킹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="bc406-105">이 자습서에서는 가상 네트워크에 여러 VM(가상 컴퓨터)을 만들고 이러한 컴퓨터 간에 네트워크 연결을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-105">In this tutorial, you create multiple virtual machines (VMs) in a virtual network and configure network connectivity between them.</span></span> <span data-ttu-id="bc406-106">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bc406-107">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="bc406-107">Create a virtual network</span></span>
> * <span data-ttu-id="bc406-108">가상 네트워크 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="bc406-108">Create virtual network subnets</span></span>
> * <span data-ttu-id="bc406-109">네트워크 보안 그룹을 사용하여 네트워크 트래픽 제어</span><span class="sxs-lookup"><span data-stu-id="bc406-109">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="bc406-110">트래픽 규칙의 실제 동작 보기</span><span class="sxs-lookup"><span data-stu-id="bc406-110">View traffic rules in action</span></span>

<span data-ttu-id="bc406-111">이 자습서는 Azure PowerShell 모듈 버전 3.6 이상 hello가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="bc406-112">실행 ` Get-Module -ListAvailable AzureRM` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="bc406-113">Tooupgrade 필요한 경우 참조 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-vnet"></a><span data-ttu-id="bc406-114">VNet 만들기</span><span class="sxs-lookup"><span data-stu-id="bc406-114">Create VNet</span></span>

<span data-ttu-id="bc406-115">VNet은 hello 클라우드에서 사용자의 네트워크의 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-115">A VNet is a representation of your own network in hello cloud.</span></span> <span data-ttu-id="bc406-116">VNet의 hello Azure 클라우드 전용 tooyour 구독 논리적 격리입니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-116">A VNet is a logical isolation of hello Azure cloud dedicated tooyour subscription.</span></span> <span data-ttu-id="bc406-117">VNet 내의 서브넷에 연결 toothose 서브넷 및 hello Vm toohello 서브넷에서 연결에 대 한 규칙 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-117">Within a VNet, you find subnets, rules for connectivity toothose subnets, and connections from hello VMs toohello subnets.</span></span>

<span data-ttu-id="bc406-118">다른 Azure 리소스를 만들기 전에 필요한 toocreate 인 리소스 그룹과 [새로 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-118">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="bc406-119">hello 다음 예제에서는 명명 된 리소스 그룹 *myRGNetwork* hello에 *EastUS* 위치:</span><span class="sxs-lookup"><span data-stu-id="bc406-119">hello following example creates a resource group named *myRGNetwork* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

<span data-ttu-id="bc406-120">서브넷은 VNet의 자식 리소스이며, IP 주소 접두사를 사용하여 CIDR 블록 내의 주소 공간 세그먼트를 정의하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-120">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="bc406-121">Nic는 toosubnets, 및 다양 한 작업에 대 한 연결을 제공 하는 연결 된 tooVMs를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-121">NICs can be added toosubnets, and connected tooVMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="bc406-122">[New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig)를 사용하여 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-122">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="bc406-123">[New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) 명령을 통해 *myFrontendSubnet*을 사용하여 *myVNet*이라는 VNET을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-123">Create a VNET named *myVNet* using *myFrontendSubnet* with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a><span data-ttu-id="bc406-124">프런트 엔드 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="bc406-124">Create front-end VM</span></span>

<span data-ttu-id="bc406-125">VNet에 VM toocommunicate에 대 한 가상 네트워크 인터페이스 (NIC) 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-125">For a VM toocommunicate in a VNet, it needs a virtual network interface (NIC).</span></span> <span data-ttu-id="bc406-126">hello *myFrontendVM* hello에서 액세스 하는 공용 IP 주소를도 필요 하므로 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-126">hello *myFrontendVM* is accessed from hello internet, so it also needs a public IP address.</span></span> 

<span data-ttu-id="bc406-127">[New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)를 사용하여 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-127">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

<span data-ttu-id="bc406-128">[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface)를 사용하여 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-128">Create a NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

<span data-ttu-id="bc406-129">Hello 사용자 이름 및 암호 hello VM에서 hello 관리자 계정에 필요한 설정으로 [Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="bc406-129">Set hello username and password needed for hello administrator account on hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="bc406-130">Hello Vm을 만들 [새로 AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [집합 AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [집합 AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [집합-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [추가 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), 및 [새 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-130">Create hello VMs with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> 

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

## <a name="install-web-server"></a><span data-ttu-id="bc406-131">웹 서버 설치</span><span class="sxs-lookup"><span data-stu-id="bc406-131">Install web server</span></span>

<span data-ttu-id="bc406-132">원격 데스크톱 세션을 사용하여 *myFrontendVM*에 IIS를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-132">You can install IIS on *myFrontendVM* by using a remote desktop session.</span></span> <span data-ttu-id="bc406-133">VM tooaccess hello tooget hello 공용 IP 주소가 필요한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-133">You need tooget hello public IP address of hello VM tooaccess it.</span></span>

<span data-ttu-id="bc406-134">Hello의 공용 IP 주소를 가져올 수 있습니다 *myFrontendVM* 와 [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-134">You can get hello public IP address of *myFrontendVM* with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="bc406-135">hello 다음 예제에서는 가져옵니다 hello IP 주소를 *myPublicIPAddress* 앞에서 만든:</span><span class="sxs-lookup"><span data-stu-id="bc406-135">hello following example obtains hello IP address for *myPublicIPAddress* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

<span data-ttu-id="bc406-136">이후 단계에서 사용할 수 있도록 이 IP 주소를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-136">Take note of this IP Address so you can use it in future steps.</span></span>

<span data-ttu-id="bc406-137">사용 하 여 hello 다음 명령은 원격 데스크톱 세션을 a toocreate *myFrontendVM*합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-137">Use hello following command toocreate a remote desktop session with *myFrontendVM*.</span></span> <span data-ttu-id="bc406-138">대체  *<publicIPAddress>*  이전에 기록한 hello 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-138">Replace *<publicIPAddress>* with hello address that you previously recorded.</span></span> <span data-ttu-id="bc406-139">메시지가 표시 되 면 hello VM을 만들 때 사용 하는 hello 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-139">When prompted, enter hello credentials used when you created hello VM.</span></span>

```
mstsc /v:<publicIpAddress>
``` 

<span data-ttu-id="bc406-140">로그인이 너무 했으므로*myFrontendVM*, hello 로컬 방화벽 규칙 tooallow 웹 트래픽을 사용 하도록 설정 및 PowerShell tooinstall IIS 전혀 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-140">Now that you have logged in too*myFrontendVM*, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="bc406-141">PowerShell 프롬프트를 열고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-141">Open a PowerShell prompt and run hello following command:</span></span>

<span data-ttu-id="bc406-142">사용 하 여 [Install-windowsfeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) hello IIS 웹 서버를 설치 하는 toorun hello 사용자 지정 스크립트 확장:</span><span class="sxs-lookup"><span data-stu-id="bc406-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun hello custom script extension that installs hello IIS webserver:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="bc406-143">이제 hello 공용 IP 주소 toobrowse toohello VM toosee hello IIS 사이트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-143">Now you can use hello public IP address toobrowse toohello VM toosee hello IIS site.</span></span>

![IIS 기본 사이트](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a><span data-ttu-id="bc406-145">인터넷 트래픽 관리</span><span class="sxs-lookup"><span data-stu-id="bc406-145">Manage internal traffic</span></span>

<span data-ttu-id="bc406-146">네트워크 보안 그룹 NSG ()를 허용 하거나 네트워크 트래픽 연결 tooresources tooa VNet을 거부 하는 보안 규칙 목록이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-146">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooa VNet.</span></span> <span data-ttu-id="bc406-147">Nsg 연결된 toosubnets 수 또는 개별 Nic tooVMs 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-147">NSGs can be associated toosubnets or individual NICs attached tooVMs.</span></span> <span data-ttu-id="bc406-148">열기 또는 닫기 액세스 tooVMs 포트를 통해 이루어진다는 NSG 규칙을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-148">Opening or closing access tooVMs through ports is done using NSG rules.</span></span> <span data-ttu-id="bc406-149">*myFrontendVM*을 만들 때 RDP 연결에 대해 인바운드 포트 3389가 자동으로 열렸습니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-149">When you created *myFrontendVM*, inbound port 3389 was automatically opened for RDP connectivity.</span></span>

<span data-ttu-id="bc406-150">VM의 내부 통신은 NSG를 사용하여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-150">Internal communication of VMs can be configured using an NSG.</span></span> <span data-ttu-id="bc406-151">이 섹션에서는 설명 어떻게 toocreate hello에 대 한 추가 서브넷 NSG tooit tooallow에서 연결을 할당 하 고 네트워크 *myFrontendVM* 너무*myBackendVM* 포트 1433에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-151">In this section, you learn how toocreate an additional subnet in hello network and assign an NSG tooit tooallow a connection from *myFrontendVM* too*myBackendVM* on port 1433.</span></span> <span data-ttu-id="bc406-152">hello 서브넷 만들어질 때 toohello VM 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-152">hello subnet is then assigned toohello VM when it is created.</span></span>

<span data-ttu-id="bc406-153">내부 트래픽이 너무 제한할 수 있습니다*myBackendVM* 36 개월 *myFrontendVM* hello 백 엔드 서브넷에 NSG를 만들어서 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-153">You can limit internal traffic too*myBackendVM* from only *myFrontendVM* by creating an NSG for hello back-end subnet.</span></span> <span data-ttu-id="bc406-154">hello 다음 규칙을 만드는 예제는 NSG 라는 *myBackendNSGRule* 와 [새로 AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span><span class="sxs-lookup"><span data-stu-id="bc406-154">hello following example creates an NSG rule named *myBackendNSGRule* with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span></span>

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

<span data-ttu-id="bc406-155">[New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup)을 사용하여 *myBackendNSG*라는 네트워크 보안 그룹을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-155">Add a network security group named *myBackendNSG* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a><span data-ttu-id="bc406-156">백 엔드 서브넷 추가</span><span class="sxs-lookup"><span data-stu-id="bc406-156">Add back-end subnet</span></span>

<span data-ttu-id="bc406-157">추가 *myBackEndSubnet* 너무*myVNet* 와 [추가 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="bc406-157">Add *myBackEndSubnet* too*myVNet* with [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span></span>

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

## <a name="create-back-end-vm"></a><span data-ttu-id="bc406-158">백 엔드 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="bc406-158">Create back-end VM</span></span>

<span data-ttu-id="bc406-159">SQL Server 이미지를 사용 하 여 백 엔드 VM이 가장 쉬운 방법은 toocreate hello를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-159">hello easiest way toocreate hello back-end VM is by using a SQL Server image.</span></span> <span data-ttu-id="bc406-160">만이 자습서 hello VM hello 데이터베이스 서버와 만들지만 hello 데이터베이스에 액세스 하는 방법에 대 한 정보를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-160">This tutorial only creates hello VM with hello database server, but doesn't provide information about accessing hello database.</span></span>

<span data-ttu-id="bc406-161">*myBackendNic*을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-161">Create *myBackendNic*:</span></span>

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

<span data-ttu-id="bc406-162">Hello 사용자 이름 및 hello 관리자 계정 hello Get-credential을 사용 하 여 VM에 필요한 암호를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-162">Set hello username and password needed for hello administrator account on hello VM with Get-Credential:</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="bc406-163">*myBackendVM*을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-163">Create *myBackendVM*:</span></span>

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

<span data-ttu-id="bc406-164">사용 되는 hello 이미지 SQL server가 설치 된 있지만이 자습서에서 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-164">hello image that is used has SQL Server installed, but is not used in this tutorial.</span></span> <span data-ttu-id="bc406-165">포함된 tooshow는 하면 VM toohandle 웹 트래픽과 VM toohandle 데이터베이스 관리를 구성 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-165">It is included tooshow you how you can configure a VM toohandle web traffic and a VM toohandle database management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc406-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bc406-166">Next steps</span></span>

<span data-ttu-id="bc406-167">이 자습서에서 만든 및 보안 관련된 toovirtual 컴퓨터와 Azure 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-167">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="bc406-168">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="bc406-168">Create a virtual network</span></span>
> * <span data-ttu-id="bc406-169">가상 네트워크 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="bc406-169">Create virtual network subnets</span></span>
> * <span data-ttu-id="bc406-170">네트워크 보안 그룹을 사용하여 네트워크 트래픽 제어</span><span class="sxs-lookup"><span data-stu-id="bc406-170">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="bc406-171">트래픽 규칙의 실제 동작 보기</span><span class="sxs-lookup"><span data-stu-id="bc406-171">View traffic rules in action</span></span>

<span data-ttu-id="bc406-172">Azure 백업을 사용 하 여 가상 컴퓨터에서 보안 데이터를 모니터링 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-172">Advance toohello next tutorial toolearn about monitoring securing data on virtual machines using Azure backup.</span></span> <span data-ttu-id="bc406-173">에서도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc406-173">.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bc406-174">Azure에서 Windows 가상 컴퓨터 백업</span><span class="sxs-lookup"><span data-stu-id="bc406-174">Back up Windows virtual machines in Azure</span></span>](./tutorial-backup-vms.md)

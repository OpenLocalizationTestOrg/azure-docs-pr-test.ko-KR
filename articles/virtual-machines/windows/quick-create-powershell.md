---
title: "Azure 빠른 시작 - Windows VM 만들기 PowerShell | Microsoft Docs"
description: "PowerShell을 사용하여 Windows 가상 컴퓨터를 만드는 방법을 빠르게 이해합니다."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 8516cfa2272694496eb353a83eca77c13a516750
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a><span data-ttu-id="e5e3e-103">PowerShell을 사용하여 Windows 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="e5e3e-103">Create a Windows virtual machine with PowerShell</span></span>

<span data-ttu-id="e5e3e-104">PowerShell 명령줄 또는 스크립트에서 Azure 리소스를 만들고 관리하는 데 Azure PowerShell 모듈이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-104">The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts.</span></span> <span data-ttu-id="e5e3e-105">이 가이드에서는 PowerShell을 사용하여 Windows Server 2016이 실행되는 Azure Virtual Machine을 만드는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-105">This guide details using PowerShell to create and Azure virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="e5e3e-106">배포가 완료되면 서버에 연결하고 IIS를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-106">Once deployment is complete, we connect to the server and install IIS.</span></span>  

<span data-ttu-id="e5e3e-107">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="e5e3e-108">이 빠른 시작에서는 Azure PowerShell 모듈 버전 3.6 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-108">This quick start requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="e5e3e-109">` Get-Module -ListAvailable AzureRM`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-109">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="e5e3e-110">설치 또는 업그레이드해야 하는 경우 [Azure PowerShell 모듈 설치](/powershell/azure/install-azurerm-ps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-110">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="e5e3e-111">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="e5e3e-111">Log in to Azure</span></span>

<span data-ttu-id="e5e3e-112">`Login-AzureRmAccount` 명령으로 Azure 구독에 로그인하고 화면의 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-112">Log in to your Azure subscription with the `Login-AzureRmAccount` command and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="e5e3e-113">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="e5e3e-113">Create resource group</span></span>

<span data-ttu-id="e5e3e-114">[New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)을 사용하여 Azure 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-114">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="e5e3e-115">리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a><span data-ttu-id="e5e3e-116">네트워킹 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="e5e3e-116">Create networking resources</span></span>

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a><span data-ttu-id="e5e3e-117">가상 네트워크, 서브넷 및 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-117">Create a virtual network, subnet, and a public IP address.</span></span> 
<span data-ttu-id="e5e3e-118">이러한 리소스는 가상 컴퓨터에 네트워크 연결을 제공하고 인터넷에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-118">These resources are used to provide network connectivity to the virtual machine and connect it to the internet.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location EastUS `
    -Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location EastUS `
    -AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="e5e3e-119">네트워크 보안 그룹 및 네트워크 보안 그룹 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-119">Create a network security group and a network security group rule.</span></span> 
<span data-ttu-id="e5e3e-120">네트워크 보안 그룹은 인바운드 및 아웃바운드 규칙을 사용하여 가상 컴퓨터를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-120">The network security group secures the virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="e5e3e-121">이 경우 포트 3389에 대해 들어오는 원격 데스크톱 연결을 허용하는 인바운드 규칙이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-121">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span> <span data-ttu-id="e5e3e-122">포트 80에 대한 인바운드 규칙을 만들어서 들어오는 웹 트래픽을 허용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-122">We also want to create an inbound rule for port 80, which allows incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
    -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
    -Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location EastUS `
    -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP,$nsgRuleWeb
```

### <a name="create-a-network-card-for-the-virtual-machine"></a><span data-ttu-id="e5e3e-123">가상 컴퓨터에 대한 네트워크 카드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-123">Create a network card for the virtual machine.</span></span> 
<span data-ttu-id="e5e3e-124">[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface)를 사용하여 가상 컴퓨터에 네트워크 카드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-124">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for the virtual machine.</span></span> <span data-ttu-id="e5e3e-125">네트워크 카드는 서브넷, 네트워크 보안 그룹 및 공용 IP 주소에 가상 컴퓨터를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-125">The network card connects the virtual machine to a subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="e5e3e-126">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="e5e3e-126">Create virtual machine</span></span>

<span data-ttu-id="e5e3e-127">가상 컴퓨터 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-127">Create a virtual machine configuration.</span></span> <span data-ttu-id="e5e3e-128">이 구성은 가상 컴퓨터 이미지, 크기 및 인증 구성 등 가상 컴퓨터를 배포할 때 사용되는 설정을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-128">This configuration includes the settings that are used when deploying the virtual machine such as a virtual machine image, size, and authentication configuration.</span></span> <span data-ttu-id="e5e3e-129">이 단계를 실행할 때 자격 증명을 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-129">When running this step, you are prompted for credentials.</span></span> <span data-ttu-id="e5e3e-130">입력하는 값은 가상 컴퓨터에 대한 사용자 이름 및 암호로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-130">The values that you enter are configured as the user name and password for the virtual machine.</span></span>

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

<span data-ttu-id="e5e3e-131">[New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)을 사용하여 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-131">Create the virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-to-virtual-machine"></a><span data-ttu-id="e5e3e-132">가상 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="e5e3e-132">Connect to virtual machine</span></span>

<span data-ttu-id="e5e3e-133">배포가 완료된 후 가상 컴퓨터에 대한 원격 데스크톱 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-133">After the deployment has completed, create a remote desktop connection with the virtual machine.</span></span>

<span data-ttu-id="e5e3e-134">[Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) 명령을 사용하여 가상 컴퓨터의 공용 IP 주소를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-134">Use the [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command to return the public IP address of the virtual machine.</span></span> <span data-ttu-id="e5e3e-135">다음 단계에서 웹 연결을 테스트하기 위해 브라우저와 연결할 수 있도록 이 IP 주소를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-135">Take note of this IP Address so you can connect to it with your browser to test web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="e5e3e-136">다음 명령을 사용하여 가상 컴퓨터와의 원격 데스크톱 세션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-136">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="e5e3e-137">해당 IP 주소를 가상 컴퓨터의 *publicIPAddress*로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-137">Replace the IP address with the *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="e5e3e-138">가상 컴퓨터를 만들 때 사용되는 자격 증명을 묻는 메시지가 표시되면 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-138">When prompted, enter the credentials used when creating the virtual machine.</span></span>

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a><span data-ttu-id="e5e3e-139">PowerShell을 통해 IIS 설치</span><span class="sxs-lookup"><span data-stu-id="e5e3e-139">Install IIS via PowerShell</span></span>

<span data-ttu-id="e5e3e-140">이제 Azure VM에 로그인했으므로 IIS를 설치하고 웹 트래픽을 허용하는 로컬 방화벽 규칙을 사용하려면 PowerShell의 단일 줄을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-140">Now that you have logged in to the Azure VM, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="e5e3e-141">PowerShell 프롬프트를 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-141">Open a PowerShell prompt and run the following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="e5e3e-142">IIS 시작 페이지 보기</span><span class="sxs-lookup"><span data-stu-id="e5e3e-142">View the IIS welcome page</span></span>

<span data-ttu-id="e5e3e-143">IIS를 설치하고 현재 포트 80이 인터넷에서 VM에 열려 있으면 사용자가 선택한 웹 브라우저를 사용하여 기본 IIS 시작 페이지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-143">With IIS installed and port 80 now open on your VM from the Internet, you can use a web browser of your choice to view the default IIS welcome page.</span></span> <span data-ttu-id="e5e3e-144">위에 설명한 *publicIpAddress*를 사용하여 기본 페이지를 방문해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-144">Be sure to use the *publicIpAddress* you documented above to visit the default page.</span></span> 

![IIS 기본 사이트](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="e5e3e-146">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="e5e3e-146">Clean up resources</span></span>

<span data-ttu-id="e5e3e-147">더 이상 필요하지 않은 경우 [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) 명령을 사용하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-147">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="e5e3e-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e5e3e-148">Next steps</span></span>

<span data-ttu-id="e5e3e-149">이 빠른 시작에서 간단한 가상 컴퓨터, 네트워크 보안 그룹 규칙을 배포했으며 웹 서버를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-149">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="e5e3e-150">Azure 가상 컴퓨터에 대한 자세한 내용을 알아보려면 Windows VM의 자습서를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e3e-150">To learn more about Azure virtual machines, continue to the tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e5e3e-151">Azure Windows 가상 컴퓨터 자습서</span><span class="sxs-lookup"><span data-stu-id="e5e3e-151">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)

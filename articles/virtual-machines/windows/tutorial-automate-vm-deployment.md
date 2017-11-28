---
title: "Azure에서 Windows VM 사용자 지정 | Microsoft Docs"
description: "사용자 지정 스크립트 확장 및 Key Vault를 사용하여 Azure에서 Windows VM을 사용자 지정하는 방법에 대해 알아봅니다."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 3be58bf8afbcff018b2b0d69a0e08c2c9ab1fca7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-customize-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="42db6-103">Azure에서 Windows 가상 컴퓨터를 사용자 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="42db6-103">How to customize a Windows virtual machine in Azure</span></span>
<span data-ttu-id="42db6-104">신속하고 일관된 방식으로 VM(Virtual Machines)을 구성하려면 일반적으로 자동화 양식이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-104">To configure virtual machines (VMs) in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="42db6-105">Windows VM을 사용자 지정하는 일반적인 방법은 [Windows용 사용자 지정 스크립트 확장](extensions-customscript.md)을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-105">A common approach to customize a Windows VM is to use [Custom Script Extension for Windows](extensions-customscript.md).</span></span> <span data-ttu-id="42db6-106">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="42db6-107">사용자 지정 스크립트 확장을 사용하여 IIS 설치</span><span class="sxs-lookup"><span data-stu-id="42db6-107">Use the Custom Script Extension to install IIS</span></span>
> * <span data-ttu-id="42db6-108">사용자 지정 스크립트 확장을 사용하는 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="42db6-108">Create a VM that uses the Custom Script Extension</span></span>
> * <span data-ttu-id="42db6-109">확장이 적용된 후 실행 중인 IIS 사이트 보기</span><span class="sxs-lookup"><span data-stu-id="42db6-109">View a running IIS site after the extension is applied</span></span>

<span data-ttu-id="42db6-110">이 자습서에는 Azure PowerShell 모듈 버전 3.6 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-110">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="42db6-111">` Get-Module -ListAvailable AzureRM`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-111">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="42db6-112">업그레이드해야 하는 경우 [Azure PowerShell 모듈 설치](/powershell/azure/install-azurerm-ps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="42db6-112">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="custom-script-extension-overview"></a><span data-ttu-id="42db6-113">사용자 지정 스크립트 확장 개요</span><span class="sxs-lookup"><span data-stu-id="42db6-113">Custom script extension overview</span></span>
<span data-ttu-id="42db6-114">사용자 지정 스크립트 확장은 Azure VM에서 스크립트를 다운로드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-114">The Custom Script Extension downloads and executes scripts on Azure VMs.</span></span> <span data-ttu-id="42db6-115">이 확장은 배포 후 구성, 소프트웨어 설치 또는 기타 구성/관리 작업에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-115">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="42db6-116">스크립트를 Azure Storage 또는 GitHub에서 다운로드하거나 확장 런타임에서 Azure Portal에 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-116">Scripts can be downloaded from Azure storage or GitHub, or provided to the Azure portal at extension run time.</span></span>

<span data-ttu-id="42db6-117">사용자 지정 스크립트 확장은 Azure Resource Manager 템플릿과 통합되고, Azure CLI, PowerShell, Azure Portal 또는 Azure 가상 컴퓨터 REST API를 사용하여 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-117">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="42db6-118">Windows VM 및 Linux VM 둘 다에 사용자 지정 스크립트 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-118">You can use the Custom Script Extension with both Windows and Linux VMs.</span></span>


## <a name="create-virtual-machine"></a><span data-ttu-id="42db6-119">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="42db6-119">Create virtual machine</span></span>
<span data-ttu-id="42db6-120">VM을 만들려면 먼저 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-120">Before you can create a VM, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="42db6-121">다음 예제에서는 *EastUS* 위치에 *myResourceGroupAutomate*라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-121">The following example creates a resource group named *myResourceGroupAutomate* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

<span data-ttu-id="42db6-122">[Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential)을 사용하여 VM의 관리자 사용자 이름과 암호를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-122">Set an administrator username and password for the VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="42db6-123">이제 [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)을 사용하여 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-123">Now you can create the VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="42db6-124">다음 예제에서는 필요한 가상 네트워크 구성 요소, OS 구성을 만든 다음 *myVM*이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-124">The following example creates the required virtual network components, the OS configuration, and then creates a VM named *myVM*:</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName myResourceGroupAutomate -Location EastUS -VM $vmConfig
```

<span data-ttu-id="42db6-125">리소스 및 VM을 만드는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-125">It takes a few minutes for the resources and VM to be created.</span></span>


## <a name="automate-iis-install"></a><span data-ttu-id="42db6-126">IIS 설치 자동화</span><span class="sxs-lookup"><span data-stu-id="42db6-126">Automate IIS install</span></span>
<span data-ttu-id="42db6-127">[Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension)을 사용하여 사용자 지정 스크립트 확장을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-127">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to install the Custom Script Extension.</span></span> <span data-ttu-id="42db6-128">확장은 `powershell Add-WindowsFeature Web-Server`를 실행하여 IIS 웹 서버를 설치한 다음 *Default.htm* 페이지를 업데이트하여 VM의 호스트 이름을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-128">The extension runs `powershell Add-WindowsFeature Web-Server` to install the IIS webserver and then updates the *Default.htm* page to show the hostname of the VM:</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName myResourceGroupAutomate `
    -ExtensionName IIS `
    -VMName myVM `
    -Publisher Microsoft.Compute `
    -ExtensionType CustomScriptExtension `
    -TypeHandlerVersion 1.4 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
    -Location EastUS
```


## <a name="test-web-site"></a><span data-ttu-id="42db6-129">웹 사이트 테스트</span><span class="sxs-lookup"><span data-stu-id="42db6-129">Test web site</span></span>
<span data-ttu-id="42db6-130">[Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)를 사용하여 부하 분산 장치의 공용 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-130">Obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="42db6-131">다음 예제에서는 앞서 만든 *myPublicIP*의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-131">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

<span data-ttu-id="42db6-132">그런 다음 웹 브라우저에 공용 IP 주소를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-132">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="42db6-133">다음 예제와 같이 부하 분산 장치가 트래픽을 분산한 VM의 호스트 이름을 포함하여 웹 사이트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-133">The website is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![실행 중인 IIS 웹 사이트](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a><span data-ttu-id="42db6-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="42db6-135">Next steps</span></span>

<span data-ttu-id="42db6-136">이 자습서에서는 VM에서 IIS 설치를 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-136">In this tutorial, you automated the IIS install on a VM.</span></span> <span data-ttu-id="42db6-137">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-137">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="42db6-138">사용자 지정 스크립트 확장을 사용하여 IIS 설치</span><span class="sxs-lookup"><span data-stu-id="42db6-138">Use the Custom Script Extension to install IIS</span></span>
> * <span data-ttu-id="42db6-139">사용자 지정 스크립트 확장을 사용하는 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="42db6-139">Create a VM that uses the Custom Script Extension</span></span>
> * <span data-ttu-id="42db6-140">확장이 적용된 후 실행 중인 IIS 사이트 보기</span><span class="sxs-lookup"><span data-stu-id="42db6-140">View a running IIS site after the extension is applied</span></span>

<span data-ttu-id="42db6-141">사용자 지정 VM 이미지를 만드는 방법에 대해 알아보려면 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="42db6-141">Advance to the next tutorial to learn how to create custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="42db6-142">사용자 지정 VM 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="42db6-142">Create custom VM images</span></span>](./tutorial-custom-images.md)

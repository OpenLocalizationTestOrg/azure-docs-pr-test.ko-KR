---
title: "Azure에서 Windows VM aaaCustomize | Microsoft Docs"
description: "사용자 지정 스크립트 확장 하 고 Windows Vm에 Azure 키 자격 증명 모음 toocustomize toouse hello 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: c03b2bb6d70875134c63ea2fe4c2e2c1777c2188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="6bc7c-103">어떻게 toocustomize Azure에서 Windows 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="6bc7c-103">How toocustomize a Windows virtual machine in Azure</span></span>
<span data-ttu-id="6bc7c-104">가상 컴퓨터 (Vm)는 신속 하 고 일관 된 방식으로 자동화 tooconfigure 방법이 일반적으로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc7c-104">tooconfigure virtual machines (VMs) in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="6bc7c-105">일반적인 접근 방식을 toocustomize Windows VM은 toouse [Windows에 대 한 사용자 지정 스크립트 확장](extensions-customscript.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc7c-105">A common approach toocustomize a Windows VM is toouse [Custom Script Extension for Windows](extensions-customscript.md).</span></span> <span data-ttu-id="6bc7c-106">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6bc7c-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6bc7c-107">Hello 사용자 지정 스크립트 확장 tooinstall IIS를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6bc7c-107">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="6bc7c-108">Hello 사용자 지정 스크립트 확장을 사용 하는 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="6bc7c-108">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="6bc7c-109">Hello 확장이 적용 된 후 실행 중인 IIS 사이트를 보려면</span><span class="sxs-lookup"><span data-stu-id="6bc7c-109">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="6bc7c-110">이 자습서는 Azure PowerShell 모듈 버전 3.6 이상 hello가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc7c-110">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="6bc7c-111">실행 ` Get-Module -ListAvailable AzureRM` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="6bc7c-111">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="6bc7c-112">Tooupgrade 필요한 경우 참조 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc7c-112">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="custom-script-extension-overview"></a><span data-ttu-id="6bc7c-113">사용자 지정 스크립트 확장 개요</span><span class="sxs-lookup"><span data-stu-id="6bc7c-113">Custom script extension overview</span></span>
<span data-ttu-id="6bc7c-114">사용자 지정 스크립트 확장 hello 다운로드 하 고 Azure Vm에서 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc7c-114">hello Custom Script Extension downloads and executes scripts on Azure VMs.</span></span> <span data-ttu-id="6bc7c-115">이 확장은 배포 후 구성, 소프트웨어 설치 또는 기타 구성/관리 작업에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc7c-115">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="6bc7c-116">스크립트는 Azure 저장소 또는 GitHub에서 다운로드 또는 toohello Azure 포털 확장 실행 시간에 제공 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bc7c-116">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span>

<span data-ttu-id="6bc7c-117">사용자 지정 스크립트 확장 hello Azure 리소스 관리자 템플릿 뿐 아니라 통합 하 고 hello Azure CLI, PowerShell, Azure 포털 또는 hello Azure 가상 컴퓨터 REST API를 사용 하 여 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bc7c-117">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="6bc7c-118">Windows와 Linux Vm의 경우와 hello 사용자 지정 스크립트 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bc7c-118">You can use hello Custom Script Extension with both Windows and Linux VMs.</span></span>


## <a name="create-virtual-machine"></a><span data-ttu-id="6bc7c-119">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="6bc7c-119">Create virtual machine</span></span>
<span data-ttu-id="6bc7c-120">VM을 만들려면 먼저 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bc7c-120">Before you can create a VM, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="6bc7c-121">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupAutomate* hello에 *EastUS* 위치:</span><span class="sxs-lookup"><span data-stu-id="6bc7c-121">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

<span data-ttu-id="6bc7c-122">된 hello Vm에 대 한 관리자 사용자 이름 및 암호 설정 [Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="6bc7c-122">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="6bc7c-123">이제 만들 수 있는 VM hello [새로 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc7c-123">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="6bc7c-124">hello 다음 예제에서는 운영 체제 hello 구성 hello 필요한 가상 네트워크 구성 요소를 만든 다음 만듭니다 라는 VM *myVM*:</span><span class="sxs-lookup"><span data-stu-id="6bc7c-124">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

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

<span data-ttu-id="6bc7c-125">Hello 리소스와 VM toobe 생성에 대 한 몇 가지 분 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="6bc7c-125">It takes a few minutes for hello resources and VM toobe created.</span></span>


## <a name="automate-iis-install"></a><span data-ttu-id="6bc7c-126">IIS 설치 자동화</span><span class="sxs-lookup"><span data-stu-id="6bc7c-126">Automate IIS install</span></span>
<span data-ttu-id="6bc7c-127">사용 하 여 [집합 AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello 사용자 지정 스크립트 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc7c-127">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="6bc7c-128">확장 실행 hello `powershell Add-WindowsFeature Web-Server` IIS 웹 서버 및 업데이트 hello tooinstall hello *Default.htm* hello VM의 페이지 tooshow hello 호스트 이름:</span><span class="sxs-lookup"><span data-stu-id="6bc7c-128">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

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


## <a name="test-web-site"></a><span data-ttu-id="6bc7c-129">웹 사이트 테스트</span><span class="sxs-lookup"><span data-stu-id="6bc7c-129">Test web site</span></span>
<span data-ttu-id="6bc7c-130">Hello 있는 부하 분산 장치 프로그램의 공용 IP 주소 가져오기 [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc7c-130">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="6bc7c-131">hello 다음 예제에서는 가져옵니다 hello IP 주소를 *myPublicIP* 앞에서 만든:</span><span class="sxs-lookup"><span data-stu-id="6bc7c-131">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

<span data-ttu-id="6bc7c-132">그런 다음 tooa 웹 브라우저에서 hello 공용 IP 주소를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bc7c-132">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="6bc7c-133">hello 웹 사이트가 표시 되어, hello VM의 hello 호스트 이름을 포함 하 여 해당 hello 부하 분산 장치는 hello 다음 예제에서에서 트래픽 tooas 분산:</span><span class="sxs-lookup"><span data-stu-id="6bc7c-133">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![실행 중인 IIS 웹 사이트](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a><span data-ttu-id="6bc7c-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6bc7c-135">Next steps</span></span>

<span data-ttu-id="6bc7c-136">이 자습서에서는 VM에 IIS를 설치 하는 hello를 자동화 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bc7c-136">In this tutorial, you automated hello IIS install on a VM.</span></span> <span data-ttu-id="6bc7c-137">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="6bc7c-137">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6bc7c-138">Hello 사용자 지정 스크립트 확장 tooinstall IIS를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6bc7c-138">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="6bc7c-139">Hello 사용자 지정 스크립트 확장을 사용 하는 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="6bc7c-139">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="6bc7c-140">Hello 확장이 적용 된 후 실행 중인 IIS 사이트를 보려면</span><span class="sxs-lookup"><span data-stu-id="6bc7c-140">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="6bc7c-141">다음 자습서 toolearn toohello 어떻게 발전 toocreate 사용자 지정 VM 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="6bc7c-141">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6bc7c-142">사용자 지정 VM 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="6bc7c-142">Create custom VM images</span></span>](./tutorial-custom-images.md)

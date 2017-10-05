---
title: "Azure 빠른 시작 - VM 만들기 PowerShell | Microsoft Docs"
description: "PowerShell을 사용하여 Linux 가상 컴퓨터를 만드는 방법을 빠르게 이해합니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: adcf492d4c2d935c880167675a1ed97566156ec7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a><span data-ttu-id="11a3d-103">PowerShell을 사용하여 Linux 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="11a3d-103">Create a Linux virtual machine with PowerShell</span></span>

<span data-ttu-id="11a3d-104">PowerShell 명령줄 또는 스크립트에서 Azure 리소스를 만들고 관리하는 데 Azure PowerShell 모듈이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-104">The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts.</span></span> <span data-ttu-id="11a3d-105">이 가이드에서는 Azure PowerShell 모듈을 사용하여 Ubuntu 서버가 실행되는 가상 컴퓨터를 배포하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-105">This guide details using the Azure PowerShell module to deploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="11a3d-106">서버가 배포되면 SSH 연결을 만들고 NGINX 웹 서버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-106">Once the server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="11a3d-107">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="11a3d-108">이 빠른 시작에서는 Azure PowerShell 모듈 버전 3.6 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-108">This quick start requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="11a3d-109">` Get-Module -ListAvailable AzureRM`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-109">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="11a3d-110">설치 또는 업그레이드해야 하는 경우 [Azure PowerShell 모듈 설치](/powershell/azure/install-azurerm-ps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11a3d-110">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="11a3d-111">마지막으로 이름이 *id_rsa.pub*인 공용 SSH 키가 Windows 사용자 프로필의 *.ssh* 디렉터리에 저장되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-111">Finally, a public SSH key with the name *id_rsa.pub* needs to be stored in the *.ssh* directory of your Windows user profile.</span></span> <span data-ttu-id="11a3d-112">Azure에 대한 SSH 키 만들기에 대한 자세한 내용은 [Azure용 SSH 키 만들기](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11a3d-112">For detailed information on creating SSH keys for Azure, see [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="11a3d-113">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="11a3d-113">Log in to Azure</span></span>

<span data-ttu-id="11a3d-114">`Login-AzureRmAccount` 명령으로 Azure 구독에 로그인하고 화면의 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-114">Log in to your Azure subscription with the `Login-AzureRmAccount` command and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="11a3d-115">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="11a3d-115">Create resource group</span></span>

<span data-ttu-id="11a3d-116">[New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)을 사용하여 Azure 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-116">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="11a3d-117">리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-117">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a><span data-ttu-id="11a3d-118">네트워킹 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="11a3d-118">Create networking resources</span></span>

<span data-ttu-id="11a3d-119">가상 네트워크, 서브넷 및 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-119">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="11a3d-120">이러한 리소스는 가상 컴퓨터에 네트워크 연결을 제공하고 인터넷에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-120">These resources are used to provide network connectivity to the virtual machine and connect it to the internet.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location eastus `
-Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location eastus `
-AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

<span data-ttu-id="11a3d-121">네트워크 보안 그룹 및 네트워크 보안 그룹 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-121">Create a network security group and a network security group rule.</span></span> <span data-ttu-id="11a3d-122">네트워크 보안 그룹은 인바운드 및 아웃바운드 규칙을 사용하여 가상 컴퓨터를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-122">The network security group secures the virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="11a3d-123">이 경우 포트 22에 대해 들어오는 SSH 연결을 허용하는 인바운드 규칙이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-123">In this case, an inbound rule is created for port 22, which allows incoming SSH connections.</span></span> <span data-ttu-id="11a3d-124">포트 80에 대한 인바운드 규칙을 만들어서 들어오는 웹 트래픽을 허용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-124">We also want to create an inbound rule for port 80, which allows incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 22
$nsgRuleSSH = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleSSH  -Protocol Tcp `
-Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 22 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
-Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location eastus `
-Name myNetworkSecurityGroup -SecurityRules $nsgRuleSSH,$nsgRuleWeb
```

<span data-ttu-id="11a3d-125">[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface)를 사용하여 가상 컴퓨터에 네트워크 카드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-125">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for the virtual machine.</span></span> <span data-ttu-id="11a3d-126">네트워크 카드는 서브넷, 네트워크 보안 그룹 및 공용 IP 주소에 가상 컴퓨터를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-126">The network card connects the virtual machine to a subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="11a3d-127">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="11a3d-127">Create virtual machine</span></span>

<span data-ttu-id="11a3d-128">가상 컴퓨터 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-128">Create a virtual machine configuration.</span></span> <span data-ttu-id="11a3d-129">이 구성은 가상 컴퓨터 이미지, 크기 및 인증 구성 등 가상 컴퓨터를 배포할 때 사용되는 설정을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-129">This configuration includes the settings that are used when deploying the virtual machine such as a virtual machine image, size, and authentication configuration.</span></span>

```powershell
# Define a credential object
$securePassword = ConvertTo-SecureString ' ' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("azureuser", $securePassword)

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Linux -ComputerName myVM -Credential $cred -DisablePasswordAuthentication | `
Set-AzureRmVMSourceImage -PublisherName Canonical -Offer UbuntuServer -Skus 14.04.2-LTS -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Configure SSH Keys
$sshPublicKey = Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub"
Add-AzureRmVMSshPublicKey -VM $vmconfig -KeyData $sshPublicKey -Path "/home/azureuser/.ssh/authorized_keys"
```

<span data-ttu-id="11a3d-130">[New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)을 사용하여 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-130">Create the virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-to-virtual-machine"></a><span data-ttu-id="11a3d-131">가상 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="11a3d-131">Connect to virtual machine</span></span>

<span data-ttu-id="11a3d-132">배포가 완료된 후 가상 컴퓨터에 대한 SSH 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-132">After the deployment has completed, create an SSH connection with the virtual machine.</span></span>

<span data-ttu-id="11a3d-133">[Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) 명령을 사용하여 가상 컴퓨터의 공용 IP 주소를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-133">Use the [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command to return the public IP address of the virtual machine.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="11a3d-134">SSH가 설치된 시스템에서 다음 명령을 사용하여 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-134">From a system with SSH installed, used the following command to connect to the virtual machine.</span></span> <span data-ttu-id="11a3d-135">Windows에서 작업하는 경우 [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty)를 사용하여 연결을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-135">If working on Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) can be used to create the connection.</span></span> 

```bash 
ssh <Public IP Address>
```

<span data-ttu-id="11a3d-136">로그인 사용자 이름을 묻는 메시지가 표시되면 *azureuser*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-136">When prompted, the login user name is *azureuser*.</span></span> <span data-ttu-id="11a3d-137">SSH 키를 만들 때 암호가 입력된 경우 이 암호도 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-137">If a passphrase was entered when creating SSH keys, you need to enter this as well.</span></span>


## <a name="install-nginx"></a><span data-ttu-id="11a3d-138">NGINX 설치</span><span class="sxs-lookup"><span data-stu-id="11a3d-138">Install NGINX</span></span>

<span data-ttu-id="11a3d-139">다음 bash 스크립트를 사용하여 패키지 원본을 업데이트하고 최신 NGINX 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-139">Use the following bash script to update package sources and install the latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-the-ngix-welcome-page"></a><span data-ttu-id="11a3d-140">NGIX 시작 페이지 보기</span><span class="sxs-lookup"><span data-stu-id="11a3d-140">View the NGIX welcome page</span></span>

<span data-ttu-id="11a3d-141">NGINX를 설치하고 현재 포트 80이 인터넷에서 VM에 열려 있으면 사용자가 선택한 웹 브라우저를 사용하여 기본 NGINX 시작 페이지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-141">With NGINX installed and port 80 now open on your VM from the Internet - you can use a web browser of your choice to view the default NGINX welcome page.</span></span> <span data-ttu-id="11a3d-142">위에 설명한 공용 IP 주소를 사용하여 기본 페이지를 방문해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-142">Be sure to use the public IP address you documented above to visit the default page.</span></span> 

![NGINX 기본 사이트](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="11a3d-144">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="11a3d-144">Clean up resources</span></span>

<span data-ttu-id="11a3d-145">더 이상 필요하지 않은 경우 [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) 명령을 사용하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-145">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="11a3d-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="11a3d-146">Next steps</span></span>

<span data-ttu-id="11a3d-147">이 빠른 시작에서 간단한 가상 컴퓨터, 네트워크 보안 그룹 규칙을 배포했으며 웹 서버를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-147">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="11a3d-148">Azure 가상 컴퓨터에 대한 자세한 내용을 알아보려면 Linux VM의 자습서를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="11a3d-148">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="11a3d-149">Azure Linux 가상 컴퓨터 자습서</span><span class="sxs-lookup"><span data-stu-id="11a3d-149">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)

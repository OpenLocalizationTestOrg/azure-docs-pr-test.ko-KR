---
title: "빠른 시작-aaaAzure VM PowerShell 만들기 | Microsoft Docs"
description: "Toocreate PowerShell과 함께 Linux 가상 컴퓨터를 빠르게 배울"
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
ms.openlocfilehash: f05ea7fedafe4fda660dc6084ae57ebf9dced473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a><span data-ttu-id="d745b-103">PowerShell을 사용하여 Linux 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="d745b-103">Create a Linux virtual machine with PowerShell</span></span>

<span data-ttu-id="d745b-104">hello Azure PowerShell 모듈에 사용 되는 toocreate 이며 hello PowerShell 명령줄에서 또는 스크립트에서 Azure 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-104">hello Azure PowerShell module is used toocreate and manage Azure resources from hello PowerShell command line or in scripts.</span></span> <span data-ttu-id="d745b-105">Ubuntu server를 실행 하는 가상 컴퓨터 Azure PowerShell 모듈 toodeploy hello를 사용 하 여이 가이드 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-105">This guide details using hello Azure PowerShell module toodeploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="d745b-106">Hello 서버 배포 되 면 SSH 연결을 만들고 및는 NGINX 웹 서버에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-106">Once hello server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="d745b-107">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="d745b-108">이 빠른 시작 hello Azure PowerShell 모듈 버전 3.6 이상 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-108">This quick start requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="d745b-109">실행 ` Get-Module -ListAvailable AzureRM` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="d745b-110">Tooinstall 또는 업그레이드를 보려면 참고 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="d745b-111">Hello 이름의 공용 SSH 키 마지막으로, *id_rsa.pub* hello에 저장 된 toobe 필요한 *.ssh* Windows 사용자 프로필의 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-111">Finally, a public SSH key with hello name *id_rsa.pub* needs toobe stored in hello *.ssh* directory of your Windows user profile.</span></span> <span data-ttu-id="d745b-112">Azure에 대한 SSH 키 만들기에 대한 자세한 내용은 [Azure용 SSH 키 만들기](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d745b-112">For detailed information on creating SSH keys for Azure, see [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="d745b-113">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="d745b-113">Log in tooAzure</span></span>

<span data-ttu-id="d745b-114">Tooyour hello로 Azure 구독에에서 로그인 `Login-AzureRmAccount` 명령 열고 지시를 따른 hello 화면에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-114">Log in tooyour Azure subscription with hello `Login-AzureRmAccount` command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="d745b-115">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="d745b-115">Create resource group</span></span>

<span data-ttu-id="d745b-116">[New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)을 사용하여 Azure 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-116">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="d745b-117">리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-117">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a><span data-ttu-id="d745b-118">네트워킹 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="d745b-118">Create networking resources</span></span>

<span data-ttu-id="d745b-119">가상 네트워크, 서브넷 및 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-119">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="d745b-120">이러한 리소스 사용 되는 tooprovide 네트워크 연결 toohello 가상 컴퓨터를 toohello 연결 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-120">These resources are used tooprovide network connectivity toohello virtual machine and connect it toohello internet.</span></span>

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

<span data-ttu-id="d745b-121">네트워크 보안 그룹 및 네트워크 보안 그룹 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-121">Create a network security group and a network security group rule.</span></span> <span data-ttu-id="d745b-122">네트워크 보안 그룹을 hello 인바운드 및 아웃 바운드 규칙을 사용 하 여 hello 가상 컴퓨터를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-122">hello network security group secures hello virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="d745b-123">이 경우 포트 22에 대해 들어오는 SSH 연결을 허용하는 인바운드 규칙이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-123">In this case, an inbound rule is created for port 22, which allows incoming SSH connections.</span></span> <span data-ttu-id="d745b-124">또한 들어오는 웹 트래픽이 허용 하는 포트 80, toocreate는 인바운드 규칙 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-124">We also want toocreate an inbound rule for port 80, which allows incoming web traffic.</span></span>

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

<span data-ttu-id="d745b-125">와 네트워크 카드를 만들고 [새로 AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) hello 가상 컴퓨터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-125">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for hello virtual machine.</span></span> <span data-ttu-id="d745b-126">hello 네트워크 카드 hello 가상 컴퓨터 tooa 서브넷, 네트워크 보안 그룹 및 공용 IP 주소에 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-126">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="d745b-127">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="d745b-127">Create virtual machine</span></span>

<span data-ttu-id="d745b-128">가상 컴퓨터 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-128">Create a virtual machine configuration.</span></span> <span data-ttu-id="d745b-129">이 구성은 가상 컴퓨터 이미지, 크기 및 인증 구성과 같은 hello 가상 컴퓨터를 배포할 때 사용 되는 hello 설정을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-129">This configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, and authentication configuration.</span></span>

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

<span data-ttu-id="d745b-130">Hello 가상 컴퓨터를 만들 [새로 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)합니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-130">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a><span data-ttu-id="d745b-131">Toovirtual 컴퓨터 연결</span><span class="sxs-lookup"><span data-stu-id="d745b-131">Connect toovirtual machine</span></span>

<span data-ttu-id="d745b-132">Hello 배포 완료 되 면 hello 가상 컴퓨터와 SSH 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-132">After hello deployment has completed, create an SSH connection with hello virtual machine.</span></span>

<span data-ttu-id="d745b-133">사용 하 여 hello [Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) hello 가상 컴퓨터의 tooreturn hello 공용 IP 주소를 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-133">Use hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command tooreturn hello public IP address of hello virtual machine.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="d745b-134">SSH 설치 된 시스템에서는 사용 되는 hello 다음 tooconnect toohello 가상 컴퓨터 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-134">From a system with SSH installed, used hello following command tooconnect toohello virtual machine.</span></span> <span data-ttu-id="d745b-135">Windows에서 작업 하는 경우 [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) 사용된 toocreate hello 연결 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-135">If working on Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) can be used toocreate hello connection.</span></span> 

```bash 
ssh <Public IP Address>
```

<span data-ttu-id="d745b-136">Hello 로그인 사용자 이름에는 대화 상자가 나타나면 *azureuser*합니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-136">When prompted, hello login user name is *azureuser*.</span></span> <span data-ttu-id="d745b-137">SSH 키를 만들 때 암호를 입력 하는 경우 tooenter도이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-137">If a passphrase was entered when creating SSH keys, you need tooenter this as well.</span></span>


## <a name="install-nginx"></a><span data-ttu-id="d745b-138">NGINX 설치</span><span class="sxs-lookup"><span data-stu-id="d745b-138">Install NGINX</span></span>

<span data-ttu-id="d745b-139">사용 하 여 hello 다음 스크립트 tooupdate 패키지 소스를 이용한 적 하 고 hello 최신 NGINX 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-139">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-ngix-welcome-page"></a><span data-ttu-id="d745b-140">Hello NGIX 시작 페이지 보기</span><span class="sxs-lookup"><span data-stu-id="d745b-140">View hello NGIX welcome page</span></span>

<span data-ttu-id="d745b-141">설치 NGINX 및 포트 80이 이제 열려 hello-인터넷에서에서 VM에 사용 하 여 선택한 tooview hello 기본 NGINX 시작 페이지의 웹 브라우저를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-141">With NGINX installed and port 80 now open on your VM from hello Internet - you can use a web browser of your choice tooview hello default NGINX welcome page.</span></span> <span data-ttu-id="d745b-142">있는지 toouse hello 공용 IP 주소 toovisit hello 기본 페이지 위에 설명한 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-142">Be sure toouse hello public IP address you documented above toovisit hello default page.</span></span> 

![NGINX 기본 사이트](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="d745b-144">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="d745b-144">Clean up resources</span></span>

<span data-ttu-id="d745b-145">더 이상 필요 hello를 사용할 수 없습니다 [제거 AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-145">When no longer needed, you can use hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="d745b-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d745b-146">Next steps</span></span>

<span data-ttu-id="d745b-147">이 빠른 시작에서 간단한 가상 컴퓨터, 네트워크 보안 그룹 규칙을 배포했으며 웹 서버를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-147">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="d745b-148">Azure 가상 컴퓨터에 대해 자세히 toolearn Linux Vm에 대 한 toohello 자습서를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745b-148">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d745b-149">Azure Linux 가상 컴퓨터 자습서</span><span class="sxs-lookup"><span data-stu-id="d745b-149">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)

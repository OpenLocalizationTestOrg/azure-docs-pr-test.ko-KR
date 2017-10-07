---
title: "빠른 시작-aaaAzure Windows VM PowerShell 만들기 | Microsoft Docs"
description: "Toocreate PowerShell 사용한 Windows 가상 컴퓨터를 빠르게 배울"
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
ms.openlocfilehash: 5e92435bf7ee443a01c158fed91c356363e2f425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a>PowerShell을 사용하여 Windows 가상 컴퓨터 만들기

hello Azure PowerShell 모듈에 사용 되는 toocreate 이며 hello PowerShell 명령줄에서 또는 스크립트에서 Azure 리소스를 관리 합니다. PowerShell toocreate 및 Windows Server 2016을 실행 하는 Azure 가상 컴퓨터를 사용 하 여이 가이드 정보입니다. 배포가 완료 되 면 toohello 서버 연결 고 IIS를 설치 했습니다.  

Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.

이 빠른 시작 hello Azure PowerShell 모듈 버전 3.6 이상 필요합니다. 실행 ` Get-Module -ListAvailable AzureRM` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.

## <a name="log-in-tooazure"></a>TooAzure 로그인

Tooyour hello로 Azure 구독에에서 로그인 `Login-AzureRmAccount` 명령 열고 지시를 따른 hello 화면에 표시 합니다.

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a>리소스 그룹 만들기

[New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)을 사용하여 Azure 리소스 그룹을 만듭니다. 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a>네트워킹 리소스 만들기

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a>가상 네트워크, 서브넷 및 공용 IP 주소를 만듭니다. 
이러한 리소스 사용 되는 tooprovide 네트워크 연결 toohello 가상 컴퓨터를 toohello 연결 인터넷 합니다.

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

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a>네트워크 보안 그룹 및 네트워크 보안 그룹 규칙을 만듭니다. 
네트워크 보안 그룹을 hello 인바운드 및 아웃 바운드 규칙을 사용 하 여 hello 가상 컴퓨터를 보호 합니다. 이 경우 포트 3389에 대해 들어오는 원격 데스크톱 연결을 허용하는 인바운드 규칙이 만들어집니다. 또한 들어오는 웹 트래픽이 허용 하는 포트 80, toocreate는 인바운드 규칙 하려고 합니다.

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

### <a name="create-a-network-card-for-hello-virtual-machine"></a>Hello 가상 컴퓨터에 대 한 네트워크 카드를 만듭니다. 
와 네트워크 카드를 만들고 [새로 AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) hello 가상 컴퓨터에 대 한 합니다. hello 네트워크 카드 hello 가상 컴퓨터 tooa 서브넷, 네트워크 보안 그룹 및 공용 IP 주소에 연결 됩니다.

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>가상 컴퓨터 만들기

가상 컴퓨터 구성을 만듭니다. 이 구성은 가상 컴퓨터 이미지, 크기 및 인증 구성과 같은 hello 가상 컴퓨터를 배포할 때 사용 되는 hello 설정을 포함 합니다. 이 단계를 실행할 때 자격 증명을 묻는 메시지가 나타납니다. 입력 한 hello 값 hello 사용자 이름 및 암호 hello 가상 컴퓨터용으로 구성 됩니다.

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

Hello 가상 컴퓨터를 만들 [새로 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)합니다.

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a>Toovirtual 컴퓨터 연결

Hello 배포 완료 되 면 hello 가상 컴퓨터와 원격 데스크톱 연결을 만듭니다.

사용 하 여 hello [Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) hello 가상 컴퓨터의 tooreturn hello 공용 IP 주소를 명령입니다. 다음 단계에서의 사용자 브라우저 tootest 웹 연결 tooit를 연결할 수 있도록이이 IP 주소를 기록해 둡니다.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

사용 하 여 hello 다음 명령은 toocreate hello 가상 컴퓨터와 원격 데스크톱 세션입니다. Hello로 hello IP 주소를 교체 *publicIPAddress* 의 가상 컴퓨터. 메시지가 표시 되 면 hello 가상 컴퓨터를 만들 때 사용 하는 hello 자격 증명을 입력 합니다.

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a>PowerShell을 통해 IIS 설치

를 toohello Azure VM에에서 로그인 한 했으므로 PowerShell tooinstall IIS 전혀 사용할 수 있으며 hello 로컬 방화벽 규칙 tooallow 웹 트래픽을 사용 하도록 설정. PowerShell 프롬프트를 열고 hello 다음 명령을 실행 합니다.

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a>보기 hello IIS 시작 페이지

IIS가 설치 및 포트 80이 hello 인터넷에서에서 VM에 이제 열려 choice tooview hello 기본 IIS 시작 페이지의 웹 브라우저를 사용할 수 있습니다. 수 있는지 toouse hello *publicIpAddress* toovisit hello 기본 페이지의 위쪽 문서화 합니다. 

![IIS 기본 사이트](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>리소스 정리

더 이상 필요 hello를 사용할 수 없습니다 [제거 AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 명령입니다.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서 간단한 가상 컴퓨터, 네트워크 보안 그룹 규칙을 배포했으며 웹 서버를 설치했습니다. Azure 가상 컴퓨터에 대해 자세히 toolearn Windows vm의 toohello 자습서를 계속 합니다.

> [!div class="nextstepaction"]
> [Azure Windows 가상 컴퓨터 자습서](./tutorial-manage-vm.md)

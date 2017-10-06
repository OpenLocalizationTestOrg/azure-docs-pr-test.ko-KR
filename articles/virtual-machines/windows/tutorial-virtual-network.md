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
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a>Azure PowerShell을 사용하여 Azure Virtual Network 및 Windows Virtual Machines 관리

Azure Virtual Machines는 내부 및 외부 네트워크 통신에서 Azure 네트워킹을 사용합니다. 이 자습서에서는 가상 네트워크에 여러 VM(가상 컴퓨터)을 만들고 이러한 컴퓨터 간에 네트워크 연결을 구성합니다. 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * 가상 네트워크 만들기
> * 가상 네트워크 서브넷 만들기
> * 네트워크 보안 그룹을 사용하여 네트워크 트래픽 제어
> * 트래픽 규칙의 실제 동작 보기

이 자습서는 Azure PowerShell 모듈 버전 3.6 이상 hello가 필요합니다. 실행 ` Get-Module -ListAvailable AzureRM` toofind hello 버전입니다. Tooupgrade 필요한 경우 참조 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.

## <a name="create-vnet"></a>VNet 만들기

VNet은 hello 클라우드에서 사용자의 네트워크의 표현입니다. VNet의 hello Azure 클라우드 전용 tooyour 구독 논리적 격리입니다. VNet 내의 서브넷에 연결 toothose 서브넷 및 hello Vm toohello 서브넷에서 연결에 대 한 규칙 찾을 수 있습니다.

다른 Azure 리소스를 만들기 전에 필요한 toocreate 인 리소스 그룹과 [새로 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)합니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myRGNetwork* hello에 *EastUS* 위치:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

서브넷은 VNet의 자식 리소스이며, IP 주소 접두사를 사용하여 CIDR 블록 내의 주소 공간 세그먼트를 정의하는 데 도움이 됩니다. Nic는 toosubnets, 및 다양 한 작업에 대 한 연결을 제공 하는 연결 된 tooVMs를 추가할 수 있습니다.

[New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig)를 사용하여 서브넷을 만듭니다.

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

[New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) 명령을 통해 *myFrontendSubnet*을 사용하여 *myVNet*이라는 VNET을 만듭니다.

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a>프런트 엔드 VM 만들기

VNet에 VM toocommunicate에 대 한 가상 네트워크 인터페이스 (NIC) 필요 합니다. hello *myFrontendVM* hello에서 액세스 하는 공용 IP 주소를도 필요 하므로 인터넷 합니다. 

[New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)를 사용하여 공용 IP 주소를 만듭니다.

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface)를 사용하여 NIC를 만듭니다.


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

Hello 사용자 이름 및 암호 hello VM에서 hello 관리자 계정에 필요한 설정으로 [Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Hello Vm을 만들 [새로 AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [집합 AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [집합 AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [집합-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [추가 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), 및 [새 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)합니다. 

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

## <a name="install-web-server"></a>웹 서버 설치

원격 데스크톱 세션을 사용하여 *myFrontendVM*에 IIS를 설치할 수 있습니다. VM tooaccess hello tooget hello 공용 IP 주소가 필요한 것입니다.

Hello의 공용 IP 주소를 가져올 수 있습니다 *myFrontendVM* 와 [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)합니다. hello 다음 예제에서는 가져옵니다 hello IP 주소를 *myPublicIPAddress* 앞에서 만든:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

이후 단계에서 사용할 수 있도록 이 IP 주소를 기록해 둡니다.

사용 하 여 hello 다음 명령은 원격 데스크톱 세션을 a toocreate *myFrontendVM*합니다. 대체  *<publicIPAddress>*  이전에 기록한 hello 주소를 사용 합니다. 메시지가 표시 되 면 hello VM을 만들 때 사용 하는 hello 자격 증명을 입력 합니다.

```
mstsc /v:<publicIpAddress>
``` 

로그인이 너무 했으므로*myFrontendVM*, hello 로컬 방화벽 규칙 tooallow 웹 트래픽을 사용 하도록 설정 및 PowerShell tooinstall IIS 전혀 사용할 수 있습니다. PowerShell 프롬프트를 열고 hello 다음 명령을 실행 합니다.

사용 하 여 [Install-windowsfeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) hello IIS 웹 서버를 설치 하는 toorun hello 사용자 지정 스크립트 확장:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

이제 hello 공용 IP 주소 toobrowse toohello VM toosee hello IIS 사이트를 사용할 수 있습니다.

![IIS 기본 사이트](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a>인터넷 트래픽 관리

네트워크 보안 그룹 NSG ()를 허용 하거나 네트워크 트래픽 연결 tooresources tooa VNet을 거부 하는 보안 규칙 목록이 포함 되어 있습니다. Nsg 연결된 toosubnets 수 또는 개별 Nic tooVMs 연결 합니다. 열기 또는 닫기 액세스 tooVMs 포트를 통해 이루어진다는 NSG 규칙을 사용 하 여 합니다. *myFrontendVM*을 만들 때 RDP 연결에 대해 인바운드 포트 3389가 자동으로 열렸습니다.

VM의 내부 통신은 NSG를 사용하여 구성할 수 있습니다. 이 섹션에서는 설명 어떻게 toocreate hello에 대 한 추가 서브넷 NSG tooit tooallow에서 연결을 할당 하 고 네트워크 *myFrontendVM* 너무*myBackendVM* 포트 1433에서 합니다. hello 서브넷 만들어질 때 toohello VM 할당 됩니다.

내부 트래픽이 너무 제한할 수 있습니다*myBackendVM* 36 개월 *myFrontendVM* hello 백 엔드 서브넷에 NSG를 만들어서 합니다. hello 다음 규칙을 만드는 예제는 NSG 라는 *myBackendNSGRule* 와 [새로 AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):

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

[New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup)을 사용하여 *myBackendNSG*라는 네트워크 보안 그룹을 추가합니다.

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a>백 엔드 서브넷 추가

추가 *myBackEndSubnet* 너무*myVNet* 와 [추가 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):

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

## <a name="create-back-end-vm"></a>백 엔드 VM 만들기

SQL Server 이미지를 사용 하 여 백 엔드 VM이 가장 쉬운 방법은 toocreate hello를 hello 합니다. 만이 자습서 hello VM hello 데이터베이스 서버와 만들지만 hello 데이터베이스에 액세스 하는 방법에 대 한 정보를 제공 하지 않습니다.

*myBackendNic*을 만듭니다.

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

Hello 사용자 이름 및 hello 관리자 계정 hello Get-credential을 사용 하 여 VM에 필요한 암호를 설정 합니다.

```powershell
$cred = Get-Credential
```

*myBackendVM*을 만듭니다.

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

사용 되는 hello 이미지 SQL server가 설치 된 있지만이 자습서에서 사용 되지 않습니다. 포함된 tooshow는 하면 VM toohandle 웹 트래픽과 VM toohandle 데이터베이스 관리를 구성 하는 방법입니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서 만든 및 보안 관련된 toovirtual 컴퓨터와 Azure 네트워크입니다. 

> [!div class="checklist"]
> * 가상 네트워크 만들기
> * 가상 네트워크 서브넷 만들기
> * 네트워크 보안 그룹을 사용하여 네트워크 트래픽 제어
> * 트래픽 규칙의 실제 동작 보기

Azure 백업을 사용 하 여 가상 컴퓨터에서 보안 데이터를 모니터링 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다. 에서도 확인할 수 있습니다.

> [!div class="nextstepaction"]
> [Azure에서 Windows 가상 컴퓨터 백업](./tutorial-backup-vms.md)

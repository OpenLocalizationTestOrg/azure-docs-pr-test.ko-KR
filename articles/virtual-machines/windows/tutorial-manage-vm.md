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
# <a name="create-and-manage-windows-vms-with-hello-azure-powershell-module"></a>만들고 있는 Windows Vm 관리 hello Azure PowerShell 모듈

Azure 가상 컴퓨터는 완전히 구성 가능하고 유연한 컴퓨팅 환경을 제공합니다. 이 자습서에서는 VM 크기 선택, VM 이미지 선택 및 VM 배포 등 기본적인 Azure Virtual Machines 배포 항목에 대해 설명합니다. 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * 만들고 tooa VM 연결
> * VM 이미지 선택 및 사용
> * 특정 VM 크기 보기 및 사용
> * VM 크기 조정
> * VM 상태 보기 및 이해

이 자습서는 Azure PowerShell 모듈 버전 3.6 이상 hello가 필요합니다. 실행 ` Get-Module -ListAvailable AzureRM` toofind hello 버전입니다. Tooupgrade 필요한 경우 참조 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.

## <a name="create-resource-group"></a>리소스 그룹 만들기

Hello로 리소스 그룹 만들기 [새로 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 명령입니다. 

Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 가상 컴퓨터보다 먼저 리소스 그룹을 만들어야 합니다. 이 예제에서는 리소스 그룹 이름이 *myResourceGroupVM* hello에서 만든 *EastUS* 영역입니다. 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

hello 리소스 그룹은 생성 하거나이 자습서 전체에서 볼 수 있는 VM을 수정할 때 지정 됩니다.

## <a name="create-virtual-machine"></a>가상 컴퓨터 만들기

가상 컴퓨터 가상 네트워크에 연결 된 tooa 이어야 합니다. 네트워크 인터페이스 카드를 통해 공용 IP 주소를 사용 하 여 hello 가상 컴퓨터와 통신 합니다.

### <a name="create-virtual-network"></a>가상 네트워크 만들기

[New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig)를 사용하여 서브넷을 만듭니다.

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

[New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork)를 사용하여 가상 네트워크를 만듭니다.

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a>공용 IP 주소 만들기

[New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)를 사용하여 공용 IP 주소를 만듭니다.

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a>네트워크 인터페이스 카드 만들기

[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface)를 사용하여 네트워크 인터페이스 카드를 만듭니다.

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a>네트워크 보안 그룹 만들기

Azure NSG([네트워크 보안 그룹](../../virtual-network/virtual-networks-nsg.md))는 하나 또는 여러 가상 컴퓨터에 대한 인바운드 및 아웃바운드 트래픽을 제어합니다. 네트워크 보안 그룹 규칙은 특정 포트 또는 포트 범위에 대한 네트워크 트래픽을 허용하거나 거부합니다. 이러한 규칙에는 미리 정의된 원본에서 시작되는 트래픽만 가상 컴퓨터와 통신할 수 있도록 원본 주소 접두사가 포함될 수도 있습니다. tooaccess hello IIS 웹 서버를 설치 하는, 인바운드 NSG 규칙을 추가 해야 합니다.

toocreate 인바운드 NSG 규칙을 사용 하 여 [추가 AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig)합니다. hello 다음 규칙을 만드는 예제는 NSG 라는 *myNSGRule* 하는 포트를 엽니다. *3389* hello 가상 컴퓨터에 대해:

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

사용 하 여 hello NSG 만들기 *myNSGRule* 와 [새로 AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

사용 하 여 가상 네트워크 hello hello NSG toohello 서브넷을 추가 [집합 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

업데이트 된 가상 네트워크 hello [집합 AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a>가상 컴퓨터 만들기

가상 컴퓨터를 만들 때 운영 체제 이미지, 디스크 크기 조정 및 관리 자격 증명 등의 몇 가지 옵션을 사용할 수 있습니다. 이 예제에서는 가상 컴퓨터의 이름으로 만들어질 *myVM* hello 최신 버전 Windows Server 2016 datacenter를 실행 합니다.

Hello 사용자 이름 및 암호 사용 hello 가상 컴퓨터에서 hello 관리자 계정에 필요한 설정 [Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Hello hello 사용 하는 가상 컴퓨터에 대 한 초기 구성을 만드는 [새로 AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

인 hello 운영 체제 정보 toohello 가상 컴퓨터 구성 추가 [집합 AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

인 hello 이미지 정보 toohello 가상 컴퓨터 구성 추가 [집합 AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

Hello 운영 체제 디스크 설정을 toohello 인 가상 컴퓨터 구성 추가 [집합 AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

이전에 만든 인 가상 컴퓨터 구성 toohello 추가 hello 네트워크 인터페이스 카드 [추가 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

Hello 가상 컴퓨터를 만들 [새로 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)합니다.

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-toovm"></a>TooVM 연결

Hello 배포 완료 되 면 hello 가상 컴퓨터와 원격 데스크톱 연결을 만듭니다.

Hello 다음 hello 가상 컴퓨터의 명령 tooreturn hello 공용 IP 주소를 실행 합니다. 다음 단계에서의 사용자 브라우저 tootest 웹 연결 tooit를 연결할 수 있도록이이 IP 주소를 기록해 둡니다.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

사용 하 여 hello 다음 명령은 toocreate hello 가상 컴퓨터와 원격 데스크톱 세션입니다. Hello로 hello IP 주소를 교체 *publicIPAddress* 의 가상 컴퓨터. 메시지가 표시 되 면 hello 가상 컴퓨터를 만들 때 사용 하는 hello 자격 증명을 입력 합니다.

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a>VM 이미지 이해

새 가상 컴퓨터를 사용 하는 toocreate 일 수 있는 많은 가상 컴퓨터 이미지를 포함 하는 hello Azure 마켓플레이스에 적용 합니다. Hello 이전 단계에서 가상 컴퓨터를 Windows Server 2016 데이터 센터 내 이미지 hello를 사용 하 여 만든 합니다. 이 단계에서는 hello PowerShell 모듈이 새 Vm에 대 한 기반으로 수도 있는 다른 Windows 이미지에 대 한 사용 되는 toosearch hello 마켓플레이스 않습니다. 이 프로세스는 hello 게시자, 제품, 및 hello 이미지 이름 (Sku) 찾기 이루어져 있습니다. 

사용 하 여 hello [Get AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) 명령 tooreturn 이미지 게시자 목록입니다.  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

사용 하 여 hello [Get AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn 이미지 제안 목록 합니다. 이 명령을 사용 하 여 hello 반환 목록을 hello 지정 된 게시자에서 필터링 됩니다. 

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

hello [Get AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) 이미지 이름의 목록을 명령은 다음 hello 게시자와 제품 이름 tooreturn에 필터링 합니다.

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

이 정보에 사용 되는 toodeploy 특정 이미지를 사용 하 여 VM 수 있습니다. 이 예제에서는 hello VM 개체에 hello 이미지 이름을 설정합니다. 완전 한 배포 단계에 대 한이 자습서에서는 toohello 앞의 예제를 참조 하십시오.

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a>VM 크기 이해

가상 컴퓨터 크기는 hello 양의 toohello 사용 가능한 가상 컴퓨터에 적용 된 메모리, CPU 및 GPU, 등 계산 리소스를 결정 합니다. 가상 컴퓨터가 사용 하 여 만든 크기를 적절 한 hello 예상 작업 부하에 대 한 toobe를 해야 합니다. 워크로드가 증가할 경우 기존 가상 컴퓨터의 크기를 조정할 수 있습니다.

### <a name="vm-sizes"></a>VM 크기

다음 표에서 hello 사용 사례에 크기를 분류 합니다.  

| 형식                     | 크기           |    설명       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| 범용 가상 컴퓨터         |DSv2, Dv2, DS, D, Av2, A0-7| CPU 대 메모리 비율이 적당합니다. 개발에 대 한 이상적인 / 테스트 및 소규모 toomedium 응용 프로그램 및 데이터 솔루션입니다.  |
| Compute에 최적화      | Fs, F             | CPU 대 메모리 비율이 높습니다. 트래픽이 중간 정도인 응용 프로그램, 네트워크 어플라이언스 및 일괄 처리 프로세스에 적합합니다.        |
| 메모리에 최적화       | GS, G, DSv2, DS, Dv2, D   | 메모리 대 코어 비율이 높습니다. 관계형 데이터베이스, 중간 toolarge 캐시 및 메모리 내 분석에 매우 유용 합니다.                 |
| Storage에 최적화       | Ls                | 높은 디스크 처리량 및 IO 빅 데이터, SQL, NoSQL 데이터베이스에 적합합니다.                                                         |
| GPU           | NV, NC            | 대량의 그래픽 렌더링 및 비디오 편집에 적합한 전문 VM입니다.       |
| 고성능 | H, A8-11          | 당사의 가장 강력한 CPU VM으로, 필요한 경우 처리량이 높은 네트워크 인터페이스(RDMA)도 제공합니다. 


### <a name="find-available-vm-sizes"></a>사용 가능한 VM 크기 찾기

특정 지역에 toosee VM 목록을 사용할 수 있는 크기, hello를 사용 하 여 [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) 명령입니다.

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a>VM 크기 조정

VM을 배포한 후 크기가 조정 된 tooincrease 하거나 이동할 수 있습니다 리소스 할당을 줄입니다.

VM의 크기를 조정 하기 전에 hello 원하는 크기는 hello 현재 VM 클러스터에서 사용할 수 있는 경우를 확인 합니다. hello [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) 명령은 크기의 목록을 반환 합니다. 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

Hello 원하는 크기는 사용할 수 있는 경우 hello VM 크기를 조정할 수 전원이 켜진 상태에서 있지만 hello 작업 동안 다시 부팅 합니다.

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

Hello 크기를 원하는 경우에 없습니다 hello 현재 클러스터에 VM hello 요구 hello 크기 조정 작업 전에 할당 취소 toobe 발생할 수 있습니다. Note hello VM의 전원이 켜져 다시, hello 임시 디스크의 모든 데이터가 제거 되 고 고정 IP 주소를 사용 하는 경우가 아니면 hello 공용 IP 주소를 변경 하는 경우. 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a>VM 전원 상태

Azure VM의 전원 상태는 여러 상태 중 하나일 수 있습니다. 이 상태를 hello 하이퍼바이저의 hello 관점에서 hello hello VM의 현재 상태를 나타냅니다. 

### <a name="power-states"></a>전원 상태

| 전원 상태 | 설명
|----|----|
| 시작 중 | Hello 가상 컴퓨터가 시작 되 고 나타냅니다. |
| 실행 중 | Hello 가상 컴퓨터 실행 중임을 나타냅니다. |
| 중지 중 | Hello 가상 컴퓨터를 중지 하 고 나타냅니다. | 
| 중지됨 | Hello 가상 컴퓨터 중지 되었음을 나타냅니다. Note hello 중지 상태의 가상 컴퓨터에 여전히 컴퓨팅 요금이 부과 됩니다.  |
| 할당 취소 중 | Hello 가상 컴퓨터를 할당 취소 되 고이 나타냅니다. |
| 할당 취소됨 | Hello 가상 컴퓨터 hello 제어 평면에서 계속 제공 되지만 hello 하이퍼바이저에서 완전히 제거 됨을 나타냅니다. Hello 할당 취소 됨 상태에서에서 가상 컴퓨터 계산 비용이 발생 하지 않습니다. |
| - | Hello 가상 컴퓨터의 전원 상태 hello 알려진 임을 나타냅니다. |

### <a name="find-power-state"></a>전원 상태 찾기

특정 VM 사용 하 여 hello의 tooretrieve hello 상태 [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) 명령입니다. 있는지 toospecify 가상 컴퓨터 및 리소스 그룹에 대 한 올바른 이름 이어야 합니다. 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

출력:

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a>관리 작업

가상 컴퓨터의 hello 수명 주기 동안 시작, 중지, 또는 가상 컴퓨터를 삭제 하는 등의 toorun 관리 작업을 할 수 있습니다. 또한 toocreate 스크립트 tooautomate 반복적 복잡 한 작업을 지정할 수 있습니다. Azure PowerShell을 사용 하 여, 여러 가지 일반적인 관리 작업 또는 실행할 수 있는 hello 명령줄에서 스크립트에서 합니다.

### <a name="stop-virtual-machine"></a>가상 컴퓨터 중지

[Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm)을 사용하여 가상 컴퓨터를 중지하고 할당을 취소합니다.

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

Tookeep hello 가상 컴퓨터 프로 비전 된 상태에서 원하는 hello-StayProvisioned 매개 변수를 사용 합니다.

### <a name="start-virtual-machine"></a>가상 컴퓨터 시작

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a>리소스 그룹 삭제

리소스 그룹을 삭제하면 그 안에 포함된 리소스도 모두 삭제됩니다.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 방법과 같이 기본 VM을 만들고 관리하는 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * 만들고 tooa VM 연결
> * VM 이미지 선택 및 사용
> * 특정 VM 크기 보기 및 사용
> * VM 크기 조정
> * VM 상태 보기 및 이해

VM 디스크에 대 한 다음 자습서 toolearn toohello를 진행 합니다.  

> [!div class="nextstepaction"]
> [VM 디스크 만들기 및 관리](./tutorial-manage-data-disk.md)

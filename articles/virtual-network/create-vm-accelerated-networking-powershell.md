---
title: "가속화된 네트워킹을 사용하는 Azure 가상 머신 만들기 | Microsoft Docs"
description: "가속 네트워킹을 사용하는 Linux 가상 머신을 만드는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: 
author: jdial
manager: jeconnoc
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 01/04/2018
ms.author: jimdial
ms.openlocfilehash: f4908963e0650be9b12b745f6868a1ba6ad933e4
ms.sourcegitcommit: d6984ef8cc057423ff81efb4645af9d0b902f843
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/05/2018
---
# <a name="create-a-windows-virtual-machine-with-accelerated-networking"></a>가속화된 네트워킹을 사용하는 Windows 가상 머신 만들기

> [!IMPORTANT] 
> 가속 네트워킹을 사용하여 가상 머신을 만들어야 합니다. 기존 가상 머신에서는 이 기능을 사용할 수 없습니다. 다음 단계를 따라 가속 네트워킹을 사용하도록 설정할 수 있습니다.
>   1. 가상 머신 삭제
>   2. 가속 네트워킹을 사용하는 가상 머신을 다시 만듭니다.
>

이 자습서에서는 가속화된 네트워킹을 사용하여 Windows VM(가상 머신)을 만드는 방법에 대해 알아봅니다. 가속화된 네트워킹을 사용하면 VM에 대한 단일 루트 I/O 가상화(SR-IOV)를 구현할 수 있어 네트워킹 성능이 크게 향상됩니다. 이 고성능 경로는 데이터 경로에서 호스트를 우회함으로써 대기 시간, 지터 및 CPU 사용률을 줄이므로 지원되는 VM 유형에서 가장 까다로운 네트워크 워크로드에 사용합니다. 다음 그림에서는 가속 네트워킹을 사용할 때와 사용하지 않을 때 두 개의 VM 간의 통신을 보여줍니다.

![비교](./media/create-vm-accelerated-networking/accelerated-networking.png)

가속화된 네트워킹을 사용하지 않는 경우 VM에서 들어오고 나가는 모든 네트워킹 트래픽이 호스트와 가상 스위치를 통과해야 합니다. 가상 스위치는 네트워크 보안 그룹, 액세스 제어 목록, 격리 및 네트워크 트래픽에 대한 다른 네트워크 가상화 서비스 등, 모든 정책 적용을 제공합니다. 가상 스위치에 대한 자세한 내용은 [Hyper-V 네트워크 가상화 및 가상 스위치](https://technet.microsoft.com/library/jj945275.aspx) 문서를 참조하세요.

가속화된 네트워킹을 사용하는 경우 네트워크 트래픽이 VM의 NIC(네트워크 인터페이스)에 도착한 다음 VM으로 전달됩니다. 이제 가상 스위치가 적용되는 모든 네트워크 정책은 오프로드되어 하드웨어에 적용됩니다. 하드웨어에서 정책을 적용하면 NIC는 호스트에 적용된 모든 정책을 유지하면서 VM에 직접 네트워크 트래픽을 전달할 수 있으므로 호스트 및 가상 스위치를 우회할 수 있습니다.

가속화된 네트워킹의 이점은 사용하도록 설정된 VM에만 적용된다는 것입니다. 최상의 결과를 얻으려면 동일한 Azure VNet(Virtual Network)에 연결된 둘 이상의 VM에서 이 기능을 사용하도록 설정하는 것이 좋습니다. VNet에서 통신하거나 온-프레미스에 연결할 때 이 기능을 사용하면 전체 대기 시간에 미치는 영향을 최소화할 수 있습니다.

## <a name="benefits"></a>이점
* **더 낮은 대기 시간/더 높은 초당 패킷 수(pps):** 데이터 경로에서 가상 스위치를 제거하면 패킷이 정채 처리를 위해 호스트에서 소요하는 시간이 제거되고 VM 내에서 처리될 수 있는 패킷 수가 늘어납니다.
* **감소된 지터:** 가상 스위치 처리는 적용해야 하는 정책의 양과 처리를 수행하는 CPU의 워크로드에 따라 달라집니다. 정책 적용을 하드웨어로 오프로드하면 패킷이 VM으로 직접 전달되고, 호스트-VM 통신과 모든 소프트웨어 인터럽트 및 컨텍스트 전환이 제거되어 이러한 가변성이 해소됩니다.
* **CPU 사용률 감소:** 호스트의 가상 스위치를 무시하면 네트워크 트래픽 처리에 사용되는 CPU가 감소됩니다.

## <a name="supported-operating-systems"></a>지원되는 운영 체제
Microsoft Windows Server 2012 R2 Datacenter 및 Windows Server 2016

## <a name="supported-vm-instances"></a>지원되는 VM 인스턴스
가속 네트워킹은 가장 일반적인 용도로 4개 이상의 vCPU가 포함된 계산 최적화 인스턴스 크기에서 지원됩니다. 하이퍼스레딩을 지원하는 D/DSv3 또는 E/ESv3과 같은 인스턴스에서 가속 네트워킹은 8개 이상의 vCPU가 포함된 VM 인스턴스에서 지원됩니다. 지원되는 계열은 D/DSv2, D/DSv3, E/ESv3, F/Fs/Fsv2 및 Ms/Mms입니다.

VM 인스턴스에 대한 자세한 내용은 [Windows VM 크기](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json)를 참조하세요.

## <a name="regions"></a>영역
모든 공용 Azure 지역 및 Azure Government 클라우드에서 사용할 수 있습니다. 

## <a name="limitations"></a>제한 사항
이 기능을 사용하는 경우 다음과 같은 제한이 적용됩니다.

* **네트워크 인터페이스 만들기:** 가속화된 네트워킹은 새 NIC에서만 사용할 수 있으며, 기존 NIC에서는 사용할 수 없습니다.
* **VM 만들기:** VM을 만들 때 가속화된 네트워킹을 사용하도록 설정된 NIC만 VM에 연결할 수 있습니다. 기존 VM에는 이 NIC를 연결할 수 없습니다. VM을 기존 가용성 집합에 추가하는 경우 가용성 집합의 모든 VM에서도 가속화된 네트워킹을 사용할 수 있어야 합니다.
* **Azure Resource Manager를 통해서만 배포:** 가속 네트워킹을 사용하여 가상 머신(클래식)을 배포할 수 없습니다.

## <a name="create-a-virtual-network"></a>가상 네트워크 만들기

[Azure PowerShell](/powershell/azure/install-azurerm-ps) 버전 5.1.1 이상을 설치합니다. 현재 설치된 버전을 찾으려면 `Get-Module -ListAvailable AzureRM`을 실행합니다. 설치 또는 업그레이드해야 할 경우 [PowerShell 갤러리](https://www.powershellgallery.com/packages/AzureRM)에서 최신 버전의 AzureRM 모듈을 설치합니다. PowerShell 세션에서 [Add-AzureRmAccount](/powershell/module/AzureRM.Profile/Add-AzureRmAccount) 명령을 사용하여 Azure 계정에 로그인합니다.

다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다. 예제 매개 변수 이름에는 *myResourceGroup*, *myNic*, *myVM*이 포함됩니다.

[New-AzureRmResourceGroup](/powershell/module/AzureRM.Resources/New-AzureRmResourceGroup)을 사용하여 리소스 그룹을 만듭니다. 다음 예제에서는 *centralus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "centralus"
```

먼저 [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/AzureRM.Network/New-AzureRmVirtualNetworkSubnetConfig)를 사용하여 서브넷 구성을 만듭니다. 다음 예제에서는 *mySubnet*이라는 서브넷을 만듭니다.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig `
    -Name "mySubnet" `
    -AddressPrefix "192.168.1.0/24"
```

*mySubnet* 서브넷에서 [New-AzureRmVirtualNetwork](/powershell/module/AzureRM.Network/New-AzureRmVirtualNetwork)를 사용하여 가상 네트워크를 만듭니다.

```powershell
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
    -Location "centralus" `
    -Name "myVnet" `
    -AddressPrefix "192.168.0.0/16" `
    -Subnet $Subnet
```

## <a name="create-a-network-security-group"></a>네트워크 보안 그룹 만들기

먼저 [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/AzureRM.Network/New-AzureRmNetworkSecurityRuleConfig)를 사용하여 네트워크 보안 그룹 규칙을 만듭니다.

```powershell
$rdp = New-AzureRmNetworkSecurityRuleConfig `
    -Name 'Allow-RDP-All' `
    -Description 'Allow RDP' `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 100 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389
```

[New-AzureRmNetworkSecurityGroup](/powershell/module/AzureRM.Network/New-AzureRmNetworkSecurityGroup)을 사용하여 네트워크 보안 그룹을 만들고 여기에 *Allow-RDP-All* 보안 규칙을 할당합니다. *Allow-RDP-All* 규칙 외에도 네트워크 보안 그룹에는 여러 기본 규칙이 포함되어 있습니다. 하나의 기본 규칙이 인터넷에서 모든 인바운드 액세스를 사용하지 않도록 설정하기 때문에 원격으로 가상 머신에 연결할 수 있도록 *Allow-RDP-All* 규칙을 만들면 네트워크 보안 그룹에 할당됩니다.

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroup `
    -Location centralus `
    -Name "myNsg" `
    -SecurityRules $rdp
```

[Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/AzureRM.Network/Set-AzureRmVirtualNetworkSubnetConfig)를 사용하여 네트워크 보안 그룹을 *mySubnet* 서브넷에 연결합니다. 네트워크 보안 그룹의 규칙은 서브넷에 배포된 모든 리소스에 효율적입니다.

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name 'mySubnet' `
    -AddressPrefix "192.168.1.0/24" `
    -NetworkSecurityGroup $nsg
```

## <a name="create-a-network-interface-with-accelerated-networking"></a>가속 네트워킹을 사용하여 네트워크 인터페이스 만들기
[New-AzureRmPublicIpAddress](/powershell/module/AzureRM.Network/New-AzureRmPublicIpAddress)를 사용하여 공용 IP 주소를 만듭니다. 인터넷에서 가상 머신에 액세스하려는 계획이 없다면 공용 IP 주소가 필요하지 않지만 이 문서의 단계를 완료하려면 필요합니다.

```powershell
$publicIp = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroup `
    -Name 'myPublicIp' `
    -location centralus `
    -AllocationMethod Dynamic
```

[New-AzureRmNetworkInterface](/powershell/module/AzureRM.Network/New-AzureRmNetworkInterface)와 가속 네트워킹을 사용하여 네트워크 인터페이스를 만들고 네트워크 인터페이스에 공용 IP 주소를 할당합니다. 다음 예제에서는 *myVnet* 가상 네트워크의 *mySubnet* 서브넷에서 *myNic*이라는 네트워크 인터페이스를 만들고 여기에 *myPublicIp* 공용 IP 주소를 할당합니다.

```powershell
$nic = New-AzureRmNetworkInterface `
    -ResourceGroupName "myResourceGroup" `
    -Name "myNic" `
    -Location "centralus" `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIp.Id `
    -EnableAcceleratedNetworking
```

## <a name="create-the-virtual-machine"></a>가상 머신 만들기

[Get-Credential](/powershell/module/microsoft.powershell.security/get-credential)을 사용하여 `$cred` 변수에 VM 자격 증명을 설정합니다.

```powershell
$cred = Get-Credential
```

먼저 [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig)를 사용하여 VM을 정의합니다. 다음 예제에서는 가속 네트워킹(*Standard_DS4_v2*)을 지원하는 VM 크기를 사용하여 *myVM*이라는 VM을 정의합니다.

```powershell
$vmConfig = New-AzureRmVMConfig -VMName "myVm" -VMSize "Standard_DS4_v2"
```

모든 VM 크기 및 특성 목록은 [Windows VM 크기](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json)를 참조하세요.

[Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) 및 [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)를 사용하여 나머지 VM 구성을 만듭니다. 다음 예제에서는 Windows Server 2016 VM을 만듭니다.

```powershell
$vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
    -Windows `
    -ComputerName "myVM" `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
    -PublisherName "MicrosoftWindowsServer" `
    -Offer "WindowsServer" `
    -Skus "2016-Datacenter" `
    -Version "latest"
```

[Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface)를 사용하여 이전에 만든 네트워크 인터페이스를 연결합니다.

```powershell
$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```

마지막으로 [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)을 사용하여 VM을 만듭니다.

```powershell
New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "centralus"
```

## <a name="confirm-the-driver-is-installed-in-the-operating-system"></a>드라이버가 운영 체제에 설치되었는지 확인

Azure에서 VM을 만들면 VM에 연결하고 Windows에서 드라이버가 설치되어 있는지를 확인합니다. 

1. 인터넷 브라우저에서 Azure [Portal](https://portal.azure.com)을 열고 Azure 계정으로 로그인합니다.
2. Azure Portal 위쪽의 *리소스 검색* 텍스트가 있는 상자에서 *myVm*을 입력합니다. 검색 결과에서 표시되는 **myVm**을 클릭합니다. **연결** 단추 아래에서 **만드는 중**이 표시되는 경우 Azure에서 VM 만들기를 아직 완료하지 않은 것입니다. 따라서 **연결** 단추 아래에서 **만드는 중**가 더 이상 표시되지 않는 경우에만 개요의 왼쪽 위 모서리에 있는 **연결**을 클릭합니다.
3. [가상 머신 만들기](#create-the-virtual-machine)에서 입력한 사용자 이름과 암호를 입력합니다. Azure에서 Windows VM에 연결된 적이 없는 경우 [가상 머신에 연결](../virtual-machines/windows/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#connect-to-virtual-machine)을 참조하세요.
4. [Windows 시작] 단추를 마우스 오른쪽 단추로 클릭한 다음 **장치 관리자**를 클릭합니다. **네트워크 어댑터** 노드를 펼칩니다. 다음 그림과 같이 **Mellanox ConnectX-3 Virtual Function Ethernet Adapter**가 나타나는지 확인합니다.
   
    ![장치 관리자](./media/create-vm-accelerated-networking/device-manager.png)

이제 가속화된 네트워킹을 VM에 사용할 수 있습니다.

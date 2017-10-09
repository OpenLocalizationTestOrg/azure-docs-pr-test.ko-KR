---
title: "Azure Vm에서 항상 사용 가능한 응용 프로그램 빌드-aaaTutorial | Microsoft Docs"
description: "자세한 내용은 방법 toocreate Azure에서 부하 분산 장치와 함께 3 개의 Windows Vm에서 항상 사용할 수 있으며 보안 응용 프로그램"
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
ms.date: 03/30/2017
ms.author: davidmu
ms.openlocfilehash: f9eff96be4f3999651c4108f0334e4eaa1a39c0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a>Azure의 Windows 가상 컴퓨터에서 부하 분산된 고가용성 응용 프로그램 빌드

이 자습서에서는 탄력적인 toomaintenance 이벤트를 항상 사용 가능한 응용 프로그램을 만듭니다. hello 앱 부하 분산 장치, 가용성 집합 및 3 개의 Windows 가상 컴퓨터 (Vm)를 사용합니다. 이 자습서에서 IIS를 설치,이 자습서에 사용 하 여 다른 응용 프로그램 프레임 워크 toodeploy hello 같은 고가용성 구성 요소 및 지침 사용하실 수 있습니다. 

## <a name="step-1---azure-prerequisites"></a>1단계 - Azure 필수 구성 요소

toocomplete이이 자습서에서는 hello 최신 설치 되어 있는지 확인 [Azure PowerShell](/powershell/azure/overview) 모듈입니다.

먼저, tooyour 로그인 AzureRmAccount 명령 hello로 Azure 구독에에서 로그인 하 고 지시를 따른 hello 화면에 표시 합니다.

```powershell
Login-AzureRmAccount
```

Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 다른 Azure 리소스를 만들기 전에 필요한 toocreate 인 리소스 그룹과 [새로 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)합니다. hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello에 `westeurope` 영역: 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a>2단계 - 가용성 집합 만들기

논리적 장애 및 업데이트 도메인 간에 가상 컴퓨터를 만들 수 있습니다. 각 논리 도메인 hello 기본 Azure 데이터 센터에서 하드웨어의 일부를 나타냅니다. 둘 이상의 VM을 만들 경우 Compute 및 저장소 리소스가 이러한 도메인 간에 분산됩니다. 하드웨어 구성 요소에는 유지 관리 해야 하는 경우이 배포 응용 프로그램의 hello 가용성을 유지 관리 합니다. 가용성 집합을 통해 이러한 논리적 장애 및 업데이트 도메인을 정의할 수 있습니다.

[New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset)을 사용하여 가용성 집합을 만듭니다. hello 다음 예제에서는 가용성 명명 된 집합 `myAvailabilitySet`:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a>3단계 - 부하 분산 장치 만들기

Azure Load Balancer는 부하 분산 장치 규칙을 사용하여 정의된 VM 집합 간에 트래픽을 분산시킵니다. 상태 프로브 각 VM에서 특정된 포트를 모니터링 하 고 트래픽을 tooan 배포 VM 작동 합니다.

### <a name="create-public-ip-address"></a>공용 IP 주소 만들기

tooaccess 앱 hello 인터넷에서 공용 IP 주소 toohello 부하 분산 장치를 할당 합니다. [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)를 사용하여 공용 IP 주소를 만듭니다. hello 다음 예제에서는 공용 IP 주소를 만들고 라는 `myPublicIP`:

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a>부하 분산 장치 만들기

[New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig)를 사용하여 프런트 엔드 IP 주소를 만듭니다. hello 다음 예제에서는 프런트 엔드 IP 주소를 만들고 라는 `myFrontEndPool`: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

[New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig)를 사용하여 백 엔드 주소 풀을 만듭니다. hello 다음 예제에서는 명명 된 백 엔드 주소 풀을 `myBackEndPool`:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

이제 있는 hello 부하 분산 장치를 만들 [새로 AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer)합니다. hello 다음 예제에서는 명명 된 부하 분산 장치 `myLoadBalancer` hello를 사용 하 여 `myPublicIP` 주소:

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a>상태 프로브 만들기

tooallow hello 부하 분산 장치 toomonitor hello 상태 응용 프로그램의 상태 프로브를 사용 합니다. hello 상태 프로브는 동적으로 추가 하거나 Vm의 응답 toohealth 검사에 따라 hello 부하 분산 장치 순환에서 제거 합니다. 기본적으로 VM은 15 초 간격으로 두 개의 연속 된 실패 후 hello 부하 분산 장치 배포에서 제거 됩니다.

[Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig)를 사용하여 상태 프로브를 만듭니다. hello 다음 예제에서는 명명 된 상태 프로브 `myHealthProbe` 각 VM을 모니터링 하는:

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a>부하 분산 장치 규칙 만들기

부하 분산 장치 규칙은 사용 되는 toodefine 트래픽 분산된 toohello Vm을가 하는 방법입니다.

[Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig)를 사용하여 부하 분산 장치 규칙을 만듭니다. hello 다음 예제에서는 명명 된 부하 분산 장치 규칙 `myLoadBalancerRule` 포트에서 트래픽을 분산 시키고 및 `80`:

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

포함 된 hello 부하 분산 장치를 업데이트 [집합 AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a>4단계 - 네트워킹 구성

각 VM에 tooa 가상 네트워크에 연결 하는 하나 이상의 가상 네트워크 인터페이스 카드 (Nic). 이 가상 네트워크 toofilter 트래픽은 정의 된 액세스 규칙에 따라 보안 됩니다.

### <a name="create-virtual-network"></a>가상 네트워크 만들기

먼저 [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig)를 사용하여 서브넷을 구성합니다. hello 다음 예제에서는 서브넷을 만듭니다. 명명 된 `mySubnet`:

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

tooprovide 네트워크 연결 tooyour Vm을 가상 네트워크를 만듭니다 [새로 AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork)합니다. hello 다음 예제에서는 가상 네트워크를 만들어 명명 된 `myVnet` 와 `mySubnet`:

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a>네트워크 보안 구성

Azure NSG([네트워크 보안 그룹](../../virtual-network/virtual-networks-nsg.md))는 하나 또는 여러 가상 컴퓨터에 대한 인바운드 및 아웃바운드 트래픽을 제어합니다. 네트워크 보안 그룹 규칙은 특정 포트 또는 포트 범위에 대한 네트워크 트래픽을 허용하거나 거부합니다. 이러한 규칙에는 미리 정의된 원본에서 시작되는 트래픽만 가상 컴퓨터와 통신할 수 있도록 원본 주소 접두사가 포함될 수도 있습니다.

tooallow 트래픽 tooreach 앱 웹 서버에서 네트워크 보안 그룹 규칙으로 만들 [새로 AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig)합니다. hello 다음 예제에서는 명명 된 네트워크 보안 그룹 규칙 `myNetworkSecurityGroupRule`:

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow
```

[New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup)을 사용하여 네트워크 보안 그룹을 만듭니다. hello 다음 예제에서는 명명 된 NSG `myNetworkSecurityGroup`:

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

Hello 네트워크 보안 그룹 toohello 서브넷을 추가 [집합 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

업데이트 된 가상 네트워크 hello [집합 AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a>가상 네트워크 인터페이스 카드 만들기

실제 VM hello 하지 않고 분산 함수 hello 가상 NIC 리소스를 로드 합니다. hello 가상 NIC 연결된 toohello 부하 분산 장치를 이며 tooa VM을 연결 합니다.

[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface)를 사용하여 가상 NIC를 만듭니다. hello 다음 예제에서는 세 개의 가상 Nic (각 VM에 대 한 가상 NIC 1 개에 대해 만드는 단계를 수행 하는 hello에서 응용 프로그램):


```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface -ResourceGroupName myResourceGroup `
     -Name myNic$i `
     -Location westeurope `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}

```

## <a name="step-5---create-virtual-machines"></a>5단계: 가상 컴퓨터 만들기

기본 위치에 구성 요소는 모든 hello로 만들 수 있습니다 이제 항상 사용 가능한 Vm toorun 앱. 

Hello 사용자 이름 및 암호 사용 hello 가상 컴퓨터에서 hello 관리자 계정에 필요한 가져오기 [Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Hello Vm을 만들 [새로 AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [집합 AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [집합 AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [집합-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [추가 AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), 및 [새 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)합니다. 다음 예제는 hello 세 개의 Vm을 만듭니다.

```powershell
for ($i=1; $i -le 3; $i++)
{
   $vm = New-AzureRmVMConfig -VMName myVM$i -VMSize Standard_D1 -AvailabilitySetId $availabilitySet.Id
   $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName myVM$i -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest
   $vm = Set-AzureRmVMOSDisk -VM $vm -Name myOsDisk$i -StorageAccountType StandardLRS -DiskSizeInGB 128 -CreateOption FromImage -Caching ReadWrite
   $nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic$i
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
}

```

몇 분 toocreate 걸리고 모두 세 개의 Vm을 구성 합니다. hello 부하 분산 장치 상태 프로브 때 자동으로 검색 각 VM에서 hello 응용 프로그램을 실행 합니다. Hello 앱이 실행 되 면 hello 부하 분산 장치 규칙 toodistribute 트래픽을 시작 합니다.

### <a name="install-hello-app"></a>Hello 앱 설치 

Azure 가상 컴퓨터 확장은 응용 프로그램을 설치 및 hello 운영 체제를 구성 하는 등 tooautomate 사용 되는 가상 컴퓨터 구성 작업입니다. hello [Windows에 대 한 사용자 지정 스크립트 확장](./../virtual-machines-windows-extensions-customscript.md) 은 사용 되는 toorun hello 가상 컴퓨터에서 모든 PowerShell 스크립트입니다. hello 스크립트는 액세스할 수 있는 모든 HTTP 끝점에 Azure 저장소에에서 저장 또는 hello 사용자 지정 스크립트 확장 구성에 포함할 수 있습니다. Hello 사용자 지정 스크립트 확장을 사용할 경우 hello Azure VM 에이전트는 hello 스크립트 실행을 관리 합니다.

사용 하 여 [집합 AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello 사용자 지정 스크립트 확장 합니다. 확장 실행 hello `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS 웹 서버:

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server"}' `
     -Location westeurope
}
```

### <a name="test-your-app"></a>앱 테스트

Hello 있는 부하 분산 장치 프로그램의 공용 IP 주소 가져오기 [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)합니다. hello 다음 예제에서는 가져옵니다 hello IP 주소를 `myPublicIP` 앞에서 만든:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

Tooa 웹 브라우저에서 hello 공용 IP 주소를 입력 합니다. 원위치에서 hello NSG 규칙을 사용 하면 hello 기본 IIS 웹 사이트가 표시 됩니다. 

![IIS 기본 사이트](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a>6단계 - 관리 작업

Hello OS 업데이트를 설치 하는 등의 응용 프로그램을 실행 하는 Vm에 tooperform 유지 관리를 할 수 있습니다. 늘어난된 트래픽 tooyour 앱과 toodeal, tooadd 할 수 있습니다 추가 Vm입니다. 이 섹션에서는 tooremove 하거나 hello 부하 분산 장치에서 VM을 추가 합니다. 

### <a name="remove-a-vm-from-hello-load-balancer"></a>Hello 부하 분산 장치에서 VM을 제거 합니다.

Hello 네트워크 인터페이스 카드의 hello LoadBalancerBackendAddressPools 속성 다시 설정 하 여 hello 백 엔드 주소 풀에서 VM을 제거 합니다.

Hello 네트워크 인터페이스 카드 가져오기 [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

Hello 네트워크 인터페이스 카드의 hello LoadBalancerBackendAddressPools 속성을 너무 설정 $null:

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

Hello 네트워크 인터페이스 카드를 업데이트 합니다.

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-toohello-load-balancer"></a>VM toohello 부하 분산 장치 추가

VM 유지 관리를 수행 하거나 tooexpand 용량이 필요한 경우 추가 VM toohello 백 엔드 주소 풀의 hello 부하 분산 장치 NIC hello 삭제 됩니다.

Hello 부하 분산 장치 가져오기:

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

Hello 부하 분산 장치 toohello 네트워크 인터페이스 카드의 hello 백 엔드 주소 풀을 추가 합니다.

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

Hello 네트워크 인터페이스 카드를 업데이트 합니다.

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>다음 단계

샘플 – [Azure Virtual Machine PowerShell 샘플 스크립트](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

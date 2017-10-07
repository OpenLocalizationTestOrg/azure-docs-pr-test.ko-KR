---
title: "aaaHow tooload 균형 Windows Azure의 가상 컴퓨터 | Microsoft Docs"
description: "Toouse hello Azure 세 개의 Windows Vm 간에 분산 toocreate 항상 사용할 수 있으며 보안 응용 프로그램을 로드 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: bfbd6a24e90a33e60d7d4f7b0c471af5d4e71f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>어떻게 tooload 균형 Azure toocreate의 Windows 가상 컴퓨터는 항상 사용 가능한 응용 프로그램
부하 분산은 들어오는 요청을 여러 가상 컴퓨터에 분산하여 높은 수준의 가용성을 제공합니다. 이 자습서에서는 hello의 여러 구성 요소가 hello Azure 부하 분산 장치 트래픽을 분산 및 고가용성을 제공 하는 방법에 대 한 설명입니다. 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Azure Load Balancer 만들기
> * 부하 분산 장치 상태 프로브 만들기
> * 부하 분산 장치 트래픽 규칙 만들기
> * 사용자 지정 스크립트 확장 toocreate hello 기본 IIS 사이트를 사용 하 여
> * 가상 컴퓨터를 만들고 연결 하려면 tooa 부하 분산 장치
> * 부하 분산 장치의 실제 동작 보기
> * 부하 분산 장치에서 VM 추가 및 제거

이 자습서는 Azure PowerShell 모듈 버전 3.6 이상 hello가 필요합니다. 실행 ` Get-Module -ListAvailable AzureRM` toofind hello 버전입니다. Tooupgrade 필요한 경우 참조 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.


## <a name="azure-load-balancer-overview"></a>Azure Load Balancer 개요
Azure Load Balancer는 들어오는 트래픽을 정상 VM 간에 분산하여 고가용성을 제공하는 계층 4(TCP, UDP) 부하 분산 장치입니다. 부하 분산 장치 상태 프로브 각 VM에서 특정된 포트를 모니터링 하 고 트래픽을 tooan 배포 VM 작동 합니다.

하나 이상의 공용 IP 주소를 포함하는 프런트 엔드 IP 구성을 정의할 수 있습니다. 이 프런트 엔드 IP 구성을 사용 하면 부하 분산 장치 및 응용 프로그램 toobe 액세스할 수 있는 hello 인터넷을 통해. 

가상 컴퓨터의 가상 네트워크 인터페이스 카드 (NIC)를 사용 하 여 tooa 부하 분산 장치를 연결 합니다. toodistribute 트래픽 toohello Vm, 백 엔드 주소 풀을 hello 가상 (Nic) 연결 된 toohello 부하 분산 장치의 hello IP 주소를 포함합니다.

트래픽 toocontrol hello 흐름을 정의한 특정 포트 및 프로토콜 tooyour Vm을 매핑하는 대 한 부하 분산 장치 규칙.


## <a name="create-azure-load-balancer"></a>Azure Load Balancer 만들기
이 섹션에는 만들어 hello 부하 분산 장치의 각 구성 요소를 구성 하는 방법을 자세히 설명 합니다. 부하 분산 장치를 만들려면 먼저 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)을 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupLoadBalancer* hello에 *EastUS* 위치:

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a>공용 IP 주소 만들기
tooaccess 앱에서 인터넷 hello hello 부하 분산 장치에 대 한 공용 IP 주소를 사용 해야 합니다. [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)를 사용하여 공용 IP 주소를 만듭니다. hello 다음 예제에서는 명명 된 공용 IP 주소를 *myPublicIP* hello에 *myResourceGroupLoadBalancer* 리소스 그룹:

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a>부하 분산 장치 만들기
[New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig)를 사용하여 프런트 엔드 IP 주소를 만듭니다. hello 다음 예제에서는 프런트 엔드 IP 주소를 만들고 명명 된 *myFrontEndPool*: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

[New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig)를 사용하여 백 엔드 주소 풀을 만듭니다. hello 다음 예제에서는 명명 된 백 엔드 주소 풀을 *myBackEndPool*:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

이제 있는 hello 부하 분산 장치를 만들 [새로 AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer)합니다. hello 다음 예제에서는 명명 된 부하 분산 장치 *myLoadBalancer* hello를 사용 하 여 *myPublicIP* 주소:

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a>상태 프로브 만들기
tooallow hello 부하 분산 장치 toomonitor hello 상태 응용 프로그램의 상태 프로브를 사용 합니다. hello 상태 프로브는 동적으로 추가 하거나 Vm의 응답 toohealth 검사에 따라 hello 부하 분산 장치 순환에서 제거 합니다. 기본적으로 VM은 15 초 간격으로 두 개의 연속 된 실패 후 hello 부하 분산 장치 배포에서 제거 됩니다. 앱의 프로토콜 또는 특정 상태 확인 페이지에 따라 상태 프로브를 만듭니다. 

다음 예제는 hello TCP 프로브를 만듭니다. 좀 더 미세 조정된 상태 검사를 위해 사용자 지정 HTTP 프로브를 만들 수도 있습니다. 사용자 지정 HTTP 검색을 사용할 경우 만들어야 hello 상태 확인 페이지와 같은 *healthcheck.aspx*합니다. hello 프로브를 반환 해야 합니다는 **HTTP 200 OK** hello 부하 분산 장치 tookeep hello 호스트 회전에 대 한 응답입니다.

사용 하면 TCP 상태 프로브 toocreate [추가 AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig)합니다. hello 다음 예제에서는 명명 된 상태 프로브 *myHealthProbe* 각 VM을 모니터링 하는:

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

포함 된 hello 부하 분산 장치를 업데이트 [집합 AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a>부하 분산 장치 규칙 만들기
부하 분산 장치 규칙은 사용 되는 toodefine 트래픽 분산된 toohello Vm을가 하는 방법입니다. Hello 들어오는 트래픽의 캡슐화 된 트래픽과 hello 백 엔드 IP 풀 tooreceive hello, hello 필요한 원본 및 대상 포트에 대 한 프런트 엔드 IP 구성을 hello를 정의 합니다. 정상 Vm만 트래픽을 받도록 toomake, 또한 정의한 hello 상태 프로브 toouse 있습니다.

[Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig)를 사용하여 부하 분산 장치 규칙을 만듭니다. hello 다음 예제에서는 명명 된 부하 분산 장치 규칙 *myLoadBalancerRule* 포트에서 트래픽을 분산 시키고 및 *80*:

```powershell
$probe = Get-AzureRmLoadBalancerProbeConfig -LoadBalancer $lb -Name myHealthProbe

Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80 `
  -Probe $probe
```

포함 된 hello 부하 분산 장치를 업데이트 [집합 AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a>가상 네트워크 구성
일부 Vm을 배포 하 여 분산 장치를 테스트할 수 전에 가상 네트워크 리소스를 지 원하는 hello를 만듭니다. 가상 네트워크에 대 한 자세한 내용은 참조 hello [Azure 가상 네트워크 관리](tutorial-virtual-network.md) 자습서입니다.

### <a name="create-network-resources"></a>네트워크 리소스 만들기
[New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork)를 사용하여 가상 네트워크를 만듭니다. hello 다음 예제에서는 가상 네트워크를 만들어 명명 된 *myVnet* 와 *mySubnet*:

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create hello virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

[New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig)를 사용하여 네트워크 보안 그룹 규칙을 만든 다음 [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup)을 사용하여 네트워크 보안 그룹을 만듭니다. Hello 네트워크 보안 그룹 toohello 서브넷을 추가 [집합 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) 후 hello와 가상 네트워크를 업데이트 하 고 [집합 AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork)합니다. 

hello 다음 예제에서는 명명 된 네트워크 보안 그룹 규칙 *myNetworkSecurityGroup* 너무 적용*mySubnet*:

```powershell
# Create security rule config
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

# Create hello network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply hello network security group tooa subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update hello virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface)를 사용하여 가상 NIC를 만듭니다. hello 다음 예제에서는 세 개의 가상 Nic (각 VM에 대 한 가상 NIC 1 개에 대해 만드는 단계를 수행 하는 hello에서 응용 프로그램). 언제 든 지 가상 Nic를 추가 하 고 Vm을 만들 수 있고 toohello 부하 분산 장치를 추가할 수 없습니다.

```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -Name myNic$i `
     -Location EastUS `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}
```

## <a name="create-virtual-machines"></a>가상 컴퓨터 만들기
tooimprove hello 고가용성 응용 프로그램의 가용성 집합에 Vm을 배치 합니다.

[New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset)을 사용하여 가용성 집합을 만듭니다. hello 다음 예제에서는 가용성 명명 된 집합 *myAvailabilitySet*:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

된 hello Vm에 대 한 관리자 사용자 이름 및 암호 설정 [Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Hello Vm을 만들 수 이제 [새로 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)합니다. 다음 예제는 hello 세 개의 Vm을 만듭니다.

```powershell
for ($i=1; $i -le 3; $i++)
{
  $vm = New-AzureRmVMConfig `
    -VMName myVM$i `
    -VMSize Standard_D1 `
    -AvailabilitySetId $availabilitySet.Id
  $vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM$i `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
  $vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
  $vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk$i `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
  $nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic$i
  $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
  New-AzureRmVM `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Location EastUS `
    -VM $vm
}
```

몇 분 toocreate 걸리고 모두 세 개의 Vm을 구성 합니다.

### <a name="install-iis-with-custom-script-extension"></a>사용자 지정 스크립트 확장을 사용하여 IIS 설치
에 대 한 이전 자습서에서 [어떻게 toocustomize Windows 가상 컴퓨터](tutorial-automate-vm-deployment.md), tooautomate VM 사용자 지정 된 사용자 지정 스크립트 확장에 대 한 Windows hello 하는 방법을 배웠습니다. Hello를 사용할 수 있습니다 동일 tooinstall에 접근 하 고 Vm에 IIS를 구성 합니다.

사용 하 여 [집합 AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello 사용자 지정 스크립트 확장 합니다. 확장 실행 hello `powershell Add-WindowsFeature Web-Server` IIS 웹 서버 및 업데이트 hello tooinstall hello *Default.htm* hello VM의 페이지 tooshow hello 호스트 이름:

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
     -Location EastUS
}
```

## <a name="test-load-balancer"></a>부하 분산 장치 테스트
Hello 있는 부하 분산 장치 프로그램의 공용 IP 주소 가져오기 [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)합니다. hello 다음 예제에서는 가져옵니다 hello IP 주소를 *myPublicIP* 앞에서 만든:

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

그런 다음 tooa 웹 브라우저에서 hello 공용 IP 주소를 입력할 수 있습니다. hello 웹 사이트가 표시 되어, hello VM의 hello 호스트 이름을 포함 하 여 해당 hello 부하 분산 장치는 hello 다음 예제에서에서 트래픽 tooas 분산:

![실행 중인 IIS 웹 사이트](./media/tutorial-load-balancer/running-iis-website.png)

응용 프로그램을 실행 하는 모든 세 개의 Vm에 트래픽을 분산 toosee hello에 대 한 부하 분산 장치, 있습니다 수 강제 새로 고침 웹 브라우저입니다.


## <a name="add-and-remove-vms"></a>VM 추가 및 제거
Hello OS 업데이트를 설치 하는 등의 응용 프로그램을 실행 하는 Vm에 tooperform 유지 관리를 할 수 있습니다. 늘어난된 트래픽 tooyour 앱과 toodeal, tooadd 할 수 있습니다 추가 Vm입니다. 이 섹션에서는 tooremove 하거나 hello 부하 분산 장치에서 VM을 추가 합니다.

### <a name="remove-a-vm-from-hello-load-balancer"></a>Hello 부하 분산 장치에서 VM을 제거 합니다.
Hello 네트워크 인터페이스 카드 가져오기 [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), 다음 집합 hello *LoadBalancerBackendAddressPools* 속성의 가상 NIC를 너무 hello*$null*합니다. Hello 가상 NIC.를 마지막으로 업데이트 합니다.

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

나머지 두 hello에 트래픽을 분산 toosee hello에 대 한 부하 분산 장치 앱을 실행 하는 Vm 있습니다 수 강제 새로 고침 웹 브라우저입니다. 이제 hello OS 업데이트를 설치 하 여 VM 다시 부팅 수행 등 VM에 유지 관리를 수행할 수 있습니다.

### <a name="add-a-vm-toohello-load-balancer"></a>VM toohello 부하 분산 장치 추가
After VM 유지 관리 수행 또는 tooexpand 용량이 필요한 경우 설정 hello *LoadBalancerBackendAddressPools* hello 가상 NIC toohello 속성 *BackendAddressPool* 에서 [ Get AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):

Hello 부하 분산 장치 가져오기:

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 부하 분산 장치 만들고 Vm tooit 첨부 합니다. 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * Azure Load Balancer 만들기
> * 부하 분산 장치 상태 프로브 만들기
> * 부하 분산 장치 트래픽 규칙 만들기
> * 사용자 지정 스크립트 확장 toocreate hello 기본 IIS 사이트를 사용 하 여
> * 가상 컴퓨터를 만들고 연결 하려면 tooa 부하 분산 장치
> * 부하 분산 장치의 실제 동작 보기
> * 부하 분산 장치에서 VM 추가 및 제거

다음 자습서 toolearn toohello 어떻게 발전 toomanage VM 네트워킹 합니다.

> [!div class="nextstepaction"]
> [VM 및 가상 네트워크 관리](./tutorial-virtual-network.md)

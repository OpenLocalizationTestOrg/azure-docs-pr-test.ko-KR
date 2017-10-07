---
title: "PowerShell cmdlet을 사용 하 여 설정 하는 가상 컴퓨터 크기 aaaCreating | Microsoft Docs"
description: "Azure PowerShell cmdlet을 사용하여 첫 번째 Azure 가상 컴퓨터 규모 집합 생성 및 관리 시작하기"
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 430d9d64-1f35-48f0-a4fd-9b69910ffa59
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: danielsollondon
ms.openlocfilehash: 7979be367d04c904b60d78849c1b751a52cc8caf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a>PowerShell cmdlet을 사용하여 가상 컴퓨터 크기 집합 만들기
이 문서는 어떻게 toocreate는 가상 컴퓨터 크기 집합 (VMSS)의 예를 안내 합니다. 관련 네트워킹 및 저장소를 포함한 세 개 노드의 크기 집합을 만듭니다.

## <a name="first-steps"></a>첫 번째 단계
Hello 최신 Azure PowerShell 모듈이 설치 되어 있는, toomake hello PowerShell commandlet 있는지 toomaintain, 필요한 및 크기 집합 만들기를 확인 합니다.
Toohello 명령줄 도구를 이동 [여기](http://aka.ms/webpi-azps) hello 최신 사용 가능한 Azure 모듈에 대 한 합니다.

VMSS toofind 관련 commandlet를 hello 검색 문자열을 사용 하 여 \*VMSS\*합니다. 예: _gcm *vmss*_

## <a name="creating-a-vmss"></a>VMSS 만들기
#### <a name="create-resource-group"></a>리소스 그룹 만들기
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a>네트워킹 만들기(VNET/서브넷)
#### <a name="subnet-specification"></a>서브넷 사양
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a>VNET 사양
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume hello new subnet is hello only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-tooallow-external-access"></a>공용 IP 리소스 tooAllow 외부 액세스 만들기
바인딩된 toohello 부하 분산 장치 사용 됩니다.

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a>부하 분산 장치 만들기
```
$frontendName = 'fe' + $rgname
$backendAddressPoolName = 'bepool' + $rgname
$probeName = 'vmssprobe' + $rgname
$inboundNatPoolName = 'innatpool' + $rgname
$lbruleName = 'lbrule' + $rgname
$lbName = 'vmsslb' + $rgname

# Bind Public IP tooLoad Balancer
$frontend = New-AzureRmLoadBalancerFrontendIpConfig -Name $frontendName -PublicIpAddress $pubip
```

#### <a name="configure-load-balancer"></a>부하 분산 장치 구성
Hello 크기 집합의 hello Vm의 hello Nic에서 공유할 수는이, 백 엔드 주소 풀 Config를 만듭니다.

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

부하 분산 된 프로브 포트 설정, 응용 프로그램에 맞게 hello 설정을 변경 합니다.

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

직접 라우팅된 연결 (하지 부하 분산)에 대 한 인바운드 NAT 풀 만들기 hello 부하 분산 장치를 통해 Vm toohello hello 규모에 맞게 설정 합니다. RDP를 사용 하 여 toodemonstrate 이므로 응용 프로그램에 필요할 수 있습니다.

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

Hello 부하 분산 규칙을 보여 줍니다 요청의 부하를 분산 포트 80을 이전 단계에서 hello 설정을 사용 하 여이 예제를 만듭니다.

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

구성을 사용하여 부하 분산 장치를 만듭니다.

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

LB 설정을 확인 하십시오 부하 분산 된 포트 configs 참고 hello 크기 집합의 Vm hello까지 인바운드 NAT 규칙을 만들 표시 되지 것입니다.

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-hello-scale-set"></a>구성 하 고 만들기 hello 크기 조정 설정
Note 보여 주는 인프라 예제를 tooset 배포 방법과 배율 웹 트래픽 hello 크기 집합 하지만 hello 여기에서 지정 된 Vm 이미지에서 설치 된 모든 웹 서비스를 필요가 없습니다.

```
# specify scale set Name
$vmssName = 'vmss' + $rgname;

## specify VMSS specific details
$adminUsername = 'azadmin';
$adminPassword = "Password1234!";

$PublisherName = 'MicrosoftWindowsServer'
$Offer         = 'WindowsServer'
$Sku          = '2012-R2-Datacenter'
$Version       = 'latest'
$vmNamePrefix = 'winvmss'

###add an extension
$extname = 'BGInfo';
$publisher = 'Microsoft.Compute';
$exttype = 'BGInfo';
$extver = '2.1';
```

서브넷과 NIC tooLoad 분산 장치 바인딩

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

크기 집합 구성 만들기

```
# Specify number of nodes
$numberofnodes = 3

$vmss = New-AzureRmVmssConfig -Location $loc -SkuCapacity $numberofnodes -SkuName 'Standard_A2' -UpgradePolicyMode 'automatic' `
    | Add-AzureRmVmssNetworkInterfaceConfiguration -Name $subnetName -Primary $true -IPConfiguration $ipCfg `
    | Set-AzureRmVmssOSProfile -ComputerNamePrefix $vmNamePrefix -AdminUsername $adminUsername -AdminPassword $adminPassword `
    | Set-AzureRmVmssStorageProfile -OsDiskCreateOption 'FromImage' -OsDiskCaching 'None' `
    -ImageReferenceOffer $Offer -ImageReferenceSku $Sku -ImageReferenceVersion $Version `
    -ImageReferencePublisher $PublisherName `
    | Add-AzureRmVmssExtension -Name $extname -Publisher $publisher -Type $exttype -TypeHandlerVersion $extver -AutoUpgradeMinorVersion $true
```

크기 집합 구성 빌드

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

이제 hello 크기 집합을 만들었습니다. 연결 toohello를 테스트할 수 RDP를 사용 하 여이 예제는 개별 VM:

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```

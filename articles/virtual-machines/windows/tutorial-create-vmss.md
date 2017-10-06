---
title: "가상 컴퓨터 크기 조정 설정에 대 한 Windows Azure에서 aaaCreate | Microsoft Docs"
description: "가상 컴퓨터 확장 집합을 사용하여 고가용성 응용 프로그램을 만들고 Windows VM에 배포"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: 
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: a3914571005c28a492c069d880992630851afae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a>가상 컴퓨터 확장 집합을 만들고 Windows에 고가용성 앱 배포
가상 컴퓨터 크기 집합 toodeploy 있으며, 자동 크기 조정 동일한 가상 컴퓨터를 관리 합니다. 수동으로 hello hello 크기 집합의 Vm 수의 크기를 조정 하거나 기반으로 CPU 사용량, 메모리 수요가 또는 네트워크 트래픽 규칙 tooautoscale 정의할 수 있습니다. 이 자습서에서는 Azure에서 가상 컴퓨터 확장 집합을 배포합니다. 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * 사용자 지정 스크립트 확장 toodefine IIS 사이트 tooscale hello를 사용 하 여
> * 확장 집합에 대한 부하 분산 장치 만들기
> * 가상 컴퓨터 확장 집합 만들기
> * Hello 크기 집합의 인스턴스 수를 늘리거나
> * 자동 크기 조정 규칙 만들기

이 자습서는 Azure PowerShell 모듈 버전 3.6 이상 hello가 필요합니다. 실행 ` Get-Module -ListAvailable AzureRM` toofind hello 버전입니다. Tooupgrade 필요한 경우 참조 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.


## <a name="scale-set-overview"></a>확장 집합 개요
크기 집합 살펴본 것 처럼에 대 한 hello 이전 자습서에서 너무 유사한 개념을 사용[항상 사용 가능한 Vm을 만들](tutorial-availability-sets.md)합니다. 확장 집합의 VM은 가용성 집합의 VM처럼 장애 도메인 및 업데이트 도메인에 분산됩니다.

VM은 필요에 따라 확장 집합에 생성됩니다. 자동 크기 조정 규칙 toocontrol 정의 방법 및 시기 Vm 더하거나 hello 크기 집합에서 제거 합니다. 이러한 규칙은 메트릭(예: CPU 부하, 메모리 사용량 또는 네트워크 트래픽)을 기반으로 트리거할 수 있습니다.

크기 조정 설정 too1, 000 Vm Azure 플랫폼 이미지 사용을 지원 합니다. 워크 로드에 중요 한 설치 또는 VM 사용자 지정 요구 사항을 지정할 수 있습니다 너무[사용자 지정 VM 이미지를 만들](tutorial-custom-images.md)합니다. Too100 vm 크기 집합 사용자 지정 이미지를 사용 하는 경우에 만들 수 있습니다.


## <a name="create-an-app-tooscale"></a>응용 프로그램 tooscale 만들기
확장 집합을 만들려면 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)을 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupAutomate* hello에 *EastUS* 위치:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

이전 자습서에서 배운 너무 어떻게[자동화 VM 구성](tutorial-automate-vm-deployment.md) 사용자 지정 스크립트 확장을 hello를 사용 하 여 합니다. 크기 조정 설정 구성을 다음 만들고 사용자 지정 스크립트 확장 tooinstall 적용 IIS를 구성 합니다.

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig `
    -Location EastUS `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

# Define hello script for your Custom Script Extension toorun
$publicSettings = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Use Custom Script Extension tooinstall IIS and configure basic website
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings
```

## <a name="create-scale-load-balancer"></a>규모 부하 분산 장치 만들기
Azure Load Balancer는 들어오는 트래픽을 정상 VM 간에 분산하여 고가용성을 제공하는 계층 4(TCP, UDP) 부하 분산 장치입니다. 부하 분산 장치 상태 프로브 각 VM에서 특정된 포트를 모니터링 하 고 트래픽을 tooan 배포 VM 작동 합니다. 자세한 내용은 hello 다음 자습서에서 참조 [tooload Windows 가상 컴퓨터를 분산 하는 방법을](tutorial-load-balancer.md)합니다.

공용 IP 주소를 갖고 있고 포트 80에서 웹 트래픽을 분산하는 부하 분산 장치를 만듭니다.

```powershell
# Create a public IP address
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupScaleSet `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP

# Create a frontend and backend IP pool
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool

# Create hello load balancer
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool

# Create a load balancer health probe on port 80
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2

# Create a load balancer rule toodistribute traffic on port 80
Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80

# Update hello load balancer configuration
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="create-a-scale-set"></a>확장 집합 만들기
이제 [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm)를 사용하여 가상 컴퓨터 확장 집합을 만듭니다. hello 다음 예제에서는 크기 명명 된 집합 *myScaleSet*:

```powershell
# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword P@ssword! `
  -ComputerNamePrefix myVM

# Create hello virtual network resources
$subnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name "mySubnet" `
  -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName "myResourceGroupScaleSet" `
  -Name "myVnet" `
  -Location "EastUS" `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $subnet
$ipConfig = New-AzureRmVmssIpConfig `
  -Name "myIPConfig" `
  -LoadBalancerBackendAddressPoolsId $lb.BackendAddressPools[0].Id `
  -SubnetId $vnet.Subnets[0].Id

# Attach hello virtual network toohello config object
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name "network-config" `
  -Primary $true `
  -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myScaleSet `
  -VirtualMachineScaleSet $vmssConfig
```

몇 분 toocreate 걸리고 모든 hello 눈금 집합 리소스와 Vm을 구성 합니다.


## <a name="test-your-app"></a>앱 테스트
IIS 웹 사이트 작업에서 toosee hello 있는 부하 분산 장치에 공용 IP 주소를 가져올 [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)합니다. hello 다음 예제에서는 가져옵니다 hello IP 주소를 *myPublicIP* hello 크기 집합의 일부로 만들어집니다.

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

Tooa 웹 브라우저에서 hello 공용 IP 주소를 입력 합니다. hello 앱 hello 해당 VM을 분산 장치 배포 트래픽의 부하를 hello의 hello 호스트 이름을 포함 하 여 표시 됩니다.

![실행 중인 IIS 사이트](./media/tutorial-create-vmss/running-iis-site.png)

작업에서 설정 toosee hello 눈금 있습니다 수 강제 새로 고침 웹 브라우저 toosee hello 부하 분산 장치 앱을 실행 하는 모든 hello Vm 트래픽을 분산 합니다.


## <a name="management-tasks"></a>관리 작업
Hello 크기 집합의 hello 수명 주기 동안 toorun 할 수 있습니다 하나 이상의 관리 작업입니다. 또한 다양 한 수명 주기 작업을 자동화 하는 toocreate 스크립트를 지정할 수 있습니다. Azure PowerShell 신속 하 게 toodo 해당 작업을 제공합니다. 다음은 몇 가지 일반적인 작업입니다.

### <a name="view-vms-in-a-scale-set"></a>확장 집합의 VM 보기
tooview 눈금에서 실행 중인 Vm의 목록 설정, 사용 하 여 [Get AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) 다음과 같습니다.

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Loop through hello instanaces in your scale set
for ($i=1; $i -le ($scaleset.Sku.Capacity - 1); $i++) {
    Get-AzureRmVmssVM -ResourceGroupName myResourceGroupScaleSet `
      -VMScaleSetName myScaleSet `
      -InstanceId $i
}
```


### <a name="increase-or-decrease-vm-instances"></a>VM 인스턴스 증가 또는 감소
인스턴스의 toosee hello 수 현재는 규모에 맞게 설정, 사용 하 여 [Get AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) 에서 쿼리 및 *sku.capacity*:

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

있습니다 다음 수동으로 거 나 낮출 수로 설정 하는 hello 규모에 맞게 가상 컴퓨터의 hello 수 [업데이트 AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss)합니다. hello 다음 예제에서는 설정 hello Vm 수 너무 설정 하 여 규모에 맞게*5*:

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Set and update hello capacity of your scale set
$scaleset.sku.capacity = 5
Update-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -Name myScaleSet `
    -VirtualMachineScaleSet $scaleset
```

경우 몇 분 tooupdate hello 지정에 인스턴스 수 크기 집합입니다.


### <a name="configure-autoscale-rules"></a>자동 크기 조정 규칙 구성
눈금의 인스턴스 수가 hello을 수동으로 확장 설정 하지 않고 자동 크기 조정 규칙을 정의 합니다. 이러한 규칙 hello 눈금에는 인스턴스 설정 및 메트릭 및 정의한 임계값에 따라 적절 하 게 응답을 모니터링 합니다. 다음 예제는 hello 5 분 동안 hello 평균 CPU 부하가 60% 보다 크면 하 여 hello 인스턴스 수가 씩 확장 합니다. Hello 평균 CPU 부하는 다음 5 분 동안 30% 아래로 떨어지면, hello 인스턴스는 배율에 따라 인스턴스 하나에서:

```powershell
# Define your scale set information
$mySubscriptionId = (Get-AzureRmSubscription).Id
$myResourceGroup = "myResourceGroupScaleSet"
$myScaleSet = "myScaleSet"
$myLocation = "East US"

# Create a scale up rule tooincrease hello number instances after 60% average CPU usage exceeded for a 5 minute period
$myRuleScaleUp = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator GreaterThan `
  -MetricStatistic Average `
  -Threshold 60 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Increase `
  -ScaleActionValue 1

# Create a scale down rule toodecrease hello number of instances after 30% average CPU usage over a 5 minute period
$myRuleScaleDown = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator LessThan `
  -MetricStatistic Average `
  -Threshold 30 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Decrease `
  -ScaleActionValue 1

# Create a scale profile with your scale up and scale down rules
$myScaleProfile = New-AzureRmAutoscaleProfile `
  -DefaultCapacity 2  `
  -MaximumCapacity 10 `
  -MinimumCapacity 2 `
  -Rules $myRuleScaleUp,$myRuleScaleDown `
  -Name "autoprofile"

# Apply hello autoscale rules
Add-AzureRmAutoscaleSetting `
  -Location $myLocation `
  -Name "autosetting" `
  -ResourceGroup $myResourceGroup `
  -TargetResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -AutoscaleProfiles $myScaleProfile
```


## <a name="next-steps"></a>다음 단계
이 자습서에서는 가상 컴퓨터 확장 집합을 만들었습니다. 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * 사용자 지정 스크립트 확장 toodefine IIS 사이트 tooscale hello를 사용 하 여
> * 확장 집합에 대한 부하 분산 장치 만들기
> * 가상 컴퓨터 확장 집합 만들기
> * Hello 크기 집합의 인스턴스 수를 늘리거나
> * 자동 크기 조정 규칙 만들기

부하 분산 가상 컴퓨터에 대 한 개념에 대 한 자세한 toohello 다음 자습서 toolearn를 진행 합니다.

> [!div class="nextstepaction"]
> [Virtual Machines 부하 분산](tutorial-load-balancer.md)

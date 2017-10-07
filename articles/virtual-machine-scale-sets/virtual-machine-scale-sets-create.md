---
title: "aaaCreate Azure 가상 컴퓨터 크기 집합 | Microsoft Docs"
description: "Azure CLI, PowerShell, 템플릿 또는 Visual Studio를 사용하여 Linux 또는 Microsoft Azure 가상 컴퓨터 확장 집합을 만들고 배포합니다."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 07/21/2017
ms.author: adegeo
ms.openlocfilehash: 73de25c1dd2424e64655b3accfea848926e72f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a>가상 컴퓨터 확장 집합 만들기 및 배포
가상 컴퓨터 크기 집합에 더 쉽게 있습니다 toodeploy 고 집합으로 동일한 가상 컴퓨터를 관리 합니다. 규모 집합은 대규모 응용 프로그램에 대한 높은 확장성과 사용자 지정 가능한 계산 계층을 제공하고 Windows 플랫폼 이미지, Linux 플랫폼 이미지, 사용자 지정 이미지 및 확장을 지원합니다. 확장 집합에 대한 자세한 내용은 [가상 컴퓨터 확장 집합](virtual-machine-scale-sets-overview.md)을 참조하세요.

이 자습서에서는 가상 컴퓨터 크기 집합 하는 toocreate 어떻게 **없이** Azure 포털 hello를 사용 하 여 합니다. 어떻게 toouse hello Azure 포털에 대 한 정보를 참조 하십시오. [어떻게 toocreate 가상 컴퓨터 크기는 Azure 포털 hello로을 집합](virtual-machine-scale-sets-portal-create.md)합니다.

>[!NOTE]
>Azure Resource Manager 리소스에 대한 자세한 내용은 [Azure Resource Manager 및 클래식 배포](../azure-resource-manager/resource-manager-deployment-model.md)를 참조하세요.

## <a name="sign-in-tooazure"></a>TooAzure에 로그인

Azure CLI 2.0 또는 Azure PowerShell toocreate 소수 자릿수를 사용 하 여 설정, 먼저 toosign tooyour 구독에 있습니다.

설정, tooinstall 및 로그인 tooAzure Azure CLI 또는 PowerShell을 참조 하는 방법에 대 한 자세한 내용은 [Azure CLI 2.0 시작](/cli/azure/get-started-with-azure-cli.md) 또는 [Azure PowerShell cmdlet과 함께 시작](/powershell/azure/overview)합니다.

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a>리소스 그룹 만들기

먼저 hello 가상 컴퓨터 크기 집합는 리소스 그룹은 연결 된 toocreate를 해야 합니다.

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a>Azure CLI에서 만들기

Azure CLI를 사용하여 적은 노력으로 가상 컴퓨터 확장 집합을 만들 수 있습니다. 기본값을 생략한 경우 기본값이 제공됩니다. 예를 들어 가상 네트워크 정보를 지정하지 않는 경우 가상 네트워크가 만들어집니다. Hello 부분 뒤를 생략 하면 사용자에 대해 만들어집니다. 
- 부하 분산 장치
- 가상 네트워크
- 공용 IP 주소

Toouse hello 가상 컴퓨터 크기 집합에 가상 컴퓨터 이미지를 hello 선택 때 몇 가지 옵션이 있습니다.

- URN  
리소스의 hello 식별자:  
**Win2012R2Datacenter**

- URN 별칭  
hello URN의 식별 이름:  
**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**

- 사용자 지정 리소스 ID  
hello 경로 tooan Azure 리소스:  
**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**

- 웹 리소스  
hello 경로 tooan HTTP URI:  
**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**

>[!TIP]
>`az vm image list`을 사용하여 사용 가능한 이미지 목록을 가져올 수 있습니다.

toocreate 가상 컴퓨터 크기 집합, hello 다음을 지정 해야 합니다.

- 리소스 그룹 
- 이름
- 운영 체제 이미지
- 인증 정보 
 
다음 예제는 hello (이 단계는 몇 분 정도 걸릴 수 있습니다) 하는 기본적인 가상 컴퓨터 크기 집합을 만듭니다.

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

Hello 명령이 완료 된 후에 가상 컴퓨터 크기 집합 만든 이제 해야 합니다. Tooget hello 가상 컴퓨터의 IP 주소를 hello tooit 연결할 수 있도록 할 수 있습니다. 다음 명령을 hello로 많은 hello 가상 컴퓨터 (IP 주소 hello 포함)에 대 한 다른 정보를 얻을 수 있습니다. 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a>PowerShell에서 만들기

PowerShell은 Azure CLI 보다 더 복잡 한 toouse입니다. Azure CLI는 네트워킹 관련 리소스(부하 분산 장치, IP 주소, 가상 네트워크 등)의 기본값을 제공하는 반면 PowerShell은 제공하지 않습니다. PowerShell을 사용하여 이미지를 참조하는 작업은 약간 더 복잡합니다. Cmdlet을 다음 hello로 이미지를 가져올 수 있습니다.

1. Get-AzureRMVMImagePublisher
2. Get-AzureRMVMImageOffer
3. Get-AzureRmVMImageSku

hello cmdlet 작업 순서에 파이프 될 수 있습니다. Hello에 대 한 모든 tooget 이미지 하는 방법의 예로 **미국 서 부 2** hello 이름이 있는 게시자를 사용 하 여 영역 **microsoft** 에 있습니다.

```powershell
Get-AzureRMVMImagePublisher -Location WestUS2 | Where-Object PublisherName -Like *microsoft* | Get-AzureRMVMImageOffer | Get-AzureRmVMImageSku | Select-Object PublisherName, Offer, Skus
```

```
PublisherName              Offer                    Skus
-------------              -----                    ----
microsoft-ads              linux-data-science-vm    linuxdsvm
microsoft-ads              standard-data-science-vm standard-data-science-vm
MicrosoftAzureSiteRecovery Process-Server           Windows-2012-R2-Datacenter
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Enterprise
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Standard
MicrosoftBizTalkServer     BizTalk-Server           2016-Developer
MicrosoftBizTalkServer     BizTalk-Server           2016-Enterprise
...
```

가상 컴퓨터 크기 집합을 만들기 위한 hello 워크플로 다음과 같습니다.

1. Hello 크기 집합에 대 한 정보를 포함 하는 구성 개체를 만듭니다.
2. 참조 hello 기본 OS 이미지입니다.
3. Hello 운영 체제 설정을 구성: 인증, VM 이름 접두사 및 사용자/통과 합니다.
4. 네트워킹을 구성합니다.
5. Hello 크기 집합을 만듭니다.

이 예제에서는 Windows Server 2016이 설치된 컴퓨터에 2개의 인스턴스로 된 기본 확장 집합을 만듭니다.

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create hello virtual network resources

## Basics
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name "my-subnet" -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name "my-network" -ResourceGroupName $rg -Location $location -AddressPrefix 10.0.0.0/16 -Subnet $subnet

## Load balancer
$publicIP = New-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName $rg -Location $location -AllocationMethod Static -DomainNameLabel "myuniquedomain"
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontend" -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
$probe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
$inboundNATRule1= New-AzureRmLoadBalancerRuleConfig -Name "webserver" -FrontendIpConfiguration $frontendIP -Protocol Tcp -FrontendPort 80 -BackendPort 80 -IdleTimeoutInMinutes 15 -Probe $probe -BackendAddressPool $backendPool
$inboundNATPool1 = New-AzureRmLoadBalancerInboundNatPoolConfig -Name "RDP" -FrontendIpConfigurationId $frontendIP.Id -Protocol TCP -FrontendPortRangeStart 53380 -FrontendPortRangeEnd 53390 -BackendPort 3389

New-AzureRmLoadBalancer -ResourceGroupName $rg -Name "LB1" -Location $location -FrontendIpConfiguration $frontendIP -LoadBalancingRule $inboundNATRule1 -InboundNatPool $inboundNATPool1 -BackendAddressPool $backendPool -Probe $probe

## IP address config
$ipConfig = New-AzureRmVmssIpConfig -Name "my-ipaddress" -LoadBalancerBackendAddressPoolsId $backendPool.Id -SubnetId $vnet.Subnets[0].Id -LoadBalancerInboundNatPoolsId $inboundNATPool1.Id

# Attach hello virtual network toohello IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a>사용자 지정 가상 컴퓨터 이미지 사용
크기 hello 갤러리에서 가상 컴퓨터 이미지를 참조 하는 대신 사용자 지정 이미지에서 집합을 만드는 경우 hello _집합 AzureRmVmssStorageProfile_ 명령은 다음과 같습니다.
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a>템플릿에서 만들기

Azure Resource Manager 템플릿을 사용하여 가상 컴퓨터 확장 집합을 배포할 수 있습니다. Hello에서 하나를 사용 하거나 사용자 고유의 템플릿을 만들 수 있습니다 [템플릿 리포지토리](https://azure.microsoft.com/resources/templates/?term=vmss)합니다. 이러한 템플릿을 배포할 수 있으며 직접 tooyour Azure 구독.

>[!NOTE]
>toocreate JSON 텍스트 파일을 만들면 사용자 지정 서식 파일입니다. 방법에 대 한 일반적인 내용은 toocreate 템플릿을 사용자 지정 하 고, 참조 [Azure 리소스 관리자 템플릿을](../azure-resource-manager/resource-group-authoring-templates.md)합니다.

[GitHub에서](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set) 샘플 템플릿을 사용할 수 있습니다. 샘플을 사용 하 고 toocreate 확인 하려면 어떻게 해야 하는 방법에 대 한 자세한 내용은 [최소 실행 가능한 크기 집합](.\virtual-machine-scale-sets-mvss-start.md)합니다.

## <a name="create-from-visual-studio"></a>Visual Studio에서 만들기

Visual Studio와 함께 Azure 리소스 그룹 프로젝트 만들고는 가상 컴퓨터 크기 집합 tooit 서식 파일을 추가할 수 있습니다. Tooimport 사용할지를 선택할 수 있습니다 GitHub 또는 hello Azure 웹 응용 프로그램 갤러리에서 합니다. PowerShell 배포 스크립트도 생성됩니다. 자세한 내용은 참조 [어떻게 toocreate 가상 컴퓨터 크기는 Visual Studio와 함께 집합](virtual-machine-scale-sets-vs-create.md)합니다.

## <a name="create-from-hello-azure-portal"></a>Hello Azure 포털에서 만들기

hello Azure 포털 tooquickly 크기 집합을 만들기는 편리한 방법을 제공 합니다. 자세한 내용은 참조 [어떻게 toocreate 가상 컴퓨터 크기는 Azure 포털 hello로을 집합](virtual-machine-scale-sets-portal-create.md)합니다.

## <a name="next-steps"></a>다음 단계

[데이터 디스크](virtual-machine-scale-sets-attached-disks.md)에 대해 자세히 알아봅니다.

너무 방법에 대해 알아봅니다[앱 관리](virtual-machine-scale-sets-deploy-app.md)합니다.

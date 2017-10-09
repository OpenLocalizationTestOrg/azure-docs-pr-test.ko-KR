---
title: "aaaOpen 포트 tooa Azure PowerShell을 사용 하 여 VM | Microsoft Docs"
description: "자세한 방법을 tooopen 포트 끝점 tooyour Windows VM을 만들 / hello Azure 리소스 관리자 배포 모드 및 Azure PowerShell을 사용 하 여"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf45f7d8-451a-48ab-8419-730366d54f1e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c1817a0c447ae4ce7a1ce2a1fc6927bedf2dacb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-and-endpoints-tooa-vm-in-azure-using-powershell"></a>어떻게 tooopen 포트와 끝점 tooa PowerShell을 사용 하 여 Azure에서 VM
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a>빠른 명령
toocreate 네트워크 보안 그룹 및 ACL 규칙 필요한 [hello 최신 버전의 Azure PowerShell 설치](/powershell/azureps-cmdlets-docs)합니다. 수도 있습니다 [hello Azure 포털을 사용 하 여 이러한 단계를 수행](nsg-quickstart-portal.md)합니다.

Azure 계정 tooyour에 로그인 합니다.

```powershell
Login-AzureRmAccount
```

Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다. 예제 매개 변수 이름에는 *myResourceGroup*, *myNetworkSecurityGroup* 및 *myVnet*이 포함됩니다.

[New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig)를 사용하여 규칙을 만듭니다. hello 다음 규칙을 만드는 예제는 명명 된 *myNetworkSecurityGroupRule* tooallow *tcp* 포트에서 트래픽을 *80*:

```powershell
$httprule = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRule" `
    -Description "Allow HTTP" `
    -Access "Allow" `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority "100" `
    -SourceAddressPrefix "Internet" `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80
```

다음으로를 네트워크 보안 그룹을 만듭니다 [새로 AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) 및 할당 hello HTTP 방금 만든 규칙 다음과 같습니다. hello 다음 예제에서는 네트워크 보안 그룹을 만든 라는 *myNetworkSecurityGroup*:

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

이제 네트워크 보안 그룹 tooa 서브넷을 할당 하겠습니다. hello 다음 예제에서는 할당 명명 된 기존 가상 네트워크가 *myVnet* toohello 변수 *$vnet* 와 [Get AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

[Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)를 사용하여 네트워크 보안 그룹을 서브넷에 연결합니다. hello 다음 예제에서는 연결 라는 hello 서브넷 *mySubnet* 네트워크 보안 그룹과:

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

마지막으로 사용한 가상 네트워크를 업데이트 [집합 AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) 변경 tootake 효과 대 한 순서 대로:

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a>네트워크 보안 그룹에 대한 자세한 정보
빠른 명령을 여기 hello를 사용 하면를 tooget 및 트래픽 이동을 tooyour VM으로 실행 합니다. 네트워크 보안 그룹 많은 향상 된 기능 및 제어 tooyour 리소스 액세스에 대 한 세분성을 제공합니다. [여기서 네트워크 보안 그룹 및 ACL 규칙 만들기](tutorial-virtual-network.md#manage-internal-traffic)에 대해 자세히 읽어보세요.

고가용성 웹 응용 프로그램인 경우 VM을 Azure Load Balancer 뒤에 배치해야 합니다. hello 부하 분산 장치 트래픽 tooVMs 트래픽 필터링이 제공 하는 네트워크 보안 그룹에 배포 합니다. 자세한 내용은 참조 [어떻게 tooload 균형 Linux 가상 컴퓨터에서 Azure toocreate 항상 사용 가능한 응용 프로그램](tutorial-load-balancer.md)합니다.

## <a name="next-steps"></a>다음 단계
이 예제에서는 간단한 규칙 tooallow HTTP 트래픽을 만들었습니다. Hello 문서 다음에 보다 자세한 환경을 만드는 방법에 대 한 정보를 찾을 수 있습니다.

* [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)
* [NSG(네트워크 보안 그룹)란?](../../virtual-network/virtual-networks-nsg.md)
* [부하 분산 장치에 대한 Azure Resource Manager 개요](../../load-balancer/load-balancer-arm.md)


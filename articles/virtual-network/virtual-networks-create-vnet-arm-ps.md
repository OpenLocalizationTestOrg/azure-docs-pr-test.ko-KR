---
title: "가상 네트워크-Azure PowerShell aaaCreate | Microsoft Docs"
description: "어떻게 가상 a toocreate PowerShell을 사용 하는 네트워크에 대해 알아봅니다."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a31f4f12-54ee-4339-b968-1a8097ca77d3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8d6e395a77f71de9f94b6304b05450e46b47544f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-powershell"></a>PowerShell을 사용하여 가상 네트워크 만들기

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure에는 Azure Resource Manager 및 클래식이라는 두 가지 배포 모델이 있습니다. Hello 리소스 관리자 배포 모델을 통해 리소스를 만드는 것이 좋습니다. hello 읽기에 대해 더 알아봅니다 toolearn hello 두 모델 간의 차이 hello [이해 Azure 배포 모델](../azure-resource-manager/resource-manager-deployment-model.md) 문서.
 
이 문서에서는 PowerShell을 사용 하 여 toocreate hello 리소스 관리자 배포를 통해 VNet을 모델링 하는 방법을 설명 합니다. 리소스 관리자를 통해 다른 도구를 사용 하 여 VNet을 만들 하거나 hello 다음 목록에서에서 다른 옵션을 선택 하 여 hello 클래식 배포 모델을 통해 VNet을 만들 수도 있습니다.

> [!div class="op_single_selector"]
> * [포털](virtual-networks-create-vnet-arm-pportal.md)
> * [PowerShell](virtual-networks-create-vnet-arm-ps.md)
> * [CLI](virtual-networks-create-vnet-arm-cli.md)
> * [템플릿](virtual-networks-create-vnet-arm-template-click.md)
> * [포털(클래식)](virtual-networks-create-vnet-classic-pportal.md)
> * [PowerShell(클래식)](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [CLI(클래식)](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a>가상 네트워크 만들기

PowerShell에서 다음 전체 hello를 사용 하 여 가상 네트워크 단계 toocreate:

1. 설치 하 고 hello에 hello 단계에 따라 Azure PowerShell을 구성 [어떻게 tooInstall 및 Azure PowerShell 구성](/powershell/azure/overview) 문서.

2. 필요에 따라 아래와 같이 새 리소스 그룹을 만듭니다. 이 시나리오의 경우 이름이 *TestRG*인 리소스 그룹을 만듭니다. 리소스 그룹에 대한 자세한 내용은 [Azure 리소스 관리자 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    예상 출력:

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. *TestVNet*라는 새 Vnet을 만듭니다.

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    예상 출력:

        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                   : W/"[Id]"
        ProvisioningState          : Succeeded
        Tags                       : 
        AddressSpace               : {
                                   "AddressPrefixes": [
                                     "192.168.0.0/16"
                                   ]
                                  }
        DhcpOptions                : {}
        Subnets                    : []
        VirtualNetworkPeerings     : []
4. Hello 가상 네트워크 개체를 변수에 저장 합니다.

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`을 실행하여 3과 4 단계를 결합할 수 있습니다.
   > 

5. 서브넷 toohello 새 VNet 변수를 추가 합니다.

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    예상 출력:
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {}
        Subnets             : [
                                  {
                                    "Name": "FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24"
                                  }
                                ]
        VirtualNetworkPeerings     : []

6. 위의 5 단계를 반복 toocreate 각 서브넷에 대해 원하는 합니다. hello 다음 명령은 만듭니다 hello *백 엔드* hello 시나리오에 대 한 서브넷:

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. 서브넷을 만들 수 있지만 현재만에 있는 지역 변수 사용 되는 tooretrieve hello hello 위의 4 단계에서 만드는 VNet 합니다. toosave hello 변경 tooAzure, hello 다음 명령을 실행 합니다.

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    예상 출력:
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {
                                  "DnsServers": []
                                }
        Subnets               : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  },
                                  {
                                    "Name": "BackEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                    "AddressPrefix": "192.168.2.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  }
                                ]
        VirtualNetworkPeerings : []

## <a name="next-steps"></a>다음 단계

자세한 내용은 방법 tooconnect:

- Hello를 참조 하 여 가상 컴퓨터 (VM) tooa 가상 네트워크 [Windows VM을 만들](../virtual-machines/virtual-machines-windows-ps-create.md) 문서. Hello 아티클의 hello 단계에서 VNet 및 서브넷을 만드는 대신 및 선택할 수 있습니다는 기존 VNet 서브넷 tooconnect VM을 합니다.
- hello를 참조 하 여 가상 네트워크 tooother 가상 네트워크를 hello [Vnet 연결](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) 문서.
- 가상 네트워크 tooan hello 온-프레미스 사이트 간 가상 사설망 (VPN) 또는 express 경로 회로 사용 하 여 네트워크. 자세한 방법은 hello [사이트 간 VPN을 사용 하 여 VNet tooan 온-프레미스 네트워크 연결](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) 및 [VNet tooan ExpressRoute 회로 연결](../expressroute/expressroute-howto-linkvnet-arm.md) 문서입니다.

---
title: "aaaManage 네트워크 보안 그룹-Azure PowerShell | Microsoft Docs"
description: "Toomanage PowerShell을 사용 하 여 보안 그룹을 네트워크 하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3706ce6c-d9ae-46cb-a048-f0a4e84dc5cc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 930fe5e0827896ad67b24d84e41a5d3f898ba838
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-powershell"></a>PowerShell을 사용하여 네트워크 보안 그룹 관리

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다. 이 문서에서는 Microsoft hello 클래식 배포 모델 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델을 사용 하 여 설명 합니다.
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a>정보 검색
기존 NSG를 보고 기존 NSG에 대한 규칙을 검색하며 NSG가 연결된 리소스에 대해 알아볼 수 있습니다.

### <a name="view-existing-nsgs"></a>기존 NSG 보기
tooview 구독에서 모든 기존 Nsg 실행 hello `Get-AzureRmNetworkSecurityGroup` cmdlet.

예상된 결과:

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : WEB1
    ResourceGroupName    : RG101
    Location             : eastus2
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG101/providers/M
                           icrosoft.Network/networkSecurityGroups/WEB1
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]


Nsg hello 실행은 특정 리소스 그룹의 tooview hello 목록 `Get-AzureRmNetworkSecurityGroup` cmdlet.

예상 출력:

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

### <a name="list-all-rules-for-an-nsg"></a>NSG에 대한 모든 규칙 나열
명명 된 NSG의 tooview hello 규칙 **NSG 프런트 엔드**, hello 다음 명령을 입력 합니다.

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

예상 출력:

    Name                     : rdp-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow RDP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 100
    Direction                : Inbound

    Name                     : web-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow HTTP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 80
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 101
    Direction                : Inbound

> [!NOTE]
> 사용할 수도 있습니다 `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` hello에서 toolist hello 기본 규칙 **NSG 프런트 엔드** NSG 합니다.
> 

### <a name="view-nsgs-associations"></a>NSG 연결 보기
tooview 어떤 리소스 hello **NSG 프런트 엔드** NSG와 연결, 실행 hello 다음 명령입니다.

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

Hello에 대 한 확인 **NetworkInterfaces** 및 **서브넷** 아래와 같이 속성:

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

Hello 이전 예에서 hello NSG는 되지 연결된 tooany Nic (네트워크 인터페이스); 명명 된 연결된 tooa 서브넷은 **프런트 엔드**합니다.

## <a name="manage-rules"></a>규칙 관리
기존 NSG 규칙 tooan 추가, 기존 규칙을 편집 하 고 규칙을 제거할 수 있습니다.

### <a name="add-a-rule"></a>규칙 추가
허용 하는 규칙 tooadd **인바운드** 트래픽 tooport **443** 모든 컴퓨터 toohello에서 **NSG 프런트 엔드** NSG, 단계를 수행 하는 전체 hello:

1. 다음 기존 NSG 명령 tooretrieve hello hello를 실행 하 고 변수에 저장 합니다.

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. 다음 명령은 tooadd hello 규칙 toohello NSG를 실행 합니다.

    ```powershell
    Add-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. toosave hello 변경 toohello NSG를 hello 다음 명령을 실행 합니다.

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    보안 규칙만 hello를 보여 주는 예상된 출력:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "*",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="change-a-rule"></a>규칙 변경
tooallow 위에서 만든 toochange hello 규칙 hello에서 트래픽 인바운드 **인터넷** 만 아래의 hello 단계를 수행 합니다.

1. 다음 기존 NSG 명령 tooretrieve hello hello를 실행 하 고 변수에 저장 합니다.

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Hello 다음 hello 새 규칙 설정으로 명령을 실행 합니다.

    ```powershell
    Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix Internet `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. toosave hello 변경 toohello NSG를 hello 다음 명령을 실행 합니다.

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    보안 규칙만 hello를 보여 주는 예상된 출력:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="delete-a-rule"></a>규칙 삭제
1. 다음 기존 NSG 명령 tooretrieve hello hello를 실행 하 고 변수에 저장 합니다.

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Hello 명령 tooremove hello 규칙 hello NSG에서에서 다음을 실행 합니다.

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. Hello 다음 명령을 실행 하 여 hello 변경 내용을 toohello NSG를 저장 합니다.

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    보안 규칙 통지 hello만 hello를 보여 주는 예상된 출력 **https 규칙** 더 이상 나열 합니다.
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 }
                               ]

## <a name="manage-associations"></a>연결 관리
NSG toosubnets 및 Nic를 연결할 수 있습니다. 또한 연결된 모든 리소스에서 NSG를 분리할 수 있습니다.

### <a name="associate-an-nsg-tooa-nic"></a>NSG tooa NIC에 연결
tooassociate hello **NSG 프런트 엔드** NSG toohello **TestNICWeb1** NIC를 다음 단계 완료 hello:

1. 다음 기존 NSG 명령 tooretrieve hello hello를 실행 하 고 변수에 저장 합니다.

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Hello 명령 tooretrieve hello 기존 NIC를 다음을 실행 하 고 변수에 저장 합니다.

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. 집합 hello **NetworkSecurityGroup** hello 속성 **NIC** hello 변수 toohello 값 **NSG** hello 다음 명령을 입력 하 여 변수:

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. toosave hello 변경 toohello NIC를 hello 다음 명령을 실행 합니다.

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    예상된 출력이 보여 주는 hello **NetworkSecurityGroup** 속성:
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a>NIC에서 NSG 분리
toodissociate hello **NSG 프런트 엔드** hello에서 NSG **TestNICWeb1** NIC를 다음 단계 완료 hello:

1. Hello 명령 tooretrieve hello 기존 NIC를 다음을 실행 하 고 변수에 저장 합니다.

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. 집합 hello **NetworkSecurityGroup** hello 속성 **NIC** 변수 너무**$null** hello 다음 명령을 실행 하 여:

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. toosave hello 변경 toohello NIC를 hello 다음 명령을 실행 합니다.

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    예상된 출력이 보여 주는 hello **NetworkSecurityGroup** 속성:
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a>서브넷에서 NSG 분리
toodissociate hello **NSG 프런트 엔드** hello에서 NSG **프런트 엔드** 서브넷, 단계를 수행 하는 전체 hello:

1. Hello 명령 tooretrieve hello 기존 VNet을 다음을 실행 하 고 변수에 저장 합니다.

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. 실행 hello 명령 tooretrieve hello 다음 **프런트 엔드** 서브넷 변수에 저장 합니다.

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. 집합 hello **NetworkSecurityGroup** hello 속성 **서브넷** 변수 너무**$null** hello 다음 명령을 입력 하 여:

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. toosave hello 변경 서브넷 toohello hello 다음 명령을 실행 합니다.

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    Hello의 hello 속성만 보여 주는 예상된 출력 **프런트 엔드** 서브넷입니다. **NetworkSecurityGroup**에 대한 속성이 없습니다.
   
            ...
            Subnets           : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                      },
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                      }
                                    ],
                                    "ProvisioningState": "Succeeded"
                                  },
                                    ...
                                ]

### <a name="associate-an-nsg-tooa-subnet"></a>NSG tooa 서브넷 연결
tooassociate hello **NSG 프런트 엔드** NSG toohello **FronEnd** 다시 서브넷, 단계를 수행 하는 전체 hello:

1. Hello 명령 tooretrieve hello 기존 VNet을 다음을 실행 하 고 변수에 저장 합니다.

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. 실행 hello 명령 tooretrieve hello 다음 **프런트 엔드** 서브넷 변수에 저장 합니다.

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. 다음 기존 NSG 명령 tooretrieve hello hello를 실행 하 고 변수에 저장 합니다.

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. 집합 hello **NetworkSecurityGroup** hello 속성 **서브넷** 변수 너무**$null** hello 다음 명령을 실행 하 여:

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. toosave hello 변경 서브넷 toohello hello 다음 명령을 실행 합니다.

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    예상된 출력이 보여 주는 hello **NetworkSecurityGroup** hello 속성 **프런트 엔드** 서브넷:
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a>NSG 삭제
NSG tooany 리소스를 연결 되지 않은 경우에 삭제할 수 있습니다. NSG를 toodelete는 아래의 hello 단계를 수행 합니다.

1. toocheck hello 리소스 관련 tooan NSG를 hello 실행 `azure network nsg show` 에서처럼 [보기 Nsg 연결](#View-NSGs-associations)합니다.
2. Hello NSG 연결된 tooany Nic 이면 hello 실행 `azure network nic set` 에서처럼 [NIC에서 NSG를 분리](#Dissociate-an-NSG-from-a-NIC) 각 NIC.에 대 한 
3. Hello NSG 연결된 tooany 서브넷 이면 hello 실행 `azure network vnet subnet set` 에서처럼 [서브넷에서 NSG를 분리](#Dissociate-an-NSG-from-a-subnet) 각 서브넷에 대 한 합니다.
4. toodelete hello NSG hello 다음 명령을 실행 합니다.

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > hello `-Force` 매개 변수를 사용 하면 tooconfirm hello 삭제 필요 하지 않습니다.
   > 

## <a name="next-steps"></a>다음 단계
* [로깅을 사용합니다](virtual-network-nsg-manage-log.md) .


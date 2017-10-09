---
title: "aaaCreate 네트워크 보안 그룹-Azure PowerShell | Microsoft Docs"
description: "자세한 내용은 방법 toocreate 및 PowerShell을 사용 하 여 네트워크 보안 그룹을 배포 합니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9cef62b8-d889-4d16-b4d0-58639539a418
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1c8db773febb163d9cb010d23f2913b5ebe0fa94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-powershell"></a>PowerShell을 사용하여 네트워크 보안 그룹 만들기

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

Azure에는 Azure Resource Manager 및 클래식이라는 두 가지 배포 모델이 있습니다. Hello 리소스 관리자 배포 모델을 통해 리소스를 만드는 것이 좋습니다. hello 읽기에 대해 더 알아봅니다 toolearn hello 두 모델 간의 차이 hello [이해 Azure 배포 모델](../azure-resource-manager/resource-manager-deployment-model.md) 문서. 이 문서에서는 hello 리소스 관리자 배포 모델에 설명 합니다. 수도 있습니다 [hello 클래식 배포 모델에서 Nsg를 만들](virtual-networks-create-nsg-classic-ps.md)합니다.

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

위의 hello 시나리오를 기반으로 hello 예제 PowerShell 명령 아래에 이미 만든 단순한 환경 필요 합니다. 이 문서에 표시 된 대로 toorun hello 명령을 원하는 경우 먼저 hello 테스트 환경을 구축 배포 하 여 [이 서식 파일](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), 클릭 **tooAzure 배포**, 대체 hello 기본 매개 변수 값 필요한 경우, 및의 지침에 따라 hello hello 포털 하는 경우.

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a>Toocreate NSG hello 프런트 엔드 서브넷에 대 한 hello 하는 방법
toocreate 라는 NSG *NSG 프런트 엔드* hello 시나리오에 따라, hello 다음 단계를 완료 합니다.

1. Azure PowerShell을 처음 사용 하는 경우 참조 [어떻게 tooInstall 및 Azure PowerShell 구성](/powershell/azure/overview) 모든 hello 방식으로 toohello toosign를 Azure로 끝나고 구독을 선택 하는 hello 지침을 따릅니다.
2. Hello 인터넷 tooport 3389에서에서 액세스를 허용 하는 보안 규칙을 만듭니다.

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name rdp-rule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
    ```

3. Hello 인터넷 tooport 80에서에서의 액세스를 허용 하는 보안 규칙을 만듭니다.

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule -Description "Allow HTTP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 101 `
    -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80
    ```

4. 새 NSG 라는 tooa 위에서 만든 hello 규칙 추가 **NSG 프런트 엔드**합니다.

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG -Location westus `
    -Name "NSG-FrontEnd" -SecurityRules $rule1,$rule2
    ```

5. Hello 다음을 입력 하 여 hello NSG에서에서 만든 hello 규칙을 확인 합니다.

    ```powershell
    $nsg
    ```
   
    표시 된 정당한 hello 보안 규칙을 출력 합니다.
   
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
                                   "Description": "Allow RDP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "3389",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 100,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 },
                                 {
                                   "Name": "web-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
                                   "Description": "Allow HTTP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "80",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 101,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]
6. NSG toohello 위에서 만든 연결 hello *프런트 엔드* 서브넷입니다.

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $nsg
    ```

    출력 표시 된 유일한 hello *프런트 엔드* 서브넷 설정, hello에 대 한 공지 hello 값 **NetworkSecurityGroup** 속성:
   
                    Subnets           : [
                                          {
                                            "Name": "FrontEnd",
                                            "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                            "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                            "AddressPrefix": "192.168.1.0/24",
                                            "IpConfigurations": [
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                              },
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                              }
                                            ],
                                            "NetworkSecurityGroup": {
                                              "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                            },
                                            "RouteTable": null,
                                            "ProvisioningState": "Succeeded"
                                          }
   
   > [!WARNING]
   > 위의 hello 명령에 대 한 hello 출력에는 PowerShell를 실행 하는 hello 컴퓨터에만 존재 하는 hello 가상 네트워크 구성 개체에 대 한 hello 콘텐츠를 보여 줍니다. Toorun hello 필요한 `Set-AzureRmVirtualNetwork` cmdlet toosave 이러한 설정 tooAzure 합니다.
   > 
   > 
7. 새 VNet 설정 tooAzure hello를 저장 합니다.

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    Hello NSG 부분만 표시를 출력 합니다.
   
        "NetworkSecurityGroup": {
          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
        }

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a>Toocreate NSG hello 백 엔드 서브넷에 대 한 hello 하는 방법
toocreate 라는 NSG *NSG 백 엔드* 위의 hello 시나리오에 따라, hello 다음 단계를 완료 합니다.

1. Hello 프런트 엔드 서브넷 tooport 1433 (SQL Server에서 사용 하는 기본 포트)에서 액세스를 허용 하는 보안 규칙을 만듭니다.

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name frontend-rule `
    -Description "Allow FE subnet" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix 192.168.1.0/24 -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 1433
    ```

2. 인터넷 액세스 toohello 차단 보안 규칙을 만듭니다.

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule `
    -Description "Block Internet" `
    -Access Deny -Protocol * -Direction Outbound -Priority 200 `
    -SourceAddressPrefix * -SourcePortRange * `
    -DestinationAddressPrefix Internet -DestinationPortRange *
    ```

3. 새 NSG 라는 tooa 위에서 만든 hello 규칙 추가 **NSG 백 엔드**합니다.

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG `
    -Location westus -Name "NSG-BackEnd" `
    -SecurityRules $rule1,$rule2
    ```

4. NSG toohello 위에서 만든 연결 hello *백 엔드* 서브넷입니다.

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd ` 
    -AddressPrefix 192.168.2.0/24 -NetworkSecurityGroup $nsg
    ```

    출력 표시 된 유일한 hello *백 엔드* 서브넷 설정, hello에 대 한 공지 hello 값 **NetworkSecurityGroup** 속성:
   
        Subnets           : [
                      {
                        "Name": "BackEnd",
                        "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                        "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                        "AddressPrefix": "192.168.2.0/24",
                        "IpConfigurations": [...],
                        "NetworkSecurityGroup": {
                          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "RouteTable": null,
                        "ProvisioningState": "Succeeded"
                      }
5. 새 VNet 설정 tooAzure hello를 저장 합니다.

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

## <a name="how-tooremove-an-nsg"></a>어떻게 tooremove NSG
toodelete 기존 NSG 호출 *NSG 프런트 엔드* 이 경우 아래의 hello 단계를 수행 합니다.

Hello 실행 **제거 AzureRmNetworkSecurityGroup** 아래에 표시 된 NSG 중인 있는지 tooinclude hello 리소스 그룹 hello 수입니다.

```powershell
Remove-AzureRmNetworkSecurityGroup -Name "NSG-FrontEnd" -ResourceGroupName "TestRG"
```


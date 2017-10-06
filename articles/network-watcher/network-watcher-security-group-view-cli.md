---
title: "Azure 네트워크 감시자 보안 그룹 보기-Azure CLI 2.0을 통한 aaaAnalyze 네트워크 보안 | Microsoft Docs"
description: "이 문서는 어떻게 Azure CLI 2.0 toouse tooanalyze a 가상 컴퓨터 보안 보안 그룹을 설명 합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a986ff4f-7e0c-4994-95e1-4ac824986500
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 31a4cd628f54d7548f495251fd275f099e79a060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-20"></a>Azure CLI 2.0을 사용하는 보안 그룹 보기에서 가상 컴퓨터 보안 분석

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-security-group-view-powershell.md)
> - [CLI 1.0](network-watcher-security-group-view-cli-nodejs.md)
> - [CLI 2.0](network-watcher-security-group-view-cli.md)
> - [REST API](network-watcher-security-group-view-rest.md)

보안 그룹 보기 구성 하 고 효과적인 네트워크 보안 규칙을 적용된 tooa 가상 컴퓨터를 반환 합니다. 이 기능은 유용 tooaudit은 네트워크 보안 그룹 진단 및 VM tooensure 트래픽이에 구성 되어 있는 규칙은 올바르게 허용 또는 거부 합니다. 이 문서에서는 보여줍니다 tooretrieve hello 구성 하는 방법 및 Azure CLI를 사용 하 여 효과적인 보안 규칙 tooa 가상 컴퓨터


이 문서에서는 Windows, Mac 및 Linux에 대 한 사용 하지 않는 hello 리소스 관리 배포 모델, Azure CLI 2.0에 대 한 우리의 차세대 CLI 합니다.

이 문서의 단계를 tooperform hello, 너무 필요한[Mac, Linux 및 Windows Azure CLI ()에 대 한 hello Azure 명령줄 인터페이스 설치](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)합니다.

## <a name="before-you-begin"></a>시작하기 전에

이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.

## <a name="scenario"></a>시나리오

이 문서에서 다루는 hello 시나리오를 구성 하는 hello 및 지정된 된 가상 컴퓨터에 대 한 효과적인 보안 규칙 검색 합니다.

## <a name="get-a-vm"></a>VM 확인

가상 컴퓨터는 필요한 toorun hello `vm list` cmdlet. hello 다음 명령은 나열 리소스 그룹의 hello 가상 컴퓨터.

```azurecli
az vm list -resource-group resourceGroupName
```

Hello 가상 컴퓨터를 알게 되 면 hello를 사용할 수 있습니다 `vm show` cmdlet tooget 상대방이 리소스 Id:

```azurecli
az vm show -resource-group resourceGroupName -name virtualMachineName
```

## <a name="retrieve-security-group-view"></a>보안 그룹 보기 검색

hello 다음 단계 tooretrieve hello 보안 그룹 뷰 결과입니다.

```azurecli
az network watcher show-security-group-view --resource-group resourceGroupName --vm vmName
```

## <a name="viewing-hello-results"></a>Hello 결과 보기

hello 다음 예제는 반환 된 hello 결과의 축약된 응답 합니다. hello 결과 표시 모든 hello 효과적이 고 적용 된 보안 규칙의 그룹에 세분화 hello 가상 컴퓨터에서 **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, 및  **EffectiveSecurityRules**합니다.

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
      "resourceGroup": "{resourceGroupName}",
      "securityRuleAssociations": {
        "defaultSecurityRules": [
          {
            "access": "Allow",
            "description": "Allow inbound traffic from all VMs in VNET",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "*",
            "direction": "Inbound",
            "etag": null,
            "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups//providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/AllowVnetInBound",
            "name": "AllowVnetInBound",
            "priority": 65000,
            "protocol": "*",
            "provisioningState": "Succeeded",
            "resourceGroup": "",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "*"
          }...
        ],
        "effectiveSecurityRules": [
          {
            "access": "Deny",
            "destinationAddressPrefix": "*",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": null,
            "expandedSourceAddressPrefix": null,
            "name": "DefaultOutboundDenyAll",
            "priority": 65500,
            "protocol": "All",
            "sourceAddressPrefix": "*",
            "sourcePortRange": "0-65535"
          },
          {
            "access": "Allow",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "expandedSourceAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "name": "DefaultRule_AllowVnetOutBound",
            "priority": 65000,
            "protocol": "All",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "0-65535"
          },...
        ],
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "resourceGroup": "{resourceGroupName}",
          "securityRules": [
            {
              "access": "Allow",
              "description": null,
              "destinationAddressPrefix": "*",
              "destinationPortRange": "3389",
              "direction": "Inbound",
              "etag": "W/\"efb606c1-2d54-475a-ab20-da3f80393577\"",
              "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "name": "default-allow-rdp",
              "priority": 1000,
              "protocol": "TCP",
              "provisioningState": "Succeeded",
              "resourceGroup": "{resourceGroupName}",
              "sourceAddressPrefix": "*",
              "sourcePortRange": "*"
            }
          ]
        },
        "subnetAssociation": null
      }
    }
  ]
}
```

## <a name="next-steps"></a>다음 단계

방문 [감사 보안 그룹 NSG (네트워크)와 네트워크 감시자](network-watcher-nsg-auditing-powershell.md) toolearn 방법을 네트워크 보안 그룹의 tooautomate 유효성 검사 합니다.

Hello 보안 규칙을 방문 하 여 적용 된 tooyour 네트워크 리소스에 대 한 자세한 [보안 그룹, 개요 보기](network-watcher-security-group-view-overview.md)

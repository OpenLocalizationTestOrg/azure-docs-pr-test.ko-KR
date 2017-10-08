---
title: "Azure 네트워크 감시자 보안 그룹 보기-Azure CLI 1.0을 통한 aaaAnalyze 네트워크 보안 | Microsoft Docs"
description: "이 문서는 어떻게 Azure CLI 1.0 toouse tooanalyze a 가상 컴퓨터 보안 보안 그룹을 설명 합니다."
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
ms.openlocfilehash: 96383a734b94d215d5b0f3d47339e46940d700b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a>Azure CLI 1.0을 사용하는 보안 그룹 보기에서 가상 컴퓨터 보안 분석

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-security-group-view-powershell.md)
> - [CLI 1.0](network-watcher-security-group-view-cli-nodejs.md)
> - [CLI 2.0](network-watcher-security-group-view-cli.md)
> - [REST API](network-watcher-security-group-view-rest.md)

보안 그룹 보기 구성 하 고 효과적인 네트워크 보안 규칙을 적용된 tooa 가상 컴퓨터를 반환 합니다. 이 기능은 유용 tooaudit은 네트워크 보안 그룹 진단 및 VM tooensure 트래픽이에 구성 되어 있는 규칙은 올바르게 허용 또는 거부 합니다. 이 문서에서는 보여줍니다 tooretrieve hello 구성 하는 방법 및 Azure CLI를 사용 하 여 효과적인 보안 규칙 tooa 가상 컴퓨터

이 문서에서는 Windows, Mac 및 Linux에 사용할 수 있는 플랫폼 간 Azure CLI 1.0을 사용합니다. Network Watcher는 현재 CLI 지원을 위한 Azure CLI 1.0을 사용합니다.

## <a name="before-you-begin"></a>시작하기 전에

이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.

## <a name="scenario"></a>시나리오

이 문서에서 다루는 hello 시나리오를 구성 하는 hello 및 지정된 된 가상 컴퓨터에 대 한 효과적인 보안 규칙 검색 합니다.

## <a name="get-a-vm"></a>VM 확인

가상 컴퓨터는 필요한 toorun hello `vm list` cmdlet. hello 다음 명령은 나열 된 리소스 그룹에에서 가상 machinese hello:

```azurecli
azure vm list -g resourceGroupName
```

Hello 가상 컴퓨터를 알게 되 면 hello를 사용할 수 있습니다 `vm show` cmdlet tooget 상대방이 리소스 Id:

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a>보안 그룹 보기 검색

hello 다음 단계 tooretrieve hello 보안 그룹 뷰 결과입니다. 추가 hello "-json" 플래그 json에서 hello 결과 서식을 지정 합니다.

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-hello-results"></a>Hello 결과 보기

hello 다음 예제는 반환 된 hello 결과의 축약된 응답 합니다. hello 결과 표시 모든 hello 효과적이 고 적용 된 보안 규칙의 그룹에 세분화 hello 가상 컴퓨터에서 **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, 및  **EffectiveSecurityRules**합니다.

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testnic",
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testvm",
          "securityRules": [
            {
              "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/test-nsg/securityRules/default-allow-rdp",
              "protocol": "TCP",
              "sourcePortRange": "*",
              "destinationPortRange": "3389",
              "sourceAddressPrefix": "*",
              "destinationAddressPrefix": "*",
              "access": "Allow",
              "priority": 1000,
              "direction": "Inbound",
              "provisioningState": "Succeeded",
              "name": "default-allow-rdp",
              "etag": "W/\"00000000-0000-0000-0000-000000000000\""
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/networkSecurityGroups//defaultSecurityRules/",
            "description": "Allow inbound traffic from all VMs in VNET",
            "protocol": "*",
            "sourcePortRange": "*",
            "destinationPortRange": "*",
            "sourceAddressPrefix": "VirtualNetwork",
            "destinationAddressPrefix": "VirtualNetwork",
            "access": "Allow",
            "priority": 65000,
            "direction": "Inbound",
            "provisioningState": "Succeeded",
            "name": "AllowVnetInBound"
          }
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a>다음 단계

방문 [감사 보안 그룹 NSG (네트워크)와 네트워크 감시자](network-watcher-nsg-auditing-powershell.md) toolearn 방법을 네트워크 보안 그룹의 tooautomate 유효성 검사 합니다.

Hello 보안 규칙을 방문 하 여 적용 된 tooyour 네트워크 리소스에 대 한 자세한 [보안 그룹, 개요 보기](network-watcher-security-group-view-overview.md)

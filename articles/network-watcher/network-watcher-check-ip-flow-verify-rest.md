---
title: "Azure 네트워크 감시자 IP 흐름을 사용 하 여 aaaVerify 트래픽을 확인-REST | Microsoft Docs"
description: "이 문서에서는 설명 방법을 toocheck 가상 컴퓨터에서 트래픽 tooor 허용 또는 거부 하는 경우"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3307a79f-03be-46a0-aaaf-b2079cb5f3b2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 956db0d326db597c6c402a9e8d4a5522c47c02d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Azure Network Watcher의 구성 요소인 IP 흐름 확인을 사용하여 트래픽을 허용하는지 아니면 거부하는지를 확인합니다.

> [!div class="op_single_selector"]
> - [Azure 포털](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST API](network-watcher-check-ip-flow-verify-rest.md)


IP 흐름은 tooor 가상 컴퓨터에서 트래픽을 허용 하는 경우 tooverify 수 있는 네트워크 감시자의 기능을 확인 합니다. 들어오거나 나가는 트래픽에 대 한 hello 유효성 검사를 실행할 수 있습니다. 이 시나리오는 유용한 tooget tooan 외부 리소스 또는 백 엔드 가상 컴퓨터를 서로 연결할 수 있는지 여부의 현재 상태입니다. IP 흐름 보안 그룹 NSG (네트워크) 규칙에 올바르게 구성 되어 NSG 규칙에 의해 차단 되는 흐름 문제를 해결 하는 경우 사용 되는 tooverify 수를 확인 합니다. IP를 사용 하는 또 다른 이유 흐름 tooensure 트래픽이 차단 되도록 제대로 hello NSG 차단 하 고이 확인 합니다.

## <a name="before-you-begin"></a>시작하기 전에

ARMclient는 PowerShell을 사용 하 여 사용 되는 toocall hello REST API입니다. ARMClient는 [Chocolatey의 ARMClient](https://chocolatey.org/packages/ARMClient)에서 chocolatey에 있습니다.

이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.

## <a name="scenario"></a>시나리오

이 시나리오에서는 가상 컴퓨터 포트 443 통해 tooanother 컴퓨터 수와 통신 하는 경우 IP 흐름 확인 tooverify를 사용 합니다. Hello 트래픽이 거부 되 면 해당 트래픽을 거부 하는 hello 보안 규칙을 반환 합니다. IP 흐름 확인에 대 한 더 toolearn 방문 [IP 흐름 개요를 확인 하십시오.](network-watcher-ip-flow-verify-overview.md)

이 시나리오에서는 다음을 수행합니다.

* 가상 컴퓨터 검색
* IP 흐름 확인 호출
* 결과 확인

## <a name="log-in-with-armclient"></a>ARMClient로 로그인

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>가상 컴퓨터 검색

다음 스크립트 tooreturn hello 가상 컴퓨터를 실행 합니다. hello 다음 코드에 필요한 값 hello 변수에 대 한:

* **subscriptionId** -구독 Id toouse hello 합니다.
* **resourceGroupName** -hello 가상 컴퓨터를 포함 하는 리소스 그룹의 이름입니다.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

hello 필요한 정보는 hello id hello 종류에서 `Microsoft.Compute/virtualMachines`합니다. hello 결과 아래의 코드 예제와 비슷한 toohello 됩니다.

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft
.Network/networkInterfaces/contosovm842"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Com
pute/virtualMachines/ContosoVM/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="call-ip-flow-verify"></a>IP 흐름 확인 호출

hello 다음 예제에서는 지정 된 가상 컴퓨터에 대 한 요청 tooverify hello 트래픽을 hello 응답 hello 트래픽을 허용 하는 경우 또는 hello 트래픽이 거부 된 경우에 반환 합니다. 트래픽에서 거부 된 경우 어떤 규칙 블록 hello 트래픽 반환 합니다.

> [!NOTE]
> IP 흐름 확인 hello VM 리소스 할당 해야 합니다.

hello 스크립트 hello 리소스 hello 가상 컴퓨터에서 네트워크 인터페이스 카드 및 가상 컴퓨터의 Id를 필요합니다. Hello 출력 앞에서 이러한 값을 제공 합니다.

> [!Important]
> 모든 네트워크 감시자 REST에 대 한 호출 hello hello 요청 URI는 hello 진단 작업에서 수행 하는 hello 리소스가 아닌 hello 네트워크 감시자 인스턴스를 포함 하는 hello에에서 리소스 그룹 이름입니다.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$vmName = "<vm name>"
$vmNICName = "<vm NIC name>"
$direction = "<direction of traffic>" # Examples are: Inbound or Outbound
$localIP = "<source IP>"
$localPort = "<source Port>"
$remoteIP = "<destination IP>"
$remotePort = "<destination Port>" # Examples are: 80, or 80-120
$protocol = "<UDP, TCP or *>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.compute/virtualMachine/${vmName}
$targetNic = "<uri of target nic resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkInterfaces/${vmNICName}

$requestBody = @"
{
    'targetResourceId':  '$targetUri',
    'direction':  '$direction',
    'protocol':  '$protocol',
    'localPort':  '$localPort',
    'remotePort':  '$remotePort',
    'localIPAddress':  '$localIP',
    'remoteIPAddress':  '$remoteIP',
    'targetNICResourceId':  '$targetNic'
}
"@
        
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/ipFlowVerify?api-version=2016-12-01" $requestBody -verbose
```

## <a name="understanding-hello-results"></a>Hello 결과 이해

hello 응답 반환 hello 트래픽을 허용 또는 거부 여부를 알려줍니다. hello 응답 예제 따르는 hello 중 같습니다.

**허용됨**

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

**거부됨**

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a>다음 단계

트래픽을 차단 하지 않아야 하는 경우 참조 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn 네트워크 보안 그룹에 대 한 자세한 합니다.













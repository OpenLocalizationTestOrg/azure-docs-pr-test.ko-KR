---
title: "Azure 네트워크 감시자 IP 흐름 확인-Azure CLI aaaVerify 트래픽 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 toocheck 가상 컴퓨터에서 트래픽 tooor 허용 또는 Azure CLI를 사용 하 여 거부 된 경우"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c6becc5c142837b04d15490b2b3bd11124434570
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>트래픽은 허용 되거나 Azure 네트워크 감시자의 구성 요소는 VM과 IP 확인 흐름에서 tooor을 거부 하는 경우를 확인 합니다.

> [!div class="op_single_selector"]
> - [Azure 포털](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST API](network-watcher-check-ip-flow-verify-rest.md)


IP 흐름은 tooor 가상 컴퓨터에서 트래픽을 허용 하는 경우 tooverify 수 있는 네트워크 감시자의 기능 확인 합니다. 이 시나리오는 유용한 tooget tooan 외부 리소스 또는 백 엔드 가상 컴퓨터를 서로 연결할 수 있는지 여부의 현재 상태입니다. IP 흐름 보안 그룹 NSG (네트워크) 규칙에 올바르게 구성 되어 NSG 규칙에 의해 차단 되는 흐름 문제를 해결 하는 경우 사용 되는 tooverify 수를 확인 합니다. IP를 사용 하는 또 다른 이유 흐름 tooensure 트래픽이 차단 되도록 제대로 hello NSG 차단 하 고이 확인 합니다.

이 문서에서는 Windows, Mac 및 Linux에 사용할 수 있는 플랫폼 간 Azure CLI 1.0을 사용합니다.

## <a name="before-you-begin"></a>시작하기 전에

이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 네트워크 감시자의 기존 인스턴스가 또는 합니다. hello 시나리오는 또한 적합 한 가상 컴퓨터가 리소스 그룹 사용 toobe 있다고 가정 합니다.

## <a name="scenario"></a>시나리오

이 시나리오는 가상 컴퓨터 수와 통신 tooa 알려진 경우 IP 확인 흐름 tooverify 사용 하 여 Bing IP 주소입니다. Hello 트래픽이 거부 되 면 해당 트래픽을 거부 하는 hello 보안 규칙을 반환 합니다. IP 확인 흐름에 대 한 자세한 toolearn 방문 [IP 흐름 확인 개요](network-watcher-ip-flow-verify-overview.md)


## <a name="get-a-vm"></a>VM 확인

IP 흐름에서의 원격 대상에서 가상 컴퓨터 tooor IP 주소를 트래픽 tooor 테스트를 확인 합니다. 가상 컴퓨터의 Id가 hello cmdlet에 대 한 필요 합니다. 가상 컴퓨터 toouse hello의 hello ID를 알고 있는 경우이 단계를 건너뛸 수 있습니다.

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-hello-nics"></a>Hello NIC 가져오기

hello 가상 컴퓨터에서 NIC의 IP 주소가 hello hello Nic는 가상 컴퓨터에서 검색 하는이 예에서 필요할 때. 원하는 tootest hello IP 주소를 알고 있으면 hello 가상 컴퓨터에서이 단계를 건너뛸 수 있습니다.

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a>IP 흐름 확인 실행

Hello 았 hello 정보 toorun hello 필요한 cmdlet을 실행할 `network watcher ip-flow-verify` cmdlet tootest hello 트래픽입니다. 이 예제에서 사용 하 여 첫 번째 IP 주소가 hello hello 첫 번째 NIC에서

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> IP 흐름 hello VM 리소스 toorun가 할당 되는 필요한 확인 합니다.

## <a name="review-results"></a>결과 검토

실행 된 후 `network watcher ip-flow-verify` hello 다음 예제는 hello 앞 단계에서에서 반환 된 hello 결과, hello 결과가 반환 됩니다.

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a>다음 단계

트래픽을 차단 하지 않아야 하는 경우 참조 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hello 네트워크 보안 그룹 및 보안 정의 된 규칙을 중지 합니다.

방문 하 여 tooaudit NSG 설정을 알아봅니다 [감사 보안 그룹 NSG (네트워크)와 네트워크 감시자](network-watcher-nsg-auditing-powershell.md)합니다.

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png

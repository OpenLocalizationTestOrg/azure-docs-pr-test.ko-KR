---
title: "Azure 네트워크 감시자 다음 홉-REST와 다음 홉 aaaFind | Microsoft Docs"
description: "이 문서는 어떤 hello 다음 홉 형식 및 ip 주소를 사용 하 여 다음 홉을 사용 하 여 hello Azure REST API를 찾는 방법을 설명 합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a2b61b355aae8ae513ebd44837184fbc6cfd668c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a>어떤 hello 다음 홉 형식이 Aure 네트워크 감시자 Azure REST API를 사용 하 여 hello 다음 홉 기능을 사용 하는 확인

> [!div class="op_single_selector"]
> - [Azure 포털](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [Azure REST API](network-watcher-check-next-hop-rest.md)

다음 홉 hello 기능을 제공 하는 네트워크 감시자의 기능을 가져오고 hello 다음 홉 형식이 지정 된 가상 컴퓨터를 기반으로 하는 IP 주소입니다. 이 기능은 가상 컴퓨터를 종료 하는 트래픽이 게이트웨이, 인터넷 또는 가상 네트워크 tooget tooits 대상에서 이동 하는 경우를 결정 하는 데 유용 합니다.

## <a name="before-you-begin"></a>시작하기 전에

ARMclient는 PowerShell을 사용 하 여 사용 되는 toocall hello REST API입니다. ARMClient는 [Chocolatey의 ARMClient](https://chocolatey.org/packages/ARMClient)에서 chocolatey에 있습니다.

이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.

## <a name="scenario"></a>시나리오

이 문서에서 설명 하는 hello 시나리오는 다음 홉 hello 다음 홉 형식 및 리소스에 대 한 IP 주소를 확인 하는 네트워크 감시자의 기능을 사용 합니다. 다음 홉에 대 한 자세한 toolearn 방문 [다음 홉 개요](network-watcher-next-hop-overview.md)합니다.

이 시나리오에서는 다음을 수행합니다.

* 가상 컴퓨터에 대 한 다음 홉 hello를 검색 합니다.

## <a name="log-in-with-armclient"></a>ARMClient에 로그인

Tooarmclient Azure 자격 증명으로 로그인 합니다.

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>가상 컴퓨터 검색

다음 스크립트 tooreturn hello 가상 컴퓨터를 실행 합니다. 다음 홉을 실행하는 데 이 정보가 필요합니다.

hello 코드 다음 변수에 따라 hello에 대 한 값을 해야 합니다.

- **subscriptionId** -구독 Id toouse hello 합니다.
- **resourceGroupName** -hello 가상 컴퓨터를 포함 하는 리소스 그룹의 이름입니다.

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

Hello 다음과 같은 출력에서 hello 가상 컴퓨터의 hello id는 다음 예제는 hello에 사용 됩니다.

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="get-next-hop"></a>다음 홉 가져오기

Hello 권한 부여 헤더를 만든 후에 가상 컴퓨터에서 다음 홉 hello를 검색할 수 있습니다. hello 다음 값 바꾸어야 코드 예제에서는 toowork hello에 대 한 합니다.

> [!Important]
> 네트워크 감시자 REST API에 대 한 호출 hello hello 요청 URI는 hello 진단 작업에서 수행 하는 hello 리소스가 아닌 hello 네트워크 감시자를 포함 하는 hello 리소스 그룹에에서 리소스 그룹 이름입니다.

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> 다음 홉 VM 리소스 hello toorun가 할당 되는 필요 합니다.

## <a name="results"></a>결과

hello 다음 코드 조각은 수신 하는 hello 출력 예입니다. hello 결과는 다음 값에는 hello 포함:

* **nextHopType** -이 값은 hello 다음 값 중 하나: 인터넷, virtualappliance 인, VirtualNetworkGateway, VnetLocal, HyperNetGateway, 또는 None입니다.
* **nextHopIpAddress** -hello hello 다음 홉의 IP 주소입니다.
* **routeTableId** hello 값은 hello 경로와 연결 된 hello 경로 테이블에 대 한 uri 또는 경로의 정의 된 hello 값이 사용자 정의 하지 않는 경우- *시스템 경로* 반환 됩니다.

hello 다음은 hello 결과를 json 형식입니다.

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a>다음 단계

가상 컴퓨터에 대 한 다음 홉 hello 아웃 수 toofind 되 면 방문 하 여 네트워크 리소스의 보안을 hello를 볼 수 있습니다 [보안 보기 개요](network-watcher-security-group-view-overview.md)















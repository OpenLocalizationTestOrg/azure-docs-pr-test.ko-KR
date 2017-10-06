---
title: "Azure 네트워크 감시자를 네트워크 보안 그룹에 대 한 aaaIntroduction tooflow 로깅을 | Microsoft Docs"
description: "이 페이지에서는 toouse NSG 흐름 Azure 네트워크 감시자의 기능을 기록 하는 방법을 설명 합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 47d91341-16f1-45ac-85a5-e5a640f5d59e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: da85e946147b14717144cb47d1c742057c6dfa24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooflow-logging-for-network-security-groups"></a>네트워크 보안 그룹에 대 한 소개 tooflow 로깅

네트워크 보안 그룹 흐름 로그는 네트워크 보안 그룹을 통해 IP 트래픽 ingress 및 egress에 대 한 tooview 정보 수 있는 네트워크 감시자의 기능입니다. 이러한 흐름 로그 json 형식으로 작성 되 고 아웃 바운드 표시 및 hello 흐름 (소스/대상 IP, 소스/대상 포트, 프로토콜)에 대 한 5-튜플 정보에 각 규칙 별로 인바운드 흐름 hello NIC hello 흐름 적용 하 고 트래픽이 허용 된 경우 hello 또는 거부 됩니다.

![흐름 로그 개요][1]

표시 되지 흐름 대상 네트워크 보안 그룹 로그, 동안 hello 동일 hello로 다른 로그입니다. 다음 예제는 hello와 같이 저장소 계정 및 다음 hello 로깅 경로 내 에서만 흐름 로그 저장 됩니다.

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

동일한 hello 다른 로그에 표시 된 대로 보존 정책을 tooflow 로그를 적용 합니다. 로그에는 1 한 일에서 설정할 수 있는 보존 정책을 포함 합니다. 보존 정책이 설정 되어 있지 않으면 hello 로그 영원히 유지 됩니다.

## <a name="log-file"></a>로그 파일

흐름 로그에는 여러 속성이 있습니다. hello 다음 목록에는의 목록을 hello NSG 흐름 로그 내에서 반환 되는 hello 속성:

* **시간** -hello 이벤트가 기록 된 시간
* **systemId** - 네트워크 보안 그룹 리소스 ID
* **범주** -hello 범주 hello 이벤트의이 항상 수 NetworkSecurityGroupFlowEvent
* **resourceid** -hello 리소스 hello NSG의 Id
* **operationName** - 항상 NetworkSecurityGroupFlowEvents
* **속성** -hello 흐름의 속성 컬렉션
    * **버전** -hello 흐름 로그 이벤트 스키마의 버전 번호
    * **흐름** - 흐름의 컬렉션입니다. 이 속성에는 서로 다른 규칙에 대한 여러 항목이 있습니다.
        * **규칙** -흐름 나열 된는 hello에 대 한 규칙
            * **흐름** - 흐름의 컬렉션
                * **mac** -hello hello hello 흐름 수집 된 VM에 대 한 hello NIC의 MAC 주소
                * **flowTuples** -hello 흐름 튜플 쉼표로 구분 된 형식에서에 대 한 여러 속성을 포함 하는 문자열
                    * **타임 스탬프** -hello 흐름 UNIX EPOCH 형식에서 발생 했을 때이 값은의 hello 타임 스탬프
                    * **원본 IP** -hello 원본 IP
                    * **대상 IP** -hello 대상 IP
                    * **원본 포트** -hello 원본 포트
                    * **대상 포트** -hello 대상 포트
                    * **프로토콜** -hello hello 흐름의 프로토콜입니다. 유효한 값은 TCP에 대해서 **T**이며 UDP에 대해서 **U**입니다.
                    * **트래픽 흐름** -hello hello 트래픽 흐름 방향입니다. 유효한 값은 인바운드에 대해서 **I**이며 아웃바운드에 대해서 **O**입니다.
                    * **트래픽** - 트래픽이 허용되었는지 거부되었는지 여부입니다. 유효한 값은 허용에 대해 **A**이며 거부에 대해 **D**입니다.


hello 다음은 흐름 로그의 예입니다. Hello 앞 섹션에서에서 설명 하는 hello 속성 목록에 나오는 레코드가 여러 개 볼 수 있습니다. 

> [!NOTE]
> Hello flowTuples 속성의 값은 쉼표로 구분 된 목록입니다.
 
```json
{
    "records": 
    [
        
        {
             "time": "2017-02-16T22:00:32.8950000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282421,42.119.146.95,10.1.0.4,51529,5358,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282370,163.28.66.17,10.1.0.4,61771,3389,T,I,A","1487282393,5.39.218.34,10.1.0.4,58596,3389,T,I,A","1487282393,91.224.160.154,10.1.0.4,61540,3389,T,I,A","1487282423,13.76.89.229,10.1.0.4,53163,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:01:32.8960000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282481,195.78.210.194,10.1.0.4,53,1732,U,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282435,61.129.251.68,10.1.0.4,57776,3389,T,I,A","1487282454,84.25.174.170,10.1.0.4,59085,3389,T,I,A","1487282477,77.68.9.50,10.1.0.4,65078,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:02:32.9040000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282492,175.182.69.29,10.1.0.4,28918,5358,T,I,D","1487282505,71.6.216.55,10.1.0.4,8080,8080,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282512,91.224.160.154,10.1.0.4,59046,3389,T,I,A"]}]}]}
        }
        ,
        ...
```

## <a name="next-steps"></a>다음 단계

방문 하 여 tooenable 흐름을 기록 하는 방법에 대해 알아봅니다 [흐름을 사용 하도록 설정 하는 로깅](network-watcher-nsg-flow-logging-portal.md)합니다.

[NSG(네트워크 보안 그룹)에 대한 로그 분석](../virtual-network/virtual-network-nsg-manage-log.md)을 방문하여 NSG 로깅에 대해 알아봅니다.

[IP 흐름 확인으로 트래픽 확인](network-watcher-check-ip-flow-verify-portal.md)을 방문하여 VM에서 트래픽이 허용되는지 또는 거부되는지 확인합니다.

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png


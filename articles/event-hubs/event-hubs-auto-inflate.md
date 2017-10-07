---
title: "Azure 이벤트 허브 처리량 단위 aaaAutomatically 수직 | Microsoft Docs"
description: "자동 확장할 처리량 단위는 네임 스페이스 tooautomatically 확장에서 사용 하도록 설정"
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: shvija;sethm
ms.openlocfilehash: 0f5216bcd619ccddc1fd4063a2f0131bfa36c7d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a>Azure Event Hubs 처리량 단위 자동 확장

## <a name="overview"></a>개요

Azure Event Hubs는 확장성이 뛰어난 데이터 스트리밍 플랫폼입니다. 따라서 이벤트 허브 고객 온 보 딩 toohello 서비스 보다 나중의 용도 종종 늘립니다. 이러한 증가 증가 함에 따라 미리 결정 된 hello 처리량 단위 (TUs) tooscale 이벤트 허브 필요 하 고 전송 속도 더 큰 처리 합니다. hello *자동 확장할* hello 수가 TUs toomeet 사용 해야 하는 이벤트 허브의 기능이 자동으로 확장 합니다. TU를 늘리면 다음 경우에 제한 시나리오를 방지합니다.

* 데이터 수신 속도가 설정된 TU를 초과하는 경우
* 데이터 송신 요청 속도가 설정된 TU를 초과하는 경우

## <a name="how-auto-inflate-works"></a>자동 확장 작동 방식

Event Hubs 트래픽은 처리량 단위로 제어됩니다. 단일 TU는 초당 1MB의 수신을 허용하고 송신량은 그 두 배입니다. Standard Event Hubs는 처리량 단위를 1-20으로 구성할 수 있습니다. 자동 확장할 toostart를 hello 필요한 최소 처리량 단위 여 작은 항목부터 있습니다. hello 기능 toohello 최대 한도 사용자 트래픽의 hello 증가 따라 필요한 처리량 단위 자동으로 다음 확장입니다. 자동 확장할 hello를 다음 이점을 제공 합니다.

- 크기 조정 메커니즘의 효율적인 toostart 작은 및 스케일 업 때 증가합니다.
- Toohello 조정 문제 없이 지정 된 최대 제한 크기를 자동으로 조정 합니다.
- 상세하게 제어할 배율 시기를 제어 하는 대로 및 얼마나 tooscale 합니다.

## <a name="enable-auto-inflate-on-a-namespace"></a>네임스페이스에서 자동 확장 사용

자동 확장할 hello 메서드를 다음 중 하나를 사용 하 여 네임 스페이스에서 사용 하지 않도록 하거나 설정할 수 있습니다.

1. hello [Azure 포털](https://portal.azure.com)합니다.
2. Azure Resource Manager 템플릿

### <a name="enable-auto-inflate-through-hello-portal"></a>자동 확장할 hello 포털을 통해 사용 하도록 설정

Hello 자동 확장할 기능 네임 스페이스에는 이벤트 허브 네임 스페이스를 만들 때 설정할 수 있습니다.
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

이 옵션을 사용하도록 설정하면 작은 처리량 단위부터 시작하여 필요한 사용량 증가에 따라 확장할 수 있습니다. hello 확장에 대 한 상한값 없이 가격, hello TUs 시간당 사용 되는 다양 한에 종속 되 있습니다.

또한 자동 확장할을 사용할 수 있습니다 hello를 사용 하 여 **배율** hello 포털의 설정 블레이드에서 hello 옵션:
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a>Azure Resource Manager 템플릿을 사용하여 자동 확장 사용

Azure Resource Manager 템플릿을 배포하는 동안 자동 확장을 사용하도록 설정할 수 있습니다. 예를 들어 집합 hello `isAutoInflateEnabled` 속성 너무**true** 설정 `maximumThroughputUnits` too10 합니다.

```json
"resources": [
        {
            "apiVersion": "2017-04-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "properties": {
                "isAutoInflateEnabled": true,
                "maximumThroughputUnits": 10
            },
            "resources": [
                {
                    "apiVersion": "2017-04-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {},
                    "resources": [
                        {
                            "apiVersion": "2017-04-01",
                            "name": "[parameters('consumerGroupName')]",
                            "type": "ConsumerGroups",
                            "dependsOn": [
                                "[parameters('eventHubName')]"
                            ],
                            "properties": {}
                        }
                    ]
                }
            ]
        }
    ]
```

Hello 전체 서식 파일에 대 한 참조 hello [만들 이벤트 허브 네임 스페이스를 사용 하도록 설정한 확장할](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) GitHub에서 서식 파일입니다.

## <a name="next-steps"></a>다음 단계

Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.

* [이벤트 허브 개요](event-hubs-what-is-event-hubs.md)
* [이벤트 허브 만들기](event-hubs-create.md)

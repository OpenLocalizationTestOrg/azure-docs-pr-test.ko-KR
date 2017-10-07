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
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="1a96d-103">Azure Event Hubs 처리량 단위 자동 확장</span><span class="sxs-lookup"><span data-stu-id="1a96d-103">Automatically scale up Azure Event Hubs throughput units</span></span>

## <a name="overview"></a><span data-ttu-id="1a96d-104">개요</span><span class="sxs-lookup"><span data-stu-id="1a96d-104">Overview</span></span>

<span data-ttu-id="1a96d-105">Azure Event Hubs는 확장성이 뛰어난 데이터 스트리밍 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-105">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="1a96d-106">따라서 이벤트 허브 고객 온 보 딩 toohello 서비스 보다 나중의 용도 종종 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-106">As such, Event Hubs customers often increase their usage after onboarding toohello service.</span></span> <span data-ttu-id="1a96d-107">이러한 증가 증가 함에 따라 미리 결정 된 hello 처리량 단위 (TUs) tooscale 이벤트 허브 필요 하 고 전송 속도 더 큰 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-107">Such increases require increasing hello predetermined throughput units (TUs) tooscale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="1a96d-108">hello *자동 확장할* hello 수가 TUs toomeet 사용 해야 하는 이벤트 허브의 기능이 자동으로 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-108">hello *Auto-inflate* feature of Event Hubs automatically scales up hello number of TUs toomeet usage needs.</span></span> <span data-ttu-id="1a96d-109">TU를 늘리면 다음 경우에 제한 시나리오를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-109">Increasing TUs prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="1a96d-110">데이터 수신 속도가 설정된 TU를 초과하는 경우</span><span class="sxs-lookup"><span data-stu-id="1a96d-110">Data ingress rates exceed set TUs.</span></span>
* <span data-ttu-id="1a96d-111">데이터 송신 요청 속도가 설정된 TU를 초과하는 경우</span><span class="sxs-lookup"><span data-stu-id="1a96d-111">Data egress request rates exceed set TUs.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="1a96d-112">자동 확장 작동 방식</span><span class="sxs-lookup"><span data-stu-id="1a96d-112">How Auto-inflate works</span></span>

<span data-ttu-id="1a96d-113">Event Hubs 트래픽은 처리량 단위로 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-113">Event Hubs traffic is controlled by throughput units.</span></span> <span data-ttu-id="1a96d-114">단일 TU는 초당 1MB의 수신을 허용하고 송신량은 그 두 배입니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-114">A single TU allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="1a96d-115">Standard Event Hubs는 처리량 단위를 1-20으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-115">Standard Event Hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="1a96d-116">자동 확장할 toostart를 hello 필요한 최소 처리량 단위 여 작은 항목부터 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-116">Auto-inflate enables you toostart small with hello minimum required throughput units.</span></span> <span data-ttu-id="1a96d-117">hello 기능 toohello 최대 한도 사용자 트래픽의 hello 증가 따라 필요한 처리량 단위 자동으로 다음 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-117">hello feature then scales automatically toohello maximum limit of throughput units you need, depending on hello increase in your traffic.</span></span> <span data-ttu-id="1a96d-118">자동 확장할 hello를 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-118">Auto-inflate provides hello following benefits:</span></span>

- <span data-ttu-id="1a96d-119">크기 조정 메커니즘의 효율적인 toostart 작은 및 스케일 업 때 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-119">An efficient scaling mechanism toostart small and scale up as you grow.</span></span>
- <span data-ttu-id="1a96d-120">Toohello 조정 문제 없이 지정 된 최대 제한 크기를 자동으로 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-120">Automatically scale toohello specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="1a96d-121">상세하게 제어할 배율 시기를 제어 하는 대로 및 얼마나 tooscale 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-121">More control over scaling, as you control when and how much tooscale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="1a96d-122">네임스페이스에서 자동 확장 사용</span><span class="sxs-lookup"><span data-stu-id="1a96d-122">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="1a96d-123">자동 확장할 hello 메서드를 다음 중 하나를 사용 하 여 네임 스페이스에서 사용 하지 않도록 하거나 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-123">You can enable or disable Auto-inflate on a namespace using either of hello following methods:</span></span>

1. <span data-ttu-id="1a96d-124">hello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-124">hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1a96d-125">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="1a96d-125">An Azure Resource Manager template.</span></span>

### <a name="enable-auto-inflate-through-hello-portal"></a><span data-ttu-id="1a96d-126">자동 확장할 hello 포털을 통해 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="1a96d-126">Enable Auto-inflate through hello portal</span></span>

<span data-ttu-id="1a96d-127">Hello 자동 확장할 기능 네임 스페이스에는 이벤트 허브 네임 스페이스를 만들 때 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-127">You can enable hello Auto-inflate feature on a namespace when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="1a96d-128">이 옵션을 사용하도록 설정하면 작은 처리량 단위부터 시작하여 필요한 사용량 증가에 따라 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-128">With this option enabled, you can start small on your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="1a96d-129">hello 확장에 대 한 상한값 없이 가격, hello TUs 시간당 사용 되는 다양 한에 종속 되 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-129">hello upper limit for inflation does not affect pricing, which depends on hello number of TUs used per hour.</span></span>

<span data-ttu-id="1a96d-130">또한 자동 확장할을 사용할 수 있습니다 hello를 사용 하 여 **배율** hello 포털의 설정 블레이드에서 hello 옵션:</span><span class="sxs-lookup"><span data-stu-id="1a96d-130">You can also enable Auto-inflate using hello **Scale** option on hello settings blade in hello portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="1a96d-131">Azure Resource Manager 템플릿을 사용하여 자동 확장 사용</span><span class="sxs-lookup"><span data-stu-id="1a96d-131">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="1a96d-132">Azure Resource Manager 템플릿을 배포하는 동안 자동 확장을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-132">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="1a96d-133">예를 들어 집합 hello `isAutoInflateEnabled` 속성 너무**true** 설정 `maximumThroughputUnits` too10 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-133">For example, set hello `isAutoInflateEnabled` property too**true** and set `maximumThroughputUnits` too10.</span></span>

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

<span data-ttu-id="1a96d-134">Hello 전체 서식 파일에 대 한 참조 hello [만들 이벤트 허브 네임 스페이스를 사용 하도록 설정한 확장할](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) GitHub에서 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-134">For hello complete template, see hello [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a96d-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1a96d-135">Next steps</span></span>

<span data-ttu-id="1a96d-136">Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a96d-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="1a96d-137">이벤트 허브 개요</span><span class="sxs-lookup"><span data-stu-id="1a96d-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="1a96d-138">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="1a96d-138">Create an Event Hub</span></span>](event-hubs-create.md)

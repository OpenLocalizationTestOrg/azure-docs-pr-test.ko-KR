---
title: "Azure Event Hubs 처리량 단위 자동 확장 | Microsoft Docs"
description: "처리량 단위를 자동으로 확장할 네임스페이스에서 자동 확장 사용"
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
ms.openlocfilehash: b085091ea7bfd601efb0eee84144ddd091422d6e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="74cd0-103">Azure Event Hubs 처리량 단위 자동 확장</span><span class="sxs-lookup"><span data-stu-id="74cd0-103">Automatically scale up Azure Event Hubs throughput units</span></span>

## <a name="overview"></a><span data-ttu-id="74cd0-104">개요</span><span class="sxs-lookup"><span data-stu-id="74cd0-104">Overview</span></span>

<span data-ttu-id="74cd0-105">Azure Event Hubs는 확장성이 뛰어난 데이터 스트리밍 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-105">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="74cd0-106">따라서 Event Hubs 고객은 서비스에 온보딩한 후 사용량을 늘리는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-106">As such, Event Hubs customers often increase their usage after onboarding to the service.</span></span> <span data-ttu-id="74cd0-107">그러려면 Event Hubs의 크기를 조정하고 더 빠른 전송 속도를 처리할 수 있도록 미리 지정된 TU(처리량 단위)를 늘려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-107">Such increases require increasing the predetermined throughput units (TUs) to scale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="74cd0-108">Event Hubs의 *자동 확장* 기능은 필요한 사용량에 맞게 TU 수를 자동으로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-108">The *Auto-inflate* feature of Event Hubs automatically scales up the number of TUs to meet usage needs.</span></span> <span data-ttu-id="74cd0-109">TU를 늘리면 다음 경우에 제한 시나리오를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-109">Increasing TUs prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="74cd0-110">데이터 수신 속도가 설정된 TU를 초과하는 경우</span><span class="sxs-lookup"><span data-stu-id="74cd0-110">Data ingress rates exceed set TUs.</span></span>
* <span data-ttu-id="74cd0-111">데이터 송신 요청 속도가 설정된 TU를 초과하는 경우</span><span class="sxs-lookup"><span data-stu-id="74cd0-111">Data egress request rates exceed set TUs.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="74cd0-112">자동 확장 작동 방식</span><span class="sxs-lookup"><span data-stu-id="74cd0-112">How Auto-inflate works</span></span>

<span data-ttu-id="74cd0-113">Event Hubs 트래픽은 처리량 단위로 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-113">Event Hubs traffic is controlled by throughput units.</span></span> <span data-ttu-id="74cd0-114">단일 TU는 초당 1MB의 수신을 허용하고 송신량은 그 두 배입니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-114">A single TU allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="74cd0-115">Standard Event Hubs는 처리량 단위를 1-20으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-115">Standard Event Hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="74cd0-116">자동 확장 기능을 사용하면 필요한 최소 처리량 단위의 작은 규모부터 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-116">Auto-inflate enables you to start small with the minimum required throughput units.</span></span> <span data-ttu-id="74cd0-117">그런 다음 트래픽 증가에 따라 필요한 처리량 단위의 최대 한도까지 자동으로 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-117">The feature then scales automatically to the maximum limit of throughput units you need, depending on the increase in your traffic.</span></span> <span data-ttu-id="74cd0-118">자동 확장의 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-118">Auto-inflate provides the following benefits:</span></span>

- <span data-ttu-id="74cd0-119">작은 규모부터 시작하여 사용량 증가에 따라 확장하는 효율적인 크기 조정 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-119">An efficient scaling mechanism to start small and scale up as you grow.</span></span>
- <span data-ttu-id="74cd0-120">제한 문제 없이 지정된 상한까지 자동으로 크기 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-120">Automatically scale to the specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="74cd0-121">크기 조정의 정도나 시점을 제어할 때 크기 조정을 더 잘 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-121">More control over scaling, as you control when and how much to scale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="74cd0-122">네임스페이스에서 자동 확장 사용</span><span class="sxs-lookup"><span data-stu-id="74cd0-122">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="74cd0-123">다음 방법 중 하나를 사용하여 네임스페이스에서 자동 확장을 사용 또는 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-123">You can enable or disable Auto-inflate on a namespace using either of the following methods:</span></span>

1. <span data-ttu-id="74cd0-124">[Azure Portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="74cd0-124">The [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="74cd0-125">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="74cd0-125">An Azure Resource Manager template.</span></span>

### <a name="enable-auto-inflate-through-the-portal"></a><span data-ttu-id="74cd0-126">포털을 통해 자동 확장 사용</span><span class="sxs-lookup"><span data-stu-id="74cd0-126">Enable Auto-inflate through the portal</span></span>

<span data-ttu-id="74cd0-127">Event Hubs 네임스페이스를 만들 때 네임스페이스에서 자동 확장 기능을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-127">You can enable the Auto-inflate feature on a namespace when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="74cd0-128">이 옵션을 사용하도록 설정하면 작은 처리량 단위부터 시작하여 필요한 사용량 증가에 따라 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-128">With this option enabled, you can start small on your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="74cd0-129">확장 상한은 가격 책정에 영향을 미치지 않으며 가격 책정은 시간당 사용된 TU 수에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-129">The upper limit for inflation does not affect pricing, which depends on the number of TUs used per hour.</span></span>

<span data-ttu-id="74cd0-130">포털의 설정 블레이드에서 **크기 조정** 옵션을 사용하여 자동 확장을 사용하도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-130">You can also enable Auto-inflate using the **Scale** option on the settings blade in the portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="74cd0-131">Azure Resource Manager 템플릿을 사용하여 자동 확장 사용</span><span class="sxs-lookup"><span data-stu-id="74cd0-131">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="74cd0-132">Azure Resource Manager 템플릿을 배포하는 동안 자동 확장을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-132">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="74cd0-133">예를 들어 `isAutoInflateEnabled` 속성을 **true**로 설정하고 `maximumThroughputUnits`를 10으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="74cd0-133">For example, set the `isAutoInflateEnabled` property to **true** and set `maximumThroughputUnits` to 10.</span></span>

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

<span data-ttu-id="74cd0-134">전체 템플릿은 GitHub에서 [Event Hubs 네임스페이스 만들기 및 확장 사용](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) 템플릿을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74cd0-134">For the complete template, see the [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74cd0-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="74cd0-135">Next steps</span></span>

<span data-ttu-id="74cd0-136">Event Hubs에 대한 자세한 내용은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74cd0-136">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="74cd0-137">이벤트 허브 개요</span><span class="sxs-lookup"><span data-stu-id="74cd0-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="74cd0-138">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="74cd0-138">Create an Event Hub</span></span>](event-hubs-create.md)

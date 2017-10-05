---
title: "Azure IoT Hub 사용자 지정 끝점 이해 | Microsoft Docs"
description: "개발자 가이드 - 라우팅 규칙을 사용하여 장치-클라우드 메시지를 사용자 지정 끝점으로 라우팅합니다."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: a21f1c61f344f96e2e03422e41fd8c5f7f841a0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a><span data-ttu-id="ad869-103">장치-클라우드 메시지에 대해 메시지 라우팅 및 사용자 지정 끝점 사용</span><span class="sxs-lookup"><span data-stu-id="ad869-103">Use message routes and custom endpoints for device-to-cloud messages</span></span>

<span data-ttu-id="ad869-104">IoT Hub를 사용하면 메시지 속성을 기반으로 IoT Hub 서비스 지향 끝점으로 [장치-클라우드 메시지][lnk-device-to-cloud]를 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad869-104">IoT Hub enables you to route [device-to-cloud messages][lnk-device-to-cloud] to IoT Hub service-facing endpoints based on message properties.</span></span> <span data-ttu-id="ad869-105">라우팅 규칙을 사용하면 메시지를 처리하거나 추가 코드를 작성하기 위해 추가 서비스에 대한 요구 사항 없이 필요한 곳에 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad869-105">Routing rules give you the flexibility to send messages where they need to go without the need for additional services to process messages or to write additional code.</span></span> <span data-ttu-id="ad869-106">구성하는 각 라우팅 규칙에는 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad869-106">Each routing rule you configure has the following properties:</span></span>

| <span data-ttu-id="ad869-107">속성</span><span class="sxs-lookup"><span data-stu-id="ad869-107">Property</span></span>      | <span data-ttu-id="ad869-108">설명</span><span class="sxs-lookup"><span data-stu-id="ad869-108">Description</span></span> |
| ------------- | ----------- |
| <span data-ttu-id="ad869-109">**Name**</span><span class="sxs-lookup"><span data-stu-id="ad869-109">**Name**</span></span>      | <span data-ttu-id="ad869-110">규칙을 식별하는 고유한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ad869-110">The unique name that identifies the rule.</span></span> |
| <span data-ttu-id="ad869-111">**원본**</span><span class="sxs-lookup"><span data-stu-id="ad869-111">**Source**</span></span>    | <span data-ttu-id="ad869-112">처리할 데이터 스트림의 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="ad869-112">The origin of the data stream to be acted upon.</span></span> <span data-ttu-id="ad869-113">예를 들어 장치 원격 분석이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad869-113">For example, device telemetry.</span></span> |
| <span data-ttu-id="ad869-114">**Condition**</span><span class="sxs-lookup"><span data-stu-id="ad869-114">**Condition**</span></span> | <span data-ttu-id="ad869-115">메시지 헤더 및 본문에 대해 실행되고 끝점과 일치하는지 여부를 확인하는 데 사용되는 라우팅 규칙에 대한 쿼리 식입니다.</span><span class="sxs-lookup"><span data-stu-id="ad869-115">The query expression for the routing rule that is run against the message's headers and body and used to determine whether it is a match for the endpoint.</span></span> <span data-ttu-id="ad869-116">경로 조건 구성에 대한 자세한 내용은 [참조 - 장치 쌍 및 작업에 대한 쿼리 언어][lnk-devguide-query-language]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad869-116">For more information about constructing a route condition, see the [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span></span> |
| <span data-ttu-id="ad869-117">**끝점**</span><span class="sxs-lookup"><span data-stu-id="ad869-117">**Endpoint**</span></span>  | <span data-ttu-id="ad869-118">IoT Hub에서 조건과 일치하는 메시지를 보내는 끝점의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ad869-118">The name of the endpoint where IoT Hub sends messages that match the condition.</span></span> <span data-ttu-id="ad869-119">끝점은 IoT Hub와 동일한 지역에 있어야 합니다. 그렇지 않으면 지역 간 쓰기 요금이 부과될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad869-119">Endpoints should be in the same region as the IoT hub, otherwise you may be charged for cross-region writes.</span></span> |

<span data-ttu-id="ad869-120">하나의 메시지가 여러 라우팅 규칙의 조건과 일치할 수 있습니다.이 경우 IoT Hub는 일치된 각 규칙과 연결된 끝점으로 메시지를 배달합니다.</span><span class="sxs-lookup"><span data-stu-id="ad869-120">A single message may match the condition on multiple routing rules, in which case IoT Hub delivers the message to the endpoint associated with each matched rule.</span></span> <span data-ttu-id="ad869-121">또한 IoT Hub는 메시지 배달을 자동으로 중복 제거하므로 메시지가 모두 동일한 대상을 가진 여러 규칙과 일치하면 해당 대상에 한 번만 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad869-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that all have the same destination, it is only written to that destination once.</span></span>

<span data-ttu-id="ad869-122">IoT Hub에는 기본 [기본 제공 끝점][lnk-built-in]이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad869-122">An IoT hub has a default [built-in endpoint][lnk-built-in].</span></span> <span data-ttu-id="ad869-123">구독의 다른 서비스를 허브에 연결하여 메시지를 라우팅할 사용자 지정 끝점을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad869-123">You can create custom endpoints to route messages to by linking other services in your subscription to the hub.</span></span> <span data-ttu-id="ad869-124">IoT Hub는 현재 사용자 지정 끝점으로 Event Hubs, Service Bus 큐 및 Service Bus 토픽을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ad869-124">IoT Hub currently supports Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span></span>

> [!WARNING]
> <span data-ttu-id="ad869-125">**세션** 또는 **중복 검색**이 사용하도록 설정된 Service Bus 큐 및 토픽은 사용자 지정 끝점으로 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad869-125">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span></span>

<span data-ttu-id="ad869-126">IoT Hub에 사용자 지정 끝점을 만드는 방법에 대한 자세한 내용은 [IoT Hub 끝점][lnk-devguide-endpoints]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad869-126">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="ad869-127">사용자 지정 끝점에서 읽는 방법에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad869-127">For more information about reading from custom endpoints, see:</span></span>

* <span data-ttu-id="ad869-128">[Event Hubs][lnk-getstarted-eh]에서 읽기</span><span class="sxs-lookup"><span data-stu-id="ad869-128">Reading from [Event Hubs][lnk-getstarted-eh].</span></span>
* <span data-ttu-id="ad869-129">[Service Bus 큐][lnk-getstarted-queue]에서 읽기</span><span class="sxs-lookup"><span data-stu-id="ad869-129">Reading from [Service Bus queues][lnk-getstarted-queue].</span></span>
* <span data-ttu-id="ad869-130">[Service Bus 토픽][lnk-getstarted-topic]에서 읽기</span><span class="sxs-lookup"><span data-stu-id="ad869-130">Reading from [Service Bus topics][lnk-getstarted-topic].</span></span>

### <a name="next-steps"></a><span data-ttu-id="ad869-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ad869-131">Next steps</span></span>

<span data-ttu-id="ad869-132">IoT Hub 끝점에 대한 자세한 내용은 [IoT Hub 끝점][lnk-devguide-endpoints]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad869-132">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="ad869-133">라우팅 규칙을 정의하는 데 사용하는 쿼리 언어에 대한 자세한 내용은 [장치 쌍, 작업 및 메시지 라우팅을 위한 IoT Hub 쿼리 언어][lnk-devguide-query-language]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad869-133">For more information about the query language you use to define routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span></span>

<span data-ttu-id="ad869-134">[경로를 사용하여 IoT Hub 장치-클라우드 메시지 처리][lnk-d2c-tutorial] 자습서는 라우팅 규칙과 사용자 지정 끝점을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ad869-134">The [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how to use routing rules and custom endpoints.</span></span>

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md

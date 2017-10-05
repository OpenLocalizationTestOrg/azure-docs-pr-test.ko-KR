---
title: "Azure IoT Hub 기본 제공 끝점 이해 | Microsoft Docs"
description: "개발자 가이드에서는 기본 제공 이벤트 허브 호환 끝점을 사용하여 장치-클라우드 메시지를 읽는 방법을 설명합니다."
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
ms.openlocfilehash: fcc3743028e369fdc42b71887d49fb41fba2c0dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="read-device-to-cloud-messages-from-the-built-in-endpoint"></a><span data-ttu-id="04fe8-103">기본 제공 끝점에서 장치-클라우드 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="04fe8-103">Read device-to-cloud messages from the built-in endpoint</span></span>

<span data-ttu-id="04fe8-104">기본적으로 메시지는 [Event Hubs][lnk-event-hubs]와 호환되는 기본 제공 서비스 연결 끝점(**messages/events**)으로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-104">By default, messages are routed to the built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="04fe8-105">이 끝점은 현재 [AMQP][lnk-amqp] 프로토콜을 통해서만 포트 5671에 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-105">This endpoint is currently only exposed using the [AMQP][lnk-amqp] protocol on port 5671.</span></span> <span data-ttu-id="04fe8-106">IoT Hub는 다음 속성을 노출하여 기본 제공 Event Hub와 호환되는 메시징 끝점 **messages/events**를 제어할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-106">An IoT hub exposes the following properties to enable you to control the built-in Event Hub-compatible messaging endpoint **messages/events**.</span></span>

| <span data-ttu-id="04fe8-107">속성</span><span class="sxs-lookup"><span data-stu-id="04fe8-107">Property</span></span>            | <span data-ttu-id="04fe8-108">설명</span><span class="sxs-lookup"><span data-stu-id="04fe8-108">Description</span></span> |
| ------------------- | ----------- |
| <span data-ttu-id="04fe8-109">**분할 개수**</span><span class="sxs-lookup"><span data-stu-id="04fe8-109">**Partition count**</span></span> | <span data-ttu-id="04fe8-110">이 속성은 생성 시 설정하여 장치-클라우드 이벤트 수집에 대한 [파티션][lnk-event-hub-partitions] 수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-110">Set this property at creation to define the number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span></span> |
| <span data-ttu-id="04fe8-111">**보존 시간**</span><span class="sxs-lookup"><span data-stu-id="04fe8-111">**Retention time**</span></span>  | <span data-ttu-id="04fe8-112">이 속성은 IoT Hub에서 메시지를 보존할 일 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-112">This property specifies how long in days messages are retained by IoT Hub.</span></span> <span data-ttu-id="04fe8-113">기본값은 1일이지만 7일로 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-113">The default is one day, but it can be increased to seven days.</span></span> |

<span data-ttu-id="04fe8-114">또한 IoT Hub를 사용하면 기본 제공 장치-클라우드 수신 끝점에서 소비자 그룹을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-114">IoT Hub also enables you to manage consumer groups on the built-in device-to-cloud receive endpoint.</span></span>

<span data-ttu-id="04fe8-115">기본적으로 메시지 라우팅 규칙과 명시적으로 일치하지 않는 모든 메시지는 기본 제공 끝점에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-115">By default, all messages that do not explicitly match a message routing rule are written to the built-in endpoint.</span></span> <span data-ttu-id="04fe8-116">이 대체 경로를 비활성화하면 메시지 라우팅 규칙과 명시적으로 일치하지 않는 메시지는 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span></span>

<span data-ttu-id="04fe8-117">[IoT Hub 리소스 공급자 REST API][lnk-resource-provider-apis]를 통해 프로그래밍 방식으로 또는 [Azure Portal][lnk-management-portal]을 사용하여 보존 시간을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-117">You can modify the retention time, either programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or by using the [Azure portal][lnk-management-portal].</span></span>

<span data-ttu-id="04fe8-118">IoT Hub는 허브에서 수신한 장치-클라우드 메시지를 읽도록 백 엔드 서비스의 기본 제공 끝점인 **messages/events**를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-118">IoT Hub exposes the **messages/events** built-in endpoint for your back-end services to read the device-to-cloud messages received by your hub.</span></span> <span data-ttu-id="04fe8-119">이 끝점은 Event Hub와 호환되기 때문에 Event Hubs 서비스가 메시지 읽기에 대해 지원하는 모든 메커니즘을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-119">This endpoint is Event Hub-compatible, which enables you to use any of the mechanisms the Event Hubs service supports for reading messages.</span></span>

## <a name="read-from-the-built-in-endpoint"></a><span data-ttu-id="04fe8-120">기본 제공 끝점에서 읽기</span><span class="sxs-lookup"><span data-stu-id="04fe8-120">Read from the built-in endpoint</span></span>

<span data-ttu-id="04fe8-121">[.NET용 Azure Service Bus SDK][lnk-servicebus-sdk] 또는 [Event Hubs - 이벤트 프로세서 호스트][lnk-eventprocessorhost]를 사용하는 경우 적절한 권한으로 모든 IoT Hub 연결 문자열을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-121">When you use the [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or the [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with the correct permissions.</span></span> <span data-ttu-id="04fe8-122">**이벤트/메시지** 를 이벤트 허브 이름으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-122">Then use **messages/events** as the Event Hub name.</span></span>

<span data-ttu-id="04fe8-123">IoT Hub를 인식하지 않는 SDK(또는 제품 통합)를 사용하는 경우 [Azure Portal][lnk-management-portal]의 IoT Hub 설정에서 Event Hub 호환 끝점 및 Event Hub 호환 이름을 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name from the IoT Hub settings in the [Azure portal][lnk-management-portal]:</span></span>

1. <span data-ttu-id="04fe8-124">IoT Hub 블레이드에서 **끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-124">In the IoT hub blade, click **Endpoints**.</span></span>
1. <span data-ttu-id="04fe8-125">**기본 제공 끝점** 섹션에서 **이벤트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-125">In the **Built-in endpoints** section, click **Events**.</span></span> <span data-ttu-id="04fe8-126">블레이드에서는 **Event Hub 호환 끝점**, **Event Hub 호환 이름**, **파티션**, **보존 시간** 및 **소비자 그룹** 값을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-126">The blade contains the following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span></span>

    ![장치-클라우드 설정][img-eventhubcompatible]

<span data-ttu-id="04fe8-128">IoT Hub SDK에는 **끝점** 블레이드에서 보여 주듯이 IoT Hub 끝점 이름으로 **messages/events**가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-128">The IoT Hub SDK requires the IoT Hub endpoint name, which is **messages/events** as shown in the **Endpoints** blade.</span></span>

<span data-ttu-id="04fe8-129">사용 중인 SDK에 **호스트 이름** 또는 **네임스페이스** 값이 필요한 경우 **Event Hub 호환 끝점**에서 스키마를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-129">If the SDK you are using requires a **Hostname** or **Namespace** value, remove the scheme from the **Event Hub-compatible endpoint**.</span></span> <span data-ttu-id="04fe8-130">예를 들어 Event Hubs 호환 끝점이 **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**인 경우 **호스트 이름**은 **iothub-ns-myiothub-1234.servicebus.windows.net**이 되고 **네임스페이스**는 **iothub-ns-myiothub-1234**가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-130">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, the **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**, and the **Namespace** would be **iothub-ns-myiothub-1234**.</span></span>

<span data-ttu-id="04fe8-131">지정된 Event Hubs에 연결할 수 있는 **ServiceConnect** 권한이 있는 공유 액세스 정책을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-131">You can then use any shared access policy that has the **ServiceConnect** permissions to connect to the specified Event Hub.</span></span>

<span data-ttu-id="04fe8-132">이전의 정보를 사용하여 이벤트 허브 연결 문자열을 작성해야 하는 경우 다음과 같은 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-132">If you need to build an Event Hub connection string by using the previous information, use the following pattern:</span></span>

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

<span data-ttu-id="04fe8-133">IoT Hub를 노출하는 이벤트 허브와 호환 가능한 끝점으로 사용할 수 있는 SDK 및 통합에는 다음 목록의 항목이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-133">The SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes the items in the following list:</span></span>

* <span data-ttu-id="04fe8-134">[Java 이벤트 허브 클라이언트](https://github.com/hdinsight/eventhubs-client)</span><span class="sxs-lookup"><span data-stu-id="04fe8-134">[Java Event Hubs client](https://github.com/hdinsight/eventhubs-client).</span></span>
* <span data-ttu-id="04fe8-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="04fe8-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span> <span data-ttu-id="04fe8-136">GitHub의 [spout 원본](https://github.com/apache/storm/tree/master/external/storm-eventhubs) 을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-136">You can view the [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span></span>
* <span data-ttu-id="04fe8-137">[Apache Spark 통합](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md)</span><span class="sxs-lookup"><span data-stu-id="04fe8-137">[Apache Spark integration](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04fe8-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="04fe8-138">Next steps</span></span>

<span data-ttu-id="04fe8-139">IoT Hub 끝점에 대한 자세한 내용은 [IoT Hub 끝점][lnk-endpoints]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04fe8-139">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span></span>

<span data-ttu-id="04fe8-140">[시작][lnk-get-started] 자습서에서는 시뮬레이션된 장치에서 장치-클라우드 메시지를 보내고 기본 제공 끝점에서 메시지를 읽는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="04fe8-140">The [Get Started][lnk-get-started] tutorials show you how to send device-to-cloud messages from simulated devices and read the messages from the built-in endpoint.</span></span> <span data-ttu-id="04fe8-141">자세한 내용은 [경로를 사용하여 IoT Hub 장치-클라우드 메시지 처리][lnk-d2c-tutorial] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04fe8-141">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

<span data-ttu-id="04fe8-142">장치-클라우드 메시지를 사용자 지정 끝점으로 라우팅하려면 [장치-클라우드 메시지에 대해 메시지 라우팅 및 사용자 지정 끝점 사용][lnk-custom]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04fe8-142">If you want to route your device-to-cloud messages to custom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span></span>

[img-eventhubcompatible]: ./media/iot-hub-devguide-messages-read-builtin/eventhubcompatible.png

[lnk-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-management-portal]: https://portal.azure.com
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-event-hub-partitions]: ../event-hubs/event-hubs-features.md#partitions
[lnk-servicebus-sdk]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-eventprocessorhost]: http://blogs.msdn.com/b/servicebus/archive/2015/01/16/event-processor-host-best-practices-part-1.aspx
[lnk-amqp]: https://www.amqp.org/

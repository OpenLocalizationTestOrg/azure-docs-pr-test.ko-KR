---
title: "aaaUnderstand hello Azure IoT 허브에 대 한 기본 제공 끝점 | Microsoft Docs"
description: "개발자 가이드-toouse 기본 제공, 이벤트 허브 호환 끝점 태그로 장치-클라우드 메시지 hello 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 15484c1b1828151ffcae5f4a1407264374223da1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="read-device-to-cloud-messages-from-hello-built-in-endpoint"></a><span data-ttu-id="30f18-103">Hello 기본 제공 끝점에서 장치-클라우드 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="30f18-103">Read device-to-cloud messages from hello built-in endpoint</span></span>

<span data-ttu-id="30f18-104">기본적으로 메시지는 라우트된 toohello 기본 제공 서비스 연결 끝점 (**이벤트 메시지/**), 즉 호환 [이벤트 허브][lnk-event-hubs]합니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-104">By default, messages are routed toohello built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="30f18-105">데이터베이스 미러링이 끝점은 현재 hello를 사용 하 여에 노출 [AMQP] [ lnk-amqp] 포트 5671의 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-105">This endpoint is currently only exposed using hello [AMQP][lnk-amqp] protocol on port 5671.</span></span> <span data-ttu-id="30f18-106">IoT hub hello를 노출 하면 toocontrol 속성 tooenable 다음 기본 제공 이벤트 허브 호환 메시징 끝점을 hello **이벤트메시지/**합니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-106">An IoT hub exposes hello following properties tooenable you toocontrol hello built-in Event Hub-compatible messaging endpoint **messages/events**.</span></span>

| <span data-ttu-id="30f18-107">속성</span><span class="sxs-lookup"><span data-stu-id="30f18-107">Property</span></span>            | <span data-ttu-id="30f18-108">설명</span><span class="sxs-lookup"><span data-stu-id="30f18-108">Description</span></span> |
| ------------------- | ----------- |
| <span data-ttu-id="30f18-109">**분할 개수**</span><span class="sxs-lookup"><span data-stu-id="30f18-109">**Partition count**</span></span> | <span data-ttu-id="30f18-110">생성 toodefine hello 수의이 속성을 설정 [파티션을] [ lnk-event-hub-partitions] 장치-클라우드 이벤트 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-110">Set this property at creation toodefine hello number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span></span> |
| <span data-ttu-id="30f18-111">**보존 시간**</span><span class="sxs-lookup"><span data-stu-id="30f18-111">**Retention time**</span></span>  | <span data-ttu-id="30f18-112">이 속성은 IoT Hub에서 메시지를 보존할 일 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-112">This property specifies how long in days messages are retained by IoT Hub.</span></span> <span data-ttu-id="30f18-113">hello 기본값은 1 일 이지만 증가 tooseven 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-113">hello default is one day, but it can be increased tooseven days.</span></span> |

<span data-ttu-id="30f18-114">IoT Hub 사용 하면 수도 toomanage 소비자 그룹에 hello 기본 제공 장치-클라우드 끝점을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-114">IoT Hub also enables you toomanage consumer groups on hello built-in device-to-cloud receive endpoint.</span></span>

<span data-ttu-id="30f18-115">기본적으로 모든 메시지는 메시지 라우팅 규칙을 명시적으로 일치 하지 않는 기본 제공 끝점 toohello 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-115">By default, all messages that do not explicitly match a message routing rule are written toohello built-in endpoint.</span></span> <span data-ttu-id="30f18-116">이 대체 경로를 비활성화하면 메시지 라우팅 규칙과 명시적으로 일치하지 않는 메시지는 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span></span>

<span data-ttu-id="30f18-117">Hello를 통해 프로그래밍 방식으로 hello 보존 시간을 수정할 수 있습니다 [IoT 허브 리소스 공급자 REST Api][lnk-resource-provider-apis], 또는 hello를 사용 하 여 [Azure 포털] [ lnk-management-portal].</span><span class="sxs-lookup"><span data-stu-id="30f18-117">You can modify hello retention time, either programmatically through hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or by using hello [Azure portal][lnk-management-portal].</span></span>

<span data-ttu-id="30f18-118">IoT Hub 노출 hello **이벤트메시지/** 백 엔드에 대 한 기본 제공 끝점 허브에서 수신한 tooread hello 장치-클라우드 메시지를 서비스 합니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-118">IoT Hub exposes hello **messages/events** built-in endpoint for your back-end services tooread hello device-to-cloud messages received by your hub.</span></span> <span data-ttu-id="30f18-119">데이터베이스 미러링이 끝점은 이벤트 허브 호환 toouse 메시지 도착 읽기에 대 한 지원 hello 메커니즘 hello 이벤트 허브 서비스 중 하나를 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-119">This endpoint is Event Hub-compatible, which enables you toouse any of hello mechanisms hello Event Hubs service supports for reading messages.</span></span>

## <a name="read-from-hello-built-in-endpoint"></a><span data-ttu-id="30f18-120">Hello 기본 제공 끝점에서 읽기</span><span class="sxs-lookup"><span data-stu-id="30f18-120">Read from hello built-in endpoint</span></span>

<span data-ttu-id="30f18-121">Hello를 사용 하는 경우 [.NET 용 Azure 서비스 버스 SDK] [ lnk-servicebus-sdk] 또는 hello [이벤트 허브-이벤트 프로세서 호스트][lnk-eventprocessorhost], 모든 IoT 허브 연결을 사용할 수 있습니다 hello 올바른 사용 권한이 있는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-121">When you use hello [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or hello [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with hello correct permissions.</span></span> <span data-ttu-id="30f18-122">다음 사용 하 여 **이벤트메시지/** hello 이벤트 허브 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-122">Then use **messages/events** as hello Event Hub name.</span></span>

<span data-ttu-id="30f18-123">사용 하는 경우 Sdk (또는 제품 통합) IoT Hub 인식 하지 않습니다, hello의 hello IoT Hub 설정에서 이벤트 허브 호환 끝점 및 이벤트 허브 호환 이름을 검색 해야 [Azure 포털] [ lnk-management-portal]:</span><span class="sxs-lookup"><span data-stu-id="30f18-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name from hello IoT Hub settings in hello [Azure portal][lnk-management-portal]:</span></span>

1. <span data-ttu-id="30f18-124">Hello IoT 허브 블레이드에서 클릭 **끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-124">In hello IoT hub blade, click **Endpoints**.</span></span>
1. <span data-ttu-id="30f18-125">Hello에 **기본 제공 끝점** 섹션에서 클릭 **이벤트**합니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-125">In hello **Built-in endpoints** section, click **Events**.</span></span> <span data-ttu-id="30f18-126">hello 블레이드 포함 된 다음 값에는 hello: **호환 이벤트 허브 끝점**, **이벤트 허브와 호환 가능한 이름**, **파티션을**, **보존시간**, 및 **소비자 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-126">hello blade contains hello following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span></span>

    ![장치-클라우드 설정][img-eventhubcompatible]

<span data-ttu-id="30f18-128">IoT 허브 SDK hello 필요 hello IoT Hub 끝점 이름이 며, **이벤트 메시지/** hello에 나와 있는 것 처럼 **끝점** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-128">hello IoT Hub SDK requires hello IoT Hub endpoint name, which is **messages/events** as shown in hello **Endpoints** blade.</span></span>

<span data-ttu-id="30f18-129">SDK를 사용 하는 hello 요구 하는 경우는 **Hostname** 또는 **Namespace** hello에서 hello 구성표 제거, 값 **호환 이벤트 허브 끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-129">If hello SDK you are using requires a **Hostname** or **Namespace** value, remove hello scheme from hello **Event Hub-compatible endpoint**.</span></span> <span data-ttu-id="30f18-130">예를 들어 이벤트 허브 호환 끝점 **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **Hostname** 것  **iothub ns-myiothub 1234.servicebus.windows.net**, 및 hello **Namespace** 것 **ns myiothub 1234 iothub**합니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-130">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**, and hello **Namespace** would be **iothub-ns-myiothub-1234**.</span></span>

<span data-ttu-id="30f18-131">Hello에 있는 공유 액세스 정책을 사용할 수 있습니다 **ServiceConnect** 권한 tooconnect toohello 이벤트 허브를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-131">You can then use any shared access policy that has hello **ServiceConnect** permissions tooconnect toohello specified Event Hub.</span></span>

<span data-ttu-id="30f18-132">Hello 이전 정보를 사용 하 여 toobuild 이벤트 허브 연결 문자열을 원하는 경우 hello 패턴을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-132">If you need toobuild an Event Hub connection string by using hello previous information, use hello following pattern:</span></span>

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

<span data-ttu-id="30f18-133">hello Sdk 및 IoT Hub를 노출 하는 이벤트 허브 호환 끝점으로 사용할 수 있는 통합 hello 목록 다음에 hello 항목을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-133">hello SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes hello items in hello following list:</span></span>

* <span data-ttu-id="30f18-134">[Java 이벤트 허브 클라이언트](https://github.com/hdinsight/eventhubs-client)</span><span class="sxs-lookup"><span data-stu-id="30f18-134">[Java Event Hubs client](https://github.com/hdinsight/eventhubs-client).</span></span>
* <span data-ttu-id="30f18-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="30f18-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span> <span data-ttu-id="30f18-136">Hello를 볼 수 있습니다 [소스 spout](https://github.com/apache/storm/tree/master/external/storm-eventhubs) GitHub에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-136">You can view hello [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span></span>
* <span data-ttu-id="30f18-137">[Apache Spark 통합](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md)</span><span class="sxs-lookup"><span data-stu-id="30f18-137">[Apache Spark integration](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="30f18-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="30f18-138">Next steps</span></span>

<span data-ttu-id="30f18-139">IoT Hub 끝점에 대한 자세한 내용은 [IoT Hub 끝점][lnk-endpoints]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30f18-139">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span></span>

<span data-ttu-id="30f18-140">hello [시작] [ lnk-get-started] 보여 주는 자습서 toosend 장치-클라우드 메시지를이 장치를 시뮬레이션 하 고 hello 기본 제공 끝점에서 hello 메시지를 읽은 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-140">hello [Get Started][lnk-get-started] tutorials show you how toosend device-to-cloud messages from simulated devices and read hello messages from hello built-in endpoint.</span></span> <span data-ttu-id="30f18-141">자세한 정보를 얻기 위해 hello 참조 [경로 사용 하 여 프로세스 IoT Hub 장치-클라우드 메시지] [ lnk-d2c-tutorial] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-141">For more detail, see hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

<span data-ttu-id="30f18-142">사용자 장치-클라우드 메시지 toocustom 끝점 tooroute 하려는 경우, 참조 [장치-클라우드 메시지에 대 한 메시지 경로 및 사용자 지정 끝점을 사용 하 여][lnk-custom]합니다.</span><span class="sxs-lookup"><span data-stu-id="30f18-142">If you want tooroute your device-to-cloud messages toocustom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span></span>

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

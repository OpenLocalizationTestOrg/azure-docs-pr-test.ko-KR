---
title: "C용 Azure IoT 장치 SDK – IoTHubClient | Microsoft Docs"
description: "C용 Azure IoT 장치 SDK에서 IoTHubClient 라이브러리를 사용하여 IoT Hub와 통신하는 장치 앱을 만드는 방법입니다."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: 828cf2bf-999d-4b8a-8a28-c7c901629600
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: 422d89014511f0d08ba57a893570ff7b253b7bc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a><span data-ttu-id="6766c-103">C용 Azure IoT 장치 SDK – IoTHubClient에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="6766c-103">Azure IoT device SDK for C – more about IoTHubClient</span></span>
<span data-ttu-id="6766c-104">이 시리즈의 [첫 번째 문서](iot-hub-device-sdk-c-intro.md)에서는 **C용 Azure IoT 장치 SDK**에 대해 소개했습니다. 첫 번째 문서에서 SDK에 두 아키텍처 계층이 있다는 것을 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-104">The [first article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C**. That article explained that there are two architectural layers in SDK.</span></span> <span data-ttu-id="6766c-105">맨 하단은 IoT Hub와의 통신을 직접 관리하는 **IoTHubClient** 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-105">At the base is the **IoTHubClient** library which directly manages communication with IoT Hub.</span></span> <span data-ttu-id="6766c-106">직렬화 서비스를 제공하기 위해 위쪽에 구축되는 **serializer** 라이브러리도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-106">There's also the **serializer** library that builds on top of that to provide serialization services.</span></span> <span data-ttu-id="6766c-107">이 문서에서는 **IoTHubClient** 라이브러리에 대한 추가 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-107">In this article we'll provide additional detail on the **IoTHubClient** library.</span></span>

<span data-ttu-id="6766c-108">이전 문서에서는 **IoTHubClient** 라이브러리를 사용하여 이벤트를 IoT Hub로 전송하고 메시지를 수신하는 방법을 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-108">The previous article described how to use the **IoTHubClient** library to send events to IoT Hub and receive messages.</span></span> <span data-ttu-id="6766c-109">이 문서에서는 *하위 수준 API* 를 소개하여 데이터를 전송 및 수신하는 **시간**을 보다 정확하게 관리하는 방법에 대한 설명으로 논의를 확대합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-109">This article extends that discussion by explaining how to more precisely manage *when* you send and receive data, introducing you to the **lower-level APIs**.</span></span> <span data-ttu-id="6766c-110">또한 **IoTHubClient** 라이브러리의 속성 처리 기능을 사용하여 이벤트에 속성을 첨부하고 메시지에서 검색하는 방법도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-110">We'll also explain how to attach properties to events (and retrieve them from messages) using the property handling features in the **IoTHubClient** library.</span></span> <span data-ttu-id="6766c-111">마지막으로 IoT Hub에서 수신한 메시지를 처리하는 다양한 방법에 대한 추가 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-111">Finally, we'll provide additional explanation of different ways to handle messages received from IoT Hub.</span></span>

<span data-ttu-id="6766c-112">장치 자격 증명에 대한 자세한 정보 및 구성 옵션을 통해 **IoTHubClient** 의 동작을 변경하는 방법 등 몇 가지 기타 항목을 다루는 것으로 문서를 마무리합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-112">The article concludes by covering a couple of miscellaneous topics, including more about device credentials and how to change the behavior of the **IoTHubClient** through configuration options.</span></span>

<span data-ttu-id="6766c-113">이 항목을 설명하기 위해 **IoTHubClient** SDK 샘플을 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-113">We'll use the **IoTHubClient** SDK samples to explain these topics.</span></span> <span data-ttu-id="6766c-114">따라서 따라하려면 C용 Azure IoT 장치 SDK에 포함된 **iothub\_client\_sample\_http** 및 **iothub\_client\_sample\_amqp** 응용 프로그램을 참조하세요. 다음 섹션에 설명된 모든 내용은 이 샘플에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-114">If you want to follow along, see the **iothub\_client\_sample\_http** and **iothub\_client\_sample\_amqp** applications that are included in the Azure IoT device SDK for C. Everything described in the following sections is demonstrated in these samples.</span></span>

<span data-ttu-id="6766c-115">GitHub 리포지토리에서 [**C용 Azure IoT 장치 SDK**](https://github.com/Azure/azure-iot-sdk-c)를 찾고 [C API 참조](https://azure.github.io/azure-iot-sdk-c/index.html)에서 API의 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-115">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="the-lower-level-apis"></a><span data-ttu-id="6766c-116">하위 수준 API</span><span class="sxs-lookup"><span data-stu-id="6766c-116">The lower-level APIs</span></span>
<span data-ttu-id="6766c-117">이전 문서에서는 **iothub\_client\_sample\_amqp** 응용 프로그램 컨텍스트 내에 있는 **IotHubClient**의 기본적인 동작을 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-117">The previous article described the basic operation of the **IotHubClient** within the context of the **iothub\_client\_sample\_amqp** application.</span></span> <span data-ttu-id="6766c-118">예를 들어 다음 코드를 사용하여 라이브러리를 초기화하는 방법을 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-118">For example, it explained how to initialize the library using this code.</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="6766c-119">또한 다음 함수 호출을 사용하여 이벤트를 전송하는 방법도 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-119">It also described how to send events using this function call.</span></span>

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

<span data-ttu-id="6766c-120">이 문서에서는 콜백 함수를 등록하여 메시지를 수신하는 방법도 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-120">The article also described how to receive messages by registering a callback function.</span></span>

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

<span data-ttu-id="6766c-121">이 문서에서는 다음과 같은 코드를 사용하여 리소스를 확보하는 방법도 보여줬습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-121">The article also showed how to free resources using code such as the following.</span></span>

```
IoTHubClient_Destroy(iotHubClientHandle);
```

<span data-ttu-id="6766c-122">그러나 이러한 각 API에는 도우미 함수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-122">However there are companion functions to each of these APIs:</span></span>

* <span data-ttu-id="6766c-123">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="6766c-123">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="6766c-124">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="6766c-124">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="6766c-125">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="6766c-125">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="6766c-126">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="6766c-126">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="6766c-127">이러한 함수는 모두 API 이름에 "LL"을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-127">These functions all include “LL” in the API name.</span></span> <span data-ttu-id="6766c-128">그 외에, 이러한 각 함수의 매개 변수는 비-LL 해당 항목과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-128">Other than that, the parameters of each of these functions are identical to their non-LL counterparts.</span></span> <span data-ttu-id="6766c-129">그러나 이러한 함수의 동작은 한 가지 중요한 방식에서 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-129">However, the behavior of these functions is different in one important way.</span></span>

<span data-ttu-id="6766c-130">**IoTHubClient\_CreateFromConnectionString**을 호출하면 기본 라이브러리에서 백그라운드로 실행되는 새 스레드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-130">When you call **IoTHubClient\_CreateFromConnectionString**, the underlying libraries create a new thread that runs in the background.</span></span> <span data-ttu-id="6766c-131">이 스레드는 IoT Hub로 이벤트 전송 및 메시지 수신을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-131">This thread sends events to, and receives messages from, IoT Hub.</span></span> <span data-ttu-id="6766c-132">이러한 스레드는 "LL" API로 작업할 때 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-132">No such thread is created when working with the "LL" APIs.</span></span> <span data-ttu-id="6766c-133">백그라운드 스레드를 생성하면 개발자가 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-133">The creation of the background thread is a convenience to the developer.</span></span> <span data-ttu-id="6766c-134">이벤트 전송 및 IoT Hub에서 메시지 수신을 명시적으로 지정하는 것에 대해 신경 쓰지 않아도 됩니다. 백그라운드로 자동으로 이루어지기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-134">You don’t have to worry about explicitly sending events and receiving messages from IoT Hub -- it happens automatically in the background.</span></span> <span data-ttu-id="6766c-135">이와 반대로, "LL" API는 필요한 경우 IoT Hub와의 통신을 명시적으로 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-135">In contrast, the "LL" APIs give you explicit control over communication with IoT Hub, if you need it.</span></span>

<span data-ttu-id="6766c-136">이에 대한 이해를 돕기 위해 예제를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-136">To understand this better, let’s look at an example:</span></span>

<span data-ttu-id="6766c-137">**IoTHubClient\_SendEventAsync**를 호출하는 경우 실제로 수행하는 작업은 이벤트를 버퍼에 넣는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-137">When you call **IoTHubClient\_SendEventAsync**, what you're actually doing is putting the event in a buffer.</span></span> <span data-ttu-id="6766c-138">**IoTHubClient\_CreateFromConnectionString** 호출 시 생성되는 백그라운드 스레드는 이 버퍼를 지속적으로 모니터하고 여기에 포함된 모든 데이터를 IoT Hub로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-138">The background thread created when you call **IoTHubClient\_CreateFromConnectionString** continually monitors this buffer and sends any data that it contains to IoT Hub.</span></span> <span data-ttu-id="6766c-139">메인 스레드에서 다른 작업을 수행하는 동안 이 작업이 백그라운드로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-139">This happens in the background at the same time that the main thread is performing other work.</span></span>

<span data-ttu-id="6766c-140">마찬가지로 **IoTHubClient\_SetMessageCallback**을 사용하여 메시지에 대한 콜백 함수를 등록하면 사용자는 SDK를 통해, 메시지를 수신할 때 백그라운드 스레드가 메인 스레드와 별개로 콜백 함수를 호출하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-140">Similarly, when you register a callback function for messages using **IoTHubClient\_SetMessageCallback**, you're instructing the SDK to have the background thread invoke the callback function when a message is received, independent of the main thread.</span></span>

<span data-ttu-id="6766c-141">"LL" API는 백그라운드 스레드를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-141">The "LL" APIs don’t create a background thread.</span></span> <span data-ttu-id="6766c-142">대신, IoT Hub에서 데이터를 명시적으로 전송 및 수신하는 새 API를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-142">Instead, a new API must be called to explicitly send and receive data from IoT Hub.</span></span> <span data-ttu-id="6766c-143">다음 예제에 이 내용이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-143">This is demonstrated in the following example.</span></span>

<span data-ttu-id="6766c-144">SDK에 포함된 **iothub\_client\_sample\_http** 응용 프로그램은 하위 수준 API를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-144">The **iothub\_client\_sample\_http** application that’s included in the SDK demonstrates the lower-level APIs.</span></span> <span data-ttu-id="6766c-145">이 샘플에서는 다음과 같은 코드로 IoT Hub에 이벤트를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-145">In that sample, we send events to IoT Hub with code such as the following:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="6766c-146">처음 세 줄은 메시지를 작성하고 마지막 줄은 이벤트를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-146">The first three lines create the message, and the last line sends the event.</span></span> <span data-ttu-id="6766c-147">그러나 이전에 언급한 대로 이벤트를 "전송"하는 것은 데이터를 단순히 버퍼에 넣는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-147">However, as mentioned previously, "sending" the event means that the data is simply placed in a buffer.</span></span> <span data-ttu-id="6766c-148">**IoTHubClient\_LL\_SendEventAsync**를 호출할 때 네트워크에 전송되는 것은 아무 것도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-148">Nothing is transmitted on the network when we call **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="6766c-149">IoT Hub로 데이터를 실제로 수신하려면 이 예에서처럼 **IoTHubClient\_LL\_DoWork**를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-149">In order to actually ingress the data to IoT Hub, you must call **IoTHubClient\_LL\_DoWork**, as in this example:</span></span>

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="6766c-150">이 코드(**iothub\_client\_sample\_http** 응용 프로그램에 있음)는 **IoTHubClient\_LL\_DoWork**를 반복적으로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-150">This code (from the **iothub\_client\_sample\_http** application) repeatedly calls **IoTHubClient\_LL\_DoWork**.</span></span> <span data-ttu-id="6766c-151">**IoTHubClient\_LL\_DoWork**가 호출될 때마다 버퍼에서 IoT Hub로 몇 개의 이벤트가 전송되고 장치로 전송된 대기 중인 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-151">Each time **IoTHubClient\_LL\_DoWork** is called, it sends some events from the buffer to IoT Hub and it retrieves a queued message being sent to the device.</span></span> <span data-ttu-id="6766c-152">후자의 경우 메시지에 대한 콜백 함수를 등록한 후 콜백을 호출했음을 의미합니다(모든 메시지가 대기 상태임을 가정).</span><span class="sxs-lookup"><span data-stu-id="6766c-152">The latter case means that if we registered a callback function for messages, then the callback is invoked (assuming any messages are queued up).</span></span> <span data-ttu-id="6766c-153">다음과 같은 코드로 이러한 콜백 함수를 등록했습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-153">We would have registered such a callback function with code such as the following:</span></span>

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

<span data-ttu-id="6766c-154">루프에서 **IoTHubClient\_LL\_DoWork**를 자주 호출하는 이유는 호출할 때마다 *일부* 버퍼링된 이벤트를 IoT Hub로 전송하고 장치에 대해 대기 상태인 *다음* 메시지를 가져오기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-154">The reason that **IoTHubClient\_LL\_DoWork** is often called in a loop is that each time it’s called, it sends *some* buffered events to IoT Hub and retrieves *the next* message queued up for the device.</span></span> <span data-ttu-id="6766c-155">호출 시마다 버퍼링된 모든 이벤트를 전송하거나 대기 상태인 모든 메시지를 가져온다고 보장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-155">Each call isn’t guaranteed to send all buffered events or to retrieve all queued messages.</span></span> <span data-ttu-id="6766c-156">버퍼의 모든 이벤트를 전송한 후 다른 처리를 진행하려면 다음과 같은 코드로 이 루프를 바꾸면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-156">If you want to send all events in the buffer and then continue on with other processing you can replace this loop with code such as the following:</span></span>

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="6766c-157">이 코드는 버퍼의 모든 이벤트가 IoT Hub로 전송될 때까지 **IoTHubClient\_LL\_DoWork**를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-157">This code calls **IoTHubClient\_LL\_DoWork** until all events in the buffer have been sent to IoT Hub.</span></span> <span data-ttu-id="6766c-158">이 또한 대기 상태인 모든 메시지를 수신함을 의미하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-158">Note this does not also imply that all queued messages have been received.</span></span> <span data-ttu-id="6766c-159">이것은 "모든" 메시지를 확인하는 것으로 동작이 결정되는 것은 아니기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-159">Part of the reason for this is that checking for "all" messages isn’t as deterministic an action.</span></span> <span data-ttu-id="6766c-160">가령, "모든" 메시지를 가져온 직후 장치에 다른 메시지가 전송된다면 어떻게 될까요?</span><span class="sxs-lookup"><span data-stu-id="6766c-160">What happens if you retrieve "all" of the messages, but then another one is sent to the device immediately after?</span></span> <span data-ttu-id="6766c-161">이를 처리하기 위한 더 나은 방법은 프로그래밍 방식의 시간 제한을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-161">A better way to deal with that is with a programmed timeout.</span></span> <span data-ttu-id="6766c-162">예를 들어, 메시지 콜백 함수가 호출될 때마다 타이머를 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-162">For example, the message callback function could reset a timer every time it’s invoked.</span></span> <span data-ttu-id="6766c-163">그런 다음 예를 들어, 마지막 *X* 초에 수신된 메시지가 없으면 처리를 진행하는 논리를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-163">You can then write logic to continue processing if, for example, no messages have been received in the last *X* seconds.</span></span>

<span data-ttu-id="6766c-164">이벤트 수신 및 메시지 수신을 완료했으면 해당 함수를 호출하여 리소스를 정리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-164">When you’re finished ingressing events and receiving messages, be sure to call the corresponding function to clean up resources.</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="6766c-165">기본적으로 백그라운드 스레드로 데이터를 전송 및 수신하는 API 집합이 하나만 있으며 백그라운드 스레드 없이 동일한 작업을 수행하는 API 집합도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-165">Basically there’s only one set of APIs to send and receive data with a background thread and another set of APIs that does the same thing without the background thread.</span></span> <span data-ttu-id="6766c-166">많은 개발자들이 비-LL API를 선호하지만, 개발자가 네트워크 전송을 명시적으로 제어하고자 하는 경우에는 하위 수준 API가 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-166">A lot of developers may prefer the non-LL APIs, but the lower-level APIs are useful when the developer wants explicit control over network transmissions.</span></span> <span data-ttu-id="6766c-167">예를 들어, 일부 장치에서 시간에 따라 데이터를 수집하고 지정된 간격(예: 1시간에 한 번, 하루에 한 번)으로만 이벤트를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-167">For example, some devices collect data over time and only ingress events at specified intervals (for example, once an hour or once a day).</span></span> <span data-ttu-id="6766c-168">하위 수준 API는 IoT Hub에서 데이터 전송 및 수신 시 명시적으로 제어하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-168">The lower-level APIs give you the ability to explicitly control when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="6766c-169">하위 수준 API가 제공하는 단순성만을 선호하는 사람도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-169">Others will simply prefer the simplicity that the lower-level APIs provide.</span></span> <span data-ttu-id="6766c-170">일부 작업이 백그라운드로 수행되지 않고 모두 메인 스레드에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-170">Everything happens on the main thread rather than some work happening in the background.</span></span>

<span data-ttu-id="6766c-171">어떤 모델을 선택하든 사용하는 API와 일관되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-171">Whichever model you choose, be sure to be consistent in which APIs you use.</span></span> <span data-ttu-id="6766c-172">**IoTHubClient\_LL\_CreateFromConnectionString**을 호출하여 시작하는 경우 후속 작업에 해당하는 하위 수준 API만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-172">If you start by calling **IoTHubClient\_LL\_CreateFromConnectionString**, be sure you only use the corresponding lower-level APIs for any follow-up work:</span></span>

* <span data-ttu-id="6766c-173">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="6766c-173">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="6766c-174">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="6766c-174">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="6766c-175">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="6766c-175">IoTHubClient\_LL\_Destroy</span></span>
* <span data-ttu-id="6766c-176">IoTHubClient\_LL\_DoWork</span><span class="sxs-lookup"><span data-stu-id="6766c-176">IoTHubClient\_LL\_DoWork</span></span>

<span data-ttu-id="6766c-177">반대의 경우도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-177">The opposite is true as well.</span></span> <span data-ttu-id="6766c-178">**IoTHubClient\_CreateFromConnectionString**으로 시작한 후 비-LL API를 사용하여 추가 처리를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-178">If you start with **IoTHubClient\_CreateFromConnectionString**, then use the non-LL APIs for any additional processing.</span></span>

<span data-ttu-id="6766c-179">C용 Azure IoT 장치 SDK에서 하위 수준 API에 대한 전체 예제는 **iothub\_client\_sample\_http** 응용 프로그램을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6766c-179">In the Azure IoT device SDK for C, see the **iothub\_client\_sample\_http** application for a complete example of the lower-level APIs.</span></span> <span data-ttu-id="6766c-180">비-LL API의 전체 예제는 **iothub\_client\_sample\_amqp** 응용 프로그램을 참조하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-180">The **iothub\_client\_sample\_amqp** application can be referenced for a full example of the non-LL APIs.</span></span>

## <a name="property-handling"></a><span data-ttu-id="6766c-181">속성 처리</span><span class="sxs-lookup"><span data-stu-id="6766c-181">Property handling</span></span>
<span data-ttu-id="6766c-182">지금까지 데이터 전송에 대해 설명할 때 메시지 본문을 참조했습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-182">So far when we've described sending data, we've been referring to the body of the message.</span></span> <span data-ttu-id="6766c-183">다음 코드를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-183">For example, consider this code:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="6766c-184">이 예에서는 "Hello World"라는 텍스트와 함께 IoT Hub에 메시지를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-184">This example sends a message to IoT Hub with the text "Hello World."</span></span> <span data-ttu-id="6766c-185">그리고 IoT Hub는 각 메시지에 속성을 첨부할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-185">However, IoT Hub also allows properties to be attached to each message.</span></span> <span data-ttu-id="6766c-186">속성은 메시지에 첨부할 수 있는 이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-186">Properties are name/value pairs that can be attached to the message.</span></span> <span data-ttu-id="6766c-187">예를 들어, 메시지에 속성을 추가하도록 이전 코드를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-187">For example, we can modify the previous code to attach a property to the message:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="6766c-188">**IoTHubMessage\_Properties**를 호출하고 메시지의 핸들을 전달하는 것으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-188">We start by calling **IoTHubMessage\_Properties** and passing it the handle of our message.</span></span> <span data-ttu-id="6766c-189">다음으로 볼 것은 속성 추가를 시작할 수 있는 **MAP\_HANDLE** 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-189">What we get back is a **MAP\_HANDLE** reference that enables us to start adding properties.</span></span> <span data-ttu-id="6766c-190">후자는 MAP\_HANDLE에 대한 참조, 속성 이름 및 속성 값을 사용하는 **Map\_AddOrUpdate**를 호출하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-190">The latter is accomplished by calling **Map\_AddOrUpdate**, which takes a reference to a MAP\_HANDLE, the property name, and the property value.</span></span> <span data-ttu-id="6766c-191">이 API를 통해 속성을 원하는 만큼 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-191">With this API we can add as many properties as we like.</span></span>

<span data-ttu-id="6766c-192">**Event Hubs**에서 이벤트를 읽을 때 수신기는 속성을 열거하고 해당 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-192">When the event is read from **Event Hubs**, the receiver can enumerate the properties and retrieve their corresponding values.</span></span> <span data-ttu-id="6766c-193">예를 들어, .NET에서는 [EventData 개체의 속성 컬렉션](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx)에 액세스하여 이를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-193">For example, in .NET this would be accomplished by accessing the [Properties collection on the EventData object](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).</span></span>

<span data-ttu-id="6766c-194">이전 예에서 IoT Hub로 전송하는 이벤트에 속성을 첨부합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-194">In the previous example, we’re attaching properties to an event that we send to IoT Hub.</span></span> <span data-ttu-id="6766c-195">IoT Hub에서 수신한 메시지에도 속성을 첨부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-195">Properties can also be attached to messages received from IoT Hub.</span></span> <span data-ttu-id="6766c-196">메시지에서 속성을 가져오려면 메시지 콜백 함수에 다음과 같은 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-196">If we want to retrieve properties from a message, we can use code such as the following in our message callback function:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from the message
    MAP_HANDLE mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                printf("Message Properties:\r\n");
                for (size_t index = 0; index < propertyCount; index++)
                {
                    printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                printf("\r\n");
            }
        }
    }

    . . .
}
```

<span data-ttu-id="6766c-197">**IoTHubMessage\_Properties**를 호출하면 **MAP\_HANDLE** 참조를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-197">The call to **IoTHubMessage\_Properties** returns the **MAP\_HANDLE** reference.</span></span> <span data-ttu-id="6766c-198">그런 다음 **Map\_GetInternals**로 참조를 전달하여 이름/값 쌍의 배열에 대한 참조를 얻습니다(속성 개수 포함).</span><span class="sxs-lookup"><span data-stu-id="6766c-198">We then pass that reference to **Map\_GetInternals** to obtain a reference to an array of the name/value pairs (as well as a count of the properties).</span></span> <span data-ttu-id="6766c-199">이 때 속성을 열거하여 원하는 값을 얻는 것은 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-199">At that point it's a simple matter of enumerating the properties to get to the values we want.</span></span>

<span data-ttu-id="6766c-200">응용 프로그램에서 속성을 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-200">You don't have to use properties in your application.</span></span> <span data-ttu-id="6766c-201">하지만 이벤트에 속성을 설정하거나 메시지에서 속성을 가져와야 하는 경우 **IoTHubClient** 라이브러리로 쉽게 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-201">However, if you need to set them on events or retrieve them from messages, the **IoTHubClient** library makes it easy.</span></span>

## <a name="message-handling"></a><span data-ttu-id="6766c-202">메시지 처리</span><span class="sxs-lookup"><span data-stu-id="6766c-202">Message handling</span></span>
<span data-ttu-id="6766c-203">앞서 설명한 것처럼 IoT Hub에서 메시지가 도착할 때 **IoTHubClient** 라이브러리가 등록된 콜백 함수를 호출하여 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-203">As stated previously, when messages arrive from IoT Hub the **IoTHubClient** library responds by invoking a registered callback function.</span></span> <span data-ttu-id="6766c-204">이 함수에는 반환 매개 변수가 있으며 이에 대한 추가 설명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-204">There is a return parameter of this function that deserves some additional explanation.</span></span> <span data-ttu-id="6766c-205">다음은 **iothub\_client\_sample\_http** 응용 프로그램 예제에 있는 콜백 함수를 발췌한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-205">Here’s an excerpt of the callback function in the **iothub\_client\_sample\_http** sample application:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="6766c-206">반환 형식은 **IOTHUBMESSAGE\_DISPOSITION\_RESULT**이며 이 특수한 경우에서는 **IOTHUBMESSAGE\_ACCEPTED**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-206">Note that the return type is **IOTHUBMESSAGE\_DISPOSITION\_RESULT** and in this particular case we return **IOTHUBMESSAGE\_ACCEPTED**.</span></span> <span data-ttu-id="6766c-207">이 함수에서 다른 값을 반환할 수 있으며 이 값으로 **IoTHubClient** 라이브러리가 메시지 콜백에 반응하는 방식을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-207">There are other values we can return from this function that change how the **IoTHubClient** library reacts to the message callback.</span></span> <span data-ttu-id="6766c-208">옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-208">Here are the options.</span></span>

* <span data-ttu-id="6766c-209">**IOTHUBMESSAGE\_ACCEPTED** – 메시지가 성공적으로 처리되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-209">**IOTHUBMESSAGE\_ACCEPTED** – The message has been processed successfully.</span></span> <span data-ttu-id="6766c-210">**IoTHubClient** 라이브러리가 동일한 메시지로 콜백 함수를 다시 호출하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-210">The **IoTHubClient** library will not invoke the callback function again with the same message.</span></span>
* <span data-ttu-id="6766c-211">**IOTHUBMESSAGE\_REJECTED** – 메시지가 처리되지 않았으며 나중에도 처리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-211">**IOTHUBMESSAGE\_REJECTED** – The message was not processed and there is no desire to do so in the future.</span></span> <span data-ttu-id="6766c-212">**IoTHubClient** 라이브러리는 같은 메시지로 콜백 함수를 다시 호출하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-212">The **IoTHubClient** library should not invoke the callback function again with the same message.</span></span>
* <span data-ttu-id="6766c-213">**IOTHUBMESSAGE\_ABANDONED** – 메시지가 성공적으로 처리되지 않았지만 **IoTHubClient** 라이브러리는 같은 메시지로 콜백 함수를 다시 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-213">**IOTHUBMESSAGE\_ABANDONED** – The message was not processed successfully, but the **IoTHubClient** library should invoke the callback function again with the same message.</span></span>

<span data-ttu-id="6766c-214">처음 두 반환 코드에서 **IoTHubClient** 라이브러리는 IoT Hub에 메시지를 전송하며 해당 메시지를 장치의 큐에서 삭제하고 다시 전달하지 않아야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-214">For the first two return codes, the **IoTHubClient** library sends a message to IoT Hub indicating that the message should be deleted from the device queue and not delivered again.</span></span> <span data-ttu-id="6766c-215">최종 결과는 동일하지만(장치의 큐에서 메시지가 삭제됨) 메시지를 수락 또는 거부할지 여부는 계속 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-215">The net effect is the same (the message is deleted from the device queue), but whether the message was accepted or rejected is still recorded.</span></span>  <span data-ttu-id="6766c-216">이러한 구분을 기록하는 것은 피드백을 수신 대기하고 장치가 특정 메시지를 수락 또는 거부했는지를 파악하는 메시지 보낸 사람에게 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-216">Recording this distinction is useful to senders of the message who can listen for feedback and find out if a device has accepted or rejected a particular message.</span></span>

<span data-ttu-id="6766c-217">마지막 경우에서 메시지는 IoT Hub로 전송되지만 메시지를 다시 전달해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-217">In the last case a message is also sent to IoT Hub, but it indicates that the message should be redelivered.</span></span> <span data-ttu-id="6766c-218">일반적으로 일부 오류가 발생하지만 메시지를 다시 처리하려는 경우 메시지를 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-218">Typically you’ll abandon a message if you encounter some error but want to try to process the message again.</span></span> <span data-ttu-id="6766c-219">이와 반대로, 복구할 수 없는 메시지가 발생하는 메시지를 거부하는 것이 적합합니다(또는 메시지를 처리하지 않기로 결정한 경우).</span><span class="sxs-lookup"><span data-stu-id="6766c-219">In contrast, rejecting a message is appropriate when you encounter an unrecoverable error (or if you simply decide you don’t want to process the message).</span></span>

<span data-ttu-id="6766c-220">어떤 경우든 다양한 반환 코드를 파악하여 **IoTHubClient** 라이브러리에서 원하는 동작을 유도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-220">In any case, be aware of the different return codes so that you can elicit the behavior you want from the **IoTHubClient** library.</span></span>

## <a name="alternate-device-credentials"></a><span data-ttu-id="6766c-221">대체 장치 자격 증명</span><span class="sxs-lookup"><span data-stu-id="6766c-221">Alternate device credentials</span></span>
<span data-ttu-id="6766c-222">이전에 설명한 것처럼 **IoTHubClient** 라이브러리로 작업할 때 가장 먼저 할 일은 다음과 같은 호출로 **IOTHUB\_CLIENT\_HANDLE**을 얻는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-222">As explained previously, the first thing to do when working with the **IoTHubClient** library is to obtain a **IOTHUB\_CLIENT\_HANDLE** with a call such as the following:</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="6766c-223">**IoTHubClient\_CreateFromConnectionString** 인수는 IoT Hub와 통신하는 데 사용할 프로토콜을 나타내는 장치 연결 문자열 및 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-223">The arguments to **IoTHubClient\_CreateFromConnectionString** are the device connection string and a parameter that indicates the protocol we use to communicate with IoT Hub.</span></span> <span data-ttu-id="6766c-224">장치 연결 문자열은 다음과 같은 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-224">The device connection string has a format that appears as follows:</span></span>

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

<span data-ttu-id="6766c-225">이 문자열에는 IoT Hub 이름, IoT Hub 접미사, 장치 ID 및 공유 액세스 키의 네 가지 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-225">There are four pieces of information in this string: IoT Hub name, IoT Hub suffix, device ID, and shared access key.</span></span> <span data-ttu-id="6766c-226">Azure 포털에서 IoT Hub 인스턴스를 만들 때 IoT Hub의 정규화된 도메인 이름(FQDN)을 가져옵니다. 여기서 IoT Hub 이름(FQDN의 첫 번째 부분) 및 IoT Hub 접미사(FQDN의 나머지 부분)가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-226">You obtain the fully qualified domain name (FQDN) of an IoT hub when you create your IoT hub instance in the Azure portal — this gives you the IoT hub name (the first part of the FQDN) and the IoT hub suffix (the rest of the FQDN).</span></span> <span data-ttu-id="6766c-227">장치를 IoT Hub에 등록할 때 장치 ID 및 공유 액세스 키를 가져옵니다([이전 문서](iot-hub-device-sdk-c-intro.md)에서 설명).</span><span class="sxs-lookup"><span data-stu-id="6766c-227">You get the device ID and the shared access key when you register your device with IoT Hub (as described in the [previous article](iot-hub-device-sdk-c-intro.md)).</span></span>

<span data-ttu-id="6766c-228">**IoTHubClient\_CreateFromConnectionString**은 라이브러리를 초기화하는 한 가지 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-228">**IoTHubClient\_CreateFromConnectionString** gives you one way to initialize the library.</span></span> <span data-ttu-id="6766c-229">원하는 경우 장치 연결 문자열 대신 개별 매개 변수를 사용하여 새 **IOTHUB\_CLIENT\_HANDLE**을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-229">If you prefer, you can create a new **IOTHUB\_CLIENT\_HANDLE** by using these individual parameters rather than the device connection string.</span></span> <span data-ttu-id="6766c-230">다음 코드로 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-230">This is achieved with the following code:</span></span>

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

<span data-ttu-id="6766c-231">**IoTHubClient\_CreateFromConnectionString**과 동일하게 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-231">This accomplishes the same thing as **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="6766c-232">보다 구체적인 초기화 메서드보다 **IoTHubClient\_CreateFromConnectionString**을 사용하려는 것이 분명해 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-232">It may seem obvious that you would want to use **IoTHubClient\_CreateFromConnectionString** rather than this more verbose method of initialization.</span></span> <span data-ttu-id="6766c-233">하지만 장치를 IoT Hub에 등록할 때 연결 문자열이 아닌, 장치 ID 및 장치 키를 얻게 되는 것을 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-233">Keep in mind, however, that when you register a device in IoT Hub what you get is a device ID and device key (not a connection string).</span></span> <span data-ttu-id="6766c-234">[이전 문서](iot-hub-device-sdk-c-intro.md)에서 소개한 *장치 Explorer* SDK 도구는 **Azure IoT 서비스 SDK**의 라이브러리를 사용하여 장치 ID, 장치 키 및 IoT Hub 호스트 이름에서 장치 연결 문자열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-234">The *device explorer* SDK tool introduced in the [previous article](iot-hub-device-sdk-c-intro.md) uses libraries in the **Azure IoT service SDK** to create the device connection string from the device ID, device key, and IoT Hub host name.</span></span> <span data-ttu-id="6766c-235">따라서 **IoTHubClient\_LL\_Create**를 호출하면 연결 문자열을 생성하는 단계가 필요 없으므로 더 적합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-235">So calling **IoTHubClient\_LL\_Create** may be preferable because it saves you the step of generating a connection string.</span></span> <span data-ttu-id="6766c-236">어떤 것이든 편한 방법을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="6766c-236">Use whichever method is convenient.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="6766c-237">구성 옵션</span><span class="sxs-lookup"><span data-stu-id="6766c-237">Configuration options</span></span>
<span data-ttu-id="6766c-238">지금까지 **IoTHubClient** 라이브러리가 작동하는 방법에 대해 설명한 모든 내용은 기본 동작에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-238">So far everything described about the way the **IoTHubClient** library works reflects its default behavior.</span></span> <span data-ttu-id="6766c-239">하지만 라이브러리가 작동하는 방식을 변경하도록 설정 가능한 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-239">However, there are a few options that you can set to change how the library works.</span></span> <span data-ttu-id="6766c-240">이 작업은 **IoTHubClient\_LL\_SetOption** API를 활용하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-240">This is accomplished by leveraging the **IoTHubClient\_LL\_SetOption** API.</span></span> <span data-ttu-id="6766c-241">다음 예를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="6766c-241">Consider this example:</span></span>

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

<span data-ttu-id="6766c-242">일반적으로 사용되는 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-242">There are a couple of options that are commonly used:</span></span>

* <span data-ttu-id="6766c-243">**SetBatching**(bool) – **true**이면 IoT Hub로 전송된 데이터가 일괄 처리로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-243">**SetBatching** (bool) – If **true**, then data sent to IoT Hub is sent in batches.</span></span> <span data-ttu-id="6766c-244">**false**이면 메시지가 개별적으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-244">If **false**, then messages are sent individually.</span></span> <span data-ttu-id="6766c-245">기본값은 **false**입니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-245">The default is **false**.</span></span> <span data-ttu-id="6766c-246">참고로 **SetBatching** 옵션은 HTTP 프로토콜에만 적용되며 MQTT 또는 AMQP 프로토콜에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-246">Note that the **SetBatching** option only applies to the HTTP protocol and not to the MQTT or AMQP protocols.</span></span>
* <span data-ttu-id="6766c-247">**Timeout** (unsigned int) – 이 값은 밀리초 단위로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-247">**Timeout** (unsigned int) – This value is represented in milliseconds.</span></span> <span data-ttu-id="6766c-248">HTTP 요청을 전송하고 응답을 수신하는 경우 이 시간보다 오래 걸리면 연결이 시간 초과됩니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-248">If sending an HTTP request or receiving a response takes longer than this time, then the connection times out.</span></span>

<span data-ttu-id="6766c-249">일괄 처리 옵션은 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-249">The batching option is important.</span></span> <span data-ttu-id="6766c-250">기본적으로 라이브러리는 개별적으로 이벤트를 수신합니다(**IoTHubClient\_LL\_SendEventAsync**에 전달한 단일 이벤트).</span><span class="sxs-lookup"><span data-stu-id="6766c-250">By default, the library ingresses events individually (a single event is whatever you pass to **IoTHubClient\_LL\_SendEventAsync**).</span></span> <span data-ttu-id="6766c-251">일괄 처리 옵션이 **true**인 경우 라이브러리는 버퍼에서 가져올 수 있는 만큼 이벤트를 수집합니다(IoT Hub에서 수락하는 최대 메시지 크기까지).</span><span class="sxs-lookup"><span data-stu-id="6766c-251">If the batching option is **true**, the library collects as many events as it can from the buffer (up to the maximum message size that IoT Hub will accept).</span></span>  <span data-ttu-id="6766c-252">이벤트 일괄 처리는 단일 HTTP 호출로 IoT Hub에 전송됩니다(개별 이벤트는 JSON 배열에 번들됨).</span><span class="sxs-lookup"><span data-stu-id="6766c-252">The event batch is sent to IoT Hub in a single HTTP call (the individual events are bundled into a JSON array).</span></span> <span data-ttu-id="6766c-253">일괄 처리를 설정하면 네트워크 왕복이 감소되므로 성능상 이점이 상당합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-253">Enabling batching typically results in big performance gains since you’re reducing network round-trips.</span></span> <span data-ttu-id="6766c-254">각 개별 이벤트에 대한 헤더 집합이 아닌, 이벤트 일괄 처리가 포함된 한 집합의 HTTP 헤더를 전송하므로 대역폭도 크게 감소합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-254">It also significantly reduces bandwidth since you are sending one set of HTTP headers with an event batch rather than a set of headers for each individual event.</span></span> <span data-ttu-id="6766c-255">다른 이유가 없는 한, 일반적으로 일괄 처리를 사용하도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-255">Unless you have a specific reason to do otherwise, typically you’ll want to enable batching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6766c-256">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6766c-256">Next steps</span></span>
<span data-ttu-id="6766c-257">이 문서에서는 **C용 Azure IoT 장치 SDK**에 있는 **IoTHubClient** 라이브러리의 동작에 대해 자세히 설명했습니다. 이 정보로 **IoTHubClient** 라이브러리의 기능에 대해 제대로 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-257">This article describes in detail the behavior of the **IoTHubClient** library found in the **Azure IoT device SDK for C**. With this information, you should have a good understanding of the capabilities of the **IoTHubClient** library.</span></span> <span data-ttu-id="6766c-258">[다음 문서](iot-hub-device-sdk-c-serializer.md) 에서는 **serializer** 라이브러리에 대한 유사한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6766c-258">The [next article](iot-hub-device-sdk-c-serializer.md) provides similar detail on the **serializer** library.</span></span>

<span data-ttu-id="6766c-259">IoT Hub를 개발하는 방법에 대한 자세한 내용은 [Azure IoT SDK][lnk-sdks]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6766c-259">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="6766c-260">IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6766c-260">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="6766c-261">[Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="6766c-261">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

---
title: "경로를 사용하여 Azure IoT Hub 장치-클라우드 메시지 처리(.Net) | Microsoft Docs"
description: "다른 백 엔드 서비스에 메시지를 발송하기 위해 경로 규칙 및 사용자 지정 끝점을 사용하여 IoT Hub 장치-클라우드 메시지를 처리하는 방법을 설명합니다."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 5177bac9-722f-47ef-8a14-b201142ba4bc
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 1d2b52ea005ab520bf294efa603512c00a92ee63
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a><span data-ttu-id="c4afc-103">경로를 사용하여 IoT Hub 장치-클라우드 메시지 처리(.Net)</span><span class="sxs-lookup"><span data-stu-id="c4afc-103">Process IoT Hub device-to-cloud messages using routes (.NET)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="c4afc-104">이 자습서는 [IoT Hub 시작] 자습서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-104">This tutorial builds on the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="c4afc-105">이 자습서의 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-105">The tutorial:</span></span>

* <span data-ttu-id="c4afc-106">I라우팅 규칙을 사용하여 손쉬운 구성 기반 방식으로 장치-클라우드 메시지를 발송하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-106">Shows you how to use routing rules to dispatch device-to-cloud messages in an easy, configuration-based way.</span></span>
* <span data-ttu-id="c4afc-107">추가 처리를 위해 솔루션 백 엔드의 즉각적인 작업을 요구하는 대화형 메시지를 격리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-107">Illustrates how to isolate interactive messages that require immediate action from the solution back end for further processing.</span></span> <span data-ttu-id="c4afc-108">예를 들어 장치는 CRM 시스템으로의 티켓 삽입을 트리거하는 경보 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="c4afc-109">반면 온도 원격 분석과 같은 데이터 요소 메시지는 분석 엔진으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-109">In contrast, data-point messages, such as temperature telemetry, feed into an analytics engine.</span></span>

<span data-ttu-id="c4afc-110">이 자습서의 끝 부분에서 다음의 세 가지 .NET 콘솔 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-110">At the end of this tutorial, you run three .NET console apps:</span></span>

* <span data-ttu-id="c4afc-111">**SimulatedDevice** - [IoT Hub 시작] 자습서에서 만든 수정된 버전의 앱이며, 매초 데이터 요소 장치-클라우드 메시지를 보내고 10초마다 대화형 장치-클라우드 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-111">**SimulatedDevice**, a modified version of the app created in the [Get started with IoT Hub] tutorial sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span>
* <span data-ttu-id="c4afc-112">**ReadDeviceToCloudMessages** - 장치 앱에서 보낸 중요하지 않은 원격 분석을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-112">**ReadDeviceToCloudMessages** that displays the non-critical telemetry sent by your device app.</span></span>
* <span data-ttu-id="c4afc-113">**ReadCriticalQueue** - Service Bus 큐에서 장치 앱이 보낸 중요한 메시지를 큐에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-113">**ReadCriticalQueue** de-queues the critical messages sent by your device app from a Service Bus queue.</span></span> <span data-ttu-id="c4afc-114">이 큐는 IoT Hub에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-114">This queue is attached to the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="c4afc-115">IoT Hub는 많은 장치 플랫폼 및 언어(C, Java 및 JavaScript 포함)에 SDK를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-115">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="c4afc-116">이 자습서의 시뮬레이션된 장치를 실제 장치로 바꾸는 방법에 대해 알아보려면 [Azure IoT 개발자 센터]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4afc-116">To learn how to replace the simulated device in this tutorial with a physical device, see the [Azure IoT Developer Center].</span></span>

<span data-ttu-id="c4afc-117">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="c4afc-118">Visual Studio 2015 또는 Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c4afc-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="c4afc-119">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="c4afc-119">An active Azure account.</span></span> <br/><span data-ttu-id="c4afc-120">계정이 없는 경우 몇 분 안에 [무료 계정](https://azure.microsoft.com/free/) 을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="c4afc-121">[Azure Storage] 및 [Azure Service Bus]에 대한 기본 지식이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-121">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages"></a><span data-ttu-id="c4afc-122">대화형 메시지 전송</span><span class="sxs-lookup"><span data-stu-id="c4afc-122">Send interactive messages</span></span>

<span data-ttu-id="c4afc-123">[IoT Hub 시작] 자습서에서 만든 장치 앱을 수정하여 대화형 메시지를 가끔씩 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-123">Modify the device app you created in the [Get started with IoT Hub] tutorial to occasionally send interactive messages.</span></span>

<span data-ttu-id="c4afc-124">Visual Studio의 **SimulatedDevice** 프로젝트에서 `SendDeviceToCloudMessagesAsync` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-124">In Visual Studio, in the **SimulatedDevice** project, replace the `SendDeviceToCloudMessagesAsync` method with the following code:</span></span>

```csharp
private static async void SendDeviceToCloudMessagesAsync()
{
    double minTemperature = 20;
    double minHumidity = 60;
    Random rand = new Random();

    while (true)
    {
        double currentTemperature = minTemperature + rand.NextDouble() * 15;
        double currentHumidity = minHumidity + rand.NextDouble() * 20;

        var telemetryDataPoint = new
        {
            deviceId = "myFirstDevice",
            temperature = currentTemperature,
            humidity = currentHumidity
        };
        var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
        string levelValue;

        if (rand.NextDouble() > 0.7)
        {
            messageString = "This is a critical message";
            levelValue = "critical";
        }
        else
        {
            levelValue = "normal";
        }
        
        var message = new Message(Encoding.ASCII.GetBytes(messageString));
        message.Properties.Add("level", levelValue);
        
        await deviceClient.SendEventAsync(message);
        Console.WriteLine("{0} > Sent message: {1}", DateTime.Now, messageString);

        await Task.Delay(1000);
    }
}
```

<span data-ttu-id="c4afc-125">이 메서드는 장치에서 보낸 메시지에 `"level": "critical"` 속성을 임의로 추가합니다. 그러면 솔루션 백 엔드에 의한 즉각적인 작업을 요구하는 메시지를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-125">This method randomly adds the property `"level": "critical"` to messages sent by the device, which simulates a message that requires immediate action by the solution back-end.</span></span> <span data-ttu-id="c4afc-126">장치 앱에서 메시지 본문 대신 메시지 속성에 이 정보를 전달하므로 IoT Hub에서 메시지를 적절한 메시지 대상으로 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-126">The device app passes this information in the message properties, instead of in the message body, so that IoT Hub can route the message to the proper message destination.</span></span>

> [!NOTE]
> <span data-ttu-id="c4afc-127">메시지 속성을 사용하면 여기서 보여 주는 실행 부하 과다 경로(hot path) 예제 외에도 실행 부하 과소 경로(cold path) 처리를 포함하여 다양한 시나리오의 메시지를 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-127">You can use message properties to route messages for various scenarios including cold-path processing, in addition to the hot-path example shown here.</span></span>

> [!NOTE]
> <span data-ttu-id="c4afc-128">간단히 하기 위해 이 자습서에서는 재시도 정책을 구현하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-128">For the sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="c4afc-129">프로덕션 코드에서는 MSDN 문서 [일시적인 오류 처리]에서 제시한 대로 재시도 정책(예: 지수 백오프)을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-129">In production code, you should implement a retry policy such as exponential backoff, as suggested in the MSDN article [Transient Fault Handling].</span></span>

## <a name="route-messages-to-a-queue-in-your-iot-hub"></a><span data-ttu-id="c4afc-130">IoT Hub에서 큐에 메시지 라우팅</span><span class="sxs-lookup"><span data-stu-id="c4afc-130">Route messages to a queue in your IoT hub</span></span>

<span data-ttu-id="c4afc-131">이 섹션에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-131">In this section, you:</span></span>

* <span data-ttu-id="c4afc-132">Service Bus 큐를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-132">Create a Service Bus queue.</span></span>
* <span data-ttu-id="c4afc-133">IoT Hub에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-133">Connect it to your IoT hub.</span></span>
* <span data-ttu-id="c4afc-134">메시지의 속성 존재 여부를 기반으로 큐에 메시지를 보내도록 IoT Hub를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-134">Configure your IoT hub to send messages to the queue based on the presence of a property on the message.</span></span>

<span data-ttu-id="c4afc-135">Service Bus 큐에서 메시지를 처리하는 방법에 대한 자세한 내용은 [큐 시작][Service Bus queue]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4afc-135">For more information about how to process messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span></span>

1. <span data-ttu-id="c4afc-136">[큐 시작][Service Bus queue]에서 설명한 대로 Service Bus 큐를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-136">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span></span> <span data-ttu-id="c4afc-137">큐는 IoT Hub와 동일한 구독 및 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-137">The queue must be in the same subscription and region as your IoT hub.</span></span> <span data-ttu-id="c4afc-138">네임스페이스 및 큐 이름을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-138">Make a note of the namespace and queue name.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c4afc-139">IoT Hub으로 사용되는 Service Bus 큐 및 토픽에는 **세션** 또는 **중복 검색**이 사용하도록 설정되어 있어서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-139">Service Bus queues and topics used as IoT Hub endpoints must not have **Sessions** or **Duplicate Detection** enabled.</span></span> <span data-ttu-id="c4afc-140">두 옵션 중 하나가 사용하도록 설정되어 있으면 Azure Portal에서 끝점이 **연결할 수 없음**으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-140">If either of those options are enabled, the endpoint appears as **Unreachable** in the Azure portal.</span></span>

2. <span data-ttu-id="c4afc-141">Azure Portal에서 IoT Hub를 열고 **끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-141">In the Azure portal, open your IoT hub and click **Endpoints**.</span></span>
    
    ![IoT Hub의 끝점][30]

3. <span data-ttu-id="c4afc-143">**끝점** 블레이드 위쪽에서 **추가**를 클릭하여 IoT Hub에 큐를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-143">In the **Endpoints** blade, click **Add** at the top to add your queue to your IoT hub.</span></span> <span data-ttu-id="c4afc-144">끝점 이름을 **CriticalQueue**로 지정하고 드롭다운을 사용하여 **Service Bus 큐**, 큐가 있는 Service Bus 네임스페이스 및 큐 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-144">Name the endpoint **CriticalQueue** and use the drop-downs to select **Service Bus queue**, the Service Bus namespace in which your queue resides, and the name of your queue.</span></span> <span data-ttu-id="c4afc-145">완료되면 아래쪽의 **저장** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-145">When you are done, click **Save** at the bottom.</span></span>
    
    ![끝점 추가][31]
    
4. <span data-ttu-id="c4afc-147">이제 IoT Hub에서 **경로**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-147">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="c4afc-148">블레이드 위쪽에서 **추가**를 클릭하여 방금 추가한 큐로 메시지를 라우팅하는 라우팅 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-148">Click **Add** at the top of the blade to create a routing rule that routes messages to the queue you just added.</span></span> <span data-ttu-id="c4afc-149">데이터 원본으로 **DeviceTelemetry**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-149">Select **DeviceTelemetry** as the source of data.</span></span> <span data-ttu-id="c4afc-150">조건으로 `level="critical"`을 입력하고 방금 사용자 지정 끝점으로 추가한 큐를 경로 규칙 끝점으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-150">Enter `level="critical"` as the condition, and choose the queue you just added as a custom endpoint as the routing rule endpoint.</span></span> <span data-ttu-id="c4afc-151">완료되면 아래쪽의 **저장** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-151">When you are done, click **Save** at the bottom.</span></span>
    
    ![경로 추가][32]
    
    <span data-ttu-id="c4afc-153">대체(fallback) 경로가 **ON**으로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-153">Make sure the fallback route is set to **ON**.</span></span> <span data-ttu-id="c4afc-154">이 값은 IoT Hub에 대한 기본 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-154">This value is the default configuration for an IoT hub.</span></span>
    
    ![대체(fallback) 경로][33]

## <a name="read-from-the-queue-endpoint"></a><span data-ttu-id="c4afc-156">큐 끝점에서 읽기</span><span class="sxs-lookup"><span data-stu-id="c4afc-156">Read from the queue endpoint</span></span>

<span data-ttu-id="c4afc-157">이 섹션에서는 큐 끝점에서 메시지를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-157">In this section, you read the messages from the queue endpoint.</span></span>

1. <span data-ttu-id="c4afc-158">Visual Studio에서 **콘솔 앱(.NET Framework)** 프로젝트 템플릿을 사용하여 Visual C# Windows 클래식 바탕화면 프로젝트를 현재 솔루션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-158">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="c4afc-159">**ReadCriticalQueue** 프로젝트의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-159">Name the project **ReadCriticalQueue**.</span></span>

2. <span data-ttu-id="c4afc-160">[솔루션 탐색기]에서 **ReadCriticalQueue** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음, **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-160">In Solution Explorer, right-click the **ReadCriticalQueue** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="c4afc-161">이 작업을 수행하면 **Nuget 패키지 관리자** 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-161">This operation displays the **NuGet Package Manager** window.</span></span>

3. <span data-ttu-id="c4afc-162">**WindowsAzure.ServiceBus**를 검색하여 **설치**를 클릭하고 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-162">Search for **WindowsAzure.ServiceBus**, click **Install**, and accept the terms of use.</span></span> <span data-ttu-id="c4afc-163">이 작업을 수행하면 모든 종속성과 함께 Azure Service Bus에 대한 참조를 다운로드, 설치 및 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-163">This operation downloads, installs, and adds a reference to the Azure Service Bus, with all its dependencies.</span></span>

4. <span data-ttu-id="c4afc-164">**Program.cs** 파일의 맨 위에 다음 **using** 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-164">Add the following **using** statements at the top of the **Program.cs** file:</span></span>
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. <span data-ttu-id="c4afc-165">마지막으로 **Main** 메서드에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-165">Finally, add the following lines to the **Main** method.</span></span> <span data-ttu-id="c4afc-166">연결 문자열을 큐에 대한 **수신 대기** 권한으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-166">Substitute the connection string with **Listen** permissions for the queue:</span></span>
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C to exit.\n");
    var connectionString = "{service bus listen string}";
    var queueName = "{queue name}";
    
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);

    client.OnMessage(message =>
        {
            Stream stream = message.GetBody<Stream>();
            StreamReader reader = new StreamReader(stream, Encoding.ASCII);
            string s = reader.ReadToEnd();
            Console.WriteLine(String.Format("Message body: {0}", s));
        });
        
    Console.ReadLine();
    ```

## <a name="run-the-applications"></a><span data-ttu-id="c4afc-167">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="c4afc-167">Run the applications</span></span>
<span data-ttu-id="c4afc-168">이제 응용 프로그램을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-168">Now you are ready to run the applications.</span></span>

1. <span data-ttu-id="c4afc-169">솔루션 탐색기의 Visual Studio에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **시작 프로젝트 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-169">In Visual Studio, in Solution Explorer, right-click your solution and select **Set StartUp Projects**.</span></span> <span data-ttu-id="c4afc-170">**여러 개의 시작 프로젝트**를 선택한 다음 **ReadDeviceToCloudMessages**, **SimulatedDevice** 및 **ReadCriticalQueue** 프로젝트에 대한 작업으로 **시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-170">Select **Multiple startup projects**, then select **Start** as the action for the **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **ReadCriticalQueue** projects.</span></span>
2. <span data-ttu-id="c4afc-171">**F5** 키를 눌러 세 가지 콘솔 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-171">Press **F5** to start the three console apps.</span></span> <span data-ttu-id="c4afc-172">**ReadDeviceToCloudMessages** 앱에는 **SimulatedDevice** 응용 프로그램에서 보낸 중요하지 않은 메시지만 있고, **ReadCriticalQueue** 앱에는 중요한 메시지만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-172">The **ReadDeviceToCloudMessages** app has only non-critical messages sent from the **SimulatedDevice** application, and the **ReadCriticalQueue** app has only critical messages.</span></span>
   
   ![3개의 콘솔 앱][50]

## <a name="next-steps"></a><span data-ttu-id="c4afc-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c4afc-174">Next steps</span></span>
<span data-ttu-id="c4afc-175">이 자습서에서는 IoT Hub의 메시지 라우팅 기능을 사용하여 장치-클라우드 메시지를 안정적으로 전달하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-175">In this tutorial, you learned how to reliably dispatch device-to-cloud messages by using the message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="c4afc-176">[IoT Hub를 사용하여 클라우드-장치 메시지를 보내는 방법][lnk-c2d]에서는 솔루션 백 엔드에서 장치로 메시지를 보내는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4afc-176">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d] shows you how to send messages to your devices from your solution back end.</span></span>

<span data-ttu-id="c4afc-177">IoT Hub를 사용하는 전체 종단 간 솔루션의 예를 보려면 [Azure IoT Suite][lnk-suite]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4afc-177">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="c4afc-178">IoT Hub를 사용하여 솔루션을 개발하는 방법에 대한 자세한 내용은 [IoT Hub 개발자 가이드]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4afc-178">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<span data-ttu-id="c4afc-179">IoT Hub의 메시지 라우팅에 대한 자세한 내용은 [IoT Hub를 통해 메시지 보내고 받기][lnk-devguide-messaging]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4afc-179">To learn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
<span data-ttu-id="c4afc-180">[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/</span><span class="sxs-lookup"><span data-stu-id="c4afc-180">[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/</span></span>
<span data-ttu-id="c4afc-181">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span><span class="sxs-lookup"><span data-stu-id="c4afc-181">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span></span>
<span data-ttu-id="c4afc-182">[IoT Hub 개발자 가이드]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="c4afc-182">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="c4afc-183">[IoT Hub 시작]: iot-hub-csharp-csharp-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="c4afc-183">[Get started with IoT Hub]: iot-hub-csharp-csharp-getstarted.md</span></span>
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
<span data-ttu-id="c4afc-184">[Azure IoT 개발자 센터]: https://azure.microsoft.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="c4afc-184">[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot</span></span>
<span data-ttu-id="c4afc-185">[일시적인 오류 처리]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="c4afc-185">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/

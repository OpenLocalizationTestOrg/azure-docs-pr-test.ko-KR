---
title: "Azure IoT Hub 시작(.NET) | Microsoft Docs"
description: ".NET용 IoT SDK를 사용하여 Azure IoT Hub에 장치-클라우드 메시지를 보내는 방법을 알아봅니다. 시뮬레이션된 장치 및 서비스 앱을 만들어서 장치를 등록하고 메시지를 전송하고 IoT Hub의 메시지를 읽습니다."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: f40604ff-8fd6-4969-9e99-8574fbcf036c
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 69296eb9ac2a74a97b632d27733a6a06500b4abd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-your-device-to-your-iot-hub-using-net"></a><span data-ttu-id="30e8d-104">.NET을 사용하여 IoT Hub에 장치 연결</span><span class="sxs-lookup"><span data-stu-id="30e8d-104">Connect your device to your IoT hub using .NET</span></span>

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="30e8d-105">이 자습서의 끝 부분에서 다음의 세 가지 .NET 콘솔 앱이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-105">At the end of this tutorial, you have three .NET console apps:</span></span>

* <span data-ttu-id="30e8d-106">**CreateDeviceIdentity**는 장치 ID 및 시뮬레이션된 보안 키를 만들어 장치 앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-106">**CreateDeviceIdentity**, which creates a device identity and associated security key to connect your device app.</span></span>
* <span data-ttu-id="30e8d-107">**ReadDeviceToCloudMessages**는 장치 앱에서 보낸 원격 분석을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-107">**ReadDeviceToCloudMessages**, which displays the telemetry sent by your device app.</span></span>
* <span data-ttu-id="30e8d-108">**SimulatedDevice**는 앞에서 만든 장치 ID로 IoT Hub에 연결하고 MQTT 프로토콜을 사용하여 매초마다 원격 분석 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-108">**SimulatedDevice**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second by using the MQTT protocol.</span></span>

<span data-ttu-id="30e8d-109">Github의 세 가지 앱이 포함된 Visual Studio 솔루션을 다운로드하거나 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-109">You can download or clone the Visual Studio solution, which contains the three apps from Github.</span></span>

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> <span data-ttu-id="30e8d-110">장치와 솔루션 백 엔드에서 실행하기 위해 두 응용 프로그램을 빌드하는 데 사용할 수 있는 Azure IoT SDK에 관한 정보는 [Azure IoT SDK][lnk-hub-sdks]를 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="30e8d-110">For information about the Azure IoT SDKs that you can use to build both applications to run on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="30e8d-111">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-111">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="30e8d-112">Visual Studio 2015 또는 Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="30e8d-112">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="30e8d-113">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="30e8d-113">An active Azure account.</span></span> <span data-ttu-id="30e8d-114">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="30e8d-115">이제 IoT Hub가 만들어졌고 이 자습서 나머지 부분을 완료하는 데 필요한 호스트 이름과 IoT Hub 연결 문자열을 갖게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-115">You have now created your IoT hub, and you have the host name and IoT Hub connection string that you need to complete the rest of this tutorial.</span></span>

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="30e8d-116">장치-클라우드 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="30e8d-116">Receive device-to-cloud messages</span></span>
<span data-ttu-id="30e8d-117">이 섹션에서는 IoT Hub에서 장치-클라우드 메시지를 읽는 .NET 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-117">In this section, you create a .NET console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="30e8d-118">IoT Hub가 [Azure Event Hubs][lnk-event-hubs-overview] 호환 끝점을 노출하여 장치-클라우드 메시지를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-118">An IoT hub exposes an [Azure Event Hubs][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="30e8d-119">작업을 단순화하기 위해 이 자습서에서는 처리량이 높은 배포용이 아닌 기본적인 판독기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-119">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="30e8d-120">대량의 장치-클라우드 메시지를 처리하는 방법을 알아보려면 [장치-클라우드 메시지 처리][lnk-process-d2c-tutorial] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30e8d-120">To learn how to process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span> <span data-ttu-id="30e8d-121">Event Hubs에서 메시지를 처리하는 방법에 대한 자세한 내용은 [Event Hubs 시작][lnk-eventhubs-tutorial] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30e8d-121">For more information about how to process messages from Event Hubs, see the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span> <span data-ttu-id="30e8d-122">(이 자습서는 IoT Hub Event Hub와 호환되는 끝점에 적용할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="30e8d-122">(This tutorial is applicable to the IoT Hub Event Hub-compatible endpoints.)</span></span>

> [!NOTE]
> <span data-ttu-id="30e8d-123">장치-클라우드 메시지를 읽는 Event Hub와 호환 가능한 끝점은 항상 AMQP 프로토콜을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-123">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>

1. <span data-ttu-id="30e8d-124">Visual Studio에서 **콘솔 앱(.NET Framework)** 프로젝트 템플릿을 사용하여 Visual C# Windows 클래식 바탕화면 프로젝트를 현재 솔루션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-124">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="30e8d-125">.NET Framework 버전이 4.5.1 이상인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-125">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="30e8d-126">프로젝트 **ReadDeviceToCloudMessages**의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-126">Name the project **ReadDeviceToCloudMessages**.</span></span>

    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][10a]

2. <span data-ttu-id="30e8d-128">솔루션 탐색기에서 **ReadDeviceToCloudMessages** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-128">In Solution Explorer, right-click the **ReadDeviceToCloudMessages** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="30e8d-129">**NuGet 패키지 관리자** 창에서 **WindowsAzure.ServiceBus**를 검색하고 **설치**를 선택한 다음 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-129">In the **NuGet Package Manager** window, search for **WindowsAzure.ServiceBus**, select **Install**, and accept the terms of use.</span></span> <span data-ttu-id="30e8d-130">이 프로시저에서는 모든 종속 항목과 함께 [Azure Service Bus][lnk-servicebus-nuget]에 대한 참조를 다운로드, 설치 및 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-130">This procedure downloads, installs, and adds a reference to [Azure Service Bus][lnk-servicebus-nuget], with all its dependencies.</span></span> <span data-ttu-id="30e8d-131">이 패키지를 사용하면 응용 프로그램을 IoT Hub의 이벤트 허브와 호환되는 끝점에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-131">This package enables the application to connect to the Event Hub-compatible endpoint on your IoT hub.</span></span>

4. <span data-ttu-id="30e8d-132">**Program.cs** 파일 위에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-132">Add the following `using` statements at the top of the **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. <span data-ttu-id="30e8d-133">**Program** 클래스에 다음 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-133">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="30e8d-134">자리 표시자 값을 "IoT Hub 만들기" 섹션에서 만든 허브의 IoT Hub 연결 문자열로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-134">Replace the placeholder value with the IoT Hub connection string for the hub you created in the "Create an IoT hub" section.</span></span>

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. <span data-ttu-id="30e8d-135">**Program** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-135">Add the following method to the **Program** class:</span></span>

    ```csharp
    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested) break;
            EventData eventData = await eventHubReceiver.ReceiveAsync();
            if (eventData == null) continue;

            string data = Encoding.UTF8.GetString(eventData.GetBytes());
            Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
        }
    }
    ```

    <span data-ttu-id="30e8d-136">이 메서드는 **EventHubReceiver** 인스턴스를 사용하여 모든 IoT Hub 장치-클라우드 수신 파티션의 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-136">This method uses an **EventHubReceiver** instance to receive messages from all the IoT hub device-to-cloud receive partitions.</span></span> <span data-ttu-id="30e8d-137">시작된 후 보낸 메시지만 수신하도록 **EventHubReceiver** 개체를 만든 경우 `DateTime.Now` 매개 변수를 전달하는 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30e8d-137">Notice how you pass a `DateTime.Now` parameter when you create the **EventHubReceiver** object, so that it only receives messages sent after it starts.</span></span> <span data-ttu-id="30e8d-138">이 필터는 테스트 환경에서 현재 메시지 집합을 볼 수 있어 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-138">This filter is useful in a test environment so you can see the current set of messages.</span></span> <span data-ttu-id="30e8d-139">프로덕션 환경에서는 코드가 모든 메시지를 처리하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-139">In a production environment, your code should make sure that it processes all the messages.</span></span> <span data-ttu-id="30e8d-140">자세한 내용은 [IoT Hub 장치-클라우드 메시지 처리 방법][lnk-process-d2c-tutorial] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30e8d-140">For more information, see the tutorial [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial].</span></span>

7. <span data-ttu-id="30e8d-141">마지막으로 **Main** 메서드에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-141">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive messages. Ctrl-C to exit.\n");
    eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, iotHubD2cEndpoint);

    var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;

    CancellationTokenSource cts = new CancellationTokenSource();

    System.Console.CancelKeyPress += (s, e) =>
    {
        e.Cancel = true;
        cts.Cancel();
        Console.WriteLine("Exiting...");
    };

    var tasks = new List<Task>();
    foreach (string partition in d2cPartitions)
    {
        tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
    }  
    Task.WaitAll(tasks.ToArray());
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="30e8d-142">장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="30e8d-142">Create a device app</span></span>

<span data-ttu-id="30e8d-143">이 섹션에서는 IoT Hub로 장치-클라우드 메시지를 전송하는 장치를 시뮬레이션하는 .NET 콘솔 앱을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-143">In this section, you create a .NET console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="30e8d-144">Visual Studio에서 **콘솔 앱(.NET Framework)** 프로젝트 템플릿을 사용하여 Visual C# Windows 클래식 바탕화면 프로젝트를 현재 솔루션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-144">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="30e8d-145">.NET Framework 버전이 4.5.1 이상인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-145">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="30e8d-146">프로젝트 **SimulatedDevice**의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-146">Name the project **SimulatedDevice**.</span></span>

    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][10b]

2. <span data-ttu-id="30e8d-148">솔루션 탐색기에서 **SimulatedDevice** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음, **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-148">In Solution Explorer, right-click the **SimulatedDevice** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="30e8d-149">**NuGet 패키지 관리자** 창에서 **찾아보기**를 선택하고 **Microsoft.Azure.Devices.Client**를 검색한 다음 **설치**를 선택하여 **Microsoft.Azure.Devices.Client** 패키지를 설치하고 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-149">In the **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Client**, select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="30e8d-150">이 프로시저에서는 [Azure IoT 장치 SDK NuGet 패키지][lnk-device-nuget] 및 종속 항목에 참조를 다운로드, 설치 및 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-150">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK NuGet package][lnk-device-nuget] and its dependencies.</span></span>

4. <span data-ttu-id="30e8d-151">**Program.cs** 파일 위에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-151">Add the following `using` statement at the top of the **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. <span data-ttu-id="30e8d-152">**Program** 클래스에 다음 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-152">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="30e8d-153">`{iot hub hostname}`을(를) "IoT 허브 만들기" 섹션에서 검색한 IoT 허브 호스트 이름으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-153">Substitute `{iot hub hostname}` with the IoT hub host name you retrieved in the "Create an IoT hub" section.</span></span> <span data-ttu-id="30e8d-154">`{device key}`을(를) “장치 ID 만들기" 섹션에서 검색한 장치 키로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-154">Substitute `{device key}` with the device key you retrieved in the "Create a device identity" section.</span></span>

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. <span data-ttu-id="30e8d-155">**Program** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-155">Add the following method to the **Program** class:</span></span>

    ```csharp
    private static async void SendDeviceToCloudMessagesAsync()
    {
        double minTemperature = 20;
        double minHumidity = 60;
        int messageId = 1;
        Random rand = new Random();

        while (true)
        {
            double currentTemperature = minTemperature + rand.NextDouble() * 15;
            double currentHumidity = minHumidity + rand.NextDouble() * 20;

            var telemetryDataPoint = new
            {
                messageId = messageId++,
                deviceId = "myFirstDevice",
                temperature = currentTemperature,
                humidity = currentHumidity
            };
            var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
            var message = new Message(Encoding.ASCII.GetBytes(messageString));
            message.Properties.Add("temperatureAlert", (currentTemperature > 30) ? "true" : "false");

            await deviceClient.SendEventAsync(message);
            Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, messageString);

            await Task.Delay(1000);
        }
    }
    ```

    <span data-ttu-id="30e8d-156">이 메서드는 1초마다 새로운 장치-클라우드 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-156">This method sends a new device-to-cloud message every second.</span></span> <span data-ttu-id="30e8d-157">메시지에는 장치 ID가 있는 JSON 직렬화된 개체와 온도 센서 및 습도 센서를 시뮬레이션하기 위해 임의로 생성된 숫자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-157">The message contains a JSON-serialized object, with the device ID and randomly generated numbers to simulate a temperature sensor, and a humidity sensor.</span></span>

7. <span data-ttu-id="30e8d-158">마지막으로 **Main** 메서드에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-158">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    <span data-ttu-id="30e8d-159">기본적으로 .NET Framework 앱의 **Create** 메서드는 AMQP 프로토콜을 사용하여 IoT Hub와 통신하는 **DeviceClient** 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-159">By default, the **Create** method in a .NET Framework app creates a **DeviceClient** instance that uses the AMQP protocol to communicate with IoT Hub.</span></span> <span data-ttu-id="30e8d-160">MQTT 또는 HTTP 프로토콜을 사용하려면 프로토콜을 지정할 수 있도록 해주는 **Create** 메서드의 재정의를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-160">To use the MQTT or HTTP protocol, use the override of the **Create** method that enables you to specify the protocol.</span></span> <span data-ttu-id="30e8d-161">UWP 및 PCL 클라이언트는 기본적으로 HTTP 프로토콜을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-161">UWP and PCL clients use the HTTP protocol by default.</span></span> <span data-ttu-id="30e8d-162">HTTP 프로토콜을 사용하려면 **Microsoft.AspNet.WebApi.Client** NuGet 패키지를 프로젝트에 추가하여 **System.Net.Http.Formatting** 네임스페이스를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-162">If you use the HTTP protocol, you should also add the **Microsoft.AspNet.WebApi.Client** NuGet package to your project to include the **System.Net.Http.Formatting** namespace.</span></span>

<span data-ttu-id="30e8d-163">이 자습서에서는 IoT Hub 장치 앱을 만드는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-163">This tutorial takes you through the steps to create an IoT Hub device app.</span></span> <span data-ttu-id="30e8d-164">[Azure IoT Hub에 연결된 서비스][lnk-connected-service] Visual Studio 확장을 사용하여 장치 앱에 필요한 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-164">You can also use the [Connected Service for Azure IoT Hub][lnk-connected-service] Visual Studio extension to add the necessary code to your device app.</span></span>

> [!NOTE]
> <span data-ttu-id="30e8d-165">간단히 하기 위해 이 자습서에서는 다시 시도 정책을 구현하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-165">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="30e8d-166">프로덕션 코드에서는 MSDN 문서 [일시적인 오류 처리][lnk-transient-faults]에서 제시한 대로 다시 시도 정책(예: 지수 백오프)을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-166">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="30e8d-167">앱 실행</span><span class="sxs-lookup"><span data-stu-id="30e8d-167">Run the apps</span></span>

<span data-ttu-id="30e8d-168">이제 앱을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-168">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="30e8d-169">솔루션 탐색기의 Visual Studio에서 솔루션을 마우스 오른쪽 단추로 클릭한 다음 **시작 프로젝트로 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-169">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="30e8d-170">**여러 개의 시작 프로젝트**를 선택한 다음 **ReadDeviceToCloudMessages** 및 **SimulatedDevice** 프로젝트 모두에 대한 작업으로 **시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-170">Select **Multiple startup projects**, and then select **Start** as the action for both the **ReadDeviceToCloudMessages** and **SimulatedDevice** projects.</span></span>

    ![시작 프로젝트 속성][41]

2. <span data-ttu-id="30e8d-172">**F5**를 눌러 두 응용 프로그램 실행을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-172">Press **F5** to start both apps running.</span></span> <span data-ttu-id="30e8d-173">**SimulatedDevice** 앱의 콘솔 출력은 장치 앱에서 IoT Hub로 전송한 메시지를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-173">The console output from the **SimulatedDevice** app shows the messages your device app sends to your IoT hub.</span></span> <span data-ttu-id="30e8d-174">**ReadDeviceToCloudMessages** 앱의 콘솔 출력은 IoT Hub가 수신하는 메시지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-174">The console output from the **ReadDeviceToCloudMessages** app shows the messages that your IoT hub receives.</span></span>

    ![앱에서 콘솔 출력][42]

3. <span data-ttu-id="30e8d-176">[Azure Portal][lnk-portal]의 **사용량** 타일에 IoT Hub로 전송된 메시지 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-176">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>

    ![Azure Portal 사용량 타일][43]

## <a name="next-steps"></a><span data-ttu-id="30e8d-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="30e8d-178">Next steps</span></span>

<span data-ttu-id="30e8d-179">이 자습서에서는 Azure Portal에서 IoT Hub를 구성한 다음, IoT Hub의 ID 레지스트리에서 장치 ID를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-179">In this tutorial, you configured an IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="30e8d-180">이 장치 ID를 사용하여 장치-클라우드 메시지를 IoT Hub로 보내기 위해 장치 앱을 사용하도록 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-180">You used this device identity to enable the device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="30e8d-181">IoT Hub에서 받은 메시지를 표시하는 앱도 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="30e8d-181">You also created an app that displays the messages received by the IoT hub.</span></span>

<span data-ttu-id="30e8d-182">계속해서 IoT Hub을 시작하고 다른 IoT 시나리오를 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30e8d-182">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="30e8d-183">[장치 연결][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="30e8d-183">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="30e8d-184">[장치 관리 시작][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="30e8d-184">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="30e8d-185">[IoT Edge 시작][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="30e8d-185">[Getting started with IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="30e8d-186">IoT 솔루션을 확장하고 대량의 장치-클라우드 메시지를 처리하는 방법을 알아보려면 [장치-클라우드 메시지 처리][lnk-process-d2c-tutorial] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30e8d-186">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[41]: ./media/iot-hub-csharp-csharp-getstarted/run-apps1.png
[42]: ./media/iot-hub-csharp-csharp-getstarted/run-apps2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png
[10a]: ./media/iot-hub-csharp-csharp-getstarted/create-receive-csharp1.png
[10b]: ./media/iot-hub-csharp-csharp-getstarted/create-device-csharp1.png


<!-- Links -->
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-servicebus-nuget]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-device-nuget]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-connected-service]: https://visualstudiogallery.msdn.microsoft.com/e254a3a5-d72e-488e-9bd3-8fee8e0cd1d6
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

---
title: "aaaGet Azure IoT 허브 (.NET)를 시작 | Microsoft Docs"
description: "Toosend 장치-클라우드 tooAzure IoT Sdk를 사용 하 여.NET에 대 한 IoT Hub를 메시지 하는 방법을 알아봅니다. 시뮬레이션 된 장치 및 서비스 응용 프로그램 tooregister 장치, 메시지를 보낼 만들고 IoT 허브에서 메시지를 읽은 합니다."
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
ms.openlocfilehash: 56cf14687411898ea0fa4ebb1782e18b3930809c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a><span data-ttu-id="d40a4-104">.NET을 사용 하 여 장치 tooyour IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-104">Connect your device tooyour IoT hub using .NET</span></span>

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="d40a4-105">이 자습서의 hello 끝 세 개의.NET 콘솔 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-105">At hello end of this tutorial, you have three .NET console apps:</span></span>

* <span data-ttu-id="d40a4-106">**CreateDeviceIdentity**, 장치 id를 만드는 연결 된 보안 키 tooconnect 장치 응용 프로그램 및입니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-106">**CreateDeviceIdentity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="d40a4-107">**ReadDeviceToCloudMessages**, 장치 앱에서 보낸 hello 원격 분석을 표시 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-107">**ReadDeviceToCloudMessages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="d40a4-108">**SimulatedDevice**, 이전에 만든 hello 장치 id를 가진 tooyour IoT 허브를 연결 하 고 hello MQTT 프로토콜을 사용 하 여 1 초 마다 원격 분석 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-108">**SimulatedDevice**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second by using hello MQTT protocol.</span></span>

<span data-ttu-id="d40a4-109">다운로드 하거나 hello Github에서 세 개의 앱을 포함 하는 hello Visual Studio 솔루션을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-109">You can download or clone hello Visual Studio solution, which contains hello three apps from Github.</span></span>

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> <span data-ttu-id="d40a4-110">Toobuild를 사용할 수 있는, Azure IoT Sdk hello에 대 한 정보에 대 한 장치에서 응용 프로그램 toorun와 솔루션 백 엔드 참조 [Azure IoT Sdk][lnk-hub-sdks]합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-110">For information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="d40a4-111">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="d40a4-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="d40a4-112">Visual Studio 2015 또는 Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d40a4-112">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="d40a4-113">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="d40a4-113">An active Azure account.</span></span> <span data-ttu-id="d40a4-114">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="d40a4-115">이제 IoT 허브를 만들고 hello 호스트 이름과 IoT 허브 연결 문자열을이 자습서의 toocomplete hello 나머지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-115">You have now created your IoT hub, and you have hello host name and IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="d40a4-116">장치-클라우드 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="d40a4-116">Receive device-to-cloud messages</span></span>
<span data-ttu-id="d40a4-117">이 섹션에서는 IoT Hub에서 장치-클라우드 메시지를 읽는 .NET 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-117">In this section, you create a .NET console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="d40a4-118">IoT hub를 노출 한 [Azure 이벤트 허브][lnk-event-hubs-overview]-호환 되는 끝점 tooenable tooread 장치-클라우드 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-118">An IoT hub exposes an [Azure Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="d40a4-119">단순 tookeep 항목을이 자습서에서는 처리량이 높은 배포에 적합 하지 않은 기본 판독기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-119">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="d40a4-120">toolearn 배율을 사용할 때 tooprocess 장치-클라우드 메시지 하는 방법을 참조 hello [장치-클라우드 메시지를 처리] [ lnk-process-d2c-tutorial] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-120">toolearn how tooprocess device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span> <span data-ttu-id="d40a4-121">이벤트 허브에서 tooprocess 메시지 하는 방법에 대 한 자세한 내용은 참조 hello [이벤트 허브 시작] [ lnk-eventhubs-tutorial] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-121">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span> <span data-ttu-id="d40a4-122">(이 자습서에는 적용 가능한 toohello 호환 IoT 허브 이벤트 허브 끝점입니다.)</span><span class="sxs-lookup"><span data-stu-id="d40a4-122">(This tutorial is applicable toohello IoT Hub Event Hub-compatible endpoints.)</span></span>

> [!NOTE]
> <span data-ttu-id="d40a4-123">hello 항상 장치-클라우드 메시지 도착 읽기에 대 한 이벤트 허브 호환 끝점 hello AMQP 프로토콜이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-123">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="d40a4-124">Visual Studio에서 Visual C# Windows 클래식 데스크톱 프로젝트 toohello 현재 솔루션을 hello를 사용 하 여 추가 **콘솔 응용 프로그램 (.NET Framework)** 서식 파일 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="d40a4-124">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="d40a4-125">Hello.NET Framework 버전 4.5.1 인지 확인 하거나 나중에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-125">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="d40a4-126">이름 hello 프로젝트 **ReadDeviceToCloudMessages**합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-126">Name hello project **ReadDeviceToCloudMessages**.</span></span>

    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][10a]

2. <span data-ttu-id="d40a4-128">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ReadDeviceToCloudMessages** 프로젝트를 마우스 클릭 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-128">In Solution Explorer, right-click hello **ReadDeviceToCloudMessages** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="d40a4-129">Hello에 **NuGet 패키지 관리자** 창, 검색할 **WindowsAzure.ServiceBus**을 선택 **설치**, hello 사용 약관에 동의 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-129">In hello **NuGet Package Manager** window, search for **WindowsAzure.ServiceBus**, select **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="d40a4-130">이 절차를 다운로드, 설치 하 고 대 한 참조를 너무 추가[Azure 서비스 버스][lnk-servicebus-nuget], 모든 종속성과 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-130">This procedure downloads, installs, and adds a reference too[Azure Service Bus][lnk-servicebus-nuget], with all its dependencies.</span></span> <span data-ttu-id="d40a4-131">이 패키지에는 hello 응용 프로그램 tooconnect toohello 호환 이벤트 허브 끝점을 IoT 허브에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-131">This package enables hello application tooconnect toohello Event Hub-compatible endpoint on your IoT hub.</span></span>

4. <span data-ttu-id="d40a4-132">Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:</span><span class="sxs-lookup"><span data-stu-id="d40a4-132">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. <span data-ttu-id="d40a4-133">다음 필드 toohello hello 추가 **프로그램** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-133">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="d40a4-134">Hello hello "IoT hub 만들기" 섹션에서에서 만든 hello 허브에 대 한 IoT 허브 연결 문자열 hello 자리 표시자 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-134">Replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello "Create an IoT hub" section.</span></span>

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. <span data-ttu-id="d40a4-135">다음 메서드 toohello hello 추가 **프로그램** 클래스:</span><span class="sxs-lookup"><span data-stu-id="d40a4-135">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="d40a4-136">이 메서드는 사용 된 **EventHubReceiver** 모든 hello IoT 허브 장치-클라우드 인스턴스 tooreceive 메시지 수신 파티션 합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-136">This method uses an **EventHubReceiver** instance tooreceive messages from all hello IoT hub device-to-cloud receive partitions.</span></span> <span data-ttu-id="d40a4-137">전달 하는 방법을 확인할 수는 `DateTime.Now` hello를 만들 때 매개 변수 **EventHubReceiver** 개체만 시작 된 후 전송 되는 메시지를 수신할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-137">Notice how you pass a `DateTime.Now` parameter when you create hello **EventHubReceiver** object, so that it only receives messages sent after it starts.</span></span> <span data-ttu-id="d40a4-138">이 필터는 hello 메시지의 현재 집합을 볼 수 있도록 테스트 환경에서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-138">This filter is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="d40a4-139">프로덕션 환경에서 코드를 모든 hello 메시지를 처리 하는지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-139">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="d40a4-140">자세한 내용은 hello 자습서를 참조 하십시오. [어떻게 tooprocess IoT Hub 장치-클라우드 메시지][lnk-process-d2c-tutorial]합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-140">For more information, see hello tutorial [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial].</span></span>

7. <span data-ttu-id="d40a4-141">마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:</span><span class="sxs-lookup"><span data-stu-id="d40a4-141">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive messages. Ctrl-C tooexit.\n");
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

## <a name="create-a-device-app"></a><span data-ttu-id="d40a4-142">장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="d40a4-142">Create a device app</span></span>

<span data-ttu-id="d40a4-143">이 섹션에서는 tooan IoT hub 장치-클라우드 메시지를 전송 하는 장치를 시뮬레이션 하 여.NET 콘솔 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-143">In this section, you create a .NET console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="d40a4-144">Visual Studio에서 Visual C# Windows 클래식 데스크톱 프로젝트 toohello 현재 솔루션을 hello를 사용 하 여 추가 **콘솔 응용 프로그램 (.NET Framework)** 서식 파일 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="d40a4-144">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="d40a4-145">Hello.NET Framework 버전 4.5.1 인지 확인 하거나 나중에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-145">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="d40a4-146">이름 hello 프로젝트 **SimulatedDevice**합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-146">Name hello project **SimulatedDevice**.</span></span>

    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][10b]

2. <span data-ttu-id="d40a4-148">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **SimulatedDevice** 프로젝트를 마우스 클릭 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-148">In Solution Explorer, right-click hello **SimulatedDevice** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="d40a4-149">Hello에 **NuGet 패키지 관리자** 창에서 **찾아보기**, 검색할 **Microsoft.Azure.Devices.Client**선택, **설치** tooinstall hello **Microsoft.Azure.Devices.Client** 패키지 및 hello 사용 약관에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-149">In hello **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Client**, select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="d40a4-150">이 절차를 다운로드, 설치 하 고 참조 toohello 추가 [Azure IoT 장치 SDK NuGet 패키지] [ lnk-device-nuget] 와 그 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-150">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK NuGet package][lnk-device-nuget] and its dependencies.</span></span>

4. <span data-ttu-id="d40a4-151">Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:</span><span class="sxs-lookup"><span data-stu-id="d40a4-151">Add hello following `using` statement at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. <span data-ttu-id="d40a4-152">다음 필드 toohello hello 추가 **프로그램** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="d40a4-153">대체 `{iot hub hostname}` hello IoT 허브 호스트 이름의 hello "IoT hub 만들기" 섹션에서 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-153">Substitute `{iot hub hostname}` with hello IoT hub host name you retrieved in hello "Create an IoT hub" section.</span></span> <span data-ttu-id="d40a4-154">대체 `{device key}` hello 장치 키가 있는 hello "하 여 장치 id 만들기" 섹션에서 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-154">Substitute `{device key}` with hello device key you retrieved in hello "Create a device identity" section.</span></span>

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. <span data-ttu-id="d40a4-155">다음 메서드 toohello hello 추가 **프로그램** 클래스:</span><span class="sxs-lookup"><span data-stu-id="d40a4-155">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="d40a4-156">이 메서드는 1초마다 새로운 장치-클라우드 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-156">This method sends a new device-to-cloud message every second.</span></span> <span data-ttu-id="d40a4-157">hello 메시지 hello 장치 ID 가진 JSON 직렬화 된 개체를 포함 하 고 숫자 toosimulate 온도 센서 및 습도 센서를 임의로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-157">hello message contains a JSON-serialized object, with hello device ID and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

7. <span data-ttu-id="d40a4-158">마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:</span><span class="sxs-lookup"><span data-stu-id="d40a4-158">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    <span data-ttu-id="d40a4-159">기본적으로 hello **만들기** 메서드는.NET Framework 응용 프로그램에 만듭니다는 **DeviceClient** hello AMQP 프로토콜 toocommunicate IoT 허브를 사용 하는 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="d40a4-159">By default, hello **Create** method in a .NET Framework app creates a **DeviceClient** instance that uses hello AMQP protocol toocommunicate with IoT Hub.</span></span> <span data-ttu-id="d40a4-160">toouse hello MQTT 또는 HTTP 프로토콜을 사용 하 여 hello hello 재정의 **만들기** toospecify hello 프로토콜을 설정 하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-160">toouse hello MQTT or HTTP protocol, use hello override of hello **Create** method that enables you toospecify hello protocol.</span></span> <span data-ttu-id="d40a4-161">UWP 및 PCL 클라이언트는 기본적으로 hello HTTP 프로토콜을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-161">UWP and PCL clients use hello HTTP protocol by default.</span></span> <span data-ttu-id="d40a4-162">Hello hello HTTP 프로토콜을 사용 하는 경우도 추가 해야 **Microsoft.AspNet.WebApi.Client** NuGet 패키지 tooyour 프로젝트 tooinclude hello **System.Net.Http.Formatting** 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-162">If you use hello HTTP protocol, you should also add hello **Microsoft.AspNet.WebApi.Client** NuGet package tooyour project tooinclude hello **System.Net.Http.Formatting** namespace.</span></span>

<span data-ttu-id="d40a4-163">이 자습서에서는 hello 단계 toocreate IoT Hub 장치 앱 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-163">This tutorial takes you through hello steps toocreate an IoT Hub device app.</span></span> <span data-ttu-id="d40a4-164">Hello를 사용할 수도 있습니다 [Azure IoT 허브에 대 한 연결 된 서비스] [ lnk-connected-service] Visual Studio 확장 tooadd hello 필요한 코드 tooyour 장치 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-164">You can also use hello [Connected Service for Azure IoT Hub][lnk-connected-service] Visual Studio extension tooadd hello necessary code tooyour device app.</span></span>

> [!NOTE]
> <span data-ttu-id="d40a4-165">단순 tookeep 항목을이 자습서는 어떠한 재시도 정책도 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-165">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="d40a4-166">프로덕션 코드에서는 hello MSDN 문서에 설명 된 대로 다시 시도 정책 (예: 지 수 백오프)를 구현 해야 [일시적인 오류 처리][lnk-transient-faults]합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-166">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="d40a4-167">Hello 앱 실행</span><span class="sxs-lookup"><span data-stu-id="d40a4-167">Run hello apps</span></span>

<span data-ttu-id="d40a4-168">준비 toorun hello 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-168">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="d40a4-169">솔루션 탐색기의 Visual Studio에서 솔루션을 마우스 오른쪽 단추로 클릭한 다음 **시작 프로젝트로 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-169">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="d40a4-170">선택 **여러 개의 시작 프로젝트**를 선택한 후 **시작** 두 hello에 대 한 hello 동작으로 **ReadDeviceToCloudMessages** 및 **SimulatedDevice** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="d40a4-170">Select **Multiple startup projects**, and then select **Start** as hello action for both hello **ReadDeviceToCloudMessages** and **SimulatedDevice** projects.</span></span>

    ![시작 프로젝트 속성][41]

2. <span data-ttu-id="d40a4-172">키를 눌러 **F5** toostart 두 앱 모두를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-172">Press **F5** toostart both apps running.</span></span> <span data-ttu-id="d40a4-173">hello에서 콘솔 출력 hello **SimulatedDevice** 응용 프로그램에서는 hello 메시지 장치 앱 tooyour IoT 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-173">hello console output from hello **SimulatedDevice** app shows hello messages your device app sends tooyour IoT hub.</span></span> <span data-ttu-id="d40a4-174">hello에서 콘솔 출력 hello **ReadDeviceToCloudMessages** 앱 IoT hub를 수신 하는 hello 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-174">hello console output from hello **ReadDeviceToCloudMessages** app shows hello messages that your IoT hub receives.</span></span>

    ![앱에서 콘솔 출력][42]

3. <span data-ttu-id="d40a4-176">hello **사용량** hello에 바둑판식으로 배열 [Azure 포털] [ lnk-portal] 표시 hello 보낸 메시지 toohello IoT 허브의 수:</span><span class="sxs-lookup"><span data-stu-id="d40a4-176">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Azure Portal 사용량 타일][43]

## <a name="next-steps"></a><span data-ttu-id="d40a4-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d40a4-178">Next steps</span></span>

<span data-ttu-id="d40a4-179">이 자습서에서는 hello Azure 포털에서에서 IoT hub를 구성 하 고 id 레지스트리에 hello IoT hub에서 장치 id를 만든 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-179">In this tutorial, you configured an IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="d40a4-180">이 장치 identity tooenable hello 장치 앱 toosend 장치-클라우드 메시지 toohello IoT 허브를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-180">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="d40a4-181">또한 hello IoT 허브에서 수신 하는 hello 메시지를 표시 하는 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-181">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="d40a4-182">시작 toocontinue IoT 허브와 tooexplore 다른 IoT 시나리오를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="d40a4-182">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="d40a4-183">[장치 연결][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="d40a4-183">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="d40a4-184">[장치 관리 시작][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="d40a4-184">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="d40a4-185">[IoT Edge 시작][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="d40a4-185">[Getting started with IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="d40a4-186">toolearn tooextend 배율 사용할 때 IoT 솔루션 및 프로세스 장치-클라우드 메시지를 확인 하려면 어떻게 hello [장치-클라우드 메시지를 처리] [ lnk-process-d2c-tutorial] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="d40a4-186">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

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

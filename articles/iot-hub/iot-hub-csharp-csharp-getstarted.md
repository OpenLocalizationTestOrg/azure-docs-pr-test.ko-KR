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
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a>.NET을 사용 하 여 장치 tooyour IoT 허브를 연결 합니다.

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

이 자습서의 hello 끝 세 개의.NET 콘솔 응용 프로그램을 사용할 수 있습니다.

* **CreateDeviceIdentity**, 장치 id를 만드는 연결 된 보안 키 tooconnect 장치 응용 프로그램 및입니다.
* **ReadDeviceToCloudMessages**, 장치 앱에서 보낸 hello 원격 분석을 표시 하는 합니다.
* **SimulatedDevice**, 이전에 만든 hello 장치 id를 가진 tooyour IoT 허브를 연결 하 고 hello MQTT 프로토콜을 사용 하 여 1 초 마다 원격 분석 메시지를 보냅니다.

다운로드 하거나 hello Github에서 세 개의 앱을 포함 하는 hello Visual Studio 솔루션을 복제할 수 있습니다.

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> Toobuild를 사용할 수 있는, Azure IoT Sdk hello에 대 한 정보에 대 한 장치에서 응용 프로그램 toorun와 솔루션 백 엔드 참조 [Azure IoT Sdk][lnk-hub-sdks]합니다.

toocomplete이이 자습서에서는 다음 hello 필요:

* Visual Studio 2015 또는 Visual Studio 2017.
* 활성 Azure 계정. 계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

이제 IoT 허브를 만들고 hello 호스트 이름과 IoT 허브 연결 문자열을이 자습서의 toocomplete hello 나머지 해야 합니다.

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a>장치-클라우드 메시지 받기
이 섹션에서는 IoT Hub에서 장치-클라우드 메시지를 읽는 .NET 콘솔 앱을 만듭니다. IoT hub를 노출 한 [Azure 이벤트 허브][lnk-event-hubs-overview]-호환 되는 끝점 tooenable tooread 장치-클라우드 메시지입니다. 단순 tookeep 항목을이 자습서에서는 처리량이 높은 배포에 적합 하지 않은 기본 판독기를 만듭니다. toolearn 배율을 사용할 때 tooprocess 장치-클라우드 메시지 하는 방법을 참조 hello [장치-클라우드 메시지를 처리] [ lnk-process-d2c-tutorial] 자습서입니다. 이벤트 허브에서 tooprocess 메시지 하는 방법에 대 한 자세한 내용은 참조 hello [이벤트 허브 시작] [ lnk-eventhubs-tutorial] 자습서입니다. (이 자습서에는 적용 가능한 toohello 호환 IoT 허브 이벤트 허브 끝점입니다.)

> [!NOTE]
> hello 항상 장치-클라우드 메시지 도착 읽기에 대 한 이벤트 허브 호환 끝점 hello AMQP 프로토콜이 사용 됩니다.

1. Visual Studio에서 Visual C# Windows 클래식 데스크톱 프로젝트 toohello 현재 솔루션을 hello를 사용 하 여 추가 **콘솔 응용 프로그램 (.NET Framework)** 서식 파일 프로젝트. Hello.NET Framework 버전 4.5.1 인지 확인 하거나 나중에 있습니다. 이름 hello 프로젝트 **ReadDeviceToCloudMessages**합니다.

    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][10a]

2. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ReadDeviceToCloudMessages** 프로젝트를 마우스 클릭 **NuGet 패키지 관리**합니다.

3. Hello에 **NuGet 패키지 관리자** 창, 검색할 **WindowsAzure.ServiceBus**을 선택 **설치**, hello 사용 약관에 동의 하 고 있습니다. 이 절차를 다운로드, 설치 하 고 대 한 참조를 너무 추가[Azure 서비스 버스][lnk-servicebus-nuget], 모든 종속성과 함께 합니다. 이 패키지에는 hello 응용 프로그램 tooconnect toohello 호환 이벤트 허브 끝점을 IoT 허브에 있습니다.

4. Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. 다음 필드 toohello hello 추가 **프로그램** 클래스입니다. Hello hello "IoT hub 만들기" 섹션에서에서 만든 hello 허브에 대 한 IoT 허브 연결 문자열 hello 자리 표시자 값을 바꿉니다.

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. 다음 메서드 toohello hello 추가 **프로그램** 클래스:

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

    이 메서드는 사용 된 **EventHubReceiver** 모든 hello IoT 허브 장치-클라우드 인스턴스 tooreceive 메시지 수신 파티션 합니다. 전달 하는 방법을 확인할 수는 `DateTime.Now` hello를 만들 때 매개 변수 **EventHubReceiver** 개체만 시작 된 후 전송 되는 메시지를 수신할 수 있도록 합니다. 이 필터는 hello 메시지의 현재 집합을 볼 수 있도록 테스트 환경에서 유용 합니다. 프로덕션 환경에서 코드를 모든 hello 메시지를 처리 하는지 않도록 해야 합니다. 자세한 내용은 hello 자습서를 참조 하십시오. [어떻게 tooprocess IoT Hub 장치-클라우드 메시지][lnk-process-d2c-tutorial]합니다.

7. 마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:

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

## <a name="create-a-device-app"></a>장치 앱 만들기

이 섹션에서는 tooan IoT hub 장치-클라우드 메시지를 전송 하는 장치를 시뮬레이션 하 여.NET 콘솔 응용 프로그램을 만들 수 있습니다.

1. Visual Studio에서 Visual C# Windows 클래식 데스크톱 프로젝트 toohello 현재 솔루션을 hello를 사용 하 여 추가 **콘솔 응용 프로그램 (.NET Framework)** 서식 파일 프로젝트. Hello.NET Framework 버전 4.5.1 인지 확인 하거나 나중에 있습니다. 이름 hello 프로젝트 **SimulatedDevice**합니다.

    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][10b]

2. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **SimulatedDevice** 프로젝트를 마우스 클릭 **NuGet 패키지 관리**합니다.

3. Hello에 **NuGet 패키지 관리자** 창에서 **찾아보기**, 검색할 **Microsoft.Azure.Devices.Client**선택, **설치** tooinstall hello **Microsoft.Azure.Devices.Client** 패키지 및 hello 사용 약관에 동의 합니다. 이 절차를 다운로드, 설치 하 고 참조 toohello 추가 [Azure IoT 장치 SDK NuGet 패키지] [ lnk-device-nuget] 와 그 종속성입니다.

4. Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. 다음 필드 toohello hello 추가 **프로그램** 클래스입니다. 대체 `{iot hub hostname}` hello IoT 허브 호스트 이름의 hello "IoT hub 만들기" 섹션에서 검색 합니다. 대체 `{device key}` hello 장치 키가 있는 hello "하 여 장치 id 만들기" 섹션에서 검색 합니다.

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. 다음 메서드 toohello hello 추가 **프로그램** 클래스:

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

    이 메서드는 1초마다 새로운 장치-클라우드 메시지를 보냅니다. hello 메시지 hello 장치 ID 가진 JSON 직렬화 된 개체를 포함 하 고 숫자 toosimulate 온도 센서 및 습도 센서를 임의로 생성 합니다.

7. 마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    기본적으로 hello **만들기** 메서드는.NET Framework 응용 프로그램에 만듭니다는 **DeviceClient** hello AMQP 프로토콜 toocommunicate IoT 허브를 사용 하는 인스턴스. toouse hello MQTT 또는 HTTP 프로토콜을 사용 하 여 hello hello 재정의 **만들기** toospecify hello 프로토콜을 설정 하는 메서드입니다. UWP 및 PCL 클라이언트는 기본적으로 hello HTTP 프로토콜을 사용합니다. Hello hello HTTP 프로토콜을 사용 하는 경우도 추가 해야 **Microsoft.AspNet.WebApi.Client** NuGet 패키지 tooyour 프로젝트 tooinclude hello **System.Net.Http.Formatting** 네임 스페이스입니다.

이 자습서에서는 hello 단계 toocreate IoT Hub 장치 앱 줍니다. Hello를 사용할 수도 있습니다 [Azure IoT 허브에 대 한 연결 된 서비스] [ lnk-connected-service] Visual Studio 확장 tooadd hello 필요한 코드 tooyour 장치 응용 프로그램입니다.

> [!NOTE]
> 단순 tookeep 항목을이 자습서는 어떠한 재시도 정책도 구현 하지 않습니다. 프로덕션 코드에서는 hello MSDN 문서에 설명 된 대로 다시 시도 정책 (예: 지 수 백오프)를 구현 해야 [일시적인 오류 처리][lnk-transient-faults]합니다.

## <a name="run-hello-apps"></a>Hello 앱 실행

준비 toorun hello 앱입니다.

1. 솔루션 탐색기의 Visual Studio에서 솔루션을 마우스 오른쪽 단추로 클릭한 다음 **시작 프로젝트로 설정**을 클릭합니다. 선택 **여러 개의 시작 프로젝트**를 선택한 후 **시작** 두 hello에 대 한 hello 동작으로 **ReadDeviceToCloudMessages** 및 **SimulatedDevice** 프로젝트.

    ![시작 프로젝트 속성][41]

2. 키를 눌러 **F5** toostart 두 앱 모두를 실행 합니다. hello에서 콘솔 출력 hello **SimulatedDevice** 응용 프로그램에서는 hello 메시지 장치 앱 tooyour IoT 허브를 보냅니다. hello에서 콘솔 출력 hello **ReadDeviceToCloudMessages** 앱 IoT hub를 수신 하는 hello 메시지를 표시 합니다.

    ![앱에서 콘솔 출력][42]

3. hello **사용량** hello에 바둑판식으로 배열 [Azure 포털] [ lnk-portal] 표시 hello 보낸 메시지 toohello IoT 허브의 수:

    ![Azure Portal 사용량 타일][43]

## <a name="next-steps"></a>다음 단계

이 자습서에서는 hello Azure 포털에서에서 IoT hub를 구성 하 고 id 레지스트리에 hello IoT hub에서 장치 id를 만든 다음 합니다. 이 장치 identity tooenable hello 장치 앱 toosend 장치-클라우드 메시지 toohello IoT 허브를 사용 했습니다. 또한 hello IoT 허브에서 수신 하는 hello 메시지를 표시 하는 응용 프로그램을 만들었습니다.

시작 toocontinue IoT 허브와 tooexplore 다른 IoT 시나리오를 참조 하세요.

* [장치 연결][lnk-connect-device]
* [장치 관리 시작][lnk-device-management]
* [IoT Edge 시작][lnk-iot-edge]

toolearn tooextend 배율 사용할 때 IoT 솔루션 및 프로세스 장치-클라우드 메시지를 확인 하려면 어떻게 hello [장치-클라우드 메시지를 처리] [ lnk-process-d2c-tutorial] 자습서입니다.

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

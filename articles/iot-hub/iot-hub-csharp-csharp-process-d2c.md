---
title: "경로 (.NET)를 사용 하 여 aaaProcess Azure IoT Hub 장치-클라우드 메시지 | Microsoft Docs"
description: "어떻게 tooprocess 라우팅 규칙 및 사용자 지정 끝점 toodispatch를 사용 하 여 IoT Hub 장치-클라우드 메시지 tooother 백 엔드 서비스 메시지입니다."
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
ms.openlocfilehash: c1dd5be04ca30c65af2be466ba6c8c1858333154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a><span data-ttu-id="80290-103">경로를 사용하여 IoT Hub 장치-클라우드 메시지 처리(.Net)</span><span class="sxs-lookup"><span data-stu-id="80290-103">Process IoT Hub device-to-cloud messages using routes (.NET)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="80290-104">이 자습서는 hello에 빌드 [IoT 허브 시작] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="80290-104">This tutorial builds on hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="80290-105">hello 자습서:</span><span class="sxs-lookup"><span data-stu-id="80290-105">hello tutorial:</span></span>

* <span data-ttu-id="80290-106">Toouse 라우팅 규칙 방식 toodispatch 장치-클라우드 메시지를 쉽게, 구성 기반 방식으로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="80290-106">Shows you how toouse routing rules toodispatch device-to-cloud messages in an easy, configuration-based way.</span></span>
* <span data-ttu-id="80290-107">Tooisolate 대화형 메시지 hello 솔루션에서 즉각적인 조치를 필요로 하는 추가 처리에 대 한 끝을 백업 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="80290-107">Illustrates how tooisolate interactive messages that require immediate action from hello solution back end for further processing.</span></span> <span data-ttu-id="80290-108">예를 들어 장치는 CRM 시스템으로의 티켓 삽입을 트리거하는 경보 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80290-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="80290-109">반면 온도 원격 분석과 같은 데이터 요소 메시지는 분석 엔진으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="80290-109">In contrast, data-point messages, such as temperature telemetry, feed into an analytics engine.</span></span>

<span data-ttu-id="80290-110">이 자습서의 hello 끝 세 개의.NET 콘솔 응용 프로그램 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-110">At hello end of this tutorial, you run three .NET console apps:</span></span>

* <span data-ttu-id="80290-111">**SimulatedDevice**, hello에서 만든 hello 응용 프로그램의 수정된 된 버전 [IoT 허브 시작] 자습서 1 초 마다 데이터 요소 장치-클라우드 메시지를 보냅니다 및 대화형 장치-클라우드 메시지 마다 10 시간 (초)입니다.</span><span class="sxs-lookup"><span data-stu-id="80290-111">**SimulatedDevice**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span>
* <span data-ttu-id="80290-112">**ReadDeviceToCloudMessages** 디스플레이 장치 앱으로 전송 하는 중요 하지 않은 원격 분석 hello 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-112">**ReadDeviceToCloudMessages** that displays hello non-critical telemetry sent by your device app.</span></span>
* <span data-ttu-id="80290-113">**ReadCriticalQueue** 장치 앱에서 서비스 버스 큐에서 보낸 hello 중요 한 메시지 큐에 넣고 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-113">**ReadCriticalQueue** de-queues hello critical messages sent by your device app from a Service Bus queue.</span></span> <span data-ttu-id="80290-114">이 큐는 연결 된 toohello IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="80290-114">This queue is attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="80290-115">IoT Hub는 많은 장치 플랫폼 및 언어(C, Java 및 JavaScript 포함)에 SDK를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-115">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="80290-116">toolearn tooreplace이이 자습서의 시뮬레이션 된 장치는 물리적 장치와 hello 참조 hello [Azure IoT 개발자 센터]합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-116">toolearn how tooreplace hello simulated device in this tutorial with a physical device, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="80290-117">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="80290-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="80290-118">Visual Studio 2015 또는 Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="80290-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="80290-119">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="80290-119">An active Azure account.</span></span> <br/><span data-ttu-id="80290-120">계정이 없는 경우 몇 분 안에 [무료 계정](https://azure.microsoft.com/free/) 을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80290-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="80290-121">[Azure Storage] 및 [Azure Service Bus]에 대한 기본 지식이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-121">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages"></a><span data-ttu-id="80290-122">대화형 메시지 전송</span><span class="sxs-lookup"><span data-stu-id="80290-122">Send interactive messages</span></span>

<span data-ttu-id="80290-123">Hello 장치 hello에서 만든 응용 프로그램 수정 [IoT 허브 시작] 자습서 toooccasionally 대화형 메시지를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-123">Modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send interactive messages.</span></span>

<span data-ttu-id="80290-124">Hello에 Visual Studio에서 **SimulatedDevice** 프로젝트를 hello 대체 `SendDeviceToCloudMessagesAsync` 메서드 코드 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="80290-124">In Visual Studio, in hello **SimulatedDevice** project, replace hello `SendDeviceToCloudMessagesAsync` method with hello following code:</span></span>

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

<span data-ttu-id="80290-125">이 메서드는 임의로 hello 속성 추가 `"level": "critical"` toomessages hello 솔루션 백 엔드 하 여 즉각적인 동작이 필요한 메시지를 시뮬레이트하는 hello 장치에 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-125">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello solution back-end.</span></span> <span data-ttu-id="80290-126">해당 IoT 허브는 hello 메시지 toohello 적절 한 메시지 대상 라우팅할 수 있도록 hello 장치 앱 hello 메시지 속성에서이 정보 대신 hello 메시지 본문에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-126">hello device app passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>

> [!NOTE]
> <span data-ttu-id="80290-127">콜드 경로 toohello 실행 부하 과다 경로 여기에 표시 된 예에서는 또한 처리를 포함 하는 다양 한 시나리오에 대 한 메시지 속성 tooroute 메시지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80290-127">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot-path example shown here.</span></span>

> [!NOTE]
> <span data-ttu-id="80290-128">이 자습서는 간단한 hello 위해서 어떠한 재시도 정책도 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80290-128">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="80290-129">프로덕션 코드에서는 hello MSDN 문서에 설명 된 대로 지 수 백오프 같은 다시 시도 정책을 구현 해야 [일시적인 오류 처리]합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-129">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

## <a name="route-messages-tooa-queue-in-your-iot-hub"></a><span data-ttu-id="80290-130">IoT 허브에서 메시지 tooa 큐 경로</span><span class="sxs-lookup"><span data-stu-id="80290-130">Route messages tooa queue in your IoT hub</span></span>

<span data-ttu-id="80290-131">이 섹션에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-131">In this section, you:</span></span>

* <span data-ttu-id="80290-132">Service Bus 큐를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80290-132">Create a Service Bus queue.</span></span>
* <span data-ttu-id="80290-133">Tooyour IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-133">Connect it tooyour IoT hub.</span></span>
* <span data-ttu-id="80290-134">Hello 메시지에서 속성의 hello 존재 여부에 따라 IoT 허브 toosend 메시지 toohello 큐를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-134">Configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span>

<span data-ttu-id="80290-135">서비스 버스 큐에서 메시지를 tooprocess 방법에 대 한 자세한 내용은 참조 [큐 작업 시작][Service Bus queue]합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-135">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span></span>

1. <span data-ttu-id="80290-136">[큐 시작][Service Bus queue]에서 설명한 대로 Service Bus 큐를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80290-136">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span></span> <span data-ttu-id="80290-137">hello 큐는 hello에 있어야 합니다. 동일한 구독 및 지역이 IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="80290-137">hello queue must be in hello same subscription and region as your IoT hub.</span></span> <span data-ttu-id="80290-138">Hello 네임 스페이스와 큐 이름을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="80290-138">Make a note of hello namespace and queue name.</span></span>

    > [!NOTE]
    > <span data-ttu-id="80290-139">IoT Hub으로 사용되는 Service Bus 큐 및 토픽에는 **세션** 또는 **중복 검색**이 사용하도록 설정되어 있어서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80290-139">Service Bus queues and topics used as IoT Hub endpoints must not have **Sessions** or **Duplicate Detection** enabled.</span></span> <span data-ttu-id="80290-140">Hello 끝점으로 표시 되는 이러한 옵션 중 하나를 사용할 수 있으면 **연결할 수 없는** hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="80290-140">If either of those options are enabled, hello endpoint appears as **Unreachable** in hello Azure portal.</span></span>

2. <span data-ttu-id="80290-141">에 Azure 포털 hello IoT 허브를 열고 클릭 **끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-141">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>
    
    ![IoT Hub의 끝점][30]

3. <span data-ttu-id="80290-143">Hello에 **끝점** 블레이드에서 클릭 **추가** 에 hello 상위 tooadd 큐 tooyour IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="80290-143">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="80290-144">이름 hello 끝점 **CriticalQueue** 드롭다운 tooselect hello를 사용 하 여 **서비스 버스 큐**, 큐 상주 하는 서비스 버스 네임 스페이스 hello 및 hello 큐의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="80290-144">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="80290-145">완료 되 면 클릭 **저장** hello 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80290-145">When you are done, click **Save** at hello bottom.</span></span>
    
    ![끝점 추가][31]
    
4. <span data-ttu-id="80290-147">이제 IoT Hub에서 **경로**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-147">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="80290-148">클릭 **추가** toohello 방금 하면 큐 메시지를 라우팅하는 라우팅 규칙을 추가 하는 hello 블레이드 toocreate hello 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80290-148">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="80290-149">선택 **DeviceTelemetry** hello 데이터 원본으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-149">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="80290-150">입력 `level="critical"` hello 조건으로 사용자 지정 끝점으로 라우팅 규칙 끝점 hello로 방금 추가한 hello 큐를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-150">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="80290-151">완료 되 면 클릭 **저장** hello 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80290-151">When you are done, click **Save** at hello bottom.</span></span>
    
    ![경로 추가][32]
    
    <span data-ttu-id="80290-153">대체 경로 hello 너무 설정 되어 있는지 확인**ON**합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-153">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="80290-154">이 값은 IoT 허브에 대 한 hello 기본 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="80290-154">This value is hello default configuration for an IoT hub.</span></span>
    
    ![대체(fallback) 경로][33]

## <a name="read-from-hello-queue-endpoint"></a><span data-ttu-id="80290-156">Hello 큐 끝점에서 읽기</span><span class="sxs-lookup"><span data-stu-id="80290-156">Read from hello queue endpoint</span></span>

<span data-ttu-id="80290-157">이 섹션에서는 hello 큐 끝점에서 hello 메시지를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="80290-157">In this section, you read hello messages from hello queue endpoint.</span></span>

1. <span data-ttu-id="80290-158">Visual Studio에서 Visual C# Windows 클래식 데스크톱 프로젝트 toohello 현재 솔루션을 hello를 사용 하 여 추가 **콘솔 응용 프로그램 (.NET Framework)** 서식 파일 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="80290-158">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="80290-159">이름 hello 프로젝트 **ReadCriticalQueue**합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-159">Name hello project **ReadCriticalQueue**.</span></span>

2. <span data-ttu-id="80290-160">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ReadCriticalQueue** 프로젝트를 마우스 클릭 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-160">In Solution Explorer, right-click hello **ReadCriticalQueue** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="80290-161">이 작업 표시 hello **NuGet 패키지 관리자** 창.</span><span class="sxs-lookup"><span data-stu-id="80290-161">This operation displays hello **NuGet Package Manager** window.</span></span>

3. <span data-ttu-id="80290-162">검색할 **WindowsAzure.ServiceBus**, 클릭 **설치**, hello 사용 약관을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-162">Search for **WindowsAzure.ServiceBus**, click **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="80290-163">이 작업을 다운로드 하 고 설치 하 여 모든 종속성과 함께 참조 toohello Azure 서비스 버스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-163">This operation downloads, installs, and adds a reference toohello Azure Service Bus, with all its dependencies.</span></span>

4. <span data-ttu-id="80290-164">Hello 다음 추가 **를 사용 하 여** hello 위쪽 hello에 문을 **Program.cs** 파일:</span><span class="sxs-lookup"><span data-stu-id="80290-164">Add hello following **using** statements at hello top of hello **Program.cs** file:</span></span>
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. <span data-ttu-id="80290-165">마지막으로 다음 줄 toohello hello 추가 **Main** 메서드.</span><span class="sxs-lookup"><span data-stu-id="80290-165">Finally, add hello following lines toohello **Main** method.</span></span> <span data-ttu-id="80290-166">Hello 연결 문자열을 대체할 **수신** hello 큐에 대 한 사용 권한:</span><span class="sxs-lookup"><span data-stu-id="80290-166">Substitute hello connection string with **Listen** permissions for hello queue:</span></span>
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C tooexit.\n");
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

## <a name="run-hello-applications"></a><span data-ttu-id="80290-167">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="80290-167">Run hello applications</span></span>
<span data-ttu-id="80290-168">이제 준비 toorun hello 응용 프로그램 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80290-168">Now you are ready toorun hello applications.</span></span>

1. <span data-ttu-id="80290-169">솔루션 탐색기의 Visual Studio에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **시작 프로젝트 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-169">In Visual Studio, in Solution Explorer, right-click your solution and select **Set StartUp Projects**.</span></span> <span data-ttu-id="80290-170">선택 **여러 개의 시작 프로젝트**을 선택한 후 **시작** hello에 대 한 hello 동작으로 **ReadDeviceToCloudMessages**, **SimulatedDevice**, 및 **ReadCriticalQueue** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="80290-170">Select **Multiple startup projects**, then select **Start** as hello action for hello **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **ReadCriticalQueue** projects.</span></span>
2. <span data-ttu-id="80290-171">키를 눌러 **F5** toostart hello 세 개의 콘솔 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="80290-171">Press **F5** toostart hello three console apps.</span></span> <span data-ttu-id="80290-172">hello **ReadDeviceToCloudMessages** 응용 프로그램에 중요 하지 않은 메시지만 hello에서 보낸 **SimulatedDevice** 응용 프로그램, 그리고 hello **ReadCriticalQueue** 응용 프로그램에만 중요 한 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="80290-172">hello **ReadDeviceToCloudMessages** app has only non-critical messages sent from hello **SimulatedDevice** application, and hello **ReadCriticalQueue** app has only critical messages.</span></span>
   
   ![3개의 콘솔 앱][50]

## <a name="next-steps"></a><span data-ttu-id="80290-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="80290-174">Next steps</span></span>
<span data-ttu-id="80290-175">이 자습서에서는 tooreliably IoT 허브의 hello 메시지 라우팅 기능을 사용 하 여 장치-클라우드 메시지를 디스패치 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="80290-175">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="80290-176">hello [IoT Hub와 toosend 클라우드-장치 메시지 방법을] [ lnk-c2d] toosend 솔루션 백 엔드에서 tooyour 장치 메시지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="80290-176">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="80290-177">IoT 허브를 사용 하는 완벽 한 종단 간 솔루션의 toosee 예 참조 [Azure IoT Suite][lnk-suite]합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-177">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="80290-178">IoT 허브를 사용 하 여 솔루션 개발에 대 한 더 toolearn 참조 hello [IoT 허브 개발자 가이드]합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-178">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="80290-179">IoT Hub에 메시지 라우팅에 대 한 더 toolearn 참조 [IoT Hub와 메시지를 주고받을][lnk-devguide-messaging]합니다.</span><span class="sxs-lookup"><span data-stu-id="80290-179">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/
[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/
[IoT 허브 개발자 가이드]: iot-hub-devguide.md
[IoT 허브 시작]: iot-hub-csharp-csharp-getstarted.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[Azure IoT 개발자 센터]: https://azure.microsoft.com/develop/iot
[일시적인 오류 처리]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/

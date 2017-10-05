---
title: "Azure IoT Hub(.NET)를 사용한 클라우드-장치 메시지 | Microsoft Docs"
description: ".NET용 Azure IoT SDK를 사용하여 Azure IoT Hub에서 장치로 클라우드-장치 메시지를 보내는 방법입니다. 클라우드-장치 메시지를 수신하도록 장치 앱을 수정하고 클라우드-장치 메시지를 보내도록 백 엔드 앱을 수정합니다."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: a31c05ed-6ec0-40f3-99ab-8fdd28b1a89a
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: 3f5f83671054c30afde3d7f18ff0edcdb8f78a01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="send-messages-from-the-cloud-to-your-device-with-iot-hub-net"></a><span data-ttu-id="18df4-104">IoT Hub(.NET)를 사용하여 클라우드에서 장치에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="18df4-104">Send messages from the cloud to your device with IoT Hub (.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="18df4-105">소개</span><span class="sxs-lookup"><span data-stu-id="18df4-105">Introduction</span></span>
<span data-ttu-id="18df4-106">Azure IoT Hub는 수백만 개의 장치와 솔루션 백 엔드 간에 안정적이고 안전한 양방향 통신이 가능하도록 지원하는 완전히 관리되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="18df4-107">[IoT Hub 시작하기] 자습서에서는 IoT Hub를 만들고 그 안에 장치 ID를 프로비전하고 장치-클라우드 메시지를 보내는 장치 앱을 코딩하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="18df4-108">이 자습서는 [IoT Hub 시작하기]를 토대로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="18df4-109">이 항목에서는 다음 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-109">It shows you how to:</span></span>

* <span data-ttu-id="18df4-110">솔루션 백 엔드에서 IoT Hub를 통해 클라우드-장치 메시지를 단일 장치로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="18df4-111">장치에서 클라우드-장치 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="18df4-112">솔루션 백 엔드에서, IoT Hub에서 장치로 보낸 메시지에 대한 배달 확인(*피드백*)을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="18df4-113">클라우드-장치 메시지에 자세한 내용은 [IoT Hub 개발자 가이드][IoT Hub developer guide - C2D]에서 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="18df4-114">이 자습서의 끝 부분에서 다음의 두 .NET 콘솔 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-114">At the end of this tutorial, you run two .NET console apps:</span></span>

* <span data-ttu-id="18df4-115">**SimulatedDevice**, [IoT Hub 시작하기]에서 만든 앱의 수정된 버전으로서 IoT Hub에 연결하고 클라우드-장치 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-115">**SimulatedDevice**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="18df4-116">**SendCloudToDevice** - IoT Hub를 통해 장치 앱에 클라우드-장치 메시지를 보낸 다음 배달 승인을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-116">**SendCloudToDevice**, which sends a cloud-to-device message to the device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="18df4-117">IoT Hub는 [Azure IoT 장치 SDK]를 통해 많은 장치 플랫폼 및 언어(C, Java 및 Javascript 포함)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through [Azure IoT device SDKs].</span></span> <span data-ttu-id="18df4-118">이 자습서의 코드 및 일반적으로 Azure IoT Hub에 장치를 연결하는 방법에 대한 단계별 지침은 [IoT Hub 개발자 가이드]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18df4-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [IoT Hub developer guide].</span></span>
> 
> 

<span data-ttu-id="18df4-119">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="18df4-120">Visual Studio 2015 또는 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="18df4-120">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="18df4-121">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="18df4-121">An active Azure account.</span></span> <span data-ttu-id="18df4-122">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-device-app"></a><span data-ttu-id="18df4-123">장치 앱에서 메시지 수신</span><span class="sxs-lookup"><span data-stu-id="18df4-123">Receive messages in the device app</span></span>
<span data-ttu-id="18df4-124">이 섹션에서는 [IoT Hub 시작하기]에서 만든 장치 앱을 수정하여 IoT Hub로부터 클라우드-장치 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-124">In this section, you'll modify the device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="18df4-125">Visual Studio에서 **SimulatedDevice** 프로젝트의 **Program** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-125">In Visual Studio, in the **SimulatedDevice** project, add the following method to the **Program** class.</span></span>
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud to device messages from service");
            while (true)
            {
                Message receivedMessage = await deviceClient.ReceiveAsync();
                if (receivedMessage == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received message: {0}", Encoding.ASCII.GetString(receivedMessage.GetBytes()));
                Console.ResetColor();
   
                await deviceClient.CompleteAsync(receivedMessage);
            }
        }
   
    <span data-ttu-id="18df4-126">`ReceiveAsync` 메서드는 수신 메시지를 장치에서 받은 시간에 비동기적으로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-126">The `ReceiveAsync` method asynchronously returns the received message at the time that it is received by the device.</span></span> <span data-ttu-id="18df4-127">지정 가능한 시간 제한 기간(이 경우 기본값 1분이 사용됨) 이후에는 *null* 을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-127">It returns *null* after a specifiable timeout period (in this case, the default of one minute is used).</span></span> <span data-ttu-id="18df4-128">앱에서 *null*을 수신하면 새 메시지를 계속 기다려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-128">When the app receives a *null*, it should continue to wait for new messages.</span></span> <span data-ttu-id="18df4-129">이 요구 사항은 `if (receivedMessage == null) continue` 줄 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-129">This requirement is the reason for the `if (receivedMessage == null) continue` line.</span></span>
   
    <span data-ttu-id="18df4-130">`CompleteAsync()`에 대한 호출은 메시지가 정상적으로 처리되었음을 IoT Hub에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-130">The call to `CompleteAsync()` notifies IoT Hub that the message has been successfully processed.</span></span> <span data-ttu-id="18df4-131">장치 큐에서 메시지를 안전하게 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-131">The message can be safely removed from the device queue.</span></span> <span data-ttu-id="18df4-132">장치 앱의 메시지 처리를 완료하지 못하게 하는 문제가 발생하는 경우 IoT Hub에서 메시지를 다시 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-132">If something happened that prevented the device app from completing the processing of the message, IoT Hub delivers it again.</span></span> <span data-ttu-id="18df4-133">장치 앱의 메시지 처리 논리는 *멱등성(idempotent)*이므로 같은 메시지를 여러 번 수신하면 동일한 결과가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-133">It is then important that message processing logic in the device app is *idempotent*, so that receiving the same message multiple times produces the same result.</span></span> <span data-ttu-id="18df4-134">응용 프로그램이 메시지를 일시적으로 중단할 수도 있으며 이 경우 IoT hub는 나중에 사용하기 위해 큐에 메시지를 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-134">An application can also temporarily abandon a message, which results in IoT hub retaining the message in the queue for future consumption.</span></span> <span data-ttu-id="18df4-135">또는 응용 프로그램이 메시지를 거부할 수 있습니다. 이 경우 큐에서 메시지가 영구적으로 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-135">Or, the application can reject a message, which permanently removes the message from the queue.</span></span> <span data-ttu-id="18df4-136">클라우드-장치 메시지 수명 주기에 대한 자세한 내용은 [IoT Hub 개발자 가이드][IoT Hub developer guide - C2D]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18df4-136">For more information about the cloud-to-device message lifecycle, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="18df4-137">MQTT 또는 AMQP 대신 HTTP를 전송으로 사용하는 경우 `ReceiveAsync` 메서드가 즉시 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-137">When using HTTP instead of MQTT or AMQP as a transport, the `ReceiveAsync` method returns immediately.</span></span> <span data-ttu-id="18df4-138">HTTP에서 클라우드-장치 메시지에 대해 지원되는 패턴은 메시지를 가끔씩(25분에 한 번씩보다 적게) 확인하는 장치에 간헐적으로 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-138">The supported pattern for cloud-to-device messages with HTTP is intermittently connected devices that check for messages infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="18df4-139">HTTP 수신을 더 많이 실행하면 IoT Hub가 요청을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-139">Issuing more HTTP receives results in IoT Hub throttling the requests.</span></span> <span data-ttu-id="18df4-140">MQTT, AMQP 및 HTTP 지원과 IoT Hub 제한 간의 차이점에 대한 자세한 내용은 [IoT Hub 개발자 가이드][IoT Hub developer guide - C2D]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18df4-140">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 
2. <span data-ttu-id="18df4-141">**Main** 메서드에서 `Console.ReadLine()` 줄 바로 앞에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-141">Add the following method in the **Main** method, right before the `Console.ReadLine()` line:</span></span>
   
        ReceiveC2dAsync();

> [!NOTE]
> <span data-ttu-id="18df4-142">간단히 하기 위해 이 자습서에서는 재시도 정책을 구현하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-142">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="18df4-143">프로덕션 코드에서는 MSDN 문서 [일시적인 오류 처리]에서 제시한 대로 재시도 정책(예: 지수 백오프)을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-143">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="18df4-144">클라우드-장치 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="18df4-144">Send a cloud-to-device message</span></span>
<span data-ttu-id="18df4-145">이 섹션에서는 클라우드-장치 메시지를 장치 앱으로 보내는 .NET 콘솔 앱을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-145">In this section, you write a .NET console app that sends cloud-to-device messages to the device app.</span></span>

1. <span data-ttu-id="18df4-146">최신 Visual Studio 솔루션에서 **콘솔 응용 프로그램** 프로젝트 템플릿을 사용하여 Visual C# 데스크톱 앱 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-146">In the current Visual Studio solution, create a Visual C# Desktop App project by using the **Console Application** project template.</span></span> <span data-ttu-id="18df4-147">프로젝트 **SendCloudToDevice**의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-147">Name the project **SendCloudToDevice**.</span></span>
   
    ![Visual Studio의 새 프로젝트][20]
2. <span data-ttu-id="18df4-149">솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭한 후 **Manage NuGet Packages for Solution...(솔루션에 대한 NuGet 패키지 관리...)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-149">In Solution Explorer, right-click the solution, and then click **Manage NuGet Packages for Solution...**.</span></span> 
   
    <span data-ttu-id="18df4-150">이 작업은 **NuGet 패키지 관리** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-150">This action opens the **Manage NuGet Packages** window.</span></span>
3. <span data-ttu-id="18df4-151">**Microsoft.Azure.Devices**를 검색하여 **설치**를 클릭하고 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-151">Search for **Microsoft.Azure.Devices**, click **Install**, and accept the terms of use.</span></span> 
   
    <span data-ttu-id="18df4-152">그러면 [Azure IoT 서비스 SDK NuGet 패키지]가 다운로드 및 설치되고 해당 참조가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-152">This downloads, installs, and adds a reference to the [Azure IoT service SDK NuGet package].</span></span>

4. <span data-ttu-id="18df4-153">**Program.cs** 파일 위에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-153">Add the following `using` statement at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="18df4-154">**Program** 클래스에 다음 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="18df4-155">자리 표시자 값을 [IoT Hub 시작하기]에서 만든 IoT Hub 연결 문자열로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-155">Substitute the placeholder value with the IoT hub connection string from [Get started with IoT Hub]:</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="18df4-156">**Program** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-156">Add the following method to the **Program** class:</span></span>
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud to device message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    <span data-ttu-id="18df4-157">이 메서드는 새 클라우드-장치 메시지를 ID `myFirstDevice`를 사용하여 장치에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-157">This method sends a new cloud-to-device message to the device with the ID, `myFirstDevice`.</span></span> <span data-ttu-id="18df4-158">이 매개 변수를 [IoT Hub 시작하기]에서 사용한 값으로 수정한 경우에만 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-158">Change this parameter only if you modified it from the one used in [Get started with IoT Hub].</span></span>
7. <span data-ttu-id="18df4-159">마지막으로 **Main** 메서드에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-159">Finally, add the following lines to the **Main** method:</span></span>
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key to send a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="18df4-160">Visual Studio 내에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **시작 프로젝트 설정...**을 선택합니다. **여러 시작 프로젝트**를 선택한 다음 **ReadDeviceToCloudMessages**, **SimulatedDevice** 및 **SendCloudToDevice**에 대한 **시작** 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-160">From within Visual Studio, right-click your solution, and select **Set StartUp projects...**. Select **Multiple startup projects**, then select the **Start** action for **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **SendCloudToDevice**.</span></span>
9. <span data-ttu-id="18df4-161">**F5**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-161">Press **F5**.</span></span> <span data-ttu-id="18df4-162">세 응용 프로그램이 모두 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-162">All three applications should start.</span></span> <span data-ttu-id="18df4-163">**SendCloudToDevice** 창을 선택하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-163">Select the **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="18df4-164">장치 앱에서 수신하고 있는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-164">You should see the message being received by the device app.</span></span>
   
   ![앱 메시지 수신][21]

## <a name="receive-delivery-feedback"></a><span data-ttu-id="18df4-166">배달 피드백 받기</span><span class="sxs-lookup"><span data-stu-id="18df4-166">Receive delivery feedback</span></span>
<span data-ttu-id="18df4-167">각 클라우드-장치 메시지에 대해 배달(또는 만료) 승인을 IoT Hub에 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-167">It is possible to request delivery (or expiration) acknowledgements from IoT Hub for each cloud-to-device message.</span></span> <span data-ttu-id="18df4-168">이 옵션을 사용하면 솔루션 백 엔드에서 다시 시도 또는 보정 논리를 쉽게 알릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-168">This option enables the solution back end to easily inform retry or compensation logic.</span></span> <span data-ttu-id="18df4-169">클라우드-장치 피드백에 대한 자세한 내용은 [IoT Hub 개발자 가이드][IoT Hub developer guide - C2D]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18df4-169">For more information about cloud-to-device feedback, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="18df4-170">이 섹션에서는 **SendCloudToDevice** 앱을 수정하여 피드백을 요청하고 IoT Hub로부터 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-170">In this section, you modify the **SendCloudToDevice** app to request feedback, and receive it from IoT Hub.</span></span>

1. <span data-ttu-id="18df4-171">Visual Studio의 **SendCloudToDevice** 프로젝트의 **Program** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-171">In Visual Studio, in the **SendCloudToDevice** project, add the following method to the **Program** class.</span></span>
   
        private async static void ReceiveFeedbackAsync()
        {
            var feedbackReceiver = serviceClient.GetFeedbackReceiver();
   
            Console.WriteLine("\nReceiving c2d feedback from service");
            while (true)
            {
                var feedbackBatch = await feedbackReceiver.ReceiveAsync();
                if (feedbackBatch == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received feedback: {0}", string.Join(", ", feedbackBatch.Records.Select(f => f.StatusCode)));
                Console.ResetColor();
   
                await feedbackReceiver.CompleteAsync(feedbackBatch);
            }
        }
   
    <span data-ttu-id="18df4-172">수신 패턴은 장치 앱으로부터 클라우드-장치 메시지를 받는 데 사용되는 것과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-172">Note this receive pattern is the same one used to receive cloud-to-device messages from the device app.</span></span>
2. <span data-ttu-id="18df4-173">**Main** 메서드에서 `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` 줄 바로 뒤에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-173">Add the following method in the **Main** method, right after the `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` line:</span></span>
   
        ReceiveFeedbackAsync();
3. <span data-ttu-id="18df4-174">클라우드-장치 메시지 배달에 대한 피드백을 요청하려면 **SendCloudToDeviceMessageAsync** 메서드에서 속성을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-174">To request feedback for the delivery of your cloud-to-device message, you have to specify a property in the **SendCloudToDeviceMessageAsync** method.</span></span> <span data-ttu-id="18df4-175">`var commandMessage = new Message(...);` 줄 바로 뒤에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-175">Add the following line, right after the `var commandMessage = new Message(...);` line:</span></span>
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. <span data-ttu-id="18df4-176">**F5** 키를 눌러 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-176">Run the apps by pressing **F5**.</span></span> <span data-ttu-id="18df4-177">세 응용 프로그램이 모두 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-177">You should see all three applications start.</span></span> <span data-ttu-id="18df4-178">**SendCloudToDevice** 창을 선택하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-178">Select the **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="18df4-179">장치 앱에서 메시지를 수신하는 것이 확인됩니다. 몇 초 후에 **SendCloudToDevice** 응용 프로그램에서 피드백 메시지를 수신하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-179">You should see the message being received by the device app, and after a few seconds, the feedback message being received by your **SendCloudToDevice** application.</span></span>
   
   ![앱 메시지 수신][22]

> [!NOTE]
> <span data-ttu-id="18df4-181">간단히 하기 위해 이 자습서에서는 재시도 정책을 구현하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-181">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="18df4-182">프로덕션 코드에서는 MSDN 문서 [일시적인 오류 처리]에서 제시한 대로 재시도 정책(예: 지수 백오프)을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-182">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="18df4-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="18df4-183">Next steps</span></span>
<span data-ttu-id="18df4-184">이 자습서에서 클라우드-장치 메시지를 보내고 받는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="18df4-184">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="18df4-185">IoT Hub를 사용하는 전체 종단 간 솔루션의 예를 보려면 [Azure IoT Suite]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18df4-185">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="18df4-186">IoT Hub를 사용하여 솔루션을 개발하는 방법에 대한 자세한 내용은 [IoT Hub 개발자 가이드]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18df4-186">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[Azure IoT 서비스 SDK NuGet 패키지]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[일시적인 오류 처리]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[IoT Hub 개발자 가이드]: iot-hub-devguide.md
[IoT Hub 시작하기]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure IoT Suite]: https://docs.microsoft.com/en-us/azure/iot-suite/
[Azure IoT 장치 SDK]: iot-hub-devguide-sdks.md
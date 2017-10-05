---
title: "Azure IoT Hub(노드)를 사용한 클라우드-장치 메시지 | Microsoft Docs"
description: "Node.js용 Azure IoT SDK를 사용하여 Azure IoT Hub에서 클라우드-장치 메시지를 보내는 방법입니다. 클라우드-장치 메시지를 수신하도록 시뮬레이션된 장치 앱을 수정하고 클라우드-장치 메시지를 보내도록 백 엔드 앱을 수정합니다."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3ca8a78f-ade2-46e8-8a49-d5d599cdf1f1
ms.service: iot-hub
ms.devlang: javascript
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 4580bda5633f84a7c7af0dc85f3cea4951024836
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a><span data-ttu-id="a6dd4-104">IoT Hub(노드)를 사용하여 클라우드-장치 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="a6dd4-104">Send cloud-to-device messages with IoT Hub (Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="a6dd4-105">소개</span><span class="sxs-lookup"><span data-stu-id="a6dd4-105">Introduction</span></span>
<span data-ttu-id="a6dd4-106">Azure IoT Hub는 수백만 개의 장치와 솔루션 백 엔드 간에 안정적이고 안전한 양방향 통신이 가능하도록 지원하는 완전히 관리되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="a6dd4-107">[IoT Hub 시작하기] 자습서에서는 IoT Hub를 만들고 그 안에 장치 ID를 프로비전하고 장치-클라우드 메시지를 보내는 시뮬레이션된 장치 앱을 코딩하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="a6dd4-108">이 자습서는 [IoT Hub 시작하기]를 토대로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="a6dd4-109">이 항목에서는 다음 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-109">It shows you how to:</span></span>

* <span data-ttu-id="a6dd4-110">솔루션 백 엔드에서 IoT Hub를 통해 클라우드-장치 메시지를 단일 장치로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="a6dd4-111">장치에서 클라우드-장치 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="a6dd4-112">솔루션 백 엔드에서, IoT Hub에서 장치로 보낸 메시지에 대한 배달 확인(*피드백*)을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="a6dd4-113">클라우드-장치 메시지에 자세한 내용은 [IoT Hub 개발자 가이드][IoT Hub developer guide - C2D]에서 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="a6dd4-114">이 자습서의 끝 부분에서는 다음 두 개의 Node.js 콘솔 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-114">At the end of this tutorial, you run two Node.js console apps:</span></span>

* <span data-ttu-id="a6dd4-115">**SimulatedDevice**, [IoT Hub 시작하기]에서 만든 앱의 수정된 버전으로서 IoT Hub에 연결하고 클라우드-장치 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-115">**SimulatedDevice**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="a6dd4-116">**SendCloudToDeviceMessage**, IoT Hub를 통해 시뮬레이션된 장치 앱에 클라우드-장치 메시지를 보낸 다음 배달 승인을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-116">**SendCloudToDeviceMessage**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="a6dd4-117">IoT Hub는 많은 장치 플랫폼 및 언어(C, Java 및 Javascript 포함)를 위해 비록 Azure IoT 장치 SDK이지만 SDK를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="a6dd4-118">이 자습서의 코드 및 일반적으로 Azure IoT Hub에 장치를 연결하는 방법에 대한 단계별 지침은 [Azure IoT 개발자 센터]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="a6dd4-119">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="a6dd4-120">Node.js 버전 0.10.x 이상</span><span class="sxs-lookup"><span data-stu-id="a6dd4-120">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="a6dd4-121">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-121">An active Azure account.</span></span> <span data-ttu-id="a6dd4-122">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-simulated-device-app"></a><span data-ttu-id="a6dd4-123">시뮬레이션된 장치 앱에서 메시지 수신</span><span class="sxs-lookup"><span data-stu-id="a6dd4-123">Receive messages in the simulated device app</span></span>
<span data-ttu-id="a6dd4-124">이 섹션에서는 [IoT Hub 시작하기]에서 만든 시뮬레이션된 장치 앱을 수정하여 IoT Hub로부터 클라우드-장치 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-124">In this section, you modify the simulated device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="a6dd4-125">텍스트 편집기를 사용하여 SimulatedDevice.js 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-125">Using a text editor, open the SimulatedDevice.js file.</span></span>
2. <span data-ttu-id="a6dd4-126">IoT Hub에서 전송된 메시지를 처리하도록 **connectCallback** 함수를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-126">Modify the **connectCallback** function to handle messages sent from IoT Hub.</span></span> <span data-ttu-id="a6dd4-127">이 예제에서는 장치가 항상 **complete** 함수를 호출하여 메시지를 처리했음을 IoT Hub에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-127">In this example, the device always invokes the **complete** function to notify IoT Hub that it has processed the message.</span></span> <span data-ttu-id="a6dd4-128">**connectCallback** 함수의 새 버전은 다음 코드 조각과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-128">Your new version of the **connectCallback** function looks like the following snippet:</span></span>
   
    ```javascript
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
        client.on('message', function (msg) {
          console.log('Id: ' + msg.messageId + ' Body: ' + msg.data);
          client.complete(msg, printResultFor('completed'));
        });
        // Create a message and send it to the IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
   
   > [!NOTE]
   > <span data-ttu-id="a6dd4-129">전송으로 MQTT 또는 AMQP 대신 HTTP을 사용하는 경우 **DeviceClient** 인스턴스는 IoT Hub의 메시지를 자주(25분 미만 간격으로) 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-129">If you use HTTP instead of MQTT or AMQP as the transport, the **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="a6dd4-130">MQTT, AMQP 및 HTTP 지원과 IoT Hub 제한 간의 차이점에 대한 자세한 내용은 [IoT Hub 개발자 가이드][IoT Hub developer guide - C2D]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-130">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="a6dd4-131">클라우드-장치 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="a6dd4-131">Send a cloud-to-device message</span></span>
<span data-ttu-id="a6dd4-132">이 섹션에서는 클라우드-장치 메시지를 시뮬레이트된 장치 앱으로 보내는 Node.js 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-132">In this section, you create a Node.js console app that sends cloud-to-device messages to the simulated device app.</span></span> <span data-ttu-id="a6dd4-133">[IoT Hub 시작하기] 자습서에서 추가한 장치의 장치 ID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-133">You need the device ID of the device you added in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="a6dd4-134">[Azure Portal]에서 찾을 수 있는 허브에 대한 IoT Hub 연결 문자열도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-134">You also need the IoT Hub connection string for your hub that you can find in the [Azure portal].</span></span>

1. <span data-ttu-id="a6dd4-135">**sendcloudtodevicemessage**라는 빈 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-135">Create an empty folder called **sendcloudtodevicemessage**.</span></span> <span data-ttu-id="a6dd4-136">**sendcloudtodevicemessage** 폴더의 명령 프롬프트에서 다음 명령을 사용하여 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-136">In the **sendcloudtodevicemessage** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="a6dd4-137">모든 기본값을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-137">Accept all the defaults:</span></span>
   
    ```shell
    npm init
    ```
2. <span data-ttu-id="a6dd4-138">**sendcloudtodevicemessage** 폴더의 명령 프롬프트에서 다음 명령을 실행하여 **azure-iothub** 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-138">At your command prompt in the **sendcloudtodevicemessage** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```shell
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="a6dd4-139">텍스트 편집기를 사용하여 **sendcloudtodevicemessage** 폴더에 **SendCloudToDeviceMessage.js** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-139">Using a text editor, create a **SendCloudToDeviceMessage.js** file in the **sendcloudtodevicemessage** folder.</span></span>
4. <span data-ttu-id="a6dd4-140">**SendCloudToDeviceMessage.js** 파일 앞에 다음 `require` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-140">Add the following `require` statements at the start of the **SendCloudToDeviceMessage.js** file:</span></span>
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. <span data-ttu-id="a6dd4-141">**SendCloudToDeviceMessage.js** 파일에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-141">Add the following code to **SendCloudToDeviceMessage.js** file.</span></span> <span data-ttu-id="a6dd4-142">“{iot hub connection string}” 자리 표시자 값을 [IoT Hub 시작하기] 자습서에서 만든 허브에 대한 IoT Hub 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-142">Replace the "{iot hub connection string}" placeholder value with the IoT Hub connection string for the hub you created in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="a6dd4-143">“{device id}” 자리 표시자 값을 [IoT Hub 시작하기] 자습서에서 추가한 장치의 장치 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-143">Replace the "{device id}" placeholder with the device ID of the device you added in the [Get started with IoT Hub] tutorial:</span></span>
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="a6dd4-144">다음 함수를 추가하여 작업 결과를 콘솔에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-144">Add the following function to print operation results to the console:</span></span>
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="a6dd4-145">다음 함수를 추가하여 배달 피드백 메시지를 콘솔에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-145">Add the following function to print delivery feedback messages to the console:</span></span>
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. <span data-ttu-id="a6dd4-146">다음 코드를 추가하여 장치에 메시지를 보내고 장치가 클라우드-장치 메시지를 승인할 때 피드백 메시지를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-146">Add the following code to send a message to your device and handle the feedback message when the device acknowledges the cloud-to-device message:</span></span>
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud to device message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. <span data-ttu-id="a6dd4-147">**SendCloudToDeviceMessage.js** 파일을 저장한 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-147">Save and close **SendCloudToDeviceMessage.js** file.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="a6dd4-148">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="a6dd4-148">Run the applications</span></span>
<span data-ttu-id="a6dd4-149">이제 응용 프로그램을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-149">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="a6dd4-150">**simulateddevice** 폴더의 명령 프롬프트에서 다음 명령을 실행하여 IoT Hub에 원격 분석을 보내고 클라우드-장치 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-150">At the command prompt in the **simulateddevice** folder, run the following command to send telemetry to IoT Hub and to listen for cloud-to-device messages:</span></span>
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![시뮬레이션된 장치 앱 실행][img-simulated-device]
2. <span data-ttu-id="a6dd4-152">명령 프롬프트의 **sendcloudtodevicemessage** 폴더에서 다음 명령을 실행하여 클라우드-장치 메시지를 보내고 승인 피드백을 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-152">At a command prompt in the **sendcloudtodevicemessage** folder, run the following command to send a cloud-to-device message and wait for the acknowledgment feedback:</span></span>
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![앱을 실행하여 클라우드-장치 명령 보내기][img-send-command]
   
   > [!NOTE]
   > <span data-ttu-id="a6dd4-154">간단히 하기 위해 이 자습서에서는 재시도 정책을 구현하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-154">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="a6dd4-155">프로덕션 코드에서는 MSDN 문서 [일시적인 오류 처리]에서 제시한 대로 재시도 정책(예: 지수 백오프)을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-155">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="a6dd4-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a6dd4-156">Next steps</span></span>
<span data-ttu-id="a6dd4-157">이 자습서에서 클라우드-장치 메시지를 보내고 받는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-157">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="a6dd4-158">IoT Hub를 사용하는 전체 종단 간 솔루션의 예를 보려면 [Azure IoT Suite]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-158">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="a6dd4-159">IoT Hub를 사용하여 솔루션을 개발하는 방법에 대한 자세한 내용은 [IoT Hub 개발자 가이드]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6dd4-159">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

<span data-ttu-id="a6dd4-160">[IoT Hub 시작하기]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="a6dd4-160">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
<span data-ttu-id="a6dd4-161">[IoT Hub 개발자 가이드]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="a6dd4-161">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="a6dd4-162">[Azure IoT 개발자 센터]: http://www.azure.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="a6dd4-162">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span></span>
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
<span data-ttu-id="a6dd4-163">[일시적인 오류 처리]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="a6dd4-163">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
<span data-ttu-id="a6dd4-164">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="a6dd4-164">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="a6dd4-165">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span><span class="sxs-lookup"><span data-stu-id="a6dd4-165">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span></span>

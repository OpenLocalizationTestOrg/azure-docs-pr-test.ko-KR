---
title: "Azure IoT Hub (노드)와 aaaCloud-장치 메시지 | Microsoft Docs"
description: "어떻게 toosend 클라우드-장치 메시지 tooa 장치 hello Azure IoT Sdk를 사용 하 여 Node.js 용 Azure IoT 허브에서 설정 합니다. 시뮬레이션 된 장치 앱 tooreceive 클라우드-장치 메시지를 수정 하 고 백 엔드 응용 프로그램 toosend hello 클라우드-장치 메시지를 수정 합니다."
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
ms.openlocfilehash: 1ccae0cada52193c2abb91504c086cac226e93da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a><span data-ttu-id="4621a-104">IoT Hub(노드)를 사용하여 클라우드-장치 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="4621a-104">Send cloud-to-device messages with IoT Hub (Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="4621a-105">소개</span><span class="sxs-lookup"><span data-stu-id="4621a-105">Introduction</span></span>
<span data-ttu-id="4621a-106">Azure IoT Hub는 수백만 개의 장치와 솔루션 백 엔드 간에 안정적이고 안전한 양방향 통신이 가능하도록 지원하는 완전히 관리되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="4621a-107">hello [IoT 허브 시작] toocreate IoT hub, 장치 id를 프로 비전 하 고 장치-클라우드 메시지를 보내는 시뮬레이션 된 장치 앱을 코딩 하는 방법을 보여 주는 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-107">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="4621a-108">이 자습서는 [IoT 허브 시작]를 토대로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="4621a-109">이 항목에서는 다음 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-109">It shows you how to:</span></span>

* <span data-ttu-id="4621a-110">솔루션 백 엔드에서 IoT 허브를 통해 tooa 단일 장치를 클라우드-장치 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-110">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="4621a-111">장치에서 클라우드-장치 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="4621a-112">솔루션 백 엔드에서 배달 확인 요청 (*피드백*) IoT 허브에서 메시지 보내는 tooa 장치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="4621a-113">Hello에서 클라우드-장치 메시지에서 자세한 정보를 찾을 수 있습니다 [IoT 허브 개발자 가이드][IoT Hub developer guide - C2D]합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-113">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="4621a-114">이 자습서의 hello 끝 두 Node.js 콘솔 응용 프로그램 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-114">At hello end of this tutorial, you run two Node.js console apps:</span></span>

* <span data-ttu-id="4621a-115">**SimulatedDevice**, 수정 된 버전에서 만든 hello 앱의 [IoT 허브 시작], tooyour IoT 허브를 연결 하 고 클라우드-장치 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-115">**SimulatedDevice**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="4621a-116">**SendCloudToDeviceMessage**는 IoT 허브를 통해 클라우드-장치 메시지 toohello 시뮬레이션 된 장치 앱을 보내고 해당 배달 승인을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-116">**SendCloudToDeviceMessage**, which sends a cloud-to-device message toohello simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="4621a-117">IoT Hub는 많은 장치 플랫폼 및 언어(C, Java 및 Javascript 포함)를 위해 비록 Azure IoT 장치 SDK이지만 SDK를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="4621a-118">에 대 한 단계별 지침은 tooconnect 장치 toothis 자습서의 코드 및 일반적으로 tooAzure IoT Hub를 확인 하려면 어떻게 hello [Azure IoT 개발자 센터]합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-118">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="4621a-119">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="4621a-119">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="4621a-120">Node.js 버전 0.10.x 이상</span><span class="sxs-lookup"><span data-stu-id="4621a-120">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="4621a-121">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="4621a-121">An active Azure account.</span></span> <span data-ttu-id="4621a-122">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-simulated-device-app"></a><span data-ttu-id="4621a-123">Hello 시뮬레이션 된 장치 응용 프로그램에서 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-123">Receive messages in hello simulated device app</span></span>
<span data-ttu-id="4621a-124">Hello 시뮬레이션 된 장치 응용 프로그램에서 만든이 섹션에서 수정 [IoT 허브 시작] hello IoT hub에서 클라우드-장치 메시지 tooreceive 합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-124">In this section, you modify hello simulated device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="4621a-125">텍스트 편집기를 사용 하 여 hello SimulatedDevice.js 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-125">Using a text editor, open hello SimulatedDevice.js file.</span></span>
2. <span data-ttu-id="4621a-126">Hello 수정 **connectCallback** IoT 허브에서 보낸 toohandle 메시지 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-126">Modify hello **connectCallback** function toohandle messages sent from IoT Hub.</span></span> <span data-ttu-id="4621a-127">이 예제에서는 hello 장치 항상 호출 hello **완료** toonotify hello 메시지를 처리 한 IoT Hub 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-127">In this example, hello device always invokes hello **complete** function toonotify IoT Hub that it has processed hello message.</span></span> <span data-ttu-id="4621a-128">새 버전의 hello **connectCallback** 함수 조각 다음 hello와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-128">Your new version of hello **connectCallback** function looks like hello following snippet:</span></span>
   
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
        // Create a message and send it toohello IoT Hub every second
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
   > <span data-ttu-id="4621a-129">MQTT 또는 AMQP 대신 hello 전송으로 HTTP를 사용 하는 경우 hello **DeviceClient** 인스턴스 IoT 허브에 자주 사용 (모든 25 분 내)에서 메시지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-129">If you use HTTP instead of MQTT or AMQP as hello transport, hello **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="4621a-130">Hello 차이 MQTT, AMQP 및 HTTP 지원 및 IoT Hub 제한에 대 한 자세한 내용은 참조 hello [IoT 허브 개발자 가이드][IoT Hub developer guide - C2D]합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-130">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="4621a-131">클라우드-장치 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="4621a-131">Send a cloud-to-device message</span></span>
<span data-ttu-id="4621a-132">이 섹션에서는 클라우드-장치 메시지 toohello 시뮬레이션 된 장치 응용 프로그램에서 전송 하 여 Node.js 콘솔 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-132">In this section, you create a Node.js console app that sends cloud-to-device messages toohello simulated device app.</span></span> <span data-ttu-id="4621a-133">Hello에 추가 하는 hello 장치의 장치 ID hello 필요 [IoT 허브 시작] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-133">You need hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="4621a-134">또한 hello에서 찾을 수 있는 허브에 대 한 연결 문자열 IoT Hub를 hello 필요 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-134">You also need hello IoT Hub connection string for your hub that you can find in hello [Azure portal].</span></span>

1. <span data-ttu-id="4621a-135">**sendcloudtodevicemessage**라는 빈 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-135">Create an empty folder called **sendcloudtodevicemessage**.</span></span> <span data-ttu-id="4621a-136">Hello에 **sendcloudtodevicemessage** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-136">In hello **sendcloudtodevicemessage** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="4621a-137">모든 hello 기본값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-137">Accept all hello defaults:</span></span>
   
    ```shell
    npm init
    ```
2. <span data-ttu-id="4621a-138">Hello에 명령 프롬프트에 **sendcloudtodevicemessage** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iothub** 패키지:</span><span class="sxs-lookup"><span data-stu-id="4621a-138">At your command prompt in hello **sendcloudtodevicemessage** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```shell
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="4621a-139">텍스트 편집기를 사용 하 여 만들는 **SendCloudToDeviceMessage.js** hello에 대 한 파일 **sendcloudtodevicemessage** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-139">Using a text editor, create a **SendCloudToDeviceMessage.js** file in hello **sendcloudtodevicemessage** folder.</span></span>
4. <span data-ttu-id="4621a-140">Hello 다음 추가 `require` hello의 시작 부분에 hello 문을 **SendCloudToDeviceMessage.js** 파일:</span><span class="sxs-lookup"><span data-stu-id="4621a-140">Add hello following `require` statements at hello start of hello **SendCloudToDeviceMessage.js** file:</span></span>
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. <span data-ttu-id="4621a-141">추가 코드를 너무 다음 hello**SendCloudToDeviceMessage.js** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-141">Add hello following code too**SendCloudToDeviceMessage.js** file.</span></span> <span data-ttu-id="4621a-142">Hello hello에서 만든 hello 허브에 대 한 IoT 허브 연결 문자열에 "{iot 허브 연결 문자열을 (를)" hello 자리 표시자 값을 바꿉니다 [IoT 허브 시작] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-142">Replace hello "{iot hub connection string}" placeholder value with hello IoT Hub connection string for hello hub you created in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="4621a-143">Hello에 추가 하는 hello 장치의 hello 장치 ID "{장치 id}" hello 자리 표시자를 바꿉니다 [IoT 허브 시작] 자습서:</span><span class="sxs-lookup"><span data-stu-id="4621a-143">Replace hello "{device id}" placeholder with hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial:</span></span>
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="4621a-144">다음 함수 tooprint 작업 결과 toohello 콘솔 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-144">Add hello following function tooprint operation results toohello console:</span></span>
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="4621a-145">다음 함수 tooprint 배달 피드백 메시지 toohello 콘솔 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-145">Add hello following function tooprint delivery feedback messages toohello console:</span></span>
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. <span data-ttu-id="4621a-146">Hello 다음 toosend 메시지 tooyour 장치를 코드로 바꾸고 hello 장치 hello 클라우드-장치 메시지를 승인 하는 경우 hello 피드백 메시지 처리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-146">Add hello following code toosend a message tooyour device and handle hello feedback message when hello device acknowledges hello cloud-to-device message:</span></span>
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud toodevice message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. <span data-ttu-id="4621a-147">**SendCloudToDeviceMessage.js** 파일을 저장한 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-147">Save and close **SendCloudToDeviceMessage.js** file.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="4621a-148">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="4621a-148">Run hello applications</span></span>
<span data-ttu-id="4621a-149">준비 toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-149">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="4621a-150">Hello에 대 한 hello 명령 프롬프트 **simulateddevice** 폴더를 hello 다음 실행 명령 toosend 원격 분석 tooIoT 허브과 클라우드-장치 메시지에 대 한 toolisten:</span><span class="sxs-lookup"><span data-stu-id="4621a-150">At hello command prompt in hello **simulateddevice** folder, run hello following command toosend telemetry tooIoT Hub and toolisten for cloud-to-device messages:</span></span>
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Hello 시뮬레이션 된 장치 앱 실행][img-simulated-device]
2. <span data-ttu-id="4621a-152">Hello에 명령 프롬프트에서 **sendcloudtodevicemessage** 폴더를 다음 명령 toosend hello 클라우드-장치 메시지를 실행 하 고 hello 승인 피드백에 대 한 대기:</span><span class="sxs-lookup"><span data-stu-id="4621a-152">At a command prompt in hello **sendcloudtodevicemessage** folder, run hello following command toosend a cloud-to-device message and wait for hello acknowledgment feedback:</span></span>
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Hello 응용 프로그램 toosend hello 클라우드-장치 명령 실행][img-send-command]
   
   > [!NOTE]
   > <span data-ttu-id="4621a-154">간단히 하기 위해 이 자습서에서는 재시도 정책을 구현하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-154">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="4621a-155">프로덕션 코드에 다시 시도 정책 (예: 지 수 형식의 백오프) hello MSDN 문서에 설명 된 대로 구현 해야 [일시적인 오류 처리]합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-155">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="4621a-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4621a-156">Next steps</span></span>
<span data-ttu-id="4621a-157">이 자습서에서는 방법에 대해 배웠습니다 toosend 및 클라우드-장치 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-157">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="4621a-158">IoT 허브를 사용 하는 완벽 한 종단 간 솔루션의 toosee 예 참조 [Azure IoT Suite]합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-158">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="4621a-159">IoT 허브를 사용 하 여 솔루션 개발에 대 한 더 toolearn 참조 hello [IoT 허브 개발자 가이드]합니다.</span><span class="sxs-lookup"><span data-stu-id="4621a-159">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

[IoT 허브 시작]: iot-hub-node-node-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[IoT 허브 개발자 가이드]: iot-hub-devguide.md
[Azure IoT 개발자 센터]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[일시적인 오류 처리]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure 포털]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/

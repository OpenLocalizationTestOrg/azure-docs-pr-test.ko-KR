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
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a>IoT Hub(노드)를 사용하여 클라우드-장치 메시지 보내기
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a>소개
Azure IoT Hub는 수백만 개의 장치와 솔루션 백 엔드 간에 안정적이고 안전한 양방향 통신이 가능하도록 지원하는 완전히 관리되는 서비스입니다. hello [IoT 허브 시작] toocreate IoT hub, 장치 id를 프로 비전 하 고 장치-클라우드 메시지를 보내는 시뮬레이션 된 장치 앱을 코딩 하는 방법을 보여 주는 자습서입니다.

이 자습서는 [IoT 허브 시작]를 토대로 작성되었습니다. 이 항목에서는 다음 방법을 설명합니다.

* 솔루션 백 엔드에서 IoT 허브를 통해 tooa 단일 장치를 클라우드-장치 메시지를 보냅니다.
* 장치에서 클라우드-장치 메시지를 받습니다.
* 솔루션 백 엔드에서 배달 확인 요청 (*피드백*) IoT 허브에서 메시지 보내는 tooa 장치에 대 한 합니다.

Hello에서 클라우드-장치 메시지에서 자세한 정보를 찾을 수 있습니다 [IoT 허브 개발자 가이드][IoT Hub developer guide - C2D]합니다.

이 자습서의 hello 끝 두 Node.js 콘솔 응용 프로그램 실행합니다.

* **SimulatedDevice**, 수정 된 버전에서 만든 hello 앱의 [IoT 허브 시작], tooyour IoT 허브를 연결 하 고 클라우드-장치 메시지를 수신 합니다.
* **SendCloudToDeviceMessage**는 IoT 허브를 통해 클라우드-장치 메시지 toohello 시뮬레이션 된 장치 앱을 보내고 해당 배달 승인을 받습니다.

> [!NOTE]
> IoT Hub는 많은 장치 플랫폼 및 언어(C, Java 및 Javascript 포함)를 위해 비록 Azure IoT 장치 SDK이지만 SDK를 지원합니다. 에 대 한 단계별 지침은 tooconnect 장치 toothis 자습서의 코드 및 일반적으로 tooAzure IoT Hub를 확인 하려면 어떻게 hello [Azure IoT 개발자 센터]합니다.
> 
> 

toocomplete이이 자습서에서는 다음 hello 필요:

* Node.js 버전 0.10.x 이상
* 활성 Azure 계정. 계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.

## <a name="receive-messages-in-hello-simulated-device-app"></a>Hello 시뮬레이션 된 장치 응용 프로그램에서 메시지를 수신 합니다.
Hello 시뮬레이션 된 장치 응용 프로그램에서 만든이 섹션에서 수정 [IoT 허브 시작] hello IoT hub에서 클라우드-장치 메시지 tooreceive 합니다.

1. 텍스트 편집기를 사용 하 여 hello SimulatedDevice.js 파일을 엽니다.
2. Hello 수정 **connectCallback** IoT 허브에서 보낸 toohandle 메시지 작동 합니다. 이 예제에서는 hello 장치 항상 호출 hello **완료** toonotify hello 메시지를 처리 한 IoT Hub 작동 합니다. 새 버전의 hello **connectCallback** 함수 조각 다음 hello와 유사 합니다.
   
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
   > MQTT 또는 AMQP 대신 hello 전송으로 HTTP를 사용 하는 경우 hello **DeviceClient** 인스턴스 IoT 허브에 자주 사용 (모든 25 분 내)에서 메시지를 확인 합니다. Hello 차이 MQTT, AMQP 및 HTTP 지원 및 IoT Hub 제한에 대 한 자세한 내용은 참조 hello [IoT 허브 개발자 가이드][IoT Hub developer guide - C2D]합니다.
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a>클라우드-장치 메시지 보내기
이 섹션에서는 클라우드-장치 메시지 toohello 시뮬레이션 된 장치 응용 프로그램에서 전송 하 여 Node.js 콘솔 응용 프로그램을 만들 수 있습니다. Hello에 추가 하는 hello 장치의 장치 ID hello 필요 [IoT 허브 시작] 자습서입니다. 또한 hello에서 찾을 수 있는 허브에 대 한 연결 문자열 IoT Hub를 hello 필요 [Azure 포털]합니다.

1. **sendcloudtodevicemessage**라는 빈 폴더를 만듭니다. Hello에 **sendcloudtodevicemessage** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 package.json 파일을 만듭니다. 모든 hello 기본값을 적용 합니다.
   
    ```shell
    npm init
    ```
2. Hello에 명령 프롬프트에 **sendcloudtodevicemessage** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iothub** 패키지:
   
    ```shell
    npm install azure-iothub --save
    ```
3. 텍스트 편집기를 사용 하 여 만들는 **SendCloudToDeviceMessage.js** hello에 대 한 파일 **sendcloudtodevicemessage** 폴더입니다.
4. Hello 다음 추가 `require` hello의 시작 부분에 hello 문을 **SendCloudToDeviceMessage.js** 파일:
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. 추가 코드를 너무 다음 hello**SendCloudToDeviceMessage.js** 파일입니다. Hello hello에서 만든 hello 허브에 대 한 IoT 허브 연결 문자열에 "{iot 허브 연결 문자열을 (를)" hello 자리 표시자 값을 바꿉니다 [IoT 허브 시작] 자습서입니다. Hello에 추가 하는 hello 장치의 hello 장치 ID "{장치 id}" hello 자리 표시자를 바꿉니다 [IoT 허브 시작] 자습서:
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. 다음 함수 tooprint 작업 결과 toohello 콘솔 hello를 추가 합니다.
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. 다음 함수 tooprint 배달 피드백 메시지 toohello 콘솔 hello를 추가 합니다.
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. Hello 다음 toosend 메시지 tooyour 장치를 코드로 바꾸고 hello 장치 hello 클라우드-장치 메시지를 승인 하는 경우 hello 피드백 메시지 처리를 추가 합니다.
   
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
9. **SendCloudToDeviceMessage.js** 파일을 저장한 후 닫습니다.

## <a name="run-hello-applications"></a>Hello 응용 프로그램 실행
준비 toorun hello 응용 프로그램입니다.

1. Hello에 대 한 hello 명령 프롬프트 **simulateddevice** 폴더를 hello 다음 실행 명령 toosend 원격 분석 tooIoT 허브과 클라우드-장치 메시지에 대 한 toolisten:
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Hello 시뮬레이션 된 장치 앱 실행][img-simulated-device]
2. Hello에 명령 프롬프트에서 **sendcloudtodevicemessage** 폴더를 다음 명령 toosend hello 클라우드-장치 메시지를 실행 하 고 hello 승인 피드백에 대 한 대기:
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Hello 응용 프로그램 toosend hello 클라우드-장치 명령 실행][img-send-command]
   
   > [!NOTE]
   > 간단히 하기 위해 이 자습서에서는 재시도 정책을 구현하지 않습니다. 프로덕션 코드에 다시 시도 정책 (예: 지 수 형식의 백오프) hello MSDN 문서에 설명 된 대로 구현 해야 [일시적인 오류 처리]합니다.
   > 
   > 

## <a name="next-steps"></a>다음 단계
이 자습서에서는 방법에 대해 배웠습니다 toosend 및 클라우드-장치 메시지를 수신 합니다. 

IoT 허브를 사용 하는 완벽 한 종단 간 솔루션의 toosee 예 참조 [Azure IoT Suite]합니다.

IoT 허브를 사용 하 여 솔루션 개발에 대 한 더 toolearn 참조 hello [IoT 허브 개발자 가이드]합니다.

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

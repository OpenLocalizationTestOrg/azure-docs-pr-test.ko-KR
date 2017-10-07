---
title: "IoT Hub aaaAzure 메서드 (노드)를 직접 | Microsoft Docs"
description: "어떻게 toouse Azure IoT Hub는 메서드를 전달 합니다. Node.js tooimplement 직접 메서드를 포함 하는 시뮬레이션 된 장치 앱 및 hello 직접 메서드를 호출 하는 서비스 응용 프로그램에 대 한 hello Azure IoT Sdk를 사용 합니다."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ea9c73ca-7778-4e38-a8f1-0bee9d142f04
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 12300ba451816fec1f80163b633f6b6e411d9e5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a>Node.js와 함께 IoT 장치에서 직접 메서드 사용
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

이 자습서의 hello 끝 두 Node.js 콘솔 응용 프로그램을 사용할 수 있습니다.

* **CallMethodOnDevice.js**, hello 시뮬레이션 된 장치 응용 프로그램의 메서드를 호출 하 고 hello 응답을 표시 합니다.
* **SimulatedDevice.js**, 앞에서 만든 hello 장치 id를 가진 tooyour IoT 허브를 연결 하 고 hello 클라우드 호출한 toohello 메서드 응답 합니다.

> [!NOTE]
> hello 문서 [Azure IoT Sdk] [ lnk-hub-sdks] 사용할 수 있는 toobuild 두 응용 프로그램 toorun 장치와 솔루션 백 엔드에, Azure IoT Sdk hello에 대 한 정보를 제공 합니다.
> 
> 

toocomplete이이 자습서에서는 다음 hello 필요:

* Node.js 버전 0.10.x 이상
* 활성 Azure 계정. 계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>시뮬레이션된 장치 앱 만들기
이 섹션에서는 응답 tooa 메서드 hello 클라우드에서 호출 하 여 Node.js 콘솔 응용 프로그램을 만들 수 있습니다.

1. **simulateddevice**라는 빈 폴더를 새로 만듭니다. Hello에 **simulateddevice** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 package.json 파일을 만듭니다. 모든 hello 기본값을 적용 합니다.
   
    ```
    npm init
    ```
2. Hello에 명령 프롬프트에 **simulateddevice** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iot 장치** 장치 SDK 패키지 및 **azure-iot-장치-mqtt**패키지:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. 텍스트 편집기를 사용 하 여 만드는 새 **SimulatedDevice.js** hello에 대 한 파일 **simulateddevice** 폴더입니다.
4. Hello 다음 추가 `require` hello의 시작 부분에 hello 문을 **SimulatedDevice.js** 파일:
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. 추가 **connectionString** 변수 toocreate를 사용 하는 **DeviceClient** 인스턴스. 대체 **{장치 연결 문자열을 (를)** hello에 생성 된 hello 장치 연결 문자열과 함께 *장치 id를 만드는* 섹션:
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. Hello 함수 tooimplement hello 메서드 hello 장치에서 다음을 추가 합니다.
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. Hello 연결 tooyour IoT 허브를 열고 initialize hello 메서드 수신기를 시작 합니다.
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. 저장 후 닫기 hello **SimulatedDevice.js** 파일입니다.

> [!NOTE]
> 단순 tookeep 항목을이 자습서는 어떠한 재시도 정책도 구현 하지 않습니다. 프로덕션 코드에 다시 시도 정책 (예: 연결 다시 시도) hello MSDN 문서에 설명 된 대로 구현 해야 [일시적인 오류 처리][lnk-transient-faults]합니다.
> 
> 

## <a name="call-a-method-on-a-device"></a>장치에 메서드 호출
이 섹션에서는 다음 hello 응답을 표시 하 고 hello 시뮬레이션 된 장치 응용 프로그램에서 메서드를 호출 하는 Node.js 콘솔 앱을 만듭니다.

1. **callmethodondevice**라는 빈 폴더를 새로 만듭니다. Hello에 **callmethodondevice** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 package.json 파일을 만듭니다. 모든 hello 기본값을 적용 합니다.
   
    ```
    npm init
    ```
2. Hello에 명령 프롬프트에 **callmethodondevice** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iothub** 패키지:
   
    ```
    npm install azure-iothub --save
    ```
3. 텍스트 편집기를 사용 하 여 만들는 **CallMethodOnDevice.js** hello에 대 한 파일 **callmethodondevice** 폴더입니다.
4. Hello 다음 추가 `require` hello의 시작 부분에 hello 문을 **CallMethodOnDevice.js** 파일:
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. 변수 선언 뒤 hello를 추가 하 고 hello 허브에 대 한 IoT 허브 연결 문자열 hello 자리 표시자 값을 바꿉니다.
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. Hello 클라이언트 tooopen hello 연결 tooyour IoT 허브를 만듭니다.
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. 다음 함수 tooinvoke hello 장치 메서드 및 인쇄 hello 장치 응답 toohello 콘솔 hello를 추가 합니다.
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed tooinvoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. 저장 후 닫기 hello **CallMethodOnDevice.js** 파일입니다.

## <a name="run-hello-apps"></a>Hello 앱 실행
준비 toorun hello 앱입니다.

1. Hello에 명령 프롬프트에서 **simulateddevice** hello IoT 허브에서 메서드 호출을 수신 대기 하는 명령 toostart 다음를 실행 하는 폴더:
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. Hello에 명령 프롬프트에서 **callmethodondevice** hello IoT 허브를 모니터링 하는 명령 toobegin 다음를 실행 하는 폴더:
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. Toohello 메서드 출력 hello 메시지와 hello 응용 프로그램 hello 장치에서 hello 메서드 디스플레이 hello 응답을 호출 하 여 대응 하는 hello 장치를 확인할 수 있습니다.
   
    ![][9]

## <a name="next-steps"></a>다음 단계
이 자습서에서는 hello Azure 포털에서에서 새 IoT 허브를 구성 하 고 id 레지스트리에 hello IoT hub에서 장치 id를 만든 다음 합니다. 이 장치 identity tooenable hello 시뮬레이션 된 장치 앱 tooreact toomethods hello 클라우드 호출한 사용 했습니다. 또한 hello 장치에 대 한 메서드를 호출 하 고 hello 장치에서 hello 응답을 표시 하는 응용 프로그램을 만들었습니다. 

시작 toocontinue IoT 허브와 tooexplore 다른 IoT 시나리오를 참조 하세요.

* [IoT Hub 시작]
* [여러 장치에서 jobs 예약][lnk-devguide-jobs]

toolearn tooextend IoT 솔루션 및 일정 메서드를 여러 장치에서 호출 하는 방법 참조 hello [일정 및 브로드캐스트 작업] [ lnk-tutorial-jobs] 자습서입니다.

<!-- Images. -->
[7]: ./media/iot-hub-node-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-node-node-direct-methods/run-callmethodondevice.png
[9]: ./media/iot-hub-node-node-direct-methods/methods-output.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[IoT Hub 시작]: iot-hub-node-node-getstarted.md

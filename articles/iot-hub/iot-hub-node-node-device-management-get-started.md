---
title: "Azure IoT Hub 장치 관리 (노드) aaaGet 시작 | Microsoft Docs"
description: "어떻게 toouse IoT Hub 장치 관리 tooinitiate 원격 장치를 다시 부팅 합니다. Node.js tooimplement 직접 메서드를 포함 하는 시뮬레이션 된 장치 앱 및 hello 직접 메서드를 호출 하는 서비스 응용 프로그램에 대 한 hello Azure IoT SDK를 사용 합니다."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: juanpere
ms.openlocfilehash: 5dd1878e71231850fb95f4170b823f1e86c3ee83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-node"></a>장치 관리 시작(노드)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.

* Azure 포털 toocreate IoT Hub hello를 사용 하 및 IoT 허브에서 장치 id를 만드는 키를 누릅니다.
* 장치를 다시 시작하는 직접 메서드가 포함된 시뮬레이트된 장치 앱을 만듭니다. Hello 클라우드에서 직접 메서드 호출 됩니다.
* IoT 허브를 통해 hello 시뮬레이션 된 장치 응용 프로그램에서 hello 재부팅 직접 메서드를 호출 하 여 Node.js 콘솔 응용 프로그램을 만듭니다.

이 자습서의 hello 끝 두 Node.js 콘솔 응용 프로그램을 사용할 수 있습니다.

**dmpatterns_getstarted_device.js**, 이전에 만든 hello 장치 id를 가진 tooyour IoT 허브를 연결 하는 다시 부팅 직접적인 방법, 실제 다시 부팅을 시뮬레이션 받아 hello 마지막 다시 부팅에 대 한 hello 시간을 보고 합니다.

**dmpatterns_getstarted_service.js**을 hello 응답 표시 hello 시뮬레이션 된 장치 응용 프로그램에서 직접 메서드를 호출 하 하 고 표시 hello 업데이트 속성을 보고 합니다.

toocomplete이이 자습서에서는 다음 hello 필요:

* Node.js 버전 0.12.x 이상, <br/>  [개발 환경을 준비] [ lnk-dev-setup] 설명 방법을 Windows 또는 Linux에서이 자습서에 대 한 tooinstall Node.js 합니다.
* 활성 Azure 계정. 계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>시뮬레이션된 장치 앱 만들기
이 섹션에서는 다음을 수행합니다.

* 응답 tooa 직접적인 방법 hello 클라우드에서 호출 하 여 Node.js 콘솔 응용 프로그램 만들기
* 시뮬레이션된 장치 재부팅 트리거
* 사용 하 여 hello 속성 tooenable 장치로 이중 쿼리 tooidentify 장치 및 마지막 재부팅 될 보고

1. **manageddevice**라는 빈 폴더를 만듭니다.  Hello에 **manageddevice** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 package.json 파일을 만듭니다.  모든 hello 기본값을 적용 합니다.
   
    ```
    npm init
    ```
2. Hello에 명령 프롬프트에 **manageddevice** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iot 장치** 장치 SDK 패키지 및 **azure-iot-장치-mqtt**패키지:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. 텍스트 편집기를 사용 하 여 만들는 **dmpatterns_getstarted_device.js** hello에 대 한 파일 **manageddevice** 폴더입니다.
4. Hello 다음 '필요' hello hello 시작 부분에 설명 추가 **dmpatterns_getstarted_device.js** 파일:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. 추가 **connectionString** 변수 toocreate를 사용 하는 **클라이언트** 인스턴스.  장치 연결 문자열과 함께 hello 연결 문자열을 대체 합니다.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Hello 나오는 hello 장치에 따라 함수 tooimplement hello에 대 한 직접 메서드를 추가 합니다.
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. Hello 연결 tooyour IoT 허브를 열고 hello 직접적인 방법 수신기를 시작 합니다.
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. 저장 후 닫기 hello **dmpatterns_getstarted_device.js** 파일입니다.

> [!NOTE]
> 단순 tookeep 항목을이 자습서는 어떠한 재시도 정책도 구현 하지 않습니다. 프로덕션 코드에서는 hello MSDN 문서에 설명 된 대로 다시 시도 정책 (예: 지 수 백오프)를 구현 해야 [일시적인 오류 처리][lnk-transient-faults]합니다.

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>트리거는 직접 메서드를 사용 하 여 hello 장치에 원격 컴퓨터를 다시 부팅
이 섹션에서는 장치에서 직접 메서드를 사용하여 원격 다시 시작을 시작하는 Node.js 콘솔 앱을 만듭니다. hello 앱 해당 장치에 대 한 장치로 이중 쿼리 toodiscover hello 마지막 부팅 시간을 사용합니다.

1. **triggerrebootondevice**라는 빈 폴더를 만듭니다.  Hello에 **triggerrebootondevice** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 package.json 파일을 만듭니다.  모든 hello 기본값을 적용 합니다.
   
    ```
    npm init
    ```
2. Hello에 명령 프롬프트에 **triggerrebootondevice** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iothub** 장치 SDK 패키지 및 **azure-iot-장치-mqtt** 패키지:
   
    ```
    npm install azure-iothub --save
    ```
3. 텍스트 편집기를 사용 하 여 만들는 **dmpatterns_getstarted_service.js** hello에 대 한 파일 **triggerrebootondevice** 폴더입니다.
4. Hello 다음 '필요' hello hello 시작 부분에 설명 추가 **dmpatterns_getstarted_service.js** 파일:
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. 다음 변수 선언을 hello를 추가 하 고 hello 자리 표시자 값을 바꿉니다.
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. Hello 함수 tooinvoke hello 장치 메서드 tooreboot hello 대상 장치를 다음을 추가 합니다.
   
    ```
    var startRebootDevice = function(twin) {
   
        var methodName = "reboot";
   
        var methodParams = {
            methodName: methodName,
            payload: null,
            timeoutInSeconds: 30
        };
   
        client.invokeDeviceMethod(deviceToReboot, methodParams, function(err, result) {
            if (err) { 
                console.error("Direct method error: "+err.message);
            } else {
                console.log("Successfully invoked hello device tooreboot.");  
            }
        });
    };
    ```
7. Hello 다음 tooquery hello 장치에 대 한 함수 및 hello 마지막 부팅 시간 가져오기 추가:
   
    ```
    var queryTwinLastReboot = function() {
   
        registry.getTwin(deviceToReboot, function(err, twin){
   
            if (twin.properties.reported.iothubDM != null)
            {
                if (err) {
                    console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
                } else {
                    var lastRebootTime = twin.properties.reported.iothubDM.reboot.lastReboot;
                    console.log('Last reboot time: ' + JSON.stringify(lastRebootTime, null, 2));
                }
            } else 
                console.log('Waiting for device tooreport last reboot time.');
        });
    };
    ```
8. Hello hello를 트리거하는 코드 toocall hello 함수를 다음 직접 메서드를 다시 부팅 하 고 hello에 대 한 쿼리는 마지막 시간 재부팅을 추가 합니다.
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. 저장 후 닫기 hello **dmpatterns_getstarted_service.js** 파일입니다.

## <a name="run-hello-apps"></a>Hello 앱 실행
준비 toorun hello 앱입니다.

1. Hello에 대 한 hello 명령 프롬프트 **manageddevice** 폴더를 다음 명령 toobegin hello 재부팅 직접적인 방법에 대 한 수신 대기 하는 hello를 실행 합니다.
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. Hello에 대 한 hello 명령 프롬프트 **triggerrebootondevice** hello 명령 tootrigger hello 원격 다음를 실행 하는 폴더를 다시 부팅 하 고 hello 장치로 이중 toofind hello 마지막 시간을 다시 부팅에 대 한 쿼리 합니다.
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. Hello 장치 응답 toohello 직접적인 방법 hello 콘솔에 표시 됩니다.

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

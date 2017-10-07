---
title: "Azure IoT Hub 장치 트윈스 (노드) aaaGet 시작 | Microsoft Docs"
description: "어떻게 toouse Azure IoT Hub 장치 트윈스 tooadd 태그를 삽입 하 고 IoT Hub 쿼리를 사용 합니다. Node.js tooimplement hello 시뮬레이션 된 장치 앱에 대 한 Azure IoT Sdk hello와 hello 태그를 추가 하 고 hello IoT Hub 쿼리를 실행 하는 서비스 응용 프로그램 사용 합니다."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: 314c88e4-cce1-441c-b75a-d2e08e39ae7d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.openlocfilehash: d60b8c3de85e9285e496b86e27d4ee31a0554a1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-node"></a>장치 쌍 시작(노드)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

이 자습서의 hello 끝 두 Node.js 콘솔 응용 프로그램 해야 합니다.

* **AddTagsAndQuery.js**, 태그를 추가하고 장치 쌍을 쿼리하는 Node.js 백 엔드 앱입니다.
* **TwinSimulatedDevice.js**, 이전에 만든 hello 장치 id를 가진 tooyour IoT 허브를 연결 하는 장치를 시뮬레이션 하 고 해당 연결 상태를 보고 하는 Node.js 응용 프로그램입니다.

> [!NOTE]
> hello 문서 [Azure IoT Sdk] [ lnk-hub-sdks] toobuild를 사용할 수 있는, Azure IoT Sdk hello에 대 한 정보를 제공 장치와 백 엔드 응용 프로그램입니다.
> 
> 

toocomplete hello 다음 해야이 자습서:

* Node.js 버전 0.10.x 이상
* 활성 Azure 계정. 계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a>Hello 서비스 앱 만들기
이 섹션에서는 위치 메타 데이터 toohello 장치로 이중와 관련 된 추가 하 여 Node.js 콘솔 응용 프로그램을 만들면 **myDeviceId**합니다. Hello 장치 트윈스 US, hello에 있는 hello 장치를 선택 하는 hello IoT 허브에 저장 하 고 셀룰러 연결을 보고 하는 스토리를 hello 쿼리 합니다.

1. **addtagsandqueryapp**라는 빈 폴더를 새로 만듭니다. Hello에 **addtagsandqueryapp** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 새로운 package.json 파일을 만듭니다. 모든 hello 기본값을 적용 합니다.
   
    ```
    npm init
    ```
2. Hello에 명령 프롬프트에 **addtagsandqueryapp** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iothub** 패키지:
   
    ```
    npm install azure-iothub --save
    ```
3. 텍스트 편집기를 사용 하 여 만드는 새 **AddTagsAndQuery.js** hello에 대 한 파일 **addtagsandqueryapp** 폴더입니다.
4. 다음 코드 toohello hello 추가 **AddTagsAndQuery.js** 파일을 찾아 hello 대체 **{iot 허브 연결 문자열을 (를)** 허브를 만들 때 복사한 IoT 허브 연결 문자열 hello로 자리 표시자:
   
        'use strict';
        var iothub = require('azure-iothub');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var patch = {
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                      }
                    }
                };
   
                twin.update(patch, function(err) {
                  if (err) {
                    console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                  } else {
                    console.log(twin.deviceId + ' twin updated successfully');
                    queryTwins();
                  }
                });
            }
        });
   
    hello **레지스트리** 개체 hello 서비스에서 장치 트윈스와 모든 hello 메서드에 필요한 toointeract을 제공 합니다. hello 이전 코드는 먼저 hello 초기화 **레지스트리** 개체를 검색에 대 한 장치로 이중 hello **myDeviceId**, 원하는 hello 위치 정보를 사용 하 여 해당 태그를 마지막으로 업데이트 합니다.
   
    Hello 후 hello 업데이트 태그를 삽입 하기 호출 hello **queryTwins** 함수입니다.
5. 코드의 hello 끝에 다음 hello 추가 **AddTagsAndQuery.js** tooimplement hello **queryTwins** 함수:
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    두 개의 쿼리를 실행 하는 이전 코드 hello: hello에 있는 장치의 장치 트윈스만 hello를 먼저 선택 하는 hello **Redmond43** 공장 별, 및 hello 두 번째 구체화 hello 쿼리 tooselect hello 장치만 또한 통해 연결 된 셀룰러 네트워크입니다.
   
    Hello를 만들 때 해당 hello 이전 코드 참고 **쿼리** 개체, 반환 된 문서의 최대 수를 지정 합니다. hello **쿼리** 개체에 포함 되어는 **hasMoreResults** tooinvoke hello를 사용할 수 있는 부울 속성 **nextAsTwin** 메서드를 여러 번 tooretrieve 모든 결과입니다. **next**라는 메서드는 장치 쌍이 아닌 결과(예: 집계 쿼리의 결과)에 대해 사용할 수 있습니다.
6. Hello 응용 프로그램을 실행 합니다.
   
        node AddTagsAndQuery.js
   
    Hello 쿼리 요청에 있는 모든 장치에 대 한 하나의 장치 hello 결과에 표시 되어야 **Redmond43** toodevices 셀룰러 네트워크를 사용 하는 결과 none hello를 제한 하는 hello 쿼리 합니다.
   
    ![][1]

변경 내용을 hello hello 이전 단원의 hello 쿼리의 결과 한 hello 연결 정보를 보고 하는 장치 앱 hello 다음 섹션에 만듭니다.

## <a name="create-hello-device-app"></a>Hello 장치 응용 프로그램 만들기
Tooyour 허브를 연결 하는 Node.js 콘솔 앱을 만들면이 섹션에서는 **myDeviceId**, 및 해당 장치로 이중 셀룰러 네트워크를 사용 하 여 연결 된 속성 toocontain hello 정보를 보고의 업데이트 합니다.

> [!NOTE]
> 이때 장치 트윈스는 tooIoT 허브를 연결 하는 장치 에서만에서 액세스할 수 hello MQTT 프로토콜을 사용 합니다. Toohello를 참조 하십시오 [MQTT 지원] [ lnk-devguide-mqtt] 방법에 대 한 문서 tooconvert 기존 장치 앱 toouse MQTT 합니다.
> 
> 

1. **reportconnectivity**라는 빈 폴더를 새로 만듭니다. Hello에 **reportconnectivity** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 새로운 package.json 파일을 만듭니다. 모든 hello 기본값을 적용 합니다.
   
    ```
    npm init
    ```
2. Hello에 명령 프롬프트에 **reportconnectivity** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iot 장치**, 및 **azure iot-장치 mqtt** 패키지 :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. 텍스트 편집기를 사용 하 여 만드는 새 **ReportConnectivity.js** hello에 대 한 파일 **reportconnectivity** 폴더입니다.
4. 다음 코드 toohello hello 추가 **ReportConnectivity.js** 파일을 찾아 hello 대체 **{장치 연결 문자열을 (를)** hello를 만들 때 복사한 hello 장치 연결 문자열과 함께 자리 표시자 **myDeviceId** 장치 id가 없음:
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    hello **클라이언트** 개체가 toointeract hello 장치에서 장치 트윈스과 필요한 모든 hello 메서드를 노출 합니다. hello를 초기화 한 후 이전 코드 hello **클라이언트** 개체를 검색에 대 한 장치로 이중 hello **myDeviceId** 를 hello 연결 정보와 함께 보고 된 해당 속성을 업데이트 합니다.
5. Hello 장치 앱 실행
   
        node ReportConnectivity.js
   
    Hello 메시지를 확인 해야 `twin state reported`합니다.
6. 이제는 hello 장치 보고 자신의 연결 정보를 두 쿼리 모두에 표시 됩니다. Hello에 다시 이동 **addtagsandqueryapp** 폴더를 열고 hello를 다시 쿼리 합니다.
   
        node AddTagsAndQuery.js
   
    이번에는 **myDeviceId**가 두 쿼리 결과에 모두 나타나야 합니다.
   
    ![][3]

## <a name="next-steps"></a>다음 단계
이 자습서에서는 hello Azure 포털에서에서 새 IoT 허브를 구성 하 고 id 레지스트리에 hello IoT hub에서 장치 id를 만든 다음 합니다. 백 엔드 앱에서 태그로 장치 메타 데이터를 추가 하 고 hello 장치로 이중의 시뮬레이션 된 장치 앱 tooreport 장치 연결 정보를 작성 합니다. 방법에 대해 배웠습니다 tooquery hello IoT Hub SQL 방식 쿼리 언어를 사용 하 여이 정보입니다.

사용 하 여 hello 리소스 toolearn을 어떻게 수행 하려면:

* hello 사용 하 여 장치에서 원격 분석 전송 [IoT 허브 시작] [ lnk-iothub-getstarted] 자습서
* hello로 장치로 이중 원하는 속성을 사용 하 여 장치 구성 [속성 tooconfigure 장치 원하는 사용할] [ lnk-twin-how-to-configure] 자습서
* 대화형으로 (예: 사용자 제어 응용 프로그램에서 팬)를 설정 하는 장치 hello로 제어 [직접 메서드를 사용 하 여] [ lnk-methods-tutorial] 자습서입니다.

<!-- images -->
[1]: media/iot-hub-node-node-twin-getstarted/service1.png
[3]: media/iot-hub-node-node-twin-getstarted/service2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

[lnk-twin-how-to-configure]: iot-hub-node-node-twin-how-to-configure.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

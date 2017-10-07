---
title: "Azure IoT 가장자리 (Linux)를 사용 하 여 장치 aaaSimulate | Microsoft Docs"
description: "어떻게 Linux toocreate 시뮬레이션된 된 장치에서 Azure IoT 가장자리 toouse를 보내는 원격 분석 IoT 가장자리를 통해 게이트웨이 tooan IoT hub."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 11e7bf28-ee3d-48d6-a386-eb506c7a31cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: andbuc
ms.openlocfilehash: 168fb8eda8671d02c63073bdf36dfcd88b397fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-linux"></a>Azure IoT 가장자리 toosend 장치-클라우드 메시지를 사용 하 여 시뮬레이션 된 장치 (Linux)

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a>Toorun 샘플 hello 하는 방법

hello **build.sh** hello로 해당 출력을 생성 하는 스크립트 **빌드** hello의 로컬 복사본에서 폴더 **iot 가장자리** 저장소입니다. 이 출력 hello이이 샘플에 사용 되는 4 개의 IoT 가장자리 모듈을 포함 합니다.

빌드 스크립트 위치 hello에서:

* **liblogger.so** hello에 **빌드/모듈/로 거** 폴더입니다.
* **libiothub.so** hello에 **빌드/모듈/iothub** 폴더입니다.
* **lib\_identity\_map.so** hello에 **빌드/모듈/identitymap** 폴더입니다.
* **libsimulated\_device.so** hello에 **빌드/모듈/시뮬레이션\_장치** 폴더입니다.

이러한 경로 사용 하 여 hello에 대 한 **모듈 경로** hello 다음 JSON 설정 파일에에서 표시 된 대로 값:

시뮬레이션 된 hello\_장치\_클라우드\_업로드\_샘플 프로세스 명령줄 인수로 hello 경로 tooa JSON 구성 파일을 사용 합니다. hello 다음 예제에서는 JSON 파일에에서 제공에서 hello SDK 리포지토리 **샘플\\시뮬레이션\_장치\_클라우드\_업로드\_샘플\\src\\ 시뮬레이션 된\_장치\_클라우드\_업로드\_샘플\_lin.json**합니다. hello를 수정 하지 않는 한이 구성 파일 작동 스크립트 tooplace hello IoT 가장자리 모듈 빌드하거나 기본이 아닌 위치에서 실행 파일을 샘플링 합니다.

> [!NOTE]
> hello 모듈 경로 hello 시뮬레이션을 실행 하는 위치에서 디렉터리를 상대 toohello\_장치\_클라우드\_업로드\_샘플 실행 파일, hello 디렉터리가 아닌 hello 실행 파일입니다. hello 샘플 JSON 구성 파일 toowriting too'deviceCloudUploadGatewaylog.log 기본값 ' 현재 작업 디렉터리에 있습니다.

텍스트 편집기를 열고 hello 파일 **샘플/시뮬레이션\_장치\_클라우드\_업로드\_샘플/src/시뮬레이션\_장치\_클라우드\_업로드\_lin.json** hello의 로컬 복사본에 **iot 가장자리** 저장소입니다. 이 파일 hello 샘플 게이트웨이에 hello IoT 가장자리 모듈을 구성합니다.

* hello **IoTHub** 모듈 tooyour IoT 허브를 연결 합니다. 구성한 toosend 데이터 tooyour IoT 허브입니다. 특히 집합 hello **IoTHubName** 값 IoT 허브의 toohello 이름 및 hello 설정 **IoTHubSuffix** 너무 값**azure devices.net**합니다. 집합 hello **전송** 의 값 tooone: **HTTP**, **AMQP**, 또는 **MQTT**합니다. 현재 **HTTP**만 모든 장치 메시지에 대한 하나의 TCP 연결을 공유합니다. 너무 hello 값을 설정 하면**AMQP**, 또는 **MQTT**, hello 게이트웨이 별도 TCP 연결 tooIoT 허브 각 장치에 대 한 유지 관리 합니다.
* hello **매핑** 모듈 시뮬레이션 된 장치 tooyour IoT Hub 장치 id hello MAC 주소를 매핑합니다. 다음 사항을 확인 **deviceId** 값 일치 hello id의 hello tooyour IoT hub 및 해당 hello를 추가 하는 두 개의 장치 **deviceKey** 두 장치 hello 키를 포함 하는 값입니다.
* hello **BLE1** 및 **BLE2** 모듈은 hello 시뮬레이션 된 장치. MAC의 일치 항목을 해결 하는 방법을 확인 hello에서 주소 hello **매핑** 모듈입니다.
* hello **로 거** 모듈 게이트웨이 활동 tooa 파일에 기록 합니다.
* hello **모듈 경로** hello 예제에 표시 된 값 hello에서 hello 샘플을 실행 하는 것으로 가정 **빌드** hello의 로컬 복사본에서 폴더 **iot 가장자리** 저장소입니다.
* hello **링크** hello를 연결 하는 hello JSON 파일의 hello 맨 아래에 있는 배열의 **BLE1** 및 **BLE2** 모듈 toohello **매핑** 모듈과 hello **매핑** 모듈 toohello **IoTHub** 모듈입니다. 또한 모든 메시지가 hello로 기록 됩니다 하면 **로 거** 모듈입니다.

```json
{
    "modules": [
        {
            "name": "IotHub",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/iothub/libiothub.so"
            }
            },
            "args": {
              "IoTHubName": "<<insert here IoTHubName>>",
              "IoTHubSuffix": "<<insert here IoTHubSuffix>>",
              "Transport": "HTTP"
            }
          },
        {
            "name": "mapping",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/identitymap/libidentity_map.so"
            }
            },
            "args": [
              {
                "macAddress": "01:01:01:01:01:01",
                "deviceId": "<<insert here deviceId>>",
                "deviceKey": "<<insert here deviceKey>>"
              },
              {
                "macAddress": "02:02:02:02:02:02",
                "deviceId": "<<insert here deviceId>>",
                "deviceKey": "<<insert here deviceKey>>"
              }
            ]
          },
        {
            "name": "BLE1",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/simulated_device/libsimulated_device.so"
            }
            },
            "args": {
              "macAddress": "01:01:01:01:01:01"
            }
          },
        {
            "name": "BLE2",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/simulated_device/libsimulated_device.so"
            }
            },
            "args": {
              "macAddress": "02:02:02:02:02:02"
            }
          },
        {
            "name": "Logger",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args": {
              "filename": "deviceCloudUploadGatewaylog.log"
            }
          }
    ],
    "links": [
        {
            "source": "*",
            "sink": "Logger"
        },
        {
            "source": "BLE1",
            "sink": "mapping"
        },
        {
            "source": "BLE2",
            "sink": "mapping"
        },
        {
            "source": "mapping",
            "sink": "IotHub"
        }
    ]
}
```

Hello 변경 내용을 저장할 toohello 구성 파일의 내용이 되었습니다.

toorun hello 샘플:

1. 프로그램 셸에서 toohello 이동 **iot-가장자리/빌드** 폴더입니다.
2. Hello 다음 명령을 실행 합니다.
   
    ```sh
    ./samples/simulated_device_cloud_upload/simulated_device_cloud_upload_sample ../samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json
    ```
3. Hello를 사용할 수 있습니다 [장치 탐색기] [ lnk-device-explorer] 또는 [iothub 탐색기] [ lnk-iothub-explorer] IoT hub hello 로부터 받는 toomonitor hello 메시지 도구 게이트웨이입니다. 예를 들어 iothub 탐색기를 사용 하 여 다음 명령을 hello를 사용 하 여 장치-클라우드 메시지 모니터링할 수 있습니다.

    ```sh
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a>다음 단계

더에 대 한 Azure IoT 가장자리와 실험 몇 가지 코드 예제와 toogain 방문 hello 다음 개발자 자습서 및 리소스:

* [Azure IoT Edge를 사용하여 물리적 장치에서 장치-클라우드 메시지 보내기][lnk-physical-device]
* [Azure IoT Edge][lnk-iot-edge]

toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

* [IoT Hub 개발자 가이드][lnk-devguide]
* [Hello 접지에서 IoT 솔루션 보안][lnk-securing]

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

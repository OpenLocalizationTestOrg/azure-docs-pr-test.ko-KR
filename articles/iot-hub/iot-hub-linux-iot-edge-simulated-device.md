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
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-linux"></a><span data-ttu-id="3c4a2-103">Azure IoT 가장자리 toosend 장치-클라우드 메시지를 사용 하 여 시뮬레이션 된 장치 (Linux)</span><span class="sxs-lookup"><span data-stu-id="3c4a2-103">Use Azure IoT Edge toosend device-to-cloud messages with a simulated device (Linux)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="3c4a2-104">Toorun 샘플 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c4a2-104">How toorun hello sample</span></span>

<span data-ttu-id="3c4a2-105">hello **build.sh** hello로 해당 출력을 생성 하는 스크립트 **빌드** hello의 로컬 복사본에서 폴더 **iot 가장자리** 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-105">hello **build.sh** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="3c4a2-106">이 출력 hello이이 샘플에 사용 되는 4 개의 IoT 가장자리 모듈을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-106">This output includes hello four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="3c4a2-107">빌드 스크립트 위치 hello에서:</span><span class="sxs-lookup"><span data-stu-id="3c4a2-107">hello build script places the:</span></span>

* <span data-ttu-id="3c4a2-108">**liblogger.so** hello에 **빌드/모듈/로 거** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-108">**liblogger.so** in hello **build/modules/logger** folder.</span></span>
* <span data-ttu-id="3c4a2-109">**libiothub.so** hello에 **빌드/모듈/iothub** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-109">**libiothub.so** in hello **build/modules/iothub** folder.</span></span>
* <span data-ttu-id="3c4a2-110">**lib\_identity\_map.so** hello에 **빌드/모듈/identitymap** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-110">**lib\_identity\_map.so** in hello **build/modules/identitymap** folder.</span></span>
* <span data-ttu-id="3c4a2-111">**libsimulated\_device.so** hello에 **빌드/모듈/시뮬레이션\_장치** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-111">**libsimulated\_device.so** in hello **build/modules/simulated\_device** folder.</span></span>

<span data-ttu-id="3c4a2-112">이러한 경로 사용 하 여 hello에 대 한 **모듈 경로** hello 다음 JSON 설정 파일에에서 표시 된 대로 값:</span><span class="sxs-lookup"><span data-stu-id="3c4a2-112">Use these paths for hello **module path** values as shown in hello following JSON settings file:</span></span>

<span data-ttu-id="3c4a2-113">시뮬레이션 된 hello\_장치\_클라우드\_업로드\_샘플 프로세스 명령줄 인수로 hello 경로 tooa JSON 구성 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-113">hello simulated\_device\_cloud\_upload\_sample process takes hello path tooa JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="3c4a2-114">hello 다음 예제에서는 JSON 파일에에서 제공에서 hello SDK 리포지토리 **샘플\\시뮬레이션\_장치\_클라우드\_업로드\_샘플\\src\\ 시뮬레이션 된\_장치\_클라우드\_업로드\_샘플\_lin.json**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-114">hello following example JSON file is provided in hello SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_lin.json**.</span></span> <span data-ttu-id="3c4a2-115">hello를 수정 하지 않는 한이 구성 파일 작동 스크립트 tooplace hello IoT 가장자리 모듈 빌드하거나 기본이 아닌 위치에서 실행 파일을 샘플링 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-115">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="3c4a2-116">hello 모듈 경로 hello 시뮬레이션을 실행 하는 위치에서 디렉터리를 상대 toohello\_장치\_클라우드\_업로드\_샘플 실행 파일, hello 디렉터리가 아닌 hello 실행 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-116">hello module paths are relative toohello directory from where you run hello simulated\_device\_cloud\_upload\_sample executable, not hello directory where hello executable is located.</span></span> <span data-ttu-id="3c4a2-117">hello 샘플 JSON 구성 파일 toowriting too'deviceCloudUploadGatewaylog.log 기본값 ' 현재 작업 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-117">hello sample JSON configuration file defaults toowriting too'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="3c4a2-118">텍스트 편집기를 열고 hello 파일 **샘플/시뮬레이션\_장치\_클라우드\_업로드\_샘플/src/시뮬레이션\_장치\_클라우드\_업로드\_lin.json** hello의 로컬 복사본에 **iot 가장자리** 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-118">In a text editor, open hello file **samples/simulated\_device\_cloud\_upload\_sample/src/simulated\_device\_cloud\_upload\_lin.json** in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="3c4a2-119">이 파일 hello 샘플 게이트웨이에 hello IoT 가장자리 모듈을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-119">This file configures hello IoT Edge modules in hello sample gateway:</span></span>

* <span data-ttu-id="3c4a2-120">hello **IoTHub** 모듈 tooyour IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-120">hello **IoTHub** module connects tooyour IoT hub.</span></span> <span data-ttu-id="3c4a2-121">구성한 toosend 데이터 tooyour IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-121">You configure it toosend data tooyour IoT hub.</span></span> <span data-ttu-id="3c4a2-122">특히 집합 hello **IoTHubName** 값 IoT 허브의 toohello 이름 및 hello 설정 **IoTHubSuffix** 너무 값**azure devices.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-122">Specifically, set hello **IoTHubName** value toohello name of your IoT hub and set hello **IoTHubSuffix** value too**azure-devices.net**.</span></span> <span data-ttu-id="3c4a2-123">집합 hello **전송** 의 값 tooone: **HTTP**, **AMQP**, 또는 **MQTT**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-123">Set hello **Transport** value tooone of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="3c4a2-124">현재 **HTTP**만 모든 장치 메시지에 대한 하나의 TCP 연결을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="3c4a2-125">너무 hello 값을 설정 하면**AMQP**, 또는 **MQTT**, hello 게이트웨이 별도 TCP 연결 tooIoT 허브 각 장치에 대 한 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-125">If you set hello value too**AMQP**, or **MQTT**, hello gateway maintains a separate TCP connection tooIoT Hub for each device.</span></span>
* <span data-ttu-id="3c4a2-126">hello **매핑** 모듈 시뮬레이션 된 장치 tooyour IoT Hub 장치 id hello MAC 주소를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-126">hello **mapping** module maps hello MAC addresses of your simulated devices tooyour IoT Hub device ids.</span></span> <span data-ttu-id="3c4a2-127">다음 사항을 확인 **deviceId** 값 일치 hello id의 hello tooyour IoT hub 및 해당 hello를 추가 하는 두 개의 장치 **deviceKey** 두 장치 hello 키를 포함 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-127">Make sure that **deviceId** values match hello ids of hello two devices you added tooyour IoT hub, and that hello **deviceKey** values contain hello keys of your two devices.</span></span>
* <span data-ttu-id="3c4a2-128">hello **BLE1** 및 **BLE2** 모듈은 hello 시뮬레이션 된 장치.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-128">hello **BLE1** and **BLE2** modules are hello simulated devices.</span></span> <span data-ttu-id="3c4a2-129">MAC의 일치 항목을 해결 하는 방법을 확인 hello에서 주소 hello **매핑** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-129">Note how their MAC addresses match hello addresses in hello **mapping** module.</span></span>
* <span data-ttu-id="3c4a2-130">hello **로 거** 모듈 게이트웨이 활동 tooa 파일에 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-130">hello **Logger** module logs your gateway activity tooa file.</span></span>
* <span data-ttu-id="3c4a2-131">hello **모듈 경로** hello 예제에 표시 된 값 hello에서 hello 샘플을 실행 하는 것으로 가정 **빌드** hello의 로컬 복사본에서 폴더 **iot 가장자리** 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-131">hello **module path** values shown in hello example assume that you run hello sample from hello **build** folder in your local copy of hello **iot-edge** repository.</span></span>
* <span data-ttu-id="3c4a2-132">hello **링크** hello를 연결 하는 hello JSON 파일의 hello 맨 아래에 있는 배열의 **BLE1** 및 **BLE2** 모듈 toohello **매핑** 모듈과 hello **매핑** 모듈 toohello **IoTHub** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-132">hello **links** array at hello bottom of hello JSON file connects hello **BLE1** and **BLE2** modules toohello **mapping** module, and hello **mapping** module toohello **IoTHub** module.</span></span> <span data-ttu-id="3c4a2-133">또한 모든 메시지가 hello로 기록 됩니다 하면 **로 거** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-133">It also ensures that all messages are logged by hello **Logger** module.</span></span>

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

<span data-ttu-id="3c4a2-134">Hello 변경 내용을 저장할 toohello 구성 파일의 내용이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-134">Save hello changes you made toohello configuration file.</span></span>

<span data-ttu-id="3c4a2-135">toorun hello 샘플:</span><span class="sxs-lookup"><span data-stu-id="3c4a2-135">toorun hello sample:</span></span>

1. <span data-ttu-id="3c4a2-136">프로그램 셸에서 toohello 이동 **iot-가장자리/빌드** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-136">In your shell, navigate toohello **iot-edge/build** folder.</span></span>
2. <span data-ttu-id="3c4a2-137">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-137">Run hello following command:</span></span>
   
    ```sh
    ./samples/simulated_device_cloud_upload/simulated_device_cloud_upload_sample ../samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json
    ```
3. <span data-ttu-id="3c4a2-138">Hello를 사용할 수 있습니다 [장치 탐색기] [ lnk-device-explorer] 또는 [iothub 탐색기] [ lnk-iothub-explorer] IoT hub hello 로부터 받는 toomonitor hello 메시지 도구 게이트웨이입니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-138">You can use hello [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool toomonitor hello messages that IoT hub receives from hello gateway.</span></span> <span data-ttu-id="3c4a2-139">예를 들어 iothub 탐색기를 사용 하 여 다음 명령을 hello를 사용 하 여 장치-클라우드 메시지 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-139">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

    ```sh
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="3c4a2-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3c4a2-140">Next steps</span></span>

<span data-ttu-id="3c4a2-141">더에 대 한 Azure IoT 가장자리와 실험 몇 가지 코드 예제와 toogain 방문 hello 다음 개발자 자습서 및 리소스:</span><span class="sxs-lookup"><span data-stu-id="3c4a2-141">toogain a more advanced understanding of Azure IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="3c4a2-142">[Azure IoT Edge를 사용하여 물리적 장치에서 장치-클라우드 메시지 보내기][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="3c4a2-142">[Send device-to-cloud messages from a physical device with Azure IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="3c4a2-143">[Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="3c4a2-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="3c4a2-144">toofurther는 IoT Hub의 hello 기능을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3c4a2-144">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="3c4a2-145">[IoT Hub 개발자 가이드][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="3c4a2-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="3c4a2-146">[Hello 접지에서 IoT 솔루션 보안][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="3c4a2-146">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

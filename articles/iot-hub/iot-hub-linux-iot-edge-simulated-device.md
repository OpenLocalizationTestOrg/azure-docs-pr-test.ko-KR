---
title: "Azure IoT Edge를 사용하여 장치 시뮬레이션(Linux) | Microsoft Docs"
description: "Linux에서 Azure IoT Edge를 사용하여 IoT Edge 게이트웨이를 통해 원격 분석을 IoT Hub에 전송하는 시뮬레이션된 장치를 만드는 방법입니다."
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
ms.openlocfilehash: 5349960373ae6815862c5f79a69dd6d5d9d624ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-iot-edge-to-send-device-to-cloud-messages-with-a-simulated-device-linux"></a><span data-ttu-id="93ccb-103">Azure IoT Edge를 사용하여 시뮬레이션된 장치(Linux)에서 장치-클라우드 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="93ccb-103">Use Azure IoT Edge to send device-to-cloud messages with a simulated device (Linux)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="93ccb-104">샘플을 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="93ccb-104">How to run the sample</span></span>

<span data-ttu-id="93ccb-105">**build.sh** 스크립트는 **iot-edge** 리포지토리의 로컬 복사본에 있는 **build** 폴더에 해당 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-105">The **build.sh** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="93ccb-106">이 출력에는 이 샘플에서 사용된 네 개의 IoT Edge 모듈이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-106">This output includes the four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="93ccb-107">빌드 스크립트는 다음을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-107">The build script places the:</span></span>

* <span data-ttu-id="93ccb-108">**build/modules/logger** 폴더에 **liblogger.so**.</span><span class="sxs-lookup"><span data-stu-id="93ccb-108">**liblogger.so** in the **build/modules/logger** folder.</span></span>
* <span data-ttu-id="93ccb-109">**build/modules/iothub** 폴더에 **libiothub.so**.</span><span class="sxs-lookup"><span data-stu-id="93ccb-109">**libiothub.so** in the **build/modules/iothub** folder.</span></span>
* <span data-ttu-id="93ccb-110">**build/modules/identitymap** 폴더에 **lib\_identity\_map.so**.</span><span class="sxs-lookup"><span data-stu-id="93ccb-110">**lib\_identity\_map.so** in the **build/modules/identitymap** folder.</span></span>
* <span data-ttu-id="93ccb-111">**build/modules/simulated\_device** 폴더에 **libsimulated\_device.so**.</span><span class="sxs-lookup"><span data-stu-id="93ccb-111">**libsimulated\_device.so** in the **build/modules/simulated\_device** folder.</span></span>

<span data-ttu-id="93ccb-112">다음 JSON 설정 파일에 표시된 대로 **module path** 값에 이러한 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-112">Use these paths for the **module path** values as shown in the following JSON settings file:</span></span>

<span data-ttu-id="93ccb-113">simulated\_device\_cloud\_upload\_sample 프로세스는 JSON 구성 파일에 대한 경로를 명령줄 인수 형태로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-113">The simulated\_device\_cloud\_upload\_sample process takes the path to a JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="93ccb-114">다음 예제 JSON 파일은 **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_lin.json**의 SDK 리포지토리에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-114">The following example JSON file is provided in the SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_lin.json**.</span></span> <span data-ttu-id="93ccb-115">이 구성 파일은 빌드 스크립트를 수정하여 IoT Edge 모듈이나 샘플 실행 파일을 기본 위치가 아닌 위치에 배치한 경우 외에는 그대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-115">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="93ccb-116">모듈 경로는 실행 파일이 있는 디렉터리가 아니라, simulated\_device\_cloud\_upload\_sample 실행 파일이 실행되는 위치의 디렉터리에 대한 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-116">The module paths are relative to the directory from where you run the simulated\_device\_cloud\_upload\_sample executable, not the directory where the executable is located.</span></span> <span data-ttu-id="93ccb-117">샘플 JSON 구성 파일은 현재 작업 디렉터리에서 작성 중인 ‘deviceCloudUploadGatewaylog.log’를 기본값으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-117">The sample JSON configuration file defaults to writing to 'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="93ccb-118">텍스트 편집기에서 **iot-edge** 리포지토리의 로컬 복사본에 있는 **samples/simulated\_device\_cloud\_upload\_sample/src/simulated\_device\_cloud\_upload\_lin.json** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-118">In a text editor, open the file **samples/simulated\_device\_cloud\_upload\_sample/src/simulated\_device\_cloud\_upload\_lin.json** in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="93ccb-119">이 파일은 샘플 게이트웨이에서 IoT Edge 모듈을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-119">This file configures the IoT Edge modules in the sample gateway:</span></span>

* <span data-ttu-id="93ccb-120">**IoTHub** 모듈이 IoT Hub에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-120">The **IoTHub** module connects to your IoT hub.</span></span> <span data-ttu-id="93ccb-121">IoT Hub에 데이터를 보내도록 이를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-121">You configure it to send data to your IoT hub.</span></span> <span data-ttu-id="93ccb-122">특히 **IoTHubName** 값을 IoT Hub의 이름으로 설정하고, **IoTHubSuffix** 값을 **azure-devices.net**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-122">Specifically, set the **IoTHubName** value to the name of your IoT hub and set the **IoTHubSuffix** value to **azure-devices.net**.</span></span> <span data-ttu-id="93ccb-123">**HTTP**, **AMQP** 또는 **MQTT** 중 하나에 **Transport** 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-123">Set the **Transport** value to one of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="93ccb-124">현재 **HTTP**만 모든 장치 메시지에 대한 하나의 TCP 연결을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="93ccb-125">값을 **AMQP** 또는 **MQTT**로 설정하는 경우 게이트웨이는 각 장치에 대해 IoT Hub에 대한 별도의 TCP 연결을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-125">If you set the value to **AMQP**, or **MQTT**, the gateway maintains a separate TCP connection to IoT Hub for each device.</span></span>
* <span data-ttu-id="93ccb-126">**mapping** 모듈은 시뮬레이션된 장치의 MAC 주소를 IoT Hub 장치 ID에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-126">The **mapping** module maps the MAC addresses of your simulated devices to your IoT Hub device ids.</span></span> <span data-ttu-id="93ccb-127">**deviceId** 값이 IoT Hub에 추가한 두 장치의 ID와 일치하는지, 그리고 **deviceKey** 값에 두 장치의 키가 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-127">Make sure that **deviceId** values match the ids of the two devices you added to your IoT hub, and that the **deviceKey** values contain the keys of your two devices.</span></span>
* <span data-ttu-id="93ccb-128">**BLE1** 및 **BLE2** 모듈은 시뮬레이션된 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-128">The **BLE1** and **BLE2** modules are the simulated devices.</span></span> <span data-ttu-id="93ccb-129">해당 MAC 주소가 **mapping** 모듈의 주소와 어떻게 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-129">Note how their MAC addresses match the addresses in the **mapping** module.</span></span>
* <span data-ttu-id="93ccb-130">**Logger** 모듈은 게이트웨이 활동을 파일에 로깅합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-130">The **Logger** module logs your gateway activity to a file.</span></span>
* <span data-ttu-id="93ccb-131">예제에 나온 **module path** 값은 **iot-edge** 리포지토리의 로컬 복사본에 있는 **build** 폴더에서 샘플을 실행하는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-131">The **module path** values shown in the example assume that you run the sample from the **build** folder in your local copy of the **iot-edge** repository.</span></span>
* <span data-ttu-id="93ccb-132">JSON 파일의 맨 아래에 있는 **링크** 배열은 **BLE1** 및 **BLE2** 모듈을 **매핑** 모듈에 연결하고 **매핑** 모듈을 **IoTHub** 모듈에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-132">The **links** array at the bottom of the JSON file connects the **BLE1** and **BLE2** modules to the **mapping** module, and the **mapping** module to the **IoTHub** module.</span></span> <span data-ttu-id="93ccb-133">또한 **로거** 모듈이 모든 메시지를 기록하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-133">It also ensures that all messages are logged by the **Logger** module.</span></span>

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

<span data-ttu-id="93ccb-134">구성 파일에 적용한 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-134">Save the changes you made to the configuration file.</span></span>

<span data-ttu-id="93ccb-135">샘플을 실행하려면</span><span class="sxs-lookup"><span data-stu-id="93ccb-135">To run the sample:</span></span>

1. <span data-ttu-id="93ccb-136">셸에서 **iot-edge/build** 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-136">In your shell, navigate to the **iot-edge/build** folder.</span></span>
2. <span data-ttu-id="93ccb-137">다음 명령 실행:</span><span class="sxs-lookup"><span data-stu-id="93ccb-137">Run the following command:</span></span>
   
    ```sh
    ./samples/simulated_device_cloud_upload/simulated_device_cloud_upload_sample ../samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json
    ```
3. <span data-ttu-id="93ccb-138">[장치탐색기][lnk-device-explorer] 또는 [iothub-explorer][lnk-iothub-explorer] 도구를 사용하여 IoT Hub가 게이트웨이에서 수신하는 메시지를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-138">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to monitor the messages that IoT hub receives from the gateway.</span></span> <span data-ttu-id="93ccb-139">예를 들어 iothub-explorer를 사용하면 다음 명령으로 장치-클라우드 메시지를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93ccb-139">For example, using iothub-explorer you can monitor device-to-cloud messages using the following command:</span></span>

    ```sh
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="93ccb-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="93ccb-140">Next steps</span></span>

<span data-ttu-id="93ccb-141">Azure IoT Edge와 코드 예제 실험에 대해 더욱 심도 있게 이해하려면 다음 개발자 자습서 및 리소스를 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="93ccb-141">To gain a more advanced understanding of Azure IoT Edge and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="93ccb-142">[Azure IoT Edge를 사용하여 물리적 장치에서 장치-클라우드 메시지 보내기][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="93ccb-142">[Send device-to-cloud messages from a physical device with Azure IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="93ccb-143">[Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="93ccb-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="93ccb-144">IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93ccb-144">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="93ccb-145">[IoT Hub 개발자 가이드][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="93ccb-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="93ccb-146">[처음부터 IoT 솔루션 보안 유지][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="93ccb-146">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

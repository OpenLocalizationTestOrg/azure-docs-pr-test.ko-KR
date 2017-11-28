---
title: "Node.js를 사용 하 여 장치 aaaConnect | Microsoft Docs"
description: "어떻게 tooconnect 장치 toohello Azure IoT Suite 미리 구성 된 Node.js에서 작성 된 응용 프로그램을 사용 하 여 원격 모니터링 솔루션에 설명 합니다."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: fc50a33f-9fb9-42d7-b1b8-eb5cff19335e
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 80bf2b70f15f539bfce4f135d533c46dd2b3f5a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-nodejs"></a><span data-ttu-id="d1f2a-103">사용자 장치 toohello 모니터링 미리 구성 된 솔루션 (Node.js) 원격 연결</span><span class="sxs-lookup"><span data-stu-id="d1f2a-103">Connect your device toohello remote monitoring preconfigured solution (Node.js)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a><span data-ttu-id="d1f2a-104">node.js 샘플 솔루션 만들기</span><span class="sxs-lookup"><span data-stu-id="d1f2a-104">Create a node.js sample solution</span></span>

<span data-ttu-id="d1f2a-105">Node.js 버전 0.11.5 이상이 개발 컴퓨터에 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-105">Ensure that Node.js version 0.11.5 or later is installed on your development machine.</span></span> <span data-ttu-id="d1f2a-106">실행할 수 있습니다 `node --version` hello 명령줄 toocheck hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-106">You can run `node --version` at hello command line toocheck hello version.</span></span>

1. <span data-ttu-id="d1f2a-107">개발 컴퓨터에서 **RemoteMonitoring**이라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-107">Create a folder called **RemoteMonitoring** on your development machine.</span></span> <span data-ttu-id="d1f2a-108">명령줄 사용자 환경에서 toothis 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-108">Navigate toothis folder in your command-line environment.</span></span>

1. <span data-ttu-id="d1f2a-109">다음 실행된 hello toodownload 및 설치 hello 필요한 패키지를 toocomplete hello 샘플 응용 프로그램 명령:</span><span class="sxs-lookup"><span data-stu-id="d1f2a-109">Run hello following commands toodownload and install hello packages you need toocomplete hello sample app:</span></span>

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="d1f2a-110">Hello에 **RemoteMonitoring** 폴더에서 파일을 만들 **remote_monitoring.js**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-110">In hello **RemoteMonitoring** folder, create a file called **remote_monitoring.js**.</span></span> <span data-ttu-id="d1f2a-111">텍스트 편집기에서 이 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-111">Open this file in a text editor.</span></span>

1. <span data-ttu-id="d1f2a-112">Hello에 **remote_monitoring.js** 파일, hello 다음 추가 `require` 문:</span><span class="sxs-lookup"><span data-stu-id="d1f2a-112">In hello **remote_monitoring.js** file, add hello following `require` statements:</span></span>

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. <span data-ttu-id="d1f2a-113">변수 선언 hello 후 다음 hello 추가 `require` 문.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-113">Add hello following variable declarations after hello `require` statements.</span></span> <span data-ttu-id="d1f2a-114">대체 hello 자리 표시자 값 [장치 Id] 및 [장치 Key] hello 원격 모니터링 솔루션 대시보드에서 장치에서 기록한 값으로.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-114">Replace hello placeholder values [Device Id] and [Device Key] with values you noted for your device in hello remote monitoring solution dashboard.</span></span> <span data-ttu-id="d1f2a-115">Hello 솔루션 대시보드 tooreplace [IoTHub Name]에서 hello IoT 허브 호스트 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-115">Use hello IoT Hub Hostname from hello solution dashboard tooreplace [IoTHub Name].</span></span> <span data-ttu-id="d1f2a-116">예를 들어 IoT Hub 호스트 이름이 **contoso.azure-devices.net**인 경우 [IoTHub Name]을 **contoso**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-116">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. <span data-ttu-id="d1f2a-117">다음 변수 toodefine hello 몇 가지 기본 원격 분석 데이터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-117">Add hello following variables toodefine some base telemetry data:</span></span>

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. <span data-ttu-id="d1f2a-118">도우미 함수 tooprint 작업 결과 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-118">Add hello following helper function tooprint operation results:</span></span>

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. <span data-ttu-id="d1f2a-119">Hello 다음 도우미 함수 toouse toorandomize hello 원격 분석 값에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-119">Add hello following helper function toouse toorandomize hello telemetry values:</span></span>

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. <span data-ttu-id="d1f2a-120">Hello hello에 대 한 정의 다음 추가 **DeviceInfo** 시작할 때 전송 하는 개체 hello 장치:</span><span class="sxs-lookup"><span data-stu-id="d1f2a-120">Add hello following definition for hello **DeviceInfo** object hello device sends on startup:</span></span>

    ```nodejs
    var deviceMetaData = {
        'ObjectType': 'DeviceInfo',
        'IsSimulatedDevice': 0,
        'Version': '1.0',
        'DeviceProperties': {
            'DeviceID': deviceId,
            'HubEnabledState': 1
        }
    };
    ```

1. <span data-ttu-id="d1f2a-121">Hello 다음 추가 장치로 이중 hello에 대 한 정의 값을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-121">Add hello following definition for hello device twin reported values.</span></span> <span data-ttu-id="d1f2a-122">이 정의 대 한 설명은 hello 직접 메서드 hello 장치에서 지원:</span><span class="sxs-lookup"><span data-stu-id="d1f2a-122">This definition includes descriptions of hello direct methods hello device supports:</span></span>

    ```nodejs
    var reportedProperties = {
        "Device": {
            "DeviceState": "normal",
            "Location": {
                "Latitude": 47.642877,
                "Longitude": -122.125497
            }
        },
        "Config": {
            "TemperatureMeanValue": 56.7,
            "TelemetryInterval": 45
        },
        "System": {
            "Manufacturer": "Contoso Inc.",
            "FirmwareVersion": "2.22",
            "InstalledRAM": "8 MB",
            "ModelNumber": "DB-14",
            "Platform": "Plat 9.75",
            "Processor": "i3-9",
            "SerialNumber": "SER99"
        },
        "Location": {
            "Latitude": 47.642877,
            "Longitude": -122.125497
        },
        "SupportedMethods": {
            "Reboot": "Reboot hello device",
            "InitiateFirmwareUpdate--FwPackageURI-string": "Updates device Firmware. Use parameter FwPackageURI toospecifiy hello URI of hello firmware file"
        },
    }
    ```

1. <span data-ttu-id="d1f2a-123">다음 함수 toohandle hello hello 추가 **재부팅** 직접 메서드 호출:</span><span class="sxs-lookup"><span data-stu-id="d1f2a-123">Add hello following function toohandle hello **Reboot** direct method call:</span></span>

    ```nodejs
    function onReboot(request, response) {
        // Implement actual logic here.
        console.log('Simulated reboot...');

        // Complete hello response
        response.send(200, "Rebooting device", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```

1. <span data-ttu-id="d1f2a-124">다음 함수 toohandle hello hello 추가 **InitiateFirmwareUpdate** 직접 메서드 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-124">Add hello following function toohandle hello **InitiateFirmwareUpdate** direct method call.</span></span> <span data-ttu-id="d1f2a-125">직접이 메서드는 hello 펌웨어 이미지 toodownload의 매개 변수 toospecify hello 위치를 사용 하 고 시작 hello 장치에 펌웨어 업데이트를 비동기적으로 hello:</span><span class="sxs-lookup"><span data-stu-id="d1f2a-125">This direct method uses a parameter toospecify hello location of hello firmware image toodownload, and initiates hello firmware update on hello device asynchronously:</span></span>

    ```nodejs
    function onInitiateFirmwareUpdate(request, response) {
        console.log('Simulated firmware update initiated, using: ' + request.payload.FwPackageURI);

        // Complete hello response
        response.send(200, "Firmware update initiated", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });

        // Add logic here tooperform hello firmware update asynchronously
    }
    ```

1. <span data-ttu-id="d1f2a-126">다음 코드는 클라이언트 인스턴스 toocreate hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-126">Add hello following code toocreate a client instance:</span></span>

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="d1f2a-127">코드를 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-127">Add hello following code to:</span></span>

    * <span data-ttu-id="d1f2a-128">Hello 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-128">Open hello connection.</span></span>
    * <span data-ttu-id="d1f2a-129">Hello 보내기 **DeviceInfo** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-129">Send hello **DeviceInfo** object.</span></span>
    * <span data-ttu-id="d1f2a-130">desired 속성에 대한 처리기를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-130">Set up a handler for desired properties.</span></span>
    * <span data-ttu-id="d1f2a-131">reported 속성을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-131">Send reported properties.</span></span>
    * <span data-ttu-id="d1f2a-132">Hello 직접 방법에 대 한 처리기를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-132">Register handlers for hello direct methods.</span></span>
    * <span data-ttu-id="d1f2a-133">원격 분석 보내기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-133">Start sending telemetry.</span></span>

    ```nodejs
    client.open(function (err) {
        if (err) {
            printErrorFor('open')(err);
        } else {
            console.log('Sending device metadata:\n' + JSON.stringify(deviceMetaData));
            client.sendEvent(new Message(JSON.stringify(deviceMetaData)), printErrorFor('send metadata'));

            // Create device twin
            client.getTwin(function(err, twin) {
                if (err) {
                    console.error('Could not get device twin');
                } else {
                    console.log('Device twin created');

                    twin.on('properties.desired', function(delta) {
                        console.log('Received new desired properties:');
                        console.log(JSON.stringify(delta));
                    });

                    // Send reported properties
                    twin.properties.reported.update(reportedProperties, function(err) {
                        if (err) throw err;
                        console.log('twin state reported');
                    });

                    // Register handlers for direct methods
                    client.onDeviceMethod('Reboot', onReboot);
                    client.onDeviceMethod('InitiateFirmwareUpdate', onInitiateFirmwareUpdate);
                }
            });

            // Start sending telemetry
            var sendInterval = setInterval(function () {
                temperature += generateRandomIncrement();
                externalTemperature += generateRandomIncrement();
                humidity += generateRandomIncrement();

                var data = JSON.stringify({
                    'DeviceID': deviceId,
                    'Temperature': temperature,
                    'Humidity': humidity,
                    'ExternalTemperature': externalTemperature
                });

                console.log('Sending device event data:\n' + data);
                client.sendEvent(new Message(data), printErrorFor('send event'));
            }, 5000);

            client.on('error', function (err) {
                printErrorFor('client')(err);
                if (sendInterval) clearInterval(sendInterval);
                client.close(printErrorFor('client.close'));
            });
        }
    });
    ```

1. <span data-ttu-id="d1f2a-134">Hello 변경 toohello 저장 **remote_monitoring.js** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-134">Save hello changes toohello **remote_monitoring.js** file.</span></span>

1. <span data-ttu-id="d1f2a-135">Hello 다음 명령 프롬프트 toolaunch hello 샘플 응용 프로그램에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f2a-135">Run hello following command at a command prompt toolaunch hello sample application:</span></span>
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

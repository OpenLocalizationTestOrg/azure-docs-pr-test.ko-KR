---
title: "Node.js를 사용하여 장치 연결 | Microsoft Docs"
description: "Node.js에 작성된 응용 프로그램을 사용하여 미리 구성된 Azure IoT Suite 원격 모니터링 솔루션에 장치를 연결하는 방법을 설명합니다."
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
ms.openlocfilehash: 6459b6196eb7f4a083b67e5a421bcc0d51d39e5c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-nodejs"></a><span data-ttu-id="312f2-103">미리 구성된 원격 모니터링 솔루션에 장치 연결(Node.js)</span><span class="sxs-lookup"><span data-stu-id="312f2-103">Connect your device to the remote monitoring preconfigured solution (Node.js)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a><span data-ttu-id="312f2-104">node.js 샘플 솔루션 만들기</span><span class="sxs-lookup"><span data-stu-id="312f2-104">Create a node.js sample solution</span></span>

<span data-ttu-id="312f2-105">Node.js 버전 0.11.5 이상이 개발 컴퓨터에 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-105">Ensure that Node.js version 0.11.5 or later is installed on your development machine.</span></span> <span data-ttu-id="312f2-106">명령줄에서 `node --version`을 실행하여 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-106">You can run `node --version` at the command line to check the version.</span></span>

1. <span data-ttu-id="312f2-107">개발 컴퓨터에서 **RemoteMonitoring**이라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-107">Create a folder called **RemoteMonitoring** on your development machine.</span></span> <span data-ttu-id="312f2-108">명령줄 환경에서 이 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-108">Navigate to this folder in your command-line environment.</span></span>

1. <span data-ttu-id="312f2-109">다음 명령을 실행하여 샘플 앱을 완료해야 하는 패키지를 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-109">Run the following commands to download and install the packages you need to complete the sample app:</span></span>

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="312f2-110">**RemoteMonitoring** 폴더에서 **remote_monitoring.js**라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-110">In the **RemoteMonitoring** folder, create a file called **remote_monitoring.js**.</span></span> <span data-ttu-id="312f2-111">텍스트 편집기에서 이 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-111">Open this file in a text editor.</span></span>

1. <span data-ttu-id="312f2-112">**remote_monitoring.js** 파일에서 다음 `require` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-112">In the **remote_monitoring.js** file, add the following `require` statements:</span></span>

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. <span data-ttu-id="312f2-113">다음 변수 선언을 `require` 문 뒤에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-113">Add the following variable declarations after the `require` statements.</span></span> <span data-ttu-id="312f2-114">원격 모니터링 솔루션 대시보드에서 자리 표시자 값 [Device Id] 및 [Device Key]를 장치에 대해 기록한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-114">Replace the placeholder values [Device Id] and [Device Key] with values you noted for your device in the remote monitoring solution dashboard.</span></span> <span data-ttu-id="312f2-115">솔루션 대시보드에서 IoT Hub 호스트 이름을 사용하여 [IoTHub Name]을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-115">Use the IoT Hub Hostname from the solution dashboard to replace [IoTHub Name].</span></span> <span data-ttu-id="312f2-116">예를 들어 IoT Hub 호스트 이름이 **contoso.azure-devices.net**인 경우 [IoTHub Name]을 **contoso**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-116">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. <span data-ttu-id="312f2-117">다음 변수를 추가하여 일부 기본 원격 분석 데이터를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-117">Add the following variables to define some base telemetry data:</span></span>

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. <span data-ttu-id="312f2-118">다음 도우미 함수를 추가하여 작업 결과를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-118">Add the following helper function to print operation results:</span></span>

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. <span data-ttu-id="312f2-119">다음 도우미 함수를 추가하여 원격 분석 값을 임의로 지정하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-119">Add the following helper function to use to randomize the telemetry values:</span></span>

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. <span data-ttu-id="312f2-120">장치가 시작 시 전송하는 **DeviceInfo** 개체에 대해 다음 정의를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-120">Add the following definition for the **DeviceInfo** object the device sends on startup:</span></span>

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

1. <span data-ttu-id="312f2-121">장치 쌍 reported 값에 대해 다음 정의를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-121">Add the following definition for the device twin reported values.</span></span> <span data-ttu-id="312f2-122">이 정의는 장치가 지원하는 직접 메서드의 설명을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-122">This definition includes descriptions of the direct methods the device supports:</span></span>

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
            "Reboot": "Reboot the device",
            "InitiateFirmwareUpdate--FwPackageURI-string": "Updates device Firmware. Use parameter FwPackageURI to specifiy the URI of the firmware file"
        },
    }
    ```

1. <span data-ttu-id="312f2-123">다음 함수를 추가하여 **Reboot** 직접 메서드 호출을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-123">Add the following function to handle the **Reboot** direct method call:</span></span>

    ```nodejs
    function onReboot(request, response) {
        // Implement actual logic here.
        console.log('Simulated reboot...');

        // Complete the response
        response.send(200, "Rebooting device", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```

1. <span data-ttu-id="312f2-124">다음 함수를 추가하여 **InitiateFirmwareUpdate** 직접 메서드 호출을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-124">Add the following function to handle the **InitiateFirmwareUpdate** direct method call.</span></span> <span data-ttu-id="312f2-125">이 직접 메서드는 매개 변수를 사용하여 다운로드할 펌웨어 이미지의 위치를 지정하고 장치에서 비동기적으로 펌웨어 업데이트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-125">This direct method uses a parameter to specify the location of the firmware image to download, and initiates the firmware update on the device asynchronously:</span></span>

    ```nodejs
    function onInitiateFirmwareUpdate(request, response) {
        console.log('Simulated firmware update initiated, using: ' + request.payload.FwPackageURI);

        // Complete the response
        response.send(200, "Firmware update initiated", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });

        // Add logic here to perform the firmware update asynchronously
    }
    ```

1. <span data-ttu-id="312f2-126">다음 코드를 추가하여 클라이언트 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-126">Add the following code to create a client instance:</span></span>

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="312f2-127">다음 코드를 추가하여:</span><span class="sxs-lookup"><span data-stu-id="312f2-127">Add the following code to:</span></span>

    * <span data-ttu-id="312f2-128">연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-128">Open the connection.</span></span>
    * <span data-ttu-id="312f2-129">**DeviceInfo** 개체를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-129">Send the **DeviceInfo** object.</span></span>
    * <span data-ttu-id="312f2-130">desired 속성에 대한 처리기를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-130">Set up a handler for desired properties.</span></span>
    * <span data-ttu-id="312f2-131">reported 속성을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-131">Send reported properties.</span></span>
    * <span data-ttu-id="312f2-132">직접 메서드에 대한 처리기를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-132">Register handlers for the direct methods.</span></span>
    * <span data-ttu-id="312f2-133">원격 분석 보내기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-133">Start sending telemetry.</span></span>

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

1. <span data-ttu-id="312f2-134">**remote_monitoring.js** 파일에 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-134">Save the changes to the **remote_monitoring.js** file.</span></span>

1. <span data-ttu-id="312f2-135">명령 프롬프트에서 다음 명령을 실행하여 샘플 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="312f2-135">Run the following command at a command prompt to launch the sample application:</span></span>
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

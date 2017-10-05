---
title: "Azure IoT Hub 직접 메서드(노드) | Microsoft Docs"
description: "Azure IoT Hub 직접 메서드를 사용하는 방법입니다. Node.js용 Azure IoT 장치 SDK를 사용하여 직접 메서드를 포함한 시뮬레이션된 장치 앱 및 직접 메서드를 호출하는 서비스 앱을 구현합니다."
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
ms.openlocfilehash: 83725c3ae3fd3807f2469be888e270ba078a8972
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a><span data-ttu-id="d78aa-104">Node.js와 함께 IoT 장치에서 직접 메서드 사용</span><span class="sxs-lookup"><span data-stu-id="d78aa-104">Use direct methods on your IoT device with Node.js</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="d78aa-105">이 자습서를 마치면 두 가지 Node.js 콘솔 앱이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-105">At the end of this tutorial, you have two Node.js console apps:</span></span>

* <span data-ttu-id="d78aa-106">**CallMethodOnDevice.js**: 시뮬레이션된 장치 앱에서 메서드를 호출하고 응답을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-106">**CallMethodOnDevice.js**, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="d78aa-107">**SimulatedDevice.js**는 앞에서 만든 장치 ID로 IoT Hub에 연결하고 클라우드에서 호출한 메서드에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-107">**SimulatedDevice.js**, which connects to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="d78aa-108">[Azure IoT SDKs][lnk-hub-sdks] 문서는 장치와 솔루션 백 엔드에서 실행하기 위해 두 응용 프로그램을 빌드하는 데 사용할 수 있는 Azure IoT SDK에 관한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="d78aa-109">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="d78aa-110">Node.js 버전 0.10.x 이상</span><span class="sxs-lookup"><span data-stu-id="d78aa-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="d78aa-111">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="d78aa-111">An active Azure account.</span></span> <span data-ttu-id="d78aa-112">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="d78aa-113">시뮬레이션된 장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="d78aa-113">Create a simulated device app</span></span>
<span data-ttu-id="d78aa-114">이 섹션에서는 클라우드에서 호출한 메서드에 응답하는 Node.js 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-114">In this section, you create a Node.js console app that responds to a method called by the cloud.</span></span>

1. <span data-ttu-id="d78aa-115">**simulateddevice**라는 빈 폴더를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-115">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="d78aa-116">**simulateddevice** 폴더의 명령 프롬프트에서 다음 명령을 사용하여 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-116">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="d78aa-117">모든 기본값을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-117">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="d78aa-118">**simulateddevice** 폴더의 명령 프롬프트에서 다음 명령을 실행하여 **azure-iot-device** 장치 SDK 패키지 및 **azure-iot-device-mqtt** 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-118">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="d78aa-119">텍스트 편집기를 사용하여 **simulateddevice** 폴더에 새 **SimulatedDevice.js** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-119">Using a text editor, create a new **SimulatedDevice.js** file in the **simulateddevice** folder.</span></span>
4. <span data-ttu-id="d78aa-120">**SimulatedDevice.js** 파일 앞에 다음 `require` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-120">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="d78aa-121">**connectionString** 변수를 추가하고 이 변수를 사용하여 **DeviceClient** 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-121">Add a **connectionString** variable and use it to create a **DeviceClient** instance.</span></span> <span data-ttu-id="d78aa-122">**{장치 연결 문자열}**을 *장치 ID 만들기* 섹션에서 생성한 장치 연결 문자열로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-122">Replace **{device connection string}** with the device connection string you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="d78aa-123">장치에서 메서드를 실행하도록 다음 함수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-123">Add the following function to implement the method on the device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written to log.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="d78aa-124">IoT Hub에 대한 연결을 열고 메서드 수신기 초기화를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-124">Open the connection to your IoT hub and start initialize the method listener:</span></span>
   
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
8. <span data-ttu-id="d78aa-125">**SimulatedDevice.js** 파일을 저장한 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-125">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="d78aa-126">간단히 하기 위해 이 자습서에서는 다시 시도 정책을 구현하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-126">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="d78aa-127">프로덕션 코드에 MSDN 문서 [일시적인 오류 처리][lnk-transient-faults]에 제시된 대로 재시도 정책(예: 연결 다시 시도)을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-127">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-method-on-a-device"></a><span data-ttu-id="d78aa-128">장치에 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="d78aa-128">Call a method on a device</span></span>
<span data-ttu-id="d78aa-129">이 섹션에서는 시뮬레이션된 장치 앱에서 메서드를 호출하고 응답을 표시하는 Node.js 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-129">In this section, you create a Node.js console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="d78aa-130">**callmethodondevice**라는 빈 폴더를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-130">Create a new empty folder called **callmethodondevice**.</span></span> <span data-ttu-id="d78aa-131">**callmethodondevice** 폴더의 명령 프롬프트에서 다음 명령을 사용하여 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-131">In the **callmethodondevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="d78aa-132">모든 기본값을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-132">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="d78aa-133">**callmethodondevice** 폴더의 명령 프롬프트에서 다음 명령을 실행하여 **azure-iothub** 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-133">At your command prompt in the **callmethodondevice** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="d78aa-134">텍스트 편집기를 사용하여 **callmethodondevice** 폴더에 **CallMethodOnDevice.js** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-134">Using a text editor, create a **CallMethodOnDevice.js** file in the **callmethodondevice** folder.</span></span>
4. <span data-ttu-id="d78aa-135">**CallMethodOnDevice.js** 파일의 시작 부분에 다음 `require` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-135">Add the following `require` statements at the start of the **CallMethodOnDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="d78aa-136">다음 변수 선언을 추가하고 자리 표시자 값을 허브의 IoT Hub 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-136">Add the following variable declaration and replace the placeholder value with the IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. <span data-ttu-id="d78aa-137">IoT hub에 대한 연결을 열도록 클라이언트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-137">Create the client to open the connection to your IoT hub.</span></span>
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. <span data-ttu-id="d78aa-138">장치 메서드를 호출하고 장치 응답을 콘솔에 출력하도록 다음 함수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-138">Add the following function to invoke the device method and print the device response to the console:</span></span>
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed to invoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. <span data-ttu-id="d78aa-139">**CallMethodOnDevice.js** 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-139">Save and close the **CallMethodOnDevice.js** file.</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="d78aa-140">앱 실행</span><span class="sxs-lookup"><span data-stu-id="d78aa-140">Run the apps</span></span>
<span data-ttu-id="d78aa-141">이제 앱을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-141">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="d78aa-142">**simulateddevice** 폴더의 명령 프롬프트에서 다음 명령을 실행하여 IoT Hub의 메서드 호출에 대한 대기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-142">At a command prompt in the **simulateddevice** folder, run the following command to start listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. <span data-ttu-id="d78aa-143">**callmethodondevice** 폴더의 명령 프롬프트에서 다음 명령을 실행하여 IoT Hub 모니터링을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-143">At a command prompt in the **callmethodondevice** folder, run the following command to begin monitoring your IoT hub:</span></span>
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. <span data-ttu-id="d78aa-144">장치가 메시지를 출력하여 메서드에 반응하는 것과 메서드를 호출한 응용 프로그램이 장치의 응답을 표시하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-144">You will see the device react to the method by printing out the message and the application which called the method display the response from the device:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="d78aa-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d78aa-145">Next steps</span></span>
<span data-ttu-id="d78aa-146">이 자습서에서는 Azure Portal에서 새 IoT Hub를 구성한 다음, IoT Hub의 ID 레지스트리에서 장치 ID를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-146">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="d78aa-147">시뮬레이션된 장치 앱이 클라우드에서 호출한 메서드에 반응할 수 있도록 장치 ID를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-147">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="d78aa-148">장치에서 메서드를 호출하고 장치의 응답을 표시하는 앱도 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d78aa-148">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="d78aa-149">계속해서 IoT Hub을 시작하고 다른 IoT 시나리오를 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d78aa-149">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="d78aa-150">[IoT Hub 시작]</span><span class="sxs-lookup"><span data-stu-id="d78aa-150">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="d78aa-151">[여러 장치에서 jobs 예약][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="d78aa-151">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="d78aa-152">IoT 솔루션을 확장하고 여러 장치에서 메서드 호출을 예약하는 방법을 알아보려면 [jobs 예약 및 브로드캐스트][lnk-tutorial-jobs] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d78aa-152">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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

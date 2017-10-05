---
title: "Azure IoT Hub 장치 관리 시작(노드) | Microsoft Docs"
description: "IoT Hub 장치 관리를 사용하여 원격 장치 재부팅을 시작하는 방법입니다. Node.js용 Azure IoT 장치 SDK를 사용하여 직접 메서드를 포함한 시뮬레이션된 장치 앱 및 직접 메서드를 호출하는 서비스 앱을 구현합니다."
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
ms.openlocfilehash: 332a3e62cb1ef75e2c6dd5562ee799465c401128
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-device-management-node"></a><span data-ttu-id="606f3-104">장치 관리 시작(노드)</span><span class="sxs-lookup"><span data-stu-id="606f3-104">Get started with device management (Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="606f3-105">이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="606f3-106">Azure Portal을 사용하여 IoT Hub를 만들고 IoT Hub에 장치 ID를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="606f3-107">장치를 다시 시작하는 직접 메서드가 포함된 시뮬레이트된 장치 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="606f3-108">직접 메서드는 클라우드에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="606f3-109">IoT Hub를 통해 시뮬레이션된 장치 앱에서 재부팅 직접 메서드를 호출하는 Node.js 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-109">Create a Node.js console app that calls the reboot direct method in the simulated device app through your IoT hub.</span></span>

<span data-ttu-id="606f3-110">이 자습서를 마치면 두 가지 Node.js 콘솔 앱이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-110">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="606f3-111">**dmpatterns_getstarted_device.js**, 이전에 만든 장치 ID로 IoT Hub에 연결하며 재부팅 직접 메서드를 수신하고 물리적 재부팅을 시뮬레이션하며 마지막 재부팅 시간을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-111">**dmpatterns_getstarted_device.js**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span></span>

<span data-ttu-id="606f3-112">**dmpatterns_getstarted_service.js**, 시뮬레이션된 장치 앱에 직접 메서드를 호출하고 응답을 표시하고 업데이트된 reported 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-112">**dmpatterns_getstarted_service.js**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span></span>

<span data-ttu-id="606f3-113">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-113">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="606f3-114">Node.js 버전 0.12.x 이상,</span><span class="sxs-lookup"><span data-stu-id="606f3-114">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="606f3-115">Windows 또는 Linux에서 이 자습서를 위해 Node.js를 설치하는 방법에 대해서는 [개발 환경 준비][lnk-dev-setup]에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-115">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="606f3-116">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="606f3-116">An active Azure account.</span></span> <span data-ttu-id="606f3-117">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-117">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="606f3-118">시뮬레이션된 장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="606f3-118">Create a simulated device app</span></span>
<span data-ttu-id="606f3-119">이 섹션에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-119">In this section, you will</span></span>

* <span data-ttu-id="606f3-120">클라우드에서 호출하는 직접 메서드에 응답하는 Node.js 콘솔 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="606f3-120">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="606f3-121">시뮬레이션된 장치 재부팅 트리거</span><span class="sxs-lookup"><span data-stu-id="606f3-121">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="606f3-122">reported 속성을 사용하여 장치 및 해당 장치가 마지막으로 재부팅한 시간을 확인하는 장치 쌍 쿼리를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="606f3-122">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span></span>

1. <span data-ttu-id="606f3-123">**manageddevice**라는 빈 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-123">Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="606f3-124">**manageddevice** 폴더의 명령 프롬프트에서 다음 명령을 사용하여 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-124">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="606f3-125">모든 기본값을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-125">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="606f3-126">**manageddevice** 폴더의 명령 프롬프트에서 다음 명령을 실행하여 **azure-iot-device** 장치 SDK 패키지 및 **azure-iot-device-mqtt** 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-126">At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="606f3-127">텍스트 편집기를 사용하여 **manageddevice** 폴더에 **dmpatterns_getstarted_device.js** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-127">Using a text editor, create a **dmpatterns_getstarted_device.js** file in the **manageddevice** folder.</span></span>
4. <span data-ttu-id="606f3-128">다음 'require' 문을 **dmpatterns_getstarted_device.js** 파일의 시작 부분에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-128">Add the following 'require' statements at the start of the **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="606f3-129">**connectionString** 변수를 추가하고 이 변수를 사용하여 **클라이언트** 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-129">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  <span data-ttu-id="606f3-130">연결 문자열을 장치 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-130">Replace the connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="606f3-131">장치에서 직접 메서드를 구현하도록 다음 함수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-131">Add the following function to implement the direct method on the device</span></span>
   
    ```
    var onReboot = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report the reboot before the physical restart
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
7. <span data-ttu-id="606f3-132">IoT Hub에 대한 연결을 열고 직접 메서드 수신기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-132">Open the connection to your IoT hub and start the direct method listener:</span></span>
   
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
8. <span data-ttu-id="606f3-133">**dmpatterns_getstarted_device.js** 파일을 저장 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-133">Save and close the **dmpatterns_getstarted_device.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="606f3-134">간단히 하기 위해 이 자습서에서는 다시 시도 정책을 구현하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-134">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="606f3-135">프로덕션 코드에서는 MSDN 문서 [일시적인 오류 처리][lnk-transient-faults]에서 제시한 대로 다시 시도 정책(예: 지수 백오프)을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-135">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="606f3-136">직접 메서드를 사용하여 장치에서 원격 재부팅 트리거</span><span class="sxs-lookup"><span data-stu-id="606f3-136">Trigger a remote reboot on the device using a direct method</span></span>
<span data-ttu-id="606f3-137">이 섹션에서는 장치에서 직접 메서드를 사용하여 원격 다시 시작을 시작하는 Node.js 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-137">In this section, you create a Node.js console app that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="606f3-138">앱은 장치 쌍 쿼리를 사용하여 해당 장치에 대한 마지막 다시 시작 시간을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-138">The app uses device twin queries to discover the last reboot time for that device.</span></span>

1. <span data-ttu-id="606f3-139">**triggerrebootondevice**라는 빈 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-139">Create an empty folder called **triggerrebootondevice**.</span></span>  <span data-ttu-id="606f3-140">**triggerrebootondevice** 폴더의 명령 프롬프트에서 다음 명령을 사용하여 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-140">In the **triggerrebootondevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="606f3-141">모든 기본값을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-141">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="606f3-142">**triggerrebootondevice** 폴더의 명령 프롬프트에서 다음 명령을 실행하여 **azure-iothub** 장치 SDK 패키지 및 **azure-iot-device-mqtt** 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-142">At your command prompt in the **triggerrebootondevice** folder, run the following command to install the **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="606f3-143">텍스트 편집기를 사용하여 **triggerrebootondevice** 폴더에 **dmpatterns_getstarted_service.js** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-143">Using a text editor, create a **dmpatterns_getstarted_service.js** file in the **triggerrebootondevice** folder.</span></span>
4. <span data-ttu-id="606f3-144">다음 'require' 문을 **dmpatterns_getstarted_service.js** 파일의 시작 부분에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-144">Add the following 'require' statements at the start of the **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="606f3-145">다음 변수 선언을 추가하고 자리 표시자 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-145">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. <span data-ttu-id="606f3-146">대상 장치를 재부팅하기 위해 장치 메서드를 호출하도록 다음 함수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-146">Add the following function to invoke the device method to reboot the target device:</span></span>
   
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
                console.log("Successfully invoked the device to reboot.");  
            }
        });
    };
    ```
7. <span data-ttu-id="606f3-147">장치를 쿼리하고 마지막 재부팅 시간을 가져오도록 다음 함수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-147">Add the following function to query for the device and get the last reboot time:</span></span>
   
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
                console.log('Waiting for device to report last reboot time.');
        });
    };
    ```
8. <span data-ttu-id="606f3-148">다시 시작 직접 메서드를 트리거하고 마지막 다시 시작 시간을 쿼리하는 함수를 호출하도록 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-148">Add the following code to call the functions that trigger the reboot direct method and query for the last reboot time:</span></span>
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. <span data-ttu-id="606f3-149">**dmpatterns_getstarted_service.js** 파일을 저장 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-149">Save and close the **dmpatterns_getstarted_service.js** file.</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="606f3-150">앱 실행</span><span class="sxs-lookup"><span data-stu-id="606f3-150">Run the apps</span></span>
<span data-ttu-id="606f3-151">이제 앱을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-151">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="606f3-152">**manageddevice** 폴더의 명령 프롬프트에서 다음 명령을 실행하여 다시 시작 직접 메서드에 대한 수신 대기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-152">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="606f3-153">**triggerrebootondevice** 폴더의 명령 프롬프트에서 다음 명령을 실행하여 원격 재부팅을 트리거하고 마지막 재부팅 시간을 찾기 위해 장치 쌍에 대한 쿼리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-153">At the command prompt in the **triggerrebootondevice** folder, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span></span>
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. <span data-ttu-id="606f3-154">콘솔에서 직접 메서드에 대한 장치 응답을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="606f3-154">You see the device response to the direct method in the console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups to manage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

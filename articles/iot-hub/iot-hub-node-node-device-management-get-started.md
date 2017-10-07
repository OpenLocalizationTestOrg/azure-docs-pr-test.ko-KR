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
# <a name="get-started-with-device-management-node"></a><span data-ttu-id="663c7-104">장치 관리 시작(노드)</span><span class="sxs-lookup"><span data-stu-id="663c7-104">Get started with device management (Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="663c7-105">이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="663c7-106">Azure 포털 toocreate IoT Hub hello를 사용 하 및 IoT 허브에서 장치 id를 만드는 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="663c7-107">장치를 다시 시작하는 직접 메서드가 포함된 시뮬레이트된 장치 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="663c7-108">Hello 클라우드에서 직접 메서드 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="663c7-109">IoT 허브를 통해 hello 시뮬레이션 된 장치 응용 프로그램에서 hello 재부팅 직접 메서드를 호출 하 여 Node.js 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-109">Create a Node.js console app that calls hello reboot direct method in hello simulated device app through your IoT hub.</span></span>

<span data-ttu-id="663c7-110">이 자습서의 hello 끝 두 Node.js 콘솔 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-110">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="663c7-111">**dmpatterns_getstarted_device.js**, 이전에 만든 hello 장치 id를 가진 tooyour IoT 허브를 연결 하는 다시 부팅 직접적인 방법, 실제 다시 부팅을 시뮬레이션 받아 hello 마지막 다시 부팅에 대 한 hello 시간을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-111">**dmpatterns_getstarted_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports hello time for hello last reboot.</span></span>

<span data-ttu-id="663c7-112">**dmpatterns_getstarted_service.js**을 hello 응답 표시 hello 시뮬레이션 된 장치 응용 프로그램에서 직접 메서드를 호출 하 하 고 표시 hello 업데이트 속성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-112">**dmpatterns_getstarted_service.js**, which calls a direct method in hello simulated device app, displays hello response, and displays hello updated reported properties.</span></span>

<span data-ttu-id="663c7-113">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="663c7-113">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="663c7-114">Node.js 버전 0.12.x 이상,</span><span class="sxs-lookup"><span data-stu-id="663c7-114">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="663c7-115">[개발 환경을 준비] [ lnk-dev-setup] 설명 방법을 Windows 또는 Linux에서이 자습서에 대 한 tooinstall Node.js 합니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-115">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="663c7-116">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="663c7-116">An active Azure account.</span></span> <span data-ttu-id="663c7-117">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-117">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="663c7-118">시뮬레이션된 장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="663c7-118">Create a simulated device app</span></span>
<span data-ttu-id="663c7-119">이 섹션에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-119">In this section, you will</span></span>

* <span data-ttu-id="663c7-120">응답 tooa 직접적인 방법 hello 클라우드에서 호출 하 여 Node.js 콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="663c7-120">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="663c7-121">시뮬레이션된 장치 재부팅 트리거</span><span class="sxs-lookup"><span data-stu-id="663c7-121">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="663c7-122">사용 하 여 hello 속성 tooenable 장치로 이중 쿼리 tooidentify 장치 및 마지막 재부팅 될 보고</span><span class="sxs-lookup"><span data-stu-id="663c7-122">Use hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted</span></span>

1. <span data-ttu-id="663c7-123">**manageddevice**라는 빈 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-123">Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="663c7-124">Hello에 **manageddevice** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-124">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="663c7-125">모든 hello 기본값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-125">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="663c7-126">Hello에 명령 프롬프트에 **manageddevice** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iot 장치** 장치 SDK 패키지 및 **azure-iot-장치-mqtt**패키지:</span><span class="sxs-lookup"><span data-stu-id="663c7-126">At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="663c7-127">텍스트 편집기를 사용 하 여 만들는 **dmpatterns_getstarted_device.js** hello에 대 한 파일 **manageddevice** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-127">Using a text editor, create a **dmpatterns_getstarted_device.js** file in hello **manageddevice** folder.</span></span>
4. <span data-ttu-id="663c7-128">Hello 다음 '필요' hello hello 시작 부분에 설명 추가 **dmpatterns_getstarted_device.js** 파일:</span><span class="sxs-lookup"><span data-stu-id="663c7-128">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="663c7-129">추가 **connectionString** 변수 toocreate를 사용 하는 **클라이언트** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="663c7-129">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  <span data-ttu-id="663c7-130">장치 연결 문자열과 함께 hello 연결 문자열을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-130">Replace hello connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="663c7-131">Hello 나오는 hello 장치에 따라 함수 tooimplement hello에 대 한 직접 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-131">Add hello following function tooimplement hello direct method on hello device</span></span>
   
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
7. <span data-ttu-id="663c7-132">Hello 연결 tooyour IoT 허브를 열고 hello 직접적인 방법 수신기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-132">Open hello connection tooyour IoT hub and start hello direct method listener:</span></span>
   
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
8. <span data-ttu-id="663c7-133">저장 후 닫기 hello **dmpatterns_getstarted_device.js** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-133">Save and close hello **dmpatterns_getstarted_device.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="663c7-134">단순 tookeep 항목을이 자습서는 어떠한 재시도 정책도 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-134">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="663c7-135">프로덕션 코드에서는 hello MSDN 문서에 설명 된 대로 다시 시도 정책 (예: 지 수 백오프)를 구현 해야 [일시적인 오류 처리][lnk-transient-faults]합니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-135">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="663c7-136">트리거는 직접 메서드를 사용 하 여 hello 장치에 원격 컴퓨터를 다시 부팅</span><span class="sxs-lookup"><span data-stu-id="663c7-136">Trigger a remote reboot on hello device using a direct method</span></span>
<span data-ttu-id="663c7-137">이 섹션에서는 장치에서 직접 메서드를 사용하여 원격 다시 시작을 시작하는 Node.js 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-137">In this section, you create a Node.js console app that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="663c7-138">hello 앱 해당 장치에 대 한 장치로 이중 쿼리 toodiscover hello 마지막 부팅 시간을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-138">hello app uses device twin queries toodiscover hello last reboot time for that device.</span></span>

1. <span data-ttu-id="663c7-139">**triggerrebootondevice**라는 빈 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-139">Create an empty folder called **triggerrebootondevice**.</span></span>  <span data-ttu-id="663c7-140">Hello에 **triggerrebootondevice** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-140">In hello **triggerrebootondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="663c7-141">모든 hello 기본값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-141">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="663c7-142">Hello에 명령 프롬프트에 **triggerrebootondevice** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iothub** 장치 SDK 패키지 및 **azure-iot-장치-mqtt** 패키지:</span><span class="sxs-lookup"><span data-stu-id="663c7-142">At your command prompt in hello **triggerrebootondevice** folder, run hello following command tooinstall hello **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="663c7-143">텍스트 편집기를 사용 하 여 만들는 **dmpatterns_getstarted_service.js** hello에 대 한 파일 **triggerrebootondevice** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-143">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerrebootondevice** folder.</span></span>
4. <span data-ttu-id="663c7-144">Hello 다음 '필요' hello hello 시작 부분에 설명 추가 **dmpatterns_getstarted_service.js** 파일:</span><span class="sxs-lookup"><span data-stu-id="663c7-144">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="663c7-145">다음 변수 선언을 hello를 추가 하 고 hello 자리 표시자 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-145">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. <span data-ttu-id="663c7-146">Hello 함수 tooinvoke hello 장치 메서드 tooreboot hello 대상 장치를 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-146">Add hello following function tooinvoke hello device method tooreboot hello target device:</span></span>
   
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
7. <span data-ttu-id="663c7-147">Hello 다음 tooquery hello 장치에 대 한 함수 및 hello 마지막 부팅 시간 가져오기 추가:</span><span class="sxs-lookup"><span data-stu-id="663c7-147">Add hello following function tooquery for hello device and get hello last reboot time:</span></span>
   
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
8. <span data-ttu-id="663c7-148">Hello hello를 트리거하는 코드 toocall hello 함수를 다음 직접 메서드를 다시 부팅 하 고 hello에 대 한 쿼리는 마지막 시간 재부팅을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-148">Add hello following code toocall hello functions that trigger hello reboot direct method and query for hello last reboot time:</span></span>
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. <span data-ttu-id="663c7-149">저장 후 닫기 hello **dmpatterns_getstarted_service.js** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-149">Save and close hello **dmpatterns_getstarted_service.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="663c7-150">Hello 앱 실행</span><span class="sxs-lookup"><span data-stu-id="663c7-150">Run hello apps</span></span>
<span data-ttu-id="663c7-151">준비 toorun hello 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-151">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="663c7-152">Hello에 대 한 hello 명령 프롬프트 **manageddevice** 폴더를 다음 명령 toobegin hello 재부팅 직접적인 방법에 대 한 수신 대기 하는 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-152">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="663c7-153">Hello에 대 한 hello 명령 프롬프트 **triggerrebootondevice** hello 명령 tootrigger hello 원격 다음를 실행 하는 폴더를 다시 부팅 하 고 hello 장치로 이중 toofind hello 마지막 시간을 다시 부팅에 대 한 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-153">At hello command prompt in hello **triggerrebootondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. <span data-ttu-id="663c7-154">Hello 장치 응답 toohello 직접적인 방법 hello 콘솔에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="663c7-154">You see hello device response toohello direct method in hello console.</span></span>

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

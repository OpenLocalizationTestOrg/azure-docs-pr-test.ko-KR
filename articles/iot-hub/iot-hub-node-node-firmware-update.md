---
title: "Azure IoT Hub (노드)와 aaaDevice 펌웨어 업데이트 | Microsoft Docs"
description: "Azure IoT Hub tooinitiate 장치 펌웨어에 toouse 장치 관리 업데이트 하는 방법입니다. 시뮬레이션 된 장치 응용 프로그램 및 서비스 앱 hello 펌웨어 업데이트를 트리거하는 Node.js tooimplement에 대 한 hello Azure IoT Sdk를 사용 합니다."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/06/2017
ms.author: juanpere
ms.openlocfilehash: 99d4b369e7aba334bf713e0c657e6e5d227fb691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-nodenode"></a><span data-ttu-id="93f29-104">장치 관리 tooinitiate 장치 펌웨어 업데이트 / (노드)를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="93f29-104">Use device management tooinitiate a device firmware update (Node/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="93f29-105">소개</span><span class="sxs-lookup"><span data-stu-id="93f29-105">Introduction</span></span>
<span data-ttu-id="93f29-106">Hello에 [장치 관리 시작] [ lnk-dm-getstarted] 자습서에서 언급 했 듯이 어떻게 toouse hello [장치로 이중] [ lnk-devtwin] 및 [직접 메서드] [ lnk-c2dmethod] 기본 형식 tooremotely는 장치를 다시 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-106">In hello [Get started with device management][lnk-dm-getstarted] tutorial, you saw how toouse hello [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives tooremotely reboot a device.</span></span> <span data-ttu-id="93f29-107">이 자습서에서는 hello IoT Hub 기본 형식과 동일 하 고 지침을 제공 및 toodo는-종단 펌웨어 업데이트를 시뮬레이션 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-107">This tutorial uses hello same IoT Hub primitives and provides guidance and shows you how toodo an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="93f29-108">이 패턴은 hello Intel Edison 장치 샘플에 대 한 hello 펌웨어 업데이트 구현에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-108">This pattern is used in hello firmware update implementation for hello Intel Edison device sample.</span></span>

<span data-ttu-id="93f29-109">이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="93f29-110">IoT 허브를 통해 hello 시뮬레이션 된 장치 응용 프로그램에서 hello firmwareUpdate 직접 메서드를 호출 하 여 Node.js 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-110">Create a Node.js console app that calls hello firmwareUpdate direct method in hello simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="93f29-111">**firmwareUpdate** 직접 메서드를 구현하는 시뮬레이트된 장치 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="93f29-112">이 메서드를 toodownload hello 펌웨어 이미지 될 때까지 대기 하 고, hello 펌웨어 이미지를 다운로드 하 고, 마지막으로 hello 펌웨어 이미지를 적용 하는 여러 단계로 이루어진 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-112">This method initiates a multi-stage process that waits toodownload hello firmware image, downloads hello firmware image, and finally applies hello firmware image.</span></span> <span data-ttu-id="93f29-113">Hello 업데이트의 각 단계 hello 장치 사용 하 여 hello 속성 tooreport를 진행률 보고 했습니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-113">During each stage of hello update, hello device uses hello reported properties tooreport on progress.</span></span>

<span data-ttu-id="93f29-114">이 자습서의 hello 끝 두 Node.js 콘솔 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-114">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="93f29-115">**dmpatterns_fwupdate_service.js**, hello 응답 표시 hello 시뮬레이션 된 장치 응용 프로그램에서 직접 메서드를 호출 하 고 정기적으로 (500 밀리초 마다) 업데이트 표시 hello 보고 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in hello simulated device app, displays hello response, and periodically (every 500ms) displays hello updated reported properties.</span></span>

<span data-ttu-id="93f29-116">**dmpatterns_fwupdate_device.js**를 포함 하 여 펌웨어 업데이트 다중 상태 프로세스 toosimulate을 통해 실행을 firmwareUpdate 직접 메서드를 받으면 앞에서 만든 hello 장치 id를 가진 tooyour IoT 허브를 연결 하는: hello에 대 한 대기 중 이미지를 다운로드 hello 새 이미지를 다운로드 하 고 마지막으로 hello 이미지를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-116">**dmpatterns_fwupdate_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process toosimulate a firmware update including: waiting for hello image download, downloading hello new image, and finally applying hello image.</span></span>

<span data-ttu-id="93f29-117">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="93f29-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="93f29-118">Node.js 버전 0.12.x 이상,</span><span class="sxs-lookup"><span data-stu-id="93f29-118">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="93f29-119">[개발 환경을 준비] [ lnk-dev-setup] 설명 방법을 Windows 또는 Linux에서이 자습서에 대 한 tooinstall Node.js 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-119">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="93f29-120">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="93f29-120">An active Azure account.</span></span> <span data-ttu-id="93f29-121">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-121">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="93f29-122">Hello에 따라 [장치 관리 시작](iot-hub-node-node-device-management-get-started.md) 문서 toocreate IoT hub 및 IoT 허브 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-122">Follow hello [Get started with device management](iot-hub-node-node-device-management-get-started.md) article toocreate your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a><span data-ttu-id="93f29-123">직접 메서드를 사용 하 여 hello 장치에 대 한 원격 펌웨어 업데이트 트리거</span><span class="sxs-lookup"><span data-stu-id="93f29-123">Trigger a remote firmware update on hello device using a direct method</span></span>
<span data-ttu-id="93f29-124">이 섹션에서는 장치에서 원격 펌웨어 업데이트를 시작하는 Node.js 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-124">In this section, you create a Node.js console app that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="93f29-125">hello 앱 직접적인 방법 tooinitiate hello 업데이트를 사용 하 고 사용 하 여 장치로 이중 쿼리 tooperiodically hello 액티브 펌웨어 업데이트의 hello 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-125">hello app uses a direct method tooinitiate hello update and uses device twin queries tooperiodically get hello status of hello active firmware update.</span></span>

1. <span data-ttu-id="93f29-126">**triggerfwupdateondevice**라는 빈 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-126">Create an empty folder called **triggerfwupdateondevice**.</span></span>  <span data-ttu-id="93f29-127">Hello에 **triggerfwupdateondevice** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-127">In hello **triggerfwupdateondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="93f29-128">모든 hello 기본값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-128">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="93f29-129">Hello에 명령 프롬프트에 **triggerfwupdateondevice** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iot 허브** 및 **azure iot-장치 mqtt** 장치 SDK 패키지:</span><span class="sxs-lookup"><span data-stu-id="93f29-129">At your command prompt in hello **triggerfwupdateondevice** folder, run hello following command tooinstall hello **azure-iot-hub** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="93f29-130">텍스트 편집기를 사용 하 여 만들는 **dmpatterns_getstarted_service.js** hello에 대 한 파일 **triggerfwupdateondevice** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-130">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerfwupdateondevice** folder.</span></span>
4. <span data-ttu-id="93f29-131">Hello 다음 '필요' hello hello 시작 부분에 설명 추가 **dmpatterns_getstarted_service.js** 파일:</span><span class="sxs-lookup"><span data-stu-id="93f29-131">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="93f29-132">다음 변수 선언을 hello를 추가 하 고 hello 자리 표시자 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-132">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. <span data-ttu-id="93f29-133">Hello 다음 toofind 함수 값을 표시할 hello hello firmwareUpdate의 추가 속성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-133">Add hello following function toofind and display hello value of hello firmwareUpdate reported property.</span></span>
   
    ```
    var queryTwinFWUpdateReported = function() {
        registry.getTwin(deviceToUpdate, function(err, twin){
            if (err) {
              console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
            } else {
              console.log((JSON.stringify(twin.properties.reported.iothubDM.firmwareUpdate)) + "\n");
            }
        });
    };
    ```
7. <span data-ttu-id="93f29-134">Hello 함수 tooinvoke hello firmwareUpdate 메서드 tooreboot hello 대상 장치를 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-134">Add hello following function tooinvoke hello firmwareUpdate method tooreboot hello target device:</span></span>
   
    ```
    var startFirmwareUpdateDevice = function() {
      var params = {
          fwPackageUri: 'https://secureurl'
      };
   
      var methodName = "firmwareUpdate";
      var payloadData =  JSON.stringify(params);
   
      var methodParams = {
        methodName: methodName,
        payload: payloadData,
        timeoutInSeconds: 30
      };
   
      client.invokeDeviceMethod(deviceToUpdate, methodParams, function(err, result) {
        if (err) {
          console.error('Could not start hello firmware update on hello device: ' + err.message)
        } 
      });
    };
    ```
8. <span data-ttu-id="93f29-135">마지막으로 추가 hello 다음 toocode toostart hello 펌웨어 업데이트 시퀀스를 작동 하 고 정기적으로 표시 되기 시작 hello 속성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-135">Finally, Add hello following function toocode toostart hello firmware update sequence and start periodically showing hello reported properties:</span></span>
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. <span data-ttu-id="93f29-136">저장 후 닫기 hello **dmpatterns_fwupdate_service.js** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-136">Save and close hello **dmpatterns_fwupdate_service.js** file.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a><span data-ttu-id="93f29-137">Hello 앱 실행</span><span class="sxs-lookup"><span data-stu-id="93f29-137">Run hello apps</span></span>
<span data-ttu-id="93f29-138">준비 toorun hello 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-138">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="93f29-139">Hello에 대 한 hello 명령 프롬프트 **manageddevice** 폴더를 다음 명령 toobegin hello 재부팅 직접적인 방법에 대 한 수신 대기 하는 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-139">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="93f29-140">Hello에 대 한 hello 명령 프롬프트 **triggerfwupdateondevice** hello 명령 tootrigger hello 원격 다음를 실행 하는 폴더를 다시 부팅 하 고 hello 장치로 이중 toofind hello 마지막 시간을 다시 부팅에 대 한 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-140">At hello command prompt in hello **triggerfwupdateondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. <span data-ttu-id="93f29-141">Hello 장치 응답 toohello 직접적인 방법 hello 콘솔에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-141">You see hello device response toohello direct method in hello console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93f29-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="93f29-142">Next steps</span></span>
<span data-ttu-id="93f29-143">이 자습서에서는 직접적인 방법 tootrigger 원격을 사용 하는 장치 및 사용 하는 hello에 펌웨어 업데이트가 보고 되는 hello 펌웨어 업데이트의 속성 toofollow hello 진행률입니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-143">In this tutorial, you used a direct method tootrigger a remote firmware update on a device and used hello reported properties toofollow hello progress of hello firmware update.</span></span>

<span data-ttu-id="93f29-144">toolearn tooextend IoT 솔루션 및 일정 메서드를 여러 장치에서 호출 하는 방법 참조 hello [일정 및 브로드캐스트 작업] [ lnk-tutorial-jobs] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="93f29-144">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

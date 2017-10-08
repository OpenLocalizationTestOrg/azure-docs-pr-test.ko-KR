---
title: "Azure IoT Hub (노드)와 aaaGet 시작 | Microsoft Docs"
description: "Toosend 장치-클라우드 tooAzure IoT Sdk를 사용 하 여 Node.js에 대 한 IoT Hub를 메시지 하는 방법을 알아봅니다. 시뮬레이션 된 장치 및 서비스 응용 프로그램 tooregister 장치, 메시지를 보낼 만들고 IoT 허브에서 메시지를 읽은 합니다."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 56618522-9a31-42c6-94bf-55e2233b39ac
ms.service: iot-hub
ms.devlang: javascript
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0747895365f2359a9c38ea1e85a5881d6efec0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-node"></a><span data-ttu-id="e1333-104">노드를 사용 하 여 시뮬레이션 된 장치 tooyour IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-104">Connect your simulated device tooyour IoT hub using Node</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="e1333-105">이 자습서의 hello 끝 세 개의 Node.js 콘솔 앱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-105">At hello end of this tutorial, you have three Node.js console apps:</span></span>

* <span data-ttu-id="e1333-106">**CreateDeviceIdentity.js**, 장치 id를 만듦 및 연결 된 보안 키 tooconnect 시뮬레이션 된 장치 앱.</span><span class="sxs-lookup"><span data-stu-id="e1333-106">**CreateDeviceIdentity.js**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="e1333-107">**ReadDeviceToCloudMessages.js**, 시뮬레이션 된 장치 앱에서 보낸 hello 원격 분석을 표시 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-107">**ReadDeviceToCloudMessages.js**, which displays hello telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="e1333-108">**SimulatedDevice.js**, 이전에 만든 hello 장치 id를 가진 tooyour IoT 허브를 연결 하 고 MQTT 프로토콜 hello 하 여 모든 두 번째 원격 분석 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-108">**SimulatedDevice.js**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="e1333-109">hello 문서 [Azure IoT Sdk] [ lnk-hub-sdks] 사용할 수 있는 toobuild 두 응용 프로그램 toorun 장치와 솔루션 백 엔드에, Azure IoT Sdk hello에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="e1333-110">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="e1333-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="e1333-111">Node.js 버전 0.10.x 이상</span><span class="sxs-lookup"><span data-stu-id="e1333-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="e1333-112">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="e1333-112">An active Azure account.</span></span> <span data-ttu-id="e1333-113">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="e1333-114">IoT Hub를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-114">You have now created your IoT hub.</span></span> <span data-ttu-id="e1333-115">Hello IoT Hub 호스트 이름 및 hello IoT 허브 연결 문자열을이 자습서의 toocomplete hello 나머지 해야 하는 것이 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-115">You have hello IoT Hub host name and hello IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="e1333-116">장치 ID 만들기</span><span class="sxs-lookup"><span data-stu-id="e1333-116">Create a device identity</span></span>
<span data-ttu-id="e1333-117">이 섹션에서는 hello id 레지스트리에 IoT 허브에서에서 장치 id를 작성 하는 Node.js 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-117">In this section, you create a Node.js console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="e1333-118">장치는 hello identity 레지스트리에 항목을 설정한 경우에 tooIoT 허브를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-118">A device can only connect tooIoT hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="e1333-119">자세한 내용은 참조 hello **Id 레지스트리에** hello 섹션 [IoT 허브 개발자 가이드][lnk-devguide-identity]합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-119">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="e1333-120">이 콘솔 응용 프로그램을 실행 하면 고유한 장치 ID를 생성 및 메시지 tooIoT 허브를 키 장치-클라우드 보낼 때 장치가 tooidentify 자체를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-120">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="e1333-121">**createdeviceidentity**라는 새 빈 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-121">Create a new empty folder called **createdeviceidentity**.</span></span> <span data-ttu-id="e1333-122">Hello에 **createdeviceidentity** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-122">In hello **createdeviceidentity** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="e1333-123">모든 hello 기본값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-123">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="e1333-124">Hello에 명령 프롬프트에 **createdeviceidentity** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iothub** 서비스 SDK 패키지:</span><span class="sxs-lookup"><span data-stu-id="e1333-124">At your command prompt in hello **createdeviceidentity** folder, run hello following command tooinstall hello **azure-iothub** Service SDK package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="e1333-125">텍스트 편집기를 사용 하 여 만들는 **CreateDeviceIdentity.js** hello에 대 한 파일 **createdeviceidentity** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-125">Using a text editor, create a **CreateDeviceIdentity.js** file in hello **createdeviceidentity** folder.</span></span>
4. <span data-ttu-id="e1333-126">Hello 다음 추가 `require` hello 시작 시 hello 문이 **CreateDeviceIdentity.js** 파일:</span><span class="sxs-lookup"><span data-stu-id="e1333-126">Add hello following `require` statement at hello start of hello **CreateDeviceIdentity.js** file:</span></span>
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. <span data-ttu-id="e1333-127">다음 코드 toohello hello 추가 **CreateDeviceIdentity.js** 파일 및 hello hello 이전 섹션에서 만든 hello 허브에 대 한 IoT 허브 연결 문자열 hello 자리 표시자 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-127">Add hello following code toohello **CreateDeviceIdentity.js** file and replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello previous section:</span></span> 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="e1333-128">다음 코드 toocreate hello id 레지스트리에 IoT 허브에서에 장치 정의 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-128">Add hello following code toocreate a device definition in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="e1333-129">Hello 장치 ID hello id 레지스트리에 존재 하지 않는 경우이 코드에서는 장치, 그렇지 않으면 기존 장치 hello의 hello 키 반환:</span><span class="sxs-lookup"><span data-stu-id="e1333-129">This code creates a device if hello device ID does not exist in hello identity registry, otherwise it returns hello key of hello existing device:</span></span>
   
    ```
    var device = {
      deviceId: 'myFirstNodeDevice'
    }
    registry.create(device, function(err, deviceInfo, res) {
      if (err) {
        registry.get(device.deviceId, printDeviceInfo);
      }
      if (deviceInfo) {
        printDeviceInfo(err, deviceInfo, res)
      }
    });
   
    function printDeviceInfo(err, deviceInfo, res) {
      if (deviceInfo) {
        console.log('Device ID: ' + deviceInfo.deviceId);
        console.log('Device key: ' + deviceInfo.authentication.symmetricKey.primaryKey);
      }
    }
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="e1333-130">**CreateDeviceIdentity.js** 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-130">Save and close **CreateDeviceIdentity.js** file.</span></span>
8. <span data-ttu-id="e1333-131">toorun hello **createdeviceidentity** 응용 프로그램을 hello 다음 hello createdeviceidentity 폴더에 hello 명령 프롬프트에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-131">toorun hello **createdeviceidentity** application, execute hello following command at hello command prompt in hello createdeviceidentity folder:</span></span>
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. <span data-ttu-id="e1333-132">Hello 메모 **장치 ID** 및 **장치 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-132">Make a note of hello **Device ID** and **Device key**.</span></span> <span data-ttu-id="e1333-133">이 값이 필요 하면 이러한 나중 tooIoT 장치로 허브를 연결 하는 응용 프로그램을 만들 때.</span><span class="sxs-lookup"><span data-stu-id="e1333-133">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="e1333-134">IoT Hub id 레지스트리에 hello만 장치 identities tooenable 보안 액세스 toohello IoT 허브를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-134">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="e1333-135">장치 Id와 키 toouse 보안 자격 증명 및 개별 장치에 대 한 toodisable 액세스를 사용할 수 있는 사용/사용 안 함 플래그로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-135">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="e1333-136">응용 프로그램는 toostore 다른 장치 관련 메타 데이터를 필요한 경우에 응용 프로그램별 저장소를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-136">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="e1333-137">자세한 내용은 참조 hello [IoT 허브 개발자 가이드][lnk-devguide-identity]합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-137">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="e1333-138">장치-클라우드 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="e1333-138">Receive device-to-cloud messages</span></span>
<span data-ttu-id="e1333-139">이 섹션에서는 IoT Hub에서 장치-클라우드 메시지를 읽는 Node.js 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-139">In this section, you create a Node.js console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="e1333-140">IoT hub를 노출 한 [이벤트 허브][lnk-event-hubs-overview]-호환 되는 끝점 tooenable tooread 장치-클라우드 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-140">An IoT hub exposes an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="e1333-141">단순 tookeep 항목을이 자습서에서는 처리량이 높은 배포에 적합 하지 않은 기본 판독기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-141">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="e1333-142">hello [장치-클라우드 메시지를 처리] [ lnk-process-d2c-tutorial] 자습서에서는 배율로 tooprocess 장치-클라우드 메시지 방법을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-142">hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how tooprocess device-to-cloud messages at scale.</span></span> <span data-ttu-id="e1333-143">hello [이벤트 허브 시작] [ lnk-eventhubs-tutorial] 자습서 tooprocess 이벤트 허브에서 메시지를 하 고는 적용 가능한 toohello IoT 허브 이벤트 허브 호환 되지 않는 끝점 하는 방법에 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-143">hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how tooprocess messages from Event Hubs and is applicable toohello IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="e1333-144">hello 항상 장치-클라우드 메시지 도착 읽기에 대 한 이벤트 허브 호환 끝점 hello AMQP 프로토콜이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-144">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>
> 
> 

1. <span data-ttu-id="e1333-145">**readdevicetocloudmessages**라는 빈 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-145">Create an empty folder called **readdevicetocloudmessages**.</span></span> <span data-ttu-id="e1333-146">Hello에 **readdevicetocloudmessages** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-146">In hello **readdevicetocloudmessages** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="e1333-147">모든 hello 기본값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-147">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="e1333-148">Hello에 명령 프롬프트에 **readdevicetocloudmessages** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure-이벤트-허브** 패키지:</span><span class="sxs-lookup"><span data-stu-id="e1333-148">At your command prompt in hello **readdevicetocloudmessages** folder, run hello following command tooinstall hello **azure-event-hubs** package:</span></span>
   
    ```
    npm install azure-event-hubs --save
    ```
3. <span data-ttu-id="e1333-149">텍스트 편집기를 사용 하 여 만들는 **ReadDeviceToCloudMessages.js** hello에 대 한 파일 **readdevicetocloudmessages** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-149">Using a text editor, create a **ReadDeviceToCloudMessages.js** file in hello **readdevicetocloudmessages** folder.</span></span>
4. <span data-ttu-id="e1333-150">Hello 다음 추가 `require` hello의 시작 부분에 hello 문을 **ReadDeviceToCloudMessages.js** 파일:</span><span class="sxs-lookup"><span data-stu-id="e1333-150">Add hello following `require` statements at hello start of hello **ReadDeviceToCloudMessages.js** file:</span></span>
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. <span data-ttu-id="e1333-151">변수 선언 뒤 hello를 추가 하 고 hello 허브에 대 한 IoT 허브 연결 문자열 hello 자리 표시자 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-151">Add hello following variable declaration and replace hello placeholder value with hello IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. <span data-ttu-id="e1333-152">다음 출력 toohello 콘솔에 인쇄 하는 두 함수 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-152">Add hello following two functions that print output toohello console:</span></span>
   
    ```
    var printError = function (err) {
      console.log(err.message);
    };
   
    var printMessage = function (message) {
      console.log('Message received: ');
      console.log(JSON.stringify(message.body));
      console.log('');
    };
    ```
7. <span data-ttu-id="e1333-153">다음 코드 toocreate hello hello 추가 **EventHubClient**hello 연결 tooyour IoT 허브를 열고 각 파티션에 대 한 수신기 만들기.</span><span class="sxs-lookup"><span data-stu-id="e1333-153">Add hello following code toocreate hello **EventHubClient**, open hello connection tooyour IoT Hub, and create a receiver for each partition.</span></span> <span data-ttu-id="e1333-154">이 응용 프로그램 읽을 수 있도록 hello 수신기만 보낸 메시지 tooIoT 허브를 실행 하는 hello 수신기가 시작 되 면 수신기를 만들 때 필터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-154">This application uses a filter when it creates a receiver so that hello receiver only reads messages sent tooIoT Hub after hello receiver starts running.</span></span> <span data-ttu-id="e1333-155">이 필터는 hello 현재 집합에만 메시지를 참조 하므로 테스트 환경에서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-155">This filter is useful in a test environment so you see just hello current set of messages.</span></span> <span data-ttu-id="e1333-156">프로덕션 환경에서 코드를 모든 hello 메시지를 처리 하는지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-156">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="e1333-157">자세한 내용은 참조 hello [어떻게 tooprocess IoT Hub 장치-클라우드 메시지] [ lnk-process-d2c-tutorial] 자습서:</span><span class="sxs-lookup"><span data-stu-id="e1333-157">For more information, see hello [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial:</span></span>
   
    ```
    var client = EventHubClient.fromConnectionString(connectionString);
    client.open()
        .then(client.getPartitionIds.bind(client))
        .then(function (partitionIds) {
            return partitionIds.map(function (partitionId) {
                return client.createReceiver('$Default', partitionId, { 'startAfterTime' : Date.now()}).then(function(receiver) {
                    console.log('Created partition receiver: ' + partitionId)
                    receiver.on('errorReceived', printError);
                    receiver.on('message', printMessage);
                });
            });
        })
        .catch(printError);
    ```
8. <span data-ttu-id="e1333-158">저장 후 닫기 hello **ReadDeviceToCloudMessages.js** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-158">Save and close hello **ReadDeviceToCloudMessages.js** file.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="e1333-159">시뮬레이션된 장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="e1333-159">Create a simulated device app</span></span>
<span data-ttu-id="e1333-160">이 섹션에서는 tooan IoT hub 장치-클라우드 메시지를 전송 하는 장치를 시뮬레이션 하는 Node.js 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-160">In this section, you create a Node.js console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="e1333-161">**simulateddevice**라는 빈 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-161">Create an empty folder called **simulateddevice**.</span></span> <span data-ttu-id="e1333-162">Hello에 **simulateddevice** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-162">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="e1333-163">모든 hello 기본값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-163">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="e1333-164">Hello에 명령 프롬프트에 **simulateddevice** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iot 장치** 장치 SDK 패키지 및 **azure-iot-장치-mqtt**패키지:</span><span class="sxs-lookup"><span data-stu-id="e1333-164">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="e1333-165">텍스트 편집기를 사용 하 여 만들는 **SimulatedDevice.js** hello에 대 한 파일 **simulateddevice** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-165">Using a text editor, create a **SimulatedDevice.js** file in hello **simulateddevice** folder.</span></span>
4. <span data-ttu-id="e1333-166">Hello 다음 추가 `require` hello의 시작 부분에 hello 문을 **SimulatedDevice.js** 파일:</span><span class="sxs-lookup"><span data-stu-id="e1333-166">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. <span data-ttu-id="e1333-167">추가 **connectionString** 변수 toocreate를 사용 하는 **클라이언트** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="e1333-167">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="e1333-168">대체 **{youriothostname}** hello hello IoT 허브의 hello 이름으로 만든 *IoT 허브를 만듭니다.* 섹션.</span><span class="sxs-lookup"><span data-stu-id="e1333-168">Replace **{youriothostname}** with hello name of hello IoT hub you created hello *Create an IoT Hub* section.</span></span> <span data-ttu-id="e1333-169">대체 **{yourdevicekey}** hello에 생성 된 hello 장치 키 값을 가진 *장치 id를 만드는* 섹션:</span><span class="sxs-lookup"><span data-stu-id="e1333-169">Replace **{yourdevicekey}** with hello device key value you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. <span data-ttu-id="e1333-170">Hello 함수 toodisplay 출력 hello 응용 프로그램에서 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-170">Add hello following function toodisplay output from hello application:</span></span>
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="e1333-171">콜백을 만들고 hello를 사용 하 여 **setInterval** toosend 메시지 tooyour IoT hub 1 초 마다 함수:</span><span class="sxs-lookup"><span data-stu-id="e1333-171">Create a callback and use hello **setInterval** function toosend a message tooyour IoT hub every second:</span></span>
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
        // Create a message and send it toohello IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
8. <span data-ttu-id="e1333-172">Hello 연결 tooyour IoT 허브를 열고 메시지를 보내기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-172">Open hello connection tooyour IoT Hub and start sending messages:</span></span>
   
    ```
    client.open(connectCallback);
    ```
9. <span data-ttu-id="e1333-173">저장 후 닫기 hello **SimulatedDevice.js** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-173">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="e1333-174">단순 tookeep 항목을이 자습서는 어떠한 재시도 정책도 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-174">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="e1333-175">프로덕션 코드에서는 hello MSDN 문서에 설명 된 대로 다시 시도 정책 (예: 지 수 백오프)를 구현 해야 [일시적인 오류 처리][lnk-transient-faults]합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-175">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="run-hello-apps"></a><span data-ttu-id="e1333-176">Hello 앱 실행</span><span class="sxs-lookup"><span data-stu-id="e1333-176">Run hello apps</span></span>
<span data-ttu-id="e1333-177">준비 toorun hello 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-177">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="e1333-178">Hello에 명령 프롬프트에서 **readdevicetocloudmessages** hello IoT 허브를 모니터링 하는 명령 toobegin 다음를 실행 하는 폴더:</span><span class="sxs-lookup"><span data-stu-id="e1333-178">At a command prompt in hello **readdevicetocloudmessages** folder, run hello following command toobegin monitoring your IoT hub:</span></span>
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Node.js IoT 허브 서비스 응용 프로그램 toomonitor 장치-클라우드 메시지][7]
2. <span data-ttu-id="e1333-180">Hello에 명령 프롬프트에서 **simulateddevice** hello 명령 toobegin 보내는 원격 분석 데이터 tooyour IoT 허브를 따라를 실행 하는 폴더:</span><span class="sxs-lookup"><span data-stu-id="e1333-180">At a command prompt in hello **simulateddevice** folder, run hello following command toobegin sending telemetry data tooyour IoT hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Node.js IoT Hub 장치 앱 toosend 장치-클라우드 메시지][8]
3. <span data-ttu-id="e1333-182">hello **사용량** hello에 바둑판식으로 배열 [Azure 포털] [ lnk-portal] 표시 hello 보낸 메시지 toohello IoT 허브의 수:</span><span class="sxs-lookup"><span data-stu-id="e1333-182">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>
   
    ![Azure 포털 사용량 타일 보여 주는 수가 전송 된 메시지 tooIoT 허브][43]

## <a name="next-steps"></a><span data-ttu-id="e1333-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e1333-184">Next steps</span></span>
<span data-ttu-id="e1333-185">이 자습서에서는 hello Azure 포털에서에서 새 IoT 허브를 구성 하 고 id 레지스트리에 hello IoT hub에서 장치 id를 만든 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-185">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="e1333-186">이 장치 identity tooenable hello 시뮬레이션 된 장치 앱 toosend 장치-클라우드 메시지 toohello IoT 허브를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-186">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="e1333-187">또한 hello IoT 허브에서 수신 하는 hello 메시지를 표시 하는 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-187">You also created an app that displays hello messages received by hello IoT hub.</span></span> 

<span data-ttu-id="e1333-188">시작 toocontinue IoT 허브와 tooexplore 다른 IoT 시나리오를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e1333-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="e1333-189">[장치 연결][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="e1333-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="e1333-190">[장치 관리 시작][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="e1333-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="e1333-191">[Azure IoT Hub 시작][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="e1333-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="e1333-192">toolearn tooextend 배율 사용할 때 IoT 솔루션 및 프로세스 장치-클라우드 메시지를 확인 하려면 어떻게 hello [장치-클라우드 메시지를 처리] [ lnk-process-d2c-tutorial] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="e1333-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]


<!-- Images. -->
[7]: ./media/iot-hub-node-node-getstarted/runapp1.png
[8]: ./media/iot-hub-node-node-getstarted/runapp2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

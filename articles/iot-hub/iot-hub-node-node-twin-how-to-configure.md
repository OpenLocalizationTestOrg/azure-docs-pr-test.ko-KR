---
title: "aaaUse Azure IoT Hub 장치로 이중 속성 (노드) | Microsoft Docs"
description: "Azure IoT Hub 장치 toouse 트윈스 어떻게 tooconfigure 장치 시뮬레이션 된 장치 앱과 장치로 이중을 사용 하는 장치 구성을 수정 하는 서비스 응용 프로그램 Node.js tooimplement에 대 한 hello Azure IoT Sdk를 사용 합니다."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: d0bcec50-26e6-40f0-8096-733b2f3071ec
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: elioda
ms.openlocfilehash: 7ebfe2dfa0876bf04fdbaceae55db76456523e8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices-node"></a><span data-ttu-id="72552-104">사용 하 여 원하는 속성 tooconfigure 장치 (노드)</span><span class="sxs-lookup"><span data-stu-id="72552-104">Use desired properties tooconfigure devices (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="72552-105">이 자습서의 hello 끝 두 Node.js 콘솔 응용 프로그램 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-105">At hello end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="72552-106">**SimulateDeviceConfiguration.js**, 원하는 구성 업데이트를 대기 하 고 시뮬레이트된 구성 업데이트 프로세스의 hello 상태를 보고 하는 시뮬레이션 된 장치 앱.</span><span class="sxs-lookup"><span data-stu-id="72552-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="72552-107">**SetDesiredConfigurationAndQuery.js**, hello를 설정 하는 Node.js 백 엔드 앱, 원하는 장치에서 구성 및 쿼리 hello 업데이트 프로세스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-107">**SetDesiredConfigurationAndQuery.js**, a Node.js back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="72552-108">hello 문서 [Azure IoT Sdk] [ lnk-hub-sdks] toobuild를 사용할 수 있는, Azure IoT Sdk hello에 대 한 정보를 제공 장치와 백 엔드 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="72552-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="72552-109">toocomplete hello 다음 해야이 자습서:</span><span class="sxs-lookup"><span data-stu-id="72552-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="72552-110">Node.js 버전 0.10.x 이상</span><span class="sxs-lookup"><span data-stu-id="72552-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="72552-111">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="72552-111">An active Azure account.</span></span> <span data-ttu-id="72552-112">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72552-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="72552-113">Hello를 따른 경우 [장치 트윈스 시작] [ lnk-twin-tutorial] 자습서에서는 이미 있는 IoT hub 및 호출 하 여 장치 id **myDeviceId**; toohello 건너뛸수있습니다[ Hello 시뮬레이션 된 장치 앱 만들기] [ lnk-how-to-configure-createapp] 섹션.</span><span class="sxs-lookup"><span data-stu-id="72552-113">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**; and you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="72552-114">Hello 시뮬레이션 된 장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="72552-114">Create hello simulated device app</span></span>
<span data-ttu-id="72552-115">Tooyour 허브를 연결 하는 Node.js 콘솔 앱을 만들면이 섹션에서는 **myDeviceId**원하는 구성 업데이트 될 때까지 대기 하 고 시뮬레이션 hello 구성 업데이트 프로세스에서 업데이트를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-115">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="72552-116">**simulatedeviceconfiguration**라는 빈 폴더를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72552-116">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="72552-117">Hello에 **simulatedeviceconfiguration** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 새로운 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72552-117">In hello **simulatedeviceconfiguration** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="72552-118">모든 hello 기본값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="72552-119">Hello에 명령 프롬프트에 **simulatedeviceconfiguration** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iot 장치**, 및 **azure-iot-장치-mqtt**패키지:</span><span class="sxs-lookup"><span data-stu-id="72552-119">At your command prompt in hello **simulatedeviceconfiguration** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="72552-120">텍스트 편집기를 사용 하 여 만드는 새 **SimulateDeviceConfiguration.js** hello에 대 한 파일 **simulatedeviceconfiguration** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="72552-120">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in hello **simulatedeviceconfiguration** folder.</span></span>
4. <span data-ttu-id="72552-121">다음 코드 toohello hello 추가 **SimulateDeviceConfiguration.js** 파일을 찾아 hello 대체 **{장치 연결 문자열을 (를)** hello 장치 연결 문자열에서 복사한 경우 자리 표시자 있습니다 hello 만든 **myDeviceId** 장치 id가 없음:</span><span class="sxs-lookup"><span data-stu-id="72552-121">Add hello following code toohello **SimulateDeviceConfiguration.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    <span data-ttu-id="72552-122">hello **클라이언트** 개체 hello 장치에서 장치 트윈스와 모든 hello 메서드에 필요한 toointeract을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-122">hello **Client** object exposes all hello methods required toointeract with device twins from hello device.</span></span> <span data-ttu-id="72552-123">hello를 초기화 한 후 이전 코드 hello **클라이언트** 개체를 검색에 대 한 장치로 이중 hello **myDeviceId**, 원하는 속성에 hello 업데이트에 대 한 처리기를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-123">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId**, and attaches a handler for hello update on desired properties.</span></span> <span data-ttu-id="72552-124">hello 처리기 있는지 확인 hello configIds 비교 하 여 실제 구성 변경 요청은 설정한 다음 hello 구성 변경을 시작 하는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-124">hello handler verifies that there is an actual configuration change request by comparing hello configIds, then invokes a method that starts hello configuration change.</span></span>
   
    <span data-ttu-id="72552-125">참고 된 간단한 hello 위해서 hello 이전 코드는 하드 코딩 된 기본 hello 초기 구성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-125">Note that for hello sake of simplicity, hello previous code uses a hard-coded default for hello inital configuration.</span></span> <span data-ttu-id="72552-126">실제 앱은 아마도 로컬 저장소로부터 그 구성을 로드할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="72552-126">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="72552-127">장치 연결에서 원하는 속성 변경 이벤트를 한 번 내보냅니다 항상 모든 작업을 수행 하기 전에 원하는 속성을 변경 되는 실제 hello 임을 toocheck 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-127">Desired property change events are always emitted once at device connection, make sure toocheck that there is an actual change in hello desired properties before performing any action.</span></span>
   > 
   > 
5. <span data-ttu-id="72552-128">Hello hello 하기 전에 다음 추가 `client.open()` 호출:</span><span class="sxs-lookup"><span data-stu-id="72552-128">Add hello following methods before hello `client.open()` invocation:</span></span>
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    <span data-ttu-id="72552-129">hello **initConfigChange** 메서드가 업데이트 hello 구성 업데이트 요청 된 hello 로컬 장치로 이중 개체에 대해 속성을 보고 및 설정 상태를 너무 hello**보류 중인**, 다음 업데이트 hello 장치 로 hello 서비스에서 이중 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-129">hello **initConfigChange** method updates reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="72552-130">Hello 장치로 이중을 성공적으로 업데이트 한 후의 hello 실행을 종료 하는 장기 실행 프로세스를 시뮬레이션 **completeConfigChange**합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-130">After successfully updating hello device twin, it simulates a long running process that terminates in hello execution of **completeConfigChange**.</span></span> <span data-ttu-id="72552-131">이 메서드가 업데이트 hello 로컬 장치로 이중 너무 hello 상태 설정 속성을 보고의**성공** 및 hello 제거 **pendingConfig** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="72552-131">This method updates hello local device twin's reported properties setting hello status too**Success** and removing hello **pendingConfig** object.</span></span> <span data-ttu-id="72552-132">그런 다음 hello 장치로 이중 hello 서비스에 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-132">It then updates hello device twin on hello service.</span></span>
   
    <span data-ttu-id="72552-133">Hello 속성 toobe만 수정 지정 하 여 속성이 업데이트 되는 보고 하는 toosave 대역폭 (라는 **패치** 코드 위의 hello에), hello 전체 문서를 교체 하는 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-133">Note that, toosave bandwidth, reported properties are updated by specifying only hello properties toobe modified (named **patch** in hello above code), instead of replacing hello whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="72552-134">이 자습서는 동시 구성 업데이트에 대해 어떤 동작도 시뮬레이션하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72552-134">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="72552-135">일부 구성 업데이트 프로세스 hello 업데이트 실행 되는 동안 대상 구성의 변경 내용 수 tooaccommodate 수 있습니다, 그리고 및 기타 수 거부 오류 조건과 함께 tooqueue도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72552-135">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, others might have tooqueue them, and others could reject them with an error condition.</span></span> <span data-ttu-id="72552-136">특정 구성 프로세스에 대해 원하는 동작을 hello 고 hello 구성 변경 시작 하기 전에 hello 적절 한 논리를 추가 했는지 tooconsider를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-136">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
6. <span data-ttu-id="72552-137">Hello 장치 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-137">Run hello device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="72552-138">Hello 메시지를 확인 해야 `retrieved device twin`합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-138">You should see hello message `retrieved device twin`.</span></span> <span data-ttu-id="72552-139">실행 중인 hello 앱을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-139">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="72552-140">Hello 서비스 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="72552-140">Create hello service app</span></span>
<span data-ttu-id="72552-141">이 섹션에서는 앱을 만들는 Node.js 콘솔 해당 업데이트 hello *원하는 속성을* 와 연결 된 장치로 이중 hello에 **myDeviceId** 새 원격 분석 구성 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-141">In this section, you will create a Node.js console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="72552-142">다음 hello IoT 허브에 저장 된 hello 장치 트윈스 쿼리하고 hello 차이 hello 원하는 및 보고 hello 장치의 구성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-142">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="72552-143">**setdesiredandqueryapp**라는 빈 폴더를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72552-143">Create a new empty folder called **setdesiredandqueryapp**.</span></span> <span data-ttu-id="72552-144">Hello에 **setdesiredandqueryapp** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 새로운 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72552-144">In hello **setdesiredandqueryapp** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="72552-145">모든 hello 기본값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-145">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="72552-146">Hello에 명령 프롬프트에 **setdesiredandqueryapp** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iothub** 패키지:</span><span class="sxs-lookup"><span data-stu-id="72552-146">At your command prompt in hello **setdesiredandqueryapp** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. <span data-ttu-id="72552-147">텍스트 편집기를 사용 하 여 만드는 새 **SetDesiredAndQuery.js** hello에 대 한 파일 **addtagsandqueryapp** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="72552-147">Using a text editor, create a new **SetDesiredAndQuery.js** file in hello **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="72552-148">다음 코드 toohello hello 추가 **SetDesiredAndQuery.js** 파일을 찾아 hello 대체 **{iot 허브 연결 문자열을 (를)** 허브를 만들 때 복사한 IoT 허브 연결 문자열 hello로 자리 표시자 :</span><span class="sxs-lookup"><span data-stu-id="72552-148">Add hello following code toohello **SetDesiredAndQuery.js** file, and substitute hello **{iot hub connection string}** placeholder with hello IoT Hub connection string you copied when you created your hub:</span></span>
   
        'use strict';
        var iothub = require('azure-iothub');
        var uuid = require('node-uuid');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var newConfigId = uuid.v4();
                var newFrequency = process.argv[2] || "5m";
                var patch = {
                    properties: {
                        desired: {
                            telemetryConfig: {
                                configId: newConfigId,
                                sendFrequency: newFrequency
                            }
                        }
                    }
                }
                twin.update(patch, function(err) {
                    if (err) {
                        console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                    } else {
                        console.log(twin.deviceId + ' twin updated successfully');
                    }
                });
                setInterval(queryTwins, 10000);
            }
        });

    <span data-ttu-id="72552-149">hello **레지스트리** 개체 hello 서비스에서 장치 트윈스와 모든 hello 메서드에 필요한 toointeract을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-149">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="72552-150">hello를 초기화 한 후 이전 코드 hello **레지스트리** 개체를 검색에 대 한 장치로 이중 hello **myDeviceId**, 새 원격 분석 구성 개체를 사용 하 여 원하는 속성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-150">hello previous code, after it initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and updates its desired properties with a new telemetry configuration object.</span></span> <span data-ttu-id="72552-151">그 후 hello 호출 **queryTwins** 이벤트 10 초 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-151">After that, it calls hello **queryTwins** function event 10 seconds.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="72552-152">이 응용 프로그램은 설명 목적으로 10초 마다 IoT Hub를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-152">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="72552-153">사용 하 여 많은 장치와 toodetect 변경 내용이 아니라 걸쳐 toogenerate 사용자 용 보고서를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-153">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="72552-154">솔루션에 장치 이벤트의 실시간 알림이 필요한 경우 [쌍 알림][lnk-twin-notifications]을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-154">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
    > 
    ><span data-ttu-id="72552-155">에서도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72552-155">.</span></span>

1. <span data-ttu-id="72552-156">다음 코드 바로 전 hello hello 추가 `registry.getDeviceTwin()` 호출 tooimplement hello **queryTwins** 함수:</span><span class="sxs-lookup"><span data-stu-id="72552-156">Add hello following code right before hello `registry.getDeviceTwin()` invocation tooimplement hello **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log();
                    results.forEach(function(twin) {
                        var desiredConfig = twin.properties.desired.telemetryConfig;
                        var reportedConfig = twin.properties.reported.telemetryConfig;
                        console.log("Config report for: " + twin.deviceId);
                        console.log("Desired: ");
                        console.log(JSON.stringify(desiredConfig, null, 2));
                        console.log("Reported: ");
                        console.log(JSON.stringify(reportedConfig, null, 2));
                    });
                }
            });
        };
   
    <span data-ttu-id="72552-157">이전 코드 쿼리 hello hello IoT 허브에 저장 된 장치 트윈스 hello 및 인쇄 hello 원하는 및 원격 분석 구성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-157">hello previous code queries hello device twins stored in hello IoT hub and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="72552-158">Toohello 참조 [IoT Hub 쿼리 언어] [ lnk-query] toolearn toogenerate 서식 있는 모든 장치에서 보고 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="72552-158">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
2. <span data-ttu-id="72552-159">와 **SimulateDeviceConfiguration.js** hello 응용 프로그램을 실행, 실행:</span><span class="sxs-lookup"><span data-stu-id="72552-159">With **SimulateDeviceConfiguration.js** running, run hello application with:</span></span>
   
        node SetDesiredAndQuery.js 5m
   
    <span data-ttu-id="72552-160">Hello 보고 된 구성에서 변경 표시 되어야 **성공** 너무**보류 중인** 너무**성공** 다시 hello 새 활성 보내기 24 대신 5 분의 빈도 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="72552-160">You should see hello reported configuration change from **Success** too**Pending** too**Success** again with hello new active send frequency of five minutes instead of 24 hours.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="72552-161">hello 장치 보고서 작업 및 hello 쿼리 결과 사이 tooa 1 분 간의 지연이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72552-161">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="72552-162">이 매우 높은 대규모 tooenable hello 쿼리 인프라 toowork입니다.</span><span class="sxs-lookup"><span data-stu-id="72552-162">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="72552-163">단일 장치로 이중의 일관 된 뷰 tooretrieve hello를 사용 하 여 **getDeviceTwin** hello에 대 한 메서드 **레지스트리** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="72552-163">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="72552-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="72552-164">Next steps</span></span>
<span data-ttu-id="72552-165">원하는 구성으로 설정 하는이 자습서에서는 *원하는 속성을* 백 엔드 응용 프로그램을 변경 하 고 해당 상태를 보고 multi-step 업데이트 프로세스를 시뮬레이션 하는 시뮬레이션 된 장치 앱 toodetect 작성 및  *속성을 보고* toohello 장치로 이중 합니다.</span><span class="sxs-lookup"><span data-stu-id="72552-165">In this tutorial, you set a desired configuration as *desired properties* from a back-end app, and wrote a simulated device app toodetect that change and simulate a multi-step update process reporting its status as *reported properties* toohello device twin.</span></span>

<span data-ttu-id="72552-166">사용 하 여 hello 리소스 toolearn을 어떻게 수행 하려면:</span><span class="sxs-lookup"><span data-stu-id="72552-166">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="72552-167">hello 사용 하 여 장치에서 원격 분석 전송 [IoT 허브 시작] [ lnk-iothub-getstarted] 자습서</span><span class="sxs-lookup"><span data-stu-id="72552-167">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="72552-168">예약 또는 수행 큰 집합의 장치에 대 한 작업 참조 hello [일정 및 브로드캐스트 작업] [ lnk-schedule-jobs] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="72552-168">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="72552-169">대화형으로 (예: 사용자 제어 응용 프로그램에서 팬)를 설정 하는 장치 hello로 제어 [직접 메서드를 사용 하 여] [ lnk-methods-tutorial] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="72552-169">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-node-node-twin-how-to-configure.md#create-the-simulated-device-app

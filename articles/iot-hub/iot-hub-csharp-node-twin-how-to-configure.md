---
title: "aaaUse Azure IoT Hub 장치로 이중 속성 (.NET/노드) | Microsoft Docs"
description: "Azure IoT Hub 장치 toouse 트윈스 어떻게 tooconfigure 장치 Node.js tooimplement 시뮬레이션 된 장치 응용 프로그램에 대 한 hello Azure IoT 장치 SDK 및.NET tooimplement 장치로 이중을 사용 하는 장치 구성을 수정 하는 서비스 응용 프로그램에 대 한 Azure IoT 서비스 SDK hello를 사용 합니다."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: elioda
ms.openlocfilehash: 840a1b2e45f4763131299577583aa89015dcdd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a><span data-ttu-id="5e1fb-104">원하는 속성 tooconfigure 장치를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5e1fb-104">Use desired properties tooconfigure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="5e1fb-105">이 자습서의 hello 끝 두 콘솔 응용 프로그램 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-105">At hello end of this tutorial, you will have two console apps:</span></span>

* <span data-ttu-id="5e1fb-106">**SimulateDeviceConfiguration.js**, 원하는 구성 업데이트를 대기 하 고 시뮬레이트된 구성 업데이트 프로세스의 hello 상태를 보고 하는 시뮬레이션 된 장치 앱.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="5e1fb-107">**SetDesiredConfigurationAndQuery**, hello를 설정 하는.NET 백 엔드 앱, 원하는 장치에서 구성 및 쿼리 hello 업데이트 프로세스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-107">**SetDesiredConfigurationAndQuery**, a .NET back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="5e1fb-108">hello 문서 [Azure IoT Sdk] [ lnk-hub-sdks] toobuild를 사용할 수 있는, Azure IoT Sdk hello에 대 한 정보를 제공 장치와 백 엔드 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="5e1fb-109">toocomplete hello 다음 해야이 자습서:</span><span class="sxs-lookup"><span data-stu-id="5e1fb-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="5e1fb-110">Visual Studio 2015 또는 Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="5e1fb-111">Node.js 버전 0.10.x 이상</span><span class="sxs-lookup"><span data-stu-id="5e1fb-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="5e1fb-112">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-112">An active Azure account.</span></span> <span data-ttu-id="5e1fb-113">계정이 없는 경우 몇 분 내에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-113">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="5e1fb-114">Hello를 따른 경우 [장치 트윈스 시작] [ lnk-twin-tutorial] 자습서에서는 이미 있는 IoT hub 및 호출 하 여 장치 id **myDeviceId**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-114">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="5e1fb-115">이 경우 toohello 건너뛸 수 있습니다 [만들기 hello 시뮬레이션 된 장치 앱] [ lnk-how-to-configure-createapp] 섹션.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-115">In that case, you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="5e1fb-116">Hello 시뮬레이션 된 장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="5e1fb-116">Create hello simulated device app</span></span>
<span data-ttu-id="5e1fb-117">Tooyour 허브를 연결 하는 Node.js 콘솔 앱을 만들면이 섹션에서는 **myDeviceId**원하는 구성 업데이트 될 때까지 대기 하 고 시뮬레이션 hello 구성 업데이트 프로세스에서 업데이트를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-117">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="5e1fb-118">**simulatedeviceconfiguration**라는 빈 폴더를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-118">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="5e1fb-119">Hello에 **simulatedeviceconfiguration** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 새로운 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-119">In hello **simulatedeviceconfiguration** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="5e1fb-120">모든 hello 기본값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-120">Accept all hello defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="5e1fb-121">Hello에 명령 프롬프트에 **simulatedeviceconfiguration** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iot 장치** 및 **azure-iot-장치-mqtt**패키지:</span><span class="sxs-lookup"><span data-stu-id="5e1fb-121">At your command prompt in hello **simulatedeviceconfiguration** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="5e1fb-122">텍스트 편집기를 사용 하 여 만드는 새 **SimulateDeviceConfiguration.js** hello에 대 한 파일 **simulatedeviceconfiguration** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-122">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in hello **simulatedeviceconfiguration** folder.</span></span>
1. <span data-ttu-id="5e1fb-123">다음 코드 toohello hello 추가 **SimulateDeviceConfiguration.js** 파일을 찾아 hello 대체 **{장치 연결 문자열을 (를)** hello 장치 연결 문자열에서 복사한 경우 자리 표시자 있습니다 hello 만든 **myDeviceId** 장치 id가 없음:</span><span class="sxs-lookup"><span data-stu-id="5e1fb-123">Add hello following code toohello **SimulateDeviceConfiguration.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="5e1fb-124">hello **클라이언트** 개체 hello 장치에서 장치 트윈스와 모든 hello 메서드에 필요한 toointeract을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-124">hello **Client** object exposes all hello methods required toointeract with device twins from hello device.</span></span> <span data-ttu-id="5e1fb-125">이 코드를 hello 초기화 **클라이언트** 개체를 검색에 대 한 장치로 이중 hello **myDeviceId**, 다음에 hello 업데이트에 대 한 처리기를 연결 하 고 *원하는 속성을*합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-125">This code initializes hello **Client** object, retrieves hello device twin for **myDeviceId**, and then attaches a handler for hello update on *desired properties*.</span></span> <span data-ttu-id="5e1fb-126">hello 처리기 있는지 확인 hello configIds 비교 하 여 실제 구성 변경 요청은 설정한 다음 hello 구성 변경을 시작 하는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-126">hello handler verifies that there is an actual configuration change request by comparing hello configIds, then invokes a method that starts hello configuration change.</span></span>
   
    <span data-ttu-id="5e1fb-127">간단한 hello 위해서이 코드에서는 하드 코드 된 기본 hello 초기 구성에 대 한 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-127">Note that for hello sake of simplicity, this code uses a hard-coded default for hello initial configuration.</span></span> <span data-ttu-id="5e1fb-128">실제 앱은 아마도 로컬 저장소로부터 그 구성을 로드할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-128">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="5e1fb-129">원하는 속성 변경 이벤트는 장치 연결 시 한 번만 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-129">Desired property change events are always emitted once at device connection.</span></span> <span data-ttu-id="5e1fb-130">작업을 수행 하기 전에 원하는 속성을 변경 되는 실제 hello 임을 toocheck 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-130">Make sure toocheck that there is an actual change in hello desired properties before performing any action.</span></span>
   > 
   > 
1. <span data-ttu-id="5e1fb-131">Hello hello 하기 전에 다음 추가 `client.open()` 호출:</span><span class="sxs-lookup"><span data-stu-id="5e1fb-131">Add hello following methods before hello `client.open()` invocation:</span></span>
   
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
   
    <span data-ttu-id="5e1fb-132">hello **initConfigChange** 메서드 업데이트 hello 너무 hello 구성 사용 하 여 hello 로컬 장치로 이중 개체의 속성 업데이트 요청 및 집합 hello 상태 보고**보류 중인**, 다음 업데이트 hello hello 서비스에 장치로 이중 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-132">hello **initConfigChange** method updates hello reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="5e1fb-133">Hello 장치로 이중을 성공적으로 업데이트 한 후의 hello 실행을 종료 하는 장기 실행 프로세스를 시뮬레이션 **completeConfigChange**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-133">After successfully updating hello device twin, it simulates a long running process that terminates in hello execution of **completeConfigChange**.</span></span> <span data-ttu-id="5e1fb-134">이 메서드는 hello 로컬 보고 속성 너무 hello 상태 설정 업데이트**성공** 및 hello 제거 **pendingConfig** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-134">This method updates hello local reported properties setting hello status too**Success** and removing hello **pendingConfig** object.</span></span> <span data-ttu-id="5e1fb-135">그런 다음 hello 장치로 이중 hello 서비스에 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-135">It then updates hello device twin on hello service.</span></span>
   
    <span data-ttu-id="5e1fb-136">Hello 속성 toobe만 수정 지정 하 여 속성이 업데이트 되는 보고 하는 toosave 대역폭 (라는 **패치** 코드 위의 hello에), hello 전체 문서를 교체 하는 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-136">Note that, toosave bandwidth, reported properties are updated by specifying only hello properties toobe modified (named **patch** in hello above code), instead of replacing hello whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5e1fb-137">이 자습서는 동시 구성 업데이트에 대해 어떤 동작도 시뮬레이션하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-137">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="5e1fb-138">일부 구성 업데이트 프로세스 hello 업데이트 실행 되는 동안 대상 구성의 변경 내용 수 tooaccommodate 수 있습니다, 그리고 일부 tooqueue 고, 일부 수 거부 오류 조건과 함께 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-138">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, some might have tooqueue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="5e1fb-139">특정 구성 프로세스에 대해 원하는 동작을 hello 고 hello 구성 변경 시작 하기 전에 hello 적절 한 논리를 추가 했는지 tooconsider를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-139">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="5e1fb-140">Hello 장치 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-140">Run hello device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="5e1fb-141">Hello 메시지를 확인 해야 `retrieved device twin`합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-141">You should see hello message `retrieved device twin`.</span></span> <span data-ttu-id="5e1fb-142">실행 중인 hello 앱을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-142">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="5e1fb-143">Hello 서비스 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="5e1fb-143">Create hello service app</span></span>
<span data-ttu-id="5e1fb-144">이 섹션에서는 만듭니다.NET 콘솔 응용 프로그램 업데이트 hello 해당 *원하는 속성을* 와 연결 된 장치로 이중 hello에 **myDeviceId** 새 원격 분석 구성 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-144">In this section, you will create a .NET console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="5e1fb-145">다음 hello IoT 허브에 저장 된 hello 장치 트윈스 쿼리하고 hello 차이 hello 원하는 및 보고 hello 장치의 구성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-145">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="5e1fb-146">Visual Studio에서 Visual C# Windows 클래식 데스크톱 프로젝트 toohello 현재 솔루션 hello를 사용 하 여 추가 **콘솔 응용 프로그램** 서식 파일 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-146">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="5e1fb-147">이름 hello 프로젝트 **SetDesiredConfigurationAndQuery**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-147">Name hello project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][img-createapp]
1. <span data-ttu-id="5e1fb-149">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **SetDesiredConfigurationAndQuery** 프로젝트를 마우스 클릭 **NuGet 패키지 관리...** .</span><span class="sxs-lookup"><span data-stu-id="5e1fb-149">In Solution Explorer, right-click hello **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="5e1fb-150">Hello에 **NuGet 패키지 관리자** 창에서 **찾아보기**, 검색할 **microsoft.azure.devices**선택, **설치** tooinstall hello **Microsoft.Azure.Devices** 패키지 및 hello 사용 약관에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-150">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="5e1fb-151">이 절차를 다운로드, 설치 하 고 참조 toohello 추가 [Azure IoT 서비스 SDK] [ lnk-nuget-service-sdk] NuGet 패키지 및 해당 종속성.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-151">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 패키지 관리자 창][img-servicenuget]
1. <span data-ttu-id="5e1fb-153">Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:</span><span class="sxs-lookup"><span data-stu-id="5e1fb-153">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="5e1fb-154">다음 필드 toohello hello 추가 **프로그램** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="5e1fb-155">Hello hello 이전 섹션에서 만든 hello 허브에 대 한 IoT 허브 연결 문자열 hello 자리 표시자 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-155">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="5e1fb-156">다음 메서드 toohello hello 추가 **프로그램** 클래스:</span><span class="sxs-lookup"><span data-stu-id="5e1fb-156">Add hello following method toohello **Program** class:</span></span>
   
        static private async Task SetDesiredConfigurationAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch = new {
                    properties = new {
                        desired = new {
                            telemetryConfig = new {
                                configId = Guid.NewGuid().ToString(),
                                sendFrequency = "5m"
                            }
                        }
                    }
                };
   
            await registryManager.UpdateTwinAsync(twin.DeviceId, JsonConvert.SerializeObject(patch), twin.ETag);
            Console.WriteLine("Updated desired configuration");
   
            try
            {
                while (true)
                {
                    var query = registryManager.CreateQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'");
                    var results = await query.GetNextAsTwinAsync();
                    foreach (var result in results)
                    {
                        Console.WriteLine("Config report for: {0}", result.DeviceId);
                        Console.WriteLine("Desired telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Desired["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine("Reported telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Reported["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine();
                    }
                    Thread.Sleep(10000);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Exception: {ex.Message}");
            }
        }
   
    <span data-ttu-id="5e1fb-157">hello **레지스트리** 개체 hello 서비스에서 장치 트윈스와 모든 hello 메서드에 필요한 toointeract을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-157">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="5e1fb-158">이 코드를 hello 초기화 **레지스트리** 개체를 검색에 대 한 장치로 이중 hello **myDeviceId**, 한 후 새 원격 분석 구성 개체를으로 원하는 속성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-158">This code initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="5e1fb-159">그 후 hello 장치 트윈스 10 초 마다 hello IoT 허브에 저장 된 쿼리 및 인쇄 hello 원하는 및 원격 분석 구성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-159">After that, it queries hello device twins stored in hello IoT hub every 10 seconds, and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="5e1fb-160">Toohello 참조 [IoT Hub 쿼리 언어] [ lnk-query] toolearn toogenerate 서식 있는 모든 장치에서 보고 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-160">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="5e1fb-161">이 응용 프로그램은 설명 목적으로 10초 마다 IoT Hub를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-161">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="5e1fb-162">사용 하 여 많은 장치와 toodetect 변경 내용이 아니라 걸쳐 toogenerate 사용자 용 보고서를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-162">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="5e1fb-163">솔루션에 장치 이벤트의 실시간 알림이 필요한 경우 [쌍 알림][lnk-twin-notifications]을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-163">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="5e1fb-164">마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:</span><span class="sxs-lookup"><span data-stu-id="5e1fb-164">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. <span data-ttu-id="5e1fb-165">Hello 솔루션 탐색기를 열고 hello **설정 시작 프로젝트...**  hello 있는지를 확인 하 고 **동작** 에 대 한 **SetDesiredConfigurationAndQuery** 프로젝트는 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-165">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="5e1fb-166">Hello 솔루션을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-166">Build hello solution.</span></span>
1. <span data-ttu-id="5e1fb-167">와 **SimulateDeviceConfiguration.js** 에서 Visual Studio를 사용 하 여 hello.NET 응용 프로그램 실행, 실행 **F5** hello 보고 된 구성에서 변경 하면 볼 **성공** 너무**보류 중인** 너무**성공** 다시 hello 새 활성 대신 24 시간 동안 5 분의 빈도 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-167">With **SimulateDeviceConfiguration.js** running, run hello .NET application from Visual Studio using **F5** and you should see hello reported configuration change from **Success** too**Pending** too**Success** again with hello new active send frequency of five minutes instead of 24 hours.</span></span>

 ![장치가 성공적으로 구성됨][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="5e1fb-169">hello 장치 보고서 작업 및 hello 쿼리 결과 사이 tooa 1 분 간의 지연이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-169">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="5e1fb-170">이 매우 높은 대규모 tooenable hello 쿼리 인프라 toowork입니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-170">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="5e1fb-171">단일 장치로 이중의 일관 된 뷰 tooretrieve hello를 사용 하 여 **getDeviceTwin** hello에 대 한 메서드 **레지스트리** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-171">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="5e1fb-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5e1fb-172">Next steps</span></span>
<span data-ttu-id="5e1fb-173">이 자습서에서는으로 원하는 구성을 설정 하면 *원하는 속성을* hello 솔루션에서 백 엔드를 하 고 변경 하 고 보고 하는 hello 통해 해당 상태를 보고 multi-step 업데이트 프로세스를 시뮬레이션 하는 장치 앱 toodetect 작성 했습니다. 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-173">In this tutorial, you set a desired configuration as *desired properties* from hello solution back end, and wrote a device app toodetect that change and simulate a multi-step update process reporting its status through hello reported properties.</span></span>

<span data-ttu-id="5e1fb-174">사용 하 여 hello 리소스 toolearn을 어떻게 수행 하려면:</span><span class="sxs-lookup"><span data-stu-id="5e1fb-174">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="5e1fb-175">hello 사용 하 여 장치에서 원격 분석 전송 [IoT 허브 시작] [ lnk-iothub-getstarted] 자습서</span><span class="sxs-lookup"><span data-stu-id="5e1fb-175">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="5e1fb-176">예약 또는 수행 큰 집합의 장치에 대 한 작업 참조 hello [일정 및 브로드캐스트 작업] [ lnk-schedule-jobs] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-176">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="5e1fb-177">대화형으로 (예: 사용자 제어 응용 프로그램에서 팬)를 설정 하는 장치 hello로 제어 [직접 메서드를 사용 하 여] [ lnk-methods-tutorial] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="5e1fb-177">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-node-twin-how-to-configure/deviceconfigured.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

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
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-csharp-node-twin-how-to-configure.md#create-the-simulated-device-app

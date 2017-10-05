---
title: "Azure IoT Hub 장치 쌍 시작(노드) | Microsoft Docs"
description: "Azure IoT Hub 장치 쌍을 사용하여 태그를 추가한 다음 IoT Hub 쿼리를 사용하는 방법입니다. Node.js용 Azure IoT SDK를 사용하여 시뮬레이션된 장치 앱 및 태그를 추가하고 IoT Hub 쿼리를 실행하는 서비스 앱을 구현합니다."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: 314c88e4-cce1-441c-b75a-d2e08e39ae7d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.openlocfilehash: 633c9fd4f8a1d017d93148f8c2e860ccba14238c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-device-twins-node"></a><span data-ttu-id="2d2c9-104">장치 쌍 시작(노드)</span><span class="sxs-lookup"><span data-stu-id="2d2c9-104">Get started with device twins (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="2d2c9-105">이 자습서의 끝 부분에 다음 두 개의 Node.js 콘솔 앱이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-105">At the end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="2d2c9-106">**AddTagsAndQuery.js**, 태그를 추가하고 장치 쌍을 쿼리하는 Node.js 백 엔드 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-106">**AddTagsAndQuery.js**, a Node.js back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="2d2c9-107">**TwinSimulatedDevice.js** - 앞에서 만든 장치 ID와 IoT Hub를 연결하고 연결 상태를 보고하는 장치를 시뮬레이션하는 Node.js 앱.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="2d2c9-108">[Azure IoT SDK][lnk-hub-sdks] 문서는 장치 및 백 엔드 앱을 빌드하는 데 사용할 수 있는 Azure IoT SDK에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="2d2c9-109">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="2d2c9-110">Node.js 버전 0.10.x 이상</span><span class="sxs-lookup"><span data-stu-id="2d2c9-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="2d2c9-111">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-111">An active Azure account.</span></span> <span data-ttu-id="2d2c9-112">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-service-app"></a><span data-ttu-id="2d2c9-113">서비스 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="2d2c9-113">Create the service app</span></span>
<span data-ttu-id="2d2c9-114">이 섹션에서는 **myDeviceId**와 연결된 장치 쌍에 위치 메타데이터를 추가하는 Node.js 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-114">In this section, you create a Node.js console app that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="2d2c9-115">그런 다음 IoT Hub에 저장된 장치 쌍을 쿼리하여 미국에 있는 장치를 선택한 다음 셀룰러 연결을 보고하는 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-115">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that are reporting a cellular connection.</span></span>

1. <span data-ttu-id="2d2c9-116">**addtagsandqueryapp**라는 빈 폴더를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-116">Create a new empty folder called **addtagsandqueryapp**.</span></span> <span data-ttu-id="2d2c9-117">**addtagsandqueryapp** 폴더의 명령 프롬프트에 다음 명령을 사용하여 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-117">In the **addtagsandqueryapp** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="2d2c9-118">모든 기본값을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="2d2c9-119">**addtagsandqueryapp** 폴더의 명령 프롬프트에서 다음 명령을 실행하여 **azure-iothub** 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-119">At your command prompt in the **addtagsandqueryapp** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="2d2c9-120">텍스트 편집기를 사용하여 **addtagsandqueryapp** 폴더에 새 **AddTagsAndQuery.js** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-120">Using a text editor, create a new **AddTagsAndQuery.js** file in the **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="2d2c9-121">다음 코드를 **AddTagsAndQuery.js** 파일에 추가하고 허브를 만들 때 복사한 IoT Hub 연결 문자열을 사용해 **{iot hub 연결 문자열}** 자리 표시자를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-121">Add the following code to the **AddTagsAndQuery.js** file, and substitute the **{iot hub connection string}** placeholder with the IoT Hub connection string you copied when you created your hub:</span></span>
   
        'use strict';
        var iothub = require('azure-iothub');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var patch = {
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                      }
                    }
                };
   
                twin.update(patch, function(err) {
                  if (err) {
                    console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                  } else {
                    console.log(twin.deviceId + ' twin updated successfully');
                    queryTwins();
                  }
                });
            }
        });
   
    <span data-ttu-id="2d2c9-122">**레지스트리** 개체는 서비스의 장치 쌍을 조작하는 데 필요한 모든 메서드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-122">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="2d2c9-123">이전 코드는 **Registry** 개체를 초기화한 다음 **myDeviceId**에 대한 장치 쌍을 검색하고, 마지막으로 원하는 위치 정보를 사용해 태그를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-123">The previous code first initializes the **Registry** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="2d2c9-124">태그를 업데이트한 후 **queryTwins** 함수를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-124">After the updating the tags it calls the **queryTwins** function.</span></span>
5. <span data-ttu-id="2d2c9-125">다음 코드를 **queryTwins** 함수를 구현할 **AddTagsAndQuery.js** 끝 부분에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-125">Add the following code at the end of  **AddTagsAndQuery.js** to implement the **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    <span data-ttu-id="2d2c9-126">이전 코드는 두 개의 쿼리를 실행합니다. 첫 번째는 **Redmond43** 공장에 위치한 장치의 장치 쌍만을 선택하고, 두 번째는 또한 셀룰러 네트워크를 통해서 연결된 장치만을 선택하기 위해 쿼리를 구체화합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-126">The previous code executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="2d2c9-127">이전 코드는 **쿼리** 개체를 만들 때 반환되는 최대 문서 수를 지정한다는 점에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-127">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="2d2c9-128">**query** 개체에는 모든 결과를 검색하기 위해 여러번 **nextAsTwin** 메서드를 호출하는 데 사용할 수 있는 **hasMoreResults** 부울 속성이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-128">The **query** object contains a **hasMoreResults** boolean property that you can use to invoke the **nextAsTwin** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="2d2c9-129">**next**라는 메서드는 장치 쌍이 아닌 결과(예: 집계 쿼리의 결과)에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-129">A method called **next** is available for results that are not device twins for example, results of aggregation queries.</span></span>
6. <span data-ttu-id="2d2c9-130">키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-130">Run the application with:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="2d2c9-131">**Redmond43**에 위치한 모든 장치를 요청하는 쿼리에 대한 결과로는 하나의 장치를 보고 셀룰러 네트워크를 사용하는 장치에 대해서는 결과를 제한하는 쿼리에 대한 결과로는 아무 장치도 볼 수 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-131">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![][1]

<span data-ttu-id="2d2c9-132">다음 섹션에서는 연결 정보를 보고하고 이전 섹션의 쿼리 결과를 변경하는 장치 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-132">In the next section you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="2d2c9-133">장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="2d2c9-133">Create the device app</span></span>
<span data-ttu-id="2d2c9-134">이 섹션에서는 **myDeviceId**로 허브에 연결하는 Node.js 콘솔 앱을 만들고 셀룰러 네트워크를 사용하여 연결된 정보를 포함하도록 장치 쌍의 reported 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-134">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, and then updates its device twin's reported properties to contain the information that it is connected using a cellular network.</span></span>

> [!NOTE]
> <span data-ttu-id="2d2c9-135">현재 장치 쌍은 MQTT 프로토콜을 사용하여 IoT Hub에 연결하는 장치에서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-135">At this time, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="2d2c9-136">기존 장치 앱이 MQTT를 사용하도록 변환하는 방법에 관한 설명은 [MQTT 지원][lnk-devguide-mqtt] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-136">Please refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>
> 
> 

1. <span data-ttu-id="2d2c9-137">**reportconnectivity**라는 빈 폴더를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-137">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="2d2c9-138">**reportconnectivity** 폴더의 명령 프롬프트에서 다음 명령을 사용하여 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-138">In the **reportconnectivity** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="2d2c9-139">모든 기본값을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-139">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="2d2c9-140">**reportconnectivity** 폴더의 명령 프롬프트에서 다음 명령을 실행하여 **azure-iot-device** 및 **azure-iot-device-mqtt** 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-140">At your command prompt in the **reportconnectivity** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="2d2c9-141">텍스트 편집기를 사용하여 **reportconnectivity** 폴더에 새 **ReportConnectivity.js** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-141">Using a text editor, create a new **ReportConnectivity.js** file in the **reportconnectivity** folder.</span></span>
4. <span data-ttu-id="2d2c9-142">다음 코드를 **ReportConnectivity.js** 파일에 추가하고 **myDeviceId** 장치 ID를 만들 때 복사한 장치 연결 문자열을 사용해 **{장치 연결 문자열}** 자리 표시자를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-142">Add the following code to the **ReportConnectivity.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    <span data-ttu-id="2d2c9-143">**Client** 개체는 서비스의 장치 쌍을 조작하는 데 필요한 모든 메서드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-143">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="2d2c9-144">이전 코드에서는 **Client** 개체를 초기화한 다음 **myDeviceId**에 대한 장치 쌍을 검색하고, 연결 정보로 reported 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-144">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId** and updates its reported property with the connectivity information.</span></span>
5. <span data-ttu-id="2d2c9-145">장치 앱 실행</span><span class="sxs-lookup"><span data-stu-id="2d2c9-145">Run the device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="2d2c9-146">메시지 `twin state reported`이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-146">You should see the message `twin state reported`.</span></span>
6. <span data-ttu-id="2d2c9-147">장치가 연결 정보를 보고했으므로 두 쿼리 모두에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-147">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="2d2c9-148">**addtagsandqueryapp** 폴더로 돌아가 쿼리를 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-148">Go back in the **addtagsandqueryapp** folder and run the queries again:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="2d2c9-149">이번에는 **myDeviceId**가 두 쿼리 결과에 모두 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-149">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][3]

## <a name="next-steps"></a><span data-ttu-id="2d2c9-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2d2c9-150">Next steps</span></span>
<span data-ttu-id="2d2c9-151">이 자습서에서는 Azure Portal에서 새 IoT Hub를 구성한 다음, IoT Hub의 ID 레지스트리에서 장치 ID를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-151">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="2d2c9-152">백 엔드 앱에서 tags로 장치 메타데이터를 추가하고, 장치 쌍에서 장치 연결 정보를 보고하는 시뮬레이션된 장치 앱을 작성했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-152">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="2d2c9-153">또한 SQL과 유사한 IoT Hub 쿼리 언어를 사용하여 이 정보를 쿼리하는 방법도 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-153">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="2d2c9-154">아래와 같이 실행할 방법을 알아보려면 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-154">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="2d2c9-155">[IoT Hub 시작][lnk-iothub-getstarted] 자습서를 참조하여 장치에서 원격 분석을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-155">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="2d2c9-156">[desired 속성을 사용하여 장치 구성][lnk-twin-how-to-configure] 자습서를 참조하여 장치 쌍의 desired 속성을 사용하여 장치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-156">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="2d2c9-157">[직접 메서드 사용][lnk-methods-tutorial] 자습서를 참조하여 대화형으로(예: 사용자가 제어하는 앱에서 팬을 켬) 장치를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2c9-157">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[1]: media/iot-hub-node-node-twin-getstarted/service1.png
[3]: media/iot-hub-node-node-twin-getstarted/service2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

[lnk-twin-how-to-configure]: iot-hub-node-node-twin-how-to-configure.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

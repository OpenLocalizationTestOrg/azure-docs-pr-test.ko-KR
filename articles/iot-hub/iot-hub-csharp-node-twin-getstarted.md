---
title: "Azure IoT Hub 장치 트윈스 (.NET/노드) aaaGet 시작 | Microsoft Docs"
description: "어떻게 toouse Azure IoT Hub 장치 트윈스 tooadd 태그를 삽입 하 고 IoT Hub 쿼리를 사용 합니다. Node.js tooimplement hello 시뮬레이션 된 장치 앱과 hello.NET tooimplement hello 태그를 추가 하 고 hello IoT Hub 쿼리를 실행 하는 서비스 응용 프로그램에 대 한 Azure IoT 서비스 SDK에 대 한 hello Azure IoT 장치 SDK를 사용 합니다."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: elioda
ms.openlocfilehash: 1cec082ebddc19c9b87998a5fd0159d32b07acd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnode"></a><span data-ttu-id="290a9-104">장치 쌍(.NET/노드) 시작</span><span class="sxs-lookup"><span data-stu-id="290a9-104">Get started with device twins (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="290a9-105">이 자습서의 hello 끝 해야 합니다는.NET 및 Node.js 콘솔 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="290a9-105">At hello end of this tutorial, you will have a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="290a9-106">**AddTagsAndQuery.sln**, 태그를 추가하고 장치 쌍을 쿼리하는 .NET 백 엔드 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-106">**AddTagsAndQuery.sln**, a .NET back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="290a9-107">**TwinSimulatedDevice.js**, 이전에 만든 hello 장치 id를 가진 tooyour IoT 허브를 연결 하는 장치를 시뮬레이션 하 고 해당 연결 상태를 보고 하는 Node.js 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="290a9-108">hello 문서 [Azure IoT Sdk] [ lnk-hub-sdks] toobuild를 사용할 수 있는, Azure IoT Sdk hello에 대 한 정보를 제공 장치와 백 엔드 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="290a9-109">toocomplete hello 다음 해야이 자습서:</span><span class="sxs-lookup"><span data-stu-id="290a9-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="290a9-110">Visual Studio 2015 또는 Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="290a9-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="290a9-111">Node.js 버전 0.10.x 이상</span><span class="sxs-lookup"><span data-stu-id="290a9-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="290a9-112">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="290a9-112">An active Azure account.</span></span> <span data-ttu-id="290a9-113">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a><span data-ttu-id="290a9-114">Hello 서비스 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="290a9-114">Create hello service app</span></span>
<span data-ttu-id="290a9-115">이 섹션에서는.NET 콘솔 응용 프로그램 (사용 하 여 C#) 위치 메타 데이터 toohello 장치로 이중와 관련 된 추가 하는 만들게 **myDeviceId**합니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-115">In this section, you create a .NET console app (using C#) that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="290a9-116">Hello 장치 트윈스 US, hello에 있는 hello 장치를 선택 하는 hello IoT 허브에 저장 하 고 셀룰러 연결을 보고 하는 스토리를 hello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-116">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="290a9-117">Visual Studio에서 Visual C# Windows 클래식 데스크톱 프로젝트 toohello 현재 솔루션 hello를 사용 하 여 추가 **콘솔 응용 프로그램** 서식 파일 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="290a9-117">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="290a9-118">이름 hello 프로젝트 **AddTagsAndQuery**합니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-118">Name hello project **AddTagsAndQuery**.</span></span>
   
    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][img-createapp]
1. <span data-ttu-id="290a9-120">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **AddTagsAndQuery** 프로젝트를 마우스 클릭 **NuGet 패키지 관리...** .</span><span class="sxs-lookup"><span data-stu-id="290a9-120">In Solution Explorer, right-click hello **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="290a9-121">Hello에 **NuGet 패키지 관리자** 창에서 **찾아보기** 검색 한 **microsoft.azure.devices**합니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-121">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="290a9-122">선택 **설치** tooinstall hello **Microsoft.Azure.Devices** 패키지 및 hello 사용 약관에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-122">Select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="290a9-123">이 절차를 다운로드, 설치 하 고 참조 toohello 추가 [Azure IoT 서비스 SDK] [ lnk-nuget-service-sdk] NuGet 패키지 및 해당 종속성.</span><span class="sxs-lookup"><span data-stu-id="290a9-123">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 패키지 관리자 창][img-servicenuget]
1. <span data-ttu-id="290a9-125">Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:</span><span class="sxs-lookup"><span data-stu-id="290a9-125">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="290a9-126">다음 필드 toohello hello 추가 **프로그램** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-126">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="290a9-127">Hello hello 이전 섹션에서 만든 hello 허브에 대 한 IoT 허브 연결 문자열 hello 자리 표시자 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-127">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="290a9-128">다음 메서드 toohello hello 추가 **프로그램** 클래스:</span><span class="sxs-lookup"><span data-stu-id="290a9-128">Add hello following method toohello **Program** class:</span></span>
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    <span data-ttu-id="290a9-129">hello **RegistryManager** hello 서비스에서 장치 트윈스와 모든 hello 메서드에 필요한 toointeract 클래스를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-129">hello **RegistryManager** class exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="290a9-130">hello 이전 코드는 먼저 hello 초기화 **registryManager** 개체를 검색에 대 한 장치로 이중 hello **myDeviceId**, 원하는 hello 위치 정보를 사용 하 여 해당 태그를 마지막으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-130">hello previous code first initializes hello **registryManager** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="290a9-131">두 개의 쿼리를 업데이트 한 후 실행: hello에 있는 장치의 장치 트윈스만 hello를 먼저 선택 하는 hello **Redmond43** 공장 별, 및 hello 두 번째 구체화 hello 쿼리 tooselect hello 장치만 또한 통해 연결 된 셀룰러 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-131">After updating, it executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="290a9-132">Hello를 만들 때 해당 hello 이전 코드 참고 **쿼리** 개체, 반환 된 문서의 최대 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-132">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="290a9-133">hello **쿼리** 개체에 포함 되어는 **HasMoreResults** tooinvoke hello를 사용할 수 있는 부울 속성 **GetNextAsTwinAsync** 메서드에 여러 번 tooretrieve 모든 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-133">hello **query** object contains a **HasMoreResults** boolean property that you can use tooinvoke hello **GetNextAsTwinAsync** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="290a9-134">**GetNextAsJson**이라는 메서드는 장치 쌍이 아닌 결과(예: 집계 쿼리의 결과)에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="290a9-135">마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:</span><span class="sxs-lookup"><span data-stu-id="290a9-135">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="290a9-136">Hello 솔루션 탐색기를 열고 hello **설정 시작 프로젝트...**  hello 있는지를 확인 하 고 **동작** 에 대 한 **AddTagsAndQuery** 프로젝트는 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-136">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="290a9-137">Hello 솔루션을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="290a9-137">Build hello solution.</span></span>
1. <span data-ttu-id="290a9-138">Hello를 마우스 오른쪽 단추로 클릭 하 여이 응용 프로그램을 실행 **AddTagsAndQuery** 프로젝트를 선택 하 고 **디버그**옵니다 **새 인스턴스 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-138">Run this application by right-clicking on hello **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="290a9-139">Hello 쿼리 요청에 있는 모든 장치에 대 한 하나의 장치 hello 결과에 표시 되어야 **Redmond43** toodevices 셀룰러 네트워크를 사용 하는 결과 none hello를 제한 하는 hello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-139">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![창에서 쿼리 결과][img-addtagapp]

<span data-ttu-id="290a9-141">Hello 다음 섹션에서 hello 연결 정보를 보고 하는 장치 앱을 만들고 변경 hello hello 이전 단원의 hello 쿼리의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-141">In hello next section, you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="290a9-142">Hello 장치 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="290a9-142">Create hello device app</span></span>
<span data-ttu-id="290a9-143">Tooyour 허브를 연결 하는 Node.js 콘솔 앱을 만들면이 섹션에서는 **myDeviceId**, 한 다음 셀룰러 네트워크를 사용 하 여 연결 되어 있음을 보고 속성 toocontain hello 정보를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-143">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, and then updates its reported properties toocontain hello information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="290a9-144">**reportconnectivity**라는 빈 폴더를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-144">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="290a9-145">Hello에 **reportconnectivity** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 새로운 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-145">In hello **reportconnectivity** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="290a9-146">모든 hello 기본값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-146">Accept all hello defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="290a9-147">Hello에 명령 프롬프트에 **reportconnectivity** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iot 장치**, 및 **azure iot-장치 mqtt** 패키지 :</span><span class="sxs-lookup"><span data-stu-id="290a9-147">At your command prompt in hello **reportconnectivity** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="290a9-148">텍스트 편집기를 사용 하 여 만드는 새 **ReportConnectivity.js** hello에 대 한 파일 **reportconnectivity** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-148">Using a text editor, create a new **ReportConnectivity.js** file in hello **reportconnectivity** folder.</span></span>
1. <span data-ttu-id="290a9-149">다음 코드 toohello hello 추가 **ReportConnectivity.js** 파일을 찾아 hello를 만들 때 복사한 하나 hello로 장치 연결 문자열에 대 한 hello 자리 표시자를 대체할 **myDeviceId** 장치 식별:</span><span class="sxs-lookup"><span data-stu-id="290a9-149">Add hello following code toohello **ReportConnectivity.js** file, and substitute hello placeholder for device connection string with hello one you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="290a9-150">hello **클라이언트** 개체가 toointeract hello 장치에서 장치 트윈스과 필요한 모든 hello 메서드를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-150">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="290a9-151">hello를 초기화 한 후 이전 코드 hello **클라이언트** 개체를 검색에 대 한 장치로 이중 hello **myDeviceId** 를 hello 연결 정보와 함께 보고 된 해당 속성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-151">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId** and updates its reported property with hello connectivity information.</span></span>
1. <span data-ttu-id="290a9-152">Hello 장치 앱 실행</span><span class="sxs-lookup"><span data-stu-id="290a9-152">Run hello device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="290a9-153">Hello 메시지를 확인 해야 `twin state reported`합니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-153">You should see hello message `twin state reported`.</span></span>
1. <span data-ttu-id="290a9-154">이제는 hello 장치 보고 자신의 연결 정보를 두 쿼리 모두에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-154">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="290a9-155">Hello.NET 실행 **AddTagsAndQuery** 앱 toorun hello를 다시 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-155">Run hello .NET **AddTagsAndQuery** app toorun hello queries again.</span></span> <span data-ttu-id="290a9-156">이번에는 **myDeviceId**가 두 쿼리 결과에 모두 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-156">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][img-addtagapp2]

## <a name="next-steps"></a><span data-ttu-id="290a9-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="290a9-157">Next steps</span></span>
<span data-ttu-id="290a9-158">이 자습서에서는 hello Azure 포털에서에서 새 IoT 허브를 구성 하 고 id 레지스트리에 hello IoT hub에서 장치 id를 만든 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-158">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="290a9-159">백 엔드 앱에서 태그로 장치 메타 데이터를 추가 하 고 hello 장치로 이중의 시뮬레이션 된 장치 앱 tooreport 장치 연결 정보를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-159">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="290a9-160">방법에 대해 배웠습니다 tooquery hello IoT Hub SQL 방식 쿼리 언어를 사용 하 여이 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-160">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="290a9-161">사용 하 여 hello 리소스 toolearn을 어떻게 수행 하려면:</span><span class="sxs-lookup"><span data-stu-id="290a9-161">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="290a9-162">hello 사용 하 여 장치에서 원격 분석 전송 [IoT 허브 시작] [ lnk-iothub-getstarted] 자습서</span><span class="sxs-lookup"><span data-stu-id="290a9-162">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="290a9-163">hello로 장치로 이중 원하는 속성을 사용 하 여 장치 구성 [속성 tooconfigure 장치 원하는 사용할] [ lnk-twin-how-to-configure] 자습서</span><span class="sxs-lookup"><span data-stu-id="290a9-163">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="290a9-164">hello로 장치를 대화형으로 (예: 사용자 제어 응용 프로그램에서 팬 설정)를 제어할 [직접 메서드를 사용 하 여] [ lnk-methods-tutorial] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="290a9-164">control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-node-twin-getstarted/addtagapp.png
[img-addtagapp2]: media/iot-hub-csharp-node-twin-getstarted/addtagapp2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md


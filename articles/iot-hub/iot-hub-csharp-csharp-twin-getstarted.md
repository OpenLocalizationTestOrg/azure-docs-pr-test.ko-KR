---
title: "Azure IoT Hub 장치 쌍 시작(.NET/.NET) | Microsoft Docs"
description: "Azure IoT Hub 장치 쌍을 사용하여 태그를 추가한 다음 IoT Hub 쿼리를 사용하는 방법입니다. .NET용 Azure IoT 장치 SDK를 사용하여 시뮬레이트된 장치 앱을 구현하고 .NET용 Azure IoT 서비스 SDK를 사용하여 태그를 추가하고 IoT Hub 쿼리를 실행하는 서비스 앱을 구현합니다."
services: iot-hub
documentationcenter: node
author: dsk-2015
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: dkshir
ms.openlocfilehash: 6073d594117e69676b753a1e3af25fffa3583a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-device-twins-netnet"></a><span data-ttu-id="0d2cb-104">장치 쌍(.NET/.NET) 시작</span><span class="sxs-lookup"><span data-stu-id="0d2cb-104">Get started with device twins (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="0d2cb-105">이 자습서의 끝 부분에 다음 .NET 콘솔 앱이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-105">At the end of this tutorial, you will have these .NET console apps:</span></span>

* <span data-ttu-id="0d2cb-106">**CreateDeviceIdentity**, 장치 ID 및 관련된 보안 키를 만들어 시뮬레이트된 장치 앱에 연결하는 .NET 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-106">**CreateDeviceIdentity**, a .NET app which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="0d2cb-107">**AddTagsAndQuery**, 태그를 추가하고 장치 쌍을 쿼리하는 .NET 백 엔드 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-107">**AddTagsAndQuery**, a .NET back-end app which adds tags and queries device twins.</span></span>
* <span data-ttu-id="0d2cb-108">**ReportConnectivity**, 앞에서 만든 장치 ID와 IoT Hub를 연결하고 연결 상태를 보고하는 장치를 시뮬레이트하는 .NET 장치 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-108">**ReportConnectivity**, a .NET device app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="0d2cb-109">[Azure IoT SDK][lnk-hub-sdks] 문서는 장치 및 백 엔드 앱을 빌드하는 데 사용할 수 있는 Azure IoT SDK에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="0d2cb-110">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-110">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="0d2cb-111">Visual Studio 2015 또는 Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-111">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="0d2cb-112">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-112">An active Azure account.</span></span> <span data-ttu-id="0d2cb-113">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="0d2cb-114">프로그래밍 방식으로 장치 ID를 만들려면 [.NET을 사용하여 IoT Hub에 시뮬레이트된 장치 연결][lnk-device-identity-csharp] 문서의 해당 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-114">If you want to create the device identity programmatically instead, read the corresponding section in the [Connect your simulated device to your IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="0d2cb-115">서비스 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="0d2cb-115">Create the service app</span></span>
<span data-ttu-id="0d2cb-116">이 섹션에서는 **myDeviceId**와 연결된 장치 쌍에 위치 메타데이터를 추가하는 .NET 콘솔 앱(C# 사용)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-116">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="0d2cb-117">그런 다음 IoT Hub에 저장된 장치 쌍을 쿼리하여 미국에 있는 장치를 선택한 다음 셀룰러 연결을 보고하는 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-117">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="0d2cb-118">Visual Studio에서 **콘솔 응용 프로그램** 프로젝트 템플릿을 사용하여 Visual C# Windows 클래식 데스크톱 프로젝트를 최신 솔루션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-118">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="0d2cb-119">프로젝트의 이름을 **AddTagsAndQuery**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-119">Name the project **AddTagsAndQuery**.</span></span>
   
    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][img-createapp]
1. <span data-ttu-id="0d2cb-121">솔루션 탐색기에서 **AddTagsAndQuery** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 관리...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-121">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="0d2cb-122">**NuGet 패키지 관리자** 창에서 **찾아보기**를 선택하고 **microsoft.azure.devices**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-122">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="0d2cb-123">**설치**를 설치하여 **Microsoft.Azure.Devices** 패키지를 설치한 후 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-123">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="0d2cb-124">이 프로시저에서는 [Azure IoT 서비스 SDK][lnk-nuget-service-sdk] NuGet 패키지 및 종속 항목에 참조를 다운로드, 설치 및 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-124">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 패키지 관리자 창][img-servicenuget]
1. <span data-ttu-id="0d2cb-126">**Program.cs** 파일 위에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-126">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="0d2cb-127">**Program** 클래스에 다음 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-127">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="0d2cb-128">자리 표시자 값을 이전 섹션에서 만든 허브의 IoT Hub 연결 문자열로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-128">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="0d2cb-129">**Program** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-129">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="0d2cb-130">**RegistryManager** 클래스는 서비스의 장치 쌍을 조작하는 데 필요한 모든 메서드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-130">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="0d2cb-131">이전 코드에서는 **registryManager** 개체를 초기화한 다음 **myDeviceId**에 대한 장치 쌍을 검색하고, 마지막으로 원하는 위치 정보로 tags를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-131">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="0d2cb-132">업데이트한 후 두 개의 쿼리를 실행합니다. 첫 번째는 **Redmond43** 공장에 위치한 장치의 장치 쌍만을 선택하고, 두 번째는 또한 셀룰러 네트워크를 통해서 연결된 장치만을 선택하기 위해 쿼리를 구체화합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-132">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="0d2cb-133">이전 코드는 **쿼리** 개체를 만들 때 반환되는 최대 문서 수를 지정한다는 점에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-133">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="0d2cb-134">**query** 개체에는 모든 결과를 검색하기 위해 여러 번 **GetNextAsTwinAsync** 메서드를 호출하는 데 사용할 수 있는 **HasMoreResults** 부울 속성이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-134">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="0d2cb-135">**GetNextAsJson**이라는 메서드는 장치 쌍이 아닌 결과(예: 집계 쿼리의 결과)에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-135">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="0d2cb-136">마지막으로 **Main** 메서드에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-136">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="0d2cb-137">솔루션 탐색기에서 **시작 프로젝트 설정...**을 열고 **AddTagsAndQuery** 프로젝트의 **작업**이 **시작**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-137">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="0d2cb-138">솔루션을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-138">Build the solution.</span></span>
1. <span data-ttu-id="0d2cb-139">**AddTagsAndQuery** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **디버그**를 선택한 후 **새 인스턴스 시작**을 선택하여 이 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-139">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="0d2cb-140">**Redmond43**에 위치한 모든 장치를 요청하는 쿼리에 대한 결과로는 하나의 장치를 보고 셀룰러 네트워크를 사용하는 장치에 대해서는 결과를 제한하는 쿼리에 대한 결과로는 아무 장치도 볼 수 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-140">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![창에서 쿼리 결과][img-addtagapp]

<span data-ttu-id="0d2cb-142">다음 섹션에서는 연결 정보를 보고하고 이전 섹션의 쿼리 결과를 변경하는 장치 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-142">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="0d2cb-143">장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="0d2cb-143">Create the device app</span></span>
<span data-ttu-id="0d2cb-144">이 섹션에서는 **myDeviceId**로 허브에 연결하는 .NET 콘솔 앱을 만든 다음 셀룰러 네트워크를 사용하여 연결되는 정보에 포함된 reported 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-144">In this section, you create a .NET console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="0d2cb-145">Visual Studio에서 **콘솔 응용 프로그램** 프로젝트 템플릿을 사용하여 Visual C# Windows 클래식 데스크톱 프로젝트를 최신 솔루션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-145">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="0d2cb-146">프로젝트 이름을 **ReportConnectivity**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-146">Name the project **ReportConnectivity**.</span></span>
   
    ![새 Visual C# Windows 클래식 장치 앱][img-createdeviceapp]
    
1. <span data-ttu-id="0d2cb-148">[솔루션 탐색기]에서 **ReportConnectivity** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음, **NuGet 패키지 관리...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-148">In Solution Explorer, right-click the **ReportConnectivity** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="0d2cb-149">**NuGet 패키지 관리자** 창에서 **찾아보기**를 선택하고 **microsoft.azure.devices.client**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-149">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="0d2cb-150">**설치**를 선택하여 **Microsoft.Azure.Devices.Client** 패키지를 설치한 후 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-150">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="0d2cb-151">이 절차에서는 [Azure IoT 장치 SDK][lnk-nuget-client-sdk] NuGet 패키지 및 해당 종속 항목에 참조를 다운로드, 설치 및 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-151">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 패키지 관리자 창 클라이언트 앱][img-clientnuget]
1. <span data-ttu-id="0d2cb-153">**Program.cs** 파일 위에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-153">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="0d2cb-154">**Program** 클래스에 다음 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="0d2cb-155">자리 표시자 값을 이전 섹션에서 메모한 장치 연결 문자열로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-155">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="0d2cb-156">**Program** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-156">Add the following method to the **Program** class:</span></span>

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting to hub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
                Console.WriteLine("Retrieving twin");
                await Client.GetTwinAsync();
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    <span data-ttu-id="0d2cb-157">**Client** 개체는 서비스의 장치 쌍을 조작하는 데 필요한 모든 메서드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-157">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="0d2cb-158">위에 표시된 코드는 **Client** 개체를 초기화한 다음 **myDeviceId**에 대한 장치 쌍을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-158">The code shown above, initializes the **Client** object, and then retrieves the device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="0d2cb-159">**Program** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-159">Add the following method to the **Program** class:</span></span>
   
        public static async void ReportConnectivity()
        {
            try
            {
                Console.WriteLine("Sending connectivity data as reported property");
                
                TwinCollection reportedProperties, connectivity;
                reportedProperties = new TwinCollection();
                connectivity = new TwinCollection();
                connectivity["type"] = "cellular";
                reportedProperties["connectivity"] = connectivity;
                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

   <span data-ttu-id="0d2cb-160">위의 코드는 **myDeviceId**의 보고된 속성을 연결 정보로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-160">The code above updates **myDeviceId**'s reported property with the connectivity information.</span></span>

1. <span data-ttu-id="0d2cb-161">마지막으로 **Main** 메서드에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-161">Finally, add the following lines to the **Main** method:</span></span>
   
       try
       {
            InitClient();
            ReportConnectivity();
       }
       catch (Exception ex)
       {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
       }
       Console.WriteLine("Press Enter to exit.");
       Console.ReadLine();

1. <span data-ttu-id="0d2cb-162">[솔루션 탐색기]에서 **시작 프로젝트 설정...**을 열고 **ReportConnectivity** 프로젝트의 **작업**이 **시작**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-162">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **ReportConnectivity** project is **Start**.</span></span> <span data-ttu-id="0d2cb-163">솔루션을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-163">Build the solution.</span></span>
1. <span data-ttu-id="0d2cb-164">**ReportConnectivity** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **디버그**를 선택한 후 **새 인스턴스 시작**을 선택하여 이 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-164">Run this application by right-clicking on the **ReportConnectivity** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="0d2cb-165">쌍 정보를 가져온 다음 연결을 *보고된 속성*으로 보내는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-165">You should see it getting the twin information, and then sending connectivity as a *reported property*.</span></span>
   
    ![장치 앱을 실행하여 연결 보고][img-rundeviceapp]
    
    
1. <span data-ttu-id="0d2cb-167">장치가 연결 정보를 보고했으므로 두 쿼리 모두에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-167">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="0d2cb-168">.NET **AddTagsAndQuery** 앱을 실행하여 쿼리를 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-168">Run the .NET **AddTagsAndQuery** app to run the queries again.</span></span> <span data-ttu-id="0d2cb-169">이번에는 **myDeviceId**가 두 쿼리 결과에 모두 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-169">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![장치 연결이 성공적으로 보고됨][img-tagappsuccess]

## <a name="next-steps"></a><span data-ttu-id="0d2cb-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0d2cb-171">Next steps</span></span>
<span data-ttu-id="0d2cb-172">이 자습서에서는 Azure Portal에서 새 IoT Hub를 구성한 다음, IoT Hub의 ID 레지스트리에서 장치 ID를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-172">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="0d2cb-173">백 엔드 앱에서 tags로 장치 메타데이터를 추가하고, 장치 쌍에서 장치 연결 정보를 보고하는 시뮬레이션된 장치 앱을 작성했습니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-173">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="0d2cb-174">또한 SQL과 유사한 IoT Hub 쿼리 언어를 사용하여 이 정보를 쿼리하는 방법도 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-174">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="0d2cb-175">아래와 같이 실행할 방법을 알아보려면 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-175">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="0d2cb-176">[IoT Hub 시작][lnk-iothub-getstarted] 자습서를 참조하여 장치에서 원격 분석을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-176">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="0d2cb-177">[desired 속성을 사용하여 장치 구성][lnk-twin-how-to-configure] 자습서를 참조하여 장치 쌍의 desired 속성을 사용하여 장치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-177">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="0d2cb-178">[직접 메서드 사용][lnk-methods-tutorial] 자습서를 참조하여 대화형으로(예: 사용자 제어 앱에서 팬 작동) 장치를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="0d2cb-178">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-csharp-twin-getstarted/addtagapp.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-getstarted/clientsdknuget.png
[img-rundeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/rundeviceapp.png
[img-tagappsuccess]: media/iot-hub-csharp-csharp-twin-getstarted/tagappsuccess.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp
[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md


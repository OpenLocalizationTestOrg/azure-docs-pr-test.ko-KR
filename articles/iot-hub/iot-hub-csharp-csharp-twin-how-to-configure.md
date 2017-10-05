---
title: "Azure IoT Hub 장치 쌍 속성 사용(.NET/.NET) | Microsoft Docs"
description: "Azure IoT Hub 장치 쌍을 사용하여 장치를 구성하는 방법입니다. .NET용 Azure IoT 장치 SDK를 사용하여 시뮬레이션된 장치 앱을 구현하고 .NET용 Azure IoT 서비스 SDK를 사용하여 장치 쌍을 통해 장치 구성을 수정하는 서비스 앱을 구현합니다."
services: iot-hub
documentationcenter: .net
author: dsk-2015
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: dkshir
ms.openlocfilehash: 679cda28bf3ce9fb207fe3693a3453b355f1de15
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="use-desired-properties-to-configure-devices"></a><span data-ttu-id="c5a44-104">desired 속성을 사용하여 장치 구성</span><span class="sxs-lookup"><span data-stu-id="c5a44-104">Use desired properties to configure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="c5a44-105">이 자습서의 끝 부분에 다음 두 개의 .NET 콘솔 앱이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-105">At the end of this tutorial, you will have two .NET console apps:</span></span>

* <span data-ttu-id="c5a44-106">**SimulateDeviceConfiguration** - 원하는 구성 업데이트를 기다리고 시뮬레이션된 구성 업데이트 프로세스의 상태를 보고하는 시뮬레이션된 장치 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-106">**SimulateDeviceConfiguration**, a simulated device app that waits for a desired configuration update and reports the status of a simulated configuration update process.</span></span>
* <span data-ttu-id="c5a44-107">**SetDesiredConfigurationAndQuery** - 장치에 원하는 구성을 설정하고 구성 업데이트 프로세스를 쿼리하는 백 엔드 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-107">**SetDesiredConfigurationAndQuery**, a back-end app, which sets the desired configuration on a device and queries the configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="c5a44-108">[Azure IoT SDK][lnk-hub-sdks] 문서는 장치 및 백 엔드 앱을 빌드하는 데 사용할 수 있는 Azure IoT SDK에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="c5a44-109">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="c5a44-110">Visual Studio 2015 또는 Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c5a44-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="c5a44-111">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="c5a44-111">An active Azure account.</span></span> <span data-ttu-id="c5a44-112">계정이 없는 경우 몇 분 내에 [계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="c5a44-113">[장치 쌍 시작][lnk-twin-tutorial] 자습서를 수행했으면 이미 IoT Hub 및 **myDeviceId**라는 장치 ID가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-113">If you followed the [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="c5a44-114">이 경우 [시뮬레이션된 장치 앱 만들기][lnk-how-to-configure-createapp] 섹션으로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-114">In that case, you can skip to the [Create the simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-the-simulated-device-app"></a><span data-ttu-id="c5a44-115">시뮬레이션된 장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="c5a44-115">Create the simulated device app</span></span>
<span data-ttu-id="c5a44-116">이 섹션에서는 **myDeviceId**로 허브에 연결하는 .NET 콘솔 앱을 만들고, 원하는 구성 업데이트를 기다린 다음, 시뮬레이션된 구성 업데이트 프로세스의 업데이트를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-116">In this section, you create a .NET console app that connects to your hub as **myDeviceId**, waits for a desired configuration update and then reports updates on the simulated configuration update process.</span></span>

1. <span data-ttu-id="c5a44-117">Visual Studio에서 **콘솔 응용 프로그램** 프로젝트 템플릿을 사용하여 새 Visual C# Windows 클래식 바탕 화면 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-117">In Visual Studio, create a new Visual C# Windows Classic Desktop project by using the **Console Application** project template.</span></span> <span data-ttu-id="c5a44-118">**SimulateDeviceConfiguration**으로 프로젝트 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-118">Name the project **SimulateDeviceConfiguration**.</span></span>
   
    ![새 Visual C# Windows 클래식 장치 앱][img-createdeviceapp]

1. <span data-ttu-id="c5a44-120">솔루션 탐색기에서 **SimulateDeviceConfiguration** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음, **NuGet 패키지 관리...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-120">In Solution Explorer, right-click the **SimulateDeviceConfiguration** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="c5a44-121">**NuGet 패키지 관리자** 창에서 **찾아보기**를 선택하고 **microsoft.azure.devices.client**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-121">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="c5a44-122">**설치**를 선택하여 **Microsoft.Azure.Devices.Client** 패키지를 설치한 후 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-122">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="c5a44-123">이 절차에서는 [Azure IoT 장치 SDK][lnk-nuget-client-sdk] NuGet 패키지 및 해당 종속 항목에 참조를 다운로드, 설치 및 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-123">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 패키지 관리자 창 클라이언트 앱][img-clientnuget]
1. <span data-ttu-id="c5a44-125">**Program.cs** 파일 위에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-125">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="c5a44-126">**Program** 클래스에 다음 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-126">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="c5a44-127">자리 표시자 값을 이전 섹션에서 메모한 장치 연결 문자열로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-127">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. <span data-ttu-id="c5a44-128">**Program** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-128">Add the following method to the **Program** class:</span></span>
 
        public static void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting to hub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }
    <span data-ttu-id="c5a44-129">**Client** 개체는 서비스의 장치 쌍을 조작하는 데 필요한 모든 메서드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-129">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="c5a44-130">위에 표시된 코드는 **Client** 개체를 초기화한 다음 **myDeviceId**에 대한 장치 쌍을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-130">The code shown above, initializes the **Client** object, and then retrieves the device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="c5a44-131">**Program** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-131">Add the following method to the **Program** class.</span></span> <span data-ttu-id="c5a44-132">이 메서드는 로컬 장치에서 원격 분석의 초기 값을 설정하고 장치 쌍을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-132">This method sets the initial values of telemetry on the local device and then updates the device twin.</span></span>

        public static async void InitTelemetry()
        {
            try
            {
                Console.WriteLine("Report initial telemetry config:");
                TwinCollection telemetryConfig = new TwinCollection();
                
                telemetryConfig["configId"] = "0";
                telemetryConfig["sendFrequency"] = "24h";
                reportedProperties["telemetryConfig"] = telemetryConfig;
                Console.WriteLine(JsonConvert.SerializeObject(reportedProperties));

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. <span data-ttu-id="c5a44-133">**Program** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-133">Add the following method to the **Program** class.</span></span> <span data-ttu-id="c5a44-134">장치 쌍에서 *원하는 속성*의 변경 내용을 검색하는 콜백입니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-134">This is a callback which will detect a change in *desired properties* in the device twin.</span></span>

        private static async Task OnDesiredPropertyChanged(TwinCollection desiredProperties, object userContext)
        {
            try
            {
                Console.WriteLine("Desired property change:");
                Console.WriteLine(JsonConvert.SerializeObject(desiredProperties));

                var currentTelemetryConfig = reportedProperties["telemetryConfig"];
                var desiredTelemetryConfig = desiredProperties["telemetryConfig"];

                if ((desiredTelemetryConfig != null) && (desiredTelemetryConfig["configId"] != currentTelemetryConfig["configId"]))
                {
                    Console.WriteLine("\nInitiating config change");
                    currentTelemetryConfig["status"] = "Pending";
                    currentTelemetryConfig["pendingConfig"] = desiredTelemetryConfig;

                    await Client.UpdateReportedPropertiesAsync(reportedProperties);

                    CompleteConfigChange();
                }
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    <span data-ttu-id="c5a44-135">이 메서드는 구성 업데이트 요청으로 로컬 장치 쌍 개체에서 reported 속성을 업데이트하고 상태를 **Pending**으로 설정한 다음 서비스에서 장치 쌍을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-135">This method updates the reported properties on the local device twin object with the configuration update request and sets the status to **Pending**, then updates the device twin on the service.</span></span> <span data-ttu-id="c5a44-136">장치 쌍을 업데이트한 후 아래 설명된 `CompleteConfigChange` 메서드를 호출하여 구성 변경을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-136">After successfully updating the device twin, it completes the config change by calling the method `CompleteConfigChange` described in the next point.</span></span>

1. <span data-ttu-id="c5a44-137">**Program** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-137">Add the following method to the **Program** class.</span></span> <span data-ttu-id="c5a44-138">이 메서드는 장치 재설정을 시뮬레이션하고, 로컬 reported 속성을 업데이트하여 상태를 **Success**로 설정하고, **pendingConfig** 요소를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-138">This method simulates a device reset, then updates the local reported properties setting the status to **Success** and removes the **pendingConfig** element.</span></span> <span data-ttu-id="c5a44-139">그런 다음 서비스에서 장치 쌍을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-139">It then updates the device twin on the service.</span></span> 

        public static async void CompleteConfigChange()
        {
            try
            {
                var currentTelemetryConfig = reportedProperties["telemetryConfig"];

                Console.WriteLine("\nSimulating device reset");
                await Task.Delay(30000); 

                Console.WriteLine("\nCompleting config change");
                currentTelemetryConfig["configId"] = currentTelemetryConfig["pendingConfig"]["configId"];
                currentTelemetryConfig["sendFrequency"] = currentTelemetryConfig["pendingConfig"]["sendFrequency"];
                currentTelemetryConfig["status"] = "Success";
                currentTelemetryConfig["pendingConfig"] = null;

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
                Console.WriteLine("Config change complete \nPress any key to exit.");
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. <span data-ttu-id="c5a44-140">마지막으로 **Main** 메서드에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-140">Finally add the following lines to the **Main** method:</span></span>

        try
        {
            InitClient();
            InitTelemetry();

            Console.WriteLine("Wait for desired telemetry...");
            Client.SetDesiredPropertyUpdateCallback(OnDesiredPropertyChanged, null).Wait();
            Console.ReadKey();
        }
        catch (AggregateException ex)
        {
            foreach (Exception exception in ex.InnerExceptions)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", exception);
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }

   > [!NOTE]
   > <span data-ttu-id="c5a44-141">이 자습서는 동시 구성 업데이트에 대해 어떤 동작도 시뮬레이션하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-141">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="c5a44-142">어떤 구성 업데이트 프로세스는 업데이트가 실행되는 중에 대상 구성의 변경을 수용할 수 있는 반면에 어떤 프로세스는 대기해야 하거나 오류 조건을 사용해 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-142">Some configuration update processes might be able to accommodate changes of target configuration while the update is running, some might have to queue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="c5a44-143">특정 구성 프로세스에 대해 원하는 동작을 고려하여 구성 변경을 시작하기 전에 적절한 논리를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-143">Make sure to consider the desired behavior for your specific configuration process, and add the appropriate logic before initiating the configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="c5a44-144">솔루션을 빌드하고 **F5**를 클릭하여 Visual Studio에서 장치 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-144">Build the solution and then run the device app from Visual Studio by clicking **F5**.</span></span> <span data-ttu-id="c5a44-145">시뮬레이션된 장치가 장치 쌍을 검색하고, 원격 분석을 설정하고, 원하는 속성 변경을 기다리고 있음을 나타내는 메시지가 출력 콘솔에 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-145">On the output console, you should see the messages indicating that your simulated device is retrieving the device twin, setting up the telemetry, and waiting for desired property change.</span></span> <span data-ttu-id="c5a44-146">앱이 계속 실행되게 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-146">Keep the app running.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="c5a44-147">서비스 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c5a44-147">Create the service app</span></span>
<span data-ttu-id="c5a44-148">이 섹션에서는 새로운 원격 분석 구성 개체를 사용하여 **myDeviceId**와 연결된 장치 쌍에서 *desired 속성*을 업데이트하는 .NET 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-148">In this section, you will create a .NET console app that updates the *desired properties* on the device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="c5a44-149">그런 다음 IoT Hub에 저장된 장치 쌍을 쿼리하고 장치의 desired 구성과 reported 구성 사이의 차이점을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-149">It then queries the device twins stored in the IoT hub and shows the difference between the desired and reported configurations of the device.</span></span>

1. <span data-ttu-id="c5a44-150">Visual Studio에서 **콘솔 응용 프로그램** 프로젝트 템플릿을 사용하여 Visual C# Windows 클래식 데스크톱 프로젝트를 최신 솔루션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-150">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="c5a44-151">프로젝트 이름을 **SetDesiredConfigurationAndQuery**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-151">Name the project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][img-createapp]
1. <span data-ttu-id="c5a44-153">솔루션 탐색기에서 **SetDesiredConfigurationAndQuery** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음, **NuGet 패키지 관리...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-153">In Solution Explorer, right-click the **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="c5a44-154">**NuGet 패키지 관리자** 창에서 **찾아보기**를 선택하고 **microsoft.azure.devices**를 검색한 다음 **설치**를 선택하여 **Microsoft.Azure.Devices** 패키지를 설치하고 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-154">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="c5a44-155">이 프로시저에서는 [Azure IoT 서비스 SDK][lnk-nuget-service-sdk] NuGet 패키지 및 종속 항목에 참조를 다운로드, 설치 및 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-155">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 패키지 관리자 창][img-servicenuget]
1. <span data-ttu-id="c5a44-157">**Program.cs** 파일 위에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-157">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="c5a44-158">**Program** 클래스에 다음 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-158">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="c5a44-159">자리 표시자 값을 이전 섹션에서 만든 허브의 IoT Hub 연결 문자열로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-159">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="c5a44-160">**Program** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-160">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="c5a44-161">**레지스트리** 개체는 서비스의 장치 쌍을 조작하는 데 필요한 모든 메서드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-161">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="c5a44-162">이 코드에서는 **Registry** 개체를 초기화한 후 **myDeviceId**에 대한 장치 쌍을 검색하고, 새로운 원격 분석 구성 개체를 사용하여 desired 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-162">This code initializes the **Registry** object, retrieves the device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="c5a44-163">그런 다음 10초마다 IoT Hub에 저장된 장치 쌍을 쿼리하고, 원하는 보고된 원격 분석 구성을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-163">After that, it queries the device twins stored in the IoT hub every 10 seconds, and prints the desired and reported telemetry configurations.</span></span> <span data-ttu-id="c5a44-164">모든 장치에서 다양한 보고서를 생성하는 방법을 알아보려면 [IoT Hub 쿼리 언어][lnk-query]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5a44-164">Refer to the [IoT Hub query language][lnk-query] to learn how to generate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="c5a44-165">이 응용 프로그램은 설명 목적으로 10초 마다 IoT Hub를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-165">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="c5a44-166">변경을 감지하기 위해서가 아니라 여러 장치에서 사용자용 보고서를 생성하기 위해 쿼리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-166">Use queries to generate user-facing reports across many devices, and not to detect changes.</span></span> <span data-ttu-id="c5a44-167">솔루션에 장치 이벤트의 실시간 알림이 필요한 경우 [쌍 알림][lnk-twin-notifications]을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-167">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="c5a44-168">마지막으로 **Main** 메서드에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-168">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key to quit.");
        Console.ReadLine();
1. <span data-ttu-id="c5a44-169">솔루션 탐색기에서 **시작 프로젝트 설정...**을 열고 **SetDesiredConfigurationAndQuery** 프로젝트의 **작업**이 **시작**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-169">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="c5a44-170">솔루션을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="c5a44-170">Build the solution.</span></span>
1. <span data-ttu-id="c5a44-171">**SimulateDeviceConfiguration** 장치 앱이 실행되고 있을 때 **F5**를 사용하여 Visual Studio에서 서비스 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-171">With **SimulateDeviceConfiguration** device app running, run the service app from Visual Studio using **F5**.</span></span> <span data-ttu-id="c5a44-172">**Pending**에서 **Success**로의 reported 구성 변경 내용과 24시간이 아닌 5분이라는 새로운 활성 보내기 빈도가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-172">You should see the reported configuration change from **Pending** to **Success** with the new active send frequency of five minutes instead of 24 hours.</span></span>

 ![장치가 성공적으로 구성됨][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="c5a44-174">장치 보고서 작업 및 쿼리 결과 사이에 최대 1분간 지연됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-174">There is a delay of up to a minute between the device report operation and the query result.</span></span> <span data-ttu-id="c5a44-175">이는 쿼리 인프라를 매우 높은 규모에서 작업하도록 하기 위해서입니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-175">This is to enable the query infrastructure to work at very high scale.</span></span> <span data-ttu-id="c5a44-176">단일 장치 쌍의 일관된 보기를 검색하려면 **Registry** 클래스의 **getDeviceTwin** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-176">To retrieve consistent views of a single device twin use the **getDeviceTwin** method in the **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="c5a44-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c5a44-177">Next steps</span></span>
<span data-ttu-id="c5a44-178">이 자습서에서는 솔루션 백 엔드에서 원하는 구성을 *desired 속성*으로 설정하고, 해당 변경 사항을 감지하고 reported 속성을 통해 상태를 보고하는 다단계 업데이트 프로세스를 시뮬레이션하는 장치 앱을 작성했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-178">In this tutorial, you set a desired configuration as *desired properties* from the solution back end, and wrote a device app to detect that change and simulate a multi-step update process reporting its status through the reported properties.</span></span>

<span data-ttu-id="c5a44-179">아래와 같이 실행할 방법을 알아보려면 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5a44-179">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="c5a44-180">[IoT Hub 시작][lnk-iothub-getstarted] 자습서를 참조하여 장치에서 원격 분석을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-180">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="c5a44-181">[jobs 예약 및 브로드캐스트][lnk-schedule-jobs] 자습서를 참조하여 대규모 장비 집합에 대한 작업을 예약하거나 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-181">schedule or perform operations on large sets of devices see the [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="c5a44-182">[직접 메서드 사용][lnk-methods-tutorial] 자습서를 참조하여 대화형으로(예: 사용자 제어 앱에서 팬 작동) 장치를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a44-182">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/devicesdknuget.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png


<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-twin-tutorial]: iot-hub-csharp-csharp-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-how-to-configure-createapp]: iot-hub-csharp-csharp-twin-how-to-configure.md#create-the-simulated-device-app

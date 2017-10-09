---
title: "aaaUse Azure IoT Hub 장치로 이중 속성 (.NET/.NET) | Microsoft Docs"
description: "Azure IoT Hub 장치 toouse 트윈스 어떻게 tooconfigure 장치 .NET tooimplement 시뮬레이션 된 장치 응용 프로그램에 대 한 hello Azure IoT 장치 SDK 및.NET tooimplement 장치로 이중을 사용 하는 장치 구성을 수정 하는 서비스 응용 프로그램에 대 한 Azure IoT 서비스 SDK hello를 사용 합니다."
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
ms.openlocfilehash: 486436d29abfd5158c253adc5abf5935e0e1fdba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a><span data-ttu-id="8bd0b-104">원하는 속성 tooconfigure 장치를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="8bd0b-104">Use desired properties tooconfigure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="8bd0b-105">이 자습서의 hello 끝에 두 개의.NET 콘솔 응용 프로그램 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-105">At hello end of this tutorial, you will have two .NET console apps:</span></span>

* <span data-ttu-id="8bd0b-106">**SimulateDeviceConfiguration**, 원하는 구성 업데이트를 대기 하 고 시뮬레이트된 구성 업데이트 프로세스의 hello 상태를 보고 하는 시뮬레이션 된 장치 앱.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-106">**SimulateDeviceConfiguration**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="8bd0b-107">**SetDesiredConfigurationAndQuery**, hello를 설정 하는 백 엔드 앱, 원하는 장치에서 구성 및 쿼리 hello 업데이트 프로세스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-107">**SetDesiredConfigurationAndQuery**, a back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="8bd0b-108">hello 문서 [Azure IoT Sdk] [ lnk-hub-sdks] toobuild를 사용할 수 있는, Azure IoT Sdk hello에 대 한 정보를 제공 장치와 백 엔드 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="8bd0b-109">toocomplete hello 다음 해야이 자습서:</span><span class="sxs-lookup"><span data-stu-id="8bd0b-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="8bd0b-110">Visual Studio 2015 또는 Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="8bd0b-111">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-111">An active Azure account.</span></span> <span data-ttu-id="8bd0b-112">계정이 없는 경우 몇 분 내에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="8bd0b-113">Hello를 따른 경우 [장치 트윈스 시작] [ lnk-twin-tutorial] 자습서에서는 이미 있는 IoT hub 및 호출 하 여 장치 id **myDeviceId**합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-113">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="8bd0b-114">이 경우 toohello 건너뛸 수 있습니다 [만들기 hello 시뮬레이션 된 장치 앱] [ lnk-how-to-configure-createapp] 섹션.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-114">In that case, you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="8bd0b-115">Hello 시뮬레이션 된 장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="8bd0b-115">Create hello simulated device app</span></span>
<span data-ttu-id="8bd0b-116">Tooyour 허브를 연결 하는.NET 콘솔 응용 프로그램을 만들면이 섹션에서는 **myDeviceId**원하는 구성 업데이트 될 때까지 대기 하 고 시뮬레이션 hello 구성 업데이트 프로세스에서 업데이트를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-116">In this section, you create a .NET console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="8bd0b-117">Visual Studio에서 hello를 사용 하 여 새 Visual C# Windows 클래식 데스크톱 프로젝트를 만들 **콘솔 응용 프로그램** 서식 파일 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-117">In Visual Studio, create a new Visual C# Windows Classic Desktop project by using hello **Console Application** project template.</span></span> <span data-ttu-id="8bd0b-118">이름 hello 프로젝트 **SimulateDeviceConfiguration**합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-118">Name hello project **SimulateDeviceConfiguration**.</span></span>
   
    ![새 Visual C# Windows 클래식 장치 앱][img-createdeviceapp]

1. <span data-ttu-id="8bd0b-120">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **SimulateDeviceConfiguration** 프로젝트를 마우스 클릭 **NuGet 패키지 관리...** .</span><span class="sxs-lookup"><span data-stu-id="8bd0b-120">In Solution Explorer, right-click hello **SimulateDeviceConfiguration** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="8bd0b-121">Hello에 **NuGet 패키지 관리자** 창에서 **찾아보기** 검색 한 **microsoft.azure.devices.client**합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-121">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="8bd0b-122">선택 **설치** tooinstall hello **Microsoft.Azure.Devices.Client** 패키지 및 hello 사용 약관에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-122">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="8bd0b-123">이 절차를 다운로드, 설치 하 고 참조 toohello 추가 [Azure IoT 장치 SDK] [ lnk-nuget-client-sdk] NuGet 패키지 및 해당 종속성.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-123">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 패키지 관리자 창 클라이언트 앱][img-clientnuget]
1. <span data-ttu-id="8bd0b-125">Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:</span><span class="sxs-lookup"><span data-stu-id="8bd0b-125">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="8bd0b-126">다음 필드 toohello hello 추가 **프로그램** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-126">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="8bd0b-127">Hello 이전 섹션에서 기록한 hello 장치 연결 문자열 hello 자리 표시자 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-127">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. <span data-ttu-id="8bd0b-128">다음 메서드 toohello hello 추가 **프로그램** 클래스:</span><span class="sxs-lookup"><span data-stu-id="8bd0b-128">Add hello following method toohello **Program** class:</span></span>
 
        public static void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }
    <span data-ttu-id="8bd0b-129">hello **클라이언트** 개체가 toointeract hello 장치에서 장치 트윈스과 필요한 모든 hello 메서드를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-129">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="8bd0b-130">위에 표시 된 코드 hello 초기화 hello **클라이언트** 개체 및에 대 한 검색 hello 장치로 이중 **myDeviceId**합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-130">hello code shown above, initializes hello **Client** object, and then retrieves hello device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="8bd0b-131">다음 메서드 toohello hello 추가 **프로그램** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-131">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="8bd0b-132">이 메서드는 hello 로컬 장치에서 원격 분석의 hello 초기 값을 설정 하 고 업데이트 hello 장치로 이중.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-132">This method sets hello initial values of telemetry on hello local device and then updates hello device twin.</span></span>

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

1. <span data-ttu-id="8bd0b-133">다음 메서드 toohello hello 추가 **프로그램** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-133">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="8bd0b-134">이것은 변화를 확인할 하는 콜백을 *원하는 속성을* hello 장치로 이중에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-134">This is a callback which will detect a change in *desired properties* in hello device twin.</span></span>

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

    <span data-ttu-id="8bd0b-135">이 메서드가 업데이트 hello 너무 hello 구성 사용 하 여 hello 로컬 장치로 이중 개체의 속성 업데이트 요청 및 집합 hello 상태 보고**보류 중인**, 다음 업데이트 hello hello 서비스에 장치로 이중 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-135">This method updates hello reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="8bd0b-136">Hello 장치로 이중을 성공적으로 업데이트 한 후 hello 메서드를 호출 하 여 hello 구성 변경을 완료 `CompleteConfigChange` hello 다음 지점에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-136">After successfully updating hello device twin, it completes hello config change by calling hello method `CompleteConfigChange` described in hello next point.</span></span>

1. <span data-ttu-id="8bd0b-137">다음 메서드 toohello hello 추가 **프로그램** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-137">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="8bd0b-138">이 메서드는 장치 리셋을 시뮬레이션 한 다음 업데이트 hello 너무 hello 상태를 설정 하는 로컬 보고 속성**성공** 및 제거 hello **pendingConfig** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-138">This method simulates a device reset, then updates hello local reported properties setting hello status too**Success** and removes hello **pendingConfig** element.</span></span> <span data-ttu-id="8bd0b-139">그런 다음 hello 장치로 이중 hello 서비스에 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-139">It then updates hello device twin on hello service.</span></span> 

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
                Console.WriteLine("Config change complete \nPress any key tooexit.");
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

1. <span data-ttu-id="8bd0b-140">마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:</span><span class="sxs-lookup"><span data-stu-id="8bd0b-140">Finally add hello following lines toohello **Main** method:</span></span>

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
   > <span data-ttu-id="8bd0b-141">이 자습서는 동시 구성 업데이트에 대해 어떤 동작도 시뮬레이션하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-141">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="8bd0b-142">일부 구성 업데이트 프로세스 hello 업데이트 실행 되는 동안 대상 구성의 변경 내용 수 tooaccommodate 수 있습니다, 그리고 일부 tooqueue 고, 일부 수 거부 오류 조건과 함께 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-142">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, some might have tooqueue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="8bd0b-143">특정 구성 프로세스에 대해 원하는 동작을 hello 고 hello 구성 변경 시작 하기 전에 hello 적절 한 논리를 추가 했는지 tooconsider를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-143">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="8bd0b-144">Hello 솔루션을 구축 하 고 다음을 클릭 하 여 Visual Studio에서 hello 장치 응용 프로그램을 실행 **F5**합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-144">Build hello solution and then run hello device app from Visual Studio by clicking **F5**.</span></span> <span data-ttu-id="8bd0b-145">Hello 출력 콘솔에 hello를 시뮬레이션 된 장치는 hello 장치로 이중 검색, hello 원격 분석 설정 및 원하는 속성 변경을 기다리는 있는지를 나타내는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-145">On hello output console, you should see hello messages indicating that your simulated device is retrieving hello device twin, setting up hello telemetry, and waiting for desired property change.</span></span> <span data-ttu-id="8bd0b-146">실행 중인 hello 앱을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-146">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="8bd0b-147">Hello 서비스 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="8bd0b-147">Create hello service app</span></span>
<span data-ttu-id="8bd0b-148">이 섹션에서는 만듭니다.NET 콘솔 응용 프로그램 업데이트 hello 해당 *원하는 속성을* 와 연결 된 장치로 이중 hello에 **myDeviceId** 새 원격 분석 구성 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-148">In this section, you will create a .NET console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="8bd0b-149">다음 hello IoT 허브에 저장 된 hello 장치 트윈스 쿼리하고 hello 차이 hello 원하는 및 보고 hello 장치의 구성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-149">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="8bd0b-150">Visual Studio에서 Visual C# Windows 클래식 데스크톱 프로젝트 toohello 현재 솔루션 hello를 사용 하 여 추가 **콘솔 응용 프로그램** 서식 파일 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-150">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="8bd0b-151">이름 hello 프로젝트 **SetDesiredConfigurationAndQuery**합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-151">Name hello project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][img-createapp]
1. <span data-ttu-id="8bd0b-153">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **SetDesiredConfigurationAndQuery** 프로젝트를 마우스 클릭 **NuGet 패키지 관리...** .</span><span class="sxs-lookup"><span data-stu-id="8bd0b-153">In Solution Explorer, right-click hello **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="8bd0b-154">Hello에 **NuGet 패키지 관리자** 창에서 **찾아보기**, 검색할 **microsoft.azure.devices**선택, **설치** tooinstall hello **Microsoft.Azure.Devices** 패키지 및 hello 사용 약관에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-154">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="8bd0b-155">이 절차를 다운로드, 설치 하 고 참조 toohello 추가 [Azure IoT 서비스 SDK] [ lnk-nuget-service-sdk] NuGet 패키지 및 해당 종속성.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-155">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 패키지 관리자 창][img-servicenuget]
1. <span data-ttu-id="8bd0b-157">Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:</span><span class="sxs-lookup"><span data-stu-id="8bd0b-157">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="8bd0b-158">다음 필드 toohello hello 추가 **프로그램** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-158">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="8bd0b-159">Hello hello 이전 섹션에서 만든 hello 허브에 대 한 IoT 허브 연결 문자열 hello 자리 표시자 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-159">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="8bd0b-160">다음 메서드 toohello hello 추가 **프로그램** 클래스:</span><span class="sxs-lookup"><span data-stu-id="8bd0b-160">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="8bd0b-161">hello **레지스트리** 개체 hello 서비스에서 장치 트윈스와 모든 hello 메서드에 필요한 toointeract을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-161">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="8bd0b-162">이 코드를 hello 초기화 **레지스트리** 개체를 검색에 대 한 장치로 이중 hello **myDeviceId**, 한 후 새 원격 분석 구성 개체를으로 원하는 속성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-162">This code initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="8bd0b-163">그 후 hello 장치 트윈스 10 초 마다 hello IoT 허브에 저장 된 쿼리 및 인쇄 hello 원하는 및 원격 분석 구성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-163">After that, it queries hello device twins stored in hello IoT hub every 10 seconds, and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="8bd0b-164">Toohello 참조 [IoT Hub 쿼리 언어] [ lnk-query] toolearn toogenerate 서식 있는 모든 장치에서 보고 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-164">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="8bd0b-165">이 응용 프로그램은 설명 목적으로 10초 마다 IoT Hub를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-165">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="8bd0b-166">사용 하 여 많은 장치와 toodetect 변경 내용이 아니라 걸쳐 toogenerate 사용자 용 보고서를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-166">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="8bd0b-167">솔루션에 장치 이벤트의 실시간 알림이 필요한 경우 [쌍 알림][lnk-twin-notifications]을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-167">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="8bd0b-168">마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:</span><span class="sxs-lookup"><span data-stu-id="8bd0b-168">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. <span data-ttu-id="8bd0b-169">Hello 솔루션 탐색기를 열고 hello **설정 시작 프로젝트...**  hello 있는지를 확인 하 고 **동작** 에 대 한 **SetDesiredConfigurationAndQuery** 프로젝트는 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-169">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="8bd0b-170">Hello 솔루션을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-170">Build hello solution.</span></span>
1. <span data-ttu-id="8bd0b-171">와 **SimulateDeviceConfiguration** 응용 프로그램 실행 중인 장치, Visual Studio를 사용 하 여 서비스 응용 프로그램을 실행된 hello **F5**합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-171">With **SimulateDeviceConfiguration** device app running, run hello service app from Visual Studio using **F5**.</span></span> <span data-ttu-id="8bd0b-172">Hello 보고 된 구성에서 변경 표시 되어야 **보류 중인** 너무**성공** hello 새 활성 대신 24 시간 동안 5 분의 빈도 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-172">You should see hello reported configuration change from **Pending** too**Success** with hello new active send frequency of five minutes instead of 24 hours.</span></span>

 ![장치가 성공적으로 구성됨][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="8bd0b-174">hello 장치 보고서 작업 및 hello 쿼리 결과 사이 tooa 1 분 간의 지연이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-174">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="8bd0b-175">이 매우 높은 대규모 tooenable hello 쿼리 인프라 toowork입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-175">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="8bd0b-176">단일 장치로 이중의 일관 된 뷰 tooretrieve hello를 사용 하 여 **getDeviceTwin** hello에 대 한 메서드 **레지스트리** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-176">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="8bd0b-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8bd0b-177">Next steps</span></span>
<span data-ttu-id="8bd0b-178">이 자습서에서는으로 원하는 구성을 설정 하면 *원하는 속성을* hello 솔루션에서 백 엔드를 하 고 변경 하 고 보고 하는 hello 통해 해당 상태를 보고 multi-step 업데이트 프로세스를 시뮬레이션 하는 장치 앱 toodetect 작성 했습니다. 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-178">In this tutorial, you set a desired configuration as *desired properties* from hello solution back end, and wrote a device app toodetect that change and simulate a multi-step update process reporting its status through hello reported properties.</span></span>

<span data-ttu-id="8bd0b-179">사용 하 여 hello 리소스 toolearn을 어떻게 수행 하려면:</span><span class="sxs-lookup"><span data-stu-id="8bd0b-179">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="8bd0b-180">hello 사용 하 여 장치에서 원격 분석 전송 [IoT 허브 시작] [ lnk-iothub-getstarted] 자습서</span><span class="sxs-lookup"><span data-stu-id="8bd0b-180">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="8bd0b-181">예약 또는 수행 큰 집합의 장치에 대 한 작업 참조 hello [일정 및 브로드캐스트 작업] [ lnk-schedule-jobs] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-181">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="8bd0b-182">대화형으로 (예: 사용자 제어 응용 프로그램에서 팬)를 설정 하는 장치 hello로 제어 [직접 메서드를 사용 하 여] [ lnk-methods-tutorial] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd0b-182">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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

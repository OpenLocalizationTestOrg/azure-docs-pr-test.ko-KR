---
title: "Azure IoT Hub aaaUse 직접 메서드 (.NET/.NET) | Microsoft Docs"
description: "어떻게 toouse Azure IoT Hub는 메서드를 전달 합니다. Hello Azure IoT 장치 SDK를 사용 하 여.NET tooimplement 직접적인 방법 및 hello.NET tooimplement hello 직접 메서드를 호출 하는 서비스 응용 프로그램에 대 한 Azure IoT 서비스 SDK 포함 하는 시뮬레이션 된 장치 앱에 대 한 합니다."
services: iot-hub
documentationcenter: 
author: dsk-2015
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: dkshir
ms.openlocfilehash: d4fa093a99558ec6faf294c2583a14a722b9ac03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnet"></a><span data-ttu-id="b7ad8-104">직접 메서드 사용(.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="b7ad8-104">Use direct methods (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="b7ad8-105">이 자습서는 진행 중인 toodevelop 두 개의.NET 콘솔 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="b7ad8-105">In this tutorial, we are going toodevelop two .NET console apps:</span></span>

* <span data-ttu-id="b7ad8-106">**CallMethodOnDevice**, hello 시뮬레이션 된 장치 응용 프로그램의 메서드를 호출 하 고 hello 응답을 표시 하는 백 엔드 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-106">**CallMethodOnDevice**, a back-end app, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="b7ad8-107">**SimulateDeviceMethods**, 이전에 만든 hello 장치 id를 사용 하 여 tooyour IoT 허브를 연결 하는 장치를 시뮬레이션 및 hello 클라우드 호출한 toohello 메서드 이벤트에 응답 하 여 콘솔 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-107">**SimulateDeviceMethods**, a console app which simulates a device connecting tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="b7ad8-108">hello 문서 [Azure IoT Sdk] [ lnk-hub-sdks] 사용할 수 있는 toobuild 두 응용 프로그램 toorun 장치와 솔루션 백 엔드에, Azure IoT Sdk hello에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="b7ad8-109">toocomplete 해야이 자습서에서는:</span><span class="sxs-lookup"><span data-stu-id="b7ad8-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="b7ad8-110">Visual Studio 2015 또는 Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="b7ad8-111">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-111">An active Azure account.</span></span> <span data-ttu-id="b7ad8-112">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="b7ad8-113">원할 경우 toocreate hello 장치 id를 프로그래밍 방식으로 대신 hello의 hello 해당 섹션을 읽어 [.NET을 사용 하 여 시뮬레이션 된 장치 tooyour IoT 허브 연결] [ lnk-device-identity-csharp] 문서.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-113">If you want toocreate hello device identity programmatically instead, read hello corresponding section in hello [Connect your simulated device tooyour IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="b7ad8-114">시뮬레이션된 장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="b7ad8-114">Create a simulated device app</span></span>
<span data-ttu-id="b7ad8-115">이 섹션에서는 응답 tooa 메서드 끝 hello 솔루션 다시에서 호출 하 여.NET 콘솔 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-115">In this section, you create a .NET console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="b7ad8-116">Visual Studio에서 Visual C# Windows 클래식 데스크톱 프로젝트 toohello 현재 솔루션 hello를 사용 하 여 추가 **콘솔 응용 프로그램** 서식 파일 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-116">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="b7ad8-117">이름 hello 프로젝트 **SimulateDeviceMethods**합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-117">Name hello project **SimulateDeviceMethods**.</span></span>
   
    ![새 Visual C# Windows 클래식 장치 앱][img-createdeviceapp]
    
1. <span data-ttu-id="b7ad8-119">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **SimulateDeviceMethods** 프로젝트를 마우스 클릭 **NuGet 패키지 관리...** .</span><span class="sxs-lookup"><span data-stu-id="b7ad8-119">In Solution Explorer, right-click hello **SimulateDeviceMethods** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="b7ad8-120">Hello에 **NuGet 패키지 관리자** 창에서 **찾아보기** 검색 한 **microsoft.azure.devices.client**합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-120">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="b7ad8-121">선택 **설치** tooinstall hello **Microsoft.Azure.Devices.Client** 패키지 및 hello 사용 약관에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-121">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="b7ad8-122">이 절차를 다운로드, 설치 하 고 참조 toohello 추가 [Azure IoT 장치 SDK] [ lnk-nuget-client-sdk] NuGet 패키지 및 해당 종속성.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-122">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 패키지 관리자 창 클라이언트 앱][img-clientnuget]
1. <span data-ttu-id="b7ad8-124">Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:</span><span class="sxs-lookup"><span data-stu-id="b7ad8-124">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. <span data-ttu-id="b7ad8-125">다음 필드 toohello hello 추가 **프로그램** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-125">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="b7ad8-126">Hello 이전 섹션에서 기록한 hello 장치 연결 문자열 hello 자리 표시자 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-126">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="b7ad8-127">Hello tooimplement hello 직접적인 방법 hello 장치에서 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-127">Add hello following tooimplement hello direct method on hello device:</span></span>

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. <span data-ttu-id="b7ad8-128">마지막으로, 다음 코드 toohello hello 추가 **Main** 메서드 tooopen hello 연결 tooyour IoT 허브 및 초기화 hello 메서드 수신기:</span><span class="sxs-lookup"><span data-stu-id="b7ad8-128">Finally, add hello following code toohello **Main** method tooopen hello connection tooyour IoT hub and initialize hello method listener:</span></span>
   
        try
        {
            Console.WriteLine("Connecting toohub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter tooexit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove hello "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. <span data-ttu-id="b7ad8-129">에 hello Visual Studio 솔루션 탐색기, 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작 프로젝트 설정 중...** . 선택 **개의 시작 프로젝트**를 선택한 후 hello **SimulateDeviceMethods** hello 드롭다운 메뉴에서 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-129">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **SimulateDeviceMethods** project in hello dropdown menu.</span></span>        

> [!NOTE]
> <span data-ttu-id="b7ad8-130">단순 tookeep 항목을이 자습서는 어떠한 재시도 정책도 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-130">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b7ad8-131">프로덕션 코드에 다시 시도 정책 (예: 연결 다시 시도) hello MSDN 문서에 설명 된 대로 구현 해야 [일시적인 오류 처리][lnk-transient-faults]합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-131">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="b7ad8-132">장치에서 직접 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="b7ad8-132">Call a direct method on a device</span></span>
<span data-ttu-id="b7ad8-133">이 섹션에서는 다음 hello 응답을 표시 하 고 hello 시뮬레이션 된 장치 응용 프로그램에서 메서드를 호출 하는.NET 콘솔 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-133">In this section, you create a .NET console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="b7ad8-134">Visual Studio에서 Visual C# Windows 클래식 데스크톱 프로젝트 toohello 현재 솔루션 hello를 사용 하 여 추가 **콘솔 응용 프로그램** 서식 파일 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-134">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="b7ad8-135">Hello.NET Framework 버전 4.5.1 인지 확인 하거나 나중에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-135">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="b7ad8-136">이름 hello 프로젝트 **CallMethodOnDevice**합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-136">Name hello project **CallMethodOnDevice**.</span></span>
   
    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][img-createserviceapp]
2. <span data-ttu-id="b7ad8-138">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **CallMethodOnDevice** 프로젝트를 마우스 클릭 **NuGet 패키지 관리...** .</span><span class="sxs-lookup"><span data-stu-id="b7ad8-138">In Solution Explorer, right-click hello **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="b7ad8-139">Hello에 **NuGet 패키지 관리자** 창에서 **찾아보기**, 검색할 **microsoft.azure.devices**선택, **설치** tooinstall hello **Microsoft.Azure.Devices** 패키지 및 hello 사용 약관에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-139">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="b7ad8-140">이 절차를 다운로드, 설치 하 고 참조 toohello 추가 [Azure IoT 서비스 SDK] [ lnk-nuget-service-sdk] NuGet 패키지 및 해당 종속성.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-140">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 패키지 관리자 창][img-servicenuget]

4. <span data-ttu-id="b7ad8-142">Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:</span><span class="sxs-lookup"><span data-stu-id="b7ad8-142">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="b7ad8-143">다음 필드 toohello hello 추가 **프로그램** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-143">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="b7ad8-144">Hello hello 이전 섹션에서 만든 hello 허브에 대 한 IoT 허브 연결 문자열 hello 자리 표시자 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-144">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="b7ad8-145">다음 메서드 toohello hello 추가 **프로그램** 클래스:</span><span class="sxs-lookup"><span data-stu-id="b7ad8-145">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="b7ad8-146">이 메서드는 이름으로 직접 메서드 호출 `writeLine` hello에 `myDeviceId` 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-146">This method invokes a direct method with name `writeLine` on hello `myDeviceId` device.</span></span> <span data-ttu-id="b7ad8-147">그런 다음 hello 콘솔에 hello 장치에서 제공 하는 hello 응답을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-147">Then, it writes hello response provided by hello device on hello console.</span></span> <span data-ttu-id="b7ad8-148">가능한 toospecify 장치 toorespond hello에 대 한 제한 시간 값을 방법은 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-148">Note how it is possible toospecify a timeout value for hello device toorespond.</span></span>
7. <span data-ttu-id="b7ad8-149">마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:</span><span class="sxs-lookup"><span data-stu-id="b7ad8-149">Finally, add hello following lines toohello **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="b7ad8-150">에 hello Visual Studio 솔루션 탐색기, 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작 프로젝트 설정 중...** . 선택 **개의 시작 프로젝트**를 선택한 후 hello **CallMethodOnDevice** hello 드롭다운 메뉴에서 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-150">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **CallMethodOnDevice** project in hello dropdown menu.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="b7ad8-151">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="b7ad8-151">Run hello applications</span></span>
<span data-ttu-id="b7ad8-152">준비 toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-152">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="b7ad8-153">Hello.NET 장치 앱 실행 **SimulateDeviceMethods**합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-153">Run hello .NET device app **SimulateDeviceMethods**.</span></span> <span data-ttu-id="b7ad8-154">IoT Hub의 메서드 호출에 대한 수신이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-154">It should start listening for method calls from your IoT Hub:</span></span> 

    ![장치 앱 실행][img-deviceapprun]
1. <span data-ttu-id="b7ad8-156">이제 해당 hello 장치를 연결 하 고 hello.NET 실행 메서드 호출을 기다리는 **CallMethodOnDevice** hello 시뮬레이션 된 장치 앱의 앱 tooinvoke hello 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-156">Now that hello device is connected and waiting for method invocations, run hello .NET **CallMethodOnDevice** app tooinvoke hello method in hello simulated device app.</span></span> <span data-ttu-id="b7ad8-157">Hello 콘솔에 작성 된 hello 장치 응답을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-157">You should see hello device response written in hello console.</span></span>
   
    ![서비스 앱 실행][img-serviceapprun]
1. <span data-ttu-id="b7ad8-159">hello 장치는이 메시지를 인쇄 하 여 toohello 메서드 다음 반응 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-159">hello device then reacts toohello method by printing this message:</span></span>
   
    ![Hello 장치에서 호출 하는 직접 메서드][img-directmethodinvoked]

## <a name="next-steps"></a><span data-ttu-id="b7ad8-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b7ad8-161">Next steps</span></span>
<span data-ttu-id="b7ad8-162">이 자습서에서는 hello Azure 포털에서에서 새 IoT 허브를 구성 하 고 id 레지스트리에 hello IoT hub에서 장치 id를 만든 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-162">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="b7ad8-163">이 장치 identity tooenable hello 시뮬레이션 된 장치 앱 tooreact toomethods hello 클라우드 호출한 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-163">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="b7ad8-164">또한 hello 장치에 대 한 메서드를 호출 하 고 hello 장치에서 hello 응답을 표시 하는 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-164">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="b7ad8-165">시작 toocontinue IoT 허브와 tooexplore 다른 IoT 시나리오를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-165">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="b7ad8-166">[IoT Hub 시작]</span><span class="sxs-lookup"><span data-stu-id="b7ad8-166">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="b7ad8-167">[여러 장치에서 jobs 예약][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="b7ad8-167">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="b7ad8-168">toolearn tooextend IoT 솔루션 및 일정 메서드를 여러 장치에서 호출 하는 방법 참조 hello [일정 및 브로드캐스트 작업] [ lnk-tutorial-jobs] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="b7ad8-168">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[img-createdeviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-device-app.png
[img-clientnuget]: ./media/iot-hub-csharp-csharp-direct-methods/device-app-nuget.png
[img-createserviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-service-app.png
[img-servicenuget]: ./media/iot-hub-csharp-csharp-direct-methods/service-app-nuget.png
[img-deviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-device-app.png
[img-serviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-service-app.png
[img-directmethodinvoked]: ./media/iot-hub-csharp-csharp-direct-methods/direct-method-invoked.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[IoT Hub 시작]: iot-hub-node-node-getstarted.md

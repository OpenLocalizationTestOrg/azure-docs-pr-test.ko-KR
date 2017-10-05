---
title: "Azure IoT Hub 직접 메서드(.NET/.NET) 사용 | Microsoft Docs"
description: "Azure IoT Hub 직접 메서드를 사용하는 방법입니다. .NET용 Azure IoT 장치 SDK를 사용하여 직접 메서드를 포함한 시뮬레이트된 장치 앱을 구현하며 .NET용 Azure IoT service SDK를 사용하여 직접 메서드를 호출하는 서비스 앱을 구현합니다."
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
ms.openlocfilehash: 9ce1fbebb6417c10618aa182e3c1d9ddf8132fb6
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="use-direct-methods-netnet"></a><span data-ttu-id="c5295-104">직접 메서드 사용(.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="c5295-104">Use direct methods (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="c5295-105">이 자습서에서는 다음 2개의 .NET 콘솔 앱을 개발합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-105">In this tutorial, we are going to develop two .NET console apps:</span></span>

* <span data-ttu-id="c5295-106">**CallMethodOnDevice**: 시뮬레이트된 장치 앱에서 메서드를 호출하고 응답을 표시하는 백 엔드 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-106">**CallMethodOnDevice**, a back-end app, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="c5295-107">**SimulateDeviceMethods**: 앞에서 만든 장치 ID로 IoT Hub에 연결하고 클라우드에서 호출하는 메서드에 응답하는 장치를 시뮬레이트하는 콘솔 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-107">**SimulateDeviceMethods**, a console app which simulates a device connecting to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="c5295-108">[Azure IoT SDKs][lnk-hub-sdks] 문서는 장치와 솔루션 백 엔드에서 실행하기 위해 두 응용 프로그램을 빌드하는 데 사용할 수 있는 Azure IoT SDK에 관한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="c5295-109">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="c5295-110">Visual Studio 2015 또는 Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c5295-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="c5295-111">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="c5295-111">An active Azure account.</span></span> <span data-ttu-id="c5295-112">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="c5295-113">프로그래밍 방식으로 장치 ID를 만들려면 [.NET을 사용하여 IoT Hub에 시뮬레이트된 장치 연결][lnk-device-identity-csharp] 문서의 해당 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5295-113">If you want to create the device identity programmatically instead, read the corresponding section in the [Connect your simulated device to your IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="c5295-114">시뮬레이션된 장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="c5295-114">Create a simulated device app</span></span>
<span data-ttu-id="c5295-115">이 섹션에서는 솔루션 백 엔드에서 호출한 메서드에 응답하는 .NET 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-115">In this section, you create a .NET console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="c5295-116">Visual Studio에서 **콘솔 응용 프로그램** 프로젝트 템플릿을 사용하여 Visual C# Windows 클래식 데스크톱 프로젝트를 최신 솔루션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-116">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="c5295-117">프로젝트 이름을 **SimulateDeviceMethods**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-117">Name the project **SimulateDeviceMethods**.</span></span>
   
    ![새 Visual C# Windows 클래식 장치 앱][img-createdeviceapp]
    
1. <span data-ttu-id="c5295-119">솔루션 탐색기에서 **SimulateDeviceMethods** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 관리...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-119">In Solution Explorer, right-click the **SimulateDeviceMethods** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="c5295-120">**NuGet 패키지 관리자** 창에서 **찾아보기**를 선택하고 **microsoft.azure.devices.client**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-120">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="c5295-121">**설치**를 선택하여 **Microsoft.Azure.Devices.Client** 패키지를 설치한 후 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-121">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="c5295-122">이 절차에서는 [Azure IoT 장치 SDK][lnk-nuget-client-sdk] NuGet 패키지 및 해당 종속 항목에 참조를 다운로드, 설치 및 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-122">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 패키지 관리자 창 클라이언트 앱][img-clientnuget]
1. <span data-ttu-id="c5295-124">**Program.cs** 파일 위에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-124">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. <span data-ttu-id="c5295-125">**Program** 클래스에 다음 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-125">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="c5295-126">자리 표시자 값을 이전 섹션에서 메모한 장치 연결 문자열로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-126">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="c5295-127">장치에서 직접 메서드를 구현하도록 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-127">Add the following to implement the direct method on the device:</span></span>

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written to log.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. <span data-ttu-id="c5295-128">마지막으로 **Main** 메서드에 다음 코드를 추가하여 IoT Hub에 대한 연결을 열고 메서드 수신기를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-128">Finally, add the following code to the **Main** method to open the connection to your IoT hub and initialize the method listener:</span></span>
   
        try
        {
            Console.WriteLine("Connecting to hub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter to exit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove the "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. <span data-ttu-id="c5295-129">Visual Studio 솔루션 Explorer에서 솔루션을 마우스 오른쪽 단추로 클릭한 다음 **시작 프로젝트로 설정...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-129">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="c5295-130">**단일 시작 프로젝트**를 선택한 다음 드롭다운 메뉴에서 **SimulateDeviceMethods** 프로젝트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-130">Select **Single startup project**, and then select the **SimulateDeviceMethods** project in the dropdown menu.</span></span>        

> [!NOTE]
> <span data-ttu-id="c5295-131">간단히 하기 위해 이 자습서에서는 다시 시도 정책을 구현하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-131">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="c5295-132">[일시적인 오류 처리][lnk-transient-faults](영문) MSDN 문서에서 제시한 대로 프로덕션 코드에서 다시 시도 정책(예: 연결 다시 시도)을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-132">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="c5295-133">장치에서 직접 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="c5295-133">Call a direct method on a device</span></span>
<span data-ttu-id="c5295-134">이 섹션에서는 시뮬레이션된 장치 앱에서 메서드를 호출하고 응답을 표시하는 .NET 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-134">In this section, you create a .NET console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="c5295-135">Visual Studio에서 **콘솔 응용 프로그램** 프로젝트 템플릿을 사용하여 Visual C# Windows 클래식 데스크톱 프로젝트를 최신 솔루션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-135">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="c5295-136">.NET Framework 버전이 4.5.1 이상인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-136">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="c5295-137">프로젝트 이름을 **CallMethodOnDevice**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-137">Name the project **CallMethodOnDevice**.</span></span>
   
    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][img-createserviceapp]
2. <span data-ttu-id="c5295-139">[솔루션 Explorer]에서 **CallMethodOnDevice** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 관리...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-139">In Solution Explorer, right-click the **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="c5295-140">**NuGet 패키지 관리자** 창에서 **찾아보기**를 선택하고 **microsoft.azure.devices**를 검색한 다음 **설치**를 선택하여 **Microsoft.Azure.Devices** 패키지를 설치하고 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-140">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="c5295-141">이 프로시저에서는 [Azure IoT 서비스 SDK][lnk-nuget-service-sdk] NuGet 패키지 및 종속 항목에 참조를 다운로드, 설치 및 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-141">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 패키지 관리자 창][img-servicenuget]

4. <span data-ttu-id="c5295-143">**Program.cs** 파일 위에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-143">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="c5295-144">**Program** 클래스에 다음 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-144">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="c5295-145">자리 표시자 값을 이전 섹션에서 만든 허브의 IoT Hub 연결 문자열로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-145">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="c5295-146">**Program** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-146">Add the following method to the **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line to be written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="c5295-147">이 메서드는 `myDeviceId` 디바이스에서 `writeLine` 이름의 직접 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-147">This method invokes a direct method with name `writeLine` on the `myDeviceId` device.</span></span> <span data-ttu-id="c5295-148">그런 다음 장치에서 제공한 응답을 콘솔에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-148">Then, it writes the response provided by the device on the console.</span></span> <span data-ttu-id="c5295-149">장치에서 응답할 시간 제한 값을 지정할 수 있는 방법에 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="c5295-149">Note how it is possible to specify a timeout value for the device to respond.</span></span>
7. <span data-ttu-id="c5295-150">마지막으로 **Main** 메서드에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-150">Finally, add the following lines to the **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="c5295-151">Visual Studio 솔루션 Explorer에서 솔루션을 마우스 오른쪽 단추로 클릭한 다음 **시작 프로젝트로 설정...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-151">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="c5295-152">**단일 시작 프로젝트**를 선택한 다음 드롭다운 메뉴에서 **CallMethodOnDevice** 프로젝트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-152">Select **Single startup project**, and then select the **CallMethodOnDevice** project in the dropdown menu.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="c5295-153">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="c5295-153">Run the applications</span></span>
<span data-ttu-id="c5295-154">이제 응용 프로그램을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-154">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="c5295-155">.NET 장치 앱 **SimulateDeviceMethods**을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-155">Run the .NET device app **SimulateDeviceMethods**.</span></span> <span data-ttu-id="c5295-156">IoT Hub의 메서드 호출에 대한 수신이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-156">It should start listening for method calls from your IoT Hub:</span></span> 

    ![장치 앱 실행][img-deviceapprun]
1. <span data-ttu-id="c5295-158">이제 장치가 연결되어 메서드 호출을 기다리고 있으므로 **CallMethodOnDevice** .NET 앱을 실행하여 시뮬레이션된 장치 응용 프로그램에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-158">Now that the device is connected and waiting for method invocations, run the .NET **CallMethodOnDevice** app to invoke the method in the simulated device app.</span></span> <span data-ttu-id="c5295-159">콘솔에 작성된 장치 응답을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-159">You should see the device response written in the console.</span></span>
   
    ![서비스 앱 실행][img-serviceapprun]
1. <span data-ttu-id="c5295-161">장치는 다음 메시지를 표시하여 메서드에 반응합니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-161">The device then reacts to the method by printing this message:</span></span>
   
    ![장치에 대해 호출된 직접 메서드][img-directmethodinvoked]

## <a name="next-steps"></a><span data-ttu-id="c5295-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c5295-163">Next steps</span></span>
<span data-ttu-id="c5295-164">이 자습서에서는 Azure Portal에서 새 IoT Hub를 구성한 다음, IoT Hub의 ID 레지스트리에서 장치 ID를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-164">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="c5295-165">시뮬레이션된 장치 앱이 클라우드에서 호출한 메서드에 반응할 수 있도록 장치 ID를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-165">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="c5295-166">장치에서 메서드를 호출하고 장치의 응답을 표시하는 앱도 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5295-166">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="c5295-167">계속해서 IoT Hub을 시작하고 다른 IoT 시나리오를 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5295-167">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="c5295-168">[IoT Hub 시작]</span><span class="sxs-lookup"><span data-stu-id="c5295-168">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="c5295-169">[여러 장치에서 jobs 예약][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="c5295-169">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="c5295-170">IoT 솔루션을 확장하고 여러 장치에서 메서드 호출을 예약하는 방법을 알아보려면 [jobs 예약 및 브로드캐스트][lnk-tutorial-jobs] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5295-170">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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

<span data-ttu-id="c5295-171">[IoT Hub 시작]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="c5295-171">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>

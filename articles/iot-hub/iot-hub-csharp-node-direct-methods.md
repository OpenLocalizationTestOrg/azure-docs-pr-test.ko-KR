---
title: "Azure IoT Hub 직접 메서드(.NET/Node) 사용 | Microsoft Docs"
description: "Azure IoT Hub 직접 메서드를 사용하는 방법입니다. Node.js용 Azure IoT 장치 SDK를 사용하여 직접 메소드를 포함한 시뮬레이션된 장치 앱을 구현하며 .NET용 Azure IoT service SDK를 사용하여 직접 메소드를 호출하는 서비스 앱을 구현합니다."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: nberdy
ms.openlocfilehash: ad705789a153381e21b2ccb05d4e0c17f78671fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-direct-methods-netnode"></a><span data-ttu-id="651ab-104">직접 메서드 사용(.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="651ab-104">Use direct methods (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="651ab-105">이 자습서에서는 .NET 및 Node.js 콘솔 앱을 개발하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-105">In this tutorial, we are going to develop a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="651ab-106">**CallMethodOnDevice.js**: .NET 백엔드 앱으로 시뮬레이션된 장치 앱에서 메서드를 호출하고 응답을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-106">**CallMethodOnDevice.sln**, a .NET back-end app, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="651ab-107">**SimulatedDevice.js**: 앞에서 만든 장치 ID로 IoT Hub에 연결하고 클라우드에서 호출하는 메서드에 응답하는 장치를 시뮬레이션하는 Node.js 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-107">**SimulatedDevice.js**, a Node.js app, which simulates a device connecting to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="651ab-108">[Azure IoT SDKs][lnk-hub-sdks] 문서는 장치와 솔루션 백 엔드에서 실행하기 위해 두 응용 프로그램을 빌드하는 데 사용할 수 있는 Azure IoT SDK에 관한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="651ab-109">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="651ab-110">Visual Studio 2015 또는 Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="651ab-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="651ab-111">Node.js 버전 0.10.x 이상</span><span class="sxs-lookup"><span data-stu-id="651ab-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="651ab-112">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="651ab-112">An active Azure account.</span></span> <span data-ttu-id="651ab-113">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="651ab-114">시뮬레이션된 장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="651ab-114">Create a simulated device app</span></span>
<span data-ttu-id="651ab-115">이 섹션에서는 솔루션 백 엔드에서 호출한 메서드에 응답하는 Node.js 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-115">In this section, you create a Node.js console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="651ab-116">**simulateddevice**라는 빈 폴더를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-116">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="651ab-117">**simulateddevice** 폴더의 명령 프롬프트에서 다음 명령을 사용하여 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-117">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="651ab-118">모든 기본값을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="651ab-119">**simulateddevice** 폴더의 명령 프롬프트에서 다음 명령을 실행하여 **azure-iot-device** 및 **azure-iot-device-mqtt** 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-119">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="651ab-120">텍스트 편집기를 사용하여 **simulateddevice** 폴더에 새 파일을 만들고 이름을 **SimulatedDevice.js**으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-120">Using a text editor, create a file in the **simulateddevice** folder and name it **SimulatedDevice.js**.</span></span>
4. <span data-ttu-id="651ab-121">**SimulatedDevice.js** 파일 앞에 다음 `require` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-121">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="651ab-122">**connectionString** 변수를 추가하고 이 변수를 사용하여 **DeviceClient** 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-122">Add a **connectionString** variable and use it to create a **DeviceClient** instance.</span></span> <span data-ttu-id="651ab-123">**{장치 연결 문자열}**을 *장치 ID 만들기* 섹션에서 생성한 장치 연결 문자열로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-123">Replace **{device connection string}** with the device connection string you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="651ab-124">다음 함수를 추가하여 장치에서 직접 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-124">Add the following function to implement the direct method on the device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written to log.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="651ab-125">IoT Hub에 대한 연결을 열고 메서드 수신기를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-125">Open the connection to your IoT hub and initialize the method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. <span data-ttu-id="651ab-126">**SimulatedDevice.js** 파일을 저장한 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-126">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="651ab-127">간단히 하기 위해 이 자습서에서는 다시 시도 정책을 구현하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-127">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="651ab-128">[일시적인 오류 처리][lnk-transient-faults](영문) MSDN 문서에서 제시한 대로 프로덕션 코드에서 다시 시도 정책(예: 연결 다시 시도)을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-128">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="651ab-129">장치에서 직접 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="651ab-129">Call a direct method on a device</span></span>
<span data-ttu-id="651ab-130">이 섹션에서는 시뮬레이션된 장치 앱에서 메서드를 호출하고 응답을 표시하는 .NET 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-130">In this section, you create a .NET console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="651ab-131">Visual Studio에서 **콘솔 응용 프로그램** 프로젝트 템플릿을 사용하여 Visual C# Windows 클래식 데스크톱 프로젝트를 최신 솔루션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-131">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="651ab-132">.NET Framework 버전이 4.5.1 이상인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-132">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="651ab-133">프로젝트 이름을 **CallMethodOnDevice**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-133">Name the project **CallMethodOnDevice**.</span></span>
   
    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][10]
2. <span data-ttu-id="651ab-135">[솔루션 Explorer]에서 **CallMethodOnDevice** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 관리...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-135">In Solution Explorer, right-click the **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="651ab-136">**NuGet 패키지 관리자** 창에서 **찾아보기**를 선택하고 **microsoft.azure.devices**를 검색한 다음 **설치**를 선택하여 **Microsoft.Azure.Devices** 패키지를 설치하고 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-136">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="651ab-137">이 프로시저에서는 [Azure IoT 서비스 SDK][lnk-nuget-service-sdk] NuGet 패키지 및 종속 항목에 참조를 다운로드, 설치 및 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-137">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 패키지 관리자 창][11]

4. <span data-ttu-id="651ab-139">**Program.cs** 파일 위에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-139">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="651ab-140">**Program** 클래스에 다음 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-140">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="651ab-141">자리 표시자 값을 이전 섹션에서 만든 허브의 IoT Hub 연결 문자열로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-141">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="651ab-142">**Program** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-142">Add the following method to the **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line to be written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="651ab-143">이 메서드는 `myDeviceId` 디바이스에서 `writeLine` 이름의 직접 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-143">This method invokes a direct method with name `writeLine` on the `myDeviceId` device.</span></span> <span data-ttu-id="651ab-144">그런 다음 장치에서 제공한 응답을 콘솔에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-144">Then, it writes the response provided by the device on the console.</span></span> <span data-ttu-id="651ab-145">장치에서 응답할 시간 제한 값을 지정할 수 있는 방법에 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="651ab-145">Note how it is possible to specify a timeout value for the device to respond.</span></span>
7. <span data-ttu-id="651ab-146">마지막으로 **Main** 메서드에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-146">Finally, add the following lines to the **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

## <a name="run-the-applications"></a><span data-ttu-id="651ab-147">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="651ab-147">Run the applications</span></span>
<span data-ttu-id="651ab-148">이제 응용 프로그램을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-148">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="651ab-149">Visual Studio 솔루션 Explorer에서 솔루션을 마우스 오른쪽 단추로 클릭한 다음 **시작 프로젝트로 설정...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-149">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="651ab-150">**단일 시작 프로젝트**를 선택한 다음 드롭다운 메뉴에서 **CallMethodOnDevice** 프로젝트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-150">Select **Single startup project**, and then select the **CallMethodOnDevice** project in the dropdown menu.</span></span>

2. <span data-ttu-id="651ab-151">**simulateddevice** 폴더의 명령 프롬프트에서 다음 명령을 실행하여 IoT Hub의 메서드 호출에 대한 대기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-151">At a command prompt in the **simulateddevice** folder, run the following command to start listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   <span data-ttu-id="651ab-152">열려는 시뮬레이션된 장치를 기다립니다. ![][7]</span><span class="sxs-lookup"><span data-stu-id="651ab-152">Wait for the simulated device to open:  ![][7]</span></span>
3. <span data-ttu-id="651ab-153">이제 장치가 연결되어 메서드 호출을 기다리고 있으므로 **CallMethodOnDevice** .NET 앱을 실행하여 시뮬레이션된 장치 응용 프로그램에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-153">Now that the device is connected and waiting for method invocations, run the .NET **CallMethodOnDevice** app to invoke the method in the simulated device app.</span></span> <span data-ttu-id="651ab-154">콘솔에 작성된 장치 응답을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-154">You should see the device response written in the console.</span></span>
   
    ![][8]
4. <span data-ttu-id="651ab-155">장치는 다음 메시지를 표시하여 메서드에 반응합니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-155">The device then reacts to the method by printing this message:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="651ab-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="651ab-156">Next steps</span></span>
<span data-ttu-id="651ab-157">이 자습서에서는 Azure Portal에서 새 IoT Hub를 구성한 다음, IoT Hub의 ID 레지스트리에서 장치 ID를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-157">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="651ab-158">시뮬레이션된 장치 앱이 클라우드에서 호출한 메서드에 반응할 수 있도록 장치 ID를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-158">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="651ab-159">장치에서 메서드를 호출하고 장치의 응답을 표시하는 앱도 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="651ab-159">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="651ab-160">계속해서 IoT Hub을 시작하고 다른 IoT 시나리오를 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="651ab-160">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="651ab-161">[IoT Hub 시작]</span><span class="sxs-lookup"><span data-stu-id="651ab-161">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="651ab-162">[여러 장치에서 jobs 예약][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="651ab-162">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="651ab-163">IoT 솔루션을 확장하고 여러 장치에서 메서드 호출을 예약하는 방법을 알아보려면 [jobs 예약 및 브로드캐스트][lnk-tutorial-jobs] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="651ab-163">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-csharp-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-csharp-node-direct-methods/netserviceapp.png
[9]: ./media/iot-hub-csharp-node-direct-methods/methods-output.png

[10]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp1.png
[11]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp2.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
<span data-ttu-id="651ab-164">[IoT Hub 시작]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="651ab-164">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>

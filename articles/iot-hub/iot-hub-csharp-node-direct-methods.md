---
title: "Azure IoT Hub aaaUse 메서드 (.NET/노드)를 직접 | Microsoft Docs"
description: "어떻게 toouse Azure IoT Hub는 메서드를 전달 합니다. Node.js tooimplement 직접적인 방법 및 hello.NET tooimplement hello 직접 메서드를 호출 하는 서비스 응용 프로그램에 대 한 Azure IoT 서비스 SDK 포함 하는 시뮬레이션 된 장치 앱에 대 한 hello Azure IoT 장치 SDK를 사용 합니다."
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
ms.openlocfilehash: f566f939be840eb308b00ffa4e05c4e5b3fefb39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnode"></a><span data-ttu-id="53d21-104">직접 메서드 사용(.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="53d21-104">Use direct methods (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="53d21-105">이 자습서에서는 하겠습니다 toodevelop.NET 및 Node.js 콘솔 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="53d21-105">In this tutorial, we are going toodevelop a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="53d21-106">**CallMethodOnDevice.sln**, hello 시뮬레이션 된 장치 응용 프로그램의 메서드를 호출 하 고 hello 응답을 표시 하는.NET 백 엔드 앱.</span><span class="sxs-lookup"><span data-stu-id="53d21-106">**CallMethodOnDevice.sln**, a .NET back-end app, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="53d21-107">**SimulatedDevice.js**, 이전에 만든 hello 장치 id를 사용 하 여 tooyour IoT 허브를 연결 하는 장치를 시뮬레이션 및 hello 클라우드 호출한 toohello 메서드 이벤트에 응답 하는 Node.js 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-107">**SimulatedDevice.js**, a Node.js app, which simulates a device connecting tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="53d21-108">hello 문서 [Azure IoT Sdk] [ lnk-hub-sdks] 사용할 수 있는 toobuild 두 응용 프로그램 toorun 장치와 솔루션 백 엔드에, Azure IoT Sdk hello에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="53d21-109">toocomplete 해야이 자습서에서는:</span><span class="sxs-lookup"><span data-stu-id="53d21-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="53d21-110">Visual Studio 2015 또는 Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="53d21-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="53d21-111">Node.js 버전 0.10.x 이상</span><span class="sxs-lookup"><span data-stu-id="53d21-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="53d21-112">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="53d21-112">An active Azure account.</span></span> <span data-ttu-id="53d21-113">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="53d21-114">시뮬레이션된 장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="53d21-114">Create a simulated device app</span></span>
<span data-ttu-id="53d21-115">이 섹션에서는 응답 tooa 메서드 끝 hello 솔루션 다시에서 호출 하 여 Node.js 콘솔 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-115">In this section, you create a Node.js console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="53d21-116">**simulateddevice**라는 빈 폴더를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-116">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="53d21-117">Hello에 **simulateddevice** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-117">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="53d21-118">모든 hello 기본값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="53d21-119">Hello에 명령 프롬프트에 **simulateddevice** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iot 장치** 및 **azure iot-장치 mqtt** 패키지:</span><span class="sxs-lookup"><span data-stu-id="53d21-119">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="53d21-120">Hello에 파일을 만들 텍스트 편집기를 사용 하 여 **simulateddevice** 폴더 이름을 지정 **SimulatedDevice.js**합니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-120">Using a text editor, create a file in hello **simulateddevice** folder and name it **SimulatedDevice.js**.</span></span>
4. <span data-ttu-id="53d21-121">Hello 다음 추가 `require` hello의 시작 부분에 hello 문을 **SimulatedDevice.js** 파일:</span><span class="sxs-lookup"><span data-stu-id="53d21-121">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="53d21-122">추가 **connectionString** 변수 toocreate를 사용 하는 **DeviceClient** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="53d21-122">Add a **connectionString** variable and use it toocreate a **DeviceClient** instance.</span></span> <span data-ttu-id="53d21-123">대체 **{장치 연결 문자열을 (를)** hello에 생성 된 hello 장치 연결 문자열과 함께 *장치 id를 만드는* 섹션:</span><span class="sxs-lookup"><span data-stu-id="53d21-123">Replace **{device connection string}** with hello device connection string you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="53d21-124">Hello 함수 tooimplement hello에 대 한 직접 메서드 hello 장치에서 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-124">Add hello following function tooimplement hello direct method on hello device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="53d21-125">Hello 연결 tooyour IoT 허브를 열고 hello 메서드 수신기를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-125">Open hello connection tooyour IoT hub and initialize hello method listener:</span></span>
   
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
8. <span data-ttu-id="53d21-126">저장 후 닫기 hello **SimulatedDevice.js** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-126">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="53d21-127">단순 tookeep 항목을이 자습서는 어떠한 재시도 정책도 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-127">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="53d21-128">프로덕션 코드에 다시 시도 정책 (예: 연결 다시 시도) hello MSDN 문서에 설명 된 대로 구현 해야 [일시적인 오류 처리][lnk-transient-faults]합니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-128">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="53d21-129">장치에서 직접 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="53d21-129">Call a direct method on a device</span></span>
<span data-ttu-id="53d21-130">이 섹션에서는 다음 hello 응답을 표시 하 고 hello 시뮬레이션 된 장치 응용 프로그램에서 메서드를 호출 하는.NET 콘솔 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-130">In this section, you create a .NET console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="53d21-131">Visual Studio에서 Visual C# Windows 클래식 데스크톱 프로젝트 toohello 현재 솔루션 hello를 사용 하 여 추가 **콘솔 응용 프로그램** 서식 파일 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="53d21-131">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="53d21-132">Hello.NET Framework 버전 4.5.1 인지 확인 하거나 나중에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-132">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="53d21-133">이름 hello 프로젝트 **CallMethodOnDevice**합니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-133">Name hello project **CallMethodOnDevice**.</span></span>
   
    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][10]
2. <span data-ttu-id="53d21-135">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **CallMethodOnDevice** 프로젝트를 마우스 클릭 **NuGet 패키지 관리...** .</span><span class="sxs-lookup"><span data-stu-id="53d21-135">In Solution Explorer, right-click hello **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="53d21-136">Hello에 **NuGet 패키지 관리자** 창에서 **찾아보기**, 검색할 **microsoft.azure.devices**선택, **설치** tooinstall hello **Microsoft.Azure.Devices** 패키지 및 hello 사용 약관에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-136">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="53d21-137">이 절차를 다운로드, 설치 하 고 참조 toohello 추가 [Azure IoT 서비스 SDK] [ lnk-nuget-service-sdk] NuGet 패키지 및 해당 종속성.</span><span class="sxs-lookup"><span data-stu-id="53d21-137">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 패키지 관리자 창][11]

4. <span data-ttu-id="53d21-139">Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:</span><span class="sxs-lookup"><span data-stu-id="53d21-139">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="53d21-140">다음 필드 toohello hello 추가 **프로그램** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-140">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="53d21-141">Hello hello 이전 섹션에서 만든 hello 허브에 대 한 IoT 허브 연결 문자열 hello 자리 표시자 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-141">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="53d21-142">다음 메서드 toohello hello 추가 **프로그램** 클래스:</span><span class="sxs-lookup"><span data-stu-id="53d21-142">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="53d21-143">이 메서드는 이름으로 직접 메서드 호출 `writeLine` hello에 `myDeviceId` 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-143">This method invokes a direct method with name `writeLine` on hello `myDeviceId` device.</span></span> <span data-ttu-id="53d21-144">그런 다음 hello 콘솔에 hello 장치에서 제공 하는 hello 응답을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-144">Then, it writes hello response provided by hello device on hello console.</span></span> <span data-ttu-id="53d21-145">가능한 toospecify 장치 toorespond hello에 대 한 제한 시간 값을 방법은 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-145">Note how it is possible toospecify a timeout value for hello device toorespond.</span></span>
7. <span data-ttu-id="53d21-146">마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:</span><span class="sxs-lookup"><span data-stu-id="53d21-146">Finally, add hello following lines toohello **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

## <a name="run-hello-applications"></a><span data-ttu-id="53d21-147">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="53d21-147">Run hello applications</span></span>
<span data-ttu-id="53d21-148">준비 toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-148">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="53d21-149">에 hello Visual Studio 솔루션 탐색기, 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작 프로젝트 설정 중...** . 선택 **개의 시작 프로젝트**를 선택한 후 hello **CallMethodOnDevice** hello 드롭다운 메뉴에서 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="53d21-149">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **CallMethodOnDevice** project in hello dropdown menu.</span></span>

2. <span data-ttu-id="53d21-150">Hello에 명령 프롬프트에서 **simulateddevice** hello IoT 허브에서 메서드 호출을 수신 대기 하는 명령 toostart 다음를 실행 하는 폴더:</span><span class="sxs-lookup"><span data-stu-id="53d21-150">At a command prompt in hello **simulateddevice** folder, run hello following command toostart listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   <span data-ttu-id="53d21-151">시뮬레이션 된 hello 장치 tooopen 대기 시킵니다.![][7]</span><span class="sxs-lookup"><span data-stu-id="53d21-151">Wait for hello simulated device tooopen:  ![][7]</span></span>
3. <span data-ttu-id="53d21-152">이제 해당 hello 장치를 연결 하 고 hello.NET 실행 메서드 호출을 기다리는 **CallMethodOnDevice** hello 시뮬레이션 된 장치 앱의 앱 tooinvoke hello 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-152">Now that hello device is connected and waiting for method invocations, run hello .NET **CallMethodOnDevice** app tooinvoke hello method in hello simulated device app.</span></span> <span data-ttu-id="53d21-153">Hello 콘솔에 작성 된 hello 장치 응답을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-153">You should see hello device response written in hello console.</span></span>
   
    ![][8]
4. <span data-ttu-id="53d21-154">hello 장치는이 메시지를 인쇄 하 여 toohello 메서드 다음 반응 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-154">hello device then reacts toohello method by printing this message:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="53d21-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="53d21-155">Next steps</span></span>
<span data-ttu-id="53d21-156">이 자습서에서는 hello Azure 포털에서에서 새 IoT 허브를 구성 하 고 id 레지스트리에 hello IoT hub에서 장치 id를 만든 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-156">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="53d21-157">이 장치 identity tooenable hello 시뮬레이션 된 장치 앱 tooreact toomethods hello 클라우드 호출한 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-157">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="53d21-158">또한 hello 장치에 대 한 메서드를 호출 하 고 hello 장치에서 hello 응답을 표시 하는 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-158">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="53d21-159">시작 toocontinue IoT 허브와 tooexplore 다른 IoT 시나리오를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="53d21-159">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="53d21-160">[IoT Hub 시작]</span><span class="sxs-lookup"><span data-stu-id="53d21-160">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="53d21-161">[여러 장치에서 jobs 예약][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="53d21-161">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="53d21-162">toolearn tooextend IoT 솔루션 및 일정 메서드를 여러 장치에서 호출 하는 방법 참조 hello [일정 및 브로드캐스트 작업] [ lnk-tutorial-jobs] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="53d21-162">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
[IoT Hub 시작]: iot-hub-node-node-getstarted.md

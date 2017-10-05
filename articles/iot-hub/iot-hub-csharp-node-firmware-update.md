---
title: "Azure IoT Hub를 사용하여 장치 펌웨어 업데이트(.NET/Node) | Microsoft Docs"
description: "장치 펌웨어 업데이트를 시작하려면 Azure IoT Hub에서 장치 관리를 사용하는 방법입니다. Node.js용 Azure IoT 장치 SDK를 사용하여 시뮬레이션된 장치 앱을 구현하고 .NET용 Azure IoT 서비스 SDK를 사용하여 펌웨어 업데이트를 트리거하는 서비스 앱을 구현합니다."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/17/2017
ms.author: juanpere
ms.openlocfilehash: c2192328a152e955d182c4a07b391c98a5960964
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-device-management-to-initiate-a-device-firmware-update-netnode"></a><span data-ttu-id="97514-104">장치 관리를 사용하여 장치 펌웨어 업데이트(.NET/Node)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-104">Use device management to initiate a device firmware update (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="97514-105">소개</span><span class="sxs-lookup"><span data-stu-id="97514-105">Introduction</span></span>
<span data-ttu-id="97514-106">[장치 관리 시작][lnk-dm-getstarted] 자습서에서 [장치 쌍][lnk-devtwin] 및 [직접 메서드][lnk-c2dmethod] 기본 형식을 사용하여 장치를 원격으로 다시 부팅하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="97514-106">In the [Get started with device management][lnk-dm-getstarted] tutorial, you saw how to use the [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives to remotely reboot a device.</span></span> <span data-ttu-id="97514-107">이 자습서에서는 동일한 IoT Hub 기본 형식을 사용하고 시뮬레이션된 종단 간 펌웨어 업데이트를 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="97514-107">This tutorial uses the same IoT Hub primitives and shows you how to do an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="97514-108">이 패턴은 [Raspberry Pi 장치 구현 샘플][lnk-rpi-implementation]에 대한 펌웨어 업데이트 구현에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="97514-108">This pattern is used in the firmware update implementation for the [Raspberry Pi device implementation sample][lnk-rpi-implementation].</span></span>

<span data-ttu-id="97514-109">이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="97514-110">IoT Hub를 통해 시뮬레이션된 장치 앱에서 firmwareUpdate 직접 메서드를 호출하는 .NET 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97514-110">Create a .NET console app that calls the firmwareUpdate direct method in the simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="97514-111">**firmwareUpdate** 직접 메서드를 구현하는 시뮬레이트된 장치 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97514-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="97514-112">이 메서드는 펌웨어 이미지를 다운로드하기 위해 대기했다가 펌웨어 이미지를 다운로드하고, 마지막으로 펌웨어 이미지를 적용하는 다단계 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-112">This method initiates a multi-stage process that waits to download the firmware image, downloads the firmware image, and finally applies the firmware image.</span></span> <span data-ttu-id="97514-113">업데이트의 각 단계 동안, 장치는 보고된 속성을 사용하여 진행 상황을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-113">During each stage of the update, the device uses the reported properties to report on progress.</span></span>

<span data-ttu-id="97514-114">이 자습서의 끝 부분에는 다음과 같은 Node.js 콘솔 장치 앱과 .NET(C#) 콘솔 백 엔드 앱이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97514-114">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="97514-115">**dmpatterns_fwupdate_service.js** - 시뮬레이션된 장치 앱에서 직접 메서드를 호출하고 응답을 표시하며 업데이트된 reported 속성을 주기적으로(매 500밀리초) 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in the simulated device app, displays the response, and periodically (every 500ms) displays the updated reported properties.</span></span>

<span data-ttu-id="97514-116">**TriggerFWUpdate** - 앞에서 만든 장치 ID를 사용하여 IoT Hub 에 연결하고, firmwareUpdate 직접 메서드를 수신하며, 펌웨어 업데이트를 시뮬레이션하기 위한 다단계 프로세스(이미지 다운로드 대기, 새 이미지 다운로드, 마지막으로 이미지 적용 등)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-116">**TriggerFWUpdate**, which connects to your IoT hub with the device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process to simulate a firmware update including: waiting for the image download, downloading the new image, and finally applying the image.</span></span>

<span data-ttu-id="97514-117">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="97514-118">Visual Studio 2015 또는 Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="97514-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="97514-119">Node.js 버전 0.12.x 이상,</span><span class="sxs-lookup"><span data-stu-id="97514-119">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="97514-120">Windows 또는 Linux에서 이 자습서를 위해 Node.js를 설치하는 방법에 대해서는 [개발 환경 준비][lnk-dev-setup]에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-120">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="97514-121">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="97514-121">An active Azure account.</span></span> <span data-ttu-id="97514-122">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97514-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="97514-123">IoT hub 허브를 만들고 IoT Hub 연결 문자열을 확보하려면 [장치 관리 시작](iot-hub-csharp-node-device-management-get-started.md) 문서의 내용을 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="97514-123">Follow the [Get started with device management](iot-hub-csharp-node-device-management-get-started.md) article to create your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-the-device-using-a-direct-method"></a><span data-ttu-id="97514-124">직접 메서드를 사용하여 장치에서 원격 펌웨어 업데이트 트리거</span><span class="sxs-lookup"><span data-stu-id="97514-124">Trigger a remote firmware update on the device using a direct method</span></span>
<span data-ttu-id="97514-125">이 섹션에서는 장치에서 원격 펌웨어 업데이트를 시작하는 .NET 콘솔 앱(C# 사용)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97514-125">In this section, you create a .NET console app (using C#) that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="97514-126">앱은 직접 메서드를 사용하여 업데이트를 시작하고 장치 쌍 쿼리를 사용하여 정기적으로 활성 펌웨어 업데이트의 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="97514-126">The app uses a direct method to initiate the update and uses device twin queries to periodically get the status of the active firmware update.</span></span>

1. <span data-ttu-id="97514-127">Visual Studio에서 **콘솔 응용 프로그램** 프로젝트 템플릿을 사용하여 Visual C# Windows 클래식 데스크톱 프로젝트를 최신 솔루션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-127">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="97514-128">프로젝트 이름을 **TriggerFWUpdate**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-128">Name the project **TriggerFWUpdate**.</span></span>

    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][img-createapp]

1. <span data-ttu-id="97514-130">솔루션 탐색기에서 **TriggerFWUpdate** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 관리...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-130">In Solution Explorer, right-click the **TriggerFWUpdate** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="97514-131">**NuGet 패키지 관리자** 창에서 **찾아보기**를 선택하고 **microsoft.azure.devices**를 검색한 다음 **설치**를 선택하여 **Microsoft.Azure.Devices** 패키지를 설치하고 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-131">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="97514-132">이 프로시저에서는 [Azure IoT 서비스 SDK][lnk-nuget-service-sdk] NuGet 패키지 및 종속 항목에 참조를 다운로드, 설치 및 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-132">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![NuGet 패키지 관리자 창][img-servicenuget]
1. <span data-ttu-id="97514-134">**Program.cs** 파일 위에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-134">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. <span data-ttu-id="97514-135">**Program** 클래스에 다음 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-135">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="97514-136">여러 자리 표시자 값을 이전 섹션에서 만든 허브에 대한 IoT Hub 연결 문자열 및 장치의 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="97514-136">Replace the multiple placeholder values with the IoT Hub connection string for the hub that you created in the previous section and the Id of your device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. <span data-ttu-id="97514-137">**Program** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-137">Add the following method to the **Program** class:</span></span>
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. <span data-ttu-id="97514-138">**Program** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-138">Add the following method to the **Program** class:</span></span>

        public static async Task StartFirmwareUpdate()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("firmwareUpdate");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);
            method.SetPayloadJson(
                @"{
                    fwPackageUri : 'https://someurl'
                }");

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

1. <span data-ttu-id="97514-139">마지막으로 **Main** 메서드에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-139">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
        
1. <span data-ttu-id="97514-140">솔루션 탐색기에서 **시작 프로젝트 설정...**을 열고 **TriggerFWUpdate** 프로젝트의 **작업**이 **시작**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-140">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **TriggerFWUpdate** project is **Start**.</span></span>

1. <span data-ttu-id="97514-141">솔루션을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="97514-141">Build the solution.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-the-apps"></a><span data-ttu-id="97514-142">앱 실행</span><span class="sxs-lookup"><span data-stu-id="97514-142">Run the apps</span></span>
<span data-ttu-id="97514-143">이제 앱을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="97514-143">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="97514-144">**manageddevice** 폴더의 명령 프롬프트에서 다음 명령을 실행하여 다시 시작 직접 메서드에 대한 수신 대기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-144">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="97514-145">Visual Studio에서 **TriggerFWUpdate** 프로젝트를 마우스 오른쪽 단추로 클릭하고 C# 콘솔 앱을 실행한 후 **디버그**, **새 인스턴스 시작**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-145">In Visual Studio, right-click on the **TriggerFWUpdate** projectRun to the C# console app, select **Debug** and **Start new instance**.</span></span>

3. <span data-ttu-id="97514-146">콘솔에서 직접 메서드에 대한 장치 응답을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="97514-146">You see the device response to the direct method in the console.</span></span>

    ![펌웨어가 성공적으로 업데이트됨][img-fwupdate]

## <a name="next-steps"></a><span data-ttu-id="97514-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="97514-148">Next steps</span></span>
<span data-ttu-id="97514-149">이 자습서에서는 직접 메서드를 사용하여 장치에서 원격 펌웨어 업데이트를 트리거하고, 보고된 속성을 사용하여 펌웨어 업데이트 프로세스의 진행 상황을 이해했습니다.</span><span class="sxs-lookup"><span data-stu-id="97514-149">In this tutorial, you used a direct method to trigger a remote firmware update on a device and used the reported properties to follow the progress of the firmware update.</span></span>

<span data-ttu-id="97514-150">IoT 솔루션을 확장하고 여러 장치에서 메서드 호출을 예약하는 방법을 알아보려면 [jobs 예약 및 브로드캐스트][lnk-tutorial-jobs] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97514-150">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-firmware-update/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-firmware-update/createnetapp.png
[img-fwupdate]: media/iot-hub-csharp-node-firmware-update/fwupdated.png

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-rpi-implementation]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt_dm/pi_device
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
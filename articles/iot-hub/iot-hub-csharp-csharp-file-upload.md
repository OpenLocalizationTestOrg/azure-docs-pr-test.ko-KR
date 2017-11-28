---
title: "장치 tooAzure.net IoT 허브에서에서 aaaUpload 파일 | Microsoft Docs"
description: ".NET 용 Azure IoT 장치 SDK를 사용 하 여 장치 toohello 클라우드에서 tooupload 파일 방법 업로드된 파일은 Azure Storage blob 컨테이너에 저장됩니다."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: elioda
ms.openlocfilehash: 07d555f6ba8b067bbd3233bc8eebaa220ad2388b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub-using-net"></a><span data-ttu-id="04435-104">.NET을 사용 하 여 IoT Hub와 장치 toohello 클라우드에서 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-104">Upload files from your device toohello cloud with IoT Hub using .NET</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="04435-105">Hello에 hello 코드에 기반 하는이 자습서 [IoT Hub와 클라우드-장치 메시지를 보낼](iot-hub-csharp-csharp-c2d.md) 자습서 tooshow 있습니다 어떻게 toouse hello IoT 허브의 파일 업로드 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="04435-105">This tutorial builds on hello code in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial tooshow you how toouse hello file upload capabilities of IoT Hub.</span></span> <span data-ttu-id="04435-106">이 항목에서는 다음 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-106">It shows you how to:</span></span>

- <span data-ttu-id="04435-107">파일을 업로드하기 위한 Azure blob URI를 장치에 안전하게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="04435-108">앱 백 엔드에서 IoT Hub 파일 업로드 알림 tootrigger 처리 hello 파일 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-108">Use hello IoT Hub file upload notifications tootrigger processing hello file in your app back end.</span></span>

<span data-ttu-id="04435-109">hello [IoT 허브 시작](iot-hub-csharp-csharp-getstarted.md) 및 [IoT Hub와 클라우드-장치 메시지를 보낼](iot-hub-csharp-csharp-c2d.md) hello 장치-클라우드 및 클라우드-장치 메시징의 기본 기능 IoT Hub를 보여 주는 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="04435-109">hello [Get started with IoT Hub](iot-hub-csharp-csharp-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorials show hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="04435-110">hello [프로세스 장치-클라우드 메시지](iot-hub-csharp-csharp-process-d2c.md) 자습서에서는 Azure blob 저장소에 양방향 tooreliably 저장소 장치-클라우드 메시지를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-110">hello [Process Device-to-Cloud messages](iot-hub-csharp-csharp-process-d2c.md) tutorial describes a way tooreliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="04435-111">그러나 일부 시나리오에서는 장치가 IoT Hub 수락 하는 hello 상대적으로 작은 하는 장치-클라우드 메시지에 보낼 hello 데이터 쉽게 매핑할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="04435-111">However, in some scenarios you cannot easily map hello data your devices send into hello relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="04435-112">예:</span><span class="sxs-lookup"><span data-stu-id="04435-112">For example:</span></span>

* <span data-ttu-id="04435-113">이미지가 포함된 대형 파일</span><span class="sxs-lookup"><span data-stu-id="04435-113">Large files that contain images</span></span>
* <span data-ttu-id="04435-114">비디오</span><span class="sxs-lookup"><span data-stu-id="04435-114">Videos</span></span>
* <span data-ttu-id="04435-115">자주 샘플링되는 진동 데이터</span><span class="sxs-lookup"><span data-stu-id="04435-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="04435-116">특정 형태의 전처리된 데이터</span><span class="sxs-lookup"><span data-stu-id="04435-116">Some form of preprocessed data</span></span>

<span data-ttu-id="04435-117">이러한 파일은 일반적으로 일괄 처리와 같은 도구를 사용 하 여 hello 클라우드에서 [Azure Data Factory](../data-factory/index.md) 또는 hello [Hadoop](../hdinsight/index.md) 스택 합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-117">These files are typically batch processed in hello cloud using tools such as [Azure Data Factory](../data-factory/index.md) or hello [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="04435-118">장치에서 tooupload 파일 필요할 때 IoT 허브의 안정성 및 보안 hello 여전히 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04435-118">When you need tooupload files from a device, you can still use hello security and reliability of IoT Hub.</span></span>

<span data-ttu-id="04435-119">이 자습서의 hello 끝에 두 개의.NET 콘솔 응용 프로그램 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-119">At hello end of this tutorial you run two .NET console apps:</span></span>

* <span data-ttu-id="04435-120">**SimulatedDevice**, hello에서 만든 hello 응용 프로그램의 수정된 된 버전 [IoT Hub와 클라우드-장치 메시지를 보낼](iot-hub-csharp-csharp-c2d.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="04435-120">**SimulatedDevice**, a modified version of hello app created in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial.</span></span> <span data-ttu-id="04435-121">이 앱이 IoT 허브에서 제공 하는 SAS URI를 사용 하 여 파일 toostorage를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-121">This app uploads a file toostorage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="04435-122">**ReadFileUploadNotification** - IoT Hub에서 파일 업로드 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="04435-122">**ReadFileUploadNotification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="04435-123">IoT Hub는 Azure IoT 장치 SDK를 통해 많은 장치 플랫폼 및 언어(C, Java 및 Javascript 포함)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-123">IoT Hub supports many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="04435-124">Toohello 참조 [Azure IoT 개발자 센터] 방법에 대 한 단계별 지침에 대 한 tooconnect 프로그램 장치 tooAzure IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="04435-124">Refer toohello [Azure IoT Developer Center] for step-by-step instructions on how tooconnect your device tooAzure IoT Hub.</span></span>

<span data-ttu-id="04435-125">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="04435-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="04435-126">Visual Studio 2015 또는 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="04435-126">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="04435-127">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="04435-127">An active Azure account.</span></span> <span data-ttu-id="04435-128">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04435-128">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="04435-129">장치 앱에서 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="04435-129">Upload a file from a device app</span></span>

<span data-ttu-id="04435-130">이 섹션에서는 hello 장치 응용 프로그램에서 만든 수정 하면 [IoT Hub와 클라우드-장치 메시지를 보낼](iot-hub-csharp-csharp-c2d.md) hello IoT hub에서 클라우드-장치 메시지 tooreceive 합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-130">In this section, you modify hello device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="04435-131">Visual Studio에서 마우스 오른쪽 단추로 클릭 hello **SimulatedDevice** 프로젝트를 클릭 하 여 **추가**, 클릭 하 고 **기존 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-131">In Visual Studio, right-click hello **SimulatedDevice** project, click **Add**, and then click **Existing Item**.</span></span> <span data-ttu-id="04435-132">Tooan 이미지 파일을 탐색 하 고 프로젝트에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-132">Navigate tooan image file and include it in your project.</span></span> <span data-ttu-id="04435-133">이 자습서에서는 hello 이미지 이름이 가정 `image.jpg`합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-133">This tutorial assumes hello image is named `image.jpg`.</span></span>

1. <span data-ttu-id="04435-134">Hello 이미지를 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-134">Right-click on hello image, and then click **Properties**.</span></span> <span data-ttu-id="04435-135">다음 사항을 확인 **tooOutput 디렉터리 복사** 너무 설정**항상 복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-135">Make sure that **Copy tooOutput Directory** is set too**Copy always**.</span></span>

    ![][1]

1. <span data-ttu-id="04435-136">Hello에 **Program.cs** 파일, hello 다음 hello hello 파일 위쪽에 조건 추가:</span><span class="sxs-lookup"><span data-stu-id="04435-136">In hello **Program.cs** file, add hello following statements at hello top of hello file:</span></span>

    ```csharp
    using System.IO;
    ```

1. <span data-ttu-id="04435-137">다음 메서드 toohello hello 추가 **프로그램** 클래스:</span><span class="sxs-lookup"><span data-stu-id="04435-137">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    private static async void SendToBlobAsync()
    {
        string fileName = "image.jpg";
        Console.WriteLine("Uploading file: {0}", fileName);
        var watch = System.Diagnostics.Stopwatch.StartNew();

        using (var sourceData = new FileStream(@"image.jpg", FileMode.Open))
        {
            await deviceClient.UploadToBlobAsync(fileName, sourceData);
        }

        watch.Stop();
        Console.WriteLine("Time tooupload file: {0}ms\n", watch.ElapsedMilliseconds);
    }
    ```

    <span data-ttu-id="04435-138">hello `UploadToBlobAsync` 메서드 hello 파일 이름에는 및 업로드 하 고 hello 업로드 toostorage를 처리 하는 hello 파일 toobe의 스트림 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="04435-138">hello `UploadToBlobAsync` method takes in hello file name and stream source of hello file toobe uploaded and handles hello upload toostorage.</span></span> <span data-ttu-id="04435-139">hello 콘솔 응용 프로그램 tooupload hello 파일 hello 시간을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-139">hello console app displays hello time it takes tooupload hello file.</span></span>

1. <span data-ttu-id="04435-140">Hello hello에서 메서드를 다음 추가 **Main** hello 바로 앞의 메서드 `Console.ReadLine()` 줄:</span><span class="sxs-lookup"><span data-stu-id="04435-140">Add hello following method in hello **Main** method, right before hello `Console.ReadLine()` line:</span></span>

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> <span data-ttu-id="04435-141">간단히 하기 위해 이 자습서에서는 재시도 정책을 구현하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04435-141">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="04435-142">프로덕션 코드에 다시 시도 정책 (예: 지 수 형식의 백오프) hello MSDN 문서에 설명 된 대로 구현 해야 [일시적인 오류 처리]합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-142">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="04435-143">파일 업로드 알림 수신</span><span class="sxs-lookup"><span data-stu-id="04435-143">Receive a file upload notification</span></span>

<span data-ttu-id="04435-144">이 섹션에서는 IoT Hub에서 파일 업로드 알림 메시지를 수신하는 .NET 콘솔 앱을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-144">In this section, you write a .NET console app that receives file upload notification messages from IoT Hub.</span></span>

1. <span data-ttu-id="04435-145">Hello 현재 Visual Studio 솔루션에서 hello를 사용 하 여 Visual C# Windows 프로젝트를 만듭니다 **콘솔 응용 프로그램** 서식 파일 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="04435-145">In hello current Visual Studio solution, create a Visual C# Windows project by using hello **Console Application** project template.</span></span> <span data-ttu-id="04435-146">이름 hello 프로젝트 **ReadFileUploadNotification**합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-146">Name hello project **ReadFileUploadNotification**.</span></span>

    ![Visual Studio의 새 프로젝트][2]

1. <span data-ttu-id="04435-148">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ReadFileUploadNotification** 프로젝트를 마우스 클릭 **NuGet 패키지 관리...** .</span><span class="sxs-lookup"><span data-stu-id="04435-148">In Solution Explorer, right-click hello **ReadFileUploadNotification** project, and then click **Manage NuGet Packages...**.</span></span>

1. <span data-ttu-id="04435-149">Hello에 **NuGet 패키지 관리자** 창에 대 한 검색 **Microsoft.Azure.Devices**, 클릭 **설치**, hello 사용 약관에 동의 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04435-149">In hello **NuGet Package Manager** window, search for **Microsoft.Azure.Devices**, click **Install**, and accept hello terms of use.</span></span>

    <span data-ttu-id="04435-150">이 작업을 다운로드, 설치 하 고 참조 toohello 추가 [Azure IoT 서비스 SDK NuGet 패키지] hello에 **ReadFileUploadNotification** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="04435-150">This action downloads, installs, and adds a reference toohello [Azure IoT service SDK NuGet package] in hello **ReadFileUploadNotification** project.</span></span>

1. <span data-ttu-id="04435-151">Hello에 **Program.cs** 파일, hello 다음 hello hello 파일 위쪽에 조건 추가:</span><span class="sxs-lookup"><span data-stu-id="04435-151">In hello **Program.cs** file, add hello following statements at hello top of hello file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. <span data-ttu-id="04435-152">다음 필드 toohello hello 추가 **프로그램** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="04435-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="04435-153">대체 된 hello IoT 허브 연결 문자열에서 hello 자리 표시자 값 [IoT Hub와 시작 하려면]:</span><span class="sxs-lookup"><span data-stu-id="04435-153">Substitute hello placeholder value with hello IoT hub connection string from [Get started with IoT Hub]:</span></span>

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. <span data-ttu-id="04435-154">다음 메서드 toohello hello 추가 **프로그램** 클래스:</span><span class="sxs-lookup"><span data-stu-id="04435-154">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    private async static void ReceiveFileUploadNotificationAsync()
    {
        var notificationReceiver = serviceClient.GetFileNotificationReceiver();

        Console.WriteLine("\nReceiving file upload notification from service");
        while (true)
        {
            var fileUploadNotification = await notificationReceiver.ReceiveAsync();
            if (fileUploadNotification == null) continue;

            Console.ForegroundColor = ConsoleColor.Yellow;
            Console.WriteLine("Received file upload noticiation: {0}", string.Join(", ", fileUploadNotification.BlobName));
            Console.ResetColor();

            await notificationReceiver.CompleteAsync(fileUploadNotification);
        }
    }
    ```

    <span data-ttu-id="04435-155">이 수신 패턴 hello 장치 응용 프로그램에서 같은 하나의 사용 되는 tooreceive 클라우드-장치 메시지 hello는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-155">Note this receive pattern is hello same one used tooreceive cloud-to-device messages from hello device app.</span></span>

1. <span data-ttu-id="04435-156">마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:</span><span class="sxs-lookup"><span data-stu-id="04435-156">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter tooexit\n");
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="04435-157">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="04435-157">Run hello applications</span></span>

<span data-ttu-id="04435-158">이제 준비 toorun hello 응용 프로그램 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04435-158">Now you are ready toorun hello applications.</span></span>

1. <span data-ttu-id="04435-159">Visual Studio에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **시작 프로젝트 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-159">In Visual Studio, right-click your solution, and select **Set StartUp projects**.</span></span> <span data-ttu-id="04435-160">선택 **여러 개의 시작 프로젝트**을 선택한 후 hello **시작** 에 대 한 작업 **ReadFileUploadNotification** 및 **SimulatedDevice**합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-160">Select **Multiple startup projects**, then select hello **Start** action for **ReadFileUploadNotification** and **SimulatedDevice**.</span></span>

1. <span data-ttu-id="04435-161">**F5**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="04435-161">Press **F5**.</span></span> <span data-ttu-id="04435-162">두 응용 프로그램이 모두 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="04435-162">Both applications should start.</span></span> <span data-ttu-id="04435-163">한 콘솔 응용 프로그램에서 hello 업로드를 완료 하 고 hello 업로드 알림 메시지를 수신함 hello 다른 콘솔 응용 프로그램에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04435-163">You should see hello upload completed in one console app and hello upload notification message received by hello other console app.</span></span> <span data-ttu-id="04435-164">Hello를 사용할 수 있습니다 [Azure 포털] 또는 Visual Studio 서버 탐색기 toocheck hello의 hello 존재에 대 한 Azure 저장소 계정에서 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="04435-164">You can use hello [Azure portal] or Visual Studio Server Explorer toocheck for hello presence of hello uploaded file in your Azure Storage account.</span></span>

    ![][50]

## <a name="next-steps"></a><span data-ttu-id="04435-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="04435-165">Next steps</span></span>

<span data-ttu-id="04435-166">이 자습서에서는 toouse hello 파일에서 IoT Hub toosimplify 파일 업로드 장치에서의 기능을 업로드 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="04435-166">In this tutorial, you learned how toouse hello file upload capabilities of IoT Hub toosimplify file uploads from devices.</span></span> <span data-ttu-id="04435-167">다음 문서는 hello로 tooexplore IoT 허브 기능 및 시나리오를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04435-167">You can continue tooexplore IoT hub features and scenarios with hello following articles:</span></span>

* <span data-ttu-id="04435-168">[프로그래밍 방식으로 IoT Hub 만들기][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="04435-168">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="04435-169">[소개 tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="04435-169">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="04435-170">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="04435-170">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="04435-171">toofurther는 IoT Hub의 hello 기능을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="04435-171">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="04435-172">[IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="04435-172">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png

<!-- Links -->

[Azure 포털]: https://portal.azure.com/

[Azure IoT 개발자 센터]: http://www.azure.com/develop/iot

[일시적인 오류 처리]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure IoT 서비스 SDK NuGet 패키지]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md

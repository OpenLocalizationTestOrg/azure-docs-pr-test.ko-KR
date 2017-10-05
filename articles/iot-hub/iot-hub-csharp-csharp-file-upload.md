---
title: ".NET을 사용하여 장치에서 Azure IoT Hub로 파일 업로드 | Microsoft Docs"
description: ".NET용 Azure IoT 장치 SDK를 사용하여 장치에서 클라우드로 파일을 업로드 하는 방법입니다. 업로드된 파일은 Azure Storage blob 컨테이너에 저장됩니다."
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
ms.openlocfilehash: b45d85d0d77cf47f36cb793bc8c0dbe2d5c12634
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="upload-files-from-your-device-to-the-cloud-with-iot-hub-using-net"></a><span data-ttu-id="4d48f-104">.NET을 사용하여 장치에서 IoT Hub가 있는 클라우드로 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="4d48f-104">Upload files from your device to the cloud with IoT Hub using .NET</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="4d48f-105">이 자습서에서는 [IoT Hub를 사용하여 클라우드-장치 메시지 보내기](iot-hub-csharp-csharp-c2d.md) 자습서의 코드를 기반으로 작성되었으며 IoT Hub의 파일 업로드 기능을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-105">This tutorial builds on the code in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial to show you how to use the file upload capabilities of IoT Hub.</span></span> <span data-ttu-id="4d48f-106">이 항목에서는 다음 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-106">It shows you how to:</span></span>

- <span data-ttu-id="4d48f-107">파일을 업로드하기 위한 Azure blob URI를 장치에 안전하게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="4d48f-108">IoT Hub 파일 업로드 알림을 사용하여 앱 백 엔드에서 파일 처리를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-108">Use the IoT Hub file upload notifications to trigger processing the file in your app back end.</span></span>

<span data-ttu-id="4d48f-109">[IoT Hub 시작](iot-hub-csharp-csharp-getstarted.md) 및 [IoT Hub를 사용하여 클라우드-장치 메시지 보내기](iot-hub-csharp-csharp-c2d.md) 자습서는 IoT Hub의 기본적인 장치-클라우드 및 클라우드-장치 메시징 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-109">The [Get started with IoT Hub](iot-hub-csharp-csharp-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorials show the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="4d48f-110">[장치-클라우드 메시지 프로세스](iot-hub-csharp-csharp-process-d2c.md) 자습서에서는 장치-클라우드 메시지를 Azure Blob 저장소에 안정적으로 저장하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-110">The [Process Device-to-Cloud messages](iot-hub-csharp-csharp-process-d2c.md) tutorial describes a way to reliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="4d48f-111">그러나 일부 시나리오에서는 장치에서 전송하는 데이터를 IoT Hub에서 허용하는 비교적 작은 장치-클라우드 메시지에 쉽게 매핑할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-111">However, in some scenarios you cannot easily map the data your devices send into the relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="4d48f-112">예:</span><span class="sxs-lookup"><span data-stu-id="4d48f-112">For example:</span></span>

* <span data-ttu-id="4d48f-113">이미지가 포함된 대형 파일</span><span class="sxs-lookup"><span data-stu-id="4d48f-113">Large files that contain images</span></span>
* <span data-ttu-id="4d48f-114">비디오</span><span class="sxs-lookup"><span data-stu-id="4d48f-114">Videos</span></span>
* <span data-ttu-id="4d48f-115">자주 샘플링되는 진동 데이터</span><span class="sxs-lookup"><span data-stu-id="4d48f-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="4d48f-116">특정 형태의 전처리된 데이터</span><span class="sxs-lookup"><span data-stu-id="4d48f-116">Some form of preprocessed data</span></span>

<span data-ttu-id="4d48f-117">이러한 파일은 일반적으로 [Azure Data Factory](../data-factory/index.md) 또는 [Hadoop](../hdinsight/index.md) 스택과 같은 도구를 사용하여 클라우드에서 배치 방식으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-117">These files are typically batch processed in the cloud using tools such as [Azure Data Factory](../data-factory/index.md) or the [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="4d48f-118">장치에서 파일을 업로드해야 할 때 IoT Hub의 보안 및 안정성을 여전히 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-118">When you need to upload files from a device, you can still use the security and reliability of IoT Hub.</span></span>

<span data-ttu-id="4d48f-119">이 자습서의 끝 부분에서 다음의 두 .NET 콘솔 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-119">At the end of this tutorial you run two .NET console apps:</span></span>

* <span data-ttu-id="4d48f-120">**SimulatedDevice** - [IoT Hub를 사용하여 클라우드-장치 메시지 보내기](iot-hub-csharp-csharp-c2d.md) 자습서에서 만든 앱의 수정된 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-120">**SimulatedDevice**, a modified version of the app created in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial.</span></span> <span data-ttu-id="4d48f-121">이 앱은 IoT Hub에서 제공하는 SAS URI를 사용하여 저장소에 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-121">This app uploads a file to storage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="4d48f-122">**ReadFileUploadNotification** - IoT Hub에서 파일 업로드 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-122">**ReadFileUploadNotification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="4d48f-123">IoT Hub는 Azure IoT 장치 SDK를 통해 많은 장치 플랫폼 및 언어(C, Java 및 Javascript 포함)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-123">IoT Hub supports many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="4d48f-124">Azure IoT Hub에 장치를 연결하는 방법에 대한 단계별 지침은 [Azure IoT 개발자 센터]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d48f-124">Refer to the [Azure IoT Developer Center] for step-by-step instructions on how to connect your device to Azure IoT Hub.</span></span>

<span data-ttu-id="4d48f-125">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-125">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="4d48f-126">Visual Studio 2015 또는 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="4d48f-126">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="4d48f-127">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="4d48f-127">An active Azure account.</span></span> <span data-ttu-id="4d48f-128">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-128">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="4d48f-129">장치 앱에서 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="4d48f-129">Upload a file from a device app</span></span>

<span data-ttu-id="4d48f-130">이 섹션에서는 [IoT Hub를 사용하여 클라우드-장치 메시지 보내기](iot-hub-csharp-csharp-c2d.md)에서 만든 장치 앱을 수정하여 IoT Hub로부터 클라우드-장치 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-130">In this section, you modify the device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="4d48f-131">Visual Studio에서 **SimulatedDevice** 프로젝트를 마우스 오른쪽 단추로 클릭한 후 **추가**를 클릭하고 **기존 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-131">In Visual Studio, right-click the **SimulatedDevice** project, click **Add**, and then click **Existing Item**.</span></span> <span data-ttu-id="4d48f-132">이미지 파일을 찾아 프로젝트에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-132">Navigate to an image file and include it in your project.</span></span> <span data-ttu-id="4d48f-133">이 자습서에서는 이미지 이름을 `image.jpg`로 지정한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-133">This tutorial assumes the image is named `image.jpg`.</span></span>

1. <span data-ttu-id="4d48f-134">이미지를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-134">Right-click on the image, and then click **Properties**.</span></span> <span data-ttu-id="4d48f-135">**출력 디렉터리로 복사**가 **항상 복사**로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-135">Make sure that **Copy to Output Directory** is set to **Copy always**.</span></span>

    ![][1]

1. <span data-ttu-id="4d48f-136">**Program.cs** 파일 맨 위에 다음 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-136">In the **Program.cs** file, add the following statements at the top of the file:</span></span>

    ```csharp
    using System.IO;
    ```

1. <span data-ttu-id="4d48f-137">**Program** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-137">Add the following method to the **Program** class:</span></span>

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
        Console.WriteLine("Time to upload file: {0}ms\n", watch.ElapsedMilliseconds);
    }
    ```

    <span data-ttu-id="4d48f-138">`UploadToBlobAsync` 메서드는 업로드할 파일의 파일 이름 및 스트림 원본을 받은 후 업로드를 저장소로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-138">The `UploadToBlobAsync` method takes in the file name and stream source of the file to be uploaded and handles the upload to storage.</span></span> <span data-ttu-id="4d48f-139">콘솔 앱은 파일을 업로드하는 데 걸리는 시간을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-139">The console app displays the time it takes to upload the file.</span></span>

1. <span data-ttu-id="4d48f-140">**Main** 메서드에서 `Console.ReadLine()` 줄 바로 앞에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-140">Add the following method in the **Main** method, right before the `Console.ReadLine()` line:</span></span>

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> <span data-ttu-id="4d48f-141">간단히 하기 위해 이 자습서에서는 재시도 정책을 구현하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-141">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="4d48f-142">프로덕션 코드에서는 MSDN 문서 [일시적인 오류 처리]에서 제시한 대로 재시도 정책(예: 지수 백오프)을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-142">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="4d48f-143">파일 업로드 알림 수신</span><span class="sxs-lookup"><span data-stu-id="4d48f-143">Receive a file upload notification</span></span>

<span data-ttu-id="4d48f-144">이 섹션에서는 IoT Hub에서 파일 업로드 알림 메시지를 수신하는 .NET 콘솔 앱을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-144">In this section, you write a .NET console app that receives file upload notification messages from IoT Hub.</span></span>

1. <span data-ttu-id="4d48f-145">최신 Visual Studio 솔루션에서 **콘솔 응용 프로그램** 프로젝트 템플릿을 사용하여 Visual C# Windows 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-145">In the current Visual Studio solution, create a Visual C# Windows project by using the **Console Application** project template.</span></span> <span data-ttu-id="4d48f-146">프로젝트 이름을 **ReadFileUploadNotification**으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-146">Name the project **ReadFileUploadNotification**.</span></span>

    ![Visual Studio의 새 프로젝트][2]

1. <span data-ttu-id="4d48f-148">솔루션 Explorer에서 **ReadFileUploadNotification** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 관리...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-148">In Solution Explorer, right-click the **ReadFileUploadNotification** project, and then click **Manage NuGet Packages...**.</span></span>

1. <span data-ttu-id="4d48f-149">**NuGet 패키지 관리자** 창에서 **Microsoft.Azure.Devices**를 검색하고 **설치**를 클릭하고 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-149">In the **NuGet Package Manager** window, search for **Microsoft.Azure.Devices**, click **Install**, and accept the terms of use.</span></span>

    <span data-ttu-id="4d48f-150">이 작업은 [ReadFileUploadNotification] 프로젝트에서 **Azure IoT 서비스 SDK NuGet 패키지**에 대한 참조를 다운로드, 설치 및 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-150">This action downloads, installs, and adds a reference to the [Azure IoT service SDK NuGet package] in the **ReadFileUploadNotification** project.</span></span>

1. <span data-ttu-id="4d48f-151">**Program.cs** 파일 맨 위에 다음 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-151">In the **Program.cs** file, add the following statements at the top of the file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. <span data-ttu-id="4d48f-152">**Program** 클래스에 다음 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-152">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="4d48f-153">자리 표시자 값을 [IoT Hub 시작]에서 만든 IoT Hub 연결 문자열로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-153">Substitute the placeholder value with the IoT hub connection string from [Get started with IoT Hub]:</span></span>

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. <span data-ttu-id="4d48f-154">**Program** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-154">Add the following method to the **Program** class:</span></span>

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

    <span data-ttu-id="4d48f-155">수신 패턴은 장치 앱으로부터 클라우드-장치 메시지를 받는 데 사용되는 것과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-155">Note this receive pattern is the same one used to receive cloud-to-device messages from the device app.</span></span>

1. <span data-ttu-id="4d48f-156">마지막으로 **Main** 메서드에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-156">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter to exit\n");
    Console.ReadLine();
    ```

## <a name="run-the-applications"></a><span data-ttu-id="4d48f-157">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="4d48f-157">Run the applications</span></span>

<span data-ttu-id="4d48f-158">이제 응용 프로그램을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-158">Now you are ready to run the applications.</span></span>

1. <span data-ttu-id="4d48f-159">Visual Studio에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **시작 프로젝트 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-159">In Visual Studio, right-click your solution, and select **Set StartUp projects**.</span></span> <span data-ttu-id="4d48f-160">**여러 개의 시작 프로젝트**를 선택한 다음 **ReadFileUploadNotification** 및 **SimulatedDevice**에 대한 **시작** 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-160">Select **Multiple startup projects**, then select the **Start** action for **ReadFileUploadNotification** and **SimulatedDevice**.</span></span>

1. <span data-ttu-id="4d48f-161">**F5**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-161">Press **F5**.</span></span> <span data-ttu-id="4d48f-162">두 응용 프로그램이 모두 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-162">Both applications should start.</span></span> <span data-ttu-id="4d48f-163">한 콘솔 앱에서 완료된 업로드와 다른 콘솔 앱에서 수신한 업로드 알림 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-163">You should see the upload completed in one console app and the upload notification message received by the other console app.</span></span> <span data-ttu-id="4d48f-164">[Azure Portal] 또는 Visual Studio 서버 탐색기를 사용하여 Azure Storage 계정에서 업로드한 파일의 현재 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-164">You can use the [Azure portal] or Visual Studio Server Explorer to check for the presence of the uploaded file in your Azure Storage account.</span></span>

    ![][50]

## <a name="next-steps"></a><span data-ttu-id="4d48f-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4d48f-165">Next steps</span></span>

<span data-ttu-id="4d48f-166">이 자습서에서는 장치에서 파일 업로드를 단순화하기 위해 IoT Hub의 파일 업로드 기능을 사용하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-166">In this tutorial, you learned how to use the file upload capabilities of IoT Hub to simplify file uploads from devices.</span></span> <span data-ttu-id="4d48f-167">다음 문서를 사용하여 IoT Hub 기능 및 시나리오를 계속 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d48f-167">You can continue to explore IoT hub features and scenarios with the following articles:</span></span>

* <span data-ttu-id="4d48f-168">[프로그래밍 방식으로 IoT Hub 만들기][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="4d48f-168">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="4d48f-169">[C SDK 소개][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="4d48f-169">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="4d48f-170">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="4d48f-170">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="4d48f-171">IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d48f-171">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="4d48f-172">[IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="4d48f-172">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png

<!-- Links -->

<span data-ttu-id="4d48f-173">[Azure Portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="4d48f-173">[Azure portal]: https://portal.azure.com/</span></span>

<span data-ttu-id="4d48f-174">[Azure IoT 개발자 센터]: http://www.azure.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="4d48f-174">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span></span>

<span data-ttu-id="4d48f-175">[일시적인 오류 처리]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="4d48f-175">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
<span data-ttu-id="4d48f-176">[ReadFileUploadNotification]: https://www.nuget.org/packages/Microsoft.Azure.Devices/</span><span class="sxs-lookup"><span data-stu-id="4d48f-176">[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/</span></span>
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md

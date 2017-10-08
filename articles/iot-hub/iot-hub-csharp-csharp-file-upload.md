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
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub-using-net"></a>.NET을 사용 하 여 IoT Hub와 장치 toohello 클라우드에서 파일을 업로드 합니다.

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

Hello에 hello 코드에 기반 하는이 자습서 [IoT Hub와 클라우드-장치 메시지를 보낼](iot-hub-csharp-csharp-c2d.md) 자습서 tooshow 있습니다 어떻게 toouse hello IoT 허브의 파일 업로드 기능입니다. 이 항목에서는 다음 방법을 설명합니다.

- 파일을 업로드하기 위한 Azure blob URI를 장치에 안전하게 제공합니다.
- 앱 백 엔드에서 IoT Hub 파일 업로드 알림 tootrigger 처리 hello 파일 hello를 사용 합니다.

hello [IoT 허브 시작](iot-hub-csharp-csharp-getstarted.md) 및 [IoT Hub와 클라우드-장치 메시지를 보낼](iot-hub-csharp-csharp-c2d.md) hello 장치-클라우드 및 클라우드-장치 메시징의 기본 기능 IoT Hub를 보여 주는 자습서입니다. hello [프로세스 장치-클라우드 메시지](iot-hub-csharp-csharp-process-d2c.md) 자습서에서는 Azure blob 저장소에 양방향 tooreliably 저장소 장치-클라우드 메시지를 설명 합니다. 그러나 일부 시나리오에서는 장치가 IoT Hub 수락 하는 hello 상대적으로 작은 하는 장치-클라우드 메시지에 보낼 hello 데이터 쉽게 매핑할 수 없습니다. 예:

* 이미지가 포함된 대형 파일
* 비디오
* 자주 샘플링되는 진동 데이터
* 특정 형태의 전처리된 데이터

이러한 파일은 일반적으로 일괄 처리와 같은 도구를 사용 하 여 hello 클라우드에서 [Azure Data Factory](../data-factory/index.md) 또는 hello [Hadoop](../hdinsight/index.md) 스택 합니다. 장치에서 tooupload 파일 필요할 때 IoT 허브의 안정성 및 보안 hello 여전히 사용할 수 있습니다.

이 자습서의 hello 끝에 두 개의.NET 콘솔 응용 프로그램 실행합니다.

* **SimulatedDevice**, hello에서 만든 hello 응용 프로그램의 수정된 된 버전 [IoT Hub와 클라우드-장치 메시지를 보낼](iot-hub-csharp-csharp-c2d.md) 자습서입니다. 이 앱이 IoT 허브에서 제공 하는 SAS URI를 사용 하 여 파일 toostorage를 업로드 합니다.
* **ReadFileUploadNotification** - IoT Hub에서 파일 업로드 알림을 받습니다.

> [!NOTE]
> IoT Hub는 Azure IoT 장치 SDK를 통해 많은 장치 플랫폼 및 언어(C, Java 및 Javascript 포함)를 지원합니다. Toohello 참조 [Azure IoT 개발자 센터] 방법에 대 한 단계별 지침에 대 한 tooconnect 프로그램 장치 tooAzure IoT 허브입니다.

toocomplete이이 자습서에서는 다음 hello 필요:

* Visual Studio 2015 또는 Visual Studio 2017
* 활성 Azure 계정. 계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a>장치 앱에서 파일 업로드

이 섹션에서는 hello 장치 응용 프로그램에서 만든 수정 하면 [IoT Hub와 클라우드-장치 메시지를 보낼](iot-hub-csharp-csharp-c2d.md) hello IoT hub에서 클라우드-장치 메시지 tooreceive 합니다.

1. Visual Studio에서 마우스 오른쪽 단추로 클릭 hello **SimulatedDevice** 프로젝트를 클릭 하 여 **추가**, 클릭 하 고 **기존 항목**합니다. Tooan 이미지 파일을 탐색 하 고 프로젝트에 포함 합니다. 이 자습서에서는 hello 이미지 이름이 가정 `image.jpg`합니다.

1. Hello 이미지를 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다. 다음 사항을 확인 **tooOutput 디렉터리 복사** 너무 설정**항상 복사**합니다.

    ![][1]

1. Hello에 **Program.cs** 파일, hello 다음 hello hello 파일 위쪽에 조건 추가:

    ```csharp
    using System.IO;
    ```

1. 다음 메서드 toohello hello 추가 **프로그램** 클래스:

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

    hello `UploadToBlobAsync` 메서드 hello 파일 이름에는 및 업로드 하 고 hello 업로드 toostorage를 처리 하는 hello 파일 toobe의 스트림 원본입니다. hello 콘솔 응용 프로그램 tooupload hello 파일 hello 시간을 표시 합니다.

1. Hello hello에서 메서드를 다음 추가 **Main** hello 바로 앞의 메서드 `Console.ReadLine()` 줄:

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> 간단히 하기 위해 이 자습서에서는 재시도 정책을 구현하지 않습니다. 프로덕션 코드에 다시 시도 정책 (예: 지 수 형식의 백오프) hello MSDN 문서에 설명 된 대로 구현 해야 [일시적인 오류 처리]합니다.

## <a name="receive-a-file-upload-notification"></a>파일 업로드 알림 수신

이 섹션에서는 IoT Hub에서 파일 업로드 알림 메시지를 수신하는 .NET 콘솔 앱을 작성합니다.

1. Hello 현재 Visual Studio 솔루션에서 hello를 사용 하 여 Visual C# Windows 프로젝트를 만듭니다 **콘솔 응용 프로그램** 서식 파일 프로젝트. 이름 hello 프로젝트 **ReadFileUploadNotification**합니다.

    ![Visual Studio의 새 프로젝트][2]

1. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ReadFileUploadNotification** 프로젝트를 마우스 클릭 **NuGet 패키지 관리...** .

1. Hello에 **NuGet 패키지 관리자** 창에 대 한 검색 **Microsoft.Azure.Devices**, 클릭 **설치**, hello 사용 약관에 동의 하 고 있습니다.

    이 작업을 다운로드, 설치 하 고 참조 toohello 추가 [Azure IoT 서비스 SDK NuGet 패키지] hello에 **ReadFileUploadNotification** 프로젝트.

1. Hello에 **Program.cs** 파일, hello 다음 hello hello 파일 위쪽에 조건 추가:

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. 다음 필드 toohello hello 추가 **프로그램** 클래스입니다. 대체 된 hello IoT 허브 연결 문자열에서 hello 자리 표시자 값 [IoT Hub와 시작 하려면]:

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. 다음 메서드 toohello hello 추가 **프로그램** 클래스:

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

    이 수신 패턴 hello 장치 응용 프로그램에서 같은 하나의 사용 되는 tooreceive 클라우드-장치 메시지 hello는 참고 합니다.

1. 마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter tooexit\n");
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a>Hello 응용 프로그램 실행

이제 준비 toorun hello 응용 프로그램 됩니다.

1. Visual Studio에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **시작 프로젝트 설정**을 선택합니다. 선택 **여러 개의 시작 프로젝트**을 선택한 후 hello **시작** 에 대 한 작업 **ReadFileUploadNotification** 및 **SimulatedDevice**합니다.

1. **F5**키를 누릅니다. 두 응용 프로그램이 모두 시작됩니다. 한 콘솔 응용 프로그램에서 hello 업로드를 완료 하 고 hello 업로드 알림 메시지를 수신함 hello 다른 콘솔 응용 프로그램에 표시 됩니다. Hello를 사용할 수 있습니다 [Azure 포털] 또는 Visual Studio 서버 탐색기 toocheck hello의 hello 존재에 대 한 Azure 저장소 계정에서 파일을 업로드 합니다.

    ![][50]

## <a name="next-steps"></a>다음 단계

이 자습서에서는 toouse hello 파일에서 IoT Hub toosimplify 파일 업로드 장치에서의 기능을 업로드 하는 방법을 배웠습니다. 다음 문서는 hello로 tooexplore IoT 허브 기능 및 시나리오를 진행할 수 있습니다.

* [프로그래밍 방식으로 IoT Hub 만들기][lnk-create-hub]
* [소개 tooC SDK][lnk-c-sdk]
* [Azure IoT SDK][lnk-sdks]

toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

* [IoT Edge에서 장치 시뮬레이션][lnk-iotedge]

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

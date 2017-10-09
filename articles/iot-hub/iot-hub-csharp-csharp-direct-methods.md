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
# <a name="use-direct-methods-netnet"></a>직접 메서드 사용(.NET/.NET)
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

이 자습서는 진행 중인 toodevelop 두 개의.NET 콘솔 응용 프로그램:

* **CallMethodOnDevice**, hello 시뮬레이션 된 장치 응용 프로그램의 메서드를 호출 하 고 hello 응답을 표시 하는 백 엔드 응용 프로그램입니다.
* **SimulateDeviceMethods**, 이전에 만든 hello 장치 id를 사용 하 여 tooyour IoT 허브를 연결 하는 장치를 시뮬레이션 및 hello 클라우드 호출한 toohello 메서드 이벤트에 응답 하 여 콘솔 응용 프로그램입니다.

> [!NOTE]
> hello 문서 [Azure IoT Sdk] [ lnk-hub-sdks] 사용할 수 있는 toobuild 두 응용 프로그램 toorun 장치와 솔루션 백 엔드에, Azure IoT Sdk hello에 대 한 정보를 제공 합니다.
> 
> 

toocomplete 해야이 자습서에서는:

* Visual Studio 2015 또는 Visual Studio 2017.
* 활성 Azure 계정. 계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

원할 경우 toocreate hello 장치 id를 프로그래밍 방식으로 대신 hello의 hello 해당 섹션을 읽어 [.NET을 사용 하 여 시뮬레이션 된 장치 tooyour IoT 허브 연결] [ lnk-device-identity-csharp] 문서.


## <a name="create-a-simulated-device-app"></a>시뮬레이션된 장치 앱 만들기
이 섹션에서는 응답 tooa 메서드 끝 hello 솔루션 다시에서 호출 하 여.NET 콘솔 응용 프로그램을 만들 수 있습니다.

1. Visual Studio에서 Visual C# Windows 클래식 데스크톱 프로젝트 toohello 현재 솔루션 hello를 사용 하 여 추가 **콘솔 응용 프로그램** 서식 파일 프로젝트. 이름 hello 프로젝트 **SimulateDeviceMethods**합니다.
   
    ![새 Visual C# Windows 클래식 장치 앱][img-createdeviceapp]
    
1. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **SimulateDeviceMethods** 프로젝트를 마우스 클릭 **NuGet 패키지 관리...** .
1. Hello에 **NuGet 패키지 관리자** 창에서 **찾아보기** 검색 한 **microsoft.azure.devices.client**합니다. 선택 **설치** tooinstall hello **Microsoft.Azure.Devices.Client** 패키지 및 hello 사용 약관에 동의 합니다. 이 절차를 다운로드, 설치 하 고 참조 toohello 추가 [Azure IoT 장치 SDK] [ lnk-nuget-client-sdk] NuGet 패키지 및 해당 종속성.
   
    ![NuGet 패키지 관리자 창 클라이언트 앱][img-clientnuget]
1. Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. 다음 필드 toohello hello 추가 **프로그램** 클래스입니다. Hello 이전 섹션에서 기록한 hello 장치 연결 문자열 hello 자리 표시자 값을 바꿉니다.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. Hello tooimplement hello 직접적인 방법 hello 장치에서 다음을 추가 합니다.

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. 마지막으로, 다음 코드 toohello hello 추가 **Main** 메서드 tooopen hello 연결 tooyour IoT 허브 및 초기화 hello 메서드 수신기:
   
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
        
1. 에 hello Visual Studio 솔루션 탐색기, 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작 프로젝트 설정 중...** . 선택 **개의 시작 프로젝트**를 선택한 후 hello **SimulateDeviceMethods** hello 드롭다운 메뉴에서 프로젝트.        

> [!NOTE]
> 단순 tookeep 항목을이 자습서는 어떠한 재시도 정책도 구현 하지 않습니다. 프로덕션 코드에 다시 시도 정책 (예: 연결 다시 시도) hello MSDN 문서에 설명 된 대로 구현 해야 [일시적인 오류 처리][lnk-transient-faults]합니다.
> 
> 

## <a name="call-a-direct-method-on-a-device"></a>장치에서 직접 메서드 호출
이 섹션에서는 다음 hello 응답을 표시 하 고 hello 시뮬레이션 된 장치 응용 프로그램에서 메서드를 호출 하는.NET 콘솔 응용 프로그램을 만들 수 있습니다.

1. Visual Studio에서 Visual C# Windows 클래식 데스크톱 프로젝트 toohello 현재 솔루션 hello를 사용 하 여 추가 **콘솔 응용 프로그램** 서식 파일 프로젝트. Hello.NET Framework 버전 4.5.1 인지 확인 하거나 나중에 있습니다. 이름 hello 프로젝트 **CallMethodOnDevice**합니다.
   
    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][img-createserviceapp]
2. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **CallMethodOnDevice** 프로젝트를 마우스 클릭 **NuGet 패키지 관리...** .
3. Hello에 **NuGet 패키지 관리자** 창에서 **찾아보기**, 검색할 **microsoft.azure.devices**선택, **설치** tooinstall hello **Microsoft.Azure.Devices** 패키지 및 hello 사용 약관에 동의 합니다. 이 절차를 다운로드, 설치 하 고 참조 toohello 추가 [Azure IoT 서비스 SDK] [ lnk-nuget-service-sdk] NuGet 패키지 및 해당 종속성.
   
    ![NuGet 패키지 관리자 창][img-servicenuget]

4. Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. 다음 필드 toohello hello 추가 **프로그램** 클래스입니다. Hello hello 이전 섹션에서 만든 hello 허브에 대 한 IoT 허브 연결 문자열 hello 자리 표시자 값을 바꿉니다.
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. 다음 메서드 toohello hello 추가 **프로그램** 클래스:
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    이 메서드는 이름으로 직접 메서드 호출 `writeLine` hello에 `myDeviceId` 장치입니다. 그런 다음 hello 콘솔에 hello 장치에서 제공 하는 hello 응답을 씁니다. 가능한 toospecify 장치 toorespond hello에 대 한 제한 시간 값을 방법은 note 합니다.
7. 마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. 에 hello Visual Studio 솔루션 탐색기, 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작 프로젝트 설정 중...** . 선택 **개의 시작 프로젝트**를 선택한 후 hello **CallMethodOnDevice** hello 드롭다운 메뉴에서 프로젝트.

## <a name="run-hello-applications"></a>Hello 응용 프로그램 실행
준비 toorun hello 응용 프로그램입니다.

1. Hello.NET 장치 앱 실행 **SimulateDeviceMethods**합니다. IoT Hub의 메서드 호출에 대한 수신이 시작됩니다. 

    ![장치 앱 실행][img-deviceapprun]
1. 이제 해당 hello 장치를 연결 하 고 hello.NET 실행 메서드 호출을 기다리는 **CallMethodOnDevice** hello 시뮬레이션 된 장치 앱의 앱 tooinvoke hello 방법입니다. Hello 콘솔에 작성 된 hello 장치 응답을 표시 되어야 합니다.
   
    ![서비스 앱 실행][img-serviceapprun]
1. hello 장치는이 메시지를 인쇄 하 여 toohello 메서드 다음 반응 합니다.
   
    ![Hello 장치에서 호출 하는 직접 메서드][img-directmethodinvoked]

## <a name="next-steps"></a>다음 단계
이 자습서에서는 hello Azure 포털에서에서 새 IoT 허브를 구성 하 고 id 레지스트리에 hello IoT hub에서 장치 id를 만든 다음 합니다. 이 장치 identity tooenable hello 시뮬레이션 된 장치 앱 tooreact toomethods hello 클라우드 호출한 사용 했습니다. 또한 hello 장치에 대 한 메서드를 호출 하 고 hello 장치에서 hello 응답을 표시 하는 응용 프로그램을 만들었습니다. 

시작 toocontinue IoT 허브와 tooexplore 다른 IoT 시나리오를 참조 하세요.

* [IoT Hub 시작]
* [여러 장치에서 jobs 예약][lnk-devguide-jobs]

toolearn tooextend IoT 솔루션 및 일정 메서드를 여러 장치에서 호출 하는 방법 참조 hello [일정 및 브로드캐스트 작업] [ lnk-tutorial-jobs] 자습서입니다.

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

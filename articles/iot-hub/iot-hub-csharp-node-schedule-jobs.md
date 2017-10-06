---
title: "Azure IoT Hub (.NET/노드)와 aaaSchedule 작업 | Microsoft Docs"
description: "어떻게 tooschedule Azure IoT Hub 여러 장치에서 직접 메서드 tooinvoke를 작업입니다. Node.js tooimplement hello 시뮬레이션 된 장치 앱과 hello.NET tooimplement 서비스 응용 프로그램 toorun hello 작업에 대 한 Azure IoT 서비스 SDK에 대 한 hello Azure IoT 장치 SDK를 사용 합니다."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: juanpere
ms.openlocfilehash: f6148b67129dde4580bfe9ccceafd6400fbc5976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a>작업 예약 및 브로드캐스트(.NET/Node.js)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

수백만 개의 장치로 업데이트 하는 Azure IoT Hub tooschedule 및 추적 작업을 사용 합니다. 작업을 사용하여 다음을 수행합니다.

* desired 속성 업데이트
* tags 업데이트
* 직접 메서드 호출

작업이 다음이 작업 중 하나를 래핑하고 트랙 hello 장치로 이중 쿼리에 의해 정의 된 일련의 장치에 대 한 실행. 예를 들어 백 엔드 응용 프로그램 hello 장치를 다시 부팅 하는 장치 10, 000에서 작업 tooinvoke 직접 메서드를 사용할 수 있습니다. 장치로 이중 쿼리로 hello 일련의 장치를 지정 하 고 hello 작업 toorun 이후 시간에 예약 합니다. 각 hello 장치로 작업 추적 진행 상황 hello 수신 하 고 hello 재부팅 직접 메서드를 실행 합니다.

이러한 기능의 각각에 대해 자세히 toolearn 참조:

* 장치로 이중 및 속성: [장치 트윈스 시작] [ lnk-get-started-twin] 및 [자습서: 어떻게 toouse 장치로 이중 속성][lnk-twin-props]
* 직접 메서드: [IoT Hub 개발자 가이드 - 직접 메서드][lnk-dev-methods] 및 [자습서: 직접 메서드 사용][lnk-c2d-methods]

이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.

* 라는 직접 메서드를 구현 하는 장치 앱 만들기 **lockDoor** hello 백 엔드 응용 프로그램에서 호출할 수 있습니다. hello 장치 앱 hello 백 엔드 응용 프로그램에서 원하는 속성 변경 내용을 수신합니다.
* 백 엔드 앱을 만드는 작업 toocall hello 만들기 **lockDoor** 여러 장치에서 직접적인 방법입니다. 다른 작업이 toomultiple 장치를 업데이트 하는 원하는 속성을 보냅니다.

이 자습서의 hello 끝에 콘솔 장치 Node.js 응용 프로그램 및.NET (C#) 콘솔 백 엔드 응용 프로그램

**simDevice.js** tooyour IoT 허브를 연결 하는, 구현 hello **lockDoor** 메서드와 핸들 필요한 속성 변경 내용을 전송 합니다.

**ScheduleJob** 작업 toocall hello를 사용 하 여 **lockDoor** 원하는 여러 장치에서 속성을 직접 메서드와 업데이트 hello 장치로 이중 합니다.

toocomplete이이 자습서에서는 다음 hello 필요:

* Visual Studio 2015 또는 Visual Studio 2017.
* Node.js 버전 0.12.x 이상. hello 문서 [개발 환경을 준비] [ lnk-dev-setup] 설명 방법을 Windows 또는 Linux에서이 자습서에 대 한 tooinstall Node.js 합니다.
* 활성 Azure 계정. 계정이 없는 경우 몇 분 내에 [계정][lnk-free-trial]을 만들 수 있습니다.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a>직접 메서드를 호출하고 장치 쌍의 업데이트를 전송하기 위한 작업 예약

.NET 콘솔 응용 프로그램 (사용 하 여 C#) 작업 toocall hello를 사용 하는이 섹션에서는 만들 **lockDoor** 직접적인 방법 및 toomultiple 장치를 업데이트 하는 원하는 속성을 송신 합니다.

1. Visual Studio에서 Visual C# Windows 클래식 데스크톱 프로젝트 toohello 현재 솔루션 hello를 사용 하 여 추가 **콘솔 응용 프로그램** 서식 파일 프로젝트. 이름 hello 프로젝트 **ScheduleJob**합니다.

    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][img-createapp]

1. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ScheduleJob** 프로젝트를 마우스 클릭 **NuGet 패키지 관리...** .
1. Hello에 **NuGet 패키지 관리자** 창에서 **찾아보기**, 검색할 **microsoft.azure.devices**선택, **설치** tooinstall hello **Microsoft.Azure.Devices** 패키지 및 hello 사용 약관에 동의 합니다. 이 단계를 다운로드, 설치 하 고 참조 toohello 추가 [Azure IoT 서비스 SDK] [ lnk-nuget-service-sdk] NuGet 패키지 및 해당 종속성.

    ![NuGet 패키지 관리자 창][img-servicenuget]
1. Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. Hello 다음 추가 `using` 문을 hello 기본 문에서 아직 없는 경우.

    ```csharp
    using System.Threading.Tasks;
    ```

1. 다음 필드 toohello hello 추가 **프로그램** 클래스입니다. Hello hello 이전 섹션에서 만든 hello 허브에 대 한 IoT 허브 연결 문자열 hello 자리 표시자를 바꿉니다.

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. 다음 메서드 toohello hello 추가 **프로그램** 클래스:

    ```csharp
    public static async Task MonitorJob(string jobId)
    {
        JobResponse result;
        do
        {
            result = await jobClient.GetJobAsync(jobId);
            Console.WriteLine("Job Status : " + result.Status.ToString());
            Thread.Sleep(2000);
        } while ((result.Status != JobStatus.Completed) && (result.Status != JobStatus.Failed));
    }
    ```

1. 다음 메서드 toohello hello 추가 **프로그램** 클래스:

    ```csharp
    public static async Task StartMethodJob(string jobId)
    {
        CloudToDeviceMethod directMethod = new CloudToDeviceMethod("lockDoor", TimeSpan.FromSeconds(5), TimeSpan.FromSeconds(5));

        JobResponse result = await jobClient.ScheduleDeviceMethodAsync(jobId,
            "deviceId='myDeviceId'",
            directMethod,
            DateTime.Now,
            10);

        Console.WriteLine("Started Method Job");
    }
    ```

1. 다음 메서드 toohello hello 추가 **프로그램** 클래스:

    ```csharp
    public static async Task StartTwinUpdateJob(string jobId)
    {
        var twin = new Twin();
        twin.Properties.Desired["Building"] = "43";
        twin.Properties.Desired["Floor"] = "3";
        twin.ETag = "*";

        JobResponse result = await jobClient.ScheduleTwinUpdateAsync(jobId,
            "deviceId='myDeviceId'",
            twin,
            DateTime.Now,
            10);

        Console.WriteLine("Started Twin Update Job");
    }
    ```

1. 마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER toorun hello next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER tooexit.");
    Console.ReadLine();
    ```

1. Hello 솔루션 탐색기를 열고 hello **설정 시작 프로젝트...**  hello 있는지를 확인 하 고 **동작** 에 대 한 **ScheduleJob** 프로젝트는 **시작**합니다. Hello 솔루션을 빌드하십시오.

## <a name="create-a-simulated-device-app"></a>시뮬레이션된 장치 앱 만들기

이 섹션에서는 tooa 직접 메서드 호출에서 시뮬레이션 된 장치를 다시 부팅을 트리거하는 hello 클라우드가 응답 하 여 Node.js 콘솔 응용 프로그램을 만들고 사용 하 여 hello 속성 tooenable 장치로 이중 쿼리 tooidentify 장치 및 마지막 재부팅 될 보고 합니다.

1. **simDevice**라는 빈 폴더를 새로 만듭니다.  Hello에 **simDevice** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 package.json 파일을 만듭니다.  모든 hello 기본값을 적용 합니다.

    ```cmd/sh
    npm init
    ```

1. Hello에 명령 프롬프트에 **simDevice** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iot 장치** 및 **azure iot-장치 mqtt** 패키지:

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. 텍스트 편집기를 사용 하 여 만드는 새 **simDevice.js** hello에 대 한 파일 **simDevice** 폴더입니다.

1. Hello 다음 '필요' hello hello 시작 부분에 설명 추가 **simDevice.js** 파일:

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. 추가 **connectionString** 변수 toocreate를 사용 하는 **클라이언트** 인스턴스. 있는지 tooreplace hello 자리 표시자 값 적절 한 tooyour 설치 프로그램을 확인 하십시오.

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. 다음 함수 toohandle hello hello 추가 **lockDoor** 메서드.

    ```nodejs
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```

1. Hello hello에 대 한 코드 tooregister hello 처리기를 다음 추가 **lockDoor** 메서드.

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. 저장 후 닫기 hello **simDevice.js** 파일입니다.

> [!NOTE]
> 단순 tookeep 항목을이 자습서는 어떠한 재시도 정책도 구현 하지 않습니다. 프로덕션 코드에서는 hello MSDN 문서에 설명 된 대로 다시 시도 정책 (예: 지 수 백오프)를 구현 해야 [일시적인 오류 처리][lnk-transient-faults]합니다.

## <a name="run-hello-apps"></a>Hello 앱 실행

준비 toorun hello 앱입니다.

1. Hello에 대 한 hello 명령 프롬프트 **simDevice** 폴더를 다음 명령 toobegin hello 재부팅 직접적인 방법에 대 한 수신 대기 하는 hello를 실행 합니다.

    ```cmd/sh
    node simDevice.js
    ```

1. 실행된 hello C# 콘솔 응용 프로그램 **ScheduleJob** hello를 마우스 오른쪽 단추로 클릭 하 여 **ScheduleJob** 프로젝트를 선택 하면 다음 **디버그** 및 **새 인스턴스 시작**.

1. Hello 출력 장치와 백 엔드 응용 프로그램에서 표시 됩니다.

    ![Hello 앱 tooschedule 작업 실행][img-schedulejobs]

## <a name="next-steps"></a>다음 단계

이 자습서에서는 작업 tooschedule 직접적인 방법 tooa 장치 및 hello hello 장치로 이중의 속성을 업데이트를 사용 합니다.

읽을 hello 공기 펌웨어 업데이트를 통해 원격으로 등 IoT Hub 및 장치 관리 패턴 시작 toocontinue [자습서: 펌웨어 업데이트 하는 toodo 어떻게][lnk-fwupdate]합니다.

IoT Hub와 시작 toocontinue 참조 [IoT 가장자리 시작][lnk-iot-edge]합니다.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-schedule-jobs/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-schedule-jobs/createnetapp.png
[img-schedulejobs]: media/iot-hub-csharp-node-schedule-jobs/schedulejobs.png

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

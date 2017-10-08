---
title: "Azure IoT Hub (.NET/노드)와 aaaDevice 펌웨어 업데이트 | Microsoft Docs"
description: "Azure IoT Hub tooinitiate 장치 펌웨어에 toouse 장치 관리 업데이트 하는 방법입니다. Node.js tooimplement 시뮬레이션 된 장치 응용 프로그램에 대 한 hello Azure IoT 장치 SDK 및.NET tooimplement hello 펌웨어 업데이트가 발생 하는 서비스 앱에 대 한 Azure IoT 서비스 SDK hello를 사용 합니다."
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
ms.openlocfilehash: d48899651bcd5d67e577c971be0f9453c8f21592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-netnode"></a>장치 관리 tooinitiate 장치 펌웨어 업데이트 (.NET/노드)를 사용 하 여
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a>소개
Hello에 [장치 관리 시작] [ lnk-dm-getstarted] 자습서에서 언급 했 듯이 어떻게 toouse hello [장치로 이중] [ lnk-devtwin] 및 [직접 메서드] [ lnk-c2dmethod] 기본 형식 tooremotely는 장치를 다시 부팅 합니다. 이 자습서에서는 hello IoT Hub 기본 형식과 동일 하 고는-종단 toodo 펌웨어 업데이트를 시뮬레이션 하는 방법을 보여 줍니다.  이 패턴은 hello에 대 한 hello 펌웨어 업데이트 구현에서 사용 [라스베리 Pi 장치 구현 샘플][lnk-rpi-implementation]합니다.

이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.

* IoT 허브를 통해 hello 시뮬레이션 된 장치 응용 프로그램에서 hello firmwareUpdate 직접 메서드를 호출 하 여.NET 콘솔 응용 프로그램을 만듭니다.
* **firmwareUpdate** 직접 메서드를 구현하는 시뮬레이트된 장치 앱을 만듭니다. 이 메서드를 toodownload hello 펌웨어 이미지 될 때까지 대기 하 고, hello 펌웨어 이미지를 다운로드 하 고, 마지막으로 hello 펌웨어 이미지를 적용 하는 여러 단계로 이루어진 프로세스를 시작 합니다. Hello 업데이트의 각 단계 hello 장치 사용 하 여 hello 속성 tooreport를 진행률 보고 했습니다.

이 자습서의 hello 끝에 콘솔 장치 Node.js 응용 프로그램 및.NET (C#) 콘솔 백 엔드 응용 프로그램

**dmpatterns_fwupdate_service.js**, hello 응답 표시 hello 시뮬레이션 된 장치 응용 프로그램에서 직접 메서드를 호출 하 고 정기적으로 (500 밀리초 마다) 업데이트 표시 hello 보고 속성입니다.

**TriggerFWUpdate**를 포함 하 여 펌웨어 업데이트 다중 상태 프로세스 toosimulate을 통해 실행을 firmwareUpdate 직접 메서드를 받으면 앞에서 만든 hello 장치 id를 가진 tooyour IoT 허브를 연결 하는: hello 이미지 다운로드를 기다리는 중 hello 새 이미지와 마지막으로 적용 hello 이미지를 다운로드 합니다.

toocomplete이이 자습서에서는 다음 hello 필요:

* Visual Studio 2015 또는 Visual Studio 2017.
* Node.js 버전 0.12.x 이상, <br/>  [개발 환경을 준비] [ lnk-dev-setup] 설명 방법을 Windows 또는 Linux에서이 자습서에 대 한 tooinstall Node.js 합니다.
* 활성 Azure 계정. 계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.

Hello에 따라 [장치 관리 시작](iot-hub-csharp-node-device-management-get-started.md) 문서 toocreate IoT hub 및 IoT 허브 연결 문자열을 가져옵니다.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a>직접 메서드를 사용 하 여 hello 장치에 대 한 원격 펌웨어 업데이트 트리거
이 섹션에서는 장치에서 원격 펌웨어 업데이트를 시작하는 .NET 콘솔 앱(C# 사용)을 만듭니다. hello 앱 직접적인 방법 tooinitiate hello 업데이트를 사용 하 고 사용 하 여 장치로 이중 쿼리 tooperiodically hello 액티브 펌웨어 업데이트의 hello 상태를 가져옵니다.

1. Visual Studio에서 Visual C# Windows 클래식 데스크톱 프로젝트 toohello 현재 솔루션 hello를 사용 하 여 추가 **콘솔 응용 프로그램** 서식 파일 프로젝트. 이름 hello 프로젝트 **TriggerFWUpdate**합니다.

    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][img-createapp]

1. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **TriggerFWUpdate** 프로젝트를 마우스 클릭 **NuGet 패키지 관리...** .
1. Hello에 **NuGet 패키지 관리자** 창에서 **찾아보기**, 검색할 **microsoft.azure.devices**선택, **설치** tooinstall hello **Microsoft.Azure.Devices** 패키지 및 hello 사용 약관에 동의 합니다. 이 절차를 다운로드, 설치 하 고 참조 toohello 추가 [Azure IoT 서비스 SDK] [ lnk-nuget-service-sdk] NuGet 패키지 및 해당 종속성.

    ![NuGet 패키지 관리자 창][img-servicenuget]
1. Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. 다음 필드 toohello hello 추가 **프로그램** 클래스입니다. Hello로 여러 자리 표시자 값 hello hello 이전 섹션에서 만든 hello 허브에 대 한 IoT 허브 연결 문자열 및 hello 장치 Id 대체 합니다.
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. 다음 메서드 toohello hello 추가 **프로그램** 클래스:
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. 다음 메서드 toohello hello 추가 **프로그램** 클래스:

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

1. 마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
1. Hello 솔루션 탐색기를 열고 hello **설정 시작 프로젝트...**  hello 있는지를 확인 하 고 **동작** 에 대 한 **TriggerFWUpdate** 프로젝트는 **시작**합니다.

1. Hello 솔루션을 빌드하십시오.

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a>Hello 앱 실행
준비 toorun hello 앱입니다.

1. Hello에 대 한 hello 명령 프롬프트 **manageddevice** 폴더를 다음 명령 toobegin hello 재부팅 직접적인 방법에 대 한 수신 대기 하는 hello를 실행 합니다.
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. Visual Studio에서 마우스 오른쪽 단추로 클릭 hello **TriggerFWUpdate** projectRun toohello C# 콘솔 응용 프로그램, 선택 **디버그** 및 **새 인스턴스 시작**합니다.

3. Hello 장치 응답 toohello 직접적인 방법 hello 콘솔에 표시 됩니다.

    ![펌웨어가 성공적으로 업데이트됨][img-fwupdate]

## <a name="next-steps"></a>다음 단계
이 자습서에서는 직접적인 방법 tootrigger 원격을 사용 하는 장치 및 사용 하는 hello에 펌웨어 업데이트가 보고 되는 hello 펌웨어 업데이트의 속성 toofollow hello 진행률입니다.

toolearn tooextend IoT 솔루션 및 일정 메서드를 여러 장치에서 호출 하는 방법 참조 hello [일정 및 브로드캐스트 작업] [ lnk-tutorial-jobs] 자습서입니다.

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
---
title: "Azure IoT Hub 장치 관리 (.NET/노드) aaaGet 시작 | Microsoft Docs"
description: "어떻게 toouse Azure IoT Hub 장치 관리 tooinitiate 원격 장치를 다시 부팅 합니다. Node.js tooimplement 직접적인 방법 및 hello.NET tooimplement hello 직접 메서드를 호출 하는 서비스 응용 프로그램에 대 한 Azure IoT 서비스 SDK 포함 하는 시뮬레이션 된 장치 앱에 대 한 hello Azure IoT 장치 SDK를 사용 합니다."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/17/2016
ms.author: juanpere
ms.openlocfilehash: ea6d50dfac1c222d7836e3bf5503c6c9b8c89dfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-netnode"></a>장치 관리 시작(.NET/Node)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.

* Azure 포털 toocreate IoT Hub hello를 사용 하 및 IoT 허브에서 장치 id를 만드는 키를 누릅니다.
* 장치를 다시 시작하는 직접 메서드가 포함된 시뮬레이트된 장치 앱을 만듭니다. Hello 클라우드에서 직접 메서드 호출 됩니다.
* IoT 허브를 통해 hello 시뮬레이션 된 장치 응용 프로그램에서 hello 재부팅 직접 메서드를 호출 하 여.NET 콘솔 응용 프로그램을 만듭니다.

이 자습서의 hello 끝에 콘솔 장치 Node.js 응용 프로그램 및.NET (C#) 콘솔 백 엔드 응용 프로그램

**dmpatterns_getstarted_device.js**, 이전에 만든 hello 장치 id를 가진 tooyour IoT 허브를 연결 하는 다시 부팅 직접적인 방법, 실제 다시 부팅을 시뮬레이션 받아 hello 마지막 다시 부팅에 대 한 hello 시간을 보고 합니다.

**TriggerReboot**을 hello 응답 표시 hello 시뮬레이션 된 장치 응용 프로그램에서 직접 메서드를 호출 하 하 고 표시 hello 업데이트 속성을 보고 합니다.

toocomplete이이 자습서에서는 다음 hello 필요:

* Visual Studio 2015 또는 Visual Studio 2017.
* Node.js 버전 0.12.x 이상, <br/>  [개발 환경을 준비] [ lnk-dev-setup] 설명 방법을 Windows 또는 Linux에서이 자습서에 대 한 tooinstall Node.js 합니다.
* 활성 Azure 계정. 계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>트리거는 직접 메서드를 사용 하 여 hello 장치에 원격 컴퓨터를 다시 부팅
이 섹션에서는 장치에서 직접 메서드를 사용하여 원격 다시 시작을 시작하는 .NET 콘솔 앱(C# 사용)을 만듭니다. hello 앱 해당 장치에 대 한 장치로 이중 쿼리 toodiscover hello 마지막 부팅 시간을 사용합니다.

1. Visual Studio에서 Visual C# Windows 클래식 데스크톱 프로젝트 tooa 새 솔루션 hello를 사용 하 여 추가 **콘솔 응용 프로그램 (.NET Framework)** 서식 파일 프로젝트. Hello.NET Framework 버전 4.5.1 인지 확인 하거나 나중에 있습니다. 이름 hello 프로젝트 **TriggerReboot**합니다.

    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][img-createapp]

2. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **TriggerReboot** 프로젝트를 마우스 클릭 **NuGet 패키지 관리**합니다.
3. Hello에 **NuGet 패키지 관리자** 창에서 **찾아보기**, 검색할 **microsoft.azure.devices**선택, **설치** tooinstall hello **Microsoft.Azure.Devices** 패키지 및 hello 사용 약관에 동의 합니다. 이 절차를 다운로드, 설치 하 고 참조 toohello 추가 [Azure IoT 서비스 SDK] [ lnk-nuget-service-sdk] NuGet 패키지 및 해당 종속성.

    ![NuGet 패키지 관리자 창][img-servicenuget]
4. Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. 다음 필드 toohello hello 추가 **프로그램** 클래스입니다. 이전 섹션 hello 및 hello 대상 장치에서 만든 hello 허브에 대 한 IoT 허브 연결 문자열 hello로 hello 자리 표시자 값을 대체 합니다.
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. 다음 메서드 toohello hello 추가 **프로그램** 클래스입니다.  이 코드 가져옵니다 hello 장치로 이중 장치 및 출력 hello를 다시 부팅 하는 hello에 대 한 속성을 보고 합니다.
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. 다음 메서드 toohello hello 추가 **프로그램** 클래스입니다.  이 코드에서 직접 메서드를 사용 하 여 hello 장치 hello 다시 부팅을 시작 합니다.

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. 마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
8. Hello 솔루션을 빌드하십시오.

## <a name="create-a-simulated-device-app"></a>시뮬레이션된 장치 앱 만들기
이 섹션에서는 다음을 수행합니다.

* 응답 tooa 직접적인 방법 hello 클라우드에서 호출 하 여 Node.js 콘솔 응용 프로그램 만들기
* 시뮬레이션된 장치 재부팅 트리거
* 사용 하 여 hello 속성 tooenable 장치로 이중 쿼리 tooidentify 장치 및 마지막 재부팅 될 보고

1. **manageddevice**라는 빈 폴더를 새로 만듭니다.  Hello에 **manageddevice** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 package.json 파일을 만듭니다.  모든 hello 기본값을 적용 합니다.
   
    ```
    npm init
    ```
2. Hello에 명령 프롬프트에 **manageddevice** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iot 장치** 장치 SDK 패키지 및 **azure-iot-장치-mqtt**패키지:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. 텍스트 편집기를 사용 하 여 만드는 새 **dmpatterns_getstarted_device.js** hello에 대 한 파일 **manageddevice** 폴더입니다.
4. Hello 다음 '필요' hello hello 시작 부분에 설명 추가 **dmpatterns_getstarted_device.js** 파일:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. 추가 **connectionString** 변수 toocreate를 사용 하는 **클라이언트** 인스턴스.  장치 연결 문자열과 함께 hello 연결 문자열을 대체 합니다.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Hello 나오는 hello 장치에 따라 함수 tooimplement hello에 대 한 직접 메서드를 추가 합니다.
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. Hello 다음 tooopen hello 연결 tooyour IoT hub를 코드로 바꾸고 시작 hello 직접적인 방법 수신기를 추가 합니다.
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. 저장 후 닫기 hello **dmpatterns_getstarted_device.js** 파일입니다.
   
> [!NOTE]
> 단순 tookeep 항목을이 자습서는 어떠한 재시도 정책도 구현 하지 않습니다. 프로덕션 코드에서는 hello MSDN 문서에 설명 된 대로 다시 시도 정책 (예: 지 수 백오프)를 구현 해야 [일시적인 오류 처리][lnk-transient-faults]합니다.


## <a name="run-hello-apps"></a>Hello 앱 실행
준비 toorun hello 앱입니다.

1. Hello에 대 한 hello 명령 프롬프트 **manageddevice** 폴더를 다음 명령 toobegin hello 재부팅 직접적인 방법에 대 한 수신 대기 하는 hello를 실행 합니다.
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. 실행된 hello C# 콘솔 응용 프로그램 **TriggerReboot**합니다. 마우스 오른쪽 단추로 클릭 hello **TriggerReboot** 프로젝트를 **디버그**를 선택한 후 **새 인스턴스 시작**합니다.

3. Hello 장치 응답 toohello 직접적인 방법 hello 콘솔에 표시 됩니다.

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
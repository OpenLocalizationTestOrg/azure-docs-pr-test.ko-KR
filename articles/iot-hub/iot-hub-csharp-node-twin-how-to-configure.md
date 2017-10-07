---
title: "aaaUse Azure IoT Hub 장치로 이중 속성 (.NET/노드) | Microsoft Docs"
description: "Azure IoT Hub 장치 toouse 트윈스 어떻게 tooconfigure 장치 Node.js tooimplement 시뮬레이션 된 장치 응용 프로그램에 대 한 hello Azure IoT 장치 SDK 및.NET tooimplement 장치로 이중을 사용 하는 장치 구성을 수정 하는 서비스 응용 프로그램에 대 한 Azure IoT 서비스 SDK hello를 사용 합니다."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: elioda
ms.openlocfilehash: 840a1b2e45f4763131299577583aa89015dcdd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a>원하는 속성 tooconfigure 장치를 사용 하 여
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

이 자습서의 hello 끝 두 콘솔 응용 프로그램 해야 합니다.

* **SimulateDeviceConfiguration.js**, 원하는 구성 업데이트를 대기 하 고 시뮬레이트된 구성 업데이트 프로세스의 hello 상태를 보고 하는 시뮬레이션 된 장치 앱.
* **SetDesiredConfigurationAndQuery**, hello를 설정 하는.NET 백 엔드 앱, 원하는 장치에서 구성 및 쿼리 hello 업데이트 프로세스를 구성 합니다.

> [!NOTE]
> hello 문서 [Azure IoT Sdk] [ lnk-hub-sdks] toobuild를 사용할 수 있는, Azure IoT Sdk hello에 대 한 정보를 제공 장치와 백 엔드 응용 프로그램입니다.
> 
> 

toocomplete hello 다음 해야이 자습서:

* Visual Studio 2015 또는 Visual Studio 2017.
* Node.js 버전 0.10.x 이상
* 활성 Azure 계정. 계정이 없는 경우 몇 분 내에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.

Hello를 따른 경우 [장치 트윈스 시작] [ lnk-twin-tutorial] 자습서에서는 이미 있는 IoT hub 및 호출 하 여 장치 id **myDeviceId**합니다. 이 경우 toohello 건너뛸 수 있습니다 [만들기 hello 시뮬레이션 된 장치 앱] [ lnk-how-to-configure-createapp] 섹션.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a>Hello 시뮬레이션 된 장치 앱 만들기
Tooyour 허브를 연결 하는 Node.js 콘솔 앱을 만들면이 섹션에서는 **myDeviceId**원하는 구성 업데이트 될 때까지 대기 하 고 시뮬레이션 hello 구성 업데이트 프로세스에서 업데이트를 보고 합니다.

1. **simulatedeviceconfiguration**라는 빈 폴더를 새로 만듭니다. Hello에 **simulatedeviceconfiguration** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 새로운 package.json 파일을 만듭니다. 모든 hello 기본값을 적용 합니다.
   
    ```
    npm init
    ```
1. Hello에 명령 프롬프트에 **simulatedeviceconfiguration** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iot 장치** 및 **azure-iot-장치-mqtt**패키지:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. 텍스트 편집기를 사용 하 여 만드는 새 **SimulateDeviceConfiguration.js** hello에 대 한 파일 **simulatedeviceconfiguration** 폴더입니다.
1. 다음 코드 toohello hello 추가 **SimulateDeviceConfiguration.js** 파일을 찾아 hello 대체 **{장치 연결 문자열을 (를)** hello 장치 연결 문자열에서 복사한 경우 자리 표시자 있습니다 hello 만든 **myDeviceId** 장치 id가 없음:
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    hello **클라이언트** 개체 hello 장치에서 장치 트윈스와 모든 hello 메서드에 필요한 toointeract을 제공 합니다. 이 코드를 hello 초기화 **클라이언트** 개체를 검색에 대 한 장치로 이중 hello **myDeviceId**, 다음에 hello 업데이트에 대 한 처리기를 연결 하 고 *원하는 속성을*합니다. hello 처리기 있는지 확인 hello configIds 비교 하 여 실제 구성 변경 요청은 설정한 다음 hello 구성 변경을 시작 하는 메서드를 호출 합니다.
   
    간단한 hello 위해서이 코드에서는 하드 코드 된 기본 hello 초기 구성에 대 한 참고 합니다. 실제 앱은 아마도 로컬 저장소로부터 그 구성을 로드할 것입니다.
   
   > [!IMPORTANT]
   > 원하는 속성 변경 이벤트는 장치 연결 시 한 번만 내보내집니다. 작업을 수행 하기 전에 원하는 속성을 변경 되는 실제 hello 임을 toocheck 있는지 확인 합니다.
   > 
   > 
1. Hello hello 하기 전에 다음 추가 `client.open()` 호출:
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    hello **initConfigChange** 메서드 업데이트 hello 너무 hello 구성 사용 하 여 hello 로컬 장치로 이중 개체의 속성 업데이트 요청 및 집합 hello 상태 보고**보류 중인**, 다음 업데이트 hello hello 서비스에 장치로 이중 합니다. Hello 장치로 이중을 성공적으로 업데이트 한 후의 hello 실행을 종료 하는 장기 실행 프로세스를 시뮬레이션 **completeConfigChange**합니다. 이 메서드는 hello 로컬 보고 속성 너무 hello 상태 설정 업데이트**성공** 및 hello 제거 **pendingConfig** 개체입니다. 그런 다음 hello 장치로 이중 hello 서비스에 업데이트 합니다.
   
    Hello 속성 toobe만 수정 지정 하 여 속성이 업데이트 되는 보고 하는 toosave 대역폭 (라는 **패치** 코드 위의 hello에), hello 전체 문서를 교체 하는 대신 합니다.
   
   > [!NOTE]
   > 이 자습서는 동시 구성 업데이트에 대해 어떤 동작도 시뮬레이션하지 않습니다. 일부 구성 업데이트 프로세스 hello 업데이트 실행 되는 동안 대상 구성의 변경 내용 수 tooaccommodate 수 있습니다, 그리고 일부 tooqueue 고, 일부 수 거부 오류 조건과 함께 있을 수 있습니다. 특정 구성 프로세스에 대해 원하는 동작을 hello 고 hello 구성 변경 시작 하기 전에 hello 적절 한 논리를 추가 했는지 tooconsider를 확인 합니다.
   > 
   > 
1. Hello 장치 응용 프로그램을 실행 합니다.
   
        node SimulateDeviceConfiguration.js
   
    Hello 메시지를 확인 해야 `retrieved device twin`합니다. 실행 중인 hello 앱을 유지 합니다.

## <a name="create-hello-service-app"></a>Hello 서비스 앱 만들기
이 섹션에서는 만듭니다.NET 콘솔 응용 프로그램 업데이트 hello 해당 *원하는 속성을* 와 연결 된 장치로 이중 hello에 **myDeviceId** 새 원격 분석 구성 개체를 사용 합니다. 다음 hello IoT 허브에 저장 된 hello 장치 트윈스 쿼리하고 hello 차이 hello 원하는 및 보고 hello 장치의 구성을 표시 합니다.

1. Visual Studio에서 Visual C# Windows 클래식 데스크톱 프로젝트 toohello 현재 솔루션 hello를 사용 하 여 추가 **콘솔 응용 프로그램** 서식 파일 프로젝트. 이름 hello 프로젝트 **SetDesiredConfigurationAndQuery**합니다.
   
    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][img-createapp]
1. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **SetDesiredConfigurationAndQuery** 프로젝트를 마우스 클릭 **NuGet 패키지 관리...** .
1. Hello에 **NuGet 패키지 관리자** 창에서 **찾아보기**, 검색할 **microsoft.azure.devices**선택, **설치** tooinstall hello **Microsoft.Azure.Devices** 패키지 및 hello 사용 약관에 동의 합니다. 이 절차를 다운로드, 설치 하 고 참조 toohello 추가 [Azure IoT 서비스 SDK] [ lnk-nuget-service-sdk] NuGet 패키지 및 해당 종속성.
   
    ![NuGet 패키지 관리자 창][img-servicenuget]
1. Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. 다음 필드 toohello hello 추가 **프로그램** 클래스입니다. Hello hello 이전 섹션에서 만든 hello 허브에 대 한 IoT 허브 연결 문자열 hello 자리 표시자 값을 바꿉니다.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. 다음 메서드 toohello hello 추가 **프로그램** 클래스:
   
        static private async Task SetDesiredConfigurationAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch = new {
                    properties = new {
                        desired = new {
                            telemetryConfig = new {
                                configId = Guid.NewGuid().ToString(),
                                sendFrequency = "5m"
                            }
                        }
                    }
                };
   
            await registryManager.UpdateTwinAsync(twin.DeviceId, JsonConvert.SerializeObject(patch), twin.ETag);
            Console.WriteLine("Updated desired configuration");
   
            try
            {
                while (true)
                {
                    var query = registryManager.CreateQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'");
                    var results = await query.GetNextAsTwinAsync();
                    foreach (var result in results)
                    {
                        Console.WriteLine("Config report for: {0}", result.DeviceId);
                        Console.WriteLine("Desired telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Desired["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine("Reported telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Reported["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine();
                    }
                    Thread.Sleep(10000);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Exception: {ex.Message}");
            }
        }
   
    hello **레지스트리** 개체 hello 서비스에서 장치 트윈스와 모든 hello 메서드에 필요한 toointeract을 제공 합니다. 이 코드를 hello 초기화 **레지스트리** 개체를 검색에 대 한 장치로 이중 hello **myDeviceId**, 한 후 새 원격 분석 구성 개체를으로 원하는 속성을 업데이트 합니다.
    그 후 hello 장치 트윈스 10 초 마다 hello IoT 허브에 저장 된 쿼리 및 인쇄 hello 원하는 및 원격 분석 구성을 보고 합니다. Toohello 참조 [IoT Hub 쿼리 언어] [ lnk-query] toolearn toogenerate 서식 있는 모든 장치에서 보고 하는 방법입니다.
   
   > [!IMPORTANT]
   > 이 응용 프로그램은 설명 목적으로 10초 마다 IoT Hub를 쿼리합니다. 사용 하 여 많은 장치와 toodetect 변경 내용이 아니라 걸쳐 toogenerate 사용자 용 보고서를 쿼리합니다. 솔루션에 장치 이벤트의 실시간 알림이 필요한 경우 [쌍 알림][lnk-twin-notifications]을 사용합니다.
   > 
   > 
1. 마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. Hello 솔루션 탐색기를 열고 hello **설정 시작 프로젝트...**  hello 있는지를 확인 하 고 **동작** 에 대 한 **SetDesiredConfigurationAndQuery** 프로젝트는 **시작**합니다. Hello 솔루션을 빌드하십시오.
1. 와 **SimulateDeviceConfiguration.js** 에서 Visual Studio를 사용 하 여 hello.NET 응용 프로그램 실행, 실행 **F5** hello 보고 된 구성에서 변경 하면 볼 **성공** 너무**보류 중인** 너무**성공** 다시 hello 새 활성 대신 24 시간 동안 5 분의 빈도 전송 합니다.

 ![장치가 성공적으로 구성됨][img-deviceconfigured]
   
   > [!IMPORTANT]
   > hello 장치 보고서 작업 및 hello 쿼리 결과 사이 tooa 1 분 간의 지연이 있습니다. 이 매우 높은 대규모 tooenable hello 쿼리 인프라 toowork입니다. 단일 장치로 이중의 일관 된 뷰 tooretrieve hello를 사용 하 여 **getDeviceTwin** hello에 대 한 메서드 **레지스트리** 클래스입니다.
   > 
   > 

## <a name="next-steps"></a>다음 단계
이 자습서에서는으로 원하는 구성을 설정 하면 *원하는 속성을* hello 솔루션에서 백 엔드를 하 고 변경 하 고 보고 하는 hello 통해 해당 상태를 보고 multi-step 업데이트 프로세스를 시뮬레이션 하는 장치 앱 toodetect 작성 했습니다. 속성입니다.

사용 하 여 hello 리소스 toolearn을 어떻게 수행 하려면:

* hello 사용 하 여 장치에서 원격 분석 전송 [IoT 허브 시작] [ lnk-iothub-getstarted] 자습서
* 예약 또는 수행 큰 집합의 장치에 대 한 작업 참조 hello [일정 및 브로드캐스트 작업] [ lnk-schedule-jobs] 자습서입니다.
* 대화형으로 (예: 사용자 제어 응용 프로그램에서 팬)를 설정 하는 장치 hello로 제어 [직접 메서드를 사용 하 여] [ lnk-methods-tutorial] 자습서입니다.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-node-twin-how-to-configure/deviceconfigured.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-csharp-node-twin-how-to-configure.md#create-the-simulated-device-app

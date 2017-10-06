---
title: "aaaCustomizing 미리 솔루션 구성 | Microsoft Docs"
description: "Toocustomize hello Azure IoT Suite 미리 솔루션을 구성 하는 방법에 지침을 제공 합니다."
services: 
suite: iot-suite
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4653ae53-4110-4a10-bd6c-7dc034c293a8
ms.service: iot-suite
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 1a8573f5ac6ed944c44459df495446f15174d513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-a-preconfigured-solution"></a>미리 구성된 솔루션 사용자 지정

Azure IoT Suite hello와 함께 제공 되는 미리 구성 하는 hello 솔루션 hello hello suite 작업 함께 toodeliver 종단 간 솔루션 내에 서비스를 보여 줍니다. 시작점을 확장 하 고 특정 시나리오에 대 한 hello 솔루션을 사용자 지정할 수 있는 다양 한 위치에는 있습니다. hello 다음 섹션에서는 이러한 일반적인 사용자 지정 위치를 설명 합니다.

## <a name="find-hello-source-code"></a>Hello 소스 코드 찾기

hello 미리 구성 된 솔루션에 대 한 hello 소스 코드 리포지토리 다음 hello에 GitHub에서 제공 됩니다.

* 원격 모니터링: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)
* 예측 유지 관리: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)
* 연결된 팩터리: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)

미리 구성 하는 hello 솔루션에 대 한 hello 소스 코드에는 사용 되는 Azure IoT Suite를 사용 하 여 IoT 솔루션의 tooimplement hello 종단 간 기능 toodemonstrate hello 패턴과 사례 제공 됩니다. 방법에 대 한 자세한 정보를 찾을 수 toobuild hello GitHub 리포지토리에에서 hello 솔루션을 배포 하 고 있습니다.

## <a name="change-hello-preconfigured-rules"></a>변경 미리 구성 하는 hello 규칙

hello 원격 모니터링 솔루션에 포함 된 3 개의 [Azure 스트림 분석](https://azure.microsoft.com/services/stream-analytics/) toohandle 장치 정보, 원격 분석 및 hello 솔루션에 규칙 논리를 작업 합니다.

hello 세 스트림 분석 작업 하 고 해당 구문 hello에서 자세히 설명 되어 [솔루션 연습을 미리 구성 된 원격 모니터링](iot-suite-remote-monitoring-sample-walkthrough.md)합니다. 

이러한 작업 tooalter 논리를 hello 또는 특정 tooyour 시나리오 논리를 추가 하는 직접 편집할 수 있습니다. 찾을 수 있습니다 hello 스트림 분석 작업이 다음과 같습니다.

1. 너무 이동[Azure 포털](https://portal.azure.com)합니다.
2. 하면 IoT 솔루션 이름이 hello로 toohello 리소스 그룹을 이동 합니다. 
3. Toomodify 원하는 hello Azure 스트림 분석 작업을 선택 합니다. 
4. 선택 하 여 중지 hello 작업 **중지** hello 명령 집합에서. 
5. Hello, 쿼리, 입력과 출력을 편집 합니다.
   
    간단한 수정을 hello에 대 한 toochange hello 쿼리 **규칙** 작업 toouse는 **"<"** 대신는 **">"**합니다. hello 솔루션 포털에 여전히 표시 **">"** 규칙을 편집 하지만 hello 동작은 toohello 변경 작업을 기본 hello 인해 대칭 이동 하는 방법을 확인할 수 있습니다.
6. Hello 작업 시작

> [!NOTE]
> 원격 모니터링 대시보드 hello hello 작업 변경 hello 대시보드 toofail을 줄 수 있으므로 특정 데이터에 따라 달라 집니다.

## <a name="add-your-own-rules"></a>사용자 고유 규칙 추가

Toochanging hello 미리 Azure 스트림 분석 작업을 구성 하는 또한, hello Azure 포털 tooadd 새 작업을 사용 하거나 새 쿼리 tooexisting 작업을 추가할 수 있습니다.

## <a name="customize-devices"></a>장치 사용자 지정

Hello 가장 일반적인 확장 활동 중 하나를 장치 특정 tooyour 시나리오와 함께 작동 합니다. 장치를 사용하는 여러 방법이 있습니다. 이러한 방법에는 시뮬레이션 된 장치 toomatch 시나리오를 변경 하거나 hello를 사용 하 여 포함 [IoT 장치 SDK] [ IoT Device SDK] tooconnect 물리적 장치 toohello 솔루션입니다.

단계별 가이드 tooadding 장치에 대 한 참조 hello [Iot Suite 연결 장치](iot-suite-connecting-devices.md) 아티클과 hello [원격 C SDK 샘플 모니터링](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring)합니다. 이 샘플은 미리 구성 된 솔루션 모니터링 원격 hello로 디자인 된 toowork입니다.

### <a name="create-your-own-simulated-device"></a>고유한 시뮬레이션된 장치 만들기

Hello에 포함 된 [모니터링 솔루션 소스 코드 원격](https://github.com/Azure/azure-iot-remote-monitoring)는.NET 시뮬레이터. 이 시뮬레이터는 hello hello 솔루션의 일부로 toosend 다른 메타 데이터를 원격 분석, alter 및 toodifferent 명령 및 메서드에 응답 수를 프로 비전 하나입니다.

미리 구성 된 솔루션 모니터링 원격 hello에 미리 구성 된 시뮬레이터 hello 냉각기 장치 온도 및 습도 원격 분석입니다를 시뮬레이션 합니다. Hello에 hello 시뮬레이터를 수정할 수 있습니다 [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) 시기도 hello GitHub 리포지토리를 분기 했습니다.

### <a name="available-locations-for-simulated-devices"></a>시뮬레이션된 장치에 사용 가능한 위치

hello 기본 집합이 위치 시애틀/Redmond, Washington, 미국입니다. [SampleDeviceFactory.cs][lnk-sample-device-factory]에서 이러한 위치를 변경할 수 있습니다.

### <a name="add-a-desired-property-update-handler-toohello-simulator"></a>Toohello 시뮬레이터를 원하는 속성 업데이트 처리기를 추가 합니다.

Hello 솔루션 포털에서 장치에 대해 원하는 속성에 대 한 값을 설정할 수 있습니다. hello hello 장치 toohandle hello 속성 변경 요청의 필요한 hello 속성 값을 검색 하는 hello 장치 합니다. 속성 값 변경에 대 한 tooadd 지원을 원하는 속성을 통해 tooadd 처리기 toohello 시뮬레이터 해야 합니다.

hello에 대 한 처리기를 포함 하는 hello 시뮬레이터 **SetPointTemp** 및 **TelemetryInterval** 속성을 설정 하 여 업데이트할 수 있는 원하는 hello 솔루션 포털의 값입니다.

hello 다음 보여 주는 예제 hello에 대 한 hello 처리기 **SetPointTemp** hello에서 속성을 원하는 **CoolerDevice** 클래스:

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

이 메서드는 온도 보고서 hello 백 tooIoT 허브 보고 속성을 설정 하 여 변경 하는 hello 원격 분석 지점을 업데이트 합니다.

Hello 예제 앞에 다음 hello 패턴에 의해 사용자 고유의 속성에 대 한 고유의 처리기를 추가할 수 있습니다.

바인딩해야 hello 원하는 속성 toohello 처리기 hello 다음 hello에서 예제에에서 표시 된 대로 **CoolerDevice** 생성자:

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

**SetPointTempPropertyName**은 "Config.SetPointTemp"로 정의되는 상수입니다.

### <a name="add-support-for-a-new-method-toohello-simulator"></a>새 메서드 toohello 시뮬레이터에 대 한 지원 추가

새 항목에 대 한 hello 시뮬레이터 tooadd 지원 사용자 지정할 수 있습니다 [메서드 (직접)][lnk-direct-methods]합니다. 필요한 두 가지 주요 단계는 다음과 같습니다.

- hello 시뮬레이터 hello 메서드의 세부 정보를 사용 하 여 hello 미리 구성 된 솔루션의 hello IoT 허브에 알려야 합니다.
- hello 시뮬레이터 hello에서 호출 하는 경우 코드 toohandle hello 메서드 호출을 포함 해야 **장치 세부 정보** hello 솔루션 탐색기에서 또는 작업을 통해 패널입니다.

hello 원격 모니터링 미리 구성 된 솔루션에서는 *속성을 보고* tooIoT 허브 지원 되는 방법의 toosend 세부 정보입니다. hello 솔루션 백 엔드를 메서드 호출의 기록와 함께 각 장치에서 지 원하는 모든 hello 메서드의 목록을 유지 관리 합니다. 장치에 대 한이 정보를 볼 수 있으며 hello 솔루션 포털에서 메서드를 호출할 수 있습니다.

장치는 메서드를 지원 하도록 toonotify hello IoT hub를 hello 장치 hello 메서드 toohello의 세부 정보를 추가 해야 **SupportedMethods** hello의 노드 속성을 보고 합니다.

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

hello 메서드 시그니처에 형식에 따라 hello: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`합니다. 예를 들어 toospecify hello **InitiateFirmwareUpdate** 메서드 라는 문자열 매개 변수를 기대 **FwPackageURI**, 메서드 시그니처를 다음 hello를 사용 하 여:

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

지원 되는 매개 변수 형식의 목록에 대 한 참조 hello **CommandTypes** hello 인프라 프로젝트의 클래스.

메서드를 toodelete 너무 hello 메서드 시그니처를 설정`null` hello에 속성을 보고 합니다.

> [!NOTE]
> hello 솔루션 백 엔드 업데이트 지원 되는 방법에 대 한 정보를 받을 때는 *장치 정보* hello 장치에서 메시지입니다.

다음 코드 샘플을 hello hello **SampleDeviceFactory** hello 공통 클래스 프로젝트 표시 방법을 tooadd 방법 toohello 목록의 **SupportedMethods** hello 보고 hello 전송한 속성 장치:

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' toospecifiy hello URI of hello firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

이 코드 조각은 hello에 대 한 세부 정보 추가 **InitiateFirmwareUpdate** hello 솔루션 포털 hello에 대 한 세부 정보에 텍스트 toodisplay를 포함 하는 메서드 필수 메서드 매개 변수입니다.

hello 시뮬레이터 tooIoT 허브 hello 시뮬레이터 시작 될 때 지원 되는 메서드의 hello 목록을 비롯 한 보고 속성을 보냅니다.

지 원하는 각 방법에 대 한 처리기 toohello 시뮬레이터 코드를 추가 합니다. Hello hello 기존 처리기 나타나면 **CoolerDevice** hello Simulator.WebJob 프로젝트의 클래스. hello 다음 보여 주는 예제에 대 한 hello 처리기 **InitiateFirmwareUpdate** 메서드:

```csharp
public async Task<MethodResponse> OnInitiateFirmwareUpdate(MethodRequest methodRequest, object userContext)
{
    if (_deviceManagementTask != null && !_deviceManagementTask.IsCompleted)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "Device is busy"
        }, 409));
    }

    try
    {
        var operation = new FirmwareUpdate(methodRequest);
        _deviceManagementTask = operation.Run(Transport).ContinueWith(async task =>
        {
            // after firmware completed, we reset telemetry
            var telemetry = _telemetryController as ITelemetryWithTemperatureMeanValue;
            if (telemetry != null)
            {
                telemetry.TemperatureMeanValue = 34.5;
            }

            await UpdateReportedTemperatureMeanValue();
        });

        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "FirmwareUpdate accepted",
            Uri = operation.Uri
        }));
    }
    catch (Exception ex)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = ex.Message
        }, 400));
    }
}
```

메서드 처리기 이름은으로 시작 해야 `On` hello 메서드의 hello 이름이 차례로 나옵니다. hello **methodRequest** 매개 변수는 hello 솔루션 백 엔드에서 hello 메서드 호출으로 전달 된 매개 변수를 포함 합니다. hello 반환 값 형식 이어야 합니다 **작업&lt;MethodResponse&gt;**합니다. hello **BuildMethodResponse** 유틸리티 메서드를 사용 하면 hello 반환 값을 만들 수 있습니다.

Hello 메서드 처리기 내 하면 다음과 같은 작업을 수행할 수 있습니다.

- 비동기 작업을 시작합니다.
- Hello에서 원하는 속성을 검색할 *장치로 이중* IoT 허브에서 합니다.
- Hello를 사용 하 여 단일 보고 속성을 업데이트 **SetReportedPropertyAsync** hello에 대 한 메서드 **CoolerDevice** 클래스입니다.
- 만들어서 여러 보고 속성을 업데이트 한 **TwinCollection** 인스턴스와 호출 hello **Transport.UpdateReportedPropertiesAsync** 메서드.

hello 이전 펌웨어 업데이트 수행 하는 예제 단계를 수행 하는 hello:

- 검사 hello 장치 수 tooaccept hello 펌웨어 업데이트 요청입니다.
- 비동기적으로 hello 펌웨어 업데이트 작업을 시작 하 고 hello 작업이 완료 되 면 hello 원격 분석을 다시 설정 합니다.
- 즉시 반환 hello "FirmwareUpdate 허용" hello 장치에 의해 메시지 tooindicate hello 요청이 수락 되었습니다.

### <a name="build-and-use-your-own-physical-device"></a>고유한 (물리적) 장치 빌드 및 사용

hello [Azure IoT Sdk](https://github.com/Azure/azure-iot-sdks) IoT 솔루션으로 다양 한 장치 유형 (언어 및 운영 체제)를 연결 하기 위한 라이브러리를 제공 합니다.

## <a name="modify-dashboard-limits"></a>대시보드 제한 수정

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a>대시보드 드롭다운에 표시되는 장치 수

hello 기본값은 200입니다. [DashboardController.cs][lnk-dashboard-controller]에서 이 수를 변경할 수 있습니다.

### <a name="number-of-pins-toodisplay-in-bing-map-control"></a>Bing 지도 컨트롤에서 핀 toodisplay 개수

hello 기본값은 200입니다. [TelemetryApiController.cs][lnk-telemetry-api-controller-01]에서 이 수를 변경할 수 있습니다.

### <a name="time-period-of-telemetry-graph"></a>원격 분석 그래프의 시간 간격

hello 기본값은 10 분입니다. [TelmetryApiController.cs][lnk-telemetry-api-controller-02]에서 이 값을 변경할 수 있습니다.

## <a name="manually-set-up-application-roles"></a>수동으로 응용 프로그램 역할 설정

hello 다음 절차에서는 방법을 tooadd **Admin** 및 **ReadOnly** 응용 프로그램 역할 tooa 미리 솔루션을 구성 합니다. Hello azureiotsuite.com 사이트에서 이미 프로 비전 하는 미리 구성 된 솔루션에 hello 포함 **관리자** 및 **ReadOnly** 역할입니다.

멤버의 hello **ReadOnly** 역할 hello 대시보드와 hello 장치 목록을 볼 수 있지만 tooadd 장치, 장치 특성 변경, 또는 송신 명령을 사용할 수 없습니다.  멤버의 hello **Admin** 역할 hello 솔루션에 대 한 모든 권한을 tooall hello 기능 있는 합니다.

1. Toohello 이동 [Azure 클래식 포털][lnk-classic-portal]합니다.
2. **Active Directory**를 선택합니다.
3. 솔루션을 프로 비전 할 때 사용한 hello AAD 테 넌 트의 hello 이름을 클릭 합니다.
4. **응용 프로그램**을 클릭합니다.
5. 미리 구성 된 솔루션 이름과 일치 하는 hello 응용 프로그램의 hello 이름을 클릭 합니다. 응용 프로그램 hello 목록에 보이지 않으면 경우 선택 **회사가 보유 한 응용 프로그램** hello에 **표시** 드롭다운을 클릭 하 고 확인 표시를 hello 합니다.
6. Hello hello 페이지의 아래쪽에 있는 클릭 **매니페스트 관리** 차례로 **매니페스트 다운로드**합니다.
7. 이 절차는.json 파일 tooyour 로컬 컴퓨터를 다운로드합니다. 이 파일을 편집할 수 있도록 원하는 텍스트 편집기에서 엽니다.
8. Hello.json 파일의 hello 세 번째 줄에 다음을 확인할 수 있습니다.

   ```json
   "appRoles" : [],
   ```
   이 줄을 코드 다음 hello로 바꿉니다.

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access toohello application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access toodevice information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. (Hello 기존 파일을 덮어쓸 수) hello 업데이트.json 파일을 저장 합니다.
10. Hello hello hello 페이지 맨 아래에 Azure 클래식 포털에서에서 선택 **매니페스트 관리** 다음 **매니페스트 업로드** tooupload hello.json 파일 hello 이전 단계에서 저장 합니다.
11. 이제 hello이 추가 되어 **Admin** 및 **ReadOnly** tooyour 응용 프로그램 역할입니다.
12. 디렉터리에 이러한 역할 tooa 사용자 중 하나는 tooassign 참조 [hello azureiotsuite.com 사이트에 대 한 권한을][lnk-permissions]합니다.

## <a name="feedback"></a>사용자 의견

이 문서에서 다루는 toosee 원하는 사용자 지정 있습니까? 기능 제안 너무 추가[사용자 음성](https://feedback.azure.com/forums/321918-azure-iot), 또는이 문서에서 설명 합니다. 

## <a name="next-steps"></a>다음 단계

toolearn hello 미리 구성 된 솔루션을 사용자 지정 하기 위한 hello 옵션에 대해 자세히 알아보려면

* [논리 앱 tooyour Azure IoT Suite 원격 모니터링 미리 구성 된 솔루션에 연결][lnk-logicapp]
* [동적 원격 분석을 사용 하 여 원격 미리 구성 된 솔루션을 모니터링 하는 hello로][lnk-dynamic]
* [Hello 원격 모니터링 미리 구성 된 솔루션에서에서 장치 정보 메타 데이터][lnk-devinfo]
* [Hello OPC UA는 서버에서 데이터를 표시 팩터리 솔루션에 연결 하는 방법을 사용자 지정][lnk-cf-customize]

[lnk-logicapp]: iot-suite-logic-apps-tutorial.md
[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[IoT Device SDK]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-permissions]: iot-suite-permissions.md
[lnk-dashboard-controller]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/Controllers/DashboardController.cs#L27
[lnk-telemetry-api-controller-01]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L27
[lnk-telemetry-api-controller-02]: https://github.com/Azure/azure-iot-remote-monitoring/blob/e7003339f73e21d3930f71ceba1e74fb5c0d9ea0/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L25 
[lnk-sample-device-factory]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Common/Factory/SampleDeviceFactory.cs#L40
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-cf-customize]: iot-suite-connected-factory-customize.md
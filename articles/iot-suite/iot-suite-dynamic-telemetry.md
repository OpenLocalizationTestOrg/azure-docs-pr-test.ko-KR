---
title: "aaaUse 동적 원격 분석 | Microsoft Docs"
description: "이 자습서 toolearn 따라 hello Azure IoT Suite 원격 모니터링 toouse 동적 원격 분석 미리 솔루션을 구성 하는 방법입니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 06cb2a370b67b4950efdfa4c7d906ac92106f4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-dynamic-telemetry-with-hello-remote-monitoring-preconfigured-solution"></a>동적 원격 분석을 사용 하 여 원격 미리 구성 된 솔루션을 모니터링 하는 hello로

동적 원격 분석 하면 toovisualize 모든 원격 분석 전송 toohello를 원격 모니터링 미리 구성 된 솔루션을 수 있습니다. 미리 구성 하는 hello 솔루션으로 배포 하는 hello 시뮬레이션 된 장치는 hello 대시보드에서 시각화할 수 있는 온도 및 습도 원격 분석을 전송 합니다. 기존 시뮬레이션 된 장치를 사용자 지정 하면 새 시뮬레이션 된 장치를 만들거나 물리적 장치 toohello 미리 구성 된 솔루션 hello 외부 온도, RPM을 또는 windspeed 같은 다른 원격 분석 값을 보낼 수 있습니다. 그런 다음 hello 대시보드에서 추가 원격 분석을 시각화할 수 있습니다.

이 자습서에서는 tooexperiment 된 동적 원격 분석을 쉽게 수정할 수 있는 간단한 Node.js 시뮬레이션 된 장치를 사용 합니다.

toocomplete이이 자습서에서는 해야 합니다.

* 활성 Azure 구독. 계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 평가판][lnk_free_trial]을 참조하세요.
* [Node.js][lnk-node] 버전 0.12.x 이상.

Windows나 Linux 등의 Node.js를 설치할 수 있는 모든 운영 체제에서 이 자습서를 완료할 수 있습니다.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a>원격 분석 형식 추가

hello 다음 단계는 새 값 집합을 사용 하 여 hello Node.js 시뮬레이션 된 장치에 의해 생성 된 tooreplace hello 원격 분석입니다.

1. 입력 하 여 중지 hello Node.js 시뮬레이션 된 장치 **Ctrl + C** 명령 프롬프트 또는 셸 합니다.
2. Hello remote_monitoring.js 파일에 hello 기존 온도, 습도, 및 외부 온도 원격 분석에 대 한 hello 기본 데이터 값을 볼 수 있습니다. 다음과 같이 **rpm** 의 새 기본 데이터 값을 추가합니다.

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. hello를 사용 하는 hello Node.js 시뮬레이션 된 장치가 **generateRandomIncrement** 함수 hello remote_monitoring.js 파일 tooadd 임의 증가 toohello에에서 기본 데이터 값입니다. Hello 불규칙화 **rpm** hello 기존 불규칙화 후 다음과 같은 코드 줄을 추가 하 여 값:

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. Hello 새 rpm 값 toohello JSON 페이로드 hello 장치 보냅니다 tooIoT 허브를 추가 합니다.

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. 다음 명령을 hello를 사용 하 여 hello Node.js 시뮬레이션 된 장치를 실행 합니다.

    `node remote_monitoring.js`

6. Hello 새 RPM 원격 분석 유형 hello 대시보드에 hello 차트에 표시 하는 준수 하십시오.

![RPM toohello 대시보드를 추가 합니다.][image3]

> [!NOTE]
> Toodisable 필요 하 고 hello Node.js 장치 hello에 사용 하도록 설정 될 수 있습니다 **장치** hello 대시보드 toosee hello 변경에서 즉시 페이지.

## <a name="customize-hello-dashboard-display"></a>Hello 대시보드 표시를 사용자 지정

hello **장치 정보** 메시지 메타 데이터를 포함할 수 있습니다 hello 원격 분석에 대 한 hello 장치 tooIoT 허브를 보낼 수 있습니다. 이 메타 데이터는 hello 원격 분석 유형을 전송 하는 hello 장치를 지정할 수 있습니다. Hello 수정 **deviceMetaData** hello remote_monitoring.js 파일 tooinclude에 값을 **원격 분석** hello 다음 정의 **명령을** 정의 합니다. hello 만드는 코드는 hello **명령을** 정의 (있는지 tooadd 수는 `,` hello 후 **명령을** 정의):

```nodejs
'Commands': [{
  'Name': 'SetTemperature',
  'Parameters': [{
    'Name': 'Temperature',
    'Type': 'double'
  }]
},
{
  'Name': 'SetHumidity',
  'Parameters': [{
    'Name': 'Humidity',
    'Type': 'double'
  }]
}],
'Telemetry': [{
  'Name': 'Temperature',
  'Type': 'double'
},
{
  'Name': 'Humidity',
  'Type': 'double'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double'
}]
```

> [!NOTE]
> hello 원격 모니터링 솔루션 hello 원격 분석 스트림의 데이터를 대/소문자 구분 일치 toocompare hello 메타 데이터 정의 사용합니다.


추가 **원격 분석** 처럼 hello 위의 코드 조각 hello 대시보드 hello 방식은 변경 되지 않습니다. 그러나 hello 메타 데이터도 포함 될 수 있습니다는 **DisplayName** hello 대시보드에 toocustomize hello 표시 특성입니다. 업데이트 hello **원격 분석** hello 다음 코드 조각에에서 표시 된 대로 메타 데이터 정의:

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double',
  'DisplayName': 'Outdoor Temperature (C*)'
}
]
```

hello 다음 스크린샷은이 변경 hello 대시보드에서 hello 차트 범례를 수정 하는 방법:

![Hello 차트 범례를 사용자 지정][image4]

> [!NOTE]
> Toodisable 필요 하 고 hello Node.js 장치 hello에 사용 하도록 설정 될 수 있습니다 **장치** hello 대시보드 toosee hello 변경에서 즉시 페이지.

## <a name="filter-hello-telemetry-types"></a>Hello 원격 분석 유형을 필터링합니다

기본적으로 hello 대시보드에서 hello 차트 hello 원격 분석 스트림의 모든 데이터 계열을 나타냅니다. Hello를 사용할 수 있습니다 **장치 정보** 메타 데이터 toosuppress hello hello 차트에서 특정 원격 분석 유형 표시 합니다. 

toomake hello 차트만 온도 및 습도 원격 분석 표시, 생략 **ExternalTemperature** hello에서 **장치 정보** **원격 분석** 다음과 같은 메타 데이터:

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
//{
//  'Name': 'ExternalTemperature',
//  'Type': 'double',
//  'DisplayName': 'Outdoor Temperature (C*)'
//}
]
```

hello **옥외 온도** hello 차트에 더 이상 표시 합니다.

![Hello 대시보드에서 필터 hello 원격 분석][image5]

이 변경 내용을 hello 차트 표시를만 영향을 줍니다. hello **ExternalTemperature** 데이터 값도 저장 되 고 모든 백 엔드 처리에 사용할 수 있도록 합니다.

> [!NOTE]
> Toodisable 필요 하 고 hello Node.js 장치 hello에 사용 하도록 설정 될 수 있습니다 **장치** hello 대시보드 toosee hello 변경에서 즉시 페이지.

## <a name="handle-errors"></a>오류 처리

Hello 차트에 데이터 스트림 toodisplay에 대 한 해당 **형식** hello에 **장치 정보** 메타 데이터에는 hello 원격 분석 값의 hello 데이터 형식과 일치 해야 합니다. 예를 들어 hello 메타 데이터 지정 해당 hello **형식** 데이터는 습도 **int** 및 **double** hello 습도 원격 분석에는 다음 hello 원격 분석 스트림에 있는 hello 차트에 표시 되지 않습니다. 그러나 hello **습도** 값은 여전히 저장 하 고 모든 백 엔드 처리에 사용할 수 있도록 합니다.

## <a name="next-steps"></a>다음 단계

이제 살펴보았으므로 어떻게 toouse 동적 원격 분석 학습할 수 있는 장치 정보를 사용 하 여 hello 미리 솔루션을 구성 하는 방법에 대 한 자세한: [솔루션을 미리 구성 된 장치 정보 메타 데이터에서 원격 모니터링 hello] [ lnk-devinfo].

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org

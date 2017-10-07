---
title: "C-직렬 변환기에 대 한 IoT 장치 aaaAzure SDK | Microsoft Docs"
description: "어떻게 toouse hello Serializer 라이브러리 C toocreate 장치 앱에 대 한 hello Azure IoT 장치 SDK에서에서 통신 하는 IoT 허브를 사용 합니다."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: defbed34-de73-429c-8592-cd863a38e4dd
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: c5776e9b50ffea71df96cb2d342ea2fc045f5a0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a>C용 Azure IoT 장치 SDK - 직렬 변환기에 대한 자세한 정보
hello [먼저 문서](iot-hub-device-sdk-c-intro.md) 이 도입 시리즈 hello에 **C에 대 한 Azure IoT 장치 SDK**. hello 다음 기사 hello의 더 자세한 설명을 제공 [ **IoTHubClient** ](iot-hub-device-sdk-c-iothubclient.md). 이 문서 나머지 구성 요소는 hello의 더 자세한 설명을 제공 하 여 hello SDK의 적용 범위 완료: hello **serializer** 라이브러리입니다.

방법을 설명 하는 hello 소개 문서 toouse hello **serializer** 라이브러리 toosend 이벤트 tooand IoT 허브에서 메시지를 수신 합니다. 이 문서의 내용을 확장 하였습니다 그 토론 방법에 대 한 자세한 설명은 제공 하 여 toomodel hello 사용 하 여 데이터 **serializer** 매크로 언어입니다. hello 문서 라이브러리 hello 메시지를 serialize 하는 방법에 대 한 자세한 내용은 포함 되어 (및 경우에 따라 제어 하는 방법을 hello serialization 동작). 일부 매개 변수를 수정할 수 있습니다 사용자가 만드는 hello 모델의 hello 크기를 결정 하는 설명 하겠습니다.

마지막으로, hello 문서 다시 메시지 및 속성 처리와 같은 이전 문서에서 다루는 몇 가지 항목을 검토 합니다. 살펴보겠습니다에서 이러한 기능이 작동 하는 대로 hello hello를 사용 하 여 동일한 **serializer** 라이브러리 hello와 마찬가지로 **IoTHubClient** 라이브러리입니다.

이 문서에 설명 된 모든 내용을 기반으로 hello **serializer** SDK 샘플입니다. Toofollow을 따라 하려는 경우 참조 hello **simplesample\_amqp** 및 **simplesample\_http** C. 용 hello Azure IoT 장치 SDK에에서 포함 된 응용 프로그램

Hello를 찾을 수 있습니다 [ **C에 대 한 Azure IoT 장치 SDK** ](https://github.com/Azure/azure-iot-sdk-c) hello에 hello API의 GitHub 리포지토리 및 뷰 세부 정보 [C API 참조](https://azure.github.io/azure-iot-sdk-c/index.html)합니다.

## <a name="hello-modeling-language"></a>hello 모델링 언어
hello [소개 문서](iot-hub-device-sdk-c-intro.md) 이 도입 시리즈 hello에 **C에 대 한 Azure IoT 장치 SDK** 모델링 언어 hello에서 제공 하는 hello 예제의 통해 **simplesample\_amqp**  응용 프로그램:

```
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(double, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

볼 수 있듯이 hello 모델링 언어는 C 매크로 기반으로 합니다. 항상 **BEGIN\_NAMESPACE**로 사용자 정의를 시작하고 **END\_NAMESPACE**로 끝냅니다. 일반적인 tooname hello 또는 네임 스페이스 귀사에 대 한,이 예제에서 작업 하는 hello 프로젝트와 같이 것 합니다.

Hello 네임 스페이스 내 항목의 적합 한는 모델 정의입니다. 이 경우 풍력계에 대한 단일 모델이 있습니다. 다시 한 번, 아무것도 hello 모델을 이름을 지정할 수 있지만 라는 일반적으로 hello 장치 또는 데이터의 종류에 대 한 IoT Hub와 tooexchange 원하는 합니다.  

모델 정의 포함 하면 수신 tooIoT 허브 hello 이벤트의 (hello *데이터*) hello 메시지 IoT 허브에서 받을 수 뿐만 아니라 (hello *동작*). 형식과 이름을; 이벤트에는 hello 예제에서 볼 수 있습니다, 작업 이름 및 선택적 매개 변수 (형식으로 각각) 해야 합니다.

이 샘플에서 설명 하지 않음 무엇은 hello SDK에서 지 원하는 추가 데이터 형식입니다. 다음에 설명합니다.

> [!NOTE]
> IoT Hub tooit으로 전송 하는 한 장치 toohello 데이터 참조 *이벤트*, 모델링 언어 hello tooit으로 참조 하는 반면, *데이터* (사용 하 여 정의 **WITH_DATA**). 마찬가지로, IoT Hub 참조 toohello 보내는 데이터를로 toodevices *메시지*, 모델링 언어 hello tooit으로 참조 하는 반면, *동작* (사용 하 여 정의 **WITH_ACTION**). 이 문서에서는 이러한 용어가 같은 의미로 사용될 수 있습니다.
> 
> 

### <a name="supported-data-types"></a>지원되는 데이터 원본
데이터 형식은 다음 hello는 hello를 사용 하 여 만든 모델에서 지원 **serializer** 라이브러리:

| 형식 | 설명 |
| --- | --- |
| double |배정밀도 부동 소수점 숫자 |
| int |32비트 정수 |
| float |단정밀도 부동 소수점 숫자 |
| long |정수(Long) |
| int8\_t |8비트 정수 |
| int16\_t |16비트 정수 |
| int32\_t |32비트 정수 |
| int64\_t |64비트 정수 |
| bool |부울 |
| ascii\_char\_ptr |ASCII 문자열 |
| EDM\_DATE\_TIME\_OFFSET |날짜 시간 오프셋 |
| EDM\_GUID |GUID |
| EDM\_BINARY |binary |
| DECLARE\_STRUCT |복합 데이터 형식 |

Hello 마지막 데이터 형식과 시작 하겠습니다. hello **DECLARE\_구조체** 있습니다 hello의 그룹인 toodefine 복합 데이터 형식을 다른 기본 형식입니다. 이러한 그룹화는 다음과 같은 모델 toodefine 수 있습니다:

```
DECLARE_STRUCT(TestType,
double, aDouble,
int, aInt,
float, aFloat,
long, aLong,
int8_t, aInt8,
uint8_t, auInt8,
int16_t, aInt16,
int32_t, aInt32,
int64_t, aInt64,
bool, aBool,
ascii_char_ptr, aAsciiCharPtr,
EDM_DATE_TIME_OFFSET, aDateTimeOffset,
EDM_GUID, aGuid,
EDM_BINARY, aBinary
);

DECLARE_MODEL(TestModel,
WITH_DATA(TestType, Test)
);
```

이 모델은 **TestType**형식의 단일 데이터 이벤트를 포함합니다. **TestType** hello hello에서 지원 되는 기본 형식 전체적으로 보여 주는 여러 멤버를 포함 하는 복합 유형 **serializer** 모델링 언어입니다.

이와 같은 모델, 코드 toosend 데이터 tooIoT 다음과 같이 표시 되는 허브를 작성할 수 있습니다.

```
TestModel* testModel = CREATE_MODEL_INSTANCE(MyThermostat, TestModel);

testModel->Test.aDouble = 1.1;
testModel->Test.aInt = 2;
testModel->Test.aFloat = 3.0f;
testModel->Test.aLong = 4;
testModel->Test.aInt8 = 5;
testModel->Test.auInt8 = 6;
testModel->Test.aInt16 = 7;
testModel->Test.aInt32 = 8;
testModel->Test.aInt64 = 9;
testModel->Test.aBool = true;
testModel->Test.aAsciiCharPtr = "ascii string 1";

time_t now;
time(&now);
testModel->Test.aDateTimeOffset = GetDateTimeOffset(now);

EDM_GUID guid = { { 0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0A, 0x0B, 0x0C, 0x0D, 0x0E, 0x0F } };
testModel->Test.aGuid = guid;

unsigned char binaryArray[3] = { 0x01, 0x02, 0x03 };
EDM_BINARY binaryData = { sizeof(binaryArray), &binaryArray };
testModel->Test.aBinary = binaryData;

SendAsync(iotHubClientHandle, (const void*)&(testModel->Test));
```

기본적으로,의 hello는 값 tooevery 멤버를 지정 하는 것 **테스트** 구조와 다음 호출 **SendAsync** toosend hello **테스트** 데이터 이벤트 toohello 클라우드입니다. **SendAsync** 함수는 단일 데이터 이벤트 tooIoT 허브 전송 하는 도우미 함수:

```
void SendAsync(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const void *dataEvent)
{
    unsigned char* destination;
    size_t destinationSize;
    if (SERIALIZE(&destination, &destinationSize, *(const unsigned char*)dataEvent) ==
    {
        // null terminate hello string
        char* destinationAsString = (char*)malloc(destinationSize + 1);
        if (destinationAsString != NULL)
        {
            memcpy(destinationAsString, destination, destinationSize);
            destinationAsString[destinationSize] = '\0';
            IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromString(destinationAsString);
            if (messageHandle != NULL)
            {
                IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)0);

                IoTHubMessage_Destroy(messageHandle);
            }
            free(destinationAsString);
        }
        free(destination);
    }
}
```

이 함수는 데이터 이벤트를 지정 하는 hello 또는 그 반대로 serialize 하 고 tooIoT 허브 보냅니다를 사용 하 여 **IoTHubClient\_SendEventAsync**합니다. 이 동일한 코드 이전 문서에서 설명 하는 hello (**SendAsync** 을 편리 하 게 함수로 hello 논리를 캡슐화).

Hello 이전 코드에서 사용 되는 한 도우미 함수는 **GetDateTimeOffset**합니다. 이 함수 형식의 값에 지정 된 시간 hello 변환 **EDM\_날짜\_시간\_오프셋**:

```
EDM_DATE_TIME_OFFSET GetDateTimeOffset(time_t time)
{
    struct tm newTime;
    gmtime_s(&newTime, &time);
    EDM_DATE_TIME_OFFSET dateTimeOffset;
    dateTimeOffset.dateTime = newTime;
    dateTimeOffset.fractionalSecond = 0;
    dateTimeOffset.hasFractionalSecond = 0;
    dateTimeOffset.hasTimeZone = 0;
    dateTimeOffset.timeZoneHour = 0;
    dateTimeOffset.timeZoneMinute = 0;
    return dateTimeOffset;
}
```

이 코드를 실행 하는 경우 메시지의 뒤에 hello tooIoT 허브 전송 됩니다.

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

Hello serialization hello 형식인 hello에 의해 생성 된 JSON은 **serializer** 라이브러리입니다. 또한 hello의 각 멤버는 serialize 된 JSON 개체 일치 hello의 hello 멤버 **TestType** 예제의 모델에 정의 되어 있습니다. hello 값도 일치 hello 코드에 사용 합니다. 그러나 hello 이진 데이터가 base64 인코딩 인지를 확인: "AQID"의 base64 인코딩입니다 hello은 {0x01, 0x02, 0x03}.

이 예제는 hello를 사용 하 여 활용 하는 hello **serializer** 라이브러리-수 있도록 toosend JSON toohello 클라우드 응용 프로그램의 serialization을 다루는 tooexplicitly 필요 없이 합니다. 이제 다 tooworry에 대 한을 설정의 hello hello 값 데이터 이벤트 예제의 모델 및 해당 이벤트 toohello 클라우드 단순 Api toosend를 호출한 다음 합니다.

이 정보를 통해 지원 되는 데이터 형식, 복합 형식 (다른 복합 형식 내에서 복합 형식을 포함도 수)를 포함 하 여 hello 범위를 포함 하는 모델을 정의할 수 있습니다. 하지만 생성 된 JSON 직렬화 그 hello에서 위의 예제는 중요 한 점은를 표시 합니다. *어떻게* hello 사용 하 여 데이터를 받으실 **serializer** 라이브러리 정확 하 게 hello JSON 형성 되는 방식을 결정 합니다. 이러한 특별한 내용은 다음에 다루겠습니다.

## <a name="more-about-serialization"></a>직렬화에 대한 자세한 정보
hello 이전 섹션 강조 예제 hello에 의해 생성 된 hello 출력 **serializer** 라이브러리입니다. 이 섹션에서는 hello serialization Api를 사용 하 여 해당 동작을 제어 하는 방법 및 hello 라이브러리에서 데이터를 직렬화 하는 방법을 설명 합니다.

Serialization 중에 tooadvance hello 토론 순서에서는 서머 스 탯을 기반으로 새 모델와 파악 합니다. 첫째, 몇 가지 배경 정보를 제공 하겠습니다 hello 시나리오에 tooaddress는 중입니다.

온도 및 습도 측정 하는 자동 온도 조절기 toomodel 주시기 바랍니다. 각 데이터 조각 toobe 다르게 tooIoT 허브 전송 하려고 합니다. 기본적으로 hello 자동 온도 조절기 ingresses 온도 이벤트 2 분 마다 한 번씩; 습도 이벤트는 15 분 마다 한 번씩 ingressed. 이 이벤트 중 하나 이면 ingressed hello 시간 해당 hello 해당 온도 보여 주는 타임 스탬프를 포함 해야 합니다 또는 습도 측정 되었습니다.

이 시나리오를 매개 변수로 받아 보여 드립니다 두 가지 방법으로 toomodel hello 데이터 및 모델링에 hello에 직렬화 된 출력 hello 효과 설명 합니다.

### <a name="model-1"></a>모델 1
Hello 첫 번째 모델의 버전 지원 hello 이전 시나리오는 다음과 같습니다.

```
BEGIN_NAMESPACE(Contoso);

DECLARE_STRUCT(TemperatureEvent,
int, Temperature,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_STRUCT(HumidityEvent,
int, Humidity,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureEvent, Temperature),
WITH_DATA(HumidityEvent, Humidity)
);

END_NAMESPACE(Contoso);
```

해당 hello 모델 두 개 데이터 이벤트를 포함 하는 참고: **온도** 및 **습도**합니다. 이전 예제에서와 달리 hello 유형의 각 이벤트는 사용 하 여 정의 하는 구조 **DECLARE\_구조체**합니다. **TemperatureEvent**는 온도 측정 및 타임스탬프를 포함하고 **HumidityEvent**는 습도 측정 및 타임스탬프를 포함합니다. 이 모델 위에 설명 된 hello 시나리오에 대 한 자연 스러운 방법 toomodel hello 데이터 목록 있습니다. 이벤트 toohello 클라우드 म 보내면 온도/타임 스탬프 또는 습도/타임 스탬프 쌍 하거나 보내 드립니다.

Hello 다음과 같은 코드를 사용 하는 온도 이벤트 toohello 클라우드를 보내 드립니다.

```
time_t now;
time(&now);
thermostat->Temperature.Temperature = 75;
thermostat->Temperature.Time = GetDateTimeOffset(now);

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

온도 및 습도 hello 샘플 코드에서에 하드 코드 된 값을 사용 하지만 하에서는 실제로 읽어 들이는 이러한 값 hello 해당 센서 hello 자동 온도 조절기를 샘플링 하 여 가정해 보세요. 합니다 했습니다.

위의 hello 코드 hello를 사용 하 여 **GetDateTimeOffset** 이전에 도입 된 도우미입니다. 지우기 이상 될의 이유로이 코드 hello를 직렬화 하 고 작업을 hello 이벤트를 보내는 명시적으로 구분 합니다. hello 이전 코드를 버퍼에 hello 온도 이벤트를 serialize합니다. 그런 다음 **sendMessage** 도우미 함수 (에 포함 된 **simplesample\_amqp**) 보냅니다 hello tooIoT 이벤트 허브는:

```
static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle != NULL)
    {
        IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId);

        IoTHubMessage_Destroy(messageHandle);
    }
    free((void*)buffer);
}
```

이 코드는 hello의 하위 집합 **SendAsync** 있으므로 않습니다 위로 다시 여기 hello 이전 섹션에서 설명 하는 도우미입니다.

Hello 이전 코드 toosend hello 온도 이벤트를 실행 하면이 serialize 된 형태의 hello 이벤트 허브 tooIoT 전송 됩니다.

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

**TemperatureEvent** 형식의 온도를 전송하고 해당 구조체에는 **Temperature** 및 **Time** 멤버가 포함됩니다. 이 직접 hello serialize 된 데이터에 반영 됩니다.

마찬가지로 이 코드로 습도 이벤트도 전송할 수 있습니다.

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

serialize 된 hello 양식 tooIoT 허브 전송 다음과 같이 나타납니다.

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

역시, 예상대로 입니다.

이 모델로 추가 이벤트를 어떻게 쉽게 추가할 수 있는지 생각해볼 수 있습니다. 사용 하 여 더 많은 구조체를 정의 **DECLARE\_구조체**를 사용 하 여 hello 모델에 hello 해당 이벤트를 포함 하 고 **WITH\_데이터**합니다.

이제 hello 포함 되도록 hello 모델을 수정 해 보겠습니다 동일한 데이터 하지만 서로 다른 구조를 포함 합니다.

### <a name="model-2"></a>모델 2
위의이 대체 모델 toohello 하나를 고려 합니다.

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

이 경우 hello 제거 했다고 해 **DECLARE\_구조체** 매크로 및 모델링 언어 hello 단순 형식을 사용 하 여이 시나리오에서 hello 데이터 항목 정의 하기만 하면 됩니다.

Hello 순간에 대 한 hello 보겠습니다 무시 **시간** 이벤트입니다. 와 별개로 같습니다 hello 코드 tooingress **온도**:

```
time_t now;
time(&now);
thermostat->Temperature = 75;

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

이 코드는 hello 다음 직렬화 tooIoT 이벤트 허브를 보냅니다.

```
{"Temperature":75}
```

고 hello 습도 이벤트 보내기 위한 hello 코드는 다음과 같이 표시 됩니다.

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

이 코드에서는이 tooIoT 허브를 보냅니다.

```
{"Humidity":45}
```

지금까지 특별한 사항은 없습니다. 이제 hello SERIALIZE 매크로 사용 하는 방법을 변경 해보겠습니다.

hello **SERIALIZE** 매크로 인수로 여러 데이터 이벤트 걸릴 수 있습니다. 이렇게 하면 수 tooserialize hello **온도** 및 **습도** 이벤트 함께 한 번의 호출 tooIoT 허브를 보내야 합니다.

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

두 데이터 이벤트 허브 tooIoT 전송 되도록이 코드의 hello 결과 임을 추측할 수 있습니다.:

[

{"Temperature":75},

{"Humidity":45}

]

즉, 예상 대로이 코드는 hello 동일 보내는 것과 **온도** 및 **습도** 별도로 합니다. 방금 편의 toopass는 두 이벤트 모두 너무**SERIALIZE** hello에서는 동일한 호출 합니다. 그러나 hello 대/소문자가 아닌. 대신, 위의 hello 코드는이 단일 데이터 이벤트 tooIoT 허브를 보냅니다.

{"Temperature":75, "Humidity":45}

모델에서 **온도** 및 **습도**를 두 개의 *별도* 이벤트로 정의하므로 이것이 이상하게 보일 수 있습니다.

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

이러한 이벤트 모델링 하지 않은 다른 toohello 점 위치 **온도** 및 **습도** hello에 동일한 구조:

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

이 모델을 사용한 경우에 것이 더 쉽게 toounderstand 어떻게 **온도** 및 **습도** 보낼 hello에 메시지를 직렬화 하는 동일 합니다. 그러나 아닐 지우기 너무 두 데이터 이벤트를 전달 하는 경우 이런 방식으로 작동 하는 이유**SERIALIZE** 2 모델을 사용 합니다.

해당 hello hello 가정을 알고 있는 경우에이 동작은 쉽게 toounderstand **serializer** 라이브러리를 수행 합니다. 이 toomake 의미 백 tooour 모델을 해 보겠습니다.

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

이 모델을 개체 지향 용어로 생각해봅니다. 이 경우 실제 장치(자동 온도 조절기)를 모델링하고 해당 장치가 **온도** 및 **습도**와 같은 특성을 포함합니다.

Hello hello 다음과 같은 코드와 함께 모델의 전체 상태를 보내 드립니다.

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

온도, 습도 시간과 hello 값이 설정 된 경우이 보낸된 tooIoT 허브와 같은 이벤트를 볼 수 있습니다.

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

Toosend만 필요 하기도 *일부* hello 모델 toohello 클라우드 (이 모델에 있는 데이터 이벤트 수가 많은 경우에 특히 그렇습니다)의 속성입니다. 와 같은 데이터 이벤트의 하위 집합만 유용 toosend 이전 예에서:

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

Hello 정확 하 게 생성 동일한 이벤트 처럼 serialize 정의는 **TemperatureEvent** 와 **온도** 및 **시간** 않았습니다으로 모델링 1와 같은 방법으로 멤버입니다. 이 경우 अ स म र 정확 하 게 hello 동일 직렬화 이벤트 호출 하기 때문에 다른 모델 (모델 2)를 사용 하 여 수 toogenerate **SERIALIZE** 를 다른 방식으로 합니다.

hello 중요 한 점은 너무 여러 데이터 이벤트를 전달 하는 경우**SERIALIZE,** 각 이벤트는 단일 JSON 개체의 속성을 가정 합니다.

가장 좋은 방법이 hello 및 모델에 대 한 생각 하는 방법에 따라 달라 집니다. "이벤트" toohello 클라우드 보내는 각 이벤트에 정의 된 속성 집합을 포함 하는 경우 hello 첫 번째 방법은 큰 의미를 사용 합니다. 사용이 경우 **DECLARE\_구조체** toodefine hello 각 이벤트의 구조 및 다음 hello 사용 하 여 모델에 포함할 **WITH\_데이터** 매크로입니다. 그런 다음 위의 hello 첫 번째 예제에서와 같이 각 이벤트를 보냅니다. 이 방법만 전달 하는 단일 데이터 이벤트 너무**SERIALIZER**합니다.

개체 지향 방식으로 모델에 대 한 생각 되 면 다음 hello 두 번째 방법을 사용할 수 있습니다 적합 합니다. 이 예에서 사용 하 여 정의 된 요소를 hello **WITH\_데이터** 은 개체의 hello "속성이"입니다. 이벤트의 모든 하위 집합을 너무 전달**SERIALIZE** 원하는, toosend toohello 클라우드 "개체의" 상태의 정도 따라 원하는 합니다.

어떤 접근 방식이 옳거나 그르다고 말할 수 없습니다. 어떻게 될 hello **serializer** 라이브러리 작동 하며, 요구 사항에 가장 잘 맞는 선택 hello 모델링 접근 방식입니다.

## <a name="message-handling"></a>메시지 처리
지금까지이 문서는 송신 이벤트 tooIoT 허브 설명만 하 고 메시지를 받는 주소를 지정 하지 않았습니다. 이유 hello 메시지를 수신 하는 방법에 대 한 tooknow에서 다루는 크게 필요한 것은이 대 한 프로그램 [이전 문서](iot-hub-device-sdk-c-intro.md)합니다. 메시지 콜백 함수를 등록하여 메시지를 처리하는 문서를 상기해보겠습니다.

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

그런 다음 메시지를 받을 때 호출 되는 hello 콜백 함수를 작성 합니다.

```
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = EXECUTE_COMMAND_ERROR;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = EXECUTE_COMMAND_ERROR;
        }
        else
        {
            memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

이 구현 **IoTHubMessage** 호출 hello 모델의 각 작업에 특정 기능입니다. 예를 들어 모델에서 다음 동작을 정의하는 경우:

```
WITH_ACTION(SetAirResistance, int, Position)
```

다음 서명과 함께 함수를 정의해야 합니다.

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

**SetAirResistance** 그런 다음 해당 메시지를 tooyour 장치를 보낼 때 호출 됩니다.

설명 하지 않은 것 처럼 보이는 메시지의 직렬화 된 hello 버전 또 것입니다. 즉, toosend 하려는 경우는 **SetAirResistance** 메시지 tooyour 장치, 내용에 해당 모양을?

메시지 tooa 장치를 보내는 경우 hello Azure IoT 서비스 SDK 통해 그렇게가 있습니다. 여전히 toosend tooinvoke에서 특정 동작 문자열 tooknow 필요 합니다. hello 메시지를 보내기 위한 일반 형식 다음과 같이 나타납니다.

```
{"Name" : "", "Parameters" : "" }
```

두 개의 속성이 있는 serialize 된 JSON 개체를 보낼 때: **이름** hello 동작 (메시지)의 hello 이름인 및 **매개 변수** 해당 동작의 hello 매개 변수를 포함 합니다.

예를 들어 tooinvoke **SetAirResistance** 이 메시지 tooa 장치를 보낼 수 있습니다.

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

hello 동작 이름은 모델에 정의 된 동작을 정확히 일치 해야 합니다. hello 매개 변수 이름은 일치 해야 합니다. 또한 대/소문자 구분 여부도 확인합니다. **Name** 및 **Parameters**는 항상 대문자입니다. 모델의 작업 이름 및 매개 변수 있는지 toomatch hello 사례를 확인 합니다. 이 예제에서는 hello 작업 이름이 "SetAirResistance" 및 "setairresistance" 하지 않습니다.

다른 두 가지 동작 hello **TurnFanOn** 및 **TurnFanOff** 이러한 메시지 tooa 장치를 전송 하 여 호출할 수 있습니다.

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

이 여기서 설명한 hello 이벤트를 전송 및 메시지를 받을 때 tooknow 필요한 모든 **serializer** 라이브러리입니다. 설명을 진행하기 전에, 모델의 크기를 제어하기 위해 구성할 수 있는 몇 가지 매개 변수에 대해 살펴봅니다.

## <a name="macro-configuration"></a>매크로 구성
Hello를 사용 하 여 **Serializer** hello SDK toobe 인식의 중요 한 부분이 hello azure-c-공유-유틸리티 라이브러리에서 발견 되는 라이브러리입니다.
Hello-클래스 옵션을 사용 하 여 GitHub에서 hello Azure iot-sdk c 리포지토리를 복제 하는 경우이 공유 유틸리티 라이브러리를 찾을 수 있습니다.

```
.\\c-utility
```

Hello 라이브러리를 복제 하지 하는 경우 파일을 찾을 수 [여기](https://github.com/Azure/azure-c-shared-utility)합니다.

Hello 공유 유틸리티 라이브러리 내의 폴더를 다음 hello를 찾을 수 있습니다.

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

이 폴더에는 **macro\_utils\_h\_generator.sln**이라는 Visual Studio 솔루션이 포함되어 있습니다.

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

이 솔루션에서는 hello 프로그램 생성 hello **매크로\_utils.h** 파일입니다. 기본 매크로가\_hello SDK에 포함 된 utils.h 파일입니다. 이 솔루션에서는 일부 매개 변수 및 한 후 다시 만듭니다 hello 이러한 매개 변수를 기반으로 하는 헤더 파일 toomodify가 있습니다.

와 관련 된 toobe hello 두 키 매개 변수는 **nArithmetic** 및 **nMacroParameters** 매크로이 두 줄에 정의 되어 있는\_utils.tt:

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

이러한 값은 hello SDK에 포함 된 hello 기본 매개 변수입니다. 각 매개 변수에 의미에 따라 hello:

* nMacroParameters – 하나의 DECLARE\_MODEL 매크로 정의에 포함할 수 있는 매개 변수 수를 제어합니다.
* nArithmetic hello 컨트롤 모델에서 허용 되는 멤버의 총 수입니다.

이러한 매개 변수는 중요 한 hello 이유 제어 하기 때문에 크기 모델 수입니다. 예를 들어 다음 모델 정의를 고려해보겠습니다.

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

이전에 설명한 것처럼 **DECLARE\_MODEL**은 C 매크로입니다. hello 모델과 hello 형태의 hello **WITH\_데이터** 문 (아직 다른 매크로)는의 매개 변수 **DECLARE\_모델**합니다. **nMacroParameters**는 **DECLARE\_MODEL**에 포함할 수 있는 매개 변수 수를 정의합니다. 이러한 매개 변수는 포함할 수 있는 데이터 이벤트 및 동작 선언 수를 효과적으로 정의합니다. 따라서 124 hello 기본 제한 값으로 즉, 약 60 동작 및 데이터 이벤트를 조합 하 여 모델을 정의할 수 있습니다. 이 제한을 tooexceed를 시도 하면 컴파일러 오류 비슷한 toothis을 받게 됩니다.

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

hello **nArithmetic** 매개 변수는 hello 매크로 언어의 hello 내부 작업에 대 한 응용 프로그램 보다 더 합니다.  모델에 포함할 수 있습니다는 구성원의 hello 총 수를 제어 등 **DECLARE_STRUCT** 매크로입니다. 다음과 같은 컴파일러 오류가 표시되면 **nArithmetic**을 늘려야 합니다.

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

Hello 매크로 hello 값을 수정 하려는 경우 toochange 이러한 매개 변수,\_utils.tt 파일, recompile hello 매크로\_유틸리티\_h\_generator.sln 솔루션과 실행된 hello 컴파일된 프로그램. 이렇게 하려면 다음을 새 매크로\_utils.h 파일 생성 되 고 hello에 배치 됩니다.\\ 일반적인\\inc 디렉터리입니다.

순서 toouse hello 매크로의 새 버전에\_utils.h, 제거 hello **serializer** NuGet 패키지를 솔루션에서와 그 자리에 포함 hello **serializer** Visual Studio 프로젝트입니다. 따라서 hello serializer 라이브러리의 hello 소스 코드에 대해 프로그램 코드 toocompile를 수 있습니다. 여기에 업데이트 하는 hello 매크로\_utils.h 합니다. 에 대 한이 toodo 하려면 **simplesample\_amqp**, hello 솔루션에서 hello serializer 라이브러리에 대 한 hello NuGet 패키지를 제거 하 여 시작 합니다.

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

이 프로젝트 tooyour Visual Studio 솔루션을 추가 합니다.

> .\\c\\serializer\\build\\windows\\serializer.vcxproj
> 
> 

완료되면 다음과 같이 솔루션이 표시됩니다.

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

매크로 업데이트 컴파일하는 경우, 솔루션 hello 이제\_utils.h 이진 파일에 포함 됩니다.

이 값을 너무 높게 늘리면 컴파일러 한계를 초과할 수 있음에 유의합니다. toothis 지점 hello **nMacroParameters** 은 관심된 있는 toobe hello 주 매개 변수입니다. hello C99 사양의 127 매개 변수의 최소값 매크로 정의에서 수 있도록 지정 합니다. hello Microsoft 컴파일러 정확히 hello 사양 뒤에 오는 (및 127 제한 되어) 수 tooincrease 되지 않으므로 **nMacroParameters** hello 기본값 초과 합니다. 다른 컴파일러 수 있도록 toodo 있으므로 (예를 들어 hello GNU 컴파일러 지원 더 높은 한도).

지금까지 설명한 tooknow toowrite hello로 코드가 하는 방식에 대 한 필요한 모든 항목에 대 한 **serializer** 라이브러리입니다. 마무리하기 전에 궁금해할 수 있는 이전 문서의 일부 항목을 다시 확인해보겠습니다.

## <a name="hello-lower-level-apis"></a>hello 하위 수준 Api
이 문서 포커스가 있는 hello 샘플 응용 프로그램은 **simplesample\_amqp**합니다. 이 샘플 이벤트 사용 하 여 hello 상위 수준 (hello 비-"LL") Api toosend 및 메시지를 수신 합니다. 이러한 API를 사용하는 경우 이벤트 전송 및 메시지 수신을 모두 처리하는 백그라운드 스레드가 실행됩니다. 그러나 hello 하위 (LL) Api tooeliminate이 백그라운드 스레드를 사용할 수 있으며 이벤트를 보내는 또는 hello 클라우드에서 메시지를 받을 통해 명시적으로 제어할 수 있습니다.

에 설명 된 대로 [이전 문서](iot-hub-device-sdk-c-iothubclient.md), hello로 구성 된 기능 집합이 더 높은 수준의 Api:

* IoTHubClient\_CreateFromConnectionString
* IoTHubClient\_SendEventAsync
* IoTHubClient\_SetMessageCallback
* IoTHubClient\_Destroy

이러한 API는 **simplesample\_amqp**에 나와 있습니다.

유사한 하위 수준 API 집합도 있습니다.

* IoTHubClient\_LL\_CreateFromConnectionString
* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy

참고는 hello 하위 수준 Api 작업 정확 하 게 hello hello 이전 문서에서 설명 하는 방식으로 동일 합니다. 백그라운드 스레드 toohandle 메시지 이벤트 보내기 및 받기를 원하면 hello 첫 번째 집합의 Api 사용할 수 있습니다. Hello Api의 두 번째 집합을 사용 하 여 명시적으로 제어할 보내고 IoT 허브에서 데이터를 수신 하려는 경우. Api 작업의 집합 중 하나가 hello로 동일 하 게 제대로 **serializer** 라이브러리입니다.

방법의 예에 대 한 hello 하위 Api 사용 hello로 **serializer** 라이브러리 참조 hello **simplesample\_http** 응용 프로그램입니다.

## <a name="additional-topics"></a>추가 항목
속성 처리, 대체 장치 자격 증명 사용 및 구성 옵션은 다시 강조할 필요가 있습니다. 이러한 모든 항목은 [이전 문서](iot-hub-device-sdk-c-iothubclient.md)에서 다뤘습니다. hello 핵심인은 이러한 모든 기능은 작업 한다는 hello에서 동일한 방식으로 hello로 **serializer** 라이브러리 hello와 마찬가지로 **IoTHubClient** 라이브러리. 예를 들어 모델에서 tooattach 속성 tooan 이벤트를 하려는 경우 사용 **IoTHubMessage\_속성** 및 **지도**\_**AddorUpdate**, 같은 방식으로 앞에서 설명한 hello:

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

Hello에서 hello 이벤트가 생성 된 여부 **serializer** 라이브러리 hello를 사용 하 여 수동으로 만든 또는 **IoTHubClient** 라이브러리는 중요 하지 않습니다.

Hello에 대 한 장치 자격 증명을 사용 하 여 대체 **IoTHubClient\_LL\_만들기** 작업으로 **IoTHubClient\_CreateFromConnectionString** 에 대 한 할당 된 **IOTHUB\_클라이언트\_처리**합니다.

마지막으로, hello를 사용 하 여 **serializer** 라이브러리 구성 옵션을 설정할 수 있습니다 **IoTHubClient\_LL\_SetOption** hello를사용하는경우와같이방금**IoTHubClient** 라이브러리입니다.

고유 toohello 기능 **serializer** 라이브러리 Api hello 초기화 됩니다. Hello 라이브러리 사용을 시작 하기 전에 호출 해야 **serializer\_init**:

```
serializer_init(NULL);
```

**IoTHubClient\_CreateFromConnectionString**을 호출하기 바로 전에 수행합니다.

마찬가지로, 다 hello 라이브러리, 사용 할 hello 마지막 호출이 너무**serializer\_deinit**:

```
serializer_deinit();
```

위에 나열 된 기타 기능 모두 hello 그렇지 않으면 작업 hello에 동일 hello **serializer** 라이브러리 hello에서와 마찬가지로 **IoTHubClient** 라이브러리. 다음이 항목 중 하나에 대 한 자세한 내용은 참조 hello [이전 문서](iot-hub-device-sdk-c-iothubclient.md) 이 시리즈의 합니다.

## <a name="next-steps"></a>다음 단계
이 문서에서는 자세히 hello hello의 고유한 측면에서 설명 **serializer** hello에 포함 된 라이브러리 **C에 대 한 Azure IoT 장치 SDK**합니다. 제공 된 hello 정보를 toouse toosend 이벤트를 모델링 하는 방법에 대해 잘 알고 있어야를 IoT 허브에서 메시지를 수신 합니다.

Hello 세 부분으로 이루어진 계열 toodevelop 응용 프로그램을 hello 하는 방법에 마쳤습니다 **C에 대 한 Azure IoT 장치 SDK**합니다. 이 되어야 충분 한 정보 toonot get 시작 하지만 hello Api 어떻게 작동 하는지에 대 한 철저 한 이해를 제공 합니다. 추가 정보에 대 한 hello SDK에서 다루지 않는 여기에서 몇 가지 샘플 있습니다. 그렇지 않으면 hello [SDK 설명서](https://github.com/Azure/azure-iot-sdk-c) 추가 정보에 대 한 좋은 리소스입니다.

IoT 허브에 대 한 개발에 대 한 더 toolearn 참조 hello [Azure IoT Sdk][lnk-sdks]합니다.

toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

* [Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

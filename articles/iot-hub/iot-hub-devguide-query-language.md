---
title: "aaaUnderstand hello Azure IoT Hub 쿼리 언어 | Microsoft Docs"
description: "개발자 가이드-사용 된 장치 트윈스 및 IoT 허브에서 작업 하는 방법에 대 한 tooretrieve 정보를 hello IoT Hub SQL 방식 쿼리 언어에 대 한 설명입니다."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/17
ms.author: elioda
ms.openlocfilehash: 01a7c8ffdf44c6c27b834739d02c8fef1dd3d3fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a>참조 - 장치 쌍, 작업 및 메시지 라우팅에 대한 IoT Hub 쿼리 언어

강력한 SQL 유사 언어 tooretrieve 정보를 제공 하는 IoT 허브에 대 한 [장치 트윈스] [ lnk-twins] 및 [작업][lnk-jobs], 및 [메시지 라우팅][lnk-devguide-messaging-routes]합니다. 이 문서에 제공되는 내용:

* Hello IoT Hub 쿼리 언어의는 소개 toohello 주요 기능 및
* hello 세부 설명 hello 언어입니다.

## <a name="get-started-with-device-twin-queries"></a>장치 쌍 쿼리 시작
[장치 쌍][lnk-twins]은 임의의 JSON 개체를 태그와 속성으로 포함할 수 있습니다. IoT 허브를 사용 하면 모든 장치로 이중 정보를 포함 하는 단일 JSON 문서로 있습니다 tooquery 장치 트윈스.
예를 들어, IoT 허브 장치 트윈스 프로그램 구조를 다음 hello 한지 가정 합니다.

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

IoT Hub 이라는 문서 컬렉션으로 hello 장치 트윈스 노출 **장치**합니다.
따라서 다음 쿼리에서 hello hello 장치 트윈스의 전체 집합을 검색 합니다.

```sql
SELECT * FROM devices
```

> [!NOTE]
> [Azure IoT SDK][lnk-hub-sdks]는 큰 결과에 대한 페이징을 지원합니다.

IoT Hub 임의의 조건으로 필터링 tooretrieve 장치 트윈스가 있습니다. 예를 들어

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

검색 hello로 장치 트윈스 hello **location.region** 태그 너무 설정**미국**합니다.
예를 들어, 부울 연산자 및 산술 비교도 지원됩니다. 예를 들어

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

구성 된 미국 toosend 원격 분석 1 분 마다 종종 보다 작은 hello에 있는 모든 장치 트윈스를 검색 합니다. 편의 위해 이기도 hello로 가능한 toouse 배열 상수 **IN** 및 **닌** (에 속하지 않은) 연산자. 예를 들어

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

위 코드는 WiFi 또는 유선 연결을 보고한 모든 장치 쌍을 검색합니다. 해당 특정 속성을 포함 하는 모든 장치 트윈스 종종 필요 tooidentify 됩니다. IoT Hub hello 함수를 지원 `is_defined()` 이 목적을 위해 합니다. 예를 들어

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

hello를 정의 하는 모든 장치 트윈스 검색 `connectivity` 속성을 보고 합니다. Toohello 참조 [WHERE 절] [ lnk-query-where] hello 전체 참조에 대 한 필터링 기능 hello의 섹션입니다.

그룹화 및 집계도 지원됩니다. 예를 들어

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

각 원격 분석 구성 상태에 hello hello 장치 수를 반환합니다.

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

hello 앞의 예제에서는 경우 3 개의 장치 구성이 성공적으로 완료를 보고, 두 여전히 적용 하는 hello 구성 하나에 오류가 보고 되었습니다.

### <a name="c-example"></a>C# 예제
hello 쿼리 기능 hello에 의해 노출 되 [C# 서비스 SDK] [ lnk-hub-sdks] hello에 **RegistryManager** 클래스입니다.
다음은 간단한 예제 쿼리입니다.

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

참고 어떻게 hello **쿼리** (위쪽 too1000), 페이지 크기와 개체 인스턴스화되고 hello를 호출 하 여 여러 페이지를 검색할 수 있습니다 **GetNextAsTwinAsync** 메서드를 여러 번입니다.
Hello 쿼리 개체를 여러 개를 노출할 참고 **다음\***hello 쿼리 예: 장치로 이중 또는 작업 개체에 필요한 hello deserialization 옵션 또는 예측을 사용할 때 사용 하는 일반 JSON toobe에 따라 합니다.

### <a name="nodejs-example"></a>Node.js 예제
hello 쿼리 기능 hello에 의해 노출 되 [Node.js 용 Azure IoT 서비스 SDK] [ lnk-hub-sdks] hello에 **레지스트리** 개체입니다.
다음은 간단한 예제 쿼리입니다.

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed toofetch hello results: ' + err.message);
    } else {
        // Do something with hello results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

참고 어떻게 hello **쿼리** (위쪽 too1000), 페이지 크기와 개체 인스턴스화되고 hello를 호출 하 여 여러 페이지를 검색할 수 있습니다 **nextAsTwin** 메서드를 여러 번입니다.
Hello 쿼리 개체를 여러 개를 노출할 참고 **다음\***hello 쿼리 예: 장치로 이중 또는 작업 개체에 필요한 hello deserialization 옵션 또는 예측을 사용할 때 사용 하는 일반 JSON toobe에 따라 합니다.

### <a name="limitations"></a>제한 사항
> [!IMPORTANT]
> 쿼리 결과 장치 트윈스 몇 분 정도 지연 존중 toohello 최신 값으로 가질 수 있습니다. 개별 장치 트윈스 id를 쿼리 하는 경우 항상 이므로 것이 좋습니다 toouse hello 항상 hello 최신 값이 포함 되어 있으며 높은 제한 되는 제한 된 장치로 이중 API를 검색 합니다.

현재 비교는 기본 형식(개체 없음) 간에만 지원됩니다. 예를 들어 `... WHERE properties.desired.config = properties.reported.config`는 해당 속성에 기본 값이 있는 경우에만 지원됩니다.

## <a name="get-started-with-jobs-queries"></a>작업 쿼리 시작
[작업] [ lnk-jobs] 방법을 tooexecute 장치 집합에 대 한 작업을 제공 합니다. 호출 컬렉션의 일부가 되었습니다 hello 작업의 hello 정보를 포함 하는 각 장치로 이중 **작업**합니다.
로컬에서,

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

현재이 컬렉션은으로 쿼리 가능한 **devices.jobs** hello IoT Hub 쿼리 언어에에서 있습니다.

> [!IMPORTANT]
> 현재 장치 트윈스 (즉, '' 장치에서에서 포함 된 쿼리)를 쿼리할 때 hello 작업 속성이 반환 되지 않습니다. `FROM devices.jobs`를 사용하여 쿼리를 통해서만 직접 액세스할 수 있습니다.
>
>

예를 들어, tooget 모든 작업 (지난 및 예약 된) 단일 장치에 영향을 주는 hello 다음 쿼리를 사용할 수 있습니다.

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

Note hello 장치 관련 상태 (및 가능한 hello 직접적인 방법 응답) 반환 된 각 작업의이 쿼리 제공 하는 방법입니다.
임의의 부울 조건 hello에서 모든 개체 속성에 가능한 toofilter 이기도 **devices.jobs** 컬렉션입니다.
다음 쿼리에서 hello 예를 들어:

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

2016년 9월 이후에 생성된 장치 **myDeviceId**에 대해 완료된 모든 장치 쌍 업데이트 작업을 검색합니다.

단일 작업의 가능한 tooretrieve hello 장치 단위 결과 이기도합니다.

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a>제한 사항
현재 **devices.jobs**에 대한 쿼리는 다음을 지원하지 않습니다.

* 프로젝션(따라서 `SELECT *`만 가능)
* Toohello 장치로 이중 더하기 toojob 속성 (hello 앞 섹션 참조)에서 참조 하는 조건입니다.
* 집계 수행(예: count, avg, group by)

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a>장치-클라우드 메시지 경로에 대한 쿼리 식 시작

사용 하 여 [장치-클라우드 경로][lnk-devguide-messaging-routes], IoT Hub toodispatch 장치-클라우드 메시지를 개별 메시지에 대해 계산 되는 식에 따라 toodifferent 끝점을 구성할 수 있습니다.

hello 경로 [조건] [ lnk-query-expressions] 사용 하 여 hello로 이중 쿼리와 작업의에서 조건으로 동일한 IoT Hub 쿼리 언어입니다. 경로 조건이 hello 메시지 헤더와 본문에 대해 평가 됩니다. 라우팅 쿼리 식만 hello 메시지 본문, 메시지 헤더만 포함 될 수 있습니다 또는 둘 다가 메시지 헤더 및 메시지 본문입니다. IoT Hub을 맡으며이 서버의 hello 헤더와 주문 tooroute 메시지에서 메시지 본문에 대 한 특정 스키마 IoT 허브 tooproperly 경로 위해 꼭 필요한 hello 다음 섹션에 설명 합니다.

### <a name="routing-on-message-headers"></a>메시지 헤더에서 라우팅

IoT Hub hello를 메시지 라우팅에 메시지 헤더의 JSON 표현을 다음을 가정 합니다.

```json
{
    "$messageId": "",
    "$enqueuedTime": "",
    "$to": "",
    "$expiryTimeUtc": "",
    "$correlationId": "",
    "$userId": "",
    "$ack": "",
    "$connectionDeviceId": "",
    "$connectionDeviceGenerationId": "",
    "$connectionAuthMethod": "",
    "$content-type": "",
    "$content-encoding": "",

    "userProperty1": "",
    "userProperty2": ""
}
```

메시지 시스템 속성은 hello로 접두사가 `'$'` 기호입니다.
사용자 속성은 항상 이름을 사용하여 액세스됩니다. 시스템 속성을 갖는 toocoincide 사용자 속성 이름 발생 하는 경우 (같은 `$to`), hello로 hello 사용자 속성을 검색할 `$to` 식입니다.
대괄호를 사용 하 여 hello 시스템 속성에서 항상 액세스할 수 있습니다 `{}`: hello 식을 사용 하는 예를 들어, `{$to}` tooaccess hello 시스템 속성 `to`합니다. 대괄호로 묶은 속성 이름에는 항상 hello 해당 시스템 속성이 검색 합니다.

속성 이름은 대/소문자를 구분하지 않습니다.

> [!NOTE]
> 모든 메시지 속성은 문자열입니다. 시스템 속성에 hello에 설명 된 대로 [개발자 가이드][lnk-devguide-messaging-format], 없는 현재 쿼리에서 사용할 수 있는 toouse 합니다.
>

예를 들어, 사용 하는 경우는 `messageType` 속성을 모든 원격 분석 tooone 끝점 및 모든 경고 tooanother 끝점 tooroute 할 수 있습니다. 식 tooroute hello 원격 분석을 수행 하는 hello를 작성할 수 있습니다.

```sql
messageType = 'telemetry'
```

고 hello 식 tooroute hello에 대 한 경고 메시지를 따릅니다.

```sql
messageType = 'alert'
```

부울 식 및 함수도 지원됩니다. 이 기능을 심각도 수준 사이의 toodistinguish 예를 들어 사용:

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

Toohello 참조 [식과 조건] [ lnk-query-expressions] hello 전체 목록에 대 한 지원 되는 연산자와 함수 섹션.

### <a name="routing-on-message-bodies"></a>메시지 본문에서 라우팅

IoT Hub 기반으로 메시지 본문에만 라우트할 수 내용을 hello 메시지 본문이 제대로 되어 있으면 JSON으로 인코딩된 u t F-8, utf-16 또는 u t F-32를 형성 합니다. 너무 hello hello 메시지의 콘텐츠 형식을 설정 해야`application/json` hello의 hello 콘텐츠 인코딩 tooone hello 메시지 헤더 tooallow hello 본문 콘텐츠를 기준으로 한 IoT Hub tooroute hello 메시지에서에서 UTF 인코딩은 지원 합니다. Hello 헤더 중 하나를 지정 하지 않으면 IoT Hub 시도 하지 않습니다 tooevaluate hello 메시지에 대 한 hello 본문을 포함 하는 모든 쿼리 식입니다. JSON 메시지 메시지가 면 또는 hello 메시지 hello 콘텐츠 형식 및 콘텐츠 인코딩을 지정 하지 않는 경우 메시지 라우팅 hello 메시지 헤더에 따라 tooroute hello 메시지를 사용할 수 있습니다.

사용할 수 있습니다 `$body` hello 쿼리 식 tooroute hello 메시지에 있습니다. Hello 쿼리 식에서 간단한 본문 참조, 본문 배열 참조 또는 본문 참조가 여러 개 사용할 수 있습니다. 쿼리 식에서 본문 참조를 메시지 헤더 참조와 결합할 수도 있습니다. 예를 들어 hello 다음은 모든 유효한 쿼리 식입니다.

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a>IoT Hub 쿼리의 기초
모든 IoT Hub 쿼리는 SELECT 및 FROM 절로 이루어지며 선택적으로 WHERE 및 GROUP BY 절을 포함합니다. 모든 쿼리는 JSON 문서(예: 장치 쌍) 컬렉션에 대해 실행됩니다. hello FROM 절에서 반복 하는 hello 문서 컬렉션 toobe 나타냅니다 (**장치** 또는 **devices.jobs**). 그런 다음 hello hello 절이 적용 되는 위치에 있는 필터입니다. 집계로이 단계의 hello 결과 GROUP BY 절에 지정 된 hello로 그룹화 하 고 각 그룹에 대 한 행이 생성 됩니다 hello SELECT 절에 지정 된 대로 합니다.

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a>FROM 절
hello **< from_specification >에서** 절에는 두 개의 값만 가정할 수 있습니다: **장치에서**, tooquery 장치 트윈스 또는 **devices.jobs에서**, 장치 단위 tooquery 작업 세부 정보입니다.

## <a name="where-clause"></a>WHERE 절
hello **여기서 < filter_condition >** 절은 선택 사항입니다. Hello FROM 컬렉션에서 JSON 문서 hello hello 결과의 일부로 포함 된 toobe를 충족 해야 하는 하나 이상의 조건을 지정 합니다. JSON 문서 여야 hello 지정 조건 너무 "true" toobe hello 결과에 포함 합니다.

조건 섹션에 설명 된 hello 허용 [식과 조건][lnk-query-expressions]합니다.

## <a name="select-clause"></a>SELECT 절
hello SELECT 절 (**SELECT < select_list >**) 필수 이며 값 hello 쿼리에서 검색 되는지 지정 합니다. Hello JSON 값 toobe 사용 toogenerate 새 JSON 개체를 지정 합니다.
각 요소에 대 한 hello hello FROM 컬렉션의 필터링 (및 필요에 따라 그룹화 된) 하위 집합, hello 프로젝션 단계 hello SELECT 절에 지정 된 hello 값으로 생성 된 새 JSON 개체를 생성 합니다.

다음은 SELECT 절 hello의 hello 문법입니다.

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

여기서 **attribute_name** hello FROM 컬렉션의 hello JSON 문서에서에서 tooany 속성을 참조 합니다. Hello에 SELECT 절에 대 한 예가 있습니다 [장치로 이중 쿼리 시작] [ lnk-query-getstarted] 섹션.

현재 **SELECT \***와 다른 선택 절은 장치 쌍에 대한 집계 쿼리에서만 지원됩니다.

## <a name="group-by-clause"></a>GROUP BY 절
hello **GROUP BY < group_specification >** 절은 WHERE 절 hello에 지정 된 hello 필터 후 실행 될 수 전에 hello에 지정 된 hello 도법을 선택 하는 단계는 선택 사항입니다. 특성의 hello 값에 따라 문서를 그룹화 합니다. 이러한 그룹은 hello SELECT 절에 지정 된 대로 사용 되는 toogenerate 집계 값입니다.

GROUP BY를 사용한 쿼리의 예:

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

hello 정식 GROUP BY 구문은 다음과 같습니다.

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

여기서 **attribute_name** hello FROM 컬렉션의 hello JSON 문서에서에서 tooany 속성을 참조 합니다.

현재 hello GROUP BY 절은 장치 트윈스 쿼리할 때에 지원 됩니다.

## <a name="expressions-and-conditions"></a>식 및 조건
높은 수준에서 *식*은:

* (예: 부울, 숫자, 문자열, 배열 또는 개체), JSON 형식의 tooan 인스턴스를 평가 하 고
* 기본 제공 연산자와 함수를 사용 하 여 상수 및 hello 장치 JSON 문서에서 가져온 데이터를 조작 하 여 정의 됩니다.

*조건* tooa 부울 값을 계산 하는 식이 됩니다. 부울 값을 다른 모든 상수 **true** 한 것으로 간주 **false** (포함 하 여 **null**, **정의 되지 않은**, 모든 배열 또는 개체 인스턴스 모든 문자열을 명확 하 게 부울 hello **false**).

hello 식에 대 한 구문은 다음과 같습니다.

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

설명:

| 기호 | 정의 |
| --- | --- |
| attribute_name | Hello에 대 한 hello JSON 문서의 속성 **FROM** 컬렉션입니다. |
| binary_operator | Hello에 나열 된 모든 이항 연산자 [연산자](#operators) 섹션. |
| function_name| Hello에 나열 된 모든 함수 [함수](#functions) 섹션. |
| decimal_literal |소수 표기법으로 표현되는 부동 float입니다. |
| hexadecimal_literal |'0x'가 뒤의 16 진수 문자열 hello 문자열에 의해 표시 된 숫자입니다. |
| string_literal |문자열 리터럴은 연속적인 0이상의 유니코드 문자 또는 이스케이프 시퀀스로 표현되는 유니코드 문자열입니다. 문자열 리터럴은 작은따옴표(아포스트로피: ') 또는 큰따옴표(따옴표: ")로 묶어야 합니다. 허용되는 이스케이프: `\'`, `\"`, `\\`, 4개의 16진수로 정의되는 유니코드 문자인 경우 `\uXXXX` |

### <a name="operators"></a>연산자
연산자 뒤 hello 지원 됩니다.

| 패밀리 | 연산자 |
| --- | --- |
| 산술 |+,-,*,/,% |
| 논리 |AND, OR, NOT |
| 비교 |=, !=, <, >, <=, >=, <> |

### <a name="functions"></a>함수
에서만 지원 트윈스 및 작업 hello를 쿼리할 때 함수는:

| 함수 | 설명 |
| -------- | ----------- |
| IS_DEFINED(속성) | 경우 hello 속성 값이 할당에 나타내는 부울을 반환 (포함 하 여 `null`). |

경로 조건에서 다음 수치 연산 함수 hello 지원 됩니다.

| 함수 | 설명 |
| -------- | ----------- |
| ABS(x) | Hello 절대 (양수)의 값을 반환 hello 지정 된 숫자 식입니다. |
| EXP(x) | 지정 된 숫자 식의 hello hello 지 수 값 반환 (e ^ x). |
| POWER(x,y) | 반환 값의 지정 된 hello hello 식 toohello 지정 된 거듭제곱 (x ^ y).|
| SQUARE(x) | Hello의 제곱 반환 hello 숫자 값을 지정 합니다. |
| CEILING(x) | Hello, 보다 큰 가장 작은 정수 값 또는 같음, hello 특정된 숫자 식을 반환 합니다. |
| FLOOR(x) | 작은 hello 가장 큰 정수를 반환 toohello 같거나 지정 된 숫자 식입니다. |
| SIGN(x) | 반환 hello 양수 (+ 1), 영 (0) 또는 지정 된 숫자 식의 hello 음수 (-1) 기호입니다.|
| SQRT(x) | Hello의 제곱 반환 hello 숫자 값을 지정 합니다. |

경로 조건에서 형식 검사 및 함수 캐스팅 다음 hello 지원 됩니다.

| 함수 | 설명 |
| -------- | ----------- |
| AS_NUMBER | Hello 입력된 문자열 tooa를 변환합니다. 입력이 숫자이면 `noop`이고, 문자열이 숫자를 나타내지 않으면 `Undefined`입니다.|
| IS_ARRAY | 배열 hello hello 유형의 식을 지정 된 경우를 나타내는 부울 값을 반환 합니다. |
| IS_BOOL | 지정 된 식 hello hello 유형의 경우를 나타내는 부울 값은 부울을 반환 합니다. |
| IS_DEFINED | 경우 hello 속성 값이 할당에 나타내는 부울 값을 반환 합니다. |
| IS_NULL | 지정 된 식 hello hello 유형의 경우를 나타내는 부울 값이 null을 반환 합니다. |
| IS_NUMBER | Hello hello 유형의 식을 지정 하는 경우 나타내는 부울 값은 숫자를 반환 합니다. |
| IS_OBJECT | 지정 된 식 hello hello 유형의 경우를 나타내는 부울 값은 JSON 개체를 반환 합니다. |
| IS_PRIMITIVE | Hello의 hello 형식이 지정 되는 기본 식을 나타내는 부울 값을 반환 합니다 (문자열, 부울, 숫자 또는 `null`). |
| IS_STRING | Hello hello 유형의 식을 지정 하는 경우 나타내는 부울 값은 문자열로 반환 합니다. |

경로 조건에서 다음 문자열 함수 hello 지원 됩니다.

| 함수 | 설명 |
| -------- | ----------- |
| CONCAT(x, …) | 않은 hello 두 개 이상의 문자열 값을 연결한 결과인 문자열을 반환 합니다. |
| LENGTH(x) | Hello의 문자 수를 반환 합니다 hello 지정 된 문자열 식입니다.|
| LOWER(x) | 대문자 데이터 toolowercase 변환한 후 문자열 식을 반환 합니다. |
| UPPER(x) | 소문자 데이터 toouppercase 변환한 후 문자열 식을 반환 합니다. |
| SUBSTRING(string, start [, length]) | Hello에서 시작 하는 문자열 식의 반환 일부 문자 0부터 시작 위치를 지정 하 고 길이 또는 hello 문자열의 끝 toohello toohello 지정을 계속 합니다. |
| INDEX_OF(string, fragment) | Hello hello 문자열을 찾을 수 없는 경우 시작 hello hello hello 첫 번째 지정 된 문자열 식 또는-1 내에서 두 번째 문자열 식의 첫 번째 발생 위치를 반환 합니다.|
| STARTS_WITH(x, y) | 시작 하는지 여부를 첫 번째 문자열 식 hello hello 초를 나타내는 부울 값을 반환 합니다. |
| ENDS_WITH(x, y) | 끝나는지 여부를 첫 번째 문자열 식 hello hello 초를 나타내는 부울 값을 반환 합니다. |
| CONTAINS(x,y) | 첫 번째 문자열 식 hello hello를 두 번째로 포함 되는지 여부를 나타내는 부울 값을 반환 합니다. |

## <a name="next-steps"></a>다음 단계
사용 하 여 앱의 tooexecute 쿼리 하는 방법에 대해 알아봅니다 [Azure IoT Sdk][lnk-hub-sdks]합니다.

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md

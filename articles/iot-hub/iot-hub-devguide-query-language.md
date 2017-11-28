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
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a><span data-ttu-id="a2f7b-103">참조 - 장치 쌍, 작업 및 메시지 라우팅에 대한 IoT Hub 쿼리 언어</span><span class="sxs-lookup"><span data-stu-id="a2f7b-103">Reference - IoT Hub query language for device twins, jobs, and message routing</span></span>

<span data-ttu-id="a2f7b-104">강력한 SQL 유사 언어 tooretrieve 정보를 제공 하는 IoT 허브에 대 한 [장치 트윈스] [ lnk-twins] 및 [작업][lnk-jobs], 및 [메시지 라우팅][lnk-devguide-messaging-routes]합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-104">IoT Hub provides a powerful SQL-like language tooretrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span></span> <span data-ttu-id="a2f7b-105">이 문서에 제공되는 내용:</span><span class="sxs-lookup"><span data-stu-id="a2f7b-105">This article presents:</span></span>

* <span data-ttu-id="a2f7b-106">Hello IoT Hub 쿼리 언어의는 소개 toohello 주요 기능 및</span><span class="sxs-lookup"><span data-stu-id="a2f7b-106">An introduction toohello major features of hello IoT Hub query language, and</span></span>
* <span data-ttu-id="a2f7b-107">hello 세부 설명 hello 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-107">hello detailed description of hello language.</span></span>

## <a name="get-started-with-device-twin-queries"></a><span data-ttu-id="a2f7b-108">장치 쌍 쿼리 시작</span><span class="sxs-lookup"><span data-stu-id="a2f7b-108">Get started with device twin queries</span></span>
<span data-ttu-id="a2f7b-109">[장치 쌍][lnk-twins]은 임의의 JSON 개체를 태그와 속성으로 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-109">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="a2f7b-110">IoT 허브를 사용 하면 모든 장치로 이중 정보를 포함 하는 단일 JSON 문서로 있습니다 tooquery 장치 트윈스.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-110">IoT Hub enables you tooquery device twins as a single JSON document containing all device twin information.</span></span>
<span data-ttu-id="a2f7b-111">예를 들어, IoT 허브 장치 트윈스 프로그램 구조를 다음 hello 한지 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-111">Assume, for instance, that your IoT hub device twins have hello following structure:</span></span>

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

<span data-ttu-id="a2f7b-112">IoT Hub 이라는 문서 컬렉션으로 hello 장치 트윈스 노출 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-112">IoT Hub exposes hello device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="a2f7b-113">따라서 다음 쿼리에서 hello hello 장치 트윈스의 전체 집합을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-113">So hello following query retrieves hello whole set of device twins:</span></span>

```sql
SELECT * FROM devices
```

> [!NOTE]
> <span data-ttu-id="a2f7b-114">[Azure IoT SDK][lnk-hub-sdks]는 큰 결과에 대한 페이징을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-114">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>

<span data-ttu-id="a2f7b-115">IoT Hub 임의의 조건으로 필터링 tooretrieve 장치 트윈스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-115">IoT Hub allows you tooretrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="a2f7b-116">예를 들어</span><span class="sxs-lookup"><span data-stu-id="a2f7b-116">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

<span data-ttu-id="a2f7b-117">검색 hello로 장치 트윈스 hello **location.region** 태그 너무 설정**미국**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-117">retrieves hello device twins with hello **location.region** tag set too**US**.</span></span>
<span data-ttu-id="a2f7b-118">예를 들어, 부울 연산자 및 산술 비교도 지원됩니다. 예를 들어</span><span class="sxs-lookup"><span data-stu-id="a2f7b-118">Boolean operators and arithmetic comparisons are supported as well, for example</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

<span data-ttu-id="a2f7b-119">구성 된 미국 toosend 원격 분석 1 분 마다 종종 보다 작은 hello에 있는 모든 장치 트윈스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-119">retrieves all device twins located in hello US configured toosend telemetry less often than every minute.</span></span> <span data-ttu-id="a2f7b-120">편의 위해 이기도 hello로 가능한 toouse 배열 상수 **IN** 및 **닌** (에 속하지 않은) 연산자.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-120">As a convenience, it is also possible toouse array constants with hello **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="a2f7b-121">예를 들어</span><span class="sxs-lookup"><span data-stu-id="a2f7b-121">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

<span data-ttu-id="a2f7b-122">위 코드는 WiFi 또는 유선 연결을 보고한 모든 장치 쌍을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-122">retrieves all device twins that reported WiFi or wired connectivity.</span></span> <span data-ttu-id="a2f7b-123">해당 특정 속성을 포함 하는 모든 장치 트윈스 종종 필요 tooidentify 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-123">It is often necessary tooidentify all device twins that contain a specific property.</span></span> <span data-ttu-id="a2f7b-124">IoT Hub hello 함수를 지원 `is_defined()` 이 목적을 위해 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-124">IoT Hub supports hello function `is_defined()` for this purpose.</span></span> <span data-ttu-id="a2f7b-125">예를 들어</span><span class="sxs-lookup"><span data-stu-id="a2f7b-125">For instance,</span></span>

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

<span data-ttu-id="a2f7b-126">hello를 정의 하는 모든 장치 트윈스 검색 `connectivity` 속성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-126">retrieved all device twins that define hello `connectivity` reported property.</span></span> <span data-ttu-id="a2f7b-127">Toohello 참조 [WHERE 절] [ lnk-query-where] hello 전체 참조에 대 한 필터링 기능 hello의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-127">Refer toohello [WHERE clause][lnk-query-where] section for hello full reference of hello filtering capabilities.</span></span>

<span data-ttu-id="a2f7b-128">그룹화 및 집계도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-128">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="a2f7b-129">예를 들어</span><span class="sxs-lookup"><span data-stu-id="a2f7b-129">For instance,</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="a2f7b-130">각 원격 분석 구성 상태에 hello hello 장치 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-130">returns hello count of hello devices in each telemetry configuration status.</span></span>

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

<span data-ttu-id="a2f7b-131">hello 앞의 예제에서는 경우 3 개의 장치 구성이 성공적으로 완료를 보고, 두 여전히 적용 하는 hello 구성 하나에 오류가 보고 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-131">hello preceding example illustrates a situation where three devices reported successful configuration, two are still applying hello configuration, and one reported an error.</span></span>

### <a name="c-example"></a><span data-ttu-id="a2f7b-132">C# 예제</span><span class="sxs-lookup"><span data-stu-id="a2f7b-132">C# example</span></span>
<span data-ttu-id="a2f7b-133">hello 쿼리 기능 hello에 의해 노출 되 [C# 서비스 SDK] [ lnk-hub-sdks] hello에 **RegistryManager** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-133">hello query functionality is exposed by hello [C# service SDK][lnk-hub-sdks] in hello **RegistryManager** class.</span></span>
<span data-ttu-id="a2f7b-134">다음은 간단한 예제 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-134">Here is an example of a simple query:</span></span>

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

<span data-ttu-id="a2f7b-135">참고 어떻게 hello **쿼리** (위쪽 too1000), 페이지 크기와 개체 인스턴스화되고 hello를 호출 하 여 여러 페이지를 검색할 수 있습니다 **GetNextAsTwinAsync** 메서드를 여러 번입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-135">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **GetNextAsTwinAsync** methods multiple times.</span></span>
<span data-ttu-id="a2f7b-136">Hello 쿼리 개체를 여러 개를 노출할 참고 **다음\***hello 쿼리 예: 장치로 이중 또는 작업 개체에 필요한 hello deserialization 옵션 또는 예측을 사용할 때 사용 하는 일반 JSON toobe에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-136">Note that hello query object exposes multiple **Next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="a2f7b-137">Node.js 예제</span><span class="sxs-lookup"><span data-stu-id="a2f7b-137">Node.js example</span></span>
<span data-ttu-id="a2f7b-138">hello 쿼리 기능 hello에 의해 노출 되 [Node.js 용 Azure IoT 서비스 SDK] [ lnk-hub-sdks] hello에 **레지스트리** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-138">hello query functionality is exposed by hello [Azure IoT service SDK for Node.js][lnk-hub-sdks] in hello **Registry** object.</span></span>
<span data-ttu-id="a2f7b-139">다음은 간단한 예제 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-139">Here is an example of a simple query:</span></span>

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

<span data-ttu-id="a2f7b-140">참고 어떻게 hello **쿼리** (위쪽 too1000), 페이지 크기와 개체 인스턴스화되고 hello를 호출 하 여 여러 페이지를 검색할 수 있습니다 **nextAsTwin** 메서드를 여러 번입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-140">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **nextAsTwin** methods multiple times.</span></span>
<span data-ttu-id="a2f7b-141">Hello 쿼리 개체를 여러 개를 노출할 참고 **다음\***hello 쿼리 예: 장치로 이중 또는 작업 개체에 필요한 hello deserialization 옵션 또는 예측을 사용할 때 사용 하는 일반 JSON toobe에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-141">Note that hello query object exposes multiple **next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="a2f7b-142">제한 사항</span><span class="sxs-lookup"><span data-stu-id="a2f7b-142">Limitations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a2f7b-143">쿼리 결과 장치 트윈스 몇 분 정도 지연 존중 toohello 최신 값으로 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-143">Query results can have a few minutes of delay with respect toohello latest values in device twins.</span></span> <span data-ttu-id="a2f7b-144">개별 장치 트윈스 id를 쿼리 하는 경우 항상 이므로 것이 좋습니다 toouse hello 항상 hello 최신 값이 포함 되어 있으며 높은 제한 되는 제한 된 장치로 이중 API를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-144">If querying individual device twins by id, it is always preferable toouse hello retrieve device twin API, which always contains hello latest values and has higher throttling limits.</span></span>

<span data-ttu-id="a2f7b-145">현재 비교는 기본 형식(개체 없음) 간에만 지원됩니다. 예를 들어 `... WHERE properties.desired.config = properties.reported.config`는 해당 속성에 기본 값이 있는 경우에만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-145">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="a2f7b-146">작업 쿼리 시작</span><span class="sxs-lookup"><span data-stu-id="a2f7b-146">Get started with jobs queries</span></span>
<span data-ttu-id="a2f7b-147">[작업] [ lnk-jobs] 방법을 tooexecute 장치 집합에 대 한 작업을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-147">[Jobs][lnk-jobs] provide a way tooexecute operations on sets of devices.</span></span> <span data-ttu-id="a2f7b-148">호출 컬렉션의 일부가 되었습니다 hello 작업의 hello 정보를 포함 하는 각 장치로 이중 **작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-148">Each device twin contains hello information of hello jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="a2f7b-149">로컬에서,</span><span class="sxs-lookup"><span data-stu-id="a2f7b-149">Logically,</span></span>

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

<span data-ttu-id="a2f7b-150">현재이 컬렉션은으로 쿼리 가능한 **devices.jobs** hello IoT Hub 쿼리 언어에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-150">Currently, this collection is queryable as **devices.jobs** in hello IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a2f7b-151">현재 장치 트윈스 (즉, '' 장치에서에서 포함 된 쿼리)를 쿼리할 때 hello 작업 속성이 반환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-151">Currently, hello jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span></span> <span data-ttu-id="a2f7b-152">`FROM devices.jobs`를 사용하여 쿼리를 통해서만 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-152">It can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="a2f7b-153">예를 들어, tooget 모든 작업 (지난 및 예약 된) 단일 장치에 영향을 주는 hello 다음 쿼리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-153">For instance, tooget all jobs (past and scheduled) that affect a single device, you can use hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

<span data-ttu-id="a2f7b-154">Note hello 장치 관련 상태 (및 가능한 hello 직접적인 방법 응답) 반환 된 각 작업의이 쿼리 제공 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-154">Note how this query provides hello device-specific status (and possibly hello direct method response) of each job returned.</span></span>
<span data-ttu-id="a2f7b-155">임의의 부울 조건 hello에서 모든 개체 속성에 가능한 toofilter 이기도 **devices.jobs** 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-155">It is also possible toofilter with arbitrary Boolean conditions on all object properties in hello **devices.jobs** collection.</span></span>
<span data-ttu-id="a2f7b-156">다음 쿼리에서 hello 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="a2f7b-156">For instance, hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

<span data-ttu-id="a2f7b-157">2016년 9월 이후에 생성된 장치 **myDeviceId**에 대해 완료된 모든 장치 쌍 업데이트 작업을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-157">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span></span>

<span data-ttu-id="a2f7b-158">단일 작업의 가능한 tooretrieve hello 장치 단위 결과 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-158">It is also possible tooretrieve hello per-device outcomes of a single job.</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a><span data-ttu-id="a2f7b-159">제한 사항</span><span class="sxs-lookup"><span data-stu-id="a2f7b-159">Limitations</span></span>
<span data-ttu-id="a2f7b-160">현재 **devices.jobs**에 대한 쿼리는 다음을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-160">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="a2f7b-161">프로젝션(따라서 `SELECT *`만 가능)</span><span class="sxs-lookup"><span data-stu-id="a2f7b-161">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="a2f7b-162">Toohello 장치로 이중 더하기 toojob 속성 (hello 앞 섹션 참조)에서 참조 하는 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-162">Conditions that refer toohello device twin in addition toojob properties (see hello preceding section).</span></span>
* <span data-ttu-id="a2f7b-163">집계 수행(예: count, avg, group by)</span><span class="sxs-lookup"><span data-stu-id="a2f7b-163">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="a2f7b-164">장치-클라우드 메시지 경로에 대한 쿼리 식 시작</span><span class="sxs-lookup"><span data-stu-id="a2f7b-164">Get started with device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="a2f7b-165">사용 하 여 [장치-클라우드 경로][lnk-devguide-messaging-routes], IoT Hub toodispatch 장치-클라우드 메시지를 개별 메시지에 대해 계산 되는 식에 따라 toodifferent 끝점을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-165">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub toodispatch device-to-cloud messages toodifferent endpoints based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="a2f7b-166">hello 경로 [조건] [ lnk-query-expressions] 사용 하 여 hello로 이중 쿼리와 작업의에서 조건으로 동일한 IoT Hub 쿼리 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-166">hello route [condition][lnk-query-expressions] uses hello same IoT Hub query language as conditions in twin and job queries.</span></span> <span data-ttu-id="a2f7b-167">경로 조건이 hello 메시지 헤더와 본문에 대해 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-167">Route conditions are evaluated on hello message headers and body.</span></span> <span data-ttu-id="a2f7b-168">라우팅 쿼리 식만 hello 메시지 본문, 메시지 헤더만 포함 될 수 있습니다 또는 둘 다가 메시지 헤더 및 메시지 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-168">Your routing query expression may involve only message headers, only hello message body, or both message headers and message body.</span></span> <span data-ttu-id="a2f7b-169">IoT Hub을 맡으며이 서버의 hello 헤더와 주문 tooroute 메시지에서 메시지 본문에 대 한 특정 스키마 IoT 허브 tooproperly 경로 위해 꼭 필요한 hello 다음 섹션에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-169">IoT Hub assumes a specific schema for hello headers and message body in order tooroute messages, and hello following sections describe what is required for IoT Hub tooproperly route:</span></span>

### <a name="routing-on-message-headers"></a><span data-ttu-id="a2f7b-170">메시지 헤더에서 라우팅</span><span class="sxs-lookup"><span data-stu-id="a2f7b-170">Routing on message headers</span></span>

<span data-ttu-id="a2f7b-171">IoT Hub hello를 메시지 라우팅에 메시지 헤더의 JSON 표현을 다음을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-171">IoT Hub assumes hello following JSON representation of message headers for message routing:</span></span>

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

<span data-ttu-id="a2f7b-172">메시지 시스템 속성은 hello로 접두사가 `'$'` 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-172">Message system properties are prefixed with hello `'$'` symbol.</span></span>
<span data-ttu-id="a2f7b-173">사용자 속성은 항상 이름을 사용하여 액세스됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-173">User properties are always accessed with their name.</span></span> <span data-ttu-id="a2f7b-174">시스템 속성을 갖는 toocoincide 사용자 속성 이름 발생 하는 경우 (같은 `$to`), hello로 hello 사용자 속성을 검색할 `$to` 식입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-174">If a user property name happens toocoincide with a system property (such as `$to`), hello user property will be retrieved with hello `$to` expression.</span></span>
<span data-ttu-id="a2f7b-175">대괄호를 사용 하 여 hello 시스템 속성에서 항상 액세스할 수 있습니다 `{}`: hello 식을 사용 하는 예를 들어, `{$to}` tooaccess hello 시스템 속성 `to`합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-175">You can always access hello system property using brackets `{}`: for instance, you can use hello expression `{$to}` tooaccess hello system property `to`.</span></span> <span data-ttu-id="a2f7b-176">대괄호로 묶은 속성 이름에는 항상 hello 해당 시스템 속성이 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-176">Bracketed property names always retrieve hello corresponding system property.</span></span>

<span data-ttu-id="a2f7b-177">속성 이름은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-177">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="a2f7b-178">모든 메시지 속성은 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-178">All message properties are strings.</span></span> <span data-ttu-id="a2f7b-179">시스템 속성에 hello에 설명 된 대로 [개발자 가이드][lnk-devguide-messaging-format], 없는 현재 쿼리에서 사용할 수 있는 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-179">System properties, as described in hello [developer guide][lnk-devguide-messaging-format], are currently not available toouse in queries.</span></span>
>

<span data-ttu-id="a2f7b-180">예를 들어, 사용 하는 경우는 `messageType` 속성을 모든 원격 분석 tooone 끝점 및 모든 경고 tooanother 끝점 tooroute 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-180">For example, if you use a `messageType` property, you might want tooroute all telemetry tooone endpoint, and all alerts tooanother endpoint.</span></span> <span data-ttu-id="a2f7b-181">식 tooroute hello 원격 분석을 수행 하는 hello를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-181">You can write hello following expression tooroute hello telemetry:</span></span>

```sql
messageType = 'telemetry'
```

<span data-ttu-id="a2f7b-182">고 hello 식 tooroute hello에 대 한 경고 메시지를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-182">And hello following expression tooroute hello alert messages:</span></span>

```sql
messageType = 'alert'
```

<span data-ttu-id="a2f7b-183">부울 식 및 함수도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-183">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="a2f7b-184">이 기능을 심각도 수준 사이의 toodistinguish 예를 들어 사용:</span><span class="sxs-lookup"><span data-stu-id="a2f7b-184">This feature enables you toodistinguish between severity level, for example:</span></span>

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

<span data-ttu-id="a2f7b-185">Toohello 참조 [식과 조건] [ lnk-query-expressions] hello 전체 목록에 대 한 지원 되는 연산자와 함수 섹션.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-185">Refer toohello [Expression and conditions][lnk-query-expressions] section for hello full list of supported operators and functions.</span></span>

### <a name="routing-on-message-bodies"></a><span data-ttu-id="a2f7b-186">메시지 본문에서 라우팅</span><span class="sxs-lookup"><span data-stu-id="a2f7b-186">Routing on message bodies</span></span>

<span data-ttu-id="a2f7b-187">IoT Hub 기반으로 메시지 본문에만 라우트할 수 내용을 hello 메시지 본문이 제대로 되어 있으면 JSON으로 인코딩된 u t F-8, utf-16 또는 u t F-32를 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-187">IoT Hub can only route based on message body contents if hello message body is properly formed JSON encoded in either UTF-8, UTF-16, or UTF-32.</span></span> <span data-ttu-id="a2f7b-188">너무 hello hello 메시지의 콘텐츠 형식을 설정 해야`application/json` hello의 hello 콘텐츠 인코딩 tooone hello 메시지 헤더 tooallow hello 본문 콘텐츠를 기준으로 한 IoT Hub tooroute hello 메시지에서에서 UTF 인코딩은 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-188">You must set hello content type of hello message too`application/json` and hello content encoding tooone of hello supported UTF encodings in hello message headers tooallow IoT Hub tooroute hello message based on hello body contents.</span></span> <span data-ttu-id="a2f7b-189">Hello 헤더 중 하나를 지정 하지 않으면 IoT Hub 시도 하지 않습니다 tooevaluate hello 메시지에 대 한 hello 본문을 포함 하는 모든 쿼리 식입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-189">If either of hello headers is not specified, IoT Hub will not attempt tooevaluate any query expression involving hello body against hello message.</span></span> <span data-ttu-id="a2f7b-190">JSON 메시지 메시지가 면 또는 hello 메시지 hello 콘텐츠 형식 및 콘텐츠 인코딩을 지정 하지 않는 경우 메시지 라우팅 hello 메시지 헤더에 따라 tooroute hello 메시지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-190">If your message is not a JSON message, or if hello message does not specify hello content type and content encoding, you may still use message routing tooroute hello message based on hello message headers.</span></span>

<span data-ttu-id="a2f7b-191">사용할 수 있습니다 `$body` hello 쿼리 식 tooroute hello 메시지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-191">You can use `$body` in hello query expression tooroute hello message.</span></span> <span data-ttu-id="a2f7b-192">Hello 쿼리 식에서 간단한 본문 참조, 본문 배열 참조 또는 본문 참조가 여러 개 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-192">You can use a simple body reference, body array reference, or multiple body references in hello query expression.</span></span> <span data-ttu-id="a2f7b-193">쿼리 식에서 본문 참조를 메시지 헤더 참조와 결합할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-193">Your query expression can also combine a body reference with a message header reference.</span></span> <span data-ttu-id="a2f7b-194">예를 들어 hello 다음은 모든 유효한 쿼리 식입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-194">For example, hello following are all valid query expressions:</span></span>

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="a2f7b-195">IoT Hub 쿼리의 기초</span><span class="sxs-lookup"><span data-stu-id="a2f7b-195">Basics of an IoT Hub query</span></span>
<span data-ttu-id="a2f7b-196">모든 IoT Hub 쿼리는 SELECT 및 FROM 절로 이루어지며 선택적으로 WHERE 및 GROUP BY 절을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-196">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="a2f7b-197">모든 쿼리는 JSON 문서(예: 장치 쌍) 컬렉션에 대해 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-197">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="a2f7b-198">hello FROM 절에서 반복 하는 hello 문서 컬렉션 toobe 나타냅니다 (**장치** 또는 **devices.jobs**).</span><span class="sxs-lookup"><span data-stu-id="a2f7b-198">hello FROM clause indicates hello document collection toobe iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="a2f7b-199">그런 다음 hello hello 절이 적용 되는 위치에 있는 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-199">Then, hello filter in hello WHERE clause is applied.</span></span> <span data-ttu-id="a2f7b-200">집계로이 단계의 hello 결과 GROUP BY 절에 지정 된 hello로 그룹화 하 고 각 그룹에 대 한 행이 생성 됩니다 hello SELECT 절에 지정 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-200">With aggregations, hello results of this step are grouped as specified in hello GROUP BY clause and, for each group, a row is generated as specified in hello SELECT clause.</span></span>

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a><span data-ttu-id="a2f7b-201">FROM 절</span><span class="sxs-lookup"><span data-stu-id="a2f7b-201">FROM clause</span></span>
<span data-ttu-id="a2f7b-202">hello **< from_specification >에서** 절에는 두 개의 값만 가정할 수 있습니다: **장치에서**, tooquery 장치 트윈스 또는 **devices.jobs에서**, 장치 단위 tooquery 작업 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-202">hello **FROM <from_specification>** clause can assume only two values: **FROM devices**, tooquery device twins, or **FROM devices.jobs**, tooquery job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="a2f7b-203">WHERE 절</span><span class="sxs-lookup"><span data-stu-id="a2f7b-203">WHERE clause</span></span>
<span data-ttu-id="a2f7b-204">hello **여기서 < filter_condition >** 절은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-204">hello **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="a2f7b-205">Hello FROM 컬렉션에서 JSON 문서 hello hello 결과의 일부로 포함 된 toobe를 충족 해야 하는 하나 이상의 조건을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-205">It specifies one or more conditions that hello JSON documents in hello FROM collection must satisfy toobe included as part of hello result.</span></span> <span data-ttu-id="a2f7b-206">JSON 문서 여야 hello 지정 조건 너무 "true" toobe hello 결과에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-206">Any JSON document must evaluate hello specified conditions too"true" toobe included in hello result.</span></span>

<span data-ttu-id="a2f7b-207">조건 섹션에 설명 된 hello 허용 [식과 조건][lnk-query-expressions]합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-207">hello allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="a2f7b-208">SELECT 절</span><span class="sxs-lookup"><span data-stu-id="a2f7b-208">SELECT clause</span></span>
<span data-ttu-id="a2f7b-209">hello SELECT 절 (**SELECT < select_list >**) 필수 이며 값 hello 쿼리에서 검색 되는지 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-209">hello SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from hello query.</span></span> <span data-ttu-id="a2f7b-210">Hello JSON 값 toobe 사용 toogenerate 새 JSON 개체를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-210">It specifies hello JSON values toobe used toogenerate new JSON objects.</span></span>
<span data-ttu-id="a2f7b-211">각 요소에 대 한 hello hello FROM 컬렉션의 필터링 (및 필요에 따라 그룹화 된) 하위 집합, hello 프로젝션 단계 hello SELECT 절에 지정 된 hello 값으로 생성 된 새 JSON 개체를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-211">For each element of hello filtered (and optionally grouped) subset of hello FROM collection, hello projection phase generates a new JSON object, constructed with hello values specified in hello SELECT clause.</span></span>

<span data-ttu-id="a2f7b-212">다음은 SELECT 절 hello의 hello 문법입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-212">Following is hello grammar of hello SELECT clause:</span></span>

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

<span data-ttu-id="a2f7b-213">여기서 **attribute_name** hello FROM 컬렉션의 hello JSON 문서에서에서 tooany 속성을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-213">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span> <span data-ttu-id="a2f7b-214">Hello에 SELECT 절에 대 한 예가 있습니다 [장치로 이중 쿼리 시작] [ lnk-query-getstarted] 섹션.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-214">Some examples of SELECT clauses can be found in hello [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="a2f7b-215">현재 **SELECT \***와 다른 선택 절은 장치 쌍에 대한 집계 쿼리에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-215">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="a2f7b-216">GROUP BY 절</span><span class="sxs-lookup"><span data-stu-id="a2f7b-216">GROUP BY clause</span></span>
<span data-ttu-id="a2f7b-217">hello **GROUP BY < group_specification >** 절은 WHERE 절 hello에 지정 된 hello 필터 후 실행 될 수 전에 hello에 지정 된 hello 도법을 선택 하는 단계는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-217">hello **GROUP BY <group_specification>** clause is an optional step that can be executed after hello filter specified in hello WHERE clause, and before hello projection specified in hello SELECT.</span></span> <span data-ttu-id="a2f7b-218">특성의 hello 값에 따라 문서를 그룹화 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-218">It groups documents based on hello value of an attribute.</span></span> <span data-ttu-id="a2f7b-219">이러한 그룹은 hello SELECT 절에 지정 된 대로 사용 되는 toogenerate 집계 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-219">These groups are used toogenerate aggregated values as specified in hello SELECT clause.</span></span>

<span data-ttu-id="a2f7b-220">GROUP BY를 사용한 쿼리의 예:</span><span class="sxs-lookup"><span data-stu-id="a2f7b-220">An example of a query using GROUP BY is:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="a2f7b-221">hello 정식 GROUP BY 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-221">hello formal syntax for GROUP BY is:</span></span>

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

<span data-ttu-id="a2f7b-222">여기서 **attribute_name** hello FROM 컬렉션의 hello JSON 문서에서에서 tooany 속성을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-222">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span>

<span data-ttu-id="a2f7b-223">현재 hello GROUP BY 절은 장치 트윈스 쿼리할 때에 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-223">Currently, hello GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="a2f7b-224">식 및 조건</span><span class="sxs-lookup"><span data-stu-id="a2f7b-224">Expressions and conditions</span></span>
<span data-ttu-id="a2f7b-225">높은 수준에서 *식*은:</span><span class="sxs-lookup"><span data-stu-id="a2f7b-225">At a high level, an *expression*:</span></span>

* <span data-ttu-id="a2f7b-226">(예: 부울, 숫자, 문자열, 배열 또는 개체), JSON 형식의 tooan 인스턴스를 평가 하 고</span><span class="sxs-lookup"><span data-stu-id="a2f7b-226">Evaluates tooan instance of a JSON type (such as Boolean, number, string, array, or object), and</span></span>
* <span data-ttu-id="a2f7b-227">기본 제공 연산자와 함수를 사용 하 여 상수 및 hello 장치 JSON 문서에서 가져온 데이터를 조작 하 여 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-227">Is defined by manipulating data coming from hello device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="a2f7b-228">*조건* tooa 부울 값을 계산 하는 식이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-228">*Conditions* are expressions that evaluate tooa Boolean.</span></span> <span data-ttu-id="a2f7b-229">부울 값을 다른 모든 상수 **true** 한 것으로 간주 **false** (포함 하 여 **null**, **정의 되지 않은**, 모든 배열 또는 개체 인스턴스 모든 문자열을 명확 하 게 부울 hello **false**).</span><span class="sxs-lookup"><span data-stu-id="a2f7b-229">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly hello Boolean **false**).</span></span>

<span data-ttu-id="a2f7b-230">hello 식에 대 한 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-230">hello syntax for expressions is:</span></span>

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

<span data-ttu-id="a2f7b-231">설명:</span><span class="sxs-lookup"><span data-stu-id="a2f7b-231">where:</span></span>

| <span data-ttu-id="a2f7b-232">기호</span><span class="sxs-lookup"><span data-stu-id="a2f7b-232">Symbol</span></span> | <span data-ttu-id="a2f7b-233">정의</span><span class="sxs-lookup"><span data-stu-id="a2f7b-233">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="a2f7b-234">attribute_name</span><span class="sxs-lookup"><span data-stu-id="a2f7b-234">attribute_name</span></span> | <span data-ttu-id="a2f7b-235">Hello에 대 한 hello JSON 문서의 속성 **FROM** 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-235">Any property of hello JSON document in hello **FROM** collection.</span></span> |
| <span data-ttu-id="a2f7b-236">binary_operator</span><span class="sxs-lookup"><span data-stu-id="a2f7b-236">binary_operator</span></span> | <span data-ttu-id="a2f7b-237">Hello에 나열 된 모든 이항 연산자 [연산자](#operators) 섹션.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-237">Any binary operator listed in hello [Operators](#operators) section.</span></span> |
| <span data-ttu-id="a2f7b-238">function_name</span><span class="sxs-lookup"><span data-stu-id="a2f7b-238">function_name</span></span>| <span data-ttu-id="a2f7b-239">Hello에 나열 된 모든 함수 [함수](#functions) 섹션.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-239">Any function listed in hello [Functions](#functions) section.</span></span> |
| <span data-ttu-id="a2f7b-240">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="a2f7b-240">decimal_literal</span></span> |<span data-ttu-id="a2f7b-241">소수 표기법으로 표현되는 부동 float입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-241">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="a2f7b-242">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="a2f7b-242">hexadecimal_literal</span></span> |<span data-ttu-id="a2f7b-243">'0x'가 뒤의 16 진수 문자열 hello 문자열에 의해 표시 된 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-243">A number expressed by hello string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="a2f7b-244">string_literal</span><span class="sxs-lookup"><span data-stu-id="a2f7b-244">string_literal</span></span> |<span data-ttu-id="a2f7b-245">문자열 리터럴은 연속적인 0이상의 유니코드 문자 또는 이스케이프 시퀀스로 표현되는 유니코드 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-245">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="a2f7b-246">문자열 리터럴은 작은따옴표(아포스트로피: ') 또는 큰따옴표(따옴표: ")로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-246">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span> <span data-ttu-id="a2f7b-247">허용되는 이스케이프: `\'`, `\"`, `\\`, 4개의 16진수로 정의되는 유니코드 문자인 경우 `\uXXXX`</span><span class="sxs-lookup"><span data-stu-id="a2f7b-247">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="a2f7b-248">연산자</span><span class="sxs-lookup"><span data-stu-id="a2f7b-248">Operators</span></span>
<span data-ttu-id="a2f7b-249">연산자 뒤 hello 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-249">hello following operators are supported:</span></span>

| <span data-ttu-id="a2f7b-250">패밀리</span><span class="sxs-lookup"><span data-stu-id="a2f7b-250">Family</span></span> | <span data-ttu-id="a2f7b-251">연산자</span><span class="sxs-lookup"><span data-stu-id="a2f7b-251">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="a2f7b-252">산술</span><span class="sxs-lookup"><span data-stu-id="a2f7b-252">Arithmetic</span></span> |<span data-ttu-id="a2f7b-253">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="a2f7b-253">+,-,*,/,%</span></span> |
| <span data-ttu-id="a2f7b-254">논리</span><span class="sxs-lookup"><span data-stu-id="a2f7b-254">Logical</span></span> |<span data-ttu-id="a2f7b-255">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="a2f7b-255">AND, OR, NOT</span></span> |
| <span data-ttu-id="a2f7b-256">비교</span><span class="sxs-lookup"><span data-stu-id="a2f7b-256">Comparison</span></span> |<span data-ttu-id="a2f7b-257">=, !=, <, >, <=, >=, <></span><span class="sxs-lookup"><span data-stu-id="a2f7b-257">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="a2f7b-258">함수</span><span class="sxs-lookup"><span data-stu-id="a2f7b-258">Functions</span></span>
<span data-ttu-id="a2f7b-259">에서만 지원 트윈스 및 작업 hello를 쿼리할 때 함수는:</span><span class="sxs-lookup"><span data-stu-id="a2f7b-259">When querying twins and jobs hello only supported function is:</span></span>

| <span data-ttu-id="a2f7b-260">함수</span><span class="sxs-lookup"><span data-stu-id="a2f7b-260">Function</span></span> | <span data-ttu-id="a2f7b-261">설명</span><span class="sxs-lookup"><span data-stu-id="a2f7b-261">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="a2f7b-262">IS_DEFINED(속성)</span><span class="sxs-lookup"><span data-stu-id="a2f7b-262">IS_DEFINED(property)</span></span> | <span data-ttu-id="a2f7b-263">경우 hello 속성 값이 할당에 나타내는 부울을 반환 (포함 하 여 `null`).</span><span class="sxs-lookup"><span data-stu-id="a2f7b-263">Returns a Boolean indicating if hello property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="a2f7b-264">경로 조건에서 다음 수치 연산 함수 hello 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-264">In routes conditions, hello following math functions are supported:</span></span>

| <span data-ttu-id="a2f7b-265">함수</span><span class="sxs-lookup"><span data-stu-id="a2f7b-265">Function</span></span> | <span data-ttu-id="a2f7b-266">설명</span><span class="sxs-lookup"><span data-stu-id="a2f7b-266">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="a2f7b-267">ABS(x)</span><span class="sxs-lookup"><span data-stu-id="a2f7b-267">ABS(x)</span></span> | <span data-ttu-id="a2f7b-268">Hello 절대 (양수)의 값을 반환 hello 지정 된 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-268">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| <span data-ttu-id="a2f7b-269">EXP(x)</span><span class="sxs-lookup"><span data-stu-id="a2f7b-269">EXP(x)</span></span> | <span data-ttu-id="a2f7b-270">지정 된 숫자 식의 hello hello 지 수 값 반환 (e ^ x).</span><span class="sxs-lookup"><span data-stu-id="a2f7b-270">Returns hello exponential value of hello specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="a2f7b-271">POWER(x,y)</span><span class="sxs-lookup"><span data-stu-id="a2f7b-271">POWER(x,y)</span></span> | <span data-ttu-id="a2f7b-272">반환 값의 지정 된 hello hello 식 toohello 지정 된 거듭제곱 (x ^ y).</span><span class="sxs-lookup"><span data-stu-id="a2f7b-272">Returns hello value of hello specified expression toohello specified power (x^y).</span></span>|
| <span data-ttu-id="a2f7b-273">SQUARE(x)</span><span class="sxs-lookup"><span data-stu-id="a2f7b-273">SQUARE(x)</span></span> | <span data-ttu-id="a2f7b-274">Hello의 제곱 반환 hello 숫자 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-274">Returns hello square of hello specified numeric value.</span></span> |
| <span data-ttu-id="a2f7b-275">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="a2f7b-275">CEILING(x)</span></span> | <span data-ttu-id="a2f7b-276">Hello, 보다 큰 가장 작은 정수 값 또는 같음, hello 특정된 숫자 식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-276">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| <span data-ttu-id="a2f7b-277">FLOOR(x)</span><span class="sxs-lookup"><span data-stu-id="a2f7b-277">FLOOR(x)</span></span> | <span data-ttu-id="a2f7b-278">작은 hello 가장 큰 정수를 반환 toohello 같거나 지정 된 숫자 식입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-278">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| <span data-ttu-id="a2f7b-279">SIGN(x)</span><span class="sxs-lookup"><span data-stu-id="a2f7b-279">SIGN(x)</span></span> | <span data-ttu-id="a2f7b-280">반환 hello 양수 (+ 1), 영 (0) 또는 지정 된 숫자 식의 hello 음수 (-1) 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-280">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>|
| <span data-ttu-id="a2f7b-281">SQRT(x)</span><span class="sxs-lookup"><span data-stu-id="a2f7b-281">SQRT(x)</span></span> | <span data-ttu-id="a2f7b-282">Hello의 제곱 반환 hello 숫자 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-282">Returns hello square of hello specified numeric value.</span></span> |

<span data-ttu-id="a2f7b-283">경로 조건에서 형식 검사 및 함수 캐스팅 다음 hello 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-283">In routes conditions, hello following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="a2f7b-284">함수</span><span class="sxs-lookup"><span data-stu-id="a2f7b-284">Function</span></span> | <span data-ttu-id="a2f7b-285">설명</span><span class="sxs-lookup"><span data-stu-id="a2f7b-285">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="a2f7b-286">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="a2f7b-286">AS_NUMBER</span></span> | <span data-ttu-id="a2f7b-287">Hello 입력된 문자열 tooa를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-287">Converts hello input string tooa number.</span></span> <span data-ttu-id="a2f7b-288">입력이 숫자이면 `noop`이고, 문자열이 숫자를 나타내지 않으면 `Undefined`입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-288">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="a2f7b-289">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="a2f7b-289">IS_ARRAY</span></span> | <span data-ttu-id="a2f7b-290">배열 hello hello 유형의 식을 지정 된 경우를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-290">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span> |
| <span data-ttu-id="a2f7b-291">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="a2f7b-291">IS_BOOL</span></span> | <span data-ttu-id="a2f7b-292">지정 된 식 hello hello 유형의 경우를 나타내는 부울 값은 부울을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-292">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span> |
| <span data-ttu-id="a2f7b-293">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="a2f7b-293">IS_DEFINED</span></span> | <span data-ttu-id="a2f7b-294">경우 hello 속성 값이 할당에 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-294">Returns a Boolean indicating if hello property has been assigned a value.</span></span> |
| <span data-ttu-id="a2f7b-295">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="a2f7b-295">IS_NULL</span></span> | <span data-ttu-id="a2f7b-296">지정 된 식 hello hello 유형의 경우를 나타내는 부울 값이 null을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-296">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span> |
| <span data-ttu-id="a2f7b-297">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="a2f7b-297">IS_NUMBER</span></span> | <span data-ttu-id="a2f7b-298">Hello hello 유형의 식을 지정 하는 경우 나타내는 부울 값은 숫자를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-298">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span> |
| <span data-ttu-id="a2f7b-299">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="a2f7b-299">IS_OBJECT</span></span> | <span data-ttu-id="a2f7b-300">지정 된 식 hello hello 유형의 경우를 나타내는 부울 값은 JSON 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-300">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span> |
| <span data-ttu-id="a2f7b-301">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="a2f7b-301">IS_PRIMITIVE</span></span> | <span data-ttu-id="a2f7b-302">Hello의 hello 형식이 지정 되는 기본 식을 나타내는 부울 값을 반환 합니다 (문자열, 부울, 숫자 또는 `null`).</span><span class="sxs-lookup"><span data-stu-id="a2f7b-302">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or `null`).</span></span> |
| <span data-ttu-id="a2f7b-303">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="a2f7b-303">IS_STRING</span></span> | <span data-ttu-id="a2f7b-304">Hello hello 유형의 식을 지정 하는 경우 나타내는 부울 값은 문자열로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-304">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span> |

<span data-ttu-id="a2f7b-305">경로 조건에서 다음 문자열 함수 hello 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-305">In routes conditions, hello following string functions are supported:</span></span>

| <span data-ttu-id="a2f7b-306">함수</span><span class="sxs-lookup"><span data-stu-id="a2f7b-306">Function</span></span> | <span data-ttu-id="a2f7b-307">설명</span><span class="sxs-lookup"><span data-stu-id="a2f7b-307">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="a2f7b-308">CONCAT(x, …)</span><span class="sxs-lookup"><span data-stu-id="a2f7b-308">CONCAT(x, …)</span></span> | <span data-ttu-id="a2f7b-309">않은 hello 두 개 이상의 문자열 값을 연결한 결과인 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-309">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="a2f7b-310">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="a2f7b-310">LENGTH(x)</span></span> | <span data-ttu-id="a2f7b-311">Hello의 문자 수를 반환 합니다 hello 지정 된 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-311">Returns hello number of characters of hello specified string expression.</span></span>|
| <span data-ttu-id="a2f7b-312">LOWER(x)</span><span class="sxs-lookup"><span data-stu-id="a2f7b-312">LOWER(x)</span></span> | <span data-ttu-id="a2f7b-313">대문자 데이터 toolowercase 변환한 후 문자열 식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-313">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| <span data-ttu-id="a2f7b-314">UPPER(x)</span><span class="sxs-lookup"><span data-stu-id="a2f7b-314">UPPER(x)</span></span> | <span data-ttu-id="a2f7b-315">소문자 데이터 toouppercase 변환한 후 문자열 식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-315">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| <span data-ttu-id="a2f7b-316">SUBSTRING(string, start [, length])</span><span class="sxs-lookup"><span data-stu-id="a2f7b-316">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="a2f7b-317">Hello에서 시작 하는 문자열 식의 반환 일부 문자 0부터 시작 위치를 지정 하 고 길이 또는 hello 문자열의 끝 toohello toohello 지정을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-317">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span> |
| <span data-ttu-id="a2f7b-318">INDEX_OF(string, fragment)</span><span class="sxs-lookup"><span data-stu-id="a2f7b-318">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="a2f7b-319">Hello hello 문자열을 찾을 수 없는 경우 시작 hello hello hello 첫 번째 지정 된 문자열 식 또는-1 내에서 두 번째 문자열 식의 첫 번째 발생 위치를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-319">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>|
| <span data-ttu-id="a2f7b-320">STARTS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="a2f7b-320">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="a2f7b-321">시작 하는지 여부를 첫 번째 문자열 식 hello hello 초를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-321">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span> |
| <span data-ttu-id="a2f7b-322">ENDS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="a2f7b-322">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="a2f7b-323">끝나는지 여부를 첫 번째 문자열 식 hello hello 초를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-323">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span> |
| <span data-ttu-id="a2f7b-324">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="a2f7b-324">CONTAINS(x,y)</span></span> | <span data-ttu-id="a2f7b-325">첫 번째 문자열 식 hello hello를 두 번째로 포함 되는지 여부를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-325">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a2f7b-326">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a2f7b-326">Next steps</span></span>
<span data-ttu-id="a2f7b-327">사용 하 여 앱의 tooexecute 쿼리 하는 방법에 대해 알아봅니다 [Azure IoT Sdk][lnk-hub-sdks]합니다.</span><span class="sxs-lookup"><span data-stu-id="a2f7b-327">Learn how tooexecute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

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

---
title: "Azure IoT Hub 쿼리 언어 | Microsoft Docs"
description: "개발자 가이드 - IoT Hub에서 장치 쌍 및 작업에 대한 정보를 검색하는 데 사용되는 SQL 유형의 IoT Hub 쿼리 언어에 대한 설명."
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
ms.openlocfilehash: a7650104eda58923558892f6f0f6666d16dbce28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a><span data-ttu-id="fe2ab-103">참조 - 장치 쌍, 작업 및 메시지 라우팅에 대한 IoT Hub 쿼리 언어</span><span class="sxs-lookup"><span data-stu-id="fe2ab-103">Reference - IoT Hub query language for device twins, jobs, and message routing</span></span>

<span data-ttu-id="fe2ab-104">IoT Hub는 [장치 쌍][lnk-twins] 및 [작업][lnk-jobs] 그리고 [메시지 라우팅][lnk-devguide-messaging-routes]과 관련된 정보를 검색할 수 있는 강력한 SQL 유형의 언어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-104">IoT Hub provides a powerful SQL-like language to retrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span></span> <span data-ttu-id="fe2ab-105">이 문서에 제공되는 내용:</span><span class="sxs-lookup"><span data-stu-id="fe2ab-105">This article presents:</span></span>

* <span data-ttu-id="fe2ab-106">IoT Hub 쿼리 언어의 주요 기능 소개 및</span><span class="sxs-lookup"><span data-stu-id="fe2ab-106">An introduction to the major features of the IoT Hub query language, and</span></span>
* <span data-ttu-id="fe2ab-107">언어에 대한 자세한 설명</span><span class="sxs-lookup"><span data-stu-id="fe2ab-107">The detailed description of the language.</span></span>

## <a name="get-started-with-device-twin-queries"></a><span data-ttu-id="fe2ab-108">장치 쌍 쿼리 시작</span><span class="sxs-lookup"><span data-stu-id="fe2ab-108">Get started with device twin queries</span></span>
<span data-ttu-id="fe2ab-109">[장치 쌍][lnk-twins]은 임의의 JSON 개체를 태그와 속성으로 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-109">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="fe2ab-110">IoT Hub를 사용하면 모든 장치 쌍 정보를 포함하는 단일 JSON 문서로 장치 쌍을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-110">IoT Hub enables you to query device twins as a single JSON document containing all device twin information.</span></span>
<span data-ttu-id="fe2ab-111">예를 들어 IoT Hub 장치 쌍에 다음과 같은 구조가 있다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-111">Assume, for instance, that your IoT hub device twins have the following structure:</span></span>

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

<span data-ttu-id="fe2ab-112">IoT Hub는 **devices**라는 문서 컬렉션으로 장치 쌍을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-112">IoT Hub exposes the device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="fe2ab-113">따라서 다음 쿼리는 전체적인 장치 쌍을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-113">So the following query retrieves the whole set of device twins:</span></span>

```sql
SELECT * FROM devices
```

> [!NOTE]
> <span data-ttu-id="fe2ab-114">[Azure IoT SDK][lnk-hub-sdks]는 큰 결과에 대한 페이징을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-114">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>

<span data-ttu-id="fe2ab-115">IoT Hub는 임의의 조건으로 장치 쌍 필터링을 검색하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-115">IoT Hub allows you to retrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="fe2ab-116">예를 들어</span><span class="sxs-lookup"><span data-stu-id="fe2ab-116">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

<span data-ttu-id="fe2ab-117">위 코드는 **location.region** 태그가 **US**로 설정된 장치 쌍을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-117">retrieves the device twins with the **location.region** tag set to **US**.</span></span>
<span data-ttu-id="fe2ab-118">예를 들어, 부울 연산자 및 산술 비교도 지원됩니다. 예를 들어</span><span class="sxs-lookup"><span data-stu-id="fe2ab-118">Boolean operators and arithmetic comparisons are supported as well, for example</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

<span data-ttu-id="fe2ab-119">위 코드는 미국 내에 있는 1분 이하의 간격으로 원격 분석을 보내도록 구성된 모든 장치 쌍을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-119">retrieves all device twins located in the US configured to send telemetry less often than every minute.</span></span> <span data-ttu-id="fe2ab-120">편의를 위해 **IN** 및**NIN**(IN이 아님) 연산자와 함께 배열 상수를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-120">As a convenience, it is also possible to use array constants with the **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="fe2ab-121">예를 들어</span><span class="sxs-lookup"><span data-stu-id="fe2ab-121">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

<span data-ttu-id="fe2ab-122">위 코드는 WiFi 또는 유선 연결을 보고한 모든 장치 쌍을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-122">retrieves all device twins that reported WiFi or wired connectivity.</span></span> <span data-ttu-id="fe2ab-123">특정 속성을 포함하는 모든 장치 쌍을 식별해야 하는 경우가 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-123">It is often necessary to identify all device twins that contain a specific property.</span></span> <span data-ttu-id="fe2ab-124">IoT Hub는 이러한 용도로 `is_defined()` 함수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-124">IoT Hub supports the function `is_defined()` for this purpose.</span></span> <span data-ttu-id="fe2ab-125">예를 들어</span><span class="sxs-lookup"><span data-stu-id="fe2ab-125">For instance,</span></span>

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

<span data-ttu-id="fe2ab-126">위 코드는 `connectivity` reported 속성을 정의하는 모든 장치 쌍을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-126">retrieved all device twins that define the `connectivity` reported property.</span></span> <span data-ttu-id="fe2ab-127">필터링 기능에 대한 전체 참조는 [WHERE 절][lnk-query-where] 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-127">Refer to the [WHERE clause][lnk-query-where] section for the full reference of the filtering capabilities.</span></span>

<span data-ttu-id="fe2ab-128">그룹화 및 집계도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-128">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="fe2ab-129">예를 들어</span><span class="sxs-lookup"><span data-stu-id="fe2ab-129">For instance,</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="fe2ab-130">위 코드는 원격 분석 구성 상태 각각의 장치 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-130">returns the count of the devices in each telemetry configuration status.</span></span>

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

<span data-ttu-id="fe2ab-131">위의 예제는 세 장치에서 성공적인 구성을 보고하고, 두 장치에서 아직 구성을 적용하고 있고, 한 장치에서 오류를 보고한 상황을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-131">The preceding example illustrates a situation where three devices reported successful configuration, two are still applying the configuration, and one reported an error.</span></span>

### <a name="c-example"></a><span data-ttu-id="fe2ab-132">C# 예제</span><span class="sxs-lookup"><span data-stu-id="fe2ab-132">C# example</span></span>
<span data-ttu-id="fe2ab-133">쿼리 기능은 [C# 서비스 SDK][lnk-hub-sdks]의 **RegistryManager** 클래스에서 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-133">The query functionality is exposed by the [C# service SDK][lnk-hub-sdks] in the **RegistryManager** class.</span></span>
<span data-ttu-id="fe2ab-134">다음은 간단한 예제 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-134">Here is an example of a simple query:</span></span>

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

<span data-ttu-id="fe2ab-135">**query** 개체가 페이지 크기(최대 1000)로 인스턴스화되는 방식과, **GetNextAsTwinAsync** 메서드를 여러 번 호출하여 여러 페이지를 가져오는 방식에 주목합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-135">Note how the **query** object is instantiated with a page size (up to 1000), and then multiple pages can be retrieved by calling the **GetNextAsTwinAsync** methods multiple times.</span></span>
<span data-ttu-id="fe2ab-136">쿼리 개체는 장치 쌍이나 작업 개체 또는 프로젝션을 사용할 때 사용되는 일반 JSON과 같은 쿼리에 필요한 역직렬화 옵션에 따라 여러 **Next\***를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-136">Note that the query object exposes multiple **Next\***, depending on the deserialization option required by the query, such as device twin or job objects, or plain JSON to be used when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="fe2ab-137">Node.js 예제</span><span class="sxs-lookup"><span data-stu-id="fe2ab-137">Node.js example</span></span>
<span data-ttu-id="fe2ab-138">쿼리 기능은 [Node.js용 Azure IoT 서비스 SDK][lnk-hub-sdks]의 **Registry** 개체에서 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-138">The query functionality is exposed by the [Azure IoT service SDK for Node.js][lnk-hub-sdks] in the **Registry** object.</span></span>
<span data-ttu-id="fe2ab-139">다음은 간단한 예제 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-139">Here is an example of a simple query:</span></span>

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed to fetch the results: ' + err.message);
    } else {
        // Do something with the results
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

<span data-ttu-id="fe2ab-140">**query** 개체가 페이지 크기(최대 1000)로 인스턴스화되는 방식과, **nextAsTwin** 메서드를 여러 번 호출하여 여러 페이지를 가져오는 방식에 주목합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-140">Note how the **query** object is instantiated with a page size (up to 1000), and then multiple pages can be retrieved by calling the **nextAsTwin** methods multiple times.</span></span>
<span data-ttu-id="fe2ab-141">쿼리 개체는 장치 쌍이나 작업 개체 또는 프로젝션을 사용할 때 사용되는 일반 JSON과 같은 쿼리에 필요한 역직렬화 옵션에 따라 여러 **next\***를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-141">Note that the query object exposes multiple **next\***, depending on the deserialization option required by the query, such as device twin or job objects, or plain JSON to be used when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="fe2ab-142">제한 사항</span><span class="sxs-lookup"><span data-stu-id="fe2ab-142">Limitations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fe2ab-143">쿼리 결과는 장치 쌍의 최신 값에 따라 몇 분 정도 지연될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-143">Query results can have a few minutes of delay with respect to the latest values in device twins.</span></span> <span data-ttu-id="fe2ab-144">ID별로 개별 장치 쌍을 쿼리하는 경우 항상 최신 값을 포함하며 더 높은 조정 제한을 가지는 장치 쌍 검색 API를 사용하는 것이 항상 바람직합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-144">If querying individual device twins by id, it is always preferable to use the retrieve device twin API, which always contains the latest values and has higher throttling limits.</span></span>

<span data-ttu-id="fe2ab-145">현재 비교는 기본 형식(개체 없음) 간에만 지원됩니다. 예를 들어 `... WHERE properties.desired.config = properties.reported.config`는 해당 속성에 기본 값이 있는 경우에만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-145">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="fe2ab-146">작업 쿼리 시작</span><span class="sxs-lookup"><span data-stu-id="fe2ab-146">Get started with jobs queries</span></span>
<span data-ttu-id="fe2ab-147">[작업][lnk-jobs]은 장치 집합에 대해 작업을 실행하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-147">[Jobs][lnk-jobs] provide a way to execute operations on sets of devices.</span></span> <span data-ttu-id="fe2ab-148">각 장치 쌍은 작업에 대한 정보를 포함하며 이것은 **jobs**라는 컬렉션에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-148">Each device twin contains the information of the jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="fe2ab-149">로컬에서,</span><span class="sxs-lookup"><span data-stu-id="fe2ab-149">Logically,</span></span>

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

<span data-ttu-id="fe2ab-150">현재 이 컬렉션은 IoT Hub 쿼리 언어를 사용하여 **devices.jobs**로 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-150">Currently, this collection is queryable as **devices.jobs** in the IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe2ab-151">현재 장치 쌍을 쿼리할 때(예: 'FROM devices'가 포함된 쿼리) jobs 속성이 반환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-151">Currently, the jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span></span> <span data-ttu-id="fe2ab-152">`FROM devices.jobs`를 사용하여 쿼리를 통해서만 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-152">It can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="fe2ab-153">예를 들어 단일 장치에 영향을 미치는 모든 작업(지난 작업 및 예정된 작업)을 가져오려면 다음 쿼리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-153">For instance, to get all jobs (past and scheduled) that affect a single device, you can use the following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

<span data-ttu-id="fe2ab-154">이 쿼리가 반환된 각 작업의 장치별 상태(및 가능한 경우 직접 메서드 응답)를 제공하는 방법에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-154">Note how this query provides the device-specific status (and possibly the direct method response) of each job returned.</span></span>
<span data-ttu-id="fe2ab-155">**devices.jobs** 컬렉션의 모든 개체 속성에 대해 임의의 부울 조건으로 필터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-155">It is also possible to filter with arbitrary Boolean conditions on all object properties in the **devices.jobs** collection.</span></span>
<span data-ttu-id="fe2ab-156">예를 들어, 다음 쿼리는:</span><span class="sxs-lookup"><span data-stu-id="fe2ab-156">For instance, the following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

<span data-ttu-id="fe2ab-157">2016년 9월 이후에 생성된 장치 **myDeviceId**에 대해 완료된 모든 장치 쌍 업데이트 작업을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-157">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span></span>

<span data-ttu-id="fe2ab-158">단일 작업의 장치별 출력을 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-158">It is also possible to retrieve the per-device outcomes of a single job.</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a><span data-ttu-id="fe2ab-159">제한 사항</span><span class="sxs-lookup"><span data-stu-id="fe2ab-159">Limitations</span></span>
<span data-ttu-id="fe2ab-160">현재 **devices.jobs**에 대한 쿼리는 다음을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-160">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="fe2ab-161">프로젝션(따라서 `SELECT *`만 가능)</span><span class="sxs-lookup"><span data-stu-id="fe2ab-161">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="fe2ab-162">작업 속성 외에 장치 쌍을 참조하는 조건(앞 섹션 참조)</span><span class="sxs-lookup"><span data-stu-id="fe2ab-162">Conditions that refer to the device twin in addition to job properties (see the preceding section).</span></span>
* <span data-ttu-id="fe2ab-163">집계 수행(예: count, avg, group by)</span><span class="sxs-lookup"><span data-stu-id="fe2ab-163">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="fe2ab-164">장치-클라우드 메시지 경로에 대한 쿼리 식 시작</span><span class="sxs-lookup"><span data-stu-id="fe2ab-164">Get started with device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="fe2ab-165">[장치-클라우드 경로][lnk-devguide-messaging-routes]를 사용하면 개별 메시지에 대해 평가된 식에 따라 장치-클라우드 메시지를 다른 끝점으로 전달하도록 IoT Hub를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-165">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub to dispatch device-to-cloud messages to different endpoints based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="fe2ab-166">경로 [조건][lnk-query-expressions]은 쌍 및 작업 쿼리의 조건과 동일한 IoT Hub 쿼리 언어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-166">The route [condition][lnk-query-expressions] uses the same IoT Hub query language as conditions in twin and job queries.</span></span> <span data-ttu-id="fe2ab-167">메시지 헤더 및 본문에서 경로 조건이 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-167">Route conditions are evaluated on the message headers and body.</span></span> <span data-ttu-id="fe2ab-168">라우팅 쿼리 식에 메시지 본문 헤더만 포함될 수도 있고, 메시지 본문만 포함될 수도 있고, 메시지 헤더와 메시지 본문이 모두 포함될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-168">Your routing query expression may involve only message headers, only the message body, or both message headers and message body.</span></span> <span data-ttu-id="fe2ab-169">IoT Hub는 메시지를 전달하기 위해 헤더와 메시지 본문에 대한 특정 스키마를 가정하며, 다음 섹션에서는 IoT Hub가 적절히 라우팅하려면 무엇이 필요한지 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-169">IoT Hub assumes a specific schema for the headers and message body in order to route messages, and the following sections describe what is required for IoT Hub to properly route:</span></span>

### <a name="routing-on-message-headers"></a><span data-ttu-id="fe2ab-170">메시지 헤더에서 라우팅</span><span class="sxs-lookup"><span data-stu-id="fe2ab-170">Routing on message headers</span></span>

<span data-ttu-id="fe2ab-171">IoT Hub는 메시지 라우팅에 대해 메시지 헤더의 다음 JSON 표현을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-171">IoT Hub assumes the following JSON representation of message headers for message routing:</span></span>

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

<span data-ttu-id="fe2ab-172">메시지 시스템 속성 앞에 `'$'` 기호를 붙입니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-172">Message system properties are prefixed with the `'$'` symbol.</span></span>
<span data-ttu-id="fe2ab-173">사용자 속성은 항상 이름을 사용하여 액세스됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-173">User properties are always accessed with their name.</span></span> <span data-ttu-id="fe2ab-174">사용자 속성 이름이 시스템 속성과 일치하는 것으로 나타나면(예: `$to`) 사용자 속성을 `$to` 식을 사용하여 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-174">If a user property name happens to coincide with a system property (such as `$to`), the user property will be retrieved with the `$to` expression.</span></span>
<span data-ttu-id="fe2ab-175">항상 괄호 `{}`를 사용하여 시스템 속성에 액세스할 수 있습니다. 예를 들어 식 `{$to}`를 사용하여 시스템 속성 `to`에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-175">You can always access the system property using brackets `{}`: for instance, you can use the expression `{$to}` to access the system property `to`.</span></span> <span data-ttu-id="fe2ab-176">속성 이름을 대괄호로 묶으면 항상 해당 시스템 속성이 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-176">Bracketed property names always retrieve the corresponding system property.</span></span>

<span data-ttu-id="fe2ab-177">속성 이름은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-177">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="fe2ab-178">모든 메시지 속성은 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-178">All message properties are strings.</span></span> <span data-ttu-id="fe2ab-179">[개발자 가이드][lnk-devguide-messaging-format]에서 설명한 대로 시스템 속성은 현재 쿼리에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-179">System properties, as described in the [developer guide][lnk-devguide-messaging-format], are currently not available to use in queries.</span></span>
>

<span data-ttu-id="fe2ab-180">예를 들어 `messageType` 속성을 사용하는 경우 모든 원격 분석을 하나의 끝점으로 라우팅하고, 모든 경고를 다른 끝점으로 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-180">For example, if you use a `messageType` property, you might want to route all telemetry to one endpoint, and all alerts to another endpoint.</span></span> <span data-ttu-id="fe2ab-181">다음 식을 작성하면 원격 분석을 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-181">You can write the following expression to route the telemetry:</span></span>

```sql
messageType = 'telemetry'
```

<span data-ttu-id="fe2ab-182">그리고 다음 식으로 경고 메시지를 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-182">And the following expression to route the alert messages:</span></span>

```sql
messageType = 'alert'
```

<span data-ttu-id="fe2ab-183">부울 식 및 함수도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-183">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="fe2ab-184">이 기능을 사용하면 심각도 수준을 구분할 수 있습니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-184">This feature enables you to distinguish between severity level, for example:</span></span>

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

<span data-ttu-id="fe2ab-185">지원되는 연산자와 함수의 전체 목록은 [식 및 조건][lnk-query-expressions] 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-185">Refer to the [Expression and conditions][lnk-query-expressions] section for the full list of supported operators and functions.</span></span>

### <a name="routing-on-message-bodies"></a><span data-ttu-id="fe2ab-186">메시지 본문에서 라우팅</span><span class="sxs-lookup"><span data-stu-id="fe2ab-186">Routing on message bodies</span></span>

<span data-ttu-id="fe2ab-187">메시지 본문이 UTF-8, UTF-16 또는 UTF-32로 적절하게 인코딩된 JSON 형식이어야 IoT Hub가 메시지 본문 콘텐츠를 기반으로 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-187">IoT Hub can only route based on message body contents if the message body is properly formed JSON encoded in either UTF-8, UTF-16, or UTF-32.</span></span> <span data-ttu-id="fe2ab-188">IoT Hub가 본문 내용을 기반으로 메시지를 라우팅할 수 있도록 메시지의 콘텐츠 유형을 `application/json`으로 설정하고 콘텐츠 인코딩을 메시지 헤더에서 지원되는 UTF 인코딩 중 하나로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-188">You must set the content type of the message to `application/json` and the content encoding to one of the supported UTF encodings in the message headers to allow IoT Hub to route the message based on the body contents.</span></span> <span data-ttu-id="fe2ab-189">헤더 중 하나를 지정하지 않으면 IoT Hub는 메시지에 대한 본문과 관련된 쿼리 식을 평가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-189">If either of the headers is not specified, IoT Hub will not attempt to evaluate any query expression involving the body against the message.</span></span> <span data-ttu-id="fe2ab-190">메시지가 JSON 메시지가 아니거나 메시지에서 콘텐츠 유형 및 콘텐츠 인코딩을 지정하지 않더라도 여전히 메시지 라우팅을 사용하여 메시지 헤더를 기반으로 메시지를 라우팅할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-190">If your message is not a JSON message, or if the message does not specify the content type and content encoding, you may still use message routing to route the message based on the message headers.</span></span>

<span data-ttu-id="fe2ab-191">쿼리 식에 `$body`를 사용하여 메시지를 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-191">You can use `$body` in the query expression to route the message.</span></span> <span data-ttu-id="fe2ab-192">쿼리 식에 간단한 본문 참조, 본문 배열 참조 또는 여러 본문 참조를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-192">You can use a simple body reference, body array reference, or multiple body references in the query expression.</span></span> <span data-ttu-id="fe2ab-193">쿼리 식에서 본문 참조를 메시지 헤더 참조와 결합할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-193">Your query expression can also combine a body reference with a message header reference.</span></span> <span data-ttu-id="fe2ab-194">예를 들어 다음은 모든 유효한 쿼리 식입니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-194">For example, the following are all valid query expressions:</span></span>

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="fe2ab-195">IoT Hub 쿼리의 기초</span><span class="sxs-lookup"><span data-stu-id="fe2ab-195">Basics of an IoT Hub query</span></span>
<span data-ttu-id="fe2ab-196">모든 IoT Hub 쿼리는 SELECT 및 FROM 절로 이루어지며 선택적으로 WHERE 및 GROUP BY 절을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-196">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="fe2ab-197">모든 쿼리는 JSON 문서(예: 장치 쌍) 컬렉션에 대해 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-197">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="fe2ab-198">FROM 절은 반복이 수행될 문서 컬렉션을 나타냅니다(예: **devices** 또는 **devices.jobs**).</span><span class="sxs-lookup"><span data-stu-id="fe2ab-198">The FROM clause indicates the document collection to be iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="fe2ab-199">그런 다음 WHERE 절의 필터가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-199">Then, the filter in the WHERE clause is applied.</span></span> <span data-ttu-id="fe2ab-200">집계를 사용하면 이 단계의 결과가 GROUP BY 절에 지정된 대로 그룹화되며, 각 그룹에 대해서는 SELECT 절에 지정된 대로 행이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-200">With aggregations, the results of this step are grouped as specified in the GROUP BY clause and, for each group, a row is generated as specified in the SELECT clause.</span></span>

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a><span data-ttu-id="fe2ab-201">FROM 절</span><span class="sxs-lookup"><span data-stu-id="fe2ab-201">FROM clause</span></span>
<span data-ttu-id="fe2ab-202">**FROM <from_specification>** 절은 두 가지 값만 가정할 수 있습니다. **FROM devices**는 장치 쌍을 쿼리하기 위해 **FROM devices.jobs**는 장치별 작업 세부 정보를 쿼리하기 위해 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-202">The **FROM <from_specification>** clause can assume only two values: **FROM devices**, to query device twins, or **FROM devices.jobs**, to query job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="fe2ab-203">WHERE 절</span><span class="sxs-lookup"><span data-stu-id="fe2ab-203">WHERE clause</span></span>
<span data-ttu-id="fe2ab-204">**WHERE <filter_condition>** 절은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-204">The **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="fe2ab-205">FROM 컬렉션의 JSON 문서가 결과의 일부로 포함되기 위해 충족해야 하는 하나 이상의 조건을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-205">It specifies one or more conditions that the JSON documents in the FROM collection must satisfy to be included as part of the result.</span></span> <span data-ttu-id="fe2ab-206">JSON 문서가 결과에 포함되려면 지정된 조건을 "true"로 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-206">Any JSON document must evaluate the specified conditions to "true" to be included in the result.</span></span>

<span data-ttu-id="fe2ab-207">허용되는 조건은 [식 및 조건][lnk-query-expressions] 섹션에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-207">The allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="fe2ab-208">SELECT 절</span><span class="sxs-lookup"><span data-stu-id="fe2ab-208">SELECT clause</span></span>
<span data-ttu-id="fe2ab-209">SELECT 절(**SELECT <select_list>**)은 필수이며 쿼리에서 검색되는 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-209">The SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from the query.</span></span> <span data-ttu-id="fe2ab-210">새 JSON 개체를 생성하는 데 사용될 JSON 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-210">It specifies the JSON values to be used to generate new JSON objects.</span></span>
<span data-ttu-id="fe2ab-211">FROM 컬렉션의 필터링된(그리고 선택적으로 그룹화된) 하위 집합의 각 요소에 대해 프로젝션 단계는 SELECT 절에 지정된 값으로 구성된 새 JSON 개체를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-211">For each element of the filtered (and optionally grouped) subset of the FROM collection, the projection phase generates a new JSON object, constructed with the values specified in the SELECT clause.</span></span>

<span data-ttu-id="fe2ab-212">다음은 SELECT 절의 문법입니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-212">Following is the grammar of the SELECT clause:</span></span>

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

<span data-ttu-id="fe2ab-213">**attribute_name**은 FROM 컬렉션에 있는 JSON 문서의 속성을 말합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-213">where **attribute_name** refers to any property of the JSON document in the FROM collection.</span></span> <span data-ttu-id="fe2ab-214">SELECT 절에 대한 예제는 [장치 쌍 쿼리 시작][lnk-query-getstarted] 섹션에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-214">Some examples of SELECT clauses can be found in the [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="fe2ab-215">현재 **SELECT \***와 다른 선택 절은 장치 쌍에 대한 집계 쿼리에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-215">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="fe2ab-216">GROUP BY 절</span><span class="sxs-lookup"><span data-stu-id="fe2ab-216">GROUP BY clause</span></span>
<span data-ttu-id="fe2ab-217">**GROUP BY <group_specification>** 절은 WHERE 절에 지정된 필터 뒤에서, 그리고 SELECT에 지정된 프로젝션 앞에서 실행될 수 있는 선택적 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-217">The **GROUP BY <group_specification>** clause is an optional step that can be executed after the filter specified in the WHERE clause, and before the projection specified in the SELECT.</span></span> <span data-ttu-id="fe2ab-218">특성의 값을 기반으로 문서를 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-218">It groups documents based on the value of an attribute.</span></span> <span data-ttu-id="fe2ab-219">이러한 그룹은 SELECT 절에 지정된 대로 집계된 값을 생성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-219">These groups are used to generate aggregated values as specified in the SELECT clause.</span></span>

<span data-ttu-id="fe2ab-220">GROUP BY를 사용한 쿼리의 예:</span><span class="sxs-lookup"><span data-stu-id="fe2ab-220">An example of a query using GROUP BY is:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="fe2ab-221">GROUP BY에 대한 형식 구문:</span><span class="sxs-lookup"><span data-stu-id="fe2ab-221">The formal syntax for GROUP BY is:</span></span>

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

<span data-ttu-id="fe2ab-222">**attribute_name**은 FROM 컬렉션에 있는 JSON 문서의 속성을 말합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-222">where **attribute_name** refers to any property of the JSON document in the FROM collection.</span></span>

<span data-ttu-id="fe2ab-223">현재 GROUP BY 절은 장치 쌍을 쿼리하는 경우에만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-223">Currently, the GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="fe2ab-224">식 및 조건</span><span class="sxs-lookup"><span data-stu-id="fe2ab-224">Expressions and conditions</span></span>
<span data-ttu-id="fe2ab-225">높은 수준에서 *식*은:</span><span class="sxs-lookup"><span data-stu-id="fe2ab-225">At a high level, an *expression*:</span></span>

* <span data-ttu-id="fe2ab-226">JSON 형식(예: 부울, 숫자, 문자열, 배열 또는 개체)의 인스턴스로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-226">Evaluates to an instance of a JSON type (such as Boolean, number, string, array, or object), and</span></span>
* <span data-ttu-id="fe2ab-227">기본 제공되는 연산자와 함수를 사용하여 상수 및 장치 JSON 문서에서 오는 조작 데이터에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-227">Is defined by manipulating data coming from the device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="fe2ab-228">*조건*은 부울 값으로 평가되는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-228">*Conditions* are expressions that evaluate to a Boolean.</span></span> <span data-ttu-id="fe2ab-229">부울 **true**와 다른 모든 상수는 **false**로 간주됩니다(**null**, **undefined**, 모든 개체 또는 배열 인스턴스, 모든 문자열 및 명확한 부울 **false** 포함).</span><span class="sxs-lookup"><span data-stu-id="fe2ab-229">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly the Boolean **false**).</span></span>

<span data-ttu-id="fe2ab-230">식에 대한 구문:</span><span class="sxs-lookup"><span data-stu-id="fe2ab-230">The syntax for expressions is:</span></span>

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

<span data-ttu-id="fe2ab-231">설명:</span><span class="sxs-lookup"><span data-stu-id="fe2ab-231">where:</span></span>

| <span data-ttu-id="fe2ab-232">기호</span><span class="sxs-lookup"><span data-stu-id="fe2ab-232">Symbol</span></span> | <span data-ttu-id="fe2ab-233">정의</span><span class="sxs-lookup"><span data-stu-id="fe2ab-233">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="fe2ab-234">attribute_name</span><span class="sxs-lookup"><span data-stu-id="fe2ab-234">attribute_name</span></span> | <span data-ttu-id="fe2ab-235">**FROM** 컬렉션에 있는 JSON 문서의 모든 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-235">Any property of the JSON document in the **FROM** collection.</span></span> |
| <span data-ttu-id="fe2ab-236">binary_operator</span><span class="sxs-lookup"><span data-stu-id="fe2ab-236">binary_operator</span></span> | <span data-ttu-id="fe2ab-237">[연산자](#operators) 섹션에서 나열한 모든 이항 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-237">Any binary operator listed in the [Operators](#operators) section.</span></span> |
| <span data-ttu-id="fe2ab-238">function_name</span><span class="sxs-lookup"><span data-stu-id="fe2ab-238">function_name</span></span>| <span data-ttu-id="fe2ab-239">[함수](#functions) 섹션에서 나열한 모든 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-239">Any function listed in the [Functions](#functions) section.</span></span> |
| <span data-ttu-id="fe2ab-240">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="fe2ab-240">decimal_literal</span></span> |<span data-ttu-id="fe2ab-241">소수 표기법으로 표현되는 부동 float입니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-241">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="fe2ab-242">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="fe2ab-242">hexadecimal_literal</span></span> |<span data-ttu-id="fe2ab-243">뒤에 16진수 문자열이 붙는 ‘0x’ 문자열로 표현되는 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-243">A number expressed by the string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="fe2ab-244">string_literal</span><span class="sxs-lookup"><span data-stu-id="fe2ab-244">string_literal</span></span> |<span data-ttu-id="fe2ab-245">문자열 리터럴은 연속적인 0이상의 유니코드 문자 또는 이스케이프 시퀀스로 표현되는 유니코드 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-245">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="fe2ab-246">문자열 리터럴은 작은따옴표(아포스트로피: ') 또는 큰따옴표(따옴표: ")로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-246">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span> <span data-ttu-id="fe2ab-247">허용되는 이스케이프: `\'`, `\"`, `\\`, 4개의 16진수로 정의되는 유니코드 문자인 경우 `\uXXXX`</span><span class="sxs-lookup"><span data-stu-id="fe2ab-247">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="fe2ab-248">연산자</span><span class="sxs-lookup"><span data-stu-id="fe2ab-248">Operators</span></span>
<span data-ttu-id="fe2ab-249">다음과 같은 연산자가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-249">The following operators are supported:</span></span>

| <span data-ttu-id="fe2ab-250">패밀리</span><span class="sxs-lookup"><span data-stu-id="fe2ab-250">Family</span></span> | <span data-ttu-id="fe2ab-251">연산자</span><span class="sxs-lookup"><span data-stu-id="fe2ab-251">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="fe2ab-252">산술</span><span class="sxs-lookup"><span data-stu-id="fe2ab-252">Arithmetic</span></span> |<span data-ttu-id="fe2ab-253">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="fe2ab-253">+,-,*,/,%</span></span> |
| <span data-ttu-id="fe2ab-254">논리</span><span class="sxs-lookup"><span data-stu-id="fe2ab-254">Logical</span></span> |<span data-ttu-id="fe2ab-255">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="fe2ab-255">AND, OR, NOT</span></span> |
| <span data-ttu-id="fe2ab-256">비교</span><span class="sxs-lookup"><span data-stu-id="fe2ab-256">Comparison</span></span> |<span data-ttu-id="fe2ab-257">=, !=, <, >, <=, >=, <></span><span class="sxs-lookup"><span data-stu-id="fe2ab-257">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="fe2ab-258">함수</span><span class="sxs-lookup"><span data-stu-id="fe2ab-258">Functions</span></span>
<span data-ttu-id="fe2ab-259">쌍과 작업을 쿼리할 때 지원되는 유일한 함수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-259">When querying twins and jobs the only supported function is:</span></span>

| <span data-ttu-id="fe2ab-260">함수</span><span class="sxs-lookup"><span data-stu-id="fe2ab-260">Function</span></span> | <span data-ttu-id="fe2ab-261">설명</span><span class="sxs-lookup"><span data-stu-id="fe2ab-261">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="fe2ab-262">IS_DEFINED(속성)</span><span class="sxs-lookup"><span data-stu-id="fe2ab-262">IS_DEFINED(property)</span></span> | <span data-ttu-id="fe2ab-263">속성에 값(`null` 포함)이 할당되었는지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-263">Returns a Boolean indicating if the property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="fe2ab-264">경로 조건에서 지원되는 수학 함수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-264">In routes conditions, the following math functions are supported:</span></span>

| <span data-ttu-id="fe2ab-265">함수</span><span class="sxs-lookup"><span data-stu-id="fe2ab-265">Function</span></span> | <span data-ttu-id="fe2ab-266">설명</span><span class="sxs-lookup"><span data-stu-id="fe2ab-266">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="fe2ab-267">ABS(x)</span><span class="sxs-lookup"><span data-stu-id="fe2ab-267">ABS(x)</span></span> | <span data-ttu-id="fe2ab-268">지정한 숫자 식의 절대(양수) 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-268">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| <span data-ttu-id="fe2ab-269">EXP(x)</span><span class="sxs-lookup"><span data-stu-id="fe2ab-269">EXP(x)</span></span> | <span data-ttu-id="fe2ab-270">지정한 숫자 식(e^x)의 지수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-270">Returns the exponential value of the specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="fe2ab-271">POWER(x,y)</span><span class="sxs-lookup"><span data-stu-id="fe2ab-271">POWER(x,y)</span></span> | <span data-ttu-id="fe2ab-272">지정한 식의 값을 지정한 거듭제곱(x^y)으로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-272">Returns the value of the specified expression to the specified power (x^y).</span></span>|
| <span data-ttu-id="fe2ab-273">SQUARE(x)</span><span class="sxs-lookup"><span data-stu-id="fe2ab-273">SQUARE(x)</span></span> | <span data-ttu-id="fe2ab-274">지정한 숫자 값의 제곱을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-274">Returns the square of the specified numeric value.</span></span> |
| <span data-ttu-id="fe2ab-275">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="fe2ab-275">CEILING(x)</span></span> | <span data-ttu-id="fe2ab-276">지정한 숫자 식보다 크거나 같은 가장 작은 정수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-276">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| <span data-ttu-id="fe2ab-277">FLOOR(x)</span><span class="sxs-lookup"><span data-stu-id="fe2ab-277">FLOOR(x)</span></span> | <span data-ttu-id="fe2ab-278">지정한 숫자 식보다 작거나 같은 가장 큰 정수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-278">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| <span data-ttu-id="fe2ab-279">SIGN(x)</span><span class="sxs-lookup"><span data-stu-id="fe2ab-279">SIGN(x)</span></span> | <span data-ttu-id="fe2ab-280">지정한 숫자 식의 양수(+1), 0(0) 또는 음수(-1) 부호를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-280">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span></span>|
| <span data-ttu-id="fe2ab-281">SQRT(x)</span><span class="sxs-lookup"><span data-stu-id="fe2ab-281">SQRT(x)</span></span> | <span data-ttu-id="fe2ab-282">지정한 숫자 값의 제곱을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-282">Returns the square of the specified numeric value.</span></span> |

<span data-ttu-id="fe2ab-283">경로 조건에서 지원되는 형식 검사 및 캐스팅 함수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-283">In routes conditions, the following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="fe2ab-284">함수</span><span class="sxs-lookup"><span data-stu-id="fe2ab-284">Function</span></span> | <span data-ttu-id="fe2ab-285">설명</span><span class="sxs-lookup"><span data-stu-id="fe2ab-285">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="fe2ab-286">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="fe2ab-286">AS_NUMBER</span></span> | <span data-ttu-id="fe2ab-287">입력 문자열을 숫자로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-287">Converts the input string to a number.</span></span> <span data-ttu-id="fe2ab-288">입력이 숫자이면 `noop`이고, 문자열이 숫자를 나타내지 않으면 `Undefined`입니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-288">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="fe2ab-289">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="fe2ab-289">IS_ARRAY</span></span> | <span data-ttu-id="fe2ab-290">지정한 식의 형식이 배열인지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-290">Returns a Boolean value indicating if the type of the specified expression is an array.</span></span> |
| <span data-ttu-id="fe2ab-291">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="fe2ab-291">IS_BOOL</span></span> | <span data-ttu-id="fe2ab-292">지정한 식의 형식이 부울인지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-292">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span></span> |
| <span data-ttu-id="fe2ab-293">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="fe2ab-293">IS_DEFINED</span></span> | <span data-ttu-id="fe2ab-294">속성이 값을 할당할지를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-294">Returns a Boolean indicating if the property has been assigned a value.</span></span> |
| <span data-ttu-id="fe2ab-295">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="fe2ab-295">IS_NULL</span></span> | <span data-ttu-id="fe2ab-296">지정한 식의 형식이 널인지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-296">Returns a Boolean value indicating if the type of the specified expression is null.</span></span> |
| <span data-ttu-id="fe2ab-297">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="fe2ab-297">IS_NUMBER</span></span> | <span data-ttu-id="fe2ab-298">지정한 식의 형식이 숫자인지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-298">Returns a Boolean value indicating if the type of the specified expression is a number.</span></span> |
| <span data-ttu-id="fe2ab-299">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="fe2ab-299">IS_OBJECT</span></span> | <span data-ttu-id="fe2ab-300">지정한 식의 형식이 JSON 개체인지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-300">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span></span> |
| <span data-ttu-id="fe2ab-301">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="fe2ab-301">IS_PRIMITIVE</span></span> | <span data-ttu-id="fe2ab-302">지정한 식의 형식이 기본 형식(문자열, 부울, 숫자 또는 `null`)인지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-302">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or `null`).</span></span> |
| <span data-ttu-id="fe2ab-303">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="fe2ab-303">IS_STRING</span></span> | <span data-ttu-id="fe2ab-304">지정한 식의 형식이 문자열인지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-304">Returns a Boolean value indicating if the type of the specified expression is a string.</span></span> |

<span data-ttu-id="fe2ab-305">경로 조건에서 지원되는 문자열 함수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-305">In routes conditions, the following string functions are supported:</span></span>

| <span data-ttu-id="fe2ab-306">함수</span><span class="sxs-lookup"><span data-stu-id="fe2ab-306">Function</span></span> | <span data-ttu-id="fe2ab-307">설명</span><span class="sxs-lookup"><span data-stu-id="fe2ab-307">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="fe2ab-308">CONCAT(x, …)</span><span class="sxs-lookup"><span data-stu-id="fe2ab-308">CONCAT(x, …)</span></span> | <span data-ttu-id="fe2ab-309">둘 이상의 문자열 값을 연결한 결과인 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-309">Returns a string that is the result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="fe2ab-310">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="fe2ab-310">LENGTH(x)</span></span> | <span data-ttu-id="fe2ab-311">지정한 문자열 식의 문자 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-311">Returns the number of characters of the specified string expression.</span></span>|
| <span data-ttu-id="fe2ab-312">LOWER(x)</span><span class="sxs-lookup"><span data-stu-id="fe2ab-312">LOWER(x)</span></span> | <span data-ttu-id="fe2ab-313">대문자 데이터를 소문자로 변환한 후에 문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-313">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| <span data-ttu-id="fe2ab-314">UPPER(x)</span><span class="sxs-lookup"><span data-stu-id="fe2ab-314">UPPER(x)</span></span> | <span data-ttu-id="fe2ab-315">소문자 데이터를 대문자로 변환한 후에 문자열 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-315">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| <span data-ttu-id="fe2ab-316">SUBSTRING(string, start [, length])</span><span class="sxs-lookup"><span data-stu-id="fe2ab-316">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="fe2ab-317">지정한 문자 0 기준 위치에서 시작하여 지정한 길이 또는 문자열의 끝까지에 이르는 문자열 식의 일부를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-317">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span></span> |
| <span data-ttu-id="fe2ab-318">INDEX_OF(string, fragment)</span><span class="sxs-lookup"><span data-stu-id="fe2ab-318">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="fe2ab-319">지정된 첫 번째 문자열 식 내의 두 번째 문자열 식에서 첫 번째로 나타나는 시작 위치를 반환하거나 문자열을 찾을 수 없는 경우 -1을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-319">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span>|
| <span data-ttu-id="fe2ab-320">STARTS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="fe2ab-320">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="fe2ab-321">첫 번째 문자열 식이 두 번째 문자열 식에서 시작하는지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-321">Returns a Boolean indicating whether the first string expression starts with the second.</span></span> |
| <span data-ttu-id="fe2ab-322">ENDS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="fe2ab-322">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="fe2ab-323">첫 번째 문자열 식이 두 번째 문자열 식에서 끝나는지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-323">Returns a Boolean indicating whether the first string expression ends with the second.</span></span> |
| <span data-ttu-id="fe2ab-324">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="fe2ab-324">CONTAINS(x,y)</span></span> | <span data-ttu-id="fe2ab-325">첫번째 문자열 식이 두 번째를 포함하는지를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-325">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fe2ab-326">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fe2ab-326">Next steps</span></span>
<span data-ttu-id="fe2ab-327">[Azure IoT SDK][lnk-hub-sdks]를 사용하여 앱에서 쿼리를 수행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fe2ab-327">Learn how to execute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

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

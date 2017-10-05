---
title: "Azure IoT Hub 장치 쌍 이해 | Microsoft Docs"
description: "개발자 가이드 - 장치 쌍을 사용하여 IoT Hub와 장치 간의 상태 및 구성 데이터 동기화"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 8a3da072-a5bf-46e5-8de4-24cdbb2a03fa
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b316aa419d558547f90a914a22fb29935076de21
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a><span data-ttu-id="12265-103">IoT Hub의 장치 쌍 이해 및 사용</span><span class="sxs-lookup"><span data-stu-id="12265-103">Understand and use device twins in IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="12265-104">개요</span><span class="sxs-lookup"><span data-stu-id="12265-104">Overview</span></span>
<span data-ttu-id="12265-105">*장치 쌍*은 장치 상태 정보(메타데이터, 구성 및 조건)를 저장하는 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="12265-105">*Device twins* are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="12265-106">IoT Hub는 IoT Hub에 연결하는 각 장치에 대해 하나의 장치 쌍을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-106">IoT Hub persists a device twin for each device that you connect to IoT Hub.</span></span> <span data-ttu-id="12265-107">이 문서에서는 다음을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-107">This article describes:</span></span>

* <span data-ttu-id="12265-108">장치 쌍의 구조 즉, *태그*, *desired* 및 *reported 속성*</span><span class="sxs-lookup"><span data-stu-id="12265-108">The structure of the device twin: *tags*, *desired* and *reported properties*, and</span></span>
* <span data-ttu-id="12265-109">장치 앱과 백 엔드가 장치 쌍에 수행할 수 있는 작업</span><span class="sxs-lookup"><span data-stu-id="12265-109">The operations that device apps and back ends can perform on device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="12265-110">현재 장치 쌍은 MQTT 프로토콜을 사용하여 IoT Hub에 연결하는 장치에서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-110">Currently, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="12265-111">기존 장치 앱이 MQTT를 사용하도록 변환하는 방법에 관한 설명은 [MQTT 지원][lnk-devguide-mqtt] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12265-111">Refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>
> 
> 

### <a name="when-to-use"></a><span data-ttu-id="12265-112">사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="12265-112">When to use</span></span>
<span data-ttu-id="12265-113">장치 쌍의 용도:</span><span class="sxs-lookup"><span data-stu-id="12265-113">Use device twins to:</span></span>

* <span data-ttu-id="12265-114">클라우드에서 장치 전용 메타데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-114">Store device-specific metadata in the cloud.</span></span> <span data-ttu-id="12265-115">예를 들어 자동 판매기의 배포 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="12265-115">For example, the deployment location of a vending machine.</span></span>
* <span data-ttu-id="12265-116">장치 앱의 사용 가능한 기능 및 상태와 같은 현재 상태 정보를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-116">Report current state information such as available capabilities and conditions from your device app.</span></span> <span data-ttu-id="12265-117">예를 들어 장치는 셀룰러 또는 WiFi를 통해 IoT Hub에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="12265-117">For example, a device is connected to your IoT hub over cellular or WiFi.</span></span>
* <span data-ttu-id="12265-118">장치 앱과 백 엔드 앱 간에 장기 실행 워크플로의 상태를 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-118">Synchronize the state of long-running workflows between device app and back-end app.</span></span> <span data-ttu-id="12265-119">예를 들어 솔루션 백 엔드가 설치할 새 펌웨어 버전을 지정하고 장치 앱이 다양한 업데이트 프로세스 단계를 보고할 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="12265-119">For example, when the solution back end specifies the new firmware version to install, and the device app reports the various stages of the update process.</span></span>
* <span data-ttu-id="12265-120">장치 메타데이터, 구성 또는 상태를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-120">Query your device metadata, configuration, or state.</span></span>

<span data-ttu-id="12265-121">reported 속성, 장치-클라우드 메시지 또는 파일 업로드 사용에 대한 지침은 [장치-클라우드 통신 지침][lnk-d2c-guidance]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12265-121">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span></span>
<span data-ttu-id="12265-122">desired 속성, 직접 메서드 또는 클라우드-장치 메시지 사용에 대한 지침은 [클라우드-장치 통신 지침][lnk-c2d-guidance]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12265-122">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="device-twins"></a><span data-ttu-id="12265-123">장치 쌍</span><span class="sxs-lookup"><span data-stu-id="12265-123">Device twins</span></span>
<span data-ttu-id="12265-124">장치 쌍이 저장하는 장치 관련 정보는:</span><span class="sxs-lookup"><span data-stu-id="12265-124">Device twins store device-related information that:</span></span>

* <span data-ttu-id="12265-125">장치 및 백 엔드가 장치 상태 및 구성 동기화에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-125">Device and back ends can use to synchronize device conditions and configuration.</span></span>
* <span data-ttu-id="12265-126">솔루션 백 엔드는 오래 실행되는 작업을 쿼리하고 대상으로 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-126">The solution back end can use to query and target long-running operations.</span></span>

<span data-ttu-id="12265-127">장치 쌍의 수명 주기는 해당 [장치 ID][lnk-identity]에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="12265-127">The lifecycle of a device twin is linked to the corresponding [device identity][lnk-identity].</span></span> <span data-ttu-id="12265-128">IoT Hub에서 새 장치 ID를 만들거나 삭제하면 장치 쌍이 암시적으로 만들어지거나 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="12265-128">Device twins are implicitly created and deleted when a new device identity is created or deleted in IoT Hub.</span></span>

<span data-ttu-id="12265-129">장치 쌍은 JSON 문서이며 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-129">A device twin is a JSON document that includes:</span></span>

* <span data-ttu-id="12265-130">**태그**.</span><span class="sxs-lookup"><span data-stu-id="12265-130">**Tags**.</span></span> <span data-ttu-id="12265-131">솔루션 백 엔드에서 읽고 쓸 수 있는 JSON 문서의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="12265-131">A section of the JSON document that the solution back end can read from and write to.</span></span> <span data-ttu-id="12265-132">태그는 장치 앱에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-132">Tags are not visible to device apps.</span></span>
* <span data-ttu-id="12265-133">**desired 속성**.</span><span class="sxs-lookup"><span data-stu-id="12265-133">**Desired properties**.</span></span> <span data-ttu-id="12265-134">reported 속성과 함께 장치 구성 또는 상황을 동기화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="12265-134">Used along with reported properties to synchronize device configuration or conditions.</span></span> <span data-ttu-id="12265-135">desired 속성은 솔루션 백 엔드에서만 설정할 수 있고 장치 앱에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-135">Desired properties can only be set by the solution back end and can be read by the device app.</span></span> <span data-ttu-id="12265-136">desired 속성이 변경되면 장치 앱에도 실시간으로 통보될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-136">The device app can also be notified in real time of changes in the desired properties.</span></span>
* <span data-ttu-id="12265-137">**reported 속성**.</span><span class="sxs-lookup"><span data-stu-id="12265-137">**Reported properties**.</span></span> <span data-ttu-id="12265-138">desired 속성과 함께 장치 구성 또는 상황을 동기화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="12265-138">Used along with desired properties to synchronize device configuration or conditions.</span></span> <span data-ttu-id="12265-139">reported 속성은 장치 앱에서만 설정할 수 있고 솔루션 백 엔드에서 읽고 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-139">Reported properties can only be set by the device app and can be read and queried by the solution back end.</span></span>

<span data-ttu-id="12265-140">또한 장치 쌍 JSON 문서의 루트에는 [ID 레지스트리][lnk-identity]에 포함된 해당 장치 ID의 읽기 전용 속성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="12265-140">Additionally, the root of the device twin JSON document contains the read-only properties from the corresponding device identity stored in the [identity registry][lnk-identity].</span></span>

![][img-twin]

<span data-ttu-id="12265-141">다음 예제에서는 장치 쌍 JSON 문서를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="12265-141">The following example shows a device twin JSON document:</span></span>

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

<span data-ttu-id="12265-142">루트 개체에는 시스템 속성과 `tags`, `reported` 및 `desired` 속성의 컨테이너 개체가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-142">In the root object, are the system properties, and container objects for `tags` and both `reported` and `desired` properties.</span></span> <span data-ttu-id="12265-143">`properties` 컨테이너에는 [장치 쌍 메타데이터][lnk-twin-metadata] 및 [낙관적 동시성][lnk-concurrency] 섹션에서 설명한 몇 가지 읽기 전용 요소(`$metadata`, `$etag` 및 `$version`)가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="12265-143">The `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in the [Device twin metadata][lnk-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span></span>

### <a name="reported-property-example"></a><span data-ttu-id="12265-144">reported 속성 예</span><span class="sxs-lookup"><span data-stu-id="12265-144">Reported property example</span></span>
<span data-ttu-id="12265-145">이전 예제에서 장치 쌍에 `batteryLevel` 속성이 포함되어 있으며 이것은 장치 앱에 의해 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="12265-145">In the previous example, the device twin contains a `batteryLevel` property that is reported by the device app.</span></span> <span data-ttu-id="12265-146">이 속성은 마지막으로 보고된 배터리 수준에 기반하여 장치에서 쿼리 및 작업을 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-146">This property makes it possible to query and operate on devices based on the last reported battery level.</span></span> <span data-ttu-id="12265-147">다른 예제에는 장치 앱 보고 장치 기능 또는 연결 옵션이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="12265-147">Other examples include the device app reporting device capabilities or connectivity options.</span></span>

> [!NOTE]
> <span data-ttu-id="12265-148">reported 속성은 솔루션 백 엔드가 마지막으로 알려진 속성 값에 관여하는 시나리오를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-148">Reported properties simplify scenarios where the solution back end is interested in the last known value of a property.</span></span> <span data-ttu-id="12265-149">솔루션 백 엔드에서 타임스탬프가 적용된 이벤트 시퀀스(예: 시계열)의 형태로 장치 원격 분석을 처리해야 하는 경우 [장치-클라우드 메시지][lnk-d2c]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-149">Use [device-to-cloud messages][lnk-d2c] if the solution back end needs to process device telemetry in the form of sequences of timestamped events, such as time series.</span></span>

### <a name="desired-property-example"></a><span data-ttu-id="12265-150">desired 속성 예제</span><span class="sxs-lookup"><span data-stu-id="12265-150">Desired property example</span></span>
<span data-ttu-id="12265-151">이전 예제에서 `telemetryConfig` 장치 쌍 desired 및 reported 속성은 솔루션 백 엔드 및 장치 앱에서 이 장치의 원격 분석 구성을 동기화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="12265-151">In the previous example, the `telemetryConfig` device twin desired and reported properties are used by the solution back end and the device app to synchronize the telemetry configuration for this device.</span></span> <span data-ttu-id="12265-152">예:</span><span class="sxs-lookup"><span data-stu-id="12265-152">For example:</span></span>

1. <span data-ttu-id="12265-153">솔루션 백 엔드는 desired 구성 값으로 desired 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-153">The solution back end sets the desired property with the desired configuration value.</span></span> <span data-ttu-id="12265-154">다음은 desired 속성 집합이 포함된 문서의 일부분입니다.</span><span class="sxs-lookup"><span data-stu-id="12265-154">Here is the portion of the document with the desired property set:</span></span>
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. <span data-ttu-id="12265-155">장치 앱이 연결되거나 처음으로 다시 연결되면 변경 내용이 즉시 통보됩니다.</span><span class="sxs-lookup"><span data-stu-id="12265-155">The device app is notified of the change immediately if connected, or at the first reconnect.</span></span> <span data-ttu-id="12265-156">그런 다음 장치 앱은 업데이트된 구성(또는 `status` 속성을 사용한 오류 상태)을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-156">The device app then reports the updated configuration (or an error condition using the `status` property).</span></span> <span data-ttu-id="12265-157">다음은 reported 속성의 일부분입니다.</span><span class="sxs-lookup"><span data-stu-id="12265-157">Here is the portion of the reported properties:</span></span>
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. <span data-ttu-id="12265-158">솔루션 백 엔드는 장치 쌍을 [쿼리][lnk-query]하여 많은 장치의 구성 작업 결과를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-158">The solution back end can track the results of the configuration operation across many devices, by [querying][lnk-query] device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="12265-159">이전 코드 조각은 장치 구성 및 상태를 인코딩하는 한 가지 방식을 가독성을 위해 최적화해 놓은 예입니다.</span><span class="sxs-lookup"><span data-stu-id="12265-159">The preceding snippets are examples, optimized for readability, of one way to encode a device configuration and its status.</span></span> <span data-ttu-id="12265-160">IoT Hub는 장치 쌍의 desired 및 reported 속성에 대해 특정 스키마를 적용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-160">IoT Hub does not impose a specific schema for the device twin desired and reported properties in the device twins.</span></span>
> 
> 

<span data-ttu-id="12265-161">쌍을 사용하여 펌웨어 업데이트와 같이 오래 실행되는 작업을 동기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-161">You can use twins to synchronize long-running operations such as firmware updates.</span></span> <span data-ttu-id="12265-162">속성을 사용하여 장치에서 장기 실행 작업을 동기화하고 추적하는 방법에 대한 자세한 내용은 [desired 속성을 사용하여 장치 구성][lnk-twin-properties]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12265-162">For more information on how to use properties to synchronize and track a long running operation across devices, see [Use desired properties to configure devices][lnk-twin-properties].</span></span>

## <a name="back-end-operations"></a><span data-ttu-id="12265-163">백 엔드 작업</span><span class="sxs-lookup"><span data-stu-id="12265-163">Back-end operations</span></span>
<span data-ttu-id="12265-164">솔루션 백 엔드는 HTTP를 통해 공개되는 다음과 같은 원자성 작업을 사용하여 장치 쌍에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-164">The solution back end operates on the device twin using the following atomic operations, exposed through HTTP:</span></span>

1. <span data-ttu-id="12265-165">**ID로 장치 쌍 검색** 이 작업은 태그 및 desired, reported 및 시스템 속성을 포함하여 장치 쌍 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-165">**Retrieve device twin by id**. This operation returns the device twin document, including tags and desired, reported, and system properties.</span></span>
2. <span data-ttu-id="12265-166">**장치 쌍 부분 업데이트**.</span><span class="sxs-lookup"><span data-stu-id="12265-166">**Partially update device twin**.</span></span> <span data-ttu-id="12265-167">이 작업은 솔루션 백 엔드에서 장치 쌍의 태그 또는 desired 속성을 부분적으로 업데이트할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-167">This operation enables the solution back end to partially update the tags or desired properties in a device twin.</span></span> <span data-ttu-id="12265-168">부분 업데이트는 속성을 추가하거나 업데이트하는 JSON 문서로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="12265-168">The partial update is expressed as a JSON document that adds or updates any property.</span></span> <span data-ttu-id="12265-169">`null`로 설정된 속성은 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="12265-169">Properties set to `null` are removed.</span></span> <span data-ttu-id="12265-170">다음 예제에서는 값이 `{"newProperty": "newValue"}`인 desired 속성을 새로 생성하고, `existingProperty`의 기존 값을 `"otherNewValue"`로 덮어쓰고, `otherOldProperty`를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-170">The following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites the existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span></span> <span data-ttu-id="12265-171">기존 desired 속성이나 태그에는 변화가 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-171">No other changes are made to existing desired properties or tags:</span></span>
   
        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }
3. <span data-ttu-id="12265-172">**desired 속성 바꾸기**.</span><span class="sxs-lookup"><span data-stu-id="12265-172">**Replace desired properties**.</span></span> <span data-ttu-id="12265-173">솔루션 백 엔드에서 기존의 모든 desired 속성을 완전히 덮어쓰고 `properties/desired`에 대해 새 JSON 문서를 대체할 수 있는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="12265-173">This operation enables the solution back end to completely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span></span>
4. <span data-ttu-id="12265-174">**태그 바꾸기**.</span><span class="sxs-lookup"><span data-stu-id="12265-174">**Replace tags**.</span></span> <span data-ttu-id="12265-175">이 작업을 사용하여 솔루션 백 엔드에서 기존의 모든 태그를 완전히 덮어쓰고 `tags`에 대해 새 JSON 문서를 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-175">This operation enables the solution back end to completely overwrite all existing tags and substitute a new JSON document for `tags`.</span></span>
5. <span data-ttu-id="12265-176">**쌍 알림을 받습니다**.</span><span class="sxs-lookup"><span data-stu-id="12265-176">**Receive twin notifications**.</span></span> <span data-ttu-id="12265-177">이 작업을 통해 쌍이 수정될 때 솔루션 백 엔드는 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-177">This operation allows the solution back end to be notified when the twin is modified.</span></span> <span data-ttu-id="12265-178">이를 수행하려면 IoT 솔루션은 경로를 만들고 데이터 원본을 *twinChangeEvents*와 동일하게 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-178">To do so, your IoT solution needs to create a route and to set the Data Source equal to *twinChangeEvents*.</span></span> <span data-ttu-id="12265-179">기본적으로 쌍 알림이 전송되지 않습니다. 즉, 이러한 경로는 미리 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-179">By default, no twin notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="12265-180">변경 속도가 너무 높은 경우 또는 내부 오류와 같은 다른 이유로 IoT Hub는 모든 변경 내용을 포함하는 하나의 알림만을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-180">If the rate of change is too high, or for other reasons, such as internal failures, the IoT Hub might send only one notification that contains all changes.</span></span> <span data-ttu-id="12265-181">따라서 응용 프로그램에 신뢰할 수 있는 감사 및 모든 중간 상태의 로깅이 필요한 경우 D2C 메시지를 사용하는 것이 여전히 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-181">So, if your application needs reliable auditing and logging of all intermediate states, then it is still recommended that you use D2C messages.</span></span> <span data-ttu-id="12265-182">쌍 알림 메시지는 속성 및 본문을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-182">The twin notification message includes properties, and body.</span></span>

    - <span data-ttu-id="12265-183">속성</span><span class="sxs-lookup"><span data-stu-id="12265-183">Properties</span></span>

    | <span data-ttu-id="12265-184">이름</span><span class="sxs-lookup"><span data-stu-id="12265-184">Name</span></span> | <span data-ttu-id="12265-185">값</span><span class="sxs-lookup"><span data-stu-id="12265-185">Value</span></span> |
    | --- | --- |
    <span data-ttu-id="12265-186">$content-type</span><span class="sxs-lookup"><span data-stu-id="12265-186">$content-type</span></span> | <span data-ttu-id="12265-187">application/json</span><span class="sxs-lookup"><span data-stu-id="12265-187">application/json</span></span> |
    <span data-ttu-id="12265-188">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="12265-188">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="12265-189">알림이 전송된 시간</span><span class="sxs-lookup"><span data-stu-id="12265-189">Time when the notification was sent</span></span> |
    <span data-ttu-id="12265-190">$iothub-message-source</span><span class="sxs-lookup"><span data-stu-id="12265-190">$iothub-message-source</span></span> | <span data-ttu-id="12265-191">twinChangeEvents</span><span class="sxs-lookup"><span data-stu-id="12265-191">twinChangeEvents</span></span> |
    <span data-ttu-id="12265-192">$content-encoding</span><span class="sxs-lookup"><span data-stu-id="12265-192">$content-encoding</span></span> | <span data-ttu-id="12265-193">utf-8</span><span class="sxs-lookup"><span data-stu-id="12265-193">utf-8</span></span> |
    <span data-ttu-id="12265-194">deviceId</span><span class="sxs-lookup"><span data-stu-id="12265-194">deviceId</span></span> | <span data-ttu-id="12265-195">장치의 ID</span><span class="sxs-lookup"><span data-stu-id="12265-195">Id of the device</span></span> |
    <span data-ttu-id="12265-196">hubName</span><span class="sxs-lookup"><span data-stu-id="12265-196">hubName</span></span> | <span data-ttu-id="12265-197">IoT Hub의 이름</span><span class="sxs-lookup"><span data-stu-id="12265-197">Name of IoT Hub</span></span> |
    <span data-ttu-id="12265-198">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="12265-198">operationTimestamp</span></span> | <span data-ttu-id="12265-199">[ISO8601] 작업의 타임스탬프</span><span class="sxs-lookup"><span data-stu-id="12265-199">[ISO8601] timestamp of operation</span></span> |
    <span data-ttu-id="12265-200">iothub-message-schema</span><span class="sxs-lookup"><span data-stu-id="12265-200">iothub-message-schema</span></span> | <span data-ttu-id="12265-201">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="12265-201">deviceLifecycleNotification</span></span> |
    <span data-ttu-id="12265-202">opType</span><span class="sxs-lookup"><span data-stu-id="12265-202">opType</span></span> | <span data-ttu-id="12265-203">"replaceTwin" 또는 "updateTwin"</span><span class="sxs-lookup"><span data-stu-id="12265-203">"replaceTwin" or "updateTwin"</span></span> |

    <span data-ttu-id="12265-204">메시지 시스템 속성 앞에 `'$'` 기호를 붙입니다.</span><span class="sxs-lookup"><span data-stu-id="12265-204">Message system properties are prefixed with the `'$'` symbol.</span></span>

    - <span data-ttu-id="12265-205">본문</span><span class="sxs-lookup"><span data-stu-id="12265-205">Body</span></span>
        
    <span data-ttu-id="12265-206">이 섹션은 JSON 형식으로 모든 쌍 변경 내용을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-206">This section includes all the twin changes in a JSON format.</span></span> <span data-ttu-id="12265-207">모든 쌍 섹션: 태그, properties.reported, properties.desired를 포함할 수 있으며 "$metadata" 요소를 포함한다는 차이점으로 패치와 동일한 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-207">It uses the same format as a patch, with the difference that it can contain all twin sections: tags, properties.reported, properties.desired, and that it contains the “$metadata” elements.</span></span> <span data-ttu-id="12265-208">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-208">For example,</span></span>
    ```
    {
        "properties": {
            "desired": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            },
            "reported": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            }
        }
    }
    ``` 

<span data-ttu-id="12265-209">이전의 모든 작업은 [낙관적 동시성][lnk-concurrency]을 지원하며 [보안][lnk-security] 문서에서 정의한 **ServiceConnect** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-209">All the preceding operations support [Optimistic concurrency][lnk-concurrency] and require the **ServiceConnect** permission, as defined in the [Security][lnk-security] article.</span></span>

<span data-ttu-id="12265-210">이러한 작업 외에도 솔루션 백 엔드는 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-210">In addition to these operations, the solution back end can:</span></span>

* <span data-ttu-id="12265-211">SQL 스타일 [IoT Hub 쿼리 언어][lnk-query]를 사용하여 장치 쌍을 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-211">Query the device twins using the SQL-like [IoT Hub query language][lnk-query].</span></span>
* <span data-ttu-id="12265-212">[작업][lnk-jobs]을 사용하여 장치 쌍의 큰 집합에서 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-212">Perform operations on large sets of device twins using [jobs][lnk-jobs].</span></span>

## <a name="device-operations"></a><span data-ttu-id="12265-213">장치 작업</span><span class="sxs-lookup"><span data-stu-id="12265-213">Device operations</span></span>
<span data-ttu-id="12265-214">장치 앱은 다음과 같은 원자성 작업을 사용하여 장치 쌍에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-214">The device app operates on the device twin using the following atomic operations:</span></span>

1. <span data-ttu-id="12265-215">**장치 쌍 검색**</span><span class="sxs-lookup"><span data-stu-id="12265-215">**Retrieve device twin**.</span></span> <span data-ttu-id="12265-216">이 작업은 현재 연결된 장치의 태그 및 desired, reported 및 시스템 속성을 포함하는 장치 쌍 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-216">This operation returns the device twin document (including tags and desired, reported and system properties) for the currently connected device.</span></span>
2. <span data-ttu-id="12265-217">**reported 속성 부분 업데이트**.</span><span class="sxs-lookup"><span data-stu-id="12265-217">**Partially update reported properties**.</span></span> <span data-ttu-id="12265-218">현재 연결된 장치의 reported 속성을 부분적으로 업데이트할 수 있는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="12265-218">This operation enables the partial update of the reported properties of the currently connected device.</span></span> <span data-ttu-id="12265-219">이 작업은 desired 속성의 부분 업데이트를 사용하는 솔루션 백 엔드와 동일한 JSON 업데이트 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-219">This operation uses the same JSON update format that the solution back end uses for a partial update of desired properties.</span></span>
3. <span data-ttu-id="12265-220">**desired 속성 관찰**.</span><span class="sxs-lookup"><span data-stu-id="12265-220">**Observe desired properties**.</span></span> <span data-ttu-id="12265-221">현재 연결된 장치는 desired 속성에 대한 업데이트가 발생하면 알림을 받도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-221">The currently connected device can choose to be notified of updates to the desired properties when they happen.</span></span> <span data-ttu-id="12265-222">장치는 솔루션 백 엔드에 의해 실행된 것과 같은 형태의 업데이트(부분 또는 전체 바꾸기)를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-222">The device receives the same form of update (partial or full replacement) executed by the solution back end.</span></span>

<span data-ttu-id="12265-223">이전의 모든 작업에는 [보안][lnk-security] 문서에서 정의한 **DeviceConnect** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-223">All the preceding operations require the **DeviceConnect** permission, as defined in the [Security][lnk-security] article.</span></span>

<span data-ttu-id="12265-224">[Azure IoT 장치 SDK][lnk-sdks]를 사용하면 이전 작업을 다양한 언어와 플랫폼에서 손쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-224">The [Azure IoT device SDKs][lnk-sdks] make it easy to use the preceding operations from many languages and platforms.</span></span> <span data-ttu-id="12265-225">desired 속성 동기화를 위한 IoT Hub 기본 형식에 대한 자세한 내용은 [장치 다시 연결 흐름][lnk-reconnection]에서 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12265-225">More information on the details of IoT Hub primitives for desired properties synchronization can be found in [Device reconnection flow][lnk-reconnection].</span></span>

> [!NOTE]
> <span data-ttu-id="12265-226">현재 장치 쌍은 MQTT 프로토콜을 사용하여 IoT Hub에 연결하는 장치에서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-226">Currently, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="12265-227">참조 항목:</span><span class="sxs-lookup"><span data-stu-id="12265-227">Reference topics:</span></span>
<span data-ttu-id="12265-228">다음 참조 항목에서는 IoT Hub 액세스 제어에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-228">The following reference topics provide you with more information about controlling access to your IoT hub.</span></span>

## <a name="tags-and-properties-format"></a><span data-ttu-id="12265-229">태그 및 속성 형식</span><span class="sxs-lookup"><span data-stu-id="12265-229">Tags and properties format</span></span>
<span data-ttu-id="12265-230">tags, desired 및 reported 속성은 JSON 개체이며 다음과 같은 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-230">Tags, desired, and reported properties are JSON objects with the following restrictions:</span></span>

* <span data-ttu-id="12265-231">JSON 개체의 모든 키는 대/소문자를 구분하는 64바이트 UTF-8 유니코드 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="12265-231">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span></span> <span data-ttu-id="12265-232">허용되는 문자에서 유니코드 제어 문자(세그먼트 C0 및 C1) 및 `'.'`, `' '` 및 `'$'`는 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="12265-232">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span></span>
* <span data-ttu-id="12265-233">JSON 개체의 모든 값은 부울, 숫자, 문자열, 개체와 같은 JSON 형식이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-233">All values in JSON objects can be of the following JSON types: boolean, number, string, object.</span></span> <span data-ttu-id="12265-234">배열은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-234">Arrays are not allowed.</span></span>
* <span data-ttu-id="12265-235">tags, desired 속성 및reported 속성의 모든 JSON 개체는 최대 5의 깊이를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-235">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span></span> <span data-ttu-id="12265-236">예를 들어 다음 개체는 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-236">For instance, the following object is valid:</span></span>

        {
            ...
            "tags": {
                "one": {
                    "two": {
                        "three": {
                            "four": {
                                "five": {
                                    "property": "value"
                                }
                            }
                        }
                    }
                }
            },
            ...
        }

* <span data-ttu-id="12265-237">모든 문자열 값의 길이는 최대 512바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="12265-237">All string values can be at most 512 bytes in length.</span></span>

## <a name="device-twin-size"></a><span data-ttu-id="12265-238">장치 쌍 크기</span><span class="sxs-lookup"><span data-stu-id="12265-238">Device twin size</span></span>
<span data-ttu-id="12265-239">IoT Hub는 `tags`, `properties/desired` 및 `properties/reported` 값에 8KB의 크기 제한을 적용합니다. 읽기 전용 요소는 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="12265-239">IoT Hub enforces an 8KB size limitation on the values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span></span>
<span data-ttu-id="12265-240">크기는 외부에 표시될 때 유니코드 제어 문자(세그먼트 C0 및 C1) 및 공백 `' '`을 제외한 모든 문자의 개수를 세어서 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="12265-240">The size is computed by counting all characters excluding UNICODE control characters (segments C0 and C1) and space `' '` when it appears outside of a string constant.</span></span>
<span data-ttu-id="12265-241">IoT Hub는 한도 이상으로 해당 문서의 크기를 증가시키는 모든 작업을 오류와 함께 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-241">IoT Hub rejects with an error all operations that would increase the size of those documents above the limit.</span></span>

## <a name="device-twin-metadata"></a><span data-ttu-id="12265-242">장치 쌍 메타데이터</span><span class="sxs-lookup"><span data-stu-id="12265-242">Device twin metadata</span></span>
<span data-ttu-id="12265-243">IoT Hub는 장치 쌍 desired 또는 reported 속성의 각 JSON 개체에 대한 마지막 업데이트의 타임스탬프를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-243">IoT Hub maintains the timestamp of the last update for each JSON object in device twin desired and reported properties.</span></span> <span data-ttu-id="12265-244">타임스탬프는 UTC 형식이며 [ISO8601] 형식 `YYYY-MM-DDTHH:MM:SS.mmmZ`로 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="12265-244">The timestamps are in UTC and encoded in the [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span></span>
<span data-ttu-id="12265-245">예:</span><span class="sxs-lookup"><span data-stu-id="12265-245">For example:</span></span>

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

<span data-ttu-id="12265-246">이 정보는 개체 키를 제거하는 업데이트를 유지하기 위해서 모든 수준(JSON 구조의 수준뿐만 아니라)에서 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="12265-246">This information is kept at every level (not just the leaves of the JSON structure) to preserve updates that remove object keys.</span></span>

## <a name="optimistic-concurrency"></a><span data-ttu-id="12265-247">낙관적 동시성</span><span class="sxs-lookup"><span data-stu-id="12265-247">Optimistic concurrency</span></span>
<span data-ttu-id="12265-248">태그, desired 및 reported 속성은 모두 낙관적 동시성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-248">Tags, desired, and reported properties all support optimistic concurrency.</span></span>
<span data-ttu-id="12265-249">[RFC7232]에 따르면 태그에는 ETag가 있고 이것은 태그의 JSON 표현을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="12265-249">Tags have an ETag, as per [RFC7232], that represents the tag's JSON representation.</span></span> <span data-ttu-id="12265-250">일관성을 보장하기 위해 솔루션 백 엔드에서 조건부 업데이트 작업에 ETag를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-250">You can use ETags in conditional update operations from the solution back end to ensure consistency.</span></span>

<span data-ttu-id="12265-251">장치 쌍 desired 및 reported 속성에는 ETag가 없지만 증분될 수 있는 `$version` 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-251">Device twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed to be incremental.</span></span> <span data-ttu-id="12265-252">ETag와 마찬가지로 버전은 업데이트의 일관성을 유지하는 파티를 업데이트하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-252">Similarly to an ETag, the version can be used by the updating party to enforce consistency of updates.</span></span> <span data-ttu-id="12265-253">예를 들어 reported 속성에 대한 장치 앱이나 desired 속성에 대한 솔루션 백 엔드입니다.</span><span class="sxs-lookup"><span data-stu-id="12265-253">For example, a device app for a reported property or the solution back end for a desired property.</span></span>

<span data-ttu-id="12265-254">버전은 관찰 에이전트(예: desired 속성을 관찰하는 장치 앱)가 업데이트 알림과 검색 작업의 결과 간에 속도를 중재해야 하는 경우에도 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-254">Versions are also useful when an observing agent (such as the device app observing the desired properties) must reconcile races between the result of a retrieve operation and an update notification.</span></span> <span data-ttu-id="12265-255">[장치 다시 연결 흐름][lnk-reconnection] 섹션에 자세한 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-255">The section [Device reconnection flow][lnk-reconnection] provides more information.</span></span>

## <a name="device-reconnection-flow"></a><span data-ttu-id="12265-256">장치 다시 연결 흐름</span><span class="sxs-lookup"><span data-stu-id="12265-256">Device reconnection flow</span></span>
<span data-ttu-id="12265-257">IoT Hub는 연결되지 않은 장치에 대한 desired 속성 업데이트 알림을 유지하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-257">IoT Hub does not preserve desired properties update notifications for disconnected devices.</span></span> <span data-ttu-id="12265-258">연결 중인 장치는 완전한 desired 속성 문서를 가져와야 하고 또한 업데이트 알림을 구독해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-258">It follows that a device that is connecting must retrieve the full desired properties document, in addition to subscribing for update notifications.</span></span> <span data-ttu-id="12265-259">업데이트 알림과 전체 검색이 서로 경쟁할 가능성이 있으므로 다음과 같은 흐름을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-259">Given the possibility of races between update notifications and full retrieval, the following flow must be ensured:</span></span>

1. <span data-ttu-id="12265-260">장치 앱을 IoT hub에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-260">Device app connects to an IoT hub.</span></span>
2. <span data-ttu-id="12265-261">장치 앱이 desired 속성 업데이트 알림을 구독합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-261">Device app subscribes for desired properties update notifications.</span></span>
3. <span data-ttu-id="12265-262">장치 앱이 desired 속성에 대한 전체 문서를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-262">Device app retrieves the full document for desired properties.</span></span>

<span data-ttu-id="12265-263">장치 앱은 검색이 완료된 문서의 버전보다 작거나 같은 `$version`이 포함된 모든 알림을 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-263">The device app can ignore all notifications with `$version` less or equal than the version of the full retrieved document.</span></span> <span data-ttu-id="12265-264">이 방법은 IoT Hub가 버전이 항상 증가한다는 것을 보장하기 때문에 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-264">This approach is possible because IoT Hub guarantees that versions always increment.</span></span>

> [!NOTE]
> <span data-ttu-id="12265-265">이 논리는 이미 [Azure IoT 장치 SDK][lnk-sdks]에 구현되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12265-265">This logic is already implemented in the [Azure IoT device SDKs][lnk-sdks].</span></span> <span data-ttu-id="12265-266">이 설명은 장치 앱이 Azure IoT 장치 SDK를 아무것도 사용할 수 없고 MQTT 인터페이스를 직접 프로그래밍해야 하는 경우에만 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-266">This description is useful only if the device app cannot use any of Azure IoT device SDKs and must program the MQTT interface directly.</span></span>
> 
> 

## <a name="additional-reference-material"></a><span data-ttu-id="12265-267">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="12265-267">Additional reference material</span></span>
<span data-ttu-id="12265-268">이 IoT Hub 개발자 가이드의 다른 참조 자료:</span><span class="sxs-lookup"><span data-stu-id="12265-268">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="12265-269">[IoT Hub 끝점][lnk-endpoints] 문서에서는 각 IoT Hub가 런타임 및 관리 작업에 노출하는 다양한 끝점을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-269">The [IoT Hub endpoints][lnk-endpoints] article describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="12265-270">[제한 및 할당량][lnk-quotas] 문서에서는 IoT Hub 서비스에 적용되는 할당량과 서비스를 사용할 때 예상되는 제한 동작에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-270">The [Throttling and quotas][lnk-quotas] article describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="12265-271">[Azure IoT 장치 및 서비스 SDK][lnk-sdks] 문서에서는 IoT Hub와 상호 작용하는 장치 및 서비스 앱 모두를 개발할 때 사용할 수 있는 다양한 언어 SDK를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-271">The [Azure IoT device and service SDKs][lnk-sdks] article lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="12265-272">[장치 쌍, 작업 및 메시지 라우팅을 위한 IoT Hub 쿼리 언어][lnk-query] 문서에서는 IoT Hub에서 장치 쌍 및 작업에 대한 정보를 검색하는 데 사용할 수 있는 IoT Hub 쿼리 언어에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-272">The [IoT Hub query language for device twins, jobs, and message routing][lnk-query] article describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="12265-273">[IoT Hub MQTT 지원][lnk-devguide-mqtt] 문서에서는 MQTT 프로토콜에 대한 IoT Hub 지원에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="12265-273">The [IoT Hub MQTT support][lnk-devguide-mqtt] article provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12265-274">다음 단계</span><span class="sxs-lookup"><span data-stu-id="12265-274">Next steps</span></span>
<span data-ttu-id="12265-275">장치 쌍에 대해 알아봤으니 다음 IoT Hub 개발자 가이드 항목에 대해서 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="12265-275">Now you have learned about device twins, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="12265-276">[장치에서 직접 메서드 호출][lnk-methods]</span><span class="sxs-lookup"><span data-stu-id="12265-276">[Invoke a direct method on a device][lnk-methods]</span></span>
* <span data-ttu-id="12265-277">[여러 장치에서 jobs 예약][lnk-jobs]</span><span class="sxs-lookup"><span data-stu-id="12265-277">[Schedule jobs on multiple devices][lnk-jobs]</span></span>

<span data-ttu-id="12265-278">이 문서에서 설명한 일부 개념을 시도해 보려면 다음과 같은 IoT Hub 자습서를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="12265-278">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorials:</span></span>

* <span data-ttu-id="12265-279">[장치 쌍을 사용하는 방법][lnk-twin-tutorial]</span><span class="sxs-lookup"><span data-stu-id="12265-279">[How to use the device twin][lnk-twin-tutorial]</span></span>
* <span data-ttu-id="12265-280">[장치 쌍 속성을 사용하는 방법][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="12265-280">[How to use device twin properties][lnk-twin-properties]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#device-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: media/iot-hub-devguide-device-twins/twin.png

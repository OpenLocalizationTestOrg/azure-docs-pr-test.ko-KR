---
title: "aaaUnderstand Azure IoT Hub 장치 트윈스 | Microsoft Docs"
description: "개발자 가이드-장치 사용 트윈스 IoT Hub와 장치 간에 toosynchronize 상태 및 구성 데이터"
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
ms.openlocfilehash: 7dade18665108ed352ff3d18e864dc34f451bbf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a><span data-ttu-id="6d9a5-103">IoT Hub의 장치 쌍 이해 및 사용</span><span class="sxs-lookup"><span data-stu-id="6d9a5-103">Understand and use device twins in IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="6d9a5-104">개요</span><span class="sxs-lookup"><span data-stu-id="6d9a5-104">Overview</span></span>
<span data-ttu-id="6d9a5-105">*장치 쌍*은 장치 상태 정보(메타데이터, 구성 및 조건)를 저장하는 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-105">*Device twins* are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="6d9a5-106">IoT Hub tooIoT 허브에 연결 해야 하는 각 장치에 대 한 장치로 이중을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-106">IoT Hub persists a device twin for each device that you connect tooIoT Hub.</span></span> <span data-ttu-id="6d9a5-107">이 문서에서는 다음을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-107">This article describes:</span></span>

* <span data-ttu-id="6d9a5-108">hello 장치로 이중의 구조를 hello: *태그*, *원하는* 및 *속성을 보고*, 및</span><span class="sxs-lookup"><span data-stu-id="6d9a5-108">hello structure of hello device twin: *tags*, *desired* and *reported properties*, and</span></span>
* <span data-ttu-id="6d9a5-109">장치 앱과 백 엔드 트윈스 장치에서 수행할 수 있는 hello 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-109">hello operations that device apps and back ends can perform on device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="6d9a5-110">현재 장치 트윈스 tooIoT 허브를 연결 하는 장치 에서만에서 액세스할 수는 hello MQTT 프로토콜을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-110">Currently, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="6d9a5-111">Toohello 참조 [MQTT 지원] [ lnk-devguide-mqtt] 방법에 대 한 문서 tooconvert 기존 장치 앱 toouse MQTT 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-111">Refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>
> 
> 

### <a name="when-toouse"></a><span data-ttu-id="6d9a5-112">때 toouse</span><span class="sxs-lookup"><span data-stu-id="6d9a5-112">When toouse</span></span>
<span data-ttu-id="6d9a5-113">장치 쌍의 용도:</span><span class="sxs-lookup"><span data-stu-id="6d9a5-113">Use device twins to:</span></span>

* <span data-ttu-id="6d9a5-114">Hello 클라우드에서 장치 관련 메타 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-114">Store device-specific metadata in hello cloud.</span></span> <span data-ttu-id="6d9a5-115">예를 들어 hello 배포의 위치는 판매기입니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-115">For example, hello deployment location of a vending machine.</span></span>
* <span data-ttu-id="6d9a5-116">장치 앱의 사용 가능한 기능 및 상태와 같은 현재 상태 정보를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-116">Report current state information such as available capabilities and conditions from your device app.</span></span> <span data-ttu-id="6d9a5-117">예를 들어 장치는 연결 된 tooyour IoT 허브 셀룰러 또는 병렬 WiFi 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-117">For example, a device is connected tooyour IoT hub over cellular or WiFi.</span></span>
* <span data-ttu-id="6d9a5-118">장치 앱과 백 엔드 응용 프로그램 간에 장기 실행 워크플로 hello 상태를 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-118">Synchronize hello state of long-running workflows between device app and back-end app.</span></span> <span data-ttu-id="6d9a5-119">예를 들어 hello 솔루션 다시 끝 새 펌웨어 버전 tooinstall hello 및 hello 장치 응용 프로그램 보고서 hello hello 업데이트 프로세스의 다양 한 단계를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-119">For example, when hello solution back end specifies hello new firmware version tooinstall, and hello device app reports hello various stages of hello update process.</span></span>
* <span data-ttu-id="6d9a5-120">장치 메타데이터, 구성 또는 상태를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-120">Query your device metadata, configuration, or state.</span></span>

<span data-ttu-id="6d9a5-121">너무 참조[장치-클라우드 통신 지침] [ lnk-d2c-guidance] 보고 속성, 장치-클라우드 메시지 또는 파일 업로드를 사용 하 여에 대 한 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-121">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span></span>
<span data-ttu-id="6d9a5-122">너무 참조[클라우드-장치 통신 지침] [ lnk-c2d-guidance] 원하는 속성, 직접 메서드 또는 클라우드-장치 메시지를 사용 하 여에 대 한 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-122">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="device-twins"></a><span data-ttu-id="6d9a5-123">장치 쌍</span><span class="sxs-lookup"><span data-stu-id="6d9a5-123">Device twins</span></span>
<span data-ttu-id="6d9a5-124">장치 쌍이 저장하는 장치 관련 정보는:</span><span class="sxs-lookup"><span data-stu-id="6d9a5-124">Device twins store device-related information that:</span></span>

* <span data-ttu-id="6d9a5-125">장치 및 백 엔드 toosynchronize 장치 조건 및 구성에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-125">Device and back ends can use toosynchronize device conditions and configuration.</span></span>
* <span data-ttu-id="6d9a5-126">hello 솔루션 백 엔드 tooquery를 사용할 수 있으며 대상 장기 실행 작업.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-126">hello solution back end can use tooquery and target long-running operations.</span></span>

<span data-ttu-id="6d9a5-127">연결 된 장치로 이중의 hello 수명 주기 toohello 해당 [장치 id][lnk-identity]합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-127">hello lifecycle of a device twin is linked toohello corresponding [device identity][lnk-identity].</span></span> <span data-ttu-id="6d9a5-128">IoT Hub에서 새 장치 ID를 만들거나 삭제하면 장치 쌍이 암시적으로 만들어지거나 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-128">Device twins are implicitly created and deleted when a new device identity is created or deleted in IoT Hub.</span></span>

<span data-ttu-id="6d9a5-129">장치 쌍은 JSON 문서이며 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-129">A device twin is a JSON document that includes:</span></span>

* <span data-ttu-id="6d9a5-130">**태그**.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-130">**Tags**.</span></span> <span data-ttu-id="6d9a5-131">솔루션 백 엔드 hello hello JSON 문서의 섹션에서 읽고 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-131">A section of hello JSON document that hello solution back end can read from and write to.</span></span> <span data-ttu-id="6d9a5-132">태그 표시 toodevice 앱 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-132">Tags are not visible toodevice apps.</span></span>
* <span data-ttu-id="6d9a5-133">**desired 속성**.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-133">**Desired properties**.</span></span> <span data-ttu-id="6d9a5-134">보고 속성 toosynchronize 장치 구성 또는 조건을 함께 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-134">Used along with reported properties toosynchronize device configuration or conditions.</span></span> <span data-ttu-id="6d9a5-135">원하는 속성에만 설정할 수 hello 솔루션 다시에서 끝 및 hello 장치 응용 프로그램에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-135">Desired properties can only be set by hello solution back end and can be read by hello device app.</span></span> <span data-ttu-id="6d9a5-136">또한 hello 원하는 속성의 변경 내용 중 실시간으로에서 hello 장치 앱을 알릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-136">hello device app can also be notified in real time of changes in hello desired properties.</span></span>
* <span data-ttu-id="6d9a5-137">**reported 속성**.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-137">**Reported properties**.</span></span> <span data-ttu-id="6d9a5-138">원하는 속성 toosynchronize 장치 구성 또는 조건을 함께 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-138">Used along with desired properties toosynchronize device configuration or conditions.</span></span> <span data-ttu-id="6d9a5-139">보고 속성 hello 장치 앱만 설정할 수 있습니다 및 읽고 hello 솔루션 백 엔드도 쿼리할 수 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-139">Reported properties can only be set by hello device app and can be read and queried by hello solution back end.</span></span>

<span data-ttu-id="6d9a5-140">Hello 장치로 이중 JSON 문서의 hello 루트 hello에 저장 된 hello 해당 장치의 id 로부터 hello 읽기 전용 속성을 포함 하는 또한 [id 레지스트리에][lnk-identity]합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-140">Additionally, hello root of hello device twin JSON document contains hello read-only properties from hello corresponding device identity stored in hello [identity registry][lnk-identity].</span></span>

![][img-twin]

<span data-ttu-id="6d9a5-141">다음 예제는 hello 장치로 이중 JSON 문서를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-141">hello following example shows a device twin JSON document:</span></span>

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

<span data-ttu-id="6d9a5-142">Hello 루트 개체는 hello 시스템 속성 및 컨테이너에 대 한 개체 `tags` 및 둘 다 `reported` 및 `desired` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-142">In hello root object, are hello system properties, and container objects for `tags` and both `reported` and `desired` properties.</span></span> <span data-ttu-id="6d9a5-143">hello `properties` 일부 읽기 전용 요소를 포함 하는 컨테이너 (`$metadata`, `$etag`, 및 `$version`) hello에 설명 된 [장치로 이중 메타 데이터] [ lnk-twin-metadata] 및 [ 낙관적 동시성] [ lnk-concurrency] 섹션.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-143">hello `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in hello [Device twin metadata][lnk-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span></span>

### <a name="reported-property-example"></a><span data-ttu-id="6d9a5-144">reported 속성 예</span><span class="sxs-lookup"><span data-stu-id="6d9a5-144">Reported property example</span></span>
<span data-ttu-id="6d9a5-145">Hello 이전 예에서는 hello 장치로 이중 포함 한 `batteryLevel` hello 장치 앱 로부터 보고 되는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-145">In hello previous example, hello device twin contains a `batteryLevel` property that is reported by hello device app.</span></span> <span data-ttu-id="6d9a5-146">이 속성 가능한 tooquery 있고 hello 마지막 보고 된 배터리 수준에 따라 장치에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-146">This property makes it possible tooquery and operate on devices based on hello last reported battery level.</span></span> <span data-ttu-id="6d9a5-147">다른 예로 hello 장치 앱 보고 장치 기능 또는 연결 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-147">Other examples include hello device app reporting device capabilities or connectivity options.</span></span>

> [!NOTE]
> <span data-ttu-id="6d9a5-148">보고 속성 hello 솔루션 백 엔드 hello 마지막 속성의 값으로는 관심이 시나리오를 단순화 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-148">Reported properties simplify scenarios where hello solution back end is interested in hello last known value of a property.</span></span> <span data-ttu-id="6d9a5-149">사용 하 여 [장치-클라우드 메시지] [ lnk-d2c] hello 솔루션 백 엔드 경우 시계열 같은 타임 스탬프 이벤트의 시퀀스의 hello 형태로 tooprocess 장치 원격 분석에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-149">Use [device-to-cloud messages][lnk-d2c] if hello solution back end needs tooprocess device telemetry in hello form of sequences of timestamped events, such as time series.</span></span>

### <a name="desired-property-example"></a><span data-ttu-id="6d9a5-150">desired 속성 예제</span><span class="sxs-lookup"><span data-stu-id="6d9a5-150">Desired property example</span></span>
<span data-ttu-id="6d9a5-151">Hello 이전 예에서 hello `telemetryConfig` 장치로 이중 원하는 및 보고 된 속성은이 장치에 대 한 솔루션의 백 엔드 hello 및 hello 장치 앱 toosynchronize hello 원격 분석 구성에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-151">In hello previous example, hello `telemetryConfig` device twin desired and reported properties are used by hello solution back end and hello device app toosynchronize hello telemetry configuration for this device.</span></span> <span data-ttu-id="6d9a5-152">예:</span><span class="sxs-lookup"><span data-stu-id="6d9a5-152">For example:</span></span>

1. <span data-ttu-id="6d9a5-153">hello 솔루션 백 엔드 hello 원하는 속성을 원하는 hello 구성 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-153">hello solution back end sets hello desired property with hello desired configuration value.</span></span> <span data-ttu-id="6d9a5-154">다음은 필요한 hello 속성이 설정 된 hello 문서 hello 부분이입니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-154">Here is hello portion of hello document with hello desired property set:</span></span>
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. <span data-ttu-id="6d9a5-155">hello 장치 앱에 연결 하거나 hello에서 먼저 다시 연결 하는 경우에 즉시 hello 변경 알림이 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-155">hello device app is notified of hello change immediately if connected, or at hello first reconnect.</span></span> <span data-ttu-id="6d9a5-156">hello 장치 응용 프로그램이 다음 보고 업데이트 하는 hello 구성 (또는 hello를 사용 하 여 오류 조건을 `status` 속성).</span><span class="sxs-lookup"><span data-stu-id="6d9a5-156">hello device app then reports hello updated configuration (or an error condition using hello `status` property).</span></span> <span data-ttu-id="6d9a5-157">다음은 hello 부분의 hello 속성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-157">Here is hello portion of hello reported properties:</span></span>
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. <span data-ttu-id="6d9a5-158">hello 솔루션 백 엔드 여 hello 결과 hello 구성 작업의 여러 장치에서 추적할 수 [쿼리] [ lnk-query] 장치 트윈스 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-158">hello solution back end can track hello results of hello configuration operation across many devices, by [querying][lnk-query] device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="6d9a5-159">hello 이전 조각은 예제를 보려면 장치 구성 및 서버 인스턴스의 상태는 한 가지 방법은 tooencode의 가독성을 위해 최적화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-159">hello preceding snippets are examples, optimized for readability, of one way tooencode a device configuration and its status.</span></span> <span data-ttu-id="6d9a5-160">IoT Hub는 hello 장치로 이중 원하는 hello 장치 트윈스에서 속성을 보고에 대 한 특정 스키마를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-160">IoT Hub does not impose a specific schema for hello device twin desired and reported properties in hello device twins.</span></span>
> 
> 

<span data-ttu-id="6d9a5-161">예: 펌웨어 업데이트 트윈스 toosynchronize 장기 실행 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-161">You can use twins toosynchronize long-running operations such as firmware updates.</span></span> <span data-ttu-id="6d9a5-162">Toouse 속성 toosynchronize 및 장치에서 장기 실행 작업 추적 참조 하는 방법에 대 한 자세한 내용은 [속성 tooconfigure 장치 원하는 사용할][lnk-twin-properties]합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-162">For more information on how toouse properties toosynchronize and track a long running operation across devices, see [Use desired properties tooconfigure devices][lnk-twin-properties].</span></span>

## <a name="back-end-operations"></a><span data-ttu-id="6d9a5-163">백 엔드 작업</span><span class="sxs-lookup"><span data-stu-id="6d9a5-163">Back-end operations</span></span>
<span data-ttu-id="6d9a5-164">HTTP를 통해 노출 하는 원자성 작업을 수행 하는 hello를 사용 하 여 hello 장치로 이중에서 작동 하는 hello 솔루션 백 엔드:</span><span class="sxs-lookup"><span data-stu-id="6d9a5-164">hello solution back end operates on hello device twin using hello following atomic operations, exposed through HTTP:</span></span>

1. <span data-ttu-id="6d9a5-165">**ID로 장치 쌍 검색** 이 작업은 반환 hello 장치로 이중 문서를 태그를 포함 하 고 원하는 경우 보고 및 시스템 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-165">**Retrieve device twin by id**. This operation returns hello device twin document, including tags and desired, reported, and system properties.</span></span>
2. <span data-ttu-id="6d9a5-166">**장치 쌍 부분 업데이트**.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-166">**Partially update device twin**.</span></span> <span data-ttu-id="6d9a5-167">이 작업에는 hello 솔루션 백 엔드 toopartially 업데이트 hello 태그 또는 장치로 이중에서 원하는 속성 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-167">This operation enables hello solution back end toopartially update hello tags or desired properties in a device twin.</span></span> <span data-ttu-id="6d9a5-168">hello 부분 업데이트를 추가 하거나 속성을 업데이트 하는 JSON 문서로 표현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-168">hello partial update is expressed as a JSON document that adds or updates any property.</span></span> <span data-ttu-id="6d9a5-169">속성이 너무 설정`null` 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-169">Properties set too`null` are removed.</span></span> <span data-ttu-id="6d9a5-170">hello 다음 예제에서는 속성을 새로 만들고 원하는 값으로 `{"newProperty": "newValue"}`, hello의 기존 값을 덮어쓰게 `existingProperty` 와 `"otherNewValue"`, 제거 및 `otherOldProperty`합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-170">hello following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites hello existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span></span> <span data-ttu-id="6d9a5-171">다른 변경 내용이 없는 원하는 tooexisting 속성 또는 태그:</span><span class="sxs-lookup"><span data-stu-id="6d9a5-171">No other changes are made tooexisting desired properties or tags:</span></span>
   
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
3. <span data-ttu-id="6d9a5-172">**desired 속성 바꾸기**.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-172">**Replace desired properties**.</span></span> <span data-ttu-id="6d9a5-173">이 작업을 사용 하면 hello 솔루션 백 엔드 toocompletely 모든 기존 원하는 속성을 덮어쓸 및 새 JSON 문서에 대 한 대체 `properties/desired`합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-173">This operation enables hello solution back end toocompletely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span></span>
4. <span data-ttu-id="6d9a5-174">**태그 바꾸기**.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-174">**Replace tags**.</span></span> <span data-ttu-id="6d9a5-175">이 작업을 사용 하면 hello 솔루션 백 엔드 toocompletely 모든 기존 태그를 덮어쓰고 새 JSON 문서에 대 한 대체 `tags`합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-175">This operation enables hello solution back end toocompletely overwrite all existing tags and substitute a new JSON document for `tags`.</span></span>
5. <span data-ttu-id="6d9a5-176">**쌍 알림을 받습니다**.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-176">**Receive twin notifications**.</span></span> <span data-ttu-id="6d9a5-177">이 작업에는 hello 솔루션 백 엔드 toobe를 hello로 이중 수정 될 때 알릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-177">This operation allows hello solution back end toobe notified when hello twin is modified.</span></span> <span data-ttu-id="6d9a5-178">toodo, 하면 IoT 솔루션 필요한 등 toocreate 경로 및 tooset hello 데이터 소스 같음 너무*twinChangeEvents*합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-178">toodo so, your IoT solution needs toocreate a route and tooset hello Data Source equal too*twinChangeEvents*.</span></span> <span data-ttu-id="6d9a5-179">기본적으로 쌍 알림이 전송되지 않습니다. 즉, 이러한 경로는 미리 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-179">By default, no twin notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="6d9a5-180">변경의 hello 속도가 너무 빨라 또는 내부 오류와 같은 다른 이유로 hello IoT Hub 모든 변경 내용이 포함 된 하나의 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-180">If hello rate of change is too high, or for other reasons, such as internal failures, hello IoT Hub might send only one notification that contains all changes.</span></span> <span data-ttu-id="6d9a5-181">따라서 응용 프로그램에 신뢰할 수 있는 감사 및 모든 중간 상태의 로깅이 필요한 경우 D2C 메시지를 사용하는 것이 여전히 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-181">So, if your application needs reliable auditing and logging of all intermediate states, then it is still recommended that you use D2C messages.</span></span> <span data-ttu-id="6d9a5-182">hello로 이중 알림 메시지에 속성 및 본문에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-182">hello twin notification message includes properties, and body.</span></span>

    - <span data-ttu-id="6d9a5-183">properties</span><span class="sxs-lookup"><span data-stu-id="6d9a5-183">Properties</span></span>

    | <span data-ttu-id="6d9a5-184">이름</span><span class="sxs-lookup"><span data-stu-id="6d9a5-184">Name</span></span> | <span data-ttu-id="6d9a5-185">값</span><span class="sxs-lookup"><span data-stu-id="6d9a5-185">Value</span></span> |
    | --- | --- |
    <span data-ttu-id="6d9a5-186">$content-type</span><span class="sxs-lookup"><span data-stu-id="6d9a5-186">$content-type</span></span> | <span data-ttu-id="6d9a5-187">application/json</span><span class="sxs-lookup"><span data-stu-id="6d9a5-187">application/json</span></span> |
    <span data-ttu-id="6d9a5-188">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="6d9a5-188">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="6d9a5-189">Hello 알림을 전송 시간</span><span class="sxs-lookup"><span data-stu-id="6d9a5-189">Time when hello notification was sent</span></span> |
    <span data-ttu-id="6d9a5-190">$iothub-message-source</span><span class="sxs-lookup"><span data-stu-id="6d9a5-190">$iothub-message-source</span></span> | <span data-ttu-id="6d9a5-191">twinChangeEvents</span><span class="sxs-lookup"><span data-stu-id="6d9a5-191">twinChangeEvents</span></span> |
    <span data-ttu-id="6d9a5-192">$content-encoding</span><span class="sxs-lookup"><span data-stu-id="6d9a5-192">$content-encoding</span></span> | <span data-ttu-id="6d9a5-193">utf-8</span><span class="sxs-lookup"><span data-stu-id="6d9a5-193">utf-8</span></span> |
    <span data-ttu-id="6d9a5-194">deviceId</span><span class="sxs-lookup"><span data-stu-id="6d9a5-194">deviceId</span></span> | <span data-ttu-id="6d9a5-195">Hello 장치의 id</span><span class="sxs-lookup"><span data-stu-id="6d9a5-195">Id of hello device</span></span> |
    <span data-ttu-id="6d9a5-196">hubName</span><span class="sxs-lookup"><span data-stu-id="6d9a5-196">hubName</span></span> | <span data-ttu-id="6d9a5-197">IoT Hub의 이름</span><span class="sxs-lookup"><span data-stu-id="6d9a5-197">Name of IoT Hub</span></span> |
    <span data-ttu-id="6d9a5-198">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="6d9a5-198">operationTimestamp</span></span> | <span data-ttu-id="6d9a5-199">[ISO8601] 작업의 타임스탬프</span><span class="sxs-lookup"><span data-stu-id="6d9a5-199">[ISO8601] timestamp of operation</span></span> |
    <span data-ttu-id="6d9a5-200">iothub-message-schema</span><span class="sxs-lookup"><span data-stu-id="6d9a5-200">iothub-message-schema</span></span> | <span data-ttu-id="6d9a5-201">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="6d9a5-201">deviceLifecycleNotification</span></span> |
    <span data-ttu-id="6d9a5-202">opType</span><span class="sxs-lookup"><span data-stu-id="6d9a5-202">opType</span></span> | <span data-ttu-id="6d9a5-203">"replaceTwin" 또는 "updateTwin"</span><span class="sxs-lookup"><span data-stu-id="6d9a5-203">"replaceTwin" or "updateTwin"</span></span> |

    <span data-ttu-id="6d9a5-204">메시지 시스템 속성은 hello로 접두사가 `'$'` 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-204">Message system properties are prefixed with hello `'$'` symbol.</span></span>

    - <span data-ttu-id="6d9a5-205">body</span><span class="sxs-lookup"><span data-stu-id="6d9a5-205">Body</span></span>
        
    <span data-ttu-id="6d9a5-206">이 섹션에는 JSON 형식의 hello로 이중 변경 내용을 모두 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-206">This section includes all hello twin changes in a JSON format.</span></span> <span data-ttu-id="6d9a5-207">동일한 형식 hello를 사용 하 여 패치로, hello 차이만 한다는 섹션이 포함 되어야 모두로 이중: 태그, properties.reported, properties.desired를 포함 하 고 "$metadata" hello 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-207">It uses hello same format as a patch, with hello difference that it can contain all twin sections: tags, properties.reported, properties.desired, and that it contains hello “$metadata” elements.</span></span> <span data-ttu-id="6d9a5-208">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-208">For example,</span></span>
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

<span data-ttu-id="6d9a5-209">이전 작업 지원 hello 모든 [낙관적 동시성] [ lnk-concurrency] hello 필요 **ServiceConnect** hello에 정의 된 사용 권한 [보안 ] [ lnk-security] 문서.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-209">All hello preceding operations support [Optimistic concurrency][lnk-concurrency] and require hello **ServiceConnect** permission, as defined in hello [Security][lnk-security] article.</span></span>

<span data-ttu-id="6d9a5-210">또한 작업 toothese hello 솔루션 다시 끝 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-210">In addition toothese operations, hello solution back end can:</span></span>

* <span data-ttu-id="6d9a5-211">Hello 장치 트윈스 hello를 사용 하 여 쿼리 SQL과 비슷한 [IoT Hub 쿼리 언어][lnk-query]합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-211">Query hello device twins using hello SQL-like [IoT Hub query language][lnk-query].</span></span>
* <span data-ttu-id="6d9a5-212">[작업][lnk-jobs]을 사용하여 장치 쌍의 큰 집합에서 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-212">Perform operations on large sets of device twins using [jobs][lnk-jobs].</span></span>

## <a name="device-operations"></a><span data-ttu-id="6d9a5-213">장치 작업</span><span class="sxs-lookup"><span data-stu-id="6d9a5-213">Device operations</span></span>
<span data-ttu-id="6d9a5-214">hello 장치 응용 프로그램에서 원자성 작업을 수행 하는 hello를 사용 하 여 hello 장치로 이중은 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-214">hello device app operates on hello device twin using hello following atomic operations:</span></span>

1. <span data-ttu-id="6d9a5-215">**장치 쌍 검색**</span><span class="sxs-lookup"><span data-stu-id="6d9a5-215">**Retrieve device twin**.</span></span> <span data-ttu-id="6d9a5-216">이 작업 hello 장치로 이중 문서를 반환 합니다 (태그를 포함 하 고 원하는, 보고 및 시스템 속성) hello 현재 연결 된 장치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-216">This operation returns hello device twin document (including tags and desired, reported and system properties) for hello currently connected device.</span></span>
2. <span data-ttu-id="6d9a5-217">**reported 속성 부분 업데이트**.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-217">**Partially update reported properties**.</span></span> <span data-ttu-id="6d9a5-218">이 작업을 사용 하면 hello의 부분 업데이트 hello hello 현재 연결 된 장치의 속성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-218">This operation enables hello partial update of hello reported properties of hello currently connected device.</span></span> <span data-ttu-id="6d9a5-219">이 작업을 사용 하 여 hello 동일한 JSON 업데이트에 해당 hello 솔루션 백 엔드 사용 하 여 원하는 속성의 부분 업데이트에 대 한 서식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-219">This operation uses hello same JSON update format that hello solution back end uses for a partial update of desired properties.</span></span>
3. <span data-ttu-id="6d9a5-220">**desired 속성 관찰**.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-220">**Observe desired properties**.</span></span> <span data-ttu-id="6d9a5-221">현재 연결 된 장치 hello toobe 발생할 때 업데이트 toohello 필요한 속성에 대 한 알림을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-221">hello currently connected device can choose toobe notified of updates toohello desired properties when they happen.</span></span> <span data-ttu-id="6d9a5-222">hello 장치 hello 솔루션 백 엔드에 의해 같은 형태의 업데이트 (전체 또는 일부 대체) 실행 하는 hello를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-222">hello device receives hello same form of update (partial or full replacement) executed by hello solution back end.</span></span>

<span data-ttu-id="6d9a5-223">이전 작업이 모두 hello hello 필요 **DeviceConnect** hello에 정의 된 사용 권한 [보안] [ lnk-security] 문서.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-223">All hello preceding operations require hello **DeviceConnect** permission, as defined in hello [Security][lnk-security] article.</span></span>

<span data-ttu-id="6d9a5-224">hello [Azure IoT 장치 Sdk] [ lnk-sdks] 쉽게 toouse hello 앞에 다양 한 언어 및 플랫폼에서 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-224">hello [Azure IoT device SDKs][lnk-sdks] make it easy toouse hello preceding operations from many languages and platforms.</span></span> <span data-ttu-id="6d9a5-225">자세한 내용은 hello 원하는 속성이 동기화에 대 한 IoT Hub 기본 형식에 있습니다 [장치 다시 연결 흐름][lnk-reconnection]합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-225">More information on hello details of IoT Hub primitives for desired properties synchronization can be found in [Device reconnection flow][lnk-reconnection].</span></span>

> [!NOTE]
> <span data-ttu-id="6d9a5-226">현재 장치 트윈스 tooIoT 허브를 연결 하는 장치 에서만에서 액세스할 수는 hello MQTT 프로토콜을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-226">Currently, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="6d9a5-227">참조 항목:</span><span class="sxs-lookup"><span data-stu-id="6d9a5-227">Reference topics:</span></span>
<span data-ttu-id="6d9a5-228">hello 다음 참조 항목 제공 제어 액세스 tooyour IoT 허브에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-228">hello following reference topics provide you with more information about controlling access tooyour IoT hub.</span></span>

## <a name="tags-and-properties-format"></a><span data-ttu-id="6d9a5-229">태그 및 속성 형식</span><span class="sxs-lookup"><span data-stu-id="6d9a5-229">Tags and properties format</span></span>
<span data-ttu-id="6d9a5-230">태그를 원하는 및 보고 속성 제한 사항에 따라 hello 사용 하 여 JSON 개체는:</span><span class="sxs-lookup"><span data-stu-id="6d9a5-230">Tags, desired, and reported properties are JSON objects with hello following restrictions:</span></span>

* <span data-ttu-id="6d9a5-231">JSON 개체의 모든 키는 대/소문자를 구분하는 64바이트 UTF-8 유니코드 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-231">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span></span> <span data-ttu-id="6d9a5-232">허용되는 문자에서 유니코드 제어 문자(세그먼트 C0 및 C1) 및 `'.'`, `' '` 및 `'$'`는 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-232">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span></span>
* <span data-ttu-id="6d9a5-233">JSON 개체의 모든 값의 JSON 유형만 hello 될 수 있습니다: 부울, 숫자, 문자열, 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-233">All values in JSON objects can be of hello following JSON types: boolean, number, string, object.</span></span> <span data-ttu-id="6d9a5-234">배열은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-234">Arrays are not allowed.</span></span>
* <span data-ttu-id="6d9a5-235">tags, desired 속성 및reported 속성의 모든 JSON 개체는 최대 5의 깊이를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-235">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span></span> <span data-ttu-id="6d9a5-236">예를 들어, 다음 개체는 hello가 올바릅니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-236">For instance, hello following object is valid:</span></span>

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

* <span data-ttu-id="6d9a5-237">모든 문자열 값의 길이는 최대 512바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-237">All string values can be at most 512 bytes in length.</span></span>

## <a name="device-twin-size"></a><span data-ttu-id="6d9a5-238">장치 쌍 크기</span><span class="sxs-lookup"><span data-stu-id="6d9a5-238">Device twin size</span></span>
<span data-ttu-id="6d9a5-239">IoT Hub는 8KB 크기 제한의 hello 값에 적용 `tags`, `properties/desired`, 및 `properties/reported`, 읽기 전용 요소 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-239">IoT Hub enforces an 8KB size limitation on hello values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span></span>
<span data-ttu-id="6d9a5-240">hello 크기는 계산를 계산 하 여 모든 문자를 제외한 유니코드 제어 문자 (세그먼트 C0 및 C1) 및 공간 `' '` 는 문자열 상수 외부에서 표시 되 면입니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-240">hello size is computed by counting all characters excluding UNICODE control characters (segments C0 and C1) and space `' '` when it appears outside of a string constant.</span></span>
<span data-ttu-id="6d9a5-241">IoT Hub 오류가 발생 하 여 hello 제한 초과 이러한 문서의 hello 크기를 증가 하 게 하는 모든 작업을 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-241">IoT Hub rejects with an error all operations that would increase hello size of those documents above hello limit.</span></span>

## <a name="device-twin-metadata"></a><span data-ttu-id="6d9a5-242">장치 쌍 메타데이터</span><span class="sxs-lookup"><span data-stu-id="6d9a5-242">Device twin metadata</span></span>
<span data-ttu-id="6d9a5-243">IoT Hub 원하는 스탬프와 속성을 보고 hello hello로 이중 장치에 있는 각 JSON 개체에 대 한 마지막 업데이트 타임 스탬프를 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-243">IoT Hub maintains hello timestamp of hello last update for each JSON object in device twin desired and reported properties.</span></span> <span data-ttu-id="6d9a5-244">hello 타임 스탬프가 UTC에 있으며 hello에 인코딩된 [ISO8601] 형식 `YYYY-MM-DDTHH:MM:SS.mmmZ`합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-244">hello timestamps are in UTC and encoded in hello [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span></span>
<span data-ttu-id="6d9a5-245">예:</span><span class="sxs-lookup"><span data-stu-id="6d9a5-245">For example:</span></span>

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

<span data-ttu-id="6d9a5-246">이 정보는 키 개체를 제거 하는 모든 수준 (JSON 구조 hello의 뿐 아니라 hello 잎) toopreserve 업데이트에서 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-246">This information is kept at every level (not just hello leaves of hello JSON structure) toopreserve updates that remove object keys.</span></span>

## <a name="optimistic-concurrency"></a><span data-ttu-id="6d9a5-247">낙관적 동시성</span><span class="sxs-lookup"><span data-stu-id="6d9a5-247">Optimistic concurrency</span></span>
<span data-ttu-id="6d9a5-248">태그, desired 및 reported 속성은 모두 낙관적 동시성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-248">Tags, desired, and reported properties all support optimistic concurrency.</span></span>
<span data-ttu-id="6d9a5-249">태그는 ETag를 기준으로 한 [RFC7232], hello 태그의 JSON 표현을 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-249">Tags have an ETag, as per [RFC7232], that represents hello tag's JSON representation.</span></span> <span data-ttu-id="6d9a5-250">Etag는 hello 솔루션 백 엔드 tooensure 일관성에서 조건부 업데이트 작업에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-250">You can use ETags in conditional update operations from hello solution back end tooensure consistency.</span></span>

<span data-ttu-id="6d9a5-251">장치로 이중 필요 하 고 속성을 보고 했지만 Etag를 하지 않은 한 `$version` toobe 증분 보장 되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-251">Device twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed toobe incremental.</span></span> <span data-ttu-id="6d9a5-252">마찬가지로 tooan ETag, hello 버전 hello 파티 tooenforce 일관성 업데이트를 업데이트 하 여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-252">Similarly tooan ETag, hello version can be used by hello updating party tooenforce consistency of updates.</span></span> <span data-ttu-id="6d9a5-253">예를 들어 보고 된 속성이 나 hello 솔루션 백 엔드 원하는 속성에 대 한 장치 앱.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-253">For example, a device app for a reported property or hello solution back end for a desired property.</span></span>

<span data-ttu-id="6d9a5-254">버전 (예: hello 원하는 속성을 관찰 hello 장치 응용 프로그램) 관찰 에이전트 검색 작업의 hello 결과 업데이트 알림을 간의 경합을 조정 해야 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-254">Versions are also useful when an observing agent (such as hello device app observing hello desired properties) must reconcile races between hello result of a retrieve operation and an update notification.</span></span> <span data-ttu-id="6d9a5-255">섹션 hello [장치 다시 연결 흐름] [ lnk-reconnection] 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-255">hello section [Device reconnection flow][lnk-reconnection] provides more information.</span></span>

## <a name="device-reconnection-flow"></a><span data-ttu-id="6d9a5-256">장치 다시 연결 흐름</span><span class="sxs-lookup"><span data-stu-id="6d9a5-256">Device reconnection flow</span></span>
<span data-ttu-id="6d9a5-257">IoT Hub는 연결되지 않은 장치에 대한 desired 속성 업데이트 알림을 유지하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-257">IoT Hub does not preserve desired properties update notifications for disconnected devices.</span></span> <span data-ttu-id="6d9a5-258">_ 연결 하는 장치에서 업데이트 알림에 대 한 추가 toosubscribing hello 전체 원하는 속성 문서를 검색 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-258">It follows that a device that is connecting must retrieve hello full desired properties document, in addition toosubscribing for update notifications.</span></span> <span data-ttu-id="6d9a5-259">업데이트 알림 및 전체 검색 사이의 레이스가 hello 가능성이 들어 hello 흐름 확보 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-259">Given hello possibility of races between update notifications and full retrieval, hello following flow must be ensured:</span></span>

1. <span data-ttu-id="6d9a5-260">장치 앱 tooan IoT 허브를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-260">Device app connects tooan IoT hub.</span></span>
2. <span data-ttu-id="6d9a5-261">장치 앱이 desired 속성 업데이트 알림을 구독합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-261">Device app subscribes for desired properties update notifications.</span></span>
3. <span data-ttu-id="6d9a5-262">장치 앱 hello 원하는 속성에 대 한 전체 문서를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-262">Device app retrieves hello full document for desired properties.</span></span>

<span data-ttu-id="6d9a5-263">hello 장치 응용 프로그램을 사용 하 여 모든 알림을 무시할 수 `$version` hello 전체 검색 된 문서의 hello 버전 보다 작거나 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-263">hello device app can ignore all notifications with `$version` less or equal than hello version of hello full retrieved document.</span></span> <span data-ttu-id="6d9a5-264">이 방법은 IoT Hub가 버전이 항상 증가한다는 것을 보장하기 때문에 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-264">This approach is possible because IoT Hub guarantees that versions always increment.</span></span>

> [!NOTE]
> <span data-ttu-id="6d9a5-265">이 논리 hello에서 이미 구현 되어 [Azure IoT 장치 Sdk][lnk-sdks]합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-265">This logic is already implemented in hello [Azure IoT device SDKs][lnk-sdks].</span></span> <span data-ttu-id="6d9a5-266">이 설명은 hello 장치 응용 프로그램이 Azure IoT 장치 Sdk 중 하나를 사용할 수 없는 hello MQTT 인터페이스를 직접 프로그래밍 해야 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-266">This description is useful only if hello device app cannot use any of Azure IoT device SDKs and must program hello MQTT interface directly.</span></span>
> 
> 

## <a name="additional-reference-material"></a><span data-ttu-id="6d9a5-267">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="6d9a5-267">Additional reference material</span></span>
<span data-ttu-id="6d9a5-268">Hello IoT 허브 개발자 가이드에서에서 다른 참조 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-268">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="6d9a5-269">hello [IoT Hub 끝점] [ lnk-endpoints] 설명 hello 런타임 및 관리 작업에 대 한 각 IoT 허브를 노출 하는 다양 한 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-269">hello [IoT Hub endpoints][lnk-endpoints] article describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="6d9a5-270">hello [제한 및 할당량] [ lnk-quotas] hello 서비스를 사용 하는 경우 조정 동작 tooexpect hello와 toohello IoT 허브 서비스를 적용 하는 hello 할당량에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-270">hello [Throttling and quotas][lnk-quotas] article describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="6d9a5-271">hello [Azure IoT 장치 및 서비스 Sdk] [ lnk-sdks] 문서 목록을 hello 다양 한 언어 Sdk IoT Hub와 상호 작용 하는 장치 및 서비스 모두 앱을 개발할 때 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-271">hello [Azure IoT device and service SDKs][lnk-sdks] article lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="6d9a5-272">hello [장치 트윈스, 작업 및 메시지 라우팅에 대 한 IoT Hub 쿼리 언어] [ lnk-query] hello 장치 트윈스 및 작업에 대 한 IoT 허브에서 tooretrieve 정보를 사용 하려면 IoT Hub 쿼리 언어에 설명 .</span><span class="sxs-lookup"><span data-stu-id="6d9a5-272">hello [IoT Hub query language for device twins, jobs, and message routing][lnk-query] article describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="6d9a5-273">hello [IoT 허브 MQTT 지원] [ lnk-devguide-mqtt] 문서 hello MQTT 프로토콜에 대 한 IoT Hub 지원에 대 한 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-273">hello [IoT Hub MQTT support][lnk-devguide-mqtt] article provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d9a5-274">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6d9a5-274">Next steps</span></span>
<span data-ttu-id="6d9a5-275">이제 장치 트윈스 알아보았습니다 hello 다음 IoT 허브 개발자 가이드 항목에에서 관심이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-275">Now you have learned about device twins, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="6d9a5-276">[장치에서 직접 메서드 호출][lnk-methods]</span><span class="sxs-lookup"><span data-stu-id="6d9a5-276">[Invoke a direct method on a device][lnk-methods]</span></span>
* <span data-ttu-id="6d9a5-277">[여러 장치에서 jobs 예약][lnk-jobs]</span><span class="sxs-lookup"><span data-stu-id="6d9a5-277">[Schedule jobs on multiple devices][lnk-jobs]</span></span>

<span data-ttu-id="6d9a5-278">이 문서에서 설명 하는 hello 개념 중 일부는 tootry, 원하는 경우 IoT Hub 자습서를 따라 hello에 관심이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d9a5-278">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorials:</span></span>

* <span data-ttu-id="6d9a5-279">[Toouse 장치로 이중 hello 하는 방법][lnk-twin-tutorial]</span><span class="sxs-lookup"><span data-stu-id="6d9a5-279">[How toouse hello device twin][lnk-twin-tutorial]</span></span>
* <span data-ttu-id="6d9a5-280">[어떻게 toouse 장치로 이중 속성][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="6d9a5-280">[How toouse device twin properties][lnk-twin-properties]</span></span>

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

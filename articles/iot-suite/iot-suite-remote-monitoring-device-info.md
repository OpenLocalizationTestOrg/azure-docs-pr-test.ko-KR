---
title: "원격 모니터링 솔루션의 장치 정보 메타데이터 | Microsoft Docs"
description: "Azure IoT에 대한 설명은 원격 모니터링 솔루션 및 해당 아키텍처를 미리 구성합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1b334769-103b-4eb0-a293-184f3d1ba9a3
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: f8fd452806a0a0b98cf8e434c9bd55700083a6c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="device-information-metadata-in-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="b323c-103">미리 구성된 원격 모니터링 솔루션의 장치 정보 메타데이터</span><span class="sxs-lookup"><span data-stu-id="b323c-103">Device information metadata in the remote monitoring preconfigured solution</span></span>

<span data-ttu-id="b323c-104">미리 구성된 Azure IoT Suite 원격 모니터링 솔루션은 장치 메타데이터를 관리하기 위한 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-104">The Azure IoT Suite remote monitoring preconfigured solution demonstrates an approach for managing device metadata.</span></span> <span data-ttu-id="b323c-105">이 문서에서는 이 솔루션이 취하는 방식을 이해할 수 있도록 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-105">This article outlines the approach this solution takes to enable you to understand:</span></span>

* <span data-ttu-id="b323c-106">솔루션이 저장한 장치 메타데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-106">What device metadata the solution stores.</span></span>
* <span data-ttu-id="b323c-107">솔루션이 장치 메타데이터를 관리하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-107">How the solution manages the device metadata.</span></span>

## <a name="context"></a><span data-ttu-id="b323c-108">Context</span><span class="sxs-lookup"><span data-stu-id="b323c-108">Context</span></span>

<span data-ttu-id="b323c-109">미리 구성된 원격 모니터링 솔루션은 [Azure IoT Hub][lnk-iot-hub]를 사용하여 장치가 클라우드로 데이터를 보낼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-109">The remote monitoring preconfigured solution uses [Azure IoT Hub][lnk-iot-hub] to enable your devices to send data to the cloud.</span></span> <span data-ttu-id="b323c-110">솔루션은 세 개의 서로 다른 위치에 장치에 대한 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-110">The solution stores information about devices in three different locations:</span></span>

| <span data-ttu-id="b323c-111">위치</span><span class="sxs-lookup"><span data-stu-id="b323c-111">Location</span></span> | <span data-ttu-id="b323c-112">저장된 정보</span><span class="sxs-lookup"><span data-stu-id="b323c-112">Information stored</span></span> | <span data-ttu-id="b323c-113">구현</span><span class="sxs-lookup"><span data-stu-id="b323c-113">Implementation</span></span> |
| -------- | ------------------ | -------------- |
| <span data-ttu-id="b323c-114">ID 레지스트리</span><span class="sxs-lookup"><span data-stu-id="b323c-114">Identity registry</span></span> | <span data-ttu-id="b323c-115">장치 ID, 인증 키, 사용 상태</span><span class="sxs-lookup"><span data-stu-id="b323c-115">Device id, authentication keys, enabled state</span></span> | <span data-ttu-id="b323c-116">IoT Hub에 기본 제공</span><span class="sxs-lookup"><span data-stu-id="b323c-116">Built in to IoT Hub</span></span> |
| <span data-ttu-id="b323c-117">장치 쌍</span><span class="sxs-lookup"><span data-stu-id="b323c-117">Device twins</span></span> | <span data-ttu-id="b323c-118">메타데이터: reported 속성, desired 속성, 태그</span><span class="sxs-lookup"><span data-stu-id="b323c-118">Metadata: reported properties, desired properties, tags</span></span> | <span data-ttu-id="b323c-119">IoT Hub에 기본 제공</span><span class="sxs-lookup"><span data-stu-id="b323c-119">Built in to IoT Hub</span></span> |
| <span data-ttu-id="b323c-120">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b323c-120">Cosmos DB</span></span> | <span data-ttu-id="b323c-121">명령 및 메서드 기록</span><span class="sxs-lookup"><span data-stu-id="b323c-121">Command and method history</span></span> | <span data-ttu-id="b323c-122">솔루션에 대한 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="b323c-122">Custom for solution</span></span> |

<span data-ttu-id="b323c-123">IoT Hub는 IoT Hub에 대한 액세스를 관리하는 [장치 ID 레지스트리][lnk-identity-registry]를 포함하고 [장치 쌍][lnk-device-twin]을 사용하여 장치 메타데이터를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-123">IoT Hub includes a [device identity registry][lnk-identity-registry] to manage access to an IoT hub and uses [device twins][lnk-device-twin] to manage device metadata.</span></span> <span data-ttu-id="b323c-124">명령 및 메서드 기록을 저장하는 원격 모니터링 솔루션 특정 *장치 레지스트리*도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-124">There is also a remote monitoring solution-specific *device registry* that stores command and method history.</span></span> <span data-ttu-id="b323c-125">원격 모니터링 솔루션은 [Cosmos DB][lnk-docdb] 데이터베이스를 사용하여 명령 및 메서드 기록에 대한 사용자 지정 저장소를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-125">The remote monitoring solution uses a [Cosmos DB][lnk-docdb] database to implement a custom store for command and method history.</span></span>

> [!NOTE]
> <span data-ttu-id="b323c-126">미리 구성된 원격 모니터링 솔루션은 Cosmos DB 데이터베이스의 정보와 동기화된 장치 ID 레지스트리를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-126">The remote monitoring preconfigured solution keeps the device identity registry in sync with the information in the Cosmos DB database.</span></span> <span data-ttu-id="b323c-127">둘 다 동일한 장치 ID를 사용하여 IoT Hub에 연결된 각 장치를 고유하게 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-127">Both use the same device id to uniquely identify each device connected to your IoT hub.</span></span>

## <a name="device-metadata"></a><span data-ttu-id="b323c-128">장치 메타데이터</span><span class="sxs-lookup"><span data-stu-id="b323c-128">Device metadata</span></span>

<span data-ttu-id="b323c-129">IoT Hub는 원격 모니터링 솔루션에 연결된 각 시뮬레이션된 장치 및 물리적 장치에 대한 [장치 쌍][lnk-device-twin]을 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-129">IoT Hub maintains a [device twin][lnk-device-twin] for each simulated and physical device connected to a remote monitoring solution.</span></span> <span data-ttu-id="b323c-130">솔루션은 장치 쌍을 사용하여 장치와 연결된 메타데이터를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-130">The solution uses device twins to manage the metadata associated with devices.</span></span> <span data-ttu-id="b323c-131">장치 쌍은 IoT Hub에서 유지 관리하는 JSON 문서이며 솔루션은 IoT Hub API를 사용하여 장치 쌍과 상호 작용합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-131">A device twin is a JSON document maintained by IoT Hub, and the solution uses the IoT Hub API to interact with device twins.</span></span>

<span data-ttu-id="b323c-132">장치 쌍은 세 가지 유형의 메타데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-132">A device twin stores three types of metadata:</span></span>

- <span data-ttu-id="b323c-133">장치에서 *Reported 속성*이 IoT Hub로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-133">*Reported properties* are sent to an IoT hub by a device.</span></span> <span data-ttu-id="b323c-134">원격 모니터링 솔루션에서 시뮬레이션된 장치는 시작 시와 **장치 상태 변경** 명령 및 메서드에 대한 응답으로 reported 속성을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-134">In the remote monitoring solution, simulated devices send reported properties at start-up and in response to **Change device state** commands and methods.</span></span> <span data-ttu-id="b323c-135">솔루션 포털의 **장치 목록** 및 **장치 세부 정보**에서 reported 속성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-135">You can view reported properties in the **Device list** and **Device details** in the solution portal.</span></span> <span data-ttu-id="b323c-136">reported 속성은 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-136">Reported properties are read only.</span></span>
- <span data-ttu-id="b323c-137">장치에 의해 *desired 속성*이 IoT Hub에서 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-137">*Desired properties* are retrieved from the IoT hub by devices.</span></span> <span data-ttu-id="b323c-138">장치에 대한 모든 필요한 구성을 변경하는 것은 장치의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-138">It is the responsibility of the device to make any necessary configuration change on the device.</span></span> <span data-ttu-id="b323c-139">reported 속성으로 허브에 변경 내용을 보고하는 것도 장치의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-139">It is also the responsibility of the device to report the change back to the hub as a reported property.</span></span> <span data-ttu-id="b323c-140">솔루션 포털을 통해 desired 속성 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-140">You can set a desired property value through the solution portal.</span></span>
- <span data-ttu-id="b323c-141">*태그*는 장치 쌍에만 존재하며 장치와 동기화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-141">*Tags* only exist in the device twin and are never synchronized with a device.</span></span> <span data-ttu-id="b323c-142">솔루션 포털에서 태그 값을 설정하고 장치 목록을 필터링 할 때 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-142">You can set tag values in the solution portal and use them when you filter the list of devices.</span></span> <span data-ttu-id="b323c-143">또한 솔루션은 태그를 사용하여 솔루션 포털에서 장치에 대해 표시할 아이콘을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-143">The solution also uses a tag to identify the icon to display for a device in the solution portal.</span></span>

<span data-ttu-id="b323c-144">시뮬레이션된 장치의 예제 reported 속성은 제조업체, 모델 번호, 위도 및 경도를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-144">Example reported properties from the simulated devices include manufacturer, model number, latitude, and longitude.</span></span> <span data-ttu-id="b323c-145">시뮬레이션된 장치는 reported 속성으로 지원되는 메서드의 목록도 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-145">Simulated devices also return the list of supported methods as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="b323c-146">시뮬레이션된 장치 코드는 **Desired.Config.TemperatureMeanValue** 및 **Desired.Config.TelemetryInterval** desired 속성만을 사용하여 IoT Hub로 다시 전송된 reported 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-146">The simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties sent back to IoT Hub.</span></span> <span data-ttu-id="b323c-147">다른 모든 desired 속성 변경 요청은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-147">All other desired property change requests are ignored.</span></span>

<span data-ttu-id="b323c-148">장치 레지스트리 Cosmos DB 데이터베이스에 저장된 장치 정보 메타데이터 JSON 문서는 다음과 같은 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-148">A device information metadata JSON document stored in the device registry Cosmos DB database has the following structure:</span></span>

```json
{
  "DeviceProperties": {
    "DeviceID": "deviceid1",
    "HubEnabledState": null,
    "CreatedTime": "2016-04-25T23:54:01.313802Z",
    "DeviceState": "normal",
    "UpdatedTime": null
    },
  "SystemProperties": {
    "ICCID": null
  },
  "Commands": [],
  "CommandHistory": [],
  "IsSimulatedDevice": false,
  "id": "fe81a81c-bcbc-4970-81f4-7f12f2d8bda8"
}
```

> [!NOTE]
> <span data-ttu-id="b323c-149">장치 정보는 장치가 IoT Hub에 전송하는 원격 분석을 설명하는 메타데이터를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-149">Device information can also include metadata to describe the telemetry the device sends to IoT Hub.</span></span> <span data-ttu-id="b323c-150">원격 모니터링 솔루션은 원격 분석 메타데이터를 사용하여 대시보드가 [동적 원격 분석][lnk-dynamic-telemetry]을 표시하는 방법을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-150">The remote monitoring solution uses this telemetry metadata to customize how the dashboard displays [dynamic telemetry][lnk-dynamic-telemetry].</span></span>

## <a name="lifecycle"></a><span data-ttu-id="b323c-151">수명 주기</span><span class="sxs-lookup"><span data-stu-id="b323c-151">Lifecycle</span></span>

<span data-ttu-id="b323c-152">솔루션 포털에서 장치를 처음 만들 때 솔루션은 Cosmos DB 데이터베이스에 항목을 만들어 명령 및 메서드 기록을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-152">When you first create a device in the solution portal, the solution creates an entry in the Cosmos DB database to store command and method history.</span></span> <span data-ttu-id="b323c-153">또한 이 시점에서 솔루션은 장치가 IoT Hub로 인증하는 데 사용할 키를 생성하는 장치 ID 레지스트리에서 장치에 대한 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-153">At this point, the solution also creates an entry for the device in the device identity registry, which generates the keys the device uses to authenticate with IoT Hub.</span></span> <span data-ttu-id="b323c-154">또한 장치 쌍을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-154">It also creates a device twin.</span></span>

<span data-ttu-id="b323c-155">장치가 솔루션에 처음 연결되면 reported 속성 및 장치 정보 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-155">When a device first connects to the solution, it sends reported properties and a device information message.</span></span> <span data-ttu-id="b323c-156">reported 속성 값은 장치 쌍에 자동으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-156">The reported property values are automatically saved in the device twin.</span></span> <span data-ttu-id="b323c-157">reported 속성은 장치 제조업체, 모델 번호, 일련 번호 및 지원되는 메서드의 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-157">The reported properties include the device manufacturer, model number, serial number, and a list of supported methods.</span></span> <span data-ttu-id="b323c-158">장치 정보 메시지는 명령 매개 변수에 대한 정보를 비롯하여 장치에서 지원하는 명령 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-158">The device information message includes the list of the commands the device supports including information about any command parameters.</span></span> <span data-ttu-id="b323c-159">솔루션이 이 메시지를 받으면 Cosmos DB 데이터베이스의 장치 정보를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-159">When the solution receives this message, it updates the device information in the Cosmos DB database.</span></span>

### <a name="view-and-edit-device-information-in-the-solution-portal"></a><span data-ttu-id="b323c-160">솔루션 포털에서 장치 정보 보기 및 편집</span><span class="sxs-lookup"><span data-stu-id="b323c-160">View and edit device information in the solution portal</span></span>

<span data-ttu-id="b323c-161">솔루션 포털의 장치 목록은 기본적으로 **상태**, **DeviceId**, **제조업체**, **모델 번호**, **일련 번호**, **펌웨어**, **플랫폼**, **프로세서**, **설치된 RAM** 등의 장치 속성을 열로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-161">The device list in the solution portal displays the following device properties as columns by default: **Status**, **DeviceId**, **Manufacturer**, **Model Number**, **Serial Number**, **Firmware**, **Platform**, **Processor**, and **Installed RAM**.</span></span> <span data-ttu-id="b323c-162">**열 편집기**를 클릭하여 열을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-162">You can customize the columns by clicking **Column editor**.</span></span> <span data-ttu-id="b323c-163">장치 속성 **위도** 및 **경도**는 대시보드의 Bing 맵에서 위치를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-163">The device properties **Latitude** and **Longitude** drive the location in the Bing Map on the dashboard.</span></span>

![장치 목록의 열 편집기][img-device-list]

<span data-ttu-id="b323c-165">솔루션 포털의 **장치 세부 정보** 창에서 desired 속성 및 태그를 편집할 수 있습니다(reported 속성은 읽기 전용).</span><span class="sxs-lookup"><span data-stu-id="b323c-165">In the **Device Details** pane in the solution portal, you can edit desired properties and tags (reported properties are read only).</span></span>

![장치 세부 정보 창][img-device-edit]

<span data-ttu-id="b323c-167">솔루션 포털을 사용하여 솔루션에서 장치를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-167">You can use the solution portal to remove a device from your solution.</span></span> <span data-ttu-id="b323c-168">장치를 제거하면 솔루션은 ID 레지스트리에서 장치 항목을 제거한 다음 장치 쌍을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-168">When you remove a device, the solution removes the device entry from identity registry and then deletes the device twin.</span></span> <span data-ttu-id="b323c-169">또한 솔루션은 Cosmos DB 데이터베이스에서 장치와 관련된 정보를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-169">The solution also removes information related to the device from the Cosmos DB database.</span></span> <span data-ttu-id="b323c-170">장치를 사용하지 않도록 설정해야 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-170">Before you can remove a device, you must disable it.</span></span>

![장치 제거][img-device-remove]

## <a name="device-information-message-processing"></a><span data-ttu-id="b323c-172">장치 정보 메시지 처리</span><span class="sxs-lookup"><span data-stu-id="b323c-172">Device information message processing</span></span>

<span data-ttu-id="b323c-173">장치에서 보낸 장치 정보 메시지는 원격 분석 메시지와 구별됩니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-173">Device information messages sent by a device are distinct from telemetry messages.</span></span> <span data-ttu-id="b323c-174">장치 정보 메시지는 장치가 응답할 수 있는 명령 및 모든 명령 기록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-174">Device information messages include the commands a device can respond to, and any command history.</span></span> <span data-ttu-id="b323c-175">IoT Hub 자체에는 장치 정보 메시지에 포함된 메타데이터의 정보가 없으며 장치-클라우드 메시지를 처리하는 것과 동일한 방식으로 메시지를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-175">IoT Hub itself has no knowledge of the metadata contained in a device information message and processes the message in the same way it processes any device-to-cloud message.</span></span> <span data-ttu-id="b323c-176">원격 모니터링 솔루션에서 [Azure 스트림 분석][lnk-stream-analytics](ASA) 작업은 IoT Hub의 메시지를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-176">In the remote monitoring solution, an [Azure Stream Analytics][lnk-stream-analytics] (ASA) job reads the messages from IoT Hub.</span></span> <span data-ttu-id="b323c-177">**DeviceInfo** Stream Analytics 작업은 **"ObjectType": "DeviceInfo"**를 포함하는 메시지를 필터링하고 웹 작업에서 실행되는 **EventProcessorHost** 호스트 인스턴스에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-177">The **DeviceInfo** stream analytics job filters for messages that contain **"ObjectType": "DeviceInfo"** and forwards them to the **EventProcessorHost** host instance that runs in a web job.</span></span> <span data-ttu-id="b323c-178">**EventProcessorHost** 인스턴스의 논리는 장치 ID를 사용하여 특정 장치에 대한 Cosmos DB 레코드를 찾아 레코드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-178">Logic in the **EventProcessorHost** instance uses the device id to find the Cosmos DB record for the specific device and update the record.</span></span>

> [!NOTE]
> <span data-ttu-id="b323c-179">장치 정보 메시지는 표준 장치-클라우드 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-179">A device information message is a standard device-to-cloud message.</span></span> <span data-ttu-id="b323c-180">솔루션은 ASA 쿼리를 사용하여 장치 정보 메시지와 원격 분석 메시지를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-180">The solution distinguishes between device information messages and telemetry messages by using ASA queries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b323c-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b323c-181">Next steps</span></span>

<span data-ttu-id="b323c-182">지금까지 미리 구성된 솔루션은 사용자 지정하는 방법을 살펴보았으므로 IoT Suite의 미리 구성된 솔루션이 제공하는 기능 및 기타 특징에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b323c-182">Now you've finished learning how you can customize the preconfigured solutions, you can explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="b323c-183">[예측 정비 사전 구성 솔루션 개요][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="b323c-183">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* <span data-ttu-id="b323c-184">[IoT Suite에 대한 질문과 대답][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="b323c-184">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="b323c-185">[처음부터 IoT 보안을 고려][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="b323c-185">[IoT security from the ground up][lnk-security-groundup]</span></span>

<!-- Images and links -->
[img-device-list]: media/iot-suite-remote-monitoring-device-info/image1.png
[img-device-edit]: media/iot-suite-remote-monitoring-device-info/image2.png
[img-device-remove]: media/iot-suite-remote-monitoring-device-info/image3.png

[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-docdb]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md

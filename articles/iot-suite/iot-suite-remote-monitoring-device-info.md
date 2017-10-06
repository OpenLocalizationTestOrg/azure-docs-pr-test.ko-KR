---
title: "원격 모니터링 솔루션 hello에 aaaDevice 정보 메타 데이터 | Microsoft Docs"
description: "Hello 미리 구성 된 Azure IoT 솔루션 원격 모니터링 및 해당 아키텍처의 설명입니다."
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
ms.openlocfilehash: 8387b98b8b2ae4934b0c900bc4df37dc17337c60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="device-information-metadata-in-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="aa11b-103">Hello 원격 모니터링 미리 구성 된 솔루션에서에서 장치 정보 메타 데이터</span><span class="sxs-lookup"><span data-stu-id="aa11b-103">Device information metadata in hello remote monitoring preconfigured solution</span></span>

<span data-ttu-id="aa11b-104">hello Azure IoT Suite 모니터링 솔루션 미리 구성 된 원격 장치 메타 데이터를 관리 하기 위한 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-104">hello Azure IoT Suite remote monitoring preconfigured solution demonstrates an approach for managing device metadata.</span></span> <span data-ttu-id="aa11b-105">이 문서에서는 hello 방법을 간단히 설명이 솔루션은 tooenable toounderstand 있습니다:</span><span class="sxs-lookup"><span data-stu-id="aa11b-105">This article outlines hello approach this solution takes tooenable you toounderstand:</span></span>

* <span data-ttu-id="aa11b-106">어떤 장치 메타 데이터 hello 솔루션을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-106">What device metadata hello solution stores.</span></span>
* <span data-ttu-id="aa11b-107">어떻게 hello 솔루션 hello 장치 메타 데이터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-107">How hello solution manages hello device metadata.</span></span>

## <a name="context"></a><span data-ttu-id="aa11b-108">Context</span><span class="sxs-lookup"><span data-stu-id="aa11b-108">Context</span></span>

<span data-ttu-id="aa11b-109">hello 원격 모니터링 미리 구성 된 솔루션에서는 [Azure IoT Hub] [ lnk-iot-hub] tooenable 프로그램 장치 toosend 데이터 toohello 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-109">hello remote monitoring preconfigured solution uses [Azure IoT Hub][lnk-iot-hub] tooenable your devices toosend data toohello cloud.</span></span> <span data-ttu-id="aa11b-110">hello 솔루션 장치에 대 한 정보는 다음 세 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-110">hello solution stores information about devices in three different locations:</span></span>

| <span data-ttu-id="aa11b-111">위치</span><span class="sxs-lookup"><span data-stu-id="aa11b-111">Location</span></span> | <span data-ttu-id="aa11b-112">저장된 정보</span><span class="sxs-lookup"><span data-stu-id="aa11b-112">Information stored</span></span> | <span data-ttu-id="aa11b-113">구현</span><span class="sxs-lookup"><span data-stu-id="aa11b-113">Implementation</span></span> |
| -------- | ------------------ | -------------- |
| <span data-ttu-id="aa11b-114">ID 레지스트리</span><span class="sxs-lookup"><span data-stu-id="aa11b-114">Identity registry</span></span> | <span data-ttu-id="aa11b-115">장치 ID, 인증 키, 사용 상태</span><span class="sxs-lookup"><span data-stu-id="aa11b-115">Device id, authentication keys, enabled state</span></span> | <span data-ttu-id="aa11b-116">기본 제공된 tooIoT 허브</span><span class="sxs-lookup"><span data-stu-id="aa11b-116">Built in tooIoT Hub</span></span> |
| <span data-ttu-id="aa11b-117">장치 쌍</span><span class="sxs-lookup"><span data-stu-id="aa11b-117">Device twins</span></span> | <span data-ttu-id="aa11b-118">메타데이터: reported 속성, desired 속성, 태그</span><span class="sxs-lookup"><span data-stu-id="aa11b-118">Metadata: reported properties, desired properties, tags</span></span> | <span data-ttu-id="aa11b-119">기본 제공된 tooIoT 허브</span><span class="sxs-lookup"><span data-stu-id="aa11b-119">Built in tooIoT Hub</span></span> |
| <span data-ttu-id="aa11b-120">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="aa11b-120">Cosmos DB</span></span> | <span data-ttu-id="aa11b-121">명령 및 메서드 기록</span><span class="sxs-lookup"><span data-stu-id="aa11b-121">Command and method history</span></span> | <span data-ttu-id="aa11b-122">솔루션에 대한 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="aa11b-122">Custom for solution</span></span> |

<span data-ttu-id="aa11b-123">IoT Hub를 포함 한 [장치 id 레지스트리에서] [ lnk-identity-registry] toomanage tooan IoT hub 및 사용 하 여 액세스 [장치 트윈스] [ lnk-device-twin] toomanage 장치 메타 데이터 .</span><span class="sxs-lookup"><span data-stu-id="aa11b-123">IoT Hub includes a [device identity registry][lnk-identity-registry] toomanage access tooan IoT hub and uses [device twins][lnk-device-twin] toomanage device metadata.</span></span> <span data-ttu-id="aa11b-124">명령 및 메서드 기록을 저장하는 원격 모니터링 솔루션 특정 *장치 레지스트리*도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-124">There is also a remote monitoring solution-specific *device registry* that stores command and method history.</span></span> <span data-ttu-id="aa11b-125">hello 원격 모니터링 솔루션에서 사용 하는 [Cosmos DB] [ lnk-docdb] 데이터베이스 tooimplement 명령과 메서드 기록에 대 한 사용자 지정 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-125">hello remote monitoring solution uses a [Cosmos DB][lnk-docdb] database tooimplement a custom store for command and method history.</span></span>

> [!NOTE]
> <span data-ttu-id="aa11b-126">미리 구성 된 솔루션 모니터링 원격 hello hello Cosmos DB 데이터베이스의 hello 정보 동기화 hello 장치 id 레지스트리에서 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-126">hello remote monitoring preconfigured solution keeps hello device identity registry in sync with hello information in hello Cosmos DB database.</span></span> <span data-ttu-id="aa11b-127">둘 다에 동일한 장치 id toouniquely 식별 하는 hello 사용 각 장치가 tooyour IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-127">Both use hello same device id toouniquely identify each device connected tooyour IoT hub.</span></span>

## <a name="device-metadata"></a><span data-ttu-id="aa11b-128">장치 메타데이터</span><span class="sxs-lookup"><span data-stu-id="aa11b-128">Device metadata</span></span>

<span data-ttu-id="aa11b-129">IoT Hub를 유지 관리는 [장치로 이중] [ lnk-device-twin] 각 시뮬레이션 및 물리적 장치에 대 한 모니터링 솔루션 원격 tooa를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-129">IoT Hub maintains a [device twin][lnk-device-twin] for each simulated and physical device connected tooa remote monitoring solution.</span></span> <span data-ttu-id="aa11b-130">hello 솔루션 장치 트윈스 toomanage hello 메타 데이터에 연결 된 장치를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-130">hello solution uses device twins toomanage hello metadata associated with devices.</span></span> <span data-ttu-id="aa11b-131">장치로 이중은 JSON 문서 IoT 허브에서 유지 관리 하 고 hello 솔루션 장치 트윈스와 IoT 허브 API toointeract hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-131">A device twin is a JSON document maintained by IoT Hub, and hello solution uses hello IoT Hub API toointeract with device twins.</span></span>

<span data-ttu-id="aa11b-132">장치 쌍은 세 가지 유형의 메타데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-132">A device twin stores three types of metadata:</span></span>

- <span data-ttu-id="aa11b-133">*속성을 보고* tooan IoT 허브는 장치에서 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-133">*Reported properties* are sent tooan IoT hub by a device.</span></span> <span data-ttu-id="aa11b-134">Hello 원격 솔루션 모니터링, 시뮬레이션 된 장치 보냅니다 보고 속성 시작에 대 한 응답 너무**장치 상태 변경** 명령과 메서드.</span><span class="sxs-lookup"><span data-stu-id="aa11b-134">In hello remote monitoring solution, simulated devices send reported properties at start-up and in response too**Change device state** commands and methods.</span></span> <span data-ttu-id="aa11b-135">Hello의 보고 속성을 볼 수 **장치 목록** 및 **장치 세부 정보** hello 솔루션 포털에서입니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-135">You can view reported properties in hello **Device list** and **Device details** in hello solution portal.</span></span> <span data-ttu-id="aa11b-136">reported 속성은 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-136">Reported properties are read only.</span></span>
- <span data-ttu-id="aa11b-137">*원하는 속성을* hello IoT hub에서 장치에 의해 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-137">*Desired properties* are retrieved from hello IoT hub by devices.</span></span> <span data-ttu-id="aa11b-138">hello hello 장치 toomake hello 장치에 필요한 구성 변경의 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-138">It is hello responsibility of hello device toomake any necessary configuration change on hello device.</span></span> <span data-ttu-id="aa11b-139">보고 된 속성으로 hello 장치 tooreport hello 변경 백 toohello 허브의 hello 책임 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-139">It is also hello responsibility of hello device tooreport hello change back toohello hub as a reported property.</span></span> <span data-ttu-id="aa11b-140">Hello 솔루션 포털을 통해 원하는 속성 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-140">You can set a desired property value through hello solution portal.</span></span>
- <span data-ttu-id="aa11b-141">*태그* hello 장치로 이중에만 존재 하며 장치와 동기화 되지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-141">*Tags* only exist in hello device twin and are never synchronized with a device.</span></span> <span data-ttu-id="aa11b-142">Hello 솔루션 포털의 태그 값을 설정할 수 있으며 장치 hello 목록을 필터링 할 때 사용.</span><span class="sxs-lookup"><span data-stu-id="aa11b-142">You can set tag values in hello solution portal and use them when you filter hello list of devices.</span></span> <span data-ttu-id="aa11b-143">또한 hello 솔루션 hello 솔루션 포털에서 장치에 대 한 태그 tooidentify hello 아이콘 toodisplay를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-143">hello solution also uses a tag tooidentify hello icon toodisplay for a device in hello solution portal.</span></span>

<span data-ttu-id="aa11b-144">예제 보고 제조업체, 모델 번호, 위도 및 경도 hello 시뮬레이션 된 장치에서 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-144">Example reported properties from hello simulated devices include manufacturer, model number, latitude, and longitude.</span></span> <span data-ttu-id="aa11b-145">시뮬레이션 된 장치 hello 목록은 지원 되는 방법 보고 된 속성으로 반환할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-145">Simulated devices also return hello list of supported methods as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="aa11b-146">hello 시뮬레이션 된 장치 코드만 사용 하 여 hello **Desired.Config.TemperatureMeanValue** 및 **Desired.Config.TelemetryInterval** 원하는 속성이 tooupdate hello 보고 다시 전송 속성 tooIoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-146">hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties sent back tooIoT Hub.</span></span> <span data-ttu-id="aa11b-147">다른 모든 desired 속성 변경 요청은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-147">All other desired property change requests are ignored.</span></span>

<span data-ttu-id="aa11b-148">Hello 장치 레지스트리 Cosmos DB 데이터베이스에 저장 된 장치 정보 메타 데이터가 JSON 문서 구조를 다음 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-148">A device information metadata JSON document stored in hello device registry Cosmos DB database has hello following structure:</span></span>

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
> <span data-ttu-id="aa11b-149">장치 정보는 메타 데이터 toodescribe hello 원격 분석 hello 장치 보냅니다 tooIoT 허브를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-149">Device information can also include metadata toodescribe hello telemetry hello device sends tooIoT Hub.</span></span> <span data-ttu-id="aa11b-150">원격 모니터링 솔루션 hello이 원격 분석 메타 데이터 toocustomize hello 대시보드 표시 하는 방법을 사용 하 여 [동적 원격 분석][lnk-dynamic-telemetry]합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-150">hello remote monitoring solution uses this telemetry metadata toocustomize how hello dashboard displays [dynamic telemetry][lnk-dynamic-telemetry].</span></span>

## <a name="lifecycle"></a><span data-ttu-id="aa11b-151">수명 주기</span><span class="sxs-lookup"><span data-stu-id="aa11b-151">Lifecycle</span></span>

<span data-ttu-id="aa11b-152">Hello 솔루션 포털에서 장치를 처음 만들면 hello Cosmos DB 데이터베이스 toostore 명령에에서 항목 및 메서드 기록 hello 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-152">When you first create a device in hello solution portal, hello solution creates an entry in hello Cosmos DB database toostore command and method history.</span></span> <span data-ttu-id="aa11b-153">이 시점에서 hello 솔루션은 또한 IoT Hub와 hello 키 hello 장치 사용 하 여 tooauthenticate를 생성 하는 hello 장치 id 레지스트리에서의 hello 장치에 대 한 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-153">At this point, hello solution also creates an entry for hello device in hello device identity registry, which generates hello keys hello device uses tooauthenticate with IoT Hub.</span></span> <span data-ttu-id="aa11b-154">또한 장치 쌍을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-154">It also creates a device twin.</span></span>

<span data-ttu-id="aa11b-155">장치는 먼저 toohello 솔루션 연결을 보고 된 속성과 장치 정보 메시지가 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-155">When a device first connects toohello solution, it sends reported properties and a device information message.</span></span> <span data-ttu-id="aa11b-156">hello 보고 속성 값은 자동으로 hello 장치로 이중에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-156">hello reported property values are automatically saved in hello device twin.</span></span> <span data-ttu-id="aa11b-157">hello 보고 속성에는 hello 장치 제조업체, 모델 번호, 일련 번호 및 지원 되는 메서드의 목록을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-157">hello reported properties include hello device manufacturer, model number, serial number, and a list of supported methods.</span></span> <span data-ttu-id="aa11b-158">hello 장치 정보 메시지 hello를 지 원하는 모든 명령 매개 변수에 대 한 정보를 포함 하 여 hello 명령의 hello 목록을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-158">hello device information message includes hello list of hello commands hello device supports including information about any command parameters.</span></span> <span data-ttu-id="aa11b-159">이 메시지를 수신 하는 hello 솔루션 hello Cosmos DB 데이터베이스의 hello 장치 정보를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-159">When hello solution receives this message, it updates hello device information in hello Cosmos DB database.</span></span>

### <a name="view-and-edit-device-information-in-hello-solution-portal"></a><span data-ttu-id="aa11b-160">보기 및 hello 솔루션 포털에서 장치 정보를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-160">View and edit device information in hello solution portal</span></span>

<span data-ttu-id="aa11b-161">hello hello 솔루션 포털에서 장치 목록을 표시 다음과 같은 장치 속성 열으로 기본적으로 hello: **상태**, **DeviceId**, **제조업체**, **모델 번호**, **일련 번호**, **펌웨어**, **플랫폼**, **프로세서**, 및  **RAM을 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-161">hello device list in hello solution portal displays hello following device properties as columns by default: **Status**, **DeviceId**, **Manufacturer**, **Model Number**, **Serial Number**, **Firmware**, **Platform**, **Processor**, and **Installed RAM**.</span></span> <span data-ttu-id="aa11b-162">클릭 하 여 hello 열을 사용자 지정할 수 **열 편집기**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-162">You can customize hello columns by clicking **Column editor**.</span></span> <span data-ttu-id="aa11b-163">장치 속성 hello **위도** 및 **경도** hello 대시보드에서 hello Bing 지도에서 위치 hello 드라이브입니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-163">hello device properties **Latitude** and **Longitude** drive hello location in hello Bing Map on hello dashboard.</span></span>

![장치 목록의 열 편집기][img-device-list]

<span data-ttu-id="aa11b-165">Hello에 **장치 세부 정보** 창 hello 솔루션 포털에서 원하는 속성 및 태그 편집할 수 있습니다 (속성은 읽기 전용 보고 됨).</span><span class="sxs-lookup"><span data-stu-id="aa11b-165">In hello **Device Details** pane in hello solution portal, you can edit desired properties and tags (reported properties are read only).</span></span>

![장치 세부 정보 창][img-device-edit]

<span data-ttu-id="aa11b-167">솔루션에서 hello 솔루션 포털 tooremove 장치를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-167">You can use hello solution portal tooremove a device from your solution.</span></span> <span data-ttu-id="aa11b-168">장치를 제거 하면 hello 솔루션 id 레지스트리에에서 hello 장치 항목을 제거 하 고 hello 장치로 이중을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-168">When you remove a device, hello solution removes hello device entry from identity registry and then deletes hello device twin.</span></span> <span data-ttu-id="aa11b-169">또한 hello 솔루션 정보 관련된 toohello 장치가 hello Cosmos DB 데이터베이스에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-169">hello solution also removes information related toohello device from hello Cosmos DB database.</span></span> <span data-ttu-id="aa11b-170">장치를 사용하지 않도록 설정해야 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-170">Before you can remove a device, you must disable it.</span></span>

![장치 제거][img-device-remove]

## <a name="device-information-message-processing"></a><span data-ttu-id="aa11b-172">장치 정보 메시지 처리</span><span class="sxs-lookup"><span data-stu-id="aa11b-172">Device information message processing</span></span>

<span data-ttu-id="aa11b-173">장치에서 보낸 장치 정보 메시지는 원격 분석 메시지와 구별됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-173">Device information messages sent by a device are distinct from telemetry messages.</span></span> <span data-ttu-id="aa11b-174">장치 정보 메시지는 장치에 응답할 수 하는 hello 명령 및 모든 명령 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-174">Device information messages include hello commands a device can respond to, and any command history.</span></span> <span data-ttu-id="aa11b-175">IoT 허브 자체 장치 정보 메시지에 포함 된 hello 메타 데이터의 알지 못하며 프로세스 hello 메시지 hello에 동일한 방식으로 모든 장치-클라우드 메시지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-175">IoT Hub itself has no knowledge of hello metadata contained in a device information message and processes hello message in hello same way it processes any device-to-cloud message.</span></span> <span data-ttu-id="aa11b-176">Hello 모니터링 솔루션을 원격에 [Azure 스트림 분석] [ lnk-stream-analytics] (ASA) 작업 IoT 허브에서 hello 메시지를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-176">In hello remote monitoring solution, an [Azure Stream Analytics][lnk-stream-analytics] (ASA) job reads hello messages from IoT Hub.</span></span> <span data-ttu-id="aa11b-177">hello **DeviceInfo** 스트림 분석 작업이 포함 된 메시지에 대 한 필터 **"ObjectType": "DeviceInfo"** toohello 전달 **EventProcessorHost** 호스트 웹 작업에서 실행 되는 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="aa11b-177">hello **DeviceInfo** stream analytics job filters for messages that contain **"ObjectType": "DeviceInfo"** and forwards them toohello **EventProcessorHost** host instance that runs in a web job.</span></span> <span data-ttu-id="aa11b-178">Hello에서 논리 **EventProcessorHost** 인스턴스 hello 장치 id toofind hello Cosmos DB 레코드를 사용 하 여 hello 특정 장치 및 update hello 레코드에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-178">Logic in hello **EventProcessorHost** instance uses hello device id toofind hello Cosmos DB record for hello specific device and update hello record.</span></span>

> [!NOTE]
> <span data-ttu-id="aa11b-179">장치 정보 메시지는 표준 장치-클라우드 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-179">A device information message is a standard device-to-cloud message.</span></span> <span data-ttu-id="aa11b-180">hello 솔루션 ASA 쿼리를 사용 하 여 장치 정보 메시지 및 원격 분석 메시지 간을 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-180">hello solution distinguishes between device information messages and telemetry messages by using ASA queries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa11b-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aa11b-181">Next steps</span></span>

<span data-ttu-id="aa11b-182">미리 구성 하는 hello 솔루션 사용자 지정할 수 학습 했으면 이제 다른 기능 및 hello IoT Suite 미리 구성 된 솔루션의 기능을 hello 중 일부 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa11b-182">Now you've finished learning how you can customize hello preconfigured solutions, you can explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="aa11b-183">[예측 정비 사전 구성 솔루션 개요][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="aa11b-183">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* <span data-ttu-id="aa11b-184">[IoT Suite에 대한 질문과 대답][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="aa11b-184">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="aa11b-185">[Hello 접지에서 IoT 보안][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="aa11b-185">[IoT security from hello ground up][lnk-security-groundup]</span></span>

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

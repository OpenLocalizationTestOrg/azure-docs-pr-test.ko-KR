---
title: "aaaRemote 미리 구성 된 모니터링 솔루션 연습 | Microsoft Docs"
description: "Hello 미리 구성 된 Azure IoT 솔루션 원격 모니터링 및 해당 아키텍처의 설명입니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57a336bd94938c2b9ee5d3456ea8e45446cf3d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a><span data-ttu-id="d7b4f-103">미리 구성된 원격 모니터링 솔루션 연습</span><span class="sxs-lookup"><span data-stu-id="d7b4f-103">Remote monitoring preconfigured solution walkthrough</span></span>

<span data-ttu-id="d7b4f-104">원격 모니터링 IoT Suite hello [솔루션 미리 구성 된] [ lnk-preconfigured-solutions] 는에 종단 간 구현 원격 위치에서 실행 되는 여러 컴퓨터에 대 한 솔루션을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-104">hello IoT Suite remote monitoring [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end monitoring solution for multiple machines running in remote locations.</span></span> <span data-ttu-id="d7b4f-105">hello 솔루션 핵심 Azure 서비스 tooprovide hello 비즈니스 시나리오의 제네릭 구현을 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-105">hello solution combines key Azure services tooprovide a generic implementation of hello business scenario.</span></span> <span data-ttu-id="d7b4f-106">사용자 고유의 구현에 대 한 시작 점으로 hello 솔루션을 사용할 수 있습니다 및 [사용자 지정] [ lnk-customize] 것 toomeet 특정 비즈니스 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-106">You can use hello solution as a starting point for your own implementation and [customize][lnk-customize] it toomeet your own specific business requirements.</span></span>

<span data-ttu-id="d7b4f-107">이 문서에서는 hello hello 원격 모니터링 솔루션 tooenable의 핵심 요소 중 일부를 통해 toounderstand 작동 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-107">This article walks you through some of hello key elements of hello remote monitoring solution tooenable you toounderstand how it works.</span></span> <span data-ttu-id="d7b4f-108">이 정보는 다음 항목을 도울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-108">This knowledge helps you to:</span></span>

* <span data-ttu-id="d7b4f-109">Hello 솔루션의 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-109">Troubleshoot issues in hello solution.</span></span>
* <span data-ttu-id="d7b4f-110">계획 방법을 toocustomize toohello 솔루션 toomeet 특정 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-110">Plan how toocustomize toohello solution toomeet your own specific requirements.</span></span> 
* <span data-ttu-id="d7b4f-111">Azure 서비스를 사용하는 고유한 IoT 솔루션을 디자인합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-111">Design your own IoT solution that uses Azure services.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="d7b4f-112">논리 아키텍처</span><span class="sxs-lookup"><span data-stu-id="d7b4f-112">Logical architecture</span></span>

<span data-ttu-id="d7b4f-113">다음 다이어그램 hello hello hello 미리 구성 된 솔루션의 논리적 구성 요소를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-113">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![논리 아키텍처](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a><span data-ttu-id="d7b4f-115">시뮬레이션된 장치</span><span class="sxs-lookup"><span data-stu-id="d7b4f-115">Simulated devices</span></span>

<span data-ttu-id="d7b4f-116">미리 구성 하는 hello 솔루션 hello 시뮬레이션 된 장치를 냉각 장치를 (예: 건물 공조 장치 또는 시설 공기 처리 장치)를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-116">In hello preconfigured solution, hello simulated device represents a cooling device (such as a building air conditioner or facility air handling unit).</span></span> <span data-ttu-id="d7b4f-117">자동으로에서 실행 되는 4 개의 시뮬레이션 된 장치를 프로 비전 hello 미리 구성 된 솔루션을 배포 하는 경우는 [Azure WebJob][lnk-webjobs]합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-117">When you deploy hello preconfigured solution, you also automatically provision four simulated devices that run in an [Azure WebJob][lnk-webjobs].</span></span> <span data-ttu-id="d7b4f-118">시뮬레이션 된 hello 장치 쉽게 동작에 대 한 있습니다 tooexplore hello hello 필요 toodeploy 없이 hello 솔루션의 모든 물리적 장치 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-118">hello simulated devices make it easy for you tooexplore hello behavior of hello solution without hello need toodeploy any physical devices.</span></span> <span data-ttu-id="d7b4f-119">실제 장치 toodeploy 참조 hello [원격 미리 구성 된 솔루션을 모니터링 하 여 장치 toohello 연결] [ lnk-connect-rm] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-119">toodeploy a real physical device, see hello [Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

### <a name="device-to-cloud-messages"></a><span data-ttu-id="d7b4f-120">장치-클라우드 메시지</span><span class="sxs-lookup"><span data-stu-id="d7b4f-120">Device-to-cloud messages</span></span>

<span data-ttu-id="d7b4f-121">각 시뮬레이션 된 장치는 다음 메시지 유형을 tooIoT 허브 hello를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-121">Each simulated device can send hello following message types tooIoT Hub:</span></span>

| <span data-ttu-id="d7b4f-122">Message</span><span class="sxs-lookup"><span data-stu-id="d7b4f-122">Message</span></span> | <span data-ttu-id="d7b4f-123">설명</span><span class="sxs-lookup"><span data-stu-id="d7b4f-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d7b4f-124">시작</span><span class="sxs-lookup"><span data-stu-id="d7b4f-124">Startup</span></span> |<span data-ttu-id="d7b4f-125">Hello 장치 시작 될 때 보냅니다는 **장치 정보** toohello 백 엔드 자체에 대 한 정보를 포함 하는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-125">When hello device starts, it sends a **device-info** message containing information about itself toohello back end.</span></span> <span data-ttu-id="d7b4f-126">이 데이터는 hello 장치 id와 hello 명령 목록을 포함 하 고 메서드 hello 장치 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-126">This data includes hello device id and a list of hello commands and methods hello device supports.</span></span> |
| <span data-ttu-id="d7b4f-127">현재 상태</span><span class="sxs-lookup"><span data-stu-id="d7b4f-127">Presence</span></span> |<span data-ttu-id="d7b4f-128">정기적으로 전송 하는 장치는 **존재** hello 장치 센서의 hello 존재를 감지할 수 있는지 여부를 tooreport 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-128">A device periodically sends a **presence** message tooreport whether hello device can sense hello presence of a sensor.</span></span> |
| <span data-ttu-id="d7b4f-129">원격 분석</span><span class="sxs-lookup"><span data-stu-id="d7b4f-129">Telemetry</span></span> |<span data-ttu-id="d7b4f-130">정기적으로 전송 하는 장치는 **원격 분석** hello 온도 및 습도 hello 장치에서 수집에 대 한 시뮬레이션 된 값을 보고 하는 메시지의 센서를 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-130">A device periodically sends a **telemetry** message that reports simulated values for hello temperature and humidity collected from hello device's simulated sensors.</span></span> |

> [!NOTE]
> <span data-ttu-id="d7b4f-131">hello 솔루션 hello hello 장치로 이중 아니라 Cosmos DB 데이터베이스에 hello 장치에서 지원 되는 명령 목록을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-131">hello solution stores hello list of commands supported by hello device in a Cosmos DB database and not in hello device twin.</span></span>

### <a name="properties-and-device-twins"></a><span data-ttu-id="d7b4f-132">속성 및 장치 쌍</span><span class="sxs-lookup"><span data-stu-id="d7b4f-132">Properties and device twins</span></span>

<span data-ttu-id="d7b4f-133">hello 시뮬레이션 된 장치 보낼 장치 속성 toohello 다음 hello [로 이중] [ lnk-device-twins] 으로 hello IoT 허브에서 *속성을 보고*합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-133">hello simulated devices send hello following device properties toohello [twin][lnk-device-twins] in hello IoT hub as *reported properties*.</span></span> <span data-ttu-id="d7b4f-134">hello 장치 보냅니다 보고 속성 시작 시와 응답 tooa에서 **장치 상태 변경** 명령 또는 메서드.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-134">hello device sends reported properties at startup and in response tooa **Change Device State** command or method.</span></span>

| <span data-ttu-id="d7b4f-135">속성</span><span class="sxs-lookup"><span data-stu-id="d7b4f-135">Property</span></span> | <span data-ttu-id="d7b4f-136">목적</span><span class="sxs-lookup"><span data-stu-id="d7b4f-136">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="d7b4f-137">Config.TelemetryInterval</span><span class="sxs-lookup"><span data-stu-id="d7b4f-137">Config.TelemetryInterval</span></span> | <span data-ttu-id="d7b4f-138">원격 분석을 전송 하는 빈도 (초) hello 장치</span><span class="sxs-lookup"><span data-stu-id="d7b4f-138">Frequency (seconds) hello device sends telemetry</span></span> |
| <span data-ttu-id="d7b4f-139">Config.TemperatureMeanValue</span><span class="sxs-lookup"><span data-stu-id="d7b4f-139">Config.TemperatureMeanValue</span></span> | <span data-ttu-id="d7b4f-140">시뮬레이션 된 hello 온도 원격 분석을 위한 hello 평균 값 지정</span><span class="sxs-lookup"><span data-stu-id="d7b4f-140">Specifies hello mean value for hello simulated temperature telemetry</span></span> |
| <span data-ttu-id="d7b4f-141">Device.DeviceID</span><span class="sxs-lookup"><span data-stu-id="d7b4f-141">Device.DeviceID</span></span> |<span data-ttu-id="d7b4f-142">제공 되거나 hello 솔루션에 장치를 만들 때 할당 하는 id</span><span class="sxs-lookup"><span data-stu-id="d7b4f-142">Id that is either provided or assigned when a device is created in hello solution</span></span> |
| <span data-ttu-id="d7b4f-143">Device.DeviceState</span><span class="sxs-lookup"><span data-stu-id="d7b4f-143">Device.DeviceState</span></span> | <span data-ttu-id="d7b4f-144">Hello 장치에서 보고 한 상태</span><span class="sxs-lookup"><span data-stu-id="d7b4f-144">State reported by hello device</span></span> |
| <span data-ttu-id="d7b4f-145">Device.CreatedTime</span><span class="sxs-lookup"><span data-stu-id="d7b4f-145">Device.CreatedTime</span></span> |<span data-ttu-id="d7b4f-146">시간 hello 장치 hello 솔루션에서 만들었을</span><span class="sxs-lookup"><span data-stu-id="d7b4f-146">Time hello device was created in hello solution</span></span> |
| <span data-ttu-id="d7b4f-147">Device.StartupTime</span><span class="sxs-lookup"><span data-stu-id="d7b4f-147">Device.StartupTime</span></span> |<span data-ttu-id="d7b4f-148">시작 된 시간 hello 장치</span><span class="sxs-lookup"><span data-stu-id="d7b4f-148">Time hello device was started</span></span> |
| <span data-ttu-id="d7b4f-149">Device.LastDesiredPropertyChange</span><span class="sxs-lookup"><span data-stu-id="d7b4f-149">Device.LastDesiredPropertyChange</span></span> |<span data-ttu-id="d7b4f-150">hello 마지막 원하는 속성의 hello 버전 번호 변경</span><span class="sxs-lookup"><span data-stu-id="d7b4f-150">hello version number of hello last desired property change</span></span> |
| <span data-ttu-id="d7b4f-151">Device.Location.Latitude</span><span class="sxs-lookup"><span data-stu-id="d7b4f-151">Device.Location.Latitude</span></span> |<span data-ttu-id="d7b4f-152">Hello 장치의 위도 위치</span><span class="sxs-lookup"><span data-stu-id="d7b4f-152">Latitude location of hello device</span></span> |
| <span data-ttu-id="d7b4f-153">Device.Location.Longitude</span><span class="sxs-lookup"><span data-stu-id="d7b4f-153">Device.Location.Longitude</span></span> |<span data-ttu-id="d7b4f-154">Hello 장치의 경도 위치</span><span class="sxs-lookup"><span data-stu-id="d7b4f-154">Longitude location of hello device</span></span> |
| <span data-ttu-id="d7b4f-155">System.Manufacturer</span><span class="sxs-lookup"><span data-stu-id="d7b4f-155">System.Manufacturer</span></span> |<span data-ttu-id="d7b4f-156">장치 제조업체</span><span class="sxs-lookup"><span data-stu-id="d7b4f-156">Device manufacturer</span></span> |
| <span data-ttu-id="d7b4f-157">System.ModelNumber</span><span class="sxs-lookup"><span data-stu-id="d7b4f-157">System.ModelNumber</span></span> |<span data-ttu-id="d7b4f-158">Hello 장치의 모델 번호</span><span class="sxs-lookup"><span data-stu-id="d7b4f-158">Model number of hello device</span></span> |
| <span data-ttu-id="d7b4f-159">System.SerialNumber</span><span class="sxs-lookup"><span data-stu-id="d7b4f-159">System.SerialNumber</span></span> |<span data-ttu-id="d7b4f-160">Hello 장치의 일련 번호</span><span class="sxs-lookup"><span data-stu-id="d7b4f-160">Serial number of hello device</span></span> |
| <span data-ttu-id="d7b4f-161">System.FirmwareVersion</span><span class="sxs-lookup"><span data-stu-id="d7b4f-161">System.FirmwareVersion</span></span> |<span data-ttu-id="d7b4f-162">현재 버전의 hello 장치에 펌웨어</span><span class="sxs-lookup"><span data-stu-id="d7b4f-162">Current version of firmware on hello device</span></span> |
| <span data-ttu-id="d7b4f-163">System.Platform</span><span class="sxs-lookup"><span data-stu-id="d7b4f-163">System.Platform</span></span> |<span data-ttu-id="d7b4f-164">Hello 장치의 플랫폼 아키텍처</span><span class="sxs-lookup"><span data-stu-id="d7b4f-164">Platform architecture of hello device</span></span> |
| <span data-ttu-id="d7b4f-165">System.Processor</span><span class="sxs-lookup"><span data-stu-id="d7b4f-165">System.Processor</span></span> |<span data-ttu-id="d7b4f-166">실행 중인 hello 장치 프로세서</span><span class="sxs-lookup"><span data-stu-id="d7b4f-166">Processor running hello device</span></span> |
| <span data-ttu-id="d7b4f-167">System.InstalledRAM</span><span class="sxs-lookup"><span data-stu-id="d7b4f-167">System.InstalledRAM</span></span> |<span data-ttu-id="d7b4f-168">Hello 장치에 설치 된 RAM 크기</span><span class="sxs-lookup"><span data-stu-id="d7b4f-168">Amount of RAM installed on hello device</span></span> |

<span data-ttu-id="d7b4f-169">hello 시뮬레이터 초기값 예제 값을 사용 하 여 시뮬레이션 된 장치에서 이러한 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-169">hello simulator seeds these properties in simulated devices with sample values.</span></span> <span data-ttu-id="d7b4f-170">시뮬레이션 된 장치, hello 장치를 초기화 하는 hello 시뮬레이터 때마다 보고 된 속성으로 hello 미리 정의 된 메타 데이터 tooIoT 허브를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-170">Each time hello simulator initializes a simulated device, hello device reports hello pre-defined metadata tooIoT Hub as reported properties.</span></span> <span data-ttu-id="d7b4f-171">Hello 장치에 의해 보고 된 속성을 업데이트할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-171">Reported properties can only be updated by hello device.</span></span> <span data-ttu-id="d7b4f-172">보고 속성 toochange 솔루션 포털에서 원하는 속성 설정.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-172">toochange a reported property, you set a desired property in solution portal.</span></span> <span data-ttu-id="d7b4f-173">hello 장치를 hello 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-173">It is hello responsibility of hello device to:</span></span>

1. <span data-ttu-id="d7b4f-174">주기적으로 hello IoT 허브에서 원하는 속성을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-174">Periodically retrieve desired properties from hello IoT hub.</span></span>
2. <span data-ttu-id="d7b4f-175">원하는 hello 속성 값으로 구성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-175">Update its configuration with hello desired property value.</span></span>
3. <span data-ttu-id="d7b4f-176">보고 된 속성으로 새 값 백 toohello 허브를 hello를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-176">Send hello new value back toohello hub as a reported property.</span></span>

<span data-ttu-id="d7b4f-177">Hello 솔루션 대시보드에서 사용할 수 있습니다 *원하는 속성을* hello를 사용 하 여 장치에서 tooset 속성 [장치로 이중][lnk-device-twins]합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-177">From hello solution dashboard, you can use *desired properties* tooset properties on a device by using hello [device twin][lnk-device-twins].</span></span> <span data-ttu-id="d7b4f-178">일반적으로 장치는 hello 허브 tooupdate 보고 속성으로 다시 변경의 내부 상태 및 보고서 hello에서에서 원하는 속성 값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-178">Typically, a device reads a desired property value from hello hub tooupdate its internal state and report hello change back as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="d7b4f-179">hello 시뮬레이션 된 장치 코드만 사용 하 여 hello **Desired.Config.TemperatureMeanValue** 및 **Desired.Config.TelemetryInterval** 원하는 속성이 tooupdate hello 보고 다시 전송 속성 tooIoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-179">hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties sent back tooIoT Hub.</span></span> <span data-ttu-id="d7b4f-180">Hello 시뮬레이션 된 장치에 다른 모든 원하는 속성 변경 요청은 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-180">All other desired property change requests are ignored in hello simulated device.</span></span>

### <a name="methods"></a><span data-ttu-id="d7b4f-181">메서드</span><span class="sxs-lookup"><span data-stu-id="d7b4f-181">Methods</span></span>

<span data-ttu-id="d7b4f-182">hello 시뮬레이션 된 장치 처리할 수 있는 메서드를 다음 hello ([메서드를 직접][lnk-direct-methods]) hello IoT 허브를 통해 hello 솔루션 포털에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-182">hello simulated devices can handle hello following methods ([direct methods][lnk-direct-methods]) invoked from hello solution portal through hello IoT hub:</span></span>

| <span data-ttu-id="d7b4f-183">메서드</span><span class="sxs-lookup"><span data-stu-id="d7b4f-183">Method</span></span> | <span data-ttu-id="d7b4f-184">설명</span><span class="sxs-lookup"><span data-stu-id="d7b4f-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d7b4f-185">InitiateFirmwareUpdate</span><span class="sxs-lookup"><span data-stu-id="d7b4f-185">InitiateFirmwareUpdate</span></span> |<span data-ttu-id="d7b4f-186">Hello 장치 tooperform 펌웨어 업데이트를 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-186">Instructs hello device tooperform a firmware update</span></span> |
| <span data-ttu-id="d7b4f-187">Reboot</span><span class="sxs-lookup"><span data-stu-id="d7b4f-187">Reboot</span></span> |<span data-ttu-id="d7b4f-188">Hello 장치 tooreboot을 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-188">Instructs hello device tooreboot</span></span> |
| <span data-ttu-id="d7b4f-189">FactoryReset</span><span class="sxs-lookup"><span data-stu-id="d7b4f-189">FactoryReset</span></span> |<span data-ttu-id="d7b4f-190">공장 기본 설정 hello 장치 tooperform을 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-190">Instructs hello device tooperform a factory reset</span></span> |

<span data-ttu-id="d7b4f-191">일부 메서드는 진행률에 tooreport 보고 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-191">Some methods use reported properties tooreport on progress.</span></span> <span data-ttu-id="d7b4f-192">예를 들어 hello **InitiateFirmwareUpdate** 메서드 시뮬레이션 hello 장치에 비동기적으로 실행 중인 hello 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-192">For example, hello **InitiateFirmwareUpdate** method simulates running hello update asynchronously on hello device.</span></span> <span data-ttu-id="d7b4f-193">hello 메서드 hello 장치에 즉시 반환 hello 비동기 작업이 계속 toosend 상태 업데이트를 다시 사용 하 여 toohello 솔루션 대시보드 보고 속성.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-193">hello method returns immediately on hello device, while hello asynchronous task continues toosend status updates back toohello solution dashboard using reported properties.</span></span>

### <a name="commands"></a><span data-ttu-id="d7b4f-194">명령</span><span class="sxs-lookup"><span data-stu-id="d7b4f-194">Commands</span></span>

<span data-ttu-id="d7b4f-195">시뮬레이션 된 hello 장치 hello hello IoT 허브를 통해 hello 솔루션 포털에서 전송 되는 명령을 (클라우드-장치 메시지의 경우) 다음 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-195">hello simulated devices can handle hello following commands (cloud-to-device messages) sent from hello solution portal through hello IoT hub:</span></span>

| <span data-ttu-id="d7b4f-196">명령</span><span class="sxs-lookup"><span data-stu-id="d7b4f-196">Command</span></span> | <span data-ttu-id="d7b4f-197">설명</span><span class="sxs-lookup"><span data-stu-id="d7b4f-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d7b4f-198">PingDevice</span><span class="sxs-lookup"><span data-stu-id="d7b4f-198">PingDevice</span></span> |<span data-ttu-id="d7b4f-199">보냅니다는 *ping* toohello 장치 toocheck 자신이 활성 상태임</span><span class="sxs-lookup"><span data-stu-id="d7b4f-199">Sends a *ping* toohello device toocheck it is alive</span></span> |
| <span data-ttu-id="d7b4f-200">StartTelemetry</span><span class="sxs-lookup"><span data-stu-id="d7b4f-200">StartTelemetry</span></span> |<span data-ttu-id="d7b4f-201">원격 분석 보내기 시작 hello 장치</span><span class="sxs-lookup"><span data-stu-id="d7b4f-201">Starts hello device sending telemetry</span></span> |
| <span data-ttu-id="d7b4f-202">StopTelemetry</span><span class="sxs-lookup"><span data-stu-id="d7b4f-202">StopTelemetry</span></span> |<span data-ttu-id="d7b4f-203">원격 분석 전송에서 중지 hello 장치</span><span class="sxs-lookup"><span data-stu-id="d7b4f-203">Stops hello device from sending telemetry</span></span> |
| <span data-ttu-id="d7b4f-204">ChangeSetPointTemp</span><span class="sxs-lookup"><span data-stu-id="d7b4f-204">ChangeSetPointTemp</span></span> |<span data-ttu-id="d7b4f-205">난수 데이터 생성 되는 hello 주위 변경 hello 지점 설정 값</span><span class="sxs-lookup"><span data-stu-id="d7b4f-205">Changes hello set point value around which hello random data is generated</span></span> |
| <span data-ttu-id="d7b4f-206">DiagnosticTelemetry</span><span class="sxs-lookup"><span data-stu-id="d7b4f-206">DiagnosticTelemetry</span></span> |<span data-ttu-id="d7b4f-207">트리거 hello 장치 시뮬레이터 toosend 원격 분석 추가 값 (externalTemp)</span><span class="sxs-lookup"><span data-stu-id="d7b4f-207">Triggers hello device simulator toosend an additional telemetry value (externalTemp)</span></span> |
| <span data-ttu-id="d7b4f-208">ChangeDeviceState</span><span class="sxs-lookup"><span data-stu-id="d7b4f-208">ChangeDeviceState</span></span> |<span data-ttu-id="d7b4f-209">Hello 장치에 대 한 확장 된 상태 속성을 변경 하 고 hello 장치에서 hello 장치 정보 메시지를 전송</span><span class="sxs-lookup"><span data-stu-id="d7b4f-209">Changes an extended state property for hello device and sends hello device info message from hello device</span></span> |

> [!NOTE]
> <span data-ttu-id="d7b4f-210">이러한 명령(클라우드-장치 메시지) 및 메서드(직접 메서드)의 비교는 [클라우드-장치 통신 지침][lnk-c2d-guidance]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-210">For a comparison of these commands (cloud-to-device messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

## <a name="iot-hub"></a><span data-ttu-id="d7b4f-211">IoT 허브</span><span class="sxs-lookup"><span data-stu-id="d7b4f-211">IoT Hub</span></span>

<span data-ttu-id="d7b4f-212">hello [IoT hub] [ lnk-iothub] hello 장치에서 hello 클라우드로 전송 되는 데이터를 수집 하 고 사용할 수 있는 toohello Azure 스트림 분석 ASA () 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-212">hello [IoT hub][lnk-iothub] ingests data sent from hello devices into hello cloud and makes it available toohello Azure Stream Analytics (ASA) jobs.</span></span> <span data-ttu-id="d7b4f-213">각 스트림 ASA 작업에는 별도 IoT Hub 소비자 그룹 tooread hello 메시지 스트림을 하 여 장치에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-213">Each stream ASA job uses a separate IoT Hub consumer group tooread hello stream of messages from your devices.</span></span>

<span data-ttu-id="d7b4f-214">또한 hello 솔루션에서 IoT hub를 hello:</span><span class="sxs-lookup"><span data-stu-id="d7b4f-214">hello IoT hub in hello solution also:</span></span>

- <span data-ttu-id="d7b4f-215">Hello id와 tooconnect toohello 포털을 허용 하는 모든 hello 장치 인증 키를 저장 하는 id 레지스트리에 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-215">Maintains an identity registry that stores hello ids and authentication keys of all hello devices permitted tooconnect toohello portal.</span></span> <span data-ttu-id="d7b4f-216">사용 및 id 레지스트리에 hello 통해 장치를 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-216">You can enable and disable devices through hello identity registry.</span></span>
- <span data-ttu-id="d7b4f-217">Hello 솔루션 포털을 대신 하 여 명령을 tooyour 장치를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-217">Sends commands tooyour devices on behalf of hello solution portal.</span></span>
- <span data-ttu-id="d7b4f-218">Hello 솔루션 포털을 대신 하 여 장치에 대 한 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-218">Invokes methods on your devices on behalf of hello solution portal.</span></span>
- <span data-ttu-id="d7b4f-219">등록된 모든 장치에 대한 장치 쌍을 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-219">Maintains device twins for all registered devices.</span></span> <span data-ttu-id="d7b4f-220">장치로 이중 장치에서 보고 하는 hello 속성 값을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-220">A device twin stores hello property values reported by a device.</span></span> <span data-ttu-id="d7b4f-221">또한 장치로 이중 hello 장치 tooretrieve 다음 연결에 대 한 hello 솔루션 포털에서 설정 하는 원하는 속성을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-221">A device twin also stores desired properties, set in hello solution portal, for hello device tooretrieve when it next connects.</span></span>
- <span data-ttu-id="d7b4f-222">일정을 여러 장치에 대 한 tooset 속성 작업 또는 여러 장치에서 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-222">Schedules jobs tooset properties for multiple devices or invoke methods on multiple devices.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="d7b4f-223">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d7b4f-223">Azure Stream Analytics</span></span>

<span data-ttu-id="d7b4f-224">Hello 모니터링 솔루션을 원격에 [Azure 스트림 분석] [ lnk-asa] ASA ()는 처리 또는 저장에 대 한 hello IoT 허브 tooother 백 엔드 구성 요소에서 받은 장치 메시지를 디스패치합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-224">In hello remote monitoring solution, [Azure Stream Analytics][lnk-asa] (ASA) dispatches device messages received by hello IoT hub tooother back-end components for processing or storage.</span></span> <span data-ttu-id="d7b4f-225">다른 ASA 작업 hello 메시지의 hello 내용을 기반으로 하는 특정 기능을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-225">Different ASA jobs perform specific functions based on hello content of hello messages.</span></span>

<span data-ttu-id="d7b4f-226">**작업 1: 장치 정보** hello 들어오는 메시지 스트림의 장치 정보 메시지를 필터링 하 고 tooan 이벤트 허브 끝점으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-226">**Job 1: Device Info** filters device information messages from hello incoming message stream and sends them tooan Event Hub endpoint.</span></span> <span data-ttu-id="d7b4f-227">시작 시와 응답 tooa에는 장치에서 장치 정보 메시지를 전송 **SendDeviceInfo** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-227">A device sends device information messages at startup and in response tooa **SendDeviceInfo** command.</span></span> <span data-ttu-id="d7b4f-228">이 작업에 다음 쿼리 정의 tooidentify hello 사용 하 여 **장치 정보** 메시지:</span><span class="sxs-lookup"><span data-stu-id="d7b4f-228">This job uses hello following query definition tooidentify **device-info** messages:</span></span>

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

<span data-ttu-id="d7b4f-229">이 작업은 추가 처리를 위해 해당 출력 tooan 이벤트 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-229">This job sends its output tooan Event Hub for further processing.</span></span>

<span data-ttu-id="d7b4f-230">**작업 2: 규칙** 은 장치 단위 임계값에 대해 들어오는 온도 및 습도 원격 분석 값을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-230">**Job 2: Rules** evaluates incoming temperature and humidity telemetry values against per-device thresholds.</span></span> <span data-ttu-id="d7b4f-231">임계값은 hello 솔루션 포털에서 사용할 수 있는 hello 규칙 편집기에서 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-231">Threshold values are set in hello rules editor available in hello solution portal.</span></span> <span data-ttu-id="d7b4f-232">각 장치/값 쌍은 **참조 데이터**로서 스트림 분석에서 읽는 Blob의 타임스탬프에 의해 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-232">Each device/value pair is stored by timestamp in a blob which Stream Analytics reads in as **Reference Data**.</span></span> <span data-ttu-id="d7b4f-233">hello 작업 hello 장치에 대 한 hello 설정한 임계값에 대 한 모든 비어 있지 않은 값을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-233">hello job compares any non-empty value against hello set threshold for hello device.</span></span> <span data-ttu-id="d7b4f-234">Hello 초과 하는 경우 ' >' hello 작업에서 출력 조건을 **경보** hello 임계값을 나타내는 이벤트를 초과 하 고 hello 장치, 값 및 타임 스탬프 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-234">If it exceeds hello '>' condition, hello job outputs an **alarm** event that indicates that hello threshold is exceeded and provides hello device, value, and timestamp values.</span></span> <span data-ttu-id="d7b4f-235">이 작업 경보를 트리거해야 하는 쿼리 정의 tooidentify 원격 분석 메시지 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-235">This job uses hello following query definition tooidentify telemetry messages that should trigger an alarm:</span></span>

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

<span data-ttu-id="d7b4f-236">hello 작업의 출력 tooan 이벤트 허브 추가 처리를 위해 보내고 hello 솔루션 포털 hello 경고 정보를 읽을 수 있는에서 각 경고 tooblob 저장소의 세부 정보를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-236">hello job sends its output tooan Event Hub for further processing and saves details of each alert tooblob storage from where hello solution portal can read hello alert information.</span></span>

<span data-ttu-id="d7b4f-237">**작업 3: 원격 분석** 에 두 가지 방법으로 hello 들어오는 장치 원격 분석 스트림에 대해 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-237">**Job 3: Telemetry** operates on hello incoming device telemetry stream in two ways.</span></span> <span data-ttu-id="d7b4f-238">먼저 hello 장기 저장에 대 한 hello 장치 toopersistent blob 저장소에서 모든 원격 분석 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-238">hello first sends all telemetry messages from hello devices toopersistent blob storage for long-term storage.</span></span> <span data-ttu-id="d7b4f-239">두 번째 hello 습도 평균, 최소 및 최대 5 분 슬라이딩 윈도우를 통해 값을이 데이터 tooblob 저장소 보냅니다를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-239">hello second computes average, minimum, and maximum humidity values over a five-minute sliding window and sends this data tooblob storage.</span></span> <span data-ttu-id="d7b4f-240">hello 솔루션 포털 blob 저장소 toopopulate hello 차트에서 hello 원격 분석 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-240">hello solution portal reads hello telemetry data from blob storage toopopulate hello charts.</span></span> <span data-ttu-id="d7b4f-241">이 작업에서는 쿼리 정의 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-241">This job uses hello following query definition:</span></span>

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a><span data-ttu-id="d7b4f-242">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d7b4f-242">Event Hubs</span></span>

<span data-ttu-id="d7b4f-243">hello **장치 정보** 및 **규칙** ASA 작업은 해당 데이터 tooEvent 허브 tooreliably 앞으로 toohello에 출력 **이벤트 프로세서** hello WebJob 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-243">hello **device info** and **rules** ASA jobs output their data tooEvent Hubs tooreliably forward on toohello **Event Processor** running in hello WebJob.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="d7b4f-244">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="d7b4f-244">Azure storage</span></span>

<span data-ttu-id="d7b4f-245">hello 솔루션 hello 솔루션에서 Azure blob 저장소 toopersist hello 장치에서 모든 hello 원시 및 요약 된 원격 분석 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-245">hello solution uses Azure blob storage toopersist all hello raw and summarized telemetry data from hello devices in hello solution.</span></span> <span data-ttu-id="d7b4f-246">hello 포털 blob 저장소 toopopulate hello 차트에서 hello 원격 분석 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-246">hello portal reads hello telemetry data from blob storage toopopulate hello charts.</span></span> <span data-ttu-id="d7b4f-247">toodisplay 경고 hello 솔루션 포털 데이터를 읽습니다 hello blob 저장소에서 기록 하는 원격 분석을 초과 하는 값 hello 임계값을 구성 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-247">toodisplay alerts, hello solution portal reads hello data from blob storage that records when telemetry values exceeded hello configured threshold values.</span></span> <span data-ttu-id="d7b4f-248">또한 hello 솔루션 hello 솔루션 포털에서 설정한 blob 저장소 toorecord hello 임계값 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-248">hello solution also uses blob storage toorecord hello threshold values you set in hello solution portal.</span></span>

## <a name="webjobs"></a><span data-ttu-id="d7b4f-249">웹 작업</span><span class="sxs-lookup"><span data-stu-id="d7b4f-249">WebJobs</span></span>

<span data-ttu-id="d7b4f-250">또한 toohosting hello 장치 시뮬레이터 hello WebJobs hello 솔루션에도 호스트 hello **이벤트 프로세서** 명령 응답을 처리 하는 Azure WebJob을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-250">In addition toohosting hello device simulators, hello WebJobs in hello solution also host hello **Event Processor** running in an Azure WebJob that handles command responses.</span></span> <span data-ttu-id="d7b4f-251">명령 응답 메시지 tooupdate hello 장치 명령 기록 (hello Cosmos DB 데이터베이스에 저장)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-251">It uses command response messages tooupdate hello device command history (stored in hello Cosmos DB database).</span></span>

## <a name="cosmos-db"></a><span data-ttu-id="d7b4f-252">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d7b4f-252">Cosmos DB</span></span>

<span data-ttu-id="d7b4f-253">hello 솔루션 hello 장치 연결 된 toohello 솔루션에 대 한 Cosmos DB 데이터베이스 toostore 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-253">hello solution uses a Cosmos DB database toostore information about hello devices connected toohello solution.</span></span> <span data-ttu-id="d7b4f-254">이 정보 hello 솔루션 포털에서 호출 된 메서드 및 toodevices hello 솔루션 포털에서 전송 되는 명령을의 hello 히스토리가 포함 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-254">This information includes hello history of commands sent toodevices from hello solution portal and of methods invoked from hello solution portal.</span></span>

## <a name="solution-portal"></a><span data-ttu-id="d7b4f-255">솔루션 포털</span><span class="sxs-lookup"><span data-stu-id="d7b4f-255">Solution portal</span></span>

<span data-ttu-id="d7b4f-256">hello 솔루션 포털은 hello 미리 구성 된 솔루션의 일부분으로 배포 하는 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-256">hello solution portal is a web app deployed as part of hello preconfigured solution.</span></span> <span data-ttu-id="d7b4f-257">hello 솔루션 포털의 주요 페이지 hello은 hello 대시보드 및 hello 장치 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-257">hello key pages in hello solution portal are hello dashboard and hello device list.</span></span>

### <a name="dashboard"></a><span data-ttu-id="d7b4f-258">대시보드</span><span class="sxs-lookup"><span data-stu-id="d7b4f-258">Dashboard</span></span>

<span data-ttu-id="d7b4f-259">PowerBI javascript 컨트롤을 사용 하는 hello 웹 응용 프로그램에서이 페이지 (참조 [powerbi-visuals 리포지토리](https://www.github.com/Microsoft/PowerBI-visuals)) hello 장치에서 toovisualize hello 원격 분석 데이터.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-259">This page in hello web app uses PowerBI javascript controls (See [PowerBI-visuals repo](https://www.github.com/Microsoft/PowerBI-visuals)) toovisualize hello telemetry data from hello devices.</span></span> <span data-ttu-id="d7b4f-260">hello 솔루션 hello ASA 원격 분석 작업 toowrite hello 원격 분석 데이터 tooblob 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-260">hello solution uses hello ASA telemetry job toowrite hello telemetry data tooblob storage.</span></span>

### <a name="device-list"></a><span data-ttu-id="d7b4f-261">장치 목록</span><span class="sxs-lookup"><span data-stu-id="d7b4f-261">Device list</span></span>

<span data-ttu-id="d7b4f-262">Hello 솔루션 포털에서이 페이지에서 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-262">From this page in hello solution portal you can:</span></span>

* <span data-ttu-id="d7b4f-263">새 장치를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-263">Provision a new device.</span></span> <span data-ttu-id="d7b4f-264">이 작업 hello 고유한 장치 id를 설정 하 고 hello 인증 키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-264">This action sets hello unique device id and generates hello authentication key.</span></span> <span data-ttu-id="d7b4f-265">Hello 장치 tooboth hello IoT Hub id 레지스트리에 대 한 정보와 hello 솔루션 별 Cosmos DB 데이터베이스 파일을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-265">It writes information about hello device tooboth hello IoT Hub identity registry and hello solution-specific Cosmos DB database.</span></span>
* <span data-ttu-id="d7b4f-266">장치 속성을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-266">Manage device properties.</span></span> <span data-ttu-id="d7b4f-267">이 작업은 기본 속성 보기 및 새 속성으로 업데이트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-267">This action includes viewing existing properties and updating with new properties.</span></span>
* <span data-ttu-id="d7b4f-268">명령을 tooa 장치를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-268">Send commands tooa device.</span></span>
* <span data-ttu-id="d7b4f-269">장치에 대 한 hello 명령 기록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-269">View hello command history for a device.</span></span>
* <span data-ttu-id="d7b4f-270">장치를 활성화하고 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-270">Enable and disable devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7b4f-271">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d7b4f-271">Next steps</span></span>

<span data-ttu-id="d7b4f-272">hello 다음 TechNet 블로그 게시물에 대해 자세히 모니터링 미리 구성 된 솔루션 원격 hello:</span><span class="sxs-lookup"><span data-stu-id="d7b4f-272">hello following TechNet blog posts provide more detail about hello remote monitoring preconfigured solution:</span></span>

* [<span data-ttu-id="d7b4f-273">IoT 속속들이 hello--아래 Suite 원격 모니터링</span><span class="sxs-lookup"><span data-stu-id="d7b4f-273">IoT Suite - Under hello Hood - Remote Monitoring</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [<span data-ttu-id="d7b4f-274">IoT 도구 모음 - 원격 모니터링 - 라이브 및 시뮬레이션된 장치 추가</span><span class="sxs-lookup"><span data-stu-id="d7b4f-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

<span data-ttu-id="d7b4f-275">Hello 다음 문서를 참조 하 여 IoT Suite를 시작 하기를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7b4f-275">You can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="d7b4f-276">[원격 미리 구성 된 솔루션을 모니터링 하 여 장치 toohello 연결][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="d7b4f-276">[Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="d7b4f-277">[Hello azureiotsuite.com 사이트에 대 한 권한][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="d7b4f-277">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md

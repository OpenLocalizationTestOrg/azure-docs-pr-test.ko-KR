---
title: "aaaCustomizing 미리 솔루션 구성 | Microsoft Docs"
description: "Toocustomize hello Azure IoT Suite 미리 솔루션을 구성 하는 방법에 지침을 제공 합니다."
services: 
suite: iot-suite
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4653ae53-4110-4a10-bd6c-7dc034c293a8
ms.service: iot-suite
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 1a8573f5ac6ed944c44459df495446f15174d513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="65f33-103">미리 구성된 솔루션 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="65f33-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="65f33-104">Azure IoT Suite hello와 함께 제공 되는 미리 구성 하는 hello 솔루션 hello hello suite 작업 함께 toodeliver 종단 간 솔루션 내에 서비스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-104">hello preconfigured solutions provided with hello Azure IoT Suite demonstrate hello services within hello suite working together toodeliver an end-to-end solution.</span></span> <span data-ttu-id="65f33-105">시작점을 확장 하 고 특정 시나리오에 대 한 hello 솔루션을 사용자 지정할 수 있는 다양 한 위치에는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-105">From this starting point, there are various places in which you can extend and customize hello solution for specific scenarios.</span></span> <span data-ttu-id="65f33-106">hello 다음 섹션에서는 이러한 일반적인 사용자 지정 위치를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-106">hello following sections describe these common customization points.</span></span>

## <a name="find-hello-source-code"></a><span data-ttu-id="65f33-107">Hello 소스 코드 찾기</span><span class="sxs-lookup"><span data-stu-id="65f33-107">Find hello source code</span></span>

<span data-ttu-id="65f33-108">hello 미리 구성 된 솔루션에 대 한 hello 소스 코드 리포지토리 다음 hello에 GitHub에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-108">hello source code for hello preconfigured solutions is available on GitHub in hello following repositories:</span></span>

* <span data-ttu-id="65f33-109">원격 모니터링: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="65f33-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="65f33-110">예측 유지 관리: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="65f33-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="65f33-111">연결된 팩터리: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="65f33-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="65f33-112">미리 구성 하는 hello 솔루션에 대 한 hello 소스 코드에는 사용 되는 Azure IoT Suite를 사용 하 여 IoT 솔루션의 tooimplement hello 종단 간 기능 toodemonstrate hello 패턴과 사례 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-112">hello source code for hello preconfigured solutions is provided toodemonstrate hello patterns and practices used tooimplement hello end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="65f33-113">방법에 대 한 자세한 정보를 찾을 수 toobuild hello GitHub 리포지토리에에서 hello 솔루션을 배포 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-113">You can find more information about how toobuild and deploy hello solutions in hello GitHub repositories.</span></span>

## <a name="change-hello-preconfigured-rules"></a><span data-ttu-id="65f33-114">변경 미리 구성 하는 hello 규칙</span><span class="sxs-lookup"><span data-stu-id="65f33-114">Change hello preconfigured rules</span></span>

<span data-ttu-id="65f33-115">hello 원격 모니터링 솔루션에 포함 된 3 개의 [Azure 스트림 분석](https://azure.microsoft.com/services/stream-analytics/) toohandle 장치 정보, 원격 분석 및 hello 솔루션에 규칙 논리를 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-115">hello remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs toohandle device information, telemetry, and rules logic in hello solution.</span></span>

<span data-ttu-id="65f33-116">hello 세 스트림 분석 작업 하 고 해당 구문 hello에서 자세히 설명 되어 [솔루션 연습을 미리 구성 된 원격 모니터링](iot-suite-remote-monitoring-sample-walkthrough.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-116">hello three stream analytics jobs and their syntax are described in depth in hello [Remote monitoring preconfigured solution walkthrough](iot-suite-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="65f33-117">이러한 작업 tooalter 논리를 hello 또는 특정 tooyour 시나리오 논리를 추가 하는 직접 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-117">You can edit these jobs directly tooalter hello logic, or add logic specific tooyour scenario.</span></span> <span data-ttu-id="65f33-118">찾을 수 있습니다 hello 스트림 분석 작업이 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-118">You can find hello Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="65f33-119">너무 이동[Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-119">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="65f33-120">하면 IoT 솔루션 이름이 hello로 toohello 리소스 그룹을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-120">Navigate toohello resource group with hello same name as your IoT solution.</span></span> 
3. <span data-ttu-id="65f33-121">Toomodify 원하는 hello Azure 스트림 분석 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-121">Select hello Azure Stream Analytics job you'd like toomodify.</span></span> 
4. <span data-ttu-id="65f33-122">선택 하 여 중지 hello 작업 **중지** hello 명령 집합에서.</span><span class="sxs-lookup"><span data-stu-id="65f33-122">Stop hello job by selecting **Stop** in hello set of commands.</span></span> 
5. <span data-ttu-id="65f33-123">Hello, 쿼리, 입력과 출력을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-123">Edit hello inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="65f33-124">간단한 수정을 hello에 대 한 toochange hello 쿼리 **규칙** 작업 toouse는 **"<"** 대신는 **">"**합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-124">A simple modification is toochange hello query for hello **Rules** job toouse a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="65f33-125">hello 솔루션 포털에 여전히 표시 **">"** 규칙을 편집 하지만 hello 동작은 toohello 변경 작업을 기본 hello 인해 대칭 이동 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-125">hello solution portal still shows **">"** when you edit a rule, but notice how hello behavior is flipped due toohello change in hello underlying job.</span></span>
6. <span data-ttu-id="65f33-126">Hello 작업 시작</span><span class="sxs-lookup"><span data-stu-id="65f33-126">Start hello job</span></span>

> [!NOTE]
> <span data-ttu-id="65f33-127">원격 모니터링 대시보드 hello hello 작업 변경 hello 대시보드 toofail을 줄 수 있으므로 특정 데이터에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-127">hello remote monitoring dashboard depends on specific data, so altering hello jobs can cause hello dashboard toofail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="65f33-128">사용자 고유 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="65f33-128">Add your own rules</span></span>

<span data-ttu-id="65f33-129">Toochanging hello 미리 Azure 스트림 분석 작업을 구성 하는 또한, hello Azure 포털 tooadd 새 작업을 사용 하거나 새 쿼리 tooexisting 작업을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-129">In addition toochanging hello preconfigured Azure Stream Analytics jobs, you can use hello Azure portal tooadd new jobs or add new queries tooexisting jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="65f33-130">장치 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="65f33-130">Customize devices</span></span>

<span data-ttu-id="65f33-131">Hello 가장 일반적인 확장 활동 중 하나를 장치 특정 tooyour 시나리오와 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-131">One of hello most common extension activities is working with devices specific tooyour scenario.</span></span> <span data-ttu-id="65f33-132">장치를 사용하는 여러 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-132">There are several methods for working with devices.</span></span> <span data-ttu-id="65f33-133">이러한 방법에는 시뮬레이션 된 장치 toomatch 시나리오를 변경 하거나 hello를 사용 하 여 포함 [IoT 장치 SDK] [ IoT Device SDK] tooconnect 물리적 장치 toohello 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-133">These methods include altering a simulated device toomatch your scenario, or using hello [IoT Device SDK][IoT Device SDK] tooconnect your physical device toohello solution.</span></span>

<span data-ttu-id="65f33-134">단계별 가이드 tooadding 장치에 대 한 참조 hello [Iot Suite 연결 장치](iot-suite-connecting-devices.md) 아티클과 hello [원격 C SDK 샘플 모니터링](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring)합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-134">For a step-by-step guide tooadding devices, see hello [Iot Suite Connecting Devices](iot-suite-connecting-devices.md) article and hello [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="65f33-135">이 샘플은 미리 구성 된 솔루션 모니터링 원격 hello로 디자인 된 toowork입니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-135">This sample is designed toowork with hello remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="65f33-136">고유한 시뮬레이션된 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="65f33-136">Create your own simulated device</span></span>

<span data-ttu-id="65f33-137">Hello에 포함 된 [모니터링 솔루션 소스 코드 원격](https://github.com/Azure/azure-iot-remote-monitoring)는.NET 시뮬레이터.</span><span class="sxs-lookup"><span data-stu-id="65f33-137">Included in hello [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="65f33-138">이 시뮬레이터는 hello hello 솔루션의 일부로 toosend 다른 메타 데이터를 원격 분석, alter 및 toodifferent 명령 및 메서드에 응답 수를 프로 비전 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-138">This simulator is hello one provisioned as part of hello solution and you can alter it toosend different metadata, telemetry, and respond toodifferent commands and methods.</span></span>

<span data-ttu-id="65f33-139">미리 구성 된 솔루션 모니터링 원격 hello에 미리 구성 된 시뮬레이터 hello 냉각기 장치 온도 및 습도 원격 분석입니다를 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-139">hello preconfigured simulator in hello remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="65f33-140">Hello에 hello 시뮬레이터를 수정할 수 있습니다 [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) 시기도 hello GitHub 리포지토리를 분기 했습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-140">You can modify hello simulator in hello [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked hello GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="65f33-141">시뮬레이션된 장치에 사용 가능한 위치</span><span class="sxs-lookup"><span data-stu-id="65f33-141">Available locations for simulated devices</span></span>

<span data-ttu-id="65f33-142">hello 기본 집합이 위치 시애틀/Redmond, Washington, 미국입니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-142">hello default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="65f33-143">[SampleDeviceFactory.cs][lnk-sample-device-factory]에서 이러한 위치를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-toohello-simulator"></a><span data-ttu-id="65f33-144">Toohello 시뮬레이터를 원하는 속성 업데이트 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-144">Add a desired property update handler toohello simulator</span></span>

<span data-ttu-id="65f33-145">Hello 솔루션 포털에서 장치에 대해 원하는 속성에 대 한 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-145">You can set a value for a desired property for a device in hello solution portal.</span></span> <span data-ttu-id="65f33-146">hello hello 장치 toohandle hello 속성 변경 요청의 필요한 hello 속성 값을 검색 하는 hello 장치 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-146">It is hello responsibility of hello device toohandle hello property change request when hello device retrieves hello desired property value.</span></span> <span data-ttu-id="65f33-147">속성 값 변경에 대 한 tooadd 지원을 원하는 속성을 통해 tooadd 처리기 toohello 시뮬레이터 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-147">tooadd support for a property value change through a desired property, you need tooadd a handler toohello simulator.</span></span>

<span data-ttu-id="65f33-148">hello에 대 한 처리기를 포함 하는 hello 시뮬레이터 **SetPointTemp** 및 **TelemetryInterval** 속성을 설정 하 여 업데이트할 수 있는 원하는 hello 솔루션 포털의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-148">hello simulator contains handlers for hello **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in hello solution portal.</span></span>

<span data-ttu-id="65f33-149">hello 다음 보여 주는 예제 hello에 대 한 hello 처리기 **SetPointTemp** hello에서 속성을 원하는 **CoolerDevice** 클래스:</span><span class="sxs-lookup"><span data-stu-id="65f33-149">hello following example shows hello handler for hello **SetPointTemp** desired property in hello **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="65f33-150">이 메서드는 온도 보고서 hello 백 tooIoT 허브 보고 속성을 설정 하 여 변경 하는 hello 원격 분석 지점을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-150">This method updates hello telemetry point temperature and then reports hello change back tooIoT Hub by setting a reported property.</span></span>

<span data-ttu-id="65f33-151">Hello 예제 앞에 다음 hello 패턴에 의해 사용자 고유의 속성에 대 한 고유의 처리기를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-151">You can add your own handlers for your own properties by following hello pattern in hello preceding example.</span></span>

<span data-ttu-id="65f33-152">바인딩해야 hello 원하는 속성 toohello 처리기 hello 다음 hello에서 예제에에서 표시 된 대로 **CoolerDevice** 생성자:</span><span class="sxs-lookup"><span data-stu-id="65f33-152">You must also bind hello desired property toohello handler as shown in hello following example from hello **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="65f33-153">**SetPointTempPropertyName**은 "Config.SetPointTemp"로 정의되는 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-toohello-simulator"></a><span data-ttu-id="65f33-154">새 메서드 toohello 시뮬레이터에 대 한 지원 추가</span><span class="sxs-lookup"><span data-stu-id="65f33-154">Add support for a new method toohello simulator</span></span>

<span data-ttu-id="65f33-155">새 항목에 대 한 hello 시뮬레이터 tooadd 지원 사용자 지정할 수 있습니다 [메서드 (직접)][lnk-direct-methods]합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-155">You can customize hello simulator tooadd support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="65f33-156">필요한 두 가지 주요 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-156">There are two key steps required:</span></span>

- <span data-ttu-id="65f33-157">hello 시뮬레이터 hello 메서드의 세부 정보를 사용 하 여 hello 미리 구성 된 솔루션의 hello IoT 허브에 알려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-157">hello simulator must notify hello IoT hub in hello preconfigured solution with details of hello method.</span></span>
- <span data-ttu-id="65f33-158">hello 시뮬레이터 hello에서 호출 하는 경우 코드 toohandle hello 메서드 호출을 포함 해야 **장치 세부 정보** hello 솔루션 탐색기에서 또는 작업을 통해 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-158">hello simulator must include code toohandle hello method call when you invoke it from hello **Device details** panel in hello solution explorer or through a job.</span></span>

<span data-ttu-id="65f33-159">hello 원격 모니터링 미리 구성 된 솔루션에서는 *속성을 보고* tooIoT 허브 지원 되는 방법의 toosend 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-159">hello remote monitoring preconfigured solution uses *reported properties* toosend details of supported methods tooIoT hub.</span></span> <span data-ttu-id="65f33-160">hello 솔루션 백 엔드를 메서드 호출의 기록와 함께 각 장치에서 지 원하는 모든 hello 메서드의 목록을 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-160">hello solution back end maintains a list of all hello methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="65f33-161">장치에 대 한이 정보를 볼 수 있으며 hello 솔루션 포털에서 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-161">You can view this information about devices and invoke methods in hello solution portal.</span></span>

<span data-ttu-id="65f33-162">장치는 메서드를 지원 하도록 toonotify hello IoT hub를 hello 장치 hello 메서드 toohello의 세부 정보를 추가 해야 **SupportedMethods** hello의 노드 속성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-162">toonotify hello IoT hub that a device supports a method, hello device must add details of hello method toohello **SupportedMethods** node in hello reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="65f33-163">hello 메서드 시그니처에 형식에 따라 hello: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-163">hello method signature has hello following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="65f33-164">예를 들어 toospecify hello **InitiateFirmwareUpdate** 메서드 라는 문자열 매개 변수를 기대 **FwPackageURI**, 메서드 시그니처를 다음 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="65f33-164">For example, toospecify hello **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use hello following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="65f33-165">지원 되는 매개 변수 형식의 목록에 대 한 참조 hello **CommandTypes** hello 인프라 프로젝트의 클래스.</span><span class="sxs-lookup"><span data-stu-id="65f33-165">For a list of supported parameter types, see hello **CommandTypes** class in hello Infrastructure project.</span></span>

<span data-ttu-id="65f33-166">메서드를 toodelete 너무 hello 메서드 시그니처를 설정`null` hello에 속성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-166">toodelete a method, set hello method signature too`null` in hello reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="65f33-167">hello 솔루션 백 엔드 업데이트 지원 되는 방법에 대 한 정보를 받을 때는 *장치 정보* hello 장치에서 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-167">hello solution back end only updates information about supported methods when it receives a *device information* message from hello device.</span></span>

<span data-ttu-id="65f33-168">다음 코드 샘플을 hello hello **SampleDeviceFactory** hello 공통 클래스 프로젝트 표시 방법을 tooadd 방법 toohello 목록의 **SupportedMethods** hello 보고 hello 전송한 속성 장치:</span><span class="sxs-lookup"><span data-stu-id="65f33-168">hello following code sample from hello **SampleDeviceFactory** class in hello Common project shows how tooadd a method toohello list of **SupportedMethods** in hello reported properties sent by hello device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' toospecifiy hello URI of hello firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="65f33-169">이 코드 조각은 hello에 대 한 세부 정보 추가 **InitiateFirmwareUpdate** hello 솔루션 포털 hello에 대 한 세부 정보에 텍스트 toodisplay를 포함 하는 메서드 필수 메서드 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-169">This code snippet adds details of hello **InitiateFirmwareUpdate** method including text toodisplay in hello solution portal and details of hello required method parameters.</span></span>

<span data-ttu-id="65f33-170">hello 시뮬레이터 tooIoT 허브 hello 시뮬레이터 시작 될 때 지원 되는 메서드의 hello 목록을 비롯 한 보고 속성을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-170">hello simulator sends reported properties, including hello list of supported methods, tooIoT Hub when hello simulator starts.</span></span>

<span data-ttu-id="65f33-171">지 원하는 각 방법에 대 한 처리기 toohello 시뮬레이터 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-171">Add a handler toohello simulator code for each method it supports.</span></span> <span data-ttu-id="65f33-172">Hello hello 기존 처리기 나타나면 **CoolerDevice** hello Simulator.WebJob 프로젝트의 클래스.</span><span class="sxs-lookup"><span data-stu-id="65f33-172">You can see hello existing handlers in hello **CoolerDevice** class in hello Simulator.WebJob project.</span></span> <span data-ttu-id="65f33-173">hello 다음 보여 주는 예제에 대 한 hello 처리기 **InitiateFirmwareUpdate** 메서드:</span><span class="sxs-lookup"><span data-stu-id="65f33-173">hello following example shows hello handler for **InitiateFirmwareUpdate** method:</span></span>

```csharp
public async Task<MethodResponse> OnInitiateFirmwareUpdate(MethodRequest methodRequest, object userContext)
{
    if (_deviceManagementTask != null && !_deviceManagementTask.IsCompleted)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "Device is busy"
        }, 409));
    }

    try
    {
        var operation = new FirmwareUpdate(methodRequest);
        _deviceManagementTask = operation.Run(Transport).ContinueWith(async task =>
        {
            // after firmware completed, we reset telemetry
            var telemetry = _telemetryController as ITelemetryWithTemperatureMeanValue;
            if (telemetry != null)
            {
                telemetry.TemperatureMeanValue = 34.5;
            }

            await UpdateReportedTemperatureMeanValue();
        });

        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "FirmwareUpdate accepted",
            Uri = operation.Uri
        }));
    }
    catch (Exception ex)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = ex.Message
        }, 400));
    }
}
```

<span data-ttu-id="65f33-174">메서드 처리기 이름은으로 시작 해야 `On` hello 메서드의 hello 이름이 차례로 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-174">Method handler names must start with `On` followed by hello name of hello method.</span></span> <span data-ttu-id="65f33-175">hello **methodRequest** 매개 변수는 hello 솔루션 백 엔드에서 hello 메서드 호출으로 전달 된 매개 변수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-175">hello **methodRequest** parameter contains any parameters passed with hello method invocation from hello solution back end.</span></span> <span data-ttu-id="65f33-176">hello 반환 값 형식 이어야 합니다 **작업&lt;MethodResponse&gt;**합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-176">hello return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="65f33-177">hello **BuildMethodResponse** 유틸리티 메서드를 사용 하면 hello 반환 값을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-177">hello **BuildMethodResponse** utility method helps you create hello return value.</span></span>

<span data-ttu-id="65f33-178">Hello 메서드 처리기 내 하면 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-178">Inside hello method handler, you could:</span></span>

- <span data-ttu-id="65f33-179">비동기 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="65f33-180">Hello에서 원하는 속성을 검색할 *장치로 이중* IoT 허브에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-180">Retrieve desired properties from hello *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="65f33-181">Hello를 사용 하 여 단일 보고 속성을 업데이트 **SetReportedPropertyAsync** hello에 대 한 메서드 **CoolerDevice** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-181">Update a single reported property using hello **SetReportedPropertyAsync** method in hello **CoolerDevice** class.</span></span>
- <span data-ttu-id="65f33-182">만들어서 여러 보고 속성을 업데이트 한 **TwinCollection** 인스턴스와 호출 hello **Transport.UpdateReportedPropertiesAsync** 메서드.</span><span class="sxs-lookup"><span data-stu-id="65f33-182">Update multiple reported properties by creating a **TwinCollection** instance and calling hello **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="65f33-183">hello 이전 펌웨어 업데이트 수행 하는 예제 단계를 수행 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="65f33-183">hello preceding firmware update example performs hello following steps:</span></span>

- <span data-ttu-id="65f33-184">검사 hello 장치 수 tooaccept hello 펌웨어 업데이트 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-184">Checks hello device is able tooaccept hello firmware update request.</span></span>
- <span data-ttu-id="65f33-185">비동기적으로 hello 펌웨어 업데이트 작업을 시작 하 고 hello 작업이 완료 되 면 hello 원격 분석을 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-185">Asynchronously initiates hello firmware update operation and resets hello telemetry when hello operation is complete.</span></span>
- <span data-ttu-id="65f33-186">즉시 반환 hello "FirmwareUpdate 허용" hello 장치에 의해 메시지 tooindicate hello 요청이 수락 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-186">Immediately returns hello "FirmwareUpdate accepted" message tooindicate hello request was accepted by hello device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="65f33-187">고유한 (물리적) 장치 빌드 및 사용</span><span class="sxs-lookup"><span data-stu-id="65f33-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="65f33-188">hello [Azure IoT Sdk](https://github.com/Azure/azure-iot-sdks) IoT 솔루션으로 다양 한 장치 유형 (언어 및 운영 체제)를 연결 하기 위한 라이브러리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-188">hello [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="65f33-189">대시보드 제한 수정</span><span class="sxs-lookup"><span data-stu-id="65f33-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="65f33-190">대시보드 드롭다운에 표시되는 장치 수</span><span class="sxs-lookup"><span data-stu-id="65f33-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="65f33-191">hello 기본값은 200입니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-191">hello default is 200.</span></span> <span data-ttu-id="65f33-192">[DashboardController.cs][lnk-dashboard-controller]에서 이 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-toodisplay-in-bing-map-control"></a><span data-ttu-id="65f33-193">Bing 지도 컨트롤에서 핀 toodisplay 개수</span><span class="sxs-lookup"><span data-stu-id="65f33-193">Number of pins toodisplay in Bing Map control</span></span>

<span data-ttu-id="65f33-194">hello 기본값은 200입니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-194">hello default is 200.</span></span> <span data-ttu-id="65f33-195">[TelemetryApiController.cs][lnk-telemetry-api-controller-01]에서 이 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="65f33-196">원격 분석 그래프의 시간 간격</span><span class="sxs-lookup"><span data-stu-id="65f33-196">Time period of telemetry graph</span></span>

<span data-ttu-id="65f33-197">hello 기본값은 10 분입니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-197">hello default is 10 minutes.</span></span> <span data-ttu-id="65f33-198">[TelmetryApiController.cs][lnk-telemetry-api-controller-02]에서 이 값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="manually-set-up-application-roles"></a><span data-ttu-id="65f33-199">수동으로 응용 프로그램 역할 설정</span><span class="sxs-lookup"><span data-stu-id="65f33-199">Manually set up application roles</span></span>

<span data-ttu-id="65f33-200">hello 다음 절차에서는 방법을 tooadd **Admin** 및 **ReadOnly** 응용 프로그램 역할 tooa 미리 솔루션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-200">hello following procedure describes how tooadd **Admin** and **ReadOnly** application roles tooa preconfigured solution.</span></span> <span data-ttu-id="65f33-201">Hello azureiotsuite.com 사이트에서 이미 프로 비전 하는 미리 구성 된 솔루션에 hello 포함 **관리자** 및 **ReadOnly** 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-201">Note that preconfigured solutions provisioned from hello azureiotsuite.com site already include hello **Admin** and **ReadOnly** roles.</span></span>

<span data-ttu-id="65f33-202">멤버의 hello **ReadOnly** 역할 hello 대시보드와 hello 장치 목록을 볼 수 있지만 tooadd 장치, 장치 특성 변경, 또는 송신 명령을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-202">Members of hello **ReadOnly** role can see hello dashboard and hello device list, but are not allowed tooadd devices, change device attributes, or send commands.</span></span>  <span data-ttu-id="65f33-203">멤버의 hello **Admin** 역할 hello 솔루션에 대 한 모든 권한을 tooall hello 기능 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-203">Members of hello **Admin** role have full access tooall hello functionality in hello solution.</span></span>

1. <span data-ttu-id="65f33-204">Toohello 이동 [Azure 클래식 포털][lnk-classic-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-204">Go toohello [Azure classic portal][lnk-classic-portal].</span></span>
2. <span data-ttu-id="65f33-205">**Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-205">Select **Active Directory**.</span></span>
3. <span data-ttu-id="65f33-206">솔루션을 프로 비전 할 때 사용한 hello AAD 테 넌 트의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-206">Click hello name of hello AAD tenant you used when you provisioned your solution.</span></span>
4. <span data-ttu-id="65f33-207">**응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-207">Click **Applications**.</span></span>
5. <span data-ttu-id="65f33-208">미리 구성 된 솔루션 이름과 일치 하는 hello 응용 프로그램의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-208">Click hello name of hello application that matches your preconfigured solution name.</span></span> <span data-ttu-id="65f33-209">응용 프로그램 hello 목록에 보이지 않으면 경우 선택 **회사가 보유 한 응용 프로그램** hello에 **표시** 드롭다운을 클릭 하 고 확인 표시를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-209">If you don't see your application in hello list, select **Applications my company owns** in hello **Show** dropdown and click hello check mark.</span></span>
6. <span data-ttu-id="65f33-210">Hello hello 페이지의 아래쪽에 있는 클릭 **매니페스트 관리** 차례로 **매니페스트 다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-210">At hello bottom of hello page, click **Manage Manifest** and then **Download Manifest**.</span></span>
7. <span data-ttu-id="65f33-211">이 절차는.json 파일 tooyour 로컬 컴퓨터를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-211">This procedure downloads a .json file tooyour local machine.</span></span> <span data-ttu-id="65f33-212">이 파일을 편집할 수 있도록 원하는 텍스트 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-212">Open this file for editing in a text editor of your choice.</span></span>
8. <span data-ttu-id="65f33-213">Hello.json 파일의 hello 세 번째 줄에 다음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-213">On hello third line of hello .json file, you can see:</span></span>

   ```json
   "appRoles" : [],
   ```
   <span data-ttu-id="65f33-214">이 줄을 코드 다음 hello로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-214">Replace this line with hello following code:</span></span>

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access toohello application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access toodevice information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. <span data-ttu-id="65f33-215">(Hello 기존 파일을 덮어쓸 수) hello 업데이트.json 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-215">Save hello updated .json file (you can overwrite hello existing file).</span></span>
10. <span data-ttu-id="65f33-216">Hello hello hello 페이지 맨 아래에 Azure 클래식 포털에서에서 선택 **매니페스트 관리** 다음 **매니페스트 업로드** tooupload hello.json 파일 hello 이전 단계에서 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-216">In hello Azure classic portal, at hello bottom of hello page, select **Manage Manifest** then **Upload Manifest** tooupload hello .json file you saved in hello previous step.</span></span>
11. <span data-ttu-id="65f33-217">이제 hello이 추가 되어 **Admin** 및 **ReadOnly** tooyour 응용 프로그램 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-217">You have now added hello **Admin** and **ReadOnly** roles tooyour application.</span></span>
12. <span data-ttu-id="65f33-218">디렉터리에 이러한 역할 tooa 사용자 중 하나는 tooassign 참조 [hello azureiotsuite.com 사이트에 대 한 권한을][lnk-permissions]합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-218">tooassign one of these roles tooa user in your directory, see [Permissions on hello azureiotsuite.com site][lnk-permissions].</span></span>

## <a name="feedback"></a><span data-ttu-id="65f33-219">사용자 의견</span><span class="sxs-lookup"><span data-stu-id="65f33-219">Feedback</span></span>

<span data-ttu-id="65f33-220">이 문서에서 다루는 toosee 원하는 사용자 지정 있습니까?</span><span class="sxs-lookup"><span data-stu-id="65f33-220">Do you have a customization you'd like toosee covered in this document?</span></span> <span data-ttu-id="65f33-221">기능 제안 너무 추가[사용자 음성](https://feedback.azure.com/forums/321918-azure-iot), 또는이 문서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f33-221">Add feature suggestions too[User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="65f33-222">다음 단계</span><span class="sxs-lookup"><span data-stu-id="65f33-222">Next steps</span></span>

<span data-ttu-id="65f33-223">toolearn hello 미리 구성 된 솔루션을 사용자 지정 하기 위한 hello 옵션에 대해 자세히 알아보려면</span><span class="sxs-lookup"><span data-stu-id="65f33-223">toolearn more about hello options for customizing hello preconfigured solutions, see:</span></span>

* <span data-ttu-id="65f33-224">[논리 앱 tooyour Azure IoT Suite 원격 모니터링 미리 구성 된 솔루션에 연결][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="65f33-224">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="65f33-225">[동적 원격 분석을 사용 하 여 원격 미리 구성 된 솔루션을 모니터링 하는 hello로][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="65f33-225">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="65f33-226">[Hello 원격 모니터링 미리 구성 된 솔루션에서에서 장치 정보 메타 데이터][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="65f33-226">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="65f33-227">[Hello OPC UA는 서버에서 데이터를 표시 팩터리 솔루션에 연결 하는 방법을 사용자 지정][lnk-cf-customize]</span><span class="sxs-lookup"><span data-stu-id="65f33-227">[Customize how hello connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

[lnk-logicapp]: iot-suite-logic-apps-tutorial.md
[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[IoT Device SDK]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-permissions]: iot-suite-permissions.md
[lnk-dashboard-controller]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/Controllers/DashboardController.cs#L27
[lnk-telemetry-api-controller-01]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L27
[lnk-telemetry-api-controller-02]: https://github.com/Azure/azure-iot-remote-monitoring/blob/e7003339f73e21d3930f71ceba1e74fb5c0d9ea0/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L25 
[lnk-sample-device-factory]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Common/Factory/SampleDeviceFactory.cs#L40
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-cf-customize]: iot-suite-connected-factory-customize.md
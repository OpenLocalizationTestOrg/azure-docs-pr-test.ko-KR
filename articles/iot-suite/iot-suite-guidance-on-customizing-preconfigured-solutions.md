---
title: "미리 구성된 솔루션 사용자 지정 | Microsoft Docs"
description: "미리 구성된 Azure IoT Suite 솔루션을 사용자 지정하는 방법에 대한 지침을 제공합니다."
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
ms.openlocfilehash: bdf4cd89d5ad0392337dfe761108608d506adf18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="58de0-103">미리 구성된 솔루션 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="58de0-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="58de0-104">Azure IoT Suite와 함께 제공되는 미리 구성된 솔루션은 제품 내에서 함께 협력하는 서비스를 보여주어 종단간 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-104">The preconfigured solutions provided with the Azure IoT Suite demonstrate the services within the suite working together to deliver an end-to-end solution.</span></span> <span data-ttu-id="58de0-105">이 시작 지점에서 특정 시나리오에 대한 솔루션을 확장하고 사용자 지정할 수 있는 다양한 위치가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-105">From this starting point, there are various places in which you can extend and customize the solution for specific scenarios.</span></span> <span data-ttu-id="58de0-106">다음 섹션에서는 이러한 일반적인 사용자 지정 위치를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-106">The following sections describe these common customization points.</span></span>

## <a name="find-the-source-code"></a><span data-ttu-id="58de0-107">소스 코드 찾기</span><span class="sxs-lookup"><span data-stu-id="58de0-107">Find the source code</span></span>

<span data-ttu-id="58de0-108">미리 구성된 솔루션에 대한 소스 코드는 다음 리포지토리의 GitHub에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-108">The source code for the preconfigured solutions is available on GitHub in the following repositories:</span></span>

* <span data-ttu-id="58de0-109">원격 모니터링: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="58de0-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="58de0-110">예측 유지 관리: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="58de0-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="58de0-111">연결된 팩터리: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="58de0-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="58de0-112">미리 구성된 솔루션에 대한 소스 코드는 패턴과 Azure IoT Suite를 사용하여 IoT 솔루션의 종단 간 기능을 구현하는 데 사용하는 작업 방식과 패턴을 보여 주기 위해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-112">The source code for the preconfigured solutions is provided to demonstrate the patterns and practices used to implement the end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="58de0-113">GitHub 리포지토리에서 솔루션을 빌드 및 배포하는 방법에 대한 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-113">You can find more information about how to build and deploy the solutions in the GitHub repositories.</span></span>

## <a name="change-the-preconfigured-rules"></a><span data-ttu-id="58de0-114">미리 구성된 규칙 변경</span><span class="sxs-lookup"><span data-stu-id="58de0-114">Change the preconfigured rules</span></span>

<span data-ttu-id="58de0-115">원격 모니터링 솔루션은 솔루션에서 장치 정보, 원격 분석 및 규칙 논리를 다루는 세 개의 [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-115">The remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs to handle device information, telemetry, and rules logic in the solution.</span></span>

<span data-ttu-id="58de0-116">세 개의 Stream Analytics 작업 및 해당 구문은 [원격 모니터링 미리 구성된 솔루션 연습](iot-suite-remote-monitoring-sample-walkthrough.md)에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-116">The three stream analytics jobs and their syntax are described in depth in the [Remote monitoring preconfigured solution walkthrough](iot-suite-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="58de0-117">논리를 변경하거나 시나리오에 관련된 논리를 추가하도록 이러한 작업을 직접 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-117">You can edit these jobs directly to alter the logic, or add logic specific to your scenario.</span></span> <span data-ttu-id="58de0-118">다음과 같이 스트림 분석 작업을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-118">You can find the Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="58de0-119">[Azure 포털](https://portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-119">Go to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="58de0-120">IoT 솔루션과 이름이 동일한 새 리소스 그룹으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-120">Navigate to the resource group with the same name as your IoT solution.</span></span> 
3. <span data-ttu-id="58de0-121">수정하려는 Azure 스트림 분석 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-121">Select the Azure Stream Analytics job you'd like to modify.</span></span> 
4. <span data-ttu-id="58de0-122">명령 집합에서 **중지**를 선택하여 작업을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-122">Stop the job by selecting **Stop** in the set of commands.</span></span> 
5. <span data-ttu-id="58de0-123">입력, 쿼리 및 출력을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-123">Edit the inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="58de0-124">수정을 간편하게 수행하려면 **">"** 대신 **"<"**를 사용하도록 **규칙** 작업에 대한 쿼리를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-124">A simple modification is to change the query for the **Rules** job to use a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="58de0-125">규칙을 편집할 때 솔루션 포털에는 계속 **">"**가 표시되지만 기본 작업이 변경되어 동작이 반대로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-125">The solution portal still shows **">"** when you edit a rule, but notice how the behavior is flipped due to the change in the underlying job.</span></span>
6. <span data-ttu-id="58de0-126">작업 시작</span><span class="sxs-lookup"><span data-stu-id="58de0-126">Start the job</span></span>

> [!NOTE]
> <span data-ttu-id="58de0-127">원격 모니터링 대시보드는 특정 데이터에 따라 달라지므로 작업 변경은 대시보드 실패를 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-127">The remote monitoring dashboard depends on specific data, so altering the jobs can cause the dashboard to fail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="58de0-128">사용자 고유 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="58de0-128">Add your own rules</span></span>

<span data-ttu-id="58de0-129">미리 구성된 Azure 스트림 분석 작업 변경 외에도 Azure 포털을 사용하여 새 작업을 추가하거나 기존 작업에 새 쿼리를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-129">In addition to changing the preconfigured Azure Stream Analytics jobs, you can use the Azure portal to add new jobs or add new queries to existing jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="58de0-130">장치 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="58de0-130">Customize devices</span></span>

<span data-ttu-id="58de0-131">가장 일반적인 확장 작업 중 하나는 시나리오와 관련된 장치를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-131">One of the most common extension activities is working with devices specific to your scenario.</span></span> <span data-ttu-id="58de0-132">장치를 사용하는 여러 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-132">There are several methods for working with devices.</span></span> <span data-ttu-id="58de0-133">이 방법은 해당 시나리오에 맞게 시뮬레이션된 장치를 변경하거나 [IoT 장치 SDK][IoT Device SDK] 를 사용하여 솔루션에 대한 실제 장치에 연결하는 것이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-133">These methods include altering a simulated device to match your scenario, or using the [IoT Device SDK][IoT Device SDK] to connect your physical device to the solution.</span></span>

<span data-ttu-id="58de0-134">장치를 추가하기 위한 단계별 가이드는 [Iot Suite 연결 장치](iot-suite-connecting-devices.md) 문서 및 [원격 모니터링 C SDK 샘플](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58de0-134">For a step-by-step guide to adding devices, see the [Iot Suite Connecting Devices](iot-suite-connecting-devices.md) article and the [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="58de0-135">이 샘플은 미리 구성된 원격 모니터링 솔루션을 사용하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-135">This sample is designed to work with the remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="58de0-136">고유한 시뮬레이션된 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="58de0-136">Create your own simulated device</span></span>

<span data-ttu-id="58de0-137">.NET 시뮬레이터는 [원격 모니터링 솔루션 소스 코드](https://github.com/Azure/azure-iot-remote-monitoring)에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-137">Included in the [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="58de0-138">이 시뮬레이터는 솔루션의 일부로 프로비전되었으며 다른 메타데이터, 원격 분석을 보내거나 다른 명령 및 메서드에 응답하도록 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-138">This simulator is the one provisioned as part of the solution and you can alter it to send different metadata, telemetry, and respond to different commands and methods.</span></span>

<span data-ttu-id="58de0-139">미리 구성된 솔루션 시뮬레이터의 원격 모니터링에서 미리 구성된 시뮬레이터는 온도 및 습도 원격 분석을 내보내는 냉각 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-139">The preconfigured simulator in the remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="58de0-140">GitHub 리포지토리를 분기한 경우 [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) 프로젝트에서 시뮬레이터를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-140">You can modify the simulator in the [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked the GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="58de0-141">시뮬레이션된 장치에 사용 가능한 위치</span><span class="sxs-lookup"><span data-stu-id="58de0-141">Available locations for simulated devices</span></span>

<span data-ttu-id="58de0-142">위치의 기본 집합은 시애틀/레드먼드, 워싱턴, 미국입니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-142">The default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="58de0-143">[SampleDeviceFactory.cs][lnk-sample-device-factory]에서 이러한 위치를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-to-the-simulator"></a><span data-ttu-id="58de0-144">시뮬레이터에 desired 속성 업데이트 처리기 추가</span><span class="sxs-lookup"><span data-stu-id="58de0-144">Add a desired property update handler to the simulator</span></span>

<span data-ttu-id="58de0-145">솔루션 포털에서 장치의 desired 속성에 대한 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-145">You can set a value for a desired property for a device in the solution portal.</span></span> <span data-ttu-id="58de0-146">장치가 desired 속성 값을 검색하는 경우 속성 변경 요청을 처리하는 것이 장치의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-146">It is the responsibility of the device to handle the property change request when the device retrieves the desired property value.</span></span> <span data-ttu-id="58de0-147">desired 속성을 통해 속성 값 변경에 대한 지원을 추가하려면 시뮬레이터에 처리기를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-147">To add support for a property value change through a desired property, you need to add a handler to the simulator.</span></span>

<span data-ttu-id="58de0-148">시뮬레이터는 솔루션 포털에서 desired 값을 설정하여 업데이트할 수 있는 **SetPointTemp** 및 **TelemetryInterval** 속성에 대한 처리기를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-148">The simulator contains handlers for the **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in the solution portal.</span></span>

<span data-ttu-id="58de0-149">다음 예제는 **CoolerDevice** 클래스에서 **SetPointTemp** desired 속성에 대한 처리기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-149">The following example shows the handler for the **SetPointTemp** desired property in the **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="58de0-150">이 메서드는 원격 분석 지점 온도를 업데이트한 다음 reported 속성을 설정하여 변경 내용을 IoT Hub에 다시 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-150">This method updates the telemetry point temperature and then reports the change back to IoT Hub by setting a reported property.</span></span>

<span data-ttu-id="58de0-151">앞의 예제에서 패턴을 따라 사용자 고유의 속성에 대한 사용자 고유의 처리기를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-151">You can add your own handlers for your own properties by following the pattern in the preceding example.</span></span>

<span data-ttu-id="58de0-152">또한 **CoolerDevice** 생성자에서 다음 예제와 같이 desired 속성을 처리기에 바인딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-152">You must also bind the desired property to the handler as shown in the following example from the **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="58de0-153">**SetPointTempPropertyName**은 "Config.SetPointTemp"로 정의되는 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-to-the-simulator"></a><span data-ttu-id="58de0-154">시뮬레이터에 새 메서드에 대한 지원 추가</span><span class="sxs-lookup"><span data-stu-id="58de0-154">Add support for a new method to the simulator</span></span>

<span data-ttu-id="58de0-155">시뮬레이터를 사용자 지정하여 새 [메서드(직접 메서드)][lnk-direct-methods]에 대한 지원을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-155">You can customize the simulator to add support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="58de0-156">필요한 두 가지 주요 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-156">There are two key steps required:</span></span>

- <span data-ttu-id="58de0-157">시뮬레이터는 메서드의 세부 정보를 사용하여 미리 구성된 솔루션에서 IoT Hub에 알려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-157">The simulator must notify the IoT hub in the preconfigured solution with details of the method.</span></span>
- <span data-ttu-id="58de0-158">시뮬레이터는 솔루션 탐색기에서 또는 작업을 통해 **장치 세부 정보** 패널에서 호출할 때 메서드 호출을 처리하는 코드를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-158">The simulator must include code to handle the method call when you invoke it from the **Device details** panel in the solution explorer or through a job.</span></span>

<span data-ttu-id="58de0-159">미리 구성된 원격 모니터링 솔루션은 *reported 속성*을 사용하여 IoT Hub에 지원되는 메서드의 세부 정보를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-159">The remote monitoring preconfigured solution uses *reported properties* to send details of supported methods to IoT hub.</span></span> <span data-ttu-id="58de0-160">솔루션 백 엔드는 메서드 호출 기록과 함께 각 장치에서 지원하는 모든 메서드 목록을 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-160">The solution back end maintains a list of all the methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="58de0-161">장치에 대한 이 정보를 볼 수 있으며 솔루션 포털에서 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-161">You can view this information about devices and invoke methods in the solution portal.</span></span>

<span data-ttu-id="58de0-162">장치에서 메서드를 지원하는 것을 IoT Hub에 알리기 위해 장치는 reported 속성의 **SupportedMethods** 노드에 메서드의 세부 정보를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-162">To notify the IoT hub that a device supports a method, the device must add details of the method to the **SupportedMethods** node in the reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="58de0-163">메서드 서명은 다음 형식을 가집니다. `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`</span><span class="sxs-lookup"><span data-stu-id="58de0-163">The method signature has the following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="58de0-164">예를 들어 **FwPackageURI**라는 문자열 매개 변수를 예상하는 **InitiateFirmwareUpdate** 메서드를 지정하려면 다음 메서드 서명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-164">For example, to specify the **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use the following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="58de0-165">지원되는 매개 변수 형식의 목록은 인프라 프로젝트에서 **CommandTypes** 클래스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58de0-165">For a list of supported parameter types, see the **CommandTypes** class in the Infrastructure project.</span></span>

<span data-ttu-id="58de0-166">메서드를 삭제하려면 reported 속성에서 메서드 서명을 `null`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-166">To delete a method, set the method signature to `null` in the reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="58de0-167">솔루션 백 엔드는 장치에서 *장치 정보* 메시지를 받을 때 지원되는 메서드에 대한 정보만을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-167">The solution back end only updates information about supported methods when it receives a *device information* message from the device.</span></span>

<span data-ttu-id="58de0-168">Common 프로젝트에서 **SampleDeviceFactory** 클래스의 다음 코드 예제는 장치에서 전송된 reported 속성에서 **SupportedMethods** 목록에 메서드를 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-168">The following code sample from the **SampleDeviceFactory** class in the Common project shows how to add a method to the list of **SupportedMethods** in the reported properties sent by the device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' to specifiy the URI of the firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="58de0-169">이 코드 조각은 솔루션 포털에 표시할 텍스트를 포함하는 **InitiateFirmwareUpdate** 메서드의 세부 정보 및 필수 메서드 매개 변수의 세부 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-169">This code snippet adds details of the **InitiateFirmwareUpdate** method including text to display in the solution portal and details of the required method parameters.</span></span>

<span data-ttu-id="58de0-170">시뮬레이터는 시뮬레이터가 시작될 때 지원되는 메서드의 목록을 포함한 reported 속성을 IoT Hub에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-170">The simulator sends reported properties, including the list of supported methods, to IoT Hub when the simulator starts.</span></span>

<span data-ttu-id="58de0-171">지원하는 각 메서드에 대한 시뮬레이터 코드에 처리기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-171">Add a handler to the simulator code for each method it supports.</span></span> <span data-ttu-id="58de0-172">Simulator.WebJob 프로젝트의 **CoolerDevice** 클래스에서 기존 처리기를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-172">You can see the existing handlers in the **CoolerDevice** class in the Simulator.WebJob project.</span></span> <span data-ttu-id="58de0-173">다음 예제는 **InitiateFirmwareUpdate** 메서드에 대한 처리기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-173">The following example shows the handler for **InitiateFirmwareUpdate** method:</span></span>

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

<span data-ttu-id="58de0-174">메서드 처리기 이름은 뒤에 메서드 이름이 오는 `On`으로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-174">Method handler names must start with `On` followed by the name of the method.</span></span> <span data-ttu-id="58de0-175">**methodRequest** 매개 변수는 솔루션 백 엔드에서 메서드 호출을 통해 전달된 모든 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-175">The **methodRequest** parameter contains any parameters passed with the method invocation from the solution back end.</span></span> <span data-ttu-id="58de0-176">반환 값은 **Task&lt;MethodResponse&gt;**의 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-176">The return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="58de0-177">**BuildMethodResponse** 유틸리티 메서드를 사용하면 반환 값을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-177">The **BuildMethodResponse** utility method helps you create the return value.</span></span>

<span data-ttu-id="58de0-178">메서드 처리기 내에서 다음 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-178">Inside the method handler, you could:</span></span>

- <span data-ttu-id="58de0-179">비동기 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="58de0-180">IoT Hub의 *장치 쌍*에서 desired 속성을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-180">Retrieve desired properties from the *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="58de0-181">**CoolerDevice** 클래스의 **SetReportedPropertyAsync** 메서드를 사용하여 단일 reported 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-181">Update a single reported property using the **SetReportedPropertyAsync** method in the **CoolerDevice** class.</span></span>
- <span data-ttu-id="58de0-182">**TwinCollection** 인스턴스를 만들고 **Transport.UpdateReportedPropertiesAsync** 메서드를 호출하여 여러 reported 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-182">Update multiple reported properties by creating a **TwinCollection** instance and calling the **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="58de0-183">앞의 펌웨어 업데이트 예제는 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-183">The preceding firmware update example performs the following steps:</span></span>

- <span data-ttu-id="58de0-184">장치가 펌웨어 업데이트 요청을 수락할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-184">Checks the device is able to accept the firmware update request.</span></span>
- <span data-ttu-id="58de0-185">비동기적으로 펌웨어 업데이트 작업을 시작하고 작업이 완료되면 원격 분석을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-185">Asynchronously initiates the firmware update operation and resets the telemetry when the operation is complete.</span></span>
- <span data-ttu-id="58de0-186">"FirmwareUpdate 수락" 메시지를 즉시 반환하여 장치에서 요청이 수락되었다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-186">Immediately returns the "FirmwareUpdate accepted" message to indicate the request was accepted by the device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="58de0-187">고유한 (물리적) 장치 빌드 및 사용</span><span class="sxs-lookup"><span data-stu-id="58de0-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="58de0-188">[Azure IoT SDK](https://github.com/Azure/azure-iot-sdks) 는 IoT 솔루션으로 다양한 장치 유형(언어 및 운영 체제)를 연결하기 위한 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-188">The [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="58de0-189">대시보드 제한 수정</span><span class="sxs-lookup"><span data-stu-id="58de0-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="58de0-190">대시보드 드롭다운에 표시되는 장치 수</span><span class="sxs-lookup"><span data-stu-id="58de0-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="58de0-191">기본값은 200입니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-191">The default is 200.</span></span> <span data-ttu-id="58de0-192">[DashboardController.cs][lnk-dashboard-controller]에서 이 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-to-display-in-bing-map-control"></a><span data-ttu-id="58de0-193">Bing 지도 컨트롤에 표시할 핀 수</span><span class="sxs-lookup"><span data-stu-id="58de0-193">Number of pins to display in Bing Map control</span></span>

<span data-ttu-id="58de0-194">기본값은 200입니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-194">The default is 200.</span></span> <span data-ttu-id="58de0-195">[TelemetryApiController.cs][lnk-telemetry-api-controller-01]에서 이 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="58de0-196">원격 분석 그래프의 시간 간격</span><span class="sxs-lookup"><span data-stu-id="58de0-196">Time period of telemetry graph</span></span>

<span data-ttu-id="58de0-197">기본값은 10분입니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-197">The default is 10 minutes.</span></span> <span data-ttu-id="58de0-198">[TelmetryApiController.cs][lnk-telemetry-api-controller-02]에서 이 값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="manually-set-up-application-roles"></a><span data-ttu-id="58de0-199">수동으로 응용 프로그램 역할 설정</span><span class="sxs-lookup"><span data-stu-id="58de0-199">Manually set up application roles</span></span>

<span data-ttu-id="58de0-200">다음 절차에서는 미리 구성된 솔루션에 **관리** 및 **읽기 전용** 응용 프로그램 역할을 추가하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-200">The following procedure describes how to add **Admin** and **ReadOnly** application roles to a preconfigured solution.</span></span> <span data-ttu-id="58de0-201">azureiotsuite.com 사이트에서 프로비전되는 미리 구성된 솔루션에는 **관리** 및 **읽기 전용** 역할이 이미 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-201">Note that preconfigured solutions provisioned from the azureiotsuite.com site already include the **Admin** and **ReadOnly** roles.</span></span>

<span data-ttu-id="58de0-202">**ReadOnly** 역할의 구성원은 대시보드 및 장치 목록을 볼 수는 있지만 장치를 추가하거나 장치 특성을 변경하거나 명령을 전송할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-202">Members of the **ReadOnly** role can see the dashboard and the device list, but are not allowed to add devices, change device attributes, or send commands.</span></span>  <span data-ttu-id="58de0-203">**Admin** 역할의 구성원에게는 솔루션의 모든 기능에 대한 모든 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-203">Members of the **Admin** role have full access to all the functionality in the solution.</span></span>

1. <span data-ttu-id="58de0-204">[Azure 클래식 포털][lnk-classic-portal]로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-204">Go to the [Azure classic portal][lnk-classic-portal].</span></span>
2. <span data-ttu-id="58de0-205">**Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-205">Select **Active Directory**.</span></span>
3. <span data-ttu-id="58de0-206">솔루션을 프로비전할 때 사용한 AAD 테넌트의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-206">Click the name of the AAD tenant you used when you provisioned your solution.</span></span>
4. <span data-ttu-id="58de0-207">**응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-207">Click **Applications**.</span></span>
5. <span data-ttu-id="58de0-208">미리 구성된 솔루션 이름과 일치하는 응용 프로그램의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-208">Click the name of the application that matches your preconfigured solution name.</span></span> <span data-ttu-id="58de0-209">목록에 응용 프로그램이 표시되지 않으면 **표시** 드롭다운에서 **회사가 보유한 응용 프로그램**을 선택하고 확인 표시를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-209">If you don't see your application in the list, select **Applications my company owns** in the **Show** dropdown and click the check mark.</span></span>
6. <span data-ttu-id="58de0-210">페이지의 아래쪽에서 **매니페스트 관리**와 **매니페스트 다운로드**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-210">At the bottom of the page, click **Manage Manifest** and then **Download Manifest**.</span></span>
7. <span data-ttu-id="58de0-211">이 절차는 .json 파일을 로컬 컴퓨터에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-211">This procedure downloads a .json file to your local machine.</span></span> <span data-ttu-id="58de0-212">이 파일을 편집할 수 있도록 원하는 텍스트 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-212">Open this file for editing in a text editor of your choice.</span></span>
8. <span data-ttu-id="58de0-213">.json 파일의 세 번째 줄에는 다음 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-213">On the third line of the .json file, you can see:</span></span>

   ```json
   "appRoles" : [],
   ```
   <span data-ttu-id="58de0-214">이 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-214">Replace this line with the following code:</span></span>

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access to the application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access to device information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. <span data-ttu-id="58de0-215">업데이트한 .json 파일을 저장합니다. 기존 파일을 덮어쓰면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-215">Save the updated .json file (you can overwrite the existing file).</span></span>
10. <span data-ttu-id="58de0-216">Azure 클래식 포털 페이지의 아래쪽에서 **매니페스트 관리**와 **매니페스트 업로드**를 차례로 클릭하여 이전 단계에서 저장한 .json 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-216">In the Azure classic portal, at the bottom of the page, select **Manage Manifest** then **Upload Manifest** to upload the .json file you saved in the previous step.</span></span>
11. <span data-ttu-id="58de0-217">이제 **관리** 및 **읽기 전용** 역할이 응용 프로그램에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-217">You have now added the **Admin** and **ReadOnly** roles to your application.</span></span>
12. <span data-ttu-id="58de0-218">이러한 역할 중 하나를 디렉터리의 사용자에게 할당하려면 [azureiotsuite.com 사이트의 권한][lnk-permissions]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58de0-218">To assign one of these roles to a user in your directory, see [Permissions on the azureiotsuite.com site][lnk-permissions].</span></span>

## <a name="feedback"></a><span data-ttu-id="58de0-219">사용자 의견</span><span class="sxs-lookup"><span data-stu-id="58de0-219">Feedback</span></span>

<span data-ttu-id="58de0-220">이 문서에서 포함했으면 하는 사용자 지정이 있나요?</span><span class="sxs-lookup"><span data-stu-id="58de0-220">Do you have a customization you'd like to see covered in this document?</span></span> <span data-ttu-id="58de0-221">[사용자 의견](https://feedback.azure.com/forums/321918-azure-iot)에 기능 제안을 추가하거나 이 문서에 대한 의견을 입력해 주시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="58de0-221">Add feature suggestions to [User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="58de0-222">다음 단계</span><span class="sxs-lookup"><span data-stu-id="58de0-222">Next steps</span></span>

<span data-ttu-id="58de0-223">미리 구성된 솔루션을 사용자 지정하기 위한 옵션에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58de0-223">To learn more about the options for customizing the preconfigured solutions, see:</span></span>

* <span data-ttu-id="58de0-224">[미리 구성된 Azure IoT Suite 원격 모니터링 솔루션에 논리 앱 연결][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="58de0-224">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="58de0-225">[원격 모니터링 사전 구성 솔루션으로 동적 원격 분석 사용][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="58de0-225">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="58de0-226">[미리 구성된 원격 모니터링 솔루션의 장치 정보 메타데이터][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="58de0-226">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="58de0-227">[연결된 공장 솔루션이 OPC UA 서버의 데이터를 표시하는 방식 사용자 지정][lnk-cf-customize]</span><span class="sxs-lookup"><span data-stu-id="58de0-227">[Customize how the connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

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
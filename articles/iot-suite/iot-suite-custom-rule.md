---
title: "Azure IoT Suite에 사용자 지정 규칙 만들기 | Microsoft Docs"
description: "미리 구성된 IoT Suite 솔루션에서 사용자 지정 규칙을 만드는 방법"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: d58c27234ea05a82aaa3e8d72f70c1449980df09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-custom-rule-in-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="e80ac-103">미리 구성된 원격 모니터링 솔루션에서 사용자 지정 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="e80ac-103">Create a custom rule in the remote monitoring preconfigured solution</span></span>

## <a name="introduction"></a><span data-ttu-id="e80ac-104">소개</span><span class="sxs-lookup"><span data-stu-id="e80ac-104">Introduction</span></span>

<span data-ttu-id="e80ac-105">미리 구성된 솔루션에서 [장치에 대한 원격 분석 값이 특정 임계값에 도달할 때 트리거되는 규칙][lnk-builtin-rule]을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-105">In the preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span></span> <span data-ttu-id="e80ac-106">[원격 모니터링 사전 구성 솔루션으로 동적 원격 분석 사용][lnk-dynamic-telemetry]에서는 *ExternalTemperature*와 같은 사용자 지정 원격 분석 값을 솔루션에 추가하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-106">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* to your solution.</span></span> <span data-ttu-id="e80ac-107">이 문서에서는 솔루션에 동적 원격 분석 형식에 대한 사용자 지정 규칙을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-107">This article shows you how to create custom rule for dynamic telemetry types in your solution.</span></span>

<span data-ttu-id="e80ac-108">이 자습서에서는 간단한 Node.js 시뮬레이트 장치를 사용하여 미리 구성된 솔루션 백 엔드로 보낼 동적 원격 분석을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-108">This tutorial uses a simple Node.js simulated device to generate dynamic telemetry to send to the preconfigured solution back end.</span></span> <span data-ttu-id="e80ac-109">그런 후 **RemoteMonitoring** Visual Studio 솔루션에서 사용자 지정 규칙을 추가하고 사용자 지정된 이 백 엔드를 Azure 구독에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-109">You then add custom rules in the **RemoteMonitoring** Visual Studio solution and deploy this customized back end to your Azure subscription.</span></span>

<span data-ttu-id="e80ac-110">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="e80ac-111">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="e80ac-111">An active Azure subscription.</span></span> <span data-ttu-id="e80ac-112">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e80ac-113">자세한 내용은 [Azure 무료 평가판][lnk_free_trial]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e80ac-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="e80ac-114">시뮬레이트된 장치를 만들기 위한 [Node.js][lnk-node] 버전 0.12.x 이상</span><span class="sxs-lookup"><span data-stu-id="e80ac-114">[Node.js][lnk-node] version 0.12.x or later to create a simulated device.</span></span>
* <span data-ttu-id="e80ac-115">새 규칙으로 미리 구성된 솔루션 백 엔드를 수정하기 위한 Visual Studio 2015 또는 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="e80ac-115">Visual Studio 2015 or Visual Studio 2017 to modify the preconfigured solution back end with your new rules.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

<span data-ttu-id="e80ac-116">배포를 위해 선택한 솔루션 이름을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-116">Make a note of the solution name you chose for your deployment.</span></span> <span data-ttu-id="e80ac-117">이 솔루션은 이 자습서의 뒷부분에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-117">You need this solution name later in this tutorial.</span></span>

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

<span data-ttu-id="e80ac-118">**ExternalTemperature** 원격 분석을 미리 구성된 솔루션으로 전송하는지 확인한 다음 Node.js 콘솔 앱을 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-118">You can stop the Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry to the preconfigured solution.</span></span> <span data-ttu-id="e80ac-119">솔루션에 사용자 지정 규칙을 추가한 후에 이 Node.js 콘솔 앱을 다시 실행하게 되므로 콘솔 창을 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-119">Keep the console window open because you run this Node.js console app again after you add the custom rule to the solution.</span></span>

## <a name="rule-storage-locations"></a><span data-ttu-id="e80ac-120">규칙 저장소 위치</span><span class="sxs-lookup"><span data-stu-id="e80ac-120">Rule storage locations</span></span>

<span data-ttu-id="e80ac-121">규칙에 대한 정보는 다음 두 위치에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-121">Information about rules is persisted in two locations:</span></span>

* <span data-ttu-id="e80ac-122">**DeviceRulesNormalizedTable** 테이블 - 이 테이블은 솔루션 포털에서 정의된 규칙에 대한 정규화된 참조를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference to the rules defined by the solution portal.</span></span> <span data-ttu-id="e80ac-123">솔루션 포털에 장치 규칙이 표시되면 이 테이블에서 규칙 정의를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-123">When the solution portal displays device rules, it queries this table for the rule definitions.</span></span>
* <span data-ttu-id="e80ac-124">**DeviceRules** blob - 이 blob은 등록된 모든 장치에 대해 정의된 모든 규칙을 저장하며 Azure Stream Analytics 작업에 대한 참조 입력으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-124">**DeviceRules** blob – This blob stores all the rules defined for all registered devices and is defined as a reference input to the Azure Stream Analytics jobs.</span></span>
 
<span data-ttu-id="e80ac-125">기존 규칙을 업데이트하거나 솔루션 포털에서 새 규칙을 정의하는 경우 변경 내용을 반영하도록 테이블 및 blob이 모두 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-125">When you update an existing rule or define a new rule in the solution portal, both the table and blob are updated to reflect the changes.</span></span> <span data-ttu-id="e80ac-126">포털에 표시된 규칙 정의는 테이블 저장소에서 가져오며, Stream Analytics 작업에서 참조되는 규칙 정의는 blob에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-126">The rule definition displayed in the portal comes from the table store, and the rule definition referenced by the Stream Analytics jobs comes from the blob.</span></span> 

## <a name="update-the-remotemonitoring-visual-studio-solution"></a><span data-ttu-id="e80ac-127">RemoteMonitoring Visual Studio 솔루션 업데이트</span><span class="sxs-lookup"><span data-stu-id="e80ac-127">Update the RemoteMonitoring Visual Studio solution</span></span>

<span data-ttu-id="e80ac-128">다음 단계에서는 시뮬레이트된 장치에서 전송된 **ExternalTemperature** 원격 분석을 사용하는 새 규칙을 포함하도록 RemoteMonitoring Visual Studio 솔루션을 수정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-128">The following steps show you how to modify the RemoteMonitoring Visual Studio solution to include a new rule that uses the **ExternalTemperature** telemetry sent from the simulated device:</span></span>

1. <span data-ttu-id="e80ac-129">**azure-iot-remote-monitoring** 리포지토리를 로컬 컴퓨터의 적절한 위치로 복제하지 않은 경우 다음 Git 명령을 사용하여 지금 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-129">If you have not already done so, clone the **azure-iot-remote-monitoring** repository to a suitable location on your local machine using the following Git command:</span></span>

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. <span data-ttu-id="e80ac-130">Visual Studio에서 **azure-iot-remote-monitoring** 리포지토리의 로컬 복사본에서 RemoteMonitoring.sln 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-130">In Visual Studio, open the RemoteMonitoring.sln file from your local copy of the **azure-iot-remote-monitoring** repository.</span></span>

3. <span data-ttu-id="e80ac-131">Infrastructure\Models\DeviceRuleBlobEntity.cs 파일을 열고 다음과 같이 **ExternalTemperature** 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-131">Open the file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span></span>

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. <span data-ttu-id="e80ac-132">같은 파일에 다음과 같이 **ExternalTemperatureRuleOutput** 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-132">In the same file, add an **ExternalTemperatureRuleOutput** property as follows:</span></span>

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. <span data-ttu-id="e80ac-133">Infrastructure\Models\DeviceRuleDataFields.cs 파일을 열고, 기존 **Humidity** 속성 뒤에 다음 **ExternalTemperature** 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-133">Open the file Infrastructure\Models\DeviceRuleDataFields.cs and add the following **ExternalTemperature** property after the existing **Humidity** property:</span></span>

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. <span data-ttu-id="e80ac-134">동일한 파일에서 다음과 같이 **ExternalTemperature**를 포함하도록 **_availableDataFields** 메서드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-134">In the same file, update the **_availableDataFields** method to include **ExternalTemperature** as follows:</span></span>

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. <span data-ttu-id="e80ac-135">Infrastructure\Repository\DeviceRulesRepository.cs 파일을 열고 다음과 같이 **BuildBlobEntityListFromTableRows** 메서드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-135">Open the file Infrastructure\Repository\DeviceRulesRepository.cs and modify the **BuildBlobEntityListFromTableRows** method as follows:</span></span>

    ```csharp
    else if (rule.DataField == DeviceRuleDataFields.Humidity)
    {
        entity.Humidity = rule.Threshold;
        entity.HumidityRuleOutput = rule.RuleOutput;
    }
    else if (rule.DataField == DeviceRuleDataFields.ExternalTemperature)
    {
      entity.ExternalTemperature = rule.Threshold;
      entity.ExternalTemperatureRuleOutput = rule.RuleOutput;
    }
    ```

## <a name="rebuild-and-redeploy-the-solution"></a><span data-ttu-id="e80ac-136">솔루션을 다시 빌드하고 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-136">Rebuild and redeploy the solution.</span></span>

<span data-ttu-id="e80ac-137">이제 업데이트된 솔루션을 Azure 구독에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-137">You can now deploy the updated solution to your Azure subscription.</span></span>

1. <span data-ttu-id="e80ac-138">관리자 권한 명령 프롬프트를 열고 azure-iot-remote-monitoring 리포지토리의 로컬 복사본 루트로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-138">Open an elevated command prompt and navigate to the root of your local copy of the azure-iot-remote-monitoring repository.</span></span>

2. <span data-ttu-id="e80ac-139">업데이트된 솔루션을 배포하려면 **{deployment name}**을 이전에 적어둔 미리 구성된 솔루션 배포의 이름으로 바꾸어 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-139">To deploy your updated solution, run the following command substituting **{deployment name}** with the name of your preconfigured solution deployment that you noted previously:</span></span>

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-the-stream-analytics-job"></a><span data-ttu-id="e80ac-140">Stream Analytics 작업 업데이트</span><span class="sxs-lookup"><span data-stu-id="e80ac-140">Update the Stream Analytics job</span></span>

<span data-ttu-id="e80ac-141">배포가 완료되면 새 규칙 정의를 사용하도록 Stream Analytics 작업을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-141">When the deployment is complete, you can update the Stream Analytics job to use the new rule definitions.</span></span>

1. <span data-ttu-id="e80ac-142">Azure Portal에서 미리 구성된 솔루션 리소스를 포함하는 리소스 그룹으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-142">In the Azure portal, navigate to the resource group that contains your preconfigured solution resources.</span></span> <span data-ttu-id="e80ac-143">이 리소스 그룹은 배포하는 동안 솔루션에 대해 지정한 동일한 이름을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-143">This resource group has the same name you specified for the solution during the deployment.</span></span>

2. <span data-ttu-id="e80ac-144">{배포 이름}-규칙 Stream Analytics 작업으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-144">Navigate to the {deployment name}-Rules Stream Analytics job.</span></span> 

3. <span data-ttu-id="e80ac-145">**중지**를 클릭하여 Stream Analytics 작업 실행을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-145">Click **Stop** to stop the Stream Analytics job from running.</span></span> <span data-ttu-id="e80ac-146">(쿼리를 편집하려면 스트리밍 작업이 중지될 때까지 기다려야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="e80ac-146">(You must wait for the streaming job to stop before you can edit the query).</span></span>

4. <span data-ttu-id="e80ac-147">**쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-147">Click **Query**.</span></span> <span data-ttu-id="e80ac-148">**ExternalTemperature**에 대한 **SELECT** 문을 포함하도록 쿼리를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-148">Edit the query to include the **SELECT** statement for **ExternalTemperature**.</span></span> <span data-ttu-id="e80ac-149">다음 샘플에서는 새 **SELECT** 문을 사용하는 완전한 쿼리를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-149">The following sample shows the complete query with the new **SELECT** statement:</span></span>

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
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'ExternalTemperature' as ReadingType,
         Stream.ExternalTemperature as Reading,
         Ref.ExternalTemperature as Threshold,
         Ref.ExternalTemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.ExternalTemperature IS NOT null AND Stream.ExternalTemperature > Ref.ExternalTemperature
    )
     
    SELECT *
    INTO DeviceRulesMonitoring
    FROM AlarmsData
     
    SELECT *
    INTO DeviceRulesHub
    FROM AlarmsData
    ```

5. <span data-ttu-id="e80ac-150">**저장**을 클릭하여 업데이트된 규칙 쿼리를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-150">Click **Save** to change the updated rule query.</span></span>

6. <span data-ttu-id="e80ac-151">**시작**을 클릭하여 Stream Analytics 작업 실행을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-151">Click **Start** to start the Stream Analytics job running again.</span></span>

## <a name="add-your-new-rule-in-the-dashboard"></a><span data-ttu-id="e80ac-152">대시보드에서 새 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="e80ac-152">Add your new rule in the dashboard</span></span>

<span data-ttu-id="e80ac-153">이제 솔루션 대시보드의 장치에 **ExternalTemperature** 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-153">You can now add the **ExternalTemperature** rule to a device in the solution dashboard.</span></span>

1. <span data-ttu-id="e80ac-154">솔루션 포털로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-154">Navigate to the solution portal.</span></span>

2. <span data-ttu-id="e80ac-155">**장치** 패널로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-155">Navigate to the **Devices** panel.</span></span>

3. <span data-ttu-id="e80ac-156">**ExternalTemperature** 원격 분석을 전송하는 사용자 지정 장치를 찾은 후 **장치 세부 정보** 패널에서 **규칙 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-156">Locate the custom device you created that sends **ExternalTemperature** telemetry and on the **Device Details** panel, click **Add Rule**.</span></span>

4. <span data-ttu-id="e80ac-157">**데이터 필드**에서 **ExternalTemperature**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-157">Select **ExternalTemperature** in **Data Field**.</span></span>

5. <span data-ttu-id="e80ac-158">**임계값**을 56으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-158">Set **Threshold** to 56.</span></span> <span data-ttu-id="e80ac-159">그런 후 **규칙 저장 및 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-159">Then click **Save and view rules**.</span></span>

6. <span data-ttu-id="e80ac-160">대시보드로 돌아가 경보 기록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-160">Return to the dashboard to view the alarm history.</span></span>

7. <span data-ttu-id="e80ac-161">열어 둔 콘솔 창에서 Node.js 콘솔 앱을 시작하여 **ExternalTemperature** 원격 분석 데이터 전송을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-161">In the console window you left open, start the Node.js console app to begin sending **ExternalTemperature** telemetry data.</span></span>

8. <span data-ttu-id="e80ac-162">**경보 기록** 테이블에는 새 규칙이 트리거될 때 새 경보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-162">Notice that the **Alarm History** table shows new alarms when the new rule is triggered.</span></span>
 
## <a name="additional-information"></a><span data-ttu-id="e80ac-163">추가 정보</span><span class="sxs-lookup"><span data-stu-id="e80ac-163">Additional information</span></span>

<span data-ttu-id="e80ac-164">연산자  **>** 을 변경하는 것은 좀 더 복잡하여 이 자습서에서 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-164">Changing the operator **>** is more complex and goes beyond the steps outlined in this tutorial.</span></span> <span data-ttu-id="e80ac-165">원하는 연산자를 사용하도록 Stream Analytics 작업을 변경할 수는 있으나 솔루션 포털에서 해당 연산자를 적용하는 것이 더 복잡한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-165">While you can change the Stream Analytics job to use whatever operator you like, reflecting that operator in the solution portal is a more complex task.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e80ac-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e80ac-166">Next steps</span></span>
<span data-ttu-id="e80ac-167">사용자 지정 규칙을 만드는 방법을 살펴보았으므로 이제 미리 구성된 솔루션에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e80ac-167">Now that you've seen how to create custom rules, you can learn more about the preconfigured solutions:</span></span>

- <span data-ttu-id="e80ac-168">[미리 구성된 Azure IoT Suite 원격 모니터링 솔루션에 논리 앱 연결][lnk-logic-app]</span><span class="sxs-lookup"><span data-stu-id="e80ac-168">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span></span>
- <span data-ttu-id="e80ac-169">[미리 구성된 원격 모니터링 솔루션의 장치 정보 메타데이터][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="e80ac-169">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md
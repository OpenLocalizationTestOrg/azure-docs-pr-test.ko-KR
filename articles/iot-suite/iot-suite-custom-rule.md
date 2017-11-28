---
title: "Azure IoT Suite에서 사용자 지정 규칙 aaaCreate | Microsoft Docs"
description: "어떻게 toocreate IoT Suite에서 사용자 지정 규칙 솔루션 미리 구성 됩니다."
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
ms.openlocfilehash: 6c5bb2ca54f3f17b99ad482e727c8e9fa28d7fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="c1bd6-103">미리 구성 된 솔루션 모니터링 원격 hello에 사용자 지정 규칙을 만들려면</span><span class="sxs-lookup"><span data-stu-id="c1bd6-103">Create a custom rule in hello remote monitoring preconfigured solution</span></span>

## <a name="introduction"></a><span data-ttu-id="c1bd6-104">소개</span><span class="sxs-lookup"><span data-stu-id="c1bd6-104">Introduction</span></span>

<span data-ttu-id="c1bd6-105">미리 구성 하는 hello 솔루션에서 구성할 수 있습니다 [장치 특정 임계값에 도달할 때는 원격 분석을 트리거하는 규칙의 값][lnk-builtin-rule]합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-105">In hello preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span></span> <span data-ttu-id="c1bd6-106">[동적 원격 분석을 사용 하 여 원격 미리 구성 된 솔루션을 모니터링 하는 hello로] [ lnk-dynamic-telemetry] 와 같은 사용자 지정 원격 분석 값을 추가 하는 방법을 설명 *ExternalTemperature* tooyour 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-106">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* tooyour solution.</span></span> <span data-ttu-id="c1bd6-107">이 문서에서는 솔루션에서 동적 원격 분석을 위한 사용자 지정 규칙 toocreate 형식 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-107">This article shows you how toocreate custom rule for dynamic telemetry types in your solution.</span></span>

<span data-ttu-id="c1bd6-108">이 자습서에서는 간단한 Node.js 시뮬레이션 된 장치 toogenerate 동적 원격 분석 toosend toohello 미리 구성 된 솔루션 백 엔드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-108">This tutorial uses a simple Node.js simulated device toogenerate dynamic telemetry toosend toohello preconfigured solution back end.</span></span> <span data-ttu-id="c1bd6-109">Hello에 다음 사용자 지정 규칙을 추가 **RemoteMonitoring** Visual Studio 솔루션 및 Azure 구독에이 사용자 지정 된 백 엔드 tooyour를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-109">You then add custom rules in hello **RemoteMonitoring** Visual Studio solution and deploy this customized back end tooyour Azure subscription.</span></span>

<span data-ttu-id="c1bd6-110">toocomplete 해야이 자습서에서는:</span><span class="sxs-lookup"><span data-stu-id="c1bd6-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="c1bd6-111">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-111">An active Azure subscription.</span></span> <span data-ttu-id="c1bd6-112">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c1bd6-113">자세한 내용은 [Azure 무료 평가판][lnk_free_trial]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="c1bd6-114">[Node.js] [ lnk-node] 버전 0.12.x 또는 이후 toocreate 시뮬레이션된 된 장치.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-114">[Node.js][lnk-node] version 0.12.x or later toocreate a simulated device.</span></span>
* <span data-ttu-id="c1bd6-115">Visual Studio 2015 또는 Visual Studio 2017 toomodify hello 미리 구성 된 솔루션 다시 새 규칙 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-115">Visual Studio 2015 or Visual Studio 2017 toomodify hello preconfigured solution back end with your new rules.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

<span data-ttu-id="c1bd6-116">배포에 대해 선택한 hello 솔루션 이름을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-116">Make a note of hello solution name you chose for your deployment.</span></span> <span data-ttu-id="c1bd6-117">이 솔루션은 이 자습서의 뒷부분에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-117">You need this solution name later in this tutorial.</span></span>

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

<span data-ttu-id="c1bd6-118">보내는 지 확인 한 경우 hello Node.js 콘솔 응용 프로그램을 중지할 수 있습니다 **ExternalTemperature** 원격 분석 toohello 미리 솔루션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-118">You can stop hello Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry toohello preconfigured solution.</span></span> <span data-ttu-id="c1bd6-119">다시 실행 하면이 Node.js 콘솔 응용 프로그램 hello 사용자 지정 규칙 toohello 솔루션을 추가한 후 때문에 hello 콘솔 창을 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-119">Keep hello console window open because you run this Node.js console app again after you add hello custom rule toohello solution.</span></span>

## <a name="rule-storage-locations"></a><span data-ttu-id="c1bd6-120">규칙 저장소 위치</span><span class="sxs-lookup"><span data-stu-id="c1bd6-120">Rule storage locations</span></span>

<span data-ttu-id="c1bd6-121">규칙에 대한 정보는 다음 두 위치에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-121">Information about rules is persisted in two locations:</span></span>

* <span data-ttu-id="c1bd6-122">**DeviceRulesNormalizedTable** 테이블-이 테이블에 저장 한 정규화 된 참조 toohello 규칙 hello 솔루션 포털에서 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference toohello rules defined by hello solution portal.</span></span> <span data-ttu-id="c1bd6-123">Hello 솔루션 포털 장치 규칙을 표시 하는 경우 경우이 테이블 hello 규칙 정의 대 한 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-123">When hello solution portal displays device rules, it queries this table for hello rule definitions.</span></span>
* <span data-ttu-id="c1bd6-124">**DeviceRules** – blob이이 blob 저장 장치를 등록 하 고 참조 입력된 toohello Azure 스트림 분석 작업으로 정의 된 모든에 대해 정의 된 모든 hello 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-124">**DeviceRules** blob – This blob stores all hello rules defined for all registered devices and is defined as a reference input toohello Azure Stream Analytics jobs.</span></span>
 
<span data-ttu-id="c1bd6-125">Hello 솔루션 포털에서 새 규칙을 정의 하거나 기존 규칙을 업데이트할 때 hello 테이블 및 blob를 모두 업데이트 tooreflect hello 변경 내용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-125">When you update an existing rule or define a new rule in hello solution portal, both hello table and blob are updated tooreflect hello changes.</span></span> <span data-ttu-id="c1bd6-126">hello 규칙 정의 hello 포털에 표시 되는 hello 테이블 저장소와 정의 hello 스트림 분석 작업에서 참조 하는 hello blob에서 제공 하는 hello 규칙에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-126">hello rule definition displayed in hello portal comes from hello table store, and hello rule definition referenced by hello Stream Analytics jobs comes from hello blob.</span></span> 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a><span data-ttu-id="c1bd6-127">Hello RemoteMonitoring Visual Studio 솔루션을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-127">Update hello RemoteMonitoring Visual Studio solution</span></span>

<span data-ttu-id="c1bd6-128">hello 다음 단계 보여 어떻게 toomodify hello RemoteMonitoring Visual Studio 솔루션 tooinclude hello를 사용 하는 새 규칙 **ExternalTemperature** hello 시뮬레이션 된 장치에서 전송 하는 원격 분석:</span><span class="sxs-lookup"><span data-stu-id="c1bd6-128">hello following steps show you how toomodify hello RemoteMonitoring Visual Studio solution tooinclude a new rule that uses hello **ExternalTemperature** telemetry sent from hello simulated device:</span></span>

1. <span data-ttu-id="c1bd6-129">경우 있습니다 아직 수행 하지 않은 복제 hello 따라서 **azure iot-원격 액세스 모니터링** 다음 Git 명령을 hello를 사용 하 여 로컬 컴퓨터의 저장소 tooa 적합 한 위치:</span><span class="sxs-lookup"><span data-stu-id="c1bd6-129">If you have not already done so, clone hello **azure-iot-remote-monitoring** repository tooa suitable location on your local machine using hello following Git command:</span></span>

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. <span data-ttu-id="c1bd6-130">Visual Studio에서 hello RemoteMonitoring.sln 파일 hello의 로컬 복사본을 엽니다 **azure iot-원격 액세스 모니터링** 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-130">In Visual Studio, open hello RemoteMonitoring.sln file from your local copy of hello **azure-iot-remote-monitoring** repository.</span></span>

3. <span data-ttu-id="c1bd6-131">Infrastructure\Models\DeviceRuleBlobEntity.cs hello 파일을 열고 추가 된 **ExternalTemperature** 속성을 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-131">Open hello file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span></span>

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. <span data-ttu-id="c1bd6-132">Hello 같은 파일에서 추가 된 **ExternalTemperatureRuleOutput** 속성을 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-132">In hello same file, add an **ExternalTemperatureRuleOutput** property as follows:</span></span>

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. <span data-ttu-id="c1bd6-133">Hello 파일 Infrastructure\Models\DeviceRuleDataFields.cs 열고 hello 다음 추가 **ExternalTemperature** hello 기존 속성 **습도** 속성:</span><span class="sxs-lookup"><span data-stu-id="c1bd6-133">Open hello file Infrastructure\Models\DeviceRuleDataFields.cs and add hello following **ExternalTemperature** property after hello existing **Humidity** property:</span></span>

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. <span data-ttu-id="c1bd6-134">동일한 파일 hello 하 hello 업데이트 **_availableDataFields** 메서드 tooinclude **ExternalTemperature** 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-134">In hello same file, update hello **_availableDataFields** method tooinclude **ExternalTemperature** as follows:</span></span>

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. <span data-ttu-id="c1bd6-135">Hello 파일 Infrastructure\Repository\DeviceRulesRepository.cs을 열고 hello 수정 **BuildBlobEntityListFromTableRows** 메서드를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-135">Open hello file Infrastructure\Repository\DeviceRulesRepository.cs and modify hello **BuildBlobEntityListFromTableRows** method as follows:</span></span>

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

## <a name="rebuild-and-redeploy-hello-solution"></a><span data-ttu-id="c1bd6-136">다시 작성 한 hello 솔루션 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-136">Rebuild and redeploy hello solution.</span></span>

<span data-ttu-id="c1bd6-137">이제 업데이트 hello 솔루션 tooyour Azure 구독을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-137">You can now deploy hello updated solution tooyour Azure subscription.</span></span>

1. <span data-ttu-id="c1bd6-138">관리자 권한 명령 프롬프트를 열고 toohello 루트 hello azure iot-원격 액세스 모니터링 저장소의 로컬 복사본을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-138">Open an elevated command prompt and navigate toohello root of your local copy of hello azure-iot-remote-monitoring repository.</span></span>

2. <span data-ttu-id="c1bd6-139">toodeploy hello 명령 대체 하 여 다음을 실행 하 여 업데이트 된 솔루션을 **{배포 이름}** 이전에 기록한 미리 구성 된 솔루션 배포의 hello 이름의:</span><span class="sxs-lookup"><span data-stu-id="c1bd6-139">toodeploy your updated solution, run hello following command substituting **{deployment name}** with hello name of your preconfigured solution deployment that you noted previously:</span></span>

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a><span data-ttu-id="c1bd6-140">Hello 스트림 분석 작업 업데이트</span><span class="sxs-lookup"><span data-stu-id="c1bd6-140">Update hello Stream Analytics job</span></span>

<span data-ttu-id="c1bd6-141">Hello 배포 완료 되 면 hello 스트림 분석 작업 toouse hello 새 규칙 정의 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-141">When hello deployment is complete, you can update hello Stream Analytics job toouse hello new rule definitions.</span></span>

1. <span data-ttu-id="c1bd6-142">Hello Azure 포털에서에서 미리 구성 된 솔루션 리소스를 포함 하는 toohello 리소스 그룹을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-142">In hello Azure portal, navigate toohello resource group that contains your preconfigured solution resources.</span></span> <span data-ttu-id="c1bd6-143">이 리소스 그룹에 이름과 같은 이름을 지정 하는 hello hello 배포 하는 동안 솔루션 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-143">This resource group has hello same name you specified for hello solution during hello deployment.</span></span>

2. <span data-ttu-id="c1bd6-144">{배포 이름} toohello 탐색-규칙 스트림 분석 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-144">Navigate toohello {deployment name}-Rules Stream Analytics job.</span></span> 

3. <span data-ttu-id="c1bd6-145">클릭 **중지** toostop hello 스트림 분석 작업의 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-145">Click **Stop** toostop hello Stream Analytics job from running.</span></span> <span data-ttu-id="c1bd6-146">(기다려야 hello 쿼리를 편집 하려면 먼저 작업 toostop 스트리밍 hello에 대 한).</span><span class="sxs-lookup"><span data-stu-id="c1bd6-146">(You must wait for hello streaming job toostop before you can edit hello query).</span></span>

4. <span data-ttu-id="c1bd6-147">**쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-147">Click **Query**.</span></span> <span data-ttu-id="c1bd6-148">Hello 쿼리 tooinclude hello 편집 **선택** 문을 **ExternalTemperature**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-148">Edit hello query tooinclude hello **SELECT** statement for **ExternalTemperature**.</span></span> <span data-ttu-id="c1bd6-149">hello 다음 샘플 쿼리를 보여 줍니다 hello 전체 hello로 새 **선택** 문:</span><span class="sxs-lookup"><span data-stu-id="c1bd6-149">hello following sample shows hello complete query with hello new **SELECT** statement:</span></span>

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

5. <span data-ttu-id="c1bd6-150">클릭 **저장** toochange hello 규칙 쿼리를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-150">Click **Save** toochange hello updated rule query.</span></span>

6. <span data-ttu-id="c1bd6-151">클릭 **시작** toostart hello 스트림 분석 작업을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-151">Click **Start** toostart hello Stream Analytics job running again.</span></span>

## <a name="add-your-new-rule-in-hello-dashboard"></a><span data-ttu-id="c1bd6-152">Hello 대시보드에 새 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="c1bd6-152">Add your new rule in hello dashboard</span></span>

<span data-ttu-id="c1bd6-153">이제 hello를 추가할 수 있습니다 **ExternalTemperature** hello 솔루션 대시보드에 규칙 tooa 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-153">You can now add hello **ExternalTemperature** rule tooa device in hello solution dashboard.</span></span>

1. <span data-ttu-id="c1bd6-154">Toohello 솔루션 포털을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-154">Navigate toohello solution portal.</span></span>

2. <span data-ttu-id="c1bd6-155">Toohello 이동 **장치** 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-155">Navigate toohello **Devices** panel.</span></span>

3. <span data-ttu-id="c1bd6-156">장치를 찾을 hello 사용자 지정을 만들었으므로 보내는 **ExternalTemperature** 원격 분석 및 hello에 **장치 세부 정보** 에서 **규칙 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-156">Locate hello custom device you created that sends **ExternalTemperature** telemetry and on hello **Device Details** panel, click **Add Rule**.</span></span>

4. <span data-ttu-id="c1bd6-157">**데이터 필드**에서 **ExternalTemperature**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-157">Select **ExternalTemperature** in **Data Field**.</span></span>

5. <span data-ttu-id="c1bd6-158">설정 **임계값** too56 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-158">Set **Threshold** too56.</span></span> <span data-ttu-id="c1bd6-159">그런 후 **규칙 저장 및 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-159">Then click **Save and view rules**.</span></span>

6. <span data-ttu-id="c1bd6-160">Toohello 대시보드 tooview hello 경보 기록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-160">Return toohello dashboard tooview hello alarm history.</span></span>

7. <span data-ttu-id="c1bd6-161">열린 상태로 hello 콘솔 창에 hello Node.js 콘솔 앱 toobegin 보내기 시작 **ExternalTemperature** 원격 분석 데이터.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-161">In hello console window you left open, start hello Node.js console app toobegin sending **ExternalTemperature** telemetry data.</span></span>

8. <span data-ttu-id="c1bd6-162">해당 hello 확인 **경보 기록** 표에서 hello 새 규칙이 트리거되면 새 경보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-162">Notice that hello **Alarm History** table shows new alarms when hello new rule is triggered.</span></span>
 
## <a name="additional-information"></a><span data-ttu-id="c1bd6-163">추가 정보</span><span class="sxs-lookup"><span data-stu-id="c1bd6-163">Additional information</span></span>

<span data-ttu-id="c1bd6-164">변경 hello 연산자  **>**  더 복잡 하 고이 자습서에 설명 된 hello 단계를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-164">Changing hello operator **>** is more complex and goes beyond hello steps outlined in this tutorial.</span></span> <span data-ttu-id="c1bd6-165">Hello 스트림 분석 작업 toouse 원하는 모든 연산자를 변경할 수는 있지만, 더 복잡 한 작업은 hello 솔루션 포털에서 해당 연산자를 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-165">While you can change hello Stream Analytics job toouse whatever operator you like, reflecting that operator in hello solution portal is a more complex task.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c1bd6-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c1bd6-166">Next steps</span></span>
<span data-ttu-id="c1bd6-167">이제 살펴보았으므로 어떻게 toocreate 사용자 지정 규칙에 대해 알 수 있습니다 더 hello 미리 구성 된 솔루션:</span><span class="sxs-lookup"><span data-stu-id="c1bd6-167">Now that you've seen how toocreate custom rules, you can learn more about hello preconfigured solutions:</span></span>

- <span data-ttu-id="c1bd6-168">[논리 앱 tooyour Azure IoT Suite 원격 모니터링 미리 구성 된 솔루션에 연결][lnk-logic-app]</span><span class="sxs-lookup"><span data-stu-id="c1bd6-168">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span></span>
- <span data-ttu-id="c1bd6-169">[솔루션을 미리 구성 된 장치 정보 메타 데이터에서 원격 모니터링 hello][lnk-devinfo]합니다.</span><span class="sxs-lookup"><span data-stu-id="c1bd6-169">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md
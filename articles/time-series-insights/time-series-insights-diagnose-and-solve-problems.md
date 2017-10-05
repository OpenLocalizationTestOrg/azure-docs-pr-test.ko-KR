---
title: "문제 진단 및 해결 | Microsoft Docs"
description: "이 자습서에서는 Time Series Insights 환경에서 문제를 진단하고 해결하는 방법을 다룹니다."
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/24/2017
ms.author: venkatja
ms.openlocfilehash: 4b8d5fdab1744b2db658917f91d6dac05db30d2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="diagnose-and-solve-problems-in-your-time-series-insights-environment"></a><span data-ttu-id="bf576-103">Time Series Insights 환경에서 문제 진단 및 해결</span><span class="sxs-lookup"><span data-stu-id="bf576-103">Diagnose and solve problems in your Time Series Insights environment</span></span>

## <a name="i-dont-see-my-data"></a><span data-ttu-id="bf576-104">내 데이터가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-104">I don't see my data</span></span>
<span data-ttu-id="bf576-105">다음은 [Azure Time Series Insights 포털](https://insights.timeseries.azure.com) 환경에서 데이터가 표시되지 않는 몇 가지 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-105">Here are some reasons why you might not see your data in your environment in the [Azure Time Series Insights portal](https://insights.timeseries.azure.com).</span></span>

### <a name="your-event-source-doesnt-have-data-in-json-format"></a><span data-ttu-id="bf576-106">이벤트 원본에 JSON 형식의 데이터가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-106">Your event source doesn't have data in JSON format</span></span>
<span data-ttu-id="bf576-107">Azure Time Series Insights는 현재 JSON 데이터만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-107">Azure Time Series Insights supports only JSON data today.</span></span> <span data-ttu-id="bf576-108">JSON 샘플의 경우 [지원되는 JSON 셰이프](time-series-insights-send-events.md#supported-json-shapes)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf576-108">For JSON samples, see [Supported JSON shapes](time-series-insights-send-events.md#supported-json-shapes).</span></span>

### <a name="when-you-registered-your-event-source-you-didnt-provide-the-key-that-has-the-required-permission"></a><span data-ttu-id="bf576-109">이벤트 원본을 등록할 때 필요한 사용 권한이 있는 키를 제공하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-109">When you registered your event source, you didn't provide the key that has the required permission</span></span>
* <span data-ttu-id="bf576-110">IoT Hub의 경우 **서비스 연결** 사용 권한이 있는 키를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-110">For an IoT hub, you need to provide the key that has **service connect** permission.</span></span>

   ![Iot Hub 서비스 연결 사용 권한](media/diagnose-and-solve-problems/iothub-serviceconnect-permissions.png)

   <span data-ttu-id="bf576-112">위의 이미지에 표시된 것처럼 **iothubowner** 및 **서비스** 정책에는 모두 **서비스 연결** 사용 권한이 있으므로 둘 중 하나가 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-112">As shown in the preceding image, either of the policies **iothubowner** and **service** would work, because both have **service connect** permission.</span></span>
* <span data-ttu-id="bf576-113">이벤트 허브의 경우 **수신** 사용 권한이 있는 키를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-113">For an event hub, you need to provide the key that has **Listen** permission.</span></span>

   ![이벤트 허브 수신 사용 권한](media/diagnose-and-solve-problems/eventhub-listen-permissions.png)

   <span data-ttu-id="bf576-115">위의 이미지에 표시된 것처럼 **읽기** 및 **관리** 정책에는 모두 **수신** 사용 권한이 있으므로 둘 중 하나가 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-115">As shown in the preceding image, either of the policies **read** and **manage** would work, because both have **Listen** permission.</span></span>

### <a name="the-provided-consumer-group-is-not-exclusive-to-time-series-insights"></a><span data-ttu-id="bf576-116">제공된 소비자 그룹이 Time Series Insights에 배타적으로 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-116">The provided consumer group is not exclusive to Time Series Insights</span></span>
<span data-ttu-id="bf576-117">IoT Hub 또는 이벤트 허브의 경우 등록하면서 데이터를 읽을 때 소비자 그룹이 사용되도록 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-117">For an IoT hub or an event hub, during registration we require you to specify the consumer group that should be used for reading your data.</span></span> <span data-ttu-id="bf576-118">이 소비자 그룹은 공유하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-118">This consumer group must not be shared.</span></span> <span data-ttu-id="bf576-119">공유하면 기본 이벤트 허브는 자동으로 한 읽기 권한자와 임의로 연결을 끊습니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-119">If it's shared, the underlying event hub automatically disconnects one of the readers randomly.</span></span>

## <a name="i-see-my-data-but-theres-a-lag"></a><span data-ttu-id="bf576-120">내 데이터가 표시되지만 시간이 지연됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-120">I see my data, but there's a lag</span></span>
<span data-ttu-id="bf576-121">다음은 [Time Series Insights 포털](https://insights.timeseries.azure.com) 환경에서 부분 데이터가 표시되는 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-121">Here are reasons why you might see partial data in your environment in the [Time Series Insights portal](https://insights.timeseries.azure.com).</span></span>

### <a name="your-environment-is-getting-throttled"></a><span data-ttu-id="bf576-122">사용자 환경이 제한적입니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-122">Your environment is getting throttled</span></span>
<span data-ttu-id="bf576-123">제한적 한도는 환경의 SKU 유형 및 용량을 기준으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-123">The throttling limit is enforced based on the environment's SKU type and capacity.</span></span> <span data-ttu-id="bf576-124">환경의 모든 이벤트 원본은 이 용량을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-124">All event sources in the environment share this capacity.</span></span> <span data-ttu-id="bf576-125">IoT Hub 또는 이벤트 허브에 대한 이벤트 원본이 적용된 한도를 초과하여 데이터를 푸시하는 경우 제한 및 지연될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-125">If the event source for your IoT hub or event hub is pushing data beyond the enforced limits, you see throttling and a lag.</span></span>

<span data-ttu-id="bf576-126">다음 다이어그램에는 SKU S1 및 용량 3을 사용하는 Time Series Insights 환경이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-126">The following diagram shows a Time Series Insights environment that has a SKU of S1 and a capacity of 3.</span></span> <span data-ttu-id="bf576-127">하루에 3백만 개의 이벤트를 수신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-127">It can ingress 3 million events per day.</span></span>

![환경 SKU 현재 용량](media/diagnose-and-solve-problems/environment-sku-current-capacity.png)

<span data-ttu-id="bf576-129">이 환경이 다음 다이어그램에 나타난 것과 같은 수신 속도로 이벤트 허브에서 메시지를 수집하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-129">Assume that this environment is ingesting messages from an event hub with the ingress rate shown in the following diagram:</span></span>

![이벤트 허브에 대한 예제 수신 속도](media/diagnose-and-solve-problems/eventhub-ingress-rate.png)

<span data-ttu-id="bf576-131">다이어그램에 나온 것처럼 일일 수신 속도는 67,000 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-131">As shown in the diagram, the daily ingress rate is ~67,000 messages.</span></span> <span data-ttu-id="bf576-132">이 속도는 분당 약 46 메시지로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-132">This rate translates roughly to 46 messages every minute.</span></span> <span data-ttu-id="bf576-133">각 이벤트 허브 메시지가 단일 Time Series Insights 이벤트로 결합되는 경우 이 환경에서 제한은 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-133">If each event hub message is flattened to a single Time Series Insights event, this environment sees no throttling.</span></span> <span data-ttu-id="bf576-134">각 이벤트 허브 메시지가 100 Time Series Insights 이벤트로 결합되는 경우에는 1분마다 4,600 이벤트가 수집되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-134">If each event hub message is flattened to 100 Time Series Insights events, then 4,600 events should be ingested every minute.</span></span> <span data-ttu-id="bf576-135">용량이 3인 S1 SKU 환경은 1분마다 2,100 이벤트만 수신할 수 있습니다(일별 1백만 이벤트 = 3 단위에서 분당 700 이벤트 = 분당 2,100 이벤트).</span><span class="sxs-lookup"><span data-stu-id="bf576-135">An S1 SKU environment that has a capacity of 3 can ingress only 2,100 events every minute (1 million events per day = 700 events per minute at 3 units = 2,100 events per minute).</span></span> <span data-ttu-id="bf576-136">따라서 제한으로 인해 지연이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-136">Therefore you see a lag due to throttling.</span></span> 

<span data-ttu-id="bf576-137">평면화 논리 작동 방식을 깊이 이해하기 위해서는 [지원되는 JSON 셰이프](time-series-insights-send-events.md#supported-json-shapes)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf576-137">For a high-level understanding of how flattening logic works, see [Supported JSON shapes](time-series-insights-send-events.md#supported-json-shapes).</span></span>

#### <a name="recommended-steps"></a><span data-ttu-id="bf576-138">권장되는 단계</span><span class="sxs-lookup"><span data-stu-id="bf576-138">Recommended steps</span></span>
<span data-ttu-id="bf576-139">지연을 해결하려면 사용자 환경의 SKU 용량을 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-139">To fix the lag, increase the SKU capacity of your environment.</span></span> <span data-ttu-id="bf576-140">자세한 내용은 [Time Series Insights 환경의 크기를 조정하는 방법](time-series-insights-how-to-scale-your-environment.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf576-140">For more information, see [How to scale your Time Series Insights environment](time-series-insights-how-to-scale-your-environment.md).</span></span>

### <a name="youre-pushing-historical-data-and-causing-slow-ingress"></a><span data-ttu-id="bf576-141">기록 데이터를 푸시하고 있어서 수신이 느려지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-141">You're pushing historical data and causing slow ingress</span></span>
<span data-ttu-id="bf576-142">기존 이벤트 원본에 연결되어 있는 경우 이미 IoT Hub 또는 이벤트 허브에 데이터가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-142">If you are connecting an existing event source, it's likely that your IoT hub or event hub already has data in it.</span></span> <span data-ttu-id="bf576-143">따라서 환경은 이벤트 원본 메시지 보존 기간의 시작 부분에서 데이터 풀링을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-143">So the environment starts pulling data from the beginning of the event source's message retention period.</span></span> 

<span data-ttu-id="bf576-144">이 동작은 기본 동작이며 재정의할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-144">This behavior is the default behavior and cannot be overridden.</span></span> <span data-ttu-id="bf576-145">제한을 적용할 수 있으며 기록 데이터 수집을 캐치업하는 데 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-145">You can engage throttling, and it may take a while to catch up on ingesting historical data.</span></span>

#### <a name="recommended-steps"></a><span data-ttu-id="bf576-146">권장되는 단계</span><span class="sxs-lookup"><span data-stu-id="bf576-146">Recommended steps</span></span>
<span data-ttu-id="bf576-147">지연을 해결하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="bf576-147">To fix the lag, take the following steps:</span></span>
1. <span data-ttu-id="bf576-148">SKU 용량을 최대 허용 값(이 경우 10)으로 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-148">Increase the SKU capacity to the maximum allowed value (10 in this case).</span></span> <span data-ttu-id="bf576-149">용량을 증가시키면 수신 프로세스가 훨씬 더 빠르게 캐치업하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-149">After the capacity is increased, the ingress process starts catching up much faster.</span></span> <span data-ttu-id="bf576-150">[Time Series Insights 포털](https://insights.timeseries.azure.com)의 가용성 차트를 통해 얼마나 빨리 캐치업하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-150">You can visualize how quickly you're catching up through the availability chart in the [Time Series Insights portal](https://insights.timeseries.azure.com).</span></span> <span data-ttu-id="bf576-151">증가한 용량에 대해 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-151">You are charged for the increased capacity.</span></span>
2. <span data-ttu-id="bf576-152">지연이 캐치업되면 다시 SKU 용량을 정상 수신 속도로 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-152">After the lag is caught up, decrease the SKU capacity back to your normal ingress rate.</span></span>

## <a name="my-event-sources-timestamp-property-name-setting-doesnt-work"></a><span data-ttu-id="bf576-153">내 이벤트 원본 *타임 스탬프 속성 이름* 설정이 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-153">My event source's *timestamp property name* setting doesn't work</span></span>
<span data-ttu-id="bf576-154">이름 및 값이 다음 규칙을 준수하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-154">Ensure that the name and value conform to the following rules:</span></span>
* <span data-ttu-id="bf576-155">타임스탬프 속성 이름은 _대/소문자를 구분_합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-155">The timestamp property name is _case-sensitive_.</span></span>
* <span data-ttu-id="bf576-156">JSON 문자열처럼 이벤트 원본에서 가져오는 타임스탬프 속성 값은 _yyyy-MM-ddTHH:mm:ss.FFFFFFFK_ 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-156">The timestamp property value that's coming from your event source, as a JSON string, should have the format _yyyy-MM-ddTHH:mm:ss.FFFFFFFK_.</span></span> <span data-ttu-id="bf576-157">이러한 문자열의 예는 “2008-04-12T12:53Z”입니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-157">An example of such a string is “2008-04-12T12:53Z”.</span></span>

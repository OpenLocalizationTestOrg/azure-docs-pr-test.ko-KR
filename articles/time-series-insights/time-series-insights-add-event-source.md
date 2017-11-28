---
title: "이벤트 소스 tooyour Azure 시간 계열 Insights 환경 aaaAdd | Microsoft Docs"
description: "이 자습서에서는 연결 하는 이벤트 소스 tooyour 시간 계열 Insights 환경"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 817df5e81cb4dc3d7376914a4651aabebadbcc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a><span data-ttu-id="cd423-103">Hello Ibiza 포털을 사용 하 여 시간 시계열 Insights 환경에 대 한 이벤트 소스 만들기</span><span class="sxs-lookup"><span data-stu-id="cd423-103">Create an event source for your Time Series Insights environment using hello Ibiza portal</span></span>

<span data-ttu-id="cd423-104">Time Series Insights 이벤트 원본은 Azure Event Hubs 같은 이벤트 브로커에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd423-104">Time Series Insights Event Source is derived from an event broker, like Azure Event Hubs.</span></span> <span data-ttu-id="cd423-105">시간 시계열 Insights tooEvent 원본, 사용자가 toowrite 코드 한 줄을 요구 하지 않고 hello 데이터 스트림을 수집 직접 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd423-105">Time Series Insights connects directly tooEvent Sources, ingesting hello data stream without requiring users toowrite a single line of code.</span></span> <span data-ttu-id="cd423-106">현재 Time Series Insights는 Azure Event Hubs 및 Azure IoT Hubs를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cd423-106">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs.</span></span> <span data-ttu-id="cd423-107">Hello 이후, 더 많은 이벤트 원본은 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd423-107">In hello future, more Event Sources will be added.</span></span>

## <a name="steps-tooadd-an-event-source-tooyour-environment"></a><span data-ttu-id="cd423-108">단계 tooadd 하는 이벤트 소스 tooyour 환경</span><span class="sxs-lookup"><span data-stu-id="cd423-108">Steps tooadd an event source tooyour environment</span></span>

1.  <span data-ttu-id="cd423-109">Toohello 로그인 [Ibiza 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="cd423-109">Sign in toohello [Ibiza portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="cd423-110">Hello hello Ibiza 포털의 왼쪽에 hello 메뉴에서 "모든 리소스"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd423-110">Click “All resources” in hello menu on hello left side of hello Ibiza portal.</span></span>
3.  <span data-ttu-id="cd423-111">Time Series Insights 환경을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd423-111">Select your Time Series Insights environment.</span></span>

  ![Hello 시간 계열 Insights 이벤트 원본 만들기](media/add-event-source/getstarted-create-event-source-1.png)

4.  <span data-ttu-id="cd423-113">“이벤트 원본”을 선택하고 “+ 추가”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd423-113">Select “Event Sources”, click “+ Add.”</span></span>

  ![세부 정보-hello 시간 계열 Insights 이벤트 원본 만들기](media/add-event-source/getstarted-create-event-source-2.png)

5.  <span data-ttu-id="cd423-115">Hello hello 이벤트 소스 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd423-115">Specify hello name of hello event source.</span></span> <span data-ttu-id="cd423-116">이 이름은 이 이벤트 원본에서 오는 모든 이벤트와 연결되어 쿼리 시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd423-116">This name is associated with all events coming from this event source and is available at query time.</span></span>
6.  <span data-ttu-id="cd423-117">Hello 현재 구독에서 이벤트 허브 리소스의 hello 목록에서 이벤트 허브를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd423-117">Select an event hub from hello list of Event Hub resources in hello current subscription.</span></span> <span data-ttu-id="cd423-118">그렇지 않은 경우 가져오기 옵션을 선택 "작업 완료 이벤트 허브 설정 수동으로" toospecify 다른 구독에서 이벤트 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="cd423-118">Otherwise choose import option "Provide Event Hub settings manually” toospecify an event hub in another subscription.</span></span> <span data-ttu-id="cd423-119">이벤트는 JSON 형식으로 게시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd423-119">Events must be published in JSON format.</span></span>
7.  <span data-ttu-id="cd423-120">에 읽기 권한이 hello 이벤트 허브에 정책을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd423-120">Select policy that has read permission in hello event hub.</span></span>
8.  <span data-ttu-id="cd423-121">이벤트 허브 소비자 그룹을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd423-121">Specify event hub consumer group.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="cd423-122">이 소비자 그룹을 다른 서비스(예: Stream Analytics 작업 또는 다른 Time Series Insights 환경)에서 사용하지 못하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd423-122">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="cd423-123">소비자 그룹은 다른 서비스에서 사용 되 면 작업은이 환경에 대 한 부정적인 영향을 읽고 다른 서비스 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd423-123">If consumer group is used by other services, read operation is negatively affected for this environment and hello other services.</span></span> <span data-ttu-id="cd423-124">"$Default" hello 소비자 그룹을 사용 하는 경우 toopotential 다시 사용할 수 있도록 다른 판독기에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd423-124">If you are using “$Default” as hello consumer group, it could lead toopotential reuse by other readers.</span></span>

9.  <span data-ttu-id="cd423-125">“만들기”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd423-125">Click “Create.”</span></span>

<span data-ttu-id="cd423-126">Hello 이벤트 소스를 만든 후 시간 시계열 Insights가 자동으로 시작 환경으로 데이터를 스트리밍.</span><span class="sxs-lookup"><span data-stu-id="cd423-126">After creation of hello event source, Time Series Insights will automatically start streaming data into your environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd423-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cd423-127">Next steps</span></span>

* <span data-ttu-id="cd423-128">[이벤트를 보내는](time-series-insights-send-events.md) toohello 이벤트 소스</span><span class="sxs-lookup"><span data-stu-id="cd423-128">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="cd423-129">[Time Series Insights 포털](https://insights.timeseries.azure.com)에서 환경 보기</span><span class="sxs-lookup"><span data-stu-id="cd423-129">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>

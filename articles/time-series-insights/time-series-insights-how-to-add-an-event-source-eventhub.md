---
title: "aaaHow tooadd는 이벤트 허브 이벤트 소스 tooyour Azure 시간 계열 Insights 환경 | Microsoft Docs"
description: "이 자습서에서는 어떻게 tooadd 이벤트 원본 즉 tooan 연결 된 이벤트 허브 tooyour 시간 계열 Insights 환경"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: a98cd91deb51c829084a00c5f2a80b39d0fc511c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-event-hub-event-source"></a><span data-ttu-id="28856-103">어떻게 tooadd 이벤트 허브 이벤트 소스</span><span class="sxs-lookup"><span data-stu-id="28856-103">How tooadd an Event Hub event source</span></span>

<span data-ttu-id="28856-104">이 자습서에서는 어떻게 toouse hello Azure 포털 tooadd 이벤트 허브 tooyour 시간 계열 Insights 환경에서 읽을 수 있는 이벤트 소스를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="28856-104">This tutorial covers how toouse hello Azure portal tooadd an event source that reads from an Event Hub tooyour Time Series Insights environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28856-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="28856-105">Prerequisites</span></span>

<span data-ttu-id="28856-106">이벤트 허브를 만든 및 이벤트 tooit를 작성 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="28856-106">You have created an Event Hub and are writing events tooit.</span></span> <span data-ttu-id="28856-107">이벤트 허브에 대한 자세한 내용은 <https://azure.microsoft.com/services/event-hubs/>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28856-107">For more information on Event Hubs, see <https://azure.microsoft.com/services/event-hubs/></span></span>

> <span data-ttu-id="28856-108">[소비자 그룹] 각 시간 시계열 Insights 이벤트 소스 toohave 다른 소비자와 공유 되지 않은 자체 전용된 소비자 그룹을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="28856-108">[Consumer Groups] Each Time Series Insights event source needs toohave its own dedicated consumer group that is not shared with any other consumers.</span></span> <span data-ttu-id="28856-109">여러 판독기를 사용 하는 경우 이벤트를 hello 같은 소비자 그룹, 모든 판독기는 가능성이 toosee 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="28856-109">If multiple readers consume events from hello same consumer group, all readers are likely toosee failures.</span></span> <span data-ttu-id="28856-110">또한 이벤트 허브당 20개의 소비자 그룹으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="28856-110">Note that there is also a limit of 20 consumer groups per Event Hub.</span></span> <span data-ttu-id="28856-111">자세한 내용은 참조 hello [이벤트 허브 프로그래밍 가이드](../event-hubs/event-hubs-programming-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="28856-111">For details, see hello [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span>

## <a name="choose-an-import-option"></a><span data-ttu-id="28856-112">가져오기 옵션 선택</span><span class="sxs-lookup"><span data-stu-id="28856-112">Choose an Import option</span></span>

<span data-ttu-id="28856-113">hello 이벤트 소스에 대 한 hello 설정을 수동으로 입력할 수 또는 사용할 수 있는 tooyou 있는 hello 이벤트 허브에서 이벤트 허브를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28856-113">hello settings for hello event source can be entered manually or an event hub can be selected from hello event hubs that are available tooyou.</span></span>
<span data-ttu-id="28856-114">Hello에 **가져오기 옵션** 선택기 hello 다음 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="28856-114">In hello **Import Option** selector, choose one of hello following options:</span></span>

* <span data-ttu-id="28856-115">이벤트 허브 설정 직접 입력</span><span class="sxs-lookup"><span data-stu-id="28856-115">Provide Event Hub settings manually</span></span>
* <span data-ttu-id="28856-116">사용 가능한 구독에서 이벤트 허브 사용</span><span class="sxs-lookup"><span data-stu-id="28856-116">Use Event Hub from available subscriptions</span></span>

### <a name="select-an-available-event-hub"></a><span data-ttu-id="28856-117">사용 가능한 이벤트 허브를 선택</span><span class="sxs-lookup"><span data-stu-id="28856-117">Select an available Event Hub</span></span>

<span data-ttu-id="28856-118">hello 다음 표에서 설명 된 hello 새 이벤트 원본을 탭의 각 옵션 이벤트 소스로 사용할 수 있는 이벤트 허브를 선택 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="28856-118">hello following table explains each option in hello New Event Source tab with its description when selecting an available Event Hub as an event source:</span></span>

| <span data-ttu-id="28856-119">속성 이름</span><span class="sxs-lookup"><span data-stu-id="28856-119">PROPERTY NAME</span></span> | <span data-ttu-id="28856-120">설명</span><span class="sxs-lookup"><span data-stu-id="28856-120">DESCRIPTION</span></span> |
| --- | --- |
| <span data-ttu-id="28856-121">이벤트 원본 이름</span><span class="sxs-lookup"><span data-stu-id="28856-121">Event source name</span></span> | <span data-ttu-id="28856-122">이벤트 소스의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="28856-122">hello name of your event source.</span></span> <span data-ttu-id="28856-123">이 이름은 Time Series Insights 환경 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28856-123">This name must be unique within your Time Series Insights environment.</span></span>
| <span data-ttu-id="28856-124">원본</span><span class="sxs-lookup"><span data-stu-id="28856-124">Source</span></span> | <span data-ttu-id="28856-125">선택 **이벤트 허브** toocreate 이벤트 허브 이벤트 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="28856-125">Choose **Event Hub** toocreate an Event Hub event source.</span></span>
| <span data-ttu-id="28856-126">구독 ID</span><span class="sxs-lookup"><span data-stu-id="28856-126">Subscription Id</span></span> | <span data-ttu-id="28856-127">이 이벤트 허브를 만든 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="28856-127">Select hello subscription in which this event hub was created.</span></span>
| <span data-ttu-id="28856-128">Service Bus 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="28856-128">Service bus namespace</span></span> | <span data-ttu-id="28856-129">Hello 이벤트 허브를 포함 하는 hello 서비스 버스 네임 스페이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="28856-129">Select hello Service Bus namespace that contains hello Event Hub.</span></span>
| <span data-ttu-id="28856-130">이벤트 허브 이름</span><span class="sxs-lookup"><span data-stu-id="28856-130">Event hub name</span></span> | <span data-ttu-id="28856-131">Hello 이벤트 허브의 hello 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="28856-131">Select hello name of hello Event Hub.</span></span>
| <span data-ttu-id="28856-132">이벤트 허브 정책 이름</span><span class="sxs-lookup"><span data-stu-id="28856-132">Event hub policy name</span></span> | <span data-ttu-id="28856-133">Hello 이벤트 허브 구성 탭에서 만들 수 있는 hello 공유 액세스 정책을 선택 합니다. 각 공유 액세스 정책에는 이름, 사용자가 설정한 사용 권한 및 액세스 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28856-133">Select hello shared access policy, which can be created on hello Event Hub Configure tab. Each shared access policy has a name, permissions that you set, and access keys.</span></span> <span data-ttu-id="28856-134">hello 공유 액세스 정책 이벤트 소스에 대 한 *해야* 가 **읽을** 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="28856-134">hello shared access policy for your event source *must* have **read** permissions.</span></span>
| <span data-ttu-id="28856-135">이벤트 허브 소비자 그룹</span><span class="sxs-lookup"><span data-stu-id="28856-135">Event hub consumer group</span></span> | <span data-ttu-id="28856-136">hello 소비자 그룹 tooread hello 이벤트 허브에서에서 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="28856-136">hello Consumer Group tooread events from hello Event Hub.</span></span> <span data-ttu-id="28856-137">이 뛰어납니다 toouse 이벤트 소스에 대 한 전용된 소비자 그룹을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="28856-137">It is highly recommended toouse a dedicated consumer group for your event source.</span></span>

### <a name="provide-event-hub-settings-manually"></a><span data-ttu-id="28856-138">이벤트 허브 설정 직접 입력</span><span class="sxs-lookup"><span data-stu-id="28856-138">Provide Event Hub settings manually</span></span>

<span data-ttu-id="28856-139">hello 다음 표에서 설명 된 hello 새 이벤트 원본을 탭의 각 속성 설정을 입력할 때 수동으로:</span><span class="sxs-lookup"><span data-stu-id="28856-139">hello following table explains each property in hello New Event Source tab with its description when entering settings manually:</span></span>

| <span data-ttu-id="28856-140">속성 이름</span><span class="sxs-lookup"><span data-stu-id="28856-140">PROPERTY NAME</span></span> | <span data-ttu-id="28856-141">설명</span><span class="sxs-lookup"><span data-stu-id="28856-141">DESCRIPTION</span></span> |
| --- | --- |
| <span data-ttu-id="28856-142">이벤트 원본 이름</span><span class="sxs-lookup"><span data-stu-id="28856-142">Event source name</span></span> | <span data-ttu-id="28856-143">이벤트 소스의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="28856-143">hello name of your event source.</span></span> <span data-ttu-id="28856-144">이 이름은 Time Series Insights 환경 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28856-144">This name must be unique within your Time Series Insights environment.</span></span>
| <span data-ttu-id="28856-145">원본</span><span class="sxs-lookup"><span data-stu-id="28856-145">Source</span></span> | <span data-ttu-id="28856-146">선택 **이벤트 허브** toocreate 이벤트 허브 이벤트 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="28856-146">Choose **Event Hub** toocreate an Event Hub event source.</span></span>
| <span data-ttu-id="28856-147">구독 ID</span><span class="sxs-lookup"><span data-stu-id="28856-147">Subscription Id</span></span> | <span data-ttu-id="28856-148">이 이벤트 허브를 만든 hello 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="28856-148">hello subscription in which this event hub was created.</span></span>
| <span data-ttu-id="28856-149">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="28856-149">Resource group</span></span> | <span data-ttu-id="28856-150">이 이벤트 허브를 만든 hello 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="28856-150">hello subscription in which this event hub was created.</span></span>
| <span data-ttu-id="28856-151">Service Bus 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="28856-151">Service bus namespace</span></span> | <span data-ttu-id="28856-152">서비스 버스 네임스페이스는 메시징 엔터티 집합에 대한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="28856-152">A Service Bus namespace is a container for a set of messaging entities.</span></span> <span data-ttu-id="28856-153">새 이벤트 허브를 만들 때 서비스 버스 네임스페이스도 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="28856-153">When you created a new Event Hub, you also created a Service Bus namespace.</span></span>
| <span data-ttu-id="28856-154">이벤트 허브 이름</span><span class="sxs-lookup"><span data-stu-id="28856-154">Event hub name</span></span> | <span data-ttu-id="28856-155">이벤트 허브의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="28856-155">hello name of your Event Hub.</span></span> <span data-ttu-id="28856-156">이벤트 허브를 만들 때 지은 특정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="28856-156">When you created your event hub, you also gave it a specific name</span></span>
| <span data-ttu-id="28856-157">이벤트 허브 정책 이름</span><span class="sxs-lookup"><span data-stu-id="28856-157">Event hub policy name</span></span> | <span data-ttu-id="28856-158">hello 공유 액세스 정책 hello 이벤트 허브 구성 탭에서 만들 수 있습니다. 각 공유 액세스 정책에는 이름, 사용자가 설정한 사용 권한 및 액세스 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28856-158">hello shared access policy, which can be created on hello Event Hub Configure tab. Each shared access policy has a name, permissions that you set, and access keys.</span></span> <span data-ttu-id="28856-159">hello 공유 액세스 정책 이벤트 소스에 대 한 *해야* 가 **읽을** 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="28856-159">hello shared access policy for your event source *must* have **read** permissions.</span></span>
| <span data-ttu-id="28856-160">이벤트 허브 정책 키</span><span class="sxs-lookup"><span data-stu-id="28856-160">Event hub policy key</span></span> | <span data-ttu-id="28856-161">hello 공유 액세스 키 tooauthenticate 액세스 toohello 서비스 버스 네임 스페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="28856-161">hello Shared Access key used tooauthenticate access toohello Service Bus namespace.</span></span> <span data-ttu-id="28856-162">Hello 기본 여기 또는 보조 키를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="28856-162">Type hello primary or secondary key here.</span></span>
| <span data-ttu-id="28856-163">이벤트 허브 소비자 그룹</span><span class="sxs-lookup"><span data-stu-id="28856-163">Event hub consumer group</span></span> | <span data-ttu-id="28856-164">hello 소비자 그룹 tooread hello 이벤트 허브에서에서 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="28856-164">hello Consumer Group tooread events from hello Event Hub.</span></span> <span data-ttu-id="28856-165">이 뛰어납니다 toouse 이벤트 소스에 대 한 전용된 소비자 그룹을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="28856-165">It is highly recommended toouse a dedicated consumer group for your event source.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28856-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="28856-166">Next steps</span></span>

1. <span data-ttu-id="28856-167">추가 데이터 액세스 정책 tooyour 환경 [정의 데이터 액세스 정책](time-series-insights-data-access.md)</span><span class="sxs-lookup"><span data-stu-id="28856-167">Add a data access policy tooyour environment [Define data access policies](time-series-insights-data-access.md)</span></span>
1. <span data-ttu-id="28856-168">사용자 환경에서 hello 액세스 [시간 계열 Insights 포털](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="28856-168">Access your environment in hello [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>

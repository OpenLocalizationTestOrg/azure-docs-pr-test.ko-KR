---
title: "Azure Time Series Insights 환경에 이벤트 허브 이벤트 원본을 추가하는 방법 | Microsoft Docs"
description: "이 자습서에서는 이벤트 허브에 연결된 이벤트 원본을 Time Series Insights 환경에 추가하는 방법을 다룹니다."
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
ms.openlocfilehash: 216c2146371e2b88d4a3d7aa4f08ae8186e89443
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-an-event-hub-event-source"></a><span data-ttu-id="606b6-103">이벤트 허브 이벤트 원본을 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="606b6-103">How to add an Event Hub event source</span></span>

<span data-ttu-id="606b6-104">이 자습서에서는 Azure Portal을 사용하여 이벤트 허브에서 읽는 이벤트 원본을 Time Series Insights 환경에 추가하는 방법을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-104">This tutorial covers how to use the Azure portal to add an event source that reads from an Event Hub to your Time Series Insights environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="606b6-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="606b6-105">Prerequisites</span></span>

<span data-ttu-id="606b6-106">이벤트 허브를 만들고 이벤트를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-106">You have created an Event Hub and are writing events to it.</span></span> <span data-ttu-id="606b6-107">이벤트 허브에 대한 자세한 내용은 <https://azure.microsoft.com/services/event-hubs/>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="606b6-107">For more information on Event Hubs, see <https://azure.microsoft.com/services/event-hubs/></span></span>

> <span data-ttu-id="606b6-108">[소비자 그룹] 각 Time Series Insights 이벤트 원본에는 다른 소비자와 공유되지 않은 전용 소비자 그룹 자체가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-108">[Consumer Groups] Each Time Series Insights event source needs to have its own dedicated consumer group that is not shared with any other consumers.</span></span> <span data-ttu-id="606b6-109">같은 소비자 그룹에서 여러 읽기 권한자가 이벤트를 소비하는 경우 모든 읽기 권한자에게 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-109">If multiple readers consume events from the same consumer group, all readers are likely to see failures.</span></span> <span data-ttu-id="606b6-110">또한 이벤트 허브당 20개의 소비자 그룹으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-110">Note that there is also a limit of 20 consumer groups per Event Hub.</span></span> <span data-ttu-id="606b6-111">자세한 내용은 [이벤트 허브 프로그래밍 가이드](../event-hubs/event-hubs-programming-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="606b6-111">For details, see the [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span>

## <a name="choose-an-import-option"></a><span data-ttu-id="606b6-112">가져오기 옵션 선택</span><span class="sxs-lookup"><span data-stu-id="606b6-112">Choose an Import option</span></span>

<span data-ttu-id="606b6-113">이벤트 원본에 대한 설정을 직접 입력하거나 사용할 수 있는 이벤트 허브에서 이벤트 허브를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-113">The settings for the event source can be entered manually or an event hub can be selected from the event hubs that are available to you.</span></span>
<span data-ttu-id="606b6-114">**가져오기 옵션** 선택기에서 다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-114">In the **Import Option** selector, choose one of the following options:</span></span>

* <span data-ttu-id="606b6-115">이벤트 허브 설정 직접 입력</span><span class="sxs-lookup"><span data-stu-id="606b6-115">Provide Event Hub settings manually</span></span>
* <span data-ttu-id="606b6-116">사용 가능한 구독에서 이벤트 허브 사용</span><span class="sxs-lookup"><span data-stu-id="606b6-116">Use Event Hub from available subscriptions</span></span>

### <a name="select-an-available-event-hub"></a><span data-ttu-id="606b6-117">사용 가능한 이벤트 허브를 선택</span><span class="sxs-lookup"><span data-stu-id="606b6-117">Select an available Event Hub</span></span>

<span data-ttu-id="606b6-118">다음 테이블에는 이벤트 원본으로 사용할 수 있는 이벤트 허브를 선택하는 경우 새 이벤트 원본 탭의 각 옵션이 해당 설명과 함께 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-118">The following table explains each option in the New Event Source tab with its description when selecting an available Event Hub as an event source:</span></span>

| <span data-ttu-id="606b6-119">속성 이름</span><span class="sxs-lookup"><span data-stu-id="606b6-119">PROPERTY NAME</span></span> | <span data-ttu-id="606b6-120">설명</span><span class="sxs-lookup"><span data-stu-id="606b6-120">DESCRIPTION</span></span> |
| --- | --- |
| <span data-ttu-id="606b6-121">이벤트 원본 이름</span><span class="sxs-lookup"><span data-stu-id="606b6-121">Event source name</span></span> | <span data-ttu-id="606b6-122">이벤트 원본의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-122">The name of your event source.</span></span> <span data-ttu-id="606b6-123">이 이름은 Time Series Insights 환경 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-123">This name must be unique within your Time Series Insights environment.</span></span>
| <span data-ttu-id="606b6-124">원본</span><span class="sxs-lookup"><span data-stu-id="606b6-124">Source</span></span> | <span data-ttu-id="606b6-125">**이벤트 허브**를 선택하여 이벤트 허브 이벤트 원본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-125">Choose **Event Hub** to create an Event Hub event source.</span></span>
| <span data-ttu-id="606b6-126">구독 ID</span><span class="sxs-lookup"><span data-stu-id="606b6-126">Subscription Id</span></span> | <span data-ttu-id="606b6-127">이 이벤트 허브가 만들어진 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-127">Select the subscription in which this event hub was created.</span></span>
| <span data-ttu-id="606b6-128">Service Bus 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="606b6-128">Service bus namespace</span></span> | <span data-ttu-id="606b6-129">이벤트 허브를 포함하는 Service Bus 네임스페이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-129">Select the Service Bus namespace that contains the Event Hub.</span></span>
| <span data-ttu-id="606b6-130">이벤트 허브 이름</span><span class="sxs-lookup"><span data-stu-id="606b6-130">Event hub name</span></span> | <span data-ttu-id="606b6-131">이벤트 허브의 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-131">Select the name of the Event Hub.</span></span>
| <span data-ttu-id="606b6-132">이벤트 허브 정책 이름</span><span class="sxs-lookup"><span data-stu-id="606b6-132">Event hub policy name</span></span> | <span data-ttu-id="606b6-133">이벤트 허브 구성 탭에서 만들 수 있는 공유 액세스 정책을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-133">Select the shared access policy, which can be created on the Event Hub Configure tab.</span></span> <span data-ttu-id="606b6-134">각 공유 액세스 정책에는 이름, 사용자가 설정한 사용 권한 및 액세스 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-134">Each shared access policy has a name, permissions that you set, and access keys.</span></span> <span data-ttu-id="606b6-135">이벤트 원본에 대한 공유 액세스 정책에는 **읽기** 사용 권한이 *반드시* 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-135">The shared access policy for your event source *must* have **read** permissions.</span></span>
| <span data-ttu-id="606b6-136">이벤트 허브 소비자 그룹</span><span class="sxs-lookup"><span data-stu-id="606b6-136">Event hub consumer group</span></span> | <span data-ttu-id="606b6-137">이벤트 허브에서 이벤트를 읽는 소비자 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-137">The Consumer Group to read events from the Event Hub.</span></span> <span data-ttu-id="606b6-138">이벤트 원본에 대한 전용 소비자 그룹을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-138">It is highly recommended to use a dedicated consumer group for your event source.</span></span>

### <a name="provide-event-hub-settings-manually"></a><span data-ttu-id="606b6-139">이벤트 허브 설정 직접 입력</span><span class="sxs-lookup"><span data-stu-id="606b6-139">Provide Event Hub settings manually</span></span>

<span data-ttu-id="606b6-140">다음 테이블에는 설정을 직접 입력하는 경우 새 이벤트 원본 탭의 각 속성과 해당 설명이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-140">The following table explains each property in the New Event Source tab with its description when entering settings manually:</span></span>

| <span data-ttu-id="606b6-141">속성 이름</span><span class="sxs-lookup"><span data-stu-id="606b6-141">PROPERTY NAME</span></span> | <span data-ttu-id="606b6-142">설명</span><span class="sxs-lookup"><span data-stu-id="606b6-142">DESCRIPTION</span></span> |
| --- | --- |
| <span data-ttu-id="606b6-143">이벤트 원본 이름</span><span class="sxs-lookup"><span data-stu-id="606b6-143">Event source name</span></span> | <span data-ttu-id="606b6-144">이벤트 원본의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-144">The name of your event source.</span></span> <span data-ttu-id="606b6-145">이 이름은 Time Series Insights 환경 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-145">This name must be unique within your Time Series Insights environment.</span></span>
| <span data-ttu-id="606b6-146">원본</span><span class="sxs-lookup"><span data-stu-id="606b6-146">Source</span></span> | <span data-ttu-id="606b6-147">**이벤트 허브**를 선택하여 이벤트 허브 이벤트 원본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-147">Choose **Event Hub** to create an Event Hub event source.</span></span>
| <span data-ttu-id="606b6-148">구독 ID</span><span class="sxs-lookup"><span data-stu-id="606b6-148">Subscription Id</span></span> | <span data-ttu-id="606b6-149">이 이벤트 허브가 만들어진 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-149">The subscription in which this event hub was created.</span></span>
| <span data-ttu-id="606b6-150">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="606b6-150">Resource group</span></span> | <span data-ttu-id="606b6-151">이 이벤트 허브가 만들어진 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-151">The subscription in which this event hub was created.</span></span>
| <span data-ttu-id="606b6-152">Service Bus 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="606b6-152">Service bus namespace</span></span> | <span data-ttu-id="606b6-153">서비스 버스 네임스페이스는 메시징 엔터티 집합에 대한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-153">A Service Bus namespace is a container for a set of messaging entities.</span></span> <span data-ttu-id="606b6-154">새 이벤트 허브를 만들 때 서비스 버스 네임스페이스도 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-154">When you created a new Event Hub, you also created a Service Bus namespace.</span></span>
| <span data-ttu-id="606b6-155">이벤트 허브 이름</span><span class="sxs-lookup"><span data-stu-id="606b6-155">Event hub name</span></span> | <span data-ttu-id="606b6-156">이벤트 허브의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-156">The name of your Event Hub.</span></span> <span data-ttu-id="606b6-157">이벤트 허브를 만들 때 지은 특정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-157">When you created your event hub, you also gave it a specific name</span></span>
| <span data-ttu-id="606b6-158">이벤트 허브 정책 이름</span><span class="sxs-lookup"><span data-stu-id="606b6-158">Event hub policy name</span></span> | <span data-ttu-id="606b6-159">이벤트 허브 구성 탭에서 만들 수 있는 공유 액세스 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-159">The shared access policy, which can be created on the Event Hub Configure tab.</span></span> <span data-ttu-id="606b6-160">각 공유 액세스 정책에는 이름, 사용자가 설정한 사용 권한 및 액세스 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-160">Each shared access policy has a name, permissions that you set, and access keys.</span></span> <span data-ttu-id="606b6-161">이벤트 원본에 대한 공유 액세스 정책에는 **읽기** 사용 권한이 *반드시* 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-161">The shared access policy for your event source *must* have **read** permissions.</span></span>
| <span data-ttu-id="606b6-162">이벤트 허브 정책 키</span><span class="sxs-lookup"><span data-stu-id="606b6-162">Event hub policy key</span></span> | <span data-ttu-id="606b6-163">서비스 버스 네임스페이스에 대한 액세스를 인증하는 데 사용되는 공유 액세스 키</span><span class="sxs-lookup"><span data-stu-id="606b6-163">The Shared Access key used to authenticate access to the Service Bus namespace.</span></span> <span data-ttu-id="606b6-164">기본 또는 보조 키를 여기에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-164">Type the primary or secondary key here.</span></span>
| <span data-ttu-id="606b6-165">이벤트 허브 소비자 그룹</span><span class="sxs-lookup"><span data-stu-id="606b6-165">Event hub consumer group</span></span> | <span data-ttu-id="606b6-166">이벤트 허브에서 이벤트를 읽는 소비자 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-166">The Consumer Group to read events from the Event Hub.</span></span> <span data-ttu-id="606b6-167">이벤트 원본에 대한 전용 소비자 그룹을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="606b6-167">It is highly recommended to use a dedicated consumer group for your event source.</span></span>

## <a name="next-steps"></a><span data-ttu-id="606b6-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="606b6-168">Next steps</span></span>

1. <span data-ttu-id="606b6-169">데이터 액세스 정책을 사용자 환경의 [데이터 액세스 정책 정의](time-series-insights-data-access.md)에 추가</span><span class="sxs-lookup"><span data-stu-id="606b6-169">Add a data access policy to your environment [Define data access policies](time-series-insights-data-access.md)</span></span>
1. <span data-ttu-id="606b6-170">[Time Series Insights 포털](https://insights.timeseries.azure.com)에서 환경에 액세스</span><span class="sxs-lookup"><span data-stu-id="606b6-170">Access your environment in the [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
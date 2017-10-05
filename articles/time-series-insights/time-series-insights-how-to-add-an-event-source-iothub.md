---
title: "Azure Time Series Insights 환경에 IoT Hub 이벤트 원본을 추가하는 방법 | Microsoft Docs"
description: "이 자습서에서는 IoT Hub에 연결된 이벤트 원본을 Time Series Insights 환경에 추가하는 방법을 다룹니다."
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
ms.openlocfilehash: 72037677fac528ff8174d25b474ca7e70826a7b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-an-iot-hub-event-source"></a><span data-ttu-id="25926-103">IoT Hub 이벤트 원본을 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="25926-103">How to add an IoT Hub event source</span></span>

<span data-ttu-id="25926-104">이 자습서에서는 Azure Portal을 사용하여 IoT Hub에서 읽는 이벤트 원본을 Time Series Insights 환경에 추가하는 방법을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="25926-104">This tutorial covers how to use the Azure portal to add an event source that reads from an IoT Hub to your Time Series Insights environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25926-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="25926-105">Prerequisites</span></span>

<span data-ttu-id="25926-106">IoT Hub를 만들고 이벤트를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="25926-106">You have created an IoT Hub and are writing events to it.</span></span> <span data-ttu-id="25926-107">IoT Hub에 대한 자세한 내용은 <https://azure.microsoft.com/services/iot-hub/>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25926-107">For more information on IoT Hubs, see <https://azure.microsoft.com/services/iot-hub/></span></span>

> <span data-ttu-id="25926-108">[소비자 그룹] 각 Time Series Insights 이벤트 원본에는 다른 소비자와 공유되지 않은 전용 소비자 그룹 자체가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25926-108">[Consumer Groups] Each Time Series Insights event source needs to have its own dedicated consumer group that is not shared with any other consumers.</span></span> <span data-ttu-id="25926-109">같은 소비자 그룹에서 여러 읽기 권한자가 이벤트를 소비하는 경우 모든 읽기 권한자에게 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25926-109">If multiple readers consume events from the same consumer group, all readers are likely to see failures.</span></span> <span data-ttu-id="25926-110">자세한 내용은 [IoT Hub 개발자 가이드](../iot-hub/iot-hub-devguide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25926-110">For details, see the [IoT Hub developer guide](../iot-hub/iot-hub-devguide.md).</span></span>

## <a name="choose-an-import-option"></a><span data-ttu-id="25926-111">가져오기 옵션 선택</span><span class="sxs-lookup"><span data-stu-id="25926-111">Choose an Import option</span></span>

<span data-ttu-id="25926-112">이벤트 원본에 대한 설정을 직접 입력하거나 사용할 수 있는 IoT Hub에서 IoT Hub를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25926-112">The settings for the event source can be entered manually or an IoT hub can be selected from the IoT hubs that are available to you.</span></span>
<span data-ttu-id="25926-113">**가져오기 옵션** 선택기에서 다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25926-113">In the **Import Option** selector, choose one of the following options:</span></span>

* <span data-ttu-id="25926-114">IoT Hub 설정 직접 입력</span><span class="sxs-lookup"><span data-stu-id="25926-114">Provide IoT Hub settings manually</span></span>
* <span data-ttu-id="25926-115">사용 가능한 구독에서 IoT Hub 사용</span><span class="sxs-lookup"><span data-stu-id="25926-115">Use IoT Hub from available subscriptions</span></span>

### <a name="select-an-available-iot-hub"></a><span data-ttu-id="25926-116">사용 가능한 IoT Hub를 선택</span><span class="sxs-lookup"><span data-stu-id="25926-116">Select an available IoT Hub</span></span>

<span data-ttu-id="25926-117">다음 테이블에는 이벤트 원본으로 사용할 수 있는 IoT Hub를 선택하는 경우 새 이벤트 원본 탭의 각 옵션이 해당 설명과 함께 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25926-117">The following table explains each option in the New Event Source tab with its description when selecting an available IoT Hub as an event source:</span></span>

| <span data-ttu-id="25926-118">속성 이름</span><span class="sxs-lookup"><span data-stu-id="25926-118">PROPERTY NAME</span></span> | <span data-ttu-id="25926-119">설명</span><span class="sxs-lookup"><span data-stu-id="25926-119">DESCRIPTION</span></span> |
| --- | --- |
| <span data-ttu-id="25926-120">이벤트 원본 이름</span><span class="sxs-lookup"><span data-stu-id="25926-120">Event source name</span></span> | <span data-ttu-id="25926-121">이벤트 원본의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="25926-121">The name of your event source.</span></span> <span data-ttu-id="25926-122">이 이름은 Time Series Insights 환경 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25926-122">This name must be unique within your Time Series Insights environment.</span></span>
| <span data-ttu-id="25926-123">원본</span><span class="sxs-lookup"><span data-stu-id="25926-123">Source</span></span> | <span data-ttu-id="25926-124">**IoT Hub**를 선택하여 IoT Hub 이벤트 원본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="25926-124">Choose **IoT Hub** to create an IoT Hub event source.</span></span>
| <span data-ttu-id="25926-125">구독 ID</span><span class="sxs-lookup"><span data-stu-id="25926-125">Subscription Id</span></span> | <span data-ttu-id="25926-126">이 IoT Hub가 만들어진 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25926-126">Select the subscription in which this IoT hub was created.</span></span>
| <span data-ttu-id="25926-127">IoT Hub 이름</span><span class="sxs-lookup"><span data-stu-id="25926-127">IoT hub name</span></span> | <span data-ttu-id="25926-128">IoT Hub 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25926-128">Select the name of the IoT Hub.</span></span>
| <span data-ttu-id="25926-129">IoT Hub 정책 이름</span><span class="sxs-lookup"><span data-stu-id="25926-129">IoT hub policy name</span></span> | <span data-ttu-id="25926-130">IoT Hub 설정 탭에서 찾을 수 있는 공유 액세스 정책을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25926-130">Select the shared access policy, which can be found on the IoT Hub settings tab.</span></span> <span data-ttu-id="25926-131">각 공유 액세스 정책에는 이름, 사용자가 설정한 사용 권한 및 액세스 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25926-131">Each shared access policy has a name, permissions that you set, and access keys.</span></span> <span data-ttu-id="25926-132">이벤트 원본에 대한 공유 액세스 정책에는 **서비스 연결** 사용 권한이 *반드시* 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25926-132">The shared access policy for your event source *must* have **service connect** permissions.</span></span>
| <span data-ttu-id="25926-133">IoT Hub 소비자 그룹</span><span class="sxs-lookup"><span data-stu-id="25926-133">IoT hub consumer group</span></span> | <span data-ttu-id="25926-134">IoT Hub에서 이벤트를 읽는 소비자 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="25926-134">The Consumer Group to read events from the IoT Hub.</span></span> <span data-ttu-id="25926-135">이벤트 원본에 대한 전용 소비자 그룹을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="25926-135">It is highly recommended to use a dedicated consumer group for your event source.</span></span>

### <a name="provide-iot-hub-settings-manually"></a><span data-ttu-id="25926-136">IoT Hub 설정 직접 입력</span><span class="sxs-lookup"><span data-stu-id="25926-136">Provide IoT Hub settings manually</span></span>

<span data-ttu-id="25926-137">다음 테이블에는 설정을 직접 입력하는 경우 새 이벤트 원본 탭의 각 속성과 해당 설명이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25926-137">The following table explains each property in the New Event Source tab with its description when entering settings manually:</span></span>

| <span data-ttu-id="25926-138">속성 이름</span><span class="sxs-lookup"><span data-stu-id="25926-138">PROPERTY NAME</span></span> | <span data-ttu-id="25926-139">설명</span><span class="sxs-lookup"><span data-stu-id="25926-139">DESCRIPTION</span></span> |
| --- | --- |
| <span data-ttu-id="25926-140">이벤트 원본 이름</span><span class="sxs-lookup"><span data-stu-id="25926-140">Event source name</span></span> | <span data-ttu-id="25926-141">이벤트 원본의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="25926-141">The name of your event source.</span></span> <span data-ttu-id="25926-142">이 이름은 Time Series Insights 환경 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25926-142">This name must be unique within your Time Series Insights environment.</span></span>
| <span data-ttu-id="25926-143">원본</span><span class="sxs-lookup"><span data-stu-id="25926-143">Source</span></span> | <span data-ttu-id="25926-144">**IoT Hub**를 선택하여 IoT Hub 이벤트 원본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="25926-144">Choose **IoT Hub** to create an IoT Hub event source.</span></span>
| <span data-ttu-id="25926-145">구독 ID</span><span class="sxs-lookup"><span data-stu-id="25926-145">Subscription Id</span></span> | <span data-ttu-id="25926-146">이 IoT Hub가 만들어진 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="25926-146">The subscription in which this IoT hub was created.</span></span>
| <span data-ttu-id="25926-147">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="25926-147">Resource group</span></span> | <span data-ttu-id="25926-148">이 IoT Hub가 만들어진 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="25926-148">The subscription in which this IoT hub was created.</span></span>
| <span data-ttu-id="25926-149">IoT Hub 이름</span><span class="sxs-lookup"><span data-stu-id="25926-149">IoT hub name</span></span> | <span data-ttu-id="25926-150">IoT Hub의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="25926-150">The name of your IoT Hub.</span></span> <span data-ttu-id="25926-151">IoT Hub를 만들 때 사용자가 지은 특정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="25926-151">When you created your IoT hub, you also gave it a specific name</span></span>
| <span data-ttu-id="25926-152">IoT Hub 정책 이름</span><span class="sxs-lookup"><span data-stu-id="25926-152">IoT hub policy name</span></span> | <span data-ttu-id="25926-153">IoT Hub 설정 탭에서 찾을 수 있는 공유 액세스 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="25926-153">The shared access policy, which can be created on the IoT Hub settings tab.</span></span> <span data-ttu-id="25926-154">각 공유 액세스 정책에는 이름, 사용자가 설정한 사용 권한 및 액세스 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25926-154">Each shared access policy has a name, permissions that you set, and access keys.</span></span> <span data-ttu-id="25926-155">이벤트 원본에 대한 공유 액세스 정책에는 **서비스 연결** 사용 권한이 *반드시* 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25926-155">The shared access policy for your event source *must* have **service connect** permissions.</span></span>
| <span data-ttu-id="25926-156">IoT Hub 정책 키</span><span class="sxs-lookup"><span data-stu-id="25926-156">IoT hub policy key</span></span> | <span data-ttu-id="25926-157">서비스 버스 네임스페이스에 대한 액세스를 인증하는 데 사용되는 공유 액세스 키</span><span class="sxs-lookup"><span data-stu-id="25926-157">The Shared Access key used to authenticate access to the Service Bus namespace.</span></span> <span data-ttu-id="25926-158">기본 또는 보조 키를 여기에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="25926-158">Type the primary or secondary key here.</span></span>
| <span data-ttu-id="25926-159">IoT Hub 소비자 그룹</span><span class="sxs-lookup"><span data-stu-id="25926-159">IoT hub consumer group</span></span> | <span data-ttu-id="25926-160">IoT Hub에서 이벤트를 읽는 소비자 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="25926-160">The Consumer Group to read events from the IoT Hub.</span></span> <span data-ttu-id="25926-161">이벤트 원본에 대한 전용 소비자 그룹을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="25926-161">It is highly recommended to use a dedicated consumer group for your event source.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25926-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="25926-162">Next steps</span></span>

1. <span data-ttu-id="25926-163">데이터 액세스 정책을 사용자 환경의 [데이터 액세스 정책 정의](time-series-insights-data-access.md)에 추가</span><span class="sxs-lookup"><span data-stu-id="25926-163">Add a data access policy to your environment [Define data access policies](time-series-insights-data-access.md)</span></span>
1. <span data-ttu-id="25926-164">[Time Series Insights 포털](https://insights.timeseries.azure.com)에서 환경에 액세스</span><span class="sxs-lookup"><span data-stu-id="25926-164">Access your environment in the [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
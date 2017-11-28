---
title: "aaaHow tooadd는 IoT 허브 이벤트 소스 tooyour Azure 시간 계열 Insights 환경 | Microsoft Docs"
description: "이 자습서에 설명 된 이벤트 소스가 tooadd tooan IoT Hub tooyour 시간 계열 Insights 환경 연결 하는 방법"
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
ms.openlocfilehash: c626f9653d1c012360120fa9fc3d211d7d5beb5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-iot-hub-event-source"></a><span data-ttu-id="035a0-103">어떻게 tooadd IoT 허브 이벤트 소스</span><span class="sxs-lookup"><span data-stu-id="035a0-103">How tooadd an IoT Hub event source</span></span>

<span data-ttu-id="035a0-104">이 자습서에서는 어떻게 toouse hello Azure 포털 tooadd IoT Hub tooyour 시간 계열 Insights 환경에서 읽을 수 있는 이벤트 소스를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-104">This tutorial covers how toouse hello Azure portal tooadd an event source that reads from an IoT Hub tooyour Time Series Insights environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="035a0-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="035a0-105">Prerequisites</span></span>

<span data-ttu-id="035a0-106">만든 IoT Hub 및 이벤트 tooit를 작성 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-106">You have created an IoT Hub and are writing events tooit.</span></span> <span data-ttu-id="035a0-107">IoT Hub에 대한 자세한 내용은 <https://azure.microsoft.com/services/iot-hub/>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="035a0-107">For more information on IoT Hubs, see <https://azure.microsoft.com/services/iot-hub/></span></span>

> <span data-ttu-id="035a0-108">[소비자 그룹] 각 시간 시계열 Insights 이벤트 소스 toohave 다른 소비자와 공유 되지 않은 자체 전용된 소비자 그룹을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-108">[Consumer Groups] Each Time Series Insights event source needs toohave its own dedicated consumer group that is not shared with any other consumers.</span></span> <span data-ttu-id="035a0-109">여러 판독기를 사용 하는 경우 이벤트를 hello 같은 소비자 그룹, 모든 판독기는 가능성이 toosee 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-109">If multiple readers consume events from hello same consumer group, all readers are likely toosee failures.</span></span> <span data-ttu-id="035a0-110">자세한 내용은 참조 hello [IoT 허브 개발자 가이드](../iot-hub/iot-hub-devguide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-110">For details, see hello [IoT Hub developer guide](../iot-hub/iot-hub-devguide.md).</span></span>

## <a name="choose-an-import-option"></a><span data-ttu-id="035a0-111">가져오기 옵션 선택</span><span class="sxs-lookup"><span data-stu-id="035a0-111">Choose an Import option</span></span>

<span data-ttu-id="035a0-112">hello 이벤트 소스에 대 한 hello 설정을 직접 입력 하거나 tooyou 사용할 수 있는 hello IoT 허브에서 IoT hub를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-112">hello settings for hello event source can be entered manually or an IoT hub can be selected from hello IoT hubs that are available tooyou.</span></span>
<span data-ttu-id="035a0-113">Hello에 **가져오기 옵션** 선택기 hello 다음 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-113">In hello **Import Option** selector, choose one of hello following options:</span></span>

* <span data-ttu-id="035a0-114">IoT Hub 설정 직접 입력</span><span class="sxs-lookup"><span data-stu-id="035a0-114">Provide IoT Hub settings manually</span></span>
* <span data-ttu-id="035a0-115">사용 가능한 구독에서 IoT Hub 사용</span><span class="sxs-lookup"><span data-stu-id="035a0-115">Use IoT Hub from available subscriptions</span></span>

### <a name="select-an-available-iot-hub"></a><span data-ttu-id="035a0-116">사용 가능한 IoT Hub를 선택</span><span class="sxs-lookup"><span data-stu-id="035a0-116">Select an available IoT Hub</span></span>

<span data-ttu-id="035a0-117">hello 다음 표에서 설명 된 hello 새 이벤트 원본을 탭의 각 옵션 이벤트 소스로 사용할 수 있는 IoT Hub를 선택 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="035a0-117">hello following table explains each option in hello New Event Source tab with its description when selecting an available IoT Hub as an event source:</span></span>

| <span data-ttu-id="035a0-118">속성 이름</span><span class="sxs-lookup"><span data-stu-id="035a0-118">PROPERTY NAME</span></span> | <span data-ttu-id="035a0-119">설명</span><span class="sxs-lookup"><span data-stu-id="035a0-119">DESCRIPTION</span></span> |
| --- | --- |
| <span data-ttu-id="035a0-120">이벤트 원본 이름</span><span class="sxs-lookup"><span data-stu-id="035a0-120">Event source name</span></span> | <span data-ttu-id="035a0-121">이벤트 소스의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-121">hello name of your event source.</span></span> <span data-ttu-id="035a0-122">이 이름은 Time Series Insights 환경 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-122">This name must be unique within your Time Series Insights environment.</span></span>
| <span data-ttu-id="035a0-123">원본</span><span class="sxs-lookup"><span data-stu-id="035a0-123">Source</span></span> | <span data-ttu-id="035a0-124">선택 **IoT Hub** toocreate IoT 허브 이벤트 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-124">Choose **IoT Hub** toocreate an IoT Hub event source.</span></span>
| <span data-ttu-id="035a0-125">구독 ID</span><span class="sxs-lookup"><span data-stu-id="035a0-125">Subscription Id</span></span> | <span data-ttu-id="035a0-126">이 IoT 허브를 만든 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-126">Select hello subscription in which this IoT hub was created.</span></span>
| <span data-ttu-id="035a0-127">IoT Hub 이름</span><span class="sxs-lookup"><span data-stu-id="035a0-127">IoT hub name</span></span> | <span data-ttu-id="035a0-128">IoT Hub hello의 hello 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-128">Select hello name of hello IoT Hub.</span></span>
| <span data-ttu-id="035a0-129">IoT Hub 정책 이름</span><span class="sxs-lookup"><span data-stu-id="035a0-129">IoT hub policy name</span></span> | <span data-ttu-id="035a0-130">Hello IoT Hub 설정 탭에서 찾을 수 있는 hello 공유 액세스 정책을 선택 합니다. 각 공유 액세스 정책에는 이름, 사용자가 설정한 사용 권한 및 액세스 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-130">Select hello shared access policy, which can be found on hello IoT Hub settings tab. Each shared access policy has a name, permissions that you set, and access keys.</span></span> <span data-ttu-id="035a0-131">hello 공유 액세스 정책 이벤트 소스에 대 한 *해야* 가 **서비스 연결** 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="035a0-131">hello shared access policy for your event source *must* have **service connect** permissions.</span></span>
| <span data-ttu-id="035a0-132">IoT Hub 소비자 그룹</span><span class="sxs-lookup"><span data-stu-id="035a0-132">IoT hub consumer group</span></span> | <span data-ttu-id="035a0-133">hello 소비자 그룹 tooread hello IoT 허브에서에서 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-133">hello Consumer Group tooread events from hello IoT Hub.</span></span> <span data-ttu-id="035a0-134">이 뛰어납니다 toouse 이벤트 소스에 대 한 전용된 소비자 그룹을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-134">It is highly recommended toouse a dedicated consumer group for your event source.</span></span>

### <a name="provide-iot-hub-settings-manually"></a><span data-ttu-id="035a0-135">IoT Hub 설정 직접 입력</span><span class="sxs-lookup"><span data-stu-id="035a0-135">Provide IoT Hub settings manually</span></span>

<span data-ttu-id="035a0-136">hello 다음 표에서 설명 된 hello 새 이벤트 원본을 탭의 각 속성 설정을 입력할 때 수동으로:</span><span class="sxs-lookup"><span data-stu-id="035a0-136">hello following table explains each property in hello New Event Source tab with its description when entering settings manually:</span></span>

| <span data-ttu-id="035a0-137">속성 이름</span><span class="sxs-lookup"><span data-stu-id="035a0-137">PROPERTY NAME</span></span> | <span data-ttu-id="035a0-138">설명</span><span class="sxs-lookup"><span data-stu-id="035a0-138">DESCRIPTION</span></span> |
| --- | --- |
| <span data-ttu-id="035a0-139">이벤트 원본 이름</span><span class="sxs-lookup"><span data-stu-id="035a0-139">Event source name</span></span> | <span data-ttu-id="035a0-140">이벤트 소스의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-140">hello name of your event source.</span></span> <span data-ttu-id="035a0-141">이 이름은 Time Series Insights 환경 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-141">This name must be unique within your Time Series Insights environment.</span></span>
| <span data-ttu-id="035a0-142">원본</span><span class="sxs-lookup"><span data-stu-id="035a0-142">Source</span></span> | <span data-ttu-id="035a0-143">선택 **IoT Hub** toocreate IoT 허브 이벤트 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-143">Choose **IoT Hub** toocreate an IoT Hub event source.</span></span>
| <span data-ttu-id="035a0-144">구독 ID</span><span class="sxs-lookup"><span data-stu-id="035a0-144">Subscription Id</span></span> | <span data-ttu-id="035a0-145">이 IoT 허브를 만든 hello 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-145">hello subscription in which this IoT hub was created.</span></span>
| <span data-ttu-id="035a0-146">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="035a0-146">Resource group</span></span> | <span data-ttu-id="035a0-147">이 IoT 허브를 만든 hello 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-147">hello subscription in which this IoT hub was created.</span></span>
| <span data-ttu-id="035a0-148">IoT Hub 이름</span><span class="sxs-lookup"><span data-stu-id="035a0-148">IoT hub name</span></span> | <span data-ttu-id="035a0-149">IoT Hub의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-149">hello name of your IoT Hub.</span></span> <span data-ttu-id="035a0-150">IoT Hub를 만들 때 사용자가 지은 특정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-150">When you created your IoT hub, you also gave it a specific name</span></span>
| <span data-ttu-id="035a0-151">IoT Hub 정책 이름</span><span class="sxs-lookup"><span data-stu-id="035a0-151">IoT hub policy name</span></span> | <span data-ttu-id="035a0-152">hello 공유 액세스 정책 hello IoT Hub 설정 탭에서 만들 수 있습니다. 각 공유 액세스 정책에는 이름, 사용자가 설정한 사용 권한 및 액세스 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-152">hello shared access policy, which can be created on hello IoT Hub settings tab. Each shared access policy has a name, permissions that you set, and access keys.</span></span> <span data-ttu-id="035a0-153">hello 공유 액세스 정책 이벤트 소스에 대 한 *해야* 가 **서비스 연결** 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="035a0-153">hello shared access policy for your event source *must* have **service connect** permissions.</span></span>
| <span data-ttu-id="035a0-154">IoT Hub 정책 키</span><span class="sxs-lookup"><span data-stu-id="035a0-154">IoT hub policy key</span></span> | <span data-ttu-id="035a0-155">hello 공유 액세스 키 tooauthenticate 액세스 toohello 서비스 버스 네임 스페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-155">hello Shared Access key used tooauthenticate access toohello Service Bus namespace.</span></span> <span data-ttu-id="035a0-156">Hello 기본 여기 또는 보조 키를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-156">Type hello primary or secondary key here.</span></span>
| <span data-ttu-id="035a0-157">IoT Hub 소비자 그룹</span><span class="sxs-lookup"><span data-stu-id="035a0-157">IoT hub consumer group</span></span> | <span data-ttu-id="035a0-158">hello 소비자 그룹 tooread hello IoT 허브에서에서 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-158">hello Consumer Group tooread events from hello IoT Hub.</span></span> <span data-ttu-id="035a0-159">이 뛰어납니다 toouse 이벤트 소스에 대 한 전용된 소비자 그룹을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="035a0-159">It is highly recommended toouse a dedicated consumer group for your event source.</span></span>

## <a name="next-steps"></a><span data-ttu-id="035a0-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="035a0-160">Next steps</span></span>

1. <span data-ttu-id="035a0-161">추가 데이터 액세스 정책 tooyour 환경 [정의 데이터 액세스 정책](time-series-insights-data-access.md)</span><span class="sxs-lookup"><span data-stu-id="035a0-161">Add a data access policy tooyour environment [Define data access policies](time-series-insights-data-access.md)</span></span>
1. <span data-ttu-id="035a0-162">사용자 환경에서 hello 액세스 [시간 계열 Insights 포털](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="035a0-162">Access your environment in hello [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>

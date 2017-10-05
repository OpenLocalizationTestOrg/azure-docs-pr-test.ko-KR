---
title: "작업 그룹에서 SMS 경고 동작 | Microsoft Docs"
description: "SMS 메시지 형식 및 SMS 메시지에 대한 응답으로 구독 취소, 재구독 또는 도움을 요청합니다."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 3e4eca174209eeb9cbce1d45111d1e5cc30af8b0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a><span data-ttu-id="d1274-103">작업 그룹에서 SMS 경고 동작</span><span class="sxs-lookup"><span data-stu-id="d1274-103">SMS Alert Behavior in Action Groups</span></span>
## <a name="overview"></a><span data-ttu-id="d1274-104">개요</span><span class="sxs-lookup"><span data-stu-id="d1274-104">Overview</span></span> ##
<span data-ttu-id="d1274-105">작업 그룹을 사용하여 수신자 목록을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-105">Action groups enable you to configure a list of receivers.</span></span> <span data-ttu-id="d1274-106">그런 후 활동 로그 경고를 정의할 때 이러한 그룹을 사용할 수 있습니다. 예를 들어 활동 로그 경고가 트리거될 때 특정 작업 그룹이 알림을 받도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-106">These groups can then be leveraged when defining activity log alerts; ensuring that a particular action group is notified when the activity log alert is triggered.</span></span> <span data-ttu-id="d1274-107">지원되는 경고 메커니즘 중 하나가 SMS인 경우 경고에서 양방향 통신을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-107">One of the alerting mechanisms supported is SMS; the alerts support bi-directional communication.</span></span> <span data-ttu-id="d1274-108">사용자는 다음과 같이 경고에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-108">A user can respond to an alert to:</span></span>

- <span data-ttu-id="d1274-109">**경고에서 구독 취소:** 사용자는 모든 작업 그룹 또는 단일 작업 그룹에 대한 모든 SMS 경고에서 구독을 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-109">**Unsubscribe from alerts:** A user can unsubscribe from all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="d1274-110">**경고 재구독:** 사용자는 모든 작업 그룹 또는 단일 작업 그룹에 대한 모든 SMS 경고를 재구독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-110">**Resubscribe to alerts:** A user can resubscribe to all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="d1274-111">**도움 요청:** 사용자는 SMS에 대한 자세한 정보를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-111">**Request help:** A user can ask for more information on the SMS.</span></span> <span data-ttu-id="d1274-112">사용자는 이 문서로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-112">They will be redirected to this article</span></span>

<span data-ttu-id="d1274-113">이 문서에서는 SMS 경고 동작과 사용자가 사용자의 로캘을 기반으로 취할 수 있는 응답 작업에 대해 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-113">This article covers the behavior of the SMS alerts and the response actions the user can take based on the locale of the user:</span></span>

## <a name="usacanada-sms-behavior"></a><span data-ttu-id="d1274-114">미국/캐나다 SMS 동작</span><span class="sxs-lookup"><span data-stu-id="d1274-114">USA/Canada SMS behavior</span></span>
### <a name="receiving-an-sms-alert"></a><span data-ttu-id="d1274-115">SMS 경고 받기</span><span class="sxs-lookup"><span data-stu-id="d1274-115">Receiving an SMS Alert</span></span>
<span data-ttu-id="d1274-116">작업 그룹의 일부로 구성된 SMS 수신자는 경고가 발생할 때 SMS를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-116">An SMS receiver, who is configured as part of an action group, will receive an SMS when an alert fires.</span></span> <span data-ttu-id="d1274-117">SMS는 다음의 정보를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-117">The SMS will carry the following information:</span></span>
* <span data-ttu-id="d1274-118">이 경고가 전달된 작업 그룹의 짧은 이름</span><span class="sxs-lookup"><span data-stu-id="d1274-118">Shortname of the action group this alert was sent to</span></span>
- <span data-ttu-id="d1274-119">경고 제목</span><span class="sxs-lookup"><span data-stu-id="d1274-119">Title of the alert</span></span>

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a><span data-ttu-id="d1274-120">한 작업 그룹에 대한 SMS 경고에서 구독 취소</span><span class="sxs-lookup"><span data-stu-id="d1274-120">Unsubscribing from SMS alerts for one action group</span></span>
<span data-ttu-id="d1274-121">사용자는 “DISABLE &lt;작업 그룹의 짧은 이름&gt;” 키워드로 짧은 코드 20873에 응답하여 한 작업 그룹의 경고에 대한 SMS에서 구독 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-121">A user can unsubscribe from SMS for alerts for one action group by responding to the shortcode 20873 with the keywords: “DISABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="d1274-122">예:</span><span class="sxs-lookup"><span data-stu-id="d1274-122">Ex.</span></span> <span data-ttu-id="d1274-123">짧은 이름이 “Azure”인 작업 그룹에 대한 경고를 구독 취소하려는 사용자는 “DISABLE Azure”라고 표시된 짧은 코드 20873에 SMS를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-123">A user wishing to unsubscribe from alerts for an action group with the shortname “Azure”, would send an SMS to the shortcode 20873 that says “DISABLE Azure”</span></span>

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a><span data-ttu-id="d1274-124">모든 작업 그룹에 대한 SMS 경고에서 구독 취소</span><span class="sxs-lookup"><span data-stu-id="d1274-124">Unsubscribing from SMS alerts for all action groups</span></span>
<span data-ttu-id="d1274-125">사용자는 다음 키워드로 짧은 코드 20873에 응답하여 모든 작업 그룹에 대한 모든 SMS 경고에서 구독 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-125">A user can unsubscribe from all SMS alerts for all action groups by responding to the shortcode 20873 with any of the following keywords:</span></span>
* <span data-ttu-id="d1274-126">STOP</span><span class="sxs-lookup"><span data-stu-id="d1274-126">STOP</span></span>

<span data-ttu-id="d1274-127">예:</span><span class="sxs-lookup"><span data-stu-id="d1274-127">Ex.</span></span> <span data-ttu-id="d1274-128">모든 작업 그룹에 대한 모든 SMS 경고를 구독 취소하려는 사용자는 “STOP”이라고 표시된 짧은 코드 20873에 SMS를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-128">A user wishing to unsubscribe from all SMS alerts for all action groups, would send an SMS to the shortcode 20873 that says “STOP”</span></span>

>[!NOTE]
><span data-ttu-id="d1274-129">사용자가 SMS 경고를 구독 취소했지만 새 작업 그룹에 추가된 경우 새 작업 그룹에 대한 SMS 경고를 받게 되지만 이전의 모든 작업 그룹에서 구독 취소 상태로 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-129">If a user has unsubscribed from SMS alerts, but is then added to a new action group; they WILL receive SMS alerts for that new action group, but remain unsubscribed from all previous action groups.</span></span>
>
>

### <a name="resubscribing-to-sms-alerts-for-one-action-group"></a><span data-ttu-id="d1274-130">한 작업 그룹에 대한 SMS 경고 재구독</span><span class="sxs-lookup"><span data-stu-id="d1274-130">Resubscribing to SMS alerts for one action group</span></span>
<span data-ttu-id="d1274-131">사용자는 “ENABLE &lt;작업 그룹의 짧은 이름&gt;” 키워드로 짧은 코드 20873에 응답하여 한 작업 그룹의 경고에 대한 SMS를 재구독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-131">A user can resubscribe to SMS for alerts for one action group by responding to the shortcode 20873 with the keywords: “ENABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="d1274-132">예:</span><span class="sxs-lookup"><span data-stu-id="d1274-132">Ex.</span></span> <span data-ttu-id="d1274-133">짧은 이름이 “Azure”인 작업 그룹에 대한 경고를 재구독하려는 사용자는 “ENABLE Azure”라고 표시된 짧은 코드 20873에 SMS를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-133">A user wishing to resubscribe to alerts for an action group with the shortname “Azure”, would send an SMS to the shortcode 20873 that says “ENABLE Azure”</span></span>

### <a name="resubscribing-to-sms-alerts-for-all-action-groups"></a><span data-ttu-id="d1274-134">모든 작업 그룹에 대한 SMS 경고 재구독</span><span class="sxs-lookup"><span data-stu-id="d1274-134">Resubscribing to SMS alerts for all action groups</span></span>
<span data-ttu-id="d1274-135">사용자는 다음 키워드로 짧은 코드 20873에 응답하여 모든 작업 그룹에 대한 모든 SMS 경고를 재구독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-135">A user can resubscribe to all SMS for alerts for all action groups by responding to the shortcode 20873 with any of the following keywords:</span></span>

* <span data-ttu-id="d1274-136">START</span><span class="sxs-lookup"><span data-stu-id="d1274-136">START</span></span>

<span data-ttu-id="d1274-137">예:</span><span class="sxs-lookup"><span data-stu-id="d1274-137">Ex.</span></span> <span data-ttu-id="d1274-138">모든 작업 그룹에 대한 모든 SMS 경고를 구독 취소하려는 사용자는 “START”라고 표시된 짧은 코드 20873에 SMS를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-138">A user wishing to unsubscribe from all SMS alerts for all action groups, would send an SMS to the shortcode 20873 that says “START”</span></span>

### <a name="requesting-help-via-sms"></a><span data-ttu-id="d1274-139">SMS를 통해 도움 요청</span><span class="sxs-lookup"><span data-stu-id="d1274-139">Requesting help via SMS</span></span>
<span data-ttu-id="d1274-140">사용자는 다음 키워드로 짧은 코드 20873에 응답하여 수신한 SMS에 대한 자세한 정보를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-140">A user can ask for more information about the SMS they have received by responding to the shortcode 20873 with any of the following keywords:</span></span>
* <span data-ttu-id="d1274-141">HELP</span><span class="sxs-lookup"><span data-stu-id="d1274-141">HELP</span></span>

<span data-ttu-id="d1274-142">응답은 이 문서에 대한 링크와 함께 사용자에게 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1274-142">A response will be sent to the user with a link to this article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1274-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d1274-143">Next Steps</span></span>
<span data-ttu-id="d1274-144">[활동 로그 경고의 개요](monitoring-overview-alerts.md)를 확인하고 알림을 받는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="d1274-144">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how to get alerted</span></span>  
<span data-ttu-id="d1274-145">[SMS 속도 제한](monitoring-alerts-rate-limiting.md)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="d1274-145">Learn more about [SMS rate limiting](monitoring-alerts-rate-limiting.md)</span></span>  
<span data-ttu-id="d1274-146">[작업 그룹](monitoring-action-groups.md)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="d1274-146">Learn more about [action groups](monitoring-action-groups.md)</span></span>

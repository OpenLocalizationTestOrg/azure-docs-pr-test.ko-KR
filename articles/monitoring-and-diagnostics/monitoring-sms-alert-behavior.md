---
title: "작업 그룹의 경고 동작 aaaSMS | Microsoft Docs"
description: "SMS 메시지 형식 및 응답 tooSMS 메시지 toounsubscribe 예외: %2 또는 도움을 요청 합니다."
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
ms.openlocfilehash: 3cd09b1903e3472f6402f62b74409d97e7e7ea97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a><span data-ttu-id="5ef78-103">작업 그룹에서 SMS 경고 동작</span><span class="sxs-lookup"><span data-stu-id="5ef78-103">SMS Alert Behavior in Action Groups</span></span>
## <a name="overview"></a><span data-ttu-id="5ef78-104">개요</span><span class="sxs-lookup"><span data-stu-id="5ef78-104">Overview</span></span> ##
<span data-ttu-id="5ef78-105">작업 그룹을 사용 하면 tooconfigure 수신자의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef78-105">Action groups enable you tooconfigure a list of receivers.</span></span> <span data-ttu-id="5ef78-106">활동 로그 경고; 정의할 때 이러한 그룹을 활용 다음 있습니다. hello 활동 로그 경고가 트리거될 때 특정 작업 그룹에 알림을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef78-106">These groups can then be leveraged when defining activity log alerts; ensuring that a particular action group is notified when hello activity log alert is triggered.</span></span> <span data-ttu-id="5ef78-107">SMS; hello 메커니즘이 지원 경고 중 하나는 hello 경고 양방향 통신을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef78-107">One of hello alerting mechanisms supported is SMS; hello alerts support bi-directional communication.</span></span> <span data-ttu-id="5ef78-108">사용자는 tooan 경고에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef78-108">A user can respond tooan alert to:</span></span>

- <span data-ttu-id="5ef78-109">**경고에서 구독 취소:** 사용자는 모든 작업 그룹 또는 단일 작업 그룹에 대한 모든 SMS 경고에서 구독을 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef78-109">**Unsubscribe from alerts:** A user can unsubscribe from all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="5ef78-110">**Tooalerts 예외: %2:** 사용자는 모든 작업 그룹 또는 단 수 동작 그룹에 대 한 tooall SMS 알림을 예외: %2 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef78-110">**Resubscribe tooalerts:** A user can resubscribe tooall SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="5ef78-111">**도움을 요청:** SMS hello에 대 한 자세한 내용은 사용자 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef78-111">**Request help:** A user can ask for more information on hello SMS.</span></span> <span data-ttu-id="5ef78-112">리디렉션된 toothis 문서 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef78-112">They will be redirected toothis article</span></span>

<span data-ttu-id="5ef78-113">이 문서에서는 hello SMS 알림 hello 동작에 설명 하 고 hello 응답 동작 hello 사용자 수에 따라 수행할 hello 사용자의 로캘 hello:</span><span class="sxs-lookup"><span data-stu-id="5ef78-113">This article covers hello behavior of hello SMS alerts and hello response actions hello user can take based on hello locale of hello user:</span></span>

## <a name="usacanada-sms-behavior"></a><span data-ttu-id="5ef78-114">미국/캐나다 SMS 동작</span><span class="sxs-lookup"><span data-stu-id="5ef78-114">USA/Canada SMS behavior</span></span>
### <a name="receiving-an-sms-alert"></a><span data-ttu-id="5ef78-115">SMS 경고 받기</span><span class="sxs-lookup"><span data-stu-id="5ef78-115">Receiving an SMS Alert</span></span>
<span data-ttu-id="5ef78-116">작업 그룹의 일부로 구성된 SMS 수신자는 경고가 발생할 때 SMS를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef78-116">An SMS receiver, who is configured as part of an action group, will receive an SMS when an alert fires.</span></span> <span data-ttu-id="5ef78-117">SMS hello 운반 hello 다음 정보:</span><span class="sxs-lookup"><span data-stu-id="5ef78-117">hello SMS will carry hello following information:</span></span>
* <span data-ttu-id="5ef78-118">이 경고를 보낼 된 hello 동작 그룹의 짧은 이름</span><span class="sxs-lookup"><span data-stu-id="5ef78-118">Shortname of hello action group this alert was sent to</span></span>
- <span data-ttu-id="5ef78-119">Hello 경고의 제목</span><span class="sxs-lookup"><span data-stu-id="5ef78-119">Title of hello alert</span></span>

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a><span data-ttu-id="5ef78-120">한 작업 그룹에 대한 SMS 경고에서 구독 취소</span><span class="sxs-lookup"><span data-stu-id="5ef78-120">Unsubscribing from SMS alerts for one action group</span></span>
<span data-ttu-id="5ef78-121">사용자 구독을 취소할 수 SMS에서 하나의 작업 그룹에 대 한 경고에 대 한 hello 키워드와 함께 응답 toohello shortcode 20873 여: "사용 안 함 &lt;동작 그룹의 짧은 이름을&gt;"입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef78-121">A user can unsubscribe from SMS for alerts for one action group by responding toohello shortcode 20873 with hello keywords: “DISABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="5ef78-122">예:</span><span class="sxs-lookup"><span data-stu-id="5ef78-122">Ex.</span></span> <span data-ttu-id="5ef78-123">"사용 안 함 Azure" 라고 표시 하는 SMS toohello shortcode 20873을 보내는 것과 사용자 toounsubscribe hello shortname "Azure"를 사용 하는 작업 그룹에 대 한 경고를 브로드캐스팅합니다..</span><span class="sxs-lookup"><span data-stu-id="5ef78-123">A user wishing toounsubscribe from alerts for an action group with hello shortname “Azure”, would send an SMS toohello shortcode 20873 that says “DISABLE Azure”</span></span>

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a><span data-ttu-id="5ef78-124">모든 작업 그룹에 대한 SMS 경고에서 구독 취소</span><span class="sxs-lookup"><span data-stu-id="5ef78-124">Unsubscribing from SMS alerts for all action groups</span></span>
<span data-ttu-id="5ef78-125">사용자는 모든 작업 그룹에 대 한 모든 SMS 경고에서 hello 키워드 다음의 응답 toohello shortcode 20873 준수 하 여 지 수신을 해지할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="5ef78-125">A user can unsubscribe from all SMS alerts for all action groups by responding toohello shortcode 20873 with any of hello following keywords:</span></span>
* <span data-ttu-id="5ef78-126">STOP</span><span class="sxs-lookup"><span data-stu-id="5ef78-126">STOP</span></span>

<span data-ttu-id="5ef78-127">예:</span><span class="sxs-lookup"><span data-stu-id="5ef78-127">Ex.</span></span> <span data-ttu-id="5ef78-128">사용자에 모든 작업 그룹에 대 한 모든 SMS 경고에서 toounsubscribe 브로드캐스팅하려면 "중지" 라고 표시 하는 SMS toohello shortcode 20873 보내는 것과</span><span class="sxs-lookup"><span data-stu-id="5ef78-128">A user wishing toounsubscribe from all SMS alerts for all action groups, would send an SMS toohello shortcode 20873 that says “STOP”</span></span>

>[!NOTE]
><span data-ttu-id="5ef78-129">SMS 경고, 하지만 그런 다음 새 작업 그룹 tooa; 추가에서 사용자가 구독 취소 하는 경우 해당 새 작업 그룹에 대 한 SMS 알림을 받지 않지만 모든 이전 작업 그룹 등록을 취소할 상태를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef78-129">If a user has unsubscribed from SMS alerts, but is then added tooa new action group; they WILL receive SMS alerts for that new action group, but remain unsubscribed from all previous action groups.</span></span>
>
>

### <a name="resubscribing-toosms-alerts-for-one-action-group"></a><span data-ttu-id="5ef78-130">한 작업 그룹에 대 한 resubscribing tooSMS 경고</span><span class="sxs-lookup"><span data-stu-id="5ef78-130">Resubscribing tooSMS alerts for one action group</span></span>
<span data-ttu-id="5ef78-131">사용자 수 예외: %2 tooSMS 동작은 두 개 그룹에 대 한 경고에 대 한 hello 키워드와 함께 응답 toohello shortcode 20873 여: "사용 &lt;동작 그룹의 짧은 이름을&gt;"입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef78-131">A user can resubscribe tooSMS for alerts for one action group by responding toohello shortcode 20873 with hello keywords: “ENABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="5ef78-132">예:</span><span class="sxs-lookup"><span data-stu-id="5ef78-132">Ex.</span></span> <span data-ttu-id="5ef78-133">사용자 hello shortname "Azure"를 사용 하는 작업 그룹에 대 한 tooresubscribe tooalerts 브로드캐스팅하려면 "를 사용 하도록 설정 하는 Azure" 라고 표시 하는 SMS toohello shortcode 20873 보내는 것과</span><span class="sxs-lookup"><span data-stu-id="5ef78-133">A user wishing tooresubscribe tooalerts for an action group with hello shortname “Azure”, would send an SMS toohello shortcode 20873 that says “ENABLE Azure”</span></span>

### <a name="resubscribing-toosms-alerts-for-all-action-groups"></a><span data-ttu-id="5ef78-134">모든 작업 그룹에 대 한 resubscribing tooSMS 경고</span><span class="sxs-lookup"><span data-stu-id="5ef78-134">Resubscribing tooSMS alerts for all action groups</span></span>
<span data-ttu-id="5ef78-135">사용자는 hello 키워드 다음의 응답 toohello shortcode 20873 준수 하 여 모든 작업 그룹에 대 한 경고에 대 한 SMS tooall 다시 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="5ef78-135">A user can resubscribe tooall SMS for alerts for all action groups by responding toohello shortcode 20873 with any of hello following keywords:</span></span>

* <span data-ttu-id="5ef78-136">START</span><span class="sxs-lookup"><span data-stu-id="5ef78-136">START</span></span>

<span data-ttu-id="5ef78-137">예:</span><span class="sxs-lookup"><span data-stu-id="5ef78-137">Ex.</span></span> <span data-ttu-id="5ef78-138">모든 작업 그룹에 대 한 모든 SMS 경고에서 toounsubscribe 하려는 사용자는 "시작" 라고 표시 하는 SMS toohello shortcode 20873 보내는 것과</span><span class="sxs-lookup"><span data-stu-id="5ef78-138">A user wishing toounsubscribe from all SMS alerts for all action groups, would send an SMS toohello shortcode 20873 that says “START”</span></span>

### <a name="requesting-help-via-sms"></a><span data-ttu-id="5ef78-139">SMS를 통해 도움 요청</span><span class="sxs-lookup"><span data-stu-id="5ef78-139">Requesting help via SMS</span></span>
<span data-ttu-id="5ef78-140">사용자는 키워드 다음 hello를 사용 하 여 응답 toohello shortcode 20873에서 받은 SMS hello에 대 한 자세한 내용은 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef78-140">A user can ask for more information about hello SMS they have received by responding toohello shortcode 20873 with any of hello following keywords:</span></span>
* <span data-ttu-id="5ef78-141">HELP</span><span class="sxs-lookup"><span data-stu-id="5ef78-141">HELP</span></span>

<span data-ttu-id="5ef78-142">응답은 toohello 사용자 링크 toothis 기사와 함께 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef78-142">A response will be sent toohello user with a link toothis article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ef78-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ef78-143">Next Steps</span></span>
<span data-ttu-id="5ef78-144">가져오기는 [활동 로그 경고의 개요](monitoring-overview-alerts.md) tooget 경고가 표시 하는 방법을 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="5ef78-144">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how tooget alerted</span></span>  
<span data-ttu-id="5ef78-145">[SMS 속도 제한](monitoring-alerts-rate-limiting.md)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="5ef78-145">Learn more about [SMS rate limiting](monitoring-alerts-rate-limiting.md)</span></span>  
<span data-ttu-id="5ef78-146">[작업 그룹](monitoring-action-groups.md)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="5ef78-146">Learn more about [action groups](monitoring-action-groups.md)</span></span>

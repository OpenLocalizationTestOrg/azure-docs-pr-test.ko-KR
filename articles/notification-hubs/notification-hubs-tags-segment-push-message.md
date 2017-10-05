---
title: "라우팅 및 태그 식"
description: "이 문서는 Azure 알림 허브에 대한 알림 및 태그 식을 설명합니다."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: 0fffb3bb-8ed8-4e0f-89e8-0de24a47f644
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 18faa88641623e1248d6a33bc2d87099e1c9f624
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="routing-and-tag-expressions"></a><span data-ttu-id="cfd84-103">라우팅 및 태그 식</span><span class="sxs-lookup"><span data-stu-id="cfd84-103">Routing and tag expressions</span></span>
## <a name="overview"></a><span data-ttu-id="cfd84-104">개요</span><span class="sxs-lookup"><span data-stu-id="cfd84-104">Overview</span></span>
<span data-ttu-id="cfd84-105">태그 식을 사용하면 알림 허브를 통해 푸시 알림을 보내는 경우에 특정한 장치 집합, 보다 구체적으로는 등록을 대상으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-105">Tag expressions enable you to target specific sets of devices, or more specifically registrations, when sending a push notification through Notification Hubs.</span></span>

## <a name="targeting-specific-registrations"></a><span data-ttu-id="cfd84-106">특정 등록을 대상으로 지정</span><span class="sxs-lookup"><span data-stu-id="cfd84-106">Targeting specific registrations</span></span>
<span data-ttu-id="cfd84-107">특정한 알림 등록을 대상으로 지정하는 유일한 방법은 등록에 태그를 연결한 후에 해당 태그를 대상으로 지정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-107">The only way to target specific notification registrations is to associate tags with them, then target those tags.</span></span> <span data-ttu-id="cfd84-108">[등록 관리](notification-hubs-push-notification-registration-management.md)의 설명처럼, 푸시 알림을 받으려면 앱은 장치 핸들을 알림 허브에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-108">As discussed in [Registration Management](notification-hubs-push-notification-registration-management.md), in order to receive push notifications an app has to register a device handle on a notification hub.</span></span> <span data-ttu-id="cfd84-109">알림 허브에 등록이 생성되면, 응용 프로그램 백 엔드는 등록에 푸시 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-109">Once a registration is created on a notification hub, the application backend can send push notifications to it.</span></span>
<span data-ttu-id="cfd84-110">응용 프로그램 백 엔드는 다음과 같은 방식으로 등록이 특정 알림을 대상으로 지정하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-110">The application backend can choose the registrations to target with a specific notification in the following ways:</span></span>

1. <span data-ttu-id="cfd84-111">**브로드캐스트**: 알림 허브 내의 모든 등록이 알림을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-111">**Broadcast**: all registrations in the notification hub receive the notification.</span></span>
2. <span data-ttu-id="cfd84-112">**태그**: 지정된 태그를 포함하는 모든 등록이 알림을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-112">**Tag**: all registrations that contain the specified tag receive the notification.</span></span>
3. <span data-ttu-id="cfd84-113">**태그 식**: 등록의 태그 집합이 지정된 식과 일치하는 모든 등록이 알림을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-113">**Tag expression**: all registrations whose set of tags match the specified expression receive the notification.</span></span>

## <a name="tags"></a><span data-ttu-id="cfd84-114">태그들</span><span class="sxs-lookup"><span data-stu-id="cfd84-114">Tags</span></span>
<span data-ttu-id="cfd84-115">태그는 모든 문자열을 120 개까지 포함 된 영숫자 문자와 영숫자가 아닌 문자를 지정할 수: '_', ' @', '#', '. ',':', '-'.</span><span class="sxs-lookup"><span data-stu-id="cfd84-115">A tag can be any string, up to 120 characters, containing alphanumeric and the following non-alphanumeric characters: ‘_’, ‘@’, ‘#’, ‘.’, ‘:’, ‘-’.</span></span> <span data-ttu-id="cfd84-116">다음 예제는 특정 음악 그룹에 대한 토스트 알림을 받을 수 있는 응용 프로그램을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-116">The following example shows an application from which you can receive toast notifications about specific music groups.</span></span> <span data-ttu-id="cfd84-117">이 시나리오에서 알림을 라우팅하는 간단한 방법은 등록에 대해 아래 그림처럼 다양한 밴드를 나타내는 태그로 레이블을 붙이는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-117">In this scenario, a simple way to route notifications is to label registrations with tags that represent the different bands, as in the following picture.</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

<span data-ttu-id="cfd84-118">이 그림에서 **Beatles**라는 태그가 지정된 메시지는 **Beatles** 태그가 등록된 태블릿에만 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-118">In this picture, the message tagged **Beatles** reaches only the tablet that registered with the tag **Beatles**.</span></span>

<span data-ttu-id="cfd84-119">태그에 대한 등록을 생성하는 내용은 [등록 관리](notification-hubs-push-notification-registration-management.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfd84-119">For more information about creating registrations for tags, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

<span data-ttu-id="cfd84-120">[Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK에 포함된 `Microsoft.Azure.NotificationHubs.NotificationHubClient` 클래스의 알림 메서드를 사용하여 태그에 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-120">You can send notifications to tags using the send notifications methods of the `Microsoft.Azure.NotificationHubs.NotificationHubClient` class in the [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span></span> <span data-ttu-id="cfd84-121">Node.js 또는 푸시 알림 REST API를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-121">You can also use Node.js, or the Push Notifications REST APIs.</span></span>  <span data-ttu-id="cfd84-122">다음은 SDK 사용 예입니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-122">Here's an example using the SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




<span data-ttu-id="cfd84-123">태그를 미리 프로비전하지 않아도 되며 특정 앱과 관련된 다양한 개념을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-123">Tags do not have to be pre-provisioned and can refer to multiple app-specific concepts.</span></span> <span data-ttu-id="cfd84-124">예를 들어, 이 예제 응용 프로그램 사용자는 밴드에 대한 댓글을 추가할 수 있고 자신이 좋아하는 밴드에 대한 댓글뿐만 아니라 친구가 추가하는(어떤 밴드에 관한 댓글이든 상관없이) 댓글에 대해서도 토스트를 수신하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-124">For example, users of this example application can comment on bands and want to receive toasts, not only for the comments on their favorite bands, but also for all comments from their friends, regardless of the band on which they are commenting.</span></span> <span data-ttu-id="cfd84-125">다음 그림은 이러한 시나리오의 예를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-125">The following picture shows an example of this scenario:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

<span data-ttu-id="cfd84-126">이 그림에서 Alice는 Beatles에 대한 최신 소식에 흥미가 있고, Bob은 Wailers에 대한 최신 소식에 흥미가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-126">In this picture, Alice is interested in updates for the Beatles, and Bob is interested in updates for the Wailers.</span></span> <span data-ttu-id="cfd84-127">Bob은 Charlie의 댓글에도 흥미가 있으며, Charlie는 Wailers에 흥미가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-127">Bob is also interested in Charlie’s comments, and Charlie is in interested in the Wailers.</span></span> <span data-ttu-id="cfd84-128">Beatles에 대한 Charlie의 댓글에 대해 알림이 전송되면 Alice와 Bob이 알림을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-128">When a notification is sent for Charlie’s comment on the Beatles, both Alice and Bob receive it.</span></span>

<span data-ttu-id="cfd84-129">다양한 관심사(예: “band_Beatles” 또는 “follows_Charlie”)를 태그로 인코딩할 수 있는 반면에, 태그는 값이 있는 속성이 아니라 간단한 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-129">While you can encode multiple concerns in tags (for example, “band_Beatles” or “follows_Charlie”), tags are simple strings and not properties with values.</span></span> <span data-ttu-id="cfd84-130">등록은 특정 태그의 존재 또는 부재와만 일치 여부가 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-130">A registration is matched only on the presence or absence of a specific tag.</span></span>

<span data-ttu-id="cfd84-131">태그를 사용하여 흥미가 있는 그룹에 알림을 보내는 방법에 대한 단계별 전체 자습서는 [속보](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfd84-131">For a full step-by-step tutorial on how to use tags for sending to interest groups, see [Breaking News](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span></span>

## <a name="using-tags-to-target-users"></a><span data-ttu-id="cfd84-132">태그를 사용하여 사용자를 대상으로 지정하기</span><span class="sxs-lookup"><span data-stu-id="cfd84-132">Using tags to target users</span></span>
<span data-ttu-id="cfd84-133">태그를 사용하는 또 다른 방법은 특정 사용자의 모든 장치를 식별하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-133">Another way to use tags is to identify all the devices of a particular user.</span></span> <span data-ttu-id="cfd84-134">등록에 대해 다음 그림과 같이 사용자 ID를 포함하는 태그를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-134">Registrations can be tagged with a tag that contains a user id, as in the following picture:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

<span data-ttu-id="cfd84-135">이 그림에서 uid:Alice 태그가 적용된 메시지는 uid:Alice 태그가 적용된 모든 등록에 전송되므로 Alice의 모든 장치에도 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-135">In this picture, the message tagged uid:Alice reaches all registrations tagged uid:Alice; hence, all of Alice’s devices.</span></span>

## <a name="tag-expressions"></a><span data-ttu-id="cfd84-136">태그 식</span><span class="sxs-lookup"><span data-stu-id="cfd84-136">Tag expressions</span></span>
<span data-ttu-id="cfd84-137">알림이 단일 태그가 아니라 태그에 대한 부울 식으로 식별되는 등록 집합을 대상으로 지정해야 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-137">There are cases in which a notification has to target a set of registrations that is identified not by a single tag, but by a Boolean expression on tags.</span></span>

<span data-ttu-id="cfd84-138">보스턴에 있는 모든 사람에게 Red Sox와 Cardinals의 경기에 대해 미리 알림을 보내는 스포츠 응용 프로그램을 생각해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-138">Consider a sports application that sends a reminder to everyone in Boston about a game between the Red Sox and Cardinals.</span></span> <span data-ttu-id="cfd84-139">클라이언트 앱이 팀과 지역 관심사에 대한 태그를 등록하면, 알림은 Red Sox 또는 Cardinals에 관심이 있는 보스턴의 모든 사람을 대상으로 하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-139">If the client app registers tags about interest in teams and location, then the notification should be targeted to everyone in Boston who is interested in either the Red Sox or the Cardinals.</span></span> <span data-ttu-id="cfd84-140">이 조건은 다음과 같은 부울 식으로 표현될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-140">This condition can be expressed with the following Boolean expression:</span></span>

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

<span data-ttu-id="cfd84-141">태그 식은 AND(&&), OR(||), NOT(!)과 같은 부울 연산자를 모두 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-141">Tag expressions can contain all Boolean operators, such as AND (&&), OR (||), and NOT (!).</span></span> <span data-ttu-id="cfd84-142">괄호를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-142">They can also contain parentheses.</span></span> <span data-ttu-id="cfd84-143">태그 식은 OR만 포함하는 경우에 태그가 20개로 제한됩니다. 그렇지 않으면 태그가 6개로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-143">Tag expressions are limited to 20 tags if they contain only ORs; otherwise they are limited to 6 tags.</span></span>

<span data-ttu-id="cfd84-144">다음은 SDK를 사용하여 태그 식으로 알림을 보내는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="cfd84-144">Here's an example for sending notifications with tag expressions using the SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    String userTag = "(location_Boston && !follows_Cardinals)";    

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You want info on the Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You want info on the Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

---
title: "aaaRouting 및 태그 식"
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
ms.openlocfilehash: c2c60500f7469f1cb1a73a5cf63c221a9ad6cbb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="routing-and-tag-expressions"></a>라우팅 및 태그 식
## <a name="overview"></a>개요
태그 식을 사용 하 여 장치 또는 보다 구체적으로 등록의 특정 집합 tootarget 알림 허브를 통해 푸시 알림을 보낼 때.

## <a name="targeting-specific-registrations"></a>특정 등록을 대상으로 지정
hello만 방법은 tootarget 특정 알림 등록은 tooassociate 태그를 다음 대상 해당 태그 합니다. 에 설명 된 대로 [등록 관리](notification-hubs-push-notification-registration-management.md), 순서 tooreceive 푸시에서 알림 허브에서 앱이 장치 tooregister 알림을 처리 합니다. 알림 허브에서 등록이 만들어지고 나면 hello 응용 프로그램 백 엔드에 푸시 알림을 tooit을 보낼 수 있습니다.
응용 프로그램 백 엔드 hello hello 같은 방법으로 다음에 특정 알림 사용 하 여 hello 등록 tootarget를 선택할 수 있습니다.:

1. **브로드캐스트**: hello 알림 허브의 모든 등록 hello 알림을 수신 합니다.
2. **태그**: 지정 된 hello를 포함 하는 모든 등록 태그 hello 알림을 수신 합니다.
3. **태그 식**: 일치 하는 태그 집합이 지정 된 식이 hello 모든 등록 hello 알림을 수신 합니다.

## <a name="tags"></a>태그들
태그를 포함 하는 too120 문자 모든 문자열 영숫자 수 있고 hello 영숫자가 아닌 문자: '_', ' @', '#', '. ',':', '-'. hello 다음 예제에서는 특정 밴드에 대 한 알림 메시지를 받을 수 있는 응용 프로그램 이 시나리오는 간단한 방법을 tooroute 알림 toolabel hello hello 다음 그림에서와 같이 각 브랜드를 나타내는 태그로 등록입니다.

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

이 그림에서 hello 태그가 지정 된 메시지 **Beatles** 도달만 hello 등록 된 태블릿 hello 태그 **Beatles**합니다.

태그에 대한 등록을 생성하는 내용은 [등록 관리](notification-hubs-push-notification-registration-management.md)를 참조하세요.

알림 tootags hello를 사용 하 여 보낼 hello의 알림 메서드를 보낼 수 있습니다 `Microsoft.Azure.NotificationHubs.NotificationHubClient` hello 클래스 [Microsoft Azure 알림 허브](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK입니다. Node.js를 사용 하거나 푸시 알림을 REST Api hello 수도 있습니다.  Hello SDK를 사용 하는 예제는 다음과 같습니다.

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




태그는 toobe 미리 프로 비전 하지 않은 toomultiple 앱 관련 개념을 참조할 수 있습니다. 예를 들어이 예제에서는 응용 프로그램의 사용자가 밴드에 대 한 의견을 좋아하는 밴드는에 대 한 hello 의견 뿐만 아니라 주석는 hello 밴드에 관계 없이 친구의 모든 메모 tooreceive 알림을 원하는 됩니다. hello 다음 그림에서는이 시나리오의 예를 보여 줍니다.

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

이 그림에서 Alice는 Beatles, hello에 대 한 업데이트 및 Bob은 Wailers hello에 대 한 업데이트 합니다. 또한 Bob은의 댓글에 및 charlie hello Wailers에 관심이 있습니다. Charlie의 댓글에 Beatles hello에 대 한 알림을 보내면 Alice와 Bob 받을 것입니다.

다양한 관심사(예: “band_Beatles” 또는 “follows_Charlie”)를 태그로 인코딩할 수 있는 반면에, 태그는 값이 있는 속성이 아니라 간단한 문자열입니다. 등록 하는 특정 태그의 hello 존재 여부에 대해서만 일치 됩니다.

Toouse toointerest 그룹 보내기 위한 태그를 삽입 방법에 대 한 전체 단계별 자습서를 참조 하십시오. [최신 뉴스](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md)합니다.

## <a name="using-tags-tootarget-users"></a>태그 tootarget 사용자가 사용 하 여
또 다른 방법은 toouse 태그 tooidentify 특정 사용자의 모든 hello 장치 됩니다. 등록은 hello 다음 그림에서와 같이 사용자 id를 포함 하는 태그가 태그로 지정 될 수 있습니다.

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

이 그림에서 hello 메시지에 태그가 uid: alice에 도달 하면 모든 등록 태그가 지정 된 uid: alice; 따라서 모든 Alice의 장치입니다.

## <a name="tag-expressions"></a>태그 식
알림을 tootarget 단일 태그가 아니라 있지만 태그의 부울 식으로 식별 되는 등록 집합 경우가 있습니다.

Hello Red Sox와 Cardinals 간의 시합이 대 한 미리 알림 tooeveryone boston에서 보내는 스포츠 응용 프로그램을 고려 합니다. 팀과 위치에 대 한 관심 태그를 등록 하는 hello 클라이언트 응용 프로그램, hello 알림을 boston 거주자를 hello Red Sox와 Cardinals hello 중 하나에 관심이 대상된 tooeveryone 여야 합니다. 이 문제는 다음 부울 식은 hello로 나타낼 수 있습니다.

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

태그 식은 AND(&&), OR(||), NOT(!)과 같은 부울 연산자를 모두 포함할 수 있습니다. 괄호를 포함할 수도 있습니다. 태그 식에는 Or;만 포함 하는 경우 제한 too20 태그 그렇지 않으면 서로 제한 too6 태그입니다.

Hello SDK를 사용 하 여 태그 식을 사용 하 여 알림을 보내는 경우에 예를 들면 다음과 같습니다.

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    String userTag = "(location_Boston && !follows_Cardinals)";    

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You want info on hello Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You want info on hello Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

---
title: "aaaHow toosend 예약 알림 | Microsoft Docs"
description: "이 항목에서는 Azure 알림 허브로 예약된 알림 사용에 대해 설명합니다."
services: notification-hubs
documentationcenter: .net
keywords: "푸시 알림, 푸시 알림, 푸시 알림 예약"
author: ysxu
manager: erikre
editor: 
ms.assetid: 6b718c75-75dd-4c99-aee3-db1288235c1a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 9b3ba715dad6f5d824a615e83f2863b0db47b533
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-send-scheduled-notifications"></a><span data-ttu-id="0ddb5-104">방법: 예약된 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="0ddb5-104">How To: Send scheduled notifications</span></span>
## <a name="overview"></a><span data-ttu-id="0ddb5-105">개요</span><span class="sxs-lookup"><span data-stu-id="0ddb5-105">Overview</span></span>
<span data-ttu-id="0ddb5-106">있는 경우 하는 시나리오는 특정 시점에서 hello 알림을 toosend 미래 원하는 프로그램 백 엔드 코드 toosend hello 통지를 쉽게 toowake 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0ddb5-106">If you have a scenario in which you want toosend a notification at some point in hello future, but do not have an easy way toowake up your back-end code toosend hello notification.</span></span> <span data-ttu-id="0ddb5-107">표준 알림 허브 계층 hello 향후의 too7 일자를 tooschedule 알림 수 있는 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ddb5-107">Standard tier Notification Hubs supports a feature that enables you tooschedule notifications up too7 days in hello future.</span></span>

<span data-ttu-id="0ddb5-108">알림을 보낼을 사용 하 여 hello [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) hello 다음 예제와 같이 hello 알림 허브 SDK 클래스:</span><span class="sxs-lookup"><span data-stu-id="0ddb5-108">When sending a notification, simply use hello [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) class in hello Notification Hubs SDK as shown in hello following example:</span></span>

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

<span data-ttu-id="0ddb5-109">또한 해당 notificationId를 사용하여 이전에 예약된 알림을 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ddb5-109">Also, you can cancel a previously scheduled notification using its notificationId:</span></span>

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

<span data-ttu-id="0ddb5-110">hello 보낼 수는 예약 된 알림 수에 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0ddb5-110">There are no limits on hello number of scheduled notifications you can send.</span></span>


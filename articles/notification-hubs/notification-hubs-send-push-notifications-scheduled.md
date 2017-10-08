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
# <a name="how-to-send-scheduled-notifications"></a>방법: 예약된 알림 보내기
## <a name="overview"></a>개요
있는 경우 하는 시나리오는 특정 시점에서 hello 알림을 toosend 미래 원하는 프로그램 백 엔드 코드 toosend hello 통지를 쉽게 toowake 필요가 없습니다. 표준 알림 허브 계층 hello 향후의 too7 일자를 tooschedule 알림 수 있는 기능을 지원 합니다.

알림을 보낼을 사용 하 여 hello [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) hello 다음 예제와 같이 hello 알림 허브 SDK 클래스:

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

또한 해당 notificationId를 사용하여 이전에 예약된 알림을 취소할 수 있습니다.

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

hello 보낼 수는 예약 된 알림 수에 제한이 없습니다.


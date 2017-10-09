---
title: "SMS, 메일 및 webhook에 대 한 제한 aaaRate | Microsoft Docs"
description: "Azure에서 작업 그룹에서 가능한 SMS, 전자 메일 또는 webhook 알림 hello 수를 제한 하는 방법을 이해 합니다."
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
ms.openlocfilehash: 1cd08a5b982c82bb02e0bf93451aa1fcd9bc34af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a>SMS 메시지, 전자 메일 및 웹후크 게시에 대한 속도 제한
속도 제한 알림이 너무 많습니다 tooa 특정 전화 번호나 전자 메일 주소를 보낼 때 발생 하는 알림의 일시 중단 됩니다. 속도를 제한하면 경고를 관리하고 실행할 수 있게 됩니다.

hello 규칙은 SMS 및 전자 메일에 대 한 hello 동일 합니다. hello 속도 제한 임계값은입니다.

 - **SMS**: 1시간에 10개 메시지
 - **전자 메일**: 1시간에 100개 메시지

## <a name="rate-limit-rules"></a>속도 제한 규칙
- 특정 전화 번호나 전자 메일에는 허용 되는 hello 임계값 보다 더 많은 메시지를 받을 때 제한 하는 속도입니다.
- 전화 번호 또는 전자 메일은 많은 구독에서 작업 그룹에 속할 수 있습니다. 속도 제한은 모든 구독에 걸쳐 적용됩니다. 여러 구독에서 메시지를 보내는 경우에 hello 임계값에 도달 하면 즉시 적용 합니다.  
- 전화 번호나 전자 메일 제한 속도, 추가 알림이 보내집니다 toocommunicate hello 속도 제한 합니다. hello 알림 때 hello 상태 속도 제한에 만료 됩니다.

## <a name="rate-limit-of-webhooks"></a>웹후크의 속도 제한 ##
현재 웹후크에 대한 속도 제한은 없습니다.

## <a name="next-steps"></a>다음 단계 ##
* [SMS 경고 동작](monitoring-sms-alert-behavior.md)에 대해 자세히 알아보세요.
* 가져오기는 [활동 로그 경고의 개요](monitoring-overview-alerts.md), 알아봅니다 어떻게 tooreceive 경고 합니다.  
* 너무 방법에 대해 알아봅니다[서비스 상태 알림 게시 될 때마다 경고를 구성](monitoring-activity-log-alerts-on-service-notifications.md)합니다.

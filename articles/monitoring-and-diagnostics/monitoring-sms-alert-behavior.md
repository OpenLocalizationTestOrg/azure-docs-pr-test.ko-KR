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
# <a name="sms-alert-behavior-in-action-groups"></a>작업 그룹에서 SMS 경고 동작
## <a name="overview"></a>개요 ##
작업 그룹을 사용 하면 tooconfigure 수신자의 목록입니다. 활동 로그 경고; 정의할 때 이러한 그룹을 활용 다음 있습니다. hello 활동 로그 경고가 트리거될 때 특정 작업 그룹에 알림을 확인 합니다. SMS; hello 메커니즘이 지원 경고 중 하나는 hello 경고 양방향 통신을 지원 합니다. 사용자는 tooan 경고에 응답할 수 있습니다.

- **경고에서 구독 취소:** 사용자는 모든 작업 그룹 또는 단일 작업 그룹에 대한 모든 SMS 경고에서 구독을 취소할 수 있습니다.  
- **Tooalerts 예외: %2:** 사용자는 모든 작업 그룹 또는 단 수 동작 그룹에 대 한 tooall SMS 알림을 예외: %2 수 있습니다.  
- **도움을 요청:** SMS hello에 대 한 자세한 내용은 사용자 요청할 수 있습니다. 리디렉션된 toothis 문서 됩니다.

이 문서에서는 hello SMS 알림 hello 동작에 설명 하 고 hello 응답 동작 hello 사용자 수에 따라 수행할 hello 사용자의 로캘 hello:

## <a name="usacanada-sms-behavior"></a>미국/캐나다 SMS 동작
### <a name="receiving-an-sms-alert"></a>SMS 경고 받기
작업 그룹의 일부로 구성된 SMS 수신자는 경고가 발생할 때 SMS를 수신합니다. SMS hello 운반 hello 다음 정보:
* 이 경고를 보낼 된 hello 동작 그룹의 짧은 이름
- Hello 경고의 제목

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a>한 작업 그룹에 대한 SMS 경고에서 구독 취소
사용자 구독을 취소할 수 SMS에서 하나의 작업 그룹에 대 한 경고에 대 한 hello 키워드와 함께 응답 toohello shortcode 20873 여: "사용 안 함 &lt;동작 그룹의 짧은 이름을&gt;"입니다.

예: "사용 안 함 Azure" 라고 표시 하는 SMS toohello shortcode 20873을 보내는 것과 사용자 toounsubscribe hello shortname "Azure"를 사용 하는 작업 그룹에 대 한 경고를 브로드캐스팅합니다..

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a>모든 작업 그룹에 대한 SMS 경고에서 구독 취소
사용자는 모든 작업 그룹에 대 한 모든 SMS 경고에서 hello 키워드 다음의 응답 toohello shortcode 20873 준수 하 여 지 수신을 해지할 수 있습니다.:
* STOP

예: 사용자에 모든 작업 그룹에 대 한 모든 SMS 경고에서 toounsubscribe 브로드캐스팅하려면 "중지" 라고 표시 하는 SMS toohello shortcode 20873 보내는 것과

>[!NOTE]
>SMS 경고, 하지만 그런 다음 새 작업 그룹 tooa; 추가에서 사용자가 구독 취소 하는 경우 해당 새 작업 그룹에 대 한 SMS 알림을 받지 않지만 모든 이전 작업 그룹 등록을 취소할 상태를 유지 합니다.
>
>

### <a name="resubscribing-toosms-alerts-for-one-action-group"></a>한 작업 그룹에 대 한 resubscribing tooSMS 경고
사용자 수 예외: %2 tooSMS 동작은 두 개 그룹에 대 한 경고에 대 한 hello 키워드와 함께 응답 toohello shortcode 20873 여: "사용 &lt;동작 그룹의 짧은 이름을&gt;"입니다.

예: 사용자 hello shortname "Azure"를 사용 하는 작업 그룹에 대 한 tooresubscribe tooalerts 브로드캐스팅하려면 "를 사용 하도록 설정 하는 Azure" 라고 표시 하는 SMS toohello shortcode 20873 보내는 것과

### <a name="resubscribing-toosms-alerts-for-all-action-groups"></a>모든 작업 그룹에 대 한 resubscribing tooSMS 경고
사용자는 hello 키워드 다음의 응답 toohello shortcode 20873 준수 하 여 모든 작업 그룹에 대 한 경고에 대 한 SMS tooall 다시 수 있습니다.:

* START

예: 모든 작업 그룹에 대 한 모든 SMS 경고에서 toounsubscribe 하려는 사용자는 "시작" 라고 표시 하는 SMS toohello shortcode 20873 보내는 것과

### <a name="requesting-help-via-sms"></a>SMS를 통해 도움 요청
사용자는 키워드 다음 hello를 사용 하 여 응답 toohello shortcode 20873에서 받은 SMS hello에 대 한 자세한 내용은 요청할 수 있습니다.
* HELP

응답은 toohello 사용자 링크 toothis 기사와 함께 전송 됩니다.

## <a name="next-steps"></a>다음 단계
가져오기는 [활동 로그 경고의 개요](monitoring-overview-alerts.md) tooget 경고가 표시 하는 방법을 알아봅니다  
[SMS 속도 제한](monitoring-alerts-rate-limiting.md)에 대해 자세히 알아보기  
[작업 그룹](monitoring-action-groups.md)에 대해 자세히 알아보기

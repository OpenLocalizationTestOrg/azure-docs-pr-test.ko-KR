---
title: "서비스 버스 진단 로그 aaaAzure | Microsoft Docs"
description: "자세한 방법을 tooset Azure에서 서비스 버스에 대 한 진단 로그를 합니다."
keywords: 
documentationcenter: .net
services: service-bus-messaging
author: banisadr
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: babanisa;sethm
ms.openlocfilehash: e48d6eaba6e865ae39f5b07ed6cd53d74c92e2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-diagnostic-logs"></a>Service Bus 진단 로그

Azure Service Bus에 대해 다음 두 가지 유형의 로그를 볼 수 있습니다.
* **[활동 로그](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**. 이러한 로그에는 작업에 대해 수행된 작업 관련 정보가 포함됩니다. hello 로그는 항상 활성화 합니다.
* **[진단 로그](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**. 작업에서 발생하는 모든 상황을 보다 잘 이해할 수 있도록 진단 로그를 구성할 수 있습니다. 진단은 hello ְ  업데이트 및 hello 작업이 실행 되는 동안 발생 하는 활동을 포함 하 여 hello 작업 삭제 될 때까지 hello 시간부터 커버 활동을 기록 합니다.

## <a name="turn-on-diagnostic-logs"></a>진단 로그 설정

진단 로그는 기본적으로 해제되어 있습니다. tooenable 진단 로그 hello 다음 단계를 수행 합니다.

1.  Hello에 [Azure 포털](https://portal.azure.com)아래 **모니터링 + 관리**, 클릭 **진단 로그**합니다.

    ![블레이드 탐색 toodiagnostic 로그](./media/service-bus-diagnostic-logs/image1.png)

2. Toomonitor hello 리소스를 클릭 합니다.  

3.  **진단 켜기**를 클릭합니다.

    ![진단 로그 사용](./media/service-bus-diagnostic-logs/image2.png)

4.  **상태**에서 **켜기**를 클릭합니다.

    ![진단 로그 상태 변경](./media/service-bus-diagnostic-logs/image3.png)

5.  원하는; 집합 hello 보관 대상 예를 들어 저장소 계정, 이벤트 허브 또는 Azure 로그 분석 합니다.

6.  Hello 새 진단 설정을 저장 합니다.

새 설정은 약 10분 후에 적용됩니다. 그 후 로그가 hello에 구성 된 hello 보관 대상에 나타납니다 **진단 로그** 블레이드입니다.

진단을 구성 하는 방법에 대 한 자세한 내용은 참조 hello [Azure 진단 로그의 개요](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)합니다.

## <a name="diagnostic-logs-schema"></a>진단 로그 스키마

모든 로그는 JSON(JavaScript Object Notation) 형식으로 저장됩니다. 각 항목에 hello 다음 섹션에에서 설명 된 hello 형식을 사용 하는 문자열 필드입니다.

## <a name="operational-logs-schema"></a>작업 로그 스키마

Hello 로그인 **OperationalLogs** 범주 서비스 버스 작업 중 진행 상황을 캡처합니다. 특히, 이러한 로그를 만드는 큐를 사용 하는 리소스를 포함 하 여 hello 작업 유형을 캡처하고 hello 작업의 상태를 hello 합니다.

다음 표에 hello에 나열 된 요소를 포함 하는 작업 로그 JSON 문자열:

이름 | 설명
------- | -------
ActivityId | 추적에 사용되는 내부 ID
EventName | 작업 이름           
resourceId | Azure Resource Manager 리소스 ID
SubscriptionId | 구독 ID
EventTimeString | 작업 시간
EventProperties | 작업 속성
가동 상태 | 작업 상태
Caller | 작업 호출자(Azure Portal 또는 관리 클라이언트)
카테고리 | OperationalLogs

작업 로그 JSON 문자열 예제는 다음과 같습니다.

```json
{
  "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
  "EventName": "Create Queue",
  "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.SERVICEBUS/NAMESPACES/SHOEBOXEHNS-CY4001",
  "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
  "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
  "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
  "Status": "Succeeded",
  "Caller": "ServiceBus Client",
  "category": "OperationalLogs"
}
```

## <a name="next-steps"></a>다음 단계

서비스 버스에 대 한 자세한 링크 toolearn 다음 hello 방문.

* [소개 tooService 버스](service-bus-messaging-overview.md)
* [Service Bus 시작](service-bus-dotnet-get-started-with-queues.md)

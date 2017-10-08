---
title: "서비스 상태 알림 aaaWhat | Microsoft Docs"
description: "서비스 상태 알림 Microsoft Azure에 의해 게시 하면 tooview 서비스 상태 메시지를 허용 합니다."
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
ms.openlocfilehash: 6f2fe72154c3e80d85062655c49dd1799b718e3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-health-notifications"></a>서비스 상태 알림
## <a name="overview"></a>개요

이 문서에서는 tooview 서비스 상태 알림 사용 하 여 Azure 포털을 hello 하는 방법을 설명 합니다.

서비스 상태 알림 메시지를 허용 하면 tooview 서비스 상태 hello 구독 아래에 있는 hello 리소스를 미칠 수 있는 Azure 팀에서 게시 합니다. 이러한 알림 작업의 하위 클래스에는 로그 이벤트 및 hello 활동 로그 블레이드를 찾을 수도 있습니다. 서비스 상태 알림 정보 또는 hello 클래스에 따라 조치 가능한 가능 합니다.

5가지의 서비스 상태 알림 클래스가 있습니다.  

- **작업 필요:** 시간 tootime에서 특이 한 활동이 계정에서 발생할 표시 될 수도 있습니다. 수 있습니다이 항목이 필요한 toowork와 tooremedy 있습니다. 보내 드립니다 알림을 하거나 hello 동작에 자세히 설명 해야 tootake 또는 toocontact Azure 엔지니어링 하는 방법에 대 한 지원 하거나 지원 합니다.  
- **복구 지원:** 이벤트가 발생했으며 엔지니어가 여전히 영향이 있음을 확인했습니다. 엔지니어링 팀에 사용자와 toowork 필요 합니다 직접 toobring 서비스 toorestoration 합니다.  
- **인시던트:** hello 구독의 리소스에에서 하나 이상의 이벤트에 영향을 주지는 서비스는 현재 영향을 합니다.  
- **유지 관리:** 이 알리는 hello 구독 아래에 있는 리소스 중 하나 이상을 영향을 줄 수 있는 계획 된 유지 관리 작업의 알림입니다.  
- **정보:** 시간 tootime에서 म 수 ध ा ड 알림을 도움이 될 수 있는 잠재적인 최적화에 대 한 통신 tooyou 리소스 사용률을 향상 합니다.  
- **보안:** Azure에서 실행 중인 솔루션에 대한 긴급한 보안 관련 정보입니다.

각 서비스 상태 알림 hello 범위 및 영향 tooyour 리소스에 세부 정보를 전달 됩니다. 세부 정보에는 다음이 포함됩니다.

속성 이름 | 설명
-------- | -----------
channels | Hello 다음 값 중 하나: "Admin", "작업이"
CorrelationId | 일반적으로 hello 문자열 형식의 GUID입니다. 같은 uber 작업 대개 공유 toohello 속하는 이벤트는 같은 correlationId hello 합니다.
eventDataId | hello 이벤트의 고유 식별자
eventName | Hello 이벤트의 hello 제목
level | Hello 이벤트의 수준입니다. Hello 다음 값 중 하나: "Critical", "Error", "Warning", "Informational" 및 "Verbose"
resourceProviderName | 리소스의 영향을 hello에 대 한 hello 리소스 공급자의 이름
resourceType| hello hello의 리소스 유형의 리소스 영향을 받음
subStatus | Hello hello 해당 REST 호출의 HTTP 상태 코드는 일반적으로 있지만 이러한 공통 값과 같은 하위 상태를 설명 하는 다른 문자열을 포함할 수도 있습니다: 확인 (HTTP 상태 코드: 200) 작성 (HTTP 상태 코드: 201) 허용 되는, (HTTP 상태 코드: 202), 아니요 콘텐츠 (HTTP 상태 코드: 204), 잘못 된 요청 (HTTP 상태 코드: 400), 찾을 수 없음 (HTTP 상태 코드: 404), 충돌 (HTTP 상태 코드: 409), 내부 서버 오류 (HTTP 상태 코드: 500), 서비스 사용할 수 없음 (HTTP 상태 코드: 503), 게이트웨이 시간 초과 (HTTP 상태 코드: 504).
eventTimestamp | Hello Azure 서비스 처리 hello에서 hello 이벤트가 생성 된 시점의 타임 스탬프는 해당 하는 hello 이벤트를 요청 합니다.
submissionTimestamp |   Hello 이벤트를 쿼리 하기 위해 사용할 수 있게 하는 경우 타임 스탬프입니다.
subscriptionId | 이 이벤트가 기록 되는 Azure 구독 hello
status | Hello 연산의 hello 상태를 설명 하는 문자열입니다. 일반적인 값: Started, In Progress, Succeeded, Failed, Active, Resolved.
operationName | Hello 작업의 이름입니다.
카테고리 | "ServiceHealth"
resourceId | Hello의 리소스 id 리소스를 저하 됩니다.
Properties.title | 이 통신에 대 한 hello 지역화 된 제목입니다. 영어는 hello 기본 언어입니다.
Properties.communication | hello는 hello 통신할 때 HTML 태그의 세부 정보를 지역화 합니다. 영어는 hello 기본값입니다.
Properties.incidentType | 가능한 값: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security
Properties.trackingId | 이 이벤트와 연결 된 hello 인시던트를 식별 합니다. 이 toocorrelate hello 이벤트 관련된 tooan 인시던트에 사용 합니다.
Properties.impactedServices | Hello 서비스 및 hello 인시던트의 영향을 미치는 영역을 설명 하는 이스케이프 된 JSON blob입니다. 각각 ServiceName과 ImpactedRegions 목록을 포함하는 서비스 목록으로, 각 ImpactedRegions에는 RegionName이 포함됩니다.
Properties.defaultLanguageTitle | 영어로 hello 통신
Properties.defaultLanguageContent | html 태그 또는 일반 텍스트 영어로 hello 통신
Properties.stage | AssistedRecovery, ActionRequired, Information, Incident, Security에 대해 가능한 값: Active, Resolved. Maintenance에 대해 가능한 값: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete
Properties.communicationId | 이 이벤트는 연결 된 hello 통신 합니다.


## <a name="viewing-your-service-health-notifications-in-hello-azure-portal"></a>Hello Azure 포털에서에서 서비스 상태 알림 보기
1.  Hello에 [포털](https://portal.azure.com), toohello 이동 **모니터** 서비스

    ![모니터](./media/monitoring-service-notifications/home-monitor.png)
2.  Hello 클릭 **모니터** hello 모니터 블레이드를 tooopen 옵션입니다. 이 블레이드에서는 모든 모니터링 설정과 데이터를 하나의 통합 보기로 모읍니다. Toohello를 처음 열면 **활동 로그** 섹션.

3.  이제 **서비스 알림** 섹션을 클릭합니다.

    ![모니터](./media/monitoring-service-notifications/service-health-summary.png)
4.  Hello 품목 tooview 중 하나에서 자세한 내용을 보려면 클릭

5. Hello 클릭 **+ 활동 로그 경고 추가** 작업 tooreceive 알림 tooensure 이러한 종류의 향후 서비스 알림에 대 한 알림이 표시 됩니다. 서비스 알림 경고를 구성 하는 방법에 자세한 toolearn [여기를 클릭](monitoring-activity-log-alerts-on-service-notifications.md)

## <a name="next-steps"></a>다음 단계:
[서비스 상태 알림이 게시될 때마다 경고 알림](monitoring-activity-log-alerts-on-service-notifications.md)을 수신합니다.  
[활동 로그 경고에 대한 자세한 내용](monitoring-activity-log-alerts.md)

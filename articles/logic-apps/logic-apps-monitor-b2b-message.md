---
title: "aaaMonitor B2B 트랜잭션 로깅-Azure 논리 앱을 설정 하 고 | Microsoft Docs"
description: "AS2, X12 및 EDIFACT 메시지 모니터링, 통합 계정에 대한 진단 로깅 시작"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: a6745ebf41aab331020bfec072f5806711d125bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a>통합 계정에서 B2B 통신에 대한 진단 로깅 모니터링 및 설정

통합 계정을 통해 실행 중인 두 비즈니스 프로세스 또는 응용 프로그램 간의 B2B 통신을 설정한 후 해당 엔터티는 서로 메시지를 교환할 수 있습니다. tooconfirm이이 통신 예상 대로 작동 하는지, AS2, X12에 대 한 모니터링을 설정할 수 그리고 hello 통해 통합 계정에 대 한 진단 로깅을 함께 EDIFACT 메시지 [Azure 로그 분석](../log-analytics/log-analytics-overview.md) 서비스입니다. [OMS(Operations Management Suite)](../operations-management-suite/operations-management-suite-overview.md)의 이 서비스는 해당 가용성 및 성능을 유지할 수 있도록 클라우드 및 온-프레미스 환경을 모니터링하고 런타임 세부 정보 및 보다 풍부한 디버깅에 대한 이벤트를 수집합니다. 또한 Azure Storage 및 Azure Event Hub와 같은 [다른 서비스와 함께 진단 데이터를 사용](#extend-diagnostic-data)할 수도 있습니다.

## <a name="requirements"></a>요구 사항

* 진단 로깅과 함께 설정된 논리 앱. 자세한 내용은 [어떻게 해당 논리 앱에 대 한 로깅을 tooset](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics)합니다.

  > [!NOTE]
  > 이 요구 사항은 충족, 수 있게 hello에 대 한 작업 영역 [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md)합니다. 사용 해야 통합 계정에 대 한 로깅을 설정 하는 경우 동일한 OMS 작업 영역을 hello 합니다. OMS 작업 영역에 없을 경우에 대해 배울 [어떻게 toocreate OMS 작업 영역](../log-analytics/log-analytics-get-started.md)합니다.

* 통합 계정 tooyour 논리 앱 연결 된입니다. 자세한 내용은 [toocreate 통합 링크 tooyour 논리 앱 계정을 어떻게](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md)합니다.

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a>통합 계정에 대한 진단 로깅 켜기

통합 계정에서 직접 로깅을 설정할 수 있습니다 또는 [hello Azure 모니터 서비스를 통해](#azure-monitor-service)합니다. Azure Monitor는 인프라 수준의 데이터와 함께 기본 모니터링을 제공합니다. [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md)에 대해 자세히 알아봅니다.

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a>통합 계정에서 직접 진단 로깅 켜기

1. Hello에 [Azure 포털](https://portal.azure.com)찾아 통합 계정을 선택 합니다. **모니터링** 아래에서 다음과 같이 **진단 로그**를 선택합니다.

   ![통합 계정을 찾고 선택하고 "진단 로그"를 선택합니다.](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. 통합 계정을 선택한 후 다음 값에는 hello 자동으로 선택 됩니다. 이러한 값이 올바르면 **진단 켜기**를 선택합니다. 그렇지 않으면 hello 원하는 값을 선택 합니다.

   1. 아래 **구독**, 선택 hello 통합 계정에 사용할 Azure 구독.
   2. 아래 **리소스 그룹**선택, 통합 계정으로 사용 하는 hello 리소스 그룹입니다.
   3. **리소스 종류** 아래에서 **통합 계정**을 선택합니다. 
   4. **리소스** 아래에서 통합 계정을 선택합니다. 
   5. **진단 켜기**를 선택합니다.

   ![통합 계정에 대한 진단 설정](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. **진단 설정**, **상태** 아래에서 **켜기**를 선택합니다.

   ![Azure 진단 켜기](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. 표시 된 것 처럼 이제 로깅에 대 한 hello OMS 작업 영역 및 데이터 toouse를 선택 합니다.

   1. 선택 **tooLog 분석 보내기**합니다. 
   2. **Log Analytics** 아래에서 **구성**을 선택합니다. 
   3. 아래 **OMS 작업 영역**를 로깅에 대 한 OMS 작업 영역 toouse hello를 선택 합니다.
   4. 아래 **로그**선택, hello **IntegrationAccountTrackingEvents** 범주입니다.
   5. **저장**을 선택합니다.

   ![진단 데이터 tooa 로그를 보낼 수 있도록 로그 분석 설정](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. 이제 [OMS에서 B2B 메시지에 대한 추적을 설정](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)합니다.

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a>Azure Monitor를 통해 진단 로깅 켜기

1. Hello에 [Azure 포털](https://portal.azure.com), 주요 Azure 메뉴 hello, 선택 **모니터**, **진단 로그**합니다. 그런 다음 다음과 같이 통합 계정을 선택합니다.

   !["모니터링", "진단 로그"를 선택하고 통합 계정을 선택합니다.](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. 통합 계정을 선택한 후 다음 값에는 hello 자동으로 선택 됩니다. 이러한 값이 올바르면 **진단 켜기**를 선택합니다. 그렇지 않으면 hello 원하는 값을 선택 합니다.

   1. 아래 **구독**, 선택 hello 통합 계정에 사용할 Azure 구독.
   2. 아래 **리소스 그룹**선택, 통합 계정으로 사용 하는 hello 리소스 그룹입니다.
   3. **리소스 종류** 아래에서 **통합 계정**을 선택합니다.
   4. **리소스** 아래에서 통합 계정을 선택합니다.
   5. **진단 켜기**를 선택합니다.

   ![통합 계정에 대한 진단 설정](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. **진단 설정** 아래에서 **켜기**를 선택합니다.

   ![Azure 진단 켜기](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. 표시 된 것 처럼 이제 로깅에 대 한 hello OMS 작업 영역 및 이벤트 범주를 선택 합니다.

   1. 선택 **tooLog 분석 보내기**합니다. 
   2. **Log Analytics** 아래에서 **구성**을 선택합니다. 
   3. 아래 **OMS 작업 영역**를 로깅에 대 한 OMS 작업 영역 toouse hello를 선택 합니다.
   4. 아래 **로그**선택, hello **IntegrationAccountTrackingEvents** 범주입니다.
   5. 완료하면 **저장**을 선택합니다.

   ![진단 데이터 tooa 로그를 보낼 수 있도록 로그 분석 설정](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. 이제 [OMS에서 B2B 메시지에 대한 추적을 설정](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)합니다.

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a>다른 서비스와 함께 진단 데이터를 사용하는 방법 및 위치 확장

Azure Log Analytics와 마찬가지로 다른 Azure 서비스와 함께 논리 앱의 진단 데이터를 사용하는 방법을 다음과 같이 확장할 수 있습니다. 

* [Azure Storage에 Azure 진단 로그 보관](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [Azure 진단 로그 tooAzure 스트림 이벤트 허브](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

그런 다음 [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) 및 [Power BI](../log-analytics/log-analytics-powerbi.md)와 같은 다른 서비스의 원격 분석 및 분석을 사용하여 실시간으로 모니터링할 수 있습니다. 예:

* [이벤트 허브 tooStream 분석에서에서 스트림 데이터](../stream-analytics/stream-analytics-define-inputs.md)
* [Stream Analytics를 사용하여 스트리밍 데이터 분석 및 Power BI에서 실시간 분석 대시보드 만들기](../stream-analytics/stream-analytics-power-bi-dashboard.md)

Hello 원하는 옵션을 설정에 따라, 다음 사항을 확인 하면 첫 번째 [Azure 저장소 계정 만들기](../storage/common/storage-create-storage-account.md) 또는 [Azure 이벤트 허브 만들기](../event-hubs/event-hubs-create.md)합니다. Toosend 진단 데이터에 대 한 hello 옵션을 선택 합니다.

![데이터는 저장소 계정 또는 이벤트 허브를 tooAzure 보내기](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> 보존 기간 toouse 저장소 계정을 선택 하는 경우에 적용 됩니다.

## <a name="supported-tracking-schemas"></a>지원되는 추적 스키마

Azure는 사용자 지정 유형을 hello 점을 제외 하 고 스키마를 해결 했습니다. 스키마 형식 추적을 지원 합니다.

* [AS2 추적 스키마](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [X12 추적 스키마](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [사용자 지정 추적 스키마](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a>다음 단계

* [OMS에서 B2B 메시지 추적](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "OMS에서 B2B 메시지 추적")
* [엔터프라이즈 통합 팩 hello에 대 한 자세한](../logic-apps/logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보")

